---
title: 应用管理简介
titleSuffix: Configuration Manager
description: 了解管理和部署 Configuration Manager 中的应用程序所需的基本信息。
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0d4e83cbcb1c95303719b1d86ffc9a8969c16998
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893900"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Configuration Manager 中的应用程序管理简介

*适用范围：System Center Configuration Manager (Current Branch)*

本文介绍开始使用 Configuration Manager 应用程序之前要了解的基础知识。  

> [!TIP]  
>  如果已熟悉如何在 Configuration Manager 中管理应用程序，请跳过本文。 跳转到创建示例应用程序：[创建和部署应用程序](/sccm/apps/get-started/create-and-deploy-an-application)。  



## <a name="what-is-an-application"></a>什么是应用程序?  

尽管“应用程序”是在计算和 Configuration Manager 中广泛使用的一个术语，但它具备特定的含义。 将应用程序想象为一个框。 这个框包含一套或多套软件包的安装文件（称为*部署类型*），以及如何部署该软件的说明。  

在将应用程序部署到设备时，“要求”决定 Configuration Manager 会在设备上安装哪种部署类型。  

可以通过应用程序执行更多操作。 阅读本指南即可了解这些内容。 以下部分介绍在深入学习前需要了解的一些概念：  

#### <a name="deployment-type"></a>部署类型
如果说“应用程序”是一个框，则“部署类型”就是框中这套内容。 应用程序至少需要一个部署类型，因为类型决定了该应用的安装方式。 请使用多个部署类型来配置同一个应用程序的不同内容和安装程序。 

例如，假设公司有一个名为 Astoria 的业务线应用程序。 应用程序的开发者提供了以下应用安装方式：
- 用于在 Windows 10 设备上获取完整功能的 Windows Installer 包
- 用于终端服务器场的 App-V 包
- 针对移动用户的 Android 应用包  

在 Configuration Manager 中为 Astoria 创建一个应用。 应用程序定义与应用相关的高级元数据，这是所有安装方法和平台所通用的。 然后，为可用的安装方法创建三种部署类型，并将应用程序部署到所有用户。 Configuration Manager 根据部署类型的要求和其他配置，确定每个用例中的适当方法。 

有关详细信息，请参阅[为应用程序创建部署类型](/sccm/apps/deploy-use/create-applications#bkmk_create-dt)。

#### <a name="requirements"></a>要求
在先前版本的 Configuration Manager 中，你创建了要将应用程序部署到的设备的集合。 尽管仍可创建集合，但请使用“要求”为应用程序部署指定更详细的条件。

例如，指定只能在运行 Windows 10 的设备上安装应用程序。 在将应用程序部署到所有设备时，它只在运行 Windows 10 的设备上安装。

Configuration Manager 会评估要求，从而确定是否安装应用程序及其任何部署类型。 然后，它会确定用于安装应用程序的正确部署类型。 默认情况下，Configuration Manager 客户端根据“计划部署的重新评估”客户端设置每 7 天重新评估一次要求规则以确定符合性。

有关详细信息，请参阅[创建和部署应用程序](/sccm/apps/get-started/create-and-deploy-an-application)以及[部署类型要求](/sccm/apps/deploy-use/create-applications#bkmk_dt-require)。

#### <a name="global-conditions"></a>全局条件
尽管对单个应用程序中的特定部署类型使用要求，但也可创建全局条件。 这些条件是可用于任何应用程序和部署类型的预定义要求库。 Configuration Manager 包含一套内置全局条件，你也可自行创建全局条件。 

有关详细信息，请参阅[创建全局条件](/sccm/apps/deploy-use/create-global-conditions)。

#### <a name="simulated-deployment"></a>模拟部署
模拟部署对应用程序的要求、检测方法和依赖关系进行评估。 客户端在未实际安装应用程序的情况下报告结果。 

有关详细信息，请参阅[模拟应用程序部署](/sccm/apps/deploy-use/simulate-application-deployments)。  

#### <a name="deployment-action"></a>部署操作
部署操作指定是要安装还是要卸载正在部署的应用程序。 并非所有部署类型都支持卸载操作。 

有关详细信息，请参阅[部署应用程序](/sccm/apps/deploy-use/deploy-applications)。  

#### <a name="deployment-purpose"></a>部署目的
部署目的指定部署应用为“必需”还是“可用”：  

- 客户端根据所设置的计划自动安装“必需”部署。 如果应用程序未隐藏，则用户可跟踪其部署状态。 在截止时间之前，用户还可通过软件中心安装应用程序。  

- 如果将应用程序作为“可用”应用部署给用户，则用户能在软件中心查看到该应用，并可根据需要进行请求。  

有关详细信息，请参阅[部署应用程序](/sccm/apps/deploy-use/deploy-applications)。  

#### <a name="revisions"></a>修订版本
在修订应用程序或部署类型时，Configuration Manager 会创建应用程序的新版本。 在 Configuration Manager 控制台中执行以下操作： 
- 显示每个应用程序修订版的历史记录
- 查看其属性
- 还原应用程序的上一版本
- 删除旧版本

有关详细信息，请参阅[更新和停用应用程序](/sccm/apps/deploy-use/update-and-retire-applications)。  

#### <a name="detection-method"></a>检测方法
使用检测方法发现设备是否已安装应用程序。 如果检测方法指示已安装应用程序，则 Configuration Manager 不会尝试再次安装。

有关详细信息，请参阅[部署类型检测方法选项](/sccm/apps/deploy-use/create-applications##bkmk_dt-detect)。

#### <a name="dependencies"></a>依赖关系
依赖关系定义客户端在安装部署类型之前必须安装的另一应用程序中的一个或多个部署类型。 

有关详细信息，请参阅[部署类型依赖关系](/sccm/apps/deploy-use/create-applications#bkmk_dt-depend)。  

#### <a name="supersedence"></a>取代
Configuration Manager 允许使用取代关系来升级或替换现有应用程序。 取代应用程序时，请指定新的部署类型来替换被取代的应用程序的部署类型。 还可决定在客户端安装取代应用程序前是要升级还是要卸载被取代的应用程序。

有关详细信息，请参阅[应用程序取代](/sccm/apps/deploy-use/revise-and-supersede-applications#application-supersedence)。  

#### <a name="user-centric-management"></a>以用户为中心的管理
Configuration Manager 应用程序支持以用户为中心的管理，它可将特定用户关联到特定设备。 不用记住用户设备的名称，即可将应用部署到用户和设备。 此功能有助于确保始终能在每台用户设备上使用最重要的应用。 如果用户购买了新的计算机，则在登录之前，Configuration Manager 会自动在设备上安装其应用。 

有关详细信息，请参阅[将用户和设备与用户设备相关性进行链接](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)。  



## <a name="what-application-types-can-you-deploy"></a>可以部署哪些应用程序类型?  

可通过 Configuration Manager 部署以下应用类型：  

- Windows Installer (msi)  

- Windows 应用包（appx 或 appxbundle）  

    > [!Note]  
    > 自版本 1806 其，此类型包括新的 Windows 10 应用包 (msix) 和应用程序包 (msixbundle) 格式。<!--1357427-->  

- Microsoft Store 中的 Window 应用包  

- Microsoft App-V v4 和 v5  

- macOS  


此外，通过 Microsoft Intune 或 Configuration Manager 本地设备管理来管理设备时，一并管理以下应用类型：  

- Windows Phone 应用包 (xap)  

- Microsoft Store 中的 Windows Phone 应用包  

- iOS 应用包 (ipa)  

- “应用商店中的 iOS 应用包”  

- Android 应用包 (apk)  

- Google Play 上的 Android 应用包  

- 通过 MDM 的 Windows Installer (msi)  

- Web 应用程序



## <a name="state-based-applications"></a>基于状态的应用程序  

Configuration Manager 应用程序使用基于状态的监视。 可跟踪用户和设备的最新应用程序部署状态。 这些状态消息显示了有关单个设备的信息。 例如，如果将应用程序部署到用户集合，则可在 Configuration Manager 控制台中查看此部署的符合性状态和部署目的。 在 Configuration Manager 控制台的“监视”工作区中监视所有软件的部署。 有关详细信息，请参阅[监视应用程序](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  

Configuration Manager 客户端定期对应用程序部署进行重新评估。 例如：  

- 用户卸载已部署的应用程序。 在下一个评估周期，Configuration Manager 会检测到该应用不存在。 然后，客户端会自动重新安装该应用。  

- Configuration Manager 不会在设备上安装应用程序，因为它不满足要求。 随后将对设备进行更改，现在它即满足要求。 Configuration Manager 检测到此更改，且客户端会安装该应用程序。  

可设置应用程序部署的重新评估间隔时间。 使用“软件部署”组中的“计划部署的重新评估”客户端设置。 有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#software-deployment)。  



## <a name="get-started-creating-an-application"></a>创建应用程序入门  

如果要直接开始创建应用程序，可在[创建和部署应用程序](/sccm/apps/get-started/create-and-deploy-an-application)一文中找到相关演练。  

如果已熟悉基本知识并且想查看关于所有可用选项的更详细的参考信息，请从[创建应用程序](/sccm/apps/deploy-use/create-applications)开始。  



## <a name="software-center"></a>软件中心  

软件中心是一款使用 Configuration Manager 客户端安装的 Windows 应用程序。 软件中心可用于执行以下操作：  
- 浏览并请求部署到设备或用户的应用程序
- 安装并计划软件安装
- 查看应用程序、软件更新和操作系统的安装状态
- 配置远程控制设置
- 设置电源管理

有关详细信息，请参阅下列文章：  
- [规划和配置应用程序管理](/sccm/apps/plan-design/plan-for-and-configure-application-management)
- [软件中心用户指导](/sccm/core/understand/software-center)

> [!Note]  
> 1806 中不再需要应用程序目录站点和 Web 服务点角色，但该角色依然受支持。 
> 
> 应用程序目录网站点的 Silverlight 用户体验不再受支持。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。  



## <a name="packages-and-programs"></a>包和程序  

Configuration Manager 继续支持在产品的早期版本中使用的包和程序。 

有关详细信息，请参阅[包和程序](/sccm/apps/deploy-use/packages-and-programs)。  



## <a name="next-steps"></a>后续步骤

现在你已了解 Configuration Manager 中的应用程序管理的基本概念，请继续阅读以下文章：
- [创建和部署示例应用程序](/sccm/apps/get-started/create-and-deploy-an-application)
- [规划和配置应用程序管理](/sccm/apps/plan-design/plan-for-and-configure-application-management)
- [创建应用程序](/sccm/apps/deploy-use/create-applications)
