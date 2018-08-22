---
title: 客户端安全和隐私
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 客户端的安全和隐私。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3dfb749695ffb7a8ecdeab5e4fbed764023eb6e2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385586"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Configuration Manager 客户端的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*

本文介绍 Configuration Manager 客户端的安全和隐私信息。 它还涵盖 [Exchange Server 连接器](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)所管理的移动设备的相关信息。  



##  <a name="BKMK_Security_Clients"></a>客户端的最佳安全方案  

Configuration Manager 站点从运行 Configuration Manager 客户端的设备接受数据。 此行为会带来客户端可能攻击站点的风险。 例如，它们会发送格式不正确的清单或尝试将站点系统过载。 仅将 Configuration Manager 客户端部署到信任的设备。 此外，使用下列最佳安全方案来帮助站点免遭未授权或被侵害的设备威胁：  

#### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>使用公钥基础结构 (PKI) 证书与运行 IIS 的站点系统建立客户端通信  

-   作为站点属性，将“站点系统设置”  配置为“仅 HTTPS” 。  

-   安装具有 `UsePKICert` CCMSetup 属性的客户端。  

-   使用证书吊销列表 (CRL) 并确保客户端和通信服务器可以始终访问该列表。  

移动设备客户端和一些基于 Internet 的客户端需要这些证书。 Microsoft 建议对 Intranet 上的所有客户端连接也使用这些证书。  

有关 PKI 证书要求以及证书如何用于帮助保护 Configuration Manager 的详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  


#### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>自动批准受信任域的客户端计算机并手动检查和批准其他计算机  

在无法使用 PKI 身份验证时，批准流程可标识出由 Configuration Manager 管理的受信任计算机。 该层次结构具有以下客户端批准配置选项：  
- 手动
- 自动批准受信任域中的计算机
- 自动批准所有计算机  

最安全的批准方法是自动批准属于受信任域成员的客户端。 然后手动检查和批准其他所有计算机。 不建议自动批准所有客户端，除非你具有其他访问控制来避免不受信任的计算机访问你的网络。  

有关如何手动批准计算机的详细信息，请参阅[通过“设备”节点管理客户端](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode)。  


#### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>请勿依赖阻止操作来防止客户端访问 Configuration Manager 层次结构  

Configuration Manager 基础结构会拒绝被阻止的客户端。 如果客户端被阻止，它们将无法与站点系统通信，从而无法下载策略、上载清单数据或者发送状况或状态消息。 

阻止操作适用于以下场景： 
- 在向客户端部署 OS 时阻止已丢失或受侵害的启动媒体
- 当所有站点系统都接受 HTTPS 客户端连接时 

当站点系统接受 HTTP 客户端连接时，请勿依赖阻止操作来保护 Configuration Manager 层次结构免遭不受信任计算机的威胁。 在此场景中，被阻止的客户端可以使用新的自签名证书和硬件 ID 重新加入该站点。 

证书吊销是防御可能已泄漏的证书的主要防线。 证书吊销列表 (CRL) 只能从受支持的公钥基础结构 (PKI) 获得。 在 Configuration Manager 中阻止客户端为保护层次结构提供第二道防线。  

有关详细信息，请参阅[确定是否阻止客户端](/sccm/core/clients/deploy/plan/determine-whether-to-block-clients)。  


#### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>使用对于环境较为实用并且最为安全的客户端安装方法  

-   对于域计算机，组策略客户端安装和基于软件更新的客户端安装方法比客户端请求安装更为安全。  

-   如果应用访问控制和变更控制，请使用映像安装和手动安装方法。  

-   在 1806 或更高版本中，请将 Kerberos 相互身份验证与客户端请求安装结合使用。  

在所有客户端安装方法中，客户端请求安装最不安全，因为它有许多依赖项。 这些依赖项包括本地管理权限、Admin$ 共享和防火墙例外。 这些依赖项的数量和类型会增加攻击面。  

从 1806 版开始，在使用客户端请求时，站点可以通过不允许在建立连接之前回退到 NTLM 来要求 Kerberos 相互身份验证。 此增强有助于保护服务器与客户端之间的通信。 有关详细信息，请参阅[如何使用客户端请求安装客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)。<!--1358204-->  

有关不同客户端安装方法的详细信息，请参阅[客户端安装方法](/sccm/core/clients/deploy/plan/client-installation-methods)。  

尽可能在 Configuration Manager 中选择要求最少安全权限的客户端安装方法。 限制分配有安全角色（有权实现除客户端部署外的其他意图）的管理用户。 例如，配置自动客户端升级时要求具有“完全权限管理员”安全角色，该角色将授予管理用户所有安全权限。  

有关每种客户端安装方法所需的依赖项和安全权限的详细信息，请参阅[计算机客户端先决条件](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#BKMK_prereqs_computers)中的“安装方法依赖项”。  


#### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>如果你必须使用客户端请求安装，请采取附加步骤来确保客户端请求安装帐户安全  

此帐户必须为安装 Configuration Manager 客户端的每台计算机上的本地**管理员**组的成员。 切勿将客户端请求安装帐户添加到**域管理员**组， 而应创建全局组并将该全局组添加到客户端上的本地**管理员**组。 创建组策略对象以添加“受限制的组”设置，从而将客户端请求安装帐户添加到本地**管理员**组。  

为了提高安全性，请创建多个客户端请求安装帐户，每个帐户均具有对有限个数的计算机的管理访问权限。 如果一个帐户受到侵害，则只会损害该帐户有权访问的客户端计算机。  


#### <a name="remove-certificates-before-imaging-clients"></a>在创建客户端映像之前删除证书  

使用 OS 映像部署客户端时，应始终在捕获映像前删除证书。 这些证书包括用于客户端身份验证的 PKI 证书和自签名证书。 如果不删除这些证书，客户端可能会相互冒充。 你无法为每个客户端验证数据。  

有关详细信息，请参阅[创建用于捕获操作系统的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system)。  


#### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>确保 Configuration Manager 计算机客户端获得以下证书的授权副本  

-   Configuration Manager 信任的根密钥证书  

    当以下两个陈述都成立时，客户端将依赖 Configuration Manager 信任的根密钥来验证有效管理点的身份：  

      - 没有为 Configuration Manager 扩展 Active Directory 架构
      - 客户端在与管理点通信时未使用 PKI 证书  

    在这种情况下，除非使用受信任的根密钥，否则客户端无法验证层次结构是否信任管理点。 如果没有受信任的根密钥，则技能较高的攻击者可以将客户端导向未授权的管理点。  

    当客户端无法从全局目录或者使用 PKI 证书下载 Configuration Manager 信任的根密钥时，请使用受信任的根密钥来预先预配客户端。 此操作可确保无法将它们定向到未授权的管理点。 有关详细信息，请参阅[规划受信任的根密钥](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK)。  

-   站点服务器签名证书  

     客户端使用此证书来验证站点服务器是否已经为从管理点下载的策略签名。 此证书由站点服务器自签名并将发布到 Active Directory 域服务。  

     当客户端无法从全局目录下载站点服务器签名证书时，默认情况下，它们会从管理点下载该证书。 如果管理点暴露于不受信任的网络（如 Internet），请在客户端上手动安装站点服务器签名证书。 此操作可确保它们无法下载已在受侵害的管理点中篡改的客户端策略。  

     若要手动安装站点服务器签名证书，请使用 CCMSetup 的 client.msi 属性 **SMSSIGNCERT**。 有关详细信息，请参阅[关于客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。  


#### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>如果客户端从其接触的首个管理点下载受信任的根密钥，请勿使用自动站点分配  

为规避新客户端从未授权的管理点下载受信任的根密钥的风险，请仅在下列情况中使用自动站点分配：  

-   客户端可以访问发布到 Active Directory 域服务的 Configuration Manager 站点信息。  

-   使用受信任的根密钥来预设置客户端。  

-   使用企业证书颁发机构颁发的 PKI 证书来建立客户端和管理点之间的信任。  

有关受信任的根密钥的详细信息，请参阅[规划受信任的根密钥](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK)。  


#### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>使用 CCMSetup Client.msi 选项 SMSDIRECTORYLOOKUP=NoWINS 安装客户端计算机  

可供客户端查找站点和管理点的最安全的服务定位方法是使用 Active Directory 域服务。 在某些情况下，有时无法使用此方法。 例如，无法为 Configuration Manager 扩展 Active Directory 架构，或客户端位于不受信任的林或工作组中。 如果无法使用此方法，请将 DNS 发布用作备用服务定位方法。 如果这两种方法都不可用，并且未针对 HTTPS 客户端连接配置管理点，则客户端可以回退为使用 WINS。  

发布到 WINS 不如其他发布方法安全。 通过指定 **SMSDIRECTORYLOOKUP=NoWINS**，将客户端计算机配置为不回退为使用 WINS。 如果必须使用 WINS 进行服务定位，请使用 **SMSDIRECTORYLOOKUP=WINSSECURE**。 此设置为默认设置。 它使用 Configuration Manager 信任的根密钥来验证管理点的自签名证书。  

> [!NOTE]  
>  在将客户端配置为 **SMSDIRECTORYLOOKUP=WINSSECURE** 并且它从 WINS 中找到管理点时，客户端会检查它在 WMI 中的 Configuration Manager 受信任根密钥副本。  
> 
> 如果管理点证书上的签名与客户端的受信任根密钥副本匹配，则证书通过验证。 验证证书后，客户端开始与其使用 WINS 找到的管理点通信。  
> 
> 如果管理点证书上的签名与客户端的受信任根密钥副本不匹配，则证书无效。 在这种情况下，客户端不会与其使用 WINS 找到的管理点通信。  


#### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>确保维护时段足够大以部署关键的软件更新  

设备集合的维护时段会限制 Configuration Manager 可在这些设备上安装软件的次数。 如果将维护时段配置得太小，客户端可能无法安装关键的软件更新。 此行为使客户端容易遭受可由软件更新减轻的攻击。  


#### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>采取附加安全措施以减少具有写入筛选器的 Windows Embedded 设备上的攻击面  

当在 Windows Embedded 设备中启用写入筛选器后，将仅对覆盖区进行任何软件安装或更改。 设备重启后不保留这些更改。 如果使用 Configuration Manager 来禁用写入筛选器，则在此期间，Embedded 设备会易于面临所有卷均被更改的情况。 这些卷包括共享文件夹。  

Configuration Manager 在此期间会锁定计算机，仅允许本地管理员登录。 请尽可能采取附加安全措施来帮助保护计算机。 例如，在防火墙上启用附加限制。  

如果利用维护时段来保留更改，请仔细规划这些时段。 最大限度缩短禁用写入筛选器的时间，但时间长度应足够完成软件安装和重启。  


#### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>使用基于软件更新的客户端安装来安装最新的客户端版本

如果使用基于软件更新的客户端安装并在站点上安装更高的客户端版本，请更新已发布的软件更新。 之后，客户端会从软件更新点收到最新版本。  

更新站点时，不会自动更新发布到软件更新点的客户端部署的软件更新。 请将 Configuration Manager 客户端重新发布到软件更新点并更新版本号。  

有关详细信息，请参阅[如何使用基于软件更新的安装来安装 Configuration Manager 客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP)。  


#### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>仅在受信任且访问受限的设备上挂起 BitLocker PIN 项  

仅对于受信任且物理访问受限的计算机，将客户端设置“重启时挂起 BitLocker PIN 项”配置为“始终”。

将此客户端设置设为“始终”时，Configuration Manager 可完成软件安装。 此行为有助于安装关键软件更新和恢复服务。 如果攻击者截获重启流程，他们就可以控制计算机。 仅当你信任该计算机并且该计算机的物理访问受到限制时才使用此设置。 例如，此设置可能适用于数据中心内的服务器。  

有关此客户端设置的详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#suspend-bitlocker-pin-entry-on-restart)。  


#### <a name="dont-bypass-powershell-execution-policy"></a>请勿绕过 PowerShell 执行策略   

如果将 Configuration Manager 客户端设置“PowerShell 执行策略”配置为“绕过”，则 Windows 允许运行未签名的 PowerShell 脚本。 此行为可能会使得恶意软件能够在客户端计算机上运行。 当组织需要此选项时，请使用自定义客户端设置。 仅将其分配到必须运行未签名 PowerShell 脚本的客户端计算机。  

有关此客户端设置的详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#powershell-execution-policy)。  



##  <a name="bkmk_mobile"></a>移动设备的最佳安全方案  


#### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>安装外围网络中的注册代理点和 Intranet 中的注册点  

对于使用 Configuration Manager 注册的基于 Internet 的移动设备，请将注册代理点安装在外围网络中，将注册点安装在 Intranet 中。 此角色分隔可帮助注册点防御攻击。 如果攻击者入侵注册点，他们可能会获得身份验证证书。 同时还有可能窃取注册了移动设备的用户的凭据。  


#### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>配置密码设置以帮助防止未经授权访问移动设备。  

*对于 Configuration Manager 注册的移动设备*：使用移动设备配置项目将密码复杂性配置为 PIN。 至少指定默认的最短密码长度。  

*对于未安装 Configuration Manager 客户端但由 Exchange Server 连接器管理的移动设备*：为 Exchange Server 连接器配置“密码设置”，使密码复杂性配置为 PIN。 至少指定默认的最短密码长度。  


#### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>仅允许运行经过你信任的公司签名的应用程序  

只有在应用程序经过你信任的公司签名，才允许应用程序运行，从而帮助防止篡改清单信息和状态信息。 不允许设备安装未签名的文件。  

*对于 Configuration Manager 注册的移动设备*：使用移动设备配置项目将安全设置“未签名的应用程序”配置为“禁止”。 将“未签名的文件安装”配置为受信任源。  

*对于未安装 Configuration Manager 客户端但由 Exchange Server 连接器管理的移动设备*：为 Exchange Server 连接器配置“应用程序设置”，使“未签名的文件安装”和“未签名的应用程序”配置为“禁止”。  


#### <a name="lock-mobile-devices-when-not-in-use"></a>在未使用移动设备时将其锁定  

通过在未使用移动设备时将其锁定，帮助防止特权提升攻击。

*对于 Configuration Manager 注册的移动设备*：使用移动设备配置项目来配置密码设置“锁定移动设备之前的空闲时间”。  

*对于未安装 Configuration Manager 客户端但由 Exchange Server 连接器管理的移动设备*：为 Exchange Server 连接器配置“密码设置”，以设置“锁定移动设备之前的空闲时间”。  


#### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>限制可注册其移动设备的用户  

通过限制可注册其移动设备的用户，从而帮助防止权限提升。 使用自定义客户端设置（而不是默认客户端设置）以仅允许授权用户注册其移动设备。  


#### <a name="user-device-affinity-guidance-for-mobile-devices"></a>适用于移动设备的用户设备相关性指南  

在以下情况下，不要向其移动设备通过 Configuration Manager 或 Microsoft Intune 注册的用户部署应用程序：  

-   移动设备由多人使用。  

-   设备由管理员代表用户注册。  

-   在未停用然后重新注册设备的情况下将设备转让给另一个人。  

注册设备时会创建用户设备相关性关系。 该关系会将执行注册的用户映射到移动设备。 如果另一个用户使用移动设备，他们能够运行为原始用户部署的应用程序，从而可能会导致特权提升。 同样，如果管理员为用户注册移动设备，则不会在移动设备上安装为用户部署的应用程序， 而可能安装为管理员部署的应用程序。  

与 Windows 计算机的用户设备相关性不同，你不能为 Microsoft Intune 注册的移动设备手动定义用户设备相关性信息。  

如果转让 Intune 注册的移动设备的所有权，请先从 Intune 中停用移动设备。 此操作会解除用户设备相关性关系。 然后要求当前用户再次注册设备。  


#### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>确保用户用自己的移动设备向 Microsoft Intune 注册  

在注册过程中会创建用户设备相关性关系。 此操作会将执行注册的用户映射到移动设备。 如果管理员为用户注册移动设备，则不会在移动设备上安装为用户部署的应用程序， 而可能安装为管理员部署的应用程序。  


#### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>保护 Configuration Manager 站点服务器与 Exchange Server 之间的连接   

如果 Exchange Server 在本地，请使用 IPsec。 托管的 Exchange 会使用 SSL 自动保护连接。  


#### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>为连接器使用最小特权原则。  

有关 Exchange Server 连接器需要的最少 cmdlet 的列表，请参阅[使用 Configuration Manager 和 Exchange 管理移动设备](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)。  



##  <a name="bkmk_macs"></a> Mac 的最佳安全方案  


#### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>从安全位置中存储和访问客户端源文件  

在 Mac 计算机上安装或注册客户端之前，Configuration Manager 不会验证这些客户端源文件是否已被篡改。 从受信任源下载这些文件。 安全地存储和访问它们。  


#### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>监视和跟踪证书的有效期  

为了确保业务连续性，请监视和跟踪用于 Mac 计算机的证书的有效期。 Configuration Manager 不支持自动续订此证书，也不会在证书即将到期时发出警告。 有效期通常为一年。  

有关如何续订证书的详细信息，请参阅[手动续订 Mac 客户端证书](/sccm/core/clients/deploy/deploy-clients-to-macs#renewing-the-mac-client-certificate)。  


#### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>仅为 SSL 配置受信任的根证书  

为了帮助防止特权提升，请配置受信任根证书颁发机构的证书，使其仅对于 SSL 协议受信任。

在注册 Mac 计算机时，系统会自动安装用于管理 Configuration Manager 客户端的用户证书。 此用户证书在其信任链中包含受信任的根证书。 若要将此根证书限制为仅对于 SSL 协议受信任，请按以下过程操作：  

1.  在 Mac 计算机上，打开一个终端窗口。  

2.  输入以下命令：`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3.  在“密钥链访问”对话框的“密钥链”部分中，单击“系统”。 然后在“类别”部分中，单击“证书”。  

4.  找到并双击 Mac 客户端证书的根 CA 证书。  

5.  在根 CA 证书的对话框中，展开“信任”  部分，然后进行下列更改：  

    1.  **使用此证书时**：将“始终信任”设置更改为“使用系统默认值”。  

    2.  **安全套接字层(SSL)**：将“未指定值”更改为“始终信任”。  

6.  关闭对话框。 在出现提示时输入管理员的密码，然后单击“更新设置”。  

完成此过程后，该根证书仅在验证 SSL 协议时受信任。 该根证书现在对于其他协议不受信任，其中包括安全邮件 (S/MIME)、可扩展身份验证 (EAP) 或代码签名。  

> [!NOTE]  
>  如果独立于 Configuration Manager 安装了客户端证书，也可以按此过程操作。  



##  <a name="BKMK_SecurityIssues_Clients"></a> Configuration Manager 客户端的安全问题  

下列安全问题没有缓解措施：  


#### <a name="status-messages-arent-authenticated"></a>不对状态消息进行身份验证  

不会对状态消息执行任何验证。 当管理点接受 HTTP 客户端连接时，任何设备都可将状态消息发送到管理点。 如果管理点仅接受 HTTPS 客户端连接，则设备必须具有有效的客户端身份验证证书，但也可以发送任何状态消息。 管理点会放弃从客户端收到的任何无效状态消息。  

针对此漏洞存在一些潜在的攻击： 
- 攻击者可能会发送基于状态消息查询的伪造状态消息以获取集合中的成员身份。 
- 任何客户端可能通过使用状态消息淹没管理点来针对管理点发起拒绝服务攻击。 
- 如果状态消息触发状态消息筛选规则中的操作，则攻击者可能会触发状态消息筛选规则。 
- 攻击者可能发送表明报告信息不准确的状态消息。  


#### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>可将策略的目标重新确定为非目标客户端  

攻击者可能使用几种方法来使策略的目标确定为适用于完全不同的客户端的客户端。 例如，受信任的客户端中的攻击者可能发送错误的清单或者发现信息，以将计算机添加到不应该属于的集合。 然后，该客户端接收针对该集合的所有部署。 

可通过控制来帮助防止攻击者直接修改策略。 但是，攻击者可能采用现有策略来重新格式化和重新部署 OS 并将它发送到其他计算机。 此重定向策略可能会导致拒绝服务。 这些类型的攻击需要精确计时和 Configuration Manager 基础结构的额外知识。  


#### <a name="client-logs-allow-user-access"></a>客户端日志允许用户访问  

所有客户端日志文件都允许**用户**组具有*读取*访问权限，允许特殊**交互**用户具有*写入*访问权限。 如果启用详细日志记录，攻击者可能读取日志文件以查找有关符合性或者系统漏洞的信息。 诸如客户端在用户环境中安装软件之类的过程必须使用低权限用户帐户写入日志。 此行为意味着攻击者也可能使用低权限帐户写入日志。  

最严重的风险是攻击者可能删除日志文件中的信息。 管理员可能需要这些信息来进行审核和入侵检测。  


#### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>可使用计算机来获取专用于移动设备注册的证书  

当 Configuration Manager 处理注册请求时，它无法验证请求是否来自移动设备（而不是计算机）。 如果请求来自计算机，它可能会安装 PKI 证书，该证书随后允许它向 Configuration Manager 注册。 

为了在此情况下帮助防止特权提升攻击，请仅允许受信任用户注册其移动设备。 仔细监视站点中的设备注册活动。  


#### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>被阻止的客户端仍然可以向管理点发送消息

当阻止不再信任的客户端，而该客户端已建立客户端通知网络连接时，Configuration Manager 不会断开会话连接。 被阻止的客户端可能会继续向其管理点发送数据包，直至客户端从网络断开连接为止。 这些数据包只是非常小的保持连接数据包。 在对此客户端解除阻止之前，无法通过 Configuration Manager 对其进行管理。  


#### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>自动客户端升级不验证管理点

当你使用自动客户端升级时，客户端可定向到管理点以下载客户端源文件。 在这种情况下，客户端不会验证管理点是否为受信任源。  


#### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>当用户首次注册 Mac 计算机时，会面临 DNS 欺骗导致的风险  

当 Mac 计算机在注册过程中连接到注册代理点时，Mac 计算机不太可能已经有受信任的根 CA 证书。 此时，Mac 计算机不信任服务器，并提示用户继续。 如果未授权的 DNS 服务器解析注册代理点的完全限定域名 (FQDN)，它可能会将 Mac 计算机定向到未授权的注册代理点，以安装来自不受信任的源的证书。 为了帮助降低此风险，请遵循最佳方案以避免环境中的 DNS 欺骗。  


#### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>Mac 注册不限制证书请求  

用户可以重新注册其 Mac 计算机，每次注册均要请求新的客户端证书。 Configuration Manager 不会检查多个请求或限制单台计算机所请求的证书数目。 未授权用户可能会运行一个重复命令行注册请求的脚本。 此攻击可能导致网络或证书颁发机构 (CA) 上出现拒绝服务问题。 为了帮助降低此风险，请仔细监视颁发 CA 以确定是否有这种类型的可疑行为。 应从 Configuration Manager 层次结构中立即阻止显示此种行为模式的所有计算机。  


#### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>擦除确认不会验证是否已成功擦除设备  

当针对移动设备发起擦除操作并且 Configuration Manager 确认擦除时，所确认的是 Configuration Manager 已成功*发送*消息。 它不会验证设备是否已按照请求*进行操作*。 

对于 Exchange Server 连接器管理的移动设备，擦除确认验证 Exchange（而不是设备）是否已接收命令。  


#### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>如果选择在 Windows Embedded 设备上提交更改，帐户可能会比预期更快锁定  

如果 Windows Embedded 设备运行 Windows 7 以前的 OS 版本，并且用户在 Configuration Manager 禁用写入筛选器时尝试登录，则在帐户被锁定之前，Windows 允许的错误尝试次数仅为已配置次数的一半。 

例如，将“帐户锁定阈值”域策略配置为尝试六次。 用户错误键入其密码三次后，帐户即被锁定。此行为实际上会导致拒绝服务。 如果用户必须在这种情况下登录到 Embedded 设备，请告诫他们锁定阈值降低的可能性。  



##  <a name="BKMK_Privacy_Clients"></a> Configuration Manager 客户端的隐私信息  

在部署 Configuration Manager 客户端时，启用客户端设置以便使用 Configuration Manager 功能。 用于配置功能的设置适用于 Configuration Manager 层次结构中的所有客户端。 不管它们是直接连接到内部网络、通过远程会话连接还是连接到 Internet，此行为都相同。  

客户端信息存储在 SQL Server 的 Configuration Manager 数据库中，不会发送给 Microsoft。 信息保留在该数据库中，而“删除过期的发现数据”站点维护任务每隔 90 天就会删除这些信息一次。 可以配置删除间隔。 

系统会将一些汇总或聚合的诊断和使用情况数据发送给 Microsoft。 有关详细信息，请参阅[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)。  

在配置 Configuration Manager 客户端之前，请考虑你的隐私要求。  


### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Configuration Manager 注册的移动设备的隐私信息  

有关通过 Configuration Manager 注册移动设备时的隐私信息，请参阅 [System Center Configuration Manager 隐私声明 - 移动设备附录](/sccm/core/misc/privacy/privacy-statement-mobile-device-addendum)。  


### <a name="client-status"></a>客户端状态  

Configuration Manager 监视客户端的活动。 它定期评估 Configuration Manager 客户端，并且可解决该客户端及其依赖项出现的问题。 客户端状态已默认启用。 它使用服务器端指标进行客户端活动检查。 客户端状态使用客户端操作进行自我检查、修正以及用于将客户端状态信息发送到站点。 客户端依据你配置的计划运行自我检查。 客户端将检查结果发送到 Configuration Manager 站点。 此信息在传输过程中已加密。  

客户端状态信息存储在 SQL Server 的 Configuration Manager 数据库中，不会发送给 Microsoft。 信息并未以加密形式存储在站点数据库中。 此信息保留在数据库中，直至依据为“保留以下几天的客户端状态历史记录”客户端状态设置配置的值将其删除为止。 此设置的默认值为每隔 31 天删除一次。  

在安装包含客户端状态检查的 Configuration Manager 客户端时，请考虑你的隐私要求。  



##  <a name="BKMK_Privacy_ExchangeConnector"></a>使用 Exchange Server 连接器管理的移动设备的隐私信息  

Exchange Server 连接器通过使用 ActiveSync 协议查找和管理连接到本地或托管 Exchange Server 的设备。 Exchange Server 连接器找到的记录存储在 SQL Server 的 Configuration Manager 数据库中。 信息是从 Exchange Server 中收集的。 它不包含移动设备发送到 Exchange Server 的内容中的任何其他信息。  

系统不会将移动设备信息发送给 Microsoft。 移动设备信息存储在 SQL Server 的 Configuration Manager 数据库中。 信息保留在该数据库中，而“删除过期的发现数据”站点维护任务每隔 90 天就会删除这些信息一次。 可以配置删除间隔。  

在安装和配置 Exchange Server 连接器之前，请考虑你的隐私要求。  
