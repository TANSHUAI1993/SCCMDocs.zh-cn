---
title: "準備步驟 | Microsoft Docs"
description: "在 System Center Configuration Manager 中準備使用內部部署行動裝置管理來管理裝置。"
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
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="preparation-steps-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 之內部行動裝置管理的準備步驟

*適用於：System Center Configuration Manager (最新分支)*

使用 System Center Configuration Manager 內部部署行動來裝置管理需要設定 Configuration Manager 基礎結構，以便必要的站台系統角色 (註冊 Proxy 點、註冊點、裝置管理點和發佈點) 可透過受信任的通道與要管理的行動裝置通訊。  

 下列高階工作為準備 Configuration Manager 系統用於內部部署行動裝置管理所需：  

-   [在 System Center Configuration Manager 中為內部部署行動裝置管理設定 Microsoft Intune 訂閱](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     在此工作中，您會註冊 Microsoft Intune，然後透過 Configuration Manager 主控台新增對 Configuration Manager 的訂閱。 此步驟僅供授權之用。 不會使用 Intune 來管理裝置或儲存管理資訊。 組織企業的所有裝置協調和管理都是使用內部部署 Configuration Manager 基礎結構進行。  

-   [在 System Center Configuration Manager 中為內部部署行動裝置管理安裝站台系統角色](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     在此工作中，您會安裝和設定使用內部部署 Configuration Manager 基礎結構來管理裝置時所需的站台系統角色。 內部部署行動裝置管理至少需要註冊 Proxy 點、註冊點、裝置管理點和發佈點站台系統角色。  

-   [在 System Center Configuration Manager 中為內部部署行動裝置管理設定受信任通訊的憑證](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     在此工作中，您會設定內部部署 Configuration Manager 基礎結構，允許受管理裝置與裝載所需站台系統角色的伺服器之間進行信任的通訊 (HTTPS)。  

-   [在 System Center Configuration Manager 中為內部部署行動裝置管理設定裝置註冊](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     在此工作中，您會授與權限給使用者來註冊電腦和裝置，而且您會在裝置 (通常是未加入網域的裝置) 上安裝受信任的根憑證，來允許對站台系統伺服器的 HTTPS 連線。  
