---
title: 基于 Internet 的客户端管理
titleSuffix: Configuration Manager
description: 在 System Center Configuration Manager 中创建管理基于 Internet 的客户端的计划。
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6c0880b7ba84ecf2e99c2b0e0e791b1c56802378
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70378182"
---
# <a name="plan-for-internet-based-client-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中基于 Internet 的客户端管理计划

适用范围：  System Center Configuration Manager (Current Branch)

通过基于 Internet 的客户端管理（有时称为 IBCM），可在 System Center Configuration Manager 客户端未连接到公司网络但具有标准 Internet 连接时管理该客户端。 这种管理方式有一些优点，例如，不必运行虚拟专用网 (VPN)，从而可以降价成本，以及能够更及时地部署软件更新。  

 由于在公用网络上管理客户端计算机的安全性要求较高，因此基于 Internet 的客户端管理要求客户端以及客户端连接到的站点系统服务器使用 PKI 证书。 这样可以确保连接通过独立的机构进行身份验证，且在这些站点系统之间传输的数据使用安全套接字层 (SSL) 加密。  

 使用下列部分来帮助你规划基于 Internet 的客户端管理。  

##  <a name="features-that-are-not-supported-on-the-internet"></a>Internet 上不支持的功能  
 并非所有客户端管理功能都适用于 Internet，因此在 Internet 上管理客户端时，有些功能可能不受支持。 不支持 Internet 管理的功能通常依赖于 Active Directory 域服务或不适合用于公用网络，例如网络发现和 LAN 唤醒 (WOL)。  

 通过 Internet 管理客户端时，下列功能不受支持：  

- 通过 Internet 进行的客户端部署，如客户端请求和基于软件更新的客户端部署。 请改用手动客户端安装。  

- 自动站点分配。  

- LAN 唤醒。  

- 操作系统部署。 但是，你可以部署不部署操作系统的任务序列；例如在客户端上运行脚本和维护任务的任务序列。  

- 远程控制。  

- 除非基于 Internet 的管理点可以使用 Windows 身份验证（Kerberos 或 NTLM）对 Active Directory 域服务中的用户进行身份验证，否则将向用户部署软件。 当基于 Internet 的管理点信任用户帐户所在的林时，这种情况是有可能的。  

  此外，基于 Internet 的客户端管理不支持漫游。 漫游能够使客户端始终找到最近的分发点来下载内容。 在以下情况下，在 Internet 上管理的客户端会与其分配的站点中的站点系统通信：这些站点系统被配置为使用 Internet FQDN 并且站点系统角色允许来自 Internet 的客户端连接。 客户端不确定地选择基于 Internet 的站点系统之一，而不考虑带宽或物理位置。  

  如果你具有配置为接受 Internet 连接的软件更新点，则 Internet 上基于 Configuration Manager Internet 的客户端始终会对此软件更新点进行扫描，以确定是否需要软件更新。 但是，如果这些客户端在 Internet 上，则它们首先会尝试从 Microsoft 更新下载软件更新，而不是从基于 Internet 的分发点中下载。 只有在此下载失败的情况下，它们之后才会尝试从基于 Internet 的分发点下载所需的软件更新。 未针对基于 Internet 的客户端管理进行配置的客户端不能从 Microsoft 更新下载软件更新，而必须使用 Configuration Manager 分发点。  
 
> [!Tip]  
> Configuration Manager 客户端自动确定它是在 Intranet 上还是在 Internet 上。 如果客户端可以访问域控制器或本地管理点，它会将自己的连接类型设置为“当前 Intranet”。 否则，它会切换到当前 Internet，客户端会使用分配到其站点的管理点、软件更新点和分发点进行通信。

##  <a name="considerations-for-client-communications-from-the-internet-or-untrusted-forest"></a>来自 Internet 或不受信任林的客户端通信的注意事项  
 下列安装在主站点上的站点系统角色支持来自不受信任的位置（如 Internet 或不受信任的林）的客户端连接（辅助站点不支持来自不受信任位置的客户端连接）：  

- 应用程序目录网站点  

    > [!Important]  
    > 应用程序目录已遭弃用。 有关详细信息，请参阅[删除应用程序目录](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat)。  

- Configuration Manager 策略模块  

- 分发点（基于云的分发点需要 HTTPS）  

- 注册代理点  

- 回退状态点  

- 管理点  

- 软件更新点  

  **关于面向 Internet 的站点系统：**    
  虽然客户端和站点系统服务器的林之间不需要信任，但当包含面向 Internet 的站点系统的林信任包含用户帐户的林时，如果启用“客户端策略”客户端设置“启用来自 Internet 客户端的用户策略请求”，则此配置对 Internet 上的设备支持基于用户的策略   。  

  例如，以下配置说明了基于 Internet 的客户端管理何时支持 Internet 上设备的用户策略：  

- 基于 Internet 的管理点在只读域控制器所在外围网络中以对用户进行身份验证，并且干扰防火墙允许 Active Directory 数据包。  

- 用户帐户在林 A (Intranet) 中，基于 Internet 的管理点在林 B（外围网络）中。 林 B 信任林 A，干扰防火墙允许身份验证数据包。  

- 用户帐户和基于 Internet 的管理点在在林 A (Intranet) 中。 系统使用 Web 代理服务器（例如，Forefront 威胁管理网关）将管理点发布到 Internet。  

> [!NOTE]  
>  如果 Kerberos 身份验证失败，则会自动尝试 NTLM 身份验证。  

 如上一个示例所示，当使用 Web 代理服务器（如 ISA 服务器和前端威胁管理网关）将基于 Internet 的站点系统发布到 Internet 时，可以将这些系统放置在 Intranet 中。 可以仅为 Internet 客户端连接配置这些站点系统，或者可以为 Internet 和 Intranet 客户端连接配置这些站点系统。 使用 Web 代理服务器时，可以针对到 SSL 的安全套接字层 (SSL) 桥接或 SSL 隧道来配置它：  

-   **到 SSL 的 SSL 桥接：**    
    为基于 Internet 的客户端管理使用代理 Web 服务器时建议的配置是到 SSL 的 SSL 桥接，此配置使用 SSL 终止操作和身份验证。 必须使用计算机身份验证对客户端计算机进行身份验证，使用用户身份验证对移动设备旧客户端进行身份验证。 通过 Configuration Manager 注册的移动设备不支持 SSL 桥接。  

     代理 Web 服务器上的 SSL 终止的优点是：在将来自 Internet 的数据包转发到内部网络之前，会对该数据包进行检测。 代理 Web 服务器将对来自客户端的连接进行验证，将其终止，然后建立一个新的经身份验证的连接，连接到基于 Internet 的站点系统。 当 Configuration Manager 客户端使用代理 Web 服务器时，客户端标识（客户端 GUID）安全地包含在数据包有效负载内，因而管理点不会将代理 Web 服务器视为客户端。 Configuration Manager 中不支持 HTTP 到 HTTPS 的桥接，或 HTTPS 到 HTTP 的桥接。  
     
    > [!Note]  
    > Configuration Manager 不支持设置第三方 SSL 桥接配置。 例如，Citrix Netscaler 或 F5 BIG-IP。 请与设备供应商协作，以将其配置为与 Configuration Manager 结合使用。  

-   **隧道**：   
    如果代理 Web 服务器无法支持 SSL 桥接的要求，或者想对通过 Configuration Manager 注册的移动设备配置 Internet 支持，则也支持 SSL 隧道。 这是一项安全性较差的选项，因为来自 Internet 的 SSL 数据包会在不终止 SSL 的情况下转发到站点系统，因此无法检测其是否包含恶意内容。 使用 SSL 隧道时，代理 Web 服务器不需要证书。  

##  <a name="planning-for-internet-based-clients"></a>规划基于 Internet 的客户端  
 必须确定将通过 Internet 管理的客户端计算机是否将配置为在 Intranet 和 Internet 上进行管理，还是仅限 Internet 客户端管理。 只能在安装客户端计算机期间配置客户端管理选项。 如果过后改变了主意，则必须重新安装客户端。  

> [!NOTE]  
>  如果配置 Internet 支持的管理点，则连接到该管理点的客户端在下一步刷新其可用的管理点列表时变为受 Internet 支持。  

> [!TIP]  
>  你不必将仅限 Internet 客户端管理的配置局限于 Internet，你也可以在 Intranet 上使用它。  

 为仅限 Internet 客户端管理配置的客户端仅与为 Internet 的客户端连接配置的站点系统通信。 此配置将适合于确定永远不会连接至公司 Intranet 的计算机，例如，位于远程位置的销售点计算机。 若要将客户端通信局限于仅限 HTTPS（例如，为支持防火墙和受限制的安全策略）以及在外围网络中安装基于 Internet 的站点系统并且想要使用 Configuration Manager 客户端管理这些服务器时，此配置也合适。  

 想要管理 Internet 上的工作组客户端时，必须将其安装为仅限 Internet 的客户端。  

> [!NOTE]  
>  将移动设备客户端配置为使用基于 Internet 的管理点时，会将移动设备客户端自动配置为仅限 Internet 的客户端。  

 可以为 Internet 和 Intranet 客户端管理配置其他客户端计算机。 当它们检测到网络更改时，它们会在基于 Internet 的客户端管理和 Intranet 客户端管理之间自动切换。 如果这些客户端可以找到并连接到为 Intranet 上的客户端连接配置的管理点，则会作为具有完整的 Configuration Manager 管理功能的 Intranet 客户端来管理这些客户端。 如果客户端无法找到或连接到为 Intranet 上的客户端连接配置的管理点，则它们会尝试连接到基于 Internet 的管理点，如果此操作成功，则其分配的站点中基于 Internet 的站点系统将管理这些客户端。  

 在基于 Internet 的客户端管理和 Intranet 客户端管理之间自动切换的优点是：当客户端计算机连接到 Intranet 时可自动使用所有 Configuration Manager 功能，当客户端计算机连接到 Internet 时，可继续使用基本管理功能对其进行管理。 此外，在 Internet 上开始的下载可以在 Intranet 上无缝地继续，反之亦然。  

##  <a name="prerequisites-for-internet-based-client-management"></a>基于 Internet 的客户端管理的先决条件  
 Configuration Manager 中基于 Internet 的客户端管理具有以下外部依赖项：  

- 将在 Internet 上管理的客户端必须具有 Internet 连接。  

   Configuration Manager 使用至 Internet 的现有 Internet 服务提供商 (ISP) 连接，此连接可以是永久或临时连接。 客户端移动设备必须具有直接 Internet 连接，但客户端计算机可以具有直接 Internet 连接，或者可以使用代理 Web 服务器进行连接。  

- 支持基于 Internet 的客户端管理的站点系统必须连接到 Internet，并且必须在 Active Directory 域中。  

   基于 Internet 的站点系统不需要与站点服务器的 Active Directory 林建立信任关系。 但是，当基于 Internet 的管理点可通过使用 Windows 身份验证对用户进行身份验证时，支持用户策略。 如果 Windows 身份验证失败，则仅只支持计算机策略。  

  > [!NOTE]
  >  要支持用户策略，也必须将以下两个“客户端策略”  客户端设置设为“真”  ：  
  > 
  > - **在客户端上启用用户策略轮询**  
  >   -   **启用来自 Internet 客户端的用户策略请求**  

   当用户的计算机在 Internet 上时，基于 Internet 的应用程序目录网站点也需要使用 Windows 身份验证对用户进行身份验证。 此要求与用户策略无关。  

- 你必须具有支持的公钥基础结构 (PKI)，此结构可以部署和管理客户端需要且在 Internet 和基于 Internet 的站点系统服务器上受管理的证书。  

   有关 PKI 证书的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

- 必须将支持基于 Internet 的客户端管理的 Internet 站点系统完全限定域名 (FQDN) 注册为公用 DNS 服务器上的主机条目。  

- 干预防火墙或代理服务器必须允许与基于 Internet 的站点系统关联的客户端通信。  

   客户端通信要求：  

  - 支持 HTTP 1.1  

  - 允许多部件 MIME 附件的 HTTP 内容类型（多部件/混合和应用程序/八进制数流）  

  - 允许基于 Internet 的管理点的以下谓词：  

    -   HEAD  

    -   CCM_POST  

    -   BITS_POST  

    -   GET  

    -   PROPFIND  

  - 允许基于 Internet 的分发点的以下谓词：  

    -   HEAD  

    -   GET  

    -   PROPFIND  

  - 允许基于 Internet 的回退状态点的以下谓词：  

    -   POST  

  - 允许基于 Internet 的应用程序目录网站点的以下谓词：  

    -   POST  

    -   GET  

  - 允许基于 Internet 的管理点的以下 HTTP 标头：  

    -   范围：  

    -   CCMClientID：  

    -   CCMClientIDSignature：  

    -   CCMClientTimestamp：  

    -   CCMClientTimestampsSignature：  

  - 允许基于 Internet 的分发点的以下 HTTP 标头：  

    -   范围：  

    有关支持这些要求的配置信息，请参阅防火墙或代理服务器文档。  

    关于使用 Internet 中客户端连接的软件更新点时的类似通信要求，请参阅 Windows Server Update Services (WSUS) 的文档。 例如，对于 Windows Server 2003 上的 WSUS，请参阅 [Appendix D：Security Settings（附录 D：安全设置）](https://go.microsoft.com/fwlink/p/?LinkId=143368)，即安全设置的部署附录。
