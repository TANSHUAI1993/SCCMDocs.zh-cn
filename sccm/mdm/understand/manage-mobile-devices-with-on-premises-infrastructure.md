---
title: 本地 MDM
titleSuffix: Configuration Manager
description: 了解如何在本地移动设备管理，设备管理解决方案配置管理器中
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49e07a7ebe6ec53d61ea9e2ee3bc941dd8561094
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558212"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中的本地 MDM

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 本地移动设备管理 (MDM) 是依赖于设备操作系统的内置管理功能的设备管理解决方案。 此功能基于开放移动联盟 (OMA) 设备管理 (DM) 标准。 它使用组织的 Configuration Manager 基础结构来管理和维护设备。 在本地 MDM 要求 Microsoft Intune 设置管理功能，但只有所需的订阅。 有时使用 Intune 来帮助通知设备签入策略更改，但它不用于管理设备或存储有关它们的数据。  

![本地概念](media/On-premises-conceptual.png)  

在本地 MDM 不同于 Microsoft Intune，也依赖于内置的 OMA DM 功能。 在 Intune 中的管理功能的所有传递通过云服务。 在本地 MDM 也不同于传统上由 Configuration Manager 提供的基于客户端的管理解决方案。 它依赖类似于基础结构，而不使用它管理的设备上的单独安装的客户端软件。  

> [!Note]  
> 从版本 1810年，Intune 连接不再新的本地 MDM 部署所必需的。<!--3607730, fka 1359124--> 组织仍需要 Intune 许可证才能使用此功能。 当前不能从现有的本地 MDM 部署中删除 Intune 连接。 有关详细信息，请参阅 [Intune 支持博客文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150)。  

下表列出了本地 MDM 与传统基于客户端管理相比的优缺点：  

|优点|缺点|  
|----------------|-------------------|  
|**简化了基础结构** - 需要的站点系统角色更少。<br /><br /> **更轻松地维护**-由于管理功能内置于设备操作系统的新版本的客户端软件不需要对 Configuration Manager 系统引入新的管理功能。<br /><br /> **本地** - 所有管理和数据均保留在本地。|**客户端管理功能更少** - 没有业务流程、软件计数、第三方集成、任务序列或软件中心支持。<br /><br /> **设备支持有限**-当前本地 MDM 仅支持的设备运行 Windows 10 和 Windows 10 移动版。|  

以下文章提供了可用于规划、 准备和注册设备以在本地 MDM 的信息：  

- [规划本地 MDM](/sccm/mdm/plan-design/plan-on-premises-mdm)  

    了解有关要考虑的问题时设置的 Configuration Manager 基础结构和规划设备注册中的本地 mdm。  

- [用于本地 MDM 的准备步骤](/sccm/mdm/get-started/preparation-steps-for-on-premises-mdm)  

    使 Configuration Manager 可供本地 MDM 设置 Microsoft Intune 订阅、 设置证书、 安装站点系统角色和设置设备注册。  

- [注册设备以实现本地 MDM](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

    了解如何进行注册、用户如何注册其自己的设备，以及如何使用注册包批量注册设备。  

