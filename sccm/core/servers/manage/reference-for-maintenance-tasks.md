---
title: "维护任务参考 | Microsoft Docs"
description: "阅读每个 System Center Configuration Manager 站点维护任务的详细信息，以及是否默认启用这些任务。"
ms.custom: na
ms.date: 3/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
caps.latest.revision: "16"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a2d4420c2274a9b1ceb47ffd267849fdb5a55a61
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="reference-for-maintenance-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager 维护任务参考

*适用范围：System Center Configuration Manager (Current Branch)*

本主题列出了每个 System Center Configuration Manager 站点维护任务的详细信息，并指定可使用任务的站点类型。 每个条目还指示默认情况下启用还是未启用任务。 有关规划和配置站点来运行维护任务的信息，请参阅 [System Center Configuration Manager 的维护任务](../../../core/servers/manage/maintenance-tasks.md)。  

**备份站点服务器**：使用此任务准备恢复关键数据。 可以为关键信息创建备份，用于还原站点和 Configuration Manager 数据库。 有关详细信息，请参阅 [System Center Configuration Manager 的备份和恢复](../../../protect/understand/backup-and-recovery.md)。  

-   **管理中心站点**：已启用    
-   **主站点**：未启用    
-   辅助站点：不可用  

**通过清单信息检查应用程序标题**：使用此任务保持在软件清单中报告的软件标题与资产智能目录中的软件标题的一致性。 有关详细信息，请参阅 [System Center Configuration Manager 中的资产智能简介](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**清除安装标志**：使用此任务删除“客户端重新发现”期间不提交检测信号发现记录的客户端的安装标志。 安装的标记阻止向可能具有活动 Configuration Manager 客户端的计算机进行自动客户端请求安装。  

-   管理中心站点：不可用    
-   **主站点**：未启用    
-   辅助站点：不可用  

**删除过期的应用程序请求数据**：使用此任务从数据库中删除过期的应用程序请求。 有关应用程序请求的详细信息，请参阅[通过 System Center Configuration Manager 创建和部署应用程序](/sccm/apps/get-started/create-and-deploy-an-application)。  

-   管理中心站点：不可用
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除旧的客户端下载历史记录**：使用此任务可删除有关客户端使用的下载源的历史数据。 下载源信息用于填充[客户端数据源仪表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。  
-  管理中心站点 - 不可用
-    **主站点** - 已启用
-  辅助站点 - 不可用

**删除过期的客户端操作**：使用此任务从站点数据库中删除客户端操作的所有过期数据。 例如，其中包括过期或到期的客户端通知数据（例如下载计算机或用户策略的请求）和 Endpoint Protection 数据（例如客户端的管理用户运行扫描或下载更新定义的请求）。

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的客户端状态历史记录**：使用此任务删除有关客户端通知所记录的、指定时间以前的客户端联机状态的历史记录信息。 有关客户端通知的详细信息，请参阅[如何在 System Center Configuration Manager 中监视客户端](../../../core/clients/manage/monitor-clients.md)。  

-   **管理中心站点**：已启用   
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除旧的云管理网关通信数据**：使用此任务可从站点数据库删除所有关于通过[云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway)传递的旧的通信数据。 例如，这包括关于请求数、请求总字节数、总响应字节数、失败请求数和最大并发请求数的数据。  
- **管理中心站点** - 已启用
- **主站点** - 已启用
- 辅助站点 - 不可用


**删除过期的收集文件**：使用此任务从数据库中删除有关收集的文件的过期信息。 此任务还从所选站点内的站点服务器文件夹结构中删除收集的文件。 默认情况下，会在站点服务器上的 **Inboxes\sinv.box\FileCol** 目录中存储收集的文件的五个最新副本。 有关详细信息，请参阅 [System Center Configuration Manager 中的软件清单简介](/sccm/core/clients/manage/inventory/introduction-to-software-inventory)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的计算机关联数据**：使用此任务从数据库中删除过期的操作系统部署计算机关联数据。 此信息用作完成用户状态还原的一部分。 有关计算机关联的详细信息，请参阅[在 System Center Configuration Manager 中管理用户状态](../../../osd/get-started/manage-user-state.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的删除检测数据**：使用此任务从数据库中删除通过提取视图创建的过期数据。 默认情况下，禁用提取视图。 只能通过使用 Configuration Manager SDK 启用它们。 除非启用提取视图，否则没有可供此任务删除的数据。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的设备擦除记录**：使用此任务从数据库中删除有关移动设备擦除操作的过期数据。 有关擦除移动设备的信息，请参阅[使用 System Center Configuration Manager 通过远程擦除、锁定或密码重置功能帮助保护数据](/sccm/mdm/deploy-use/wipe-lock-reset-devices)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除由 Exchange Server 连接器管理的过期设备**：使用此任务删除有关使用 Exchange Server 连接器管理的移动设备的过期数据。 将依据在 Exchange Server 连接器属性的“发现”选项卡上为“忽略非活动天数超过以下值的移动设备”选项配置的间隔删除此数据。 有关详细信息，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

-   管理中心站点：不可用   
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的发现数据**：使用此任务从数据库中删除过期的发现数据。 此数据可能包括利用检测信号发现、网络发现和 Active Directory 域服务发现方法（系统、用户和组）生成的记录。 在某个站点运行此任务时，将删除与此站点关联的数据，而这些更改将复制到其他站点。 有关发现的信息，请参阅 [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的分发点使用数据**：使用此任务从数据库中删除存储时间比指定时间长的分发点的过期数据。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的 Endpoint Protection 运行状况状态历史数据**：使用此任务从数据库中删除 Endpoint Protection 的过期状态信息。 有关 Endpoint Protection 状态信息的详细信息，请参阅[如何在 System Center Configuration Manager 中监视 Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的已注册设备**：从 1602 的更新开始，默认禁用此任务。 可使用此任务从站点数据库中删除有关未在指定时间内向该站点报告任何信息的移动设备的过期数据。

此任务适用于通过 Microsoft Intune（混合）或 Configuration Manager 本地移动设备管理注册的设备。 有关使用 Configuration Manager 或 Intune 注册的设备的操作系统信息，请参阅 [System Center Configuration Manager 客户端和设备支持的操作系统](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)中的 [Microsoft Intune 注册的移动设备](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mobile-devices-enrolled-by-microsoft-intune)部分。

-   管理中心站点：不可用    
-   **主站点**：未启用    
-   辅助站点：不可用  

**删除过期的清单历史记录**：使用此任务从数据库中删除存储时间比指定时间长的清单数据。 有关清单历史记录的信息，请参阅[如何使用资源浏览器来查看 System Center Configuration Manager 中的硬件清单](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的日志数据**：使用此任务从数据库中删除用于故障排除的过期日志数据。 此数据与 Configuration Manager 组件操作无关。  

> [!IMPORTANT]  
> 默认情况下，此任务每天将在每个站点运行。 在管理中心站点和主站点，此任务会删除存在时间大于 30 天的数据。 在辅助站点使用 SQL Server Express 时，请确保此任务每天都运行并删除已 7 天不活动的数据。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   **辅助站点**：已启用  

**删除过期的通知任务历史记录**：使用此任务从站点数据库中删除指定时间内未更新的有关客户端通知任务的信息。 有关客户端通知的详细信息，请参阅 [System Center Configuration Manager 的客户端部署任务](../../../core/clients/manage/monitor-clients.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的复制摘要数据**：使用此任务从站点数据库中删除指定时间内未更新的过期的复制摘要数据。 有关详细信息，请参阅 [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) 主题中的 [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) 部分。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   **辅助站点**：已启用  

**删除过期的密码记录**：在层次结构的顶层站点中使用此任务删除有关 Android 和 Windows Phone 设备的密码重置的过期数据。 密码重置数据已加密，但包含设备的 PIN。 默认情况下启用此任务，并删除超过 1 天的数据。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的复制跟踪数据**：使用此任务从数据库中删除关于 Configuration Manager 站点之间的数据库复制的过期数据。 在更改此维护任务的配置时，配置将应用到层次结构中的每个合适的站点。 有关详细信息，请参阅 [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) 主题中的 [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) 部分。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   **辅助站点**：已启用  

**删除过期的软件计数数据**：使用此任务从数据库中删除存储时间比指定时间长的软件计数过期数据。 有关详细信息，请参阅 [System Center Configuration Manager 中的软件计数](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的软件计数摘要数据**：使用此任务从数据库中删除存储时间比指定时间长的软件计数的过期摘要数据。 有关详细信息，请参阅 [System Center Configuration Manager 中的软件计数](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的状态消息**：使用此任务从数据库中删除在状态筛选规则中配置的过期状态消息数据。 有关信息，请参阅[使用 System Center Configuration Manager 的警报和状态系统](../../../core/servers/manage/use-alerts-and-the-status-system.md)主题中的“监视 Configuration Manager 的状态系统”部分。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的威胁数据**：使用此任务从数据库中删除存储时间比指定时间长的过期 Endpoint Protection 威胁数据。 有关 Endpoint Protection 的信息，请参阅 [System Center Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的未知计算机**：使用此任务从站点数据库中删除指定时间内未更新的有关未知计算机的信息。 有关详细信息，请参阅[在 System Center Configuration Manager 中准备未知计算机部署](../../../osd/get-started/prepare-for-unknown-computer-deployments.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期的用户设备相关性数据**：使用此任务从数据库中删除过期的用户设备相关性数据。 有关详细信息，请参阅[在 System Center Configuration Manager 中将用户和设备与用户设备相关性相链接](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过期 MDM 批量注册包记录**：注册证书过期后使用此任务删除旧的批量注册证书和对应的配置文件。 有关详细信息，请参阅[创建证书配置文件](/sccm/protect/deploy-use/create-certificate-profiles)。
-   **管理中心站点**：已启用
-   **主站点**：已启用
-   辅助站点：不可用

**删除非活动的客户端发现数据**：使用此任务从数据库中删除非活动的客户端发现数据。 当客户端标记为过时并且由针对客户端状态所做的配置进行标记时，会将客户端标记为不活动。

此任务仅针对作为 Configuration Manager 客户端的资源运行。 它不同于删除任何过期的发现数据记录的“删除过期的发现数据”任务。 在站点运行此任务时，它会从层次结构内所有站点的数据库中删除数据。 有关详细信息，请参阅 [How to configure client status in System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md)。  

> [!IMPORTANT]  
> 启用此任务时，请将此任务配置为按大于“检测信号发现”计划的间隔运行。 这允许活动客户端发送“检测信号发现”记录，以将其客户端记录标记为活动状态，从而阻止此任务删除它们。  

-   管理中心站点：不可用    
-   **主站点**：未启用    
-   辅助站点：不可用  

**删除过时的警报**：使用此任务从数据库中删除存储时间比指定时间长的过期警报。 有关详细信息，请参阅 [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md)。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除过时的客户端发现数据**：使用此任务从数据库中删除过时的客户端记录。 标记为过时的记录通常会被同一客户端的较新记录所取代。 较新记录将成为客户端的当前记录。 有关发现的信息，请参阅 [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md)。  

> [!IMPORTANT]  
> 启用此任务时，请将此任务配置为按大于“检测信号发现”计划的间隔运行。 这允许客户端发送“检测信号发现”记录以正确设置过时的状态。  

-   管理中心站点：不可用    
-   **主站点**：未启用    
-   辅助站点：不可用  

**删除过时的林发现站点和子网**：使用此任务删除在最近 30 天内 Active Directory 林发现方法尚未发现的 Active Directory 站点、子网和域的数据。 此任务删除发现数据，但不影响利用此发现数据创建的边界。 有关详细信息，请参阅 [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md)。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**删除孤立客户端部署状态记录**：使用此任务可定期清除包含客户端部署状态信息的表。 此任务将清除与已过时或已解除授权的设备关联的记录。  
-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   辅助站点：不可用

**删除未使用的应用程序修订版本**：使用此任务删除不再被引用的应用程序修订版本。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中修订和取代应用程序](../../../apps/deploy-use/revise-and-supersede-applications.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**评估集合成员**：将集合成员身份评估配置为站点组件。 有关站点组件的信息，请参阅 [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**监视键**：使用此任务监视 Configuration Manager 数据库主键的完整性。 主键是一列或多列的组合，它在 Microsoft SQL Server 数据库表中唯一地标识一行，并将它与任何其他行区分开来。  

-   **管理中心站点**：已启用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**重建索引**：使用此任务重建 Configuration Manager 数据库索引。 索引是一种数据库结构，它在数据库表之上创建，以加快数据检索速度。 例如，搜索经过索引的列通常比搜索未经索引的列更快。

为了改善性能，Configuration Manager 数据库索引会频繁更新，以便与存储在数据库中不断变化的数据保持同步。 此任务在数据库列上创建唯一性至少达到 50% 的索引，删除唯一性低于 50% 的列索引，以及重建所有符合数据唯一性条件的现有索引。  

-   **管理中心站点**：未启用    
-   **主站点**：未启用    
-   **辅助站点**：未启用  

**汇总已安装软件的数据**：使用此任务将来自多个记录的已安装软件的数据汇总成一个总记录。 数据汇总可以压缩存储在 Configuration Manager 数据库中的数据量。 有关详细信息，请参阅 [System Center Configuration Manager 中的软件清单简介](../../clients/manage/inventory\introduction-to-software-inventory.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**汇总软件计数文件使用数据**：使用此任务将软件计数文件使用情况的多个记录的数据汇总到一个总记录中。 数据汇总可以压缩存储在 Configuration Manager 数据库中的数据量。

可配合使用此任务与“汇总软件计数每月使用数据”任务，以便汇总软件计数数据以及节省 Configuration Manager 数据库中的磁盘空间。 有关详细信息，请参阅 [System Center Configuration Manager 中的软件计数](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**汇总软件计数每月使用数据**：使用此任务将软件计数每月使用情况的多个记录的数据汇总到一个总记录中。 数据汇总可以压缩存储在 Configuration Manager 数据库中的数据量。

可配合使用此任务与“汇总软件计数文件使用数据”任务，以便汇总软件计数数据以及节省 Configuration Manager 数据库中的空间。 有关详细信息，请参阅 [System Center Configuration Manager 中的软件计数](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**更新应用程序的可用目标**：使用此任务使 Configuration Manager 重新计算将策略和应用程序部署到集合中的资源的映射。 将策略或应用程序部署到集合时，Configuration Manager 将在部署的对象和集合成员之间创建初始映射。

这些映射存储在表中供快速引用。 当集合成员身份更改时，将更新这些存储的映射以反映这些更改。 但是，这些映射有可能未能同步。 例如，如果站点无法正确处理一个通知文件，那么在对映射的更改中可能无法反映此更改。 此任务可以基于当前的集合成员身份刷新映射。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  

**更新应用程序目录表**：使用此任务将应用程序目录网站数据库缓存与最新的应用程序信息进行同步。 在更改此维护任务的配置时，配置将应用到层次结构中的所有主站点。  

-   管理中心站点：不可用    
-   **主站点**：已启用    
-   辅助站点：不可用  
