---
title: 诊断和使用情况数据
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager 收集的关于其自身的诊断和使用情况数据。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a70f632c04d7202ed1c41e5e138ed63dfdba1c6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>System Center Configuration Manager 的诊断和使用情况数据

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 收集有关自身的诊断和使用情况数据，Microsoft 使用这些数据改进将来版本的安装体验、质量和安全性。  

 诊断和使用情况数据可用于每个 Configuration Manager 层次结构。 它包含在每个主站点和管理中心站点每周运行一次的 SQL Server 查询。 层次结构使用管理中心站点时，主站点中的数据随后会复制到该站点。 在层次机构的顶层站点上，服务连接点在检查更新时提交此信息。 如果服务连接点处于脱机模式下，则将使用服务连接工具传输信息。  

> [!NOTE]  
>  Configuration Manager 仅从站点 SQL Server 数据库收集数据，而不会直接从客户端或站点服务器收集数据。  

 有关详细信息，请参阅 [Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkID=626527)。  

## <a name="articles"></a>文章
 可在以下文章中详细了解 Configuration Manager 的诊断和使用情况数据：  

-   [如何使用诊断和使用情况数据](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   诊断使用情况数据收集的级别：
    - [1802 的诊断数据](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1802)  
    - [1710 的诊断数据](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1710)  
    - [1706 的诊断数据](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1706)    

<!--
    - [Diagnostic data for 1702](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [Diagnostic data for 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [Diagnostic data for  1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [如何收集诊断和使用情况数据](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [如何查看诊断和使用情况数据](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [客户体验改善计划 (CEIP)](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

     > [!Note]  
     > 从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。


-   [有关诊断和使用情况数据的常见问题](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>另请参阅  
 [关于服务连接点](../../../core/servers/deploy/configure/about-the-service-connection-point.md)
