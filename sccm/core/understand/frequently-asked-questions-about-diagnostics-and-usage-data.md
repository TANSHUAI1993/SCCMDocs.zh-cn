---
title: "诊断数据常见问题解答 | Microsoft Docs"
description: "查找有关 System Center Configuration Manager 的诊断和使用情况数据的常见问题。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 177a30a30f6b8579fa1956d28581d4f9d3a11838
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>有关 System Center Configuration Manager 的诊断和使用情况数据的常见问题

*适用范围：System Center Configuration Manager (Current Branch)*

以下是有关 System Center Configuration Manager 的诊断和使用情况数据的常见问题：  

###  <a name="bkmk_off"></a> 如何关闭遥测？  
无法关闭遥测。 但是，你可以选择所收集的遥测数据的级别。 此外，还可以在脱机模式下使用服务连接点来帮助管理遥测数据的提交时间。

需要定期更新 Configuration Manager 的 Current Branch，以支持新版本的 Windows 10 和 Microsoft Intune。 Microsoft 至少需要基本级别的诊断和使用情况数据来使产品保持最新状态、改进更新体检以及提高产品的质量和安全性。

###  <a name="bkmk_retention"></a> 数据保留期为多久？  
 诊断和使用数据的保留期为一年。  

###  <a name="bkmk_update"></a> 安装或更新产品时是否发送了诊断和使用情况数据？  
 否。 仅当安装站点且可对其进行操作之后，才发送诊断和使用情况数据。  

###  <a name="bkmk_frequency"></a> 发送数据的频率是多高？  
 SQL 存储过程每七天（自安装站点之日起）运行一次。 在联机模式下，服务连接点配置为在查询运行后上传数据。 在脱机模式下，管理员使用服务连接工具上传数据。 （注意：安装站点后七天之内，数据最初不可脱机使用。）  

###  <a name="bkmk_network"></a> 可否将数据用于形成网络映射？  
 如 System Center Configuration Manager 的诊断使用情况数据收集的级别描述中所示，站点详细信息包括每个站点中的时区信息。 此信息使你能够深入了解层次结构中站点广泛的地理位置和全球分布。 但是，不会收集网络详细信息（例如 IP 地址或更详细的地理位置信息）。
 - [1511 的诊断数据](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [1602 的诊断数据](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [1606 的诊断数据](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [1610 的诊断数据](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="bkmk_tables"></a> 可以查看自定义表中的数据吗？  
 否。 通过 SQL 存储过程，针对数据库中的默认产品表收集诊断和使用情况数据（所有表都带有前缀 **TEL_**）。 作为 SQL 架构检测查询的一部分，对所有表名称进行了哈希处理，以便与已知默认值进行比较。 这可以确定数据库（由默认值扩展而来的数据库架构）中存在自定义表，但不能确定这些表中包含的任何数据。  

###  <a name="bkmk_databases"></a>你能看到其他数据库的名称或其他数据库中的数据吗？  
 否。 用于收集数据的存储过程仅限于站点数据库。  

## <a name="see-also"></a>另请参阅  
 [System Center Configuration Manager 的诊断和使用情况数据](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)
