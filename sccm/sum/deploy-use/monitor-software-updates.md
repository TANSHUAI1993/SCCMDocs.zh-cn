---
title: "监视软件更新 | Microsoft Docs"
description: "System Center Configuration Manager 控制台提供警报和状态以监视更新和符合性。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 11/10/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: 956ef263a1c178b5ab5926705859f4b2d0ae5bc7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-software-updates-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中监视软件更新

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 提供了许多方式来帮助你监视软件更新对象、过程和符合性信息。 使用以下部分可监视软件更新。

## <a name="software-updates-dashboard"></a>软件更新仪表板
从 Configuration Manager 版本 1610 开始，可以使用软件更新仪表板查看组织中设备的当前符合性状态，并快速分析数据以确定哪些设备处于风险中。 若要查看仪表板，请导航到“监视” > “概述” > “安全性” > “软件更新仪表板”。   

##  <a name="BKMK_SUAlerts"></a> 软件更新的警报  
 可以配置软件更新的警报，以便在软件更新部署的符合性级别低于已配置的百分比时通知管理用户。 可以在下列位置中配置软件更新部署的警报：  

-   ADR 设置：可以在“自动部署规则向导”中和 ADR 的属性中配置警报设置。  

-   部署设置：可以在“部署软件更新向导”中和部署属性中配置警报设置。  

配置警报设置后，如果出现指定的条件，则 Configuration Manager 会生成警报。 可以在下列位置中查看软件更新警报：  

1.  在“软件库”  工作区的“软件更新”  节点中查看最新警报。  

2.  在“监视”  工作区的“警报”  节点中管理已配置的警报。  

##  <a name="BKMK_SUSyncStatus"></a> 软件更新同步状态  
 启动同步过程之后，可以通过 Configuration Manager 控制台监视层次结构中的所有软件更新点的同步过程。 使用下列过程来监视软件更新同步过程。  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>监视软件更新同步过程  

- 在 Configuration Manager 控制台中，导航到“监视” > “概述” > “软件更新点同步状态”。  

    Configuration Manager 层次结构中的软件更新点显示在结果窗格中。 从此视图中，你可以监视所有软件更新点的同步状态。 若要了解有关同步过程的更多详细信息，请查看每台站点服务器上的 <ConfigMgrInstallationPath>\Logs 中的 wsyncmgr.log 文件。  

##  <a name="BKMK_SUDeployStatus"></a> 软件更新部署状态  
 在软件更新组中部署软件更新或部署单个软件更新之后，可以监视部署状态。 使用下列过程来监视软件更新组或软件更新的部署状态。  

#### <a name="to-monitor-deployment-status"></a>监视部署状态  

1.  在 Configuration Manager 控制台中，导航到“监视” > “概述” > “部署”。  

2.  单击要监视其部署状态的软件更新组或软件更新。  

3.  在“主页”  选项卡上的“部署”  组中，单击“查看状态” 。  

##  <a name="BKMK_SUReports"></a> 软件更新报表  
 软件更新的状态消息提供了有关软件更新的符合性的信息，以及有关软件更新部署的评估和强制状态的信息。 可以运行软件更新报表以显示这些状态消息。 可以使用 30 多个预定义的软件更新报表。 它们分为几个类别，可用于报告有关软件更新和部署的特定信息。 除了使用预先配置的报表之外，还可以按照企业的需求创建自定义软件更新报表。 有关详细信息，请参阅[报表的操作和维护](../../core/servers/manage/operations-and-maintenance-for-reporting.md)。  

##  <a name="BKMK_MonitorContent"></a> 监视内容  
 可以在 Configuration Manager 控制台中监视内容，以查看与关联的分发点相关的所有包类型的状态。 这可以包括包中的内容的内容验证状态、分配给特定分发点组的内容的状态、分配给分发点的内容的状态和每个分发点的可选功能（内容验证、PXE 和多播）的状态。  

###  <a name="BKMK_ContentStatus"></a> 内容状态监视  
 “监视”  工作区中的“内容状态”  节点提供有关内容包的信息。 可以查看有关包的常规信息、包的分发状态和有关包的详细状态信息。 使用下列过程来查看内容状态。  

#### <a name="to-monitor-content-status"></a>监视内容状态  

1.  在 Configuration Manager 控制台中，导航到“监视” > “概述” > “分发状态” > “内容状态”。 此时会显示包。  

2.  选择要查看其详细状态信息的包。  

3.  在“主页”  选项卡上，单击“查看状态” 。 此时会显示包的详细状态信息。  

###  <a name="BKMK_DPGroupStatus"></a> 分发点组状态  
 “监视”  工作区中的“分发点组状态”  节点提供有关分发点组的信息。 可以查看有关分发点组的常规信息（例如分发点组状态和符合性比率），以及分发点组的详细状态信息。 使用下列过程来查看分发点组状态。  

#### <a name="to-monitor-distribution-point-group-status"></a>监视分发点组状态  

1.  在 Configuration Manager 控制台中，导航到“监视” > “概述” > “分发状态” > “分发点组状态”。 此时会显示分发点组。  

2.  选择要查看其详细状态信息的分发点组。  

3.  在“主页”  选项卡上，单击“查看状态” 。 此时会显示分发点组的详细状态信息。  

###  <a name="BKMK_DPConfigStatus"></a> 分发点配置状态  
 “监视”  工作区中的“分发点配置状态”  节点提供有关分发点的信息。 可以查看为分发点启用的属性，例如 PXE、多播和内容验证。 还可以查看分发点的详细状态信息。 使用下列过程来查看分发点配置状态。  

#### <a name="to-monitor-distribution-point-configuration-status"></a>监视分发点配置状态  

1.  在 Configuration Manager 控制台中，导航到“监视” > “概述” > “分发状态” > “分发点配置状态”。 此时会显示分发点。  

2.  选择要查看其分发点状态信息的分发点。  

3.  在结果窗格中，单击“详细信息”  选项卡。 此时会显示分发点的状态信息。  
