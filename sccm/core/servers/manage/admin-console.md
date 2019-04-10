---
title: Configuration Manager 控制台
titleSuffix: Configuration Manager
description: 了解如何导航 Configuration Manager 控制台。
ms.date: 04/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb58662350caec9fd1a08295c93c3811893048a9
ms.sourcegitcommit: da753df27d3909265ca45d3e79091f1e98758d16
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2019
ms.locfileid: "58913534"
---
# <a name="using-the-configuration-manager-console"></a>使用 Configuration Manager 控制台

适用范围：System Center Configuration Manager (Current Branch)

管理员使用 Configuration Manager 控制台管理 Configuration Manager 环境。 本文介绍导航控制台的基础知识。  



## <a name="connect-to-a-site-server"></a>连接到站点服务器

控制台可连接到管理中心站点服务器或主站点服务器。 但是，无法将 Configuration Manager 控制台连接到辅助站点。 你可以[安装 Configuration Manager 控制台](/sccm/core/servers/deploy/install/install-consoles)。 安装过程中，指定控制台连接的站点服务器的完全限定的域名 (FQDN)。 

要连接到其他站点服务器，请按以下步骤操作： 

1. 选择[功能区](#ribbon)顶部的箭头，然后选择“连接到新站点”。  

    ![将控制台连接到新站点](media/connect-to-a-new-site.png)  

2. 键入站点服务器的 FQDN。 如果之前已连接到站点服务器，可从下拉列表中选择服务器。  

    ![站点连接窗口，输入站点服务器的 FQDN](media/site-server-fqdn.png)  

3. 选择“**连接**”。  


从版本 1810 开始，可以为管理员指定访问 Configuration Manager 站点的最低身份验证级别。 此功能强制管理员以要求的级别登录到 Windows。 有关详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth)。 <!--1357013-->  



## <a name="navigation"></a>导航

控制台的某些区域可能未显示，具体取决于所分配的安全角色。 有关角色的详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。 


### <a name="workspaces"></a>工作区

Configuration Manager 控制台中有四个工作区：  

- **资产和符合性**  

- **软件库**  

- **监视**  

- **管理**  

![带上下文菜单的 Configuration Manager 工作区](media/configuration-manager-workspaces.png)  

选择向下箭头并选择“导航窗格选项”，可对工作区按钮重新进行排序。 选中某个项“上移”或“上移”。 单击“重置”还原默认按钮顺序。  

 ![用于对工作区重新排序的“导航窗格选项”窗口](media/navigation-pane-options.png)  

选择“显示更少按钮”可最小化工作区按钮。 列表中的最后一个工作区首先最小化。 选择已最小化的按钮并选择“显示更多按钮”即可将按钮恢复为原始大小。   

![Configuration Manager 控制台中最小化的工作区](media/workspace-buttons.png)  


### <a name="nodes"></a>节点

工作区是一系列节点。 其中一个节点是“软件库”工作区中的“软件更新组”节点。 

在节点中可选择箭头以最小化导航窗格。  

![示例节点和突出显示的最小化箭头](media/software-update-groups-node.png)  

当导航窗格处于最小化时，使用“导航栏”在控制台中移动。  

![最小化的 Configuration Manager 导航窗格](media/minimized-navigation-pane.png)  

在控制台中，节点有时会被整理到文件夹中。 通常直接单击文件夹即可转到“导航索引”或“仪表板”。  

![Configuration Manager 软件更新导航索引](media/software-updates-navigation-index.png)  


### <a name="ribbon"></a>功能区 

功能区位于 Configuration Manager 控制台顶部。 功能区可以有多个选项卡，且可使用右侧的箭头将其最小化。 功能区上的按钮数量因节点而异。 上下文菜单中也提供了功能区中的大多数按钮。  

![示例功能区，突出显示多个选项卡和最小化箭头](media/ribbon.png)   


### <a name="details-pane"></a>细节窗格

若要获取有关项的其他信息，可查看细节窗格。 细节窗格中可以有一个或多个选项卡。 选项卡的数量因节点而异。  

![Configuration Manager 示例细节窗格](media/details-pane.png)   


### <a name="columns"></a>列 

可添加、删除、重新排列并调整列的大小。 通过这些操作，可让系统显示你喜欢的数据。 可用列的数量因节点而异。 要在视图中添加或删除列，请右键单击现有列标题，然后选择其中一项。 将列标题拖动到想要的位置即可对其重新排序。  

![Configuration Manager 添加列](media/add-columns.png)  

在列上下文菜单的底部，可以按列进行排序或分组。 另外，也可通过选择列标题对列进行排序。  

![Configuration Manager 按列分组](media/column-group-by.png)  

## <a name="bkmk_viewconnected"></a>查看最近连接的控制台
<!--3699367-->

从版本 1902 开始，可以查看 Configuration Manager 控制台的最新连接。 视图包括活动连接和最近连接。 始终可在列表中看到当前控制台连接，并且只能看见来自 Configuration Manager 控制台的连接。 而看不到 PowerShell 或其他基于 SDK 的到 SMS 提供程序的连接。 该站点将从列表中删除 30 天以前的实例。


### <a name="prerequisites-to-view-connected-consoles"></a>查看已连接控制台的先决条件

- 帐户需要 SMS_Site 对象的读取权限 
- 需要在 SMS 提供程序服务器上安装 IIS <!---SCCMDocs-pr issue 1326--> 
- 启用 SMS 提供程序以使用证书。<!--SCCMDocs-pr issue 3135--> 使用以下选项之一：  

  - 启用[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)（推荐）
  - 将基于 PKI 的证书手动绑定到承载 SMS 提供程序角色的服务器上的 IIS 中的端口 443  

### <a name="view-connected-consoles"></a>查看已连接控制台

1. 在 Configuration Manager 控制台中，转到“管理”工作区。  

2. 展开“安全”并选择“控制台连接”节点。  

3. 查看具有以下属性的最近连接：  

    - 用户名
    - 计算机名
    - 已连接的站点代码
    - 控制台版本
    - 上次连接时间：用户上一次打开控制台的时间

![查看 Configuration Manager 控制台连接](media/console-connections.png) 

## <a name="command-line-options"></a>命令行选项

Configuration Manager 控制台提供下列命令行选项：

|选项|说明|  
|------------|-----------------|  
|`/sms:debugview=1`|DebugView 包含在用于指定视图的所有 ResultView 中。 DebugView 显示原始属性（名称和值）。|  
|`/sms:NamespaceView=1`|在控制台中显示命名空间视图。|  
|`/sms:ResetSettings`|控制台忽略用户保留的连接和视图状态。 窗口大小未重置。|  
|`/sms:IgnoreExtensions`|禁用任何 Configuration Manager 扩展。|  
|`/sms:NoRestore`|控制台忽略之前保留的节点导航。|  



## <a name="tips"></a>提示

### <a name="send-feedback"></a>发送反馈
<!--1357542-->

自 1806 版起，从控制台提交产品反馈。  

- **发送笑脸**：就喜欢的内容发送反馈  

- **发送哭脸**：就不喜欢的内容发送反馈  

- **发送建议**：转到 UserVoice 分享你的观点  
 
有关详细信息，请参阅[产品反馈](/sccm/core/understand/find-help#BKMK_1806Feedback)。


### <a name="assets-and-compliance-workspace"></a>资产和符合性工作区

#### <a name="view-users-for-a-device"></a>查看设备的用户
自 1806 版起，“设备”节点中提供了以下列：  

- **主要用户** <!--1357280-->  

- **当前登录的用户** <!--1358202-->  
    > [!NOTE]  
    > 查看当前登录的用户需要[用户发现](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adud)和[用户设备相关性](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)。  

有关如何显示非默认列的详细信息，请参阅[列](#columns)。

#### <a name="improvement-to-device-search-performance"></a>设备搜索性能的改进
<!-- 3614690 -->
从 1806 版开始，在设备集合中进行搜索时，它不会针对所有对象属性搜索关键字。 如果搜索内容不精确，则会搜索以下四个属性：
- 名称
- 主要用户
- 当前登录的用户
- 上一个登录用户名

此行为显著缩短了按名称搜索所需的时间（尤其是在大型环境中）。 按特定条件进行的自定义搜索不受此更改的影响。 


### <a name="monitoring-workspace"></a>监视工作区

#### <a name="copy-details-in-monitoring-views"></a>复制监视视图中的详细信息
<!--1357856-->
从版本 1806 开始，从“资产详细信息”窗格复制以下监视节点的信息：  

- 内容分发状态  

- 部署状态  

![部署状态视图，复制资产详细信息](media/1810-deployment-status.PNG)



## <a name="next-steps"></a>后续步骤

[辅助功能](/sccm/core/understand/accessibility-features)

