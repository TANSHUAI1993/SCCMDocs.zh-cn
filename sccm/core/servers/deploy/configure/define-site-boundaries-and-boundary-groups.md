---
title: "使用边界和边界组 | Microsoft Docs"
description: "使用边界和边界组为你所管理的设备定义网络位置和可访问的站点系统。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fea1dece0768a2b7bcd3fcedc2288ea2d52e73d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>为 System Center Configuration Manager 定义站点边界和边界组

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 的边界在 Intranet 上定义可包含你要管理的设备的网络位置。 边界组是你所配置的边界的逻辑分组。

 层次结构可以包含任意数量的边界组，每个边界组可以包含以下边界类型的任意组合：  

-   IP 子网，  
-   Active Directory 站点名称  
-   IPv6 前缀  
-   IP 地址范围  

Intranet 上的客户端评估其当前网络位置，然后使用该信息确定它们所属的边界组。  

 客户端使用边界组以：  
-   **查找分配的站点：** 边界组使客户端能够为客户端分配（自动站点分配）查找主站点。  
-   **查找可以使用的某些站点系统角色：**将边界组与某些站点系统角色相关联时，边界组向客户端提供在内容定位期间以及作为首选管理点使用的站点系统的列表。  

位于 Internet 上或配置为仅 Internet 的客户端不使用边界信息。 这些客户端无法使用自动站点分配，并可始终从为其分配的站点中的任何分发点下载内容（如果分发点配置为允许来自 Internet 的客户端连接）。  

**开始使用：**
- 首先，[将网络位置定义为边界](/sccm/core/servers/deploy/configure/boundaries)。
- 然后继续[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)，将这些边界中的客户端与它们可以使用的站点系统服务器相关联。



##  <a name="BKMK_BoundaryBestPractices"></a> 边界和边界组的最佳实践  

-   **使用满足需求的最少边界混合体：**  
   过去，我们建议使用一些边界类型，而非其他类型。 借助提升性能的更改，我们现在建议使用任何边界类型，或选择适用于环境的类型，这样可以使用最少的边界，进而简化管理任务。      

-   **避免自动站点分配的重叠边界：**  
     虽然每个边界组同时支持站点分配配置和用于内容位置的配置，但最好创建一组仅用于站点分配的单独的边界组。 意味着：确保边界组中的每个边界不是具有不同站点分配的另一个边界组的成员。 这是因为：  

    -   单一边界可以包含在多个边界组中  

    -   每个边界组可与站点分配的不同主站点相关联  

    -   边界上的客户端（该边界是具有不同站点分配的两个不同边界组的成员）将随机选择要加入的站点，而这可能不是你希望客户端加入的站点。  此配置称为重叠边界。  

     重叠边界并不是内容位置的问题，相反，它通常是一项所需配置，可为客户端提供其他资源或可供他们使用的内容位置。  
