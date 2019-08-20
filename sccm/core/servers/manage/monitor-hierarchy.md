---
title: 监视层次结构
titleSuffix: Configuration Manager
description: 了解如何使用控制台中的“监视”工作区在 Configuration Manager 中监视基础结构。
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bd15890bf08d9db359f336b3ca68914fa9c2a9c6
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957847"
---
# <a name="monitor-the-hierarchy"></a>监视层次结构

适用范围：  System Center Configuration Manager (Current Branch)

若要在 Configuration Manager 中监视层次结构，请使用 Configuration Manager 控制台中的“监视”  工作区。  

> [!NOTE]  
> 迁移站点时会出现此位置的例外情况。 在“管理”工作区的“迁移”节点中监视此过程   。 有关详细信息，请参阅 [用于迁移到 System Center Configuration Manager 的操作](/sccm/core/migration/operations-for-migration)。  

除了使用 Configuration Manager 控制台进行监视外，还可以使用以下功能：

- [报表](/sccm/core/servers/manage/reporting)
- [日志文件](/sccm/core/plan-design/hierarchy/log-files)。  

在监视站点时，请查看指示需要你采取措施的问题的迹象。 例如：  

- 站点服务器和站点系统上的文件积压。  

- 指示错误或问题的状态消息。  

- 失败的站点内通信。  

- 服务器上系统事件日志中的错误和警告消息。  

- Microsoft SQL Server 错误日志中的错误和警告消息。  

- 长时间未报告状态的站点或客户端。  

- SQL Server 数据库响应缓慢。  

- 硬件故障的迹象。  

如果监视任务显示出任何存在问题的迹象，请调查问题根源。 然后，快速修复问题，以最大程度地减少站点故障的风险。  


## <a name="BKMK_MonintorMgmtTasks"></a> 监视常见管理任务

Configuration Manager 提供从 Configuration Manager 控制台中进行的内置监视。

### <a name="alerts"></a>警报

有关详细信息，请参阅[监视警报](/sccm/core/servers/manage/use-alerts-and-the-status-system#BKMK_MonitorAlerts)。  

### <a name="compliance-settings"></a>符合性设置

有关详细信息，请参阅[如何监视符合性设置](/sccm/compliance/deploy-use/monitor-compliance-settings)。

### <a name="content"></a>Content

有关监视内容的常规信息，请参阅[管理内容和内容基础结构](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)。  

有关监视特定内容类型的详细信息，请参阅以下内容：

- [监视应用程序](/sccm/apps/deploy-use/monitor-applications-from-the-console)

- [监视包和程序](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs)  

- [监视软件更新的内容](/sccm/sum/deploy-use/monitor-software-updates#BKMK_MonitorContent)

- [监视操作系统部署的内容](/sccm/osd/deploy-use/monitor-operating-system-deployments#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Endpoint Protection

有关详细信息，请参阅[如何监视 Endpoint Protection](/sccm/protect/deploy-use/monitor-endpoint-protection)。  

### <a name="os-deployment"></a>OS 部署

有关详细信息，请参阅[监视操作系统部署](/sccm/osd/deploy-use/monitor-operating-system-deployments)。

### <a name="monitor-power-management"></a>监视电源管理

有关详细信息，请参阅[如何监视和规划电源管理](/sccm/core/clients/manage/power/monitor-and-plan-for-power-management)。  

### <a name="monitor-software-metering"></a>监视软件计数

有关详细信息，请参阅[使用软件计数监视应用使用情况](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering)。  

### <a name="monitor-software-updates"></a>监视软件更新

有关详细信息，请参阅[监视软件更新](/sccm/sum/deploy-use/monitor-software-updates)。  


## <a name="BKMK_SH_Node"></a> 监视站点层次结构

“监视”  工作区中的“站点层次结构”  节点提供 Configuration Manager 层次结构和站点间链接的概述。 你可以使用两个视图：  

- **层次结构关系图**：将层次结构显示为简化后仅显示重要信息的拓扑图。 有关详细信息，请参阅[层次结构图](#hierarchy-diagram)。  

- **地理视图**：在显示你配置的站点位置的地图上显示你的站点。 有关详细信息，请参阅[地理视图](#geographical-view)。  

使用“站点层次结构”  节点来监视每个站点的运行状况。 此外，还监视站点内复制链接及它们与外部因素（例如地理位置）的关系。  

站点状态和站点内链接状态均以站点数据（而不是全局数据）形式复制。 当你将 Configuration Manager 控制台连接到子主站点时，将无法查看其他主站点或其子辅助站点的站点或链接状态。 例如，在具有多个主站点的层次结构中，当将控制台连接到主站点时，可以查看子辅助站点、主站点和管理中心站点的状态。 在此视图中，无法查看管理中心站点下其他站点的状态。  

若要控制“站点层次结构”  节点的呈现方式，请使用“配置设置”  操作。 层次结构复制在此节点中配置的设置。  

### <a name="hierarchy-diagram"></a>层次结构关系图

层次结构关系图在拓扑图中显示你的站点。 选择一个站点，并从该站点查看状态消息摘要。 钻取以查看状态消息，并访问站点“属性”  。  

若要查看站点之间的站点或复制链接的高级别状态，请将鼠标指针悬停在对象上。 复制链接状态不会进行全局复制。 若要查看层次结构中所有主站点之间的复制链接详细信息，请将控制台连接到管理中心站点。  

下列选项会修改层次结构关系图：  

#### <a name="groups"></a>组

配置触发层次结构关系图中的更改的主站点数和辅助站点数。 显示的此更改将这些站点合并为单个对象。 然后，会看到站点的总数，以及状态消息和站点状态的高级别汇总。 组配置不影响地理视图。  

#### <a name="favorite-sites"></a>收藏站点

将各个站点指定为收藏站点。 星形图标在层次结构关系图中标识收藏站点。 使用组时，收藏站点不会与其他网站合并。 它们始终单独显示。  

### <a name="geographical-view"></a>地理视图

地理视图显示每个站点在地图上的位置。 仅显示与位置一起配置的站点。 在此视图中选择站点时，将显示指向父站点或子站点的复制链接。 与层次结构关系图视图不同，无法在此视图中显示站点状态消息或复制链接详细信息。  

> [!NOTE]  
> 要使用地理视图，Configuration Manager 控制台所连接到的计算机必须安装 Internet Explorer，并且必须能够通过使用 HTTP 协议来访问必应地图。  

下列选项修改地理视图：  

#### <a name="site-location"></a>站点位置

使用以下类型之一指定每个站点的地理位置：

- 街道地址
- 地点名称，如城市名称
- 按纬度和经度坐标

例如，要使用华盛顿雷蒙德市的经纬度，指定 N 47 40 26.3572 W 122 7 17.4432  作为站点位置。 无需为经纬度的度、分或秒指定符号。 Configuration Manager 使用必应地图在地理视图上显示位置。 然后，可以查看带有地理位置的层次结构。 借助此视图，可深入了解可能影响特定站点或站点间复制的区域问题。  

在指定位置时，你可以使用“位置”  框来搜索层次结构中的特定站点。 选中站点后，在“位置”  列中输入城市名或街道地址作为位置。 Configuration Manager 使用必应地图解析位置。  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>后续步骤

[监视数据库复制](/sccm/core/servers/manage/monitor-replication)
