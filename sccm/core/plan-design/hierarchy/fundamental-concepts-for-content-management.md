---
title: 内容管理基础
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用工具和选项管理部署内容。
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4419a563a65ab9d98a76dcf58b48ae00e0763dab
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36260728"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Configuration Manager 中内容管理的基本概念

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 支持工具和选项的一个可靠系统，用于管理部署为应用程序、包、软件更新和 OS 部署的内容。 Configuration Manager 将内容存储在站点服务器和分发点上。 在不同位置间传输此内容时需要大量网络带宽。 为有效地规划和使用内容管理基础结构，建议了解可用选项和配置。 然后考虑如何使用它们以最好地适应网络环境和内容部署需求。  

> [!TIP]    
> 要详细了解内容分发进程以及帮助诊断和解决常规内容分发问题，请参阅[了解和解决 Microsoft Configuration Manager 中的内容分发问题](https://support.microsoft.com/help/4000401/content-distribution-in-mcm)。

以下主题是内容管理的重要概念。 当概念需要额外或复杂的信息时，将提供链接以将你转到这些详细信息。



## <a name="accounts-used-for-content-management"></a>用于内容管理的帐户  
 以下帐户可用于内容管理：  

-   **网络访问帐户**：由客户端用于连接到分发点和访问内容。 默认先尝试计算机帐户。  

     拉取分发点还使用此帐户从远程林中的源分发点下载内容。  

-   **包访问帐户**：默认情况下，Configuration Manager 向通用访问帐户“用户”和“管理员”授予访问分发点上的内容的权限。 但是，你可以配置其他权限来限制访问。   

-   **多播连接帐户**：用于 OS 部署。  

有关这些帐户的详细信息，请参阅[管理帐户以访问内容](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md)。



## <a name="bandwidth-throttling-and-scheduling"></a>带宽限制和计划  
 限制和计划选项均可帮助你控制将内容从站点服务器分发到分发点的时间。 这些功能类似于站点到站点基于文件的复制的带宽控制，但二者又没有直接关系。  

 有关详细信息，请参阅[管理网络带宽](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)。



## <a name="binary-differential-replication"></a>二进制差异复制  
 二进制差异复制 (BDR) 是分发点的先决条件。 它有时称为增量复制。 将更新分发到以前部署到其他站点或远程分发点的内容时，BDR 将自动用于减少带宽。  

 BDR 将用于发送已分发内容更新的网络带宽降至最低。 每次更改文件时，它仅重新发送新的或更改的内容，而不是发送整个内容源文件集。  

 如果使用 BDR，Configuration Manager 将标识对以前已分发的每个内容集的源文件所做的更改。  

-   当源内容中的文件发生更改时，站点会创建内容集的新增量版本。 然后，它仅将更改的文件复制到目标站点和分发点。 如果重命名、移动了该文件，或更改了其内容，则将该文件视为已更改。 例如，替换了以前分发到若干站点的驱动程序包的一个驱动程序文件，则只会复制更改的驱动程序文件。  

-   在重新发送整个内容集之前，Configuration Manager 最多支持五个内容集增量版本。 第五次更新后，对内容集的下一次更改会使该站点创建新版本的内容集。 Configuration Manager 分发新版本的内容集以替换上一个内容集和其任何增量版本。 分发新的内容集后，对源文件进行的后续增量更改会再次通过 BDR 进行复制。  

支持在层次结构中的每个父站点和子站点之间进行 BDR。 在站点内，支持在站点服务器及其常规分发点之间进行 BDR。 但是，拉取分发点和基于云的分发点不支持通过 BDR 来传输内容。 拉取分发点支持文件级增量，传输新的文件，但不是文件内的块。

应用程序始终使用二进制差异复制。 BDR 对于包是可选的，默认情况下未启用。 要对包使用 BDR，请为每个包启用此功能。 创建或编辑包时，选择“启用二进制差异复制”选项。   



## <a name="branchcache"></a>BranchCache  
 [BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) 是一项 Windows 技术。 支持 BranchCache 且下载了为 BranchCache 配置的部署的客户端随后可充当其他启用了 BranchCache 的客户端的内容源。  

 例如，有运行 Windows Server 2012 或更高版本的分发点，并将其配置为 BranchCache 服务器。 当第一个启用 BranchCache 的客户端向此服务器请求内容时，客户端将下载并缓存该内容。  

- 然后，该客户端可以使内容可用于同一子网上的其他启用 BranchCache 的客户端，这些客户端也会缓存该内容。  
- 同一子网上的其他客户端无需从分发点下载内容。  
- 该内容分布在多个客户端，以供将来传输。  

有关详细信息，请参阅[对 Windows 10 BranchCache 的支持](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache)。



## <a name="delivery-optimization"></a>传递优化
<!-- 1324696 -->使用 Configuration Manager 边界组来定义和控制跨公司网络和到远程办公室的内容分发。 [Windows 传递优化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)是一种基于云的对等技术，用于在 Windows 10 设备之间共享内容。 从版本 1802 开始，配置传递优化以在对等方之间共享内容时使用边界组。 客户端设置将边界组标识符用作客户端上的传递优化组标识符。 当客户端与传递优化云服务进行通信时，它使用此标识符来查找具有所需内容的对等方。 有关详细信息，请参阅[传递优化](/sccm/core/clients/deploy/about-client-settings#delivery-optimization)客户端设置。

对于 Windows 10 质量更新，传递优化是[优化 Windows 10 更新传递](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)快速安装文件的推荐技术。



## <a name="peer-cache"></a>对等缓存
客户端对等缓存可帮助管理对远程客户端内容的部署。 对等缓存是内置 Configuration Manager 解决方案，使客户端能够直接从本地缓存将内容与其他客户端共享。

将启用对等缓存的客户端设置部署到集合后，该集合的成员可以充当同一边界组中其他客户端的对等内容源。

有关详细信息，请参阅[用于 Configuration Manager 客户端的对等缓存](/sccm/core/plan-design/hierarchy/client-peer-cache)。



## <a name="windows-pe-peer-cache"></a>Windows PE 对等缓存
使用 Configuration Manager 部署新 OS 时，运行任务序列的计算机可以使用 Windows PE 对等缓存。 它们从对等缓存源而不是从分发点下载内容。 此行为有助于最大限度减小没有本地分发点的分支机构方案中的 WAN 流量。

有关详细信息，请参阅 [Windows PE 对等缓存](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)。



## <a name="client-locations"></a>客户端位置  
 客户端将访问以下位置中的内容：  

-   **Intranet** （本地）：  

    -   分发点可使用 HTTP 或 HTTPS。  

    -   仅当本地分发点不可用时，才使用基于云的分发点进行回退。  

-   **Internet**：  

    -   要求分发点接受 HTTPS。  

    -   可使用基于云的分发点进行回退。  

-   **工作组**：  

    -   要求分发点接受 HTTPS。  

    -   可使用基于云的分发点进行回退。  



## <a name="content-library"></a>内容库  
 内容库是 Configuration Manager 中内容的单实例存储。 此库可减少分发内容的总体大小。  

- 深入了解[内容库](../../../core/plan-design/hierarchy/the-content-library.md)。
- 使用[内容库清理工具](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool)删除不再与应用程序关联的内容。  



## <a name="distribution-points"></a>分发点  
 Configuration Manager 使用分发点存储在客户端计算机上运行软件所需的文件。 客户端必须至少可访问一个能用于下载所部属内容的文件的分发点。  

 基本（非专用）分发点通常称为标准分发点。 标准分发点有两种变体需要特别注意：  

-   **拉取分发点**：分发点的一种变体，该分发点获取其他分发点（源分发点）中的内容。 此过程与客户端从分发点下载内容的方式类似。 在站点服务器必须将内容直接分发给每个分发点时，拉取分发点有助于避免可能出现的网络带宽瓶颈。 [使用拉取分发点](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)。

-   **基于云的分发点**：安装在 Microsoft Azure 中的分发点的变体。 [了解如何使用基于云的分发点](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)。  


标准分发点支持一系列配置和功能：  

- 可使用“计划”或“带宽限制”等控件辅助控制此传输。  
- 使用其他选项，包括“预留内容”和“拉取分发点”以最小化和控制网络消耗。 
- “BranchCache”、“对等缓存”和“传递优化”是对等技术，用于减少部署内容时使用的网络带宽。  
- OS 部署有不同的配置，例如 [PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) 和[多播](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)
- “移动设备”的选项   
  
  
基于云的分发点和拉取分发点支持许多此类配置，但具有特定于各分发点变体的限制。  



## <a name="distribution-point-groups"></a>分发点组  
 分发点组是指可简化内容分发的分发点的逻辑分组。  

 有关详细信息，请参阅[管理分发点组](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)。



## <a name="distribution-point-priority"></a>分发点优先级  
 分发点优先级值取决于它将以前的部署传输到该分发点所花费的时间。  

-   此值可自调整。 它设置在每个分发点上，以帮助 Configuration Manager 更快地将内容传输到更多分发点。  

-   同时向多个分发点或分发点组分发内容时，站点会首先将内容发送到优先级最高的服务器。 然后它将相同内容发送到优先级较低的分发点。  

-   分发点优先级不会替代包的分发优先级。 包优先级仍然是站点发送不同内容的决定因素。  

例如，有一个优先级较高的包。 将其分发到分发点优先级较低的服务器。 此优先级较高的包始终在优先级较低的包之前传输。 即使站点将优先级较低的包分发到分发点优先级较高的服务器，包优先级也适用。

包的高优先级确保 Configuration Manager 在发送任何优先级较低的包之前，将该内容分发到分发点。  

> [!NOTE]  
>  请求分发点也使用优先级的概念来对其源分发点的序列进行排序。  
>   
>  -   传输到服务器的内容的分发点优先级不同于拉取分发点使用的优先级。 拉取分发点从源分发点搜索内容时使用其优先级。  
>  -   有关详细信息，请参阅[使用拉取分发点](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)。  



## <a name="fallback"></a>回退  
 在 Configuration Manager Current Branch 中，客户端找到包含内容的分发点的方式发生了诸多变化，其中包括回退。 

对于无法从与其当前边界组关联的分发点找到内容的客户端，可进行回退，使用与临近边界组关联的内容源位置。 若要实现回退，临近边界组与客户端的当前边界组必须存在定义的关系。 此关系包含配置的时间，此时间后，无法在本地找到内容的客户端才可在搜索中包含来自临近边界组的内容源。

不再使用首选分发点概念，且无法再使用或执行“允许回退内容源位置”设置。

有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)。

<!--
**Version 1511, 1602, and 1606**   
Fallback settings are related to the use of **preferred distribution points** and to content source locations that are used by clients.

-   By default, clients only download content from a preferred distribution point (one that is associated with the client's boundary groups).  

-   However, when a distribution point is configured with **Allow clients to use this site system as a fallback source location for content**, that distribution point is only offered as a valid content source to any client that can't get a deployment from one of its preferred distribution points.  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="network-bandwidth"></a>网络带宽  
 可使用以下选项，帮助管理分发内容时所用的网络带宽量：  

-   **预留内容**：将内容传输到分发点，而不通过网络分发内容。  

-   **计划和限制**：此配置有助于控制将内容分发到分发点的时间和方式。  

有关详细信息，请参阅[管理网络带宽](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)。



## <a name="network-connection-speed-to-content-source"></a>到内容源的网络连接速度  
 在 Configuration Manager Current Branch 中，客户端查找带内容的分发点的方式已发生诸多变化。 这些更改包括到内容源的网络速度。 

不再使用将分发点定义为“快”或“慢”的网络连接速度。 相反，与边界组关联的各站点系统都被视为相同的系统。

有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)。

<!--
**Version 1511, 1602, and 1606**   
 You can configure the network connection speed of each distribution point in a boundary group:  

-   Clients use this value when they connect to the distribution point.

-   By default, the network connection speed is configured as **Fast**, but it can also be set as **Slow**.  

-   The **network connection speed**, along with the configuration of a deployment, determine if a client can download content from a distribution point when the client is in an associated boundary group  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="on-demand-content-distribution"></a>按需内容分发  
 按需内容分发是个别应用程序和包部署的选项。 此选项可将内容按需分发到首选服务器。  

-   若要为部署启用此设置，请启用：“将此包的内容分发到首选分发点”。  

-   为部署启用此选项后，如果客户端尝试请求该内容而该内容在任何客户端首选分发点上都不可用，Configuration Manager 会将该内容自动分发到客户端首选分发点。  

-   尽管这会触发 Configuration Manager 将内容自动分发到客户端首选分发点，但客户端仍可在首选分发点接收到部署之前从其他分发点获取该内容。 若出现该行为，该内容将在该分发点上显示，供搜寻该部署的下一个客户端使用。  

有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)。

<!--
If you use version 1511, 1602, or 1606, see  [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) for information about the different content location and fallback scenarios.
-->



## <a name="package-transfer-manager"></a>包传输管理器  
 包传输管理器是一个站点服务器组件，该组件可将内容传输到其他计算机上的分发点。  

 有关详细信息，请参阅[包传输管理器](../../../core/plan-design/hierarchy/package-transfer-manager.md)。  



<!--
## Preferred distribution point  
 A preferred distribution point includes any distribution points that are associated with a client's current boundary groups.  

 You have the option to associate each distribution point with one or more boundary groups:  

-   This association helps the client identify distribution points from which it can download content.  
-   By default, clients can only download content from a preferred distribution point.  


For more information:
 - If you use version 1610 or later, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - If you use version 1511, 1602, or 1606, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).
-->



## <a name="prestage-content"></a>预留内容  
 预留内容是将内容传输到分发点，而不通过网络分发内容的过程。  

 有关详细信息，请参阅[管理网络带宽](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)。
