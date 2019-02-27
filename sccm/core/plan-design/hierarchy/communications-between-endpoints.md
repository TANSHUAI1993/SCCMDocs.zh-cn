---
title: 终结点之间的通信
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 站点系统和组件如何跨网络通信。
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5ebe37bb97c4a1e231bfaf94f420f7f0471f30f6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141953"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Configuration Manager 中终结点之间的通信

适用范围：System Center Configuration Manager (Current Branch)

本文介绍了 Configuration Manager 站点系统和客户端如何跨网络通信。 它包括以下部分：  

- [站点中站点系统间的通信](#Planning_Intra-site_Com)  
    - [站点服务器到分发点](#bkmk_site2dp)  

- [从客户端到站点系统和服务的通信](#Planning_Client_to_Site_System)  
    - [客户端到管理点的通信](#bkmk_client2mp)  
    - [客户端到分发点的通信](#bkmk_client2dp)  
    - [来自 Internet 或不受信任林的客户端通信的注意事项](#BKMK_clientspan)  
    - [关于面向 Internet 的站点系统](#bkmk_internetfacing)  

- [跨 Active Directory 林的通信](#Plan_Com_X-Forest)  
    - [支持不受站点服务器林信任的林中的域计算机](#bkmk_noforesttrust)  
    - [支持工作组中的计算机](#bkmk_workgroup)  
    - [支持跨多个域和林的站点或层次结构的方案](#bkmk_span)  



##  <a name="Planning_Intra-site_Com"></a> 站点中站点系统间的通信  

 当 Configuration Manager 站点系统或组件跨网络与站点中的其他站点系统或组件通信时，它们将根据你配置站点的方式使用以下其中一项协议：  

-   服务器消息块 (SMB)  

-   HTTP  

-   HTTPS  

除了站点服务器与分发点之间的通信之外，随时都可能发生站点中服务器与服务器的通信。 这些通信不使用机制来控制网络带宽。 由于你无法控制站点系统之间的通信，因此请确保在网络快速且连接良好的位置中安装站点系统服务器。  


### <a name="bkmk_site2dp"></a>站点服务器到分发点 

为帮助管理内容从站点服务器向分发点的传输，可使用以下策略：  

-   配置网络带宽控件和计划的分发点。 这些控件类似于站点间地址使用的配置。 如果将内容传输到远程网络位置是你的主要带宽考虑事项，则可经常使用此配置，而不用安装其他 Configuration Manager 站点。  

-   你可以安装一个分发点作为预留的分发点。 预留的分发点允许你使用手动放在分发点服务器上的内容，并且不需要在网络中传输内容文件。  

有关详细信息，请参阅[管理用于内容管理的网络带宽](manage-network-bandwidth.md)。



##  <a name="Planning_Client_to_Site_System"></a> 从客户端到站点系统和服务的通信  

客户端启动与站点系统角色、Active Directory 域服务以及联机服务的通信。 若要启用这些通信，防火墙必须允许客户端与其通信的终结点之间的网络流量。 有关客户端与这些终结点通信时所使用的端口和协议的详细信息，请参阅 [Configuration Manager 中使用的端口](/sccm/core/plan-design/hierarchy/ports)。  

客户端必须先使用服务定位找出支持客户端协议（HTTP 或 HTTPS）的角色，然后才可与站点系统角色通信。 默认情况下，客户端使用提供给它们的最安全方法。 有关详细信息，请参阅[了解客户端如何查找站点资源和服务](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services)。  

若要使用 HTTPS，请配置下列选项之一：  

- 使用公钥基础结构 (PKI) 并在客户端和服务器上安装 PKI 证书。 有关如何使用证书的信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

- 自版本 1806 开始，将该站点配置为“将 Configuration Manager 生成的证书用于 HTTP 站点系统”。 有关详细信息，请参阅[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)。  

在部署使用 Internet 信息服务 (IIS) 并支持来自客户端的通信的站点系统角色时，必须指定客户端是否使用 HTTP 或 HTTPS 连接到站点系统。 如果使用 HTTP，还必须考虑签名和加密选项。 有关详细信息，请参阅[规划签名和加密](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForSigningEncryption)。  


### <a name="bkmk_client2mp"></a>客户端到管理点的通信

客户端与管理点通信时存在两个阶段：身份验证（传输）和授权（消息）。 此过程因以下因素而异： 
- 网站配置：HTTP、HTTPS 或增强型 HTTP
- 管理点配置：是仅 HTTPS，还是允许使用 HTTP 或 HTTPS
- 以设备为中心的方案的设备标识
- 以用户为中心的方案的用户标识

使用下表了解此过程的工作原理：  

| MP 类型  | 客户端身份验证  | 客户端授权<br>设备标识  | 客户端授权<br>用户标识  |
|----------|---------|---------|---------|
| HTTP     | 匿名<br>使用增强型 HTTP，该站点可验证 Azure AD“用户”或“设备”令牌。 | 位置请求：匿名<br>客户端包：匿名<br>注册时，使用以下方法之一来证明设备标识：<br> - 匿名（手动批准）<br> - Windows 集成身份验证<br> - Azure AD“设备”令牌（增强型 HTTP）<br>注册后，客户端使用消息签名来证明设备身份 | 对于以用户为中心的方案，请使用以下方法之一来证明用户身份：<br> - Windows 集成身份验证<br> - Azure AD“用户”令牌（增强型 HTTP） |
| HTTPS    | 使用以下方法之一：<br> - PKI 证书<br> - Windows 集成身份验证<br> - Azure AD“用户”或“设备”令牌 | 位置请求：匿名<br>客户端包：匿名<br>注册时，使用以下方法之一来证明设备标识：<br> - 匿名（手动批准）<br> - Windows 集成身份验证<br> - PKI 证书<br> - Azure AD“用户”或“设备”令牌<br>注册后，客户端使用消息签名来证明设备身份 | 对于以用户为中心的方案，请使用以下方法之一来证明用户身份：<br> - Windows 集成身份验证<br> - Azure AD“用户”令牌 |

> [!Tip]  
> 有关不同设备标识类型和云管理网关的管理点配置的详细信息，请参阅[为 HTTPS 启用管理点](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps)。  


### <a name="bkmk_client2dp"></a> 客户端到分发点的通信

当客户端与分发点通信时，该客户端只需要在下载内容之前进行身份验证。 使用下表了解此过程的工作原理：


| DP 类型  | 客户端身份验证  |
|----------|---------|
| HTTP     | - 匿名（若允许）<br>- 计算机帐户或网络访问帐户的 Windows 集成身份验证<br> - 内容访问令牌（增强型 HTTP） |
| HTTPS    | - PKI 证书<br> - 计算机帐户或网络访问帐户的 Windows 集成身份验证<br> - 内容访问令牌 |


###  <a name="BKMK_clientspan"></a> 来自 Internet 或不受信任林的客户端通信的注意事项  

下列安装在主站点上的站点系统角色支持来自不受信任的位置（如 Internet 或不受信任的林）的客户端连接。 （辅助站点不支持来自不受信任位置的客户端连接。） 

-   应用程序目录网站点  

-   Configuration Manager 策略模块 (NDES) 

-   分发点   

-   基于云的分发点（需要 HTTPS）

-   注册代理点  

-   回退状态点  

-   管理点  

-   软件更新点  

-   云管理网关（需要 HTTPS）


### <a name="bkmk_internetfacing"></a> 关于面向 Internet 的站点系统

> [!Note]  
> 下一节介绍基于 Internet 的客户端管理方案。 本节不适用于云管理网关方案。 有关详细信息，请参阅[在 Internet 上管理客户端](/sccm/core/clients/manage/manage-clients-internet)。  

客户端的林和站点系统服务器的林之间不需要信任。 但当包含面向 Internet 的站点系统的林信任包含用户帐户的林时，如果启用“客户端策略”客户端设置“启用来自 Internet 客户端的用户策略请求”，则此配置对 Internet 上的设备支持基于用户的策略。  

例如，以下配置说明了基于 Internet 的客户端管理何时支持 Internet 上设备的用户策略：  

-   基于 Internet 的管理点在只读域控制器所在外围网络中以对用户进行身份验证，并且干扰防火墙允许 Active Directory 数据包。  

-   用户帐户在林 A (Intranet) 中，基于 Internet 的管理点在林 B（外围网络）中。 林 B 信任林 A，干扰防火墙允许身份验证数据包。  

-   用户帐户和基于 Internet 的管理点在在林 A (Intranet) 中。 系统使用 Web 代理服务器（例如，Forefront 威胁管理网关）将管理点发布到 Internet。  

> [!NOTE]  
>  如果 Kerberos 身份验证失败，则会自动尝试 NTLM 身份验证。  

如上一个示例所示，当使用 Web 代理服务器将基于 Internet 的站点系统发布到 Internet 时，可将这些系统放置在 Intranet 中。 可仅为 Internet 客户端连接配置这些站点系统，或者可为 Internet 和 Intranet 客户端连接配置这些站点系统。 使用 Web 代理服务器时，可以针对到 SSL 的安全套接字层 (SSL) 桥接或 SSL 隧道来配置它，如下所示：  

-   **到 SSL 的 SSL 桥接：**   
    为基于 Internet 的客户端管理使用代理 Web 服务器时建议的配置是到 SSL 的 SSL 桥接，此配置使用 SSL 终止操作和身份验证。 必须使用计算机身份验证对客户端计算机进行身份验证，使用用户身份验证对移动设备旧客户端进行身份验证。 通过 Configuration Manager 注册的移动设备不支持 SSL 桥接。  

     代理 Web 服务器上的 SSL 终止的优点是：在将来自 Internet 的数据包转发到内部网络之前，会对该数据包进行检测。 代理 Web 服务器将对来自客户端的连接进行验证，将其终止，然后建立一个新的经身份验证的连接，连接到基于 Internet 的站点系统。 当 Configuration Manager 客户端使用代理 Web 服务器时，客户端标识（客户端 GUID）安全地包含在数据包有效负载内，因而管理点不会将代理 Web 服务器视为客户端。 Configuration Manager 中不支持 HTTP 到 HTTPS 的桥接，或 HTTPS 到 HTTP 的桥接。  

-   **隧道**：   
    如果代理 Web 服务器无法支持 SSL 桥接的要求，或者想对通过 Configuration Manager 注册的移动设备配置 Internet 支持，则也支持 SSL 隧道。 这是一项安全性较差的选项，因为来自 Internet 的 SSL 数据包会在不终止 SSL 的情况下转发到站点系统，因此无法检测其是否包含恶意内容。 使用 SSL 隧道时，代理 Web 服务器不需要证书。  



##  <a name="Plan_Com_X-Forest"></a> 跨 Active Directory 林的通信  

Configuration Manager 支持跨越 Active Directory 林的站点和层次结构。 它也支持与站点服务器不在相同 Active Directory 林中的域计算机，以及工作组中的计算机。  


### <a name="bkmk_noforesttrust"></a> 支持不受站点服务器林信任的林中的域计算机 

-   在该不受信任的林中安装站点系统角色，并可以将站点信息发布到该 Active Directory 林  

-   管理这些计算机，就好像它们是工作组计算机一样  

在不受信任的 Active Directory 林中安装站点系统服务器时，会在该林中保留来自该林的客户端的客户端到服务器的通信，并且 Configuration Manager 可以使用 Kerberos 对计算机进行身份验证。 将站点信息发布到客户端的林时，客户端将得益于检索站点信息（如可用管理点的列表），得益于其 Active Directory 林，而不用从其分配的管理点中下载此信息。  

> [!NOTE]  
>  如果要管理 Internet 上的设备，则当站点系统服务器在 Active Directory 林中时，可在外围网络中安装基于 Internet 的站点系统角色。 此方案不需要外围网络与站点服务器林之间的双向信任。  


### <a name="bkmk_workgroup"></a> 支持工作组中的计算机  

-   在工作组计算机对站点系统角色使用 HTTP 客户端连接时，手动批准这些计算机。 Configuration Manager 不能通过使用 Kerberos 对这些计算机进行身份验证。  

-   将工作组客户端配置为使用网络访问帐户，以便这些计算机可以从分发点中检索内容。  

-   为工作组客户端提供替代机制以查找管理点。 使用 DNS 发布、WINS 或直接分配管理点。 这些客户端无法从 Active Directory 域服务中检索站点信息。  

有关详细信息，请参阅下列文章：  

-   [管理冲突的记录](/sccm/core/clients/manage/manage-clients#BKMK_ConflictingRecords)  

-   [网络访问帐户](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#accounts-used-for-content-management)  

-   [如何在工作组计算机上安装 Configuration Manager 客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientWorkgroup)  


###  <a name="bkmk_span"></a> 支持跨多个域和林的站点或层次结构的方案  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>方案 1：跨林的层次结构中站点之间的通信  
此方案要求支持 Kerberos 身份验证的双向林信任。  如果没有支持 Kerberos 身份验证的双向林信任，则 Configuration Manager 不支持远程林中的子站点。  

Configuration Manager 支持在与父站点林之间具有所需双向信任的远程林中安装子站点。 例如，只要存在所需的信任，就可以将辅助站点放在与其主父站点不同的林中。  

> [!NOTE]  
>  子站点可以是主站点（其中，管理中心站点为父站点）或辅助站点。  

Configuration Manager 中的站点间通信使用数据库复制和基于文件的传输。 在安装站点时，必须指定用于在指定服务器上安装该站点的帐户。 此帐户还建立并维护站点之间的通信。 当站点成功安装并启动基于文件的传输和数据库复制之后，不必为站点通信进行任何其他配置。  

存在双向林信任时，Configuration Manager 不需要任何其他配置步骤。  

默认情况下，在安装新的子站点时，Configuration Manager 会配置以下组件：  

-   使用站点服务器计算机帐户的每个站点处基于站点间文件的复制路由。 Configuration Manager 将每台计算机的计算机帐户添加到目标计算机上的 **SMS_SiteToSiteConnection_&lt;sitecode\>** 组。  

-   每个站点中 SQL Server 之间的数据库复制。  

此外，请设置以下配置：  

-   干扰防火墙和网络设备必须允许 Configuration Manager 请求的网络包。  

-   名称解析必须在林之间工作。  

-   若要安装站点或站点系统角色，必须指定在指定的计算机上具有本地管理员权限的帐户。  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>方案 2：跨林的站点中的通信  
此方案不需要双向林信任。  

主站点支持在远程林中的计算机上安装站点系统角色。  

-   该应用程序目录 Web 服务点是唯一的例外。  仅在站点服务器所在的同一个林中受支持。  

-   当站点系统角色接受来自 Internet 的连接时，作为最佳安全做法，请将站点系统角色安装在林边界为站点服务器提供保护的位置（例如，在外围网络中）。  

若要在位于不受信任的林中的计算机上安装站点系统角色：  

- 指定站点用以安装站点系统角色的“站点系统安装帐户”。 （该帐户必须具有要连接的本地管理凭据。）然后在指定计算机上安装站点系统角色。  

- 选择站点系统选项“要求站点服务器启动到此站点系统的连接”。 此设置需要站点服务器建立到站点系统服务器的连接以传输数据。 此配置会阻止不受信任位置中的计算机与信任的网络中的站点服务器联系。 这些连接使用“站点系统安装帐户” 。  

若要使用安装在不受信任的林中的站点系统角色，即使站点服务器启动数据传输，防火墙也必须允许网络流量。  

此外，下列站点系统角色需要直接访问站点数据库。 因此，防火墙必须允许从不受信任的林到站点 SQL Server 的适用流量：  

-   资产智能同步点  

-   Endpoint Protection 点  

-   注册点  

-   管理点  

-   报告服务点  

-   状态迁移点  

有关详细信息，请参阅 [Configuration Manager 中使用的端口](/sccm/core/plan-design/hierarchy/ports)。  

你可能需要配置站点数据库的管理点和注册点访问权限。

-   默认情况下，安装这些角色时，Configuration Manager 会将新站点系统服务器的计算机帐户配置为该站点系统角色的连接帐户。 然后，它将该帐户添加到适当的 SQL Server 数据库角色。  

-   在不受信任的域中安装这些站点系统角色时，请配置站点系统角色连接帐户以使站点系统角色能够从数据库中获取信息。  

如果将域用户帐户配置为这些站点系统角色的连接帐户，请确保该域用户帐户具有对该站点上的 SQL Server 数据库的适当访问权限：  

-   管理点：**管理点数据库连接帐户**  

-   注册点：**注册点连接帐户**  

在规划其他林中的站点系统角色时，请考虑以下其他信息：  

-   如果运行 Windows 防火墙，请配置合适的防火墙配置文件，以传递站点数据库服务器与随远程站点系统角色一起安装的计算机之间的通信。   

-   当基于 Internet 的管理点信任包含用户帐户的林时，支持用户策略。 当不存在信任时，仅支持计算机策略。  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>方案 3：当客户端与其站点服务器不在相同 Active Directory 林中时客户端与站点系统角色之间的通信  
Configuration Manager 对不在其站点的站点服务器所在的相同林中的客户端支持以下方案：  

-   客户端的林与站点服务器的林之间存在双向林信任。  

-   站点系统角色服务器与客户端在相同林中。  

-   客户端在与站点服务器之间没有双向林信任的域计算机上，客户端林中未安装站点系统角色。  

-   客户端在工作组计算机上。  

当加入域的计算机上的客户端的站点已发布到其 Active Directory 林时，这些客户端可以将 Active Directory 域服务用于服务定位。  

将站点信息发布到另一个 Active Directory 林：  

-   首先指定林，然后在“管理”  工作区的“Active Directory 林”  节点中启用发布到该林。  

-   将每个站点配置为将其数据发布到 Active Directory 域服务。 此配置允许该林中的客户端检索站点信息以及查找管理点。 对于无法将 Active Directory 域服务用于服务定位的客户端，可使用 DNS、WINS 或客户端的分配的管理点。  


####  <a name="bkmk_xchange"></a> 方案 4：将 Exchange Server 连接器放置到远程林中  

若要支持此方案，请确保在林之间进行名称解析。 例如，配置 DNS 转发。 配置 Exchange Server 连接器时，请指定 Exchange Server 的 Intranet FQDN。 有关详细信息，请参阅[使用 Configuration Manager 和 Exchange 管理移动设备](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)。  



## <a name="see-also"></a>另请参阅

- [规划安全性](/sccm/core/plan-design/security/plan-for-security)  

- [Configuration Manager 客户端的安全和隐私](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

