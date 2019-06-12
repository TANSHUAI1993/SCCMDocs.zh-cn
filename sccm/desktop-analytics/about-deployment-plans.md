---
title: 在桌面 Analytics 中的部署计划
titleSuffix: Configuration Manager
description: 了解桌面 Analytics 中的部署计划。
ms.date: 06/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88c78cef4717cc3a51a53b7fd5aba0cbefa93a8e
ms.sourcegitcommit: 0bd336e11c9a7f2de05656496a1bc747c5630452
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2019
ms.locfileid: "66834927"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>有关桌面 Analytics 中的部署计划

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

桌面 Analytics 收集并分析你的组织中的设备、 应用程序和驱动程序数据。 基于此分析和你的输入，可以使用该服务来创建适用于 Windows 10 的部署计划。 部署计划具有以下功能：  

- 自动建议要包括在试验中的设备  

- 确定兼容性问题和建议的缓解措施  

- 评估部署之前、 期间和之后的更新的运行状况  

- 跟踪部署进度  

作为部署计划的一部分，你可以执行以下操作：  

- 定义要部署哪些版本的 Windows 10  

- 选择你想要部署的设备哪些组  

- 创建用于部署的准备情况规则  

- 定义您的应用程序的重要性  

- 选择基于自动建议的试验设备  

- 决定如何修复应用根据 Desktop 分析建议的问题  

默认情况下，桌面分析每日刷新部署计划数据。 部署计划，例如，分配到应用程序的重要性或选择要包含在试点范围内中的设备中的任何更改将花费最多 24 小时来处理。 若要加快此过程，请求按需数据刷新。 有关详细信息，请参阅[Desktop 分析常见问题](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。  

连接到 Configuration Manager Desktop 分析后, 选择部署计划中的集合。 然后此集成可以将 Windows 部署到基于桌面分析数据的集合。



## <a name="readiness-rules"></a>准备情况规则

部署计划中提供了以下的准备情况规则：

- 无论你的设备自动从 Windows 更新接收驱动程序。 如果设备从 Windows 更新接收驱动程序更新，则标识为准备情况评估的一部分的任何驱动程序问题自动标记为**准备**。  

- 低安装计数阈值为 Windows 应用。 如果百分比大于此阈值更高版本的计算机上安装应用，部署计划将标记应用作为**Noteworthy**。 此标记表示可以决定要在试验阶段测试是非常重要。  



## <a name="importance"></a>重要性

作为部署计划的一部分，设置*重要性*的应用。 桌面分析检测到目标设备上安装这些应用。 此设置可帮助桌面分析确定它在试验阶段的部署中包括哪些设备。

如果小于 2%的目标设备上安装应用，将被标记**低安装计数**。 默认值为 %2%。 您可以调整中从 0%到 10%的准备情况设置的阈值。 桌面分析会自动将标记为这些应用程序**已准备好升级**。  

对于应用程序，选择的重要性**严重**，**重要**，或**不重要**。 如果你将标记为关键或重要的其中一个，桌面分析包括该应用的某些设备中试验部署。 该服务包括在试点的关键应用程序的更多实例。 如果标记为不重要的应用，桌面分析自动将其设置为**已准备好升级**。



## <a name="pilot-devices"></a>试验设备

桌面分析结合了与全局试验设置你重要性的信息。 然后，它创建为其设备应试验部署的一部分的建议。 建议的试验部署包括具有不同的硬件配置的设备和所有关键和重要应用的一个或多个实例。 如果应用程序标记为关键，该服务建议使用该应用在试用中的更多设备。



## <a name="deployment-plans-in-configuration-manager"></a>在 Configuration Manager 中的部署计划

在创建部署计划，使用 Configuration Manager 来部署产品。 在部署开始时，桌面分析会监视基于设置的计划中的部署。


## <a name="next-steps"></a>后续步骤

- [了解有关桌面分析资产](/sccm/desktop-analytics/about-assets)： 设备、 驱动程序和应用  

- [了解安全性和功能更新](/sccm/desktop-analytics/about-updates)  

- [创建部署计划](/sccm/desktop-analytics/create-deployment-plans)  
