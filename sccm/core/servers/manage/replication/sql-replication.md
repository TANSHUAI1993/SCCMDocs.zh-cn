---
title: SQL 复制
titleSuffix: Configuration Manager
description: 使用此图示开始对 Configuration Manager 站点之间的 SQL 复制进行故障排除
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35c807010e821f5a9857e7cc9d18354db5758298
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957737"
---
# <a name="sql-replication"></a>SQL 复制

在多站点层次结构中，Configuration Manager 使用 SQL 复制在站点之间传输数据。 有关详细信息，请参阅[数据库复制](/sccm/core/plan-design/hierarchy/database-replication)。

使用以下图示开始对链接失败时的 SQL 复制进行故障排除：

![SQL 复制故障排除图示](media/sql-replication.svg)

## <a name="queries"></a>查询

此图示使用以下查询：

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>检查复制组链接是否处于降级或失败状态

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>检查是否最近计算了复制组链接

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>检查 SQL 维护模式

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>后续步骤

- [SQL 复制重新初始化 (reinit)](/sccm/core/servers/manage/replication/sql-replication-reinit)
- [SQL 性能](/sccm/core/servers/manage/replication/sql-performance)
- [SQL 配置](/sccm/core/servers/manage/replication/sql-configuration)
