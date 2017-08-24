---
title: "迁移数据 | Microsoft Docs"
description: "了解如何将数据从源层次结构传输到 System Center Configuration Manager 目标层次结构。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: dface33392c2a2a662522656eabf0936b52b28fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="migrate-data-between-hierarchies-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中层次结构之间迁移数据

*适用范围：System Center Configuration Manager (Current Branch)*

使用迁移将数据从受支持的源层次结构传输到 System Center Configuration Manager 目标层次结构。  从源层次结构迁移数据时：  

-   从在源基础结构中标识的站点数据库访问数据，然后将数据传输到当前环境。  

-   迁移不会改变源层次结构中的数据，而是发现数据，然后在目标层次结构的数据库中存储这些数据的副本。  

规划迁移策略时，请考虑以下事项：  

-   可将现有 Configuration Manager 2007 SP2 基础结构迁移到 System Center Configuration Manager。  

-   可以从源站点迁移部分或全部受支持的数据。  

-   可以将数据从单个源站点迁移到目标层次结构中的多个不同站点。  

-   可以将数据从多个源站点移到目标层次结构中的单个站点。  

##  <a name="BKMK_MigrationConcepts"></a> 有关迁移的概念  
 使用迁移时可能遇到以下概念和术语。  

|概念或术语|更多信息|  
|---------------------|----------------------|  
|源层次结构|一种层次结构，其运行 Configuration Manager 的受支持版本，并具有想要迁移的数据。 在设置迁移时，在指定源层次结构的顶层站点时标识源层次结构。 在指定源层次结构之后，目标层次结构的顶层站点从指定的源站点的数据库中收集数据，以确定可迁移的数据。<br /><br /> 有关详细信息，请参阅[在 System Center Configuration Manager 中规划源层次结构策略](../../core/migration/planning-a-source-hierarchy-strategy.md)中的[源层次结构](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies)。|  
|源站点|源层次结构中的站点，具有可迁移到目标层次结构中的数据。<br /><br /> 有关详细信息，请参阅[在 System Center Configuration Manager 中规划源层次结构策略](../../core/migration/planning-a-source-hierarchy-strategy.md)中的[源站点](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites)。|  
|目标层次结构|一个 System Center Configuration Manager 层次结构，迁移在其中运行以从源层次结构导入数据。|  
|数据收集|确定源层次结构中可迁移到目标层次结构的信息的持续过程。 Configuration Manager 将按计划检查源层次结构，以确定对源层次结构中先前迁移的信息和目标层次结构中可能需要更新的信息的任何更改。<br /><br /> 有关详细信息，请参阅[在 System Center Configuration Manager 中规划源层次结构策略](../../core/migration/planning-a-source-hierarchy-strategy.md)中的[数据收集](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)。|  
|迁移作业|配置要迁移的特定对象，然后管理将这些对象迁移到目标层次结构的过程。<br /><br /> 有关详细信息，请参阅[在 System Center Configuration Manager 中规划迁移作业策略](../../core/migration/planning-a-migration-job-strategy.md)|  
|客户端迁移|将客户端使用的信息从源站点的数据库传输到目标层次结构的数据库的过程。 在进行此数据迁移之后，将设备上的客户端软件升级到目标层次结构中的客户端软件版本。<br /><br /> 有关详细信息，请参阅 [在 System Center Configuration Manager 中规划客户端迁移策略](../../core/migration/planning-a-client-migration-strategy.md)。|  
|共享的分发点|源层次结构中的分发点，它们在迁移期间与目标层次结构共享。<br /><br /> 在迁移期间，分配到目标层次结构中的站点的客户端可以从共享的分发点中获得内容。<br /><br /> 有关详细信息，请参阅[在 System Center Configuration Manager 中规划内容部署迁移策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)中的[在源和目标层次结构之间共享分发点](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)。|  
|监视迁移|监视迁移活动的过程。 通过“管理” 工作区中的“迁移”节点监视迁移的进度和成功情况。<br /><br /> 有关详细信息，请参阅[在 System Center Configuration Manager 中规划监视迁移活动](../../core/migration/planning-to-monitor-migration-activity.md)。|  
|停止收集数据|停止从源站点收集数据的过程。 如果不再具有要从源层次结构迁移的数据，或者，如果要暂停与迁移相关的活动，则可以将目标层次结构配置为停止从该源层次结构收集数据。<br /><br /> 有关详细信息，请参阅[在 System Center Configuration Manager 中规划源层次结构策略](../../core/migration/planning-a-source-hierarchy-strategy.md)中的[数据收集](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)。|  
|清理迁移数据|通过从目标层次结构数据库中删除有关迁移的信息来完成从源层次结构进行的迁移的过程。<br /><br /> 有关详细信息，请参阅 [计划完成 System Center Configuration Manager 中迁移](../../core/migration/planning-to-complete-migration.md)。|  

## <a name="typical-workflow-for-migration"></a>迁移的典型工作流  
设置迁移的工作流：

1.  指定支持的源层次结构。  

2.  设置数据收集。 数据收集能让 Configuration Manager 收集有关可以从源层次结构迁移的数据的信息。  

     Configuration Manager 会自动按照简单的计划重复这个数据收集过程，直到停止此过程为止。 默认情况下，数据收集过程每小时重复一次，使 Configuration Manager 得以识别对源层次结构中可能想迁移的数据所做的更改。 如果将分发点从源层次结构共享到目标层次结构，则也要进行数据收集。  

3.  创建迁移作业以在源和目标层次结构之间迁移数据。  

4.  你随时都可以使用“停止收集数据”  命令来停止数据收集过程。 停止数据收集时，Configuration Manager 不再识别对源层次结构中的数据所做的更改，而且不能够再在源和目标层次结构之间共享分发点。 通常，在你不再计划迁移数据或共享源层次结构中的分发点时使用此操作。  

5.  在源层次结构的所有站点均已停止数据收集之后，你可以根据需要使用“清理迁移数据”  命令来清理迁移数据。 此命令将从目标层次结构的数据库中删除有关从源层次结构进行的迁移的历史数据。  

从 Configuration Manager 源层次结构中迁移了不再用于管理环境的数据之后，可以解除该源层次结构和基础结构的授权。  

##  <a name="BKMK_MigrationScenarios"></a> 迁移方案  
 Configuration Manager 支持以下迁移方案。  

> [!NOTE]  
>  将具有独立站点的层次结构扩展为具有管理中心站点的层次结构并不归类为迁移。 有关层次结构扩展的信息，请参阅[使用安装向导来安装站点](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)中的[扩展独立主站点](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)。  

### <a name="migration-from-configuration-manager-2007-hierarchies"></a>从 Configuration Manager 2007 层次结构进行迁移  
 使用迁移方法从 Configuration Manager 2007 迁移数据时，可保留在现有站点基础结构中的投资，并获得以下好处：  

|好处|更多信息|  
|-------------|----------------------|  
|站点数据库的改进|System Center Configuration Manager 数据库支持完整的 Unicode。|  
|站点之间的数据库复制|System Center Configuration Manager 中的副本基于 Microsoft SQL Server。 这能改善站点间数据传输的性能。|  
|以用户为中心的管理|用户是 System Center Configuration Manager 中管理任务的重点。 例如，即使你不知道某用户的设备名称，也可以将软件分发给该用户。 此外，System Center Configuration Manager 还能让用户在更大程度上控制在其设备上安装哪个软件，以及何时安装该软件。|  
|层次结构简化|在 System Center Configuration Manager 中，管理中心站点类型以及主站点和辅助站点的行为更改允许构建使用更少网络带宽、需要更少服务器且更简单的站点层次结构。|  
|基于角色的管理|这是 System Center Configuration Manager 中的中央安全模型，它提供了与管理要求和业务要求相对应的、覆盖整个层次结构的安全性和管理。|  

> [!NOTE]  
>  由于 System Center 2012 Configuration Manager 中首次引入的设计更改，无法将 Configuration Manager 2007 基础结构升级为 System Center Configuration Manager。 支持从 System Center 2012 Configuration Manager 就地升级到 System Center Configuration Manager。  

### <a name="migration-from-configuration-manager-2012-or-another-system-center-configuration-manager-hierarchy"></a>从 Configuration Manager 2012 或另一个 System Center Configuration Manager 层次结构的迁移  
 从 System Center 2012 Configuration Manager 或 System Center Configuration Manager 层次结构迁移数据的过程是相同的。 这包括将数据从多个源层次结构迁移到一个目标层次结构，例如在贵公司获得了已经由 Configuration Manager 管理的额外资源时。 此外，还可以将数据从测试环境迁移到 Configuration Manager 生产环境。 这可以保留 Configuration Manager 测试环境中的投资。  

## <a name="additional-topics-for-migration"></a>关于迁移的的其他主题：  

-   [迁移到 System Center Configuration Manager 的规划](../../core/migration/planning-for-migration.md)  

-   [配置源层次结构和源站点以迁移到 System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [用于迁移到 System Center Configuration Manager 的操作](../../core/migration/operations-for-migration.md)  

-   [有关迁移到 System Center Configuration Manager 的安全和隐私](../../core/migration/security-and-privacy-for-migration.md)  

## <a name="see-also"></a>另请参阅  
 [开始使用 System Center Configuration Manager](../../core/servers/deploy/start-using.md)
