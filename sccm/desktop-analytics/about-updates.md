---
title: 在桌面 Analytics 中的更新
titleSuffix: Configuration Manager
description: 了解有关桌面 Analytics 中的安全性和功能更新。
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7fc673cfa11224394df785f2e13e77ad2e0f5888
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159219"
---
# <a name="updates-in-desktop-analytics"></a>在桌面 Analytics 中的更新

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

在 Desktop 分析门户中查看安全性和功能更新的状态。 在 Desktop 分析主菜单的监视器组中选择这些节点。 这些节点让您的环境中深入了解这些更新的状态。



## <a name="security-updates"></a>安全更新

若要查看安全更新的当前状态，请选择**安全更新**中**监视器**Desktop 分析部分：

![安全更新桌面分析的节点](media/security-updates.png)

此视图汇总*安全*运行 Windows 10 的设备的更新。 按以下标签，条形图中的设备进行分类：

#### <a name="latest"></a>最新

设备正在运行该版本和通道的最新安全更新。

#### <a name="latest-1"></a>最新版本 1

设备运行早于最新的可用更新的安全更新一个版本，该通道上。

#### <a name="older"></a>较旧

设备正在运行早于最新版本 1 的安全更新。

#### <a name="not-measured"></a>不测量

桌面分析尚未评估设备。 此状态包括运行 Windows 预览体验计划的已注册的 Windows 7、 Windows 8.1 或 Windows 10 设备的设备。  



## <a name="feature-updates"></a>功能更新

若要查看功能更新的当前状态，请选择**功能更新**中**监视器**Desktop 分析部分：

![Desktop 分析的功能更新节点](media/feature-updates.png)

此视图汇总*功能*运行 Windows 10 的设备的更新。

服务段的详细信息，请参阅[Windows 生命周期简报](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。  

按以下标签，条形图中的设备进行分类：

#### <a name="in-service"></a>在服务中

设备正在运行该版本和通道的最新功能更新。  

#### <a name="near-end-of-service"></a>服务的接近结束

设备正在运行的服务的结束前的 90 天内的功能更新。

#### <a name="end-of-service"></a>服务的结束

设备正在运行已超过服务日期的功能更新。 有关终止服务日期的详细信息，请参阅[Windows 生命周期简报](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。

#### <a name="not-measured"></a>不测量

桌面分析尚未评估设备。 此状态包括运行 Windows 预览体验计划的已注册的 Windows 7、 Windows 8.1 或 Windows 10 设备的设备。



## <a name="next-steps"></a>后续步骤

- [了解有关桌面分析资产](/sccm/desktop-analytics/about-assets)： 设备、 驱动程序和应用  

- [了解如何部署计划](/sccm/desktop-analytics/about-deployment-plans)  
