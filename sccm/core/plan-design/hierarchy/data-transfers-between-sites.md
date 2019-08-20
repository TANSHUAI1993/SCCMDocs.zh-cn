---
title: 站点间数据传输
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 如何在站点之间移动数据，并了解如何管理网络上的数据传输。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d9d2a318b6516fef8f5336cd738a3d2517014a4
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957907"
---
# <a name="data-transfers-between-sites"></a>站点间数据传输

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager 使用基于文件的复制  和数据库复制  在站点之间传输不同类型的信息。 了解 Configuration Manager 如何在站点之间移动数据，并了解如何管理网络上的数据传输。  

## <a name="types-of-replication"></a>复制类型

### <a name="a-namebkmk_fileroute--file-based-replication"></a><a name="bkmk_fileroute" /> 基于文件的复制

Configuration Manager 使用基于文件的复制在层次结构中的站点之间传输基于文件的数据。 此数据包括要部署到子站点中的分发点的应用程序和包。 它还处理未处理的发现数据记录，站点将这些记录传输到其父站点然后进行处理。  

有关详细信息，请参阅[基于文件的复制](/sccm/core/plan-design/hierarchy/file-based-replication)。

### <a name="a-namebkmk_dbrep--database-replication"></a><a name="bkmk_dbrep" /> 数据库复制

Configuration Manager 数据库复制使用 SQL Server 来传输数据。 它使用此方法将其站点数据库中的更改与层次结构中其他站点上的数据库中的信息进行合并。

有关详细信息，请参阅[数据库复制](/sccm/core/plan-design/hierarchy/database-replication)。

有关排除 SQL 复制故障的帮助，请参阅 [SQL 复制故障排除](/sccm/core/servers/manage/replication/overview)。

## <a name="see-also"></a>另请参阅

[监视复制](/sccm/core/servers/manage/monitor-replication)
