---
title: "使用资产智能 | Microsoft Docs"
description: "在 System Center Configuration Manager 中执行常见的资产智能任务。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 17168e26f13340847928f6e3623115cd4b55997b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-asset-intelligence-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中使用资产智能

*适用范围：System Center Configuration Manager (Current Branch)*

本主题包含的信息可帮助在 System Center Configuration Manager 层次结构中管理典型的资产智能任务：  

##  <a name="BKMK_ViewInformation"></a> 查看资产智能信息  
 你可以在“资产智能”  主页上和资产智能报表中查看资产智能信息。  

###  <a name="BKMK_AssetIntelligenceHomePage"></a> “资产智能”主页  
 “资产智能”  主页显示了资产智能目录信息的摘要仪表板。 在主页上可以查看有关目录同步和清单软件状态的信息。 “资产智能”  主页包含以下部分：  

-   **目录同步**：该部分提供了有关是否启用资产智能、资产智能同步点当前的状态、同步计划、是否导入客户许可证声明、上次状态更新的时间和下次计划更新的时间以及在安装资产智能同步点站点系统之后发生的更改数的信息。  

    > [!NOTE]  
    >  如果安装了资产智能同步点站点系统角色，则仅显示“资产智能”  主页的“资产智能目录同步状态”部分。  

-   **清单软件状态**：该部分提供了清单软件、软件类别以及由 Microsoft 标识、由管理用户标识、等待联机标识或未标识并且未等待的软件系列的计数和百分比。 以表格格式显示的信息显示每个对象的计数，而以图表格式显示的信息则显示每个对象的百分比。  

 使用以下过程查看在“资产智能”  主页上的资产智能信息。  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>若要查看“资产智能”主页上的资产智能信息  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” 。 将显示资产智能报表。  

###  <a name="BKMK_AssetIntelligenceReports"></a> 资产智能报表  
 总共有 60 多个资产智能报表，这些报表显示了由资产智能收集的信息。 大多数报表都是链接至更具针对性的报表，你可以从中查询常规信息以及向下钻取更多详细信息。 资产智能报表位于 Configuration Manager 控制台，“监视”工作区中的“报表”节点下。 这些报表提供有关硬件、许可证管理和软件的信息。 有关 Configuration Manager 中报表的详细信息，请参阅 [System Center Configuration Manager 中的报表](../../../../core/servers/manage/reporting.md)。  

> [!NOTE]  
>  由于要列出安装在企业环境中的软件许可证信息的软件标题涉及到复杂的依赖关系和限制，因此已安装的软件标题质量的准确性以及在资产智能报表中显示的许可证信息可能会与环境中已安装的软件标题或者正在使用中的许可证的实际数目不一致。 资产智能报表不应作为确定所购买的软件许可证符合性的唯一源。  

 使用以下过程，通过使用资产智能报表来查看资产智能信息。  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>若要通过使用资产智能报表查看收集的资产智能信息  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”  工作区中，依次展开“报告” ，“报表” ，然后单击“资产智能” 。 将显示资产智能报表。  

    > [!WARNING]  
    >  如果在“报表”  节点下没有报表文件夹存在，请验证你是否配置了报告。 有关详细信息，请参阅[在 System Center Configuration Manager 中配置报表](../../../../core/servers/manage/configuring-reporting.md)。  

3.  选择你希望运行的资产智能报表，然后在“主页”  选项卡上的“报表组”  组中，单击“运行” 。  

##  <a name="BKMK_SynchronizeTheCatalog"></a> 同步资产智能目录  
 你可以将本地资产智能目录与 System Center Online 同步以检索最新的软件标题分类。 当你手动请求将目录与 System Center Online 同步时，可能需要 15 分钟或者更长时间才能完成与 System Center Online 同步的过程。 同步成功完成时，Configuration Manager 会将“资产智能”主页上的“上次成功更新时间”设置更新成与当前时间相一致。  

> [!NOTE]  
>  必须先使用此过程安装资产智能同步点站点系统角色。 有关如何安装资产智能同步点的信息，请参阅[在 System Center Configuration Manager 中配置资产智能](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

 使用以下过程为资产智能目录创建同步计划。  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>若要为资产智能目录创建同步计划  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“同步” ，然后单击“日程安排同步” 。  

4.  在“资产智能同步点日程安排”  对话框中，选择“按日程安排启用同步” ，然后配置简单的或自定义的日程安排。  

5.  单击“确定”  以保存更改。  

    > [!NOTE]  
    >  有关同步日程安排，包括下一次安排的同步，请参阅层次结构顶层站点上“资产和符合性”  工作区中的“资产智能”  节点。  

 使用以下过程手动同步资产智能目录。  

> [!WARNING]  
>  System Center Online 在 12 小时内仅接受一次手动同步请求。  

###  <a name="BKMK_ManuallySynchronizeCatalog"></a> 若要手动同步资产智能目录  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“同步” ，再单击“同步资产智能目录” ，然后单击“确定” 。  

##  <a name="BKMK_CustomizeCatalog"></a> 自定义资产智能目录  
 从 System Center Online 接收到的资产智能目录分类信息存储在站点数据库中，权限为只读且不能修改或删除。 然而，你可以创建、修改并删除自定义软件类别、软件系列、软件标签以及硬件要求目录信息。 对于现有或用户定义的软件标题信息，你可以使用自定义分类数据，而不使用由 System Center Online 提供的信息。 当你更改或添加分类信息时，目录信息将被视为用户定义的信息。 用户定义的分类信息存储在与已验证的目录信息不同的数据库表中。  

###  <a name="BKMK_SoftwareCategories"></a> 软件类别  
 资产智能软件类别可用于对已列出清单的软件标题进行广泛的分类，也可用作更具体的软件家族的高级别分组。 例如，软件类别可以是能源公司，而该软件类别中的软件家族可以是石油和天然气或水力电气。 在资产智能目录中预定义了许多软件类别，并且可以创建其他用户定义的类别以进一步定义已列出清单的软件。 所有预定义软件类别的验证状态始终为“已验证” ，而添加到资产智能目录的自定义软件类别信息则为“用户定义” 。  

 使用以下过程创建用户定义的软件类别。  

##### <a name="to-create-a-user-defined-software-category"></a>若要创建用户定义的软件类别  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” ，然后单击“目录” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建软件类别” 。  

4.  在“常规”  页面上，为新的软件类别输入名称和（可选）说明。  

    > [!NOTE]  
    >  始终将所有新的自定义软件类别的验证状态设置为“用户定义” 。  

     单击“下一步” 。  

5.  在“摘要”  页面上查看设置，然后单击“下一步” 。  

6.  在“完成”  页上，单击“关闭”  退出向导。  

###  <a name="BKMK_SoftwareFamilies"></a> 软件家族  
 资产智能软件家族可用于进一步定义软件类别中的已列出清单的软件标题。 例如，软件类别可以是能源公司，而该软件类别中的软件家族可以是石油和天然气或水力电气。 可以在资产智能目录中预定义许多软件系列，并且还可以创建其他用户定义的系列以进一步定义清单软件。 所有预定义的软件系列的验证状态始终为“已验证” ，而添加到资产智能目录的自定义软件家族信息则为“用户定义” 。  

 使用以下过程创建用户定义的软件系列。  

##### <a name="to-create-a-user-defined-software-family"></a>若要创建用户定义的软件系列  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” ，然后单击“目录” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建软件系列” 。  

4.  在“常规”  页面上，为新的软件系列输入名称和（可选）说明。  

    > [!NOTE]  
    >  始终将所有新自定义软件家族的验证状态设置为“用户定义” 。  

5.  在“摘要”  页面上查看设置，然后单击“下一步” 。  

6.  在“完成”  页上，单击“关闭”  退出向导。  

###  <a name="BKMK_SoftwareLabels"></a> 软件标签  
 你可以通过资产智能自定义软件标签创建筛选器，然后用筛选器对软件标题进行分组并通过使用资产智能报表查看它们。 例如，你可以创建被称为共享件的软件标签，将它与大量的应用程序相关联，然后运行报表以显示共享件软件标签的所有标题。 所有你添加到资产智能目录中的自定义软件标签的验证状态为“用户定义”  。  

 使用以下过程创建用户定义的自定义标签。  

##### <a name="to-create-a-user-defined-software-label"></a>若要创建用户定义的软件标签  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” ，然后单击“目录” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建软件标签” 。  

4.  在“常规”  页面上，为新的软件系列输入名称和（可选）说明。  

    > [!NOTE]  
    >  始终将所有新自定义软件标签的验证状态设置为“用户定义” 。  

5.  在“摘要”  页面上查看设置，然后单击“下一步” 。  

6.  在“完成”  页上，单击“关闭”  退出向导。  

###  <a name="BKMK_HardwareRequirements"></a> 硬件要求  
 对软件标题进行软件部署前，可使用硬件要求信息来验证计算机是否满足软件标题的硬件要求。 资产智能目录中预定义了许多硬件要求，你可以创建新的用户定义的硬件要求信息以满足自定义要求。 所有预定义的硬件要求的验证状态始终为“已验证” ，而添加到资产智能目录的用户定义的硬件要求信息为“用户定义” 。  

> [!IMPORTANT]  
>  Configuration Manager 控制台中显示的硬件要求均从本地计算机上的资产智能目录检索，并且不基于 System Center 2012 Configuration Manager 客户端的已列出清单的软件标题信息。 硬件要求信息不作为 System Center Online 同步过程的一部分进行更新。 你可以为没有关联硬件要求的清单软件创建用户定义的硬件要求。  

 使用以下过程创建用户定义的硬件要求。  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>若要创建用户定义的硬件要求  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” ，然后单击“硬件要求” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建硬件要求” 。  

4.  在“常规”  页面上，输入以下信息：  

    1.  **软件标题**：指定硬件要求关联的软件标题。 软件标题不能是资产智能目录中已存在的标题。  

    2.  **验证状态**：为硬件要求列出“用户定义”  验证状态。 你无法修改此设置。  

    3.  **最低 CPU (MHz)**：指定软件标题所需的最低处理器速度，以兆赫 (MHz) 为单位。  

    4.  **最小 RAM (KB)**：指定软件标题所需的最小 RAM，以 KB 为单位。  

    5.  **最小磁盘空间 (KB)**：指定软件标题所需的最小可用硬盘空间，以 KB 为单位。  

    6.  **最小磁盘大小 (KB)**：指定软件标题所需的最小硬盘大小，以 KB 为单位。  

     单击“下一步” 。  

5.  在“摘要”  页面上查看设置，然后单击“下一步” 。  

6.  在“完成”  页上，单击“关闭”  退出向导。  

###  <a name="BKMK_ModifyCategorization"></a> 修改清单软件的分类信息  
 使用特定分类信息（例如产品名称、供应商、软件类别以及软件系列）配置资产智能目录中预定义的软件。 当预定义的分类信息不满足你的要求时，你可以在软件标题的属性中修改该信息。 当你修改预定义软件的分类信息时，软件的验证状态会从“已验证”  更改为“用户定义” 。  

> [!IMPORTANT]  
>  只能修改顶层站点上的分类信息。  

 使用以下过程修改清单软件的分类信息。  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>若要修改软件标题的分类  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” ，然后单击“清单软件” 。  

3.  为你希望修改的分类选择一个或多个软件标题。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

5.  在“常规”  选项卡上，你可以修改以下分类信息：  

    -   **产品名称**：指定清单软件标题的名称。  

    -   **供应商**：指定开发已列出清单的软件标题的供应商名称。  

    -   **类别**：指定已列出清单的软件标题当前所分配的软件类别。  

    -   **家族**：指定已列出清单的软件标题当前所分配的软件家族。  

6.  单击“确定”  以保存更改。  

 使用以下过程将软件还原到原始分类信息。  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>将软件的分类信息还原为软件的原始设置  
 Configuration Manager 会将从 System Center Online 中获得的分类信息存储在数据库中。 不能删除该信息。 修改信息后，你可以将该分类信息还原为 System Center Online 分类。 资产智能目录中不存在的清单软件也可以还原为原始设置。  

 使用以下过程将分类信息还原为原始设置。  

##### <a name="to-revert-categorization-information-to-original-settings"></a>若要将分类信息还原为原始设置  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” ，然后单击“清单软件” 。  

3.  选择你希望还原到原始设置的一个或多个软件标题。 只能还原状态为“用户定义”  的软件。  

    > [!TIP]  
    >  单击“状态”  列以按验证状态进行排序。 通过排序，你可以查看按验证状态排列的所有软件并快速选择多个项以还原至原始设置。  

4.  在“主页”  选项卡上的“产品”  组中，单击“还原” 。  

5.  单击“是”  以将软件还原为原始分类信息。  

6.  当你还原资产智能目录中存在的软件分类信息时，验证状态会从“用户定义”  更改为“已验证” 。 当你还原资产智能目录中不存在的软件时，验证状态会从“用户定义”  更改为“未分类” 。  

##  <a name="BKMK_RequestCatalogUpdate"></a> 为未分类的软件标题请求目录更新  
 可以将未分类的软件标题信息提交至 System Center Online 以供研究和分类。 提交了未分类的软件标题，并且客户对相同软件标题至少进行了 4 次分类请求之后，研究人员会进行标识、分类，然后将软件标题分类信息提供给所有正在使用 System Center Online 的客户。 Microsoft 会对具有最多分类请求的软件标题指定最高优先级。 自定义软件和业务线应用程序不大可能接收类别，作为最佳做法，不应将这些软件标题发送给 Microsoft 进行分类。  

 当软件标题信息提交至 System Center Online 以供分类时，下列条件适用：  

-   仅向 System Center Online 传输基本的软件标题信息，可以在提交前查看要分类的软件标题信息。  

-   永远不会传输软件许可证信息。  

-   任何已上载的软件标题将作为 System Center Online 目录的一部分予以公开，其他客户均可下载。  

-   软件标题源未在 System Center Online 目录中存储。 然而，不应提交包含机密或专有信息的应用程序标题供 System Center Online 进行分类。  

> [!NOTE]  
>  有关资产智能隐私信息的详细信息，请参阅 [System Center Configuration Manager 中资产智能的安全和隐私](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md)。  

 使用下列过程从 System Center Online 中请求资产智能目录的软件标题分类。  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>若要为未分类的软件标题请求目录更新  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” ，然后单击“清单软件” 。  

3.  选择一个或多个产品名称，将它们提交至 System Center Online 进行分类。 仅未分类并已列出清单的软件标题可以提交到 System Center Online 以供分类。 如果管理员已对清单软件标题进行了分类并生成了用户定义的状态，则必须右键单击清单软件标题，再单击“还原”  以将软件标题还原到“未分类”  状态，然后将其提交到 System Center Online 进行分类。  

    > [!NOTE]  
    >  Configuration Manager 可以一次处理多达 100 个软件标题的分类。 如果选择了超过 100 个软件标题，则只会处理前 100 个软件标题。 必须选择少于 100 个要在批次中进行分类的其余软件标题。  

    > [!TIP]  
    >  单击“状态”  列以按验证状态进行排序。 这样可让你看见所有未分类的产品名称，快速选择多个项目并提交进行分类。  

4.  在“主页”  选项卡上的“产品”  组中，单击“请求目录更新” 。  

5.  查看 System Center Online 分类提交隐私消息。 单击“详细信息”  以查看将发送到 System Center Online 的信息。  

6.  选择“我已阅读并理解此消息” ，然后单击“确定”  以允许提交所选的软件标题进行分类。  

7.  验证已提交至 System Center Online 进行分类的清单软件名称的状态是否已从“未分类”  更改为“挂起” 。  

    > [!NOTE]  
    >  提交至 System Center Online 进行分类的软件在管理中心站点上具有验证状态为“挂起”  的软件在子主站点上仍然会显示为“未分类”  的验证状态。  

##  <a name="BKMK_ResolveSoftwareDetails"></a> 解决软件详细信息冲突  
 System Center Online 与现有软件详细信息存在冲突，因此在其已收到最近更新的软件分类详细信息之后，你可以选择如何解决该冲突。 当前具有冲突的软件的验证状态为“可更新” 。 在解决软件详细信息冲突之后，根据你指定的设置，软件分类信息将保留在资产智能目录中。 在解决冲突之后，对于相同软件分类值，软件详细信息冲突不会再次发生，除非 System Center Online 值发生变化。  

 使用以下过程解决软件详细信息冲突。  

#### <a name="to-resolve-a-software-details-conflict"></a>解决软件详细信息冲突  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“资产智能” ，然后单击“清单软件” 。  

3.  查看软件标题的“状态”  列是否处于“可更新”  状态。  

4.  选择你希望解决冲突的软件标题，然后在“主页”  选项卡上的“产品”  组中，单击“解决冲突” 。  

5.  查看以下信息：  

    -   **本地值**：指定资产智能目录中与较新的 System Center Online 软件分类详细信息发生冲突的现有软件分类信息。  

    -   **已下载的值**：为冲突的资产智能目录软件分类信息指定新的 System Center Online 软件分类信息。  

6.  选择以下设置之一以解决软件详细信息冲突：  

    -   **不更改本地编辑的目录信息值**：通过保留现有资产智能目录软件分类信息来解决软件详细信息冲突。 当你选择此设置时，软件标题状态会从“可更新”  更改为“用户定义” 。  

    -   **用已下载的 System Center Online 值覆盖本地编辑的目录信息值**：通过用从 System Center Online 获得的新信息覆盖现有的资产智能目录软件分类信息来解决软件详细信息冲突。 当你选择此设置时，软件标题状态会从“可更新”  更改为“已验证” 。  

     单击“确定”  保存冲突解决。  
