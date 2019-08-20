---
title: 全局数据重新初始化
titleSuffix: Configuration Manager
description: 使用此图示开始对 Configuration Manager 层次结构中站点数据的 SQL 复制重新初始化进行故障排除
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b40a38f928351315fe1d0bd9dabc4f187e082a96
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957757"
---
# <a name="sql-replication"></a>SQL 复制

在多站点层次结构中，Configuration Manager 使用 SQL 复制在站点之间传输数据。 有关详细信息，请参阅[数据库复制](/sccm/core/plan-design/hierarchy/database-replication)。

使用以下图示开始对 Configuration Manager 层次结构中站点数据的 SQL 复制重新初始化 (reinit) 进行故障排除：

![站点数据重新初始化故障排除图示](media/site-data-reinit.svg)

## <a name="queries"></a>查询

此图示使用以下查询：

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>检查站点复制是否尚未完成重新初始化

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>从 CAS 获取 TrackingGuid 和状态

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>从主站点获取 TrackingGuid 和状态

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>检查主站点是否处于维护模式

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>检查跟踪 ID 的请求状态

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>后续步骤

- [重新初始化丢失的消息](/sccm/core/servers/manage/replication/reinit-missing-message)
- [全局数据重新初始化](/sccm/core/servers/manage/replication/global-data-reinit)
