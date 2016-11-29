---
title: "内容管理基础知识 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中使用工具和选项管理部署内容。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: 28
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 27342ef83d877c31f39bc232e3e19e37b78e62da


---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中内容管理的基本概念

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 支持工具和选项的一个可靠系统，用于管理部署为应用程序、包、软件更新和操作系统部署的内容。  

 你部署的内容将同时存储在站点服务器和分发点站点系统服务器上。 在不同位置间进行传输时，此内容可能需要大量的网络带宽。  为了有效地规划和使用内容管理基础结构，应了解可用的选项和配置，然后考虑如何使用这些选项和配置在最大限度上适应你的网络环境并满足内容部署需求。  

随后是内容管理的关键概念。 当概念需要额外或复杂的信息时，将提供链接以将你转到这些详细信息。  

## <a name="accounts-used-for-content-management"></a>用于内容管理的帐户  
 以下帐户可用于内容管理：  

-   **网络访问帐户** - 由客户端用于连接到分发点和访问内容。 默认情况下，客户端将首先尝试其计算机帐户  

     此帐户还由请求分发点用于从远程林中的源分发点获取内容  

-   **包访问帐户** - 默认情况下，Configuration Manager 向通用访问帐户“用户”和“管理员”授予对分发点上内容的访问权限。 但是，你可以配置其他权限来限制访问。 请参阅&lt;管理帐户以访问包内容\>  

-   **多播连接帐户** - 用于操作系统部署  

有关这些帐户的详细信息，请参阅[管理帐户以访问内容](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md)

## <a name="bandwidth-throttling-and-scheduling"></a>带宽限制和计划  
 限制和计划选项均可帮助你控制将内容从站点服务器分发到分发点的时间。 这类似于站点到站点基于文件的复制的带宽控制，但二者又没有直接关系。  

 有关详细信息，请参阅[管理网络带宽](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)

## <a name="binary-differential-replication"></a>二进制差异复制  
 二进制差异复制 (BDR) 是分发点的必备条件，它有时称为增量复制，在将以前部署的内容的更新分发到其他站点或远程分发点时，将自动将其用于减少带宽使用。  

 BDR 只会发送新内容或已更改的内容，而不会在每次对文件进行更改时发送整个内容源文件集，从而可最大程度地减少用于为分发内容而发送更新的网络带宽。  

 如果使用二进制差异复制，Configuration Manager 将标识对以前已分发的每组内容的源文件所做的更改。  

-   源内容中的文件发生更改时，Configuration Manager 将创建内容集新的增量版本，并仅将更改的文件复制到目标站点和分发点。 如果重命名、移动了文件，或者文件的内容发生更改，则将文件视为已更改。 例如，你替换了以前分发到若干站点的操作系统部署包的单一驱动程序文件，则只会将更改的驱动程序文件复制到那些目标站点。  

-   在重新发送整个内容集之前，Configuration Manager 最多支持五个内容集增量版本。 第五次更新后，对内容集的下一次更改会使 Configuration Manager 创建新版本的内容集。 Configuration Manager 分发新版本的内容集以替换上一个内容集和其任何增量版本。 分发新的内容集后，对源文件进行的后续增量更改会再次通过二进制差异复制进行复制。  


支持在层次结构中的每个父站点和子站点之间进行 BDR。 在站点内，支持在站点服务器和其分发点之间进行 BDR。 此项支持包括请求分发点，但不包括基于云的分发点。 基于云的分发点不支持二进制差异复制来传输内容。  

应用程序始终使用二进制差异复制。 对于包，二进制差异复制是可选的，默认情况下未启用。 若要为包使用二进制差异复制，你必须为每个包启用此功能。 为此，请在创建新包或编辑包属性的“数据源”  选项卡时选择“启用二进制差异复制”  选项。  

## <a name="branchcache"></a>BranchCache  
 一项 Windows 技术，它使得支持 BranchCache 且下载了为分支缓存配置的部署的客户端能够届时充当其他 BranchCache 启用的客户端的内容源。  

 例如，当第一台 BranchCache 启用的客户端计算机从运行 Windows Server 2012 并且被配置为 BranchCache 服务器的分发点请求内容时，客户端计算机将下载此内容并对其进行缓存。  

-   该客户端计算机然后可以使内容可用于同一子网上的其他分支缓存启用的客户端，这些客户端也会缓存该内容。  

-   这样，相同子网上的后续客户端不必从分发点下载内容，该内容将跨多个客户端进行分发以便将来传输。  





## <a name="windows-pe-peer-cache"></a>Windows PE 对等缓存
在 System Center Configuration Manager 中部署新的操作系统时，运行任务序列的计算机可使用 Windows PE 对等缓存从本地对等计算机（对等缓存源）中获取内容，而无需从分发点下载内容。 这有助于最大限度减小没有本地分发点的分支机构场景中的广域网 (WAN) 流量。

有关详细信息，请参阅 [Windows PE 对等缓存](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)


## <a name="client-locations"></a>客户端位置  
 客户端将访问以下位置中的内容：  

-   **Intranet** （本地）：  

    -   分发点可使用 HTTP 或 HTTPs  

    -   仅当本地分发点不可用时，才将基于云的分发点用于回退  

-   **Internet** ：  

    -   要求分发点接受 HTTPS  

    -   可将基于云的分发点用于回退  

-   **工作组**：  

    -   要求分发点接受 HTTPS  

    -   可将基于云的分发点用于回退  



## <a name="content-library"></a>内容库  
 内容的单实例存储，Configuration Manager 使用它来减少分发内容的组合正文的总体大小。  

了解关于[内容库](../../../core/plan-design/hierarchy/the-content-library.md)的详细信息


## <a name="distribution-point"></a>分发点  
 Configuration Manager 使用分发点存储在客户端计算机上运行软件所需的文件。 客户端必须对它们可从中下载你部署内容的文件的至少一个分发点具有访问权限。  

 基本（非专用）分发点通常称为标准分发点。  标准分发点有两种变体需要特别注意：  

-   **请求分发点** - 分发点的一种变体，其中分发点从另一个分发点（源分发点）获取内容，获取方式类似于客户端从分发点下载内容。 请求分发点可帮助你在站点服务器必须将内容直接分发给每个分发点时避免可能出现的网络带宽瓶颈。  [结合使用请求分发点与 System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

-   **基于云的分发点** - 安装在 Microsoft Azure 中的分发点的变体。 [结合使用基于云的分发点与 System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  


标准分发点支持一系列的配置和功能，如限制和计划、PXE 和多播或预留内容。  

-   可以使用如**计划**或**带宽限制**等控件来帮助控制此传输。  

-   还可以使用其他选项（包括“预留内容”、“请求分发点”）或利用“BranchCache”来减少部署内容时使用的网络带宽。  

-   分发点支持用于操作系统部署的 **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** 和**[多播](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**等不同的配置，或支持用于支持**移动设备**的配置  

 基于云的请求分发点支持许多相同的配置，但对每个分发点变体都有特定的限制。  

## <a name="distribution-point-group"></a>分发点组  
 可以简化内容分发的分发点逻辑分组。  

 有关详细信息，请参阅[管理分发点组](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)

## <a name="distribution-point-priority"></a>分发点优先级  
 分发点优先级值取决于它将以前的部署传输到该分发点所花费的时间。  

-   这是分配给分发点一个自我调整值，可帮助 Configuration Manager 在更短时间内将内容传输到更多分发点  

-   在将内容同时分发到多个分发点或分发到分发点组时，Configuration Manager 会将内容发送到优先级最高的分发点，之后再将该相同内容发送到优先级较低的分发点。  

-   它不会替换包的分发优先级，后者仍然是决定不同分发传输时间顺序的决定性因素  


**例如，** 你将具有高分发优先级的内容分发到具有低分发点优先级的分发点，则此高分发优先级包始终会在具有较低分发优先级的包之前传输。 即使具有较低分发优先级的包分发到具有较高分发点优先级的分发点，此分发优先级也适用。 包的高分发优先级确保 Configuration Manager 在发送具有较低分发优先级的任何包之前将该内容分发到其适用的分发点。  

> [!NOTE]  
>  请求分发点也使用优先级的概念来对其源分发点的序列进行排序。  
>   
>  -   针对分发点的内容传输的分发点优先级与请求分发点在从源分发点中搜索内容时使用的优先级不同  
> -   有关详细信息，请参阅[将请求分发点用于 System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  


## <a name="fallback"></a>回退  
 回退设置与 **首选分发点** 的使用和客户端使用的内容源位置相关。  

-   默认情况下，客户端仅从（与客户端的边界组关联的）首选分发点下载内容  

-   但是，当分发点配置为“允许客户端使用此站点系统作为内容的回退源位置”时，该分发点仅可作为有效的内容源提供给任何无法从其首选分发点之一获取部署的客户端。  


有关不同的内容位置和回退方案的信息，请参阅[内容源位置方案](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)。

## <a name="network-bandwidth"></a>网络带宽  
 可以使用以下选项，帮助管理分发内容时所使用的网络带宽量：  

-   使用预安排内容：此进程可将内容传输到分发点，而不依赖 Configuration Manager 通过网络分发内容。  

-   使用计划和限制：此配置有助于控制将内容分发到分发点的时间和方式。  

有关详细信息，请参阅[管理网络带宽](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)

## <a name="network-connection-speed-to-content-source"></a>到内容源的网络连接速度  
 你可以配置边界组中每个分发点的网络连接速度：  

-   客户端在连接到分发点时使用此值  

-   默认情况下，网络连接速度配置为 **快**，但也可将其设置为 **慢**  

-   **网络连接速度** 和部署配置确定当客户端位于关联的边界组中时是否能从分发点下载内容  


有关不同的内容位置和回退方案的信息，请参阅[内容源位置方案](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  

## <a name="on-demand-content-distribution"></a>按需内容分发  
 可为个别应用程序和包（部署）设置的一个选项，用于启用向首选分发点进行按需内容分发。  

-   要为部署启用此选项，请启用 **将此包的内容分发到首选分发点**  

-   为部署启用此选项后，当客户端尝试请求该内容而该内容在任何客户端首选分发点上都不可用时，Configuration Manager 会将该内容自动分发到客户端首选分发点  

-   尽管这会触发 Configuration Manager 将内容自动分发到客户端首选分发点，但客户端仍可在其首选分发点接收到部署之前从其他分发点获取该内容。 当出现这种情况时，该内容将会显示在该分发点上，供搜寻该部署的下一个客户端使用  


有关不同的内容位置和回退方案的信息，请参阅[内容源位置方案](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  


## <a name="package-transfer-manager"></a>包传输管理器  
 将内容传输到其他计算机上分发点的站点服务器组件。  

 了解关于[包传输管理器](../../../core/plan-design/hierarchy/package-transfer-manager.md)的详细信息  

## <a name="preferred-distribution-point"></a>首选分发点  
 与客户端当前边界组关联的分发点。  

 你可以选择将每个分发点关联到一个或多个边界组：  

-   这种关联帮助客户端标识它可以从其中下载内容的分发点  

-   默认情况下，客户端只能从首选分发点下载内容  


有关不同的内容位置和回退方案的信息，请参阅[内容源位置方案](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  

## <a name="prestage-content"></a>预留内容  
 此进程可将内容传输到分发点，而不依赖 Configuration Manager 通过网络分发内容。  

 有关详细信息，请参阅[管理网络带宽](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)



<!--HONumber=Nov16_HO1-->


