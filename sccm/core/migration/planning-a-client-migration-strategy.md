---
title: "规划客户端迁移 | Microsoft Docs"
description: "了解将客户端从源层次结构迁移到 System Center Configuration Manager 目标层次结构的任务。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b52ca4059dfeed08cabf1f75319da40d6499622f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-a-client-migration-strategy-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中规划客户端迁移策略

*适用范围：System Center Configuration Manager (Current Branch)*

要将客户端从源层次结构迁移到 System Center Configuration Manager 目标层次结构，必须执行两个任务。 你必须迁移与客户端关联的对象，并且必须重新安装或将客户端从源层次结构重新分配到目标层次结构。 请先迁移对象，以便在迁移客户端时这些对象可用。 与客户端关联的对象是通过使用迁移作业迁移的。 有关如何迁移与客户端关联的对象的信息，请参阅[在 System Center Configuration Manager 中规划迁移作业策略](../../core/migration/planning-a-migration-job-strategy.md)。  

 使用下列部分来帮助你规划将客户端迁移到目标层次结构。  

-   [规划将客户端迁移到目标层次结构](#Planning_for_Client_Agent_Migration)  

-   [规划在迁移过程中处理客户端中保留的数据](#Planning_for_Client_Data_Migration)  

-   [在迁移过程中规划清单和符合性数据](#Planning_for_Inventory_data_migration)  

##  <a name="Planning_for_Client_Agent_Migration"></a> 规划将客户端迁移到目标层次结构  
 从源层次结构中迁移客户端时，客户端计算机上的客户端软件将升级，以与目标层次结构的产品版本匹配。  

-   **Configuration Manager 2007 源层次结构：**从运行受支持版本的 Configuration Manager 源层次结构中迁移客户端时，客户端软件将升级到目标层次结构的客户端版本。  

-   **System Center 2012 Configuration Manager 或更高版本的层次结构：**在产品版本相同的层次结构之间迁移客户端时，客户端软件不会更改或升级。 而是会从源层次结构重新分配到目标层次结构中的站点。  

    > [!NOTE]  
    >  如果层次结构的产品版本不支持迁移到目标层次结构，请将源层次结构中的所有站点和客户端升级到兼容的产品版本。 源层次结构升级到支持的产品版本后，你可以在层次结构之间进行迁移。 有关详细信息，请参阅 [System Center Configuration Manager 中迁移的先决条件](../../core/migration/prerequisites-for-migration.md)中的[迁移支持的 Configuration Manager 版本](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions)。  

使用以下信息来帮助你规划客户端迁移：  

-   若要将客户端从源站点升级或重新分配到目标站点，你可以使用支持的任何客户端部署方法在目标层次结构中部署客户端。 典型的客户端部署方法包括客户端请求安装、软件分发、组策略和基于软件更新的客户端安装。 有关详细信息，请参阅 [System Center Configuration Manager 中的客户端安装方法](../../core/clients/deploy/plan/client-installation-methods.md)。  

-   确保源层次结构中运行客户端软件的设备满足最低硬件要求，并运行目标层次结构中的 Configuration Manager 版本支持的操作系统。  

-   在迁移客户端之前，请运行迁移作业以迁移客户端将在目标层次结构中使用的信息。  

-   升级的客户端保留其部署的运行历史记录。 这可以防止部署在目标层次结构中进行不必要的重新运行。  

    -   对于 Configuration Manager 2007 客户端，会保留播发运行历史记录。  

    -   对于 System Center 2012 Configuration Manager 或 System Center Configuration Manager 客户端，会保留部署运行历史记录。  

-   你可以按所选的任何顺序从源层次结构内的站点中迁移客户端。 但是，请考虑分阶段迁移限制数量的客户端，而不是一次迁移大量的客户端。 分阶段迁移可减少每个新升级的客户端将其初始完整清单和符合性数据提交到为其分配的站点时的网络带宽需求和服务器处理。  

-   在迁移 Configuration Manager 2007 客户端时，会从客户端计算机中卸载现有客户端软件，并安装新的客户端软件。  

-   Configuration Manager 无法迁移安装了 App-V 客户端的 Configuration Manager 2007 客户端，除非 App-V 客户端版本为 4.6 SP1 或更高版本。  

可以在 Configuration Manager 控制台“管理”工作区的“迁移”节点中监视客户端迁移进程。  

将客户端迁移到目标层次结构后，将不再能够使用源层次结构管理该设备，并且应考虑从源层次结构中删除客户端。 尽管这不是迁移层次结构时必须进行的操作，但它可帮助防止在源层次结构报表中标识已迁移的客户端，或不正确地计算迁移过程中两个层次结构之间的资源数量。 例如，当已迁移客户端保留在源站点数据库中时，如果计算机现在由目标层次结构管理，则运行的软件更新报表可能会不正确地将该计算机标识为不受管理的资源。  

##  <a name="Planning_for_Client_Data_Migration"></a> 规划在迁移过程中处理客户端中保留的数据  
将客户端从其源层次结构迁移到目标层次结构时，某些信息在迁移之后会保留在设备上，而其他信息则在设备上不可用。  

以下信息将保留在客户端设备上：  

-   唯一标识符 (GUID)，用于将客户端与其在 Configuration Manager 数据库中的信息关联。  

-   播发或部署历史记录，用于防止客户端不必要地在目标层次结构中重新运行播发或部署。  

以下信息不会保留在客户端设备上：  

-   客户端缓存中的文件。 如果客户端需要这些文件来安装软件，则客户端将再次从目标层次结构中下载这些文件。  

-   源层次结构中有关尚未运行的任何播发或部署的信息。 如果希望客户端在其迁移后运行这些播发或部署，你必须将它们重新部署到目标层次结构中的客户端。  

-   有关清单的信息。 客户端在迁移之后向目标层次结构中为其分配的站点呈现此信息，并且已生成新的客户端数据。  

-   符合性数据。 客户端在迁移之后向目标层次结构中为其分配的站点呈现此信息，并且已生成新的客户端数据。  

当客户端迁移时，不会保留存储在 Configuration Manager 客户端注册表和文件路径中的信息。 迁移之后，请重新应用这些设置。 典型的设置包括以下各项：  

-   电源使用方案  

-   日志记录设置  

-   本地策略设置  

此外，你可能必须重新安装某些应用程序。  

##  <a name="Planning_for_Inventory_data_migration"></a> 在迁移过程中规划清单和符合性数据  
当你将客户端迁移到目标层次结构时，不会保存客户端清单和符合性数据， 而是会在客户端第一次将其信息发送到为其分配的站点时在目标层次结构中重新创建此信息。 为了帮助减少产生的网络带宽需求和服务器处理，请考虑分阶段迁移少量的客户端，而不是一次迁移大量的客户端。  

 此外，你无法从源层次结构迁移硬件清单的自定义项。 你必须独立于迁移将这些自定义项引入目标层次结构。 有关如何扩展硬件清单的信息，请参阅[如何在 System Center Configuration Manager 中配置硬件清单](../../core/clients/manage/inventory/configure-hardware-inventory.md)。  
