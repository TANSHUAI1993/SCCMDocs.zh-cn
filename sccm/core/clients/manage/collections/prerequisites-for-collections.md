---
title: "集合先决条件 | Microsoft Docs"
description: "在 System Center Configuration Manager 中获取使用集合的先决条件。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 41fc3eb20a7441939eb0dc80bc121c8f3ea322b2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager 中集合的先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的集合仅包含产品内部的依赖关系。  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  

|依赖关系|更多信息|  
|----------------|----------------------|  
|Reporting Services 点|在运行集合的报表前，必须先安装 Reporting Services 点站点系统角色。 有关详细信息，请参阅 [System Center Configuration Manager 中的报表](../../../../core/servers/manage/reporting.md)。|  
|必须授予特定的安全权限来管理集合|必须具有以下安全权限才能管理符合性设置：<br /><br /> - 若要创建和管理集合：“集合”对象的“创建”、“删除”、“修改”、“修改文件夹”、“移动对象”、“读取”和“读取资源”。<br /><br /> - 若要管理集合设置：“集合”对象的“修改集合设置”。<br /><br /> 所有集合文件夹（包括根文件夹）都需要“修改文件夹”  权限。|  
