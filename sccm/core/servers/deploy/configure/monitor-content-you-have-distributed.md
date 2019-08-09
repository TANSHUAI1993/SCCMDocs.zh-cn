---
title: 监视内容
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 控制台监视分发的内容。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37bb1386284fa80d362479242a693b1a6f9b45a3
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536485"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>使用 Configuration Manager 监视分发的内容

适用范围：  System Center Configuration Manager (Current Branch)

使用 Configuration Manager 控制台监视分发的内容，包括：  

- 关联的分发点的所有包类型的状态。  
- 包中内容的内容验证状态。  
- 分配给特定分发点组的内容的状态。  
- 分配给分发点的内容的状态。  
- 每个分发点（内容验证、PXE 和多播）可选功能的状态。  

> [!NOTE]  
> Configuration Manager 仅监视分发点上位于内容库中的内容。 而不会监视存储在分发点上的包或自定义共享中的内容。  

## <a name="BKMK_ContentStatus"></a> 内容状态监视

“监视”  工作区中的“内容状态”  节点提供有关内容包的信息。 在 Configuration Manager 控制台中，可以查看如下信息：  

- 包名称、类型和 ID
- 已将包发送到多少个分发点
- 符合性比率
- 创建包的时间
- 源版本

你还可以找到任何包的详细状态信息，包括：  

- 分发状态
- 失败次数
- 挂起的分发  
- 安装次数

还可管理仍在向分发点进行的分发或未能成功向分发点分发内容的分发：  

- 当在“资产详细信息”  窗格中查看针对分发点的分发作业的部署状态消息时，可使用取消或重新分发内容选项。 此窗格位于“内容状态”  节点的“正在进行”  选项卡或“错误”  选项卡中。  
- 此外，当在“正在进行”  选项卡上查看作业详细信息时，作业详细信息会显示作业完成的百分比。作业详细信息还会显示保留作业的重试次数。 当你在“错误”  选项卡上查看作业的详细信息时，它会显示下次重试之前的等待时间。  

当你取消尚未完成的部署时，用于传输该内容的分发作业将停止：  

- 部署的状态随后将更新以指示分发失败并且被用户操作取消。  
- 这个新状态出现在“错误”  选项卡中。  

> [!NOTE]  
> 当部署接近完成时，用于取消该分发的操作有可能不会在针对分发点的分发完成之前进行。 如果出现这种情况，则会忽略用于取消部署的操作，并且部署的状态显示为成功。  
>
> 尽管你可以选择选项来取消针对位于站点服务器上的分发点的分发，但此操作不起作用。 此行为是因为站点服务器和站点服务器上的分发点共享相同的单一实例内容存储。 没有要取消的实际分发作业。  

当重新分发以前未能传输到分发点的内容时，Configuration Manager 会立即开始将该内容再次部署到分发点。 Configuration Manager 更新部署的状态以反映重新部署正在进行的状态。  

### <a name="tasks-to-monitor-content"></a>监视内容的任务

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“分发状态”，然后选择“内容状态”节点    。 此节点会显示包。  

2. 选择要管理的包。  

3. 在功能区的“主页”  选项卡上的“内容”  组中，选择“查看状态”  。 控制台会显示包的详细状态信息。

继续执行其他操作的以下部分之一：

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>取消仍在进行的分发  

1. 切换到“正在进行”  选项卡。

2. 在“资产详细信息”窗格中，右键单击要取消的分发的条目，并选择“取消”   。  

3. 选择“是”  确认操作并取消针对该分发点的分发作业。  

#### <a name="redistribute-content-that-failed-to-distribute"></a>重新分发未能分发的内容  

1. 切换到“错误”  选项卡。

2. 在“资产详细信息”窗格中，右键单击要重新分发的分发的条目，并选择“重新分发”   。  

3. 选择“是”  确认操作并开始针对该分发点的重新分发过程。  


## <a name="distribution-point-group-status"></a>分发点组状态

“监视”  工作区中的“分发点组状态”  节点提供有关分发点组的信息。 你可以查看如下信息：  

- 分发点组名称、说明和状态
- 属于分发点组成员的分发点数
- 已分发到组的包数
- 符合性比率

你还可以查看以下详细状态信息：  

- 分发点组错误  
- 正在进行的分发数
- 已成功分发的数量  

### <a name="monitor-distribution-point-group-status"></a>监视分发点组状态  

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“分发状态”，然后选择“分发点组状态”节点    。 此时会显示分发点组。  

2. 选择要查看其详细状态信息的分发点组。  

3. 在功能区的“主页”选项卡上，选择“查看状态”   。 此时会显示分发点组的详细状态信息。  


## <a name="distribution-point-configuration-status"></a>分发点配置状态

“监视”  工作区中的“分发点配置状态”  节点提供有关分发点的信息。 可以查看为分发点启用的属性，例如 PXE、多播和内容验证。 还可以查看分发点的分发状态。

> [!WARNING]  
> 分发点配置状态是过去 24 小时的状态。 如果分发点出错并恢复，则可能会显示分发点恢复后最多 24 小时的错误状态。  

### <a name="monitor-distribution-point-configuration-status"></a>监视分发点配置状态  

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“分发状态”，然后选择“分发点配置状态”节点    。  

2. 选择分发点。  

3. 在结果窗格中，切换到“详细信息”  选项卡。此时会显示分发点的状态信息。  


## <a name="client-data-sources-dashboard"></a>客户端数据源仪表板

使用客户端数据源  仪表板可以更好地了解客户端在你的环境中获取内容的位置。 客户端下载内容后，仪表板将开始显示数据，并将该信息报告给网站。 此过程最多可能需要 24 小时。

> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须先启用“客户端对等缓存”  功能，然后才能使用它。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。  

在 Configuration Manager 控制台中，转到“监视”工作区，展开“分发状态”，然后选择“客户端数据源”节点    。 选择要应用于仪表板的时间段。 然后选择要查看其信息的边界组。 可以将鼠标悬停在磁贴上方，以查看有关不同内容或策略源的更多详细信息。

还可以使用报表“客户端数据源 - 摘要”  查看每个边界组的客户端数据源摘要。

### <a name="dashboard-tiles"></a>仪表板磁贴

该仪表板具有以下磁贴：  

#### <a name="client-content-sources"></a>客户端内容源

显示客户端从其处获取内容的源：

- 分发点
- [云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)
- [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache)
- [对等缓存](/sccm/core/plan-design/hierarchy/client-peer-cache)
- [传递优化](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization)（从版本 1906 开始）<sup>[注释 1](#bkmk_note1)</sup>
- Microsoft 更新：Configuration Manager 客户端从 Microsoft 云服务下载软件更新时，设备会报告此源。 这些服务包括 Microsoft 更新和 Office 365。

![仪表板上的客户端内容源磁贴](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> 从版本 1906 开始<!--3555759-->，要在此仪表板上包含传递优化，请执行以下操作：
>
> - 配置客户端设置，在“软件更新”组中的客户端上启用 Express 更新的安装 
>
> - 部署 Windows 10 快速更新
>
> 有关详细信息，请参阅[管理 Windows 10 更新的快速安装文件](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)。

#### <a name="distribution-points"></a>分发点

显示属于所选边界组的分发点的数量。

#### <a name="clients-that-used-a-distribution-point"></a>使用分发点的客户端

此磁贴显示所选边界组中使用了分发点来获取内容的客户端的数量。

#### <a name="peer-cache-sources"></a>对等缓存源

对于所选的边界组，此磁贴显示已报出曾进行过下载操作的对等缓存源的数量。

#### <a name="clients-that-used-a-peer"></a>使用对等的客户端

此磁贴显示所选边界组中使用了对等缓存源来获取内容的客户端的数量。

#### <a name="top-distributed-content"></a>分发最多的内容

分发最多的内容（按源类型）
