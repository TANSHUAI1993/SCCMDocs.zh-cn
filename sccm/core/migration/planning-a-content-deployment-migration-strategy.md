---
title: "迁移内容 |System Center Configuration Manager"
description: "将数据迁移到 System Center Configuration Manager 目标层次结构中时，使用分发点来管理内容。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aa88f18247b49995bff4a4a6f5fd1e1ed70ca214


---
# <a name="planning-a-content-deployment-migration-strategy-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中规划内容部署迁移策略

*适用范围：System Center Configuration Manager (Current Branch)*

在以主动方式将数据迁移到 System Center Configuration Manager 目标层次结构时，源和目标层次结构中的 Configuration Manager 客户端都能继续访问在源层次结构中部署的内容。 此外，你可以使用迁移升级或重新分配源层次结构中的分发点，以成为目标层次结构中的分发点。 在共享和升级或重新分配分发点时，此策略使你不必为你迁移的客户端将内容重新部署到目标层次结构中的新服务器。  

尽管你可以在目标层次结构中重新创建和分发内容，但你也可以使用下列选项来管理此内容：  

-   将源层次结构中的分发点与目标层次结构中的客户端共享。  

-   将源层次结构中的独立 Configuration Manager 2007 分发点或 Configuration Manager 2007 辅助站点升级成为目标层次结构中的分发点。  

-   将分发点从 System Center Configuration Manager 源层次结构重新分配到目标层次结构中的站点。  

使用下列部分来帮助你在迁移过程中规划内容部署：  

-   [在源和目标层次结构之间共享分发点](#About_Shared_DPs_in_Migration)  

-   [计划升级 Configuration Manager 2007 共享的分发点](#Planning_to_Upgrade_DPs)  

    -   [分发点升级过程](#BKIMK_UpgradeProcess)  

    -   [Planning to upgrade Configuration Manager 2007 secondary sites](#BKMK_UpgradeSS)  

-   [规划 System Center Configuration Manager 分发点的重新分配](#BKMK_ReassignDistPoint)  

    -   [分发点重新分配过程](#BKMK_ReassignProcess)  

-   [迁移内容时的内容所有权](#About_Migrating_Content)  

##  <a name="a-nameaboutshareddpsinmigrationa-share-distribution-points-between-source-and-destination-hierarchies"></a><a name="About_Shared_DPs_in_Migration"></a> 在源和目标层次结构之间共享分发点  
在迁移过程中，你可以将源层次结构中的分发点与目标层次结构共享。 你可以使用共享的分发点，在不必重新创建内容的情况下使从源层次结构中迁移的内容立即可供目标层次结构中的客户端使用，然后将其分发给目标层次结构中的新分发点。 当目标层次结构中的客户端请求部署到你已共享的分发点的内容时，可将共享的分发点提供给客户端作为有效的内容位置。  

 除了成为目标层次结构中客户端的有效内容位置外，只要从源层次结构中进行的迁移仍在进行，就可以将分发点升级或重新分配到目标层次结构。 可以升级 Configuration Manager 2007 共享的分发点并重新分配 System Center 2012 Configuration Manager 共享分发点。 在升级或重新分配共享的分发点时，该分发点将被从源层次结构中删除并成为目标层次结构中的分发点。 升级或重新分配共享的分发点后，你可以在从源层次结构迁移完成后继续使用目标层次结构中的分发点。 有关如何升级共享分发点的详细信息，请参阅 [Planning to upgrade Configuration Manager 2007 shared distribution points](#Planning_to_Upgrade_DPs)。 有关如何重新分配共享的分发点的信息，请参阅 [规划 System Center Configuration Manager 分发点的重新分配](#BKMK_ReassignDistPoint)。  

 你可以选择共享源层次结构的任何源站点中的分发点。 在为源站点共享分发点时，将共享该主站点上以及该主站点的每个子辅助站点上的每个符合条件的分发点。 要符合作为共享的分发点的条件，承载分发点的站点系统服务器必须配置为具有完全限定的域名 (FQDN)。 将忽略配置为具有 NetBIOS 名称的任何分发点。  

> [!TIP]  
>  Configuration Manager 2007 不需要为站点系统服务器配置 FQDN。  

使用下列信息来帮助你规划共享的分发点：  

-   你共享的分发点必须满足共享的分发点的先决条件。 有关这些先决条件的信息，请参阅 [System Center Configuration Manager 中迁移的先决条件](../../core/migration/prerequisites-for-migration.md)主题中的[迁移的所需配置](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations)部分。  

-   共享分发点操作是站点范围的设置，它共享源站点和任何直接子辅助站点上的所有符合条件的分发点。 在启用分发点共享时，你无法选择单独的分发点进行共享。  

-   目标层次结构中的客户端可接收包的内容位置信息，这些包分发到从源层次结构中共享的分发点上。 对于 Configuration Manager 2007 源层次结构中的分发点，这包括分支分发点、服务器共享上的分发点以及标准分发点。  

    > [!WARNING]  
    >  如果你更改源层次结构，原始源层次结构中的共享的分发点将不再可用，并且无法作为内容位置提供给目标层次结构中的客户端。 如果重新配置迁移以使用原始源层次结构，则会还原以前共享的分发点作为有效的内容位置服务器。  

-   当你迁移共享的分发点上承载的包时，包版本在源层次结构和目标层次结构中必须相同。 如果包版本在源层次结构和目标层次结构中不相同，则目标层次结构中的客户端无法从共享的分发点中检索该内容。 因此，如果更新源层次结构中的包，你必须重新迁移包数据，然后目标层次结构中的客户端才能从共享的分发点中检索该内容。  

    > [!NOTE]  
    >  在查看共享的分发点上承载的包的详细信息时，在源站点“共享的分发点”  选项卡上显示为“承载的迁移包”  的包的数量将不会更新，直至下一个数据收集周期完成为止。  

-   可以从“管理”作区的“源层次结构”中查看共享的分发点及其属性，该工作区位于连接到目标层次结构的 Configuration Manager 控制台中。  

-   无法使用 Configuration Manager 2007 源层次结构中的共享的分发点来承载 Microsoft Application Virtualization (App-V) 的包。 App-V 包必须迁移并进行转换才能供目标层次结构中的客户端使用。 但是，可以使用 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构中的共享的分发点为目标层次结构中的客户端承载 App-V 包。  

-   在共享 Configuration Manager 2007 源层次结构中的受保护分发点时，目标层次结构将创建一个边界组，其中包括该分发点的受保护网络位置。 你无法在目标层次结构中修改此边界组。 但是，如果为 Configuration Manager 2007 源层次结构中的分发点更改受保护边界信息，在下一个数据收集周期完成后，该更改将反映在目标层次结构中。  

    > [!NOTE]  
    >  由于 System Center 2012 Configuration Manager 和 System Center Configuration Manager 站点使用首选分发点（而不是受保护分发点）的概念，因此，这种情况仅适用于从 Configuration Manager 2007 源站点中共享的分发点。  

在从源站点中共享分发点之前，合格分发点不会显示在 Configuration Manager 控制台中。 共享分发点之后，只会列出成功共享的分发点。  

共享了分发点之后，你可以在源层次结构中更改任何共享的分发点的配置。 对分发点的配置所做的更改将在下一个数据收集周期后反映在目标层次结构中。 你更新为符合共享条件的分发点会自动共享，而不再符合条件的那些分发点则会停止共享分发点。 例如，你可能有一个分发点，该分发点未配置为具有 Intranet FQDN，并且最初未与目标层次结构共享。 为该分发点配置 FQDN 之后，下一个数据收集周期将识别此配置，并随后与目标层次结构共享该分发点。  

##  <a name="a-nameplanningtoupgradedpsa-planning-to-upgrade-configuration-manager-2007-shared-distribution-points"></a><a name="Planning_to_Upgrade_DPs"></a> 计划升级 Configuration Manager 2007 共享的分发点  
在从 Configuration Manager 2007 源层次结构中迁移时，可以升级共享的分发点以使其成为 System Center Configuration Manager 分发点。 你可以在主站点和辅助站点上升级分发点。 升级过程将从 Configuration Manager 2007 层次结构中删除分发点，并使其成为目标层次结构中的站点系统服务器。 此过程还会将分发点上的现有内容复制到分发点计算机上的新位置。 然后，升级过程将修改内容的副本，创建单一实例存储以用于目标层次结构中的内容部署。 因此，在升级分发点时，不必重新分发 Configuration Manager 2007 分发点上承载的已迁移内容。  

在 Configuration Manager 将内容转换为单实例存储后，Configuration Manager 将删除分发点计算机上的原始源内容以释放磁盘空间，并且不使用原始源内容位置。  

并非所有可以共享的 Configuration Manager 2007 分发点都适合升级到 System Center Configuration Manager。 为了适合进行升级， Configuration Manager 2007 分发点必须满足升级条件，其中包括安装了分发点的站点系统服务器，以及所安装的 Configuration Manager 2007分发点的类型。 例如，你无法升级安装在主站点的站点服务器计算机上的任何类型的分发点，但可以升级安装在辅助站点的站点服务器计算机上的标准分发点。  

> [!NOTE]  
>  只能升级运行的操作系统版本对于目标层次结构中的分发点受支持的计算机上的那些 Configuration Manager 2007 共享的分发点。 例如，尽管可以共享运行 Windows Vista 的计算机上的 Configuration Manager 2007 分发点，但无法升级共享的此分发点，因为 System Center Configuration Manager 不支持将此操作系统用作分发点。  

下表列出了可升级的每种类型的 Configuration Manager 2007 分发点的受支持位置。  

|分发点的类型|位于站点系统计算机（而不是站点服务器）上的分发点|位于站点系统计算机（而不是站点服务器）上并承载其他站点系统角色的分发点|位于辅助站点服务器上的分发点|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|标准分发点|是|否|是|  
|位于服务器共享上的分发点<sup>1</sup>|是|否|否|  
|分支分发点|是|否|否|  

 <sup>1</sup> System Center Configuration Manager 对于站点系统不支持服务器共享，但支持升级位于服务器共享上的 Configuration Manager 2007 分发点。 在升级位于服务器共享上的 Configuration Manager 2007 分发点时，分发点类型会自动转换为服务器，并且必须选择将存储单一实例内容存储的分发点计算机上的驱动器。  

> [!WARNING]  
>  在升级分支分发点之前，请卸载 Configuration Manager 2007 客户端软件。 在升级安装了 Configuration Manager 2007 客户端软件的分支分发点时，将从计算机中删除以前部署到计算机的内容，并且分发点的升级将失败。  

若要标识适合于 Configuration Manager 控制台（位于“源层次结构”节点）中的升级的分发点，请选择源站点，然后选择“共享的分发点”选项卡。 适合的分发点在“适合升级”  列中显示“是”  。  

在升级 Configuration Manager 2007 辅助站点服务器上安装的分发点时，将从源层次结构中卸载辅助站点。 尽管此方案称为辅助站点升级，但这种情况仅适用于分发点站点系统角色。 结果是不会升级辅助站点，而是会将其卸载。 这只会在曾经是辅助站点服务器的计算机上留下一个目标层次结构中的分发点。 由于会从源层次结构中删除辅助站点，因此，如果你计划升级辅助站点上的分发点，请参阅本主题中的 [Planning to upgrade Configuration Manager 2007 secondary sites](#BKMK_UpgradeSS) 部分。  

###  <a name="a-namebkimkupgradeprocessa-distribution-point-upgrade-process"></a><a name="BKIMK_UpgradeProcess"></a> 分发点升级过程  
可以使用 Configuration Manager 控制台来升级已与目标层次结构共享的 Configuration Manager 2007 分发点。 当升级共享的分发点时，分发点会从 Configuration Manager 2007 站点中卸载，然后作为与在目标层次结构中指定的主站点或辅助站点相连的分发点进行安装。 升级过程将创建在分发点存储的迁移内容副本，然后将此副本转换为单一实例的内容存储。 当 Configuration Manager 将某个包转换为单一实例内容存储时，它将从分发点计算机上的 SMSPKG 共享删除该包，除非该包具有一个或多个配置为“从分发点运行程序”的播发。  

为升级分发点， Configuration Manager 会使用配置为“从源站点的 SMS 提供程序收集数据”的“源站点访问帐户”。 尽管此帐户仅要求具有站点对象的“读取”权限即可从源站点收集数据，但是它必须还具有“站点”类的“删除”和“修改”权限才能在升级过程中从 Configuration Manager 2007 站点成功删除分发点。  

> [!NOTE]  
>  Configuration Manager 一次仅可以将内容转化为一个分发点上的单一实例存储。 在你配置多个分发点升级时，分发点将排队等待升级并且一次处理一个分发点。  

在升级共享分发点之前，确保已迁移部署到分发点的所有内容。 对于在升级分发点前未迁移的内容，在升级之后，它们将在目标层次结构中不可用。 当你升级分发点时，迁移的包中的内容会转换为与目标层次结构的单一实例存储兼容的格式。  

若要从 Configuration Manager 控制台中升级分发点，Configuration Manager 2007 站点系统服务器必须满足下列条件：  

-   分发点配置和位置必须适合升级。  

-   分发点计算机必须具有足够的磁盘空间才能使内容从 Configuration Manager 2007 内容存储格式转换为单一实例存储格式。 此转换要求可用磁盘空间等于在分发点上存储的最大包的大小。  

-   作为目标层次结构中的分发点，分发点计算机所运行的操作系统版本必须受支持。  

    > [!NOTE]  
    >  当 Configuration Manager 检查分发点是否符合升级条件时，它不会验证分发点计算机的操作系统版本。  

若要升级分发点，请在“管理”  工作区中依次展开“迁移” 、“源层次结构”  节点，然后选择包含要升级的分发点的站点。 接下来，在“详细信息”窗格中“共享的分发点”  选项卡上，选择要升级的分发点。  

通过查看“适合重新分配”  列中的状态，可以确认分发点已准备好进行升级。  接下来，在 Configuration Manager 控制台功能区的“分发点”选项卡上，选择“分发点”组中的“重新分配”。 这将打开用于完成分发点升级的向导。  

在升级共享分发点时，必须将分发点分配给你在目标层次结构中选择的主站点或辅助站点。 在将分发点升级后，可与管理任何其他分发点一样，将分发点作为目标层次结构中的分发点进行管理。  

通过选择“分发点迁移”节点（位于“管理”工作区的“迁移”节点下），可以在 Configuration Manager 控制台中监视分发点升级的进度。 你还可以在目标层次结构的管理中心站点服务器上查看 **Migmctrl.log** 中的信息，或者也可以在负责管理已升级分发点的目标层次结构中的站点服务器上查看 **distmgr.log** 中的信息。  

> [!NOTE]  
>  在将分发点升级到目标层次结构时，将从 Configuration Manager 2007 源站点中删除分发点站点系统角色；但是，已发送至分发点的包不会在 Configuration Manager 2007 层次结构中更新。 在 Configuration Manager 2007 控制台中，已发送至分发点的包会继续将站点系统计算机列为“未知”“类型”的分发点。 如果对 Configuration Manager 2007 中的包进行后续更新，则将导致在站点尝试更新未知站点系统上的包时，该站点的 distmgr.log 中会出现分发管理器报表错误。  

如果决定不升级共享的分发点，则仍然可以在以前的 Configuration Manager 2007 分发点上安装一个目标层次结构中的分发点。 必须首先从分发点计算机上卸载所有 Configuration Manager 2007 站点系统角色，然后才能安装新的分发点。 如果这是站点服务器计算机，则这包括 Configuration Manager 2007 站点。 卸载 Configuration Manager 2007 分发点时，不会从计算机中删除部署到分发点的内容。  

###  <a name="a-namebkmkupgradessa-planning-to-upgrade-configuration-manager-2007-secondary-sites"></a><a name="BKMK_UpgradeSS"></a> Planning to upgrade Configuration Manager 2007 secondary sites  
 当使用迁移来升级 Configuration Manager 2007 辅助站点服务器上承载的共享分发点时，Configuration Manager 不仅会将分发点站点系统角色升级到目标层次结构中的分发点，而且还将从源层次结构中卸载辅助站点。 结果是 System Center Configuration Manager 分发点，而非辅助站点。  

 为使站点服务器计算机上的分发点适合升级， Configuration Manager 必须能够卸载辅助站点，其中包括该计算机上的每个站点系统角色。 通常，Configuration Manager 2007 服务器共享上的共享分发点适合升级。 但是，当辅助站点服务器上存在服务器共享时，辅助站点和该计算机上的任何共享分发点均不适合升级。 这是因为当该流程尝试卸载辅助站点时，服务器共享将作为附加站点系统对象处理，并且该流程无法卸载该对象。 在这种情况下，你可以在辅助站点服务器上启用标准分发点，然后将内容重新分发到该标准分发点。 这不占用网络带宽，并且在完成时，你可以卸载服务器共享上的分发点，删除服务器共享，然后升级分发点和辅助站点。  

 在升级共享分发点之前，审阅 Configuration Manager 2007 中的分发点配置以免升级仍要与 Configuration Manager 2007 一起使用的辅助站点上的分发点。 这是因为，在升级辅助站点服务器上的共享分发点之后，将从 Configuration Manager 2007 层次结构中删除站点系统服务器，并且不再可与该层次结构一起使用。 如果删除了辅助站点，该辅助站点上的任何其余分发点将会孤立。 这意味着，它们将脱离 Configuration Manager 2007 的管理，并且不再共享或适合升级。  

> [! 警告]  
>  在 Configuration Manager 控制台中查看共享的分发点时，没有指出共享分发点位于远程站点系统服务器上或者它是否位于辅助站点服务器上的明显指示。  

 如果你具有位于远程网络位置中的辅助站点，并且该辅助站点主要用于控制到该远程位置的内容部署，则考虑升级带共享分发点的辅助站点。 由于可就何时将内容分配到 System Center Configuration Manager 分发点进行带宽控制配置，因此可以经常将辅助站点升级为分发点、为带宽控制配置分发点，并避免在目标层次结构的该网络位置上安装辅助站点。  

 用于升级辅助站点服务器上的共享分发点的流程与任何其他共享分发点升级的运作相同。 会将内容复制并转换到目标层次结构正在使用的单一实例存储。 但是，当你升级位于辅助站点服务器上的共享分发点时，升级过程还将卸载管理点（如果存在），然后从服务器中卸载辅助站点。 结果，辅助站点会从 Configuration Manager 2007 层次结构中删除。 若要卸载辅助站点，Configuration Manager 将使用配置的帐户从源站点收集数据。  

 升级过程中，在卸载 Configuration Manager 2007 辅助站点后会出现一段延迟，然后才会开始在目标层次结构中安装分发点。 数据收集周期确定此延迟最高达四小时。 延迟旨在为辅助站点提供在新分发点安装开始前进行卸载的时间。  

 有关如何升级共享分发点的详细信息，请参阅 [Planning to upgrade Configuration Manager 2007 shared distribution points](#Planning_to_Upgrade_DPs)。  

##  <a name="a-namebkmkreassigndistpointa-planning-to-reassign-system-center-configuration-manager-distribution-points"></a><a name="BKMK_ReassignDistPoint"></a> 规划 System Center Configuration Manager 分发点的重新分配  
 当从 System Center 2012 Configuration Manager 的支持版本迁移到同一版本的层次结构时，可以将共享分发点从源层次结构重新分配到目标层次结构中的站点。 这类似于将 Configuration Manager 2007 分发点升级成为目标层次结构中的分发点的概念。 你可以从主站点和辅助站点中重新分配分发点。 重新分配分发点的操作会从源层次结构中删除分发点，并使计算机及其分发点成为你在目标层次结构中选择的站点的站点系统服务器。  

 在重新分配分发点时，你不必重新分发在源站点的分发点上承载的已迁移内容。 此外，与 Configuration Manager 2007 分发点的升级不同，分发点的重新分配不需要分发点计算机上的额外磁盘空间。 这是因为，从 System Center 2012 Configuration Manager 开始，分发点为内容使用单一实例存储格式，并且，在层次结构之间重新分配分发点时，不需要转换分发点计算机上的内容。  

 要使 System Center 2012 Configuration Manager 分发点适合于重新分配，它必须满足下列条件：  

-   必须在除站点服务器外的计算机上安装共享分发点。  

-   共享分发点不能与任何附加站点系统角色共存。  

若要标识适合于 Configuration Manager 控制台（位于“源层次结构”节点）中的重新分配的分发点，请选择源站点，然后选择“共享的分发点”选项卡。 适合的分发点在“适合重新分配”列中显示“是”（在 System Center 2012 R2 Configuration Manager 之前的版本中，此列名为“适合升级”）。  

###  <a name="a-namebkmkreassignprocessa-distribution-point-reassignment-process"></a><a name="BKMK_ReassignProcess"></a> 分发点重新分配过程  
 可以使用 Configuration Manager 控制台重新分配从活动的源层次结构中共享的分发点。 当你重新分配共享的分发点时，分发点会从其源站点中卸载，然后作为与你在目标层次结构中指定的主站点或辅助站点相连的分发点进行安装。  

 为重新分配分发点，目标层次结构会使用配置的“源站点访问帐户”从源站点的 SMS 提供程序收集数据。 有关必需的权限和附加的先决条件的信息，请参阅 [System Center Configuration Manager 中迁移的先决条件](../../core/migration/prerequisites-for-migration.md)。  

##  <a name="a-nameaboutmigratingcontenta-content-ownership-when-migrating-content"></a><a name="About_Migrating_Content"></a> 迁移内容时的内容所有权  
 在为部署迁移内容时，你必须将内容对象分配给目标层次结构中的站点。 此站点随后将成为目标层次结构中该内容的所有者。 尽管目标层次结构的顶层站点是实际迁移内容元数据的站点，但却是分配的站点在网络上访问内容的原始源文件。  

 为了最大程度地减少迁移内容时使用的网络带宽，请考虑将内容的所有权转让给目标层次结构中的站点，该站点在网络上与源层次结构中的内容位置接近。 由于有关目标层次结构中的内容的信息是全局共享的，因此该信息将在每个站点上可用。  

 尽管有关内容的信息是通过使用数据库复制共享到所有站点的，但你分配给主站点并随后部署到其他主站点上的分发点的任何内容将通过使用基于文件的复制传输。 此传输将经过管理中心站点，并随后传送到其他主站点。 在分配站点作为内容所有者时，通过在迁移之前或在迁移过程中将你打算分发到多个主站点的包集中在一起，你可以减少低带宽网络上的数据传输。  



<!--HONumber=Nov16_HO1-->


