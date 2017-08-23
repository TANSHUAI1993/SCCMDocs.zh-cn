---
title: "封鎖用戶端 | Microsoft Docs"
description: "為了系統安全性，使用 System Center Configuration Manager 封鎖用戶端存取。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3e323ab90ec4cc274581e19065fd7d81c0c11c35
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="determine-whether-to-block-clients-in-system-center-configuration-manager"></a>判斷是否要在 System Center Configuration Manager 中封鎖用戶端

*適用於：System Center Configuration Manager (最新分支)*

如果您不再信任某個用戶端電腦或用戶端行動裝置，可以在 Systerm Center 2012 Configuration Manager 主控台中封鎖該用戶端。 Configuration Manager 基礎結構會拒絕被封鎖的用戶端，因此這些用戶端無法與站台系統通訊並下載原則、上傳清查資料或傳送狀態或狀態訊息。  

 您必須從用戶端指派到的網站封鎖和解除封鎖該用戶端，而不是從次要網站或管理中心網站。  

> [!IMPORTANT]  
>  雖然 Configuration Manager 中的封鎖有助於保護 Configuration Manager 站台的安全，但如果允許站台使用 HTTP 與網站系統通訊，請勿依賴此功能來防範不受信任的電腦或行動裝置，因為被封鎖的用戶端可以使用新的自我簽署憑證和硬體 ID 重新加入站台。 反之，如果用於部署作業系統的開機媒體遺失或遭到竄改，且站台系統接受 HTTPS 用戶端連線時，再使用封鎖功能封鎖這類開機媒體。  

 您無法封鎖使用 ISV Proxy 憑證存取網站的用戶端。 如需 ISV Proxy 憑證的詳細資訊，請參閱 System Center Configuration Manager 軟體開發套件 (SDK)。  

 如果網站系統接受 HTTPS 用戶端連線，且您的公開金鑰基礎結構 (PKI) 支援憑證撤銷清單 (CRL)，請務必考慮使用憑證撤銷作為主要防禦機制以防止可能遭竄改的憑證。 在 Configuration Manager 中封鎖用戶端是保護階層的第二條防線。  

##  <a name="BKMK_Block_vs_CRL"></a> 封鎖用戶端的考量  

-   此選項適用於 HTTP 和 HTTPS 用戶端連線，但如果用戶端使用 HTTP 來連線到站台系統，則安全性有限。  

-   Configuration Manager 系統管理使用者有權封鎖用戶端，且此動作會在 Configuration Manager 主控台中執行。  

-   只有 Configuration Manager 階層拒絕用戶端通訊。  

    > [!NOTE]  
    >  同一個用戶端可能在不同的 Configuration Manager 階層註冊。  

-   Configuration Manager 站台會立即封鎖用戶端。  

-   有助於保護網站系統防止遭竄改的電腦和行動裝置入侵。  

## <a name="considerations-for-using-certificate-revocation"></a>使用憑證撤銷的考量  

-   如果公開金鑰基礎結構支援憑證撤銷清單 (CRL)，此選項便可適用於 HTTPS Windows 用戶端連線。  

     Mac 用戶端一律會執行 CRL 檢查，無法停用此功能。  

     雖然行動裝置用戶端不使用憑證撤銷清單來檢查站台系統的憑證，但 Configuration Manager可以撤銷及檢查站台系統的憑證。  

-   公開金鑰基礎結構系統管理員有權撤銷憑證，此動作會在 Configuration Manager 主控台以外執行。  

-   可透過任何要求此用戶端憑證的電腦或行動裝置拒絕用戶端通訊。  

-   撤銷憑證與網站系統下載修改過的憑證撤銷清單 (CRL) 之間可能會有延遲。  

-   在許多 PKI 部署中，此類延遲可能會達一天或更久。 例如，在 Active Directory 憑證服務中，完整 CRL 的預設到期時間是一週，差異 CRL 的預設到期時間則是一天。  

-   有助於保護網站系統和用戶端防止遭竄改的電腦和行動裝置入侵。  

    > [!NOTE]  
    >  您可以在 IIS 中設定憑證信任清單 (CTL)，進一步防範未知用戶端破壞執行 IIS 的網站系統。  
