---
title: "軟體清查安全性隱私權 | Microsoft Docs"
description: "取得 System Center Configuration Manager 中軟體清查的安全性與隱私權資訊。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 7652e46d2168e2de623fa8e6d5b8663701764244
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中軟體清查的安全性和隱私權

*適用對象：System Center Configuration Manager (最新分支)*

本主題包含 System Center Configuration Manager 中軟體清查的安全性與隱私權資訊。  

##  <a name="BKMK_Security_HardwareInventory"></a> 軟體清查的安全性最佳做法  
 當您收集來自用戶端的軟體清查資料時，請使用下列安全性最佳做法：  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|簽署並加密清查資料|用戶端使用 HTTPS 與管理點進行通訊時，它們傳送的所有資料都是使用 SSL 進行加密。 不過，用戶端電腦使用 HTTP 與內部網路上的管理點進行通訊時，可以透過未簽署和未加密方式傳送用戶端清查資料和收集到的檔案。 請確定站台設定成需要簽署並使用加密。 此外，如果用戶端可以支援 SHA-256 演算法，請選取需要 SHA-256 的選項。|  
|請不要使用檔案收集來收集重要檔案或機密資訊。|Configuration Manager 軟體清查會使用 LocalSystem 帳戶的所有權限來收集重要系統檔案 (例如登錄或安全性帳戶資料庫) 的複本。 這些檔案位於站台伺服器時，具有讀取資源權限或所儲存檔案位置之 NTFS 權限的人員可以分析其內容，而且可能會察覺出用戶端的重要詳細資料，進而危及其安全。|  
|限制用戶端電腦上的本機系統管理權限|具有本機系統管理權限的使用者可以將無效的資料傳送為清查資訊。|  

### <a name="security-issues-for-software-inventory"></a>軟體清查的安全性問題  
 收集清查會公開潛在的弱點。 攻擊者可以執行下列作業：  

-   傳送無效資料是管理點無法接受的作業，即使停用軟體清查用戶端設定但未啟用檔案收集也是一樣。  

-   透過單一檔案和許多檔案傳送極大量的資料，可能會造成拒絕服務。  

-   存取清查資訊，就像是傳送至 Configuration Manager 一樣。  

 如果使用者知道他們可以建立名為 **Skpswi.dat** 的隱藏檔案，並將它放在用戶端硬碟機的根目錄中以排除不進行軟體清查，則無法收集來自該電腦的軟體清查資料。  

 因為具有本機系統管理權限的使用者可以將任何資訊傳送為清查資料，所以請不要將 Configuration Manager 所收集的清查資料視為已授權。  

 軟體清查預設會啟用為用戶端設定。  

##  <a name="BKMK_Privacy_HardwareInventory"></a> 軟體清查的隱私權資訊  
 硬體清查可讓您擷取登錄以及 Configuration Manager 用戶端之 WMI 中所儲存的任何資訊。 軟體清查可讓您找出所指定類型的所有檔案，或從用戶端中收集任何指定的檔案。 Asset Intelligence 透過擴充硬體與軟體清查，並加入新的授權管理功能，來增強清查功能。  

 硬體清查預設會啟用為用戶端設定，而收集到的 WMI 資訊取決於您選取的選項。 預設會啟用軟體清查，但預設不會收集檔案。 雖然您可以選取要啟用的硬體清查報告類別，但是會自動啟用 Asset Intelligence 資料收集。  

 清查資訊不會傳送給 Microsoft。 清查資訊會儲存在 Configuration Manager 資料庫中。 用戶端使用 HTTPS 來連線到管理點時，會在傳輸期間加密他們傳送到站台的清查資料。 如果用戶端使用 HTTP 來連線到管理點，則您可以選擇啟用清查加密。 清查資料不會以加密格式儲存在資料庫中。 資訊會保留在資料庫中，直到每 90 天由站台維護工作 [刪除過時清查歷程記錄]  或 [刪除過時收集檔案]  刪除為止。 您可以設定刪除間隔。  

 設定硬體清查、軟體清查、檔案收集或 Asset Intelligence 資料收集之前，請考慮您的隱私權需求。  
