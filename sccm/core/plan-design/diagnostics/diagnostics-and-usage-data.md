---
title: "诊断和使用情况数据 | Microsoft Docs"
description: "了解 System Center Configuration Manager 收集的关于其自身的诊断和使用情况数据。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4a4b7c9c0d40b6bd3ea2f318e37d744f1a0cc084
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>System Center Configuration Manager 的诊断和使用情况数据

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 收集有关自身的诊断和使用情况数据，Microsoft 使用这些数据改进将来版本的安装体验、质量和安全性。  

 诊断和使用情况数据可用于每个 System Center Configuration Manager 层次结构。 它包含在每个主站点和管理中心站点每周运行一次的 SQL Server 查询。 层次结构使用管理中心站点时，主站点中的数据随后会复制到该站点。 在层次机构的顶层站点上，服务连接点在检查更新时提交此信息。 如果服务连接点处于脱机模式下，则将使用服务连接工具传输信息。  

> [!NOTE]  
>  Configuration Manager 仅从站点 SQL Server 数据库收集数据，而不会直接从客户端或站点服务器收集数据。  

 有关详细信息，请参阅 [System Center Configuration Manager 隐私声明](http://go.microsoft.com/fwlink/?LinkID=626527)。  

 可在以下文章中详细了解 System Center Configuration Manager 的诊断和使用数据：  

-   [如何将诊断和使用情况数据用于 System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   诊断使用情况数据收集的级别：
    - [1702 的诊断数据](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [1610 的诊断数据](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [1606 的诊断数据](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    

<!--
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [System Center Configuration Manager 如何收集诊断和使用情况数据](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [如何查看 System Center Configuration Manager 的诊断和使用情况数据](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [System Center Configuration Manager 的客户体验改善计划 (CEIP)](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

-   [有关 System Center Configuration Manager 的诊断和使用情况数据的常见问题](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>另请参阅  
 [关于 System Center Configuration Manager 中的服务连接点](../../../core/servers/deploy/configure/about-the-service-connection-point.md)
