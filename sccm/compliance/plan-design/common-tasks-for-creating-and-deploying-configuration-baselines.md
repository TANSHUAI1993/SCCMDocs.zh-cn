---
title: "配置基线的常见任务 - Configuration Manager | Microsoft Docs"
description: "了解如何创建和部署 System Center Configuration Manager 配置基线。"
ms.custom: na
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 5bf4457af6bedf7bc9cd73c879f1857209c0725d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager"></a>System Center Configuration Manager 用于创建和部署配置基线的常见任务

*适用范围：System Center Configuration Manager (Current Branch)*

本主题包含帮助了解有关如何创建和部署 System Center Configuration Manager 配置基线的常用方案。  

 如果已熟悉符合性设置，可以在[创建配置基线](../../compliance/deploy-use/create-configuration-baselines.md)和[部署配置基线](../../compliance/deploy-use/deploy-configuration-baselines.md)主题中找到有关你使用的所有功能的详细文档。  

 在开始之前，请阅读 [System Center Configuration Manager 中的符合性设置入门](../../compliance/get-started/get-started-with-compliance-settings.md)以了解有关符合性设置的一些基础知识，另请阅读[规划和配置符合性设置](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)来实施任何必要的先决条件。  

## <a name="create-a-configuration-baseline"></a>创建配置基线  
 在本例中，已创建了仅针对运行 Configuration Manager 客户端的 Windows 10 电脑的配置项目。  

 此配置项目强制要求在 Windows 10 电脑上输入至少 6 位字符的密码。 配置项目名为“Windows 10 密码实施” 。  

使用下面的过程了解如何将此配置项目添加到配置基线以准备部署。  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “配置基线”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建配置基线” 。  

4.  在“创建配置基线”  对话框中，配置以下设置：  

    -   **名称** – 输入 **Windows 10 密码** （或你选择的另一名称）  

5.  单击“添加”  > 。  

6.  在“添加配置项目”  对话框中，选择之前创建的“Windows 10 密码实施”  配置项目，然后单击“添加” 。  

7.  单击“确定”以关闭“添加配置项目”  对话框并返回到“创建配置基线”  对话框。

8.  单击“确定”  以关闭“创建配置基线”  对话框。  

 现在，可以看到在 Configuration Manager 控制台的“配置基线”节点中创建的配置基线。  

## <a name="deploy-the-configuration-baseline"></a>部署配置基线  
 在本例中，会将前一过程中创建的配置基线部署到计算机集合中。  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “配置基线”。  

3.  从配置基线列表中选择“Windows 10 密码” 。  

4.  在“主页”  选项卡上的“部署”  组中，单击“部署” 。  

5.  在“部署配置基线”  对话框中，配置以下设置：  

    -   **所选配置基线** – 确保“Windows 10 密码”  配置基线已自动添加到此列表中。  

    -   **修正非符合性规则(如果支持)** - 勾选此框，以确保如果目标设备上没有正确的设置，则通过 Configuration Manager 进行修正。  

    -   **集合** – 单击“浏览”  以选择在其上评估配置基线并针对符合性进行修正的计算机集合。 在本例中，已将配置基线部署到内置“所有台式计算机和服务器客户端”  集合。  

        > [!TIP]  
        >  不要担心选择的集合是否包含不运行 Windows 10 的计算机或设备。 只要在创建的配置项目中配置支持的平台，则只针对 Windows 10 电脑评估符合性。  

    -   如有必要，配置用于评估配置基线的计划。 否则，请保留默认值“7 天” 。  

7.  单击“确定”  以关闭“部署配置基线”  对话框并创建部署。  

 如果想要快速了解此部署的合规性统计信息，请在“监视”  工作区中，单击“部署” 。 在屏幕底部，可看到“符合性统计信息”图表。  

## <a name="next-steps"></a>后续步骤 

有关如何监视配置基线的详细信息，请参阅[监视符合性设置](../../compliance/deploy-use/monitor-compliance-settings.md)。  
