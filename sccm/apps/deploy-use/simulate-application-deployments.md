---
title: "模拟应用程序部署 | Microsoft Docs"
description: "评估部署类型的检测方法、要求和依赖关系，而无需安装该应用程序。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b06539ded21eac71dda7da89dae96fda7a801260
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 模拟应用程序部署

*适用范围：System Center Configuration Manager (Current Branch)*

如果想在不安装或卸载应用程序的前提下测试应用程序部署，可以使用模拟部署。 模拟部署评估部署类型的检测方法、要求和依赖关系。 它在“监视”工作区的“部署”节点中报告结果。 请使用本主题中的过程模拟 System Center Configuration Manager (Configuration Manager) 中的应用程序部署。  

> [!NOTE]  
> 不能将模拟部署用于移动设备的集合。  
>   
> 如果某个应用程序的模拟部署处于活动状态，则不能出于“卸载”  这个部署目的而部署此应用程序。  

## <a name="configure-a-simulated-application-deployment"></a>配置模拟应用程序部署

1.  在 Configuration Manager 控制台中，选择以下其一：  
    -   用户集合。  
    -   设备集合。  
    -   Configuration Manager 应用程序。  

2.  在“主页”选项卡的“部署”组中，选择“模拟部署”。  

3.  在“模拟应用程序部署向导”中，为模拟部署设置以下详细内容：  

    -   **应用程序**。 选择“浏览”，然后选择要为其创建模拟部署的应用程序。  

    -   **集合**。 选择“浏览”，然后选择要用于模拟部署的集合。  

    -   **操作**。 在下拉列表中，选择是想模拟所选应用程序的安装还是模拟其卸载。  

    -   **使用或不使用用户登录信息自动部署**。 如果选中此选项，则客户端将评估模拟部署，而不管用户是否登录客户端。  

4.  单击“下一步”，查看“摘要”页上的信息，然后完成向导以创建模拟应用程序部署。  

5.  模拟的应用程序将出现在“监视”工作区的“部署”节点中，其用途为“模拟”。 有关如何监视应用程序部署的详细信息，请参阅[从 System Center Configuration Manager 控制台监视应用程序](../../apps/deploy-use/monitor-applications-from-the-console.md)。  
