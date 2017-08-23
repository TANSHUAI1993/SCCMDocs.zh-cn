---
title: "硬體清查安全性隱私權 | Microsoft Docs"
description: "取得 System Center Configuration Manager 中硬體清查的安全性與隱私權資訊。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: ec182ec3102e0f4ae8bcf3d1ef843b25510b6ce6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-hardware-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中硬體清查的安全性與隱私權

*適用對象：System Center Configuration Manager (最新分支)*

本主題包含 System Center Configuration Manager 中硬體清查的安全性與隱私權資訊。  

##  <a name="BKMK_Security_HardwareInventory"></a> 硬體清查的安全性最佳做法  
 當您要收集來自用戶端的硬體清查資料時，請使用下列安全性最佳做法：  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|簽署並加密清查資料|用戶端使用 HTTPS 與管理點進行通訊時，它們傳送的所有資料都是使用 SSL 進行加密。 不過，用戶端電腦使用 HTTP 與內部網路上的管理點進行通訊時，可以透過未簽署和未加密方式傳送用戶端清查資料和收集到的檔案。 請確定站台設定成需要簽署並使用加密。 此外，如果用戶端可以支援 sha-256 演算法，選取 需要 sha-256 的選項。|  
|不會收集在高安全性環境中的 IDMIF 和 NOIDMIF 檔案|您可以使用 IDMIF 和 NOIDMIF 檔案集合來擴充硬體清查彙總。 Configuration Manager 會在必要時建立新的資料表或修改現有資料表中的 Configuration Manager 資料庫，以容納 IDMIF 和 NOIDMIF 檔案中的屬性。 不過，Configuration Manager 不會驗證 IDMIF 和 NOIDMIF 檔案，因此這些檔案可以用來改變您不想更改的資料表。 有效的資料可能會覆寫不正確的資料。 此外，無法新增大量的資料和處理這項資料可能會導致延遲所有 Configuration Manager 函式。 若要降低這些風險，請將硬體清查用戶端設定 [收集 MIF 檔案]  設定為 [無] 。|  

### <a name="security-issues-for-hardware-inventory"></a>硬體清查的安全性問題  
 收集清查可找出潛在的漏洞。 攻擊者可以執行下列作業：  

-   傳送無效資料是管理點無法接受的作業，即使停用軟體清查用戶端設定但未啟用檔案收集也是一樣。  

-   透過單一檔案和許多檔案傳送極大量的資料，可能會造成拒絕服務。  

-   存取清查資訊，就像是傳送至 Configuration Manager 一樣。  

 因為具有本機系統管理權限的使用者可以將任何資訊傳送為清查資料，所以請不要將 Configuration Manager 所收集的清查資料視為已授權。  

 硬體清查預設會啟用為用戶端設定。  

##  <a name="BKMK_Privacy_HardwareInventory"></a> 硬體清查的隱私權資訊  
 硬體清查可讓您擷取登錄以及 Configuration Manager 用戶端之 WMI 中所儲存的任何資訊。 軟體清查可讓您找出所指定類型的所有檔案，或從用戶端中收集任何指定的檔案。 Asset Intelligence 透過擴充硬體與軟體清查，並加入新的授權管理功能，來增強清查功能。  

 硬體清查預設會啟用為用戶端設定，而收集到的 WMI 資訊取決於您選取的選項。 預設會啟用軟體清查，但預設不會收集檔案。 雖然您可以選取要啟用的硬體清查報告類別，但是會自動啟用 Asset Intelligence 資料收集。  

 清查資訊不會傳送給 Microsoft。 清查資訊會儲存在 Configuration Manager 資料庫中。 用戶端使用 HTTPS 來連線到管理點時，會在傳輸期間加密他們傳送到站台的清查資料。 如果用戶端使用 HTTP 來連線到管理點，則您可以選擇啟用清查加密。 清查資料不會以加密格式儲存在資料庫中。 資訊會保留在資料庫中，直到每 90 天由站台維護工作 [刪除過時清查歷程記錄]  或 [刪除過時收集檔案]  刪除為止。 您可以設定刪除間隔。  

 設定硬體清查、軟體清查、檔案收集或 Asset Intelligence 資料收集之前，請考慮您的隱私權需求。  
