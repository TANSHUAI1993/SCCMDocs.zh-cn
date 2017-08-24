---
title: "维护任务 | Microsoft Docs"
description: "了解针对 Configuration Manager 站点和层次结构执行的维护任务以及何时执行它们。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 90b6e4434abc5573a364c769bd835e08e5dff16d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager 的维护任务

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 站点和层次结构需要定期维护和监视以有效和连续提供服务。 通过定期维护，可确保硬件、软件和 Configuration Manager 数据库继续正常有效运行。 最佳性能大大降低了出现故障的风险。  

 若要设置警报并使用状态系统监视 Configuration Manager 的运行状况，请参阅[使用 System Center Configuration Manager 的警报和状态系统](../../../core/servers/manage/use-alerts-and-the-status-system.md)。  

-   [维护任务](#bkmk_MTs)  

##  <a name="bkmk_MTs"></a>维护任务  
 定期维护对于确保正确的站点操作非常重要。 保留维护日志，以记录维护日期、执行者以及任务的维护相关备注。  

### <a name="when-to-do-common-maintenance-tasks"></a>何时执行常见维护任务  
 请考虑每日或每周维护一次站点。 某些任务可能需要不同的计划。 常见维护可包括内置维护任务和其他任务（如帐户维护），以保证公司策略的符合性。  

 使用下列信息作为指南，帮助计划执行不同维护任务的时间。 以这些列表为起点，然后添加可能需要的任务。  

**每日任务**   
可能要考虑的每日维护任务如下：  

-   检查计划每日运行的预定义维护任务是否成功运行。  

-   检查 Configuration Manager 数据库状态。  

-   检查站点服务器状态。  

-   检查 Configuration Manager 站点系统收件箱是否存在文件积压。  

-   检查站点系统状态。  

-   检查站点系统上的操作系统事件日志。  

-   检查站点数据库计算机上的 SQL Server 错误日志。  

-   检查系统性能。  

-   检查 Configuration Manager 警报。  

**每周任务**   
可能要考虑的每周维护任务如下：  

-   检查计划每周运行的预定义维护任务是否成功运行。  

-   从站点系统中删除不必要的文件。  

-   制作并分发最终用户报告（如果需要）。  

-   备份应用程序、安全和系统事件日志并将其清除。  

-   检查站点数据库大小，并检查站点数据库服务器上是否有足够的可用磁盘空间，以便站点数据库可以增大。  

-   按照 SQL Server 维护计划，对站点数据库执行 SQL Server 数据库维护。  

-   检查所有站点系统上的可用磁盘空间。  

-   在所有站点系统上运行磁盘碎片整理工具。  

**定期任务**   
某些任务无需每天或每周维护，但对确保站点总体运行状况非常重要。 这些任务还可确保安全和灾难恢复计划保持最新。 可能要考虑的更定期维护任务（比每日或每周任务更频繁）如下：  

-   如有必要，按照安全计划更改帐户和密码。  

-   查看维护计划，检查是否根据配置的站点设置正确有效地安排了所计划的维护任务。  

-   查看所有必需更改的 Configuration Manager 层次结构设计。  

-   检查网络性能，确保未进行影响站点操作的更改。  

-   检查是否未更改影响站点操作的 Active Directory 设置。 例如，检查是否未更改分配给 Active Directory 站点并用作 Configuration Manager 站点边界的子网。  

-   查看灾难恢复计划是否有任何必需的更改。  

-   通过“备份站点服务器”维护任务所创建的最新备份的备份副本，在测试实验室中按照灾难恢复计划执行站点恢复。

-   检查硬件是否有任何错误，或者是否有可用的硬件更新。  

-   检查站点的总体健康状况。  

###  <a name="BKMK_UseMTs"></a>维护站点数据库的操作运行状况  
 当 Configuration Manager 站点和层次结构执行所计划和设置的任务时，站点组件会向 Configuration Manager 数据库持续添加数据。 随着数据量增大，数据库性能和数据库中的可用存储空间将降低。 可设置站点维护任务，使其删除不再需要的过时数据。  

 Configuration Manager 提供预定义的维护任务，你可以使用这些任务维护 Configuration Manager 数据库的健康状况。 默认情况下，并非所有维护任务在每个站点都可用。 仅启用部分任务，但所有任务均支持你可设置的计划。  

 大多数维护任务定期从 Configuration Manager 数据库中删除过期数据。 通过删除不必要的数据降低数据库大小可以提高数据库的性能和完整性，从而提高站点和层次结构的效率。 其他任务（如**重建索引**）有助于维护数据库效率。 其他任务（如**备份站点服务器**任务）可帮助准备灾难恢复。  

> [!IMPORTANT]  
>  规划删除数据的任何任务的计划时，请考虑在整个层次结构中使用该数据的情况。 在站点中运行删除数据的任务时，会从 Configuration Manager 数据库中删除信息，这会更改复制到层次结构中的所有站点的内容。 此删除操作可能会影响依赖该数据的其他任务。 例如，在管理中心站点，可将“发现”设置为每月运行一次以识别非客户端计算机。 你计划在发现的两周内将 Configuration Manager 客户端安装到这些计算机。 但是，在层次结构的某个站点中，管理员将“删除过期的发现数据”任务设置为每 7 天运行一次。 结果是，在发现非客户端计算机的 7 天后，将从 Configuration Manager 数据库中删除它们。 你可以返回管理中心站点，并准备在第 10 天将 Configuration Manager 客户端请求安装到这些新计算机上。 然而，因为最近运行了“删除过期的发现数据”任务并且删除了已存在七天或更长时间的数据，所以最近发现的计算机在数据库中不再可用。  

在安装 Configuration Manager 站点之后，请查看可用的维护任务，并且启用操作所需的那些任务。 查看每项任务的默认计划，并在需要时设置计划进行维护任务的细微调整，使其适合你的层次结构和环境。 虽然每项任务的默认计划应适合大多数环境，但是，请监视站点和数据库的性能，且需细微调整任务以提高部署效率。 计划定期查看站点和数据库性能，并重新配置维护任务及其计划以维护该效率。  

#### <a name="set-up-maintenance-tasks"></a>设置维护任务  
 每个 Configuration Manager 站点都支持帮助维护站点数据库的运营效率的维护任务。 默认情况下，在每个站点中，启用了几项维护任务和所有任务都支持独立的日程安排。 为每个站点单独设置维护任务，并应用于该站点的数据库。 但是，某些任务（如**删除过期的发现数据**）会影响层次结构的所有站点中的可用信息。  

 Configuration Manager 控制台中仅显示可在站点中设置的维护任务。 有关按站点类型划分的维护任务的完整列表，请参阅 [System Center Configuration Manager 维护任务参考](../../../core/servers/manage/reference-for-maintenance-tasks.md)。  

 使用以下过程帮助设置维护任务的常见设置。  

###### <a name="to-set-up-maintenance-tasks-for-configuration-manager"></a>设置 Configuration Manager 的维护任务  

1.  在 Configuration Manager 控制台中，转到“管理” > “站点配置” >“站点”。  

2.  选择包含要设置的维护任务的站点。  

3.  在“主页”选项卡的“设置”组中，选择“站点维护”，然后选择要设置的维护任务。  

    > [!TIP]  
    >  仅显示所选站点中可用的任务。  

4.  若要设置任务，请选择“编辑”，确保选中“启用此任务”复选框并设置任务运行时间安排。 如果此任务还会删除过期的数据，请设置在任务运行时要从数据库中删除的数据的期限。 选择“确定”以关闭“属性”任务。  

    > [!NOTE]  
    >  对于“删除过期的状态消息”，需在设置状态筛选规则时设置要删除的数据的期限。  

5.  若要启用或禁用该任务，而不编辑任务属性，请选择“启用”或“禁用”按钮。 具体取决于任务的当前配置的按钮标签更改。  

6.  完成维护任务的配置后，选择“确定”完成该过程。
