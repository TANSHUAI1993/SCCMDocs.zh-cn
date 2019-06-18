---
title: 如何创建部署计划
titleSuffix: Configuration Manager
description: 用于在桌面 Analytics 中创建部署计划的操作方法指南。
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 696d2ecedc659330715d42c05ecc046f0a6cc7ff
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159175"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>如何在桌面 Analytics 中创建部署计划

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

本文提供用于在桌面 Analytics 中创建部署计划的步骤。 在开始之前，请首先[了解有关部署计划](/sccm/desktop-analytics/about-deployment-plans)。

## <a name="create-a-plan-for-windows-10"></a>适用于 Windows 10 创建计划

按照本部分使用 Desktop 分析来创建用于部署 Windows 10 计划中的步骤。

1. 打开[Desktop 分析门户](https://aka.ms/desktopanalytics)。 使用凭据至少具有**工作区参与者**权限。  

2. 选择**部署计划**管理组中。  

3. 在中**部署计划**窗格中，选择**创建**。  

4. 在中**创建部署计划**窗格中，配置以下设置：  

    - **名称**：部署计划的唯一名称  

    - **产品和版本**:选择要部署的 Windows 10 版本。 Microsoft 建议创建使用最新版本的部署计划。  

    - **设备组**:选择一个或多个组，然后选择**设置为目标组**。 与分组**SCCM**作为源是集合从 Configuration Manager 同步。  

    - **准备情况规则**:这些规则帮助确定哪些设备有资格获得升级。 有关详细信息，请参阅[准备情况规则](#readiness-rules)。  

    - **完成日期**:选择依据 Windows 应完全部署到所有目标设备的日期。  

5. 选择“创建”  。 其正在处理时，在部署计划列表中显示新的计划。 若要加快处理，请求按需数据刷新。 有关详细信息，请参阅[Desktop 分析常见问题](/sccm/desktop-analytics/faq##can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。  

6. 选择其名称以打开部署计划。  

7. 在部署计划菜单上，在**准备**组中，选择**识别重要性**。  

    1. 上**应用程序**选项卡上，选择此选项可以仅显示**未检查**资产。  

    2. 选择每个应用，并选择**编辑**。 您可以选择多个应用在同一时间编辑。  

    3. 选择重要性级别从**重要性**列表。 如果您希望桌面分析在试运行过程中验证应用程序，选择**严重**或**重要**。 它不会验证应用程序标记为**不重要**。 评估其[兼容性](/sccm/desktop-analytics/compat-assessment)和其他计划见解分配重要性级别时。  

        如果将分配重要性级别，您还可以选择升级决策。  

    4. 选择**保存**时完成。  

8. 在部署计划菜单上，在**准备**组中，选择**标识试点**。  

    1. 为试点查看建议的设备。  

    2. 选择每个设备，然后选择**将添加到试验**。 如果您不同意建议，请选择**替换为**。  

        对于桌面分析如何使这些建议的详细信息中的右上角选择信息图标**标识试点**窗格。

## <a name="readiness-rules"></a>准备情况规则

这些规则帮助您确定哪些设备有资格获得的就地升级。 在创建部署计划或更高版本对其进行编辑时，可以设置这些规则。

若要更改的准备情况规则：

1. 在 Desktop 分析门户中，选择部署计划。
1. 名称旁边，选择**编辑**。
1. 选择**准备情况规则**。
1. 选择**Windows OS**。
1. 必要时，进行更改，然后选择**保存**。

有关**Windows OS**升级，有两个规则：设备驱动程序和 Windows 应用程序。

### <a name="device-drivers"></a>设备驱动程序

配置是否将设备从 Windows Update 中获取驱动程序。 此值是**关闭**默认情况下。 使用适用于企业的 Windows 更新来管理更新包括驱动程序时，请启用此规则。 如果正在使用 Configuration Manager 来管理软件更新，将此规则设置为**关闭**。

### <a name="windows-applications"></a>Windows 应用程序

显示为桌面分析的应用*值得注意*基于低安装计数阈值。 在部署计划的准备情况规则中设置此阈值。 默认情况下，此阈值是**2.0%** 。 你可以将值从`0.0`到`10.0`。


## <a name="next-steps"></a>后续步骤

转到下一步的文章，将部署到试运行的设备。
> [!div class="nextstepaction"]  
> [将部署到试运行](/sccm/desktop-analytics/deploy-pilot)  
