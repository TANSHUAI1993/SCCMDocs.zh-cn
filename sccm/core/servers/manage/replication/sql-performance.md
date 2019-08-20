---
title: SQL 性能
titleSuffix: Configuration Manager
description: 使用此图示开始对 Configuration Manager 的 SQL 性能进行故障排除
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 9930a8a4-4d7f-47a4-bf6b-4c36d0ed5528
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b2f77f1bf8e1dd46d8ee9cd65c30f72c1f936bbd
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957747"
---
# <a name="sql-performance"></a>SQL 性能

在多站点层次结构中，Configuration Manager 使用 SQL 复制在站点之间传输数据。 有关详细信息，请参阅[数据库复制](/sccm/core/plan-design/hierarchy/database-replication)。

使用以下图示对可能影响复制状态的 SQL 性能进行故障排除：

![SQL 性能故障排除图示](media/sql-performance.png)

<!-- PNG used instead of SVG because the SQL statements wrap weird in the SVG. The SVG file exists in the same location. -->

## <a name="queries"></a>查询

此图示使用以下查询：

### <a name="make-sure-sql-change-tracking-table-is-cleaned-up"></a>确保已清除 SQL 更改跟踪表

```sql
DECLARE @RetentionUnit INT = 0;
DECLARE @RetentionPeriod INT = 0;
DECLARE @CTCutOffTime DATETIME;
DECLARE @CTMinTime DATETIME;

SELECT @RetentionPeriod=retention_period,  
    @RetentionUnit=retention_period_units  
FROM sys.change_tracking_databases  
WHERE database_id = DB_ID();

IF @RetentionUnit = 1
    SET @CTCutOffTime = DATEADD(MINUTE,-@RetentionPeriod,GETUTCDATE())
ELSE IF @RetentionUnit = 2
    SET @CTCutOffTime = DATEADD(HOUR,-@RetentionPeriod,GETUTCDATE())
ELSE IF @RetentionUnit = 3
    SET @CTCutOffTime = DATEADD(DAY,-@RetentionPeriod,GETUTCDATE())

-- give a buffer of two days
SET @CTCutOffTime = DATEADD(DAY, -2, @CTCutOffTime)
select top 1 @CTMinTime=commit_time from sys.dm_tran_commit_table order by commit_ts asc
IF @CTMinTime < @CTCutOffTime
    PRINT 'there is change tracking backlog, please contact Microsoft support'
```

### <a name="change-current-sessions-that-handle-sql-service-broker-messages-are-blocked"></a>更改处理 SQL Service Broker 消息的当前会话被阻止

```sql
select
       req.session_id
       ,req.blocking_session_id
       ,req.last_wait_type
       ,req.wait_type
       ,req.wait_resource
       ,t.text
from sys.dm_exec_sessions s
inner join sys.dm_exec_requests req on s.Session_id=req.session_id
cross apply sys.dm_exec_sql_text(sql_handle) t
where program_name='SMS_data_replication_service'
```

### <a name="check-sessions-asking-too-much-memory"></a>检查会话是否请求过多内存

```sql
SELECT * FROM sys.dm_exec_query_memory_grants
ORDER BY requested_memory_kb DESC
```

### <a name="check-sessions-taking-too-many-locks"></a>检查会话是否占用过多锁

```sql
SELECT TOP 10 request_session_id,
program_name = (SELECT program_name FROM sys.dm_exec_sessions WHERE session_id=request_session_id),
COUNT (*) num_locks
FROM sys.dm_tran_locks
GROUP BY request_session_id
ORDER BY count (*) DESC
```

## <a name="see-also"></a>另请参阅

[SQL 配置](/sccm/core/servers/manage/replication/sql-configuration)
