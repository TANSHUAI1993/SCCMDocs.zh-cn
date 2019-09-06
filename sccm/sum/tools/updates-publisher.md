---
title: 更新发布服务器
titleSuffix: Configuration Manager
description: 使用 System Center Updates Publisher 管理自定义更新
ms.date: 6/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: dee1a5a998f6d99678f85e6d5f39e52cb35a2bad
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70378718"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*适用范围：System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) 是一款独立工具，可方便独立软件供应商或业务线应用程序开发者管理自定义更新。 此自定义更新管理包括具有依赖关系的更新，如驱动程序和更新捆绑。

使用 Updates Publisher，可以执行下列操作：

-   导入外部目录（非 Microsoft 更新目录）中的更新。
-   修改更新定义（包括适用性和部署元数据）。
-   将更新导出到外部目录中。
-   将更新发布到更新服务器。

将更新发布到更新服务器后，可以使用 System Center Configuration Manager 检测这些更新，并将其部署到受管理设备中。

> [!TIP]  
> 旧版 [System Center Updates Publisher 2011](https://go.microsoft.com/fwlink/?LinkId=848111) 仍受支持。 此更新版保留了相同的功能，区别在于支持其他操作系统，新增了可简化某些任务的功能，并更新了用户界面。

## <a name="workspaces"></a>工作区
打开 Updates Publisher 时，默认打开的是“更新工作区”  的“概述”节点。

![Updates Publisher 控制台](media/console1.png)   


Updates Publisher 有四个工作区，可方便整理。


**更新工作区：** 使用此工作区可[创建](/sccm/sum/tools/create-updates-with-updates-publisher)和[管理](/sccm/sum/tools/manage-updates-with-updates-publisher)软件更新和更新捆绑包。 在此工作区中，可以将更新和捆绑包分配给发布项、发布它们，并能将它们导出到另一个 Updates Publisher 存储库中。

**发布项工作区：** 可以在此工作区中[管理发布项](/sccm/sum/tools/updates-publisher-publications)。 发布项是创建的一组更新，以便于简化更新的导出和发布。

管理发布项包括将更新发布到服务器以便客户端能够查找和安装更新、导出更新和捆绑包以供其他 Updates Publisher 安装项使用，或修改发布项的内容或详细信息。

**规则工作区：** 可以在其中[管理适用性规则](/sccm/sum/tools/updates-publisher-applicability-rules)，此类规则可以进行保存，随后与部署的更新结合使用。 规则分为两种类型：

-   可安装规则 - 此类规则有助于确定客户端是否应安装更新。
-   已安装规则 - 此类规则可验证更新是否已安装。

**目录工作区：** 使用此工作区可添加和[管理软件更新目录](/sccm/sum/tools/updates-publisher-catalogs)。 在此工作区中，可以将目录中的软件更新导入 Updates Publisher 存储库。

## <a name="whats-new-in-the-system-center-updates-publisher-preview"></a>System Center Updates Publisher 预览版的新增功能

>[!NOTE] 
>本部分中的信息仅适用于 System Center Updates publisher 的预览版本。 若要安装预览版，请从[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=58390)下载。

System Center Updates Publisher 预览版中有一种新的创作模式，可帮助你创作更新。 启用创作模式时，"**类别" 工作区**将添加到 "开始" 屏幕。 当启用了创作模式时，还会将一个新的**Detectoid**按钮添加到 "**更新" 工作区**。 

### <a name="to-enable-authoring-mode-in-the-preview"></a>在预览版中启用创作模式

1. 在控制台的左上角，单击 "**更新发布服务器** **属性**" 选项卡，然后选择 "**选项**"。
1. 请参阅**创作**选项。
1. 选中 "**启用创作模式**" 复选框。

![为 Updates Publisher 启用创作模式](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>关于 "类别" 工作区

"类别" 工作区使更新创作者能够组织组成的更新。 例如，如果你是 OEM，则可能想要根据模型或产品系列来组织更新。 您可以定义多个类别和子类别，但不能定义子类别，因为您限制为两个级别。

!["类别" 工作区的屏幕截图](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>为类别分配更新

编写更新后，可以通过选择 "更新"，然后单击 "**分类**" 按钮，将其分配到某个类别。 你还可以右键单击该更新，然后选择 "**分类**"。

![分类更新的屏幕截图](media/scup-categorize-update.png)


### <a name="about-detectoids"></a>关于 detectoid

一旦启用了创作模式，你就可以创建更新的 detectoid。 如果有多个更新使用同一规则（或一组规则）来确定适用性，detectoid 将非常有用。 在这些实例中，你将创建一个 detectoid，并将其分配为更新的必备组件。 可以将多个 detectoid 分配给创作的更新。


### <a name="create-a-detectoid"></a>创建 detectoid

1. 打开“更新工作区”  。
1. 在功能区中，单击 " **Detectoid** " 按钮。
1. 按照向导中的提示创建你的 detectoid。



![使用 detectoid 更新必备组件](media/scup-detectoid-as-prerequisite.png)


## <a name="next-steps"></a>后续步骤
首先进行[安装](/sccm/sum/tools/install-updates-publisher)，然后为 Updates Publisher [配置选项](/sccm/sum/tools/updates-publisher-options)。
