---
title: "迁移对象 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 环境中规划跨层次结构的对象迁移。"
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 17f3955aa7c63a13bab03b46002f7de0b0ec38fe
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-system-center-configuration-manager"></a>规划将 Configuration Manager 对象迁移到 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

借助 System Center Configuration Manager，可以迁移与源站点上的不同功能关联的许多不同对象。 使用下列部分来帮助你规划层次结构之间的对象迁移。  

-   [规划软件更新迁移](#Plan_migrate_Software_updates)  

-   [规划内容迁移](#Plan_Migrate_content)  

-   [规划集合迁移](#BKMK_MigrateCollections)  

-   [规划操作系统部署迁移](#Plan_migrate_OSD)  

-   [规划所需的配置管理的迁移](#Plan_Migrate_Compliance_settings)  

-   [规划边界迁移](#Plan_migrate_Boundaries)  

-   [规划报表迁移](#Plan_Migrate_reports)  

-   [规划组织文件夹和搜索文件夹的迁移](#Plan_Migrate_Org_Folders)  

-   [规划资产智能自定义项的迁移](#Plan_Migrate_AI)  

-   [规划软件计数规则自定义的迁移](#Plan_Migrate_SWM_Rules)  

##  <a name="Plan_migrate_Software_updates"></a>规划软件更新迁移  
 可以迁移软件更新对象，例如软件更新包和软件更新部署。  

 要成功迁移软件更新对象，必须首先将目标层次结构设置为包含与源层次结构环境匹配的配置。 这需要进行以下操作：  

-   在目标层次结构中部署活动软件更新点  

-   设置产品目录和语言以与源层次结构的配置匹配  

-   将目标层次结构中的软件更新点与 Windows Server Update Services (WSUS) 同步  

在迁移软件更新时，请考虑下列事项：  

-   如果尚未同步目标层次结构中的信息以与源层次结构中的配置匹配，软件更新对象的迁移可能会失败。  

    > [!WARNING]  
    >  Configuration Manager 不支持使用 WSUSutil 工具在源和目标层次结构之间同步数据。  

-   你无法迁移通过使用 System Center Updates Publisher 发布的自定义更新， 而是必须将自定义更新重新发布到目标层次结构。  

在从 Configuration Manager 2007 源层次结构中进行迁移时，迁移过程会将某些软件更新对象修改为目标层次结构使用的格式。 使用下表来帮助你规划从 Configuration Manager 2007 进行的软件更新对象迁移。  

|Configuration Manager 2007 对象|迁移后的对象名称|  
|-----------------------------------|---------------------------------|  
|软件更新列表|软件更新列表将转换为软件更新组。|  
|软件更新部署|软件更新部署将转换为部署和更新组。<br /><br /> 从 Configuration Manager 2007 中迁移软件更新部署后，必须在目标层次结构中启用该部署，然后才能使用它。|  
|软件更新包|软件更新包仍然是软件更新包。|  
|软件更新模板|软件更新模板仍然是软件更新模板。<br /><br /> Configuration Manager 2007 部署中的“持续时间”值不会迁移。|  

从 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构中迁移对象时，不会修改软件更新对象。  

##  <a name="Plan_Migrate_content"></a>规划内容迁移  
 你可以将内容从支持的源层次结构迁移到目标层次结构。 对于 Configuration Manager 2007 源层次结构，此内容包括软件分发包以及程序和虚拟应用程序，如 Microsoft Application Virtualization (App-V)。 对于 System Center 2012 Configuration Manager 和 System Center Configuration Manager 源层次结构，此内容包括应用程序和 App-V 虚拟应用程序。 在层次结构之间迁移内容时，压缩的源文件迁移到目标层次结构。  

### <a name="packages-and-programs"></a>包和程序  
 当你迁移包和程序时，迁移过程不会对其进行修改。 但是，在迁移这些包和程序之前，必须设置每个包以便为其源文件位置使用通用命名约定 (UNC) 路径。 在进行配置以迁移包和程序的过程中，你必须在目标层次结构中分配一个站点来管理此内容。 不会从分配的站点中迁移内容，但在迁移之后，分配的站点将通过使用 UNC 映射来访问原始源文件位置。  

 将包和程序迁移到目标层次结构之后，并且从源层次结构中进行的迁移处于活动状态时，你可以通过使用共享的分发点使内容可供该层次结构中的客户端使用。 若要使用共享的分发点，内容在源站点的分发点上必须保持为可访问。 有关共享的分发点的详细信息，请参阅[在 System Center Configuration Manager 中规划内容部署迁移策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)中的[在源和目标层次结构之间共享分发点](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)。  

 对于已迁移的内容，如果内容版本在源层次结构或目标层次结构中发生变化，则客户端将不再能够从目标层次结构中共享的分发点中访问内容。 在这种情况下，你必须重新迁移内容以还原源层次结构和目标层次结构之间一致的包版本。 此信息在数据收集周期中同步。  

> [!TIP]  
>  对于每个所迁移的包，请更新目标层次结构中的包。 此操作可以防止将包部署到目标层次结构中的分发点时产生问题。 但是，当更新目标层次结构分发点中的包时，该层次结构中的客户端将不再能够从共享的分发点获取该程序包。 要更新目标层次结构中的包，请在 Configuration Manager 控制台中转到“软件库”，右键单击此包，然后选择“更新分发点”。 对于每个迁移的包执行此操作。  

> [!TIP]  
>  可以使用 Microsoft System Center Configuration Manager 包转换管理器将包和程序转换成 System Center Configuration Manager 应用程序。 请从 [Microsoft Download Center（Microsoft 下载中心）](http://go.microsoft.com/fwlink/p/?LinkId=212950) 站点中下载包转换管理器。 有关详细信息，请参阅 [Configuration Manager 包转换管理器](http://go.microsoft.com/fwlink/p/?LinkId=247245)。  

### <a name="virtual-applications"></a>虚拟应用程序  
从支持的 Configuration Manager 2007 站点中迁移 App-V 包时，迁移过程会将这些包转换为目标层次结构中的应用程序。 此外，将根据 App-V 包的现有播发在目标层次结构中创建下列部署类型：  

-   如果没有播发，则会创建一个使用默认部署类型设置的部署类型。  

-   如果存在一个播发，则会创建一个使用与 Configuration Manager 2007 播发相同的设置的部署类型。  

-   如果存在多个播发，则会使用该播发的设置为每个 Configuration Manager 2007 播发创建一个部署类型。  

> [!IMPORTANT]  
>  如果迁移以前迁移过的 Configuration Manager 2007 App-V 包，则迁移将失败，原因是虚拟应用程序包不支持覆盖迁移行为。 在这种情况下，你必须从目标层次结构中删除迁移的虚拟应用程序包，然后创建一个新迁移作业来迁移虚拟应用程序。  

> [!NOTE]  
>  迁移 App-V 包之后，可以使用更新内容向导来更改 App-V 部署类型的源路径。 有关如何更新部署类型内容的详细信息，请参阅 [System Center Configuration Manager 应用程序的管理任务](../../apps/deploy-use/management-tasks-applications.md)中的“如何管理部署类型”。  

从 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构中进行迁移时，除了 App-V 部署类型和应用程序外，还可以迁移 App-V 虚拟环境的对象。 有关 App-V 环境的详细信息，请参阅[使用 System Center Configuration Manager 部署 App-V 虚拟应用程序](../../apps/get-started/deploying-app-v-virtual-applications.md)。  

### <a name="advertisements"></a>播发  
可以通过使用基于集合的迁移将播发从支持的 Configuration Manager 2007 源站点迁移到目标层次结构。 如果升级客户端，它将保留以前运行的播发的历史记录以防止客户端重新运行已迁移的播发。  

> [!NOTE]  
>  你无法迁移虚拟包的播发。 这是播发迁移的一个例外。  

### <a name="applications"></a>应用程序  
 可以将应用程序从支持的 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构迁移到目标层次结构中。 如果将客户端从源层次结构重新分配到目标层次结构，则客户端将保留以前安装的应用程序的历史记录以防止客户端重新运行已迁移的应用程序。  

##  <a name="BKMK_MigrateCollections"></a>规划集合迁移  
 可以从支持的 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构迁移集合的条件。 为此，请使用基于对象的迁移作业。 在迁移集合时，你将迁移集合的规则，而不是有关集合成员的信息，或者与集合成员相关的信息或对象。  

 在从 Configuration Manager 2007 源层次结构中进行迁移时，不支持迁移集合对象。  

##  <a name="Plan_migrate_OSD"></a>规划操作系统部署迁移  
你可以从支持的源层次结构中迁移下列操作系统部署对象：  

-   操作系统映像和包。 启动映像的源路径在目标站点上将更新为 Windows 管理安装工具包 (Windows AIK) 的默认映像位置。 下面是迁移操作系统映像和包的要求及限制：  

    -   要成功迁移映像文件，目标层次结构顶层站点的 SMS 提供程序服务器的计算机帐户必须具有源站点 Windows AIK 位置的映像源文件的“读取”和“写入”权限。  

    -   在迁移操作系统安装包时，请确保源站点上包的配置指向包含 WIM 文件的文件夹，而不是指向 WIM 文件本身。 如果安装包指向 WIM 文件，安装包的迁移将失败。  

    -   从 Configuration Manager 2007 源站点中迁移启动映像包时，此包的包 ID 不会保留在目标站点中。 结果是，目标层次结构中的客户端无法使用在共享的分发点上可用的启动映像包。  

-   任务序列。 在迁移包含对客户端安装包的引用的任务序列时，会将该引用替换为对目标层次结构的客户端安装包的引用。  

    > [!NOTE]  
    >  在迁移任务序列时，Configuration Manager 可能会迁移目标层次结构中不需要的对象。 这些对象包括启动映像和 Configuration Manager 2007 客户端安装包。  

-   驱动程序和驱动程序包。 在迁移驱动程序包时，目标层次结构中 SMS 提供程序的计算机帐户必须可以完全控制包源。

##  <a name="Plan_Migrate_Compliance_settings"></a>规划所需的配置管理的迁移  
你可以迁移配置项目和配置基线。  

> [!NOTE]  
>  迁移不支持 Configuration Manager 2007 源层次结构中未解释的配置项目。 你无法将这些配置项目迁移或导入到目标层次结构。 有关未解释的配置项目的详细信息，请参阅 Configuration Manager 2007 文档库的[关于所需的配置管理中的配置项目](http://go.microsoft.com/fwlink/?LinkId=103846)主题中的“未解释的配置项目”。  

可以导入 Configuration Manager 2007 配置包。 导入过程会自动转换配置包以与 System Center Configuration Manager 兼容。  

##  <a name="Plan_migrate_Boundaries"></a>规划边界迁移  
 你可以在层次结构之间迁移边界。 从 Configuration Manager 2007 中迁移边界时，源站点中的每个边界会同时迁移，而且将添加到在目标层次结构中创建的新边界组。 从 System Center 2012 Configuration Manager 或 System Center Configuration Manager 层次结构中迁移边界时，你选择的每个边界均将添加到目标层次结构中的新边界组。  

 将为内容位置启用自动创建的每个边界组，但不会为站点分配这样做。 这可以防止在源和目标层次结构之间出现站点分配的重叠边界。 从 Configuration Manager 2007 源站点中迁移有助于防止新安装的 Configuration Manager 2007 客户端错误地分配到目标层次结构。 默认情况下，System Center Configuration Manager 客户端不会自动分配到 Configuration Manager 2007 站点。  

 在迁移过程中，如果与目标层次结构共享分发点，则与该分发点关联的任何边界都会自动迁移到目标层次结构。 在目标层次结构中，迁移过程会为每个共享的分发点创建一个新的只读边界组。 如果更改源层次结构中的分发点的边界，则在下次数据收集周期中，会使用这些更改来更新目标层次结构中的边界组。  

##  <a name="Plan_Migrate_reports"></a>规划报表迁移  
Configuration Manager 不支持迁移报表。 实际上，它使用 SQL Server Reporting Services Report Builder 从源层次结构中导出报表，然后将它们导入到目标层次结构。  

> [!NOTE]  
>  由于对 Configuration Manager 2007 和 System Center Configuration Manager 之间的报表进行了架构上的更改，请测试从 Configuration Manager 2007 层次结构导入的每个报表，以确保它们正常工作。  

有关报表的详细信息，请参阅 [System Center Configuration Manager 中的报表](../../core/servers/manage/reporting.md)。  

##  <a name="Plan_Migrate_Org_Folders"></a>规划组织文件夹和搜索文件夹的迁移  
 可以将组织文件夹和搜索文件夹从支持的源层次结构迁移到目标层次结构。 此外，可以将保存的搜索条件从 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构迁移到目标层次结构中。  

 默认情况下，在迁移时迁移过程将为对象和集合保持搜索文件夹和管理文件夹的结构。 但是，在“创建迁移作业向导”的“设置”页上，可以将迁移作业设置为不迁移对象的组织结构（取消勾选此选项的框）。 将始终保持集合的组织结构。  

 但包含虚拟应用程序的搜索文件夹是一个例外。 在迁移 App-V 包时，会将 App-V 包转换为 System Center Configuration Manager 中的应用程序。 在迁移搜索文件夹之后，只会查找剩余的包，而且搜索文件夹无法查找 App-V 包，因为在迁移 App-V 包时已将此包转换为应用程序。  

 从 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构中迁移已保存的搜索时，将迁移搜索的条件，而不是有关搜索结果的信息。 迁移已保存的搜索并不适用于 Configuration Manager 2007 源站点。  

##  <a name="Plan_Migrate_AI"></a>规划资产智能自定义项的迁移  
 可以将资产智能的自定义从支持的源层次结构迁移到目标层次结构。 在 Configuration Manager 2007 与 System Center Configuration Manager 之间，资产智能自定义的结构并无显著变化。  

> [!NOTE]  
>  System Center Configuration Manager 不支持从使用 Asset Intelligence Service 2.0 (AIS 2.0) 的 Configuration Manager 2007 站点中迁移资产智能对象。  

##  <a name="Plan_Migrate_SWM_Rules"></a>规划软件计数规则自定义的迁移  
 在 Configuration Manager 2007 与 System Center Configuration Manager 之间，软件计数并无显著变化。 可以将软件计数规则从支持的源层次结构迁移到目标层次结构。  

 默认情况下，迁移到目标层次结构的软件计数规则不会与目标层次结构中的特定站点关联，而是应用到层次结构中的所有客户端。 若要将软件计数规则应用到特定站点中的客户端，必须在迁移计数规则后编辑它。  
