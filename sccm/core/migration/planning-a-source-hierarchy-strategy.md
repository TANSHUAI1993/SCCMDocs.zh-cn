---
title: "源层次结构策略 | Microsoft Docs"
description: "在配置 System Center Configuration Manager 迁移作业之前，请先配置源层次结构并从源站点中收集数据。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0619de32f859f512ee1c9f5a9c83ef8d04a256ca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-a-source-hierarchy-strategy-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中规划源层次结构策略

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 环境中设置迁移作业之前，必须配置源层次结构，并从该层次结构内的至少一个源站点中收集数据。 使用以下部分来帮助规划配置源层次结构、配置源站点，并确定 Configuration Manager 从源层次结构内的源站点中收集信息的方式。 

##  <a name="BKMK_Source_Hierarchies"></a> 源层次结构  
源层次结构是 Configuration Manager 层次结构，其中包含要迁移的数据。 在设置迁移并指定源层次结构时，将指定源层次结构的顶层站点。 此站点也称为源站点。 源层次结构内你可从中迁移数据的其他站点也称为源站点。  

-   在设置迁移作业以从 Configuration Manager 2007 源层次结构迁移数据时，将其配置为从源层次结构中的一个或多个特定源站点迁移数据。  

-   在设置迁移作业以从运行 System Center 2012 Configuration Manager 或更高版本的源层次结构迁移数据时，只需指定顶层站点。  

一次只能设置一个源层次结构。  

-   如果设置新的源层次结构，该层次结构将自动成为当前源层次结构，替代以前的源层次结构。  

-   在设置源层次结构时，必须指定源层次结构的顶层站点，并指定供 Configuration Manager 用以连接到 SMS 提供程序和源站点的站点数据库的凭据。  

-   Configuration Manager 使用这些凭据来运行数据收集以从源站点中检索有关对象和分发点的信息。  

-   在数据收集过程中，将确定源层次结构中的子站点。  

-   如果源层次结构是 Configuration Manager 2007 层次结构，则可以随后将那些附加站点设置为源站点，每个源站点有单独的凭据。  

尽管可连续设置多个源层次结构，但一次只有一个源层次结构的迁移可处于活动状态。  

-   如果在完成从当前源层次结构中进行的迁移之前设置其他源层次结构，Configuration Manager 将为当前源层次结构取消任何活动的迁移作业，并推迟任何计划的迁移作业。  

-   新配置的源层次结构随后将成为当前源层次结构，原始源层次结构现在处于非活动状态。  

-   可随后为新源层次结构设置连接凭据、其他源站点和迁移作业。  

如果还原非活动源层次结构，并且之前未使用过“清理迁移数据”，则可以查看该源层次结构的以前配置的迁移作业。 但是，你必须重新配置凭据以连接到层次结构中的适用源站点，然后重新计划任何未完成的迁移作业，然后才能继续从该层次结构中进行迁移。  

> [!CAUTION]  
>  如果从超过一个源层次结构中迁移数据，则每个额外的源层次结构都必须包含一组唯一的站点代码。  

有关配置源层次结构的详细信息，请参阅[配置源层次结构和源站点以迁移到 System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

##  <a name="BKMK_Source_Sites"></a> 源站点  
 源站点是源层次结构中具有要迁移的数据的站点。 源层次结构的顶层站点始终是第一个源站点。 当迁移从新源层次结构的第一个源站点中收集数据时，它将发现有关该层次结构中的其他站点的信息。  

 初始源站点的数据收集完成后，你接下来进行的操作取决于源层次结构的产品版本。  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>运行 Configuration Manager 2007 SP2 的源站点  
 从 Configuration Manager 2007 SP2 层次结构的初始源站点中收集数据后，不必在创建迁移作业之前设置其他源站点。 但是，必须将其他站点设置为源站点，并且 System Center Configuration Manager 必须成功从这些站点中收集数据，然后才能从其他站点中迁移数据。  

 要从其他站点中收集数据，请单独将每个站点设置为源站点。 这需要为 System Center Configuration Manager 指定凭据以连接到每个源站点的 SMS 提供程序和站点数据库。 为源站点设置凭据之后，该站点的数据收集过程将开始。  

 在 Configuration Manager 2007 SP2 源层次结构中设置其他源站点时，必须按自上而下的顺序设置源站点，这意味着将最后设置底层站点。 可随时在层次结构的分支中配置源站点，但在将某个站点的任何子站点设置为源站点之前，必须将该站点设置为源站点。  

> [!NOTE]  
>  对于迁移，只支持 Configuration Manager 2007 SP2 层次结构中的主站点。  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>运行 System Center 2012 Configuration Manager 或更高版本的源站点  
 从 System Center 2012 Configuration Manager 或其后的层次结构的初始源站点中收集数据后，不必设置其他源站点以从源层次结构中配置额外源站点。 这是因为不同于 Configuration Manager 2007，Configuration Manager 的这些版本使用共享数据库，通过共享数据库可确定初始源站点中的所有可用对象并随后将其迁移。  

 在设置访问帐户以收集数据时，可能需要向“源站点 SMS 提供程序帐户”授予对源层次结构中的多台计算机的访问权限。 当源站点支持 SMS 提供程序的多个实例，且每个实例位于不同的计算机上时，可能需要此权限。 当数据收集开始时，目标层次结构的顶层站点将与源层次结构中的顶层站点联系，以确定该站点的 SMS 提供程序的位置。 只会确定 SMS 提供程序的第一个实例。 如果数据收集过程无法访问它确定的位置处的 SMS 提供程序，则该过程将失败，并且不会尝试连接到运行该站点的 SMS 提供程序实例的其他计算机。  

##  <a name="BKMK_Data_Gathering"></a> 数据收集  
 在指定源层次结构之后，立即为源层次结构中的每个其他源站点设置凭据，或共享源站点的分发点，Configuration Manager 将开始从该源站点中收集数据。  

 数据收集过程随后将按简单的计划重复运行，以便与源站点中的任何数据更改保持同步。 默认情况下，该过程每隔四小时重复一次。 可通过编辑源站点的“属性”来更改此周期的计划。 初始数据收集过程必须审阅 Configuration Manager 数据库中的所有对象，并且可能需要较长时间才能完成。 后续的数据收集过程只确定数据更改，完成操作所需的时间较短。  

 为了收集数据，目标层次结构中的顶层站点将连接到源站点的 SMS 提供程序和站点数据库，以检索对象和分发点的列表。 这些连接使用源站点访问帐户。 有关用于收集数据的所需配置的信息，请参阅 [System Center Configuration Manager 中迁移的先决条件](../../core/migration/prerequisites-for-migration.md)。  

 可以通过使用 Configuration Manager 控制台中的“立即收集数据”和“停止收集数据”来开始或停止数据收集进程。  

 在出于任何原因为源站点使用“停止收集数据”后，必须为站点重新配置凭据，然后才能再次从该站点收集数据。 在重新配置源站点之前，Configuration Manager 将无法确定新对象或对该站点上以前迁移的对象所做的更改。  

> [!NOTE]  
>  在将独立主站点扩展为包含管理中心站点的层次结构之前，必须停止所有数据收集操作。 可在站点扩展完成之后重新配置数据收集。  

### <a name="gather-data-now"></a>控制台中的“立即收集数据”  
 为站点运行初始数据收集过程后，此过程将重复运行以确定自上次数据收集周期以来已更新的对象。 也可以使用 Configuration Manager 控制台中的“立即收集数据”操作立即开始该进程并重新设置下一个周期的开始时间。  

 源站点的数据收集过程成功完成后，你可以共享源站点中的分发点，并配置迁移作业以从该站点中迁移数据。 对于迁移而言，数据收集是一个重复进行的过程，并将持续运行，直至更改源层次结构或使用“停止收集数据”来结束该站点的数据收集过程为止。  

### <a name="stop-gathering-data"></a>和“停止收集数据”  
 当你不再想要 Configuration Manager 来确定来自该站点的新的或已更改的对象，则可以使用“停止收集数据”来结束源站点的数据收集过程。 此操作还可防止 Configuration Manager 向目标层次结构中的客户端提供源中的任何共享分发点作为已迁移内容的内容位置。  

 要停止从每个源站点中收集数据，必须在底层源站点上运行“停止收集数据”，然后在每个父站点上重复该过程。 源层次结构的顶层站点必须是你执行停止收集数据操作的最后一个站点。 你必须在每个子站点上停止数据收集，之后在父站点上执行此操作。 通常，你只有在准备完成迁移过程时才停止收集数据。  

 为源站点停止收集数据后，之前从该站点中收集的有关对象和集合的信息仍然可在设置新迁移作业时使用。 但是，你不会看到任何新对象或集合，也不会看到之前对现有对象所做的更改。 如果重新配置源站点并再次开始收集数据，你将看到有关以前迁移的对象的信息和状态。  
