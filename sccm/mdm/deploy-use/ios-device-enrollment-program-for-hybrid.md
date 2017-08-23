---
title: "使用裝置註冊計劃 (DEP) 註冊 iOS 裝置 - Configuration Manager | Microsoft Docs"
description: "啟用 iOS 裝置註冊計畫 (DEP) 註冊，以使用 Intune 進行 Configuration Manager 混合式部署。"
ms.custom: na
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78d44adc-9b1c-4bc6-b72d-e93873916ea6
caps.latest.revision: "9"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: e76e46ce0d6ee0582d5161709ff114b936ac5660
ms.sourcegitcommit: db7b7ec347638efd05cdba474e8a8f8535516116
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2017
---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>適用於 Configuration Manager 混合式部署的 iOS 裝置註冊計畫 (DEP) 註冊

適用於：System Center Configuration Manager (最新分支)

公司可以透過 Apple 的裝置註冊計畫，購買 iOS 裝置，並使用 Microsoft Intune 進行管理。 若要使用 Apple 裝置註冊程式 (DEP) 來管理公司所擁有的 iOS 裝置，公司必須完成和 Apple 參與此計畫的步驟，並透過該計畫取得裝置。 下列網址提供該程序的詳細資訊：  [https://deploy.apple.com](https://deploy.apple.com)來管理它們。 這個方案的優點包括裝置自動安裝，而不需要透過 USB 將每部裝置連線到電腦。  

 在您以 DEP 註冊公司所擁有的 iOS 裝置之前，您需要從 Apple 取得 DEP 權杖。 此權杖可讓 Intune 同步處理貴公司所擁有的 DEP 參與裝置資訊。 它也讓 Intune 得以將註冊設定檔上傳至 Apple，並將這些設定檔指定給裝置。  

## <a name="apple-dep-enrollment-for-ios-devices"></a>適用於 iOS 裝置的 Apple DEP 註冊  
 下列程序說明如何將透過 Apple DEP 購買的 iOS 裝置指定為受 Intune 管理的屬公司所擁有之裝置。 當使用者第一次啟動裝置電源時，即會收到 DEP 管理設定檔，並執行設定輔助程式，以使裝置受到管理。  

##  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>啟用搭配 Intune 之 Configuration Manager 中的 DEP 註冊  

1.  **開始使用 Configuration Manager 管理 iOS 裝置**   
    您必須先完成[設定混合式行動裝置管理](../../mdm/deploy-use/setup-hybrid-mdm.md)的步驟 (包括[支援 iOS 註冊的步驟](../deploy-use/enroll-hybrid-ios-mac.md)) 之後，才能註冊 iOS 裝置註冊計畫 (DEP) 的裝置。
2.  **建立 DEP 權杖要求**   
    在 Configuration Manager 主控台的 [系統管理] 工作區中，依序展開 [階層設定]、[雲端服務]，然後按一下 [Microsoft Intune 訂閱]。 在 [首頁] 索引標籤上按一下 [建立 DEP 權杖要求]，按一下 [瀏覽] 指定 DEP 權杖要求的下載位置，然後按一下 [下載]。 將 DEP 權杖要求 (.pem) 檔案儲存在本機。 這個 .pem 檔案會用於向 Apple 裝置註冊計畫入口網站要求信任的權杖 (.p7m)。  
3.  **取得裝置註冊計畫權杖**   
    移至 [裝置註冊計畫入口網站](https://deploy.apple.com) (https://deploy.apple.com) ，並使用公司的 Apple ID 登入。 未來必須使用這個 Apple 識別碼來更新 DEP 權杖。  
    1.  在[裝置註冊計畫入口網站](https://deploy.apple.com)中，移至 [裝置註冊計畫] > [管理伺服器]，然後按一下 [新增 MDM 伺服器]。  
    2.  輸入 [MDM 伺服器名稱] ，然後按一下 [下一步] 。 伺服器名稱可用於識別 MDM 伺服器。 它不是 Intune 或 Configuration Manager 伺服器的名稱或 URL。  
    3.  [新增 <伺服器名稱\>] 對話方塊隨即開啟。 按一下 [選取檔案...]  上傳您在上一個步驟建立的 .pem 檔案，然後按一下 [下一步]。  
    4.  [新增 <伺服器名稱\>] 對話方塊會顯示 [您的伺服器權杖] 連結。 將伺服器權杖 (.p7m) 檔案下載到您的電腦，然後按一下 [完成] 。  

     此憑證 (.p7m) 檔案會用於建立 Intune 與 Apple 裝置註冊程式伺服器之間的信任關係。  
4.  **將 DEP 權杖新增至 Configuration Manager**   
    在 Configuration Manager 主控台的 [系統管理] 工作區中，展開 [階層設定]，然後按一下 [Microsoft Intune 訂閱]。 在 [首頁] 索引標籤上按一下 [設定平台]，然後按一下 [iOS]。 選取 [啟用裝置註冊計畫] ，瀏覽至憑證 (.p7m) 檔案，依序按一下 [開啟]、[上傳] 及 [確定]。  

## <a name="add-a-corporate-device-enrollment-policy"></a>新增公司的裝置註冊原則  

1. 在 Configuration Manager 主控台的 [資產與相容性] 工作區中，依序展開 [概觀]、[公司擁有的所有裝置]、[iOS]，然後按一下 [註冊設定檔]。 在 [首頁] 索引標籤上按一下 [建立設定檔]，開啟 [建立設定檔精靈]。 在下列頁面上設定：  
2. 在 [一般]  頁面上指定下列資訊，然後按 [下一步] 。  
  -   **名稱** - 裝置註冊設定檔的名稱。 (使用者看不到)  
  -   **描述** - 裝置註冊設定檔的描述。 (使用者看不到)  
  -   **使用者親和性** – 指定裝置的註冊方式。 請參閱 [User affinity for hybrid managed devices in Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md) (Configuration Manager 中針對混合式受管理裝置的使用者親和性)。  

      -  **提示輸入使用者親和性**：該裝置必須在初始設定期間關聯到使用者，以便之後能夠以該使用者的身分存取公司資料及傳送電子郵件。  應針對使用者所擁有且需要使用公司入口網站 (如安裝 App) 之受 DEP 管理的裝置設定使用者親和性。  
      > [!NOTE]
      > 設有使用者親和性的 DEP 必須啟用 WS-Trust 1.3 使用者名稱/混合端點，才能要求使用者權杖。

      -   **沒有使用者親和性**：該裝置不會關聯到使用者。 針對執行工作而不需存取本機使用者資料的裝置，請使用此關係。 需要使用者關係的 App 會無法運作。  
    ![DEP 設定檔名稱、描述及使用者親和性提示的螢幕擷取畫面](../media/dep-general.png)

3. 在 [裝置註冊計劃設定] 頁面上，指定下列資訊，然後按一下 [下一步]。  
    -   **部門**：使用者在啟用期間點選 [About Configuration]\(關於設定) 時，會顯示這項資訊。  
    -   **支援電話號碼**：使用者在啟用期間按一下 [需要協助] 按鈕時顯示。
       ![將 DEP 設定檔指派給 iOS 裝置的螢幕擷取畫面](../media/dep-settings.png)

    - **準備模式**：在啟用期間會設定此狀態，而且需要將裝置重設為出廠預設值才能進行變更︰  
        -   **不受監督** - 有限的管理功能。  
        -   **受監督** - 啟用更多管理選項，並且預設會停用 [啟用鎖定]。  
    - **鎖定裝置的註冊設定檔**：在啟用期間會設定此狀態，而且需要重設為出廠預設值才能進行變更。  
      -   **停用** - 允許從 [設定] 功能表中移除管理設定檔。  
      -   **啟用** - (需要**準備模式** = **受監督**) 停用允許移除管理設定檔的 iOS 設定  

4.  在 [設定助理] 頁面，設定為可自訂 [iOS 設定助理] 在一開啟裝置電源時就啟動，然後按 [下一步]。 這些設定包括：  
  -   **密碼** - 在啟用期間提示輸入密碼。 除非裝置會受到保護，或以其他方式控制存取 (例如，將裝置限制為單一應用程式的 Kiosk 模式)，否則一律需要密碼。  
  -   **定位服務** - 啟用時，設定輔助程式會在啟用期間提示服務。  
  -   **還原** - 啟用時，設定輔助程式會在啟用期間提示 iCloud 備份。  
  -   **Apple ID** - 若要下載 iOS App Store 應用程式 (包含 Intune 所安裝的應用程式)，您必須提供 Apple ID。 啟用時，如果 Intune 嘗試不使用 Apple ID 來安裝應用程式，iOS 會提示使用者輸入 Apple ID。  
  -   **條款及條件** - 啟用時，設定輔助程式會在啟用期間提示使用者接受 Apple 的條款及條件。  
  -   **Touch ID** - 啟用時，設定助理會在啟用期間提示此服務
  -   **Apple Pay** - 啟用時，設定助理會在啟用期間提示此服務
  -   **縮放** - 啟用時，設定助理會在啟用期間提示此服務
  -   **Siri** - 啟用時，設定輔助程式會在啟用期間提示此服務。  
  -   **傳送診斷資料給 Apple** - 啟用時，設定輔助程式會在啟用期間提示此服務。  
    ![將 DEP 設定檔指派給 iOS 裝置的螢幕擷取畫面](../media/dep-setup-assistant.png)
5.  在 [其他管理] 頁面上，指定其他管理設定是否可以使用 USB 連線。 當您選取 [需要憑證] ，您就必須匯入為了此設定檔而使用的 Apple Configurator 管理憑證。  設為 [不允許] 時，可防止使用 iTunes 同步處理檔案或透過 Apple Configurator 進行管理。 Microsoft 建議您選擇 [不允許]，並從 Apple Configurator 匯出任何進一步設定，然後將其部署為自訂 iOS 組態設定檔，而不是使用此設定來允許進行手動部署 (不論是否使用憑證)。  

  -   **不允許** - 防止裝置透過 USB 進行通訊 (停用配對)。  
  -   **允許** - 允許裝置透過任何電腦或 Mac 的 USB 連線進行通訊。  
  -   **需要憑證** - 允許使用匯入註冊設定檔的憑證與 Mac 配對。  

## <a name="assign-dep-devices-for-management"></a>指派要管理的 DEP 裝置

1. 移至 [裝置註冊計畫入口網站](https://deploy.apple.com) (https://deploy.apple.com) ，並使用公司的 Apple ID 登入。
2. 移至 [部署計畫] > [裝置註冊計畫] > [管理裝置]。 指定您 [Choose Devices (選擇裝置)] 的方式、提供裝置資訊，並利用裝置的 [序號]、[訂單號碼] 或 [上傳 CSV 檔案] 來指定詳細資料。 接著，選取 [指派給伺服器]，選取您在步驟 3 指定的 [<*伺服器名稱*>]，然後按一下 [確定]。  

3.  **同步處理 DEP 管理的裝置**   
    在 [資產與相容性] 工作區中，前往 [公司擁有的所有裝置] > [預先宣告的裝置]。 在 [首頁] 索引標籤上，按一下 [DEP 同步處理] 。 同步處理要求會傳送至 Apple。 同步處理完成之後，會顯示 DEP 管理的裝置。

    > [!NOTE]
    > 使用混合式設定時，在 Configuration Manager 主控台中，按一下 [DEP 同步處理] 可手動觸發 DEP 同步處理作業。

4.  **指派 DEP 設定檔**<br>在 [資產與相容性] 工作區中，前往 [公司擁有的所有裝置] > [iOS] > [註冊設定檔]。 選取 DEP 註冊設定檔，然後在 [首頁] 索引標籤中，按一下 [指派給裝置]。 選取將使用此註冊設定檔的裝置，按一下 [新增]，然後按一下 [確定]。   
     ![將 DEP 設定檔指派給 iOS 裝置的螢幕擷取畫面](../media/dep-assign-profile.png)

## <a name="distribute-devices-to-users"></a>將裝置散發給使用者
現在您可以將公司所擁有的裝置提供給使用者。 受管理裝置的 [註冊狀態]  會顯示為 **未連線** ，直到裝置開機並執行 [設定助理] 來註冊該裝置為止。 當 iOS 裝置開機時，就會加以註冊交由 Intune 管理。
