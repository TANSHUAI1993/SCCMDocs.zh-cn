---
title: "规划 System Center Configuration Manager 中的安全性"
description: "获取 System Center Configuration Manager 中安全相关的最佳安全方案和其他信息。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f38d7275a39d16f9e6cf90334a46668fcc860bc1


---
# <a name="plan-for-security-in-system-center-configuration-manager"></a>规划 System Center Configuration Manager 中的安全性

*适用范围：System Center Configuration Manager (Current Branch)*

使用本主题中的信息来帮助规划 System Center Configuration Manager 中的安全性。  

   有关 Configuration Manager 如何使用证书和加密控件的详细信息，请参阅 [System Center Configuration Manager 的加密控件技术参考](../../../protect/deploy-use/cryptographic-controls-technical-reference.md)。  


##  <a name="a-namebkmkplanningforcertificatesa-planning-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> 规划证书（自签名和 PKI）  
 Configuration Manager 组合使用自签名证书和公钥基础结构 (PKI) 证书。  

 作为最佳安全方案，请尽可能使用 PKI 证书。 有关 PKI 证书要求的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../core/plan-design/network/pki-certificate-requirements.md)。 Configuration Manager 请求 PKI 证书时，如在移动设备注册和 AMT 设置过程中，必须使用 Active Directory 域服务和企业证书颁发机构。 对于其他 PKI 证书，必须独立于 Configuration Manager 部署和管理它们。  

 当客户端计算机连接到基于 Internet 的站点系统时也需要 PKI 证书，建议在客户端连接到运行 Internet Information Services (IIS) 的站点系统时使用这些证书。 有关客户端通信的详细信息，请参阅 [如何在 System Center Configuration Manager 中配置客户端通信端口](../../../core/clients/deploy/configure-client-communication-ports.md)。  

 使用 PKI 时，也可以使用 IPsec 帮助保护站点中站点系统之间以及站点之间的服务器对服务器通信，并且可将其用于在计算机之间传输数据的任何其他情况。 必须独立于 Configuration Manager 来配置和实现 IPsec。  

 PKI 证书不可用时，Configuration Manager 可以自动生成自签名证书，Configuration Manager 中的某些证书始终是自签名证书。 在某些情况下，Configuration Manager 会自动管理自签名证书，不必采取任何其他操作。 一个可能的例外是站点服务器签名证书。 站点服务器签名证书始终是自签名证书，它可以确保从站点服务器发送客户端从管理点下载的客户端策略，并且客户端策略未被篡改。  

### <a name="planning-for-the-site-server-signing-certificate-self-signed"></a>规划站点服务器签名证书（自签名）  
 客户端可以从 Active Directory 域服务和客户端请求安装中安全地获取站点服务器签名证书的副本。 如果客户端无法使用其中一种机制获取站点服务器签名证书的副本，那么作为最佳安全方案，请在安装客户端时安装站点服务器签名证书的副本。 如果客户端与站点的首次通信通过 Internet 进行，那么这非常重要，因为管理点连接至不受信任的网络，因此易受到攻击。 如果未采取此额外步骤，则客户端会自动从管理点中下载站点服务器签名证书的副本。  

 客户端无法安全地获取站点服务器证书副本的情况包括：  

-   未使用客户端请求来安装客户端，并且下列条件成立：  

    -   未针对 Configuration Manager 扩展 Active Directory 架构。  

    -   客户端的站点未发布到 Active Directory 域服务。  

    -   客户端来自不受信任的林或工作组。  

-   当客户端在 Internet 上时安装客户端。  

使用以下过程与站点服务器签名证书的副本一起安装客户端。  

##### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>安装客户端与站点服务器签名证书的副本  

1.  在客户端的主站点服务器上找到站点服务器签名证书。 此证书存储在“SMS”  证书存储中，并且具有“站点服务器”  使用者名称以及“站点服务器签名证书” 友好名称。  

2.  导出无私钥的证书，安全地存储文件并从受保护的通道中访问它（例如，通过使用 SMB 签名或 IPsec）。  

3.  将 Client.msi 属性 **SMSSIGNCERT=**&lt;完整路径和文件名\> 与 CCMSetup.exe 配合使用来安装客户端。  

###  <a name="a-namebkmkplanningforcrlsa-planning-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> 规划 PKI 证书吊销  
将 PKI 证书用于 Configuration Manager 时，请规划客户端和服务器是否将使用证书吊销列表 (CRL) 来验证连接计算机上的证书以及如何进行。 证书吊销列表 (CRL) 是证书颁发机构 (CA) 创建和签署的文件，其中包含已经发放但被吊销的证书的列表。 CA 管理员可以吊销证书，例如，发放的证书已知或者被怀疑已遭篡改。  

> [!IMPORTANT]  
>  因为在 CA 颁发证书时已经将 CRL 的位置添加到证书中，所以请确保在部署 Configuration Manager 将使用的任何 PKI 证书之前先规划 CRL。  

默认情况下，IIS 始终会检查 CRL 中是否有客户端证书，且无法在 Configuration Manager 中更改此配置。 默认情况下，Configuration Manager 客户端始终检查 CRL 中是否有站点系统；但是，可通过指定站点属性和指定 CCMSetup 属性来禁用此设置。 对基于 Intel AMT 的计算机进行带外管理时，也可以针对带外服务点和运行带外管理控制台的计算机启用 CRL 检查。  

如果计算机使用证书吊销检查，但计算机无法找到 CRL，则计算机的行为方式好像是吊销了证书链中的所有证书一样，因为无法验证列表中是否缺少这些证书。 在此情况下，需要证书并使用 CRL 的所有连接都将失败。  

如果在每次使用证书时都检查 CRL，则能更好地抵御因使用已吊销的证书而造成的安全威胁，但这样做会使连接出现延迟，并在客户端上引发额外的处理操作。 当客户端在 Internet 上或在不受信任的网络上时，你很有可能需要此附加安全性检查。  

在确定 Configuration Manager 客户端是否必须检查 CRL 之前先咨询 PKI 管理员，然后在以下条件都成立时考虑在 Configuration Manager 中启用此选项：  

-   你的 PKI 基础结构支持 CRL，并且其已发布到所有 Configuration Manager 客户端都可以找到它的位置。 请记住，这可能包括 Internet 上的客户端（如果你正在使用基于 Internet 的客户端管理）和不受信任的林中的客户端。  

-   对配置为使用 PKI 证书的每个站点系统连接检查 CRL 的要求大于在客户端上进行较快连接以及有效处理的要求，并且也大于无法连接到服务器的客户端的风险（如果服务器找不到 CRL）。  

###  <a name="a-namebkmkplanningforrootcasa-planning-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> 规划 PKI 受信任的根证书和证书颁发者列表  
如果 IIS 站点系统使用 PKI 客户端证书通过 HTTP 进行客户端身份验证，或者通过 HTTPS 进行客户端身份验证和加密，则可能必须以站点属性形式导入根 CA 证书。 这两个方案如下：  

-   使用 Configuration Manager 部署操作系统，管理点仅接受 HTTPS 客户端连接。  

-   使用的 PKI 客户端证书未链接至管理点信任的根证书颁发机构 (CA) 证书。  

    > [!NOTE]  
    >  如果从发放用于管理点的服务器证书的同一 CA 层次结构中发放客户端 PKI 证书，则不必指定此根 CA 证书。 但是，如果使用多个 CA 层次结构，并且不确定它们彼此是否信任，请导入客户端的 CA 层次结构的根 CA。  

如果必须为 Configuration Manager 导入根 CA 证书，请从颁发证书的 CA 中或从客户端计算机中导出它们。 如果从颁发证书的 CA（也为根 CA）中导出证书，请确保未导出私钥。 将导出的证书文件存储在安全的位置，以防止篡改。 配置站点时，你必须能够访问文件，因此，如果通过网络访问文件，请确保使用 SMB 签名或 IPsec 来防止通信被篡改。  

如果续订了导入的任何根 CA 证书，则必须导入续订的证书。  

这些导入的根 CA 证书和每个管理点的根 CA 证书会创建证书颁发者列表，Configuration Manager 通过以下方式使用该列表：  

-   客户端连接到管理点时，管理点会验证客户端证书是否链接至站点证书颁发者列表中的受信任的根证书。 如果没有，则拒绝证书，并且 PKI 连接失败。  

-   当客户端选择 PKI 证书时，如果它们具有证书颁发者列表，则它们会选择链接至证书颁发者列表中受信任的根证书的证书。 如果不匹配，则客户端不选择 PKI 证书。 有关客户端证书处理的详细信息，请参阅本主题中的 [Planning for PKI client certificate selection](#BKMK_PlanningForClientCertificateSelection) 部分。  

注册移动设备或 Mac 计算机时，以及针对无线网络设置基于 Intel AMT 的计算机时，你可能也必须导入根 CA 证书，这与站点配置无关。  

###  <a name="a-namebkmkplanningforclientcertificateselectiona-planning-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> Planning for PKI client certificate selection  
 如果 IIS 站点系统使用 PKI 客户端证书通过 HTTP 进行客户端身份验证，或者通过 HTTPS 进行客户端身份验证和加密，请规划基于 Windows 的客户端选择要用于 Configuration Manager 的证书的方式。  

> [!NOTE]  
>  并非所有设备都支持证书选择方法，而是会自动改为选择满足证书要求的第一个证书。 例如，Mac 计算机上的客户端和移动设备不支持证书选择方法。  

在许多情况下，采用默认配置和行为就行了。 基于 Windows 的计算机上的 Configuration Manager 客户端使用下列条件筛选多个证书：  

1.  证书颁发者列表：证书链接至管理点信任的根 CA。  

2.  证书在“个人” 默认证书存储中。  

3.  该证书有效、没有被吊销，并且尚未过期。 有效性检查包括验证私钥是否可访问，是否未使用证书模板版本 3 创建证书，该版本与 Configuration Manager 不兼容。  

4.  证书具有客户端身份验证功能，或者已发放给计算机名。  

5.  证书具有最长有效期。  

可以使用下列机制将客户端配置为使用证书颁发者列表：  

-   以 Configuration Manager 站点信息形式将其发布到 Active Directory 域服务。  

-   使用客户端请求安装客户端。  

-   将客户端成功分配给其站点之后，客户端从管理点下载它。  

-   在客户端安装过程中将其指定为 CCMCERTISSUERS 的 CCMSetup client.msi 属性。  

如果在首次安装客户端时客户端没有证书颁发者列表，并且尚未将其分配给站点，则它们会跳过此检查。 如果它们有证书颁发者列表，但没有链接至证书颁发者列表中的受信任根证书的 PKI 证书，则证书选择将失败，并且客户端不会继续使用其他证书选择条件。  

在大多数情况下，Configuration Manager 客户端会正确标识要使用的唯一适合的 PKI 证书。 但是，当情况不是这样，而是根据客户端身份验证功能选择证书时，你可以配置下列两种替代选择方法：  

-   在客户端证书的“使用者名称”中进行部分字符串匹配。 如果你在主题字段中使用计算机的完全限定的域名 (FQDN) 并且想基于域后缀选择证书，则此不区分大小写的匹配很适用，例如 **contoso.com**。 但是，你可以使用此选择方法在证书使用者名称中标识任何连续字符串，以将此证书与客户端证书存储中的其他证书区分开来。  

    > [!NOTE]  
    >  你无法将使用者可选名称 (SAN) 部分字符串匹配用作站点设置。 虽然可以使用 CCMSetup 为 SAN 指定部分字符串匹配，但在下列情况下将由站点属性对其进行覆盖：  
    >   
    >  -   客户端检索发布到 Active Directory 域服务的站点信息。  
    > -   使用客户端请求安装方式安装的客户端。  
    >   
    >  仅当手动安装客户端以及客户端未从 Active Directory 域服务中检索到站点信息时，才在 SAN 中使用部分字符串匹配。 例如，这些条件适用于仅 Internet 客户端。  

-   匹配客户端证书“使用者名称”属性值或“使用者可选名称 (SAN)”属性值。 该匹配区分大小写，当你使用符合 RFC 3280 标准的 X500 可分辨名称或同等 OID（对象标识符），并希望根据属性值选择证书时适用。 你可以仅指定唯一识别或验证证书并使证书与证书存储中其他证书区别开来所需的属性及其值。  

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

如果应用了选择条件之后找到了多个合适的证书，则可以替代默认配置以选择有效期最长的证书，并改为指定不选择证书。 在此情况下，客户端将无法使用 PKI 证书与 IIS 站点系统通信。 客户端将向分配的回退状态点发送一则错误消息，警告你证书选择失败，以便你可以修改或改进证书选择条件。 客户端行为则取决于失败的连接是通过 HTTPS 还是 HTTP 进行的。  

-   如果失败的连接是通过 HTTPS 进行的：客户端会尝试通过 HTTP 进行连接并使用客户端自签名证书。  

-   如果失败的连接是通过 HTTP 进行的：客户端会通过使用自签名的客户端证书尝试通过 HTTP 进行另一个连接。  

为了帮助标识唯一的 PKI 客户端证书，你也可以指定自定义存储，而不是在“计算机”  存储中指定“个人”  默认值。 但是，必须独立于 Configuration Manager 创建此存储，并且必须能够将证书部署到此自定义存储并在有效期到期之前续订证书。  

有关如何配置客户端证书设置的信息，请参阅[配置 System Center Configuration Manager 中的安全性](../../../core/plan-design/security/configure-security.md)主题中的[为客户端 PKI 证书配置设置](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI)部分。  

###  <a name="a-namebkmkplanningforpkitransitiona-planning-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> 规划 PKI 证书和基于 Internet 的客户端管理的过渡策略  
利用 Configuration Manager 中灵活的配置选项，可逐步过渡客户端和站点，以使用 PKI 证书帮助保护客户端端点的安全。 PKI 证书提供了更佳的安全性，当客户端在 Internet 上时，可以利用这些证书管理客户端。  

由于 Configuration Manager 中配置选项数量的缘故，因此无法使用单一方法来过渡站点以使所有客户端都使用 HTTPS 连接。 但是，可以按照下列步骤作为指导：  

1.  安装 Configuration Manager 站点并对其进行配置，使站点系统接受 HTTPS 和 HTTP 客户端连接。  

2.  配置站点属性中的“客户端计算机通信”  选项卡，以便“站点系统设置”  为“HTTP 或 HTTPS” ，然后选择“在可用时使用 PKI 客户端证书(客户端身份验证功能)”  复选框。 配置该选项卡中所需的任何其他设置。 有关详细信息，请参阅[配置 System Center Configuration Manager 中的安全性](../../../core/plan-design/security/configure-security.md)主题中的[为客户端 PKI 证书配置设置](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI)部分。  

3.  试运行客户端证书的 PKI 推出。 有关示例部署，请参阅[System Center Configuration Manager 的 PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)主题中的为 Windows 计算机部署客户端证书部分。  

4.  使用客户端请求安装方法安装客户端。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 Windows 计算机](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)主题中的[如何使用客户端请求安装 Configuration Manager 客户端](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)部分。  

5.  使用 Configuration Manager 控制台中的报表和信息来监视客户端部署和状态。  

6.  通过查看“设备”  节点的“资产和符合性”  工作区中的“客户端证书”  列，来跟踪使用客户端 PKI 证书的客户端的数目。  

     也可以将 Configuration Manager HTTPS 准备情况评估工具 (**cmHttpsReadiness.exe**) 部署到计算机，并使用报表查看可以将客户端 PKI 证书用于 Configuration Manager 的计算机数量。  

    > [!NOTE]  
    >  当 Configuration Manager 客户端安装在客户端计算机上时，**cmHttpsReadiness.exe** 工具将安装在 %windir%**\CCM** 文件夹中。 在客户端上运行此工具时，你可以指定下列选项：  
    >   
    >  -   /Store：&lt;名称\>  
    > -   /Issuers：&lt;列表\>  
    > -   /Criteria：&lt;条件\>  
    > -   /SelectFirstCert  
    >   
    >  这些选项会分别映射到 **CCMCERTSTORE**、 **CCMCERTISSUERS**、 **CCMCERTSEL**和 **CCMFIRSTCERT** Client.msi 属性。 有关这些选项的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

7.  当你确信足够数目的客户端正在成功使用其客户端 PKI 证书通过 HTTP 进行身份验证时，请执行下列操作：  

    1.  将 PKI Web 服务器证书部署到将为站点运行其他管理点的成员服务器，并在 IIS 中配置该证书。 有关详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)主题中的*为运行 IIS 的站点系统部署 Web 服务器证书*部分。  

    2.  在此服务器上安装管理点角色，并针对“HTTPS”  配置管理点属性中的“客户端连接” 选项。  

8.  进行监视并使用 HTTPS 验证具有 PKI 证书的客户端是否使用新管理点。 你可以使用 IIS 日志记录或性能计数器来验证这一点。  

9. 将其他站点系统角色重新配置为使用 HTTPS 客户端连接。 如果想要管理 Internet 上的客户端，请确保站点系统具有 Internet FQDN，并将单独的管理点和分发点配置为接受 Internet 中的客户端连接。  

    > [!IMPORTANT]  
    >  在将站点系统角色配置为接受 Internet 连接之前，请查看基于 Internet 的客户端管理的计划信息和先决条件。 有关详细信息，请参阅 [System Center Configuration Manager 中终结点之间的通信](../../../core/plan-design/hierarchy/communications-between-endpoints.md)。  

10. 针对客户端和运行 IIS 的站点系统扩展 PKI 证书推出，并根据需要配置 HTTPS 客户端连接和 Internet 连接的站点系统角色。  

11. 对于最高的安全性：当你确信所有的客户端正使用客户端 PKI 证书进行身份验证和加密时，将此站点属性更改为仅使用 HTTPS。  

 如果按照此计划逐渐引入 PKI 证书（首先针对仅通过 HTTP 进行的身份验证，然后针对通过 HTTPS 进行的身份验证和加密），则可以减少客户端不受管理的风险。 此外，将得益于 Configuration Manager 支持的最高安全性。  

##  <a name="a-namebkmkplanningforrtka-planning-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> 规划受信任的根密钥  
Configuration Manager 受信任的根密钥提供了一种机制供 Configuration Manager 客户端验证站点系统是否属于其层次结构。 每个站点服务器都会生成站点交换密钥以与其他站点通信。 层次结构内顶层站点中的站点交换密钥称为受信任的根密钥。  

Configuration Manager 中受信任的根密钥的功能类似于公钥基础结构中的根证书，因为将沿层次结构向下进一步信任受信任根密钥的私钥所签名的任何内容。 例如，通过使用受信任的根密钥对的私钥对管理点证书进行签名，并复制可供客户端使用的受信任根密钥对的私钥，客户端可以区分位于其层次结构中的管理点以及不在其层次结构中的管理点。 客户端使用 WMI 将受信任的根密钥的副本存储在命名空间 **root\ccm\locationservices**中。  

客户端可以使用两种机制自动检索受信任的根密钥的公共副本：  

-   为 Configuration Manager 扩展 Active Directory 架构，并将站点发布到 Active Directory 域服务，客户端可以从全局目录服务器中检索此站点信息。  

-   使用客户端请求安装客户端。  

如果客户端无法使用其中一种机制检索受信任的根密钥，则它们信任与其通信的第一个管理点提供的受信任的根密钥。 在此情况下，客户端可能会被错误地定向到攻击者的管理点，在那里，它将接收恶意管理点提供的策略。 这可能是经验丰富的攻击者执行的操作，并且可能仅在客户端从有效管理点中接收受信任的根密钥之前的有限时间内发生。 但是，为了降低攻击者将客户端错误定向到未恶意管理点的风险，你可以使用受信任的根密钥来预先设置客户端。  

使用以下过程预先设置并验证 Configuration Manager 客户端的受信任的根密钥：  

-   使用受信任的根密钥和文件来预先设置客户端。  

-   使用受信任的根密钥而不使用文件来预先设置客户端。  

-   验证客户端上的受信任的根密钥。  

> [!NOTE]  
>  如果客户端可以从 Active Directory 域服务中获取受信任的根密钥，或者客户端是使用客户端请求安装的，则不必使用受信任的根密钥来预先设置客户端。 此外，当客户端使用 HTTPS 与管理点通信时，则不必预先设置客户端，因为使用 PKI 证书建立了信任。  

你可以将 Client.msi 属性 **RESETKEYINFORMATION = TRUE** 与 CCMSetup.exe 配合使用，以从客户端删除受信任的根密钥。 若要替换受信任的根密钥，请将客户端与新的受信任的根密钥一起重新安装，例如，通过使用客户端请求，或者通过使用 CCMSetup.exe 来指定 Client.msi **SMSPublicRootKey** 属性。  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a>使用文件预先设置客户端和受信任的根密钥  

1.  在文本编辑器中，打开文件 &lt;Configuration Manager 目录\>**\bin\mobileclient.tcf**。  

2.  找到 **SMSPublicRootKey=**条目，复制该行中的密钥，关闭文件而不进行任何更改。  

3.  创建新文本文件，并粘贴从 mobileclient.tcf 文件中复制的密钥信息。  

4.  保存此文件并将其放在所有计算机都可以访问它的某个位置，但保护此文件以防止篡改。  

5.  使用接受 Client.msi 属性的任何安装方法来安装客户端，并指定 Client.msi 属性 **SMSROOTKEYPATH=**&lt;完整路径和文件名\>。  

    > [!IMPORTANT]  
    >  在客户端安装期间为增加安全性而指定受信任的根密钥时，还必须使用 Client.msi 属性 **SMSSITECODE=&lt;站点代码\>** 来指定站点代码。  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a>不使用文件来预先设置客户端和受信任的根密钥  

1.  在文本编辑器中，打开文件 &lt;Configuration Manager 目录\>**\bin\mobileclient.tcf**。  

2.  找到 SMSPublicRootKey= 条目，记录该行中的密钥或者将其复制到剪贴板，然后关闭文件而不进行任何更改。  

3.  使用接受 Client.msi 属性的任何安装方法来安装客户端，并指定 Client.msi 属性 **SMSPublicRootKey=**&lt;密钥\>，其中 &lt;密钥\> 是从 mobileclient.tcf 中复制的字符串。  

    > [!IMPORTANT]  
    >  在客户端安装期间为增加安全性而指定受信任的根密钥时，还必须使用 Client.msi 属性 **SMSSITECODE=&lt;站点代码\>** 来指定站点代码  

#### <a name="to-verify-the-trusted-root-key-on-a-client"></a>验证客户端上的受信任的根密钥  

1.  在“启动”  菜单上，单击“运行” ，然后键入 **Wbemtest**。  

2.  在“Windows Management Instrumentation 测试器”  对话框中，单击“连接” 。  

3.  在“连接”  对话框中，在“命名空间”  框中键入 **root\ccm\locationservices**，然后单击“连接” 。  

4.  在“Windows Management Instrumentation 测试器”  对话框内的“IWbemServices”  部分中，单击“枚举类” 。  

5.  在“超类信息”  对话框中，选择“递归” ，然后单击“确定” 。  

6.  在“查询结果”  窗口中，滚动到列表末尾，然后双击“TrustedRootKey ()” 。  

7.  在“TrustedRootKey 的对象编辑器”  对话框中，单击“实例” 。  

8.  在显示“TrustedRootKey”实例的新“查询结果”窗口中，双击“TrustedRootKey=@”   

9. 在“TrustedRootKey=@对象编辑器”对话框内的“属性”部分中，向下滚动到“TrustedRootKey CIM_STRING”。 右列中的字符串是受信任的根密钥。 验证它是否与文件 &lt;Configuration Manager 目录\>**\bin\mobileclient.tcf** 中的 **SMSPublicRootKey** 值匹配。  

##  <a name="a-namebkmkplanningforsigningencryptiona-planning-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> 规划签名和加密  
 使用 PKI 证书进行所有客户端通信时，不必规划签名和加密以帮助保护客户端数据通信。 但是，如果将运行 IIS 的任何站点系统配置为允许 HTTP 客户端连接，则必须确定如何帮助保护站点客户端通信。  

 为了帮助保护客户端发送到管理点的数据，你可以要求对数据进行签名。 此外，你可以要求使用 SHA-256 算法对使用 HTTP 的客户端中所有已签名数据进行签名。 虽然此设置更安全，但除非所有客户端都支持 SHA-256，否则不要启用此选项。 许多操作系统都本机支持 SHA-256，但较早的操作系统可能需要更新或修补程序。 例如，运行 Windows Server 2003 SP2 的计算机必须安装 [知识库文章 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666)中引用的修补程序。  

 而签名有助于保护数据不被篡改，加密有助于保护数据信息不被透露。 你可以对客户端在某种状态发送到管理点的清单数据和状况消息启用 3DES 加密。 你不必在客户端上安装任何更新来支持此选项，但要考虑客户端和管理点上将需要的其他 CPU 使用率以执行加密和解密。  

 有关如何配置签名和加密设置的信息，请参阅[配置 System Center Configuration Manager 中的安全性](../../../core/plan-design/security/configure-security.md)主题中的[配置签名和加密](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption)部分。  

##  <a name="a-namebkmkplanningforrbaa-planning-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> 规划基于角色的管理  
 有关此信息，请参阅 [System Center Configuration Manager 基于角色的管理基础](../../../core/understand/fundamentals-of-role-based-administration.md)。  



<!--HONumber=Nov16_HO1-->


