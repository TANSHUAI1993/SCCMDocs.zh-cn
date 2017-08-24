---
title: "完成迁移 | Microsoft Docs"
description: "了解如何在源层次结构不再包含数据后，完成到 System Center Configuration Manager 目标层次结构的迁移。"
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: eb1d2e320df02b26423ed4341d5bd1568b9444ad
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-to-complete-migration-in-system-center-configuration-manager"></a>规划在 System Center Configuration Manager 中完成迁移

*适用范围：System Center Configuration Manager (Current Branch)*

对于 System Center Configuration Manager，当源层次结构不再包含要迁移到目标层次结构的数据时，可以完成迁移过程。 完成迁移包括下列常规步骤：  

-   确保已迁移所需的数据。 从源层次结构中完成迁移之前，请确保已经从源层次结构中成功迁移了目标层次结构中所需的所有资源。 这可以包括数据和客户端。  

-   停止从源站点收集数据。 若要从源层次结构中完成迁移，必须首先停止从源站点收集数据。  

-   清理迁移数据。 从源层次结构内的所有源站点中停止收集数据后，可以从目标层次结构的数据库中删除关于迁移过程和源层次结构的数据。  

-   解除源层次结构授权。 从源层次结构中完成迁移并且该层次结构不再包含你管理的资源之后，可以解除该源层次结构中站点的授权以及从环境中删除相关的基础结构。 有关如何解除站点和源层次结构授权的信息，请查阅该 Configuration Manager 版本的文档。  

使用下列部分来帮助你通过停止数据收集并清理迁移数据以规划在源层次结构中完成迁移：  

-   [计划停止收集数据](#Plan_to_Stop_Data_Gath)  

-   [计划清理迁移数据](#Plan_to_clean_up)  

##  <a name="Plan_to_Stop_Data_Gath"></a>计划停止收集数据  
 完成迁移以及清理迁移数据之前，必须停止从源层次结构内的每个源站点中收集数据。 要停止从每个源站点中收集数据，必须在底层源站点上执行“停止收集数据”  命令，然后在每个父站点重复该过程。 源层次结构的顶层站点必须是你执行停止收集数据操作的最后一个站点。 在父站点上执行此命令之前，必须在每个子站点上停止数据收集。 通常，只有在准备好完成迁移过程时才停止收集数据。  

 停止从源站点中收集数据之后，该站点中的共享分发点不再可用作目标层次结构中客户端的内容位置。 因此，请使用以下选项之一确保目标层次结构中的客户端需要访问的任何迁移内容仍然可用：  

-   在目标层次结构中，将内容分发到至少一个分发点。  

-   在停止从源站点收集数据之前，请升级或重新分配具有所需内容的共享分发点。 有关升级或重新分配共享的分发点的详细信息，请参阅[在 System Center Configuration Manager 中规划内容部署迁移策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)中的适用部分。  

从源层次结构内的每个源站点中停止收集数据之后，你可以清理迁移数据。 在清理迁移数据之前，已经运行或者计划运行的每个迁移作业在 Configuration Manager 控制台中仍处于可访问状态。  

有关源站点和数据收集的详细信息，请参阅[在 System Center Configuration Manager 中规划源层次结构策略](../../core/migration/planning-a-source-hierarchy-strategy.md)。  

##  <a name="Plan_to_clean_up"></a>计划清理迁移数据  
 完成迁移所需的最后一步是清理迁移数据。 在停止收集源层次结构中每个源站点的数据之后，你可以使用“清理迁移数据”  命令。 此可选操作将从目标层次结构的数据库中删除有关当前源层次结构的数据。  

 清理迁移数据时，会从目标层次结构的数据库中删除有关迁移的大部分数据。 但是，有关迁移对象的详细信息将会保留。 通过这些详细信息，可以使用“迁移”工作区重新配置包含已迁移的数据的源层次结构，以恢复从该源层次结构进行迁移，或者查看以前迁移的对象的对象和站点所有权。  
