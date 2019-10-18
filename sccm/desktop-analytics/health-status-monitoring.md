---
title: 运行状况监视
titleSuffix: Configuration Manager
description: 了解运行状况状态监视在桌面分析中的工作原理。
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b27238ea4a77879c353a882c860959d028b81adb
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72384940"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>桌面分析中的运行状况状态监视

在将[更新部署到生产环境](/sccm/desktop-analytics/deploy-prod)时，请使用桌面分析来帮助监视设备的运行状况状态。 本文详细说明了运行状况监视的工作原理。

有关如何使用此功能的详细信息，请参阅[监视已更新设备的运行状况](/sccm/desktop-analytics/deploy-prod#bkmk_monitor)。

![桌面分析的 "监视运行状况" 页的屏幕截图](media/monitor-health.png)

> [!NOTE]  
> 桌面分析仅从提供使用情况数据的设备收集运行状况数据，该数据可用作分母。 这意味着它不包含运行 Windows 7 和 Windows 10 的设备，这些设备未设置为在 "增强（受限）" 级别共享诊断数据。 如果将多个运行 Windows 10 的设备的设备数设置为在 "增强（受限）" 级别以外的级别上共享诊断数据，则 "**监视器运行状况**" 页将在标题区域显示警告。  

若要查看有关特定应用的详细信息，请在列表中选择它。



## <a name="apps"></a>应用

![桌面分析中应用的运行状况状态因素](media/monitor-health-status-factors.png)

桌面分析监视应用的以下运行状况状态因素：

- **出现故障的设备百分比**：过去两周内，此特定应用程序崩溃的设备数除以使用应用的设备数。 此视图可让你查看新操作系统版本上的应用稳定性是否已增加或减少。 桌面分析为以下集计算此百分比：  

    - **更新后**：已更新到部署计划中指定的目标 OS 版本的设备。 为了减少数据不足的资产数量，桌面分析为所有已更新的设备收集此数据。 此集包括不在部署计划中的那些设备。  

    - **更新之前**：版本低于部署计划中指定的操作系统版本的设备。 此列表不包括运行 Windows 7 的设备。  

    - **商业平均线**：所有商业设备的平均（平均）故障率。 此平均值在应用的*所有*版本中进行计算。 如果你的版本显示的故障率高于商业平均，则可能存在更稳定的可用版本。  

- **包含崩溃的会话百分比**：类似于前面的会话，但计算在过去两周内出现崩溃的会话百分比。  

若要确定应用程序的运行状况，桌面分析需要至少20台设备中的数据。 否则，它将报告应用的**数据不足**。 服务根据这些设备的*会话故障率*计算运行状况状态。 仅提供设备故障率以获取信息。 它不用于运行状况状态计算。

在应用详细信息页的底部，以下三个选项卡可帮助你进行故障排除：

- **其他版本**：此应用的替代版本的列表。 对于每个版本，它会显示组织内的故障率的相对变化和商业平均线。 如果找到应用程序的更高版本，但该应用程序的崩溃率较低，则更新应用程序可能会有所帮助。  

    它还显示了版本是否**为 Windows 就绪**状态。 有关详细信息，请参阅[兼容性评估](compat-assessment.md#driver-risk-assessment)。  

- **主要问题**：按实例计数列出的最常见故障 id。 失败 ID 标识与崩溃关联的堆栈跟踪。 在调用应用程序供应商以寻求支持时，可以使用此 ID。  

- **最近的故障**：应用最近崩溃的设备的列表。 可以按故障 ID 和其他条件进行筛选。 使用此信息来解决该问题，方法是：收集日志或尝试在特定设备上进行修复，然后再尝试进行更广泛的部署。  

如果发现你无法解决的严重运行状况回归，请将应用的**升级决策**更改为 "**无法**修复"。 此操作阻止将来将更新部署到具有此资产的设备。


## <a name="see-also"></a>另请参阅

- [桌面分析中的兼容性评估](/sccm/desktop-analytics/compat-assessment)  

- [如何通过桌面分析部署到生产环境](/sccm/desktop-analytics/deploy-prod)  
