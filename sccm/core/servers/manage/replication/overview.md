---
title: SQL 复制故障排除
titleSuffix: Configuration Manager
description: 使用这些图示来帮助了解 Configuration Manager 站点之间的 SQL 复制并进行故障排除
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4f1506ce7931fdb95a447695fbd9bf0c12146e0
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957797"
---
# <a name="troubleshoot-sql-replication"></a>SQL 复制故障排除

在多站点层次结构中，Configuration Manager 使用 SQL 复制在站点之间传输数据。 有关详细信息，请参阅[数据库复制](/sccm/core/plan-design/hierarchy/database-replication)。

为了更好地了解和帮助排查 SQL 复制相关问题，请使用以下图示。

- [SQL 复制](/sccm/core/servers/manage/replication/sql-replication)
- [SQL 配置](/sccm/core/servers/manage/replication/sql-configuration)
- [SQL 性能](/sccm/core/servers/manage/replication/sql-performance)
- [SQL 复制重新初始化 (reinit)](/sccm/core/servers/manage/replication/sql-replication-reinit)
- [全局数据重新初始化](/sccm/core/servers/manage/replication/global-data-reinit)
- [站点数据重新初始化](/sccm/core/servers/manage/replication/site-data-reinit)
- [重新初始化丢失的消息](/sccm/core/servers/manage/replication/reinit-missing-message)

这些故障排除图示是相互关联的。 使用以下图示了解其关系：

![SQL 复制故障排除过程概述图](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

有关详细信息，请参阅以下 Microsoft 支持部门的系列博客：

- [ConfigMgr DRS 同步内部机制](https://blogs.technet.microsoft.com/umairkhan/2019/06/01/configmgr-drs-synchronization-internals/)
- [ConfigMgr 2012 数据复制服务 (DRS) 揭秘](https://blogs.technet.microsoft.com/umairkhan/2014/02/17/configmgr-2012-data-replication-service-drs-unleashed/)
- [ConfigMgr 2012 DRS – 故障排除常见问题解答](https://blogs.technet.microsoft.com/umairkhan/2014/03/24/configmgr-2012-drs-troubleshooting-faqs/)
- [ConfigMgr 2012 DRS 初始化内部机制](https://blogs.technet.microsoft.com/umairkhan/2015/01/21/configmgr-2012-drs-initialization-internals/)
- [ConfigMgr 2012：DRS 和 SQL Service Broker 证书问题](https://blogs.technet.microsoft.com/umairkhan/2013/12/12/configmgr-2012-drs-and-sql-service-broker-certificate-issues/)
