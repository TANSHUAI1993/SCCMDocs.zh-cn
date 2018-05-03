---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1804 版中提供的新功能。
ms.date: 04/25/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82de25f24771d4b66d58a550eb4caed6ad262869
ms.sourcegitcommit: d67c6246bb6027cd5501e772b0521f9272407c28
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2018
---
# <a name="capabilities-in-technical-preview-1804-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1804 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍 Configuration Manager Technical Preview 1804 版中提供的功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 

安装此更新之前，请查看 [Technical Preview](/sccm/core/get-started/technical-preview) 一文。 该文章将帮助你熟悉使用 Technical Preview 的常规要求和限制，如何在版本之间进行更新以及如何提供相关的反馈。     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>此 Technical Preview 中的已知问题

### <a name="bkmk_appcathttps"></a> 应用程序目录 Web 服务点不能是启用了 HTTPS 的服务点
<!--512637-->
如果应用程序目录 Web 服务点是启用了 HTTPS 的服务点：

- 可供用户使用的已部署的应用程序不会在软件中心显示  

- 在 awebsctl.log 中显示以下错误：  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>解决方法
重新配置应用程序目录 Web 服务点以使用 HTTP 连接进行通信。  




</br>

**以下是此版本可以试用的新功能。**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>配置用于站点服务器的远程内容库  
<!--1357525-->
若要释放主站点服务器上的硬盘空间，请将其[内容库](/sccm/core/plan-design/hierarchy/the-content-library)重新定位到另一个存储位置。 可以将内容库移至站点服务器上的另一个驱动器、单独服务器或者存储区域网络 (SAN) 中的容错磁盘。 我们建议 SAN，因为它提供了弹性存储，随着时间的推移，它会增长或收缩，以满足不断变化的内容需求。 

此远程内容库是[站点服务器角色高可用性](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability)的新先决条件。 

> [!Note]  
> 此操作仅在站点服务器上移动内容库。 它不会影响分发点上的内容库的位置。 

### <a name="prerequisites"></a>先决条件  
- 站点服务器计算机帐户需要将内容库移至其中的网络路径的“读取”和“写入”权限。 远程系统上不安装任何组件。 

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，切换到“管理”工作区。 展开“站点配置”并选择“站点”。 在详细信息窗格底部的“摘要”选项卡上，注意“内容库”的新列。  

2. 单击功能区上的“管理内容库”。  

3. 选择“在网络共享上”，然后输入有效的网络路径。 此路径是站点将内容库移至其中的位置。 单击" **确定**"。  

4. 请注意“详细信息”窗格中内容库列的“Status”属性。 它会更新以显示站点在移动内容库方面的进度。 在进程中，它显示已完成的百分比。 如果存在错误状态，将显示错误。 典型错误包括 `access denied` 或 `disk full`。 完成时，显示 `OK`。 有关详细信息，请参阅 **distmgr.log**。 有关详细信息，请参阅[站点服务器和站点系统服务器日志](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog)。  

如果需要将内容库移回站点服务器，请重复此过程，但选择选项“本地到站点服务器”。  

> [!Tip]  
> 若要将内容移动到站点服务器上的另一个驱动器，请使用“内容库传输”工具。 有关详细信息，请参阅 [Configuration Manager 工具包](#configuration-manager-toolkit)。  



## <a name="bkmk_feedback"></a> 从 Configuration Manager 控制台提交反馈  
<!--1357542-->

发送笑脸！ 现在可以就你的体验直接告知 Configuration Manager 团队。 从 Configuration Manager 控制台发送反馈很简单。 我们希望听到你的所有反馈：表扬、问题和建议。  

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送反馈，以便我们了解其运作状况。  

1. 在 Configuration Manager 控制台中，单击功能区上方右上角的笑脸按钮。  

2. 从下拉列表中，选择可用选项之一：  

   - 发送笑脸：你真的很喜欢！ 对于此选项，请输入反馈详细信息。 然后根据需要包含屏幕截图和电子邮件地址。  

   - 发送哭脸：在控制台中遇到问题，或内容未按预期方式工作。 对于此选项，请输入潜在产品问题的详细信息。 然后根据需要包含屏幕截图、电子邮件地址和诊断数据。  

   - 发送建议：你对更改和改进 Configuration Manager 有想法。 此选项将在 Web 浏览器中打开我们的 [UserVoice](https://configurationmanager.uservoice.com) 网站。  

该反馈将直接提交给 Configuration Manager 的 Microsoft 产品团队。 虽然仍然支持使用 Windows 10 反馈中心，但最好使用控制台内部的反馈机制。  

以下匿名信息始终包含在上下文反馈中：  

 - Configuration Manager 控制台版本和语言  

 - Configuration Manager 站点版本  

 - 支持 ID，也称为层次结构 ID  

 - OS 版本和运行控制台的系统语言  

 - 在控制台中单击笑脸的确切位置  

此数据与我们的诊断和使用情况数据的集合一致。 有关详细信息，请参阅[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)。

### <a name="known-issues"></a>已知问题

如果尝试从无法访问 Internet 的设备发送反馈，可能会意外关闭应用程序。 若要发送笑脸或哭脸，请确保设备能够访问 petrol.office.microsoft.com。



## <a name="support-center"></a>支持中心
<!--1357489-->

使用支持中心排除客户端故障、查看实时日志，或者捕获 Configuration Manager 客户端计算机状态供日后分析。 支持中心是用于整合多个管理员故障排除工具的单一工具。 在 Technical Preview 中可以看到修复了 bug 并进行了改进的支持中心最新版本的预览，以及我们的新日志查看器的预览。 在站点服务器的 cd.latest\SMSSETUP\Tools\SupportCenter 文件夹中找到支持中心安装程序。

 > [!Tip]  
 > 支持中心中的现有功能的旧文档在 [TechNet](https://technet.microsoft.com/library/dn688621.aspx) 上提供。 相关信息正在迁移到 docs.microsoft.com 库。  

### <a name="new-support-center-features"></a>新支持中心功能  

 - 新日志查看器 OneTrace。 其工作方式类似于 CMTrace，并包括改进，例如选项卡式视图和可停靠窗口。  

 - 新的数据收集器功能将从本地或远程 Configuration Manager 客户端收集诊断日志。 它提供清单（替换客户端 Spy）、策略（替换策略 Spy）以及客户端缓存的实时诊断。  



## <a name="configuration-manager-toolkit"></a>Configuration Manager 工具包
<!--1357145-->

Configuration Manager 服务器和客户端工具现在 Technical Preview 中提供。 可在站点服务器的 cd.latest\SMSSETUP\Tools 文件夹中找到这些工具。 无需进行其他安装。

#### <a name="server-tools"></a>服务器工具  

 - DP 作业管理器：对面向分发点的内容分发作业进行故障排除  

 - 集合评估查看器：查看集合评估详细信息  

 - 内容库资源管理器：查看内容库单一实例存储的内容  

 - 内容库传输：在驱动器之间传输内容库  

 - 内容所有权工具：更改孤立包的所有权。 这些包存在于没有自有站点服务器的站点。  

 - 基于角色的管理和审核工具：可帮助管理员审核角色配置  

#### <a name="client-tools"></a>客户端工具

 - CMTrace：查看日志  

 - 部署监视工具：对应用程序、更新和基线部署进行故障排除  

 - 策略 Spy：查看策略分配  

 - Power Viewer 工具：查看电源管理功能的状态  

 - 发送计划工具：触发 DCM 基线的计划和评估  

> [!Important]  
> 对于大多数用例，建议使用[支持中心](#support-center)，因为它包含以下工具的相同或改进功能：  
>  - 客户端 Spy
>  - CMTrace<sup>1</sup> 
>  - 部署监视工具
>  - 策略 Spy
>  - 发送计划工具
> 
> <sup>1</sup> CMTrace 不依赖于 .NET 或 Windows Presentation Foundation (WPF)，因此仍在 Windows PE 启动映像中使用。



## <a name="uninstall-application-on-approval-revocation"></a>在批准撤消时卸载应用程序
<!--1357891-->

当你撤消应用程序的批准时，行为已更改。 现在当你拒绝应用程序的请求时，客户端将从用户的设备卸载应用程序。 

### <a name="prerequisites"></a>先决条件
- 启用功能“审批每台设备的用户的应用程序请求”。

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，向用户部署需要批准的应用程序。 在部署的“部署设置”选项卡上，启用选项“管理员必须批准对设备上的此应用程序的请求”。  

2. 在软件中心的 Configuration Manager 客户端上，用户请求批准以安装应用程序。  

3. 在 Configuration Manager 控制台中，批准此用户在设备上安装应用程序的请求。 应用程序批准请求显示在“软件库”工作区的“应用程序管理”下的“批准请求”节点中。  

4. 在软件中心的客户端上，用户安装应用程序。  

5. 在 Configuration Manager 控制台中，拒绝用户在设备上对应用程序的请求。  

### <a name="known-issues"></a>已知问题
- 当用户在客户端上安装应用程序后，更新用户策略。 在软件中心，切换到“选项”选项卡，展开“计算机维护”并单击“同步策略”。<!--480609-->  

- 应用程序目录 Web 服务点必须是 HTTPS。 有关详细信息，请参阅[此 Technical Preview 中的已知问题](#bkmk_appcathttps)。<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>从发现中排除 Active Directory 容器
<!--1358143-->
若要减少发现的对象数，现在可以从 Active Directory 系统发现中排除特定容器。 此功能是 [UserVoice 反馈](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery)的结果。

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“层次结构配置”并选择“发现方法”。 选择“Active Directory 系统发现”，然后单击功能区中的“属性”。  

2. 单击“新建”图标，以指定新的 Active Directory 容器。   

3. 在“Active Directory 容器”对话框中，在“位置”部分浏览到或输入“路径”以启动发现。  

4. 在“搜索选项”部分，启用选项“以递归方式搜索 Active Directory 子容器”。 然后单击“添加”以选择要从此发现中排除的子容器。  

5. 在“选择新容器”对话框中，选择要排除的子容器。 单击“确定”以关闭“选择新容器”对话框。  

6. 单击“确定”以关闭“Active Directory 容器”对话框。  

7. 在“Active Directory 系统发现属性”窗口中，查看在其中启动发现的 Active Directory 容器的路径。 “递归”列显示“是”，新的“已排除”列也显示“是”。 单击“确定”以关闭“Active Directory 系统发现属性”窗口。  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>在软件中心指定应用程序目录网站链接的可见性
<!--1358214-->

现在，可以控制“打开应用程序目录网站”的链接是否显示在软件中心的“安装状态”节点中。  

> [!Note]  
> 对应用程序目录网站用户体验的支持将在 2018 年 6 月 1 日后发布的首个更新中结束。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。  

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，通过“管理”工作区中的“客户端设置”节点来创建自定义客户端设备设置策略。  

2. 选择“软件中心”组。  

3. 对于“软件中心设置”，单击“自定义”。  

4. 启用选项“在软件中心中隐藏应用程序目录网站链接”。   

有关客户端设置的详细信息，请参阅[配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>通过软件更新体系结构更新自动部署规则
 <!--1322266-->
现在可以筛选自动部署规则以排除 Itanium 和 ARM64 等体系结构。

### <a name="try-it-out"></a>试试看！
尝试完成任务。 然后发送[反馈](#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，切换到“软件库”工作区。 展开“软件更新”，并选择“自动部署规则”。 在功能区，选择“创建自动部署规则”。  

2. 在“常规”选项卡和“部署设置”选项卡中填写适当的设置。  

3. 在“软件更新”选项卡上，选择“体系结构”，然后单击“搜索条件”中的“要查找的项”。  

4. 选择要包括在自动部署规则中的体系结构。  

5. 单击“下一步”，然后继续创建自动部署规则。  

> [!IMPORTANT]  
> 请记住，有 32 位 (x86) 应用程序和组件在 64 位 (x64) 系统上运行。 除非确定不需要 x86，否则在选择 x64 时也请启用它。  

### <a name="known-issues"></a>已知问题
在添加体系结构条件后，自动部署规则属性页将在搜索条件中显示“Title”。 自动部署规则仍会按预期运行，并选择正确的软件更新。 但是，此时不能同时包括“Architecture”和“Title”条件。 <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>对 OS 部署的改进
我们对 OS 部署做了以下改进，其中有些是根据用户之声的反馈做出的。  

 - [隐藏存储在任务序列变量中的敏感数据](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed)：在[设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)步骤中，选择新选项“不显示此值”。 例如，当指定密码时。<!--1358330--> 当启用此选项时，以下行为适用：
   - 变量值不显示在 smsts.log 中。
   - Configuration Manager 控制台和 SMS 提供程序处理此值的方式与处理其他机密（如密码）的方式相同。
   - 导出任务序列时，该值不包括在内。
   - 编辑步骤时，任务序列编辑器不读取此值。 重新键入整个值以进行更改。

   > [!Important]  
   > 变量及其值同任务序列作为 XML 保存，并以混淆方式置于数据库中。 当客户端从管理点请求任务序列策略时，它会在传输过程中加密，并存储在客户端上。 但是，所有变量值都是客户端上运行时期间内存的任务序列环境中的纯文本。 如果任务序列包含一个输出变量值的步骤，此输出将为纯文本。 此行为需要管理员显式操作，以便在任务序列中包含此类步骤。 


 - [在任务序列的运行命令步骤中隐藏程序名称](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed)：若要禁止显示或记录潜在的敏感数据，请将任务序列变量“OSDDoNotLogCommand”设置为 `TRUE`。 此变量在[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)任务序列步骤中隐藏 smsts.log 中的程序名称。 <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>对 Configuration Manager 控制台的改进
- 在查看“资产和符合性”、“设备集合”下的成员集合时，主要用户信息现可见。<!--510252-->  



## <a name="next-steps"></a>后续步骤
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。    
