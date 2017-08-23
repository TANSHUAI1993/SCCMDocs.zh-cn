---
title: "Technical Preview 1601 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1601 版中可用的功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
caps.latest.revision: "7"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: ef0db5b11ae2be5edcb4db87400c5c273c89972e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1601-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1601 中的功能

適用於︰System Center Configuration Manager (Technical Preview)

本文介紹 System Center Configuration Manager Technical Preview 1601 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。      安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。  

 **此 Technical Preview 的已知問題：**  

-   當您管理 [用戶端更新選項] 以將生產階段前用戶端升級到生產環境時，核取方塊的文字會顯示用戶端版本為零 (0)，而不是實際的用戶端組建編號。 正確的實際執行前用戶端版本會顯示在此選項上方的介面上，而且是當您選取此選項時升級到實際執行環境的用戶端版本。  

-   升級到 Technical Preview 1601 並選擇測試生產階段前集合中的 Configuration Manager 用戶端時，將不會升級集合的用戶端套件。 此問題僅針對 Technical Preview 1601。  

     若要解決此問題，請執行下列其中一項操作：  

    -   在主要站台資料庫上執行下列 SQL 指令碼︰  

        ```  
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   將新發佈點站台系統角色新增到您的實驗室站台。 新發佈點將會以新的用戶端套件升級實際執行前集合。  

**以下是您可以使用此版本試用的新功能。**  

##  <a name="bkmk_hybrid1"></a> Microsoft Intune 整合的增強功能  
在 1601 Technical Preview 中，我們已新增下列功能的支援：  

### <a name="improvements-to-conditional-access"></a>條件式存取的增強功能  

-   **System Center Configuration Manager 所管理電腦的條件存取支援**  

     您現在可以設定 System Center Configuration Manager 所管理電腦的條件式存取原則，而且電腦必須符合相容性原則，才能存取 Exchange Online 和 SharePoint Online 服務。  運用這項新功能，您也可以透過相容性原則向 Azure AD 註冊電腦，以及監視和報告 Azure AD 註冊。  

    > [!NOTE]  
    >  Windows 10 尚未支援條件式存取。  

    以下是使用這項功能的先決條件：  

    -   Azure Active Directory Premium 訂閱和 ADFS Sync。  

    -   Microsoft Intune 訂閱。 應該在 Configuration Manager 主控台中設定 Microsoft Intune 訂閱。  

    -   [Azure AD 自動註冊的必要條件](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)。  

    若要使用這個選項，您必須在 Configuration Manager 中使用下面所述的特定規則來建立相容性原則，並在 Intune 主控台中設定條件式存取原則。  而且，若要確保只允許相容的電腦進行存取，您必須將 Windows 電腦需求設定為 [裝置必須符合規定] 選項。 以下是適用於 System Center Configuration Manager 所管理電腦的相容原則規則。  

    -   **需要 Azure ActiveDirectory 內的登錄：**這個規則會檢查使用者的裝置是否為加入 Azure AD 的工作區，如果沒有，則會在 Azure AD 中自動登錄裝置。 在 Windows 8.1 上才支援自動註冊。 在 Windows 7 電腦上，部署 MSI 以執行自動註冊。 如需詳細資訊，請參閱[這裡](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)。  

    -   **所有期限超過特定天數的已安裝必要更新：**這個規則會確認使用者的裝置在您指定的期限和寬限期內是否具有所有必要更新 (在**必要的自動更新**規則中指定)，並會自動安裝任何擱置的必要更新。  

    -   **需要 BitLocker 磁碟機加密：**這會確認裝置上的主要磁碟機 (例如 C:\\) 是否為 BitLocker 加密。 如果未在主要裝置上啟用 BitLocker 加密，則會封鎖存取電子郵件和 SharePoint 服務。  

    -   **需要反惡意程式碼：**這會確認是否已啟用並執行反惡意程式碼軟體 (僅限 System Center Endpoint Protection 或 Windows Defender)。  
         如果未啟用，則會封鎖存取電子郵件和 SharePoint 服務。  

    因不相容而封鎖的使用者將在 SCCM 軟體中心中檢視相容性資訊，並且將在修復相容性問題時起始新的原則評估。  

-   **條件存取與健康情況證明服務：**您現在可以根據健康情況證明服務所報告裝置的健康情況，來限制電子郵件和 0365 服務的存取。  此外，Intune 所管理的裝置包括在裝置健康情況報告中。  

    新的相容性規則已新增至 Configuration Manager 主控台，可讓您指定應該根據健康情況狀態來允許還是封鎖裝置的存取。  若要建立這個規則，請開啟 [建立相容性原則精靈]，並新增規則。  選取 [健康情況證明服務回報狀況良好] 作為條件，並將值設為 **True**。  這將確定只有報告為健康的裝置才能存取您的公司資源。 如需健康情況證明服務以及 Intune 中如何報告裝置健康情況的詳細資料，請參閱[裝置健康情況證明](#bkmk_devicehealth)。  

-   **新的相容性原則設定：**新的相容性原則設定有助於改善用來存取公司電子郵件和 SharePoint 服務之裝置上的安全性和保護：  

    -   **需要自動更新：**您可能需要具有 Windows 8.1 或更新版本的裝置才能允許自動安裝更新，也可以指定已安裝更新的類別。  您可以選擇僅安裝標示為重要的更新，或安裝所有建議的更新。  

         若要建立自動更新的規則，請開啟 [建立相容性原則精靈]，並新增規則。  選取 [所需更新的最小分類] 作為條件，並將值設為其中一個可用的值：[無]、[建議] 和 [重要]。  

        -   **無：**未自動安裝更新。  

        -   **建議：**安裝所有建議的更新  

        -   **重要：**僅安裝分類為重要的更新。  

    -   **需要密碼來解除鎖定行動裝置：**這個設定設為 [是] 時，使用者必須輸入密碼才能存取其裝置。  

         若要建立用來解除鎖定行動裝置之密碼的規則，請開啟 [建立相容性原則精靈]，並新增規則。 選取 [需要密碼才能將閒置的裝置解除鎖定] 作為條件，並將值設為 **True**。  

    -   **在非使用狀態幾分鐘後需要輸入密碼：**指定使用者必須重新輸入密碼之前的閒置時間。  

         若要建立這個規則，請開啟 [建立相容性原則精靈]，並新增規則。 選取 [在非使用狀態幾分鐘後需要輸入密碼] 作為條件，並將值設為其中一個可用選項：1 分鐘、5 分鐘、15 分鐘、30 分鐘、I 小時。  

-   **預設規則覆寫 - 一律允許已在 Intune 註冊且相容的裝置存取 Exchange 內部部署：**  

     如果您核取此選項，即允許已在 Intune 註冊並與相容性原則相容的裝置存取 Exchange 內部部署。 這個規則會覆寫 [預設規則]，這表示即使您將 [預設規則] 設為隔離或封鎖存取，已註冊且相容的裝置還是可以存取 Exchange 內部部署。  
     如果您想要已註冊且相容的裝置一律可以透過 Exchange 內部部署存取電子郵件，請使用這個設定。  

     支援的平台如下︰Windows Phone 8 和更新版本、iOS 6 和更新版本。 Android 4.0 和更新版本、Samsung KNOX Standard 4.0 和更新版本。  

     若要使用這個選項，請移至 Exchange 內部部署之 [設定條件存取原則精靈] 的 [一般] 頁面。  

##  <a name="bkmk_clientStatus"></a> 用戶端線上狀態  
從 Technical Preview 1601 開始，您在 Configuration Manager 主控台中可以一眼就看出用戶端在線上還是離線。 運用主控台裝置清單中已更新的圖示和資料行，您可以評估環境中用戶端的狀態，找出問題區域以及其他可能需要注意的問題。  

如果用戶端目前連線到 Configuration Manager 管理點站台系統角色，則用戶端在線上。 只要管理點接收來自用戶端的 ping 類似訊息，其狀態會是線上。 如果管理未接收訊息 5 分鐘左右，用戶端的狀態就會變更為離線。  

### <a name="icons-for-client-status"></a>用戶端狀態圖示  

|||  
|-|-|  
|![用戶端的線上狀態圖示](media/online-status-icon.png)|用戶端在線上。|  
|![用戶端的離線狀態圖示](media/offline-status-icon.png)|裝置離線。|  
|![用戶端的未知狀態圖示](media/unknown-status-icon.png)|用戶端狀態不明。|  

### <a name="prerequisites"></a>先決條件  
 用戶端線上狀態沒有先決條件。 只要安裝 Configuration Manager Technical Preview 1601，就可以開始使用它。  

### <a name="limitations"></a>限制  
 用戶端線上狀態僅適用於已安裝 Configuration Manager 用戶端的 Windows 的電腦。 Mac 電腦、Linux 或 UNIX 電腦或是使用內部部署行動裝置管理所管理的裝置不支援用戶端線上狀態。  

### <a name="to-view-client-online-status"></a>檢視用戶端線上狀態  

1.  在 Configuration Manager 主控台中，移至 [資產與相容性] > [概觀] > [裝置]。  

2.  在資料行標頭上按一下滑鼠右鍵，然後按一下其中一個用戶端線上狀態欄位，以將它新增至裝置檢視。 欄位如下：  

    -   **裝置線上狀態** 指出用戶端目前在線上還是離線。  

    -   [上次連線時間] 指出用戶端線上狀態從離線變更為線上的時間。  

    -   [上次離線時間] 指出用戶端線上狀態從線上變更為離線的時間。  

 若要顯示用戶端狀態最近的變更，請重新整理主控台。  

##  <a name="bkmk_appmgmt1601"></a> 應用程式管理的增強功能  
 在 1601 Technical Preview 中，我們已新增下列功能的支援：  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>管理大量採購的 iOS 裝置應用程式  
 某些應用程式市集可讓您購買多個您想要在公司內執行的應用程式授權。 這可協助您降低追蹤多個已購買之應用程式複本的管理開銷。  

 Configuration Manager 現在藉由從應用程式市集匯入授權資訊，可透過此種程式協助您管理購買的應用程式，並追蹤您已經使用了多少個授權。  

 如需詳細資訊，請參閱[使用 Configuration Manager 管理您透過大量採購方案購買的應用程式](https://technet.microsoft.com/library/mt627954.aspx)。  

### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS - 混合式應用程式的應用程式<br />設定  
 有些 iOS 應用程式支援預先設定的設定 (例如應用程式應該連線的伺服器或資料庫)。 Configuration Manager 現在支援將應用程式設定原則部署至裝置，而這些裝置可以讓使用者立即使用應用程式，而不需要知道這項資訊。 開發人員必須在其應用程式中啟用這項功能。  

 有限數目的公開發行應用程式目前支援預先設定的設定；您也可能有支援這些設定的內部開發企業營運應用程式。  

#### <a name="prerequisites-for-this-scenario"></a>這個案例的先決條件  

-   您必須已將 Microsoft Intune 訂閱新增至 Configuration Manager。  

-   您必須已將有效的 Apple APNs 憑證新增至 Intune 訂閱。  

-   您必須已部署支援應用程式設定的 iOS 應用程式。  

#### <a name="try-it-out"></a>試試看！  
 符合上述必要條件之後，您必須建立使用 iOS 部署類型的 Configuration Manager 應用程式。 您使用的應用程式必須支援應用程式設定。 請參閱應用程式的廠商文件，了解您可以設定的特定項目 (名稱/值組)。  

 然後，在應用程式部署期間，將應用程式設定原則與 iOS 部署類型建立關聯。 您也可以從 [應用程式設定原則] 節點部署原則，而且目標設為現有應用程式和集合。  

 請嘗試完成下列工作，然後使用本主題頂端附近的意見反應資訊，告訴我們工作的成效：  

-   如果您有支援應用程式設定的 iOS 應用程式，請參閱應用程式廠商的文件，了解您必須指定才能設定應用程式的名稱/值組。  

-   啟動 [建立應用程式設定原則精靈]。 在精靈的 [iOS 原則] 頁面上，嘗試新增您從應用程式廠商文件中找到的名稱/值組，也可以匯入包含必要值的 XML 檔案。  

-   在 [部署軟體精靈] 的 [應用程式設定原則] 頁面中，請將您建立的應用程式設定原則與應用程式中的相容部署類型建立關聯。  

##  <a name="bkmk_compliance1601"></a> 合規性設定的增強功能  
 在 1601 Technical Preview 中，我們已新增下列功能的支援：  

### <a name="microsoft-edge-browser-settings"></a>Microsoft Edge 瀏覽器設定  
 Microsoft Edge 瀏覽器的新設定已新增至 [Windows 8.1 與 Windows 10] 設定項目 (設定僅適用於 Windows 10 裝置)。  

 若要查看新的設定，請從 [建立設定項目精靈] 的設定項目 [裝置設定] 頁面中選擇 [Microsoft Edge]。  

 如需詳細資訊，請參閱[如何為不是使用 System Center Configuration Manager 用戶端所管理的 Windows 8.1 和 Windows 10 裝置建立設定項目](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)。  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Windows 10 Team 裝置的相容性設定  
 使用這些新的相容性設定可設定執行 Windows 10 Team 的裝置 (例如 Surface Hub 裝置)。  

 若要查看新的設定，請從 [建立設定項目精靈] 的設定項目 [裝置設定] 頁面中選擇 [Windows 10 團隊版]。  

 如需詳細資訊，請參閱[如何為不是使用 System Center Configuration Manager 用戶端所管理的 Windows 8.1 和 Windows 10 裝置建立設定項目](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)。  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android - Samsung KNOX Standard 的 Kiosk 模式<br />模式  
 Kiosk 模式可讓您限制裝置只能執行某些特定功能。 例如，您可以允許裝置只執行您指定的一個受管理應用程式，也可以停用裝置上的音量按鈕。 這些設定可能用於裝置的展示模型，或是專用來只執行一個功能的裝置 (例如銷售點裝置)。 在 [Windows 8.1 與 Windows 10] 設定項目中，這些設定不適用於 Samsung KNOX Standard 裝置 (設定僅適用於 Windows 10 裝置)。  

 若要查看新的設定，請從 [建立設定項目精靈] 的設定項目 [裝置設定] 頁面中選擇 [Kiosk 模式 - Samsung KNOX]。  

 如需詳細資訊，請參閱[如何為不是使用 System Center Configuration Manager 用戶端所管理的 Windows 8.1 和 Windows 10 裝置建立設定項目](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)。  
