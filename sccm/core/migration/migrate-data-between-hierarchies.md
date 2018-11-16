---
title: 迁移数据
titleSuffix: Configuration Manager
description: 了解如何将数据从源层次结构传输到 Configuration Manager 目标层次结构。
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4c33c0f2c3b4848d67a09b77247fa53284b02882
ms.sourcegitcommit: 1f8731ed8f0308cb2cb576722adb0821a366e9ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223681"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>在 Configuration Manager 中的层次结构之间迁移数据

*适用范围：System Center Configuration Manager (Current Branch)*

使用迁移将数据从受支持的源层次结构传输到 Configuration Manager（当前分支）目标层次结构。 从源层次结构迁移数据时：  

- 可从源基础结构中的站点数据库访问数据，然后将数据传输到当前环境。  

- 迁移不会更改源层次结构中的数据。 相反，它会发现数据并将副本存储在目标层次结构的数据库中。  

规划迁移策略时，请考虑以下几点：  

- 可将现有 Configuration Manager 2007 SP2 基础结构迁移到 Configuration Manager（当前分支）。  

- 可以从源站点迁移部分或全部受支持的数据。  

- 可以将数据从单个源站点迁移到目标层次结构中的多个不同站点。  

- 可以将数据从多个源站点移到目标层次结构中的单个站点。  


下面的视频讨论并演示了两种常见[迁移方案](#BKMK_MigrationScenarios)。 它还包括在迁移计划中包含 Microsoft Azure 的选项。
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="BKMK_MigrationConcepts"></a> 概念  

 Configuration Manager 在迁移过程中使用以下概念和术语。  

#### <a name="source-hierarchy"></a>源层次结构
一种层次结构，其运行 Configuration Manager 的受支持版本，并具有想要迁移的数据。 在设置迁移时，在指定源层次结构的顶层站点时标识源层次结构。 在指定源层次结构之后，目标层次结构的顶层站点从指定的源站点的数据库中收集数据，以确定可迁移的数据。 

有关详细信息，请参阅[源层次结构](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Source_Hierarchies)。

#### <a name="source-sites"></a>源站点
源层次结构中的站点，具有可迁移到目标层次结构中的数据。 

有关详细信息，请参阅[源站点](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Source_Sites)。

#### <a name="destination-hierarchy"></a>目标层次结构
Configuration Manager（当前分支）层次结构，迁移在其中运行以从源层次结构导入数据。

#### <a name="data-gathering"></a>数据收集
确定源层次结构中可迁移到目标层次结构的信息的持续过程。 Configuration Manager 按计划检查源层次结构。 此过程确定对先前迁移的源层次结构中的信息以及可能要在目标层次结构中更新的信息的任何更改。

有关详细信息，请参阅[数据收集](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Data_Gathering)。

#### <a name="migration-jobs"></a>迁移作业
配置要迁移的特定对象，然后管理将这些对象迁移到目标层次结构的过程。

有关详细信息，请参阅[规划迁移作业策略](/sccm/core/migration/planning-a-migration-job-strategy)。

#### <a name="client-migration"></a>客户端迁移
将客户端使用的信息从源站点的数据库传输到目标层次结构的数据库的过程。 在进行此数据迁移之后，将设备上的客户端软件升级到目标层次结构中的客户端软件版本。

有关详细信息，请参阅[规划客户端迁移策略](/sccm/core/migration/planning-a-client-migration-strategy)。

#### <a name="shared-distribution-points"></a>共享的分发点
在迁移期间，Configuration Manager 与目标层次结构共享的源层次结构中的分发点。

在迁移期间，分配到目标层次结构中的站点的客户端可以从共享的分发点中获得内容。

有关详细信息，请参阅[在源和目标层次结构之间共享分发点](/sccm/core/migration/planning-a-content-deployment-migration-strategy#About_Shared_DPs_in_Migration)。

#### <a name="monitoring-migration"></a>监视迁移
监视迁移活动的过程。 通过“管理” 工作区中的“迁移”节点监视迁移的进度和成功情况。

有关详细信息，请参阅[规划监视迁移活动](/sccm/core/migration/planning-to-monitor-migration-activity)。

#### <a name="stop-gathering-data"></a>停止收集数据
停止从源站点收集数据的过程。 如果不再具有要从源层次结构迁移的数据，或者，如果要暂停与迁移相关的活动，则可以将目标层次结构配置为停止从该源层次结构收集数据。

有关详细信息，请参阅[数据收集](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Data_Gathering)。

#### <a name="clean-up-migration-data"></a>清理迁移数据
通过从目标层次结构数据库中删除有关迁移的信息来完成从源层次结构进行的迁移的过程。

有关详细信息，请参阅[规划完成迁移](/sccm/core/migration/planning-to-complete-migration)。



## <a name="typical-workflow"></a>典型工作流  

设置迁移的工作流：

1.  指定支持的源层次结构。  

2.  设置数据收集。 数据收集能让 Configuration Manager 收集有关可以从源层次结构迁移的数据的信息。  

     Configuration Manager 会自动按照简单的计划重复这个数据收集过程，直到停止此过程为止。 默认情况下，数据收集过程每 4 小时重复一次，以便 Configuration Manager 能够识别对源层次结构中的数据所做的更改。 共享分发点也需要数据收集。  

3.  创建迁移作业以在源和目标层次结构之间迁移数据。  

4.  随时都可以使用“停止收集数据”操作来停止数据收集过程。 停止数据收集时，Configuration Manager 不再识别对源层次结构中的数据所做的更改，并且不再共享分发点。 通常，在你不再计划迁移数据或共享源层次结构中的分发点时使用此操作。  

5.  在源层次结构的所有站点均已停止数据收集之后，可以根据需要使用“清理迁移数据”操作来清理迁移数据。 此操作将从目标层次结构的数据库中删除有关从源层次结构进行的迁移的历史数据。  

数据已迁移且不再需要源层次结构以管理环境中的设备之后，可以解除该源层次结构和基础结构的授权。  



##  <a name="BKMK_MigrationScenarios"></a> 方案  

 Configuration Manager 支持以下迁移方案：
- [从 Configuration Manager 2007 层次结构进行迁移](#bkmk_2007)  
- [从 Configuration Manager 2012 或另一个 Configuration Manager 层次结构进行迁移](#bkmk_2012)

> [!NOTE]  
>  将具有独立站点的层次结构扩展为具有管理中心站点的层次结构并不归类为迁移。 要详细了解层次结构扩展，请参阅[扩展独立主站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand)。  


### <a name="bkmk_2007"></a> 从 Configuration Manager 2007 层次结构进行迁移  

 使用迁移方法从 Configuration Manager 2007 迁移数据时，可保留在现有站点基础结构中的投资，并获得以下好处：  

#### <a name="site-database-improvements"></a>站点数据库的改进
Configuration Manager（当前分支）数据库支持完整的 Unicode。

#### <a name="database-replication-between-sites"></a>站点之间的数据库复制
Configuration Manager（当前分支）中的副本基于 Microsoft SQL Server。 此行为可提高站点间数据传输的性能。

#### <a name="user-centric-management"></a>以用户为中心的管理
用户是 Configuration Manager（当前分支）中管理任务的重点。 例如，即使不知道某用户的设备名称，也可以将软件分发给该用户。 此外，Configuration Manager 还能让用户在更大程度上控制在其设备上安装哪个软件，以及何时安装该软件。

#### <a name="hierarchy-simplification"></a>层次结构简化
Configuration Manager（当前分支）可以生成更简单的站点层次结构。 此项改进归功于管理中心站点类型的引入以及主站点和辅助站点的行为更改。 与以前版本相比，Configuration Manager（当前分支）使用的网络带宽更少，所需服务器也更少。

#### <a name="role-based-administration"></a>基于角色的管理
Configuration Manager 中的中央安全模型提供了与管理要求和业务要求相对应的、覆盖整个层次结构的安全和管理。

> [!NOTE]  
>  由于 System Center 2012 Configuration Manager 中首次引入了设计更改，因此无法将 Configuration Manager 2007 升级到 Configuration Manager（当前分支）。 支持从 System Center 2012 Configuration Manager 就地升级到 Configuration Manager（当前分支）。  


### <a name="bkmk_2012"></a> 从 Configuration Manager 2012 或另一个 Configuration Manager 层次结构进行迁移  
 从 System Center 2012 Configuration Manager 或 Configuration Manager 层次结构迁移数据的过程是相同的。 此过程包括将数据从多个源层次结构迁移到单个目标层次结构中。 如果公司获得已由 Configuration Manager 管理的其他资源时，可以使用此过程。 此外，还可以将数据从测试环境迁移到 Configuration Manager 生产环境。 此过程可以保留 Configuration Manager 测试环境中的投资。  



## <a name="see-also"></a>另请参阅  

-   [规划迁移到 Configuration Manager](/sccm/core/migration/planning-for-migration)  

-   [配置源层次结构和源站点以进行迁移](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration)  

-   [迁移操作](/sccm/core/migration/operations-for-migration)  

-   [迁移的安全和隐私](/sccm/core/migration/security-and-privacy-for-migration)  

-   [开始使用 Configuration Manager ](/sccm/core/servers/deploy/start-using)
