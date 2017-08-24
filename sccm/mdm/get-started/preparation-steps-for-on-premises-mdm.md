---
title: "准备步骤 | Microsoft Docs"
description: "准备在 System Center Configuration Manager 中通过本地移动设备管理对设备进行管理。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
caps.latest.revision: "4"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 85bdadaaaeed9a42cfa5165d2b9f0f3ef434dc03
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="preparation-steps-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>用于 System Center Configuration Manager 中本地移动设备管理的准备步骤

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 本地移动设备管理对设备进行管理需要设置 Configuration Manager 基础结构，以便所需的站点系统角色（注册代理点、注册点、设备管理点和分发点）可以跨整个受信任通道与要管理的移动设备进行通信。  

 需要以下高级任务来为本地移动设备管理准备 Configuration Manager 系统：  

-   [在 System Center Configuration Manager 中为本地移动设备管理设置 Microsoft Intune 订阅](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     在此任务中，需注册 Microsoft Intune，然后将订阅通过 Configuration Manager 控制台添加到 Configuration Manager。 此步骤仅需用于许可授权的目的。 Intune 不用于管理设备或存储管理信息。 设备的所有协调和管理均由你组织的企业通过使用本地 Configuration Manager 基础结构实施。  

-   [在 System Center Configuration Manager 中为本地移动设备管理安装站点系统角色](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     在此任务中，安装和配置使用本地 Configuration Manager 基础结构管理设备所需的站点系统角色。 本地移动设备管理至少需要注册代理点、注册点、设备管理点和分发点这些站点系统角色。  

-   [在 System Center Configuration Manager 中为本地移动设备管理的受信任通信设置证书](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     在此任务中，配置本地 Configuration Manager 基础结构，以允许管理的设备和承载所需站点系统角色的服务器之间能够进行受信任的通信 (HTTPS)。  

-   [在 System Center Configuration Manager 中为本地移动设备管理设置设备注册](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     在此任务中，向用户授予注册计算机和设备的权限，并在设备（通常是未加入域的设备）上安装受信任的根证书，以允许 HTTPS 连接到站点系统服务。  
