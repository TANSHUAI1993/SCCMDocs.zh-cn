---
title: 管理软件更新同步
titleSuffix: Configuration Manager
description: 使用以下步骤可计划软件更新同步、手动启动软件更新同步，以及监视软件更新同步。
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: e89fd9422b6bf6c5abb61e154f38a1f479c7ff7e
ms.sourcegitcommit: cdf2827fb3f44d7522a9b533c115f910aa9c382a
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70902980"
---
#  <a name="BKMK_SUMSync"></a> 同步软件更新

*适用范围：System Center Configuration Manager (Current Branch)*

 Configuration Manager 中的软件更新同步是指检索满足你配置的条件的软件更新元数据的过程。 这包括特定的产品、分类和语言。 通常，管理中心站点或独立主站点上的软件更新点从 Microsoft 更新中检索元数据。 然后，顶层站点将向其他站点发送同步请求。 当站点收到来自父站点的同步请求时，站点的软件更新点将从其上游[同步源](../plan-design/plan-for-software-updates.md#BKMK_SyncSource)检索软件更新元数据。 有关软件更新同步的详细信息，请参阅[软件更新同步](../understand/software-updates-introduction.md#BKMK_Synchronization)。

可以配置软件更新同步，以在顶层站点处软件更新点的属性中的计划上运行。 配置同步计划之后，你通常将不会在正常操作过程中更改该计划。 但是，必要时可以手动启动软件更新同步。

  > [!NOTE]  
  >  软件更新点必须连接到其上游同步源以同步软件更新。 当软件更新点从其上游同步源断开连接时，你可以使用导出和导入方法来同步软件更新。 有关详细信息，请参阅[从断开连接的软件更新点中同步软件更新](synchronize-software-updates-disconnected.md)。  

## <a name="schedule-software-updates-synchronization"></a>计划软件更新同步
在配置软件更新同步计划时，顶层软件更新点将按计划的日期和时间启动与 Microsoft 更新的同步。 自定义计划允许你在 Windows Server Update Services (WSUS) 服务器、站点服务器和网络的需求不高的日期和时间同步软件更新。 例如，你可以设置计划，以便每周凌晨 2:00 同步软件更新。 在按计划同步期间，自上次计划的同步以来对软件更新元数据所做的所有更改将插入到站点数据库。 这包括新的软件更新元数据，或已修改、删除或者现在已过期的元数据。

在顶层站点上使用下列过程来计划软件更新同步。  

#### <a name="to-schedule-software-updates-synchronization"></a>计划软件更新同步  

  1.  在 Configuration Manager 控制台中，单击“管理”  。  

  2.  在“管理”工作区中，展开“站点配置”  ，然后单击“站点”  。  

  3.  在结果窗格中，单击管理中心站点或独立主站点。  

  4.  在“主页”  选项卡上的“设置”  组中，展开“配置站点组件”  ，然后单击“软件更新点”  。  

  5.  在“软件更新点组件属性”对话框中，选择“按计划启用同步”  ，然后指定同步计划。  

## <a name="manually-start-software-updates-synchronization"></a>手动启动软件更新同步
可以从“软件库”  工作区的“所有软件更新”  节点手动启动 Configuration Manager 控制台中顶层站点上的软件更新同步。  

在顶层站点上使用下列过程来手动启动软件更新同步。  

#### <a name="to-manually-start-software-updates-synchronization"></a>手动启动软件更新同步  

1. 在连接到管理中心站点或独立主站点的 Configuration Manager 控制台中，单击“软件库”  。  

2. 在“软件库”工作区中，展开“软件更新”  ，并单击“所有软件更新”  或“软件更新组”  。  

3. 在“主页”  选项卡上的“创建”  组中，单击“同步软件更新”  。 在对话框中单击“是”  确认要启动同步过程。  

   在软件更新点上启动同步过程之后，可以通过 Configuration Manager 控制台监视层次结构中所有软件更新点的同步过程。 使用下列过程来监视软件更新同步过程。  


## <a name="monitor-software-updates-synchronization"></a>监视软件更新同步
启动同步过程之后，可以使用 Configuration Manager 控制台监视层次结构中所有软件更新点的同步过程。 使用下列过程来监视软件更新同步过程。 有关监视软件更新同步（包括同步过程）的详细信息，请参阅[监视软件更新](../deploy-use/monitor-software-updates.md)。

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>监视软件更新同步过程  

1. 在 Configuration Manager 控制台中，单击“监视”  。  

2. 在“监视”  工作区中，单击“软件更新点同步状态”  。  

   Configuration Manager 层次结构中的软件更新点显示在结果窗格中。 从此视图中，你可以监视所有软件更新点的同步状态。 如果要了解有关同步过程的更多详细信息，请查看位于每台站点服务器上的 <*ConfigMgrInstallationPath*>\Logs 中的 wsyncmgr.log 文件。  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>从 Microsoft 更新目录导入更新

顶层软件更新点使用 WSUS 获取有关软件从 Microsoft 更新到 Configuration Manager 的信息。 有时，可能需要一个更新，该更新不会自动同步到所选产品和分类的 WSUS，但可以在 [Microsoft Update 目录](https://catalog.update.microsoft.com)中使用。 通常，不会自动同步到 WSUS 的更新旨在解决针对性极强的问题。 通常情况下，如果目录中有可用更新，则可将其导入 WSUS。 然后可将该更新同步到 Configuration Manager，并像部署任何其他更新一样对其进行部署。

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>从 Microsoft 更新目录导入更新

1. 打开 WSUS 管理控制台，并将其连接到层次结构中的顶层 WSUS 服务器。
   - 如果 Internet Explorer 不是计算机的默认 Web 浏览器，请暂时将其设置为默认浏览器。
2. 单击“更新”或单击 WSUS 服务器的名称  。 
3. 在“操作”窗格中，选择“导入更新...”，此操作将打开转到 [Microsoft 更新目录](https://catalog.update.microsoft.com)的浏览器窗口   。
   ![在 WSUS 控制台中选择导入更新](media/wsus-console-import-updates.png)
4. 如果出现提示，请安装 Microsoft 更新目录 ActiveX 控件。 必须安装该控件才能将更新导入 WSUS。 
5. 在浏览器窗口中，搜索所需的更新。 单击“添加”按钮以将其添加到购物篮  。
6. 单击“查看购物篮”  。 请确保选中“直接导入 Windows Server Update Services”选项  。 然后，单击“导入”  。
    ![将目录中的更新导入 WSUS](./media/import-catalog-update-into-wsus.png)
7. 导入完成后，单击浏览器窗口中的“关闭”  。
     - 如果有需要，请重置默认浏览器。
8. 同步 Configuration Manager 软件更新点。


## <a name="next-steps"></a>后续步骤
在首次同步软件更新后，或有新的可用分类或产品时，必须[配置新的分类和产品](configure-classifications-and-products.md)以便通过新条件同步软件更新。

通过所需的条件同步软件更新后，[管理软件更新的设置](manage-settings-for-software-updates.md)。  
