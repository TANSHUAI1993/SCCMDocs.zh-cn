---
title: "应用程序管理的安全和隐私 | Microsoft Docs"
description: "System Center Configuration Manager 中应用程序管理的安全和隐私最佳方案。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6ee99fa0c07676f004e41a50bf16d0d17604e790
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-application-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中应用程序管理的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*


##  <a name="security-best-practices-for-application-management"></a>应用程序管理的最佳安全方案  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|将应用程序目录点配置为使用 HTTPS 连接并通知用户恶意网站风险。|将应用程序目录网站点和应用程序目录 Web 服务点配置为接受 HTTPS 连接，以便服务器向用户进行身份验证并且防止篡改和查看传输的数据。 通过通知用户仅连接到受信任的网站来帮助防止社会工程攻击。<br /><br /> 当你不使用 HTTPS 时，不要使用将应用程序目录中的组织名称显示为标识证明的品牌配置选项。|  
|使用角色分隔，在单独的服务器上安装应用程序目录网站点和应用程序目录服务点。|如果应用程序目录网站点被泄露，请将其安装到应用程序目录 Web 服务点的单独服务器上。 这将有助于保护 Configuration Manager 客户端和 Configuration Manager 基础结构。 如果应用程序目录网站点接受来自 Internet 的客户端连接，则这非常重要，因为此配置使服务器易受到攻击。|  
|通知用户在使用完应用程序目录时关闭浏览器窗口。|如果用户在用于应用程序目录的同一浏览器窗口中浏览到外部网站，则浏览器将继续使用适合 Intranet 中的受信任站点的安全设置。|  
|手动指定用户设备相关性，而不是让用户确定其主要设备。 不要启用基于使用情况的配置。|不考虑从用户或从待授权的设备中收集的信息。 如果使用信任管理用户未指定的用户设备相关性来部署软件，则可以在计算机上或者为无权接收该软件的用户安装该软件。|  
|始终将部署配置为从分发点下载内容，而不是从分发点运行。|将部署配置为从分发点下载内容并在本地运行时，Configuration Manager 客户端会在下载内容后验证包哈希。 如果该哈希与策略中的哈希不匹配，则客户端会丢弃该包。 相比之下，如果将部署配置为直接从分发点运行，则 Configuration Manager 客户端不验证包哈希，这意味着 Configuration Manager 客户端可以安装已经被篡改的软件。<br /><br /> 如果必须直接从分发点运行部署，请在分发点上使用对包的 NTFS 最低权限，并使用 Internet 协议安全性 (IPsec) 保护客户端与分发点之间的通道，以及分发点与站点服务器之间的通道。|  
|在需要“使用管理权限运行”选项的情况下不允许用户与程序交互。|配置程序时，可以设置“允许用户与此程序交互”选项，以便用户能够响应用户界面中的任何所需提示。 如果程序也被配置为“使用管理权限运行” ，则以运行该程序的计算机为目标的攻击者可以使用用户界面提升对客户端计算机的权限。<br /><br /> 使用利用 Windows Installer 进行安装并通过每用户提升权限进行软件部署的程序，这些程序需要管理凭据。 必须在不具有管理凭据的用户的上下文中运行安装程序。 Windows Installer 每用户提升权限提供了最安全的方法来部署具有此要求的应用程序。|  
|使用“安装权限”  客户端设置限制用户是否能够以交互方式安装软件。|将“计算机代理”客户端设备的“安装权限”设置配置为限制可以使用应用程序目录或软件中心来安装软件的用户的类型。 例如，创建一个自定义客户端设置，并将“安装权限”  设置为“仅管理员” 。 然后将此客户端设置应用于服务器集合，以防止无管理权限的用户在这些计算机上安装软件。|  
|对于移动设备，仅部署签名的应用程序。|只有当移动设备信任的证书颁发机构 (CA) 对移动设备应用程序进行了代码签名后再部署移动设备应用程序。 例如：<br /><br /><ul><li>由已知 CA（如 VeriSign）签名的供应商应用程序。</li><li>使用内部 CA 独立于 Configuration Manager 进行签名的内部应用程序。</li><li>在创建应用程序类型以及使用签名证书时使用 Configuration Manager 签名的内部应用程序。</li></ul>|  
|如果通过使用 Configuration Manager 中的“创建应用程序向导”对移动设备应用程序进行签名，请确保签名证书文件的位置安全以及确保信道的安全。|为了帮助防止权限提升以及防御中间人攻击，请将签名证书文件存储在受保护的文件夹内，并在以下计算机之间使用 IPsec 或服务器消息块 (SMB)：<br /><br /><ul><li>运行 Configuration Manager 控制台的计算机</li><li>存储证书签名文件的计算机</li><li>存储应用程序源文件的计算机</li></ul> 或者，在运行“创建应用程序向导”之前，对独立于 Configuration Manager 的应用程序签名。|  
|实现访问控制来保护引用计算机。|当管理用户通过浏览到引用计算机来配置部署类型中的检测方法时，请确保计算机未被泄露。|  
|限制和监视被授予基于角色的安全角色（与应用程序管理相关）的管理用户：<br /><br /><ul><li>**应用程序管理员**</li><li>**应用程序作者**</li><li> **应用程序部署管理员**</li></ul>|即使配置基于角色的管理，创建和部署应用程序的管理用户具有的权限也可能比你获得的权限多。 例如，创建或更改应用程序的管理用户可以选择不在其安全作用域中的相关应用程序。|  
|配置 Microsoft Application Virtualization (App-V) 虚拟环境时，请选择在虚拟环境中具有相同信任级别的应用程序。|由于 App-V 虚拟环境中的应用程序可以共享资源，如剪贴板，因此，请配置虚拟环境，使选择的应用程序具有相同的信任级别。<br /><br /> 有关详细信息，请参阅[创建 App-V 虚拟环境](../../apps/deploy-use/create-app-v-virtual-environments.md)。|  
|如果针对 Mac 计算机部署应用程序，请确保源文件来自可信来源。|CMAppUtil 工具不会验证源包的签名，因此请确保它来自你信任的来源。 CMAppUtil 工具无法检测文件是否已被篡改。|  
|如果为 Mac 计算机部署应用程序，将 **.cmmac** 文件导入 Configuration Manager 时，请确保该文件的位置以及信道的安全。|由 CMAppUtil 工具生成的要导入 Configuration Manager 的 **.cmmac** 文件未签名或未经验证。 为了帮助防止此文件被篡改，请将其存储在受保护的文件夹中，并在以下计算机之间使用 IPsec 或 SMB：<br /><br /><ul><li>运行 Configuration Manager 控制台的计算机</li><li>存储 **.cmmac** 文件的计算机</li></ul>。|  
|如果配置 Web 应用程序部署类型，请使用 HTTPS（而不是 HTTP）来保护连接的安全。|如果通过使用 HTTP 链接（而不是 HTTPS 链接）来部署 Web 应用程序，则设备可能会被重定向到未授权服务器，并且设备和服务器之间传输的数据可能会被篡改。|  

##  <a name="security-issues-for-application-management"></a>应用程序管理的安全问题  

-   低权限用户可以从客户端计算机上的客户端缓存中复制文件。  

     用户可以读取客户端缓存，但无法写入客户端缓存。 用户可以使用读取权限将一台计算机中的应用程序安装文件复制到另一台计算机中。  

-   低权限用户可以更改在客户端计算机上记录软件部署历史记录的文件。  

     因为应用程序历史记录信息未受到保护，所以用户可以更改报告是否安装了应用程序的文件。  

-   APP-V 包未签名。  

     Configuration Manager 中的 App-V 包不支持签名来验证内容是否来自受信任的源以及在传输中是否修改了内容。 无法缓解此安全问题。 请确保按照最佳安全实践从可靠来源或安全位置中下载内容。  

-   所有用户都可以在计算机上安装发布的 APP-V 应用程序。  

     在计算机上发布 App-V 应用程序后，登录到该计算机的所有用户都可以安装应用程序。 这意味着无法限制在发布应用程序后可以安装该应用程序的用户。  

-   无法限制公司门户的安装权限。  

     举例来说，尽管可以配置客户端设置以使设备的主要用户或只有本地管理员才有安装权限，但此设置对于公司门户不起作用。 这可能会导致权限提升，原因是用户可安装不应允许其进行安装的应用。  

##  <a name="BKMK_CertificatesSilverlight5"></a> Microsoft Silverlight 5 的证书，以及应用程序目录所需的提升的信任模式  
 Configuration Manager 客户端需要 Microsoft Silverlight 5，必须在提升的信任模式下运行 Microsoft Silverlight 5，用户才能从应用程序目录中安装软件。 默认情况下，Silverlight 应用程序在部分信任模式下运行，以防止应用程序访问用户数据。 如果尚未安装 Microsoft Silverlight 5，Configuration Manager 会自动将其安装在客户端上。 默认情况下，Configuration Manager 会将计算机代理“允许 Silverlight 应用程序在提升的信任模式下运行”客户端设置设为“是”。 此设置会让签名和信任的 Silverlight 应用程序请求提升的信任模式。  

 安装应用程序目录网站点系统角色时，客户端还会在每个 Configuration Manager 客户端计算机上安装受信任的发布者计算机证书存储中的 Microsoft 签名证书。 此证书允许由其签名的 Silverlight 应用程序在提升的信任模式下运行，计算机从应用程序目录中安装软件需要此模式。 Configuration Manager 将自动管理此签名证书。 为了确保服务连续性，请不要手动删除或移动此 Microsoft 签名证书。  

> [!WARNING]  
>  如果启用“允许 Silverlight 应用程序在提升的信任模式下运行”客户端设置，则它允许计算机存储或用户存储内受信任的发布者证书存储中的证书所签名的所有 Silverlight 应用程序在提升的信任模式下运行。 此客户端设置无法专门为 Configuration Manager 应用程序目录或为计算机存储中受信任的发布者证书存储启用提升的信任模式。 如果恶意软件在受信任的发布者存储中添加了一个恶意证书，例如在用户存储中，则使用其自己的 Silverlight 应用程序的恶意软件现在也能够在提升的信任模式下运行。  

 如果将客户端设置“允许 Silverlight 应用程序在提升的信任模式下运行”设置为“否”，则此设置不会从客户端中删除 Microsoft 签名证书。  

 若要深入了解 Silverlight 中受信任的应用程序，请参阅[受信任的应用程序](http://go.microsoft.com/fwlink/p/?LinkId=252842)。  

##  <a name="privacy-information-for-application-management"></a>应用程序管理的隐私信息  
 应用程序管理允许在任何客户端计算机或层次结构中的客户端移动设备上运行任何应用程序、程序或脚本。 Configuration Manager 无法控制运行的应用程序、程序或脚本的类型或它们传输的信息类型。 在应用程序部署过程中，Configuration Manager 可能会在客户端和服务器之间传输标识设备和登录帐户的信息。  

 Configuration Manager 会维护有关软件部署过程的状态信息。 除非客户端使用 HTTPS 进行通信，否则，在传输过程中不会对软件部署状态信息加密。 状态信息并未以加密形式存储在数据库中。  

 使用 Configuration Manager 应用程序安装在客户端上以远程、交互或无提示方式安装软件时，可能要遵守该软件的软件许可条款。 这不同于 System Center Configuration Manager 的软件许可条款。 使用 Configuration Manager 部署软件之前，请务必查看并同意软件许可条款。  

 默情况下不会进行应用程序部署，并需要几个配置步骤。  

 有助于有效地进行软件部署的两个可选功能是用户设备相关性和应用程序目录：  

-   用户设备相关性将用户映射到设备，以便 Configuration Manager 管理员可以向用户部署软件，软件自动安装在用户最常使用的一台或多台计算机上。  

-   应用程序目录是一个网站，用户可在其中请求要安装的软件。  

 有关用户设备相关性和应用程序目录的隐私信息，请查看以下部分。  

 在配置应用程序管理之前，请考虑隐私要求。  

##  <a name="user-device-affinity"></a>用户设备相关性  
-  Configuration Manager 可能会在客户端和管理点站点系统之间传输信息。 该信息可能会标识计算机和登录帐户，以及登录帐户的使用情况汇总。  
-  除非将管理点配置为要求客户端通过 HTTPS 进行通信，否则，在客户端和服务器之间传输的信息并未加密。  
-  用于将用户映射到设备的计算机和登录帐户的使用情况信息存储在客户端计算机上，并发送给管理点，然后存储在 Configuration Manager 数据库中。 默认情况下，在 90 天后将从数据库中删除旧的信息。 通过设置“删除过期的用户设备相关性数据”  站点维护任务，可以配置删除行为。
-  Configuration Manager 会维护有关用户设备相关性的状态信息。 除非将客户端配置为使用 HTTPS 与管理点进行通信，否则，在传输过程中不会对状态信息加密。 状态信息并未以加密形式存储在数据库中。  
-  计算机、登录帐户使用情况信息和状态信息不会发送给 Microsoft。  
-  用于建立用户及设备相关性的计算机和登录帐户使用情况信息始终都是启用的。 此外，普通用户和管理用户也可以提供用户设备相关性信息。  

##  <a name="application-catalog"></a>应用程序目录  
-  应用程序目录允许 Configuration Manager 管理员发布任何应用程序或程序或脚本，以供用户运行。 Configuration Manager 无法控制在目录中发布的程序或脚本的类型以及它们传输的信息类型。    
-  Configuration Manager 可能会在客户端和应用程序目录站点系统角色之间传输信息。 该信息可能会标识计算机和登录帐户。 除非将这些站点系统角色配置为要求客户端使用 HTTPS 进行通信，否则，在客户端和服务器之间传输的信息并未加密。  
-  有关应用程序批准请求的信息存储在 Configuration Manager 数据库中。 默认情况下，将在 30 天后删除那些被取消或拒绝的请求以及对应的请求历史记录条目。 通过设置“删除过期的应用程序请求数据”  站点维护任务，可以配置删除行为。 绝不会删除处于已批准状态和挂起状态的应用程序批准请求。  
-  发送到和接收自应用程序目录的信息不会发送给 Microsoft。  
-  默认情况下，不会安装应用程序目录。 此安装需要执行几个配置步骤。  
