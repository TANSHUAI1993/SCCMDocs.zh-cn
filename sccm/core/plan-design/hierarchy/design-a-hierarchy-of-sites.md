---
title: "设计站点层次结构 - Configuration Manager | Microsoft Docs"
description: "了解 System Center Configuration Manager 的可用拓扑和管理选项以便你可以规划站点层次结构。"
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
caps.latest.revision: "22"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4710b1b89eb50cb7bcf4c4ee50c12a96b6561bc9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>设计 System Center Configuration Manager 的站点层次结构

*适用范围：System Center Configuration Manager (Current Branch)*

安装新的 System Center Configuration Manager 层次结构的第一个站点前，最好先了解 Configuration Manager 的可用拓扑、可用站点的类型及其彼此之间的关系以及每个站点类型提供的管理范围。
然后，在考虑了可减少需安装的站点数的内容管理选项后，可以计划能够高效地为当前业务需求提供服务，并且可之后进行拓展以满足将来增长的需求的拓扑。  

> [!NOTE]
> 在计划安装新的 Configuration Manager 时，请熟悉[发行说明]( /sccm/core/servers/deploy/install/release-notes)，其中详细说明了活动版本中的当前问题。 此发行说明适用于 Configuration Manager 的所有分支。  但是，在使用[Technical Preview 分支]( /sccm/core/get-started/technical-preview)时，你将在每个版本的 Technical Preview 文档中发现仅针对该分支的问题。  

##  <a name="bkmk_topology"></a>层次结构拓扑  
 层次结构拓扑的范围从单一独立主站点一直到一组连接的主要和辅助站点，该组站点在层次结构顶级（顶层）站点处具有管理中心站点。   在层次结构中所用的站点类型和计数的关键驱动程序通常是你必须支持的设备的类型和数量，如下所示：   

 **独立主站点：**在单一主站点可支持所有设备和用户的管理时，使用独立主站点（请参阅[调整大小和扩展数量](/sccm/core/plan-design/configs/size-and-scale-numbers)）。 如果不同的地理位置可由单一主站点成功地提供服务，则该拓扑也成功。  若要帮助管理网络流量，可以使用首选的管理点和精心规划的内容基础结构（请参阅 [System Center Configuration Manager 中内容管理的基本概念](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)）。  

 此拓扑的好处包括：  

-   简化管理开销。  

-   简化可用资源和服务的客户端站点分配和发现。  

-   消除站点之间的数据库复制可能引起的延迟。

-   此选项可以将独立的主层次结构扩展到更大的具有管理中心站点的层次结构。 这使你随后能够安装新主站点以扩展部署的规模。  


**带有一个或多个子主站点的管理中心站点：**在你需要多个主站点支持所有设备和用户的管理时，使用此拓扑。  当需要使用多于一个主站点时需要。 此拓扑的好处包括：  


-   最多支持 25 个主站点，这样能够扩展层次结构的规模。  

-   将始终使用管理中心站点（除非重新安装站点）。 这是永久性选项。 不能分离子主站点而将其变为独立主站点。

 下列部分可帮助你理解何时使用特定站点或内容管理选项来替代其他站点。  

##  <a name="BKMK_ChooseCAS"></a>确定何时使用管理中心站点  
 使用管理中心站点配置层次结构范围设置，以及监视层次结构中的所有站点和对象。 此站点类型不直接管理客户端，但它可协调站点间数据复制，其中包括整个层次结构中的站点和客户端的配置。  

**以下信息可帮助你决定何时安装管理中心站点：**  

-   管理中心站点是层次结构中的顶层站点。  

-   在配置具有多个主站点的层次结构时，必须安装管理中心站点。 如果你立即需要两个或多个主站点，请先安装管理中心站点。 如果你已有主站点并想随后安装管理中心站点，则必须扩展独立主站点[](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand)，以安装管理中心站点。 

-   管理中心站点仅支持使用主站点作为子站点。  

-   无法为管理中心站点分配客户端。  

-   管理中心站点不支持直接支持客户端（例如管理点和分发点）的站点系统角色。  

-   在使用连接到管理中心站点的 Configuration Manager 控制台时，你可以管理层次结构中的所有客户端，并为任何子站点执行站点管理任务。 这可能包括在子级主站点或辅助站点安装管理点或其他站点系统角色。  

-   在使用管理中心站点时，只能在管理中心站点中看到层次结构中所有站点的站点数据。 此数据包括诸如清单数据和状态消息等信息。  

-   你可以从管理中心站点中通过将发现方法指派在单独的站点上运行，从而配置整个层次结构中的发现操作。  

-   你可以通过将不同的安全角色、安全作用域和集合分配给不同的管理用户来管理整个层次结构中的安全性。 这些配置在层次结构中的每个站点上适用。  

-   你可以配置文件复制和数据库复制来控制层次结构中站点之间的通信。 这包括计划站点数据的数据库复制，以及管理用于站点之间基于文件的数据传输的带宽。  

##  <a name="BKMK_ChoosePriimary"></a>确定何时使用主站点  
 使用主站点来管理客户端。 你可以在管理中心站点下面安装主站点以作为子主站点，也可以作为新层次结构的第一个站点。 安装为层次结构的第一个站点的主站点将创建独立主站点。 子主站点和独立主站点均支持辅助站点作为主站点的子站点。  

 出于以下任何原因而考虑使用主站点：  

-   要管理设备和用户。  

-   要增加设备的数目，你可以使用单一层次结构进行管理。  

-   要为部署管理提供其他连接点。  

-   满足组织的管理要求。 例如，你可以在远程位置安装主站点来管理低带宽网络上的部署内容传输。 但是，利用 System Center Configuration Manager，你可以使用选项来限制将数据传输到分发点时的网络带宽使用量。 借助此内容管理功能，便不再需要安装其他站点。  


**以下信息帮助你决定何时安装主站点：**  

-   主站点可以是独立主站点或较大层次结构中的子主站点。 如果主站点是包含管理中心站点的层次结构的成员，则站点将使用数据库复制在站点之间复制数据。 除非你需要支持的客户端和设备数大于单一主站点可支持的数目，否则，请考虑安装独立主站点。  安装独立主站点后，可以将其扩展到可向新管理中心站点报告以扩展部署。  

-   主站点仅支持使用管理中心站点作为父站点。  

-   主站点仅支持使用辅助站点作为子站点，并且还可以支持多个辅助子站点。  

-   主站点负责处理为其分配的客户端中的所有客户端数据。  

-   主站点使用数据库复制与其管理中心站点（在安装新站点时会自动配置）直接通信。  

##  <a name="BKMK_ChooseSecondary"></a>确定何时使用辅助站点  
 使用辅助站点管理跨低带宽网络的部署内容和客户端数据传输。  

 你可从管理中心站点或辅助站点的直接父主站点管理辅助站点。 辅助站点必须连接到主站点，并且你无法在不卸载这些辅助站点的情况下将它们移至不同的父站点，然后在新的主站点下将它们作为子站点重新安装。

但是，你可以在两个对等辅助站点之间进行内容路由，以便于管理部署内容的基于文件的复制。 为将客户端数据传输到主站点，辅助站点将使用基于文件的复制。 辅助站点还使用数据库复制与其父主站点进行通信。  

 如果满足下列任何条件，请考虑安装辅助站点：  

-   管理用户不需要本地连接点时。  

-   必须管理指向层次结构中较低级别站点的部署内容的传输时。  

-   必须管理发送到层次结构中较高级别站点的客户端信息时。  

 如果不希望安装辅助站点，并具有位于远程位置的客户端，请考虑使用 Windows BranchCache 或安装已为带宽控制和计划而启用的分发点。 可以使用以下具有或不具有辅助站点的内容管理选项，并且它们可以帮助减少必须安装的站点和服务器数量。 有关 Configuration Manager 中内容管理选项的信息，请参阅[确定何时使用内容管理选项](#BKMK_ChooseSecondaryorDP)。  


**以下信息帮助你决定何时安装辅助站点：**  

-   如果 SQL Server 的本地实例不可用，则在站点安装过程中，辅助站点将自动安装 SQL Server Express。  

-   从 Configuration Manager 控制台启动辅助站点安装，而不是直接在计算机上运行安装程序。  

-   辅助站点使用站点数据库中信息的子集，其减少了父主站点和辅助站点间数据库复制时产生的复制数据量。  

-   辅助站点支持将基于文件的内容路由至具有公用父主站点的其他辅助站点。  

-   辅助站点安装将自动部署位于辅助站点服务器的管理点和分发点。  

##  <a name="BKMK_ChooseSecondaryorDP"></a>确定何时使用内容管理选项  
 如果你具有设在远程网络位置的客户端，请考虑使用一个或多个内容管理选项而非一个主站点或辅助站点。 当你使用 Windows BranchCache、配置带宽控制分发点或手动将内容复制到分发点（预留内容）时，通常可以消除安装另一站点的需要。  


**如果满足下列任何条件，请考虑部署分发点（而非安装另一站点）：**  

-   对于远程位置的客户端计算机，你的网络带宽已足够与管理点进行通信以下载客户端策略、发送清单、报告状态和发现信息。  

-   后台智能传输服务 (BITS) 提供的带宽控制不足以满足你的网络要求。  

 有关 Configuration Manager 中内容管理选项的详细信息，请参阅 [System Center Configuration Manager 中内容管理的基本概念](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)。  

##  <a name="bkmk_beyond"></a>除层次结构拓扑之外  
 除了初始层次结构拓扑外，还需考虑不同站点的哪些服务或功能将可用（站点系统角色），以及如何在基础结构中管理层次结构范围的配置和功能。 以下常见的注意事项会在单独主题中进行介绍。 这些注意事项很重要，因为它们可影响层次结构设计或受层次结构设计影响：  

-   当你准备[使用 System Center Configuration Manager 管理计算机和设备](/sccm/core/clients/manage/manage-clients)时，请考虑所管理的设备是在本地，在云中还是包括用户拥有的设备 (BYOD)。  此外，请考虑如何管理多个管理选项支持的设备，例如可以直接通过 Configuration Manager 或通过与 Microsoft Intune 进行集成管理的 Windows 10 计算机。  

-   了解可用网络基础结构可能会影响远程位置之间数据流的方式（请参阅[为 System Center Configuration Manager 准备网络环境](/sccm/core/plan-design/network/configure-firewalls-ports-domains)）。 同时考虑所管理的用户和设备的地理位置，以及它们是通过公司的域还是从 Internet 访问你的基础结构。  

-   规划用于将部署的信息（文件和应用）高效分发到所管理的设备的内容基础结构（请参阅 [System Center Configuration Manager 管理内容和内容基础结构](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)）。  

-   确定计划使用的 [System Center Configuration Manager 的特性和功能](../../../core/plan-design/changes/features-and-capabilities.md)、站点系统角色或角色需要的 Windows 基础结构以及可能会选择在多站点层次结构中的哪些站点对它们进行部署以最有效地使用你的网络和服务器资源。  

-   请考虑数据和设备的安全，包括对 PKI 的使用。 请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../core/plan-design/network/pki-certificate-requirements.md)。  


**查看以下用于站点特定配置的资源：**  

-   [为 System Center Configuration Manager 规划 SMS 提供程序](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  

-   [为 System Center Configuration Manager 规划站点数据库](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  

-   [为 System Center Configuration Manager 规划站点系统服务器和站点系统角色](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

-   [规划 System Center Configuration Manager 中的安全性](../../../core/plan-design/security/plan-for-security.md)  

-   当在站点内部署内容时，则为[Managing network bandwidth](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) 。  


**考虑跨站点和层次结构的配置：**  

-   用于站点和层次结构的 [System Center Configuration Manager 高可用性选项](/sccm/protect/understand/high-availability-options)

-   [扩展 System Center Configuration Manager 的 Active Directory 架构](../../../core/plan-design/network/extend-the-active-directory-schema.md)，然后将所有站点配置为[发布 System Center Configuration Manager 的站点数据](../../../core/servers/deploy/configure/publish-site-data.md)  

-   [System Center Configuration Manager 中的站点间数据传输](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [System Center Configuration Manager 的基于角色的管理基础](../../../core/understand/fundamentals-of-role-based-administration.md)
