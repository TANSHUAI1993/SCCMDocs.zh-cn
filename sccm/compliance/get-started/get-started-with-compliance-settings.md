---
title: 符合性设置入门
titleSuffix: Configuration Manager
description: 了解核心概念以及符合性设置如何工作
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: 11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a8f672d4d92db8f1bd6e19c4a483b5b3107ad703
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的符合性设置入门

*适用范围：System Center Configuration Manager (Current Branch)*

在创建 Configuration Manager 符合性设置之前，首先了解核心概念，并了解它们如何工作。  



## <a name="how-compliance-settings-work"></a>符合性设置如何工作  
 通过符合性设置，可以管理组织中客户端的配置和符合性。  

 配置项目分为两个主要类别：  

-   **使用 Configuration Manager 客户端管理的设备的设置** - 通常是需要在这些设备上安装 Configuration Manager 客户端软件后才能管理的设备。  

-   **不使用 Configuration Manager 客户端管理的设备的设置** - 通常是可使用 Microsoft Intune 或 Configuration Manager 本地设备管理管理的设备。  



## <a name="what-devices-are-supported"></a>支持哪些移动设备？  

| 设备类型 | 更多信息 |  
|------------|----------------------|  
| Windows 电脑（使用 Configuration Manager 客户端） | 创建自定义配置项目以评估类似于注册表项、文件和 Active Directory 属性的对象。<br /><br /> 当使用 Windows 10 的配置项目类型时，从预定义列表中选择设置。 |  
| Windows 电脑（已注册 Microsoft Intune） | 从预定义列表中选择设置。 |  
| iOS 设备（已注册 Microsoft Intune） | 从预定义列表中选择设置。 |  
| Android 设备（已注册 Microsoft Intune） | 从预定义列表中选择设置。 |  
| Windows Phone 设备（已注册 Microsoft Intune） | 从预定义列表中选择设置。 |  
| Mac 计算机（使用 Configuration Manager 客户端） | 创建自定义配置项目以评估对象（如 macOS 首选项）和脚本返回的结果。 |  
| Mac 计算机（已注册 Microsoft Intune） | 从预定义列表中选择设置。 |  



## <a name="what-is-a-configuration-item"></a>什么是配置项目？  
 配置项目是存储特定信息的容器。 配置的信息取决于配置项目类型。 配置项目可以包含以下信息：

-   检测方法信息仅适用于包含应用程序设置的 Windows 配置项目。 它检测是否安装了应用程序。 此检测使用应用程序的 Windows Installer 文件，或者使用自定义脚本。  

-   设置表示用于评估客户端设备上的符合性的业务或技术条件。 配置新设置，或浏览到引用计算机上的现有设置。  

-   符合性规则指定定义配置项目设置的符合性的条件。 客户端评估符合性设置之前，它必须具有至少一个符合性规则。 某些设置修正不符合要求的值。 创建新规则，或浏览到任何配置项目中的现有设置并在其中选择规则。  

-   受支持的平台是定义的设备平台，客户端在这些平台上评估配置项目的遵从性。 如果将配置项目部署到不在受支持的平台列表上的设备，则不评估符合性。  



## <a name="what-is-a-configuration-baseline"></a>什么是配置基线？  
 定义包含要评估的配置项目的配置基线。 还包括描述所需符合性级别的设置和规则。 从 Configuration Manager 配置包导入此配置数据。 Microsoft 和其他供应商定义这些配置包。 或者可以创建新的配置项目或配置基线。  

 定义配置基线后，请将其部署到用户和设备集合。 然后客户端根据计划评估基线设置的符合性。 可以将多个配置基线部署到设备。 此粒度能够更好地控制符合性。 

 客户端设备根据部署的每个配置基线评估其符合性，并使用状况消息和状态消息立即向站点报告结果。 如果设备当前与网络断开连接，但下载了配置基线，则仍然会评估配置项目的符合性。 当它重新连接时会发送符合性信息。  

### <a name="monitoring-configuration-baselines"></a>监视配置基线
- 在“部署”节点中的“监视”工作区下监视 Configuration Manager 控制台中的符合性评估结果。 例如：
    - 不符合的常见原因
    - 错误
    - 受影响的用户和设备数
- 使用其他详细信息运行符合性设置报表。 例如：
    - 哪些设备是符合还是不符合
    - 配置基线的哪个元素造成计算机不符合
- 从运行 Configuration Manager 客户端的 Windows 计算机查看符合性评估结果。 打开“Configuration Manager”控制面板，并切换到“配置”选项卡。  



## <a name="user-data-and-profiles-configuration-items"></a>用户数据和配置文件的配置项目  
 用户数据和配置文件配置项目包括控制运行 Windows 8 和更高版本的计算机上的用户如何管理的设置：  
   - 文件夹重定向
   - 脱机文件
   - 漫游配置文件  

将这些配置项目部署到用户集合。 从 Configuration Manager 控制台的“监视”节点中监视其符合性。 与其他配置项目不同，你在部署它们之前没有将它们添加到配置基线。 单击功能区中的“部署”直接部署。  

 有关详细信息，请参阅[创建用户数据和配置文件配置项目](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)。  



## <a name="remote-connection-profiles"></a>远程连接配置文件  
 远程连接配置文件提供了一组工具和资源，有助于创建、部署和监视远程连接设置。 通过将这些设置部署到设备，可以最大程度地减少最终用户将其计算机连接到公司网络所需的工作量。  

有关详细信息，请参阅[创建远程连接配置文件](/sccm/compliance/deploy-use/create-remote-connection-profiles)。  



## <a name="windows-edition-upgrade"></a>Windows 版本升级
凭借版本升级策略，可将运行某些版本的 Windows 10 的设备自动升级到较新的版本。 此策略提供设备用于升级的新产品密钥或许可证文件。

有关详细信息，请参阅[使用版本升级策略升级 Windows 设备](/sccm/compliance/deploy-use/upgrade-windows-version)



## <a name="microsoft-edge-browser-profiles"></a>Microsoft Edge 浏览器配置文件
<!-- 1357310 -->
从版本 1802 开始，在 Windows 10 客户端上使用 [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) Web 浏览器的客户，可创建符合性设置策略以配置多个 Microsoft Edge 设置。 

有关详细信息，请参阅 [Microsoft Edge 浏览器配置文件](/sccm/compliance/deploy-use/browser-profiles)。

