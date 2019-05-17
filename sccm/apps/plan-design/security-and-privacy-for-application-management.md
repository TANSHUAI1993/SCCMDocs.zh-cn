---
title: 应用程序的安全和隐私
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中管理应用程序时有关安全和隐私的指导和建议。
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d8715b8d91f6397fbf5d4d254b48f8078b0dfc3
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083229"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>在 Configuration Manager 中管理应用程序的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*


##  <a name="security-guidance-for-application-management"></a>应用程序管理的安全指南  


### <a name="use-the-new-software-center-without-the-application-catalog"></a>使用新的软件中心，而无需应用程序目录
<!--1358309-->
从版本 1806 开始，不再需要应用程序目录角色，即可在软件中心显示用户可用的应用程序。 此项配置有助于减少向用户交付应用程序所需的服务器基础结构。 减少服务器基础结构还可以减少攻击面。 

若要为基于 Internet 的客户端提供一致且安全的应用程序体验，使用 Azure Active Directory 和云管理网关。

有关详细信息，请参阅[配置软件中心](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)。 


### <a name="use-https-with-the-application-catalog"></a>在应用程序目录中使用 HTTPS

配置应用程序目录网站点和应用程序目录 web 服务点以接受 HTTPS 连接。 使用此配置，将向用户对服务器进行身份验证。 传输数据受到保护，不会遭篡改和查看。 

通过让用户只连接受信任的网站来帮助防止社会工程攻击。 帮助用户了解恶意网站的危害。

如果不使用 HTTPS，则不要使用品牌配置选项。 这些设置在应用程序目录中显示组织名称，作为身份证明。  


### <a name="use-role-separation"></a>使用角色分离

在单独的服务器上安装应用程序目录网站点和应用程序目录服务点。 如果应用程序目录网站点遭泄露，它将独立于应用程序目录 Web 服务点。 此设计将有助于保护 Configuration Manager 客户端和基础结构。 如果应用程序目录网站点接受来自 Internet 的客户端连接，则此配置非常重要。 它使服务器更易受攻击。  


### <a name="close-browser-windows"></a>关闭浏览器窗口

通知用户在使用完应用程序目录时关闭浏览器窗口。 如果用户在用于应用程序目录的同一浏览器窗口中浏览到外部网站，则浏览器将继续使用适合 Intranet 中的受信任站点的安全设置。  


### <a name="centrally-specify-user-device-affinity"></a>集中指定用户设备相关性

手动指定用户设备相关性，而不是让用户确定其主要设备。 不要启用基于使用情况的配置。

不考虑从用户或从待授权的设备中收集的信息。 如果使用信任管理未指定的用户设备相关性来部署软件，则可以在计算机上或者为无权接收该软件的用户安装该软件。  


### <a name="dont-run-deployments-from-distribution-points"></a>不从分发点运行部署

始终将部署配置为从分发点下载内容，而不是从分发点运行。 将部署配置为从分发点下载内容并在本地运行时，Configuration Manager 客户端会在下载内容后验证包哈希。 如果该哈希与策略中的哈希不匹配，则客户端会弃用该包。 

如果将部署配置为直接从分发点运行，则 Configuration Manager 客户端不验证包哈希。 此行为意味着 Configuration Manager 客户端可能会安装被篡改的软件。

如果必须直接从分发点运行部署，请在分发点的包上使用 NTFS 最低权限。 此外，使用 Internet 协议安全性 (IPsec) 来保护客户端与分发点之间以及分发点与站点服务器之间的通道。


### <a name="bkmk_interact"></a> 不允许用户与已提升的进程交互
  
如果启用“使用管理权限运行”或“针对系统安装”选项，则不要让用户与这些应用程序交互。 配置应用程序时，可以将选项设置为“允许用户查看程序安装并与之交互”。 此设置允许用户响应用户界面中的任何必要提示。 如果也将应用程序配置为“使用管理权限运行”或“针对系统安装”（从 1802 版开始），则以运行该程序的计算机为目标的攻击者可以使用用户界面提升对客户端计算机的权限。

使用利用 Windows Installer 进行安装并通过每用户提升权限进行软件部署的程序，这些程序需要管理凭据。 必须在不具有管理凭据的用户的上下文中运行安装程序。 Windows Installer 每用户提升权限提供了最安全的方法来部署具有此要求的应用程序。


### <a name="restrict-whether-users-can-install-software-interactively"></a>限制用户是否可以交互方式安装软件

在“计算机代理”组中配置“安装权限”客户端设置。 此设置将限制可以使用应用程序目录或软件中心安装软件的用户类型。 

例如，创建一个自定义客户端设置，并将“安装权限”  设置为“仅管理员” 。 将此客户端设置应用到服务器集合。 此配置可防止无管理权限的用户在这些服务器上安装软件。  


### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>对于移动设备，请仅部署签名的应用程序

只有当移动设备信任的证书颁发机构 (CA) 对移动设备应用程序进行了代码签名后才能部署移动设备应用程序。 

例如：
- 由已知 CA（如 VeriSign）签名的供应商应用程序。  

- 使用内部 CA 独立于 Configuration Manager 进行签名的内部应用程序。  

- 在创建应用程序类型以及使用签名证书时使用 Configuration Manager 签名的内部应用程序。


### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>确保移动设备应用程序签名证书位置的安全性

如果通过使用 Configuration Manager 中的“创建应用程序向导”对移动设备应用程序进行签名，请确保签名证书文件的位置安全以及确保信道的安全。 为了帮助防止权限提升以及防御中间人攻击，请将签名证书文件存储在受保护的文件夹内。 

在以下计算机之间使用 IPsec：
- 运行 Configuration Manager 控制台的计算机
- 存储证书签名文件的计算机
- 存储应用程序源文件的计算机

或者，在运行“创建应用程序向导”之前，对独立于 Configuration Manager 的应用程序签名。


### <a name="implement-access-controls"></a>实现访问控制

实现访问控制来保护引用计算机。 当通过浏览到引用计算机来配置部署类型中的检测方法时，请确保计算机未被泄露。


### <a name="restrict-and-monitor-administrative-users"></a>限制和监视管理用户

限制和监视管理用户，这些用户被授予以下基于应用程序管理角色的安全角色：
- **应用程序管理员**
- **应用程序作者**
- **应用程序部署管理员**

即使配置基于角色的管理，创建和部署应用程序的管理用户具有的权限也可能比你获得的权限多。 例如，创建或更改应用程序的管理用户可以选择不在其安全作用域中的相关应用程序。


### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>在使用相同信任级别的虚拟环境中配置 APP-V 应用

配置 Microsoft Application Virtualization (App-V) 虚拟环境时，请选择在虚拟环境中具有相同信任级别的应用程序。 由于 App-V 虚拟环境中的应用程序可以共享资源，如剪贴板，因此，请配置虚拟环境，使选择的应用程序具有相同的信任级别。

有关详细信息，请参阅[创建 App-V 虚拟环境](/sccm/apps/deploy-use/create-app-v-virtual-environments)。


### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>确保 macOS 应用来自可信来源

如果针对 macOS 设备部署应用程序，请确保源文件来自可信来源。 CMAppUtil 工具不会验证源包的签名。 请确保包来自信任的源。 CMAppUtil 工具无法检测文件是否已被篡改。


### <a name="secure-the-cmmac-file-for-macos-apps"></a>保护 macOS 应用的 cmmac 文件

如果为 macOS 计算机部署应用程序，请确保 .cmmac 文件位置的安全。 CMAppUtil 工具生成此文件，然后将其导入到 Configuration Manager。 此文件未经签名或验证。 

将此文件导入到 Configuration Manager 时，请确保通信通道的安全。 为帮助防止篡改此文件，请将其存储在受保护的文件夹中。 在以下计算机之间使用 IPsec：
- 运行 Configuration Manager 控制台的计算机  
- 存储 **.cmmac** 文件的计算机  


### <a name="use-https-for-web-applications"></a>为 Web 应用程序使用 HTTPS

如果配置 Web 应用程序部署类型，请使用 HTTPS 来保护连接的安全。 如果通过使用 HTTP 链接（而不是 HTTPS 链接）来部署 Web 应用程序，则设备可能会被重定向到恶意服务器。 设备和服务器之间传输的数据可能会被篡改。



##  <a name="security-issues-for-application-management"></a>应用程序管理的安全问题  

-   低权限用户可以从客户端计算机上的客户端缓存中复制文件。  

     用户可以读取客户端缓存，但无法写入客户端缓存。 用户可以使用读取权限将一台计算机中的应用程序安装文件复制到另一台计算机中。  

-   低权限用户可以更改在客户端计算机上记录软件部署历史记录的文件。  

     因为应用程序历史记录信息未受到保护，所以用户可以更改用于报告是否安装了应用程序的文件。  

-   APP-V 包未签名。  

     Configuration Manager 中的 APP-V 包不支持签名。 数字签名验证内容是否来自受信任的源，并且在传输过程中未被更改。 无法缓解此安全问题。 请按照最佳安全实践从可靠来源或安全位置下载内容。  

-   所有用户都可以在计算机上安装发布的 APP-V 应用程序。  

     在计算机上发布 App-V 应用程序后，登录到该计算机的所有用户都可以安装应用程序。 无法限制在发布应用程序后可以安装该应用程序的用户。  

-   无法在移动设备上限制公司门户的安装权限。  

     尽管可以配置客户端设置来限制安装权限，但此设置不适用于公司门户。 此问题可能导致特权提升。 用户能够安装不允许安装的应用。  



##  <a name="BKMK_CertificatesSilverlight5"></a> Microsoft Silverlight 5 的证书，以及应用程序目录所需的提升的信任模式  

> [!Important]  
> 自 Configuration Manager 版本 1802 起，客户端不再自动安装 Silverlight。
> 
> 从版本 1806 开始，应用程序目录网站点的 Silverlight 用户体验不再受支持。 用户应使用新的软件中心。 有关详细信息，请参阅[配置软件中心](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)。  

 Configuration Manager 客户端版本 1710 和早期版本需安装 Microsoft Silverlight 5，必须在提升的信任模式下运行 Microsoft Silverlight 5，用户才能从应用程序目录中安装软件。 默认情况下，Silverlight 应用程序在部分信任模式下运行，以防止应用程序访问用户数据。 如果尚未安装 Microsoft Silverlight 5，Configuration Manager 会自动将其安装在客户端上。 默认情况下，Configuration Manager 会将计算机代理“允许 Silverlight 应用程序在提升的信任模式下运行”客户端设置设为“是”。 此设置会让签名和信任的 Silverlight 应用程序请求提升的信任模式。  

 安装应用程序目录网站点系统角色时，客户端还会在每个 Configuration Manager 客户端计算机上安装受信任的发布者计算机证书存储中的 Microsoft 签名证书。 由此证书签名的 Silverlight 应用程序在提升的信任模式下运行，计算机从应用程序目录中安装软件需要此模式。 Configuration Manager 将自动管理此签名证书。 为增加服务连续性，请不要手动删除或移动此 Microsoft 签名证书。  

> [!WARNING]  
>  如果启用“允许 Silverlight 应用程序在提升的信任模式下运行”客户端设置，则它允许计算机存储或用户存储内受信任的发布者证书存储中的证书所签名的所有 Silverlight 应用程序在提升的信任模式下运行。 此客户端设置无法专门为 Configuration Manager 应用程序目录或为计算机存储中受信任的发布者证书存储启用提升的信任模式。 如果恶意软件在受信任的发布者存储中添加了一个恶意证书，则使用其自己的 Silverlight 应用程序的恶意软件现在也能够在提升的信任模式下运行。  

 如果将“允许 Silverlight 应用程序在提升的信任模式下运行”设置设为“否”，则客户端不会删除 Microsoft 签名证书。  

 若要深入了解 Silverlight 中受信任的应用程序，请参阅[受信任的应用程序](https://go.microsoft.com/fwlink/p/?LinkId=252842)。  



##  <a name="privacy-information-for-application-management"></a>应用程序管理的隐私信息  

 应用程序管理允许在层次结构中的任何客户端上运行任何应用程序、程序或脚本。 Configuration Manager 无法控制运行的应用程序、程序或脚本的类型或它们传输的信息类型。 在应用程序部署过程中，Configuration Manager 可能会在客户端和服务器之间传输标识设备和登录帐户的信息。  

 Configuration Manager 会维护有关软件部署过程的状态信息。 除非客户端使用 HTTPS 进行通信，否则，在传输过程中不会对软件部署状态信息加密。 状态信息并未以加密形式存储在数据库中。  

 使用 Configuration Manager 应用程序安装在客户端上以远程、交互或无提示方式安装软件时，可能要遵守该软件的软件许可条款。 这不同于 System Center Configuration Manager 的软件许可条款。 使用 Configuration Manager 部署软件之前，请务必查看并同意软件许可条款。  

 Configuration Manager 收集有关应用程序的诊断和使用情况数据，Microsoft 使用这些数据来改进将来版本。 有关详细信息，请参阅[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)。

 默情况下不会进行应用程序部署，并需要几个配置步骤。  

 下列功能可帮助有效地进行软件部署：   

- 用户设备相关性将用户映射到设备。 Configuration Manager 管理员向用户部署软件。 客户端自动在用户最常使用的一个或多个计算机上安装软件。  

- 应用程序目录是一个网站，用户可在其中请求要安装的软件。  

    > [!Note]  
    > 自 Configuration Manager 1802 开始，应用程序目录的主要功能现包含在软件中心内。 有关详细信息，请参阅[配置软件中心](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)。  

- 安装 Configuration Manager 客户端时，还会在设备上自动安装软件中心。 用户从软件中心更改设置、浏览和安装应用程序。  

  有关[用户设备相关性](#bkmk_privacy-uda)和[软件中心和应用程序目录](#bkmk_privacy-userex)的隐私信息，请查看以下部分。  

  在配置应用程序管理之前，请考虑隐私要求。  


### <a name="bkmk_privacy-uda"></a> 用户设备相关性  

-  Configuration Manager 可能会在客户端和管理点站点系统之间传输信息。 该信息可能会标识计算机和登录帐户，以及登录帐户的使用情况汇总。  

-  除非将管理点配置为要求客户端通过 HTTPS 进行通信，否则，在客户端和服务器之间传输的信息并未加密。  

-  用于将用户映射到设备的计算机和登录帐户的使用情况信息存储在客户端计算机上，并发送给管理点，然后存储在 Configuration Manager 数据库中。 默认情况下，在 90 天后将从数据库中删除旧的信息。 通过设置“删除过期的用户设备相关性数据”  站点维护任务，可以配置删除行为。  

-  Configuration Manager 会维护有关用户设备相关性的状态信息。 除非将客户端配置为使用 HTTPS 与管理点进行通信，否则，在传输过程中不会对状态信息加密。 状态信息并未以加密形式存储在数据库中。  

-  用于建立用户及设备相关性的计算机和登录帐户使用情况信息始终都是启用的。 普通用户和管理用户也可以提供用户设备相关性信息。  


### <a name="bkmk_privacy-userex"></a> 软件中心和应用程序目录  

-  软件中心和应用程序目录允许 Configuration Manager 管理员发布任何应用程序或程序或脚本，以供用户运行。 Configuration Manager 无法控制在目录中发布的程序或脚本的类型以及它们传输的信息类型。  

-  Configuration Manager 可能会在客户端和应用程序目录站点系统角色之间传输信息。 该信息可能会标识计算机和登录帐户。 除非将这些站点系统角色配置为要求客户端使用 HTTPS 进行通信，否则，在客户端和服务器之间传输的信息并未加密。  

-  有关应用程序批准请求的信息存储在 Configuration Manager 数据库中。 默认情况下，将在 30 天后删除那些被取消或拒绝的请求以及对应的请求历史记录条目。 通过设置“删除过期的应用程序请求数据”  站点维护任务，可以配置删除行为。 绝不会删除处于已批准状态和挂起状态的应用程序批准请求。  

-  在设备安装 Configuration Manager 客户端时，还会自动安装软件中心。  

-  默认情况下，不会安装应用程序目录。 此安装需要执行几个配置步骤。  
