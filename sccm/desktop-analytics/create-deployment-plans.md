---
title: 如何创建部署计划
titleSuffix: Configuration Manager
description: 用于在桌面 Analytics 中创建部署计划的操作方法指南。
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4b56fac3060acc16fe46221464ddc6535b478399
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754671"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>如何在桌面 Analytics 中创建部署计划 

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

本文提供用于在桌面 Analytics 中创建部署计划的步骤。 在开始之前，请首先[了解有关部署计划](/sccm/desktop-analytics/about-deployment-plans)。

按照此项目以使用 Desktop 分析以创建用于部署 Windows 10 和 Office 365 专业增强版计划中的步骤。 Windows 10、 Office 365 ProPlus，和 / 或创建部署计划。

1. 打开[Desktop 分析门户](https://aka.ms/m365aprod)。 使用凭据至少具有**工作区参与者**权限。  

2. 选择**部署计划**管理组中。  

3. 在中**部署计划**窗格中，选择**创建**。  

4. 在中**创建部署计划**窗格中，配置以下设置：  

    - **名称**：部署计划的唯一名称  

    - **产品和版本**:选择的产品和版本来部署。 Microsoft 建议在一起，创建适用于 Office 和 Windows 的部署计划并使用最新版本。  

    - **设备组**:选择一个或多个组，然后选择**设置为目标组**。 与分组**SCCM**作为源是集合从 Configuration Manager 同步。  

    - **准备情况规则**:这些规则帮助确定哪些设备有资格获得升级。 

    - **完成日期**:选择按其 Windows 和 Office 应完全部署到所有目标设备的日期。  

5. 选择“创建”。 其正在处理时，在部署计划列表中显示新的计划。 处理可以需要长达 48 小时，然后才能继续执行下一步。   

6. 选择其名称以打开部署计划。  

7. 在部署计划菜单上，在**准备**组中，选择**识别重要性**。  

    1. 上**应用程序**选项卡上，选择此选项可以仅显示**未检查**资产。  

    2. 选择每个应用，并选择**编辑**。 您可以选择多个应用在同一时间编辑。   

    3. 选择重要性级别从**重要性**列表。 如果您希望桌面分析在试运行过程中验证外接程序，选择**严重**或**重要**。 它不会验证加载项标记为**不重要**。 分配重要性级别时，请考虑兼容性风险和其他计划见解。  

        如果将分配重要性级别，您还可以选择升级决策。  

    4. 选择**保存**时完成。  

    5. 重复这些步骤**Office 加载项**。  

8. 在部署计划菜单上，在**准备**组中，选择**标识试点**。  

    1. 为试点查看建议的设备。  

    2. 选择每个设备，然后选择**将添加到试验**。 如果您不同意建议，请选择**替换为**。  

        对于桌面分析如何使这些建议的详细信息中的右上角选择信息图标**标识试点**窗格。



### <a name="next-steps"></a>后续步骤

转到下一步的文章，将部署到试运行的设备。
> [!div class="nextstepaction"]  
> [将部署到试运行](/sccm/desktop-analytics/deploy-pilot)  
