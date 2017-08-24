---
title: "客户端安全和隐私 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中客户端的安全和隐私。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
caps.latest.revision: "10"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1d871b0e1a2897c236d17211a23c9c7d93e42313
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-clients-in-system-center-configuration-manager"></a>System Center Configuration Manager 中客户端的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*

本文包含 System Center Configuration Manager 中的客户端以及 Exchange Server 连接器所管理的移动设备的安全和隐私信息：  

##  <a name="BKMK_Security_Cliients"></a>客户端的最佳安全方案  
 当 Configuration Manager 从运行 Configuration Manager 客户端的设备接受数据时，这将带来客户端可能会攻击站点的风险。 例如，它们会发送格式不正确的清单或尝试将站点系统过载。 仅将 Configuration Manager 客户端部署到信任的设备。 此外，使用下列最佳安全方案来帮助站点免遭未授权或被侵害的设备威胁：  

 **使用公钥基础结构 (PKI) 证书与运行 IIS 的站点系统建立客户端通信。**  

-   作为站点属性，将“站点系统设置”  配置为“仅 HTTPS” 。  

-   安装具有 **/UsePKICert** CCMSetup 属性的客户端  

-   使用证书吊销列表 (CRL) 并确保客户端和通信服务器可以始终访问该列表。  

 对于 Internet 上的移动设备客户端和客户端计算机连接（分发点除外），这些证书必不可少，建议对 Intranet 上的所有客户端连接也使用这些证书。  

 有关 PKI 证书要求以及证书如何用于帮助保护 Configuration Manager 的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

 **自动批准受信任域的客户端计算机并手动检查和批准其他计算机**  

 你可以配置为对层次结构进行手动批准、对受信任域中的计算机进行自动批准，或者对所有计算机进行自动批准。 最安全的批准方法是自动批准作为受信任域成员的客户端，然后手动检查和批准所有其他计算机。 不建议自动批准所有客户端，除非您具有其他访问控制来避免不受信任的计算机访问您的网络。  

 在无法使用 PKI 身份验证时，“批准”将标识出由 Configuration Manager 管理的受信任计算机。  

 有关如何手动批准计算机的详细信息，请参阅[通过“设备”节点管理客户端](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)。  

 **请勿依赖阻止来防止客户端访问 Configuration Manager 层次结构**  

 Configuration Manager 基础结构会拒绝被阻止的客户端，使它们无法与站点系统通信，从而无法下载策略、上载清单数据或者发送状况或状态消息。 但是，当站点系统接受 HTTP 客户端连接时，请勿依赖阻止来保护 Configuration Manager 层次结构免遭不受信任计算机的威胁。 在此方案中，被阻止的客户端可以使用新的自签名证书和硬件 ID 重新加入该站点。 “阻止”旨在当你将操作系统部署到客户端并且所有站点系统均接受 HTTPS 客户端连接时用于阻止丢失或受侵害的启动媒体。 如果你使用公钥基础结构 (PKI) 并且它支持证书吊销列表 (CRL)，则始终考虑将证书吊销作为预防证书泄漏的主要防线。 在 Configuration Manager 中阻止客户端为保护层次结构提供第二道防线。  

 有关详细信息，请参阅[确定是否在 System Center Configuration Manager 中阻止客户端](../../../../core/clients/deploy/plan/determine-whether-to-block-clients.md)。  

 **使用对于环境较为实用并且最为安全的客户端安装方法：**  

-   对于域计算机，组策略客户端安装和基于软件更新的客户端安装方法比客户端请求安装更为安全。  

-   如果你应用访问控件和更改控件，则映像安装和手动安装会非常安全。  

 对于所有客户端安装方法，客户端请求安装最不安全，因为它有许多依赖性，包括本地管理权限、Admin$ 共享和许多防火墙异常。 这些依赖性将增加你的攻击面。  

 有关不同客户端安装方法的详细信息，请参阅 [System Center Configuration Manager 中的客户端安装方法](../../../../core/clients/deploy/plan/client-installation-methods.md)。  

 此外，尽可能在 Configuration Manager 中选择要求最少安全权限的客户端安装方法，并限制具有分配的安全角色（有权实现除客户端部署外的其他意图）的管理用户。 例如，自动客户端升级要求具有“完全权限管理员”  安全角色，该角色将授予管理用户所有安全权限。  

 有关每个客户端安装方法所需的依赖项和安全权限的详细信息，请参阅[计算机客户端先决条件](../../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers)中的“安装方法依赖关系”。  

 **如果必须使用客户端请求安装，请采取附加步骤来确保客户端请求安装帐户安全**  

 尽管该帐户必须为将安装 Configuration Manager 客户端软件的每个计算机上的本地“管理员”组的成员，永远不要将客户端请求安装帐户添加到域管理员”组。 相反，创建全局组并将该全局组添加到你的客户端计算机上的本地“管理员”  组。 你还可以创建组策略对象以添加受限制的组设置，从而将客户端请求安装帐户添加到本地“管理员”  组。  

 为实现附加的安全性，创建多个客户端请求安装帐户，每个帐户均具有对有限个数的计算机的管理权限，以便在一个帐户受到侵害时，只会损害该帐户能够访问的客户端计算机。  

 **在创建客户端计算机映像前删除证书**  

 如果计划通过运用映像技术来部署客户端，请始终在捕获映像前删除证书，如包括客户端身份验证和自签名证书的 PKI 证书。 如果你不删除这些证书，则客户端可能会相互模拟并且你将无法为每个客户端验证数据。  

 有关使用 Sysprep 准备计算机进行映像的详细信息，请参阅你的 Windows 部署文档。  

 **确保 Configuration Manager 计算机客户端获得这些证书的授权副本：**  

-   Configuration Manager 信任的根密钥  

     如果尚未为 Configuration Manager 扩展 Active Directory 架构，并且客户端在与管理点通信时未使用 PKI 证书，则客户端将依赖 Configuration Manager 的受信任根密钥来验证有效管理点的身份。 在这种情况下，除非管理点使用受信任的根密钥，否则客户端无法验证这些管理点是否为该层次结构的受信任管理点。 如果没有受信任的根密钥，则技能较高的攻击者可以将客户端导向未授权的管理点。  

     当客户端无法从全局目录或者使用 PKI 证书下载 Configuration Manager 的受信任根密钥时，使用受信任的根密钥来预设置客户端，以确保无法将它们导向未授权的管理点。 有关详细信息，请参阅 [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

-   站点服务器签名证书  

     客户端使用站点服务器签名证书来验证站点服务器是否已将它们从管理点下载的客户端策略签名。 此证书由站点服务器自签名并将发布到 Active Directory 域服务。  

     当客户端无法从全局目录下载站点服务器签名证书时，默认情况下，它们会从管理点下载该证书。 当管理点面临不受信任的网络（如 Internet）时，在客户端上手动安装站点服务器签名证书，以确保它们无法运行已在受侵害的管理点中篡改的客户端策略。  

     若要手动安装站点服务器签名证书，请使用 CCMSetup 的 client.msi 属性 **SMSSIGNCERT**。 有关详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../../core/clients/deploy/about-client-installation-properties.md)。  

 **如果客户端将从其接触的首个管理点下载受信任的根密钥，则请勿使用自动站点分配**  

 此最佳安全方案与上述条目有关。 为规避新客户端从未授权的管理点下载受信任的根密钥的风险，请仅在下列情况中使用自动站点分配：  

-   客户端可以访问发布到 Active Directory 域服务的 Configuration Manager 站点信息。  

-   使用受信任的根密钥来预设置客户端。  

-   使用企业证书颁发机构颁发的 PKI 证书来建立客户端和管理点之间的信任。  

 有关受信任的根密钥的详细信息，请参阅 [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

 **使用 CCMSetup Client.msi 选项 SMSDIRECTORYLOOKUP=NoWINS 安装客户端计算机**  

 可供客户端查找站点和管理点的最安全的服务定位方法是使用 Active Directory 域服务。 如果无法做到这点（例如，由于无法为 Configuration Manager 扩展 Active Directory 架构，或客户端位于不受信任的林或工作组中），则可以将 DNS 发布用作备用服务定位方法。 如果未能采用这两个方法，则在未针对 HTTPS 客户端连接配置管理点时，客户端可以回退到使用 WINS。  

 由于其他发布方法比发布到 WINS 更为安全，因此通过指定 SMSDIRECTORYLOOKUP=NoWINS，将客户端计算机配置为不会回退到使用 WINS。 如果必须使用 WINS 进行服务定位，请使用 SMSDIRECTORYLOOKUP=WINSSECURE（默认设置），它将使用 Configuration Manager 受信任根密钥来验证管理点的自签名证书。  

> [!NOTE]  
>  当针对 SMSDIRECTORYLOOKUP=WINSSECURE 配置客户端并从 WINS 中找到管理点时，客户端将检查它在 WMI 中的 Configuration Manager 受信任根密钥副本。 如果管理点证书上的签名与客户端的受信任根密钥的副本相匹配，则将验证证书，并且客户端将与其使用 WINS 找到的管理点通信。 如果管理点证书上的签名与客户端的受信任根密钥的副本不匹配，则证书无效，并且客户端将不会与其使用 WINS 找到的管理点通信。  

 **确保维护时段足够大以部署关键的软件更新**  

 可为设备集合配置维护时段，以限制 Configuration Manager 可在这些设备上安装软件的次数。 如果你将该维护时段配置得太小，则客户端可能无法安装关键的软件更新，这使客户端容易遭受可由软件更新减轻的攻击。  

 **对于具有写入筛选器的 Windows Embedded 设备，如果 Configuration Manager 禁用写入筛选器以保留软件安装和更改，请采取附加安全措施以减少攻击面**  

 当在 Windows Embedded 设备中启用写入筛选器后，将仅对覆盖区进行任何软件安装或更改，并且在设备重启后不会保留。 如果使用 Configuration Manager 来临时禁用写入筛选器以保留软件安装和更改，则在此期间，嵌入式设备会易于面临所有卷（这包括共享文件夹）均被更改的情况。  

 尽管 Configuration Manager 在此期间将锁定计算机以仅允许本地管理员登录，但仍要尽可能采取附加安全措施以便保护计算机。 例如，在防火墙上启用额外限制并从网络中断开设备。  

 如果你使用维护时段来保留更改，请仔细计划这些时段以最大限度缩短可能禁用写入筛选器的时间，但是时间长度应足够使软件安装和重启完成。  

 **如果你使用基于软件更新的客户端安装并在站点上安装更高的客户端版本，请更新在软件更新点发布的软件更新以便客户端收到最新版本**  

 如果你在站点上安装更高的客户端版本，例如，升级站点，则不会自动更新发布到软件更新点的客户端部署的软件更新。 必须将 Configuration Manager 客户端重新发布到软件更新点，然后单击“是”以更新版本号。  

 有关详细信息，请参阅[如何使用基于软件更新的安装来安装 Configuration Manager 客户端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP)中的部“将 Configuration Manager 客户端发布到软件更新点”。  

 **仅对于受信任并具有受限制的物理访问的计算机，将“计算机代理”客户端设备设置“重启时挂起 BitLocker PIN 项”配置为“始终”**  

 将此客户端设置设为“始终”时，Configuration Manager 可完成软件安装以帮助确保关键软件更新已安装且服务已恢复。 但是，如果攻击者截获重启流程，则她将控制计算机。 仅当你信任该计算机并且该计算机的物理访问受到限制时才使用此设置。 例如，此设置可能适用于数据中心中的服务器。  

 **请勿将“计算机代理”客户端设备设置“PowerShell 执行策略”配置为“绕过”。**  

 此客户端设置允许 Configuration Manager 客户端能够运行未签名的 PowerShell 脚本，这可能会使得恶意软件能够在客户端计算机上运行。 如果你必须选择此选项，请使用自定义客户端设置并仅将其分配到必须运行未签名的 PowerShell 脚本的客户端计算机。  

##  <a name="bkmk_mobile"></a>移动设备的最佳安全方案  
 **对于你使用 Configuration Manager 注册并将在 Internet 上支持的移动设备：安装外围网络中的注册代理点和 Intranet 中的注册点**  

 此角色分隔可帮助注册点防御攻击。 如果注册点受到侵害，攻击者可能会获得身份验证证书，并且可能会偷窃注册了移动设备的用户的凭据。  

 **对于移动设备：配置密码设置以帮助防止未经授权访问移动设备**  

 对于 Configuration Manager 注册的移动设备：使用移动设备配置项目将密码复杂性配置为 PIN，并且至少为最小密码长度的默认长度。  

 对于未安装 Configuration Manager 客户端但由 Exchange Server 连接器管理的移动设备：为 Exchange Server 连接器配置“密码设置”，以使密码复杂性为 PIN 并指定至少为最小密码长度的默认长度。  

 **对于移动设备：只有在应用程序经过你信任的公司签名并且不允许未签名的文件安装时，才允许应用程序运行，从而帮助防止篡改清单信息和状态信息**  

 对于 Configuration Manager 注册的更多移动设备：使用移动设备配置项目将安全设置“未签名的应用程序”配置为“禁止”，并将“未签名的文件安装”配置为受信任源。  

 对于未安装 Configuration Manager 客户端但由 Exchange Server 连接器管理的移动设备：为 Exchange Server 连接器配置“应用程序设置”，以使“未签名的文件安装”和“未签名的应用程序”配置为“禁止”。  

 **对于移动设备：通过在未使用移动设备时将其锁定，从而防止权限提升攻击**  

 对于 Configuration Manager 注册的更多移动设备：使用移动设备配置项目来配置密码设置“锁定移动设备之前的空闲时间”。  

 对于未安装 Configuration Manager 客户端但由 Exchange Server 连接器管理的移动设备：为 Exchange Server 连接器配置“密码设置”，以配置“锁定移动设备之前的空闲时间”。  

 **对于移动设备：通过限制可注册其移动设备的用户，从而帮助防止权限提升。**  

 使用自定义客户端设置（而不是默认客户端设置）以仅允许授权用户注册其移动设备。  

 **对于移动设备：在以下情况下，不要向具有通过 Configuration Manager 或 Microsoft Intune 注册的移动设备的用户部署应用程序：**  

-   如果移动设备由多人使用。  

-   如果设备由管理员代表用户注册。  

-   如果在未停用然后重新注册设备的情况下将设备转让给另一个人。  

 在注册过程中会创建用户设备相关性关系，该关系将执行注册的用户映射到移动设备。 如果另一个用户使用移动设备，他们将能够运行你为原始用户部署的应用程序，从而可能会导致权限提升。 同样，如果管理员为用户注册移动设备，则为用户部署的应用程序将不会安装在移动设备上，而是可能会安装为管理员部署的应用程序。  

 与 Windows 计算机的用户设备相关性不同，你不能为 Microsoft Intune 注册的移动设备手动定义用户设备相关性信息。  

 如果转让 Intune 注册的移动设备的成员身份，请从 Intune 中停用移动设备以删除用户设备相关性，然后要求当前用户再次注册设备。  

 **对于移动设备：确保将用户对其设备进行 Microsoft Intune 注册**  

 由于在注册过程中会创建用户设备相关性关系，该关系将执行注册的用户映射到移动设备，因此，如果管理员为用户注册移动设备，则为用户部署的应用程序将不会安装在移动设备上，而是可能会安装为管理员部署的应用程序。  

 **对于 Exchange Server 连接器：确保 Configuration Manager 站点服务器和 Exchange Server 计算机之间的连接受到保护**  

 如果 Exchange Server 在本地，请使用 IPsec；承载的 Exchange 会通过使用 SSL 自动保护连接的安全。  

 **对于 Exchange Server 连接器：为连接器使用最小特权原则**  

 有关 Exchange Server 连接器要求的最小 cmdlet 的列表，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

##  <a name="bkmk_macs"></a> Mac 的最佳安全方案  
 **对于 Mac 计算机：从安全位置中存储和访问客户端源文件。**  

 在 Mac 计算机上安装或注册客户端之前 Configuration Manager 不会验证这些客户端源文件是否已被篡改。 请从可信来源下载这些文件并且安全地存储和访问它们。  

 **对于 Mac 计算机：以独立于 Configuration Manager 的方式，监视和跟踪用户所注册证书的有效期。**  

 为了确保业务连续性，请监视和跟踪用于 Mac 计算机的证书的有效期。 Configuration Manager 不支持此证书的自动续订，并且会警告你证书即将过期。 有效期通常为 1 年。  

 有关如何续订证书的信息，请参阅  [Renewing the Mac Client Certificate Manually](../../../../core/clients/deploy/deploy-clients-to-macs.md#renewing-the-mac-client-certificate)。  

 **对于 Mac 计算机：考虑配置受信任的根 CA 证书，以使其仅对于 SSL 协议受信任，从而防止权限提升。**  

 在注册 Mac 计算机时，会连同用户证书链接到的受信任根证书一起自动安装用于管理 Configuration Manager 客户端的用户证书。 如果要将此根证书的信任限制到 SSL 协议，你可以使用下列过程。  

 完成此过程之后，根证书将不会受到信任来验证除 SSL 之外的协议，例如，安全邮件 (S/MIME)、可扩展身份验证 (EAP) 或代码签名。  

> [!NOTE]  
>  如果独立于 Configuration Manager 安装了客户端证书，也可以使用此过程。  

 将根 CA 证书限制到 SSL 协议：  

1.  在 Mac 计算机上，打开一个终端窗口。  

2.  输入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

3.  在“密钥链访问”  对话框中的“密钥链”  部分中，单击“系统” ，然后在“类别”  部分中，单击“证书” 。  

4.  找到然后双击 Mac 客户端证书的根 CA 证书。  

5.  在根 CA 证书的对话框中，展开“信任”  部分，然后进行下列更改：  

    1.  对于“使用此证书时”  设置，将“始终信任”  默认设置更改为“使用系统默认值” 。  

    2.  对于“安全套接字层(SSL)”  设置，将“未指定值”  更改为“始终信任” 。  

6.  关闭对话框，并在提示时输入管理员的密码，然后单击“更新设置”。  

##  <a name="BKMK_SecurityIssues_Clients"></a> Configuration Manager 客户端的安全问题  
 下列安全问题没有缓解措施：  

-   不会对状态消息执行验证  

     不会对状态消息执行任何验证。 当管理点接受 HTTP 客户端连接时，任何设备都可将状态消息发送到管理点。 如果管理点仅接受 HTTPS 客户端连接，则设备必须从受信任的根证书颁发机构获取有效的客户端身份验证证书，但也可能随后发送任何状态消息。 如果客户端发送无效的状态消息，则该消息将被放弃。  

     针对此漏洞存在一些潜在的攻击。 攻击者可能会发送基于状态消息查询的伪造状态消息以获取集合中的成员身份。 任何客户端可能通过使用状态消息淹没管理点来针对管理点发起拒绝服务攻击。 如果状态消息触发状态消息筛选规则中的操作，则攻击者可能会触发状态消息筛选规则。 攻击者还可能发送表明报表信息不准确的状态消息。  

-   可将策略的目标重新确定为非目标客户端  

     攻击者可能使用几种方法来使策略的目标确定为适用于完全不同的客户端的客户端。 例如，受信任的客户端中的攻击者可能发送错误的清单或者发现信息，以将计算机添加到不应该属于的集合，然后接收针对该集合的所有部署。 如果存在控制来帮助防止攻击者直接修改策略，攻击者可能采用现有策略来重新格式化和重新部署操作系统并将它发送到其他计算机，从而创建拒绝服务。 这些类型的攻击需要精确计时和 Configuration Manager 基础结构的额外知识。  

-   客户端日志允许用户访问  

     所有客户端日志文件都允许用户具有读取访问权限和交互用户写入访问权限。 如果启用详细日志记录，攻击者可能读取日志文件以查找有关符合性或者系统漏洞的信息。 诸如在用户的上下文中执行的软件安装之类的过程必须能够使用低权限用户帐户写入日志。 这意味着攻击者也可能使用低权限帐户写入日志。  

     最严重的风险是攻击者可能删除日志文件中的信息，管理员可能需要这些信息来进行审核和入侵者检测。  

-   可使用计算机来获取针对移动设备注册的证书  

     当 Configuration Manager 处理注册请求时，它无法验证请求是否来自移动设备（而不是计算机）。 如果请求来自计算机，它可能会安装 PKI 证书，该证书随后允许它向 Configuration Manager 注册。 为了在情况中帮助防止权限提升攻击，请仅允许受信任用户注册其移动设备并仔细监视注册活动。  

-   如果你阻止客户端，从客户端到管理点的连接将不会断开，并且被阻止的客户端可能会继续以保持连接消息的形式向管理点发送客户端通知数据包  

     当你阻止不再信任的客户端，而该客户端已建立客户端通知通信时，Configuration Manager 不会断开会话连接。 被阻止的客户端可能会继续向其管理点发送数据包，直至客户端从网络断开连接为止。 这些数据是非常小的保持连接数据包，并且，在对这些客户端解锁之前，将无法通过 Configuration Manager 对其进行管理。  

-   当你使用自动客户端升级，并且将客户端定向到管理点以下载客户端源文件时，不会将管理点验证为受信任源  

-   当用户首次注册 Mac 计算机时，会面临 DNS 欺骗导致的风险  

     当 Mac 计算机在注册过程中连接到注册代理点时，Mac 计算机不太可能已经有根 CA 证书。 此时，服务器不受 Mac 计算机信任，并会提示用户继续。 如果注册代理点的完全限定的名称被恶意 DNS 服务器解析，它可能会将 Mac 计算机引导到恶意注册代理点，并安装来自不受信任的来源的证书。 为了帮助降低此风险，请遵循最佳方案以避免环境中的 DNS 欺骗。  

-   Mac 注册不限制证书请求  

     用户可以重新注册其 Mac 计算机，每次注册均要请求新的客户端证书。 Configuration Manager 不会检查多个请求或限制单台计算机所请求的证书数目。 恶意用户可能会运行一个重复命令行注册请求的脚本，导致网络或证书颁发机构 (CA) 上出现拒绝服务问题。 为了帮助降低此风险，请仔细监视颁发 CA 以确定是否有这种类型的可疑行为。 应从 Configuration Manager 层次结构中立即阻止显示此种行为模式的计算机。  

-   擦除确认不会验证是否已成功擦除了设备  

     当针对移动设备发起擦除操作并且 Configuration Manager 显示要确认的擦除状态时，所确认的是 Configuration Manager 已成功发送消息，而不是设备已按照它进行操作。 此外，对于 Exchange Server 连接器管理的移动设备，擦除确认验证 Exchange（而不是设备）是否已接收了命令。  

-   如果使用选项在 Windows Embedded 设备上提交更改，帐户可能会在过期之前被锁定。  

     如果 Windows Embedded 设备运行 Windows 7 以前的操作系统，并且用户在已禁用写入筛选器以提交 Configuration Manager 所做更改时尝试登录，则在帐户被锁定之前允许的不正确登录尝试次数实际上会减半。 例如，“帐户锁定阈值”  配置为 6，并且帐户在用户错误键入了其密码 3 次的情况即被锁定，实际上造成了拒绝服务状况。  如果用户必须在这种情况下登录到嵌入式设备，请告诫他们锁定阈值被减少的可能性。  

##  <a name="BKMK_Privacy_Cliients"></a> Configuration Manager 客户端的隐私信息  
 在部署 Configuration Manager 客户端时，启用客户端设置，以便你能够使用 Configuration Manager 管理功能。 用于配置功能的设置适用于 Configuration Manager 层次结构中的所有客户端，不管它们是直接连接到公司网络、通过远程会话连接还是连接到 Internet 但受 Configuration Manager 支持。  

 客户端信息存储在 Configuration Manager 数据库中，不会发送给 Microsoft。 信息保留在该数据库中，而“删除过期的发现数据”  站点维护任务每隔 90 天就会删除这些信息一次。 可以配置删除间隔。  

 在配置 Configuration Manager 客户端之前，请考虑你的隐私要求。  

### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Configuration Manager 注册的移动设备的隐私信息  
 有关通过 Configuration Manager 注册移动设备时的隐私信息，请参阅 [System Center Configuration Manager 隐私声明 - 移动设备附录](../../../../core/misc/privacy/privacy-statement-mobile-device-addendum.md)。  

### <a name="client-status"></a>客户端状态  
 Configuration Manager 监视客户端的活动并定期进行评估，并且可修正 Configuration Manager 客户端以及其依赖关系。 客户端状态默认情况下已启用，并且它使用服务器端指标进行客户端活动检查，并使用客户端操作进行自我检查、修正以及用于将客户端状态信息发送到 Configuration Manager 站点。 客户端依据你可配置的计划运行自我检查。 客户端将检查结果发送到 Configuration Manager 站点。 此信息在传输过程中已加密。  

 客户端状态信息存储在 Configuration Manager 数据库中，不会发送给 Microsoft。 信息并未以加密形式存储在站点数据库中。 此信息保留在数据库中，直至依据为“保留以下几天的客户端状态历史记录”  客户端状态设置配置的值将其删除为止。 此设置的默认值为每隔 31 天删除一次。  

 在安装包含客户端状态检查的 Configuration Manager 客户端时，请考虑你的隐私要求。  

##  <a name="BKMK_Privacy_ExchangeConnector"></a>使用 Exchange Server 连接器管理的移动设备的隐私信息  
 Exchange Server 连接器通过使用 ActiveSync 协议查找和管理连接到 Exchange Server（本地或托管）的设备。 Exchange Server 连接器找到的记录存储在 Configuration Manager 数据库中。 信息是从 Exchange Server 中收集的。 它不包含移动设备发送到 Exchange Server 的内容中的任何其他信息。  

 不会将移动设备信息发送到 Microsoft。 移动设备信息储会存在 Configuration Manager 数据库中。 信息保留在该数据库中，而“删除过期的发现数据”  站点维护任务每隔 90 天就会删除这些信息一次。 可以配置删除间隔。  

 在安装和配置 Exchange Server 连接器之前，请考虑你的隐私要求。  
