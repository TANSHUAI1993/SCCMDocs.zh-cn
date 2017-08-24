---
title: "应用程序管理简介 | Microsoft Docs"
description: "发现管理和部署 System Center Configuration Manager 应用程序所需的基本信息。"
ms.custom: na
ms.date: 12/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
caps.latest.revision: "18"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 959a36413d06bb225f260bd44c1d3d59efd44e69
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-application-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的应用程序管理简介

*适用范围：System Center Configuration Manager (Current Branch)*

本主题中，将了解开始使用 System Center Configuration Manager 应用程序之前需要了解的基础知识。  

> [!TIP]  
>  如果已经熟悉如何在 Configuration Manager 中管理应用程序，可跳过本主题并移至创建示例应用程序。 请参阅[使用 System Center Configuration Manager 创建和部署应用程序](../../apps/get-started/create-and-deploy-an-application.md)。  

## <a name="what-is-an-application"></a>什么是应用程序?  
 尽管应用程序在计算和 Configuration Manager 中广泛使用，但它具有不同的含义。 将应用程序想象为一个框。 这个框包含一套或多套软件包的安装文件（称为**部署类型**），以及如何部署该软件的说明。  

 当应用程序部署到设备上时，“要求”  决定在设备上安装哪种部署类型。  

 可以通过应用程序执行更多操作。 阅读本指南即可了解这些内容。 下表介绍了在深入学习前需要了解的一些概念：  

|概念|描述|    
|-|-|  
|**惠?**|在之前版本的 Configuration Manager 中，经常要创建包含你想要向其部署应用程序的设备的集合。 尽管仍然可以创建集合，但使用要求可以为应用程序部署指定更多的详细条件。<br /><br /> 例如，可以指定应用程序仅在运行 Windows 10 的计算机上安装。 接下来，可以将应用程序部署到设备，但它只会在运行 Windows 10 的设备上安装。<br /><br /> Configuration Manager 会评估要求，确定是否安装应用程序及其任何部署类型。 然后，它会确定用于安装应用程序的正确部署类型。 默认情况下，根据“计划部署的重新评估” 客户端设置，每七天重新评估一次要求规则以确保符合性。<br /><br /> 有关详细信息，请参阅[创建和部署应用程序](../../apps/get-started/create-and-deploy-an-application.md)。|  
|**全局条件**|尽管要求用于单个应用程序中的特定部署类型，但也可创建全局条件。 这些条件是可用于任何应用程序和部署类型的预定义要求库。<br /><br /> Configuration Manager 包含一套内置全局条件，并且也可以创建自己的全局条件。<br /><br /> 有关详细信息，请参阅[创建全局条件](../../apps/deploy-use/create-global-conditions.md)。|  
|**模拟部署**|评估应用程序的要求、检测方法和依赖关系。 在未实际安装应用程序的情况下报告结果。<br /><br /> 有关详细信息，请参阅[模拟应用程序部署](../../apps/deploy-use/simulate-application-deployments.md)。|  
|**部署操作**|指定是否想要安装或卸载（如果支持）正在部署的应用程序。<br /><br /> 有关详细信息，请参阅[部署应用程序](../../apps/deploy-use/deploy-applications.md)。|  
|**部署目的**|指定部署应用程序为“必需” 还是“可用” 。<br /><br /> **必需**意味着依据设置的计划自动部署应用程序。 不过，用户可以跟踪应用程序部署状态（如果未隐藏），并且可使用软件中心在截止时间之前安装该应用程序。<br /><br /> “可用” 意味着如果将应用程序部署到用户，则用户将在软件中心看到发布的应用程序，并可根据需要进行请求。<br /><br /> 有关详细信息，请参阅[部署应用程序](../../apps/deploy-use/deploy-applications.md)。|  
|**修订版本**|修订应用程序或应用程序中包含的部署类型时，Configuration Manager 会创建应用程序的新版本。 可显示每个应用程序版本的历史记录、查看其属性、还原应用程序以前的版本或删除旧版本。<br /><br /> 有关详细信息，请参阅[更新和停用应用程序](../../apps/deploy-use/update-and-retire-applications.md)。|  
|**检测方法**|检测方法用于发现是否已安装部署的应用程序。 如果检测方法指示已安装应用程序，则 Configuration Manager 不会尝试重新安装。<br /><br /> 有关详细信息，请参阅[创建应用程序](../../apps/deploy-use/create-applications.md)。|  
|**依赖关系**|依赖关系定义在安装部署类型之前必须先安装的另一应用程序中的部署类型。 可以将相关部署类型设置为在安装部署类型之前自动安装。<br /><br /> 有关详细信息，请参阅[创建应用程序](../../apps/deploy-use/create-applications.md)。|  
|**取代**|Configuration Manager 允许使用取代关系来升级或替换现有应用程序。 取代应用程序时，可以指定新的部署类型来替换被取代应用程序的部署类型。 还可决定安装取代应用程序前，是否升级或卸载被取代应用程序。<br /><br /> 有关详细信息，请参阅[创建应用程序](../../apps/deploy-use/create-applications.md)。|  
|**以用户为中心的管理**|Configuration Manager 应用程序支持以用户为中心的管理，从而允许将特定用户与特定设备关联。 你可以将应用部署到用户和设备，而不必记住用户设备的名称。 此功能可帮助你确保在特定用户访问的每台设备上始终可以使用最重要的应用。 如果用户购买了新计算机，则在登录之前可在设备上自动安装用户的应用。<br /><br /> 有关详细信息，请参阅[将用户和设备与用户设备相关性相链接](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。|  

## <a name="what-application-types-can-you-deploy"></a>可以部署哪些应用程序类型?  
 可通过 Configuration Manager 部署以下应用类型：  

- Windows Installer（*.msi 文件）
- Windows 应用包（*.appx、*.appxbundle）
- Windows 应用包（在 Windows 应用商店中）
- Microsoft Application Virtualization 4
- Microsoft Application Virtualization  5
- Windows Mobile Cabinet
- macOS  


此外，通过 Microsoft Intune 或 Configuration Manager 本地设备管理来管理设备时，还可以管理以下应用类型：

- Windows Phone 应用包（*.xap 文件）
- iOS 应用包（*.ipa 文件）
- Android 应用包（*.apk 文件）
- “Google Play 上的 Android 应用包”
- Windows Phone 应用包（在 Windows Phone 应用商店中）
- 通过 MDM 的 Windows 安装程序
- Web 应用程序



## <a name="state-based-applications"></a>基于状态的应用程序  
 Configuration Manager 应用程序使用基于状态的监视，通过此功能可跟踪用户和设备的上一应用程序部署状态。 这些状态消息显示了有关单个设备的信息。 例如，将应用程序部署到用户集合，则可在 Configuration Manager 控制台中查看此部署的符合性状态和部署目的。 可以通过使用 Configuration Manager 控制台中的“监视”工作区来监视所有软件的部署。 软件部署包括软件更新、符合性设置、应用程序、任务序列以及包和程序。 有关详细信息，请参阅[监视应用程序](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  

 应用程序部署由 Configuration Manager 定期重新计算。 例如：  

-   最终用户卸载了部署的应用程序。 在下一个评估周期，Configuration Manager 将检测到应用程序不存在并重新安装它。  

-   应用程序由于未满足要求而未安装在设备上。 随后将对设备进行更改，现在它即满足要求。 Configuration Manager 检测到此更改并安装应用程序。  


 可以使用“计划部署的重新评估”客户端设置设置应用程序部署的重新评估时间间隔。 有关详细信息，请参阅[关于客户端设置](../../core/clients/deploy/about-client-settings.md)。  

## <a name="get-started-creating-an-application"></a>创建应用程序入门  
 如果要直接开始创建应用程序，会在[创建和部署应用程序](../../apps/get-started/create-and-deploy-an-application.md)主题中找到创建简单应用程序的演练。  

 若已熟悉基本知识，想查看所有可用选项有关的更多详细参考信息，可从[创建应用程序](/sccm/apps/deploy-use/create-applications)开始。  

## <a name="software-center-and-the-application-catalog"></a>软件中心和应用程序目录  
 在以前版本的 Configuration Manager 中，软件中心用于安装和计划软件安装、配置远程控制设置和设置电源管理。 用户可以连接到应用程序目录，以便浏览和请求软件、设置某些首选项，以及远程擦除其移动设备。  

 虽然这些设置在 System Center Configuration Manager 中仍然可用，但现已推出软件中心的新版本，让用户能够浏览应用程序。 无需使用应用程序目录，该目录要求已启用 Silverlight 的 Web 浏览器。 但是，仍然需要应用程序目录网站点站点系统角色和应用程序目录 Web 服务点站点系统角色来让用户可用的应用显示在软件中心。  

 有关详细信息，请参阅[规划和配置应用程序管理](../../apps/plan-design/plan-for-and-configure-application-management.md)。  

## <a name="configuration-manager-packages-and-programs"></a>Configuration Manager 包和程序  
 Configuration Manager 继续支持在产品的早期版本中使用的包和程序。 部署以下任何一项时，使用包和程序的部署可能比使用某个应用程序的部署更适用：  

-   不在计算机上安装应用程序的脚本，如用于对计算机磁盘驱动器进行碎片整理的脚本。  

-   不需要进行密切监视之下的"一次性"脚本。  

-   按定期计划运行且不能使用全局评估的脚本。

 有关详细信息，请参阅[包和程序](../../apps/deploy-use/packages-and-programs.md)。  
