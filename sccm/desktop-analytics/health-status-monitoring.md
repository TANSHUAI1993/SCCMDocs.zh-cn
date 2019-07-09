---
title: 运行状况监视
titleSuffix: Configuration Manager
description: 了解运行状况状态监视桌面 Analytics 中的工作方式。
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4b32105304354e9b9d4473451a32f52162f80d02
ms.sourcegitcommit: 20bbb870baf624c7809d3972f2d09a8d2df79cda
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2019
ms.locfileid: "67623339"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>在桌面 Analytics 中监视的运行状况状态

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

为您[将更新部署到生产](/sccm/desktop-analytics/deploy-prod)，使用 Desktop 分析来帮助监视你的设备的运行状况状态。 本文详细介绍运行状况监视的工作原理。

有关如何使用此功能的详细信息，请参阅[监视更新设备的运行状况](/sccm/desktop-analytics/deploy-prod#bkmk_monitor)。

![Desktop 分析的监视运行状况页屏幕截图](media/monitor-health.png)

> [!NOTE]  
> 桌面 Analytics 仅从设备提供可用作分母的使用情况数据收集运行状况数据。 这意味着它不包括运行 Windows 7 和 Windows 10 的设备不是设置共享的增强 （受限） 级别的诊断数据。 如果超过 10%的运行 Windows 10 的设备设置为共享在增强 （受限） 以外的级别的诊断数据**监视运行状况**页的标题区域中显示一条警告。  

若要查看有关特定应用的详细信息，请在列表中选择。



## <a name="apps"></a>应用

![在桌面 Analytics 中对应用的运行状况状态因素](media/monitor-health-status-factors.png)

桌面分析监视应用的以下运行状况状态因素：

- **出现故障的设备百分比**:过去两周内，为此特定应用程序发生崩溃的设备数除以在其使用该应用的设备数。 此视图可以查看应用程序稳定性是否已增加或减少新操作系统版本上。 桌面分析计算下面的设置此百分比：  

    - **更新后**:已更新到部署计划中指定的目标 OS 版本的设备。 若要减少具有足够的数据资产的数量，桌面 Analytics 中收集所有更新设备，这些的数据。 此集部署计划中不包括这些设备。  

    - **更新前**:设备上的操作系统版本早于部署计划中指定的内容。 此列表不包括运行 Windows 7 的设备。  

    - **商业平均**:平均值 (avg) 在所有商业设备上崩溃率。 在计算此平均值*所有*版本的应用程序。 如果你的版本显示故障率高于商业平均水平，可能有更稳定版本可用。  

- **%崩溃会话**:类似于前面的但过去两周内包含的会话百分比崩溃的计数。  

若要确定应用程序的运行状况状态，桌面分析要求至少 20 个设备中的数据。 否则，它报告**数据不足**应用。 服务能计算的基于运行状况*会话崩溃率*从这些设备。 设备故障率是只用于提供信息。 它未在运行状况状态计算中使用。

应用详细信息页的底部，在以下三个选项卡可以帮助您进行故障排除：

- **其他版本**:此应用程序的备用版本的列表。 对于每个版本，它显示在你的组织和商业平均水平的故障率的相对更改。 如果发现使用较低的故障率应用程序的更高版本，更新应用程序可能会帮助。  

    它还演示了是否版本都具有**准备用于 Windows**信号。 有关详细信息，请参阅[兼容性评估](compat-assessment.md#driver-risk-assessment)。  

- **热门问题**:按实例计数最常见失败 Id 的列表。 失败 ID 标识与故障相关联的堆栈跟踪。 当应用程序供应商寻求支持时，可以使用此 ID。  

- **最近崩溃**:应用最近崩溃的设备的列表。 您可以通过失败 ID 和其他条件进行筛选。 使用此信息来收集日志或尝试更广泛的部署之前尝试修复特定设备上的解决此问题。  

如果您发现您无法解决的严重运行状况回归，更改应用的**升级决策**到**无法**。 此操作阻止将来部署更新到与此资产的设备。


## <a name="see-also"></a>另请参阅

- [在桌面 Analytics 中的兼容性评估](/sccm/desktop-analytics/compat-assessment)  

- [如何将部署到生产环境且 Desktop 分析](/sccm/desktop-analytics/deploy-prod)  
