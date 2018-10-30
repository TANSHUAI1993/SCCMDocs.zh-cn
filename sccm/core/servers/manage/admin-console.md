---
title: Configuration Manager 控制台
titleSuffix: Configuration Manager
description: 了解如何导航 Configuration Manager 控制台。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f936cf1c1317940f28691863eafdb4aa883fc1cb
ms.sourcegitcommit: aa91f0d376de03b614b70d5fc513cb384ff58db4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50216908"
---
# <a name="using-the-system-center-configuration-manager-console"></a>使用 System Center Configuration Manager 控制台

*适用范围：System Center Configuration Manager (Current Branch)*

管理员使用 System Center Configuration Manager 控制台管理 Configuration Manager 环境。 本文介绍导航控制台的基础知识。 本文最下方按版本顺序列出了对控制台的改进。 

## <a name="connect-the-console-to-a-site-server"></a>将控制台连接到站点服务器
控制台可连接到管理中心站点服务器或主站点服务器。 但无法将 Configuration Manager 控制台连接到辅助站点。 如有需要，请[安装 Configuration Manager 控制台](../deploy/install/install-consoles.md)。 安装过程中，指定 Configuration Manager 控制台连接的站点服务器的完全限定的域名 (FQDN)。 若要连接到不同的站点服务器，请按照以下说明操作： 

1. 单击功能区顶部的箭头，然后选择“连接到新站点”。
    ![将控制台连接到新站点](media/connect-to-a-new-site.png)
2. 键入站点服务器的 FQDN。 如果之前已连接到站点服务器，可从下拉列表中选择服务器。  
    ![键入站点服务器的 FQDN](media/site-server-fqdn.png)
3. 单击“连接” 。 

## <a name="navigate-the-console"></a>导航控制台
控制台下的某些选项可能未显示，具体取决于所分配的安全角色。 有关角色的详细信息，请参阅[基于角色的管理基础](../../understand/fundamentals-of-role-based-administration.md)。 

### <a name="workspaces"></a>工作区
Configuration Manager 控制台中有四个工作区： 
   - **资产和符合性**
   - **软件库**
   - **监视**
   - **管理**

 ![Configuration Manager 工作区](media/configuration-manager-workspaces.png)

单击向下箭头并选择“导航窗格选项”，可对工作区按钮重新进行排序。 选中某个项“上移”或“上移”。 单击“重置”还原默认按钮顺序。 

 ![对 Configuration Manager 工作区重新进行排序](media/navigation-pane-options.png)

可选择“显示更少按钮”，最小化工作区按钮。 工作区列表中的最后一个工作区首先最小化。 单击已最小化的按钮并选择“显示更多按钮”即可将按钮恢复为原始大小。  

![Configuration Manager 工作区](media/workspace-buttons.png)


### <a name="nodes"></a>节点
工作区是一系列节点。 其中一个节点便是“软件更新组”节点。 在节点中可单击箭头以最小化导航窗格。 

![Configuration Manager 工作区](media/software-update-groups-node.png)

当导航窗格处于最小化时，可使用“导航栏”在控制台中移动。 

![最小化的 Configuration Manager 导航窗格](media/minimized-navigation-pane.png)

在控制台中，节点有时会被整理到文件夹中。 通常直接单击文件夹即可转到“导航索引”或“仪表板”。

![Configuration Manager 软件更新导航索引](media/software-updates-navigation-index.png)

### <a name="ribbon"></a>功能区 
功能区位于 Configuration Manager 控制台顶部。 功能区可以有多个选项卡，且可使用右侧的箭头将其最小化。 功能区上的按钮数量因节点而异。 另外，通过右键单击菜单还可以使用功能区中的大部分按钮。 
 
![Configuration Manager 软件更新导航索引](media/ribbon.png)

### <a name="details-pane"></a>“详细信息”窗格
若要获取有关项的其他信息，可查看细节窗格。 细节窗格中可以有一个或多个选项卡。 选项卡的数量因节点而异。 
![Configuration Manager 细节窗格](media/details-pane.png)

### <a name="columns"></a>列 
可添加、删除、重新排列并调整列的大小。 通过这些操作，可让系统显示你喜欢的数据。 可用列的数量因节点而异。 右键单击现有列标题，然后单击要在视图中添加或删除的项。 将列标题拖动到想要的位置即可对其重新排序。 
![Configuration Manager 添加列](media/add-columns.png)

在列的底部右键单击菜单，可对列进行排序或分组。 另外，也可单击列标题，对其进行排序。 

![Configuration Manager 按列分组](media/column-group-by.png)

##<a name="console-command-line-options"></a>控制台命令行选项
Microsoft System Center Configuration Manager 控制台具有下列命令行选项。

|选项|说明|  
|------------|-----------------|  
|**/sms:debugview=1**|DebugView 包含在用于指定视图的所有 ResultView 中。 DebugView 显示原始属性（名称和值）。|  
|**/sms:NamespaceView=1**|在 System Center Configuration Manager 控制台中显示命名空间视图。|  
|**/sms:ResetSettings**|System Center Configuration Manager 控制台将忽略用户保留的连接和视图状态（不会重置 Microsoft 管理控制台窗口大小）。|  
|**/sms:IgnoreExtensions**|禁用任何 System Center Configuration Manager 扩展。|  
|**/sms:NoRestore**|System Center Configuration Manager 控制台将忽略上一个保留的节点导航。|  

## <a name="console-improvements-in-version-1806"></a>1806 版中的控制台改进
在 Configuration Manager 1806 版中，添加了以下控制台改进：

- 在设备节点中，“主要用户”可作为一列。 <!--1357280-->
- 在设备节点中，“当前登录的用户”可作为一列。<!--1358202-->
- 从“资产详细信息”窗格复制以下监视视图中的信息：<!--1357856-->
    - 内容分发状态
    - 部署状态 

    ![Configuration Manager 复制资产详细信息](media/1810-deployment-status.PNG)

 - 从控制台提交反馈。 如果未接入 Internet，可以保存副本稍后提交。 <!--1357542-->
   
    - **发送笑脸**：就喜欢的内容发送反馈。
    - **发送哭脸**：就不喜欢的内容发送反馈。 
    - **发送建议**：转到 UserVoice 分享你的观点。 
 
       ![向 Configuration Manager 发送反馈](media/1810-send-a-smile.PNG)
![Configuration Manager 反馈窗体](media/1810-feedback-form.PNG)

## <a name="next-steps"></a>后续步骤
> [!div class="nextstepaction"]
> [辅助功能](../../understand/accessibility-features.md)

