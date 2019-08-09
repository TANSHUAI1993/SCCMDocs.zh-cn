---
title: 支持的 SQL Server 版本
titleSuffix: Configuration Manager
description: 获取托管 Configuration Manager 站点数据库的 SQL Server 版本和配置要求。
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b88ca3361390f8577dc44f2a3fd9640d5a49ad7d
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536815"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Configuration Manager 支持的 SQL Server 版本

*适用于：System Center Configuration Manager (Current Branch)*

每个 System Center Configuration Manager 站点都需要受支持的 SQL Server 版本和配置来托管站点数据库。  



##  <a name="bkmk_Instances"></a> SQL Server 实例和位置  
 
### <a name="central-administration-site-and-primary-sites"></a>管理中心站点和主站点  
站点数据库必须使用 SQL Server 的完整安装。  

SQL Server 可位于以下位置：  

- 站点服务器计算机。  
- 远离站点服务器的计算机。  

支持以下实例：  

- SQL Server 的默认或已命名实例。  
- 多个实例配置。  
- SQL Server 群集。 请参阅[使用 SQL Server 群集托管站点数据库](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database)。
- SQL Server AlwaysOn 可用性组。 有关详细信息，请参阅[高可用性站点数据库的 SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。


### <a name="secondary-sites"></a>辅助站点  
站点数据库可使用完整安装的 SQL Server 或 SQL Server Express 的默认实例。  

SQL Server 必须位于站点服务器计算机上。  


### <a name="limitations-to-support"></a>支持限制   
不支持下列配置：
- 网络负载均衡 (NLB) 群集配置中的 SQL Server 群集
- 群集共享卷 (CSV) 上的 SQL Server 群集
- SQL Server 数据库镜像技术和对等复制

SQL Server 事务复制仅支持将对象复制到配置为使用[数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)的管理点。  



##  <a name="bkmk_SQLVersions"></a> 支持的 SQL Server 版本  
在含有多个网站的层次结构中，各个网站可以使用不同版本的 SQL Server 托管网站数据库。 只要满足以下各项：
- Configuration Manager 支持你使用的 SQL Server 版本。
- Microsoft 仍支持你使用的 SQL Server 版本。
- SQL Server 支持在两个 SQL Server 版本之间进行复制。 例如，SQL Server 不支持在 SQL Server 2008 R2 和 SQL Server 2016 之间进行复制。 有关详细信息，请参阅 [SQL Server 复制中的弃用功能](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication)。



除非另行指定，否则 Configuration Manager 的所有活动版本均支持以下版本的 SQL Server。 如果支持新的 SQL Server 版本或添加 Service Pack，则将显示添加该支持的 Configuration Manager 版本。 同样，如果弃用支持，则查找有关受影响的 Configuration Manager 版本的详细信息。   

对特定 SQL Server Service Pack 的支持包括累积更新，除非中断对基本 Service Pack 版本的后向兼容性。 如果没有另行说明 Service Pack 版本，则支持是针对不带 Service Pack 的 SQL Server 版本。 将来如果针对某个 SQL Server 版本发布 Service Pack，单独的支持声明将在支持该新的 Service Pack 版本前宣布。


> [!IMPORTANT]  
> 为管理中心站点上的数据库使用 SQL Server Standard 时，会限制层次结构可支持的客户端总数。 请参阅 [调整大小和扩展数量](/sccm/core/plan-design/configs/size-and-scale-numbers)。

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017：Standard、Enterprise  
自 [Configuration Manager 版本 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710) 起，此版本的 SQL Server 最低可与以下站点的[累积更新版本 2](https://support.microsoft.com/help/4052574) 一起使用： 

- 管理中心站点  
- 主站点  
- 辅助站点  
  <!--SMS.498506-->

### <a name="sql-server-2016-sp2-standard-enterprise"></a>SQL Server 2016 SP2：Standard、Enterprise  
<!--514985-->
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 管理中心站点  
- 主站点  
- 辅助站点  

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1：Standard、Enterprise  
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 管理中心站点  
- 主站点  
- 辅助站点  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016：Standard、Enterprise  
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 管理中心站点  
- 主站点  
- 辅助站点  

### <a name="sql-server-2014-sp3-standard-enterprise"></a>SQL Server 2014 SP3：Standard、Enterprise  
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 管理中心站点  
- 主站点  
- 辅助站点

### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2：Standard、Enterprise  
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 管理中心站点  
- 主站点  
- 辅助站点

### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1：Standard、Enterprise  
 可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 管理中心站点  
- 主站点  
- 辅助站点

### <a name="sql-server-2012-sp4-standard-enterprise"></a>SQL Server 2012 SP4：Standard、Enterprise  
 可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 管理中心站点  
- 主站点  
- 辅助站点  

### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3：Standard、Enterprise  
 可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 管理中心站点  
- 主站点  
- 辅助站点  

### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3：Standard、Enterprise、Datacenter     
不支持此版本的 SQL Server。 有关详细信息，请参阅 [SQL Server 版本作为站点数据库的已弃用支持](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#sql-server)。  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express   
自 [Configuration Manager 版本 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710) 起，此版本的 SQL Server 最低可与以下站点的[累积更新版本 2](https://support.microsoft.com/help/4052574) 一起使用：
- 辅助站点
<!--SMS.498506-->

### <a name="sql-server-2016-express-sp2"></a>SQL Server 2016 Express SP2  
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：
- 辅助站点

### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：
- 辅助站点

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：
- 辅助站点

### <a name="sql-server-2014-express-sp3"></a>SQL Server 2014 Express SP3   
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 辅助站点  

### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 辅助站点  

### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 辅助站点  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
可将此版本的 SQL Server 与以下站点的非最低累积更新版本一起使用：  

- 辅助站点  


## <a name="bkmk_SQLConfig"></a> SQL Server 所需的配置

用于站点数据库（包括 SQL Server Express）的 SQL Server 的所有安装都需要以下配置。 Configuration Manager 将 SQL Server Express 作为辅助站点安装的一部分进行安装时，将自动创建这些配置。  

### <a name="sql-server-architecture-version"></a>SQL Server 体系结构版本

Configuration Manager 需要 64 位版本的 SQL Server 以托管站点数据库。  

### <a name="database-collation"></a>数据库排序规则

在每个站点上，用于站点和站点数据库的 SQL Server 实例必须使用以下排序规则：**SQL_Latin1_General_CP1_CI_AS**。  

对于中国 GB18030 标准，Configuration Manager 支持此排序规则的两个例外情况。 有关详细信息，请参阅[国际支持](/sccm/core/plan-design/hierarchy/international-support)。  

### <a name="database-compatibility-level"></a>数据库兼容性级别

Configuration Manager 要求站点数据库的兼容性级别不低于 Configuration Manager 版本支持的最低 SQL Server 版本。 例如，从版本 1702 开始，需要有高于或等于 110 的[数据库兼容性级别](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database)。 <!-- SMS.506266-->

### <a name="sql-server-features"></a>SQL Server 功能

仅“数据库引擎服务”  功能是每个站点服务器所必需的。  

Configuration Manager 数据库复制不需要“SQL Server 复制”  功能。 但是，当你使用[管理点的数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)时，则需进行此 SQL Server 配置。  

### <a name="windows-authentication"></a>Windows 身份验证

Configuration Manager 需要“Windows 身份验证”  来验证与数据库的连接。  

### <a name="sql-server-instance"></a>SQL Server 实例

为每个站点使用专用的 SQL Server 实例。 此实例可以为命名实例  或默认实例  。  

### <a name="sql-server-memory"></a>SQL Server 内存

使用 SQL Server Management Studio 保留用于 SQL Server 的内存。 在“服务器内存选项”下设置“最小服务器内存”   。 有关如何配置此设置的详细信息，请参阅 [SQL Server 内存服务器配置选项](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options)。  

- **对于作为站点服务器安装在同一计算机上的数据库服务器**：将用于 SQL Server 的内存限制为，可用的可寻址系统内存的 50% 到 80%。  

- **对于专用的数据库服务器（远离站点服务器）** ：将用于 SQL Server 的内存限制为，可用的可寻址系统内存的 80% 到 90%。  

- 对于使用中的每个 SQL Server 实例的缓冲池内存预留  ：  

  - 对于中央管理站点：至少设置 8 GB。  
  - 对于主站点：至少设置 8 GB。  
  - 对于辅助站点：至少设置 4 GB。  

### <a name="sql-nested-triggers"></a>SQL 嵌套触发器

必须启用 SQL 嵌套触发器。 有关详细信息，请参阅[配置嵌套触发器服务器配置选项](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option)

### <a name="sql-server-clr-integration"></a>SQL Server CLR 集成

站点数据库要求启用 SQL Server 公共语言运行时 (CLR)。 此选项在 Configuration Manager 安装时会自动启用。 有关 CLR 的详细信息，请参阅 [SQL Server CLR 集成简介](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Service Broker (SSB)

站点间复制和单个主站点都需要 SQL Server Service Broker。

### <a name="trustworthy-setting"></a>可信设置

Configuration Manager 会自动启用 SQL [可信数据库属性](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property)。 Configuration Manager 要求此属性为“打开”  。


##  <a name="bkmk_optional"></a> SQL Server 可选配置  
以下配置对使用完整 SQL Server 安装的每个数据库是可选的。  

### <a name="sql-server-service"></a>SQL Server 服务  
你可以将 SQL Server 服务配置为使用以下账户运行：  

- 低权限域用户  帐户：  

  - 此配置是最佳做法，并且可能要求你手动注册该帐户的服务主体名称 (SPN)。  

- 运行 SQL Server 的计算机的**本地系统**帐户：  

  - 使用本地系统帐户简化配置过程。  
  - 使用本地系统帐户时，Configuration Manager 将自动注册 SQL Server 服务的 SPN。  
  - 为 SQL Server 服务使用本地系统帐户不是 SQL Server 最佳做法。  

运行 SQL Server 的计算机不使用其本地系统帐户运行 SQL Server 服务时，配置帐户的 SPN，该帐户在 Active Directory 域服务中运行 SQL Server 服务。 （使用系统帐户时，将为你自动注册 SPN。）

有关站点数据库 SPN 的信息，请参阅[管理站点数据库服务器的 SPN](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_SPN)。  

有关如何更改 SQL Server 服务使用的帐户的信息，请参阅 [SCM 服务 - 更改服务启动帐户](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account)。  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  
SQL Server Reporting Services 是安装可运行报表的 Reporting Services 点的必需条件。  

> [!IMPORTANT]  
> 将以前版本的 SQL Server 升级后，可能会看到以下错误：*报表生成器不存在*。  
> 要修复此错误，必须重新安装 Reporting Services 点站点系统角色。  

### <a name="sql-server-ports"></a>SQL Server 端口  
对于与 SQL Server 数据库引擎的通信和站点间复制，可以使用默认的 SQL Server 端口配置，也可以指定自定义端口：  

- **站点间通信**使用 SQL Server Service Broker，它默认使用端口 TCP 4022。  
- SQL Server 数据库引擎与各种 Configuration Manager 站点系统角色之间的站点内通信  默认使用端口 TCP 1433。 下列站点系统角色直接与 SQL Server 数据库进行通信：  

  - 管理点  
  - SMS 提供程序计算机  
  - Reporting Services 点  
  - 站点服务器  

运行 SQL Server 的计算机托管多个站点中的数据库时，每个数据库必须使用独立的 SQL Server 实例。 此外，每个实例必须配置为使用一组唯一的端口。  

> [!WARNING]  
> Configuration Manager 不支持动态端口。 由于 SQL Server 命名实例默认情况下使用动态端口来连接到数据库引擎，因此，在使用命名实例时，必须手动配置要用于站点内通信的静态端口。  

如果在运行 SQL Server 的计算机上启用防火墙，请确保将防火墙配置为不阻止你的部署使用的端口，以及位于与 SQL Server 通信的计算机之间的网络上任何位置处的端口。  

有关如何将 SQL Server 配置为使用特定端口的示例，请参阅[将服务器配置为侦听特定的 TCP 端口](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)。  



## <a name="upgrade-options-for-sql-server"></a>SQL Server 的升级选项

如果需要升级 SQL Server 版本，请使用以下方法（难度从简单到复杂）：  

- [就地升级 SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#to-upgrade-sql-server-on-the-site-database-server)（推荐）  

- 在新计算机上安装新版本的 SQL Server，然后使用 Configuration Manager 设置的[数据库移动选项](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_dbconfig)将站点服务器指向新的 SQL Server  

- 使用[备份和恢复](/sccm/protect/understand/backup-and-recovery)。 支持在 SQL 升级方案中使用备份和恢复。 在查看[恢复站点前的注意事项](/sccm/protect/understand/recover-sites#considerations-before-recovering-a-site)时，可以忽略 SQL 版本控制要求。 
