---
title: "使用 Microsoft Intune 注册的移动设备的软件清单 | Microsoft Docs"
description: "使用 Microsoft Intune 注册的移动设备的软件清单。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 2ed79d02535768de136947e4a5b63ad186d9a3cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Microsoft Intune 注册的移动设备的软件清单

*适用范围：System Center Configuration Manager (Current Branch)*

 可针对移动设备上安装的应用收集清单。 是否将应用加入清单将取决于设备归公司所有还是归个人所有。 对于个人设备，仅将通过 Microsoft Intune 管理的应用加入清单。  

> [!NOTE]  
>  会将移动设备上安装的应用的清单作为[硬件清单](mobile-device-hardware-inventory-hybrid.md)过程的一部分进行收集。  

 下方列出了适用于个人拥有设备或公司拥有设备的应用清单。  

|平台|个人拥有设备|公司拥有设备|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10（不带 Configuration Manager 客户端）|仅托管应用|仅托管应用|
|Windows 8.1（不带 Configuration Manager 客户端）|仅托管应用|仅托管应用|  
|Windows Phone 8|仅托管应用|仅托管应用|  
|Windows RT|仅托管应用|仅托管应用|  
|iOS|仅托管应用|设备上安装的所有应用|  
|Android|仅托管应用|设备上安装的所有应用|  

若要深入了解使用软件清单在客户端设备上收集文件信息，请参阅[软件清单简介](../../core/clients/manage/inventory/introduction-to-software-inventory.md)和[如何配置软件清单](../../core/clients/manage/inventory/configure-software-inventory.md)。
