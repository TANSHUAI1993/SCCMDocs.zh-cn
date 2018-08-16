---
title: CMG 证书
description: 了解用于云管理网关的各种数字证书。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: fbae44d1344dd36d3c0a6faf2e50727dfa830ba0
ms.sourcegitcommit: 8060ea520fb08629e1d5f249daffe825536673a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "35232364"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>云管理网关证书

*适用范围：System Center Configuration Manager (Current Branch)*

根据通过云管理网关 (CMG) 管理 Internet 上的客户端所用的方案，可能需要一个或多个数字证书。 有关不同方案的详细信息，请参阅[规划云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)。


## <a name="cmg-server-authentication-certificate"></a>CMG 服务器身份验证证书

所有方案都需要此证书。

在 Configuration Manager 控制台中创建 CMG 时需要提供此证书。

CMG 创建基于 Internet 的客户端要连接到的 HTTPS 服务。 此服务器需要使用服务器身份验证证书构建安全频道。 请从公共提供程序购买此用途的证书，或通过公钥基础结构 (PKI) 颁发此证书。 有关详细信息，请参阅[针对客户端的 CMG 受信任的根证书](#cmg-trusted-root-certificate-to-clients)。

 > [!TIP]
 > 此证书需要使用全局唯一名称标识 Azure 中的服务。 请求证书前，请确认所需的 Azure 域名是否唯一。 例如，GraniteFalls.CloudApp.Net。 登录 [Microsoft Azure 门户](https://portal.azure.com)。 单击“创建资源”，选择“计算”类别，然后单击“云服务”。 在“DNS 名称”字段中，键入所需的前缀，例如 GraniteFalls。 界面将反映域名是否可用，或是否已被其他服务使用。 不要在门户中创建服务，仅使用此流程检查名称可用性。 
  
 > [!NOTE]
 > 从 1802 版开始，CMG 服务器身份验证证书支持通配符。 某些证书颁发机构颁发证书时将通配符用作主机名。 例如，.contoso.com**\***。 某些组织使用通配符证书简化其 PKI 并降低维护成本。
 <!--491233-->


### <a name="cmg-trusted-root-certificate-to-clients"></a>针对客户端的 CMG 受信任的根证书

客户端必须信任 CMG 服务器身份验证证书。 有两种方法可实现此信任：
- 使用公共和全局受信任的证书提供程序提供的证书。 例如（但不限于）DigiCert、Thawte 或 VeriSign。 Windows 客户端包括来自这些提供程序的受信任的根证书颁发机构 (CA)。 通过使用这些受信任提供程序中的一个提供程序发布的服务器身份验证证书，客户端会自动信任该证书。 
- 使用公钥基础结构 (PKI) 中的企业 CA 颁发的证书。 大多数企业 PKI 实现会向 Windows 客户端添加受信任的根 CA。 例如，在组策略中使用 Active Directory 证书服务。 如果从客户端不自动信任的 CA 颁发 CMG 服务器身份验证证书，则需要向基于 Internet 的客户端添加 CA 受信任的根证书。
    - 还可以使用 Configuration Manager 证书配置文件在客户端上预配证书。 有关详细信息，请参阅[证书配置文件简介](/sccm/protect/deploy-use/introduction-to-certificate-profiles)。

### <a name="server-authentication-certificate-issued-by-public-provider"></a>由公共提供程序颁发的服务器身份验证证书

如果使用此方法，客户端会自动信任证书，无需自行创建自定义证书。 Configuration Manager 在 Azure 中创建具有 cloudapp.net 域的服务。 公共证书提供程序不能向你颁发具有此名称的证书。 使用以下流程创建 DNS 别名：

1. 在组织的公共 DNS 中创建规范名称记录 (CNAME)。 该记录会将 CMG 的别名创建为一个友好名称，你可以在公共证书中使用。
例如，Contoso 将其 CMG 命名为 GraniteFalls，它在 Azure 中将变成 GraniteFalls.CloudApp.Net。 在 Contoso 的公共 DNS contoso.com 命名空间中，DNS 管理员为实际主机名 GraniteFalls.CloudApp.net 新建 GraniteFalls.Contoso.com 的 CNAME 记录。
2. 使用 CNAME 别名的公用名称 (CN) 向公共提供程序请求一个服务器身份验证证书。
例如，Contoso 对证书 CN 使用 **GraniteFalls.Contoso.com**。
3. 使用此证书在 Configuration Manager 控制台中创建 CMG。 在创建云管理网关向导的“设置”页面： 
    - 当（从“证书文件”）添加此云服务的服务器证书时，向导将从证书 CN 中提取主机名用作服务名称。 
    - 然后将该主机名追加到 Azure 美国政府云的 cloudapp.net 或 usgovcloudapp.net，作为用于在 Azure 中创建服务的服务 FQDN。
    - 例如，当 Contoso 创建 CMG 时，Configuration Manager 会从证书 CN 中提取主机名 GraniteFalls。 Azure 将实际服务创建为 GraniteFalls.CloudApp.net。

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a>企业 PKI 颁发的服务器身份验证证书

为 CMG 创建与云分发点相同的自定义 SSL 证书。 按照[为基于云的分发点部署服务证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012)中的说明，但以不同方式执行以下操作：

- 请求自定义 Web 服务器证书时，为证书公用名称提供 FQDN。 要在 Azure 公共云上使用 CMG，请对 Azure 美国政府云使用以 cloudapp.net 或 usgovcloudapp.net 结尾的名称。



## <a name="azure-management-certificate"></a>Azure 管理证书

经典服务部署需要此证书。Azure 资源管理器部署不需要此证书。

在 Azure 门户中的 Configuration Manager 控制台中创建 CMG 时需要提供此证书。

要在 Azure 中创建 CMG，Configuration Manager 服务连接点需要首先对 Azure 订阅进行身份验证。 使用经典服务部署时，它将 Azure 管理证书用于此身份验证。 Azure 管理员会将此证书上传到你的订阅。 在 Configuration Manager 控制台中创建 CMG 时，请提供此证书。

有关如何上传管理证书的详细信息和说明，请参阅 Azure 文档中的以下文章：

- [云服务和管理证书](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)

- [上传 Azure 服务管理证书](/azure/azure-api-management-certs)

> [!IMPORTANT]
> 请确保复制与管理证书关联的订阅 ID。 在 Configuration Manager 控制台中创建 CMG 时需使用此证书。



## <a name="client-authentication-certificate"></a>客户端身份验证证书

运行未加入 Azure Active Directory (Azure AD) 的 Windows 7、Windows 8.1 和 Windows 10 设备的基于 Internet 的客户端需要此证书。CMG 连接点也需要此证书。加入 Azure AD 的 Windows 10 客户端不需要此证书。

客户端使用此证书向 CMG 进行身份验证。 已加入混合域或云域的 Windows 10 设备不需要此证书，因为它们使用 Azure AD 进行身份验证。

请在 Configuration Manager 的上下文外预配此证书。 例如，使用 Active Directory 证书服务和组策略颁发客户端身份验证证书。 有关详细信息，请参阅[为 Windows 计算机部署客户端证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012)。


### <a name="client-trusted-root-certificate-to-cmg"></a>针对 CMG 的客户端受信任的根证书

使用客户端身份验证证书时需要此证书。如果所有客户端使用 Azure AD 进行身份验证，则不需要此证书。 

在 Configuration Manager 控制台中创建 CMG 时需要提供此证书。

CMG 必须信任客户端身份验证证书。 要实现此信任，请提供受信任的根证书链。 可指定两个受信任的根 CA 和四个中间（从属）CA。 


#### <a name="export-the-client-certificates-trusted-root"></a>导出客户端证书的受信任根

向计算机颁发客户端身份验证证书后，在该计算机上使用以下流程导出受信任的根。

1.  单击“开始”菜单。 键入“run”打开“运行”窗口。 打开“mmc”。 

2.  在“文件”菜单中，选择“添加/删除管理单元...”。

3.  在“添加/删除管理单元”对话框中，选择“证书”，然后单击“添加”。 
    a. 在“证书管理单元”对话框中，选择“计算机帐户”，然后单击“下一步”。 
    b. 在“选择计算机”对话框中，选择“本地计算机”，然后单击“完成”。 
    c. 在“添加/删除管理单元”对话框中，单击“确定”。

4.  依次展开“证书”、“个人”，然后选择“证书”。

5.  选择一个预期用途为“客户端身份验证”的证书。 
    a. 从“操作”菜单中，选择“打开”。 
    b. 切换到“证书路径”选项卡。c. 从证书链上选择下一个证书，然后单击“查看证书”。

6.  在新“证书”对话框中，切换到“详细信息”选项卡。单击“复制到文件...”。

7.  使用默认证书格式（DER 编码二进制 X.509 (.CER)）完成证书导出向导。 记下导出证书的名称和位置。

8. 导出原始客户端身份验证证书的证书路径中的所有证书。 记下哪些导出证书是中间 CA，哪些是受信任的根 CA。



## <a name="enable-management-point-for-https"></a>为 HTTPS 启用管理点

证书要求
- 在 1706 或 1710 版中，使用客户端身份验证证书管理具有本地标识的传统客户端时，建议但不强制使用此证书。
- 在 1710 版中，管理加入 Azure AD 的 Windows 10 客户端时，管理点需要此证书。 
- 从 1802 版开始，所有方案都需要使用此证书。 只有针对 CMG 启用的管理点才需使用 HTTPS。 此行为更改为基于 Azure AD 令牌的身份验证提供了更好的支持。 

请在 Configuration Manager 的上下文外预配此证书。 例如，使用 Active Directory 证书服务和组策略颁发 Web 服务器证书。 有关详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)和[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)。



## <a name="next-steps"></a>后续步骤

- [设置云管理网关](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [有关云管理网关的常见问题解答](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [云管理网关的安全和隐私](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
