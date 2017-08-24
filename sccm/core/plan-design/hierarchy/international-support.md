---
title: "国际支持 | Microsoft Docs"
description: "配置 System Center Configuration Manager 以符合特定的国际要求。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3bab51be96445f766e8f5bbf54eee854e5d09cee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="international-support-in-system-center-configuration-manager"></a>System Center Configuration Manager 的国际支持

*适用范围：System Center Configuration Manager (Current Branch)*

以下部分提供技术详细信息，帮助使 System Center Configuration Manager 符合特定的国际要求。  

## <a name="gb18030-requirements"></a>GB18030 要求  
 Configuration Manager 符合在 GB18030 中定义的标准，因此，可以在中国使用 Configuration Manager。 Configuration Manager 部署必须具有下列配置才能符合 GB18030 要求：  

-   与 Configuration Manager 一起使用的每台站点服务器计算机和 SQL Server 计算机都必须使用中文操作系统。  

-   层次结构中的每个站点数据库和 SQL Server 的每个实例都必须使用相同的排序规则，而且必须是下列排序规则之一：  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  对于[对 System Center Configuration Manager 的 SQL Server 版本的支持](../../../core/plan-design/configs/support-for-sql-server-versions.md)中所述的要求，这些数据库排序规则是一个例外。  

-   必须将名为 **GB18030.SMS** 的文件放在层次结构中的每台站点服务器计算机的系统卷根文件夹下。 此文件不包含任何数据，而且可能是按照此要求命名的空白文本文件。  
