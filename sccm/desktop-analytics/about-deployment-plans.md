---
title: 在桌面 Analytics 中的部署计划
titleSuffix: Configuration Manager
description: 了解桌面 Analytics 中的部署计划。
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce726ffa0dfc8a46bd0891e50ff087ad4931d901
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754709"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>有关桌面 Analytics 中的部署计划 

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

桌面 Analytics 收集并分析你的组织中的设备、 应用程序和驱动程序数据。 基于此分析和你的输入，可以使用该服务来创建适用于 Windows 10 和 Office 365 专业增强版部署计划。 部署计划具有以下功能：  

- 自动建议要包括在试验中的设备  

- 确定兼容性问题和建议的缓解措施  

- 评估部署之前、 期间和之后的更新的运行状况  

- 跟踪部署进度  


作为部署计划的一部分，你可以执行以下操作：  

 - 定义要部署哪些产品和版本：Windows 10，Office 365 专业增强版，和 / 或  

 - 选择你想要部署的设备哪些组  

 - 创建用于部署的准备情况规则  

 - 定义应用程序和 Office 加载项的重要性  

 - 选择基于自动建议的试验设备  

 - 决定如何修复应用程序和 Office 加载项根据 Desktop 分析建议的问题  


桌面分析每日刷新部署计划数据。 所做的任何更改可能不会显示 24 小时。 此类更改包括将重要性分配到应用程序，或选择要包括在试验中的设备。  

如果将桌面 Analytics 连接到 Configuration Manager，部署计划中选择您的集合。 然后此集成可以将 Windows 或 Office 部署到基于桌面分析数据的集合。 

如果不使用配置管理器，您可以在 Log Analytics 中创建组。 有关详细信息，请参阅[日志搜索在 Log Analytics 中的计算机组](https://docs.microsoft.com/azure/log-analytics/log-analytics-computer-groups)。 



## <a name="readiness-rules"></a>准备情况规则

部署计划中提供了以下的准备情况规则：

- 无论你的设备自动从 Windows 更新接收驱动程序。 如果设备从 Windows 更新接收驱动程序更新，则标识为准备情况评估的一部分的任何驱动程序问题自动标记为**准备**。  

- 低安装计数阈值为 Windows 应用。 如果百分比大于此阈值更高版本的计算机上安装应用，部署计划将标记应用作为**Noteworthy**。 此标记表示可以决定要在试验阶段测试是非常重要。  

- 更新 Office 365 专业增强版从 32 位到 64 位 Windows 的 64 位版本的设备上。 此行为是默认值。  

- 从较旧版本的 Office 更新时，将较旧的 Office 应用，即使在较新的 Office 版本中不存在这些应用程序。 此行为不在默认情况下。  

- 低安装 Office 加载项的计数阈值。默认阈值为`2%`。 低于此阈值的外接程序将自动设置为*低安装计数*。 桌面分析在试用期间不会验证这些加载项。 

    如果外接程序安装在大于此阈值为较高百分比的计算机外, 接程序作为将标记部署计划*Noteworthy*。 然后可以决定要在试验阶段测试其重要性。   



## <a name="importance"></a>重要性

作为部署计划的一部分，设置*重要性*的应用和 Office 加载项。桌面分析检测到目标设备上安装这些应用。 此设置可帮助桌面分析确定它在试验阶段的部署中包括哪些设备。 

如果小于 2%的目标设备上安装的应用程序或外接程序，将被标记**低安装计数**。 默认值为 %2%。 您可以调整中从 0%到 10%的准备情况设置的阈值。 这些应用程序和外接程序作为桌面分析会自动将标记**已准备好升级**。  

对于应用程序和外接程序，请选择的重要性**严重**，**重要**，或**不重要**。 如果你将标记为关键或重要的其中一个，Desktop 分析包括该应用程序或外接程序的某些设备中试验部署。 该服务包括在试点的关键应用程序或外接程序的更多实例。 如果将应用标记或外接程序为不重要，桌面分析自动将其设置为**已准备好升级**。



## <a name="pilot-devices"></a>试验设备

桌面分析结合了与全局试验设置你重要性的信息。 然后，它创建为其设备应试验部署的一部分的建议。 建议的试验部署包括具有不同的硬件配置的设备和所有关键和重要应用的一个或多个实例。 如果应用程序标记为关键，该服务建议使用该应用在试用中的更多设备。



## <a name="deployment-plans-in-configuration-manager"></a>在 Configuration Manager 中的部署计划

在创建部署计划，使用 Configuration Manager 来部署产品。 在部署开始时，桌面分析会监视基于设置的计划中的部署。

<!--more on deployment plans in SCCM-->

<!-- test comment-->

## <a name="next-steps"></a>后续步骤

- [了解有关桌面分析资产](/sccm/desktop-analytics/about-assets)： 设备、 应用、 Office 应用、 Office 加载项和 Office 宏  

- [了解安全性和功能更新](/sccm/desktop-analytics/about-updates)  

- [创建部署计划](/sccm/desktop-analytics/create-deployment-plans)  

