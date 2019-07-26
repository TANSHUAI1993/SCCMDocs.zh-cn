---
title: 将客户端部署到 Windows
titleSuffix: Configuration Manager
description: 了解如何将 Configuration Manager 客户端部署到 Windows 计算机。
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b468162ce19718b6c0f6f31b961cf61378834597
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68339767"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>如何在 Configuration Manager 中将客户端部署到 Windows 计算机

适用范围：  System Center Configuration Manager (Current Branch)

本文详细介绍如何将 Configuration Manager 客户端部署到 Windows 计算机。 若要详细了解如何计划和准备客户端部署，请参阅以下文章：
- [客户端安装方法](/sccm/core/clients/deploy/plan/client-installation-methods)  
- [将客户端部署到 Windows 计算机的先决条件](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers)   
- [Configuration Manager 客户端的安全和隐私](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  
- [客户端部署的最佳方案](/sccm/core/clients/deploy/plan/best-practices-for-client-deployment)  



##  <a name="BKMK_ClientPush"></a> 客户端请求安装

可通过三种主要方式使用客户端请求：  

- 为站点配置客户端请求安装时，客户端安装会自动在站点发现的计算机上运行。 当站点的已配置边界配置为边界组时，此方法限定于这些边界。  

- 通过为特定集合或集合内的资源运行“客户端请求安装向导”来启动客户端请求安装。  

- 使用客户端请求安装向导来安装 Configuration Manager 客户端（可用于[查询](/sccm/core/servers/manage/introduction-to-queries)结果）。 只有当查询返回的项之一为“系统资源”  类的“ResourceID”  特性，安装才会成功。

如果站点服务器无法与客户端计算机联系或者无法启动安装过程，则它每小时都会自动重试安装。 服务器不断重试长达七天。  

为了帮助跟踪客户端安装过程，请在安装客户端之前安装回退状态点。 安装回退状态点后，在使用客户端请求安装方法安装客户端时，会自动将该回退状态点分配给客户端。 若要跟踪客户端安装进度，请查看客户端部署和分配报表。

客户端日志文件提供了用于疑难解答的更加详细的信息。 日志文件不需要回退状态点。 例如，站点服务器上的 CCM.log 文件记录在站点服务器连接到计算机时发生的任何问题。 客户端上的 CCMSetup.log 文件记录安装过程。  

> [!IMPORTANT]  
>  只有满足所有先决条件，客户端请求安装才会成功。 有关详细信息，请参阅[安装方法依赖项](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies)。


### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>将站点配置为对发现的计算机自动使用客户端请求

1.  在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。  

2.  选择要为其配置自动站点范围客户端请求安装的站点。  

3.  在功能区的“主页”  选项卡上，依次选择“设置”  组中的“客户端安装设置”  和“客户端请求安装”  。  

4.  在“客户端请求安装属性”窗口的“常规”选项卡上，选择“启用自动站点范围客户端请求安装”   。

5. 自版本 1806 起，如果更新站点，便会启用用于客户端请求安装的 Kerberos 检查。 “允许连接回退到 NTLM”选项已默认启用，该选项与以前的行为一致  。 如果站点无法使用 Kerberos 验证客户端，它会使用 NTLM 重试连接。 为了提高安全性，建议的配置是禁用此设置，即要求使用 Kerberos 但不回退到 NTLM。<!--1358204-->  

    > [!NOTE]  
    > 如果使用客户端请求安装来安装 Configuration Manager 客户端，站点服务器会与客户端建立远程连接。 从 1806 版开始，站点可以通过不允许在建立连接之前回退到 NTLM 来要求 Kerberos 相互身份验证。 此增强有助于保护服务器与客户端之间的通信。  
    > 
    > 环境可能首选或要求使用 Kerberos，而不是旧 NTLM 身份验证，具体视安全策略而定。 若要详细了解这些身份验证协议的安全注意事项，请参阅[用于限制 NTLM 的 Windows 安全策略设置](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations)。  
    > 
    > 要使用此功能，客户端必须位于信任的 Active Directory 林中。 Windows 中的 Kerberos 依赖 Active Directory 进行相互身份验证。  

6.  选择 Configuration Manager 应向其推送客户端软件的系统类型。 选择是否要在域控制器上安装客户端。  

7.  在“帐户”  选项卡上，指定 Configuration Manager 在连接到目标计算机时要使用的一个或多个帐户。 选择“创建”  图标，输入“用户名”  和“密码”  （不超过 38 个字符），确认密码，再选择“确定”  。 指定至少一个客户端请求安装帐户。 此帐户必须在目标计算机上拥有本地管理员权限，才能安装客户端。 如果未指定客户端请求安装帐户，则 Configuration Manager 会尝试使用站点系统计算机帐户。 使用站点系统计算机帐户时，跨域客户端请求失败。  

    > [!NOTE]  
    >  若要从辅助站点使用客户端请求，请指定用于启动客户端请求的辅助站点上的帐户。  
    >   
    >  有关客户端请求安装帐户的详细信息，请参阅下一个过程，即[使用客户端请求安装向导](#use-the-client-push-installation-wizard)。  

8.  在“安装属性”  选项卡上，指定任何必需安装属性。

     如果你已为 Configuration Manager 扩展 Active Directory 架构，站点会向 Active Directory 域服务发布指定的[客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。 当 CCMSetup 在没有安装属性的情况下运行时，它会从 Active Directory 中读取这些属性。  

    > [!NOTE]  
    >  如果在辅助站点上启用客户端请求安装，请将 **SMSSITECODE** 属性设置为其父主站点的 Configuration Manager 站点代码。 如果为 Configuration Manager 扩展了 Active Directory 架构，请将此属性设置为“自动”，以自动查找正确的站点分配  。


### <a name="use-the-client-push-installation-wizard"></a>使用“客户端请求安装向导”

1.  在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。  

2.  选择要为其配置自动站点范围客户端请求安装的站点。  

3.  在功能区的“主页”  选项卡上，依次选择“设置”  组中的“客户端安装设置”  和“客户端请求安装”  。  

4.  在“安装属性”  选项卡上，指定任何必需安装属性。  

    如果你已为 Configuration Manager 扩展 Active Directory 架构，站点会向 Active Directory 域服务发布指定的[客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。 当 CCMSetup 在没有安装属性的情况下运行时，它会从 Active Directory 中读取这些属性。

5.  在 Configuration Manager 控制台中，转到“资产和符合性”  工作区。  

6.  在“设备”节点中，选择一台或多台计算机  。 或者在“设备集合”节点中选择一个计算机集合  。  

7.  在功能区的“主页”  选项卡上，选择以下选项之一：  

    -   若要将客户端推送到一个或多个设备，请选择“设备”  组中的“安装客户端”  。  

    -   若要将客户端推送到设备集合，请选择“集合”  组中的“安装客户端”  。  

8. 在“安装 Configuration Manager 客户端向导”的“开始前”  页上，先审阅信息，再选择“下一步”  。  

9. 选择“安装选项”  页上的相应选项。  

10. 查看安装设置，然后完成向导。  

> [!NOTE]  
> 即使站点没有配置客户端请求，也可以使用此向导来安装客户端。  

##  <a name="BKMK_ClientSUP"></a> 基于软件更新的安装  

基于软件更新的客户端安装将客户端作为软件更新发布到软件更新点。 首次安装或升级时使用此方法。  

如果计算机上安装了 Configuration Manager 客户端，计算机会从站点接收客户端策略。 此策略包括软件更新点的服务器名称，以及从中获取软件更新的端口。

> [!IMPORTANT]  
>  使用基于软件更新的安装时，应对客户端安装和软件更新使用相同的 Windows Server Update Services (WSUS) 服务器。 此服务器必须是主站点中的活动软件更新点。 有关详细信息，请参阅[安装软件更新点](/sccm/sum/get-started/install-a-software-update-point)。

如果计算机上未安装 Configuration Manager 客户端，请配置并分配组策略对象。 此组策略用于指定软件更新点的服务器名称。  

不能将命令行属性添加到基于软件更新的客户端安装中。 如果你已为 Configuration Manager 扩展 Active Directory 架构，客户端安装会自动在 Active Directory 域服务中查询安装属性。  

如果尚未扩展 Active Directory 架构，请使用组策略来预配客户端安装设置。 这些设置会自动应用于任何基于软件更新的客户端安装。 有关详细信息，请参阅[如何预配客户端安装属性](#BKMK_Provision)部分以及[如何向站点分配客户端](/sccm/core/clients/deploy/assign-clients-to-a-site)一文。  

按照以下过程将没有 Configuration Manager 客户端的计算机配置为使用软件更新点。 还有可用于将客户端软件发布到软件更新点的过程。  

> [!TIP]  
>  如果计算机在上次安装软件后处于待重启状态，基于软件更新的客户端安装可能会导致计算机重启。  


### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>配置组策略对象以指定软件更新点  

1.  使用“组策略管理控制台”  打开新的或现有的组策略对象。  

2.  依次展开“计算机配置”  、“管理模板”  和“Windows 组件”  ，再选择“Windows 更新”  。  

3.  打开“指定 Intranet Microsoft 更新服务位置”  设置的属性，再选择“已启用”  。  

4.  **设置检测更新的 Intranet 更新服务**：指定软件更新点服务器的名称和端口。  

    -   如果已将 Configuration Manager 站点系统配置为使用完全限定的域名 (FQDN)，请使用此格式。  

    -   如果 Configuration Manager 站点系统未配置为使用 FQDN，则使用短名称格式。

    > [!TIP]  
    >  若要确定端口号，请参阅[如何确定 WSUS 使用的端口设置](/sccm/sum/plan-design/plan-for-software-updates)。  

     使用 FQDN 格式的示例：`http://server1.contoso.com:8530`  

5.  **设置 Intranet 统计服务器**：此设置通常使用相同服务器名称进行配置。

6.  将组策略对象分配到想要在其中安装客户端以及接收软件更新的计算机。  


### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>将 Configuration Manager 客户端发布到软件更新点  

1.  在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。  

2.  选择要为其配置基于软件更新的客户端安装的站点。  

3.  在功能区的“主页”  选项卡上，依次选择“设置”  组中的“客户端安装设置”  和“基于软件更新的客户端安装”  。  

4.  选择“启用基于软件更新的客户端安装”  。  

5.  如果站点的客户端版本比软件更新点上的版本更新，则会打开“检测到客户端包的较高版本”对话框  。 选择“是”  ，以发布最新版本。  

    > [!NOTE]  
    >  如果你尚未将客户端软件发布到软件更新点，此对话框为空白。

当有新版本时不会自动更新 Configuration Manager 客户端的软件更新。 更新站点时，请重复此过程以更新客户端。  

##  <a name="BKMK_ClientGP"></a> 组策略安装

使用 Active Directory 域服务中的组策略来发布或分配 Configuration Manager 客户端。 客户端在计算机启动时安装。 如果你使用组策略，客户端显示在“控制面板”的“添加或删除程序”  中。 用户可以在其中安装它。  

使用 Windows Installer 包 CCMSetup.msi 进行基于组策略的安装。 此文件位于站点服务器上的 `<ConfigMgr installation directory>\bin\i386` 文件夹中。 无法通过向此文件添加属性来更改安装行为。  

> [!IMPORTANT]  
>  必须拥有管理员权限，才能访问客户端安装文件。  

-   如果你已为 Configuration Manager 扩展 Active Directory 架构，并已选择“站点属性”  对话框中“高级”  选项卡上的“在 Active Directory 域服务中发布此站点”  ，客户端计算机会在 Active Directory 域服务中自动搜索安装属性。 有关详细信息，请参阅[关于发布到 Active Directory 域服务的客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services)。  

-   如果尚未扩展 Active Directory 架构，请参阅[预配客户端安装属性](#BKMK_Provision)部分，以了解如何将安装属性存储在计算机的 Windows 注册表中。 客户端在安装时会使用这些安装属性。  

有关详细信息，请参阅[如何使用组策略来远程安装软件](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server)。  

##  <a name="BKMK_Manual"></a> 手动安装

使用 CCMSetup.exe 在计算机上手动安装客户端软件。 此程序及其支持文件位于站点服务器上 Configuration Manager 安装文件夹中的“客户端”文件夹内。 站点按以下方式将此文件夹共享到网络：  

 `\\<site server name>\SMS_<site code>\Client\`  

 `<site server name>` 是主站点服务器名称。 `<site code>` 是客户端分配到的主站点代码。 若要在客户端上从命令行运行 CCMSetup.exe，请连接到此网络位置，然后运行命令。  

> [!IMPORTANT]  
>  必须拥有管理员权限，才能访问客户端安装文件。  

CCMSetup.exe 会将所有必需的先决条件复制到客户端计算机，并调用 Windows Installer 包 (Client.msi)，以安装客户端。 不能直接运行 Client.msi。  

若要修改客户端安装的行为，请指定 CCMSetup.exe 和 Client.msi 的命令行选项。 在指定 Client.msi 属性之前，请确保指定以 `/` 开头的 CCMSetup 参数。 例如：  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

在此示例中，客户端使用以下选项进行安装：  

|选项|说明|  
|--------------|-----------------|  
|`/mp:SMSMP01`|此 CCMSetup 参数指定管理点 SMSMP01，用于下载必需的客户端安装文件。|  
|`/logon`|此 CCMSetup 参数指定在计算机上发现已有 Configuration Manager 客户端时应停止安装。|  
|`SMSSITECODE=AUTO`|此 Client.msi 属性指定，客户端尝试查找要使用的 Configuration Manager 站点代码，例如通过使用 Active Directory 域服务来查找。|  
|`FSP=SMSFP01`|此 Client.msi 属性指定使用名为 SMSFP01 的回退状态点接收从客户端计算机发送的状态消息。|  

 有关详细信息，请参阅[关于客户端安装参数和属性](/sccm/core/clients/deploy/about-client-installation-properties)。  

> [!TIP]  
> 有关使用 Azure Active Directory (Azure AD) 标识在新式 Windows 10 设备上安装 Configuration Manager 客户端的过程，请参阅[使用 Azure AD 身份验证安装并分配 Configuration Manager Windows 10 客户端](/sccm/core/clients/deploy/deploy-clients-cmg-azure)。 此过程适用于 Intranet 或 Internet 上的客户端。  


### <a name="manual-installation-examples"></a>手动安装示例

这些示例适用于 Intranet 上已加入 Active Directory 的客户端。 它们使用以下值：  

- **MPSERVER**：托管管理点的服务器   
- **FSPSERVER**：托管回退状态点的服务器  
- **ABC**：站点代码  
- **contoso.com**：域名  

假设你已为所有站点系统服务器配置 Intranet FQDN，并已将站点信息发布到 Active Directory。  

先在客户端计算机上执行以下步骤：  
1. 以本地管理员身份登录。  
2. 将驱动器 Z 映射到 `\\MPSERVER\SMS_ABC\Client`。  
3. 将命令提示符切换到驱动器 Z。  

然后运行以下命令之一：  


#### <a name="manual-example-1"></a>手动示例 1  

`CCMSetup.exe`  

此命令安装客户端，而不使用其他任何参数或属性。 客户端自动配置有发布到 Active Directory 域服务的客户端安装属性，包括以下设置：  

- 站点代码：此设置要求客户端的网络位置包含在为客户端分配配置的边界组中。  
- 管理点。
- 回退状态点。
- 仅使用 HTTPS 进行通信。  

有关详细信息，请参阅[关于发布到 Active Directory 域服务的客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services)。  


#### <a name="manual-example-2"></a>手动示例 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
此命令替代 Active Directory 域服务提供的自动配置。 它不要求必须在为客户端分配而配置的边界组中添加客户端的网络位置。 相反，安装会指定以下设置：
- 站点代码。
- Intranet 管理点。
- 基于 Internet 的管理点。
- 接受 Internet 连接的回退状态点。
- 使用有效期最长的客户端公钥基础结构 (PKI) 证书（若有）。  

##  <a name="BKMK_ClientLogonScript"></a> 登录脚本安装

Configuration Manager 支持使用登录脚本来安装 Configuration Manager 客户端软件。 在登录脚本中使用 CCMSetup.exe 程序文件，以触发客户端安装。  

登录脚本安装使用的方法与手动客户端安装使用的方法相同。 为 CCMSsetup.exe 指定 `/logon` 安装参数。 如果计算机上已存在任意版本的客户端，则此参数会阻止安装客户端。 此行为可防止每次运行登录脚本时重新安装客户端。  

如果你未使用 `/Source` 参数指定安装源，且未使用 `/MP` 参数指定可从中获取安装的管理点，CCMSetup.exe 会通过搜索 Active Directory 域服务来查找管理点。 只有当你已为 Configuration Manager 扩展架构，且已将站点发布到 Active Directory 域服务时，才会发生此行为。 或者，客户端可能会使用 DNS 或 WINS 来查找管理点。  



##  <a name="BKMK_ClientApp"></a> 包和程序安装  

使用 Configuration Manager 来创建和部署包和程序，以便为所选设备升级客户端软件。 Configuration Manager 提供一个包定义文件，此文件使用常用值填充包属性。 通过指定其他命令行参数和属性来自定义客户端安装的行为。  

> [!NOTE]  
>  使用这种方法无法升级 Configuration Manager 2007 客户端。 请改用自动客户端升级，它能自动创建并部署包含客户端最新版本的包。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients)。  
>   
>  有关如何从旧版 Configuration Manager 客户端迁移的详细信息，请参阅[规划客户端迁移策略](/sccm/core/migration/planning-a-client-migration-strategy)。  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>创建客户端软件的包和程序  

使用以下过程创建 Configuration Manager 包和程序，你可以将此包和程序部署到 Configuration Manager 客户端计算机以升级客户端软件。  

1.  在 Configuration Manager 控制台中，转到“软件库”工作区，展开“应用程序管理”，然后选择“包”节点    。  

2.  在功能区的“主页”  选项卡上，选择“创建”  组中的“从定义创建包”  。  

3.  在向导的“包定义”  页上，从“发布者”  列表中选择“Microsoft”  ，并从“包定义”  列表中选择“Configuration Manager 客户端升级”  。  

4.  在“源文件”  页上，选择“始终从源文件夹获取文件”  。  

5.  在“源文件夹”页上，选择“网络路径(UNC 名称)”   。 然后，输入服务器的网络路径，并共享包含客户端安装文件的路径。  

    > [!NOTE]  
    >  运行 Configuration Manager 部署的计算机必须能够访问指定的网络文件夹。 否则，客户端安装失败。  

    若要更改任何客户端安装属性，请在“Configuration Manager 代理无提示升级属性”程序对话框的“常规”选项卡上修改 CCMSetup.exe 命令行   。 默认安装属性为 `/noservice SMSSITECODE=AUTO`。  

6. 将包分发给你想要承载客户端升级包的所有分发点。 然后，将包部署到包含想要升级的客户端的设备集合。  



## <a name="bkmk_mdm"></a> Intune MDM 托管的 Windows 设备

将 Configuration Manager 客户端部署到使用 Microsoft Intune 注册的设备。

此过程适用于连接到 Intranet 的传统客户端。 它使用传统的客户端身份验证方法。 若要确保设备在安装客户端后仍保持托管状态，它必须在 Intranet 上，并且位于 Configuration Manager 站点边界内。  

有关使用 Azure AD 标识在新式 Windows 10 设备上安装 Configuration Manager 客户端的过程，请参阅[使用 Azure AD 身份验证安装并分配 Configuration Manager Windows 10 客户端](/sccm/core/clients/deploy/deploy-clients-cmg-azure)。

> [!NOTE]  
> 在一些版本的 Configuration Manager 中，在客户端软件安装后，设备默认从 Intune 取消注册。
> 
> 从 1710 版开始，客户端不从 Intune 取消注册。 它们可以同时使用 Configuration Manager 客户端和 MDM 注册。 有关详细信息，请参阅[共同管理概述](/sccm/comanage/overview)。  


###  <a name="install-clients-by-using-intune"></a>使用 Intune 安装客户端  

1. 在 Intune 中，[添加 Windows 业务线应用程序](https://docs.microsoft.com/intune/lob-apps-windows)，其中包含 Configuration Manager 客户端安装文件 CCMSetup.msi。 此文件位于站点服务器上的以下文件夹中：`<ConfigMgr installation directory>\bin\i386`。  

2. 在 Intune 软件发行者中，输入命令行参数。 例如，在 Intranet 上，将以下命令用于传统客户端：  

   `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

   > [!NOTE]  
   > 有关用于使用 Azure AD 身份验证的新式 Windows 10 客户端的示例命令，请参阅[如何准备基于 Internet 的设备以进行共同管理](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client)。  

3. [将应用分配](https://docs.microsoft.com/intune/deploy-use/deploy-apps-in-microsoft-intune)给一组已注册的 Windows 计算机。  



##  <a name="BKMK_ClientImage"></a> OS 映像安装

在用于创建 OS 映像的引用计算机上预装 Configuration Manager 客户端。

> [!IMPORTANT]  
> 如果你使用 Configuration Manager 任务序列部署 OS 映像，[准备 ConfigMgr 客户端](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)步骤会完全删除 Configuration Manager 客户端。  


### <a name="prepare-the-client-computer-for-imaging"></a>准备要映像的客户端计算机  

1.  在引用计算机上手动安装 Configuration Manager 客户端软件。 有关详细信息，请参阅[如何手动安装 Configuration Manager 客户端](#BKMK_Manual)。  

    > [!IMPORTANT]  
    >  请不要在 CCMSetup.exe 命令行属性中为客户端指定 Configuration Manager 站点代码。  

2.  在命令提示符处，键入“`net stop ccmexec`”，以停止引用计算机上的“SMS 代理主机”服务 (CcmExec.exe)。  

3.  从引用计算机上的 Windows 文件夹中删除 SMSCFG.INI 文件。  

4.  删除存储在引用计算机上的本地计算机存储中的任何证书。 例如，如果使用 PKI 证书，请先在“计算机”  和“用户”  的“个人”  存储中删除此证书，再创建计算机映像。  

5.  如果客户端与引用计算机安装在不同的 Configuration Manager 层次结构中，请从引用计算机中删除受信任的根密钥。  

    > [!NOTE]  
    >  如果客户端无法查询 Active Directory 域服务来查找管理点，它们会使用受信任的根密钥来确定受信任的管理点。 如果将所有映像的客户端与主计算机部署在同一层次结构中，请保留受信任的根密钥。 
    > 
    > 如果将客户端部署在不同层次结构中，请删除受信任的根密钥。 还为这些客户端设置新的受信任的根密钥。 有关详细信息，请参阅[规划受信任的根密钥](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK)。  

6.  使用映像软件捕获引用计算机的映像。  

7.  将映像部署到目标计算机。  



##  <a name="BKMK_ClientWorkgroup"></a> 工作组计算机  

Configuration Manager 支持为工作组中的计算机安装客户端。 使用[如何手动安装 Configuration Manager 客户端](#BKMK_Manual)中指定的方法在工作组计算机上安装客户端。  


### <a name="prerequisites"></a>先决条件  

-   在每台工作组计算机上手动安装客户端。 在安装过程中，交互用户必须具有本地管理员权限。  

-   若要访问 Configuration Manager 站点服务器域中的资源，请为此站点配置网络访问帐户。 在软件分发站点组件中指定此帐户。 有关详细信息，请参阅[站点组件](/sccm/core/servers/deploy/configure/site-components)。  


### <a name="limitations"></a>限制  

-   工作组客户端无法从 Active Directory 域服务中查找管理点， 而是使用 DNS、WINS 或其他管理点。  

-   不支持全局漫游。 工作组客户端无法在 Active Directory 域服务中查询站点信息。  

-   Active Directory 发现方法无法发现工作组中的计算机。  

-   你无法向工作组计算机的用户部署软件。  

-   你无法使用客户端请求安装方法在工作组计算机上安装客户端。  

-   工作组客户端无法使用 Kerberos 进行身份验证，可能需要手动批准。  

-   你无法将工作组客户端配置为分发点。 Configuration Manager 要求分发点计算机是某个域的成员。  


### <a name="install-the-client-on-workgroup-computers"></a>在工作组计算机上安装客户端  

审阅先决条件，再按照[如何手动安装 Configuration Manager 客户端](#BKMK_Manual)部分中的说明操作。  


#### <a name="workgroup-example-1"></a>工作组示例 1

此示例执行以下操作：
- 针对 Intranet 客户端管理安装客户端
- 指定站点代码
- 指定 DNS 后缀以查找管理点  

 `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     
#### <a name="workgroup-example-2"></a>工作组示例 2

此示例要求客户端位于在边界组中配置的网络位置上。 如果不满足此要求，自动站点分配将无法运行。 该命令包含位于服务器 FSPSERVER 上的回退状态点。 此属性有助于跟踪客户端部署，并发现任何客户端通信问题。

   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> 基于 Internet 的客户端管理  
 
> [!NOTE]  
> 此部分不适用于使用[云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway)的客户端。 若要使用云管理网关安装基于 Internet 的客户端，请参阅[使用 Azure AD 身份验证安装并分配 Configuration Manager Windows 10 客户端](/sccm/core/clients/deploy/deploy-clients-cmg-azure)。  

如果 Configuration Manager 站点支持对有时位于 Intranet 有时位于 Internet 上的客户端进行[基于 Internet 的客户端管理](/sccm/core/clients/manage/plan-internet-based-client-management)，在 Intranet 上安装客户端时有两种选择：  

-   在安装客户端时添加 Client.msi 属性 `CCMHOSTNAME=<internet FQDN of the internet-based management point>`，例如通过使用手动安装或客户端请求安装来添加。 使用此方法时，将客户端直接分配到站点。 无法使用自动站点分配。 请参阅[如何手动安装 Configuration Manager 客户端](#BKMK_Manual)部分，其中提供了此配置方法的示例。  

-   针对 Intranet 客户端管理安装客户端，然后向客户端分配基于 Internet 的客户端管理点。 更改管理点，具体是通过使用“控制面板”中“Configuration Manager”  页上的客户端属性，或使用脚本。 在使用此方法时，你可以使用自动客户端分配。 有关详细信息，请参阅[如何在客户端安装后针对基于 Internet 的客户端管理配置客户端](#BKMK_ConfigureIBCM_MP)部分。  

若要安装 Internet 上的客户端，请选择以下受支持的方法之一：  

-   为这些客户端提供机制以使用 VPN 临时连接到 Intranet。 然后使用任何合适的客户端安装方法安装客户端。  

-   使用与 Configuration Manager 无关的安装方法。 例如，将客户端安装源文件打包到可移动媒体上，并将此媒体发送给用户。 客户端安装源文件位于 Configuration Manager 站点服务器上的 `<installation path>\Client` 文件夹中。 在媒体上添加脚本，以手动复制客户端文件夹。 从此文件夹中使用 CCMSetup.exe 以及所有合适的 CCMSetup 命令行属性安装客户端。  

> [!NOTE]  
>  Configuration Manager 不支持直接通过基于 Internet 的管理点或基于 Internet 的软件更新点安装客户端。

通过 Internet 管理的客户端必须与基于 Internet 的站点系统进行通信。 在安装客户端之前，确保这些客户端还具有公钥基础结构 (PKI) 证书。 独立于 Configuration Manager 安装这些证书。 有关详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  


### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>通过指定 CCMSetup 命令行属性在 Internet 上安装客户端  

1.  按照[如何手动安装 Configuration Manager 客户端](#BKMK_Manual)部分中的指示进行操作。 始终包括以下选项：  

    -   CCMSetup 命令行参数 `/source:<local path of the copied Client folder>`  

    -   CCMSetup 命令行参数 `/UsePKICert`  

    -   Client.msi 属性 `CCMHOSTNAME=<FQDN of internet-based management point>`  

    -   Client.msi 属性 `SMSSIGNCERT=<local path of exported site server signing certificate>`  

    -   Client.msi 属性 `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    >  如果站点有多个基于 Internet 的管理点，为 `CCMHOSTNAME` 属性指定哪个管理点并不重要。 当 Configuration Manager 客户端连接到基于 Internet 的指定管理点时，它会向客户端发送一个站点中基于 Internet 的可用管理点的列表。 客户端从该列表中随机选择一个。

2.  如果不希望客户端检查证书吊销列表 (CRL)，请指定 CCMSetup 命令行参数 `/NoCRLCheck`。  

3.  如果在使用基于 Internet 的回退状态点，请指定 Client.msi 属性 `FSP=<internet FQDN of the internet-based fallback status point>`。  

4.  如果要针对仅限 Internet 的客户端管理安装客户端，请指定 Client.msi 属性 `CCMALWAYSINF=1`。  

5.  确定是否必须指定其他 CCMSetup 命令行参数。 例如，如果客户端有多个有效 PKI 证书，你可能必须指定证书选择条件。 有关可用属性的列表，请参阅[关于客户端安装参数和属性](/sccm/core/clients/deploy/about-client-installation-properties)。  


#### <a name="internet-based-example"></a>基于 Internet 的示例

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

此示例使用以下行为安装客户端：
- 使用驱动器 D 上文件夹中的源文件。
- 使用客户端 PKI 证书。
- 选择有效期最长的证书。
- 仅限 Internet 的客户端管理。
- 分配客户端以使用基于 Internet 的管理点 SERVER1。
- 分配 contoso.com 域中基于 Internet 的回退状态点。
- 将客户端分配到 ABC 站点。  


###  <a name="BKMK_ConfigureIBCM_MP"></a> 在客户端安装后针对基于 Internet 的客户端管理配置客户端  

若要在安装客户端之后分配基于 Internet 的管理点，请使用以下过程之一。 第一个过程需手动进行配置，并且仅适用于某些客户端。 第二个过程更适用于配置大部分客户端。  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>在从 Configuration Manager 控制面板安装客户端之后，针对基于 Internet 的客户端管理配置客户端  

1.  打开客户端上的“Configuration Manager”控制面板  。  

2.  在“Internet”选项卡上，输入基于 Internet 的管理点的完全限定域名 (FQDN) 作为“Internet FQDN”   。  

    > [!NOTE]  
    >  只有当客户端有客户端 PKI 证书时，“Internet”  选项卡才可用。  

3.  如果客户端通过使用代理服务器访问 Internet，请输入代理服务器设置。  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>在客户端安装后通过使用脚本来针对基于 Internet 的客户端管理配置客户端  

##### <a name="vbscript"></a>VBScript

1.  打开文本编辑器（如记事本）。  

2.  将以下 VBScript 代码复制并插入文件中。 将 `mp.contoso.com` 替换为基于 Internet 的管理点的 Internet FQDN。  

    ``` VBScript 
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  若要删除基于 Internet 的指定管理点，请删除引号内的服务器 FQDN 值。 此行变为 `newInternetBasedManagementPointFQDN = ""`。

4.  以 .vbs 扩展名保存文件。  

5.  使用 cscript.exe 在客户端计算机上运行脚本。 使用以下方法之一：  

    -   通过使用包和程序将文件部署到现有 Configuration Manager 客户端。  

    -   通过在文件资源管理器中双击脚本文件，以本地方式在现有 Configuration Manager 客户端上运行文件。  

可能必须重启客户端以使更改生效。  

##### <a name="powershell"></a>PowerShell

1. 打开 PowerShell 内联编辑器（如 PowerShell ISE 或 Visual Studio Code）。 也可以使用文本编辑器（如记事本）。

2. 将以下代码行复制并插入编辑器。 将 `'mp.contoso.com'` 替换为基于 Internet 的管理点的 Internet FQDN。

    ``` PowerShell
    
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    
    ```

    > [!NOTE]  
    >  最后一行仅用于验证新的 Internet 管理点值。
    >
    >  若要删除基于 Internet 的指定管理点，请删除引号内的服务器 FQDN 值。 此行变为 `$newInternetBasedManagementPointFQDN = ''`。

3. 使用提升的权限运行此脚本。


##  <a name="BKMK_Provision"></a> 为组策略客户端安装和基于软件更新的客户端安装预配客户端安装属性

使用 Windows 组策略为计算机预配 Configuration Manager 客户端安装属性。 这些属性存储在计算机的注册表中。 客户端在安装时会读取这些属性。 通常不需要此过程，但在某些客户端安装方案中可能需要，例如：  

-   正在使用组策略设置或基于软件更新的客户端安装方法。 没有为 Configuration Manager 扩展 Active Directory 架构。  

-   你希望覆盖特定计算机上的客户端安装属性。  

> [!NOTE]  
>  如果在 CCMSetup.exe 命令行上提供了任何安装属性，则不使用计算机上设置的安装属性。

Configuration Manager 安装介质上提供了名为 ConfigMgrInstallation.adm 的组策略管理模板。 可使用该模板为客户端计算机预配安装属性。


### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>使用组策略对象来配置和分配客户端安装属性  

1.  使用编辑器（如 Windows 组策略对象编辑器），将 ConfigMgrInstallation.adm 管理模板导入新的或现有的组策略对象中。 此文件位于 Configuration Manager 安装介质上的 `TOOLS\ConfigMgrADMTemplates` 文件夹中。  

2.  打开导入的设置“配置客户端部署设置”  的属性。  

3.  选择“已启用”  。  

4.  在“CCMSetup”  框中，输入必需的 CCMSetup 命令行属性。 有关所有 CCMSetup 命令行属性的列表及其用法示例，请参阅[关于客户端安装参数和属性](/sccm/core/clients/deploy/about-client-installation-properties)。  

5.  将组策略对象分配给要通过 Configuration Manager 客户端安装属性设置的计算机。  
