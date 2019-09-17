---
title: 教程：为 Internet 设备启用共同管理
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 和 Microsoft Intune 为基于 Internet 的新 Windows 10 设备配置共同管理。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/26/2019
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7fb02a5c-e286-46b1-a972-6335c858429a
ms.openlocfilehash: 6215842691aece6eb13bc1969640e4d9c19d9fae
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70890778"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>教程：为基于 Internet 的新设备启用共同管理

通过共同管理，可以保持完善的流程，以便使用 Configuration Manager 管理组织中的电脑。 同时，通过使用 Intune 在云上投入，实现安全性和新式预配。

在本教程中，你将在使用 Azure Active Directory (AD) 和本地 AD，但不使用[混合 Azure Active Directory](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (AD) 的环境中设置 Windows 10 设备的共同管理。 Configuration Manager 环境包括一个主站点，其中所有站点系统角色都位于同一服务器（站点服务器）上。 学习本教程的前提是你的 Windows 10 设备已在 Intune 中注册。 

如果具有联接本地 AD 与 Azure AD 的混合 Azure AD，建议学习我们的配套教程：[为 Configuration Manager 客户端启用共同管理](/sccm/comanage/tutorial-co-manage-clients)。

若要使用本教程，需要具备以下条件：
  
- 拥有要引入共同管理的 Windows 10 设备。 这些设备可能已通过 Windows Autopilot 进行预配，也可能直接来自你的硬件 OEM。
- Windows 10 设备处于以下状态：已连接到 Internet，目前通过 Intune 管理，并且要向该设备添加 Configuration Manager 客户端。

**在本教程中，你将：**  
> [!div class="checklist"]  
> * 检查 Azure 和本地环境的先决条件
> * 请求云管理网关 (CMG) 的公用 SSL 证书
> * 在 Configuration Manager 中启用 Azure 服务
> * 部署和配置云管理网关  
> * 配置管理点和客户端以使用 CMG
> * 在 Configuration Manager 中启用共同管理
> * 配置 Intune 以安装 Configuration Manager 客户端
> * 为云服务分配许可证

## <a name="prerequisites"></a>先决条件  

### <a name="azure-services-and-environment"></a>Azure 服务和环境

- Azure 订阅（[免费试用版](https://azure.microsoft.com/free)）
- Azure Active Directory Premium
- Microsoft Intune 订阅
  > [!TIP]  
  > 企业移动和安全性 (EMS) 订阅包括 Azure Active Directory Premium 和 Microsoft Intune。 EMS 订阅（[免费试用版](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)）。  

- 必须为用户分配 Intune 和 Azure Active Directory Premium [许可证](tutorial-co-manage-clients.md#assign-intune-licenses-to-users)  
- 将 Intune 配置为[自动注册设备](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune)  

### <a name="on-premises-infrastructure"></a>本地基础结构

- System Center Configuration Manager Current Branch 1810 版或更高版本。
  
  1810 版引入了[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)，本教程中使用增强型 HTTP 来避免更复杂的 PKI 需求。 通过使用增强型 HTTP，必须将用于管理客户端的主站点配置为使用 Configuration Manager 为 HTTP 站点系统生成的证书。  

  1810 版还为基于 Internet 的 Configuration Manager 客户端安装引入了一个更简单的命令行。

- 必须将 [MDM 机构](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority)设置为 Intune  

### <a name="external-certificates"></a>外部证书

- CMG 服务器身份验证证书。 此证书是全局受信任的公共证书提供程序提供的 SSL 证书。 例如（但不限于）DigiCert、Thawte 或 VeriSign。 将此证书导出为包含私钥的 .PFX 文件。  

- 在本教程后面的部分中，我们提供了有关如何配置此证书请求的指导。

### <a name="permissions"></a>权限

在本教程中，请使用以下权限来完成各项任务：

- Azure 中的全局管理员帐户 
- 本地基础结构上的域管理员帐户   
- Configuration Manager 中所有范围的完全权限管理员帐户  

## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>请求云管理网关的公共证书

如果设备已连接到 Internet，那么共同管理需要使用 Configuration Manager 云管理网关 (CMG)。 CMG 使基于 Internet 的 Windows 10 设备能够与本地 Configuration Manager 部署进行通信。 若要在设备和 Configuration Manager 环境之间建立信任，CMG 需要 SSL 证书。

本教程使用名为“CMG 服务器身份验证证书”的公共证书，该证书从全局受信任的证书提供程序派生机构  。 虽然可以使用从本地 Microsoft 证书颁发机构派生机构的证书来配置共同管理，但使用自签名证书的内容超出了本教程的范围。

CMG 服务器身份验证证书用于加密 Configuration Manager 客户端与 CMG 之间的通信流量  。 证书将追溯到受信任的根，向客户端验证服务器的身份。 公共证书包括 Windows 客户端已信任的受信任的根。

关于此证书： 

- 在 Azure 中为 CMG 服务标识唯一名称，然后在证书请求中指定该名称。  
- 在特定服务器上生成证书请求，然后将请求提交给公共证书提供程序以获取必要的 SSL 证书。  
- 将从提供程序返回的证书导入生成了请求的系统。 使用同一台计算机导出证书，以便以后在将 CMG 部署到 Azure 时使用。  
- 安装 CMG 时，它使用你在证书中指定的名称在 Azure 中创建 CMG 服务。  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>在 Azure 中为云管理网关标识唯一名称

在请求 CMG 服务器身份验证证书时，指定哪些项必须为唯一名称才能在 Azure 中标识“云服务(经典)”  。 默认情况下，Azure 公有云使用 cloudapp.net，CMG 作为 \<YourUniqueDnsName>.cloudapp.net 托管在 cloudapp.net 域中   。  

> [!TIP]  
> 在本教程中，CMG 服务器身份验证证书使用以 contoso.com 结尾的 FQDN   。  创建 CMG 之后，我们将在组织的公用 DNS 中配置规范名称记录 (CNAME)。 该记录会创建 CMG 的别名，该别名会映射到公共证书中使用的名称。  

在请求公共证书之前，请确认要使用的名称在 Azure 中可用。 不直接在 Azure 中创建服务。 相反，在安装 CMG 时，Configuration Manager 使用你请求的公共证书中指定的名称来创建云服务。  

1. 登录 [Microsoft Azure 门户](https://portal.azure.com/)。  

2. 依次选择“创建资源”、“计算”类别，以及“云服务”    。 随即打开“云服务(经典)”页。

3. 对于“DNS 名称”，请指定将要使用的云服务的前缀名称  。 此前缀必须与稍后在请求 CMG 服务器身份验证证书的发布证书时使用的前缀相同。 我们使用 MyCSG，它可以创建 MyCSG.cloudapp.net 的命名空间   。 界面将确认名称是否可用，或是否已由其他服务使用。  
 确认要使用的名称可用后，就可以提交证书签名请求 (CSR) 了。

### <a name="request-the-certificate"></a>请求证书

使用以下信息向公共证书提供程序提交 CMG 证书签名请求。 将以下值更改为与环境相关的值。  

- MyCMG：用于标识云管理网关的服务名称 
- Contoso：用作公司名称 
- Contoso.com：用作公共域 

建议使用主站点服务器生成证书签名请求 (CSR)。 获取证书时，必须将其注册到生成了 CSR 的同一服务器上，否则将无法导出证书私钥（这是必需的）。  

生成 CSR 时请求版本 2 密钥提供程序类型。 仅支持版本 2 证书。  

> [!TIP]  
> 在部署 CMG 时，还会同时安装云分发点 (CDP)。 默认情况下，在部署 CMG 时，会选中“允许 CMG 充当云分发点并提供 Azure 存储中的内容”选项  。 通过 CMG 在服务器上并置 CDP，无需单独的证书和配置来支持 CDP。 尽管 CDP 不需要使用共同管理，但它在大多数环境中都很有用。  
>
> 如果要使用其他云分发点进行共同管理，需要为每个其他服务器请求单独的证书。 若要为 CDP 请求公共证书，请使用与云管理网关 CSR 相同的详细信息。 只需更改公用名，使其对每个 CDP 都是唯一的。  

#### <a name="details-for-the-cloud-management-gateway-csr"></a>云管理网关 CSR 的详细信息

- **公用名**：ClousServiceNameCMG.YourCompanyPubilcDomainName.com  
例如：MyCSG.contoso.com  
- **使用者可选名称**：与公用名 (CN) 相同  
- **组织**：组织的名称  
- **部门**：根据组织而定  
- **城市**：根据组织而定  
- **状态**：根据组织而定  
- **国家/地区**：根据组织而定  
- **密钥大小：2048**  
- **提供程序：Microsoft RSA SChannel 加密提供程序**  

### <a name="import-the-certificate"></a>导入证书

收到公共证书后，将其导入到创建了 CSR 的计算机的本地证书存储中。 然后将证书导出为 .PFX 文件，以便在 Azure 中将其用于 CMG。  

公共证书提供程序通常提供导入证书的说明。 导入证书的过程应类似于以下指导步骤：  

1. 在要导入证书的计算机上，找到证书 .pfx 文件。  

2. 右键单击“文件”，然后选择“安装 PFX”   

3. “证书导入向导”启动时，选择“下一步”  。  

4. 在“要导入的文件”页上，选择“下一步”   。

5. 在“密码”页上的“密码”框中输入私钥的密码，然后选择“下一步”   。  
  
   选择可导出密钥的选项。

6. 在“证书存储”页上，选择“根据证书类型自动选择证书存储”，然后选择“下一步”    。  

7. 选择“完成”  。

### <a name="export-the-certificate"></a>导出证书

从服务器导出 CMG 服务器身份验证证书  。 重新导出证书后，证书就可在 Azure 中用于云管理网关了。  

1. 在导入了公用 SSL 证书的服务器上，运行 certlm.msc 以打开“证书管理员”控制台  。  

2. 在“证书管理员”控制台上，选择“个人”>“证书”  。 然后，右键单击在上一过程中注册的 CMG 服务器身份验证证书，然后选择“所有任务”>“导出”   。  

3. 在“证书导出向导”中，依次选择“下一步”、“是，导出私钥”，然后单击“下一步”    。  

4. 在“导出文件格式”页上，选择“个人信息交换 - PKCS #12 (.PFX)”，选择“下一步”，然后提供密码   。 对于文件名，请指定类似于 C:\ConfigMgrCloudMGServer 的名称  。 在 Azure 中创建 CMG 时，将引用此文件。  

5. 选择“下一步”，先确认以下设置，然后再选择“完成”以完成导出   ：  

   - 导出密钥 = 是  
   - 包括证书路径中的所有证书 = 是  
   - 文件格式 = 个人信息交换(*.pfx)  

6. 完成导出后，找到 .pfx 文件并将其副本放在将管理基于 Internet 的客户端的 Configuration Manager 主站点服务器上的 C:\Certs 中  。 Certs 文件夹是在服务器之间移动证书时使用的临时文件夹。 将云管理网关部署到 Azure 时，可以从主站点服务器访问证书文件。  

将证书复制到主站点服务器后，可以从成员服务器上的“个人证书”存储中删除该证书。

## <a name="enable-azure-cloud-services-in-configuration-manager"></a>在 Configuration Manager 中启用 Azure 云服务

若要在 Configuration Manager 控制台中配置 Azure 服务，请使用“配置 Azure 服务”向导并创建两个 Azure Active Directory (Azure AD) 应用。  

- **服务器应用**：Azure AD 中的 Web 应用   
- **客户端应用**：Azure AD 中的本机客户端应用   

从主站点服务器运行以下过程。  

1. 在主站点服务器上，打开 Configuration Manager 控制台，转到“管理”>“云服务”>“Azure 服务”，然后选择“配置 Azure 服务”   。  

   在“配置 Azure 服务”页上，为要配置的云管理服务指定友好名称。 例如：*我的云管理服务*。

   选择“云管理”，然后选择“下一步”   。  

   > [!TIP]  
   > 有关向导中的配置的详细信息，请参阅[启动 Azure 服务向导](https://docs.microsoft.com/sccm/core/servers/deploy/configure/Azure-services-wizard#start-the-azure-services-wizard)

2. 在“应用属性”页上，对于“Web 应用”，选择“浏览”以打开“服务器应用”对话框，然后选择“创建”      。 配置以下字段：

   - **应用程序名称**：为应用指定友好名称，如“云管理 Web 应用”  。  

   - **主页 URL**：Configuration Manager 不使用此值，但是 Azure AD 需要它。 默认情况下，此值为 `https://ConfigMgrService`。  

   - **应用 ID URI**：此值在 Azure AD 租户中必须是唯一的。 它在 Configuration Manager 客户端用于请求访问服务的访问令牌中。 默认情况下，此值为 `https://ConfigMgrService`。  

   接下来，选择“登录”，然后指定 Azure 全局管理员帐户  。 Configuration Manager 不保存这些凭据。 此角色不需要 Configuration Manager 中的权限，其帐户也不需要与运行 Azure 服务向导的帐户相同。

   登录后，将显示结果。 选择“确定”以关闭“创建服务器应用程序”对话框并返回“应用属性”页  。

3. 对于“本机客户端应用”，选择“浏览”以打开“客户端应用”对话框    。

4. 选择“创建”以打开“创建客户端应用程序”对话框，然后配置以下字段   ：  

   - **应用程序名称**：为应用指定友好名称，如“云管理本机客户端应用”  。

   - **回复 URL**：Configuration Manager 不使用此值，但是 Azure AD 需要它。 默认情况下，此值为 `https://ConfigMgrClient`。
   接下来，选择“登录”，然后指定 Azure 全局管理员帐户  。 与 Web 应用一样，这些凭据不会保存，也不需要 Configuration Manager 中的权限。

   登录后，将显示结果。 选择“确定”以关闭“创建客户端应用程序”对话框并返回“应用属性”页  。 然后，选择“下一步”继续操作  。

5. 在“配置发现设置”页上，选中“启用 Azure Active Directory 用户发现”复选框，选择“下一步”，然后为环境完成“发现”对话框的配置    。  

6. 继续完成“摘要”、“进度”和“完成”页，然后关闭向导。  

   现在，Configuration Manager 中已启用 Azure AD 用户发现的 Azure 服务。  暂时让控制台保持打开状态。  

7. 打开浏览器并登录到 [Azure 门户](https://portal.azure.com/)。  

8. 选择“所有服务”>“Azure Active Directory”>“应用注册”，然后  ：

   1. 选择所创建的 Web 应用。

   2. 转到“设置”>“所需权限”，选择“授予权限”，然后选择“是”    。  

   3. 选择所创建的本机客户端应用。

   4. 转到“设置”>“所需权限”，选择“授予权限”，然后选择“是”    。  

9. 在 Configuration Manager 控制台中，转到“管理”>“概述”>“云服务”>“Azure服务”，然后选择你的 Azure 服务  。 然后右键单击“Azure Active Directory 用户发现”，并选择“立即运行完整发现”   。 选择“是”  以确认操作。  

10. 在主站点服务器上，打开配置管理器 SMS_AZUREAD_DISCOVERY_AGENT.log 并查找以下条目以确认该发现正常工作：  “已成功为 Azure Active Directory 用户发布 UDX”   

    默认情况下，日志文件位于 %Program_Files%\Microsoft Configuration Manager\Logs  中。  

## <a name="create-the-cloud-services-in-azure"></a>在 Azure 中创建云服务

**在本教程的这一部分中，你将：**

- 创建 CMG 云服务  
- 为两种服务创建 DNS CNAME 记录  

### <a name="create-the-cmg"></a>创建 CMG

使用此过程在 Azure 中安装云管理网关作为服务。 CMG 安装在层次结构的顶层站点中。 本教程将继续使用已注册和导出证书的主站点。

1. 在主站点服务器上，打开 Configuration Manager 控制台，转到“管理”>“概述”>”云服务”>”云管理网关”，然后选择“创建云管理网关”   。  

2. 在“常规”页上  ：  

   1. 对于”Azure 环境”，选择你的云环境  。 本教程使用 AzurePublicCloud  。  

   2. 选择“Azure 资源管理器部署”  。  
  
   3. 登录到你的 Azure 订阅  。 Configuration Manager 根据你为 Configuration Manager 启用 Azure 云服务时配置的信息填写其他信息。  

   选择“下一步”继续操作  。  

3. 在“设置”页上，浏览到名为“ConfigMgrCloudMGServer.pfx”的文件并选中它，该文件是在导入 CMG 服务器身份验证证书后导出的那个文件   。 指定密码后，将根据 .pfx 证书文件中的详细信息自动填写“服务名称”和“部署名称”   。

4. 设置你的“区域”  。

5. 对于“资源组”，请使用现有资源组或创建一个具有友好名称（不使用空格）的组，如 CofigMgrCloudServices   。 如果选择创建组，该组将作为资源组添加到 Azure 中。  

6. 除非你已准备好进行大规模配置，否则请将“VM 实例”的数量设置为一 (1)  。 通过设置 VM 实例的数量，可将单个云管理网关 (CMG) 云服务横向扩展以支持更多客户端连接。 稍后，可以使用 Configuration Manager 控制台返回所使用的 VM 实例数并对其进行编辑。  

7. 启用“验证客户端证书吊销”复选框  。

8. 如果要部署 CMG 云分发点，请启用“允许 CMG 充当云分发点并提供 Azure 存储中的内容”复选框  。

9. 选择“下一步”继续操作  。

10. 查看“警报”页上的值，然后选择“下一步”   。

11. 查看“摘要”页，然后单击“下一步”以创建云管理网关云服务   。 选择“关闭”  ，完成向导。  

12. 现在，可以在 Configuration Manager 控制台的“云管理网关”节点中查看新服务。  

### <a name="create-dns-cname-records"></a>创建 DNS CNAME 记录

为 CMG 创建 DNS 条目时，可以使企业网络内外的 Windows 10 设备使用名称解析来查找 Azure 中的 CMG 云服务。

我们的 CNAME 记录示例使用以下详细信息：  

- 公司名称为 Contoso，其公共 DNS 命名空间为 Contoso.com  。  

- CMG 服务名称为 MyCMG，它在 Azure 中的名称变为 MyCMG.CloudApp.Net  。  

CNAME 记录示例：MyCMG.contoso.com => My.cloudapp.net 

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>配置管理点和客户端以使用 CMG

配置允许本地管理点和客户端使用云管理网关的设置。

由于我们使用增强型 HTTP 进行客户端通信，因此，不需要使用 HTTPS 管理点。  

### <a name="create-the-cmg-connection-point"></a>创建 CMG 连接点

配置站点以支持增强型 HTTP。  

1. 在 Configuration Manager 控制台中，转到“管理”>“概述”>“站点配置”>“站点”，然后打开主站点的属性  。  

2. 在“客户端计算机通信”选项卡上，为“将 Configuration Manager 生成的证书用于 HTTP 站点系统”选择“HTTPS”或“HTTP”选项，然后选择“确定”以保存配置     。

    > [!Note]
    > 从版本 1906 开始，此选项卡称为“通信安全”  。<!-- SCCMDocs#1645 -->  

3. 现在转到”管理“>”概述“>”站点配置“>”服务器和站点系统角色“，然后选择具有要安装云管理网关连接点的管理点的服务器  。  

4. 选择“添加站点系统角色”，然后选择“下一步”> “下一步”    。  

5. 选择“云管理网关连接点”，然后选择“下一步”以继续操作   。  

6. 查看“云管理网关连接点”页上的默认选择内容，并确保选择了正确的 CMG  。 如果具有多个云管理网关，可以使用下拉列表指定其他 CMG。 也可以在安装后更改正在使用的 CMG。 选择“下一步”继续操作  。

7. 选择“下一步”开始安装，然后在“完成”页上查看结果  。  选择“关闭”，完成连接点的安装  。

8. 现在转到“管理”>“概述”>“站点配置”>“服务器和站点系统角色”，并打开安装了连接点的管理点的“属性”   。 在“常规”选项卡上，选中“允许 Configuration Manager 云管理网关流量”复选框，然后选择“确定”以保存配置    。
   > [!TIP]  
   > 虽然启用共同管理不是必需的操作，但建议对所有软件更新点进行相同的编辑。

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>配置“客户端设置”以指示客户端使用 CMG

使用“客户端设置”将 Configuration Manager 客户端配置为与 CMG 通信。  

1. 打开 Configuration Manager 控制台，在“管理”>“概述”>“客户端设置”中，编辑“默认客户端设置”   。  

2. 选择“云服务”  。

3. 在“默认设置”页上，将以下设置项设置为 =“是”   。  

   - **在 Azure Active Directory 中自动注册已加入域的新 Windows 10 设备**  

   - **允许客户端使用云管理网关**

   - **允许访问云分发点**

4. 在“客户端策略”页上，将“从 Internet 客户端启用用户策略请求”设置为  = “是”    。

5. 选择“确定”以保存此配置  。

## <a name="enable-co-management-in-configuration-manager"></a>在 Configuration Manager 中启用共同管理

Azure 配置、站点系统角色和客户端设置配置就绪后，可以配置 Configuration Manager 以启用共同管理。 不过，启用共同管理后，仍需要在 Intune 中进行一些配置才能完成本教程。 其中一项任务是配置 Intune 以部署 Configuration Manager 客户端。 通过保存“共同管理配置向导”中可用的客户端部署命令行，可以更轻松地完成该任务。 这就是我们在完成 Intune 配置之前启用共同管理的原因。

> [!TIP]
> - 启用共同管理后，会分配集合作为试点组  。 此组包含少量客户端，用于测试共同管理配置。 建议在开始此过程前先创建合适的集合。 然后，可以选择此集合，而无需退出该过程来执行此操作。
> - 从 Configuration Manager 版本 1906 开始，可能需要多个集合，因为可以为每个工作负载分配不同的试点组  。

### <a name="enable-co-management-starting-in-version-1906"></a>从版本 1906 开始启用共同管理

若要从 Configuration Manager 版本 1906 开始启用共同管理，请按照以下说明操作：

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>在版本 1902 及更早版本中启用共同管理

若要为 Configuration Manager 版本 1902 及更早版本启用共同管理，请按照以下说明操作：

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>使用 Intune 部署 Configuration Manager 客户端

可以使用 Intune 在当前仅使用 Intune 管理的 Windows 10 设备上安装 Configuration Manager 客户端。  

然后，当以前未管理的 Windows 10 设备注册到 Intune 时，它会自动安装 Configuration Manager 客户端。

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>创建 Intune 应用以安装 Configuration Manager 客户端

1. 从主站点服务器登录到 [Azure 门户](https://portal.azure.com/)并转到“Intune”>“客户端应用”>“应用”>“添加”  。

2. 对于应用类型  ：选择“业务线应用”  。

3. 选择“应用包文件”，浏览到 Configuration Manager 文件 ccmsetup.msi 的位置，然后选择“打开”>“确定”    。
例如，C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi 

4. 选择“应用信息”，然后指定以下详细信息  ：
   - **描述**：Configuration Manager 客户端  

   - **发布者**：Microsoft  

   - **命令行参数**： *\<指定 CCMSETUPCMD 命令行  。可以使用从“共同管理配置向导”的“启用”页保存的命令行* *。此命令行包含云服务的名称以及使设备能够安装 Configuration Manager 客户端软件的其他值。>*  

     命令行结构应该类似于仅使用 CCMSETUPCMD 和 SMSSiteCode 参数的以下示例：  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > 如果没有可用的命令行，可以在 Configuration Manager 控制台中查看 CoMgmtSettingsProd 的属性以获取命令行的副本  。

5. 选择“确定”>“添加”  。  应用已创建并在 Intune 控制台中可用。 一旦应用可用，就可以使用以下部分配置 Intune，以便将其分配给 Windows 10 设备。

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>分配 Intune 应用以安装 Configuration Manager 客户端

以下过程部署应用以安装在上一过程中创建的 Configuration Manager 客户端。

1. 登录到 [Azure 门户](https://portal.azure.com/)。  选择“所有服务”>“Intune”>“客户端应用”>“应用”，然后选择“ConfigMgr 客户端安装启动”，这是你为部署 Configuration Manager 客户端而创建的应用   。  

2. 选择“分配”>“添加组”  。  将“分配类型”设置为“必需”，然后使用“包含的组”和“排除的组”设置包含要参与共同管理的用户和设备的 Azure Active Directory (AD) 组     。  

3. 选择“确定”，然后选择“保存”以保存配置   。
现在，为其分配了应用的用户和设备需要该应用。 应用在设备上安装 Configuration Manager 客户端后，通过共同管理对其进行管理。

## <a name="assign-intune-licenses-to-users"></a>将 Intune 许可证分配给用户

有一个关键操作（但这个操作通常被忽略）是向使用共同管理的设备的每个用户分配 Intune 许可证。  

若要将许可证分配给用户组，请使用 Azure Active Directory。  

1. 使用管理员帐户登录到 [Azure 门户](https://portal.azure.com/)。 若要管理许可证，该帐户必须是全局管理员角色或用户帐户管理员。  

2. 选择左侧导航窗格中的“所有服务”，然后选择“Azure Active Directory”   。  

3. 在“Azure Active Directory”窗格上，选择“许可证”以打开窗格，可以在此处查看和管理租户中的所有可许可的产品   。  

4. 在“所有产品”下，选择包含 Intune 许可证的产品选项，然后选择窗格顶部的“分配”   。  

   例如，如果是要获取 Intune，可以选择“企业移动性 + 安全性 E5”  。  

5. 在“分配许可证”窗格上，单击“用户和组”打开“用户和组”    窗格。 选择要为其分配许可证的组和单个用户。  然后，单击窗格底部的“选择”  以确认所选内容。  

6. 在“分配许可证”窗格上，单击“分配选项”以显示之前选择的产品中包含的所有服务计划   。 如果选中某个产品（如 Intune），则仅显示该产品。  
   - 将“Microsoft Intune”设置为“启用”   。  
   - 为每个用户分配 Azure Active Directory Premium 许可证  。  

   分配适用的许可证后，选择“确定”  。  

7. 若要完成分配，在“分配许可证”  窗格上，单击窗格底部的“分配”  。  

8. 右上角随即出现一条通知，显示过程的状态和结果。 如果无法完成组的分配（例如，由于组中预先存在的许可证），单击该通知以查看失败的详细信息。 

## <a name="summary"></a>摘要

完成本教程的配置步骤（包括确保许可证已分配的最后一个操作）后，你的设备就可以成功进行共同管理了。

## <a name="next-steps"></a>后续步骤

- 使用[共同管理仪表板](https://docs.microsoft.com/sccm/core/clients/manage/co-management-dashboard)查看共同管理的设备的状态
- 使用 [Windows Autopilot](/sccm/comanage/quickstart-autopilot) 预配新设备
- 使用[条件访问](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access)和 Intune 符合性规则来管理用户对企业资源的访问权限
