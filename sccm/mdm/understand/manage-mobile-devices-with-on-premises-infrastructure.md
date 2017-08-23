---
title: "內部部署行動裝置管理 (MDM) | Microsoft Docs"
description: "了解內部部署行動裝置管理，System Center Configuration Manager 的裝置管理解決方案。"
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
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>System Center Configuration Manager 的內部部署行動裝置管理 (MDM)

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 內部部署行動裝置管理是一種裝置管理解決方案，依賴裝置作業系統的內建管理功能 (根據 Open Mobile Alliance Device Management 或 OMA DM 標準)，同時使用企業的 Configuration Manager 基礎結構來管理和維護裝置。 內部部署行動裝置管理需要 Microsoft Intune 設定管理功能，但只有訂閱需要 (以及幫助通知裝置簽入原則變更時)，但不會用於管理裝置或儲存其相關資料。  

 ![內部部署概念](media/On-premises-conceptual.png)  

 Microsoft Intune 的內部部署行動裝置管理，也依賴內建的 OMA DM 功能，但所有管理功能都是透過雲端服務提供。  內部部署行動裝置管理也不同於傳統上由 Configuration Manager 所提供的用戶端管理解決方案，差異在於它依賴類似的企業基礎結構，但未在所管理的電腦和裝置上使用個別安裝的用戶端軟體。  

 下表列出相較於傳統用戶端管理的內部部署行動裝置管理優缺點：  

|優點|缺點|  
|----------------|-------------------|  
|**簡化基礎結構** - 需要較少的站台系統角色。<br /><br /> **容易維護**：因為管理功能內建於裝置作業系統，所以在 Configuration Manager 系統中引入新的管理功能時不需要用戶端軟體的新版本。<br /><br /> **內部部署** - 所有管理和資料都是以內部部署方式保留。|**較少的用戶端管理功能** - 無協調流程、軟體計量、協力廠商整合、工作順序或軟體中心支援。<br /><br /> **有限裝置支援**：內部部署行動裝置管理目前只支援執行 Windows 10 和 Windows 10 Mobile 的裝置。|  

 下列主題所提供的資訊可用來規劃、準備和註冊內部部署行動裝置管理的裝置：  

-   [System Center Configuration Manager 中的內部部署行動裝置管理規劃](../plan-design/plan-on-premises-mdm.md)  

     深入了解設定 Configuration Manager 基礎結構以及規劃內部部署行動裝置管理中的裝置註冊時必須考量的事項。  

-   [System Center Configuration Manager 之內部部署行動裝置管理的準備步驟](../get-started/preparation-steps-for-on-premises-mdm.md)  

     深入了解如何設定 Microsoft Intune 訂閱、設定憑證、安裝站台系統角色，以及設定裝置註冊，以針對內部部署行動裝置管理準備 Configuration Manager 系統。  

-   [在 System Center Configuration Manager 中註冊裝置以進行內部部署行動裝置管理](../deploy-use/enroll-devices-on-premises-mdm.md)  

     了解如何進行註冊、使用者如何註冊自己的裝置，以及如何使用註冊套件來大量註冊裝置。  
