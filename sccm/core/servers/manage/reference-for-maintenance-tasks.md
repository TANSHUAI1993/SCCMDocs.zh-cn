---
title: 维护任务参考
titleSuffix: Configuration Manager
description: 每个 Configuration Manager 站点维护任务的详细信息
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e32e96063f6c65a77e398c8434ce6b833c7be890
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70379730"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Configuration Manager 中维护任务的参考

适用范围：  System Center Configuration Manager (Current Branch)

本文列出了每个 Configuration Manager 站点维护任务的详细信息。 每个条目指定任务可用的站点类型，以及是否在默认情况下启用。

有关详细信息，请参阅[设置维护任务](/sccm/core/servers/manage/maintenance-tasks#set-up-maintenance-tasks)。  

## <a name="tasks"></a>任务

### <a name="backup-site-server"></a>备份站点服务器

使用此任务创建关键信息备份，以还原站点和 Configuration Manager 数据库。 有关详细信息，请参阅[备份 Configuration Manager 站点](/sccm/core/servers/manage/backup-and-recovery)。  

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|未启用|
|辅助站点|不可用|

### <a name="check-application-title-with-inventory-information"></a>检查应用程序标题与清单信息

使用此任务在软件清单与资产智能目录中的软件标题之间保持一致。 有关详细信息，请参阅[资产智能简介](/sccm/core/clients/manage/asset-intelligence/introduction-to-asset-intelligence)。  

|||
|---------|---------|
|**管理中心站点**|Enabled|
|主站点|不可用|
|辅助站点|不可用|

### <a name="clear-undiscovered-clients"></a>清除未发现的客户端

> [!Tip]
> 还可以在名为“清除安装标志”  控制台中看到此任务。

使用此任务删除“客户端重新发现”期间未提交检测信号发现记录的客户端的安装标记  。 安装的标记阻止向可能具有活动 Configuration Manager 客户端的计算机进行自动客户端请求安装。  

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|未启用|
|辅助站点|不可用|

### <a name="delete-aged-application-request-data"></a>删除过期的应用程序请求数据

此任务可用于从数据库中删除过期的应用程序请求。 有关详细信息，请参阅[创建和部署应用程序](/sccm/apps/get-started/create-and-deploy-an-application)。  

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-application-revisions"></a>删除过期的应用程序版本

此任务可用于删除不再被引用的应用程序版本。 有关详细信息，请参阅[如何修改和取代应用程序](/sccm/apps/deploy-use/revise-and-supersede-applications)。

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-client-download-history"></a>删除过期的客户端下载历史记录

使用此任务可删除客户端使用的下载源历史数据。 此站点使用下载源信息来填充[客户端数据源仪表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-client-operations"></a>删除过期的客户端操作

使用此任务从站点数据库中删除客户端操作的所有过期数据。 例如，此数据包括以下操作：

- 过期的客户端通知，如计算机的下载请求或用户策略
- Endpoint Protection，例如管理用户所提出的让客户端运行扫描或下载更新的定义的请求

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-client-presence-history"></a>删除过期的客户端状态历史记录
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
使用此任务删除客户端通知所记录的客户端联机状态历史记录信息。 这会删除早于指定时间的客户端联机状态的信息。 有关详细信息，请参阅[如何监视客户端](/sccm/core/clients/manage/monitor-clients)。

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>删除过期的云管理网关通信数据

使用此任务可从站点数据库删除所有通过[云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway)传递的过期通信数据。 此数据包括：

- 请求数
- 总请求字节数
- 总响应字节数
- 失败请求数
- 最大并发请求数量

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-cmpivot-results"></a>删除过期的 CMPivot 结果

使用此任务从站点数据库删除 CMPivot 查询中客户端的过期信息。 有关详细信息，请参阅[使用 CMPivot 获得实时数据](/sccm/core/servers/manage/cmpivot)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-collected-files"></a>删除过期的收集文件

使用此任务从数据库中删除已收集文件的过期信息。 此任务还从所选站点内的站点服务器文件夹结构中删除收集的文件。 默认情况下，会在站点服务器上的 **Inboxes\sinv.box\FileCol** 目录中存储收集的文件的五个最新副本。 有关详细信息，请参阅[软件清单简介](/sccm/core/clients/manage/inventory/introduction-to-software-inventory)。  

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-computer-association-data"></a>删除过期的计算机关联数据

使用此任务从数据库中删除过期的操作系统部署计算机关联数据。 在任务序列期间恢复用户状态时使用此信息。 有关详细信息，请参阅[管理用户状态](/sccm/osd/get-started/manage-user-state)。  

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-console-connection-data"></a>删除过期的控制台连接数据

此任务从站点数据库删除有关到站点的控制台连接的数据。<!-- SCCMDocs#528 -->

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-delete-detection-data"></a>删除过期的删除检测数据

此任务可用于从提取视图创建的数据库中删除过期数据。 这会删除外部系统从数据库提取数据时使用的旧数据更改信息。<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-device-wipe-record"></a>删除过期的设备擦除记录

使用此任务从数据库中删除移动设备擦除操作的过期数据。 有关详细信息，请参阅[使用远程擦除、锁定或密码重置保护数据](/sccm/mdm/deploy-use/wipe-lock-reset-devices)。  

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-discovery-data"></a>删除过期的发现数据

此任务可用于从数据库中删除过期的发现数据。 此数据可以包括来自以下内容的记录：

- 检测信号发现
- 网络发现
- Active Directory 发现方法：系统、用户和组

此任务还会移除标记为已解除授权的过期设备。 在某个站点运行此任务时，将删除与此站点关联的数据，而这些更改将复制到其他站点。 有关详细信息，请参阅[运行发现](/sccm/core/servers/deploy/configure/run-discovery)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-distribution-point-usage-stats"></a>删除过期的分发点使用情况统计信息

此任务可用于从数据库中删除存储时间长于指定时间的过期分发点数据。  

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-enrolled-devices"></a>删除过期的注册设备

使用此任务从站点数据库中删除有关未在指定时间内向该站点报告任何信息的移动设备的过期数据。

此任务适用于使用 Configuration Manager [本地 MDM](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure) 注册的设备。 有关这些设备的详细信息，请参阅[客户端和设备支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#bkmk_OnpremOS)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|未启用|
|辅助站点|不可用|

### <a name="delete-aged-ep-health-status-history-data"></a>删除过期的 EP 运行状况状态历史记录数据

使用此任务从数据库删除 Endpoint Protection (EP) 的过期状态信息。 有关详细信息，请参阅[如何监视 Endpoint Protection](/sccm/protect/deploy-use/monitor-endpoint-protection)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-exchange-partnership"></a>删除过期的 Exchange 合作关系

> [!Tip]
> > 还可以在名为“删除由 Exchange Server 连接器托管的过期设备”的控制台中看到此任务  。

使用此任务删除由 Exchange Server 连接器托管的移动设备的过期数据。 此站点根据 Exchange Server 连接器属性的“发现”选项卡上的“忽略非活动天数超过以下值的移动设备”来删除此数据   。 有关详细信息，请参阅[使用 Configuration Manager 和 Exchange 管理移动设备](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-inventory-history"></a>删除过期的清单历史记录

使用此任务从数据库中删除存储时间长于指定时间的清单数据。 有关详细信息，请参阅[如何使用资源浏览器查看硬件清单](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-log-data"></a>删除过期的日志数据

使用此任务从数据库中删除用于故障排除的过期日志数据。 此数据与 Configuration Manager 组件操作无关。  

> [!IMPORTANT]  
> 默认情况下，此任务每天将在每个站点运行。 在管理中心站点和主站点上，该任务删除 30 天以前的数据。 在辅助站点使用 SQL Server Express 时，确保此任务每天运行并删除七天均处于非活动状态的数据。  

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|**辅助站点**|Enabled|

### <a name="delete-aged-metering-data"></a>删除过期的计数数据

使用此任务从数据库中删除存储时间长于指定时间的软件计数的过期数据。 有关详细信息，请参阅 [软件计数](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-metering-summary-data"></a>删除过期的计数摘要数据

使用此任务从数据库中删除存储时间长于指定时间的软件计数的过期摘要数据。 有关详细信息，请参阅 [软件计数](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-notification-server-history"></a>删除过期的通知服务器历史记录

此任务会删除过期的客户端状态历史记录。

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-notification-task-history"></a>删除过期的通知任务历史记录

使用此任务从站点数据库中删除有关客户端通知任务的信息。 此任务适用于在指定时间未更新的数据。 有关详细信息，请参阅[客户端通知](/sccm/core/clients/manage/client-notification)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-passcode-records"></a>删除过期的密码记录

在层次结构的顶层站点中使用此任务删除有关 Android 和 Windows Phone 设备的密码重置的过期数据。 密码重置数据已加密，但包含设备的 PIN。 默认情况下，此任务处于启用状态，删除超过一天的数据。  

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-replication-data"></a>删除过期的复制数据

使用此任务从数据库中删除有关 Configuration Manager 站点之间的数据库复制的过期数据。 在更改此维护任务的配置时，配置将应用到层次结构中的每个合适的站点。 有关详细信息，请参阅[监视数据库复制](/sccm/core/servers/manage/monitor-replication)。  

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|**辅助站点**|Enabled|

### <a name="delete-aged-replication-summary-data"></a>删除过期的复制摘要数据

使用此任务从站点数据库中删除在指定时间未更新的过期复制摘要数据。 有关详细信息，请参阅[监视数据库复制](/sccm/core/servers/manage/monitor-replication)。  

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|**辅助站点**|Enabled|

### <a name="delete-aged-status-messages"></a>删除过期的状态消息

使用此任务从数据库中删除在状态筛选规则中配置的过期状态消息数据。 有关详细信息，请参阅[监视 Configuration Manager 的状态系统](/sccm/core/servers/manage/use-alerts-and-the-status-system#BKMK_MonitorSystemStatus)。

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-threat-data"></a>删除过期的威胁数据

使用此任务从数据库中删除存储时间长于指定时间的过期 Endpoint Protection 威胁数据。 有关详细信息，请参阅 [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-unknown-computers"></a>删除过期的未知计算机

当有关未知计算机的信息在一段指定时间内未更新时，使用此任务从站点数据库中将其删除。 有关详细信息，请参阅[准备未知计算机部署](/sccm/osd/get-started/prepare-for-unknown-computer-deployments)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-aged-user-device-affinity-data"></a>删除过期的用户设备相关性数据

此任务可用于从数据库中删除过期的用户设备相关性数据。 有关详细信息，请参阅[将用户和设备与用户设备相关性进行链接](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-duplicate-system-discovery-data"></a>删除重复的系统发现数据

使用此任务从站点数据库中删除由系统发现生成的任何重复记录。<!-- SCCMDocs#1339 -->

|||
|---------|---------|
|**管理中心站点**|Enabled|
|主站点|不可用|
|辅助站点|不可用|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>删除过期的 MDM 批量注册包记录

注册证书过期后使用此任务删除过期的批量注册证书和对应的配置文件。 有关详细信息，请参阅[创建证书配置文件](/sccm/protect/deploy-use/create-certificate-profiles)。

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-inactive-client-discovery-data"></a>删除非活动状态的客户端发现数据

使用此任务从数据库中删除非活动客户端的发现数据。 当客户端标记为过时并且由针对客户端状态所做的配置进行标记时，此站点会将客户端标记为不活动。

此任务仅针对作为 Configuration Manager 客户端的资源运行。 它不同于删除任何过期的发现数据记录的“删除过期的发现数据”  任务。 在站点运行此任务时，它会从层次结构内所有站点的数据库中删除数据。 有关详细信息，请参阅[如何配置客户端状态](/sccm/core/clients/deploy/configure-client-status)。

> [!IMPORTANT]  
> 启用此任务时，请将此任务配置为按大于“检测信号发现”  计划的间隔运行。 此配置允许活动客户端发送“检测信号发现”记录，以将其客户端记录标记为活动状态，从而阻止此任务删除它们。  

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|未启用|
|辅助站点|不可用|

### <a name="delete-obsolete-alerts"></a>删除过时的警报

使用此任务从数据库中删除存储时间长于指定时间的过期警报。 有关详细信息，请参阅[使用警报和状态系统](/sccm/core/servers/manage/use-alerts-and-the-status-system)。

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-obsolete-client-discovery-data"></a>删除过时的客户端发现数据

此任务可用于从数据库中删除过时的客户端记录。 标记为过时的记录通常会被同一客户端的较新记录所取代。 较新记录将成为客户端的当前记录。 有关发现的信息，请参阅[运行发现](/sccm/core/servers/deploy/configure/run-discovery)。

> [!IMPORTANT]  
> 启用此任务时，请将此任务配置为按大于“检测信号发现”计划的间隔运行。 此配置允许客户端发送“检测信号发现”记录以正确设置过时的状态。  

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|未启用|
|辅助站点|不可用|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>删除过时的林发现站点和子网

使用此任务删除有关 Active Directory 站点、子网和域的数据。 它会删除该站点在过去 30 天内 Active Directory 林发现方法未发现的数据。 此任务删除发现数据，但不影响从此发现数据创建的边界。 有关详细信息，请参阅[运行发现](/sccm/core/servers/deploy/configure/run-discovery)。

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="delete-orphaned-client-deployment-state-records"></a>删除孤立的客户端部署状态记录

使用此任务可定期清除包含客户端部署状态信息的表。 此任务会清除与已过时或已解除授权的设备关联的记录。  

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="evaluate-collection-members"></a>计算集合成员

将集合成员身份评估配置为站点组件。 有关详细信息，请参阅[站点组件](/sccm/core/servers/deploy/configure/site-components)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="monitor-keys"></a>监视键

使用此任务监视 Configuration Manager 数据库主键的完整性。 主键是唯一标识一行的列或列的组合。 该键将行与 Microsoft SQL Server 数据库表中的任何其他行区分开来。

|||
|---------|---------|
|**管理中心站点**|Enabled|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="rebuild-indexes"></a>重建索引

使用此任务重建 Configuration Manager 数据库索引。 索引是一种数据库结构，它在数据库表之上创建，以加快数据检索速度。 例如，搜索经过索引的列通常比搜索未经索引的列更快。

为了提高性能，Configuration Manager 数据库索引经常更新，以便与存储在数据库中的不断变化的数据保持同步。 此任务包括：

- 在数据库列上创建唯一性至少为 50% 的索引
- 删除列上唯一性小于 50% 的索引
- 重新生成满足数据唯一性条件的所有现有索引

|||
|---------|---------|
|**管理中心站点**|未启用|
|**主站点**|未启用|
|**辅助站点**|未启用|

### <a name="summarize-file-usage-metering-data"></a>汇总文件使用情况计数数据

此任务可用于将来自多个记录的软件计数文件使用情况数据汇总成一条总记录。 数据汇总可以压缩存储在 Configuration Manager 数据库中的数据量。

若要汇总软件计数数据和节省数据库中的磁盘空间，请配合使用此任务与“汇总软件计数每月使用数据”  任务。 有关详细信息，请参阅 [软件计数](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="summarize-installed-software-data"></a>汇总已安装软件的数据

此任务可用于将来自多个记录的已安装软件数据汇总成一条总记录。 数据汇总可以压缩存储在 Configuration Manager 数据库中的数据量。 有关详细信息，请参阅[软件清单简介](/sccm/core/clients/manage/inventory/introduction-to-software-inventory)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="summarize-monthly-usage-metering-data"></a>汇总月度使用计数数据

此任务可用于将来自多个记录的软件计数每月使用情况数据汇总成一条总记录。 数据汇总可以压缩存储在 Configuration Manager 数据库中的数据量。

若要汇总软件计数数据和节省数据库中的空间，请配合使用此任务与“汇总软件计数文件使用数据”  任务。 有关详细信息，请参阅 [软件计数](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering)。

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="update-application-available-targeting"></a>更新应用程序可用目标

使用此任务使 Configuration Manager 重新计算将策略和应用程序部署到集合中的资源的映射。 将策略或应用程序部署到集合时，Configuration Manager 将在部署的对象和集合成员之间创建初始映射。

这些映射存储在表中供快速引用。 当集合成员关系发生更改时，站点将更新这些存储的映射以反映这些更改。 但是，这些映射有可能未能同步。例如，如果站点无法正确处理一个通知文件，那么在对映射的更改中可能无法反映此更改。 此任务可以基于当前的集合成员身份刷新映射。  

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|

### <a name="update-application-catalog-tables"></a>更新应用程序目录表

此任务可用于将应用程序目录网站数据库缓存与最新的应用程序信息同步。 更改此维护任务的配置时，它适用于层次结构中的所有主站点。  

|||
|---------|---------|
|管理中心站点|不可用|
|**主站点**|Enabled|
|辅助站点|不可用|


## <a name="see-also"></a>另请参阅

[维护任务](/sccm/core/servers/manage/maintenance-tasks)
