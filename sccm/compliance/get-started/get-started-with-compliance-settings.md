---
title: "符合性设置入门 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中符合性设置的工作原理。 此外，还可以了解需要知道的核心概念。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f16c87dfd0c4f80d96aedf7f5f7497f2bbd4752a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的符合性设置入门

*适用范围：System Center Configuration Manager (Current Branch)*

在开始创建 System Center Configuration Manager 配置项目之前，应查看此主题以理解符合性设置的工作原理，并了解需要知道的核心概念。  

## <a name="how-compliance-settings-works"></a>符合性设置如何工作  
 通过符合性设置，可以管理组织中的服务器、笔记本电脑、台式计算机和移动设备的配置和符合性。  

 配置项目分为两个主要类别：  

-   **使用 Configuration Manager 客户端管理的设备的设置** - 通常是需要在这些设备上安装 Configuration Manager 客户端软件后才能管理的设备。  

-   **不使用 Configuration Manager 客户端管理的设备的设置** - 通常是可使用 Microsoft Intune 或 Configuration Manager 本地设备管理管理的设备。  

## <a name="what-devices-are-supported"></a>支持哪些移动设备？  


|设备类型|更多信息|  
|------------|----------------------|  
|Windows 电脑（使用 Configuration Manager 客户端）|允许创建自定义配置项目，这些项目可让你访问类似于注册表项、文件和 Active Directory 特性的项目。<br /><br /> 当使用 Windows 10 的配置项目类型时，将从预定义列表中选择所需的设置。|  
|Windows 电脑（已注册 Microsoft Intune）|从预定义列表中选择所需的设置。|  
|iOS 设备（已注册 Microsoft Intune）|从预定义列表中选择所需的设置。|  
|Android 设备（已注册 Microsoft Intune）|从预定义列表中选择所需的设置。|  
|Windows Phone 设备（已注册 Microsoft Intune）|从预定义列表中选择所需的设置。|  
|Mac 计算机（使用 Configuration Manager 客户端）|允许你创建自定义配置项目，这些项目可让你访问类似 Mac OS X 首选项（属性列表）值和脚本返回的结果等项目。|  
|Mac 计算机（已注册 Microsoft Intune）|从预定义列表中选择所需的设置。|  

## <a name="what-is-a-configuration-item"></a>什么是配置项目？  
 可以将配置项目看作一个容器，它存储以下信息（你配置的信息取决于配置项目类型：  

-   “检测方法信息” （适用于仅包含应用程序设置 Windows 的配置项目）- 可让你通过检测此应用程序的 Windows installer 文件或使用自定义脚本来检测应用程序是否安装。  

-   “设置” -  represent the business or technical conditions that are used to assess compliance on client devices. 你可以配置新设置，或浏览到引用计算机上的现有设置。  

-   “符合性规则” -  specify the conditions that define the compliance of a configuration item setting. 设置必须具有至少一个符合性规则，才能对它评估符合性。 某些设置可以让你修正发现不符合的值。 可以创建新规则，或浏览到任何配置项目中的现有设置以在其中选择规则。  

-   “受支持的平台” - 这些是你定义的设备平台，在这些平台上将对配置项目进行符合性评估。 如果将配置项目部署到不在受支持的平台列表上的设备，则无法对其进行符合性评估。  

## <a name="what-is-a-configuration-baseline"></a>什么是配置基线？  
 通过定义配置基线来进行符合性评估，配置基线包含要评估的配置项目和描述你必须具有的符合性级别的设置和规则。 作为由 Microsoft 和其他供应商在 Configuration Manager 中定义的最佳做法，可以从 Microsoft System Center Configuration Manager 配置包的 Web 中导入此配置数据，然后导入到 Configuration Manager 中。 或者，你可以创建新的配置项目或配置基线。  

 定义配置基线后，可以通过集合将它分配给用户和设备并按计划评估其设置的符合性。 可将多个配置基线分配给设备。 这样可为你提供高级版的控制。  

 客户端设备根据部署的每个配置基线评估其符合性，并使用状况消息和状态消息立即向站点报告结果。 如果客户端当前未连接到网络，但已下载在部署的配置基线中引用的配置项目，则将评估配置基线的符合性信息。 将在重新连接时发送符合性信息。  

 可从 Configuration Manager 控制台中的“监视”工作区中的“部署”节点监视配置基线评估符合性的结果，以查看出现不符合性和错误最常见的原因以及受影响的用户和设备数量。 你也可以运行符合性设置报告来查找其他详细信息，例如哪些设备符合，哪些不符合，以及哪些配置基线的元素导致计算机出现不符合的情况。 还可以通过“控制面板”中的“Configuration Manager”中的“配置”选项卡，从运行 Configuration Manager 客户端软件的 Windows 计算机中查看符合性评估结果。  

## <a name="user-data-and-profiles-configuration-items"></a>用户数据和配置文件的配置项目  
 用户数据和配置文件配置项目包含控制层次机构中的用户如何在运行 Windows 8 和更高版本的计算机上管理文件夹重定向、脱机文件和漫游配置文件的设置。 可以将这些设置部署到用户的集合，然后从 Configuration Manager 控制台的“监视”节点中监视其符合性。 与其他配置项目不同，你在部署它们之前没有将其添加到配置基线。 你可在“部署用户数据和配置文件的配置项目”  对话框中直接部署它们。  

 有关详细信息，请参阅[创建用户数据和配置文件配置项目](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)。  

## <a name="remote-connection-profiles"></a>远程连接配置文件  
 远程连接配置文件提供了一组工具和资源，帮助你为组织中的设备创建、部署和监视远程连接设置。 通过部署这些设置，你可以最大程度地减少最终用户连接到公司网络上他们的计算机所需的工作。  

有关详细信息，请参阅[创建远程连接配置文件](/sccm/compliance/deploy-use/create-remote-connection-profiles)。  

## <a name="windows-edition-upgrade"></a>Windows 版本升级
凭借版本升级策略，可通过提供新的产品密钥或许可证文件将运行某些版本的 Windows 10 的设备自动升级到较新的版本。

有关详细信息，请参阅[使用版本升级策略升级 Windows 设备](/sccm/compliance/deploy-use/upgrade-windows-version)
