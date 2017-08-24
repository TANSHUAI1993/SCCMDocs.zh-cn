---
title: "诊断数据集合 | Microsoft Docs"
description: "了解 System Center Configuration Manager 如何收集关于其自身的诊断和使用情况数据。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9c0165212fe34f460be2ce870d0542b616f3bc4d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>System Center Configuration Manager 如何收集诊断和使用情况数据

*适用范围：System Center Configuration Manager (Current Branch)*

若要为 System Center Configuration Manager 收集诊断和使用情况数据，每个主站点每周都会运行 SQL Server 查询。 在多站点层次结构中，数据会复制到管理中心站点。  

在层次机构的顶层站点上，服务连接点站点系统角色在检查更新时提交此信息。 服务连接点的模式决定数据的传输方式：  

-   **在联机模式下：** 每周自动从服务连接点向云服务发送一次诊断和使用情况数据。  

-   **在脱机模式下：** 使用服务连接工具手动传输诊断和使用情况数据。 有关详细信息，请参阅 [关于 System Center Configuration Manager 服务连接点](../../../core/servers/manage/use-the-service-connection-tool.md)。  

有关详细信息，请参阅 [关于 System Center Configuration Manager 服务连接点](../../../core/servers/deploy/configure/about-the-service-connection-point.md)。  
