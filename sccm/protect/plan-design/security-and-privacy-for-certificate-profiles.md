---
title: "憑證設定檔安全性和隱私權 | Microsoft Docs"
description: "了解管理 System Center Configuration Manager 使用者和裝置憑證設定檔的安全性最佳作法。"
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: c51787ad3fa0bdb285017cfab1ca6931afba9ea6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 的憑證設定檔安全性和隱私權

*適用於：System Center Configuration Manager (最新分支)*


##  <a name="security-best-practices-for-certificate-profiles"></a>憑證設定檔的安全性最佳作法  
 您管理使用者和裝置的憑證設定檔時，可使用下列安全性最佳作法。  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|識別並遵循任何網路裝置註冊服務的安全性最佳實務，包含在 Internet Information Services (IIS) 設定網路裝置註冊服務網站，要求使用 SSL 並忽略用戶端的憑證。|請參閱 TechNet 上 Active Directory 憑證服務文件庫中的 [網路裝置註冊服務指南](http://go.microsoft.com/fwlink/p/?LinkId=309016) 。|  
|當您設定 SCEP 憑證設定檔時，請選擇裝置和基礎結構可支援的最安全選項。|識別、實作及遵循為您的裝置和基礎結構所建議的任何安全性最佳作法。|  
|手動指定使用者裝置親和性，而不是讓使用者識別自己的主要裝置。 此外，請勿啟用基於使用方式的設定。|如果您按一下 SCEP 憑證設定檔中的 [只允許在使用者主要裝置上註冊憑證]  選項，請勿將由使用者或裝置收集到的資訊視為已授權。 如果您使用此設定來部署 SCEP 憑證設定檔，而且信任的系統管理使用者未指定使用者裝置親和性，未授權的使用者可能會因而獲得較高的權限，以及被授與驗證憑證。<br /><br /> **注意：** 如果您確實啟用了基於使用方式的設定，則會藉由使用未受到 System Center Configuration Manager 保護的狀態訊息來收集此資訊。 若要降低此威脅，請在用戶端電腦和管理點之間使用 SMB 簽署或 IPsec。|  
|請勿將使用者的讀取及註冊權限加入憑證範本，或設定憑證登錄點跳過憑證範本檢查。|雖然 Configuration Manager 支援額外檢查以確認您是否新增使用者的讀取及註冊安全性權限，但是您也可以在無法驗證時設定憑證登錄點以跳過該檢查，但這兩種設定都不是安全性最佳作法。 如需詳細資訊，請參閱[規劃憑證設定檔在 System Center Configuration Manager 中的憑證範本權限](../../protect/plan-design/planning-for-certificate-template-permissions.md)。|  

## <a name="privacy-information-for-certificate-profiles"></a>憑證設定檔的隱私權資訊  
 您可以使用憑證設定檔來部署根憑證授權單位 (CA) 和用戶端憑證，然後評估這些裝置在套用設定檔之後是否可相容。 管理點會將相容性資訊傳送至站台伺服器，且 System Center Configuration Manager 會將該資訊存放在站台資料庫中。 相容性資訊包含如主體名稱和指紋等憑證內容。 當裝置將此資訊傳送至管理點時會進行加密，但不會以加密格式儲存在站台資料庫內。 資料庫會保留這些資訊，直到站台維護工作 [刪除過時設定管理資料]  在預設的 90 天間隔後將它刪除為止。 您可以設定刪除間隔。 不會將相容性資訊傳送給 Microsoft。  

 憑證設定檔會使用 Configuration Manager 透過探索收集的資訊。 如需探索隱私權資訊的詳細資訊，請參閱 **Security and privacy for System Center Configuration Manager** 中的 [探索的隱私權資訊](../../core/plan-design/security/security-and-privacy.md)一節。  

> [!NOTE]  
>  發行給使用者或裝置的憑證可允許存取機密資訊。  

 依預設，裝置不會評估憑證設定檔。 此外，您必須設定憑證設定檔，然後將其部署至使用者或裝置。  

 設定	憑證設定檔之前，請考慮您的隱私權需求。  
