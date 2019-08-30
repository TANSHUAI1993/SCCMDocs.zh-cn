---
title: 内容管理基础
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用工具和选项管理部署内容。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e53e5fc081be04209312cd3144c38d0ecd944fc1
ms.sourcegitcommit: 04dd0c17e47763a3e2b6c44c005428ea7d67f4bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70021953"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Configuration Manager 中内容管理的基本概念

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager 支持可靠的工具和选项系统来管理软件内容。 软件部署（如应用程序、包、软件更新和 OS 部署）都需要内容。 Configuration Manager 将内容存储在站点服务器和分发点上。 在不同位置间传输此内容时需要大量网络带宽。 为有效地规划和使用内容管理基础结构，首先了解可用选项和配置。 然后考虑如何使用它们以最好地适应网络环境和内容部署需求。  

> [!TIP]  
> 要详细了解内容分发进程以及帮助诊断和解决常规内容分发问题，请参阅[了解和解决 Microsoft Configuration Manager 中的内容分发问题](https://support.microsoft.com/help/4000401/content-distribution-in-mcm)。

以下部分是内容管理的重要概念。 当概念需要额外或复杂的信息时，将提供链接以将你转到这些详细信息。


## <a name="accounts-used-for-content-management"></a>用于内容管理的帐户

以下帐户可用于内容管理：  

### <a name="network-access-account"></a>网络访问帐户

由客户端用于连接到分发点和访问内容。 默认先尝试计算机帐户。  

拉取分发点还使用此帐户从远程林中的源分发点下载内容。  

从 1806 版开始，某些方案不再需要网络访问帐户。 可使站点搭配使用增强型 HTTP 和 Azure Active Directory 身份验证。<!--1358228-->

有关详细信息，请参阅[网络访问帐户](/sccm/core/plan-design/hierarchy/accounts#network-access-account)。

### <a name="package-access-account"></a>包访问帐户

默认情况下，Configuration Manager 向通用访问帐户“用户”和“管理员”授予访问分发点上的内容的权限。 但是，你可以配置其他权限来限制访问。

有关详细信息，请参阅[包访问帐户](/sccm/core/plan-design/hierarchy/accounts#package-access-account)。


## <a name="bandwidth-throttling-and-scheduling"></a>带宽限制和计划

限制和计划选项均可帮助你控制将内容从站点服务器分发到分发点的时间。 这些功能类似于站点到站点基于文件的复制的带宽控制，但二者又没有直接关系。  

有关详细信息，请参阅[管理网络带宽](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)。


## <a name="binary-differential-replication"></a>二进制差异复制

Configuration Manager 使用二进制差异复制 (BDR) 更新以前分发到其他站点或远程分发点的内容。 要支持 BDR 减少对带宽的使用，请在分发点上安装“远程差分压缩”功能  。 有关详细信息，请参阅[分发点先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012dppreq)。

BDR 将用于发送已分发内容更新的网络带宽降至最低。 每次更改文件时，它仅重新发送新的或更改的内容，而不是发送整个内容源文件集。  

如果使用 BDR，Configuration Manager 将标识对以前已分发的每个内容集的源文件所做的更改。  

- 当源内容中的文件发生更改时，站点会创建内容的新增量版本。 然后，它仅将更改的文件复制到目标站点和分发点。 如果重命名、移动了该文件，或更改了其内容，则将该文件视为已更改。 例如，替换了以前分发到若干站点的驱动程序包的一个驱动程序文件，则只会复制更改的驱动程序文件。  

- 在重新发送整个内容集之前，Configuration Manager 最多支持五个内容集增量版本。 第五次更新后，对内容集的下一次更改会使该站点创建新版本的内容集。 Configuration Manager 分发新版本的内容集以替换上一个内容集和其任何增量版本。 分发新的内容集后，对源文件进行的后续增量更改会再次通过 BDR 进行复制。  

支持在层次结构中的每个父站点和子站点之间进行 BDR。 在站点内，支持在站点服务器及其常规分发点之间进行 BDR。 但是，拉取分发点和云分发点不支持通过 BDR 来传输内容。 拉取分发点支持文件级增量，传输新的文件，但不是文件内的块。

应用程序始终使用二进制差异复制。 BDR 对于包是可选的，默认情况下未启用。 要对包使用 BDR，请为每个包启用此功能。 创建或编辑包时，选择“启用二进制差异复制”选项  。


### <a name="bdr-or-delta-replication"></a>BDR 或增量复制

<!-- SCCMDocs#1209 -->
以下列表汇总了二进制差异复制  (BDR) 与增量复制  之间的差异。

#### <a name="summary-of-binary-differential-replication"></a>二进制差异复制的摘要

- Windows 远程差分压缩的 Configuration Manager 术语 
-  块级差异
- 始终为应用启用
- 在旧包上可选
- 如果某个文件已存在于分发点上，并且发生了更改，则站点将使用 BDR 复制块级更改，而不是整个文件。

#### <a name="summary-of-delta-replication"></a>增量复制的摘要

-  文件级差异
- 默认情况下，不可配置
- 当包发生更改时，站点将检查对单个文件而不是整个包的更改。
    - 如果文件发生更改，请使用 BDR 来完成工作
    - 如果有新文件，请复制该新文件


## <a name="peer-caching-technologies"></a>对等缓存技术

<!-- SCCMDocs#1044 -->

Configuration Manager 支持用于管理同一网络上的对等设备之间的内容的多种选项：

- [BranchCache](#branchcache)
- [传递优化](#delivery-optimization)
- [Configuration Manager 对等缓存](#peer-cache)

使用下表来比较这些技术的主要功能：

| 功能  | 对等&nbsp;缓存  | 传递&nbsp;优化  | BranchCache  |
|---------|---------|---------|---------|
| 跨子网 | 是 | 是 | 否 |
| 限制带宽 | 是 (BITS) | 是（本机） | 是 (BITS) |
| 部分内容 | 是 | 是 | 是 |
| 控制磁盘上的缓存大小 | 是 | 是 | 是 |
| 对等源发现 | 手动（客户端设置） | 自动 | 自动 |
| 对等发现 | 通过管理点（使用边界组） | 提供云服务 | 广播 |
| 报表 | 客户端数据源仪表板 | 客户端数据源仪表板 | 客户端数据源仪表板 |
| WAN 使用控制 | 边界组 | 提供 GroupID | 仅子网 |
| 支持的内容 | 所有 ConfigMgr 内容 | Windows 更新、驱动程序、应用商店应用 | 所有 ConfigMgr 内容 |
| 策略控制 | 客户端代理设置 | 客户端代理设置（部分） | 客户端代理设置 |

### <a name="recommendations"></a>建议

- 新式管理：如果已使用 Intune 等新式工具，请实现传递优化

- Configuration Manager 和共同管理：使用对等缓存和传递优化的组合。 使用具有本地分发点的对等缓存，并对云方案使用传递优化。

- 已实现现有 BranchCache：并行使用所有三种技术。 对 BranchCache 不支持的方案使用对等缓存和传递优化。


## <a name="branchcache"></a>BranchCache

[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) 是一项 Windows 技术。 支持 BranchCache 且下载了为 BranchCache 配置的部署的客户端随后可充当其他启用了 BranchCache 的客户端的内容源。  

例如，有运行 Windows Server 2012 或更高版本的分发点，并将其配置为 BranchCache 服务器。 当第一个启用 BranchCache 的客户端向此服务器请求内容时，客户端将下载并缓存该内容。  

- 然后，该客户端可以使内容可用于同一子网上的其他启用 BranchCache 的客户端，这些客户端也会缓存该内容。  
- 同一子网上的其他客户端无需从分发点下载内容。  
- 该内容分布在多个客户端，以供将来传输。  

有关详细信息，请参阅[对 Windows 10 BranchCache 的支持](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache)。


## <a name="delivery-optimization"></a>传递优化

<!-- 1324696 -->
使用 Configuration Manager 边界组来定义和控制跨公司网络和到远程办公室的内容分发。 [Windows 传递优化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)是一种基于云的对等技术，用于在 Windows 10 设备之间共享内容。 配置传递优化以在对等方之间共享内容时使用边界组。 客户端设置将边界组标识符用作客户端上的传递优化组标识符。 当客户端与传递优化云服务进行通信时，它使用此标识符来查找具有内容的对等方。 有关详细信息，请参阅[传递优化](/sccm/core/clients/deploy/about-client-settings#delivery-optimization)客户端设置。

对于 Windows 10 质量更新，传递优化是[优化 Windows 10 更新传递](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)快速安装文件的推荐技术。


## <a name="delivery-optimization-in-network-cache"></a>传递优化网络内缓存

<!--3555764-->
从版本 1906 开始，可以在分发点上安装传递优化网络内缓存 (DOINC) 服务器。 通过将此内容缓存在本地，你的客户端可以从传递优化功能中受益，但你可帮助保护 WAN 链接。

此缓存服务器充当由传递优化下载的内容的按需透明缓存。 使用客户端设置以确保此服务器仅提供给本地 Configuration Manager 边界组的成员。

此缓存独立于 Configuration Manager 分发点内容。 如果选择和分发点角色一样的驱动，它将单独存储内容。

有关详细信息，请参阅 [Configuration Manager 中的传递优化网络内缓存](/sccm/core/plan-design/hierarchy/delivery-optimization-in-network-cache)。


## <a name="peer-cache"></a>对等缓存

客户端对等缓存可帮助管理对远程客户端内容的部署。 对等缓存是内置 Configuration Manager 解决方案，使客户端能够直接从本地缓存将内容与其他客户端共享。

首先将启用对等缓存的客户端设置部署到集合。 然后，该集合的成员可充当同一边界组中其他客户端的对等内容源。

从版本 1806 开始，客户端对等缓存源可以将内容分成多个部分。 这些部分最大限度地减少了网络传输，从而降低了 WAN 利用率。 管理点提供更详细的内容部分跟踪。 它试图消除每个边界组多次下载相同内容的行为。<!--1357346-->

有关详细信息，请参阅[用于 Configuration Manager 客户端的对等缓存](/sccm/core/plan-design/hierarchy/client-peer-cache)。


## <a name="windows-pe-peer-cache"></a>Windows PE 对等缓存

使用 Configuration Manager 部署新 OS 时，运行任务序列的计算机可以使用 Windows PE 对等缓存。 它们从对等缓存源而不是从分发点下载内容。 此行为有助于最大限度减小没有本地分发点的分支机构方案中的 WAN 流量。

有关详细信息，请参阅 [Windows PE 对等缓存](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic)。


## <a name="windows-ledbat"></a>Windows LEDBAT

<!--1358112-->
Windows 低额外延迟后台传输 (LEDBAT) 是 Windows Server 的一项网络拥塞控制功能，可帮助管理后台网络传输。 对于在受支持版本的 Windows Server 上运行的分发点，请启用一个选项以帮助调整网络流量。 然后，客户端仅在允许的情况下使用网络带宽。

有关 Windows LEDBAT 的详细信息，请参阅[新建传输改进](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726)博客文章。

有关如何将 Windows LEDBAT 与 Configuration Manager 分发点一起使用的详细信息，在[配置分发点的常规设置时](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-general)，请参阅设置“调整下载速度以使用未使用的网络带宽 (Windows LEDBAT)”  。


## <a name="client-locations"></a>客户端位置

客户端将访问以下位置中的内容：  

- **Intranet** （本地）：  

    - 分发点可使用 HTTP 或 HTTPS。  

    - 仅当本地分发点不可用时，才使用云分发点进行回退。  

- **Internet**：  

    - 要求面向 Internet 的分发点接受 HTTPS。  

    - 可使用云分发点或云管理网关 (CMG)。  

        从版本 1806 开始，CMG 也可向客户端提供内容。 此功能减少了所需的证书和 Azure VM 的成本。 有关详细信息，请参阅[修改 CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)。

- **工作组**：  

    - 要求分发点接受 HTTPS。  

    - 可使用云分发点或 CMG。  


## <a name="content-source-priority"></a>内容源优先级

当客户端需要内容时，它会向管理点发出内容位置请求。 管理点返回对所请求内容有效的源位置列表。 此列表因具体方案、使用的技术、站点设计、边界组和部署设置而异。 以下列表包含客户端可使用的所有可能的内容源位置，按其优先级排序：  

1. 与客户端位于同一台计算机上的分发点
2. 同一网络子网中的对等源
3. 同一网络子网中的分发点
4. 同一边界组中的对等源
5. 当前边界组中的分发点
6. 为回退配置的临近边界组中的分发点
7. 默认站点边界组中的分发点
8. Windows 更新云服务
9. 面向 Internet 的分发点
10. Azure 中的云分发点

> [!Note]  
> <!-- SCCMDocs#1607 -->传递优化不适用于此源优先级。 此列表介绍 Configuration Manager 客户端查找内容的方式。 Windows 更新代理下载内容进行传递优化。 如果 Windows 更新代理找不到内容，则 Configuration Manager 客户端使用此列表搜索该内容。

## <a name="content-library"></a>内容库

内容库是 Configuration Manager 中内容的单实例存储。 此库可减少分发内容的总体大小。  

- 深入了解[内容库](/sccm/core/plan-design/hierarchy/the-content-library)。
- 使用[内容库清理工具](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool)删除不再与应用程序关联的内容。  


## <a name="distribution-points"></a>分发点

Configuration Manager 使用分发点存储在客户端计算机上运行软件所需的文件。 客户端必须至少可访问一个能用于下载所部属内容的文件的分发点。  

基本（非专用）分发点通常称为标准分发点。 标准分发点有两种变体需要特别注意：  

- **拉取分发点**：分发点的一种变体，该分发点获取其他分发点（源分发点）中的内容。 此过程与客户端从分发点下载内容的方式类似。 在站点服务器必须将内容直接分发给每个分发点时，拉取分发点有助于避免可能出现的网络带宽瓶颈。 [使用拉取分发点](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)。

- **云分发点**：在 Microsoft Azure 中安装的分发点的变体。 [了解如何使用云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)。  

标准分发点支持一系列配置和功能：  

- 可使用“计划”或“带宽限制”等控件辅助控制此传输   。  

- 使用其他选项，包括“预留内容”和“拉取分发点”以最小化和控制网络消耗   。  

- “BranchCache”、“对等缓存”和“传递优化”是对等技术，用于减少部署内容时使用的网络带宽    。  

- OS 部署有不同的配置，例如 [PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint) 和[多播](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_DPMulticast)    

- “移动设备”的选项   
  
云分发点和拉取分发点支持许多此类配置，但具有特定于各分发点变体的限制。  


## <a name="distribution-point-groups"></a>分发点组

分发点组是指可简化内容分发的分发点的逻辑分组。  

有关详细信息，请参阅[管理分发点组](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage)。


## <a name="distribution-point-priority"></a>分发点优先级

分发点优先级值取决于它将以前的部署传输到该分发点所花费的时间。  

- 此值可自调整。 它设置在每个分发点上，以帮助 Configuration Manager 更快地将内容传输到更多分发点。  

- 同时向多个分发点或分发点组分发内容时，站点会首先将内容发送到优先级最高的服务器。 然后它将相同内容发送到优先级较低的分发点。  

- 分发点优先级不会替代包的分发优先级。 包优先级仍然是站点发送不同内容的决定因素。  

例如，有一个优先级较高的包。 将其分发到分发点优先级较低的服务器。 此优先级较高的包始终在优先级较低的包之前传输。 即使站点将优先级较低的包分发到分发点优先级较高的服务器，包优先级也适用。

包的高优先级确保 Configuration Manager 在发送任何优先级较低的包之前，将该内容分发到分发点。  

> [!NOTE]  
> 请求分发点也使用优先级的概念来对其源分发点的序列进行排序。  
>
> - 传输到服务器的内容的分发点优先级不同于拉取分发点使用的优先级。 拉取分发点从源分发点搜索内容时使用其优先级。  
> - 有关详细信息，请参阅[使用拉取分发点](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)。  


## <a name="fallback"></a>回退

在 Configuration Manager Current Branch 中，客户端找到包含内容的分发点的方式发生了诸多变化，其中包括回退。

对于无法从与其当前边界组关联的分发点找到内容的客户端，可进行回退，使用与临近边界组关联的内容源位置。 若要实现回退，临近边界组与客户端的当前边界组必须存在定义的关系。 此关系包含配置的时间，此时间后，无法在本地找到内容的客户端才可在搜索中包含来自临近边界组的内容源。

不再使用首选分发点概念，且无法再使用或执行“允许回退内容源位置”  设置。

有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/boundary-groups)。


## <a name="network-bandwidth"></a>网络带宽

可使用以下选项，帮助管理分发内容时所用的网络带宽量：  

- **预留内容**：将内容传输到分发点，而不通过网络分发内容。  

- **计划和限制**：此配置有助于控制将内容分发到分发点的时间和方式。  

有关详细信息，请参阅[管理网络带宽](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)。


## <a name="network-connection-speed-to-content-source"></a>到内容源的网络连接速度

在 Configuration Manager Current Branch 中，客户端查找带内容的分发点的方式已发生诸多变化。 这些更改包括到内容源的网络速度。

不再使用将分发点定义为“快”  或“慢”  的网络连接速度。 相反，与边界组关联的各站点系统都被视为相同的系统。

有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/boundary-groups)。


## <a name="on-demand-content-distribution"></a>按需内容分发

按需内容分发是个别应用程序和包部署的选项。 此选项可将内容按需分发到首选服务器。  

- 要为部署启用此设置，请启用以下选项：将此包的内容分发到首选分发点  。  

- 为部署启用此选项后，如果客户端请求该内容而该内容在任何客户端首选分发点上都不可用，Configuration Manager 会将该内容自动分发到客户端首选分发点。  

- 尽管这会触发 Configuration Manager 将内容自动分发到客户端首选分发点，但客户端仍可在首选分发点接收到部署之前从其他分发点获取该内容。 若出现该行为，该内容将在该分发点上显示，供搜寻该部署的下一个客户端使用。  

有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/boundary-groups)。


## <a name="package-transfer-manager"></a>包传输管理器

包传输管理器是一个站点服务器组件，该组件可将内容传输到其他计算机上的分发点。  

有关详细信息，请参阅[包传输管理器](/sccm/core/plan-design/hierarchy/package-transfer-manager)。  


## <a name="prestage-content"></a>预留内容

预留内容是将内容传输到分发点，而不通过网络分发内容的过程。  

有关详细信息，请参阅[管理网络带宽](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)。
