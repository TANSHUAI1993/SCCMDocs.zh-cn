---
title: 使用边界和边界组
titleSuffix: Configuration Manager
description: 使用边界和边界组为你所管理的设备定义网络位置和可访问的站点系统。
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d160c6ab64c5ad097bf5986882b65171b0df4651
ms.sourcegitcommit: 60d45a5df135b84146f6cfea2bac7fd4921d0469
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2019
ms.locfileid: "67194164"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>定义站点边界和边界组

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager 中的边界用于定义 Intranet 上的网络位置。  这些位置包括你想要管理的设备。 边界组是你所配置的边界的逻辑分组。 

一个层次结构可以包括任意数量的边界组。 每个边界组可以包含以下边界类型的任意组合：  

- IP 子网  
- Active Directory 站点名称  
- IPv6 前缀  
- IP 地址范围  

Intranet 上的客户端评估其当前网络位置，然后使用该信息确定它们所属的边界组。  

客户端使用边界组以：  

- **查找分配的站点：** 边界组使客户端能够为客户端分配找到主站点。 此行为也称为“自动站点分配”。   

- **查找可以使用的某些站点系统角色：** 将边界组与某些站点系统角色关联。 然后站点向客户端提供边界组中的站点系统的列表。 客户端使用这些站点系统执行查找内容或附近的管理点等操作。  

位于 Internet 上或配置为仅 Internet 的客户端不使用边界信息。 这些客户端无法使用自动站点分配。 它们可以从其分配站点的基于 Internet 的分发点或从基于云的分发点下载内容。  

从版本 1902 开始，可以将云管理网关 (CMG) 与边界组关联。 有关详细信息，请参阅 [CMG 层次结构设计](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#hierarchy-design)。<!--3640932-->


## <a name="BKMK_BoundaryBestPractices"></a> 建议

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>使用满足需求的最少边界混合体

使用适用于你的环境的任意边界类型或所选类型。 使用可以让你使用尽可能少的边界的边界类型，以便简化管理任务。

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>避免自动站点分配的重叠边界

虽然每个边界组均同时支持站点分配和站点系统引用，但请创建一组仅用于站点分配的单独的边界组。 请确保边界组中的每个边界不是具有不同站点分配的另一个边界组的成员。

- 单一边界可以包含在多个边界组中  

- 每个边界组可与站点分配的不同主站点相关联  

- 如果边界属于两个拥有不同站点分配的不同边界组的成员，客户端将随机选择一个站点来联接。 此行为可能不会联接你希望客户端联接的站点。 此配置称为重叠边界。   

    重叠边界不会妨碍内容位置。 它可以成为为客户端提供额外可用资源或内容位置的有用配置。  


## <a name="next-steps"></a>后续步骤

- [将网络位置定义为边界](/sccm/core/servers/deploy/configure/boundaries)

- [配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)
