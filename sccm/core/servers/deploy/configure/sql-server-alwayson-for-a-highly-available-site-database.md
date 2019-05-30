---
title: SQL Server AlwaysOn
titleSuffix: Configuration Manager
description: 计划将 SQL Server AlwaysOn 可用性组与 Configuration Manager 配合使用
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f70373f1fea7928e801c0ccdbbe75cf96e54d20
ms.sourcegitcommit: f531d0a622f220739710b2fe6644ea58d024064a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65933523"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>准备将 SQL Server AlwaysOn 可用性组与 Configuration Manager 配合使用

适用范围：  System Center Configuration Manager (Current Branch)

本文介绍如何准备 Configuration Manager 以使用 SQL Server AlwaysOn 可用性组。 此功能为站点数据库提供高可用性和灾难恢复解决方案。  

Configuration Manager 支持在以下位置使用可用性组：
- 主站点和管理中心站点。
- 本地环境或 Microsoft Azure 中。

在 Microsoft Azure 中使用可用性组时，可使用 Azure 可用性集  进一步提升站点数据库的可用性。 有关 Azure 可用性集的详细信息，请参阅 [管理虚拟机的可用性](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/)。

> [!Important]
>  在继续之前，熟悉如何配置 SQL Server 和 SQL Server 可用性组。 以下信息引用 SQL Server 文档库和过程。



## <a name="supported-scenarios"></a>支持的方案

以下是将可用性组与 Configuration Manager 配合使用的支持方案。 有关每个方案的详细信息和过程，请参阅[配置 Configuration Manager 的可用性组](/sccm/core/servers/deploy/configure/configure-aoag)。

- [创建与 Configuration Manager 配合使用的可用性组](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group)  
- [配置站点以使用可用性组](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group)  
- [可以从托管站点数据库的可用性组添加或删除同步副本成员](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members)  
- [配置异步提交副本](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca)  
- [从异步提交副本恢复站点](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site)  
- [可以将站点数据库从可用性组移到独立 SQL Server 的默认实例或命名实例](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group)  



## <a name="prerequisites"></a>先决条件

将以下先决条件应用到所有方案。 如果将其他先决条件应用到特定方案，将针对该方案详细介绍这些先决条件。   

### <a name="configuration-manager-accounts-and-permissions"></a>Configuration Manager 帐户和权限

#### <a name="site-server-to-replica-member-access"></a>站点服务器到副本成员访问权限   
站点服务器的计算机帐户必须是可用性组成员计算机上“本地管理员”  组的成员。


### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>版本  
可用性组中的每个副本必须运行由 Configuration Manager 版本支持的 SQL Server 版本。 如果 SQL Server 支持，可用性组的不同节点可以运行不同版本的 SQL Server。 有关更多信息，请参阅 [Configuration Manager 支持的 SQL Server 版本](/sccm/core/plan-design/configs/support-for-sql-server-versions)。<!--SCCMDocs issue 656-->

#### <a name="edition"></a>版本  
使用 SQL Server 企业  版。

#### <a name="account"></a>帐户  
每个 SQL Server 实例可以在域用户帐户（服务帐户  ）或非域帐户下运行。 组中的每个副本可以具有不同的配置。 

- 使用具有最低权限的帐户。 有关详细信息，请参阅 [SQL Server 安装的安全注意事项](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)。  

- 有关配置服务帐户和 SQL Server 权限的详细信息，请参阅[配置 Windows 服务帐户和权限](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions)。  

- 要使用非域帐户，必须使用证书。 有关详细信息，请参阅[使用数据库镜像端点证书 (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql)。  

- 有关详细信息，请参阅[为 AlwaysOn 可用性组创建数据库镜像终结点](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell)。  


### <a name="availability-group-configurations"></a>可用性组配置

#### <a name="replica-members"></a>副本成员  
- 此可用性组必须具有一个主要副本。  

- 在可用性组中使用与 SQL Server 版本支持的数量和类型相同的副本。

- 可以使用异步提交副本来恢复同步副本。 有关详细信息，请参阅[站点数据库恢复选项](/sccm/core/servers/manage/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption)。  

    > [!Warning]  
    > Configuration Manager 不支持*故障转移*使用异步提交副本作为站点数据库。 有关详细信息，请参阅[故障转移和故障转移模式（AlwaysOn 可用性组）](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups?view=sql-server-2014)。  

Configuration Manager 不会验证异步提交副本的状态来确认它是否为最新状态。 使用异步提交副本作为站点数据库可能会将站点和数据的完整性置于危险之中。 根据设计，此类副本可能不会同步。有关详细信息，请参阅 [SQL Server AlwaysOn 可用性组概述](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)。

每个副本成员都必须进行以下配置：

- 使用默认实例  或命名实例   

- “主角色中的连接”设置为“允许所有连接”    

- “可读次要副本”  设置为“是”   

- 已启用“手动故障转移”      

  > [!TIP]
  >  Configuration Manager 设置为“自动故障转移”  时，支持使用可用性组同步副本。 在以下情况下设置“手动故障转移”  ：
  >  -  运行 Configuration Manager 安装程序以指定在可用性组中使用站点数据库。  
  >  -  安装任何 Configuration Manager 更新。 （不仅仅是安装适用于站点数据库的更新）。  

#### <a name="replica-member-location"></a>副本成员位置
可用性组中的所有副本要么在本地托管，要么全部托管在 Microsoft Azure 上。 不支持包含本地成员或 Azure 中成员的组。     

Configuration Manager 安装程序需要连接到每个副本。 在 Azure 中设置可用性组，且组处于内部或外部负载均衡器后面时，开放以下默认端口：   

- RPC 端点映射程序：TCP 135    

- SQL Server Service Broker：TCP 4022   

- SQL over TCP：TCP 1433    


安装完成后，以下端口必须在 Configuration Manager 中保持开放状态：  

- SQL Server Service Broker：TCP 4022   

- SQL over TCP：TCP 1433   

可以为这些配置使用自定义端口。 在可用性组中的所有副本上，在终结点处使用相同的自定义端口。


#### <a name="listener"></a>侦听器   
此可用性组必须具有至少一个“可用组侦听器”  。 将 Configuration Manager 配置为使用可用性组中的站点数据库时，将使用此侦听器的虚拟名称。 尽管可用性组可以包含多个侦听器，但 Configuration Manager 只能使用其中一个。 有关详细信息，请参阅[创建或配置 SQL Server 可用性组侦听器](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server)。

#### <a name="file-paths"></a>文件路径   
运行 Configuration Manager 安装程序以配置站点使用可用性组中的数据库时，每个次要副本服务器的 SQL Server 文件路径必须和当前主要副本上的站点数据库文件的文件路径相同。 如果不存在相同的路径，则安装程序无法将可用性组实例添加为站点数据库的新位置。  

本地 SQL Server 服务帐户必须具有对此文件夹的“完全控制”  权限。

仅当使用 Configuration Manager 安装程序指定可用性组中的数据库实例时，次要副本服务器才需要此文件路径。 在安装程序完成在可用性组中站点数据库的配置后，你可以从次要副本服务器删除未使用的路径。

例如，考虑以下情况：

- 创建可使用三个 SQL Server 的可用性组。  

- 主副本服务器是新安装的 SQL Server 2014。 默认情况下，它将数据库 .MDF 和 .LDF 文件存储在 `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` 中。  

- 将这两个次要副本服务器从早期版本升级到了 SQL Server 2014。 通过升级，这些服务器将保留用于存储数据库文件的原始文件路径：`C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`。  

- 在将站点数据库移至此可用性组之前，在每个次要副本服务器上，创建以下文件路径：`C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`。 此路径是在主要副本上使用的路径副本，即使次要副本不会使用此文件位置。  

- 然后向每个次要副本上的 SQL Server 服务帐户授予对该服务器上新创建文件位置的完全控制访问权限。  

- 现在，便可以成功运行 Configuration Manager 安装程序以配置站点使用可用性组中的站点数据库。  

#### <a name="configure-the-database-on-a-new-replica"></a>在新副本上配置数据库   
 为每个副本的数据库配置以下设置：  

- 启用“CLR 集成”  。 有关详细信息，请参阅 [CLR 集成](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling)。  

- 将“最大文本复制大小”  设置为 `2147483647`  

- 将数据库所有者设置为“SA 帐户”   

- 打开  “可信”  设置。 有关详细信息，请参阅[可信数据库属性](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property)。   

- 启用“Service Broker”   

仅在主要副本上进行这些配置。 若要配置次要副本，首先将主要副本故障转移到次要副本。 此操作使得次要副本成为新的主要副本。   


### <a name="verification-script"></a>验证脚本

运行以下 SQL 脚本来验证主要副本和次要副本的数据库配置。 将该次要副本更改为主要副本才能修复次要副本上的某个问题。

```SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```



## <a name="limitations-and-known-issues"></a>限制和已知问题

以下限制适用于所有方案。   

#### <a name="unsupported-sql-server-options-and-configurations"></a>不受支持的 SQL Server 选项和配置

- **基本可用性组**：随着 SQL Server 2016 Standard 版本的推出，Basic 可用性组不支持对次要副本的读取访问。 配置需要此访问权限。 有关详细信息，请参阅 [Basic SQL Server 可用性组](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017)。  

- **故障转移群集实例**：与 Configuration Manager 一起使用的副本不支持故障转移群集实例。 有关详细信息，请参阅 [SQL Server AlwaysOn 故障转移群集实例](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server)。  

- **MultiSubnetFailover**：不支持在多子网配置中将可用性组与 Configuration Manager 结合使用。 还不能使用 [MutliSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) 关键字连接字符串。  

#### <a name="sql-servers-that-host-additional-availability-groups"></a>托管其他可用性组的 SQL Server
<!--SCCMDocs issue 649-->
SQL Server 承载除用于 Configuration Manager 的组之外的一个或多个可用性组时，它在运行 Configuration Manager 安装程序时需要特定的设置。 还需要这些设置来安装 Configuration Manager 更新。 每个可用性组中的每个副本必须具有以下配置：

- 手动故障转移  
- 允许任何只读连接  

#### <a name="unsupported-database-use"></a>不支持使用的数据库

- **Configuration Manager 仅支持可用性组中的站点数据库：** SQL Server Always On 可用性组中的 Configuration Manager 不支持以下数据库：  
    - 报表数据库  
    - WSUS 数据库  

- **预先存在的数据库：** 不能使用在副本上创建的新数据库。 在配置可用性组时，将现有 Configuration Manager 数据库的副本还原为主要副本。  

#### <a name="setup-errors-in-configmgrsetuplog"></a>ConfigMgrSetup.log 中的安装错误  
运行 Configuration Manager 安装程序将站点数据库移到可用性组时，它会尝试处理可用性组的次要副本上的数据库角色。 ConfigMgrSetup.log  文件将显示以下错误：  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

这些错误可以忽略。

#### <a name="site-expansion"></a>站点扩展
<!--SCCMDocs issue 568-->
如果为独立主站点配置站点数据库以使用 SQL Always On，则不能扩展此站点以包含管理中心站点。 如果尝试执行此过程，将失败。 若要展开站点，暂时从可用性组中删除主站点数据库。



## <a name="changes-for-site-backup"></a>站点备份的更改

### <a name="backup-database-files"></a>备份数据库文件
  
当站点数据库使用某个可用性组时，运行内置“备份站点服务器”  维护任务来备份常规 Configuration Manager 设置和文件。 不要使用由该备份创建的 .MDF 或 .LDF 文件。 相反，通过使用 SQL Server 直接备份这些数据库文件。


### <a name="transaction-log"></a>事务日志  

将站点数据库的恢复模型设置为“完整”  。 此配置是在可用性组中使用 Configuration Manager 的必要设置。 计划监视和维护站点数据库事务日志的大小。 在完整恢复模型下，在进行数据库或事务日志的完整备份后，才对事务进行强化。 有关详细信息，请参阅 [SQL Server 数据库的备份与还原](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases)。



## <a name="changes-for-site-recovery"></a>站点恢复的更改

如果可用性组至少有一个节点仍正常工作，则使用“跳过数据库恢复(当站点数据库未受影响时使用此选项)”  站点恢复选项。

在可用性组的所有节点都已丢失时，必须重新创建可用性组才能恢复站点。 Configuration Manager 无法重新生成或还原可用性节点。 重新创建组、还原备份，并重新配置 SQL。 然后使用站点恢复选项“跳过数据库恢复(在站点数据库未受到影响的情况下使用此选项)  ”。

有关详细信息，请参阅[备份和恢复](/sccm/core/servers/manage/backup-and-recovery)。



## <a name="changes-for-reporting"></a>报表的更改

### <a name="install-the-reporting-service-point"></a>安装 Reporting Services 点

Reporting Services 点不支持使用可用性组的侦听器虚拟名称。 此外，它不支持在 SQL Server AlwaysOn 可用性组中托管其数据库。  

- 默认情况下，Reporting Services 点安装将“站点数据库服务器名称”  设置为指定作为侦听器的虚拟名称。 更改此设置以指定可用性组中的计算机名称和副本的实例。  

- 若要在副本节点处于脱机状态时，卸载报告并提高可用性，请考虑在每个副本节点上安装其他 Reporting Services 点。 然后将每个 Reporting Services 点配置为使用其自己的计算机名称。 在可用性组的每个副本上安装 Reporting Services 点时，报表可以始终连接到活动的报表点服务器。  


### <a name="switch-the-reporting-services-point-used-by-the-console"></a>切换由控制台使用的 Reporting Services 点

1. 在 Configuration Manager 控制台中，转到“监视”  工作区。  

2. 展开“报告”  ，然后选择“报表”  。  

3. 单击“报表选项”  。  

4. 在“报表选项”对话框中，选择要使用的 Reporting Services 点。  



## <a name="next-steps"></a>后续步骤

本文介绍了在使用可用性组时 Configuration Manager 所需的常见任务的先决条件、限制和更改。 有关设置和配置站点以使用可用性组的过程，请参阅[配置可用性组](/sccm/core/servers/deploy/configure/configure-aoag)。
