---
title: "如何建立 SCEP 憑證設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用憑證設定檔，透過受管理裝置所需的憑證來佈建受管理裝置。"
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
caps.latest.revision: "16"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 1e00804d27ecef2aadd8bfa395db1919c46243ee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-certificate-profiles"></a>建立憑證設定檔

*適用於：System Center Configuration Manager (最新分支)*


在 Configuration Manager (SCCM) 中使用憑證設定檔，透過受管理裝置存取公司資源所需的憑證來佈建受管理裝置。 建立憑證設定檔之前，請設定[設定 System Center Configuration Manager 的憑證基礎結構](certificate-infrastructure.md)中所述的憑證基礎結構。  

本主題描述如何建立受信任根和 SCEP 憑證設定檔。 如果您想要建立 PFX 憑證設定檔，請參閱[建立 PFX 憑證設定檔](../../protect/deploy-use/create-pfx-certificate-profiles.md)。

建立憑證設定檔：

1.  啟動建立憑證設定檔精靈。
1.  提供憑證的一般資訊。
1.  設定受信任的憑證授權單位 (CA) 憑證。  
1.  設定 SCEP 憑證資訊 (僅適用於 SCEP 憑證)。  
1.  指定憑證設定檔的支援平台。


## <a name="start-the-create-certificate-profile-wizard"></a>啟動建立憑證設定檔精靈  

1.  在 System Center Configuration Manager 主控台中，按一下 [資產與相容性]。  

2.  在 [資產與合規性] 工作區中，依序展開 [合規性設定] 和 [公司資源存取]，然後按一下 [憑證設定檔] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立憑證設定檔] 。  

## <a name="provide-general-information-about-the-certificate-profile"></a>提供憑證設定檔的一般相關資訊  

在 [建立憑證設定檔精靈] 的 [一般]  頁面上，指定下列資訊：  

-   **名稱**：輸入不重複的憑證設定檔名稱。 您最多可以使用 256 個字元。  

-   **描述**：提供一段描述以說明憑證設定檔的概觀，以及可協助您在 System Center Configuration Manager 主控台中進行識別的其他相關資訊。 您最多可以使用 256 個字元。  

-   **指定您要建立的憑證設定檔類型**：選擇下列其中一個憑證設定檔類型：  

-   **信任的 CA 憑證**：當使用者或裝置必須驗證其他裝置時，如果您要部署信任的根憑證授權單位 (CA) 或中繼 CA 憑證以組成信任的憑證鏈結，請選取此憑證設定檔類型。 例如，裝置可能是遠端驗證撥入使用者服務 (RADIUS) 伺服器或虛擬私人網路 (VPN) 伺服器。 在建立 SCEP 憑證設定檔之前，您還必須設定信任的 CA 憑證設定檔。 在此情況中，信任的 CA 憑證設定檔必須是發行憑證至使用者或裝置之 CA 的受信任根憑證。  

-   **簡單憑證註冊通訊協定 (SCEP) 設定**：如果您使用簡單憑證註冊通訊協定和網路裝置註冊服務角色服務來要求使用者或裝置的憑證，請選取此憑證設定檔類型。

-   **個人資訊交換 PKCS #12 (PFX) 設定 - 匯入**：選取此選項以匯入 PFX 憑證。 若要深入了解 PFX 憑證的建立，請參閱[匯入 PFX 憑證設定檔](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md)。

-   **個人資訊交換 PKCS #12 (PFX) 設定 - 建立**：選取此選項以使用憑證授權單位處理 PFX 憑證。 若要深入了解如何建立 PFX 憑證，請參閱[建立 PFX 憑證設定檔](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md)。


## <a name="configure-a-trusted-ca-certificate"></a>設定受信任 CA 憑證  

> [!IMPORTANT]  
>  在建立 SCEP 憑證設定檔之前，您還必須設定至少一個信任的 CA 憑證設定檔。    
>  
>  如果您在部署憑證後變更其中任何值，則會要求新憑證：
>  -  金鑰儲存提供者
>  -  憑證範本名稱
>  -  憑證類型
>  -  主體名稱格式
>  -  主體別名
>  -  憑證有效期間
>  -  金鑰使用方法
>  -  金鑰大小
>  -  擴充金鑰使用方法
>  -  根 CA 憑證

1.  在 [建立憑證設定檔精靈] 的 [信任的 CA 憑證]  頁面上，指定下列資訊：  

 -   **憑證檔案**：按一下[匯入]  ，然後瀏覽至您要使用的憑證檔案。  

 -   **目的地存放區**：若裝置有多個憑證存放區，請選取儲存憑證的存放區。 若裝置只有一個存放區，則忽略此設定。  

2.  使用 [憑證指紋]  值來確認您已匯入正確的憑證。  


## <a name="configure-scep-certificate-information-only-for-scep-certificates"></a>設定 SCEP 憑證資訊 (僅適用於 SCEP 憑證)  

1.  在 [建立憑證設定檔精靈] 的 [SCEP 伺服器]  頁面上，指定會透過 SCEP 發行憑證的 NDES 伺服器之 URL。 您可以選擇依據憑證登錄點站台系統伺服器，自動指派 NDES URL，或以手動方式新增 URL。  

2.  完成 [建立憑證設定檔精靈] 的 [SCEP 註冊] 頁面。

 -  **重試**：指定裝置自動向執行網路裝置註冊服務的伺服器要求重試憑證的次數。 此設定可支援 CA 管理員在接受之前必須先核准憑證要求的情況。 這項設定通常用於高安全性環境，或是您具有獨立的發行 CA 而非企業 CA 的情況。 您可能也會基於測試目的使用此設定，使您可以在發行 CA 處理憑證要求之前檢查憑證要求選項。 搭配 [重試延遲 (分鐘)]  設定來使用此設定。  

 -   **重試延遲 (分鐘)**：指定在發行 CA 處理憑證要求之前使用 CA 管理員核准時，每一次註冊嘗試之間的間隔分鐘數。 如果您基於測試目的來使用管理員核准，您可能會指定較低的值，使您在核准要求之後，不需要長時間等待裝置重試憑證要求。 不過，如果您在生產網路中使用管理員核准，您可能會需要指定較高的值，使 CA 系統管理原有較充裕的時間來檢查以及核准或拒絕擱置中的核准。  

 -   **更新閾值 (%)**：指定裝置要求憑證更新之前，剩餘的憑證存留時間百分比。  

 -   **金鑰儲存提供者 (KSP)**：指定儲存憑證金鑰的位置。 選擇下列其中一個值：  

   -   **安裝至信賴平台模組 (TPM) (若存在)**：將金鑰安裝至 TPM。 如果 TPM 不存在，金鑰將會安裝至軟體金鑰的儲存提供者。  

   -   **安裝至信賴平台模組 (TPM) 否則便失敗**：將金鑰安裝至 TPM。 如果 TPM 模組不存在，安裝將會失敗。  

   -   **安裝至商務用 Windows Hello，否則失敗**：此選項適用於 Windows 10 桌面版和行動裝置版裝置。 它會向 [商務用 Windows Hello] 註冊金鑰 (如 [System Center Configuration Manager 中的商務用 Windows Hello 設定](../../protect/deploy-use/windows-hello-for-business-settings.md)中所述)。 您也可利用此選項，在對這些裝置發出憑證之前，於裝置註冊期間 **要求多重要素驗證** 。 如需詳細資訊，請參閱[使用 Multi-Factor Authentication 來保護 Windows 裝置](https://technet.microsoft.com/library/dn889751.aspx)。

   > [!NOTE]  
   > 
   > 當使用者建立商務用 Windows Hello PIN 時，Windows 會傳送 Configuration Manager 所接聽的通知。 這可讓 Configuration Manager 快速察覺已建立 Windows Hello PIN 的使用者。 如果將 Windows Hello 用來作為憑證設定檔中的「金鑰儲存提供者」，Configuration Manager 便可接著將新的憑證一併發行給這些使用者。  

   -   **安裝至軟體金鑰儲存提供者**：將金鑰安裝至軟體金鑰的儲存提供者。  

 -   **要註冊憑證的裝置**：如果憑證設定檔部署至使用者集合，則選取只允許在使用者的主要裝置上，還是允許在使用者登入的所有裝置上註冊憑證。 如果憑證設定檔部署至裝置集合，則選取只允許裝置的主要使用者註冊，還是允許登入裝置的所有使用者註冊憑證。  

3.  在 [建立憑證設定檔精靈] 的 [憑證內容]  頁面上，指定下列資訊：  

 -   **憑證範本名稱**：按一下 [瀏覽]  以選取網路裝置註冊服務已設定使用，且已新增至發行 CA 的憑證範本名稱。 若要成功瀏覽至憑證範本，您執行 System Center Configuration Manager 主控台所使用的使用者帳戶必須具有憑證範本的 [讀取] 權限。 或者如果您無法使用 [瀏覽] ，請輸入憑證範本的名稱。  

 > [!IMPORTANT]
 >   
 >  如果憑證範本名稱包含非 ASCII 字元 (例如中文字母中的字元)，憑證將不會部署。 為確保憑證能順利部署，您必須在 CA 上建立憑證範本的複本，並使用 ASCII 字元重新命名該複本。  

   依據您是瀏覽到憑證範本還是輸入憑證名稱，請注意下列事項：  

 -   如果您瀏覽以選取憑證範本的名稱，頁面上的某些欄位會自動從憑證範本填入。 在某些情況下，除非您選擇不同的憑證範本，否則無法變更這些值。  

 -   如果您輸入憑證範本的名稱，請確定該名稱完全符合執行網路裝置註冊服務的伺服器之登錄中列出的其中一個憑證範本。 請確定您指定的是憑證範本的名稱，而非憑證範本的顯示名稱。  

   若要尋找憑證範本的名稱，請瀏覽至下列機碼：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP。 您將會看見憑證範本已列為 [EncryptionTemplate] 、[GeneralPurposeTemplate] 和 [SignatureTemplate] 的值。 根據預示，這三個憑證範本的值是 [IPSECIntermediateOffline] ，並對應至 [IPSec (Offline request)] 的範本顯示名稱。  

   > [!WARNING]  
   > 
   >  當您輸入憑證範本的名稱而非使用瀏覽方式時，因為 System Center Configuration Manager 無法確認憑證範本的內容，所以您可能會選取憑證範本不支援的選項，因而造成憑證要求失敗。 當發生此情況時，您將會在 CPR.log 檔案中看見 w3wp.exe 的錯誤訊息，表示憑證簽署要求 (CSR) 中的範本名稱與挑戰不相符。  
   >   
   >  當您輸入為 [GeneralPurposeTemplate]  值指定的憑證範本名稱時，您必須為此憑證設定檔選取 [金鑰編密]  和 [數位簽章]  選項。 不過，如果您只要在此憑證設定檔中啟用 [金鑰編密]  選項，請指定 [EncryptionTemplate]  金鑰的憑證範本名稱。 同樣地，如果您只要在此憑證設定檔中啟用 [數位簽章]  選項，請指定 [SignatureTemplate]  金鑰的憑證範本名稱。  

 -   **憑證類型**：選取憑證將部署至裝置或使用者。  
 -   **主體名稱格式**：從清單中選取 System Center Configuration Manager 自動在憑證要求中建立主體名稱的方式。 如果憑證是針對使用者，您也可以在主體名稱中包含使用者的電子郵件地址。 
    
   > [!NOTE]  
   > 
   > 選取 [IMEI 編號] 或 [序號] 可讓您區分相同使用者所擁有的不同裝置。 例如，這些裝置可能會共用一般名稱，但無法共用 IMEI 編號或序號。 如果裝置未報告 IMEI 編號或序號，憑證將以一般名稱核發。

 -   **主體別名**：指定 System Center Configuration Manager 在憑證要求中自動建立主體別名 (SAN) 值的方式。 舉例來說，如果您選擇使用者憑證類型，您可以在主體別名中包含使用者主體名稱 (UPN)。  如果用戶端憑證將用來驗證網路原則伺服器，您必須將主體別名設定成 UPN。  

   > [!NOTE]  
   >  - iOS 裝置在 SCEP 憑證中支援的主體名稱格式和主體別名受到限制。 如果您指定不支援的格式，憑證將不會在 iOS 裝置上註冊。 當您設定將 SCEP 憑證設定檔部署至 iOS 裝置時，請使用 [一般名稱]  作為 [主體名稱格式] ，並使用 [DNS 名稱] 、[電子郵件地址]  或 [UPN]  作為 [主體別名] 。  

 -   **憑證有效期間**：如果您已在發行 CA 上執行 certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE 命令以允許自訂有效期間，則可以指定憑證到期之前的剩餘時間長度。 如需這個命令的詳細資訊，請參閱 [System Center Configuration Manager 中的憑證基礎結構](../../protect/deploy-use/certificate-infrastructure.md)主題。  

   您可以指定一個比憑證範本中指定之有效期間更低，而不是更高的值。 舉例來說，如果憑證範本中的憑證有效期間為兩年，您可以指定一年而不是五年的值。 該值也必須低於發行 CA 憑證的剩餘有效期。  

 -   **金鑰使用方法**：指定憑證的金鑰使用方法選項。 您可以選擇下列選項：  

        -   **金鑰編密**：只允許在金鑰加密後交換金鑰。  

        -   **數位簽章**：只允許在以數位簽章協助保護金鑰後交換金鑰。  

   如果您是利用 [瀏覽] 選取憑證範本，除非選取不同的憑證範本，您可能無法變更這些設定。  

   您選取的憑證範本必須使用上述兩種金鑰使用方法選項或其中一種進行設定。 如果不是，您會在憑證註冊點記錄檔 **Crp.log** 中看到訊息 **CSR 與挑戰的金鑰使用方式不相符**。  


   -   **金鑰大小 (位元)**：選取金鑰大小 (以位元為單位)。  

   -   **擴充金鑰使用方法**：按一下 [選取] 以新增憑證使用目的值。 在大部分情況下，憑證需要 [用戶端驗證]  ，使用者或裝置才能向伺服器進行驗證。 不過，您可以視需要新增任何其他金鑰使用方式。  


   -   **雜湊演算法**：選取其中一種可用的雜湊演算法類型，以搭配此憑證使用。 選取連線中裝置所支援的最強安全性層級。  

   > [!NOTE]  
   > 
   >  **SHA-2** 支援 SHA-256、SHA-384 和 SHA-512。 **SHA-3** 只支援 SHA-3。  

   -   **根 CA 憑證**：按一下 [選取]  ，選擇您之前設定並部署到使用者或裝置的根 CA 憑證設定檔。 此 CA 憑證必須是將發行憑證 (您在此憑證設定檔中設定) 之 CA 的根憑證。  

   > [!IMPORTANT]  
   >  如果您指定未部署到使用者或裝置的根 CA 憑證，System Center Configuration Manager 將不會起始您在此憑證設定檔中設定的憑證要求。  


##  <a name="specify-supported-platforms-for-the-certificate-profile"></a>指定憑證設定檔的支援平台  

1. 在 [建立憑證設定檔精靈] 的 [支援的平台]  頁面上，選取您要安裝憑證設定檔的作業系統。 或者，按一下 [全選]  將憑證設定檔安裝到所有可用的作業系統。
2. 檢閱精靈的 [摘要] 頁面，並選擇 [完成]。 
 
 
新的憑證設定檔會出現在 [資產與相容性] 工作區的 [憑證設定檔] 節點，隨時可供部署到使用者或裝置 (如[如何在 System Center Configuration Manager 中部署設定檔](deploy-wifi-vpn-email-cert-profiles.md)中所述)。  