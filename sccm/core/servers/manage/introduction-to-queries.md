---
title: "查询简介 | Microsoft Docs"
description: "可创建和运行查询，在 System Center Configuration Manager 层次结构中查找与查询条件相匹配的对象。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f84d518670c0ece3c08c890d2293335518f7f8e9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的查询简介

*适用范围：System Center Configuration Manager (Current Branch)*

可创建和运行查询，在 System Center Configuration Manager 层次结构中查找与查询条件相匹配的对象。 这些对象包括特定类型的计算机或用户组等项目。 查询可以返回大部分类型的 Configuration Manager 对象，包括站点、集合、应用程序和清单数据。  

 创建查询时，必须至少指定两个参数：搜索位置和搜索内容。 例如，若要查找 Configuration Manager 站点中所有计算机上的可用硬盘空间量，可以创建一个查询，搜索“逻辑磁盘”属性类以及可用硬盘空间的“可用空间 (MB)”属性。  

 在创建初始查询之后，可以指定其他查询条件。 例如，可以指定查询结果仅包括分配给指定站点的计算机。 还可以修改结果的显示方式，以便按照有意义的顺序查看结果。 例如，可以指定按可用硬盘空间量的升序或降序对结果进行排序。  

 创建查询时，它会由 Configuration Manager 存储并显示在“监视”工作区中的“查询”节点中。 从此位置可以创建新查询，然后运行、更新或管理现有查询。  

 还可以将查询导入 Configuration Manager 集合中的查询规则中。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中创建集合](../../../core/clients/manage/collections/create-collections.md)。  

## <a name="see-also"></a>另请参阅  
 [System Center Configuration Manager 的查询技术参考](../../../core/servers/manage/queries-technical-reference.md)
