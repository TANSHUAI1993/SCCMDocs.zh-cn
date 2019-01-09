---
title: 规划安全性
titleSuffix: Configuration Manager
description: 获取 Configuration Manager 中安全相关的最佳做法和其他信息。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f7cb374859d2605021a3f1ec98d6a6b6081bfc4
ms.sourcegitcommit: 54e5786875c4e5f5c1b54e38ed59e96344faf9b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2019
ms.locfileid: "53817896"
---
# <a name="plan-for-security-in-configuration-manager"></a>在 Configuration Manager 中规划安全性

适用范围：System Center Configuration Manager (Current Branch)

本文介绍了使用 Configuration Manager 实现进行安全规划时要考虑的原理。 它包括以下部分：  

- [规划证书（自签名和 PKI）](#BKMK_PlanningForCertificates)  
    - [加密：下一代 (CNG) 证书](#bkmk_plan-cng)  
    - [增强型 HTTP](#bkmk_plan-ehttp)  
    - [CMG 和 CDP 证书](#bkmk_plan-cmgcdp)  
    - [站点服务器签名证书（自签名）](#bkmk_plansitesign)  
    - [PKI 证书吊销](#BKMK_PlanningForCRLs)  
    - [PKI 受信任的根证书和证书颁发者](#BKMK_PlanningForRootCAs)  
    - [PKI 客户端证书选择](#BKMK_PlanningForClientCertificateSelection)  
    - [PKI 证书和基于 Internet 的客户端管理的过渡策略](#BKMK_PlanningForPKITransition)  

- [规划受信任的根密钥](#BKMK_PlanningForRTK)  

- [规划签名和加密](#BKMK_PlanningForSigningEncryption)  

- [规划基于角色的管理](#BKMK_PlanningForRBA)  

- [规划 Azure Active Directory](#bkmk_planazuread)  

- [规划 SMS 提供程序的身份验证](#bkmk_auth)



##  <a name="BKMK_PlanningForCertificates"></a> 规划证书（自签名和 PKI）  

 Configuration Manager 组合使用自签名证书和公钥基础结构 (PKI) 证书。  

 尽可能使用 PKI 证书。 有关详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。 Configuration Manager 在移动设备注册期间请求 PKI 证书时，必须使用 Active Directory 域服务和企业证书颁发机构。 对于所有其他 PKI 证书，请独立于 Configuration Manager 部署和管理它们。 

 客户端计算机连接到基于 Internet 的站点系统时，需要 PKI 证书。 云管理网关和云分发点的某些方案也需要 PKI 证书。 有关详细信息，请参阅[在 Internet 上管理客户端](/sccm/core/clients/manage/manage-clients-internet)。

 使用 PKI 时，也可以使用 IPsec 帮助保护站点中站点系统之间以及站点之间的服务器对服务器通信，以及计算机之间的其他数据传输。 IPsec 的实现独立于 Configuration Manager。  

 PKI 证书不可用时，Configuration Manager 将自动生成自签名的证书。 Configuration Manager 中的某些证书始终是自签名证书。 在某些情况下，Configuration Manager 会自动管理自签名证书，不必采取任何其他操作。 其中一个示例是站点服务器签名证书。 该证书始终是自签名证书。 它可确保客户端从管理点下载的策略发送自站点服务器，并且未被篡改。  


### <a name="bkmk_plan-cng"></a>加密：下一代 (CNG) 证书  

 Configuration Manager 支持加密：下一代 (CNG) 证书. Configuration Manager 客户端可以通过 CNG 密钥存储提供者 (KSP) 中的私钥使用 PKI 客户端身份验证证书。 通过 KSP 支持，Configuration Manager 客户端可支持基于硬件的私钥，如用于 PKI 客户端身份验证证书的 TPM KSP。 有关详细信息，请参阅 [CNG 证书概述](/sccm/core/plan-design/network/cng-certificates-overview)。


### <a name="bkmk_plan-ehttp"></a> 增强型 HTTP  

 建议对于所有 Configuration Manager 通信路径使用 HTTPS 通信，但由于管理 PKI 证书的开销，对一些客户来说颇具挑战性。 Azure Active Directory (Azure AD) 集成的引入可以减少某些证书要求但不是所有证书要求。 自版本 1806 开始，可启用此站点以使用“增强型 HTTP”。 此配置通过结合使用自签名证书和 Azure AD 来支持站点系统上的 HTTPS。 此配置不需要 PKI。 有关详细信息，请参阅[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)。  


### <a name="bkmk_plan-cmgcdp"></a> CMG 和 CDP 证书

通过云管理网关 (CMG) 和云分发点 (CDP) 管理 Internet 上的客户端需要使用证书。 证书的数量和类型取决于具体方案。 有关详细信息，请参阅下列文章：
- [云管理网关证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)  
- [云分发点证书](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_certs)  


### <a name="bkmk_plansitesign"></a> 规划站点服务器签名证书（自签名）  

 客户端可以从 Active Directory 域服务和客户端请求安装中安全地获取站点服务器签名证书的副本。 如果客户端无法通过其中一种机制获取此证书的副本，请在安装客户端时进行安装。 如果客户端与站点的第一次通信是通过基于 Internet 的管理点实现的，则此过程尤为重要。 由于此服务器连接到不受信任的网络，因此更容易受到攻击。 如果未采取此额外步骤，则客户端会自动从管理点中下载站点服务器签名证书的副本。  

 在以下情况下，客户端无法安全地获取站点服务器证书的副本：  

 - 不使用客户端请求安装客户端，并且：  

    - 没有为 Configuration Manager 扩展 Active Directory 架构。  

    - 尚未将客户端的站点发布到 Active Directory 域服务。  

    - 客户端来自不受信任的林或工作组。  

 - 正在使用基于 Internet 的客户端管理，并且当客户端位于 Internet 上时安装该客户端。  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>安装客户端与站点服务器签名证书的副本  

1.  在主站点服务器上找到站点服务器签名证书。 证书存储在 Windows 的 SMS 证书存储中。 它具有使用者名称“站点服务器”和友好名称“站点服务器签名证书”。  

2.  导出无私钥的证书，安全地存储文件并只从受保护的通道中访问它。  

3.  使用以下 client.msi 属性安装客户端：`SMSSIGNCERT=<full path and file name>`  


###  <a name="BKMK_PlanningForCRLs"></a> 规划 PKI 证书吊销  

将 PKI 证书与 Configuration Manager 配合使用时，请规划证书吊销列表 (CRL) 的使用。 设备使用 CRL 验证连接计算机上的证书。 CRL 是证书颁发机构 (CA) 创建和签名的文件。 其中包含一系列 CA 曾颁发但已吊销的证书。 证书管理员吊销证书时，其指纹将添加到 CRL。 例如，如果颁发的证书已确定或者疑似遭盗用，则该证书将被吊销。

> [!IMPORTANT]  
>  因为在 CA 颁发证书时已经将 CRL 的位置添加到证书中，所以请确保在部署 Configuration Manager 使用的任何 PKI 证书之前先规划 CRL。  

IIS 始终会检查 CRL 中是否有客户端证书，且无法在 Configuration Manager 中更改此配置。 默认情况下，Configuration Manager 客户端将始终检查站点系统的 CRL。 通过指定站点属性并指定 CCMSetup 属性来禁用此设置。  

如果计算机使用证书吊销检查但无法找到 CRL，则会视作证书链中的所有证书均已被吊销。 发生此行为是因为他们无法验证这些证书是否存在于证书吊销列表中。 在此情况下，需要证书并包含 CRL 检查的所有连接都将失败。 在验证是否可通过浏览到 CRL 的 http 位置访问该 CRL 时，请务必注意 Configuration Manager 客户端应作为本地系统运行。 因此，对使用用户上下文内运行的 Web 浏览器是否能够访问 CRL 的测试才可能会成功，但由于内部 Web 筛选解决方案的原因，在尝试与同一 CRL URL 建立 http 连接时，可能会阻止计算机帐户。 在这种情况下，可能需要将任何 Web 筛选解决方案中的 CRL URL 列入允许列表。

每次使用证书时检查 CRL 可提供更高的安全性，防止使用已吊销的证书。 但这会导致客户端上出现连接延迟和额外的处理。 组织可能需要对 Internet 或不受信任的网络上的客户端进行此附加安全性检查。  

在确定 Configuration Manager 客户端是否必须检查 CRL 之前，请咨询 PKI 管理员。 然后，在以下两个条件都为 true 时，请考虑在 Configuration Manager 中保持启用此选项：  

-   PKI 基础结构支持 CRL，并且已将其发布到所有 Configuration Manager 客户端都可找到的位置。 这些客户端可能包括 Internet 上的设备和不受信任的林中的设备。  

-   要求检查与站点系统（配置为使用 PKI 证书）的每个连接的 CRL，此要求高于以下要求：  
    - 连接速度更快  
    - 在客户端上进行高效处理  
    - 如果客户端找不到 CRL，无法连接到服务器的风险  


###  <a name="BKMK_PlanningForRootCAs"></a> 规划 PKI 受信任的根证书和证书颁发者列表  

如果 IIS 站点系统使用 PKI 客户端证书通过 HTTP 进行客户端身份验证，或者通过 HTTPS 进行客户端身份验证和加密，则可能必须以站点属性形式导入根 CA 证书。 以下为这两个方案：  

-   使用 Configuration Manager 部署操作系统，管理点仅接受 HTTPS 客户端连接。  

-   使用的 PKI 客户端证书未链接到管理点信任的根证书。  

    > [!NOTE]  
    >  如果从发放用于管理点的服务器证书的同一 CA 层次结构中发放客户端 PKI 证书，则不必指定此根 CA 证书。 但是，如果使用多个 CA 层次结构，并且不确定它们彼此是否信任，请导入客户端的 CA 层次结构的根 CA。  

如果必须为 Configuration Manager 导入根 CA 证书，请从颁发证书的 CA 中或从客户端计算机中导出它们。 如果从颁发证书的 CA（也为根 CA）中导出证书，请确保未导出私钥。 将导出的证书文件存储在安全的位置，以防止篡改。 设置站点时需要访问该文件。 如果通过网络访问文件，请确保使用 IPsec 来防止通信被篡改。  

如果续订了导入的任何根 CA 证书，则必须导入续订的证书。  

这些导入的根 CA 证书和每个管理点的根 CA 证书会创建证书颁发者列表，Configuration Manager 通过以下方式使用该列表：  

-   客户端连接到管理点时，管理点会验证客户端证书是否链接至站点证书颁发者列表中的受信任的根证书。 如果没有，则证书将被拒绝，并且 PKI 连接失败。  

-   如果客户端选择 PKI 证书且具有证书颁发者列表，它们会选择链接至证书颁发者列表中受信任的根证书的证书。 如果不匹配，则客户端不选择 PKI 证书。 有关详细信息，请参阅[规划 PKI 客户端证书选择](#BKMK_PlanningForClientCertificateSelection)。  


###  <a name="BKMK_PlanningForClientCertificateSelection"></a> 规划 PKI 客户端证书选择  

 如果 IIS 站点系统使用 PKI 客户端证书通过 HTTP 进行客户端身份验证，或者通过 HTTPS 进行客户端身份验证和加密，请规划 Windows 客户端选择要用于 Configuration Manager 的证书的方式。  

> [!NOTE]  
>  某些设备不支持证书选择方法。 而是自动选择满足证书要求的第一个证书。 例如，Mac 计算机上的客户端和移动设备不支持证书选择方法。  

在许多情况下，采用默认配置和行为即可。 Windows 计算机上的 Configuration Manager 客户端按此顺序使用这些条件筛选多个证书：  

1.  证书颁发者列表：证书链接至管理点信任的根 CA。  

2.  证书在“个人” 默认证书存储中。  

3.  该证书有效、没有被吊销，并且尚未过期。 有效性检查还验证私钥是否可访问。  

4.  证书具有客户端身份验证功能，或者已发放给计算机名。  

5.  证书具有最长有效期。  

可使用下列机制将客户端配置为使用证书颁发者列表：  

-   将其与 Configuration Manager 站点信息一起发布到 Active Directory 域服务。  

-   使用客户端请求来安装客户端。  

-   将客户端成功分配给其站点之后，客户端从管理点下载它。  

-   在客户端安装过程中将其指定为 CCMCERTISSUERS 的 CCMSetup client.msi 属性。  

首次安装时没有证书颁发者列表并且尚未分配到站点的客户端可跳过此检查。 当客户端具有证书颁发者列表且没有链接到证书颁发者列表中的受信任根证书的 PKI 证书时，证书选择将失败。 客户端不会继续使用其他证书选择条件。  

在大多数情况下，Configuration Manager 客户端会正确标识唯一适合的 PKI 证书。 但是，若情况并非如此，而是根据客户端身份验证功能选择证书时，可设置下列两种替代选择方法：  

- 在客户端证书的“使用者名称”中进行部分字符串匹配。 此方法不区分大小写。 如果你在使用者字段中使用计算机的完全限定的域名 (FQDN) 并且想基于域后缀（例如 contoso.com）选择证书，则该方法很适用。 但是，你可使用此选择方法在证书使用者名称中标识任何连续字符串，以将此证书与客户端证书存储中的其他证书区分开来。  

  > [!NOTE]
  >  你无法将与使用者可选名称 (SAN) 匹配的部分字符串用作站点设置。 虽然可使用 CCMSetup 为 SAN 指定部分字符串匹配，但在下列情况下将由站点属性对其进行覆盖：  
  > 
  > - 客户端检索发布到 Active Directory 域服务的站点信息。  
  >   -   使用客户端请求安装方式安装的客户端。  
  > 
  >   仅当手动安装客户端以及客户端未从 Active Directory 域服务中检索到站点信息时，才在 SAN 中使用部分字符串匹配。 例如，这些条件适用于仅 Internet 客户端。  

- 匹配客户端证书“使用者名称”属性值或“使用者可选名称 (SAN)”属性值。 此方法区分大小写。 使用符合 RFC 3280 标准的 X500 可分辨名称或同等对象标识符 (OID)，并希望根据属性值选择证书时，该方法适用。 你可以仅指定唯一识别或验证证书并使证书与证书存储中其他证书区别开来所需的属性及其值。  

下表显示 Configuration Manager 针对客户端证书选择条件支持的属性值。  

|OID 属性|可分辨名称属性|属性定义|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|域组件|  
|1.2.840.113549.1.9.1|E 或 E-mail|电子邮件地址|  
|2.5.4.3|CN|公用名|  
|2.5.4.4|SN|使用者名称|  
|2.5.4.5|SERIALNUMBER|序列号|  
|2.5.4.6|C|国家/地区代码|  
|2.5.4.7|L|区域|  
|2.5.4.8|S 或 ST|省或自治区名称|  
|2.5.4.9|STREET|街道地址|  
|2.5.4.10|O|组织名称|  
|2.5.4.11|OU|组织单位|  
|2.5.4.12|T 或 Title|标题|  
|2.5.4.42|G 或 GN 或 GivenName|给定名称|  
|2.5.4.43|I 或 Initials|缩写|  
|2.5.29.17|（没有值）|使用者可选名称|  

如果应用了选择条件之后找到了多个合适的证书，则可以替代默认配置以选择有效期最长的证书，并改为指定不选择证书。 在此情况下，客户端将无法使用 PKI 证书与 IIS 站点系统通信。 客户端将向分配的回退状态点发送一则错误消息，警告你证书选择失败，以便可更改或改进证书选择条件。 客户端行为则取决于失败的连接是通过 HTTPS 还是 HTTP 进行的。  

-   如果失败的连接是通过 HTTPS 进行的：则客户端尝试通过 HTTP 进行连接，并使用客户端自签名证书。  

-   如果失败的连接是通过 HTTP 进行的：则客户端尝试使用自签名客户端证书通过 HTTP 再次连接。  

为了帮助标识唯一的 PKI 客户端证书，也可以指定自定义存储，而不是在“计算机”存储中指定“个人”默认值。 但必须独立于 Configuration Manager 创建此存储。 必须能够将证书部署到此自定义存储并在有效期到期之前续订证书。  

有关详细信息，请参阅[为客户端 PKI 证书配置设置](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureClientPKI)。  


###  <a name="BKMK_PlanningForPKITransition"></a> 规划 PKI 证书和基于 Internet 的客户端管理的过渡策略  

利用 Configuration Manager 中灵活的配置选项，可逐步过渡客户端和站点，以使用 PKI 证书帮助保护客户端端点的安全。 PKI 证书提供更好的安全性，通过它还可管理 Internet 客户端。  

由于 Configuration Manager 中配置选项数量的缘故，无法使用单一方法来转换站点以使所有客户端都使用 HTTPS 连接。 但是，可以按照下列步骤作为指导：  

1. 安装 Configuration Manager 站点并对其进行配置，使站点系统接受 HTTPS 和 HTTP 客户端连接。  

2. 配置站点属性中的“客户端计算机通信”选项卡，从而“站点系统设置”为“HTTP 或 HTTPS”，然后选择“在可用时使用 PKI 客户端证书(客户端身份验证功能)”。  有关详细信息，请参阅[为客户端 PKI 证书配置设置](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureClientPKI)。  

3. 试运行客户端证书的 PKI 推出。 有关部署示例，请参阅[为 Windows 计算机部署客户端证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012)。  

4. 使用客户端请求安装方法安装客户端。 有关详细信息，请参阅[如何使用客户端请求安装 Configuration Manager 客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)。  

5. 使用 Configuration Manager 控制台中的报表和信息来监视客户端部署和状态。  

6. 通过查看“设备”  节点的“资产和符合性”  工作区中的“客户端证书”  列，来跟踪使用客户端 PKI 证书的客户端的数目。  

    还可将 Configuration Manager HTTPS 准备情况评估工具 (cmHttpsReadiness.exe) 部署到计算机。 然后，使用这些报表查看可结合使用 Configuration Manager 和客户端 PKI 证书的计算机数量。  

   > [!NOTE]
   >  安装 Configuration Manager 客户端时，CMHttpsReadiness.exe 工具将安装在 `%windir%\CCM` 文件夹中。 运行此工具时可使用以下命令行选项：  
   > 
   > - `/Store:<name>`：此选项与 CCMCERTSTORE client.msi 属性相同  
   > - `/Issuers:<list>`：此选项与 CCMCERTISSUERS client.msi 属性相同    
   > - `/Criteria:<criteria>`：此选项与 CCMCERTSEL client.msi 属性相同    
   > - `/SelectFirstCert`：此选项与 CCMFIRSTCERT client.msi 属性相同    
   > 
   >   有关详细信息，请参阅[关于客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。  

7. 如果确信足够多的客户端成功使用其客户端 PKI 证书通过 HTTP 进行身份验证，请执行下列步骤：  

   1.  将 PKI Web 服务器证书部署到为站点运行其他管理点的成员服务器，并在 IIS 中配置该证书。 有关详细信息，请参阅[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)。  

   2.  在此服务器上安装管理点角色，并针对“HTTPS”  配置管理点属性中的“客户端连接” 选项。  

8. 进行监视并使用 HTTPS 验证具有 PKI 证书的客户端是否使用新管理点。 可使用 IIS 日志记录或性能计数器进行验证。  

9. 将其他站点系统角色重新配置为使用 HTTPS 客户端连接。 若要在 Internet 上管理客户端，请确保站点系统具有 Internet FQDN。 配置各个管理点和分发点以接受来自 Internet 的客户端连接。  

    > [!IMPORTANT]  
    >  在将站点系统角色设置为接受 Internet 连接之前，请查看基于 Internet 的客户端管理的计划信息和先决条件。 有关详细信息，请参阅[终结点之间的通信](/sccm/core/plan-design/hierarchy/communications-between-endpoints)。  

10. 扩展客户端和运行 IIS 的站点系统的 PKI 证书推出。 根据需要为 HTTPS 客户端连接和 Internet 连接设置站点系统角色。  

11. 对于最高安全性：如果确信所有客户端均正在使用客户端 PKI 证书进行身份验证和加密，请将站点属性更改为仅使用 HTTPS。  

    该计划引入 PKI 证书，首先仅通过 HTTP 进行身份验证，然后通过 HTTPS 进行身份验证和加密。 按照此计划逐步引入这些证书时，可降低客户端不受管理的风险。 此外，还可得益于 Configuration Manager 支持的最高安全性。  

##  <a name="BKMK_PlanningForRTK"></a> 规划受信任的根密钥  

 Configuration Manager 受信任的根密钥提供了一种机制供 Configuration Manager 客户端验证站点系统是否属于其层次结构。 每个站点服务器都会生成站点交换密钥以与其他站点通信。 层次结构内顶层站点中的站点交换密钥称为受信任的根密钥。  

 Configuration Manager 中受信任的根密钥的功能类似于公钥基础结构中的根证书。 由受信任的根密钥的私钥签名的任何内容，均将沿层次结构向下受到进一步信任。 客户端将受信任的根密钥的副本存储在 root\ccm\locationservices WMI 命名空间中。 

 例如，站点向管理点颁发证书，该证书使用受信任根密钥的私钥进行签名。 该站点与客户端共享其受信任的根密钥的公钥。 然后，客户可区分其层次结构中的管理点和不在其层次结构中的管理点。   

 客户端使用两种机制自动检索受信任的根密钥的公共副本：  

- 为 Configuration Manager 扩展 Active Directory 架构，并将站点发布到 Active Directory 域服务。 然后，客户端从全局目录服务器检索此站点信息。 有关详细信息，请参阅[为站点发布准备 Active Directory](/sccm/core/plan-design/network/extend-the-active-directory-schema)。  

- 使用客户端请求安装方法安装客户端时。 有关详细信息，请参阅[客户端请求安装](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation)。  

  如果客户端无法使用其中一种机制检索受信任的根密钥，则它们信任与其通信的第一个管理点提供的受信任的根密钥。 在此情况下，客户端可能会被错误地定向到攻击者的管理点，在那里，它将接收恶意管理点提供的策略。 此操作可能需由经验丰富的攻击者执行。 此攻击仅限于客户端从有效管理点检索受信任根密钥之前的短时间内发生。 为了降低攻击者将客户端错误定向到恶意管理点的风险，可为客户端预配置受信任的根密钥。  

  使用以下过程预先设置并验证 Configuration Manager 客户端的受信任的根密钥：  

- [使用受信任的根密钥和文件来预配置客户端](#bkmk_trk-provision-file)  

- [使用受信任的根密钥而不使用文件来预配置客户端](#bkmk_trk-provision-nofile)  

- [验证客户端上的受信任的根密钥](#bkmk_trk-verify)  

- [删除或替换受信任的根密钥](#bkmk_trk-reset)  

  > [!NOTE]  
  > 若客户端可从 Active Directory 域服务或客户端请求中获取受信任的根密钥，则无需预先配置它。 
  > 
  > 当客户端使用 HTTPS 与管理点进行通信时，无需预先配置受信任的根密钥。 这些客户端通过使用 PKI 证书建立信任。  


### <a name="bkmk_trk-provision-file"></a> 使用受信任的根密钥和文件来预配置客户端  

1.  在站点服务器上的文本编辑器中打开以下文件：`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  找到 SMSPublicRootKey= 条目。 复制该行中的密钥，关闭文件而不进行任何更改。  

3.  创建新文本文件，并粘贴从 mobileclient.tcf 文件中复制的密钥信息。  

4.  将此文件保存在所有计算机都可访问但可保护其不被篡改的位置。  

5.  使用接受 Client.msi 属性的任何安装方法来安装客户端。 指定以下属性：`SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    >  在客户端安装期间指定受信任的根密钥时，还要指定站点代码。 使用以下 client.msi 属性：`SMSSITECODE=<site code>`   


### <a name="bkmk_trk-provision-nofile"></a> 使用受信任的根密钥而不使用文件来预配置客户端  

1.  在站点服务器上的文本编辑器中打开以下文件：`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  找到 SMSPublicRootKey= 条目。 复制该行中的密钥，关闭文件而不进行任何更改。  

3.  使用接受 Client.msi 属性的任何安装方法来安装客户端。 指定以下 client.msi 属性：`SMSPublicRootKey=<key>`，其中 `<key>` 是从 mobileclient.tcf 复制的字符串。  

    > [!IMPORTANT]  
    >  在客户端安装期间指定受信任的根密钥时，还要指定站点代码。 使用以下 client.msi 属性：`SMSSITECODE=<site code>`   


### <a name="bkmk_trk-verify"></a>验证客户端上的受信任的根密钥  

1. 以管理员身份打开 Windows PowerShell 控制台。  

2. 运行以下命令：  

``` PowerShell
 (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
```

返回的字符串是受信任的根密钥。 验证它是否与站点服务器上 mobileclient.tcf 文件中的 SMSPublicRootKey 值匹配。  


### <a name="bkmk_trk-reset"></a>删除或替换受信任的根密钥  

 使用 client.msi 属性 RESETKEYINFORMATION = TRUE 从客户端删除受信任的根密钥。 

 若要替换受信任的根密钥，请将客户端与新的受信任根密钥一起重新安装。 例如，使用客户端请求或指定 client.msi 属性 SMSPublicRootKey。  

 有关这些安装属性的详细信息，请参阅[关于客户端安装参数和属性](/sccm/core/clients/deploy/about-client-installation-properties)。



##  <a name="BKMK_PlanningForSigningEncryption"></a> 规划签名和加密  
 
 使用 PKI 证书进行所有客户端通信时，不必规划签名和加密以帮助保护客户端数据通信。 如果将运行 IIS 的任何站点系统设置为允许 HTTP 客户端连接，请确定如何帮助保护站点客户端通信。  

 为了帮助保护客户端发送到管理点的数据，可要求客户端对数据进行签名。 还可要求使用 SHA-256 算法进行签名。 虽然此配置更安全，但除非所有客户端均支持 SHA-256，否则不需要 SHA-256。 许多操作系统都本机支持此算法，但较早的操作系统可能需要更新或修补程序。 

 签名有助于保护数据不被篡改，而加密有助于保护数据信息不被透露。 你可以对客户端在某种状态发送到管理点的清单数据和状况消息启用 3DES 加密。 无需在客户端上安装任何更新即可支持此选项。 客户端和管理点需要额外使用 CPU 以进行加密和解密。  

 有关如何配置签名和加密设置的详细信息，请参阅[配置签名和加密](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureSigningEncryption)。  



##  <a name="BKMK_PlanningForRBA"></a> 规划基于角色的管理  

 有关详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。  



## <a name="bkmk_planazuread"></a> 规划 Azure Active Directory

 Configuration Manager 与 Azure Active Directory (Azure AD) 集成，使站点和客户端能够使用新式身份验证。 使用 Azure AD 载入站点时，支持以下 Configuration Manager 方案：

**客户端**  

- [通过云管理网关在 Internet 上管理客户端](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

- [管理已加入云域的设备](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

- [共同管理](/sccm/core/clients/manage/co-management-overview)  

- [部署用户可用的应用](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [适用于企业的 Microsoft Store 联机应用](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

- 降低基础结构要求。 例如，[使用管理点的软件中心](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex)而不是应用程序目录  

- [管理 Office 365 应用](/sccm/sum/deploy-use/manage-office-365-proplus-updates)  


**服务器**  

- [升级就绪情况](/sccm/core/clients/manage/upgrade-readiness)  

- [Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics)  

- [Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  

- [社区中心](/sccm/core/get-started/capabilities-in-technical-preview-1807#bkmk_hub)  

- [云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- [用户发现](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  


 有关将站点连接到 Azure AD 的详细信息，请参阅[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)。


 有关 Azure AD 的详细信息，请参阅 [Azure Active Directory 文档](https://docs.microsoft.com/azure/active-directory/)。



## <a name="bkmk_auth"></a> 规划 SMS 提供程序的身份验证
<!--1357013--> 

从版本 1810 开始，可以为管理员指定访问 Configuration Manager 站点的最低身份验证级别。 此功能强制管理员以要求的级别登录到 Windows。 它适用于访问 SMS 提供程序的所有组件。 例如，Configuration Manager 控制台、SDK 方法和 Windows PowerShell cmdlet。 

此配置是层次结构范围的设置。 更改此设置前，请确保所有 Configuration Manager 管理员都能够使用所需的身份验证级别登录到 Windows。 

可用的级别如下：

- **Windows 身份验证**：要求使用 Active Directory 域凭据进行身份验证。   

- **证书身份验证**：要求使用由受信任的 PKI 证书颁发机构颁发的有效证书进行身份验证。  

- **Windows Hello 企业版身份验证**：要求使用与设备关联并采用生物识别或 PIN 的强双因素身份验证进行身份验证。  

有关详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth)。 



## <a name="see-also"></a>另请参阅
- [Configuration Manager 客户端的安全和隐私](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [配置安全性](/sccm/core/plan-design/security/configure-security)  

- [终结点之间的通信](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [加密控制技术参考](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  

- [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)  

