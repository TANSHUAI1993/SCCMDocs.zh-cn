---
title: Updates Publisher | Microsoft Docs
description: "使用 System Center Updates Publisher 管理自定义更新"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: f4951c204b32da58174b94a539b380c278fa9756
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*适用范围：System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) 是一款独立工具，可方便独立软件供应商或业务线应用程序开发者管理自定义更新。 这包括具有依赖项的更新，如驱动程序和更新捆绑包。

使用 Updates Publisher，可以执行下列操作：

-   导入外部目录（非 Microsoft 更新目录）中的更新。
-   修改更新定义（包括适用性和部署元数据）。
-   将更新导出到外部目录中。
-   将更新发布到更新服务器。

将更新发布到更新服务器后，可以使用 System Center Configuration Manager 检测这些更新，并将其部署到受管理设备中。

> [!TIP]  
> 旧版 [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111) 仍受支持。 此更新版保留了相同的功能，区别在于支持其他操作系统，新增了可简化某些任务的功能，并更新了用户界面。

## <a name="workspaces"></a>工作区
打开 Updates Publisher 时，默认打开的是“更新工作区”的“概述”节点。

![Updates Publisher 控制台](media/console1.png)   


Updates Publisher 有四个工作区，可方便整理。


**更新工作区：**使用此工作区可[创建](/sccm/sum/tools/create-updates-with-updates-publisher)和[管理](/sccm/sum/tools/manage-updates-with-updates-publisher)软件更新和更新捆绑包。 这包括将更新和捆绑包分配给发布项、发布它们，以及将它们导出到其他 Updates Publisher 存储库中。

**发布项工作区：**可以在其中[管理发布项](/sccm/sum/tools/updates-publisher-publications)。 发布项是创建的一组更新，以便于简化更新的导出和发布。

管理发布项包括将更新发布到服务器以便客户端能够查找和安装更新、导出更新和捆绑包以供其他 Updates Publisher 安装项使用，或修改发布项的内容或详细信息。



**规则工作区：**可以在其中[管理适用性规则](/sccm/sum/tools/updates-publisher-applicability-rules)，此类规则可以进行保存，随后与部署的更新结合使用。 规则分为两种类型：

-   可安装规则 - 此类规则有助于确定客户端是否应安装更新。
-   已安装规则 - 此类规则可验证更新是否已安装。

**目录工作区：**使用此工作区可添加和[管理软件更新目录](/sccm/sum/tools/updates-publisher-catalogs)。 这包括将目录中的软件更新导入 Updates Publisher 存储库。
## <a name="first-steps"></a>前几个步骤
首先进行[安装](/sccm/sum/tools/install-updates-publisher)，然后为 Updates Publisher [配置选项](/sccm/sum/tools/updates-publisher-options)。
