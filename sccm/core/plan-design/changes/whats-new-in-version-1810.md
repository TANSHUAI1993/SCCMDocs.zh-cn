---
title: 1810 版中的新增功能
titleSuffix: Configuration Manager
description: 获取有关 Configuration Manager Current Branch 1810 版中引入的更改和新功能的详细信息。
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d2ab324038e833da7bc080286c820b3df8d06fa
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558161"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch 1810 版中的新增功能

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager Current Branch 的 1810 更新作为控制台中更新提供。 将此更新应用于运行 1710、1802 或 1806 版的站点。 <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->本文汇总了 Configuration Manager 1810 版中的更改和新增功能。  

始终查看安装此更新的最新清单。 有关详细信息，请参阅 [1810 的安装更新清单](/sccm/core/servers/manage/checklist-for-installing-update-1810)。 更新站点后，还可以查看[更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist)。

若要利用新的 Configuration Manager 功能，请先将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

> [!Note]  
> 本文目前列出了此版本中的所有重要功能。 但是，并非所有部分都链接到更新的内容并提供有关新功能的进一步信息。 定期查看此页面以获取更新。 我们使用 [已更新] 标记标注更改。 内容最终确定后，将删除此标注。  

> [!Tip]  
> 若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="bkmk_deprecated"></a>弃用的功能和操作系统

在[已删除和已启用的项](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)中实施支持更改之前，先了解这些更改。

自 2018 年 8 月 14 日起，混合移动设备管理功能已弃用。 有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<!--Intune feature 2683117-->  

将于 2018 年 12 月 31 日结束对 Mac 版和 Linux 版 System Center Endpoint Protection (SCEP)（所有版本）的支持。 在支持结束后，可能会停止为 SCEP for Mac 和 SCEP for Linux 提供新的病毒定义。 有关详细信息，请参阅[“不再提供支持”博客文章](https://go.microsoft.com/fwlink/?linkid=870182)。

Configuration Manager 现已弃用 Azure 的经典服务部署。 开始将 Azure 资源管理器部署用于云管理网关和云分发点。 有关详细信息，请参阅 [CMG 规划](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager)。
<!--
Version 1810 drops support for the following products:
-->



## <a name="bkmk_infra"></a>站点基础结构

### <a name="support-for-windows-server-2019"></a>对 Windows Server 2019 的支持
<!--1359195--> Configuration Manager 现支持将 Windows Server 2019 和 Windows Server 1809 版作为站点系统。 

有关详细信息，请参阅[站点系统服务器支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)。


### <a name="hierarchy-support-for-site-server-high-availability"></a>对站点服务器高可用性的层次结构支持
<!--1358224--> 管理中心站点和子主站点现可拥有其他被动模式下的站点服务器。 

<!--For more information, see [Site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability).-->


### <a name="improvements-to-setup-prerequisites"></a>安装先决条件方面的改进

安装或更新到版本 1810 时，Configuration Manager 安装程序现在包括或改进了以下先决条件检查：

- **正在等待系统重启**：此先决条件检查现可复原。 它会检查 Windows 功能的其他注册表项。 有关详细信息，请参阅[正在等待系统重启](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart)。 <!--SCCMDocs-pr issue 3010-->  

- **SQL 更改跟踪清除**：一项新检查，检查站点数据库是否有 SQL 更改跟踪数据的积压工作 (backlog)。 有关详细信息（包括验证和清除此积压工作的过程），请参阅 [SQL 更改跟踪清除](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#bkmk_changetracking)。 <!--SCCMDocs-pr issue 3023-->  

- **SQL Native Client 版本**：对于支持 TLS 1.2 的 SQL Native Client 版本，将更新此先决条件检查。 最低版本是 [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402)。 有关详细信息，请参阅 [SQL Native Client 版本](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-native-client)。 <!--SCCMDocs-pr issue 3094-->  

- **Windows 群集节点上的站点系统**：Configuration Manager 设置进程不再阻止在具有适用于故障转移群集的 Windows 角色的计算机上安装站点服务器角色。 SQL Always On 需要此角色，因此，以前你无法在站点服务器上共置站点数据库。 进行此更改后，你可以通过在被动模式下使用 SQL Always On 和站点服务器创建具有更少服务器的高可用站点。 有关详细信息，请参阅 [Windows 故障转移群集](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#windows-failover-cluster)。 <!--1359132-->  




### <a name="new-permission-for-client-notification-actions"></a>客户端通知操作的新权限
<!--SCCMDocs-pr issue #2972--> 客户端通知操作现在需要 SMS_Collection 类上的“通知资源”权限。 默认情况下，以下内置角色具有此权限：
- 完全权限管理员  
- 基础结构管理员  

向所有需要使用客户端通知操作的自定义角色添加此权限。 

有关详细信息，请参阅[客户端通知](/sccm/core/clients/manage/client-notification)。



## <a name="bkmk_content"></a>内容管理

### <a name="new-boundary-group-options"></a>新的边界组选项
<!--1358749--> 边界组现在包含以下附加设置，可让你更好地控制环境中的内容分发：

- **优先选择分发点而非具有相同子网的对等**：默认情况下，管理点会优先考虑内容位置列表顶部的对等缓存源。 此设置会反转与对等缓存源位于同一子网的客户端的优先级。  

- **优先选择云分发点而非一般分发点**：如果你的分支机构具有更快的 Internet 链接，你现在可以优先考虑云内容。  

有关详细信息，请参阅[对等下载适用的边界组选项](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions)。


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>对等缓存源客户端版本的管理见解规则
<!-- 1358008 -->“管理见解”节点使用新规则来确定用作对等缓存源但尚未从 1806 之前的客户端版本升级的客户端。 新规则是“将对等缓存源升级到最新版本的 Configuration Manager 客户端”，并且是新“主动维护”规则组的一部分。 先前的 1806 客户端不能用作运行版本 1806 或更高版本的客户端的对等缓存源。 选择“采取措施”打开显示客户端列表的设备视图。 

有关详细信息，请参阅[管理见解](/sccm/core/servers/manage/management-insights)。



## <a name="bkmk_client"></a> 客户端管理

### <a name="new-client-notification-action-to-wake-up-device"></a>用于唤醒设备的新客户端通知操作
<!--1317364--> 现在你可以从 Configuration Manager 控制台唤醒客户端，即使客户端与站点服务器不在同一子网中。 如果你需要执行维护或查询设备，则不会受到处于睡眠状态的远程客户端的限制。 站点服务器使用客户端通知通道来标识在同一远程子网上处于唤醒状态的另一个客户端。 然后唤醒的客户端发送 LAN 唤醒请求（幻数据包）。

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>从“设备”节点执行“客户端通知”的新选项
<!--1317364--> 在 1810 推出前，“客户端通知”选项仅在“设备集合”节点中可用，或仅在查看设备集合的成员资格时可用。 现在，可以直接从“设备”节点执行“客户端通知”。 不再要求必须在集合成员资格视图内。 

有关详细信息，请参阅[客户端通知](/sccm/core/clients/manage/client-notification)。


### <a name="improvements-to-collection-evaluation"></a>对集合评估的改进
<!--3607726, fka 1358981-->
 ***[已更新]*** 集合评估行为中的以下更改可改进站点性能：  

- 以前，在基于查询的集合上配置计划时，站点将继续评估查询，无论你是否启用了“在此集合上计划完全更新”的集合设置。 若要完全禁用计划，必须将计划更改为“无”。 现在，当你禁用此设置时，站点将清除计划。 若要指定对计划进行集合评估，请启用“在此集合上计划完全更新”的选项。  

- 你无法禁用“所有系统”等内置集合的评估，但现在可以配置计划。 此行为使你能够在满足你的业务需求的同时自定义此操作。 

有关详细信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections#bkmk_create)。


### <a name="improvement-to-client-installation"></a>客户端安装改进
<!--1358840--> 在安装 Configuration Manager 客户端时，ccmsetup 进程会联系管理点以查找所需的内容。 以前在此进程中，管理点仅返回客户端当前边界组中的分发点。 如果没有可用内容，安装进程会回退，以从管理点下载内容。 无法回退到其他边界组中可能具有必要内容的分发点。 现在，管理点会基于边界组配置返回分发点。 

有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_ccmsetup)。



## <a name="bkmk_comgmt"></a> 共同管理

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>共同托管的设备所需的应用符合性策略
<!--1358196--> 在 Configuration Manager 中为所需应用程序定义符合性策略规则。 此应用评估是向 Microsoft Intune 发送的针对共同托管设备的整体符合性状态的一部分。

<!--For more information, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).-->


### <a name="improvement-to-co-management-dashboard"></a>对共同管理仪表板的改进
<!--1358980--> 通过在共同管理仪表板中增加了以下更多详细信息，共同管理仪表板功能得到了增强：  

- “共同管理注册状态”磁贴包含了其他状态

- 带有漏斗图的新增“共同管理状态”磁贴显示了注册过程的状态

- 新增一个显示“注册错误”计数的磁贴

![显示了前四个磁贴的共同托管仪表板的屏幕截图](media/1358980-comgmt-dashboard.png)

有关详细信息，请参阅[共同管理仪表板](/sccm/comanage/how-to-monitor#co-management-dashboard)。


### <a name="improvements-to-internet-based-client-setup"></a>对基于 Internet 的客户端设置的改进
<!--3607731, fka 1359181-->
 ***[已更新]*** 此版本进一步简化了针对 Internet 上的客户端的 Configuration Manager 客户端安装过程。 此站点向云管理网关 (CMG) 发布其他 Azure Active Directory (Azure AD) 信息。 Azure AD 联接的客户端使用其联接的同一租户在 ccmsetup 进程中从 CMG 获取此信息。 这种行为进一步简化了注册设备，使其在有多个 Azure AD 租户的环境中进行共同管理。 现在，只有两个必需的 ccmsetup 属性：CCMHOSTNAME 和 SMSSiteCode。

有关详细信息，请参阅[如何准备基于 Internet 的设备以进行共同管理](/sccm/comanage/how-to-prepare-Win10#install-the-configuration-manager-client)。



<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a>应用程序管理

### <a name="convert-applications-to-msix"></a>将应用程序转换为 MSIX
<!--3607729, fka 1359029-->
 ***[已更新]*** 从版本 1806 开始，Configuration Manager 支持部署新的 Windows 10 应用包 (.msix) 格式。 现在可以将你的现有 Windows Installer (.msi) 应用程序转换为 MSIX 格式。

有关详细信息，请参阅[创建 Windows 应用程序](/sccm/apps/get-started/creating-windows-applications#bkmk_msix)。  


### <a name="repair-applications"></a>修复应用程序
<!--1357866--> 指定 Windows 安装程序和脚本安装程序部署类型的修复命令行。 然后，如果在部署中启用该选项，则可以在软件中心中使用新按钮“修复”应用程序。 当为应用程序配置修复程序时，用户可以从软件中心启动命令。 

有关详细信息，请参阅[创建应用程序](/sccm/apps/deploy-use/create-applications#bkmk_dt-content)和[部署应用程序](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-settings)。


### <a name="approve-application-requests-via-email"></a>通过电子邮件批准应用程序请求
<!--1321550--> 配置用于应用程序批准请求的电子邮件通知。 当用户请求应用程序时，你会收到一封电子邮件。 单击电子邮件中的链接以批准或拒绝该请求，而无需使用 Configuration Manager 控制台。

有关详细信息，请参阅[批准应用程序](/sccm/apps/deploy-use/app-approval)。


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>检测方法不会加载 Windows PowerShell 配置文件
<!--3607762, fka 1359239-->
 ***[已更新]*** 可以使用 Windows PowerShell 脚本来检测应用程序和配置项中的设置。 当这些脚本在客户端上运行时，Configuration Manager 客户端现在使用 `-NoProfile` 参数调用 PowerShell。 此选项在没有配置文件的情况下启动 PowerShell。 

PowerShell 配置文件是在 PowerShell 启动时运行的脚本。 可以创建 PowerShell 配置文件以自定义环境，并向启动的每个 PowerShell 会话中添加特定于会话的元素。 

> [!Note]  
> 此行为中的更改不适用于[脚本](/sccm/apps/deploy-use/create-deploy-scripts)或 [CMPivot](/sccm/core/servers/manage/cmpivot)。 这两项功能均已使用此 PowerShell 参数。    

有关详细信息，请参阅[创建应用程序](/sccm/apps/deploy-use/create-applications)和[创建自定义配置项](/sccm/compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client)。



## <a name="bkmk_osd"></a> OS 部署

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>针对现有设备的 Windows Autopilot 的任务序列支持
<!--3607717, fka 1358333-->

***[已更新]*** [面向现有设备的 Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) 现可通过 Windows 10 版本 1809 或更高版本提供。 此新功能可重置映像并使用单个本机 Configuration Manager 任务序列为 [Windows Autopilot 用户驱动模式](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven)预配 Windows 7 设备。 

有关详细信息，请参阅[面向现有设备的 Windows Autopilot](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices)。


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>指定用于为脱机 OS 映像提供服务的驱动器  
<!--1358924--> 现在指定 Configuration Manager 在向 OS 映像和 OS 升级包添加软件更新时使用的驱动器。 此过程可能会产生临时文件占用大量的磁盘空间，因此，借助此选项，你可以灵活地选择要使用的驱动器。 

有关详细信息，请参阅[管理 OS 映像](/sccm/osd/get-started/manage-operating-system-images#bkmk_servicing-drive) 或 [管理 OS 升级包](/sccm/osd/get-started/manage-operating-system-upgrade-packages#bkmk_servicing-drive)。


### <a name="task-sequence-support-for-boundary-groups"></a>对边界组的任务序列支持
<!--1359025--> 当设备运行任务序列并且需要获取内容时，它现在可以使用类似于 Configuration Manager 客户端的边界组行为。   

有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd)。


### <a name="improvements-to-driver-maintenance"></a>对驱动程序维护的改进
<!--3607716, fka 1358270-->
 ***[已更新]*** 驱动程序包现在具有用于“制造商”和“模型”的其他元数据字段。 使用这些字段可标记驱动程序包的信息，以帮助进行常规任务管理，或标识可以删除的旧的及重复的驱动程序。

有关详细信息，请参阅[管理驱动程序](/sccm/osd/get-started/manage-drivers)。


### <a name="new-task-sequence-variable-for-last-action-name"></a>最后一个操作名称的新任务序列变量
<!--SCCMDocs-pr issue #2964--> 任务序列变量与任务序列变量 _SMSTSLastActionRetCode 一起设置新建变量“_SMSTSLastActionName”。 它还会将此值记录到 smsts.log 文件中。 对任务序列进行故障排除时，此新变量十分有用。 当步骤失败时，自定义脚本可以包含步骤名称和返回代码。

有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables#SMSTSLastActionName)。



<!-- ## <a name="bkmk_userxp"></a> Software Center -->



## <a name="bkmk_sum"></a>软件更新

### <a name="phased-deployment-of-software-updates"></a>软件更新的分阶段部署
<!--1358146--> 创建软件更新的分阶段部署。 通过分阶段部署，可以根据可自定义条件和组进行协调安排，有序推出软件。

有关详细信息，请参阅[创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)。


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>软件更新的维护时段的改进
<!--vso2839307--> 以下客户端设置位于“软件更新”组中，以控制在维护时段中的软件更新的安装行为： 

当“软件更新”维护时段可用时，在“所有部署”维护时段中启用更新安装

默认情况下，此选项为“否”以与现有行为保持一致。 请将其更改为“是”，以允许客户端使用其他可用的维护时段来安装软件更新。

<!--For more information, see []().-->

### <a name="improvement-to-software-updates-maintenance"></a>对软件更新维护的改进
<!--2839349--> WSUS 清理任务现在在辅助站点上运行。 为辅助站点运行已过期更新的 WSUS 清理，并拒绝 WSUS 中的取代更新。

有关更多信息，请参阅[从版本 1810 开始的 WSUS 清理行为](/sccm/sum/deploy-use/software-updates-maintenance#wsus-cleanup-behavior-starting-in-version-1810)

## <a name="bkmk_report"></a>报表

### <a name="improvement-to-lifecycle-dashboard"></a>生命周期仪表板的改进
<!--1358702--> 产品生命周期仪表板现包含“System Center 2012 Configuration Manager 及更高版本”的信息。 

此外，还有新的报表，“生命周期 05A - 产品生命周期仪表板”。 它包括与控制台中仪表板类似的信息。

有关此仪表板的更多信息，请参阅[使用产品生命周期仪表板](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard)。


### <a name="improvement-to-data-warehouse"></a>数据仓库的改进
<!--1358870--> 现可将更多表从站点数据库同步到数据仓库。 通过此更改，可根据业务需求创建更多报告。

有关详细信息，请参阅[数据仓库](/sccm/core/servers/manage/data-warehouse)。



<!-- ## <a name="bkmk_inv"></a> Inventory -->




<!-- ## <a name="bkmk_protect"></a> Protect devices-->




## <a name="bkmk_admin"></a> Configuration Manager 控制台

### <a name="configuration-manager-administrator-authentication"></a>Configuration Manager 管理员身份验证
<!--1357013--> 现在可以为管理员指定访问 Configuration Manager 站点的最低身份验证级别。 此功能强制管理员以要求的级别登录到 Windows。 若要配置此设置，请查找“层次结构设置”中的“身份验证”选项卡。 

有关详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth)。


### <a name="support-center"></a>支持中心
<!--1357489--> 使用支持中心排除客户端故障、查看实时日志，或者捕获 Configuration Manager 客户端计算机状态供日后分析。 支持中心是合并多个管理员故障排除工具的单一工具。 在站点服务器的 cd.latest\SMSSETUP\Tools\SupportCenter 文件夹中找到支持中心安装程序。

有关详细信息，请参阅[支持中心](/sccm/core/support/support-center)。


### <a name="management-insights-dashboard"></a>管理见解仪表板
<!--1357979-->

“管理见解”节点现在包括一个图形仪表板。 此仪表板可概要显示规则状态，让你能够更轻松地显示进度。 该仪表板具有以下磁贴：

- **管理见解索引**：跟踪管理见解规则的总体进度。 该索引为加权平均值。 关键规则最为重要。 此索引为可选规则提供的加权最低。  

- **管理见解组**：显示每个组中的规则所占百分比。  

- **管理见解优先级**：按优先级显示规则所占百分比。  

- **所有见解**：一个包括优先级和状态的见解表。  

![管理见解仪表板的屏幕截图](media/1357979-management-insights-dashboard.png)

有关详细信息，请参阅[管理见解](/sccm/core/servers/manage/management-insights)。


### <a name="improvements-to-cmpivot"></a>CMPivot 的改进
<!--1359068--> CMPivot 包括以下改进：

- 保存收藏夹查询  

- 在“查询摘要”选项卡上，选择“故障”或“脱机”设备的计数，然后选择“创建集合”选项。 

有关 CMPivot 其他性能和故障诊断改进的详细信息，请参阅[脚本改进](#bkmk_scripts)。

<!--For more information on CMPivot, see [CMPivot](/sccm/core/servers/manage/cmpivot).-->


### <a name="bkmk_scripts"></a> 脚本改进
<!--1358239--> 现在，可以原始或结构化的 JSON 格式查看详细的脚本输出。 此格式设置可使输出更易于读取和分析。 

以下性能和故障诊断改进适用于 CMPivot 和脚本：

- 更新的客户端会通过快速信道将不超过 80 KB 的输出返回到站点。 这一更改提高了查看脚本或查询输出的性能。  

- 用于故障排除的其他日志  

<!--For more information, see the following articles:  

- [Create and run PowerShell scripts from the Configuration Manager console](/sccm/apps/deploy-use/create-deploy-scripts)  

- [CMPivot](/sccm/core/servers/manage/cmpivot)  -->


### <a name="sms-provider-api"></a>SMS 提供程序 API
<!--1321523--> SMS 提供程序现通过 HTTPS 提供对 WMI 的只读 API 互操作性访问。 SMS 提供程序显示为角色，其中包含允许通过云管理网关进行通信的选项。 此设置的当前用途是通过来自远程设备的电子邮件启用应用程序批准。 有关详细信息，请参阅[通过电子邮件批准应用程序请求](#approve-application-requests-via-email)。



## <a name="bkmk_opmdm"></a> 本地 MDM

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>新的本地 MDM 部署不再需要 Intune 连接
<!--1359124--> 新部署不再需要配置 Microsoft Intune 订阅的本地 MDM 先决条件。 组织仍需要 Intune 许可证才能使用此功能。 目前无法从现有的本地 MDM 部署中删除 Intune 连接。 有关详细信息，请参阅 [Intune 支持博客文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150)。



## <a name="other-updates"></a>其他更新

除了新增功能外，这一版还有其他变化（如缺陷修复）。 有关详细信息，请参阅 [Configuration Manager Current Branch（版本 1810）的更改摘要](https://support.microsoft.com/help/4482169)。

若要详细了解对用于 Configuration Manager 的 Windows PowerShell cmdlet 的更改，请参阅 [PowerShell 1810 版发行说明](https://docs.microsoft.com/powershell/sccm/1810-release-notes?view=sccm-ps)。

以下更新汇总 (4486457) 于 2019 年 1 月 25 日起在控制台中提供：[Configuration Manager Current Branch（版本 1810）更新汇总](https://support.microsoft.com/help/4486457)。


### <a name="hotfixes"></a>修补程序

以下附加修补程序可用于解决特定问题：

| ID | 标题 | 日期 | 控制台内部 |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune 连接器证书在 Configuration Manager 中未续订 | 2019 年 1 月 18 日 | 是 |
| [4490434](https://support.microsoft.com/help/4490434) | 在 Configuration Manager 中创建重复的用户发现列 | 2019 年 2 月 22 日 | 是 |
| [4490575](https://support.microsoft.com/help/4490575) | 更新安装在 Configuration Manager 1810 版中停止响应或从未显示完成 | 2019 年 2 月 22 日 | 是 |


## <a name="next-steps"></a>后续步骤

准备好安装此版本时，请参阅[安装 Configuration Manager 的更新](/sccm/core/servers/manage/updates)和 [1810 安装更新清单](/sccm/core/servers/manage/checklist-for-installing-update-1810)。

> [!TIP]  
> 若要安装新站点，请使用 Configuration Manager 的基准版本。  
>
>  了解详细信息：    
>   - [安装新站点](/sccm/core/servers/deploy/install/installing-sites)  
>   - [基准和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

关于已知的重要问题，请参阅[发行说明](/sccm/core/servers/deploy/install/release-notes)。

更新站点后，还可以查看[更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist)。
