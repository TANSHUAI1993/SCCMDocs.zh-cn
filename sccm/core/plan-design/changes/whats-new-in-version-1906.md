---
title: 1906 版中的新增功能
titleSuffix: Configuration Manager
description: 获取有关 Configuration Manager Current Branch 版本 1906 中引入的更改和新增功能的详细信息。
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 13c9f2e6f6b279aeea13ce2ede66b6d11f2c12a2
ms.sourcegitcommit: e2e07d74779a2f48693ecaa17a5974204949d109
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999436"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch 版本 1906 中的新增功能

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager Current Branch 的更新 1906 作为控制台中更新提供。 将此更新应用于运行版本 1802 或更高版本的站点。 <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> 本文汇总了 Configuration Manager 版本 1906 中的更改和新增功能。  

始终查看安装此更新的最新清单。 有关详细信息，请参阅[用于安装更新 1906 的清单](/sccm/core/servers/manage/checklist-for-installing-update-1906)。 更新站点后，还可以查看[更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1906#post-update-checklist)。

若要利用 Configuration Manager 的新功能，更新站点后，还请将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

> [!Tip]  
> 若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>要求更改

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>版本 1906 客户端需要 SHA-2 代码签名支持

<!--SCCMDocs-pr#3404-->
由于 SHA-1 算法中存在缺点，并且为了符合行业标准，Microsoft 现在仅使用更安全的 SHA-2 算法来对 Configuration Manager 二进制文件进行签名。 以下 Windows OS 版本需要更新才能获得 SHA-2 代码签名支持：

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

有关详细信息，请参阅 [Windows 客户端的先决条件](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#bkmk_sha2)。


## <a name="bkmk_infra"></a>站点基础结构

### <a name="site-server-maintenance-task-improvements"></a>站点服务器维护任务改进

<!--3555894-->
在站点服务器的详细信息视图上，站点服务器维护任务现可通过它们各自的选项卡进行查看和编辑。 新的“维护任务”选项卡提供了如下信息  ：

- 任务是否已启用
- 任务计划
- 上次启动时间
- 上次完成时间
- 任务是否已成功完成

![站点服务器详细信息视图中用于维护任务的新选项卡](./media/3555894-maintenance-tasks.png)

有关详细信息，请参阅[维护任务](/sccm/core/servers/manage/maintenance-tasks#bkmk_MTs1906)。

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Configuration Manager 更新数据库升级监视

<!--4200581-->
应用 Configuration Manager 更新时，现可在安装状态窗口中查看“升级 ConfigMgr 数据库”任务的状态  。

- 如果数据库升级受阻，则会收到“正在进行，需要注意”的警告  。
   - cmupdate.log 将记录阻止数据库升级的 SQL 中的程序名和会话 ID。
- 数据库升级不再受阻时，状态将重置为“正在进行”或“完成”   。
   - 如果数据库升级受阻，则每 5 分钟进行一次检查，查看其是否仍然受阻。

   ![安装过程中的数据库升级监视](./media/4200581-database-upgrade-monitoring.png)

有关详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates#3-monitor-the-progress-of-updates-as-they-install)。

### <a name="management-insights-rule-for-ntlm-fallback"></a>NTLM 回退的管理见解规则

<!--4572953-->
管理见解包含一项新的规则，用于检测是否为站点启用了安全级别较低的 NTLM 身份验证回退方法：已启用 NTLM 回退  。

有关详细信息，请参阅[管理见解](/sccm/core/servers/manage/management-insights#security)。

### <a name="improvements-to-support-for-sql-always-on"></a>对 SQL Always On 的支持的改进

- 从安装程序添加新的同步副本<!--3127336-->：现在可以将新的次要副本节点添加到现有 SQL Always On 可用性组。 使用 Configuration Manager 安装程序来进行此更改，而不使用手动过程。 有关详细信息，请参阅[配置 SQL Server Always On 可用性组](/sccm/core/servers/deploy/configure/configure-aoag#bkmk_sync)。

- 多子网故障转移<!-- SCCMDocs-pr#3734 -->：现在可以在 SQL Server 中启用 [MultiSubnetFailover 连接字符串关键字](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover)。 你还需要手动配置站点服务器。 有关详细信息，请参阅[多子网故障转移](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#multi-subnet-failover)先决条件。

- 对分布式视图的支持<!-- SCCMDocs-pr#3792 -->：站点数据库可以托管在 SQL Server Always On 可用性组上，并且可以启用数据库复制链接来使用[分布式视图](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_dbrep)。

    > [!Note]  
    > 此更改不适用于 SQL Server 群集。

- 站点恢复可以在 SQL Always On 组中重新创建数据库。 此过程适用于手动和自动种子设定。<!-- SCCMDocs-pr#3846 -->

- 新安装程序先决条件检查：<!-- SCCMDocs-pr#3899 -->  

    - SQL 可用性组副本必须都具有相同的种子设定模式
    - SQL 可用性组副本必须正常运行

## <a name="bkmk_cloud"></a>云附加管理

### <a name="azure-active-directory-user-group-discovery"></a>Azure Active Directory 用户组发现

<!--3611956-->

现可从 Azure Active directory (Azure AD) 中发现用户组和这些组的成员。 站点之前未发现的 Azure AD 组中的用户将作为用户资源添加到 Configuration Manager 中。 如果用户组是一个安全组，则创建其资源记录。 此功能是[预发行功能](/sccm/core/servers/manage/pre-release-features)，必须启用。

有关详细信息，请参阅[配置发现方法](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_azuregroupdisco)。

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>将集合成员身份结果同步到 Azure Active Directory 组

<!--3607475-->

现在可以将集合成员身份同步到 Azure Active Directory (Azure AD) 组。 此同步是一项预发行功能。 若要启用此功能，请参阅[预发行功能](/sccm/core/servers/manage/pre-release-features)。

借助同步，可以通过基于集合成员身份结果创建 Azure AD 组成员身份来使用云中的现有本地分组规则。 只有具有 Azure Active Directory 记录的设备才会反映在 Azure AD 组中。 同时支持已联接混合 Azure AD 的设备和已联接 Azure Active Directory 的设备。

有关详细信息，请参阅[创建集合](/sccm/core/clients/manage/collections/create-collections#bkmk_aadcollsync)。


## <a name="bkmk_da"></a> 桌面分析

### <a name="readiness-insights-for-desktop-apps"></a>桌面应用的就绪情况见解

<!-- 4021225 -->

现在可以获取桌面应用程序（包括业务线应用）的更多详细见解。 以前的 App Health Analyzer 工具包现已与 Configuration Manager 客户端集成。 此集成可简化桌面分析门户中的应用就绪情况见解的部署和可管理性。

有关详细信息，请参阅[桌面分析中的兼容性评估](/sccm/desktop-analytics/compat-assessment#advanced-insights)。


### <a name="dalogscollector-tool"></a>DALogsCollector 工具

<!--4622989-->
使用 Configuration Manager 安装目录中的 DesktopAnalyticsLogsCollector.ps1 工具来帮助对桌面分析进行故障排除。 它会运行一些基本故障排除步骤，并将相关日志收集到单个工作目录中。

有关详细信息，请参阅[日志收集器](/sccm/desktop-analytics/log-collector)。


## <a name="bkmk_real"></a>实时管理

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>在 CMPivot 中添加联接、其他运算符和聚合器

<!--4054074-->

对于 CMPivot，你现在有更多的算术运算符和聚合器，还可以添加查询联接（例如可以同时使用注册表和文件）。

有关详细信息，请参阅 [CMPivot](/sccm/core/servers/manage/cmpivot#bkmk_cmpivot1906)。

### <a name="cmpivot-standalone"></a>CMPivot 独立应用

<!--3555890, 4619340, 4692885 -->

现在可以将 CMPivot 用作独立应用。 CMPivot 独立应用是**预发行功能**，只提供英语版本。 在 Configuration Manager 控制台外部运行 CMPivot，可以查看环境中设备的实时状态。 借助此变化，无需先安装控制台，即可在设备上使用 CMPivot。

可以与其他尚未在计算机上安装控制台的角色（如支持人员或安全管理员）共享功能强大的 CMPivot。 这些其他角色可以将 CMPivot 与他们传统上使用的其他工具并行使用，以查询 Configuration Manager。 通过共享此类丰富的管理数据，你们可以一起工作，共同主动解决跨角色的业务问题。

有关详细信息，请参阅 [CMPivot](/sccm/core/servers/manage/cmpivot#bkmk_standalone) 和[预发行功能](/sccm/core/servers/manage/pre-release-features#bkmk_table)。

### <a name="added-permissions-to-the-security-administrator-role"></a>已向安全管理员角色添加权限

<!--4683130-->

已向 Configuration Manager 的内置[安全管理员](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_Planroles)角色添加以下权限  ：

- 读取 SMS 脚本
- 在集合上运行 CMPivot
- 读取清单报表

有关详细信息，请参阅 [CMPivot](/sccm/core/servers/manage/cmpivot#bkmk_cmpivot_secadmin1906)。


## <a name="bkmk_content"></a>内容管理

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>客户端数据源仪表板中的传递优化下载数据

<!--3555759-->
客户端数据源仪表板现在包括[传递优化](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization)数据。 此仪表板可帮助你了解客户端在环境中获取内容的位置。

有关详细信息，请参阅[客户端数据源仪表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>将分发点用作传递优化的网络内缓存服务器

<!--3555764-->
现在可以在分发点上安装传递优化网络内缓存 (DOINC) 服务器。 通过将此内容缓存在本地，你的客户端可以从传递优化功能中受益，但你可帮助保护 WAN 链接。

此缓存服务器充当由传递优化下载的内容的按需透明缓存。 使用客户端设置以确保此服务器仅提供给本地 Configuration Manager 边界组的成员。

有关详细信息，请参阅 [Configuration Manager 中的传递优化网络内缓存](/sccm/core/plan-design/hierarchy/delivery-optimization-in-network-cache)。


## <a name="bkmk_client"></a> 客户端管理

### <a name="support-for-windows-virtual-desktop"></a>对 Windows 虚拟桌面的支持

<!--3556025-->
[Windows 虚拟桌面](https://docs.microsoft.com/azure/virtual-desktop/)是 Microsoft Azure 和 Microsoft 365 的一项预览功能。 现可使用 Configuration Manager 来管理在 Azure 中运行 Windows 的虚拟设备。

与终端服务器类似，这些虚拟设备支持多个并发的活动用户会话。 为帮助提高客户端性能，Configuration Manager 现在任何可支持多个用户会话的设备上禁用了用户策略。 即使启用用户策略，客户端任何设备（包括 Windows 虚拟桌面和终端服务器）上也会默认禁用这些用户策略。

有关详细信息，请参阅[客户端和设备支持的 OS 版本](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#windows-computers)。

### <a name="support-center-onetrace-preview"></a>支持中心 OneTrace（预览）

<!--3555962-->
OneTrace 是一个带有支持中心的新日志查看器。 它的工作方式与 CMTrace 类似，同时具有以下改进：

- 选项卡式视图
- 可停靠窗口
- 改进了搜索功能
- 无需离开日志视图，即可启用筛选器
- 可以快速识别错误群集的滚动条提示
- 可快速打开大型文件的日志

![OneTrace 日志查看器的屏幕截图](./media/3555962-onetrace.png)

有关详细信息，请参阅[支持中心 OneTrace](/sccm/core/support/support-center-onetrace)。

### <a name="configure-client-cache-minimum-retention-period"></a>配置客户端缓存最短保持期

<!--4485509-->
现在可以指定 Configuration Manager 客户端保留缓存内容的最短时间。 此客户端设置定义了在需要更多空间的情况下，Configuration Manager 代理可以从缓存中删除内容之前应等待的最短时间。 在客户端设置的“客户端缓存设置”组中，配置以下设置  ：**可以删除缓存内容前的最短持续时间（以分钟为单位）** 。

> [!Note]  
> 在同一个客户端设置组中，现有设置“在完整 OS 中启用 Configuration Manager 客户端以共享内容”现重命名为“启用为对等缓存源”   。 此设置的行为不会发生更改。  

有关详细信息，请参阅[客户端缓存设置](/sccm/core/clients/deploy/about-client-settings#client-cache-settings)。


## <a name="bkmk_comgmt"></a> 共同管理

### <a name="improvements-to-co-management-auto-enrollment"></a>共同管理自动注册的改进

- 新的共同管理设备现可根据其 Azure Active Directory (Azure AD) 设备令牌自动注册到 Microsoft Intune 服务  。 无需等待用户登录到设备，就能启动自动注册。 这项更改有助于减少[注册状态](/sccm/comanage/how-to-monitor#co-management-enrollment-status)为“挂起用户登录”的设备数量  。<!-- 4454491 -->

- 对于已将设备注册到共同管理的客户，新设备一旦满足先决条件即可立即注册。 例如，将设备联接到 Azure AD 并且安装了 Configuration Manager 客户端。<!--4321130-->

有关详细信息，请参阅[启用共同管理](/sccm/comanage/how-to-enable)。

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>用于共同管理工作负载的多个试点组

<!--3555750-->
现可为每个共同管理工作负载配置不同的试点集合。 如果能够使用不同的试点集合，那么在移动工作负载时就能采用更具体的方法。

- 在“启用”选项卡上，现可指定 Intune 自动注册集合   。
    - Intune 自动注册集合应包含所有要加入共同管理的客户端  。 它实质上是所有其他暂存集合的超集。

- 在“暂存”选项卡上，现可为每个工作负载选择一个单独的集合，而不是将一个试点集合用于所有工作负载  。

    ![使用共同管理“暂存”选项卡，可为每个工作负载选择一个集合](./media/3555750-co-management-staging-tab.png)

首次启用共同管理时，也可以使用这些选项。

有关详细信息，请参阅[启用共同管理](/sccm/comanage/how-to-enable)。

### <a name="co-management-support-for-government-cloud"></a>对政府云的共同管理支持

<!--4075452-->
美国政府客户现在可以将共同管理用于美国版 Azure政府云 (portal.azure.us)。 有关详细信息，请参阅[启用共同管理](/sccm/comanage/how-to-enable)。


## <a name="bkmk_app"></a>应用程序管理

### <a name="filter-applications-deployed-to-devices"></a>筛选部署到设备的应用程序

<!--4451056-->
以设备为目标的应用程序部署的用户类别在软件中心现显示为筛选器。 在其属性的“软件中心”页上，为应用程序指定“用户类别”   。 然后，在软件中心打开应用并查看可用的筛选器。

有关详细信息，请参阅[手动指定应用程序信息](/sccm/apps/deploy-use/create-applications#bkmk_manual-app)。

### <a name="application-groups"></a>应用程序组

<!--3555907-->
创建一组可以作为单个部署发送到用户或设备集合的应用程序。 指定的有关应用组的元数据在软件中心中显示为单个实体。 可以在组中对应用排序，以便客户端将其以特定顺序安装。

此功能是预发行功能。 若要启用此功能，请参阅[预发行功能](/sccm/core/servers/manage/pre-release-features)。

有关详细信息，请参阅[创建应用程序组](/sccm/apps/deploy-use/create-app-groups)。

### <a name="retry-the-install-of-pre-approved-applications"></a>重新安装预先审批的应用程序

<!--4336307-->
现可重试安装之前为用户或设备批准的应用。 批准选项仅适用于可用部署。 如果用户卸载应用，或者初始安装过程失败，Configuration Manager 将不会重新评估其状态并重新安装。 此功能允许技术支持人员为需要帮助的用户快速重试应用安装。

有关详细信息，请参阅[批准应用程序](/sccm/apps/deploy-use/app-approval)。

### <a name="install-an-application-for-a-device"></a>为设备安装应用程序

<!--4402180-->
从 Configuration Manager 控制台，现在可以将应用程序实时安装到设备。 此功能有助于减少对每个应用程序的单独集合的需求。

有关详细信息，请参阅[为设备安装应用程序](/sccm/apps/deploy-use/install-app-for-device)。

### <a name="improvements-to-app-approvals"></a>对应用审批的改进

<!--4224910-->
此版本包括对应用批准的以下改进：

- 如果在控制台中批准了应用请求，然后拒绝该请求，则现在可以再次批准该请求。 批准后，应用将重新安装在客户端上。  

- 在 Configuration Manager 控制台的“软件库”工作区中的“应用程序管理”下，“审批请求”节点重命名为“应用程序请求”     。<!-- SCCMDocs-pr#4028 -->

- 要删除应用批准请求，可以使用新的 WMI 方法 DeleteInstance  。 此操作不会卸载设备上的应用。 如果尚未安装，则用户无法从软件中心安装该应用。

- 调用 CreateApprovedRequest API，为设备上的应用创建预先批准的请求  。 要阻止在客户端上自动安装应用，请将 AutoInstall 参数设置为 `FALSE`  。 用户可以在软件中心中看到该应用，但系统不会自动安装该应用。

有关详细信息，请参阅[批准应用程序](/sccm/apps/deploy-use/app-approval)。


## <a name="bkmk_osd"></a> OS 部署

### <a name="task-sequence-debugger"></a>任务序列调试程序

<!--3612274-->
任务序列调试器是一种新型故障排除工具。 请将调试模式下的任务序列部署到一个设备的集合中。 这样便可通过可控方式单步执行任务序列，以帮助进行故障排除和调查。

![任务序列调试器的屏幕截图](./media/3612274-tsdebug.png)

此功能是预发行功能。 若要启用此功能，请参阅[预发行功能](/sccm/core/servers/manage/pre-release-features)。

有关详细信息，请参阅[调试任务序列](/sccm/osd/deploy-use/debug-task-sequence)。

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>在任务序列期间清除客户端缓存中的应用内容

<!--4485675-->
在“安装应用程序”任务序列步骤中，现可在步骤运行后删除客户端缓存中的应用内容  。

有关详细信息，请参阅[关于任务序列步骤](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication)。

> [!Important]  
> 将目标客户端更新至最新版本以支持该新功能。

### <a name="reclaim-sedo-lock-for-task-sequences"></a>回收任务序列的 SEDO 锁定

<!--3699337-->
如果 Configuration Manager 控制台停止响应，你可能会被锁定而无法对任务序列做出进一步更改。 尝试访问已锁定的任务序列时，现在可以放弃更改，并继续编辑对象  。

有关详细信息，请参阅[管理任务序列](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#bkmk_sedo)。

### <a name="pre-cache-driver-packages-and-os-images"></a>预缓存驱动程序包和 OS 映像

<!--4224642-->
任务序列预缓存现在包括其他内容类型。 预缓存内容以前仅适用于 OS 升级包。 现在可以使用预缓存来减少以下各项的带宽消耗：

- OS 映像
- 驱动程序包
- 包

有关详细信息，请参阅[配置预缓存内容](/sccm/osd/deploy-use/configure-precache-content)。

### <a name="improvements-to-os-deployment"></a>对 OS 部署的改进

此版本包括对 OS 部署的以下改进：

- 使用下面两个 PowerShell cmdlet 来创建和编辑[运行任务序列](/sccm/osd/understand/task-sequence-steps#child-task-sequence)步骤：<!--2839943-->

    - **New-CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- 运行任务序列时，现可更加轻松地编辑变量。 在“任务序列向导”窗口中选择任务序列后，用于编辑任务序列变量的页面中包含一个“编辑”按钮  。<!-- 4668846 --> 有关详细信息，请参阅[如何使用任务序列变量](/sccm/osd/understand/using-task-sequence-variables#bkmk_set-tswiz)。

-  “禁用 BitLocker”任务序列步骤拥有新的重启计数器。 使用此选项可指定禁用 BitLocker 的重启次数。 此更改有助于简化任务序列。 可以使用单个步骤，而不是添加此步骤的多个实例。 <!--4512937--> 有关详细信息，请参阅[禁用 BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_DisableBitLocker)。

- 将新的任务序列变量 SMSTSRebootDelayNext  与现有的 [SMSTSRebootDelay](/sccm/osd/understand/task-sequence-variables#SMSTSRebootDelay) 变量结合使用。 若要稍后执行超时值不同于第一个的任何重启，请将此新变量设置为其他值（以秒为单位）。 <!--4447680--> 有关详细信息，请参阅 [SMSTSRebootDelayNext](/sccm/osd/understand/task-sequence-variables#SMSTSRebootDelayNext)。

- 任务序列设置了新的只读变量“_SMSTSLastContentDownloadLocation”  。 此变量包含下载任务序列或尝试下载内容的最后位置。 检查此变量，而不是分析客户端日志。<!-- 2840337 -->


## <a name="bkmk_userxp"></a>软件中心

### <a name="improvements-to-software-center-tab-customizations"></a>对软件中心选项卡自定义项的改进

<!--4063773-->
现在可以在软件中心中添加最多五个自定义选项卡。 还可以编辑这些选项卡在“软件中心”中的显示顺序。

有关详细信息，请参阅[软件中心客户端设置](/sccm/core/clients/deploy/about-client-settings#software-center)。

### <a name="software-center-infrastructure-improvements"></a>软件中心基础结构的改进

<!--3555950-->

此版本包括以下软件中心基础结构改进：

- 软件中心现在可以与面向用户公开发布的应用的管理点通信。 它不再使用应用程序目录。 借助此变化，可以更轻松地从站点中删除应用程序目录。

- 过去，软件中心选择可用服务器列表中的第一个管理点。 自此版本起，它与客户端使用同一个管理点。 借助此变化，软件中心可以与客户端使用分配的主站点中的同一个管理点。

> [!Important]  
> 对软件中心和管理点的这些迭代改进将停用应用程序目录角色。
>
> - 从当前分支版本 1806 开始，不支持 Silverlight 用户体验。
> - 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。
> - 在 2019 年 10 月 31 日之后的第一个当前分支版本中，应用程序目录角色不再受支持。  

有关详细信息，请参阅[删除应用程序目录](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat)和[为软件中心制定计划](/sccm/apps/plan-design/plan-for-software-center)。

### <a name="redesigned-notification-for-newly-available-software"></a>重新为最新可用的软件设计了通知

<!--3555904-->
“新软件可用”通知将仅为给定应用程序和修订版本的用户显示一次  。 用户每次登录时将不再看到该通知。 只有应用程序发生更改或重新部署时，用户才会看到另外的通知。

有关详细信息，请参阅[创建和部署应用程序](/sccm/apps/get-started/create-and-deploy-an-application#end-user-experience)。

### <a name="more-frequent-countdown-notifications-for-restarts"></a>更频繁的重启倒计时通知

<!--3976435-->

现在，系统将通过间歇性倒计时通知更频繁地提醒最终用户待重启。 可以在“计算机重新启动”页上的“客户端设置”中定义间歇性通知的时间间隔   。 更改“指定计算机重启倒计时通知的暂停持续时间(分钟)”  的值，以配置在出现最终倒计时通知前提醒用户等待重启的频率。

此外，向用户显示一条临时通知，指示注销用户或重启计算机之前的时间间隔（以分钟为单位），这一时间间隔的最大值从 1440 分钟（24小时）增加到了 20160 分钟（两周）  。

有关详细信息，请参阅[设备重新启动通知](/sccm/core/clients/deploy/device-restart-notifications)和[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#computer-restart)。

### <a name="direct-link-to-custom-tabs-in-software-center"></a>直接指向软件中心自定义选项卡的链接

<!--4655176-->

现可向用户提供直接指向软件中心[自定义选项卡](/sccm/core/clients/deploy/about-client-settings#software-center-tab-visibility)的链接。

使用以下 URL 格式可打开软件中心的特定选项卡：

`softwarecenter:page=CustomTab1`

字符串 `CustomTab1` 是按顺序排列的第一个自定义选项卡。

例如，在 Windows“运行”窗口中键入此 URL  。

此语法还可用于打开软件中心的默认选项卡：

|命令行  |选项卡  |
|---------|---------|
|`AvailableSoftware`|应用程序|
|`Updates`|更新|
|`OSD`|操作系统|
|`InstallationStatus`|安装状态|
|`Compliance`|设备符合性|
|`Options`|选项|

有关详细信息，请参阅[软件中心选项卡的可见性](/sccm/core/clients/deploy/about-client-settings#software-center-tab-visibility)。

## <a name="bkmk_sum"></a>软件更新

### <a name="additional-options-for-wsus-maintenance"></a>WSUS 维护的其他选项

<!--4110109-->
你现在具有 Configuration Manager 为维护软件更新点正常运行而执行的其他 WSUS 维护任务。 每次同步后都会进行 WSUS 维护。 除了可以拒绝 WSUS 中的过期更新外，Configuration Manager 现在还可以：

- 从 WSUS 数据库中删除过时的更新。
- 将非聚集索引添加到 WSUS 数据库以提高 WSUS 清理性能。

有关详细信息，请参阅[软件更新维护](/sccm/sum/deploy-use/software-updates-maintenance#wsus-cleanup-starting-in-version-1906)。

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>配置软件更新的默认最长运行时间

<!--3734426-->

现可指定完成软件更新安装所需的最长时间。 可以在软件更新点上的“最长运行时间”  选项卡中指定以下各项：

- **Windows 功能更新的最长运行时间(分钟)**
- **Office 365 更新和 Windows 非功能更新的最长运行时间(分钟)**

有关详细信息，请参阅[规划软件更新](/sccm/sum/plan-design/plan-for-software-updates#bkmk_maxruntime)。

### <a name="configure-dynamic-update-during-feature-updates"></a>配置功能更新的动态更新

<!--4062619-->

使用新客户端设置来配置 Windows 10 功能更新安装期间的[动态更新](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847)。 动态更新通过指示客户端从 Internet 下载这些更新，在 Windows 安装过程中安装语言包、按需功能、驱动程序和累积更新。

有关详细信息，请参阅[软件更新客户端设置](/sccm/core/clients/deploy/about-client-settings#software-updates)和[管理 Windows 即服务](/sccm/osd/deploy-use/manage-windows-as-a-service)。

### <a name="new-windows-10-version-1903-and-later-product-category"></a>新的 Windows 10 1903 版以及更高版本产品类别

<!--4682946-->

Windows 10 1903 版以及更高版本都已经作为其自身产品添加到 Microsoft 更新中，而不像早期版本那样作为 Windows 10 产品的一部分进行添加   。 这项更改需要你执行许多手动步骤，才可确保客户端显示这些更新。 我们已采取措施减少了需要手动对新产品执行操作的步骤数量。

更新至 Configuration Manager 1906 版，并选择了 Windows 10 产品进行同步后，系统将自动执行以下操作  ：

- 已添加 Windows 10 1903 版以及更高版本产品用于进行同步操作  。
- 包含 Windows 10 产品的自动部署规则将更新为包含 Windows 10 1903 版和更高版本   。
- 维护服务计划将更新为包含 Windows 10 1903 版和更高版本产品  。

有关详细信息，请参阅[配置要同步的分类和产品](/sccm/sum/get-started/configure-classifications-and-products)、[维护服务计划](/sccm/osd/deploy-use/manage-windows-as-a-service#servicing-plan-workflow)和[自动部署规则](/sccm/sum/deploy-use/automatically-deploy-software-updates#bkmk_adr-process)。

### <a name="drill-through-required-updates"></a>钻取必需更新

<!--4224414-->
现可深入查看符合性统计信息，了解哪些设备需要特定软件更新。 若要查看设备列表，需要具有查看更新和设备所属集合的权限。 若要深入查看设备列表，请在更新的“摘要”选项卡中选择饼图旁的“查看所需更新”超链接   。 单击此超链接将转到“设备”下的临时节点，可以在其中查看需要更新的设备  。

 可在以下位置找到“查看所需更新”超链接：

   - “软件库” > “软件更新” > “所有软件更新”   
   - “软件库” > “Windows 10 维护服务” > “所有 Windows 10 更新”   
   - “软件库” > “Office 365 客户端管理” > “Office 365 更新”   

有关详细信息，请参阅[监视软件更新](/sccm/sum/deploy-use/monitor-software-updates#drill-through-required-updates)、[管理 Windows 即服务](/sccm/osd/deploy-use/manage-windows-as-a-service#drill-through-required-updates)和[管理 Office 365 专业增强版更新](/sccm/sum/deploy-use/manage-office-365-proplus-updates#drill-through-required-office-365-updates)。


## <a name="bkmk_o365"></a>Office 管理

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Office 365 专业增强版升级就绪情况仪表板

<!--4021125-->

为了帮助你确定哪些设备已准备好升级到 Office 365 专业增强版，我们推出了新的就绪情况仪表板。 它包括 Configuration Manager 当前分支版本 1902 中发布的“Office 365 专业增强版升级就绪情况”  磁贴。 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“Office 365 客户端管理”  ，再选择“Office 365 专业增强版升级就绪情况”  节点。

若要详细了解仪表板、先决条件和如何使用此数据，请参阅 [Office 365 专业增强版集成的就绪情况](/sccm/sum/deploy-use/office-365-dashboard#office-365-proplus-upgrade-readiness-dashboard)。


## <a name="bkmk_protect"></a> 保护

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Windows Defender 应用程序防护文件信任标准

<!--3555858-->

通过使用新的策略设置，用户可以信任通常在 Windows Defender 应用程序防护 (WDAG) 中打开的文件。 成功完成后，文件将在主机设备上打开，而不是在 WDAG 中打开。

有关详细信息，请参阅[创建和部署 Windows Defender 应用程序防护策略](/sccm/protect/deploy-use/create-deploy-application-guard-policy#bkmk_FM)。


## <a name="bkmk_admin"></a> Configuration Manager 控制台

### <a name="role-based-access-for-folders"></a>文件夹的基于角色的访问

<!--3600867-->

现在可以在文件夹上设置安全作用域。 如果有权访问文件夹中的对象，但无权访问文件夹，则无法查看对象。 同样，如果有权访问文件夹，但无权访问该文件夹中的对象，则无法查看对象。 右键单击文件夹，选择“设置安全作用域”  ，然后选择要应用的安全作用域。

有关详细信息，请参阅[使用 Configuration Manager 控制台](/sccm/core/servers/manage/admin-console#tips)和[配置基于角色的管理](/sccm/core/servers/deploy/configure/configure-role-based-administration#bkmk_config-folder)。

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>将 SMBIOS GUID 列添加到设备和设备集合节点

<!--4526580-->
在设备和设备集合节点中，现在可以为“SMBIOS GUID”添加新列    。 此值与 System Resource 类的“BIOS GUID”属性相同  。 它是设备硬件的唯一标识符。

### <a name="administration-service-support-for-security-nodes"></a>对安全节点的管理服务支持

<!--4223683-->
现可启用 Configuration Manager 控制台的某些节点以使用管理服务。 此项更改使控制台可以通过 HTTPS 而不是 WMI 来与 SMS 提供程序进行通信。

有关详细信息，请参阅[管理服务](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service)。

> [!Note]
> 从版本 1906 开始，站点属性上的“客户端计算机通信”选项卡现在称为“通信安全”   。<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>设备节点中的“集合”选项卡

<!--4616810-->
在“资产和符合性”工作区中，转到“设备”节点，然后选择设备   。 在详细信息窗格中，切换到新的“集合”选项卡  。此选项卡列出包含此设备的集合。

> [!Note]  
> - 此选项卡当前在“设备集合”节点下的设备子节点中不可用  。 例如，在集合上选择“显示成员”选项时，此选项卡不可用  。
> - 对于某些用户而言，此选项卡可能无法按预期方式填充。 若要查看设备所属的完整集合列表，你必须具有“完全权限管理员”安全角色  。 这是一个已知问题。 <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>应用程序节点中的“任务序列”选项卡

<!--4616810-->
在“软件库”工作区中，展开“应用程序管理”，转到“应用程序”节点，然后选择应用程序    。 在详细信息窗格中，切换到新的“任务序列”选项卡  。此选项卡列出了引用此应用程序的任务序列。

### <a name="show-collection-name-for-scripts"></a>显示脚本的集合名称

<!--4616810-->
在“监视”工作区中，选择“脚本状态”节点   。 除了列出 ID 之外，还列出了“集合名称”  。

### <a name="real-time-actions-from-device-lists"></a>设备列表中的实时操作

<!--4616810-->
有多种方法可以在“资产和符合性”工作区中的“设备”节点下显示设备列表   。

- 在“资产和符合性”  工作区中，选择“设备集合”  节点。 选择设备集合，然后选择“显示成员”操作  。 此操作将打开“设备”节点的子节点，其中包含该集合的设备列表  。  

  - 选择集合子节点时，现在可以从功能区的集合组中启动“CMPivot”  。  

- 在“监视”工作区中，选择“部署”节点   。 选择部署，然后在功能区中选择“查看状态”操作  。 在部署状态窗格中，双击总资产，以向下钻取到设备列表。  

  - 在此列表中选择设备时，现在可以从功能区的“设备”组中启动“CMPivot”和“运行脚本”   。  

### <a name="order-by-program-name-in-task-sequence"></a>按任务序列中的程序名称进行排序

<!--4616810-->
在“软件库”工作区中，展开“操作系统”，选择“任务序列”节点    。 编辑任务序列，然后选择或添加[安装包](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)步骤。 如果包包含多个程序，则下拉列表现在按字母顺序对程序进行排序。

### <a name="correct-names-for-client-operations"></a>正确的客户端操作名称

<!--4616810-->
在“监视”工作区中，选择“客户端操作”   。 现在，“切换到下一个软件更新点”操作已正确命名  。


## <a name="bkmk_deprecated"></a>弃用的功能和操作系统

在[已删除和已启用的项](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)中实施支持更改之前，先了解这些更改。

版本 1906 删除了对以下功能的支持：  

- 无法安装新的应用程序目录角色。 更新后的客户端自动使用管理点进行用户可用应用程序部署。 有关详细信息，请参阅[为软件中心制定计划](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)。

版本 1906 弃用了对以下产品的支持：  

- Windows CE 7.0
- Windows 10 移动版
- Windows 10 移动企业版


## <a name="other-updates"></a>其他更新

从此版本开始，以下功能不再预发行版本：

- [SMS 提供程序管理服务](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service)
- [Device Guard 管理](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)

 除了新增功能外，这一版还有其他变化（如缺陷修复）。 有关详细信息，请参阅 [Configuration Manager Current Branch（版本 1906）的更改摘要](https://support.microsoft.com/help/4514258)。

有关 Configuration Manager 的 Windows PowerShell cmdlet 更改的详细信息，请参阅 [PowerShell 版本 1906 发行说明](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps)。<!-- link is not live yet; will be published before this release branch -->

<!--
The following update rollup (4486457) is available in the console starting on 25 January 2019: [Update rollup for Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4486457).

### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](/sccm/core/servers/manage/updates#bkmk_supersede).
-->


## <a name="next-steps"></a>后续步骤

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](/sccm/core/servers/manage/checklist-for-installing-update-1906#early-update-ring). -->
自 2019 年 8 月 16 日起，版本 1906 公开发布，可供所有用户安装。

准备好安装此版本时，请参阅[安装 Configuration Manager 的更新](/sccm/core/servers/manage/updates)和[用于安装更新 1906 的清单](/sccm/core/servers/manage/checklist-for-installing-update-1906)。

> [!TIP]  
> 若要安装新站点，请使用 Configuration Manager 的基准版本。  
>
> 了解详细信息：
>
> - [安装新站点](/sccm/core/servers/deploy/install/installing-sites)  
> - [基准和更新版本](/sccm/core/servers/manage/updates#bkmk_Baselines)  

关于已知的重要问题，请参阅[发行说明](/sccm/core/servers/deploy/install/release-notes)。

更新站点后，还可以查看[更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1906#post-update-checklist)。
