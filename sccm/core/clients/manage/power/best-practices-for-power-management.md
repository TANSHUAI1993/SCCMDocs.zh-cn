---
title: 有关电源管理的建议
titleSuffix: Configuration Manager
description: 了解 Microsoft 对 Configuration Manager 中电源管理的建议。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: a68dceb82f630720287b5215fbdad15eb5bebf93
ms.sourcegitcommit: cdf2827fb3f44d7522a9b533c115f910aa9c382a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70902593"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>对 Configuration Manager 中电源管理的建议

适用范围：  System Center Configuration Manager (Current Branch)

使用以下对 Configuration Manager 中电源管理的建议。  

## <a name="monitor-at-a-representative-time"></a>在具有代表性的时间进行监视

电源管理的监视阶段提供所在组织中计算机的以下信息：

- 功率消耗
- 活动
- 电源管理功能
- 环境影响

选择具有代表性的时间进行设备监视。 例如，在公休假日期间进行监视不会提供关于计算机电源使用情况的真实报表。

## <a name="create-a-control-collection"></a>创建控制集合

创建两个计算机集合以帮助你监视向计算机应用电源计划的效果。 第一个集合应包含大多数要对其应用电源设置的计算机。 控制集合应包含剩余的计算机  。 将所需的电源管理计划应用于第一个集合。 然后运行报表来比较两个集合之间的影响。  

## <a name="run-reports-before-you-apply-a-plan"></a>先运行报表然后再应用计划

向计算机集合应用电源管理计划之前，先运行“电源设置”报表  。 使用此报表来帮助了解已在集合中的计算机上配置的电源管理设置。 如果不先检查现有设置就将新的电源管理设置应用于计算机，这可能使功率消耗变大。  

## <a name="exclude-servers"></a>排除服务器

不支持对运行 Windows Server 的计算机进行电源管理。 将服务器添加到集合，并从电源管理中将其排除。  

> [!NOTE]
> 尽管 Configuration Manager 不支持 Windows Server 电源管理，但仍会收集电源使用情况数据，用于分析和报告。

## <a name="exclude-other-computers"></a>排除其他计算机

如果不希望通过电源管理对某些计算机进行管理，请将这些计算机添加到排除集合。  

可能会想要从电源管理中排除以下类型的计算机：

- 必须保持开机状态的计算机。  

- 用户需要远程连接到的计算机。  

- 不能使用电源管理的计算机。  

- 具有分发点站点系统角色的计算机。  

- 公用计算机（如网亭计算机、信息显示器或监视控制台），其中的计算机和监视器必须保持开启状态。  

有关详细信息，请参阅[配置电源管理](/sccm/core/clients/manage/power/configuring-power-management)。  

## <a name="apply-power-plans-to-a-test-collection"></a>向测试集合应用电源计划

在将电源计划应用于较大的计算机集合前，务必测试对计算机测试集合应用电源管理计划的效果。  

将计算机排除电源管理时，所有电源设置都将恢复为其初始值。 无法将单个电源设置还原为其初始值。  

## <a name="apply-power-plan-settings-individually"></a>单独应用电源计划设置

先监视应用每个电源设置的效果，然后再应用下一个设置。 此过程可确保每个设置都产生所需的效果。 有关电源计划设置的详细信息，请参阅[可用的电源管理计划设置](/sccm/core/clients/manage/power/create-and-apply-power-plans#BKMK_Plans)。  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>针对多个电源计划定期监视计算机

电源管理包括显示应用了多个电源计划的计算机的报告：具有多个电源计划的计算机  。

如果计算机是多个集合的成员，每个应用不同的电源计划，则适用以下行为：  

- 电源计划  ：如果对某计算机应用了电源设置的多个值，则计算机使用限制最少的值。  

- 唤醒时间  ：如果将多个唤醒时间应用到台式计算机，则计算机使用最接近午夜的时间。  

有关详细信息，请参阅[具有多个电源计划的计算机](/sccm/core/clients/manage/power/monitor-and-plan-for-power-management#BKMK_Multiple)。  

## <a name="save-or-export-power-management-information"></a>保存或导出电源管理信息

在监视和符合性阶段运行报表时，保存或导出结果。 保留数据供以后比较适用，以防 Configuration Manager 以后删除数据。  

Configuration Manager 在站点数据库中保留以下电源管理信息：

- 每日报表所使用的电源管理信息：31 天

- 每月报表所使用的电源管理信息：13 个月
