---
title: "创建 Windows Embedded 应用程序 | Microsoft Docs"
description: "请参阅创建和部署适用于 Windows Embedded 设备的应用程序时必须考虑的注意事项。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
caps.latest.revision: "7"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: cb0c22f3060ba654778dca958d620f1e1725b93c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-windows-embedded-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建 Windows Embedded 应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

除了创建应用程序的其他 System Center Configuration Manager 要求和过程，在创建和部署适用于 Windows Embedded 设备的应用程序时还必须考虑以下注意事项。  

## <a name="general-considerations"></a>一般注意事项  

-   将应用程序部署到启用了写入筛选的 Windows Embedded 设备时，可以指定是否在应用部署过程中对设备禁用写入筛选器。 然后可以选择在应用部署后重启写入筛选器。 如果未禁用写入筛选器，则软件会部署到临时覆盖区。 这意味着，除非另一部署强制保留更改，否则设备重启时将不再安装该软件。  

-   将应用程序部署到 Windows Embedded 设备时，确保设备是配置了维护时段的集合的成员。 这样，你可以管理禁用和启用写入筛选器的时间，以及设备重启的时间。  

-   控制写入筛选器行为的设置是一个名为“在截止时间或在维护时段内提交更改(需要重启)”的复选框。  

## <a name="tips-for-deploying-applications"></a>部署应用程序提示  

**为启用了写入筛选器的 Windows Embedded 设备使用必需的应用程序（而不是可用应用程序）** 由于用户无法在启用了写入筛选器的 Windows Embedded 设备上通过软件中心安装应用，因此请在部署应用程序时始终以对这些设备**必需**为部署目标，而不是对这些设备**可用**。 通常这不会有问题，因为运行 Windows Embedded 操作系统的计算机通常运行必须为多个用户采用相同方式运行的单一应用程序。 正因为如此，IT 部门会严密管理和锁定这些设备。 必需的应用程序非常适合于这种情况。

 但是，如果在启用了写入筛选器的情况下用户确实在嵌入式设备上运行多个应用程序，请将以下限制告知这些用户：  

-   用户无法通过软件中心安装所需的软件。  

-   用户无法在软件中心的“选项”选项卡上更改其工作时间。  

-   用户无法推迟必需应用程序的安装。  

此外，如果 Configuration Manager 为软件安装和更新提交更改，低权限用户将无法在维护期间登录。 在此期间，用户将看到一条消息，告知他们设备由于正在维护而不可用。  

**如果应用程序要求用户接受许可条款，请不要将应用程序部署到启用了写入筛选器的 Windows Embedded 设备。** 在禁用了写入筛选器以便 Configuration Manager 能够在嵌入式设备上安装软件时，低权限用户将无法登录到设备。 如果安装要求用户接受许可条款，这将无法进行，并且安装将失败。 如果安装需要用户交互，请确保不要将软件部署到 Windows Embedded 设备。 你可以使用“适用平台”列表来筛选这些操作系统。  
