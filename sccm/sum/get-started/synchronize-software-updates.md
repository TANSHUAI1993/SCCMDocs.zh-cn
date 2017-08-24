---
title: "管理软件更新同步 | Microsoft Docs"
description: "使用以下步骤可计划软件更新同步、手动启动软件更新同步，以及监视软件更新同步。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
ms.openlocfilehash: e68170a16a6a908e035247ed9c0f3cc6cdbe1983
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_SUMSync"></a> 同步软件更新

*适用范围：System Center Configuration Manager (Current Branch)*

 Configuration Manager 中的软件更新同步是指检索满足你配置的条件的软件更新元数据的过程。 这包括特定的产品、分类和语言。 通常，管理中心站点或独立主站点上的软件更新点从 Microsoft 更新中检索元数据。 然后，顶层站点将向其他站点发送同步请求。 当站点收到来自父站点的同步请求时，站点的软件更新点将从其上游[同步源](../plan-design/plan-for-software-updates.md#BKMK_SyncSource)检索软件更新元数据。 有关软件更新同步的详细信息，请参阅[软件更新同步](../understand/software-updates-introduction.md#BKMK_Synchronization)。

可以配置软件更新同步，以在顶层站点处软件更新点的属性中的计划上运行。 配置同步计划之后，你通常将不会在正常操作过程中更改该计划。 但是，必要时可以手动启动软件更新同步。

  > [!NOTE]  
  >  软件更新点必须连接到其上游同步源以同步软件更新。 当软件更新点从其上游同步源断开连接时，你可以使用导出和导入方法来同步软件更新。 有关详细信息，请参阅[从断开连接的软件更新点中同步软件更新](synchronize-software-updates-disconnected.md)。  

## <a name="schedule-software-updates-synchronization"></a>计划软件更新同步
在配置软件更新同步计划时，顶层软件更新点将按计划的日期和时间启动与 Microsoft 更新的同步。 自定义计划允许你在 WSUS 服务器、站点服务器和网络的需求不高的日期和时间同步软件更新。 例如，你可以设置计划，以便每周凌晨 2:00 同步软件更新。 在按计划同步期间，自上次计划的同步以来对软件更新元数据所做的所有更改将插入到站点数据库。 这包括新的软件更新元数据，或已修改、删除或者现在已过期的元数据。

在顶层站点上使用下列过程来计划软件更新同步。  

#### <a name="to-schedule-software-updates-synchronization"></a>计划软件更新同步  

  1.  在 Configuration Manager 控制台中，单击“管理” 。  

  2.  在“管理”工作区中，展开“站点配置” ，然后单击“站点” 。  

  3.  在结果窗格中，单击管理中心站点或独立主站点。  

  4.  在“主页”  选项卡上的“设置”  组中，展开“配置站点组件” ，然后单击“软件更新点” 。  

  5.  在“软件更新点组件属性”对话框中，选择“按计划启用同步” ，然后指定同步计划。  

## <a name="manually-start-software-updates-synchronization"></a>手动启动软件更新同步
可以从“软件库”工作区的“所有软件更新”节点手动启动 Configuration Manager 控制台中顶层站点上的软件更新同步。  

在顶层站点上使用下列过程来手动启动软件更新同步。  

#### <a name="to-manually-start-software-updates-synchronization"></a>手动启动软件更新同步  

  1.  在连接到管理中心站点或独立主站点的 Configuration Manager 控制台中，单击“软件库”。  

  2.  在“软件库”工作区中，展开“软件更新”  ，并单击“所有软件更新”  或“软件更新组” 。  

  3.  在“主页”  选项卡上的“创建”  组中，单击“同步软件更新” 。 在对话框中单击“是”  确认要启动同步过程。  

   在软件更新点上启动同步过程之后，可以通过 Configuration Manager 控制台监视层次结构中所有软件更新点的同步过程。 使用下列过程来监视软件更新同步过程。  


## <a name="monitor-software-updates-synchronization"></a>监视软件更新同步
启动同步过程之后，可以使用 Configuration Manager 控制台监视层次结构中所有软件更新点的同步过程。 使用下列过程来监视软件更新同步过程。 有关监视软件更新同步（包括同步过程）的详细信息，请参阅[监视软件更新](../deploy-use/monitor-software-updates.md)。

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>监视软件更新同步过程  

  1.  在 Configuration Manager 控制台中，单击“监视” 。  

  2.  在“监视”  工作区中，单击“软件更新点同步状态” 。  

    Configuration Manager 层次结构中的软件更新点显示在结果窗格中。 从此视图中，你可以监视所有软件更新点的同步状态。 如果要了解有关同步过程的更多详细信息，请查看位于每台站点服务器上的 <*ConfigMgrInstallationPath*>\Logs 中的 wsyncmgr.log 文件。  

## <a name="next-steps"></a>后续步骤
在首次同步软件更新后，或有新的可用分类或产品时，必须[配置新的分类和产品](configure-classifications-and-products.md)以便通过新条件同步软件更新。

通过所需的条件同步软件更新后，[管理软件更新的设置](manage-settings-for-software-updates.md)。  
