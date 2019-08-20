---
title: 重新初始化丢失的消息
titleSuffix: Configuration Manager
description: 使用此图示开始对 Configuration Manager 中使用 SQL 复制重新初始化丢失的消息进行故障排除
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2307a4bddb3651f0954e479f34b987312a18e12f
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957607"
---
# <a name="reinit-missing-message"></a>重新初始化丢失的消息

在多站点层次结构中，Configuration Manager 使用 SQL 复制在站点之间传输数据。 有关详细信息，请参阅[数据库复制](/sccm/core/plan-design/hierarchy/database-replication)。

使用以下图示开始对 SQL 复制重新初始化 (reinit) 的丢失消息进行故障排除：

![对重新初始化的丢失消息进行故障排除的图示](media/reinit-missing-message.svg)

## <a name="queries"></a>查询

此图示使用以下查询：

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>检查站点复制是否尚未完成重新初始化

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>从订阅服务器站点获取 TrackingGuid 和状态

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>从发布站点获取 TrackingGuid 和状态

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>修正操作

### <a name="version-1902-and-later"></a>1902 版和更高版本

若要检测问题和重新初始化，请运行[复制链接分析器](/sccm/core/servers/manage/monitor-replication#BKMK_RLA)。

### <a name="version-1810-and-earlier"></a>1810 版和更高版本

运行以下 SQL 查询以获取 `ReplicationGroupID`：

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

然后，通过以下值对 `SMS_ReplicationGroup` WMI 类使用 `InitializeData` 方法：

- ReplicationGroupID: 来自上面的 SQL 查询
- SiteCode1: 父站点
- SiteCode2: 子站点

有关详细信息，请参阅 [class SMS_ReplicationGroup 中的 InitializeData 方法](/sccm/develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup)。

#### <a name="example"></a>示例

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>后续步骤

- [SQL 复制重新初始化 (reinit)](/sccm/core/servers/manage/replication/sql-replication-reinit)
