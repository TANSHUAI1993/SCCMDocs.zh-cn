---
title: "规划迁移 | Microsoft Docs"
description: "将数据迁移到 System Center Configuration Manager 目标层次结构之前，了解有关站点和层次结构的信息。"
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: fffef1e95e1dfa03971f140a6e5a7fff9bfe5e27
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-migration-to-system-center-configuration-manager"></a>规划向 System Center Configuration Manager 的迁移

*适用范围：System Center Configuration Manager (Current Branch)*

在将数据迁移到 System Center Configuration Manager 目标层次结构之前，请确保熟知 Configuration Manager 中的站点和层次结构。 有关站点和层次结构的详细信息，请参阅 [System Center Configuration Manager 的基础知识](../../core/understand/fundamentals.md)。  

 必须先安装将成为目标层次结构的 System Center Configuration Manager 层次结构，然后才能从支持的源层次结构中迁移数据。  

 安装目标层次结构之后，设置要在目标层次结构中使用的管理特性和功能，然后再开始迁移数据。  

 此外，可能还必须规划源层次结构与目标层次结构之间的重叠。 例如，可能需要设置源层次结构以将相同网络位置或边界用作目标层次结构，随后将新客户端安装到目标层次结构并使用自动站点分配。 在这种情况下，因为新安装的 Configuration Manager 客户端可以从任一层次结构中选择要加入的站点，所以，该客户端可能会错误地分配到源层次结构。 为此，应计划将目标层次结构中的每个新客户端分配到该层次结构中的特定站点，而不是使用自动站点分配。  

 有关站点分配的详细信息，请参阅 [System Center Configuration Manager 不同版本之间的互操作性](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)中的[客户端站点分配注意事项](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment)。  

## <a name="plan-topics"></a>规划主题  
 使用下列主题来帮助你规划如何将支持的源层次结构迁移到 System Center Configuration Manager 目标层次结构：

-   [System Center Configuration Manager 中迁移的先决条件](../../core/migration/prerequisites-for-migration.md)  

-   [System Center Configuration Manager 中针对迁移规划的管理员清单](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [确定是否将数据迁移到 System Center Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [在 System Center Configuration Manager 中规划源层次结构策略](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [System Center Configuration Manager 中针对迁移规划的管理员清单](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [在 System Center Configuration Manager 中规划客户端迁移策略](../../core/migration/planning-a-client-migration-strategy.md)  

-   [在 System Center Configuration Manager 中规划内容部署迁移策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [规划将 Configuration Manager 对象迁移到 System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [在 System Center Configuration Manager 中规划监视迁移活动](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [规划在 System Center Configuration Manager 中完成迁移](../../core/migration/planning-to-complete-migration.md)  
