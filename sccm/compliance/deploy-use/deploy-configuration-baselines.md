---
title: "部署配置基线 | Microsoft Docs"
description: "部署配置基线以定义配置基线部署以及对部署添加或删除配置基线。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9c9e6b7780c7c10c20a60dbbbf506e916031eb88
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-configuration-baselines-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中部署配置基线

*适用范围：System Center Configuration Manager (Current Branch)*

必须首先将 System Center Configuration Manager 中的配置基线部署到一个或多个用户或设备集合，这些集合中的客户端设备才可以评估与配置基线的符合性。  

使用“部署配置基线”  对话框来定义配置基线部署，其中包括将配置基线添加到部署或从部署中删除配置基线以及指定评估计划。  

## <a name="deploy-a-configuration-baseline"></a>部署配置基线  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “配置基线”。  

3.  在“配置基线”  列表中，选择要部署的配置基线，然后，在“主页”  选项卡上的“部署”  组中单击“部署” 。  

4.  在“部署配置基线”  对话框中，在“可用配置基线”  列表中选择你想要部署的配置基线。 单击“添加”  以将它们添加到“所选配置基线”  列表。  

    > [!IMPORTANT]  
    >  如果更改已添加到部署的配置基线的配置项目，则将配置基线的下一次计划评估时间才会对修改后的配置项目进行符合性评估。  

5.  指定以下附加信息：  

    -   **在支持时修正非符合性规则** – 自动修正 Windows Management Instrumentation (WMI)、注册表、脚本和 Configuration Manager 所注册移动设备的所有设置的任何非符合性规则。  

    -   **允许维护时段外的修正** - 如果已为你向其部署配置基线的集合配置了维护时段，请启用此选项以让符合性设置在维护时段外修正值。 有关维护时段的详细信息，请参阅[如何使用维护时段](/sccm/core/clients/manage/collections/use-maintenance-windows)。  

6.  **生成警报** – 配置一个警报，如果在指定日期和时间之前配置基线符合性小于指定百分比，则生成该警报。 你也可以指定是否希望将警报发送到 System Center Operations Manager。  

7.  **集合** - 单击“浏览”  以选择要在其中部署配置基线的集合。  

8.  **指定此配置基线的符合性评估计划** - 指定在客户端计算机上对部署的配置基线进行评估所依据的计划。 这可以是简单计划或自定义计划。  

    > [!NOTE]  
    >  如果将配置基线部署到计算机，则将在你计划的开始时间后两小时内对其进行符合性评估。 如果将配置基线部署到用户，则将在用户登录后对其进行符合性评估。  

9. 单击“确定”  关闭“部署配置基线”  对话框并创建部署。 有关如何监视部署的详细信息，请参阅[监视符合性设置](/sccm/compliance/deploy-use/monitor-compliance-settings)。  
