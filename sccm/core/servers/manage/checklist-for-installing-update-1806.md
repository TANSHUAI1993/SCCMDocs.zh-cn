---
title: 1806 清单
titleSuffix: Configuration Manager
description: 了解更新到 Configuration Manager 1806 版之前需要执行的操作。
ms.date: 08/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb0a87a6-fd65-440b-90a5-2fef35622c9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d8d681dbd9996fb7eddbc2b37cf6af6a32401560
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65497575"
---
# <a name="checklist-for-installing-update-1806-for-configuration-manager"></a>用于为 Configuration Manager 安装更新 1806 的清单

适用范围：System Center Configuration Manager (Current Branch)

使用 Configuration Manager 的 Current Branch 时，可安装版本为 1806 的控制台内部更新，从之前的版本更新层次结构。 <!-- baseline only statement: (Because version 1802 is also available as [baseline media](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions), you can use the installation media to install the first site of a new hierarchy.)-->

要获取版本 1806 的更新，必须在层次结构的顶级站点上使用服务连接点。 站点系统角色可处于任一模式（联机或脱机）。 层次结构从 Microsoft 下载更新包之后，可在控制台中找到它。 在“管理”工作区中，选择“更新和维护服务”节点。

-   当更新列为“可用”时，此更新即可准备安装。 安装版本 1806 之前，请查看以下[关于安装更新 1806](#about-installing-update-1806) 和[清单](#checklist)的信息，了解在开始更新之前要进行的配置。

-   如果更新显示为“正在下载”且未更改，请查看 hman.log 和 dmpdownloader.log 是否有误。

    -   dmpdownloader.log 可能指示 dmpdownloader 进程要等待一段时间之后才检查更新。 若要重启更新的重分发文件的下载，请在站点服务器上重启 SMS_Executive 服务。

    -   当代理服务器设置阻止从 http://silverlight.dlservice.microsoft.com 和 http://download.microsoft.com 下载时，会出现另一个常见下载问题。

有关安装更新的详细信息，请参阅[控制台内部的更新和维护服务](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing)。

有关 Current Branch 版本的详细信息，请参阅[基线和更新版本](/sccm/core/servers/manage/updates#bkmk_Baselines)。



## <a name="about-installing-update-1806"></a>关于安装更新 1806

#### <a name="sites"></a>站点
在层次结构的顶级站点上安装更新 1806。 从管理中心站点或从独立主站点启动安装。 在顶级站点安装更新后，子站点具有以下更新行为：

-   管理中心站点完成更新安装之后，子主站点会自动安装更新。 可以使用服务时段控制站点安装更新的时间。 有关详细信息，请参阅[站点服务器的服务时段](/sccm/core/servers/manage/service-windows)。

-   在主父站点完成更新安装之后，从 Configuration Manager 控制台中手动更新每个辅助站点。 不支持辅助站点服务器的自动更新。

#### <a name="site-system-roles"></a>站点系统角色
站点服务器安装更新时，会自动更新所有站点系统角色。 这些角色处于站点服务器上或安装在远程服务器上。 安装更新之前，请确保每个站点系统服务器满足新更新版本的当前先决条件。

#### <a name="configuration-manager-consoles"></a>Configuration Manager 控制台   
更新完成后首次使用 Configuration Manager 控制台时，系统会提示更新该控制台。 还可以在托管该控制台的计算机上运行 Configuration Manager 安装程序，并选择用于更新该控制台的选项。 请尽快将更新安装到控制台。 有关详细信息，请参阅[安装 Configuration Manager 控制台](/sccm/core/servers/deploy/install/install-consoles)。

> [!IMPORTANT]  
> 在管理中心站点上安装更新时，应注意以下限制和延迟存在，直到所有子主站点也完成了更新安装：    
> - **客户端升级**不会启动。 这包括客户端和预生产客户端的自动更新。 此外，不能将预生产客户端提升至生产，直到最后一个站点完成更新安装。 最后一个站点完成更新安装后，客户端升级将根据你的配置选择启动。   
> - 更新启用的**新功能**将不可用。 这是为了防止将与该功能有关的数据的复制发送到尚未安装针对该功能的支持的站点。 所有主站点安装更新后，此功能将可供使用。   
> - 管理中心站点和子主站点之间的**复制链接**显示为未升级。 这会在更新包安装状态中显示为“完成”状态，并带有监视复制初始化的警告。 在控制台的监视节点中，这将显示为*正在配置链接*。


## <a name="checklist"></a>清单

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>所有站点都运行 Configuration Manager 的支持版本  
层次结构中的每个站点服务器都必须运行相同的 Configuration Manager 版本，然后才能开始安装更新 1806。 若要更新到 1806，必须使用版本 1706、1710 或 1802。

#### <a name="review-the-status-of-your-product-licensing"></a>查看产品许可的状态 
必须拥有有效的软件保障 (SA) 协议或等效的订阅权利才能安装此更新。 更新站点时，“许可”页将出现确认“软件保障到期日期”的选项。

此值是可选的。 可将其指定为许可证到期日期的方便提示。 该日期在安装未来更新时可见。 你可能已在先前设置或安装更新期间指定了此值。 也可以在 Configuration Manager 控制台中指定此值。 在“管理”工作区中，展开“站点配置”，并选择“站点”。 单击功能区中的“层次结构设置”，并切换到“许可”选项卡。

有关详细信息，请参阅[许可和分支](/sccm/core/understand/learn-more-editions)。

#### <a name="review-microsoft-net-versions"></a>查看 Microsoft.NET 版本 
在站点安装此更新时，Configuration Manager 将自动安装.NET Framework 4.5.2。 如果尚未安装此必备组件，站点会将其安装在托管以下站点系统角色之一的每个服务器上：

-   管理点
-   服务连接点
-   注册代理点
-   注册点

此安装可以将站点系统服务器置于重启挂起状态，并向 Configuration Manager 组件状态查看器报告错误。 此外，服务器上的 .NET 应用程序可能会遇到随机故障，直到重启服务器。

有关详细信息，请参阅 [站点和站点系统先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>查看适用于 Windows 10 的 Windows ADK 版本
Windows 10 评估和部署工具包 (ADK) 的版本应受到 Configuration Manager 版本 1806 的支持。 有关受支持的 Windows ADK 版本的详细信息，请参阅 [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)。 如果需要更新 Windows ADK，请在开始更新 Configuration Manager 前进行此操作。 该顺序可确保默认启动映像自动更新为最新版本的 Windows PE。 更新站点后手动更新任何自定义启动映像。

如果先更新站点，再更新 Windows ADK，请参阅[利用启动映像更新分发点](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)。

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>查看站点和层次结构状态以寻找未解决的问题 
更新站点之前，请解决远程计算机上安装的站点服务器、站点数据库服务器和站点系统角色的所有操作问题。 由于现有的操作问题，站点更新可能会失败。

有关详细信息，请参阅 [使用警报和状态系统](/sccm/core/servers/manage/use-alerts-and-the-status-system)。

#### <a name="review-file-and-data-replication-between-sites"></a>查看站点之间的文件和数据复制   
确保站点之间的文件和数据库复制正常运行并且处于最新状态。 延迟或积压工作可能会阻止顺利、成功更新。 对于数据库复制，可以在开始更新之前，使用复制链接分析器来帮助解决问题。

有关详细信息，请参阅[关于复制链接分析器](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)。

#### <a name="install-all-applicable-critical-windows-updates"></a>安装所有适用的关键 Windows 更新
为 Configuration Manager 安装更新之前，为每个适用的站点系统安装任何关键的 OS 更新。 这些服务器包括站点服务器、站点数据库服务器和远程站点系统角色。 如果安装的更新需要重启，请在开始升级之前重启相应的服务器。

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>在主站点上禁用管理点的数据库副本   
Configuration Manager 无法成功更新启用了管理点数据库副本的主站点。 为 Configuration Manager 安装更新之前，禁用数据库复制。

有关详细信息，请参阅[管理点的数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)。

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>将 SQL Server AlwaysOn 可用性组设置为手动故障转移   
如果使用可用性组，请确保在开始安装更新之前将可用性组设置为手动故障转移。 站点更新后，可以将故障转移还原为自动进行。 有关详细信息，请参阅 [站点数据库的 SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>禁用每个站点的站点维护任务
在安装更新之前，请禁用可能会在更新过程进行时运行的任何站点维护任务。 例如，但不限于：

-   备份站点服务器
-   删除过期的客户端操作
-   删除过期的发现数据

站点数据库维护任务在更新安装过程中运行时，更新安装可能会失败。 在禁用任务之前，请记录该任务的计划，以便在安装更新之后可恢复其配置。

有关详细信息，请参阅 [维护任务](/sccm/core/servers/manage/maintenance-tasks) 和[维护任务参考](/sccm/core/servers/manage/reference-for-maintenance-tasks)。

#### <a name="temporarily-stop-any-antivirus-software"></a>暂时停止任何防病毒软件 
更新站点之前，停止 Configuration Manager 服务器上的防病毒软件。 <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>创建站点数据库的备份 
更新站点之前，在管理中心站点和主站点上备份站点数据库。 此备份可确保你具有可用于灾难恢复的成功备份。

有关详细信息，请参阅 [备份和恢复](/sccm/protect/understand/backup-and-recovery)。

#### <a name="plan-for-client-piloting"></a>规划客户端试点   
安装更新客户端的更新后，可以在新的客户端更新部署和升级所有活动的客户端之前在预生产中对其进行测试。 若要利用此选项，在开始安装更新之前必须配置站点，以支持预生产的自动升级。

有关详细信息，请参阅 [升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients) 和[如何在预生产集合中测试客户端升级](/sccm/core/clients/manage/upgrade/test-client-upgrades)。

#### <a name="plan-to-use-service-windows"></a>计划使用服务时段   
若要定义可向站点服务器安装更新的时间段，请使用服务时段。 它们可以帮助控制层次结构中的站点安装更新的时间。 有关详细信息，请参阅 [站点服务器的服务时段](/sccm/core/servers/manage/service-windows)。

#### <a name="review-supported-extensions"></a>查看支持的扩展
<!--SCCMdocs#587-->
如果使用 Microsoft 或 Microsoft 合作伙伴的其他产品来扩展 Configuration Manager，请确认这些产品是否支持版本 1806。 检查产品供应商的此项信息。 例如，请查看 Microsoft Deployment Toolkit 的[发行说明](/sccm/mdt/release-notes)。

#### <a name="run-the-setup-prerequisite-checker"></a>运行安装程序先决条件检查程序   
当更新在控制台中列为“可用”时，可以独立运行先决条件检查程序，然后再安装更新。 （在站点上安装更新时，会再次运行必备组件检查程序。）

若要从控制台运行先决条件检查，请转到“管理”工作区，并选择“更新和服务”。 选择 Configuration Manager 1806 更新包，然后在功能区单击“运行先决条件检查”。

有关详细信息，请参阅[安装控制台内部更新前](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)中的“安装更新之前运行先决条件检查程序”部分。

> [!IMPORTANT]  
> 运行先决条件检查程序时，该过程会更新某些用于站点维护任务的产品源文件。 因此，在运行先决条件检查程序之后但在安装更新之前，如果需要执行站点维护任务，可从站点服务器上的 CD.Latest 文件夹运行  **Setupwpf.exe** （Configuration Manager 安装程序）。

#### <a name="update-sites"></a>更新站点   
现已准备好为层次结构开始更新安装。 有关安装更新的详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)。

你有可能计划在常规工作时间外安装更新。 确定过程将对业务操作造成最小影响的时间。 安装更新及其操作会重新安装站点组件和站点系统角色。

有关详细信息，请参阅  [Configuration Manager 更新](/sccm/core/servers/manage/updates)。



## <a name="post-update-checklist"></a>更新后的清单

更新站点后，使用以下清单可完成常见任务和配置。


#### <a name="confirm-version-and-restart-if-necessary"></a>确认版本并重启（如有必要）
确保每个站点服务器和站点系统角色都已更新为版本 1806。 在控制台的“管理”工作区中，将“版本”列添加到“站点”和“分发点”节点。 如有必要，站点系统角色将自动重新安装以更新到新的版本。 

请考虑重新启动初次未成功更新的远程站点系统。 查看站点基础结构，确保适用的站点服务器和远程站点系统服务器已成功重启。 通常，仅当 Configuration Manager 安装 .NET 作为站点系统角色的先决条件时，站点服务器才重新启动。


#### <a name="confirm-site-to-site-replication-is-active"></a>确认站点到站点复制处于活动状态
在 Configuration Manager 控制台中，转到以下位置以查看状态并确保复制处于活动状态：  

-   “监视”工作区、“站点层次结构”节点  

-   “监视”工作区、“数据库复制”节点  

有关详细信息，请参阅下列文章：  
- [监视层次结构和复制基础结构](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)
- [关于复制链接分析器](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>更新 Configuration Manager 控制台
将所有远程 Configuration Manager 控制台更新为相同版本。 系统会在以下情况下提示你更新控制台：  

-   打开控制台。  

-   在控制台中转到新节点。  


#### <a name="reconfigure-database-replicas-for-management-points"></a>重新配置管理点的数据库副本
更新主站点之后，为在站点更新之前卸载的管理点重新配置数据库副本。 有关详细信息，请参阅[管理点的数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)。  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>重新配置已禁用的所有维护任务
如果安装更新之前在站点上禁用了数据库[维护任务](/sccm/core/servers/manage/maintenance-tasks)，请重新配置这些任务。 使用更新之前就已经存在的相同设置。  


#### <a name="update-clients"></a>更新客户端
如果在安装更新前已配置客户端试点，请按照你创建的计划更新客户端。 有关详细信息，请参阅[如何升级 Windows 计算机的客户端](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers)。  


#### <a name="third-party-extensions"></a>第三方扩展
如果使用任何 Configuration Manager 的扩展，请将其更新为最新版本，以支持 Configuration Manager 版本 1806。 


#### <a name="update-custom-boot-images-and-media"></a>更新自定义启动映像和媒体
<!--SCCMDocs issue 775-->

对使用的任何启动映像使用更新分发点操作，无论是默认启动映像还是自定义启动映像均是如此。 此操作可确保客户端能够使用最新版本。 即使没有新的 Windows ADK 版本，Configuration Manager 客户端组件也可能随更新而更改。 如果未更新启动映像和媒体，设备上的任务序列部署可能会失败。 

更新站点时，Configuration Manager 会自动更新默认启动映像。 它不会将更新的内容自动分发到分发点。 准备好在网络中分发此内容时，请对特定启动映像使用更新分发点操作。 

更新站点后，手动更新任何自定义 启动映像。 如有必要，此操作将使用最新的客户端组件更新启动映像，可选择使用当前的 Windows PE 版本重载它，并将内容重新分发到分发点。 

有关详细信息，请参阅[使用启动映像更新分发点](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)。 
