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
ms.openlocfilehash: 26ad3be032a3dd8ea21d7eeb6a4755c32d546f38
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67158640"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*适用范围：System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) 是一款独立工具，可方便独立软件供应商或业务线应用程序开发者管理自定义更新。 此自定义更新管理包括具有依赖项，如驱动程序和更新捆绑包的更新。

使用 Updates Publisher，可以执行下列操作：

-   导入外部目录（非 Microsoft 更新目录）中的更新。
-   修改更新定义（包括适用性和部署元数据）。
-   将更新导出到外部目录中。
-   将更新发布到更新服务器。

将更新发布到更新服务器后，可以使用 System Center Configuration Manager 检测这些更新，并将其部署到受管理设备中。

> [!TIP]  
> 旧版 [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111) 仍受支持。 此更新版保留了相同的功能，区别在于支持其他操作系统，新增了可简化某些任务的功能，并更新了用户界面。

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

## <a name="whats-new-in-the-system-center-updates-publisher-preview"></a>什么是 System Center Updates Publisher 预览版中的新增功能

>[!NOTE] 
>在本部分中的信息仅适用于 System Center Updates publisher 的预览版本。 若要安装预览版时，可以从下载[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=58390)。

System Center Updates Publisher，以帮助你创作你的更新在预览中没有新的创作模式。 当启用创作模式**类别的工作区**添加到开始屏幕。 一个新**检测**按钮也已添加到**更新工作区**当创作模式处于启用状态。 

### <a name="to-enable-authoring-mode-in-the-preview"></a>若要启用在预览中的创作模式

1. 在控制台的左上角，单击**Updates Publisher** **属性**选项卡，然后选择**选项**。
1. 转到**创作**选项。
1. 选中的复选框**创作模式启用**。

![有关更新发布服务器启用创作模式](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>有关类别的工作区

类别工作区允许更新作者组织拥有共同的更新。 例如，如果您是 OEM，您可能希望组织基于在模型或产品系列上应用更新。 可以定义多个类别和子类别，但不是 grand 子类别局限于两个级别。

![类别的工作区的屏幕截图](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>将更新分配给类别

一旦创建了你的更新，您可以将其分配给类别选择更新，然后单击**分类**按钮。 此外可以右键单击该更新，然后选择**分类**。

![对更新进行分类的屏幕截图](media/scup-categorize-update.png)


### <a name="about-detectoids"></a>有关 detectoid

创作模式启用后，可以创建更新的 detectoid。 必须使用相同的规则 （或一组规则） 来确定适用性的多个更新时，Detectoid 非常有用。 在这些情况下，您可以创建检测，并将其分配为更新的必备组件。 可以将多个 detectoid 分配给创作更新。


### <a name="create-a-detectoid"></a>创建检测

1. 打开“更新工作区”  。
1. 在功能区中，单击**检测**按钮。
1. 按照向导以创建在检测中的提示。



![使用检测更新先决条件](media/scup-detectoid-as-prerequisite.png)


## <a name="next-steps"></a>后续步骤
首先进行[安装](/sccm/sum/tools/install-updates-publisher)，然后为 Updates Publisher [配置选项](/sccm/sum/tools/updates-publisher-options)。
