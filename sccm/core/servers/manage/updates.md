---
title: "更新 | Microsoft Docs"
description: "了解称为“更新与维护服务”的控制台中服务方法，该方法可轻松找到并安装建议的更新。"
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: 51
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 816c6bd33e42b70bbafed0dea7624bc5a5421544
ms.openlocfilehash: 55d4f1805937405c4101f5b814875818d2aa72c0


---
# <a name="updates-for-system-center-configuration-manager"></a>System Center Configuration Manager 的更新

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 使用称为“更新和维护服务”的控制台中服务方法，可轻松为 Configuration Manager 基础结构找到并安装建议的更新。 此控制台中服务方法由带外更新补充，例如适用于需要解决其环境特定问题的客户的修补程序。  

> [!TIP]
> 管理 System Center Configuration Manager 站点和层次结构基础结构时，术语“升级”、“更新”和“安装”用于描述三种不同概念。 若要了解每个术语的使用方法，请参阅[有关升级、更新和安装](/sccm/core/understand/upgrade-update-install)。


 **以下主题可帮助了解如何为 System Center Configuration Manager 查找和安装不同更新类型：**  

-   [为 System Center Configuration Manager 安装控制台中更新](../../../core/servers/manage/install-in-console-updates.md)  

-   [使用适用于 System Center Configuration Manager 的服务连接工具](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [使用更新注册工具将修补程序导入 System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [使用修补程序安装程序为 System Center Configuration Manager 安装更新](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


如果使用 Technical Preview 分支，请参阅[System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview) 了解特定于该分支的其他信息。


##  <a name="a-namebkmkbaselinesa-baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> 基准和更新版本  
 System Center Configuration Manager Current Branch 的初始版本为版本 1511，即基准版本。 最近版本 1606 作为基准版本发布：  

-   在新的层次结构中安装新站点时，请使用最新的基准版本。  

-   必须使用基准版本从 System Center 2012 Configuration Manager 升级。  

-   我们会定期发布其他基准版本。 使用最新基准版本安装新的层次结构时，应避免安装过期版本的 Configuration Manager，然后升级基础结构以使其保持最新状态。  

安装基准版本之后，其他版本的 Configuration Manager 都可用作控制台中更新。 控制台中更新可将你的基础结构更新为最新版本的 Configuration Manager。  

-   请安装控制台中更新来更新顶层站点的版本。  

-   在管理中心站点上安装的更新将自动安装到子主站点，除非主站点中配置的维护窗口阻止。  

-   必须手动在控制台中将辅助站点更新到新的更新版本。  

安装更新时，更新会将该版本的安装文件存储在站点服务器上名为 CD.Latest 的文件夹中。 有关这些文件的详细信息，请参阅 [System Center Configuration Manager 的 CD.Latest 文件夹](../../../core/servers/manage/the-cd.latest-folder.md)。  

-   可以使用 CD.Latest 文件夹中的文件来进行站点恢复，以及在不再运行基准版本的层次结构中安装其他站点。  

-   不能使用 CD.Latest 中的安装文件来安装新层次结构的首个站点，或从 System Center 2012 Configuration Manager 升级站点。  

Configuration Manager 的某些更新可用作现有基础结构的控制台中更新版本，以及新的基准版本。  

以下版本的 Configuration Manager 可用作基准和/或更新：  

|版本|可用日期|[支持结束日期](/sccm/core/servers/manage/current-branch-versions-supported) |Baseline|控制台中更新|  
|-------------|-----------|------------|--------------|------------------------|  
| 1511 <br /><br /> 5.00.8325.1000|2015 年&12; 月&8; 日| 2016 年&12; 月&8; 日|是|否|  
|[1602](/sccm/core/plan-design/changes/whats-new-in-version-1602)<br /><br /> 5.00.8355.1000|2016 年&3; 月&11; 日| 2017 年&3; 月&11; 日|否|是|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|2016/7/22| 2017 年&7; 月&22; 日|否|是|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) 和 1606 修补程序汇总 (KB3186654) </br></br>5.00.8412.1307（注释 1） |2016/10/12| 2017 年&7; 月&22; 日|是|否|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|2016/11/18| 11/18/2017|否|是|
（注释 1）此 1606 基线介质作为 Microsoft System Center 2016 或 System Center Configuration Manager（Current Branch 和 Long-Term Servicing Branch 1606）版的一部分提供。

若要检查 Configuration Manager 站点的版本，请在控制台中，转至控制台左上角的 **“关于 System Center Configuration Manager”** ，新站点和控制台版本将会显示在那里。  

##  <a name="a-namebkmkinconsolea-in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> 控制台中更新和服务  
 使用 System Center Configuration Manager 的生产就绪型安装（也称为当前分支）时，通过“更新和维护服务”渠道可提供安装的大部分更新。 此方法标识、下载并提供适用于你当前基础结构版本和配置的更新，并且仅包含 Microsoft 针对所有客户建议的更新。   
 其中包括:  

-   新版本，如版本 1602  

-   更新，包括当前版本的新功能  

-   修补程序，适用于你的 Configuration Manager 版本，所有客户都应安装  

控制台中更新可提供更强的稳定性并解决常见的问题。 它们可替代早期产品版本的更新类型，如服务包、累积更新、适用于所有客户的修补程序以及 Extension for Microsoft Intune。 这些更新可应用于以下一种或多种设备：  

-   主站点和管理中心站点服务器  

-   站点系统角色和站点系统服务器  

-   SMS 提供程序的实例  

-   Configuration Manager 控制台  

-   Configuration Manager 客户端  

将服务连接点站点系统角色与 Microsoft 云服务和下载中心同步时，Configuration Manager 会发现新的更新：  

-   当服务连接点处于联机模式时，站点将每天与 Microsoft 同步，以自动确定适用于你的基础结构的新更新。  若要下载更新和用于更新的 redist 文件，则承载服务连接点站点系统角色的计算机使用**系统**上下文访问以下 Internet 位置：go.microsoft.com 和 download.microsoft.com。 有关服务连接点连接到的其他位置的信息，请参阅[关于 System Center Configuration Manager 中的服务连接点](../../../core/servers/deploy/configure/about-the-service-connection-point.md)中的 [Internet 访问要求](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls)。  

-   当服务连接点处于脱机模式时，请使用服务连接工具手动与 Microsoft 云同步。 有关详细信息，请参阅 [Use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md)。  

-   凭借控制台中更新，无需再单独查找和安装单个更新、服务包和新功能。  

-   只安装选择的控制台中更新，并且安装某些更新时，可以选择要启用和使用的各个功能。 有关详细信息，请参阅[启用更新中的可选功能](../../../core/servers/manage/install-in-console-updates.md#bkmk_options)。  

安装控制台中更新时：  

-   它将自动运行先决条件检查。 也可以先运行此检查，再开始安装。  

-   它自动在管理中心站点（如果有）和主站点上安装。 可以通过使用[站点服务器的服务时段](../../../core/servers/manage/service-windows.md)控制允许每个主站点服务器更新其基础结构的时间。  

-   站点服务器更新后，受影响的所有站点系统角色 （包括 SMS 提供程序的实例）会自动更新。 站点安装更新后，Configuration Manager 控制台还会提示控制台用户更新控制台。  

-   如果更新包括 Configuration Manager 客户端，还会提供在预生产中测试更新或立即将更新应用到所有客户端的选项。  

-   更新主站点后，辅助站点不会自动更新。 而必须启动辅助站点更新。  

> [!NOTE]  
>  System Center Configuration Manager (Current Branch) 的生产版本、Long-Term Servicing Branch 和 Technical Preview for System Center Configuration Manager 是不同的版本。 因此，适用于一个分支的更新无法作为其他分支的控制台中更新。 有关可用分支的详细信息，请参阅[我应使用 Configuration Manager 的哪一个分支？](/sccm/core/understand/which-branch-should-i-use)

##  <a name="a-namebkmkoutofbanda-out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> 带外修补程序  
一些修补程序在发布时的可用性受到限制，用于解决特定的问题，或者虽然适用于所有客户，但不能使用控制台中方法进行安装。 这些修补程序在带外提供，Microsoft 云服务不会发现。  

通常情况下，可从 Microsoft 客户支持服务、知识库文章或 [System Center Configuration Manager 团队博客](https://blogs.technet.microsoft.com/configmgrteam)了解带外修补程序，以寻求修复或解决 Configuration Manager 部署问题的方法。  

请使用以下两种方法中的一种手动安装这些修补程序：  

-   **更新注册工具：**使用此工具，可手动将修补程序导入 Configuration Manager 控制台，然后可以根据需要在控制台中安装自动发现的控制台中更新。 此方法适用于使用以下文件名结构的更新： **.update.exe**.  此类修补程序的完整文件名类似于：**&lt;产品\>-&lt;产品版本\>-&lt;知识库文章 ID\>-ConfigMgr.Update.exe**。  

     有关详细信息，请参阅[使用更新注册工具将修补程序导入 System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)。  

-   **修补程序安装工具：** 此工具用于手动安装无法使用控制台中方法安装的修补程序。 此方法用于使用如下文件名结构的修补程序：**&lt;产品\>-&lt;产品版本\>-&lt;知识库文章 ID\>-&lt;平台\>-&lt;语言\>.exe**。

     有关详细信息，请参阅[使用修补程序安装程序为 System Center Configuration Manager 安装更新](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)。



<!--HONumber=Feb17_HO1-->


