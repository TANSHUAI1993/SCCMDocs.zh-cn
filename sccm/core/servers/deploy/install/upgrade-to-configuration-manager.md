---
title: 升级到 Configuration Manager
description: 了解从运行 System Center 2012 Configuration Manager 的站点和层次结构成功进行就地升级的步骤。
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb0d120fd9d9b301cf02af9c6126a0991524e9c6
ms.sourcegitcommit: 4241c15a277c57b5480dea70fc30f1ed46ffd4f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69490047"
---
# <a name="upgrade-to-configuration-manager"></a>升级到 Configuration Manager

适用范围：  System Center Configuration Manager (Current Branch)

从运行 System Center 2012 Configuration Manager 的站点和层次结构就地升级到 Configuration Manager Current Branch。 在从 System Center 2012 Configuration Manager 升级之前，必须准备这些站点。 此准备工作需要删除可能会阻止成功升级的特定配置。 如果涉及多个站点，则按升级顺序依次升级。  

> [!TIP]  
> 管理 Configuration Manager 站点和层次结构基础结构时，术语“升级”  、“更新”  和“安装”  用于描述三种不同概念。 若要了解每个术语的使用方法，请参阅[有关升级、更新和安装](/sccm/core/understand/upgrade-update-install)。



## <a name="bkmk_path"></a> 就地升级路径  

以下选项是当前支持的就地升级路径：


### <a name="upgrade-to-version-1902"></a>升级到版本 1902

可以将以下内容升级到 System Center Configuration Manager 版本 1902 的完全许可版本：   
- System Center Configuration Manager 版本 1902 的评估版安装
- System Center 2012 Configuration Manager Service Pack 1
- System Center 2012 Configuration Manager Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager Service Pack 1

### <a name="upgrade-to-version-1802"></a>升级到版本 1802
可以将以下内容升级到 System Center Configuration Manager 版本 1802 的完全许可版本：   
- System Center Configuration Manager 版本 1802 的评估版安装
- System Center 2012 Configuration Manager Service Pack 1
- System Center 2012 Configuration Manager Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager Service Pack 1

有关详细信息，请参阅 [Configuration Manager 分支和许可的常见问题解答](/sccm/core/understand/product-and-licensing-faq)。

> [!TIP]  
>  从 System Center 2012 Configuration Manager 版本升级到 Current Branch 时，或许能够简化升级过程。 有关详细信息，请参阅以下内容：  
>   
> - [基准和更新版本](/sccm/core/servers/manage/updates#bkmk_Baselines)  
> - [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)  


### <a name="unsupported-paths"></a>不支持的路径

不支持以下路径：

- 不支持将技术预览分支升级到完整许可版安装。 技术预览版只能升级到更高版本的技术预览版。  

- 不支持从技术预览版迁移到完整许可版。  



##  <a name="bkmk_checklist"></a> 升级清单  

下列清单可帮助规划成功升级到 Configuration Manager。  


### <a name="before-you-upgrade"></a>升级准备工作  

在升级到 Configuration Manager 之前，请核查以下步骤。


#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>检查 System Center 2012 Configuration Manager 环境
解决以下 Microsoft 支持文章中所述的问题：[由于重复的重试任务，Configuration Manager 客户端每五个小时重新安装一次，并可能在无意间导致客户端升级](https://support.microsoft.com/help/4018655)。

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>确保环境满足支持的配置要求

- 查看正在用于托管站点系统角色的服务器操作系统版本：  

    - System Center 2012 Configuration Manager 支持的某些较旧版本操作系统不受 Configuration Manager Current Branch 支持。 在升级之前，请删除这些操作系统版本上的站点系统角色。 有关详细信息，请参阅[站点系统服务器支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)。   

    - Configuration Manager 的先决条件检查程序不会验证站点服务器或远程站点系统上的站点系统角色的先决条件  

- 查看托管站点系统角色的每台计算机必须满足的先决条件。 例如，为了部署操作系统，Configuration Manager 使用 Windows 10 评估和部署工具包 (Windows ADK)。 运行安装程序之前，必须在站点服务器以及运行 SMS 提供程序实例的每台计算机上下载和安装 Windows 10 ADK。  

有关支持的平台和先决条件配置的详细信息，请参阅[支持的配置](/sccm/core/plan-design/configs/supported-configurations)。  

有关将 Windows ADK 与 Configuration Manager 搭配使用的详细信息，请参阅[操作系统部署的基础架构要求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>查看站点和层次结构状态，并确认没有未解决的问题
升级站点之前，请解决远程计算机上安装的站点服务器、站点数据库服务器和站点系统角色的所有操作问题。 由于现有的操作问题，站点升级可能会失败。  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>为托管站点、站点数据库服务器和远程站点系统角色的计算机上的操作系统安装所有适用的重要更新
升级站点之前，请为每个合适的站点系统安装任何关键更新。 如果安装的更新需要重启，请在启动 Service Pack 更新之前重启合适的计算机。  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>卸载 Configuration Manager 不支持的站点系统角色
Configuration Manager 不再使用以下站点系统角色。 在从 System Center 2012 Configuration Manager 升级之前将其卸载：  

- 带外管理点  

- 系统健康验证程序点  

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>在主站点上禁用管理点的数据库副本
Configuration Manager 无法升级具有管理点数据库副本的主站点。 禁用数据库复制，然后：  

- 创建站点数据库的备份以测试数据库升级  

- 将生产站点升级到 System Center Configuration Manager  

有关详细信息，请参阅下列文章：  

- System Center 2012 Configuration Manager：[为管理点配置数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points#BKMK_DBReplica_Config)  

- Configuration Manager Current Branch：[管理点的数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>重新配置使用 NLB 的软件更新点
Configuration Manager 无法升级使用网络负载均衡 (NLB) 群集来托管软件更新点的站点。  

如果为软件更新点使用 NLB 群集，请使用 PowerShell 删除 NLB 群集。 （从 System Center 2012 Configuration Manager SP1 开始，Configuration Manager 控制台中不再有配置 NLB 群集的选项）  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>在该站点的升级过程中，禁用每个站点上的所有站点维护任务
在升级到 Configuration Manager 之前，请禁用可能会在升级过程进行时运行的任何站点维护任务。 此列表包括但不限于以下任务：  

- 备份站点服务器  
- 删除过期的客户端操作  
- 删除过期的发现数据  

如果站点数据库维护任务在升级过程中运行，站点升级可能会失败。  

在禁用任务之前，请记录该任务的计划，以便能够在站点升级完成后恢复其配置。 

有关站点维护任务的详细信息，请参阅以下文章：  

- System Center 2012 Configuration Manager：[规划站点操作](/sccm/core/plan-design/hierarchy/plan-for-the-site-database)  

- Configuration Manager Current Branch：[维护任务参考](/sccm/core/servers/manage/reference-for-maintenance-tasks)  

#### <a name="run-setup-prerequisite-checker"></a>运行安装程序先决条件检查程序
在升级站点之前，请运行独立于安装程序的**先决条件检查程序**，验证站点是否满足先决条件。 稍后升级该站点时会再次运行必备组件检查程序。  

如果使用 2016 年 10 月发行的 1606 版基线介质，独立的先决条件检查会对要升级到 Configuration Manager 的 Current Branch 和 Long-Term Servicing Branch (LTSB) 的站点进行评估。 由于 LTSB 不支持某些功能，在 ConfigMgrPrereq.log  中可能会看到以下类似条目：
- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

如果计划升级到 Current Branch，可以安全地忽略 LTSB 版本的错误。 如果计划升级到 LTSB 才适用。

稍后当你运行 Configuration Manager 安装程序以执行升级时，将再次运行先决条件检查。 它会根据选择安装的 Configuration Manager 的分支（Current Branch 或 LTSB）评估你的站点。 如果选择升级到 Current Branch，则不会对 LTSB 不支持的功能运行检查。

有关详细信息，请参阅[先决条件检查程序](/sccm/core/servers/deploy/install/prerequisite-checker)和[先决条件检查列表](/sccm/core/servers/deploy/install/list-of-prerequisite-checks)。  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>下载 Configuration Manager 的先决条件文件和可再发行文件
使用安装程序下载程序  下载 Configuration Manager 的先决条件可再发行文件、语言包和最新产品更新。  

有关信息，请参阅[安装程序下载程序](/sccm/core/servers/deploy/install/setup-downloader)。  

#### <a name="plan-to-manage-server-and-client-languages"></a>计划管理服务器和客户端语言
当站点升级时，站点升级仅安装在升级过程中选择的语言包版本。  

- 安装程序将查看你的站点的当前语言配置。 随后将识别在存储以前下载的先决条件文件的文件夹中提供的语言包。  

- 可以确认选择的当前服务器和客户端语言包，或者更改选择以添加或删除语言支持。  

- 只能选择在运行安装程序时可用的语言包。  

> [!NOTE]  
> 不能使用 System Center 2012 Configuration Manager 的语言包为 Configuration Manager Current Branch 站点启用语言。  

有关语言包的详细信息，请参阅[语言包](/sccm/core/servers/deploy/install/language-packs)。  

#### <a name="review-considerations-for-site-upgrades"></a>查看站点升级注意事项
升级站点时，某些功能和配置会重置为默认配置。 若要帮助准备这些更改以及相关更改，请参阅[升级注意事项](#bkmk_considerations)。  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>在管理中心站点和主站点上创建站点数据库备份
升级站点之前，请备份站点数据库，以确保具有用于灾难恢复的成功备份。  

有关详细信息，请参阅[备份和恢复](/sccm/core/servers/manage/backup-and-recovery)。  

#### <a name="back-up-a-customized-configurationmof-file"></a>备份自定义 Configuration.mof 文件
如果使用自定义 Configuration.mof 文件定义与硬件清单一起使用的数据类，请创建此文件的备份。 升级之后，将此文件还原到你的站点。 有关详细信息，请参阅[如何扩展硬件清单](/sccm/core/clients/manage/inventory/extend-hardware-inventory)。  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>在最近的站点数据库备份副本上测试数据库升级过程
在升级 Configuration Manager 管理中心站点或主站点之前，请对站点数据库的副本测试站点数据库升级过程。  

- 测试站点数据库升级过程。 升级站点时，可能会修改站点数据库。  

- 虽然测试数据库升级不是必需的，但可以在生产数据库受到影响之前先行确定升级的问题  

- 失败的站点数据库升级可能会使站点数据库无法运行，并且可能需要进行站点恢复以还原功能  

- 虽然在层次结构的站点之间共享了站点数据库，但是，请在升级每个合适的站点之前计划在该站点上测试数据库  

- 如果在主站点上对管理点使用数据库副本，请在创建站点数据库备份之前禁用复制  

Configuration Manager 不支持辅助站点备份，也不支持辅助站点数据库的测试升级。  

不支持在生产站点数据库上运行测试数据库升级。 执行此操作会升级站点数据库，并可能导致你的站点无法运行。  

有关详细信息，请参阅 [测试站点数据库升级](#bkmk_test)。  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>重启站点服务器和托管站点系统角色的每台计算机
执行此操作以确保更新的最新安装或先决条件没有挂起操作。  

#### <a name="upgrade-sites"></a>升级站点
从层次结构的顶层站点开始，运行 Configuration Manager 源媒体中的 Setup.exe。  

在顶层站点升级之后，可以开始升级每个子站点。 请先完成每个站点的升级，然后开始升级下一个站点。  

在层次结构中的所有站点均升级到 Configuration Manager 之前，层次结构将在混合版本模式下运行。  

有关如何运行升级的信息，请参阅[升级站点](#bkmk_upgrade)。  


### <a name="after-you-upgrade"></a>升级后续工作  

在升级到 Configuration Manager 之后，请核查以下步骤。

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>升级独立的 Configuration Manager 控制台
默认情况下，在升级管理中心站点或主站点时，安装过程也会升级站点服务器上安装的 Configuration Manager 控制台。 手动升级安装在非站点服务器的计算机上的每个控制台。  

> [!TIP]  
> 在开始升级之前，关闭每个打开的控制台。  

有关详细信息，请参阅[安装 Configuration Manager 控制台](/sccm/core/servers/deploy/install/install-consoles)。  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>为主站点上的管理点重新配置数据库副本
如果将数据库副本用于主站点中的管理点，请先卸载数据库副本，再升级站点。 升级主站点之后，为管理点重新配置数据库副本。   

有关详细信息，请参阅[管理点的数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)。  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>重新配置在升级前禁用的任何数据库维护任务
如果升级之前在站点上禁用了数据库[维护任务](/sccm/core/servers/manage/reference-for-maintenance-tasks)，请使用与升级之前存在的相同设置在站点上重新配置这些任务。  

#### <a name="upgrade-clients"></a>升级客户端
所有站点都升级到 Configuration Manager 后，可计划升级客户端。  

升级客户端时，会卸载当前的客户端软件，然后安装新的客户端软件版本。 可以使用 Configuration Manager 支持的任何方法来升级客户端。  

> [!TIP]  
> 在升级层次结构的顶层站点时，也会更新层次结构中的每个分发点上的客户端安装包。 升级主站点时，会更新该主站点提供的客户端升级包。  

有关详细信息，请参阅[如何升级 Windows 计算机的客户端](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers)。  



## <a name="bkmk_considerations"></a> 升级注意事项  


### <a name="automatic-actions"></a>自动操作

升级到 Configuration Manager 时，会自动执行下列操作：  

- 站点重置。 此操作包括重新安装所有站点系统角色。  

- 如果站点是层次结构的顶层站点，则会更新层次结构中的每个分发点上的客户端安装包。 站点还会更新默认启动映像以使用 Windows 评估和部署工具包 10 随附的新 Windows PE 版本。 但是，升级操作不会升级现有媒体以用于映像部署。  

- 如果站点是主站点，则会更新该站点的客户端升级包。  


### <a name="manual-actions-after-an-upgrade"></a>升级后的手动操作

升级站点后，请务必执行下列操作：  

- 确保分配到每个主站点的客户端都升级并安装新客户端版本  

- 升级连接到站点以及在远离站点服务器的计算机上运行的每个 Configuration Manager 控制台  

- 在将数据库副本用于管理点的主站点中，重新配置数据库副本  

- 站点升级后，手动升级 CD、DVD 或 U 盘的物理媒体（如 ISO 文件）。 还包括提供给硬件供应商的预留媒体。 站点升级可更新默认启动映像，但它不能升级在 Configuration Manager 以外使用的这些媒体文件或设备。  

- 计划在不需要较低版本的 Windows PE 时更新自定义启动映像。  


### <a name="actions-that-affect-configurations-and-settings"></a>影响配置和设置的操作**   

在站点升级到 Configuration Manager 时，某些配置和设置在升级后将不再存在。 某些配置设置为新的默认配置。 以下列表包含一些不再存在或发生更改的设置：  

- **软件中心**  
    下列软件中心项目被重置为它们的默认值：  

    - “工作信息”  被重置为周一到周五从凌晨 5:00  到晚上 10:00  Monday 到晚上 10:00 Friday.  

    - “计算机维护”  的值被设置为“当我的计算机处于演示模式时暂停软件中心活动”  。  
    
    - “远程控制”  的值被设置为分配到计算机的客户端设置中的值。  

- **软件更新摘要计划**：软件更新或软件更新组的自定义摘要计划被重置为默认值（1 小时）。 升级完成后，请将自定义摘要值重置为所需的频率。  



## <a name="bkmk_test"></a> 测试站点数据库升级  

以下信息仅适用于将先前版本（如 System Center 2012 Configuration Manager）升级到 Configuration Manager Current Branch。

在升级站点之前，请针对升级测试该站点的数据库副本。  

若要针对升级测试数据库，请首先将站点数据库的副本还原到未托管 Configuration Manager 站点的 SQL Server 实例。 用于托管数据库副本的 SQL Server 版本必须是 Configuration Manager 支持的 SQL Server 版本。  

在还原站点数据库之后，在 SQL Server 计算机上，从 Configuration Manager 的源媒体文件夹中运行 Configuration Manager 安装程序。 使用 `/TESTDBUPGRADE` 命令行选项。  

有关详细信息，请参阅下列文章：

- [备份 Configuration Manager 站点](/sccm/core/servers/manage/backup-and-recovery)  

- [适用于安装程序的命令行选项](/sccm/core/servers/deploy/install/command-line-options-for-setup#bkmk_setup)  

- [支持 SQL Server 版本](/sccm/core/plan-design/configs/support-for-sql-server-versions)  

> [!TIP]  
> 如果将 Microsoft Intune 与 Configuration Manager 集成：  
>   
>  当你对已有 5 天或超过 5 天的站点数据库副本运行测试数据库升级时，可能会收到以下其中一条消息：  
>   
> - 警告：升级将强制完全同步到云。  
> - 错误：数据库升级将强制完全同步到云。  
>   
> 这两种情况都可以在测试数据库升级的过程中被安全地忽略。 它们并未指明测试升级失败或出现问题。 相反，它们会指出在实际升级期间，来自**云**数据库复制组的数据可能会与 Microsoft Intune 同步。  


### <a name="test-a-site-database-for-upgrade"></a>测试要升级的站点数据库  

在计划升级的每个管理中心站点和主站点上使用下列过程：  

1. 创建站点数据库的副本。 然后将该副本还原到 SQL Server 的实例，该实例使用与站点数据库相同的版本，并且未托管 Configuration Manager 站点。 例如，站点数据库运行在 SQL Server 的 Enterprise Edition 实例上，请确保将数据库还原到也运行 SQL Server Enterprise Edition 的 SQL Server 实例。  

2. 还原数据库副本之后，请从 Configuration Manager Current Branch 的源媒体中运行安装程序。 运行安装程序时，使用 `/TESTDBUPGRADE` 命令行选项。 如果托管数据库副本的 SQL Server 实例不是默认实例，还请提供命令行参数以确定托管站点数据库副本的实例。  

    例如，你计划升级数据库名称为 SMS_ABC 的站点数据库。 你将此站点数据库的副本还原到实例名称为 DBTest 的受支持 SQL Server 实例。 若要测试此站点数据库副本的升级，请使用下列命令行：`Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Setup.exe 在 Configuration Manager 源媒体上位于以下位置：`SMSSETUP\BIN\X64`  

3. 在运行数据库升级测试的 SQL Server 实例上，监视系统驱动器根目录中的 ConfigMgrSetup.log 以了解进度和成功情况。  

    - 如果测试升级失败，请解决与站点数据库升级失败相关的任何问题。 然后，新建站点数据库的备份并测试站点数据库的新副本升级。  

    - 过程成功完成后，你可以删除该数据库副本。  

        > [!NOTE]  
        > 不支持还原用于测试升级的站点数据库的副本以用作任何站点上的站点数据库。  

成功升级站点数据库的副本后，请继续执行 Configuration Manager 站点及其站点数据库的升级。  



## <a name="bkmk_upgrade"></a> 升级站点  

完成以下任务后，即已准备好升级 Configuration Manager 站点：
- 站点升级前配置
- 在数据库副本上测试站点数据库升级
- 下载你打算安装的版本的先决条件文件和语言包

在升级层次结构中的站点时，将会先升级层次结构的顶层站点。 此顶层站点是管理中心站点或独立主站点。 管理中心站点的升级完成后，可以按任何所需顺序升级子主站点。 升级主站点之后，可以升级该站点的子辅助站点，或在升级任何辅助站点之前升级其他主站点。  

若要升级管理中心站点或主站点，请从 Configuration Manager 源媒体中运行安装程序。 不要运行该安装程序来升级辅助站点。 相反，请使用 Configuration Manager 控制台在完成辅助站点的主父站点的升级之后升级该辅助站点。  

在升级站点之前，请关闭站点服务器上的 Configuration Manager 控制台，直至站点升级完成。 还要关闭在站点服务器以外的计算机上运行的每个 Configuration Manager 控制台。 站点升级完成后，你可以重新连接控制台。 但是，在将 Configuration Manager 控制台升级到其新版本之前，该控制台无法显示 Configuration Manager 新版本中提供的某些对象和信息。  


### <a name="upgrade-a-central-administration-site-or-primary-site"></a>升级管理中心站点或主站点  

1. 验证运行安装程序的用户是否具有以下安全权限：  

    - 站点服务器上的本地“管理员”  权限  

    - 如果站点数据库服务器是站点服务器的远程服务器，则为该服务器上的本地“管理员”  权限。  

2. 在站点服务器上，打开以下程序：`<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`。 此操作将打开 Configuration Manager 安装向导。  

3. 阅读“准备工作”  页上的信息，并选择“下一步”  。  

4. 在“入门”  页上，选择“升级此 Configuration Manager 站点”  ，然后选择“下一步”  。  

5. “产品密钥”  页：  

    如果以前安装了 Configuration Manager 评估版，则可以选择“安装此产品的许可版本”  。 然后输入 Configuration Manager 的完整安装产品密钥。 此操作将站点转换为完整版。  

    还可以指定许可协议的“软件保障到期日期”  ，方便向你提醒该日期。 如果在设置期间未输入此值，则稍后可在 Configuration Manager 控制台中指定。  

    > [!NOTE]  
    > Microsoft 不会验证所输入的到期日期，且不会使用此日期验证许可证。 可以使用该日期作为到期日期提醒。 Configuration Manager 会定期检查在线提供的新软件更新，而软件保障许可证应为最新状态，才有资格使用这些额外的更新。    

    有关详细信息，请参阅[许可和分支](/sccm/core/understand/learn-more-editions)。

6. 在“Microsoft 软件许可条款”  页上，阅读并接受许可条款，然后选择“下一步”  。  

7. 在“先决条件许可”  页上，阅读并接受先决条件软件许可条款，然后选择“下一页”  。 安装程序将在必需时下载该软件并将其自动安装到站点系统或客户端上。 在可以继续进入到下一页之前，同意所有条款。  

8. 在“先决条件下载”  页上，指定安装程序是从 Internet 下载最新的内容还是使用以前下载的文件。 此内容包括先决条件可再发行文件、语言包以及最新产品更新。 如果以前通过使用安装程序下载程序下载了文件，请选择“使用以前下载的文件”  并指定下载文件夹。 有关详细信息，请参阅[安装程序下载程序](/sccm/core/servers/deploy/install/setup-downloader)。  

    > [!NOTE]  
    > 在使用以前下载的文件时，请验证下载文件夹的路径是否包含文件的最新版本。  

9. 在“服务器语言选择”  页上，查看当前为站点安装的语言的列表。 选择此站点上可用于 Configuration Manager 控制台和报表的其他语言。 还可清除不再希望在此站点上支持的语言。 默认情况下，“英语”处于选定状态，并且无法删除。  

    > [!IMPORTANT]  
    > 每个版本的 Configuration Manager 都不能使用其之前版本的 Configuration Manager 的语言包。 若要启用对所升级的 Configuration Manager 站点上的某种语言的支持，必须使用该新版本的语言包版本。 例如，在从 System Center 2012 Configuration Manager 升级到 Configuration Manager Current Branch 的过程中，如果语言包的 Current Branch 版本不适用于所下载的先决条件文件，则无法安装对该语言的支持。  

10. 在“客户端语言选择”  页上，查看当前为站点安装的语言的列表。 为客户端计算机选择此站点上可用的其他语言，或清除不再希望在此站点上支持的语言。 指定是否为移动设备客户端启用所有客户端语言，然后单击“下一步”  。 默认情况下，“英语”处于选定状态，并且无法删除。  

11. 在“设置摘要”  页上，查看配置。 准备好后，选择“下一步”  启动先决条件检查程序，针对站点升级验证服务器准备情况。  

12. 在“先决条件安装检查”  页上，如果未列出任何问题，请选择“下一步”  以升级站点和站点系统角色。 

    如果先决条件检查程序发现问题，请选择列表上的项目以了解有关如何解决该问题的详细信息。 在继续安装程序之前，请解决列表中状态为“错误”  的所有项目。 解决问题之后，单击“运行检查”  以重启先决条件检查。 你也可以打开系统驱动器根目录中的 ConfigMgrPrereq.log 文件以查看先决条件检查程序结果。 日志文件可以包含用户界面上未显示的额外信息。 有关安装先决条件规则和说明的列表，请参阅[先决条件检查程序](/sccm/core/servers/deploy/install/list-of-prerequisite-checks)。

在“升级”  页上，安装程序将显示总体进度状态。 当安装程序完成核心站点服务器和站点系统安装时，你可以关闭向导。 站点配置将在后台继续进行。  


### <a name="upgrade-a-secondary-site"></a>升级辅助站点  

1. 验证运行安装程序的管理用户是否具有以下安全权限：  

    - 辅助站点服务器上的本地“管理员”  权限  

    - 父主站点上的“基础结构管理员”  或“完全权限管理员”  安全角色  

    - 辅助站点的站点数据库上的系统管理员 (SA  ) 权限  

2. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点    。  

3. 选择要升级的辅助站点。 在功能区的“主页”  选项卡上，在“站点”  组中，选择“升级”  。  

4. 选择“是”  以确认决定，并开始升级辅助站点。  

辅助站点升级在后台运行。 升级完成后，在 Configuration Manager 控制台中确认状态。 选择辅助站点服务器，然后在功能区的“主页”  选项卡上，在“站点”  组中，选择“显示安装状态”  。  



## <a name="BKMK_PostUpgrade"></a>升级后任务  

升级站点后，可能必须完成额外任务才能完成升级或重新配置站点。 这些任务可包括以下项： 
- 升级 Configuration Manager 客户端
- 升级 Configuration Manager 控制台
- 为管理点重新启用数据库副本
- 还原你使用的且升级后不再存在的 Configuration Manager 功能的设置  

