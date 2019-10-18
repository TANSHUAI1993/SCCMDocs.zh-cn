---
title: 如何创建部署计划
titleSuffix: Configuration Manager
description: 在桌面分析中创建部署计划的操作指南。
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 03befc6758d70acd93f1d884b9f29ca01483fe01
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72386541"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>如何在桌面分析中创建部署计划

本文提供在桌面分析中创建部署计划的步骤。 在开始之前，请先[了解部署计划](/sccm/desktop-analytics/about-deployment-plans)。

## <a name="create-a-plan-for-windows-10"></a>为 Windows 10 创建计划

按照本部分中的步骤使用桌面分析来创建用于部署 Windows 10 的计划。

1. 打开[桌面分析门户](https://aka.ms/desktopanalytics)。 使用至少具有**工作区参与者**权限的凭据。  

2. 选择 "管理" 组中的 "**部署计划**"。  

3. 在 "**部署计划**" 窗格中，选择 "**创建**"。  

4. 在 "**创建部署计划**" 窗格中，配置以下设置：  

    - **名称**：部署计划的唯一名称  

    - "**产品" 和 "版本**"：选择要部署的 Windows 10 版本。 Microsoft 建议创建使用最新版本的部署计划。  

    - **设备组**：选择一个或多个组，然后选择 "**设置为目标组**"。 用**SCCM**作为源的组是从 Configuration Manager 同步的集合。  

    - **就绪规则**：这些规则可帮助确定哪些设备符合升级条件。 有关详细信息，请参阅[准备情况规则](#readiness-rules)。  

    - **完成日期**：选择要将 Windows 完全部署到所有目标设备的截止日期。  

5. 选择“创建”。 新计划将显示在部署计划的列表中，而不会进行处理。 若要加快处理过程，请请求按需进行数据刷新。 有关详细信息，请参阅[桌面分析常见问题解答](/sccm/desktop-analytics/faq##can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。  

6. 通过选择部署计划的名称将其打开。  

7. 在 "部署计划" 菜单上的 "**准备**" 组中，选择 "**标识重要性**"。  

    1. 在 "**应用**" 选项卡上，选择仅显示**未查看**的资产。  

    2. 选择每个应用，然后选择 "**编辑**"。 您可以选择同时编辑多个应用程序。  

    3. 从 "**重要性**" 列表中选择重要性级别。 如果希望在试验期间进行桌面分析来验证应用，请选择 "**关键**" 或 "**重要**"。 它不会验证标记为**不重要**的应用。 在分配重要性级别时评估其[兼容性](/sccm/desktop-analytics/compat-assessment)和其他计划见解。  

        分配重要性级别时，还可以选择升级决策。  

    4. 完成后选择 "**保存**"。  

8. 在 "部署计划" 菜单上的 "**准备**" 组中，选择 "**标识试点**"。  

    1. 查看推荐的设备进行试验。  

    2. 选择每个设备，并选择 "**添加到试点**"。 如果你不同意此建议，请选择 "**替换**"。  

        有关桌面分析如何进行这些建议的详细信息，请选择 "**标识试验**" 窗格右上角的 "信息" 图标。

## <a name="readiness-rules"></a>准备情况规则

这些规则可帮助你确定哪些设备符合就地升级。 您可以在创建部署计划时设置这些规则，或在以后编辑它们。

更改准备情况规则：

1. 在桌面分析门户中，选择 "部署计划"。
1. 选择名称旁边的 "**编辑**"。
1. 选择**准备情况规则**。
1. 选择 " **WINDOWS OS**"。
1. 根据需要进行更改，然后选择 "**保存**"。

对于**WINDOWS OS**升级，有两个可用的规则：设备驱动程序和 Windows 应用程序。

### <a name="device-drivers"></a>设备驱动程序

配置设备是否从 Windows 更新获取驱动程序。 默认情况下，此值为**Off** 。 当你使用 Windows 更新 for Business 管理包含驱动程序的更新时，启用此规则。 如果使用 Configuration Manager 管理软件更新，请将此规则设置为 "**关闭**"。

### <a name="windows-applications"></a>Windows 应用程序

桌面分析显示为 "*值得注意*" 的应用基于 "低安装计数" 阈值。 在部署计划的准备情况规则中设置此阈值。 默认情况下，此阈值为**2.0%**。 你可以将值从 `0.0` 更改为 `10.0`。


## <a name="next-steps"></a>后续步骤

转到下一篇文章，部署到试验设备。
> [!div class="nextstepaction"]  
> [部署到试点](/sccm/desktop-analytics/deploy-pilot)  
