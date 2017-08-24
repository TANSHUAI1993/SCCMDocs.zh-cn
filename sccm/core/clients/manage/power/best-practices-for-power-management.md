---
title: "电源管理的最佳实践 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中电源管理的最佳方案。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d3cc24c7923141f039dcda26ac27489cb0143e89
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中电源管理的最佳方案

*适用范围：System Center Configuration Manager (Current Branch)*

使用以下 System Center Configuration Manager 中电源管理的最佳方案。  

## <a name="perform-the-monitoring-phase-at-a-representative-time"></a>在具有代表性的时间执行监视阶段  
 电源管理的监视阶段为你提供有关组织中计算机的功率消耗、活动、电源管理功能和环境影响的信息。 确保你选择一个具有代表性的时间来执行监视阶段。 例如，在公休假日期间执行监视阶段不会提供关于计算机电源使用情况的真实报表。  

## <a name="create-a-control-collection-of-computers-with-no-power-plans-applied"></a>创建未应用任何电源计划的计算机的控件集合  
 创建两个计算机集合以帮助你监视向计算机应用电源计划的效果。 第一个集合应包括要对其应用电源设置的大多数计算机，另一个集合（即控件集合）应包含剩余的计算机。 将所需电源管理计划应用与包含大多数计算机的集合。 然后可以运行报表，将应用了电源设置的计算机与未应用电源设置的控件集合的的电力成本、电源使用情况以及环境影响进行比较。  

## <a name="run-the-power-settings-report-before-you-apply-a-power-management-plan"></a>先运行电源设置报表，然后再应用电源管理计划  
 将电源管理计划应用到计算机的集合之前，请运行“电源设置”  报表，帮助你了解已在集合中的计算机上配置的电源管理设置。 如果不先检查现有设置就将新的电源管理设置应用于计算机，这可能导致功率消耗变大。  

## <a name="exclude-servers-from-power-management"></a>从电源管理中排除服务器  
 运行 Windows Server 的计算机不支持电源管理（尽管已收集电源使用情况数据）。 确保将服务器添加到集合，并从电源管理中将其排除。  

## <a name="exclude-computers-that-you-do-not-want-to-manage"></a>排除你不希望管理的计算机  
 如果你有不希望使用电源管理进行管理的计算机，请将它们添加到集合，并确保该集合已从电源管理中排除。  

 你可能想要从电源管理中排除的计算机的示例包括：  

-   必须保持开机状态的计算机。  

-   用户需要通过使用远程桌面连接来连接的计算机。  

-   不能使用电源管理的计算机。  

-   具有分发点站点系统角色的计算机。  

-   其中的计算机和监视器必须保持开启状态的公用计算机（如网亭计算机、信息显示器或监视控制台）。  

 有关详细信息，请参阅[在 System Center Configuration Manager 中配置电源管理](../../../../core/clients/manage/power/configuring-power-management.md)。  

## <a name="first-apply-power-plans-to-a-test-collection-of-computers"></a>首先，向计算机的测试集合应用电源计划  
 在将电源计划应用于较大的计算机集合前，务必测试对计算机测试集合应用电源管理计划的效果。  

 应用于运行 Windows XP 或 Windows Server 2003 的计算机的电源设置不会还原为其原始值，即使从电源管理中排除该计算机。 在更高版本的 Windows 中，从电源管理中排除一台计算机会导致所有电源设置还原到其原始值。 无法将单个电源设置还原为其初始值。  

## <a name="apply-power-plan-settings-individually"></a>单独应用电源计划设置  
 先监视应用每个电源设置的效果，然后再应用下一个设置，以确保每个设置都具有所需的效果。 有关电源计划设置的详细信息，请参阅[如何在 System Center Configuration Manager 中创建并应用电源计划](../../../../core/clients/manage/power/create-and-apply-power-plans.md)主题中的[可用的电源管理计划设置](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans)。  

## <a name="regularly-monitor-computers-to-see-if-they-have-multiple-power-plans-applied"></a>定期监视计算机以查看它们是否应用多个电源计划  
 电源管理包括显示应用了多个电源计划的计算机的报告。  

 如果某台计算机是多个集合的成员，且每个集合应用不同的电源计划，则应执行以下操作：  

-   电源计划：如果对某计算机应用了电源设置的多个值，则使用限制最少的值。  

-   唤醒时间：如果对台式计算机应用多个唤醒时间，则将使用最接近午夜的时间。  

     有关详细信息，请参阅[如何在 System Center Configuration Manager 中监视和规划电源管理](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)主题中的[具有多个电源计划的计算机](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Multiple)。 有关电源管理如何解决冲突的详细信息，请参阅[如何在 System Center Configuration Manager 中创建并应用电源计划](../../../../core/clients/manage/power/create-and-apply-power-plans.md)。  

## <a name="save-or-export-power-management-information-during-the-monitoring-and-planning-phase-of-power-management"></a>在电源管理的监控和规划阶段保存或导出电源管理信息  
 每日报表所使用的电源管理信息将在 Configuration Manager 站点数据库中保留 31 天。  

 每月报表所使用的电源管理信息将在 Configuration Manager 站点数据库中保留 13 个月。  

 在电源管理的监视和规划阶段以及符合性阶段运行报表时，请从要为将来对比保留数据的报表保存或导出结果，以免以后 Configuration Manager 将其删除。  
