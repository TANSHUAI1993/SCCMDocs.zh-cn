---
title: 创建 iOS 应用程序
titleSuffix: Configuration Manager
description: 如何在 Configuration Manager 中针对 iOS 设备创建和部署应用程序。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 246ca26b8fab3a1006e8d72b803c298fe48df9df
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385229"
---
# <a name="create-ios-applications-in-configuration-manager"></a>在 Configuration Manager 中创建 iOS 应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 应用程序具有一个或多个部署类型，包含将软件部署到设备所需的安装文件和信息。 部署类型还具有指定软件的部署时间和方法的规则。  

请参阅[创建应用程序](/sccm/apps/deploy-use/create-applications#bkmk_create)，了解创建 Configuration Manager 应用程序和部署类型的步骤。 

创建和部署适用于 iOS 设备的应用程序时，请记住以下注意事项：  

- Configuration Manager 支持部署 iOS .ipa 包。 不需要在导入 iOS 应用时指定属性列表 (.plist) 文件。 

- 将 iOS 应用程序部署为“可用”或“必需”。 用户必须同意安装和卸载。

> [!IMPORTANT]  
>  目前，最终用户无法从 iOS 的 Microsoft Intune 公司门户应用中安装公司应用。 此限制源于 iOS 应用商店中发布的应用的限制。 （请参阅应用商店审核指南第 2 部分）。 用户可以通过浏览到其设备上的 Intune 门户来安装公司应用。 这些应用包括托管的应用商店应用和业务线应用包。 有关 Intune 公司门户应用启用的移动管理功能的详细信息，请参阅 [Microsoft Intune 中的注册设备管理功能](https://docs.microsoft.com/intune/device-enrollment)。  
