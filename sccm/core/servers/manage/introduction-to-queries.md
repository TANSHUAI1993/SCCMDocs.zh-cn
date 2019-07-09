---
title: 查询简介
titleSuffix: Configuration Manager
description: 可创建和运行查询，在 System Center Configuration Manager 层次结构中查找与查询条件相匹配的对象。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28fe8d38b03efaa101cfe01d8a8a054f0b26f2ed
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561955"
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的查询简介

适用范围：  System Center Configuration Manager (Current Branch)

可创建和运行查询，在 System Center Configuration Manager 层次结构中查找与查询条件相匹配的对象。 这些对象包括特定类型的计算机或用户组等项。 查询可以返回大部分类型的 Configuration Manager 对象，包括站点、集合、应用程序和清单数据。  

## <a name="query-creation-overview"></a>查询创建概述

 创建查询时，必须至少指定两个参数：搜索位置和搜索内容。 例如，若要查找 Configuration Manager 站点中所有计算机上的可用硬盘空间量，可以创建查询来搜索“逻辑磁盘”  特性类，以及可用硬盘空间的“可用空间(MB)”  特性。  

 在创建初始查询之后，可以指定其他查询条件。 例如，可以指定查询结果仅包括分配给指定站点的计算机。 还可以更改结果显示方式，以按照对你有意义的顺序查看结果。 例如，可以指定按可用硬盘空间量对结果进行升序或降序排序。  

 创建的查询由 Configuration Manager 存储，并显示在“监视”  工作区的“查询”  节点中。 在此位置上，可以新建查询，并能运行、更新和管理现有查询。  

 还可以将查询导入 Configuration Manager 集合中的查询规则中。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中创建集合](../../../core/clients/manage/collections/create-collections.md)。  

## <a name="next-steps"></a>后续步骤

 [如何在 System Center Configuration Manager 中创建查询](../../../core/servers/manage/create-queries.md)
