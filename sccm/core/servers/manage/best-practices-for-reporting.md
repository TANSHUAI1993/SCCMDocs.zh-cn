---
title: "报告最佳实践 | Microsoft Docs"
description: "阅读有关使用 System Center Configuration Manager 的报表功能的一些有用提示。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 759258999f3eaa810803a6a7f856f00fe7771a9e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager 中报告的最佳做法

*适用范围：System Center Configuration Manager (Current Branch)*

使用以下 System Center Configuration Manager 中的报表的最佳实践：  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>为了获得最佳性能，请将 Reporting Services 点安装在远程站点系统服务器上  
 尽管你可以将 Reporting Services 点安装在站点服务器或远程站点系统上，但如果将 Reporting Services 点安装在远程站点系统服务器上，性能将得到提升。  

## <a name="optimize-sql-server-reporting-services-queries"></a>优化 SQL Server Reporting Services 查询  
 通常，任何报表延迟都是由于运行查询和检索结果所花费的时间导致的。 如果你在使用 Microsoft SQL Server，则诸如查询分析器和事件探查器等工具可帮助你优化查询。  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>将报表订阅处理安排在标准办公时间之外运行  
 请尽可能将报表订阅处理安排在正常标准办公时间之外进行，以最大程度地减少 Configuration Manager 站点数据库服务器上的 CPU 处理。 这种方案还可改善不可预测报表请求的可用性。  

## <a name="next-steps"></a>后续步骤
[配置报表](configuring-reporting.md)
