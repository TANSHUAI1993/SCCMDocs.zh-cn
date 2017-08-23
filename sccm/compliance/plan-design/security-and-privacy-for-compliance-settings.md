---
title: "合規性設定的安全性和隱私權 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中相容性設定的安全性最佳作法。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e7dc554ffcd23978eed44819b525f6cc239b2135
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-compliance-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager 中相容性設定的安全性和隱私權

*適用對象：System Center Configuration Manager (最新分支)*


## <a name="security-best-practices-for-compliance-settings"></a>相容性設定的安全性最佳做法  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|不要監視機密資料。|為了避免資訊外洩，請不要將組態項目設定為監視可能的機密資訊。|  
|不要設定使用一般使用者可以修改之資料的相容性規則。|如果您建立的相容性規則是以使用者可以修改的資料為依據，例如用於組態選擇的登錄設定，則相容性結果的可靠性就無法受到保證。|  
|僅有當外部來源具備受信任發行者的有效數位簽章時，才由該外部來源匯入 Microsoft System Center 組態套件和其他組態資料。|您可為已發行的組態資料進行數位簽署，以驗證發佈來源並確保資料未遭到竄改。 若數位簽章驗證檢查失敗，就會向您發出警告，並提示您是否要繼續匯入。 如果您無法確認來源和資料的完整性，請不要匯入未簽署的資料。|  
|實作用於保護參照電腦的存取控制。|請確認在系統管理使用者瀏覽至參照電腦以設定登錄或檔案系統設定時，該參照電腦未遭入侵。|  
|瀏覽至參照電腦時，確保通訊通道的安全。|在透過網路傳送資料時，為避免資料遭到竄改，請在執行 Configuration Manager 主控台的電腦及參照電腦之間，使用網際網路通訊協定安全性 (IPsec) 或伺服器訊息區 (SMB)。|  
|限制並監視已獲得「相容性設定管理員」安全性角色的系統管理使用者。|具有 **「相容性設定管理員」** 角色的系統管理使用者可將組態項目部署到階層中的所有裝置與使用者。 組態項目可能影響非常強大，包括指令碼和登錄重新組態之類的項目。|  

## <a name="privacy-information-for-compliance-settings"></a>相容性設定的隱私權資訊  
 您可以使用相容性設定，來評估用戶端裝置是否與您在組態基準中部署的組態項目相容。 某些設定可以在不相容的情況下自動進行補救。 相容性資訊會由管理點傳送至站台伺服器並且儲存在站台資料庫中。 當裝置將此資訊傳送至管理點時會進行加密，但不會以加密格式儲存在站台資料庫內。 資訊會保留在資料庫中，直到每 90 天由站台維護工作 [刪除過時設定管理資料]  將它刪除為止。 您可以設定刪除間隔。 不會將相容性資訊傳送給 Microsoft。  

 依預設，裝置不會評估相容性設定。 此外，您必須先進行組態項目和組態基準的設定，然後將其部署至裝置。  
