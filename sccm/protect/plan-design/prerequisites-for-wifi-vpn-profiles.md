---
title: "Wi-Fi 和 VPN 設定檔必要條件 | Microsoft Docs"
description: "了解在 System Center Configuration Manager 中管理憑證設定檔、Wi-Fi 設定檔和 VPN 設定檔所需的安全性權限。"
ms.custom: na
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 309b0363f9b3ec4a31b8323b9e64c9f73060c281
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中 Wi-Fi 和 VPN 設定檔的必要條件

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的 Wi-Fi 和 VPN 設定檔僅具有產品內的相依性。  

 您必須具有下列安全性權限才能管理公司資源存取設定，例如憑證設定檔、Wi-Fi 設定檔和 VPN 設定檔：  

-   檢視與管理 Wi-Fi 設定檔的警示和報告：[警示] 物件的 [建立]、[刪除]、[修改]、[修改報告]、[讀取] 和 [執行報告]。  

-   建立和管理憑證設定檔：[憑證設定檔] 物件的 [撰寫原則] 、[修改報告] 、[讀取]  及 [執行報告]  。  

-   管理 Wi-Fi、憑證和 VPN 設定檔部署：[集合] 物件的 [部署組態原則] 、[修改用戶端狀態警示] 、[讀取]  及 [讀取資源]  。  

-   管理所有組態原則：[組態原則] 物件的 [建立] 、[刪除] 、[修改] 、[讀取]  及 [設定安全性範圍]  。  

-   執行與 Wi-Fi 和 VPN 設定檔相關的查詢：[查詢] 物件的 [讀取] 權限。  

-   在 System Center Configuration Manager 主控台中檢視 Wi-Fi 和 VPN 設定檔資訊：[站台] 物件的 [讀取] 權限。  

-   檢視 Wi-Fi 和 VPN 設定檔的狀態訊息：[狀態訊息] 物件的 [讀取] 權限。  

-   建立和修改信任的 CA 憑證設定檔：[信任的 CA 憑證設定檔] 物件的 [撰寫原則] 、[修改報告] 、[讀取]  及 [執行報告]  。  

-   建立和管理 VPN 設定檔：[VPN 設定檔] 物件的 [撰寫原則] 、[修改報告] 、[讀取]  及 [執行報告]  。  

-   建立和管理 Wi-Fi 設定檔：[Wi-Fi 設定檔] 物件的 [撰寫原則] 、[修改報告] 、[讀取]  及 [執行報告]  。  

 [公司資源存取管理員] 安全性角色包括在 System Center Configuration Manager 中管理 Wi-Fi 設定檔所需的上列權限。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中設定安全性](../../core/plan-design/security/configure-security.md)。
