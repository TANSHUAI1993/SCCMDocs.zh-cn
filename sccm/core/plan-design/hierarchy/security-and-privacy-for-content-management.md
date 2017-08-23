---
title: "內容管理安全性和隱私權 | Microsoft Docs"
description: "在 System Center Configuration Manager 中最佳化內容管理的安全性與隱私權。"
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: c4b9d13079c313879c6d43b10867c616fa962668
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-content-management-for-system-center-configuration-manager"></a>System Center Configuration Manager 內容管理的安全性與隱私權

*適用對象：System Center Configuration Manager (最新分支)*

本主題包含 System Center Configuration Manager 中內容管理的安全性和隱私權資訊。 請搭配下列主題閱讀：  

-   [System Center Configuration Manager 的應用程式管理安全性與隱私權](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

-   [System Center Configuration Manager 中軟體更新的安全性和隱私權](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

-   [System Center Configuration Manager 中作業系統部署的安全性和隱私權](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  

##  <a name="BKMK_Security_ContentManagement"></a> 內容管理的安全性最佳做法  
 利用下列安全性最佳作法進行內容管理：  

 **對於內部網路上的發佈點，請考慮使用 HTTPS 和 HTTP 的優缺點**：在大部分案例下，使用 HTTP 和套件存取帳戶以獲得授權，能提供比使用具加密但沒有授權的 HTTPS 更高的安全性。 不過，如果您的內容中包含機密資料，而您想要在傳送時加密資料，請使用 HTTPS。  

-   **當您對發佈點使用 HTTPS 時**，Configuration Manager 不會使用套件存取帳戶以授權內容存取，但內容透過網路傳送時會經過加密。  

-   **當您對發佈點使用 HTTP 時**，可以使用封裝存取帳戶進行授權，但內容透過網路傳送時不會經過加密。  


**如果您對發佈點使用 PKI 用戶端驗證憑證，而不是自我簽署的憑證，請用強式密碼保護憑證檔案 (.pfx)。如果您將檔案儲存在網路上，在將檔案匯入 Configuration Manager 時保護網路通道**：如果您需要密碼才能匯入發佈點用來與管理點進行通訊的用戶端驗證憑證，這就有助於保護憑證不受攻擊者利用。 在網路位置和站台伺服器之間使用伺服器訊息區 (SMB) 簽署或 IPsec，以防止攻擊者竄改憑證檔案。  

**從站台伺服器移除發佈點角色**：根據預設，發佈點會與站台伺服器安裝在相同的伺服器上。 用戶端不需要直接與站台伺服器進行通訊，因此若要減少攻擊層面，請將發佈點角色指派至其他站台系統，並且從站台伺服器中移除。  

**保護套件存取層級的內容**：發佈點共用允許所有使用者的 [讀取] 存取權限。 若要限制哪些使用者可存取內容，針對 HTTP 設定發佈點時，請使用套件存取帳戶。 這不適用於雲端架構的發佈點，因為其不支援套件存取帳戶。 如需套件存取帳戶的詳細資訊，請參閱[管理帳戶以存取內容](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md)。


**當您新增發佈點站台系統角色時，如果 Configuration Manager 安裝 IIS，請在發佈點安裝完成時移除 HTTP 重新導向或 IIS 管理指令碼及工具**：發佈點不需要 HTTP 重新導向或 IIS 管理指令碼及工具。 若要減少攻擊層面，請移除 Web 伺服器 (IIS) 角色的這些角色服務。  如需有關發佈點上 Web 伺服器 (IIS) 角色之角色服務的詳細資訊，請參閱[站台與站台系統必要條件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。  

**建立套件時設定套件存取權限**：由於對套件檔案上存取帳戶的變更只有在重新發佈套件時才會生效，因此初次建立套件時，務必小心設定套件存取權限。 當套件很大或是會發佈到多個發佈點，且內容發佈的網路頻寬容量有限時，這點特別重要。  

**實作存取控制以保護包含預先設置內容的媒體**：預先設置內容經過壓縮，但未加密。 攻擊者就可以讀取及修改之後下載到裝置的檔案。 Configuration Manager 用戶端會拒絕遭竄改的內容，但仍會下載它。  

**僅使用附有 Configuration Manager 之 ExtractContent 命令列工具 (ExtractContent.exe) 來匯入預先設置的內容，並確定經過 Microsoft 簽署**：若要避免竄改及提高權限，請僅使用附有 Configuration Manager 的授權命令列工具。  

**保護站台伺服器與套件來源位置之間通訊通道的安全**：當您建立應用程式和套件時，在站台伺服器與套件來源位置之間使用 IPsec 或 SMB 簽署。 這樣有助於避免攻擊者竄改來源檔案。  

**如果您在安裝任何發佈點角色之後，將站台設定選項變更為使用自訂網站，而不是預設網站，請移除預設虛擬目錄**：當您從預設網站切換為自訂網站時，Configuration Manager 不會移除舊的虛擬目錄。 移除 Configuration Manager 原本在預設網站下建立的虛擬目錄：  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**若是雲端式發佈點，保護您的訂閱詳細資料及憑證**：當您使用雲端式發佈點時，請保護高價值的項目，包括您 Azure 訂用帳戶的使用者名稱和密碼、Azure 管理憑證，以及雲端式發佈點服務憑證。 安全保存憑證，如果設定雲端架構的發佈點時要透過網路瀏覽憑證，請在站台系統伺服器與來源位置之間使用 IPsec 或 SMB 簽署。  

**雲端式發佈點︰為繼續獲得服務，請監視憑證的到期日**：Configuration Manager 在雲端式發佈點服務的匯入憑證管理即將到期時，不會向您提出警告。 您必須在 Configuration Manager 之外另行監視到期日，並請確定在到期日之前更新並匯入新憑證。 如果您向外部憑證授權單位 (CA) 購買 Configuration Manager 雲端架構的發佈點服務憑證，這點就相當重要，因為您可能需要額外的時間來取得更新的憑證。  

 如果這兩個憑證中的任一個已過期，雲端服務管理員就會產生狀態訊息識別碼 **9425**，而 CloudMgr.log 檔案會包含項目以指出憑證**處於過期狀態**，其中也會以 UTC 格式記錄到期日。  

## <a name="security-considerations-for-content-management"></a>內容管理的安全性考量  
規劃內容管理時，請考量下列項目︰  

-   用戶端只會驗證下載的內容。  

     Configuration Manager 用戶端只有在內容下載到其用戶端快取後，才會驗證內容上的雜湊。 如果攻擊者竄改下載的檔案清單或內容本身，則下載程序可能佔用相當大的網路頻寬，這樣只會讓用戶端在遭遇無效的雜湊時捨棄內容。  

-   當您使用雲端式發佈點時，存取內容時會自動將範圍限制在您的企業中，因此您無法進一步限制在選取的使用者或群組中。  

-   當您使用雲端架構的發佈點時，管理點會驗證用戶端，然後使用 Configuration Manager 權杖來存取雲端架構的發佈點。 權杖的有效時間為八個小時。 這表示，如果某個用戶端因不再受信任而遭到封鎖，它可繼續從雲端式發佈點下載內容，直到此權杖的有效期間到期。 這種情況下，因為用戶端遭到封鎖，所以管理點不會對用戶端發出另一個權杖。  

     若要防止封鎖的用戶端在八小時的時間範圍內下載內容，您可以從 Configuration Manager 主控台中 [系統管理] 工作區之 [階層設定] 的 [雲端] 節點，停止雲端服務。  

##  <a name="BKMK_Privacy_ContentManagement"></a> 內容管理的隱私權資訊  
 Configuration Manager 不會在內容檔案中包含任何使用者資料，雖然管理使用者可能選擇這樣做。  

 在您設定內容管理之前，請先考慮隱私權需求。  
