---
title: "用于软件更新的图标 | Microsoft Docs"
description: "Configuration Manager 控制台包含指示已同步更新或软件更新组的状态的图标。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
ms.openlocfilehash: 04c5ccc53263b2672096b564695a636bfb28d952
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="icons-used-for-software-updates-in-system-center-configuration-manager"></a>System Center Configuration Manager 中用于软件更新的图标

*适用范围：System Center Configuration Manager (Current Branch)*

同步后的软件更新会显示在 Configuration Manager 控制台中，每个软件更新的首列均包含一个指示特定状态的图标。 软件更新组也使用一个图标表示，该图标提供有关组中所包含软件更新的状态信息。 本部分提供有关软件更新图标和每个图标表示的内容的信息。  

## <a name="icons-for-software-updates"></a>软件更新图标  
 同步后的软件更新由以下其中一个图标表示。  

### <a name="normal-icon"></a>“正常”图标  
 ![图标](../media/Normal.jpg "“正常”图标") 带有绿色箭头的图标表示正常的软件更新。  

 **描述：**  

 正常软件更新已同步，可用于软件部署。  

 **操作问题：**  

 没有操作问题。  

### <a name="expired-icon"></a>“被取代”图标  
 ![图标](../media/Expired.jpg "“已过期”图标") 带有黑色 X 的图标表示过期的软件更新。 当软件更新显示在 Configuration Manager 控制台中时，也可以通过查看软件更新的“已过期”列来识别过期的软件更新。  

 **描述：**  

 过期的软件更新以前可部署到客户端计算机，但是软件更新过期之后，不能再为软件更新创建新部署。 过期的软件更新会从活动部署中删除，并且不再对客户端可用。  

 **操作问题：**  

 没有操作问题。

### <a name="superseded-icon"></a>“被取代”图标  
 ![图标](../media/Superseded.jpg "“被取代”图标") 带有黄色星号的图标表示被取代的软件更新。 当软件更新显示在 Configuration Manager 控制台中时，也可以通过查看软件更新的“被取代”列来识别被取代的软件更新。  

 **描述：**  

 被取代的软件更新已替换为更新版本的软件更新。 通常，取代另一个软件更新的软件更新将执行以下一项或多项操作：  

-   增强、改进或添加到由以前发布的一个或多个软件更新提供的修补程序。  

-   提高（如果批准安装软件更新，则由客户端安装的）软件更新文件包的效率。 例如，被取代的软件更新可能包含不再与修补程序或新软件更新现在支持的操作系统相关的文件，因此这些文件未包括在软件更新的取代文件包中。  

-   换句话说，产品的较新版本不再适用于产品的较旧版本或配置。 如果进行了修改来扩展语言支持，则软件更新还可能取代其他软件更新。 例如，稍后对 Microsoft Office 的产品更新进行的修订可能会删除对较旧操作系统的支持，但会在初始软件更新版本中添加对新语言的额外支持。  

 在“软件更新点组件”属性的“取代规则”选项卡上，你可以指定管理取代的软件更新的方式。 有关详细信息，请参阅 [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules)。  

 **操作问题：**  

 如果可能，将用于取代的软件更新而不是被取代的更新部署到客户端计算机上。 你可以在软件更新属性中的“取代信息”  选项卡上显示用于取代软件更新的软件更新列表。  

### <a name="invalid-icon"></a>“无效”图标  
 ![图标](../media/Invalid.jpg "“无效”图标") 带有红色 X 的图标表示无效的软件更新。  

 **描述：**  

 活动部署中有无效的软件更新，但是由于某种原因，其内容（软件更新文件）不可用。 以下是可能出现此状态的情况：  

-   成功部署了软件更新，但已从部署包中删除此软件更新文件，此文件已不再可用。  

-   在站点上创建了软件更新部署，并且已成功将部署对象复制到子站点，但部署包尚未成功复制到子站点。  

 **操作问题：**  

 当软件更新缺少内容时，客户端将无法安装软件更新，直到内容在分发点上可用。 你可以通过使用“重新分发”  操作，将内容重新分发到分发点。 当在父站点创建的部署中缺少软件更新的内容时，必须将软件更新复制或重新分发到子站点上。 有关内容重新分发的详细信息，请参阅[管理已分发的内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage)。  

### <a name="metadata-only-icon"></a>“仅元数据”图标
 ![图标](../media/MetadataOnly.png "“仅元数据”图标") 带有蓝色箭头的图标表示仅元数据软件更新。

 **描述：**  

 仅元数据软件更新在 Configuration Manager 控制中可用于报告。 不能部署或下载仅元数据软件更新，因为软件更新文件与软件更新元数据不相关联。  

 **操作问题：**  

 仅元数据软件更新可用于报告目的，但不可用于软件更新部署。  

## <a name="icons-for-software-update-groups"></a>软件更新组图标  
 软件更新组由以下其中一个图标表示。  

### <a name="normal-icon"></a>“正常”图标  
 ![图标](../media/Normal.jpg "“正常”图标") 带有绿色箭头的图标表示仅包含正常软件更新的软件更新组。  

 **操作问题：**  

 没有操作问题。  

### <a name="expired-icon"></a>“被取代”图标  
 ![图标](../media/Expired.jpg "“已过期”图标") 带有黑色 X 的图标表示包含一个或多个过期的软件更新的软件更新组。  

 **操作问题：**  

 如果可能，删除或替换软件更新组中过期的软件更新。  

### <a name="superseded-icon"></a>“被取代”图标  
 ![图标](../media/Superseded.jpg "“被取代”图标") 带有黄色星号的图标表示包含一个或多个被取代的软件更新的软件更新组。  

 **操作问题：**  

 如果可能，将软件更新组中被取代的软件更新替换为用于取代的软件更新。  

### <a name="invalid-icon"></a>“无效”图标  
 ![图标](../media/Invalid.jpg "“无效”图标") 带有红色 X 的图标表示包含一个或多个无效的软件更新的软件更新组。  

 **操作问题：**  

 当软件更新缺少内容时，客户端将无法安装软件更新，直到内容在分发点上可用。 你可以通过使用“重新分发”  操作，将内容重新分发到分发点。 当在父站点创建的部署中缺少软件更新的内容时，需要将软件更新复制或重新分发到子站点上。 有关内容重新分发的详细信息，请参阅[管理已分发的内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage)。  
