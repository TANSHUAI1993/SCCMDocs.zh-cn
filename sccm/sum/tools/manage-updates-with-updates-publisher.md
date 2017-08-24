---
title: "管理更新 | Microsoft Docs"
description: "管理使用 System Center Updates Publisher 部署和创建的更新"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 1d6c3b1db14867bdbc5cae8ded099d9024a79549
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-software-updates-in-updates-publisher"></a>管理 Updates Publisher 中的软件更新

*适用范围：System Center Updates Publisher*     

在 System Center Updates Publisher 中，可以使用“更新工作区”管理已导入存储库中的软件更新和捆绑包。  

管理任务包括复制、编辑和终止或重新激活更新和捆绑包，以及将更新和捆绑包分配给发布项。 此外，还可以导出自定义目录，以供其他 Updates Publisher 安装项使用。

若要获取可以管理的更新，请执行以下操作：
-  [将更新目录添加](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs)到 Updates Publisher 安装项中
-  将目录中的更新[导入](/sccm/sum/tools/updates-publisher-catalogs#import-updates)存储库中。

还可以[创建你自己的更新](/sccm/sum/tools/create-updates-with-updates-publisher)。



## <a name="create-a-duplicate-of-an-update"></a>创建更新副本
可以创建存储库中更新的副本。 然后，可以修改副本，而不用修改原始更新。 无法创建更新捆绑包的副本。

若要创建副本，请在“更新工作区”中依次选择更新和“复制”。 更新的副本与其在“更新工作区”中的同一位置处显示，但名称中添加了“(副本)”一词。

虽然新建的副本处于“未终止”状态，但保留了原始更新的设置。

## <a name="edit-updates-and-bundles"></a>编辑更新和捆绑包
可以选择存储库中的更新和捆绑包进行修改。

在“更新工作区”中，选择更新或捆绑包，然后在“开始”选项卡中选择“编辑”，打开编辑向导。 虽然更新和捆绑包各自有向导，但它们密切相关，显示[“创建更新”](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard)或[“创建捆绑包”](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-bundle-wizard)向导中的相同选项。

编辑时，可以更改与更新或捆绑包相关的任意可用详细信息，以便能够在环境中使用。 例如，可以编辑适用性或优先规则，也可以更改语言。 还可以更改产品和供应商，将更新或捆绑包移到自定义文件夹中，从而对更新进行分组，以供你自己使用。

## <a name="assign-updates-and-bundles-to-a-publication"></a>将更新和捆绑包分配给发布项
可以在“更新工作区”中选择更新和捆绑包，然后从功能区的“开始”选项卡中选择“分配”，将其添加到发布项中。 这会启动“分配软件更新”向导。
-  请参阅[发布更新和捆绑包](#publish-updates-and-bundles-from-the-updates-workspace)，了解如何选择更新和捆绑包，并将其作为一个任务进行发布。
-  若要了解如何将各组更新和捆绑包作为一个对象进行管理，请参阅[管理发布项](/sccm/sum/tools/updates-publisher-publications)。 将更新分配给发布项后，可以管理相应的发布项，继而会覆盖所有已分配更新。

将更新和捆绑包分配给发布项后：

-   可以在同一发布项中添加已终止和未终止的更新和捆绑包。

-   指定发布项类型：

    -   **完整内容** - 这会将更新的完整内容发布到 WSUS 服务器。 包括元数据和更新二进制文件。

    -   **仅元数据** - 仅发布元数据；不发布更新二进制文件。 如果要收集符合性数据，可以选择此选项。

    -   **自动** - 只有在已连接 Updates Publisher 和 Configuration Manager 时，此模式才可用（请参阅 [ConfigMgr 服务器](/sccm/sum/tools/updates-publisher-options#configmgr-server)选项。）

    使用此类型，Updates Publisher 可以查询 Configuration Manager，以确定应发布更新或捆绑包的完整内容还是仅元数据。 仅当更新满足 Updates Publisher 选项的“ConfigMgr 服务器”页中指定的“请求客户端计数阈值”和“包源大小阈值”时，才会发布更新的完整内容。

-   选择发布项：

    -   如果已创建要使用的发布项，请使用“将软件更新分配给现有发布项”。 只有在至少有一个发布项时，此选项才可用。

    -   如果没有合适的发布项，请使用“将软件更新分配给新发布项”。 这会创建采用你指定的名称的新发布项。

将更新分配给发布项后，可以使用“发布项工作区”将发布项作为组进行[发布](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations)或[导出](/sccm/sum/tools/updates-publisher-publications#export-a-pubilcation)。

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>在“更新工作区”中发布更新和捆绑包
发布更新和捆绑包时，Updates Publisher 会向更新服务器添加这些更新和捆绑包的相关信息（元数据），可能还会添加更新的二进制文件（完整内容），以供部署到设备。

必须先为 Updates Publisher 配置[“更新服务器”](/sccm/sum/tools/updates-publisher-options#update-server)选项，然后才能进行发布。 若要打开此配置选项，请依次转到“更新工作区”&gt;“概述”，然后选择“配置 WSUS 和签名证书”。 还可以转到 Updates Publisher 选项的“更新服务器”页。

发布更新和捆绑包的方法有两种：
-   直接在“更新工作区”中发布。 （请参阅以下过程*如何发布更新和捆绑包*。）
-   作为[发布项](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations)在“发布项工作区”中发布。  

> [!NOTE]   
> Updates Publisher 只能发布大小不超过 375 MB 的更新。

### <a name="to-publish-updates-and-bundles"></a>如何发布更新和捆绑包
1.  转到“更新工作区”，并选择一个或多个要发布的更新和捆绑包。 然后，从功能区的“开始”选项卡中，选择“发布”

2.  在“发布”向导的“选择”页中，选择所需的更新发布方式。 选项与[分配更新](#assign-updates-and-bundles-to-a-publication)时相同：“完整内容”、“仅元数据”或“自动”。

    还可以选择使用新发布证书对所有更新进行签名。

3.  完成向导。

如果发布失败，将会看到指向 UpdatesPublisher.log 文件的链接，其中介绍了详细信息。

## <a name="export-updates"></a>导出更新
可以导出 Updates Publisher 存储库中的更新和捆绑包，从而创建自定义更新目录。 然后，可以[添加](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs)目录，并将其[导入](/sccm/sum/tools/updates-publisher-catalogs#mport-updates)其他 Updates Publisher 实例。 （还可以[将更新导出为发布项](/sccm/sum/tools/updates-publisher-publications##export-a-publication)。）

若要直接导出，请依次转到“更新工作区” > “所有软件更新”，然后选择一个或多个更新和捆绑包。 无法导出供应商或产品文件夹，但可以选择一个文件夹，然后选择导出其中的更新。

对于选定的一个或多个更新，请从功能区的“开始”选项卡中选择“导出”，然后提供目录导出的路径和文件名。

可以视需要导出（添加）从属软件更新。

## <a name="delete-updates-and-bundles"></a>删除更新和捆绑包
可以从 Updates Publisher 存储库中删除更新和更新捆绑包。

依次转到“更新工作区” > “所有软件更新”，并单独选择一个或多个更新。 然后，从功能区的“开始”选项卡中，选择“删除”。

-   如果只选择了尚未发布或已终止的更新或捆绑包，需要在删除之前确认删除。

-   如果选择的更新或捆绑包已发布且尚未终止，则会看到警告。 应先[终止](/sccm/sum/tools/updates-publisher-pubilcations#expire-or-reactivate-updates-and-bundles)这些更新并发布更改，然后才能将更新从存储库中删除。  

如果在删除供应商提供的更新或捆绑包后又重新导入相应目录，更新会还原到存储库中。

## <a name="manage-vendor-and-product-folders"></a>管理供应商和产品文件夹
若要查看已导入或创建的更新的供应商和产品列表，请依次转到“更新工作区” > “概述” > “所有软件更新”。

使用向导导入或创建软件更新或捆绑包时，Updates Publisher 会自动创建供应商和产品文件夹。 也可以手动创建这些文件夹。

-   若要创建供应商文件夹，请在“更新工作区”的导航窗格中右键单击“所有软件更新”，然后选择“创建供应商”。

-   若要在供应商文件夹下创建产品文件夹，请右键单击供应商文件夹，然后选择“创建产品”。

除了能够创建文件夹之外，还可以重命名或删除存储库中的任意供应商或产品文件夹。 为此，请右键单击文件夹，然后选择所需的选项（“重命名”或“删除”）。 删除文件夹同时也会从 Updates Publisher 存储库中删除此文件夹及其产品文件夹中的所有更新和捆绑包。

可以在供应商和产品文件夹（包括你创建的文件夹）之间移动更新。 若要将更新或捆绑包移到新文件夹中，必须选择并**编辑**更新或捆绑包。 然后，可以在“编辑更新”向导的“信息”页中重新分配供应商和产品。 “编辑更新”向导完成后，更改会得到应用，更新也会移到新文件夹中。

## <a name="view-the-xml-of-an-update-or-bundle"></a>查看更新或捆绑包的 XML
可以在“更新工作区”中选择一个更新或捆绑包，然后选择“查看 XML”，查看更新的 XML 结构。 没有可直接编辑 XML 结构的选项。
