---
title: "升级到 System Center Configuration Manager | Microsoft Docs"
description: "了解从运行 System Center 2012 Configuration Manager 的站点和层次结构成功进行就地升级的步骤。"
ms.custom: na
ms.date: 6/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
caps.latest.revision: "21"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1166b739e1e8d667172d97883f484fdbc3a142c1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-to-system-center-configuration-manager"></a>升级到 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

可以运行就地升级，以从运行 System Center 2012 Configuration Manager 的站点和层次结构升级到 System Center Configuration Manager。  

 在从 System Center 2012 Configuration Manager 升级之前，必须准备站点，需要删除可能会阻止成功升级的特定配置，然后在涉及多个站点时需要按照升级顺序操作。  

 > [!TIP]
 > 管理 System Center Configuration Manager 站点和层次结构基础结构时，术语“升级”“更新”和“安装”用于描述三种不同概念。 若要了解每个术语的使用方法，请参阅[有关升级、更新和安装](/sccm/core/understand/upgrade-update-install)。

##  <a name="bkmk_path"></a> 就地升级路径  

**升级到版本 1702**   
如果具有版本 1702 基线介质，可以将下列版本升级到 System Center Configuration Manager 版本 1702 的完整许可版本：   
-     System Center Configuration Manager 版本 1702 的评估版安装
-     System Center 2012 Configuration Manager Service Pack 1
-     System Center 2012 Configuration Manager Service Pack 2
-     System Center 2012 R2 Configuration Manager
-     System Center 2012 R2 Configuration Manager Service Pack 1

**升级到 1606 版本**  
2016 年 12 月 15 日，为添加对其他升级方案的支持，已发布版本 1606 的基线媒体。 此新版本支持将以下版本升级到 System Center Configuration Manager 版本 1606 的完整许可版本：  
-   System Center Configuration Manager 版本 1606 的评估版安装
-   System Center Configuration Manager 的候选发布版安装  
-   System Center 2012 Configuration Manager Service Pack 1  
-   System Center 2012 Configuration Manager Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager Service Pack 1  

如果使用 2016 年 12 月 15 日之前下载的 1606 版基线媒体，可以仅将以下版本升级到 System Center Configuration Manager 版本 1606 的完整许可版本：
-   System Center Configuration Manager 版本 1606 的评估版安装
-   System Center 2012 Configuration Manager Service Pack 2
-   System Center 2012 R2 Configuration Manager Service Pack 1

<!-- Version 1511 has now dropped out of support
**Upgrade to version 1511**  
When you have version 1511 baseline media, you can upgrade the following to a fully licensed  version of System Center Configuration Manager version 1511:  
-   An evaluation install of System Center Configuration Manager version 1511
-   A release candidate install of System Center Configuration Manager  
-   System Center 2012 Configuration Manager with Service Pack 1  
-   System Center 2012 Configuration Manager with Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager with Service Pack 1  
-->


> [!TIP]  
>  从 System Center 2012 Configuration Manager 版本升级到 Current Branch 时，或许能够简化升级过程。 有关详细信息，请参阅以下内容：  
>   
>  -   [System Center Configuration Manager 更新](../../../../core/servers/manage/updates.md)中的[基准和更新版本](../../../../core/servers/manage/updates.md#bkmk_Baselines)  
>  -   [System Center Configuration Manager 的 CD.Latest 文件夹](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **不支持以下项目：**  
-   不支持将 Technical Preview for System Center Configuration Manager 升级为完整许可版安装。  Technical Preview 版本只能升级到更高版本的 Technical Preview。  

-   不支持从 Technical Preview 迁移到完整许可版本。  

##  <a name="bkmk_checklist"></a> 升级清单  
 下列清单可帮助计划成功升级到 System Center Configuration Manager。  

### <a name="before-you-upgrade"></a>升级准备工作  

**检查 System Center 2012 Configuration Manager 环境**并按照 KB4018655：[由于反复重试任务 Configuration Manager 客户端每五个小时重新安装一次并可能导致客户端意外升级](https://support.microsoft.com/help/4018655)中详细介绍的方式解决问题。

**确保计算机环境符合升级到 System Center Configuration Manager 所需的支持配置**：  

查看正在用于承载站点系统角色的服务器操作系统：  

-   System Center 2012 Configuration Manager 支持的某些较旧操作系统不受 System Center Configuration Manager 支持，必须重定位或删除这些操作系统上的站点系统角色，然后才进行升级。 请参阅[站点系统服务器支持的操作系统](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)文档。   
-   Configuration Manager 的先决条件检查程序不在站点服务器或远程站点系统上验证站点系统角色的先决条件  

查看承载站点系统角色的每台计算机所需的先决条件组件：  

-   例如，为部署操作系统，System Center Configuration Manager 使用 Windows 10 评估和部署工具包 (Windows ADK)。 运行安装程序之前，必须在站点服务器以及运行 SMS 提供程序实例的每台计算机上下载和安装 Windows 10 ADK。  

有关支持的平台和先决条件配置的一般信息，请参阅 [Supported configurations for System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)。  

有关将 Windows ADK 与 Configuration Manager 搭配使用的信息，请参阅 [System Center Configuration Manager 中的操作系统部署的基础结构要求](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

**查看站点和层次结构状态，并确认没有未解决的问题：**  
升级站点之前，请解决远程计算机上安装的站点服务器、站点数据库服务器和站点系统角色的所有操作问题。 由于现有的操作问题，站点升级可能会失败。  

**为承载站点、站点数据库服务器和远程站点系统角色的计算机上的操作系统，安装所有合适的关键更新：**  
升级站点之前，请为每个合适的站点系统安装任何关键更新。 如果安装的更新需要重启，请在启动 Service Pack 更新之前重启合适的计算机。  

有关详细信息，请参阅 [Windows 更新](http://go.microsoft.com/fwlink/p/?LinkId=105851)。  

**卸载 System Center Configuration Manager 不支持的站点系统角色：**  
以下站点系统角色不再用于 System Center Configuration Manager，必须先将其卸载，然后再从 System Center 2012 Configuration Manager 进行升级：  

-   带外管理点  
-   系统健康验证程序点  

**在主站点上禁用管理点数据库副本：**  
Configuration Manager 无法成功升级启用了管理点数据库副本的主站点。 禁用数据库复制，然后：  

-   创建站点数据库的备份以测试数据库升级  
-   将生产站点升级到 System Center Configuration Manager  

有关详细信息，请参阅以下内容：  
-   System Center 2012 Configuration Manager：[配置管理点的数据库副本](https://technet.microsoft.com/library/hh846234.aspx)  
-   System Center Configuration Manager：[System Center Configuration Manager 管理点的数据库副本](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

**重新配置使用 NLB 的软件更新点：**  
Configuration Manager 无法升级使用网络负载平衡 (NLB) 群集来承载软件更新点的站点。  

如果为软件更新点使用 NLB 群集，请使用 PowerShell 删除 NLB 群集。 （从 System Center 2012 Configuration Manager SP1 开始，Configuration Manager 控制台中不再有配置 NLB 群集的选项）  

**在该站点的升级过程中，禁用每个站点上的所有站点维护任务：**  
在升级到 System Center Configuration Manager 之前，请禁用可能会在升级过程进行时运行的任何站点维护任务。 这包括但不限于以下各项：  

-   备份站点服务器  
-   删除过期的客户端操作  
-   删除过期的发现数据  

如果站点数据库维护任务在升级过程中运行，站点升级可能会失败。  

在禁用任务之前，请记录该任务的计划，以便能够在站点升级完成后恢复其配置。  

有关站点维护任务的详细信息，请参阅：  

-   System Center 2012 Configuration Manager：[规划 Configuration Manager 的维护任务](https://technet.microsoft.com/library/gg712686.aspx)  
-   System Center Configuration Manager：[System Center Configuration Manager 维护任务参考](../../../../core/servers/manage/reference-for-maintenance-tasks.md)  

**运行安装程序先决条件检查程序**：  
升级站点之前，可以独立于安装程序运行 **先决条件检查程序** ，以验证站点是否满足先决条件 稍后升级该站点时会再次运行必备组件检查程序。  

如果使用 2016 年 10 月发行的 1606 版基线媒体，独立的必备组件检查会对要升级到 System Center Configuration Manage 的 Current Branch 和 Long-Term Servicing Branch (LTSB) 的站点进行评估。 由于 LTSB 不支持某些功能，在 ConfigMgrPrereq.log 中可能会看到以下类似条目：
 - 信息：该站点为 LTSB 版本。
 - LTSB 版本不支持的站点系统角色“资产智能同步点”；    错误；    Configuration Manager 已检测到“资产智能同步点”已安装。 LTSB 版本不支持资产智能。 必须卸载资产智能同步点站点系统角色才能继续操作。

如果计划升级到 Current Branch，可以安全地忽略 LTSB 版本中的错误。 如果计划升级到 LTSB 才适用。

稍后运行 Configuration Manager 安装程序进行升级时，将再次运行必备组件检查并评估基于选择安装的 System Center Configuration Manager 分支（Current Branch 或 LTSB）的站点。 如果选择升级到 Current Branch，则不会检查 LTSB 不支持的功能。

有关详细信息，请参阅[必备组件检查程序](/sccm/core/servers/deploy/install/prerequisite-checker)和 [System Center Configuration Manager 的必备组件检查列表](/sccm/core/servers/deploy/install/list-of-prerequisite-checks)。  

**下载 System Center Configuration Manager 的必备组件文件和可再发行文件：**    
使用**安装程序下载程序**下载用于 System Center Configuration Manager 的先决条件可再发行文件、语言包以及最新产品更新。  

有关信息，请参阅[安装程序下载程序](/sccm/core/servers/deploy/install/setup-downloader)。  

**计划管理服务器和客户端语言**：  
当站点升级时，站点升级仅安装在升级过程中选择的语言包版本。  

-   安装程序查看站点的当前语言配置，然后确定存储以前下载的先决条件文件的文件夹中可用的语言包。  
-   然后，你可以确认选择的当前服务器和客户端语言包，或者更改选择以添加或删除语言支持。  
-   仅可以选择在运行安装程序（可以使用下载的先决条件文件获取）时可用的语言包。  

> [!NOTE]  
>  不能使用 System Center 2012 Configuration Manager 的语言包为 System Center Configuration Manager 站点启用语言。  

有关语言包的详细信息，请参阅 [System Center Configuration Manager 中的语言包](../../../../core/servers/deploy/install/language-packs.md)。  

**查看站点升级考虑事项**：  
升级站点时，某些功能和配置会重置为默认配置。 若要帮助你准备这些更改以及相关更改，请查看  [升级注意事项](#bkmk_considerations)中的信息。  

**在管理中心站点和主站点上创建站点数据库备份：**  
升级站点之前，请备份站点数据库，以确保具有用于灾难恢复的成功备份。  

请参阅 [System Center Configuration Manager 的备份和恢复](../../../../protect/understand/backup-and-recovery.md)。  

**备份自定义 Configuration.mof 文件**：  
如果使用自定义 Configuration.mof 文件定义与硬件清单一起使用的数据类，则在升级站点之前创建此文件的备份。 随后在进行升级之后，将此文件还原到你的站点。 有关使用此文件的详细信息，请参阅[如何在 System Center Configuration Manager 中扩展硬件清单](../../../../core/clients/manage/inventory/extend-hardware-inventory.md)。  

**在最近的站点数据库备份副本上测试数据库升级过程：**  
在升级 Configuration Manager 管理中心站点或主站点之前，请对站点数据库的副本测试站点数据库升级过程。  

-   你应该测试站点数据库升级过程，因为当你升级站点时，可能会修改站点数据库  
-   虽然测试数据库升级不是必需的，但可以在生产数据库受到影响之前先行确定升级的问题  
-   失败的站点数据库升级可能会使站点数据库无法运行，并且可能需要进行站点恢复以还原功能  
-   虽然在层次结构的站点之间共享了站点数据库，但是，请在升级每个合适的站点之前计划在该站点上测试数据库  
-   如果在主站点上对管理点使用数据库副本，请在创建站点数据库备份之前禁用复制  

Configuration Manager 不支持辅助站点备份，也不支持辅助站点数据库的测试升级。  

不支持在生产站点数据库上运行测试数据库升级。 执行此操作会升级站点数据库，并可能导致你的站点无法运行。  

有关详细信息，请参阅 [测试站点数据库升级](#bkmk_test)。  

**重启站点服务器和承载站点系统角色的每台计算机**：  
这样可以确保更新的最近安装或必备组件中没有任何挂起的操作，并且这是公司特定的内部流程。  

**升级站点**：  
从层次结构的顶层站点开始，运行 System Center Configuration Manager 源媒体中的 Setup.exe。  

在顶层站点升级之后，你可以开始升级每个子站点。 请先完成每个站点的升级，然后开始升级下一个站点  

在层次结构中的所有站点均升级到 System Center Configuration Manager 之前，层次结构会在混合版本模式下运行。  

有关如何运行升级的信息，请参阅[升级站点](#bkmk_upgrade)。  

### <a name="after-you-upgrade"></a>升级后续工作  
**升级独立的 Configuration Manager 控制台**：  
默认情况下，升级管理中心站点或主站点时，安装过程也会升级站点服务器上安装的 Configuration Manager 控制台。 但是，你必须手动升级安装在非站点服务器计算机上的每个控制台。  

> [!TIP]  
>  在开始升级之前，关闭每个打开的控制台。  

有关详细信息，请参阅[安装 System Center Configuration Manager 控制台](../../../../core/servers/deploy/install/install-consoles.md)。  

**为主站点中的管理点重新配置数据库副本：**  
如果将数据库副本用于主站点中的管理点，则必须先卸载数据库副本，再升级站点。 升级主站点之后，为管理点重新配置数据库副本。   
有关详细信息，请参阅  [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

**重新配置在升级前禁用的任何数据库维护任务：**  
如果升级之前在站点上禁用了数据库 [System Center Configuration Manager 维护任务的引用](../../../../core/servers/manage/reference-for-maintenance-tasks.md)，请使用与升级之前存在的相同设置在站点上重新配置这些任务。  

**升级客户端**：  
所有站点都升级到 System Center Configuration Manager 后，可计划升级客户端。  

升级客户端时，会卸载当前的客户端软件，然后安装新的客户端软件版本。 可以使用 Configuration Manager 支持的任何方法来升级客户端。  

> [!TIP]  
>  在升级层次结构的顶层站点时，也会更新层次结构中的每个分发点上的客户端安装包。 升级主站点时，会更新该主站点提供的客户端升级包。  

有关如何升级现有客户端和如何安装新客户端的信息，请参阅[如何在 System Center Configuration Manager 中升级 Windows 计算机的客户端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

##  <a name="bkmk_considerations"></a> 升级注意事项  
**自动操作**：  
升级到 System Center Configuration Manager 时，会自动执行下列操作：  

-   站点执行站点重置，这包括重新安装所有站点系统角色。  
-   如果站点是层次结构的顶层站点，则会更新层次结构中的每个分发点上的客户端安装包。 站点还会更新默认启动映像以使用附带 Windows 评估和部署工具包 10 的新 Windows PE 版本。 但是，升级不会升级现有媒体以用于映像部署。  
-   如果站点是主站点，则会更新该站点的客户端升级包。  

**管理用户在升级后手动执行的操作**   
升级站点后，确保执行下列操作：  

-   确保分配到每个主站点的客户端都升级和安装适用于新版本的客户端软件  
-   升级连接到站点以及在远离站点服务器的计算机上运行的每个 Configuration Manager 控制台  
-   在将数据库副本用于管理点的主站点中，重新配置数据库副本  
-   站点升级后，你必须手动升级 CD 和 DVD 或 U 盘的物理媒体（如 ISO 文件），或手动升级用于 Windows To Go 部署或提供给硬件供应商的预留媒体。 虽然站点升级可更新默认启动映像，但它不能升级在 Configuration Manager 以外使用的这些媒体文件或设备  
-   计划在不需要原始（较旧）版本的 Windows PE 时更新非默认启动映像。  

**影响配置和设置的操作**   
站点升级到 System Center Configuration Manager 时，某些配置和设置在升级后将不复存在，或者被设置为新的默认配置。 下表是不再存在或有所改变的设置，并提供详细信息来帮助你在站点升级过程中为它们做好规划：  

-   **软件中心：**  
    下列软件中心项目被重置为它们的默认值：  
    -   “工作信息” 被重置为周一到周五从凌晨 5:00  到晚上 10:00  Monday 到晚上 10:00 Friday.  
    -   “计算机维护”  的值被设置为“当我的计算机处于演示模式时暂停软件中心活动” 。  
    -   “远程控制”  的值被设置为分配到计算机的客户端设置中的值。  
-   **软件更新摘要计划：**  
     软件更新或软件更新组的自定义摘要计划被重置为默认值（1 小时）。 升级完成后，请将自定义摘要值重置为所需的频率。  

##  <a name="bkmk_test"></a> 测试站点数据库升级  
以下信息仅适用于将先前版本（如 System Center 2012 Configuration Manager）升级到 System Center Configuration Manager。

在升级站点之前，请针对升级测试该站点的数据库副本。  

若要针对升级测试数据库，请首先将站点数据库的副本还原到未承载 Configuration Manager 站点的 SQL Server 实例。 用于承载数据库副本的 SQL Server 版本必须是作为数据库副本源的 Configuration Manager 版本支持的 SQL Server 版本。  

接下来，在还原站点数据库之后，在 SQL Server 计算机上，使用  **/TESTDBUPGRADE**  命令行选项从 System Center Configuration Manager 的源媒体文件夹中运行 Configuration Manager 安装程序。  

-   有关如何创建和还原站点数据库备份的信息，请参阅[适用于安装程序的命令行选项](../../../../core/servers/deploy/install/command-line-options-for-setup.md)。  
-   有关 **/TESTDBUPGRADE** 命令行选项的信息，请参阅[适用于安装程序的命令行选项](../../../../core/servers/deploy/install/command-line-options-for-setup.md) 中的表。  
-   有关支持的 SQL Server 版本的信息，请参阅[对 System Center Configuration Manager 的 SQL Server 版本的支持](../../../../core/plan-design/configs/support-for-sql-server-versions.md)主题。  

> [!TIP]  
>  如果将 Microsoft Intune 与 Configuration Manager 集成：  
>   
>  当你对已有 5 天或超过 5 天的站点数据库副本运行测试数据库升级时，可能会收到以下其中一条消息：  
>   
>  -   警告：升级将强制完全同步到云。  
>  -   错误：数据库升级将强制完全同步到云。  
>   
> 这两种情况都可以在测试数据库升级的过程中被安全地忽略，因为它们并未指明测试升级失败或出现问题。 相反，它们会指出在实际升级期间，来自**云**数据库复制组的数据可能会与 Microsoft Intune 同步。  

在计划升级的每个管理中心站点和主站点上使用下列过程。  

#### <a name="to-test-a-site-database-for-upgrade"></a>若要测试站点数据库进行升级  

1.  建立站点数据库的副本，然后将该副本还原到 SQL Server 的实例，该实例使用与站点数据库相同的版本，并且未承载 Configuration Manager 站点。 例如，站点数据库运行在 SQL Server 的 Enterprise Edition 实例上，请确保将数据库还原到也运行 SQL Server Enterprise Edition 的 SQL Server 实例。  

2.  还原数据库副本之后，请从 System Center Configuration Manager 的源媒体中运行安装程序。 运行安装程序时，使用 **/TESTDBUPGRADE** 命令行选项。 如果承载数据库副本的 SQL Server 实例不是默认实例，你还必须提供命令行参数以确定承载站点数据库副本的实例。  

     例如，你计划升级数据库名称为 SMS_ABC 的站点数据库。 你将此站点数据库的副本还原到实例名称为 DBTest 的受支持 SQL Server 实例。 要测试站点数据库的此副本的升级，请使用下列命令行： **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     可以在 System Center Configuration Manager 的源媒体上的下列位置中找到 Setup.exe：**SMSSETUP\BIN\X64**。  

3.  在运行数据库升级测试的 SQL Server 实例上，监视系统驱动器根目录中的 ConfigMgrSetup.log 以了解进度和成功情况。  

    -   如果测试升级失败，请解决与站点数据库升级失败相关的任何问题，创建站点数据库的新备份，然后测试站点数据库的新副本的升级。  
    -   过程成功完成后，你可以删除该数据库副本。  

        > [!NOTE]  
        >  不支持还原用于测试升级的站点数据库的副本以用作任何站点上的站点数据库。  

成功升级站点数据库的副本后，请继续执行 Configuration Manager 站点及其站点数据库的升级。  

##  <a name="bkmk_upgrade"></a> 升级站点  
完成站点的升级前配置、测试了数据库副本上站点数据库的升级，并下载了计划安装的 Service Pack 版本的先决条件文件和语言包后，即已准备好升级 Configuration Manager 站点。  

在升级层次结构中的站点时，将会先升级层次结构的顶层站点。 此顶层站点是管理中心站点或独立主站点。 管理中心站点的升级完成后，你可以按任何所需顺序升级子主站点。 升级主站点之后，可以升级该站点的子辅助站点，或在升级任何辅助站点之前升级其他主站点。  

若要升级管理中心站点或主站点，请从 System Center Configuration Manager 源媒体中运行安装程序。 但是，不要运行该安装程序来升级辅助站点。 相反，请使用 Configuration Manager 控制台在完成辅助站点的主父站点的升级之后升级该辅助站点。  

在升级站点之前，请关闭站点服务器上安装的 Configuration Manager 控制台，直至站点升级完成。 还要关闭在站点服务器以外的计算机上运行的每个 Configuration Manager 控制台。 站点升级完成后，你可以重新连接控制台。 但是，在将 Configuration Manager 控制台升级到其新版本之前，该控制台无法显示 Configuration Manager 新版本中提供的某些对象和信息。  

使用以下过程升级 Configuration Manager 站点：  

#### <a name="to-upgrade-a-central-administration-site-or-primary-site"></a>升级管理中心站点或主站点  

1.  验证运行安装程序的用户是否具有以下安全权限：  

    -   站点服务器计算机上的本地管理员权限。  
    -   站点（如果为远程）的远程站点数据库服务器上的本地管理员权限。    </br></br>

2.  在站点服务器计算机上，打开 Windows 资源管理器，并浏览到 **&lt;ConfigMgSourceMedia\>\SMSSETUP\BIN\X64**。  

3.  双击 **Setup.exe**。 Configuration Manager 安装向导将打开。  

4.  在“开始之前”  页面上，单击“下一步” 。  

5.  在“入门”  页上，选择“升级此 Configuration Manager 站点” ，然后单击“下一步” 。  

6.  在“产品密钥”  页上，单击“下一步” 。  

     如果以前安装了 Configuration Manager 评估版，则可以选择“安装此产品的许可版本”，然后输入 Configuration Manager 的完整安装产品密钥以将站点转换为完整版。  

     从 2016 年 10 月发布的 System Center Configuration Manager 的 1606 版基线介质开始，可以指定软件保障协议的到期日期。 还可以选择指定许可协议的**软件保障到期日期**，方便向你提醒该日期。 如果在设置期间未输入此信息，则可以稍后在 Configuration Manager 控制台中指定。

     >  [!NOTE]   
     >  Microsoft 不会验证输入的到期日期，且不会将此日期用作许可证验证。  相反，可以使用该日期作为到期日期提醒。 这很有用，因为 Configuration Manager 定期检查在线提供的新软件更新，而软件保障许可证应为最新状态，以便有资格使用这些额外的更新。    

     有关详细信息，请参阅 [System Center Configuration Manager 的许可和分支](/sccm/core/understand/learn-more-editions)。

7.  在“Microsoft 软件许可条款”  页上，阅读并接受许可条款，然后单击“下一步” 。  

8.  在“先决条件许可证”  页上，阅读并接受必备软件的许可条款，然后单击“下一步” 。 安装程序将在需要软件时下载该软件并将其自动安装在站点系统或客户端上。 你必须选中所有复选框，然后才能继续进入下一页。  

9. 在“先决条件下载”  页上，指定安装程序是从 Internet 下载最新的必备软件可再发行文件、语言包和最新的产品更新还是使用以前下载的文件，然后单击“下一步” 。 如果以前通过使用安装程序下载程序下载了文件，请选择“使用以前下载的文件”  并指定下载文件夹。 有关详细信息，请参阅[安装程序下载程序](/sccm/core/servers/deploy/install/setup-downloader)。

    > [!NOTE]  
    >  在使用以前下载的文件时，请验证下载文件夹的路径是否包含文件的最新版本。  

10. 在“服务器语言选择”  页上，查看当前为站点安装的语言的列表。 为 Configuration Manager 控制台和报表选择此站点上可用的其他语言，或清除不再希望在此站点上支持的语言，然后单击“下一步”。 默认情况下，“英语”处于选定状态，并且无法删除。  

    > [!IMPORTANT]  
    >  每个版本的 Configuration Manager 都不能使用其之前版本的 Configuration Manager 的语言包。 若要启用对所升级的 Configuration Manager 站点上的某种语言的支持，必须使用该新版本的语言包版本。 例如，在从 System Center 2012 Configuration Manager 升级到 System Center Configuration Manager 的过程中，如果语言包的 System Center Configuration Manager 版本不适用于所下载的先决条件文件，则无法安装对该语言的支持。  

11. 在“客户端语言选择”  页上，查看当前为站点安装的语言的列表。 为客户端计算机选择此站点上可用的其他语言，或清除不再希望在此站点上支持的语言。 指定是否为移动设备客户端启用所有客户端语言，然后单击“下一步” 。 默认情况下，“英语”处于选定状态，并且无法删除。  

    > [!IMPORTANT]  
    >  每个版本的 Configuration Manager 都不能使用其之前版本的 Configuration Manager 的语言包。 若要启用对所升级的 Configuration Manager 站点上的某种语言的支持，必须使用该新版本的语言包版本。 例如，在从 System Center 2012 Configuration Manager 升级到 System Center Configuration Manager 的过程中，如果语言包的 System Center Configuration Manager 版本不适用于所下载的先决条件文件，则无法安装对该语言的支持。  

12. 在“设置摘要”  页上，单击“下一步”  启动先决条件检查程序，针对站点升级验证服务器准备情况。  

13. 在“先决条件安装检查”  页上，如果未列出任何问题，请单击“下一步”  以升级站点和站点系统角色。 如果先决条件检查程序发现问题，请单击列表上的项目以了解有关如何解决该问题的详细信息。 在继续安装程序之前，请解决列表中状态为“错误”  的所有项目。 解决问题之后，单击“运行检查”  以重启先决条件检查。 你也可以打开系统驱动器根目录中的 ConfigMgrPrereq.log 文件以查看先决条件检查程序结果。 该日志文件可能包含用户界面中未显示的某些其他信息。 有关安装先决条件规则和说明的列表，请参阅[先决条件检查程序](/sccm/core/servers/deploy/install/list-of-prerequisite-checks)。  

在“升级”  页上，安装程序将显示总体进度状态。 当安装程序完成核心站点服务器和站点系统安装时，你可以关闭向导。 站点配置将在后台继续进行。  

#### <a name="to-upgrade-a-secondary-site"></a>升级辅助站点  

1.  验证运行安装程序的管理用户是否具有以下安全权限：  

    -   辅助站点计算机上的本地管理员权限  
    -   父主站点上的“基础结构管理员”或“完全权限管理员”安全角色  
    -   辅助站点的站点数据库上的系统管理员 (SA) 权限  
    </br>
2.  在 Configuration Manager 控制台中，单击“管理” 。  

3.  在“管理”  工作区中，展开“站点配置” ，然后单击“站点” 。  

4.  选择要升级的辅助站点，然后在“主页”  选项卡上的“站点”  组中，单击“升级” 。  

5.  单击“是”  以确认决定，并开始辅助站点的升级。  

辅助站点升级将在后台进行。 升级完成后，可以在 Configuration Manager 控制台中确认状态。 要确认状态，请选择辅助站点服务器，然后在“主页”  选项卡上的“站点”  组中单击“显示安装状态” 。  

##  <a name="BKMK_PostUpgrade"></a>执行升级后任务  
将站点升级到新的 Service Pack 后，你可能必须完成其他任务以完成升级或重新配置站点。 这些任务可能包括升级 Configuration Manager 客户端或 Configuration Manager 控制台、重新启用管理点的数据库副本，或者还原所使用的并且在 Service Pack 升级后未保留的 Configuration Manager 功能的设置。  

**辅助站点的已知问题：**  
- **升级到版本 1511 时：**若要确保辅助站点上的客户端可以从辅助站点（代理管理点）找到管理点，请将管理点手动添加到还包含辅助站点上的分发点的边界组。  

- **升级到版本 1606 或更高版本时：**代理管理点会自动添加到包含辅助站点上的分发点的边界组。
