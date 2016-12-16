---
title: "维护任务 | System Center Configuration Manager"
description: "了解针对 Configuration Manager 站点和层次结构执行的维护任务以及何时执行它们。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ac47f1b88a89a42bb51b87b36147b731e37a5824


---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager 的维护任务

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 站点和层次结构需要定期维护和监视以有效和连续提供服务。 通过进行定期维护，可以确保硬件、软件和 Configuration Manager 数据库继续正常和有效地运行。 最佳性能大大降低了出现故障的风险。  

 若要配置警报以及使用状态系统监视 Configuration Manager 的运行状况，请参阅[使用 System Center Configuration Manager 的警报和状态系统](../../../core/servers/manage/use-alerts-and-the-status-system.md)。  

-   [维护任务](#bkmk_MTs)  

##  <a name="a-namebkmkmtsa-maintenance-tasks"></a><a name="bkmk_MTs"></a>维护任务  
 执行定期维护对于确保正确的站点操作非常重要。 请维护维护日志，以记录维护的执行日期、执行者以及关于所执行任务的任何维护相关备注。  

### <a name="when-to-perform-common-maintenance-tasks"></a>何时执行常见维护任务  
 要维护站点，请考虑每日、每周执行定期维护，对于某些任务，请考虑更具间歇性的计划。 常见维护可以包括内置维护任务和其他任务（如帐户维护）以维护公司策略符合性。  

 使用下列信息作为指南以帮助你计划执行不同维护任务的时间。 使用这些列表作为起点，并添加你可能需要的任何其他任务。  

**每日任务**   
以下是你可能考虑每天执行的维护任务：  

-   验证计划每日运行的预定义维护任务是否成功运行  

-   检查 Configuration Manager 数据库状态  

-   检查站点服务器状态  

-   检查 Configuration Manager 站点系统收件箱是否存在文件积压  

-   检查站点系统状态  

-   检查站点系统上的操作系统事件日志  

-   检查站点数据库计算机上的 SQL Server 错误日志  

-   检查系统性能  

-   检查 Configuration Manager 警报  

**每周任务**   
以下是你可能考虑每周执行的维护任务：  

-   验证计划每周运行的预定义维护任务是否成功运行。  

-   从站点系统中删除不必要的文件  

-   制作并分发最终用户报告（如果需要）  

-   备份应用程序、安全和系统事件日志并将其清除  

-   检查站点数据库大小，并验证站点数据库服务器上是否有足够的可用磁盘空间，以便站点数据库可以增大  

-   按照 SQL Server 维护计划对站点数据库执行 SQL Server 数据库维护  

-   检查所有站点系统上的可用磁盘空间  

-   在所有站点系统上运行磁盘碎片整理工具  

**定期任务**   
某些任务不必在每日或每周维护期间执行，但对于确保站点的总体运行状况以及安全和灾难恢复计划为最新计划很重要。 以下是你可能考虑定期（比每日或每周任务更频繁）执行的维护任务：  

-   如有必要，按照安全计划更改帐户和密码  

-   查看维护计划以验证是否根据配置的站点设置正确并有效地计划了所计划的维护任务  

-   查看任何所需更改的 Configuration Manager 层次结构设计  

-   检查网络性能以确保未进行影响站点操作的更改  

-   验证是否尚未更改影响站点操作的 Active Directory 设置。 例如，验证是否尚未更改分配给用作 Configuration Manager 站点边界的 Active Directory 站点的子网  

-   查看灾难恢复计划是否有任何必需的更改  

-   通过使用“备份站点服务器”维护任务所创建的最新备份的备份副本，在测试实验室中按照灾难恢复计划执行站点恢复  

-   检查硬件是否有任何错误，或者是否有可用的硬件更新  

-   检查站点的总体运行状况  

###  <a name="a-namebkmkusemtsa-maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a>维护站点数据库的操作运行状况  
 当 Configuration Manager 站点和层次结构执行你计划和配置的任务时，站点组件不断将数据添加到 Configuration Manager 数据库中。 随着数据量增大，数据库性能和数据库中的可用存储空间将降低。 你可以将站点维护任务配置为删除不再需要的过时数据。  

 Configuration Manager 提供预定义的维护任务，你可以使用这些任务维护 Configuration Manager 数据库的健康状况。 并非所有维护任务都可以在每个站点中使用，默认情况下，一些任务处于启用状态，而某些任务未处于启用状态，所有任务都支持可配置的运行时间计划。  

 大多数维护任务定期从 Configuration Manager 数据库中删除过期数据。 通过删除不必要的数据降低数据库大小可以提高数据库的性能和完整性，从而提高站点和层次结构的效率。 诸如“重建索引” 之类的其他任务有助于维护数据库效率，而诸如“备份站点服务器”  之类的某些任务有助于你为灾难恢复做好准备。  

> [!IMPORTANT]  
>  规划删除数据的任何任务的计划时，请考虑在整个层次结构中使用该数据的情况。 在站点中运行删除数据的任务时，会从 Configuration Manager 数据库中删除信息，这会更改复制到层次结构中的所有站点的内容。 这可能会影响依赖于该数据的其他任务。 例如，在管理中心站点，你可以将发现配置为每月运行一次以标识非客户端计算机，并且可以计划将 Configuration Manager 客户端安装到两周内发现的那些计算机上。 然而，在层次结构中的一个站点，管理员将“删除过期的发现数据”任务配置为每七天运行一次，结果在发现非客户端计算机的七天后，会从 Configuration Manager 数据库中删除它们。 你可以返回管理中心站点，并准备在第 10 天将 Configuration Manager 客户端请求安装到这些新计算机上。 然而，因为最近运行了“删除过期的发现数据”任务并且删除了已存在七天或更长时间的数据，所以最近发现的计算机在数据库中不再可用。  

在安装 Configuration Manager 站点之后，请查看可用的维护任务，并且启用操作所需的那些任务。 查看每项任务的默认计划，在需要时，请修改计划以对维护任务进行细微调整，从而适合你的层次结构和环境。 虽然每项任务的默认计划应该适合大多数环境，但是，请监视站点和数据库的性能，并且应该对任务进行细微调整以提高部署的效率。 计划定期查看站点和数据库性能，以及重新配置维护任务及其计划以维护该效率。  

#### <a name="configure-maintenance-tasks"></a>配置维护任务  
 每个 Configuration Manager 站点都支持帮助维护站点数据库的运营效率的维护任务。 默认情况下，在每个站点中，启用了几项维护任务和所有任务都支持独立的日程安排。 维护任务为每个站点单独配置和将应用于在该站点; 数据库但是，某些任务如 **删除过期的发现数据**, ，会影响层次结构中的所有站点中可用的信息。  

 Configuration Manager 控制台中仅显示可以在站点中配置的维护任务。 有关按站点类型划分的维护任务的完整列表，请参阅 [System Center Configuration Manager 维护任务参考](../../../core/servers/manage/reference-for-maintenance-tasks.md)  

 使用以下过程来帮助你配置的维护任务的常见设置。  

###### <a name="to-configure-maintenance-tasks-for-configuration-manager"></a>若要配置为 Configuration Manager 的维护任务  

1.  在 Configuration Manager 控制台中，导航至“管理” > “站点配置” >“站点”。  

2.  选择包含您想要配置的维护任务的站点。  

3.  在上 **主页** 选项卡上，在 **设置** 组中，单击 **站点维护**, ，然后选择你想要配置的维护任务。  

    > [!TIP]  
    >  仅显示的任务可在所选的站点。  

4.  若要配置任务时，请单击 **编辑**, ，确保 **启用此任务** 复选框已选中并配置计划的任务的运行时。 如果该任务还将删除的过期的数据，则配置的任务运行时从数据库删除的数据的期限。 单击 **确定** 要关闭任务 **属性**。  

    > [!NOTE]  
    >  对于 **删除过期的状态消息**, ，配置的数据以在配置状态筛选规则时删除的期限。  

5.  若要启用或禁用该任务而无需编辑任务属性，请单击 **启用** 或 **禁用** 按钮。 具体取决于任务的当前配置的按钮标签更改。  

6.  在您完成配置的维护任务，请单击 **确定** 以完成该过程。



<!--HONumber=Nov16_HO1-->


