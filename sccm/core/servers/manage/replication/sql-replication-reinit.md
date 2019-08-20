---
title: SQL 复制重新初始化
titleSuffix: Configuration Manager
description: 使用此图示开始对 Configuration Manager 站点之间的 SQL 复制重新初始化进行故障排除
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ddc80fe039745930bfd5ecbdfedc5b028849f4d4
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957627"
---
# <a name="sql-replication-reinit"></a>SQL 复制重新初始化

在多站点层次结构中，Configuration Manager 使用 SQL 复制在站点之间传输数据。 有关详细信息，请参阅[数据库复制](/sccm/core/plan-design/hierarchy/database-replication)。

使用以下图示开始对 SQL 复制重新初始化 (reinit) 进行故障排除：

![对 SQL 复制重新初始化 (reinit) 进行故障排除的图示](media/sql-replication-reinit.svg)

## <a name="queries"></a>查询

此图示使用以下查询：

### <a name="check-if-site-is-in-maintenance-mode"></a>检查站点是否处于维护模式

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>检查哪个复制组尚未完成重新初始化

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>检查全局数据

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>检查站点数据

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>后续步骤

- [全局数据重新初始化](/sccm/core/servers/manage/replication/global-data-reinit)
- [站点数据重新初始化](/sccm/core/servers/manage/replication/site-data-reinit)
- [SQL 配置](/sccm/core/servers/manage/replication/sql-configuration)
