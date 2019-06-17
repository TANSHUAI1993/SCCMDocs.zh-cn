---
title: 在桌面 Analytics 中的资产
titleSuffix: Configuration Manager
description: 了解有关设备、 驱动程序和桌面 Analytics 中的应用程序。
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 972ccf97590cb7662b5bf0a8e5bd3acb410f5766
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67145806"
---
# <a name="assets-in-desktop-analytics"></a>在桌面 Analytics 中的资产

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

设备到桌面 Analytics 报告数据后，它提供了以下资产的清单：

- 设备  
- 硬件驱动程序  
- 已安装的应用  

在服务门户中，选择**资产**Desktop 分析菜单中。


## <a name="devices"></a>设备

**设备**选项卡显示注册到 Desktop 分析在组织中的所有设备有关的关键信息。 您可以对任何列或筛选器的特定值进行排序。

> [!NOTE]  
> 如果仪表板并不报告的设备数预期为您的环境，请参阅[Desktop 分析故障排除](/sccm/desktop-analytics/troubleshooting)。  

在部署计划中，没有关于设备的更多详细信息。 有关详细信息，请参阅[计划资产](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## <a name="apps"></a>应用

**应用**选项卡上显示所有安装应用程序在 Windows 设备上检测到该服务。

**值得注意**超过 2%的已注册的设备上安装应用。

配置**重要性**的应用程序通过设置以下类别之一：

- 严重
- 重要提示
- 忽略
- 未检查

从列表中，选择应用，并选择**编辑**。 此操作将显示应用详细信息。 选择**重要性**下拉列表菜单，然后设置的值。 你还可以分配**所有者**。 如果您进行任何更改，则选择**保存**。

在部署计划中，您还可以设置**升级决策**。 有关详细信息，请参阅[计划资产](/sccm/desktop-analytics/about-deployment-plans#plan-assets)


## <a name="next-steps"></a>后续步骤

- [了解桌面分析部署计划](/sccm/desktop-analytics/about-deployment-plans)  

- [了解安全性和功能更新](/sccm/desktop-analytics/about-updates)  

- [在桌面 Analytics 中的兼容性评估](/sccm/desktop-analytics/compat-assessment)  
