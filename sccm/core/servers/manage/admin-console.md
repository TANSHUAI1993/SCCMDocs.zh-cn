---
title: Configuration Manager 控制台
titleSuffix: Configuration Manager
description: 了解如何导航 Configuration Manager 控制台。
ms.date: 08/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b93e636ea690fa99fd2a0dfc63bd12932d2f7a5e
ms.sourcegitcommit: b5c7496ca408803046acc8403858aafd5dca8808
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794665"
---
# <a name="using-the-configuration-manager-console"></a>使用 Configuration Manager 控制台

适用范围：  System Center Configuration Manager (Current Branch)

管理员使用 Configuration Manager 控制台管理 Configuration Manager 环境。 本文介绍导航控制台的基础知识。  


## <a name="connect-to-a-site-server"></a>连接到站点服务器

控制台可连接到管理中心站点服务器或主站点服务器。 但是，无法将 Configuration Manager 控制台连接到辅助站点。 你可以[安装 Configuration Manager 控制台](/sccm/core/servers/deploy/install/install-consoles)。 安装过程中，指定控制台连接的站点服务器的完全限定的域名 (FQDN)。

要连接到其他站点服务器，请按以下步骤操作：

1. 选择[功能区](#ribbon)顶部的箭头，然后选择“连接到新站点”  。  

    ![将控制台连接到新站点](media/connect-to-a-new-site.png)  

2. 键入站点服务器的 FQDN。 如果之前已连接到站点服务器，可从下拉列表中选择服务器。  

    ![站点连接窗口，输入站点服务器的 FQDN](media/site-server-fqdn.png)  

3. 选择“**连接**”。  

从版本 1810 开始，可以为管理员指定访问 Configuration Manager 站点的最低身份验证级别。 此功能强制管理员以要求的级别登录到 Windows。 有关详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth)。 <!--1357013-->  


## <a name="navigation"></a>导航

控制台的某些区域可能未显示，具体取决于所分配的安全角色。 有关角色的详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。

### <a name="workspaces"></a>工作区

Configuration Manager 控制台中有四个工作区  ：  

- **资产和符合性**  

- **软件库**  

- **监视**  

- **管理**  

![带上下文菜单的 Configuration Manager 工作区](media/configuration-manager-workspaces.png)  

选择向下箭头并选择“导航窗格选项”，可对工作区按钮重新进行排序  。 选中某个项“上移”或“上移”   。 单击“重置”还原默认按钮顺序  。  

![用于对工作区重新排序的“导航窗格选项”窗口](media/navigation-pane-options.png)  

选择“显示更少按钮”可最小化工作区按钮  。 列表中的最后一个工作区首先最小化。 选择已最小化的按钮并选择“显示更多按钮”即可将按钮恢复为原始大小  。

![Configuration Manager 控制台中最小化的工作区](media/workspace-buttons.png)  

### <a name="nodes"></a>节点

工作区是一系列节点  。 其中一个节点是“软件库”工作区中的“软件更新组”节点   。

在节点中可选择箭头以最小化导航窗格。  

![示例节点和突出显示的最小化箭头](media/software-update-groups-node.png)  

当导航窗格处于最小化时，使用“导航栏”在控制台中移动  。  

![最小化的 Configuration Manager 导航窗格](media/minimized-navigation-pane.png)  

在控制台中，节点有时会被整理到文件夹中。 选择文件夹时，通常会显示导航索引或仪表板   。  

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
- 在 SMS 提供程序服务器上安装 IIS <!---SCCMDocs-pr issue 1326-->
- 启用 SMS 提供程序以使用证书。<!--SCCMDocs-pr issue 3135--> 使用以下选项之一：  

    - 启用[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)（推荐）
    - 将基于 PKI 的证书手动绑定到承载 SMS 提供程序角色的服务器上的 IIS 中的端口 443  

### <a name="view-connected-consoles"></a>查看已连接控制台

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。  

2. 展开“安全”并选择“控制台连接”节点   。  

3. 查看具有以下属性的最近连接：  

    - 用户名
    - 计算机名
    - 已连接的站点代码
    - 控制台版本
    - 上次连接时间：用户上一次打开控制台的时间 

![查看 Configuration Manager 控制台连接](media/console-connections.png) 


## <a name="bkmk_notify"></a> Configuration Manager 控制台通知

<!--3556016, fka 1318035-->
从 Configuration Manager 版本 1902 起，控制台将通知你以下事件：

- Configuration Manager 本身有可用的更新
- 环境中发生生命周期和维护事件

此通知位于功能区下方控制台窗口顶部的栏。 Configuration Manager 更新可用时，它将替换以前的体验。 这些控制台内通知仍显示关键信息，但不会干扰你在控制台中的工作。 不能消除重要通知。 控制台在标题栏的新通知区域中显示所有通知。

![控制台中的通知栏和标志](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>配置站点以显示非重要通知

可以从各个站点的属性中配置站点，以显示非重要通知。

1. 在“管理”工作区中，展开“站点配置”，然后选择“站点”节点    。
1. 选择想要为其配置非重要通知的站点。
1. 在功能区中，选择“属性”  。
1. 在“警报”选项卡上，选择“为非重要站点运行状况更改启用控制台通知”选项   。
   - 如果启用此设置，则所有控制台用户都会看到重要、警告和信息通知。 默认情况下将启用此设置。  
   - 如果禁用此设置，控制台用户只能看到重要通知。  

大多数控制台的通知都是按会话操作的。 控制台在用户启动查询时会对其进行评估。 要查看通知中的更改，请重启控制台。 如果用户关闭非重要通知，则在控制台重启时它会再次通知（如果仍然适用）。

以下通知每五分钟重新评估一次：

- 站点处于维护模式  
- 站点处于恢复模式  
- 站点处于升级模式  

通知遵循基于角色的管理的权限。 例如，如果用户没有权限查看 Configuration Manager 更新，则用户看不到这些通知。

某些通知具有相关操作。 例如，如果控制台版本与站点版本不匹配，请选择“安装新控制台版本”  。 此操作将启动控制台安装程序。

以下通知最适用于技术预览分支：  

- 评估版本将在 30 天内到期（警告）：评估版本在 30 天内即将到期  
- 评估版已过期（重要）：已超过评估版本的到期日期  
- 控制台版本不匹配（重要）：控制台版本与站点版本不匹配  
- 有可用的站点更新（警告）：有一个新的更新包可用  

有关详细信息和疑难解答帮助，请参阅控制台计算机上的 SmsAdminUI.log 文件  。 默认情况下，此日志文件位于以下路径：`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`。


## <a name="bkmk_doc-dashboard"></a> 控制台中的文档仪表板

<!--3556019 FKA 1357546-->
从 Configuration Manager 版本 1902 起，新“社区”工作区包含“文档”节点。   此节点包含有关 Configuration Manager 文档和支持文章的最新信息。 它包括以下部分：  

### <a name="product-documentation-library"></a>产品文档库

-  推荐：重要文章的手动特选列表。
-  趋势：上个月的最热门文章。
-  最近更新：上个月修订的文章。

### <a name="support-articles"></a>支持文章

-  疑难解答文章：用来帮助排查 Configuration Manager 组件和功能问题的演练指南。
-  新的和更新的支持文章：过去两个月新的或更新的支持文章。


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

### <a name="general"></a>常规

#### <a name="role-based-administration-for-folders"></a>文件夹的基于角色的管理
<!--3600867-->
（从版本 1906 中引入） 

可以在文件夹上设置安全作用域。 如果有权访问文件夹中的对象，但无权访问文件夹，则无法查看对象。 同样，如果有权访问文件夹，但无权访问该文件夹中的对象，则无法查看对象。 右键单击文件夹，选择“设置安全作用域”  ，然后选择要应用的安全作用域。

#### <a name="views-sort-by-integer-values"></a>视图按整数值排序

（从版本 1902 中引入） 

我们改进了各个视图对数据排序的方式。 例如，在“监视”工作区的“部署”节点中，以下列现在按数字而不是字符串值排序   ：  

- 错误数
- 正在进行的数量
- 其他数量
- 成功数
- 未知数量  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>移动警告以获得大量结果

（从版本 1902 中引入） 

在控制台中选择返回 1,000 个以上结果的节点时，Configuration Manager 将显示以下警告：

> Configuration Manager 返回了大量结果。 可使用搜索缩小结果范围。 或者，单击此处可查看最多 100000 个结果。

此警告和搜索字段之间现在有额外的空白区域。 此次移动有助于防止无意中选择该警告，从而显示更多结果。

#### <a name="send-feedback"></a>发送反馈

（从版本 1806 中引入） 
<!--1357542-->

从控制台提交产品反馈。  

- **发送笑脸**：就喜欢的内容发送反馈  

- **发送哭脸**：就不喜欢的内容发送反馈  

- **发送建议**：转到 UserVoice 分享你的观点  

有关详细信息，请参阅[产品反馈](/sccm/core/understand/find-help#BKMK_1806Feedback)。


### <a name="assets-and-compliance-workspace"></a>资产和符合性工作区

#### <a name="real-time-actions-from-device-lists"></a>设备列表中的实时操作
<!--4616810-->
（从版本 1906 中引入） 

有多种方法可以在“资产和符合性”工作区中的“设备”节点下显示设备列表   。

- 在“资产和符合性”  工作区中，选择“设备集合”  节点。 选择设备集合，然后选择“显示成员”操作  。 此操作将打开“设备”节点的子节点，其中包含该集合的设备列表  。  

  - 选择集合子节点时，现在可以从功能区的集合组中启动“CMPivot”  。  

- 在“监视”工作区中，选择“部署”节点   。 选择部署，然后在功能区中选择“查看状态”操作  。 在部署状态窗格中，双击总资产，以向下钻取到设备列表。  

  - 在此列表中选择设备时，现在可以从功能区的“设备”组中启动“CMPivot”和“运行脚本”   。  


#### <a name="collections-tab-in-devices-node"></a>设备节点中的“集合”选项卡
<!--4616810-->
（从版本 1906 中引入） 

在“资产和符合性”工作区中，转到“设备”节点，然后选择设备   。 在详细信息窗格中，切换到新的“集合”选项卡  。此选项卡列出包含此设备的集合。 

> [!Note]  
> 此选项卡当前在“设备集合”节点下的设备子节点中不可用  。 例如，在集合上选择“显示成员”选项时，此选项卡不可用  。


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>将 SMBIOS GUID 列添加到设备和设备集合节点

（从版本 1906 中引入） 

<!--4526580-->
在设备和设备集合节点中，现在可以为“SMBIOS GUID”添加新列    。 此值与 System Resource 类的“BIOS GUID”属性相同  。 它是设备硬件的唯一标识符。

#### <a name="search-device-views-using-mac-address"></a>使用 MAC 地址搜索设备视图

<!--3600878-->
（从版本 1902 中引入） 

可以在 Configuration Manager 控制台的设备视图中搜索 MAC 地址。 此属性在 OS 部署管理员排查基于 PXE 部署的问题时很有用。 查看设备列表时，请向视图添加“MAC 地址”列  。 使用搜索字段添加“MAC 地址”搜索条件  。

#### <a name="view-users-for-a-device"></a>查看设备的用户

自 1806 版起，“设备”节点中提供了以下列  ：  

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


### <a name="software-library-workspace"></a>软件库工作区

#### <a name="order-by-program-name-in-task-sequence"></a>按任务序列中的程序名称进行排序
<!--4616810-->
（从版本 1906 中引入） 

在“软件库”工作区中，展开“操作系统”，选择“任务序列”节点    。 编辑任务序列，然后选择或添加[安装包](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)步骤。 如果包包含多个程序，则下拉列表现在按字母顺序对程序进行排序。

#### <a name="task-sequences-tab-in-applications-node"></a>应用程序节点中的“任务序列”选项卡
<!--4616810-->
（从版本 1906 中引入） 

在“软件库”工作区中，展开“应用程序管理”，转到“应用程序”节点，然后选择应用程序    。 在详细信息窗格中，切换到新的“任务序列”选项卡  。此选项卡列出了引用此应用程序的任务序列。

#### <a name="drill-through-required-updates"></a>钻取必需更新
<!--4224414-->
（从版本 1906 中引入） 

1. 请转到 Configuration Manager 控制台中的以下位置之一：

   - “软件库” > “软件更新” > “所有软件更新”   
   - “软件库” > “Windows 10 维护服务” > “所有 Windows 10 更新”   
   - “软件库” > “Office 365 客户端管理” > “Office 365 更新”   

1. 选择至少一台设备所需的任何更新。
1. 查看“摘要”选项卡，找到“统计信息”下的饼图   。
1. 选择饼图旁的“查看所需更新”超链接以深入查看设备列表  。
1. 此操作将转到“设备”下的临时节点，可以在其中查看需要更新的设备  。 还可对节点执行操作，例如从列表创建新集合。


#### <a name="maximize-the-browse-registry-window"></a>将浏览注册表窗口最大化

<!--3594151 includes all MMS 1902 console changes-->
（从版本 1902 中引入） 

1. 在“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”节点    。
1. 选择具有检测方法的部署类型的应用程序。 例如，Windows Installer 检测方法。
1. 在详细信息窗格中，切换到“部署类型”选项卡  。
1. 打开部署类型的属性，然后切换到“检测方法”选项卡  。选择“添加子句”  。
1. 将“设置类型”更改为“注册表”，然后选择“浏览”以打开“浏览注册表”窗口     。 可将此窗口最大化。  

#### <a name="edit-a-task-sequence-by-default"></a>默认情况下编辑任务序列

（从版本 1902 中引入） 

在“软件库”工作区中，展开“操作系统”，选择“任务序列”节点    。 打开默认序列时，默认操作是“编辑”  。 默认操作以前为“属性”  。  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>从应用程序部署转到集合

（从版本 1902 中引入） 

1. 在“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”节点    。
1. 选择应用程序。 在详细信息窗格中，切换到“部署”选项卡  。
1. 选择部署，然后在“部署”选项卡的功能区中选择新的“集合”选项  。此操作将视图切换到作为部署目标的集合。
   - 在此视图中右键单击部署上的上下文菜单也可以执行此操作。


### <a name="monitoring-workspace"></a>监视工作区

#### <a name="correct-names-for-client-operations"></a>正确的客户端操作名称
<!--4616810-->
（从版本 1906 中引入） 

在“监视”工作区中，选择“客户端操作”   。 现在，“切换到下一个软件更新点”操作已正确命名  。

#### <a name="show-collection-name-for-scripts"></a>显示脚本的集合名称
<!--4616810-->
（从版本 1906 中引入） 

在“监视”工作区中，选择“脚本状态”节点   。 除了列出 ID 之外，还列出了“集合名称”  。

#### <a name="remove-content-from-monitoring-status"></a>从监视状态中删除内容

（从版本 1902 中引入） 

1. 在“监视”工作区中，展开“分发状态”，然后选择“内容状态”    。
1. 选择列表中的项，然后选择功能区中的“查看状态”选项  。
1. 在“资产详细信息”窗格中，右键单击分发点，然后选择新选项“删除”  。 此操作会从选定的分发点中删除此内容。

#### <a name="copy-details-in-monitoring-views"></a>复制监视视图中的详细信息

（从版本 1806 中引入） 
<!--1357856-->
从“资产详细信息”窗格复制以下监视节点中的信息  ：  

- 内容分发状态   

- 部署状态   

![部署状态视图，复制资产详细信息](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>管理工作区

<!--4223683-->
从版本 1906 开始，可以启用“安全”  节点下的某些节点以使用管理服务。 此项更改使控制台可以通过 HTTPS 而不是 WMI 来与 SMS 提供程序进行通信。 有关详细信息，请参阅[管理服务](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service)。


## <a name="next-steps"></a>后续步骤

[辅助功能](/sccm/core/understand/accessibility-features)
