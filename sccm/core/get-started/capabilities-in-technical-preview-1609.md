---
title: "Technical Preview 1609 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1609 版中可用的功能。"
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
caps.latest.revision: "2"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 89a41c8a3137d0e54011ddf9a1d9b4894ecb7df8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1609-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1609 中的功能

適用於︰System Center Configuration Manager (Technical Preview)



本文介紹 System Center Configuration Manager Technical Preview 1609 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。      安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    

**此 Technical Preview 的已知問題：**  
*  當您更新至 Configuration Manager 1609 Technical Preview 時，將會刪除任何您已部署的版本升級原則。 若要繼續使用這些原則，您必須重新建立並部署這些原則。


**以下是您可以使用此版本試用的新功能。**  

## <a name="improvements-to-endpoint-protection"></a>Endpoint Protection 的改進
Endpoint Protection 反惡意程式碼原則設定的改進 - 您現在可以指定 Endpoint Protection 雲端保護服務將封鎖可疑檔案的層級。 這項新設定可讓系統管理員根據所遇到的大量惡意程式碼，指定「具風險」的電腦。

## <a name="increased-number-of-enrolled-devices"></a>增加已註冊裝置的數目
系統管理員現在可讓使用者在混合式行動裝置管理中，向 Intune 註冊最多 15 部裝置。 之前每位使用者僅限 5 部裝置。

## <a name="additional-apple-dep-settings"></a>其他 Apple DEP 設定

系統管理員現在可以在適用於 iOS 和 Mac 裝置的 DEP 設定檔中，設定下列 Apple 裝置註冊方案 (DEP) 設定：
- **Touch ID**
- **縮放**
- **Siri**

啟用時，Apple 的設定助理會在裝置啟用期間提示此服務。

## <a name="integration-with-upgrade-analytics"></a>與 Upgrade Analytics 的整合

Upgrade Analytics 可讓您評估及分析裝置整備及與 Windows 10 的相容性，以更輕鬆順暢地進行升級。 整合 Upgrade Analytics 與 Configuration Manager 之後，您可以在 Configuration Manager 管理主控台中存取升級相容性資料，然後從裝置清單中設定要升級或修復的目標裝置。

您可以在 [Get started with Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) (開始使用 Upgrade Analytics) 中閱讀更多有關 Upgrade Analytics 的資訊。

## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Windows 10 VPN 混合式設定檔的原生連線類型

搭配使用 Configuration Manager 和 Intune 時，您現在可以在 Configuration Manager 主控台中不使用 OMA-URI，以 Microsoft Automatic、IKEv2、PPTP 和 L2TP 連線類型建立 Windows 10 VPN 設定檔。

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>商務用 Windows 市集與 Configuration Manager 整合的改善

在此版本中，我們更新了[商務用 Windows 市集整合](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)並新增下列功能：

**更新︰**在最新版的 Technical Preview 中，立即同步處理功能無法運作。

- 之前，您只能從商務用 Windows 市集部署免費應用程式。 Configuration Manager 現在會另外支援部署付費線上授權應用程式 (僅適用已在 Intune 註冊的裝置)。
- 您現在可以起始商務用 Windows 市集與 Configuration Manager 之間的立即同步處理。
- 您現在可以修改從 Azure Active Directory 取得的用戶端秘密金鑰

### <a name="try-it-out"></a>試試看！

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>購買並同步付費線上授權應用程式

1. 從商務用 Windows 市集至少購買一個付費線上授權應用程式。
2. 在 Configuration Manager 主控台的 [管理] 工作區中，按一下 [雲端服務] > [更新與服務] > [商務用 Windows 市集]。
3. 在 [常用] 索引標籤的 [同步] 群組中，按一下 [立即同步]。
4. 不久，您所購買的應用程式就會出現在 [應用程式管理] 工作區的 [市集應用程式的授權資訊] 節點中。

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>從已同步處理的應用程式資料建立和部署 Configuration Manager 應用程式

從付費市集應用程式建立和部署 Configuration Manager 應用程式的程序，與從免費應用程式建立應用程式的程序一樣。 請參閱[使用 System Center Configuration Manager 管理從商務用 Windows 市集購買的應用程式](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)中的**從商務用 Windows 市集建立和部署 Configuration Manager 應用程式**一節。


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>從 Azure Active Directory 修改用戶端秘密金鑰

1. 在 Configuration Manager 主控台的 [管理] 工作區中，按一下 [雲端服務] > [更新與服務] > [商務用 Windows 市集]。
2. 選取您的商務用 Windows 市集帳戶，然後按一下 [內容]。
3. 在 [商務用 Windows 市集帳戶內容] 對話方塊的 [用戶端秘密金鑰] 欄位中，輸入新的金鑰，然後按一下 [驗證]。 驗證後，按一下 [套用]，然後關閉對話方塊。


## <a name="new-compliance-settings-for-configuration-items"></a>設定項目的新相容性設定

我們新增了許多新設定，可供您針對各種裝置平台在設定項目中使用。
這些是先前存在於 Microsoft Intune 獨立設定中的設定，現在當您搭配使用 Intune 和 Configuration Manager 時可以使用這些設定。
如果您需要任何設定的說明，請開啟[透過 Microsoft Intune 原則管理裝置上的設定和功能](https://docs.microsoft.com/en-us/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies)，然後選取所需平台的設定子主題。


### <a name="new-settings-for-android-devices"></a>Android 裝置的新設定

#### <a name="password-settings"></a>密碼設定

- **記住密碼歷程記錄**
- **允許指紋解除鎖定**

#### <a name="security-settings"></a>安全性設定

- **儲存卡需要加密**
- **允許螢幕擷取**
- **允許提交診斷資料**

#### <a name="browser-settings"></a>瀏覽器設定

- **允許網頁瀏覽器**
- **允許自動填入**
- **允許快顯封鎖程式**
- **允許 Cookie**
- **允許動態指令碼處理**

#### <a name="app-settings"></a>應用程式設定

- **允許 Google Play 商店**

#### <a name="device-capability-settings"></a>裝置功能設定

- **允許卸除式存放裝置**
- **允許 Wi-Fi 網際網路共用功能**
- **允許使用地理位置**
- **允許 NFC**
- **允許藍芽**
- **允許語音漫遊**
- **允許數據漫遊**
- **允許 SMS/MMS 傳訊**
- **允許語音助理**
- **允許語音撥號**
- **允許複製並貼上**


### <a name="new-settings-for-ios-devices"></a>iOS 裝置的新設定

#### <a name="password-settings"></a>密碼設定

- **密碼所需的複合字元數**
- **允許簡單密碼**
- **在非使用狀態幾分鐘後需要輸入密碼**
- **記住密碼歷程記錄**

### <a name="new-settings-for-mac-os-x-devices"></a>Mac OS X 裝置的新設定

#### <a name="password-settings"></a>密碼設定

- **密碼所需的複合字元數**
- **允許簡單密碼**
- **記住密碼歷程記錄**
- **在非使用狀態幾分鐘後啟用螢幕保護**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Windows 10 Desktop 與行動裝置版裝置的新設定

#### <a name="password-settings"></a>密碼設定

- **字元集數目下限**
- **記住密碼歷程記錄**
- **裝置從閒置狀態恢復時必須輸入密碼**

#### <a name="security-settings"></a>安全性設定

- **行動裝置需要加密**
- **允許手動取消註冊**

#### <a name="device-capability-settings"></a>裝置功能設定

- **允許透過行動數據使用 VPN**
- **允許透過行動數據進行 VPN 漫遊**
- **允許重設手機**
- **允許 USB 連線**
- **允許 Cortana**
- **允許行動中心通知**

### <a name="new-settings-for-windows-10-team-devices"></a>Windows 10 團隊版裝置的新設定

#### <a name="device-settings"></a>裝置設定

- **啟用 Azure Operational Insights**
- **啟用 Miracast 無線投影**
- **選擇要顯示在歡迎畫面上的會議資訊**
- **鎖定畫面背景圖片 URL**


### <a name="new-settings-for-windows-81-devices"></a>Windows 8.1 裝置的新設定

#### <a name="applicability-settings"></a>適用性設定

- **套用所有設定至 Windows 10**

#### <a name="password-settings"></a>密碼設定

- **必要的密碼類型**
- **字元集數目下限**
- **密碼長度下限**
- **重複登入失敗多少次之後抹除該裝置**
- **在非使用狀態幾分鐘後會關閉螢幕**
- **密碼到期 (天數)**
- **記住密碼歷程記錄**
- **不得重複使用以前用過的密碼**
- **允許圖片密碼和 PIN**

#### <a name="browser-settings"></a>瀏覽器設定

- **允許自動偵測內部網路**


### <a name="new-settings-for-windows-phone-81-devices"></a>Windows Phone 8.1 裝置的新設定

#### <a name="applicability-settings"></a>適用性設定

- **套用所有設定至 Windows 10**

#### <a name="password-settings"></a>密碼設定

- **字元集數目下限**
- **允許簡單密碼**
- **記住密碼歷程記錄**

#### <a name="device-capability-settings"></a>裝置功能設定

- **允許自動連線到免費的 Wi-Fi 熱點**


## <a name="improvements-for-boundary-groups"></a>界限群組的改進
此預覽版引進了界限群組及其如何與發佈點搭配使用的重要變更。 這些變更有助於簡化內容基礎結構的設計，同時讓您更充分掌控用戶端如何及何時進行後援，以搜尋其他發佈點作為內容來源位置。 這包括內部部署和雲端架構的發佈點。

這些改進將您可能很熟悉的現今概念和行為 (例如將發佈點設定為快速或低速)，取代成更容易設定和維護的新模型。 這些變更也是未來變更的基礎，未來變更將會改進要與界限群組關聯的其他站台系統角色。  

升級至 1609 版的期間，此升級會轉換您目前的界限群組設定以符合新的模型，讓這些變更不會干擾您的內容發佈設定 (請參閱[將現有的界限群組更新為新的模型](/sccm/core/get-started/capabilities-in-technical-preview-1609#bkmk_update))。

下列各節將詳細說明此預覽版所引進的變更、新模型的運作方式，以及升級已設定界限群組的站台時可預期的情況。



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>界限群組和內容位置的 UI 和行為變更
以下是界限群組及用戶端尋找內容方式的主要變更。 許多變更和概念會搭配運作。
-   **移除快速或低速的設定︰**您不會再將個別發佈點設定為快速或低速。  相反地，與界限群組相關聯的每個站台系統都會視為相同。 由於這項變更，界限群組內容的 [參考] 索引標籤不再支援快速或低速的設定。
-   **每個站台的新預設界限群組︰**每個主要站台都有新的預設界限群組，名為 ***Default-Site-Boundary-Group\<站台碼>***。  如果用戶端不在指派給界限群組的網路位置，該用戶端會從其指派的站台使用與預設群組相關聯的站台系統。 請規劃使用此界限群組，來取代後援內容位置的概念。    
 -  移除 [允許內容的後援來源位置]︰您無法再明確設定要用於後援的發佈點，而且已從 UI 移除此設定選項。

    此外，應用程式部署類型的 [允許用戶端使用內容的後援來源位置] 設定結果已變更。 部署類型的這項設定現在可讓用戶端使用預設站台界限群組作為內容來源位置。

 -  **界限群組關聯性︰**每個界限群組可以連結至一或多個額外的界限群組。 這些連結會形成關聯性，可在名為 [關聯性] 的新界限群組內容索引標籤上設定：
    -   直接與用戶端建立關聯的每個界限群組稱為**目前**界限群組。  
    -   用戶端因其「目前」界限群組與另一個群組之間的關聯而可以使用的任何界限群組，稱為**芳鄰**界限群組。
    -  它位於 [關聯性] 索引標籤上，您可以在其中新增界限群組以作為「芳鄰」界限群組。 您也可以設定時間 (以分鐘為單位)，以決定若使用者無法從「目前」群組中的發佈點找到內容，將於何時從這些「芳鄰」界限群組開始搜尋內容位置。

        當您新增或變更界限群組設定時，您可以選擇防止您設定的目前群組切換回該特定界限群組。

    若要使用新的設定，您可以定義從一個界限群組到另一個界限群組的明確關聯 (連結)，並將該關聯群組中的所有發佈點設定為相同的時間 (以分鐘為單位)。 您設定的時間會決定若用戶端無法從其「目前」界限群組找到內容，可於何時從該芳鄰界限群組開始搜尋內容來源。

    除了明確設定的界限群組之外，每個界限群組還有預設站台界限群組的隱含連結。 此連結會在 120 分鐘後開始生效，此時預設站台界限群組會成為芳鄰界限群組，讓用戶端可使用與該界限群組相關聯的發佈點作為內容來源位置。

    此行為會取代先前稱為內容後援的行為。  您可以覆寫此 120 分鐘的預設行為，方法是將預設站台界限群組明確關聯至「目前」群組，然後以分鐘為單位設定特定時間，或完全封鎖以防止使用後援。


-   **用戶端嘗試從每個發佈點取得內容，最多 2 分鐘︰**當用戶端搜尋內容來源位置時，它會嘗試存取一個發佈點 2 分鐘，再嘗試另一個發佈點。 這是舊版的一項變更，在舊版中，用戶端會嘗試連線到發佈點，最多 2 小時。

    - 用戶端嘗試使用的第一個發佈點，是從用戶端的「目前」界限群組 (或群組) 中可用的發佈點集區隨機選取而來。

    - 如果用戶端在兩分鐘後還找不到內容，則會切換至新的發佈點，並嘗試從該伺服器取得內容。 此程序會每隔兩分鐘重複一次，直到用戶端找到內容或到達其集區中最後一部伺服器為止。

    - 如果用戶端在必須切換回「芳鄰」界限群組之前，從其「目前」集區找不到有效的內容來源位置，則用戶端會將該「芳鄰」群組中的發佈點新增至其目前清單結尾，然後搜尋包含兩個界限群組之發佈點的擴充來源位置群組。

        > [!TIP]  
        > 如果您建立從目前界限群組到預設站台界限群組的明確連結，並定義比連結至芳鄰界限群組的後援時間更短的後援時間，用戶端在包含芳鄰群組之前，會先從預設站台界限群組開始搜尋來源位置。

    - 當用戶端無法從集區中的最後一部伺服器取得內容時，就會重新開始此程序。


### <a name="how-the-new-model-works"></a>新模型的運作方式
當您設定界限群組時，您可以將界限 (網路位置) 和站台系統角色 (例如發佈點) 關聯至界限群組。 這可協助將用戶端連結至站台系統伺服器，例如位於網路上用戶端附近的發佈點。   
-   您可以將相同的界限指派給多個界限群組
-   站台系統伺服器 (例如發佈點) 可以關聯至多個界限群組，以提供給更廣泛的網路位置使用
-   如果發佈點未關聯至界限群組，用戶端將無法使用該發佈點作為內容來源位置。

從此 Technical Preview 開始，您可以定義界限群組關聯性，以設定內容來源位置的後援行為。 此新行為是在界限群組內容的新 [關聯性] 索引標籤上設定，不會再將站台系統設定為低速或快速，而是設定界限群組以允許內容的後援來源位置。

在 [關聯性] 索引標籤上，您可以新增其他界限群組，以設定這些群組的關聯性。 每個關聯性都是從**目前**界限群組到您新增之界限群組 (稱為**芳鄰**) 的單向連結。 針對您建立的每個連結，您可以設定具有後援時間 (以分鐘為單位) 的發佈點。 如果用戶端無法從其目前界限群組找到有效的內容來源位置，此時間可用來決定用戶端在「目前」界限群組中經過多久，才可以開始使用「芳鄰」界限群組中的發佈點。

當用戶端找不到內容並從芳鄰界限群組開始搜尋位置時，它會以控制的方式為用戶端增加集區中的可用發佈點數目。  

-   界限群組可以有多個關聯性。 這可讓您設定在不同的期間後切換回不同的芳鄰。
-   用戶端只會切換回其目前界限群組的直接芳鄰界限群組。
-   當用戶端是多個界限群組的成員時，目前界限群組會定義為該用戶端的所有界限群組聯集。  該用戶端接著可切換回任何原始界限群組的芳鄰。

除了您定義的連結之外，還會在您建立的界限群組與針對每個站台自動建立的預設界限群組之間，自動建立一個隱含連結。 此自動連結：
-   可供不在與您階層中任何界限群組相關聯之界限上的用戶端使用，這些用戶端會自動使用其指派站台中的預設界限群組，來識別有效的內容來源位置。   
-   為預設後援選項，會在 120 分鐘後從目前界限群組切換回站台預設界限群組。

**使用新模型的範例︰**     
您將建立不共用界限或站台系統伺服器三個界限群組：
-   群組 BG_A，以及與該群組相關聯的發佈點 DP_A1 和 DP_A2
-   群組 BG_B，以及與該群組相關聯的發佈點 DP_B1 和 DP_B2
-   群組 BG_C，以及與該群組相關聯的發佈點 DP_C1 和 DP_C2

您會將用戶端的網路位置只新增至 BG_A 界限群組作為界限，接著您會設定從該界限群組到其他兩個界限群組的關聯性：
-   您將設定要在 10 分鐘後使用之第一個「芳鄰」群組 (BG_B) 中的發佈點。 此群組包含發佈點 DP_B1 和 DP_B2。 這兩者會適當地連線到第一個群組界限位置。
-   您將設定要在 20 分鐘後使用的第二個「芳鄰」 群組 (BG_C)。 此群組包含發佈點 DP_C1 和 DP_C2。 這兩者來自其他兩個界限群組並跨 WAN。
-   您也會將位於站台伺服器上的另一個發佈點新增至站台預設站台界限群組。 這是您最少使用的內容來源位置，但它位於所有界限群組的中央。

    界限群組和後援時間的範例：

     ![BG_Fallack](media/BG_Fallback.png)


使用下列設定：
-   用戶端會從其「目前」界限群組 (BG_A) 中的發佈點開始搜尋內容，搜尋每個發佈點兩分鐘，再切換到界限群組中的下一個發佈點。 有效內容來源位置的用戶端集區包含 DP_A1 和 DP_A2。
-   如果用戶端從其「目前」界限群組搜尋 10 分鐘後找不到內容，則會在其搜尋中新增 BG_B 界限群組中的發佈點。 接著會從其結合之發佈點集區中的發佈點繼續搜尋內容，該集區現在包含 BG_A 和 BG_B 界限群組中的發佈點。 用戶端會繼續花兩分鐘的時間連絡每個發佈點，再切換到其集區中的下一個發佈點。 有效內容來源位置的用戶端集區包含 DP_A1、DP_A2、DP_B1 和 DP_B2。
-   如果用戶端在延長的 10 分鐘 (20 分鐘) 後仍然找不到具有內容的發佈點，它會擴充其可用的發佈點集區，加入第二個「芳鄰」群組 (界限群組 BG_C) 中的發佈點。 用戶端現在有 6 個發佈點可供搜尋 (DP_A1、DP_A2、DP_B2、DP_B2、DP_C1 和 DP_C2)，而且會繼續每隔兩分鐘變更為新的發佈點，直到找到內容為止。
-   如果用戶端在總計 120 分鐘後找不到內容，就會切換回加入「預設站台界限群組」作為其繼續搜尋的一部分。 現在，發佈點集區包含已設定之三個界限群組中的所有發佈點，而且最後一個發佈點位於站台伺服器電腦上。  用戶端接著會繼續搜尋內容，每隔兩分鐘變更發佈點一次，直到找到內容為止。

藉由設定在不同的時間使用不同的芳鄰群組，您就可以控制何時將特定發佈點新增為內容來源位置，以及用戶端何時或是否會使用後援當做防護機制，以在任何其他位置都沒有內容時切換回預設站台界限群組。


### <a name="bkmk_update"></a>將現有的界限群組更新為新的模型
當您安裝 1609 版並更新站台時，會自動進行下列設定。 這些設定是為了確保您目前的後援行為在您設定新的界限群組和關聯性之前維持可用。  
-   站台上未受保護的發佈點會新增至該站台的 *Default-Site-Boundary-Group\<站台碼>* 界限群組。
-   系統會為每個現有的界限群組建立一個複本，其中包含設定為低速連線的站台伺服器。 新群組的名稱是 ***\<原始界限群組名稱>-Slow-Tmp***：  
    -   原始界限群組中會保留使用快速連線的站台系統。
    -   使用低速連線的站台系統複本會新增至界限群組複本。 設定為慢速的原始站台系統會在原始界限群組中保留供回溯相容性，但不會從該界限群組中使用。
    -   此界限群組複本沒有相關聯的界限。 不過，原始群組與後援時間設定為零的新界限群組複本之間，會建立一個後援連結。

 下表指出結合原始部署設定與發佈點設定之後，您可以預期的新後援行為：

低速網路中之 [不要執行程式] 的原始部署設定  |[允許用戶端使用內容的後援來源位置] 的原始發佈點設定  |新的後援行為  
---------|---------|---------
已選取     |  已選取    |  **沒有後援** - 只使用目前界限群組中的發佈點       
已選取     |  未選取|  **沒有後援** - 只使用目前界限群組中的發佈點       
未選取 |  未選取|  **切換回芳鄰** - 使用目前界限群組中的發佈點，然後新增芳鄰界限群組中的發佈點。 除非設定預設站台界限群組的明確連結，否則用戶端不會切換回該群組。    
未選取 | 已選取     |   **標準後援** - 先使用目前界限群組中的發佈點，再使用芳鄰和站台預設界限群組中的發佈點

 所有其他部署設定都會導致**標準後援**。  



## <a name="office-365-client-management-dashboard"></a>Office 365 用戶端管理儀表板  
Configuration Manager 1609 Technical Preview 引進了新的儀表板。 若要檢視此儀表板，請在 Configuration Manager 主控台中，移至 [軟體程式庫] > [概觀] > [Office 365 用戶端管理]。
>[!NOTE]
>在 Configuration Manager 主控台的 [新增功能] 工作區中，此新儀表板錯誤命名為 **Office 365 服務儀表板**。

此儀表板會顯示下列圖表：

- Office 365 用戶端數目
- Office 365 用戶端版本
- Office 365 用戶端語言
- Office 365 用戶端通道     
如需詳細資訊，請參閱 [Office 365 ProPlus 更新通道的概觀](https://technet.microsoft.com/library/mt455210.aspx)。
- 在可用產品集合中選取 Office 365 用戶端的自動部署規則。

您可以在此儀表板上執行下列動作：
- 使用儀表板頂端的 [集合] 下拉式清單設定，依特定集合成員篩選儀表板資料。
- 在儀表板右上方，按一下 [Office 365 Installer] 啟動 [Office 365 用戶端安裝精靈]，將 Office 365 應用程式部署至用戶端。 如需詳細資訊，請參閱[將 Office 365 應用程式部署至用戶端](#deploy-office-365-apps-to-clients)。
- 在儀表板中間右邊，按一下 [建立 ADR] 開啟 [自動部署規則精靈]，以建立新的自動部署規則 (ADR)。 若要建立適用於 Office 365 應用程式的 ADR，請在選擇產品時選取 [Office 365 用戶端]。 如需詳細資訊，請參閱[自動部署軟體更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)。
- 在儀表板右下方，按一下 [Create Client Agent Settings]\(建立用戶端代理程式設定) 開啟用戶端代理程式設定。 如需詳細資訊，請參閱[關於用戶端設定](/sccm/core/clients/deploy/about-client-settings)。



如需 Office 365 ProPlus 更新的詳細資訊，請參閱[使用 Configuration Manager 管理 Office 365 ProPlus 更新](/sccm/sum/deploy-use/manage-office-365-proplus-updates)。

## <a name="deploy-office-365-apps-to-clients"></a>將 Office 365 應用程式部署至用戶端
在此版本中，您可以從 [Office 365 用戶端管理] 儀表板啟動 Office 365 Installer，以便設定 Office 365 安裝設定、從 Office 內容傳遞網路 (CDN) 下載檔案，並在 Configuration Manager 中將檔案當做應用程式來部署。

### <a name="limitations-of-office-365-deployment"></a>Office 365 部署的限制
- 當您嘗試在 [Office 365 應用程式安裝精靈] 中匯入現有的用戶端設定 (XML) 時，可能會發生問題。 您可以手動設定用戶端設定，而不會發生問題。

#### <a name="to-deploy-office-365-apps-to-clients"></a>將 Office 365 應用程式部署至用戶端
1. 在 Configuration Manager 主控台中，巡覽至 [軟體程式庫] > [概觀] > [Office 365 用戶端管理]。
2. 按一下右上方窗格中的 [Office 365 Installer]。 [Office 365 用戶端安裝精靈] 隨即開啟。
3. 在 [應用程式設定] 頁面上，提供應用程式的名稱和描述，輸入檔案的下載位置，然後按一下 [下一步]。 請注意，您必須使用 &#92;&#92;*server*&#92;*share* 格式來指定位置。
4. 在 [匯入用戶端設定] 頁面上，選擇要從現有的 XML 組態檔匯入 Office 365 用戶端設定，還是要手動指定設定，然後按一下 [下一步]。
如果您有現成的組態檔，請輸入檔案的位置，然後跳至步驟 7。 請注意，您必須使用 &#92;&#92;*server*&#92;*share*&#92;*檔案名稱*.XML 格式來指定位置。

    > [!IMPORTANT]
    >當您嘗試在此 Technical Preview 中匯入現有的用戶端設定 (XML) 時，可能會發生問題。

5. 在 [Client Products]\(用戶端產品) 頁面上，依序選取您使用的 Office 365 套件、要包含的應用程式、應包含的任何其他 Office 產品，然後按一下 [下一步]。
6. 在 [用戶端設定] 頁面上，選擇要包含的設定，然後按一下 [下一步]。
7. 在 [部署] 頁面上，選擇是否要部署應用程式，然後按一下 [下一步]。
如果您選擇不要在精靈中部署套件，請跳至步驟 9。
8. 設定精靈頁面的其餘部分，就像是一般應用程式部署一樣。 如需詳細資訊，請參閱[建立和部署應用程式](/sccm/apps/get-started/create-and-deploy-an-application)。
9. 完成精靈。
10. 您可以在 Configuration Manager 中，從 [軟體程式庫] > [概觀] > [應用程式管理] > [應用程式] 部署或編輯應用程式，就像是任何其他應用程式一樣。

>[!NOTE]
>部署 Office 365 應用程式之後，您可以建立自動部署規則，以維護應用程式。 若要建立適用於 Office 365 應用程式的 ADR，請按一下 [Create an ADR]\(建立 ADR)，然後在選擇產品時選取 [Office 365 用戶端]。 如需詳細資訊，請參閱[自動部署軟體更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)。

## <a name="BKMK_UEFIConversion"></a>BIOS 轉換成 UEFI 的改進
您現在可以使用新變數 TSUEFIDrive 來自訂作業系統部署工作順序，如此一來，「重新啟動電腦」步驟就會在硬碟上準備用於轉換成 UEFI 的 FAT32 磁碟分割。 下列程序提供範例，說明如何建立工作順序步驟，以準備用於將 BIO 轉換成 UEFI 的硬碟。

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>若要準備用於轉換成 UEFI 的 FAT32 磁碟分割：
在安裝作業系統的現有工作順序中，您將新增具有執行 BIOS 轉換成 UEFI 之步驟的新群組。

1. 在擷取檔案和設定的步驟之後，以及安裝作業系統的步驟之前，建立新的工作順序群組。 例如，在 [擷取檔案和設定] 之後，建立名為 **BIOS-to-UEFI** 的群組。
2. 在新群組的 [選項] 索引標籤中，新增工作順序變數作為條件，其中 **_SMSTSBootUEFI** **不等於** **true**。 當電腦已在 UEFI 模式時，這會防止執行群組中的步驟。
![BIOS to UEFI 群組](media/BIOS-to-UEFI-group.png)
3. 在新群組底下，新增 [重新啟動電腦] 工作順序步驟。 在 [指定重新啟動後執行的項目] 中，選取 [指派給此工作順序的開機映像] 以在 Windows PE 中啟動電腦。  
4. 在 [選項] 索引標籤上，新增工作順序變數作為條件，其中 **_SMSTSInWinPE 等於 false**。 如果電腦已在 Windows PE 中，這會防止執行此步驟。

    ![重新啟動電腦步驟](media/Restart-in-Windows-PE.png)
5. 新增啟動 OEM 工具的步驟，以將韌體從 BIOS 轉換成 UEFI。 這通常會是 [執行命令列] 工作順序步驟，其中包含啟動 OEM 工具的命令列。
5.  新增 [格式化和分割磁碟] 工作順序步驟，對硬碟進行分割與格式化。 在此步驟中，執行下列動作：
    1.  安裝作業系統之前，先建立將轉換成 UEFI 的 FAT32 磁碟分割。 選擇 [GPT] 作為 [磁碟類型]。
    ![格式化和分割磁碟步驟](media/Format-and-partition-disk.png)
    2.  移至 FAT32 的 [磁碟分割內容]。 在 [變數] 欄位中輸入 **TSUEFIDrive**。 當工作順序偵測到此變數時，它會準備 UEFI 轉換，再重新啟動電腦。
    ![磁碟分割內容](media/Partition-properties.png)
    3. 建立工作順序引擎用來儲存其狀態及存放記錄檔的 NTFS 磁碟分割。
6.  新增 [重新啟動電腦] 工作順序步驟。 在 [指定重新啟動後執行的項目] 中，選取 [指派給此工作順序的開機映像] 以在 Windows PE 中啟動電腦。  




## <a name="intune-compliance-charts"></a>Intune 相容性圖表
在此版本中，您可以使用 Configuration Manager 主控台之 [監視] 工作區底下的新圖表，快速檢視裝置的整體相容性及不相容的主要原因。

#### <a name="to-view-the-intune-compliance-charts"></a>檢視 Intune 相容性圖表
1. 在 Configuration Manager 主控台中，移至 [監視] > [概觀] > [相容性設定]。
2. [Overall Device Compliance]\(整體裝置相容性) 圖表隨即顯示。
3. 按一下 [相容性原則] 節點，以檢視 [Overall Device Compliance]\(整體裝置相容性) 和 [Top Non-Compliance Reasons]\(不相容的主要原因) 圖表。

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>TP 1609 中的 Intune 相容性圖表限制
- 向下切入 [Overall Device Compliance]\(整體裝置相容性) 圖表目前會產生錯誤。
- [Top Non-Compliance Reasons]\(不相容的主要原因) 圖表會列出原則名稱，而不是個別不相容原因。 您可以按一下原則，向下切入並查看不符合該原則的裝置。

### <a name="try-it-out"></a>試試看
依序完成下列各節：

#### <a name="check-overall-compliance-chart"></a>查看 Overall Compliance (整體相容性) 圖表
1. 在 Configuration Manager 中新增兩個 iOS 相容性原則。 一個原則應該包含裝置的一組設定 (例如將 PIN 長度設定為 6)。 另一個原則應該包含另一組設定 (例如 PIN 複雜性)。 原則設定不應該重疊或互相衝突。
2. 將兩個原則部署給一組使用者。
3. 使用相同的使用者帳戶以及在上一個步驟中收到原則的帳戶，在 Intune 註冊兩部 iOS 裝置。 裝置不應符合相容性原則的準則。
4. 在 Configuration Manager 中，查看 [Overall Device Compliance]\(整體裝置相容性) 圖表。 這兩部裝置應報告為不相容。
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>查看 Top Non-compliance Reasons (不相容的主要原因) 圖表
5. 查看 [不相容的主要原因]\(Top Non-compliance Reasons) 圖表。 此圖表列出不相容的主要 5 個原因，但如果在不同的原則之間只設定兩個相容性設定，則只會顯示不相容的主要 2 個原因。
6. 按一下圖表中的其中一個區段。 這兩部裝置應該會出現在 [資產與相容性] > [概觀] > [裝置] 底下的篩選檢視中。

#### <a name="make-devices-compliant-and-check-the-charts"></a>將裝置設為相容並查看圖表
7. 將其中一部裝置設為符合其中一個原則。 再次查看 [Overall Device Compliance]\(整體裝置相容性) 圖表。 此圖表應該會顯示一部相容的裝置和一部不相容的裝置。
8. 將另一部裝置設為符合相同原則。 這會讓一部裝置符合兩個原則，而另一部裝置只符合其中一個原則。
9. 查看 [不相容的主要原因]\(Top Non-compliance Reasons) 圖表。 應該只會列出一個不相容的原因。
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>另請參閱
[System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)
