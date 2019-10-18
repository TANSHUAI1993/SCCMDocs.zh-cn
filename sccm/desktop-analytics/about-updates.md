---
title: 桌面分析中的更新
titleSuffix: Configuration Manager
description: 了解桌面分析中的安全性和功能更新。
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f090c80f70ef8d286a36236c48503817adb93591
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72387035"
---
# <a name="updates-in-desktop-analytics"></a>桌面分析中的更新

在桌面分析门户中，查看 "安全和功能更新" 的状态。 在 "桌面分析" 主菜单的 "监视" 组中选择这些节点。 这些节点可让你深入了解环境中这些更新的状态。


## <a name="security-updates"></a>安全更新

若要查看当前的安全更新状态，请在 "桌面分析" 的 "**监视**" 部分中选择 "**安全更新**"：

![桌面分析的 "安全更新" 节点](media/security-updates.png)

此视图汇总了运行 Windows 10 的设备的*安全*更新。 条形图中的设备按以下标签分类：

#### <a name="latest"></a>最近

设备正在运行该版本和频道的最新安全更新。

#### <a name="latest-1"></a>最新-1

设备运行的安全更新版本早于该通道上的最新可用更新版本。

#### <a name="older"></a>保留

设备运行的安全更新早于最新版本。

#### <a name="not-measured"></a>未度量

桌面分析尚未评估设备。 此状态包括运行 Windows 7、Windows 8.1 的设备或为 Windows 预览体验计划注册的 Windows 10 设备。  

如果 Windows 10 设备未使用 Microsoft 帐户进行*身份验证*，则 windows 不会报告此数据。 此身份验证通常作为 Windows 安装程序全新体验（OOBE）的一部分完成。<!-- 5148153 -->


## <a name="feature-updates"></a>功能更新

若要查看功能更新的当前状态，请在 "桌面分析" 的 "**监视**" 部分中选择 "**功能更新**"：

![桌面分析的功能更新节点](media/feature-updates.png)

此视图汇总了运行 Windows 10 的设备的*功能*更新。

有关服务周期的详细信息，请参阅[Windows 生命周期事实数据表](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。  

条形图中的设备按以下标签分类：

#### <a name="in-service"></a>服务中

设备运行的是该版本和频道的最新功能更新。  

#### <a name="near-end-of-service"></a>接近服务结束

设备运行的功能更新在90天内到达服务结束。

#### <a name="end-of-service"></a>服务结束

设备运行的功能更新已超过服务截止日期。 有关服务日期结束的详细信息，请参阅[Windows 生命周期事实数据表](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。

#### <a name="not-measured"></a>未度量

桌面分析尚未评估设备。 此状态包括运行 Windows 7、Windows 8.1 的设备或为 Windows 预览体验计划注册的 Windows 10 设备。

如果 Windows 10 设备未使用 Microsoft 帐户进行*身份验证*，则 windows 不会报告此数据。 此身份验证通常作为 Windows 安装程序全新体验（OOBE）的一部分完成。<!-- 5148153 -->


## <a name="next-steps"></a>后续步骤

- [了解桌面分析资产](/sccm/desktop-analytics/about-assets)：设备、驱动程序和应用  

- [了解部署计划](/sccm/desktop-analytics/about-deployment-plans)  
