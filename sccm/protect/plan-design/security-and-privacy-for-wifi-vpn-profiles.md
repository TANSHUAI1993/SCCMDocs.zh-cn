---
title: "Wi-Fi 和 VPN 設定檔安全性和隱私權 | Microsoft Docs"
description: "了解管理 System Center Configuration Manager 裝置 Wi-Fi 和 VPN 設定檔的安全性最佳作法。"
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 6d1d0a393a2ce614ae5f819475bd47b05e699b45
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中 Wi-Fi 和 VPN 設定檔的安全性和隱私權

*適用於：System Center Configuration Manager (最新分支)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Wi-Fi 和 VPN 設定檔的安全性最佳作法  
 當您管理裝置的 Wi-Fi 和 VPN 設定檔時，可使用下列安全性最佳作法。  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|盡可能選擇 Wi-Fi 和 VPN 基礎結構和用戶端作業系統能夠支援的最安全選項。|Wi-Fi 和 VPN 設定檔提供便利的方法，集中散發及管理裝置已支援的 Wi-Fi 和 VPN 設定。 Configuration Manager 不會新增 Wi-Fi 或 VPN 功能。<br /><br /> 識別、實作及遵循為您的裝置和基礎結構所建議的任何安全性最佳作法。|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Wi-Fi 設定檔的隱私權資訊  
 您可以使用 Wi-Fi 和 VPN 設定檔將用戶端裝置設定為連線至 Wi-Fi 和 VPN 伺服器，然後評估在套用設定檔後這些裝置是否相容。 管理點會將相容性資訊傳到站台伺服器，且該資訊會存放在站台資料庫中。 當裝置將此資訊傳送至管理點時會進行加密，但不會以加密格式儲存在站台資料庫內。 資料庫會保留資訊，直到站台維護工作 [刪除過時設定管理資料]  將它刪除為止。 預設的刪除間隔時間為 90 天，但此設定可以變更。 不會將相容性資訊傳送給 Microsoft。  

 根據預設，裝置不會評估 Wi-Fi 和 VPN 設定檔。 此外，您必須設定設定檔，然後將其部署至使用者。  

 設定 Wi-Fi 或 VPN 設定檔之前，請考慮您的隱私權需求。  
