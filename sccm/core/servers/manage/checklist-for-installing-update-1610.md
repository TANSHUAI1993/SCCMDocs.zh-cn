---
title: "1610 的清单 | System Center Configuration Manager"
description: "了解更新到 System Center Configuration Manager 版本 1610 之前需要执行的操作。"
ms.custom: na
ms.date: 11/18/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0c7d32a80559a4aa684ea1533cd36d0ef977fbfc
ms.openlocfilehash: 25bffa256cbe70fb590eccb641c94f572f618ef3

---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>用于为 System Center Configuration Manager 安装更新 1610 的清单

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 的 Current Branch 时，可安装版本 1610 的控制台内部更新，从版本 1606 更新层次结构。 如果层次结构运行版本 1511、1602 或 1606，则可更新到版本 1610。 

若要获取版本 1610 的更新，必须在层次结构的顶层站点上使用服务连接点站点系统角色。 其可处于联机或脱机模式。 层次结构从 Microsoft 下载更新包之后，它会在“管理”&gt;“概述”&gt;“云服务”&gt;“更新和维护服务”下的控制台中显示。

-   当更新列为“可用”时，此更新即可准备安装。 安装版本 1610, 之前，请查看以下[关于安装更新 1610](#about-installing-update-1610)和[清单](#checklist)信息，了解在开始更新之前要进行的配置。

-   如果更新显示为“正在下载”且未更改，请查看 ** hman.log ** 和 ** dmpdownloader.log ** 是否有误。

    -   通常情况下，还可以在站点服务器上重启 SMS\_Executive 服务，以重启更新重新分发文件的下载。

    -   另一个常见的下载问题是代理服务器设置，其阻止 <http://silverlight.dlservice.microsoft.com> 和 <http://download.microsoft.com> 中的下载。

有关安装更新的详细信息，请参阅[控制台内部的更新和维护服务](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing)。

有关 Current Branch 版本的信息，请参阅 [System Center Configuration Manager 更新](/sccm/core/servers/manage/updates#bkmk_Baselines)中的[基线和更新版本](/sccm/core/servers/manage/updates)。

## <a name="about-installing-update-1610"></a>关于安装更新 1610

**站点：**  
只能在层次结构的顶层站点上安装更新 1610。 这意味着会从管理中心站点（如果有）或从独立主站点启动安装。 更新安装在顶层站点后，子站点具有以下更新行为：

-   管理中心站点完成更新安装之后，子主站点会自动安装更新。 可以使用服务时段控制站点安装更新的时间。 版本 1606 之前，服务时段被称为维护时段。 有关详细信息，请参阅[站点服务器的服务时段](https://docs.microsoft.com/en-us/sccm/core/servers/manage/install-in-console-updates#bkmk_ServiceWindow)。

-   在主父站点完成更新安装之后，必须从 Configuration Manager 控制台中手动更新辅助站点。 不支持辅助站点服务器的自动更新。

**站点系统角色：**  
站点服务器安装更新时，站点服务器上安装的站点系统角色和远程计算机上安装的那些角色会自动更新。 因此，安装更新之前，请确保每个站点系统服务器满足使用新更新版本进行操作的任何新的先决条件。

**Configuration Manager 控制台：**   
更新完成之后首次使用 Configuration Manager 控制台时，系统会提示你更新该控制台。 为此，必须在承载该控制台的计算机上运行 Configuration Manager 安装程序，并选择用于更新该控制台的选项。 我们建议不要延迟将更新安装到该控制台。



## <a name="checklist"></a>清单

**确保所有站点都运行支持的 System Center Configuration Manager 版本：**开始安装更新 1610 之前，层次结构中的每个站点都必须运行相同版本的 System Center Configuration Manager（版本 1511、版本 1602 或版本 1606）。

**查看软件保障的状态或等效订阅权限：**   
必须具有有效的软件保障 (SA) 协议才能安装更新 1610。 安装版本 1610 时，可在“许可”选项卡上选择确认“软件保障到期日期”。 这是一个可选值，可将其指定为许可证到期日期的方便提示，在安装未来更新时显示。 如果是从版本 1606 基线介质安装 Configuration Manager，则之前可能在安装时指定此值或在“层次结构设置”的“许可证”选项卡上安装此站点后指定此值。

有关详细信息，请参阅 [System Center Configuration Manager 的许可和分支](/sccm/core/understand/learn-more-editions)。

**查看站点系统服务器上安装的 .NET 版本：**站点安装更新 1610 时，如果尚未安装 .NET Framework 4.5 或更高版本，则 Configuration Manager 会在承载以下站点系统角色之一的每台计算机上自动安装 .NET Framework 4.5.2：

-   注册代理点
-   注册点
-   管理点
-   服务连接点

此安装可以将站点系统服务器置于重启挂起状态，并向 Configuration Manager 组件状态查看器报告错误。 此外，服务器上的 .NET 应用程序可能具有随机故障，直到重新启动服务器。

有关详细信息，请参阅[站点和站点系统先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。

**查看站点和层次结构状态，并确认没有未解决的问题：** 更新站点之前，请解决远程计算机上安装的站点服务器、站点数据库服务器和站点系统角色的所有操作问题。 由于现有的操作问题，站点更新可能会失败。

有关详细信息，请参阅 [Use alerts and the status system for System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system)。

**查看站点之间的文件和数据复制：**   
确保站点之间的文件和数据库复制正常运行并且处于最新状态。 延迟或积压工作可能会阻止平稳或成功更新。\
对于数据库复制，可以在开始更新之前，使用复制链接分析器来帮助解决问题。

有关详细信息，请参阅 [System Center Configuration Manager 中的监视层次结构和复制基础结构](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)主题中的[关于复制链接分析器](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)。

**为托管站点、站点数据库服务器和远程站点系统角色的计算机上的操作系统安装所有合适的关键更新：**为 Configuration Manager 安装更新之前，请为每个适用的站点系统安装任何关键更新。 如果安装的更新需要重启，请在启动 Configuration Manager 更新之前重启合适的计算机。

**在主站点上禁用管理点数据库副本：**   
Configuration Manager 无法成功更新启用了管理点数据库副本的主站点。 禁用数据库复制，然后：

-   创建站点数据库的备份以测试数据库升级
-   为 Configuration Manager 安装更新

有关详细信息，请参阅 [System Center Configuration Manager 管理点的数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)。

**将 SQL Server AlwaysOn 可用性组设置为手动故障转移：**   
在安装更新（例如版本 1610）之前，请确保将可用性组设置为手动故障转移。 站点更新后，可以将故障转移还原为自动故障转移。 有关详细信息，请参阅[站点数据库的 SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。

**重新配置使用 NLB 的软件更新点：**   
Configuration Manager 无法更新使用网络负载平衡 (NLB) 群集来托管软件更新点的站点。

如果为软件更新点使用 NLB 群集，请使用 PowerShell 删除 NLB 群集。
有关详细信息，请参阅 [System Center Configuration Manager 的软件更新计划](/sccm/sum/plan-design/plan-for-software-updates)。

**在站点升级安装的过程中，禁用每个站点上的所有站点维护任务：**   
在安装更新之前，请禁用可能会在更新过程进行时运行的任何站点维护任务。 这包括但不限于以下各项：

-   备份站点服务器
-   删除过期的客户端操作
-   删除过期的发现数据

站点数据库维护任务在更新安装过程中运行时，更新安装可能会失败。 在禁用任务之前，请记录该任务的计划，以便可以在安装更新之后恢复其配置。

有关详细信息，请参阅 [System Center Configuration Manager 的维护任务](/sccm/core/servers/manage/maintenance-tasks)和 [System Center Configuration Manager 维护任务参考](/sccm/core/servers/manage/reference-for-maintenance-tasks)。

**在管理中心站点和主站点上创建站点数据库备份：** 更新站点之前，请备份站点数据库，以确保具有用于灾难恢复的成功备份。

有关详细信息，请参阅 [System Center Configuration Manager 的备份和恢复](/sccm/protect/understand/backup-and-recovery)。

**在最近的站点数据库备份副本上测试数据库升级：**更新 System Center Configuration Manager 管理中心站点或主站点之前，请在站点数据库副本上测试站点数据库升级过程。

-   你应该测试站点数据库升级过程，因为当你升级站点时，可能会修改站点数据库
-   虽然测试数据库升级不是必需的，但可以在生产数据库受到影响之前先行确定升级的问题
-   失败的站点数据库升级可能会使站点数据库无法运行，并且可能需要进行站点恢复以还原功能
-   虽然在层次结构的站点之间共享了站点数据库，但是，请在升级每个合适的站点之前计划在该站点上测试数据库
-   如果在主站点上对管理点使用数据库副本，请在创建站点数据库备份之前禁用复制

Configuration Manager 不支持辅助站点备份，也不支持辅助站点数据库的测试升级。

不支持在生产站点数据库上运行测试数据库升级。 执行此任务会升级站点数据库，并可能导致你的站点无法运行。 有关详细信息，请参阅[升级到 System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) 中的[测试站点数据库升级](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#bkmk_test)部分。

**规划客户端试点：**   
安装更新客户端的更新后，可以在部署和升级所有活动客户端前在预生产中测试新的客户端更新。

若要利用此选项，在开始更新安装之前必须配置站点，以便对预生产支持自动升级。

有关详细信息，请参阅[在 System Center Configuration Manager 中升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients)和[如何在 System Center Configuration Manager 中的预生产集合中测试客户端升级](/sccm/core/clients/manage/upgrade/test-client-upgrades)。

**计划使用服务时段控制站点服务器安装更新的时间：**   
可以使用服务时段定义应用于主站点服务器的时间段，在此期间可以安装该站点的更新。

这可以帮助你控制层次结构中的站点安装更新的时间。 版本 1606 之前，服务时段被称为维护时段。 有关详细信息，请参阅[站点服务器的服务时段](/sccm/core/servers/manage/install-in-console-updates#bkmk_servicewindow)。

**运行安装程序必备组件检查程序：**   
当更新在控制台中列为**可用**时，可以独立运行必备组件检查程序，然后再安装更新。 （在站点上安装更新时，会再次运行必备组件检查程序。）

若要从控制台运行必备组件检查程序，请转到“管理”>“概述”>“云服务”>“更新和维护服务”，右键单击“Configuration Manager 1610 更新包”，然后选择“运行必备组件检查”。

有关启动并监视必备组件检查的详细信息，请参阅[安装 System Center Configuration Manager 的控制台内部更新](/sccm/core/servers/manage/install-in-console-updates)主题中的**步骤 3：安装更新之前运行必备组件检查程序**。

> [!IMPORTANT]  
> 先决条件检查程序作为更新安装的一部分运行或独立运行时，该过程会更新某些用于站点维护任务的产品源文件。 因此，在运行必备组件检查程序之后但安装 1610 更新之前，如果必须执行站点维护任务，则从站点服务器上的 CD.Latest 文件夹运行 **Setupwpf.exe**（Configuration Manager 安装程序）。

**更新站点：**   
现已准备好可以为层次结构开始更新安装。 有关安装更新的信息，请参阅[安装控制台内部更新。](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

我们建议你计划在正常营业时间之外为每个站点安装更新，此时安装更新的过程以及用于重新安装站点组件和站点系统角色的操作对业务运营的影响最小。 有关详细信息，请参阅 [ System Center Configuration Manager 的更新](/sccm/core/servers/manage/updates)。



<!--HONumber=Dec16_HO3-->


