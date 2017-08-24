---
title: "本地移动设备管理 (MDM) | Microsoft Docs"
description: "了解本地移动设备管理 - System Center Configuration Manager 中的设备管理解决方案。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
caps.latest.revision: "8"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 7b96c4d4d87aa150eacc5d7d20710f5d2199e48a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的本地移动设备管理 (MDM)

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 本地移动设备管理是一个设备管理解决方案，它在使用企业的 Configuration Manager 基础结构管理和维护设备时，（基于开放移动联盟设备管理或 OMA DM 标准）需要依赖设备操作系统的内置管理功能。 本地移动设备管理要求 Microsoft Intune 设置管理功能，但仅在订阅（有时帮助通知设备签入更改的策略）时需要，而不用于管理设备或存储有关这些设备的数据。  

 ![本地概念](media/On-premises-conceptual.png)  

 本地移动设备管理不同于 Microsoft Intune，后者还依赖于内置的 OMA DM 功能，但所有管理功能都通过云服务提供。  本地移动设备管理也不同于基于客户端的管理解决方案（过去由 Configuration Manager 提供），因为它依赖类似于企业的基础结构而不是使用其管理的计算机和设备上独立安装的客户端软件。  

 下表列出了本地移动设备管理与传统基于客户端管理相比的优缺点：  

|优点|缺点|  
|----------------|-------------------|  
|**简化了基础结构** - 需要的站点系统角色更少。<br /><br /> **更易于维护** - 由于管理功能是内置于设备操作系统的，因此当向 Configuration Manager 系统引入新的管理功能时将不再需要新版本的客户端软件。<br /><br /> **本地** - 所有管理和数据均保留在本地。|**客户端管理功能更少** - 没有业务流程、软件计数、第三方集成、任务序列或软件中心支持。<br /><br /> **设备支持有限** - 当前本地移动设备管理仅支持运行 Windows 10 和 Windows 10 移动版的设备。|  

 以下主题提供的信息可用于本地移动设备管理规划、准备和注册设备：  

-   [在 System Center Configuration Manager 中规划本地移动设备管理](../plan-design/plan-on-premises-mdm.md)  

     了解在本地移动设备管理中设置 Configuration Manager 基础结构和规划设备注册时需要考虑的事项。  

-   [用于 System Center Configuration Manager 中本地移动设备管理的准备步骤](../get-started/preparation-steps-for-on-premises-mdm.md)  

     了解如何通过设置 Microsoft Intune 订阅、设置证书、安装站点系统角色和设置设备注册为本地移动设备管理准备 Configuration Manager 系统。  

-   [在 System Center Configuration Manager 中为本地移动设备管理注册设备](../deploy-use/enroll-devices-on-premises-mdm.md)  

     了解如何进行注册、用户如何注册其自己的设备，以及如何使用注册包批量注册设备。  
