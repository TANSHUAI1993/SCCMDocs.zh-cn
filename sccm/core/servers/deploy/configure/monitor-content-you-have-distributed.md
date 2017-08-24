---
title: "监视内容 | Microsoft Docs"
description: "了解如何使用 Configuration Manager 控制台监视分发的内容。"
ms.custom: na
ms.date: 4/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7659d5789b8ce4e9e0b585a331c8f68869c9492d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 监视分发的内容

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 控制台监视分发的内容，包括：  

-   与关联的分发点相关的所有包类型的状态。  
-   包中内容的内容验证状态。  
-   分配给特定分发点组的内容的状态。  
-   分配给分发点的内容的状态。  
-   每个分发点（内容验证、PXE 和多播）可选功能的状态。  

> [!NOTE]  
>  Configuration Manager 仅监视分发点上位于内容库中的内容。 而不会监视存储在分发点上的包或自定义共享中的内容。  

##  <a name="BKMK_ContentStatus"></a> 内容状态监视  
 “监视”  工作区中的“内容状态”  节点提供有关内容包的信息。 在 Configuration Manager 控制台中，你可以查看如下信息：  

-   包名称。  
-   类型。  
-   已将包发送到多少个分发点。  
-   符合性比率。  
-   创建包的时间。  
-   包 ID。  
-   源版本。  

还可找到任何包的详细状态信息以及该包的分发状态，包括：  

-   失败次数。  
-   挂起的分发。  
-   安装次数。

还可管理仍在向分发点进行的分发或未能成功向分发点分发内容的分发：  

-   当在“资产详细信息”窗格中查看针对分发点的分发作业的部署状态消息时，可使用取消或重新分发内容选项。 此窗格位于“内容状态”节点的“正在进行”选项卡或“错误”选项卡中。  
-   此外，当在“正在进行”选项卡上查看作业详细信息时，作业详细信息会显示作业完成的百分比。 当查看“错误”选项卡中的作业详细信息时，作业详细信息还会显示作业的剩余重试次数以及下次重试之前的等待时间。  

当你取消尚未完成的部署时，用于传输该内容的分发作业将停止：  

-   部署的状态随后将更新以指示分发失败并且被用户操作取消。  
-   这个新状态出现在“错误”  选项卡中。  

> [!TIP]  
>  当部署接近完成时，用于取消该分发的操作有可能不会在针对分发点的分发完成之前进行。 如果出现这种情况，则会忽略用于取消部署的操作，并且部署的状态显示为成功。  

> [!NOTE]  
>  尽管你可以选择选项来取消针对位于站点服务器上的分发点的分发，但此操作不起作用。 这是因为站点服务器和站点服务器上的分发点共享相同的单一实例内容存储。 没有要取消的实际分发作业。  

当重新分发以前未能传输到分发点的内容时，Configuration Manager 会立即开始将该内容再次部署到分发点。 Configuration Manager 更新部署的状态以反映重新部署正在进行的状态。  

使用下列过程来查看内容状态以及管理仍在进行或失败的分发。  

### <a name="to-monitor-content-status"></a>监视内容状态  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”  工作区中，展开“分发状态” ，然后单击“内容状态” 。 此时会显示包。  

3.  选择要查看其详细状态信息的包。  

4.  在“主页”  选项卡上，单击“查看状态” 。 此时会显示包的详细状态信息。  

### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>取消仍在进行的分发  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”  工作区中，展开“分发状态” ，然后单击“内容状态” 。 此时会显示包。  

3.  选择要管理的包，然后在详细信息窗格中单击“查看状态” 。  

4.  在“正在进行”选项卡的“资产详细信息”窗格中，右键单击要取消的分发的条目，并选择“取消”。  

5.  单击“是”  确认操作并取消针对该分发点的分发作业。  

### <a name="to-redistribute-content-that-failed-to-distribute"></a>重新分发未能分发的内容  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”  工作区中，展开“分发状态” ，然后单击“内容状态” 。 此时会显示包。  

3.  选择要管理的包，然后在详细信息窗格中单击“查看状态” 。  

4.  在“错误”选项卡的“资产详细信息”窗格中，右键单击要重新分发的分发的条目，并选择“重新分发”。  

5.  单击“是”确认操作并开始针对该分发点的重新分发过程。  

## <a name="distribution-point-group-status"></a>分发点组状态  
“监视”  工作区中的“分发点组状态”  节点提供有关分发点组的信息。 你可以查看如下信息：  

-   分发点组名称。  
-   说明。  
-   属于分发点组成员的分发点数。  
-   已分发到组的包数。  
-   分发点组状态。  
-   符合性比率。  

你还可以查看以下项目的详细状态信息：  

-   分发点组错误。  
-   正在进行的分发数。
-   已成功分发的数量。  

### <a name="to-monitor-distribution-point-group-status"></a>监视分发点组状态  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”  工作区中，展开“分发状态” ，然后单击“分发点组状态” 。 此时会显示分发点组。  

3.  选择要查看其详细状态信息的分发点组。  

4.  在“主页”  选项卡上，单击“查看状态” 。 此时会显示分发点组的详细状态信息。  

## <a name="distribution-point-configuration-status"></a>分发点配置状态  
 “监视”  工作区中的“分发点配置状态”  节点提供有关分发点的信息。 可查看为分发点启用的属性（例如 PXE、多播和内容验证）以及分发点的分发状态。 还可以查看分发点的详细状态信息。  

> [!WARNING]  
>  分发点配置状态是过去 24 小时的状态。 如果分发点出错并恢复，则可能会显示分发点恢复后最多 24 小时的错误状态。  

使用下列过程来查看分发点配置状态。  

### <a name="to-monitor-distribution-point-configuration-status"></a>监视分发点配置状态  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”  工作区中，展开“分发状态” ，然后单击“分发点配置状态” 。 此时会显示分发点。  

3.  选择要查看其分发点状态信息的分发点。  

4.  在结果窗格中，单击“详细信息”  选项卡。 此时会显示分发点的状态信息。  

## <a name="client-data-sources-dashboard"></a>客户端数据源仪表板
从 1610 版起，可以使用“客户端数据源”仪表板，来帮助了解环境中[对等缓存](/sccm/core/plan-design/hierarchy/client-peer-cache)的使用。 客户端下载内容后，仪表板将开始显示数据，并将该信息报告给网站。 此过程最多可能需要 24 小时。

> [!TIP]  
> “客户端对等缓存”和“客户端数据源”仪表板均为 1610 版本中引入的预发行功能。 必须先启用“客户端对等缓存”，“客户端数据源”仪表板才能在控制台中显示。 若要启用“客户端对等缓存”，请参阅[使用更新中的预发行功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。 从启用到开始显示数据，最长需要 24 小时。

在控制台中，转到“监视” > “分发状态” > “客户端数据源”。 在此处可以选择要应用于仪表板的时间段。 然后在显示中，可以选择要查看其信息的边界组或包。 查看信息时，可以将鼠标悬停在表面上方，以查看有关不同内容或策略源的更多详细信息。

这些详细信息包括以下内容：  
- **客户端内容源**：显示客户端从其处获取内容的源。
- **分发点**：显示属于所选边界组的分发点的数量。
- **使用分发点的客户端**：显示所选边界组中使用了分发点来获取内容的客户端的数量。
- **对等缓存源**：对于所选的边界组，显示已报出曾进行过下载操作的对等缓存源的数量。
- “使用对等的客户端”：是所选边界组中的客户端数，显示使用对等缓存源来获取内容的客户端数。



还可以使用新报表“客户端数据源 - 摘要”查看每个边界组的客户端数据源摘要。
