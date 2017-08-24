---
title: "迁移操作 | Microsoft Docs"
description: "创建并运行作业，将数据和客户端迁移到 System Center Configuration Manager。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: fb8a292c4fecbe5744e2cd09bc1442fab11046bc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="operations-for-migrating-to-system-center-configuration-manager"></a>用于迁移到 System Center Configuration Manager 的操作

*适用范围：System Center Configuration Manager (Current Branch)*

对于 System Center Configuration Manager 中的迁移，在从支持的源层次结构中的源站点成功收集数据后，即可迁移数据和客户端。 使用下列部分中的信息来创建和运行迁移作业以便迁移数据和客户端，并随后完成迁移过程。  

-   [创建和编辑迁移作业](#Create_Edit_migration_Jobs)  

-   [运行迁移作业](#Run_Migration_Jobs)  

-   [升级或重新分配共享分发点](#BKMK_ProcUpgrdSS)  

-   [在“迁移”工作区中监视迁移活动](#Monitor_MIgration)  

-   [迁移客户端](#BKMK_MigrateClients)  

-   [完成迁移](#Complete_Migration)  

##  <a name="Create_Edit_migration_Jobs"></a> 创建和编辑迁移作业  
 使用以下过程来创建数据迁移作业、编辑基于集合的迁移作业的排除列表、设置共享的分发点，以及编辑迁移作业计划。  

> [!NOTE]  
>  以下用于创建按集合进行迁移的迁移作业的过程仅适用于运行 Configuration Manager 2007 的受支持版本的源层次结构。 从 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构中迁移时，基于集合的迁移作业类型不可用。  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>创建迁移作业以按集合进行迁移  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“迁移”，然后选择“迁移作业”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建迁移作业”。  

4.  在创建迁移作业向导的“常规”页上，设置以下各项，然后选择“确定”：  

    -   指定迁移作业的名称。  

    -   在“作业类型”  下拉列表中，选择“集合迁移” 。  

5.  在“选择集合”页上，设置以下各项，然后选择“下一步”：  

    -   选择要迁移的集合。  

    -   如果要仅迁移集合，而不迁移与这些集合关联的对象，请取消选中“迁移与指定集合关联的对象”。 如果取消选中此选项，则不会在此作业中迁移关联的对象，因此你可跳过步骤 6 和 7。  

6.  在“选择对象”页上，取消选中你不希望迁移的任何对象类型或特定可用对象。 默认情况下，所有关联的对象类型和可用对象都处于选定状态。 选择“下一步”。  

7.  在“内容所有权”页上，将每个列出的源站点中的内容的所有权分配给目标层次结构中的站点，然后选择“下一步”。  

8.  在“安全作用域”页上，选择一个或多个基于角色的管理安全作用域，以分配给要在此迁移作业中迁移的对象，然后选择“下一步”。  

9. 在“集合限制”页上，设置目标层次结构中的集合以限制每个列出的集合的作用域，然后选择“下一步”。 如果未列出集合，请选择“下一步”。  

10. 在“站点代码替换”页上，分配目标层次结构中的一个站点代码以替换每个列出的集合的 Configuration Manager 2007 站点代码，然后选择“下一步”。 如果未列出集合，请选择“下一步”。  

11. 在“查看信息”页上，选择“保存到文件”保存显示的信息，供以后查看。 当你准备好继续时，选择“下一步”。  

12. 在“设置”页上，设置迁移作业的运行时间，并选择此迁移作业所需的任何其他设置，然后选择“下一步”。  

13. 确认设置并完成向导。  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>创建迁移作业以按对象进行迁移  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“迁移”，然后选择“迁移作业”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建迁移作业”。  

4.  在创建迁移作业向导的“常规”页上，设置以下各项，然后单击“下一步”：  

    -   指定迁移作业的名称。  

    -   在“作业类型”  下拉列表中，选择“对象迁移” 。  

5.  在“选择对象”  页上，选择要迁移的对象类型。 默认情况下，会为所选的每种对象类型选择所有可用对象。  

6.  在“内容所有权”页上，将每个列出的源站点中的内容的所有权分配给目标层次结构中的站点，然后选择“下一步”。 如果未列出源站点，请选择“下一步”。  

7.  在“安全作用域”页上，选择一个或多个基于角色的管理安全作用域，以分配给此迁移作业中的对象，然后选择“下一步”。  

8.  在“查看信息”页上，选择“保存到文件”保存显示的信息，供以后查看。 当你准备好继续时，选择“下一步”。  

9. 在“设置”页上，设置迁移作业的运行时间，并选择此迁移作业所需的任何其他设置。 然后选择“下一步”。  

10. 确认设置并完成向导。  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>创建迁移作业以迁移更改的对象  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“迁移”，然后选择“迁移作业”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建迁移作业”。  

4.  在创建迁移作业向导的“常规”页上，设置以下各项，然后选择“下一步”：  

    -   指定迁移作业的名称。  

    -   在“作业类型”下拉列表中，选择“迁移之后修改的对象”。  

5.  在“选择对象”  页上，选择要迁移的对象类型。 默认情况下，会为所选的每种对象类型选择所有可用对象。  

6.  在“内容所有权”页上，将每个列出的源站点中的内容的所有权分配给目标层次结构中的站点，然后选择“下一步”。 如果未列出源站点，请选择“下一步”。  

7.  在“安全作用域”页上，选择一个或多个基于角色的管理安全作用域，以分配给此迁移作业中的对象，然后选择“下一步”。  

8.  在“查看信息”页上，选择“保存到文件”保存显示的信息，供以后查看。 当你准备好继续时，选择“下一步”。  

9. 在“设置”页上，设置迁移作业的运行时间，并选择此迁移作业需要的任何其他设置。 与其他迁移作业类型不同，此迁移作业必须覆盖 System Center Configuration Manager 数据库中以前迁移的对象。 选择“下一步”。  

10. 确认设置，然后完成向导。  

###  <a name="BKMK_Modify_Exclusion_List"></a>修改迁移的排除列表  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，选择“迁移”以访问排除列表。 你也可以从“源层次结构”  或“迁移作业”  节点中访问排除列表。  

3.  在“主页”选项卡上的“迁移”组中，选择“编辑排除列表”。  

4.  在“编辑排除列表”对话框中，选择要从排除列表中删除的已排除对象，然后选择“删除”。  

5.  选择“确定”保存更改并完成编辑。 要取消当前更改并还原所有已删除的对象，请选择“取消”，然后选择“否”。 这将取消对象的删除，并关闭“编辑排除列表”  对话框。  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>从源层次结构中共享分发点  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“迁移”，选择“源层次结构”，然后选择要设置的源站点。  

3.  在“主页”选项卡上的“源站点”组中，选择“配置”。  

4.  在“源站点凭据”对话框上，选择“为源站点服务器启用分发点共享”，然后选择“确定”。  

5.  数据收集完成时，选择“关闭”。  

#### <a name="change-the-schedule-of-a-migration-job"></a>更改迁移作业的计划  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“迁移”，然后选择“迁移作业”。  

3.  选择要更改的迁移作业。 在“主页”选项卡上的“属性”组中，选择“属性”。  

4.  在迁移作业的属性中，选择“设置”选项卡，更改迁移作业的运行时间，然后选择“确定”。  

##  <a name="Run_Migration_Jobs"></a> 运行迁移作业  
 使用以下过程来运行尚未启动的迁移作业。  


1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“迁移”，然后选择“迁移作业”。  

3.  选择要运行的迁移作业。 在“主页”选项卡上的“迁移作业”组中，选择“启动”。  

4.  选择“是”以启动迁移作业。  

##  <a name="BKMK_ProcUpgrdSS"></a> 升级或重新分配共享分发点  
 可以升级从 Configuration Manager 2007 源站点中共享的受支持的分发点（或重新分配从 System Center Configuration Manager 源站点中共享的受支持的分发点）以成为目标层次结构中的分发点。  

> [!IMPORTANT]  
>  升级 Configuration Manager 2007 分支分发点之前，必须从分支分发点计算机中卸载 Configuration Manager 2007 客户端软件。 如果 Configuration Manager 2007 客户端软件是在尝试升级分发点时安装的，则升级将失败，并且将从计算机中删除以前部署到分支分发点的内容。  

> [!CAUTION]  
>  当你升级或重新分配共享的分发点时，将从源站点中删除分发点站点系统角色和站点系统计算机，并将其作为分发点添加到所选目标层次结构中的站点。  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>升级或重新分配共享分发点  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“迁移”，然后选择“源层次结构”。  

3.  选择拥有要升级的分发点的站点，选择“共享的分发点”选项卡，并选择要升级或重新分配的合格分发点。  

4.  在“分发点”选项卡上的“分发点”组中，选择“重新分配”。  

5.  在“重新分配共享分发点向导”中指定设置，与为目标层次结构安装新分发点一样，但增加了以下步骤：  

    -   在“内容转换”页上，查看有关转换现有内容所需空间的指导。 然后，在向导的“驱动器设置”页上，确保所选分发点计算机的驱动器具有所需的可用磁盘空间量。  

6.  确认设置，然后完成向导。  

##  <a name="Monitor_MIgration"></a> 在“迁移”工作区中监视迁移活动  
 使用 Configuration Manager 控制台监视迁移。  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“迁移”，然后选择“迁移作业”。  

3.  选择要监视的迁移作业。  

4.  在“摘要”  和“作业对象” 选项卡上查看有关所选迁移作业的详细信息和状态。  

##  <a name="BKMK_MigrateClients"></a> 迁移客户端  
 在层次结构之间迁移客户端数据之后，但在完成迁移之前，计划将客户端迁移到目标层次结构。 层次结构之间客户端的迁移涉及从分配给源层次结构的计算机中卸载 Configuration Manager 客户端软件，然后从目标层次结构中安装 Configuration Manager 客户端软件。 在从目标层次结构中安装客户端时，还会将客户端分配给该层次结构中的主站点。 有关迁移客户端的详细信息，请参阅[在 System Center Configuration Manager 中规划客户端迁移策略](../../core/migration/planning-a-client-migration-strategy.md)。  

##  <a name="Complete_Migration"></a> 完成迁移  
 使用此过程来完成从源层次结构进行的迁移。  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“迁移”，然后选择“源层次结构”。  

3.  对于Configuration Manager 2007 源层次结构，选择位于源层次结构底部级别的源站点。 对于 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构，选择可用源站点。  

4.  在“主页”选项卡上的“清除”组中，选择“停止收集数据”。  

5.  选择“是”确认操作。  

6.  对于Configuration Manager 2007 源层次结构，请在继续下一步之前重复执行步骤 3、4 和 5。 在层次结构中的每个位置执行这些步骤（从层次结构的底层到顶层）。 对于 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构，继续下一步。  

7.  在“主页”选项卡上的“清除”组中，选择“清理迁移数据”。  

8.  在“清理迁移数据”对话框上，从“源层次结构”下拉列表中选择源层次结构的顶层站点的站点代码和站点服务器，然后选择“确定”。  

9. 选择“是”完成源层次结构的迁移过程。  
