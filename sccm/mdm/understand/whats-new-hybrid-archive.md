---
title: "新混合式 MDM 的封存 | Microsoft Docs"
description: "System Center Configuration Manager 與 Intune 的混合式部署可以使用過去之行動裝置管理功能的封存。"
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 0abd1cdcf44e778c91bacb8011efd711818ce2e9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 和 Microsoft Intune 過去的混合式功能

*適用對象：System Center Configuration Manager (最新分支)*

本文提供 System Center Configuration Manager 與 Microsoft Intune 混合式部署可以使用過去的行動裝置管理 (MDM) 功能的詳細資訊。  

##  <a name="compatibility-with-configuration-manager-versions"></a>與 Configuration Manager 版本的相容性  

 本文的各節會列出 3 個不同目錄下的混合式功能。 請使用下列指導方針判斷每個類別功能與 Configuration Manager 不同版本的相容性︰  

|功能類別|
|-|  
|**Microsoft Intune 的新功能**：通常此類別下列出的所有功能都應該能夠搭配所有的 Configuration Manager 版本，包括 System Center 2012 R2 Configuration Manager 版本，因為這些功能只需要 Intune 服務，不需要其他的 Configuration Manager 功能。<br /><br /> **Configuration Manager Technical Preview 的新功能**：此類別下列出的所有功能只能搭配 Technical Preview 版本使用。 若要試用這些功能，您必須安裝功能描述中指定的 Technical Preview 版本。 如需詳細資訊，請參閱 [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) 。<br /><br /> **Configuration Manager 的新功能 (最新分支)**：此類別下列出的所有功能僅能搭配指定的 Configuration Manager 版本 (最新分支) 使用，例如 1511 版或 1602 版。 如果您的混合式部署使用舊版的 Configuration Manager，即必須升級到功能描述中指定的 Configuration Manager 版本 (最新分支)。 如需詳細資訊，請參閱[升級至 System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。|  

## <a name="december-2016"></a>2016 年 12 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

- **移至 Azure 入口網站的註冊相關 Multi-Factor Authentication (MFA)**

  您之前會移至 Intune 主控台或 Configuration Manager 主控台，來設定用於 Intune 註冊的 MFA。 透過這項更新的功能，您現在可以使用 Intune 認證登入 [Microsoft Azure 入口網站] (https://manage.windowsazure.com)，並透過 Azure AD 進行 MFA 設定。 若要深入了解，請參閱 [Microsoft Intune 的 Multi-Factor Authentication] (https://aka.ms/mfa_ad)。

- **中國現在提供適用於 Android 的公司入口網站應用程式**

  中國現在提供適用於 Android 的公司入口網站應用程式。 由於中國沒有 Google Play 商店，因此 Android 裝置必須從中文應用程式服務商場取得應用程式。 適用於 Android 的公司入口網站應用程式已於下列市集中可供下載：

  - [百度](https://go.microsoft.com/fwlink/?linkid=836946)
  - [華為](https://go.microsoft.com/fwlink/?linkid=836948)
  - [騰訊](https://go.microsoft.com/fwlink/?linkid=836949)
  - [豌豆莢](https://go.microsoft.com/fwlink/?linkid=836950)
  - [小米應用商店](https://go.microsoft.com/fwlink/?linkid=836947)

  適用於 Android 的公司入口網站應用程式會使用 Google Play 服務來與 Microsoft Intune 服務通訊。 由於中國尚無法使用 Google Play 服務，因此執行下列任何工作可能需要多達 8 小時才能完成。

  | Configuration Manager 系統管理員主控台 | 適用於 Android 的 Intune 公司入口網站應用程式 | Intune 公司入口網站 |
  |----|----|----|      
  | 淘汰/抹除 (移除所有資料)   | 移除遠端裝置 | 移除裝置 (本機和遠端) |
  | 淘汰/抹除 (移除公司資料)   | 重設裝置 | 重設裝置|
  | 新的或更新的應用程式部署 | 安裝可用的企業營運應用程式 | 裝置密碼重設|
  | 遠端鎖定 | | |
  | 密碼重設 | | |        


## <a name="november-2016"></a>2016 年 11 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

- **適用於 Windows 10 裝置的新 Microsoft Intune 公司入口網站**

  Microsoft 已發行新的[適用於 Windows 10 裝置的公司入口網站應用程式](https://www.microsoft.com/store/apps/9wzdncrfj3pz)。 此應用程式會利用新的 Windows 10 通用格式，提供與所有 Windows 10 裝置、電腦及行動裝置之類的裝置上完全相同的更新使用者體驗，同時仍會啟用先前公司入口網站應用程式所提供的所有相同功能。

  新的應用程式會利用 Windows 10 裝置上的平台功能，例如單一登入 (SSO) 和憑證式驗證。 此應用程式可用來升級到現有的 Windows 8.1 公司入口網站，而 Windows Phone 8.1 公司入口網站會從 Windows 市集進行安裝。 如需詳細資訊，請參閱 [Intune 支援小組部落格](http://aka.ms/intunecp_universalapp)。

  新的公司入口網站應用程式也會在 Configuration Manager 主控台中，顯示所有標記為**可用**的商務用 Windows 市集應用程式。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

Configuration Manager Technical Preview 各版本過去提供的下列功能，目前可在 Intune 和 Configuration Manager (最新分支) 1610 版的混合式部署中使用。

* [設定項目的額外設定和改進體驗](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [DEP 設定檔的其他設定](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [商務用 Windows 市集的付費 App](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Windows 10 VPN 設定檔的原生連接類型](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Intune 相容性圖表](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [從主控台要求同步處理原則](/sccm/mdm/deploy-use/sync-intune-device)
* [Windows Defender 組態設定](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

Configuration Manager (最新分支) 1610 版也包含下列額外的混合式功能：

- **增加已註冊裝置的數目**

  您現在可讓使用者最多註冊 15 個裝置。 先前的限制是每位使用者 5 個裝置。


- **其他的安全性支援**

  除了系統高權限管理員，下列內建的安全性角色現在也具備「公司擁有的所有裝置」節點中項目的完整存取權，包括預先宣告的裝置、iOS 註冊設定檔，以及 Windows 註冊設定檔：

    - 資產管理員
    - 公司資源存取管理員

  系統仍會為唯讀分析師角色授與 Configuration Manager 主控台中這些區域的唯讀存取權。

- **從 Windows 資訊保護應用程式自動觸發 VPN 存取**

  您可以將 Windows 資訊保護主要網域加入 Windows 10 VPN 設定檔，這將導致所有相關聯的應用程式在裝置上執行時會自動觸發 VPN 連線。 唯有在選擇原生連線類型時，才能使用此選項。

- **Windows 10 VPN 設定檔的條件式存取**

    您現在可以要求在 Azure Active Directory 中註冊的 Windows 10 裝置必須符合標準，才能透過在 Configuration Manager 主控台中建立的 Windows 10 VPN 設定檔來存取 VPN。 這能夠透過 VPN 設定檔精靈中 [驗證方法] 頁面上新的 [為此 VPN 連線啟用條件存取] 核取方塊以及 Windows 10 VPN 設定檔的 VPN 設定檔內容來進行。 唯有在選擇原生連線類型時，才能使用此選項。

    如果您啟用設定檔的條件式存取，您也可以指定不同的憑證來進行單一登入驗證。

## <a name="october-2016"></a>2016 年 10 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 10 月推出的下列 Intune 功能可在混合式部署中運作。

- **行動應用程式管理的條件式存取**

  您可以限制存取 Exchange Online，只讓支援 Intune 行動應用程式管理原則的應用程式存取，例如 Outlook。 [這項新功能](/intune/deploy-use/allow-policy-managed-apps-access-to-o365)可以完美配合 Intune 行動應用程式管理 (MAM) 原則，因為您可以封鎖內建郵件用戶端或其他尚未使用 Intune MAM 原則設定之應用程式的存取權。 這可確保您的使用者以使用 Intune MAM 保護的應用程式存取組織資料。 您可以透過 Azure 入口網站在 Intune 行動裝置應用程式管理中開始。 在 [設定] 刀鋒視窗中尋找新的 [條件式存取] 區段。

-   **適用於 Android 的 Intune 應用程式包裝工具**

  您可以使用 Intune 應用程式包裝工具，讓應用程式使用 Intune 行動應用程式管理 (MAM) 原則。

- **Android Samsung KNOX Standard 與 Intune 的相容性**

  Samsung Galaxy Ace 手機有些型號不能當成 Samsung KNOX Standard 裝置由 Intune 管理。 當您向 Intune 註冊這些裝置時，它們會改作為標準的 Android 裝置來管理。

  受影響的型號為︰

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  您和您的使用者不需要採取任何進一步的動作。 如需詳細資訊，請瀏覽 Samsung KNOX 網站。

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Configuration Manager Technical Preview 1610 的新功能

Configuration Manager Technical Preview 1610 於 2016 年 10 月推出下列新的混合式功能。

- **要求從管理主控台同步處理原則**

  您可以從 Configuration Manager 主控台要求同步處理已註冊的行動裝置原則，不必要求在裝置本身的公司入口網站應用程式中同步處理。 這是 [遠端裝置動作] 功能表中的新動作，稱為 **「Send Sync Request」** (傳送同步要求)，在 [裝置] 節點中選取行動裝置時會出現在功能區。

- **Windows Defender 組態設定**

  您現在可以使用 Configuration Manager 主控台中的設定項目，在 Intune 註冊的 Windows 10 電腦上設定 Windows Defender 用戶端設定。 設定項目精靈中有一個新的設定群組，稱為 **Windows Defender**。 請注意，只有 Windows 10 1511 版和更新版本才支援。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

Configuration Manager 2016 年 8 月 (最新分支) 未推出任何新的混合式功能。

## <a name="september-2016"></a>2016 年 9 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 9 月推出的下列 Intune 功能可在混合式部署中運作。

- **Android 公司入口網站新增「通知」**

  新的通知圖示已經加入 Android 公司入口網站的首頁。 點選此圖示可存取 [通知] 頁面，向使用者顯示公司入口網站應用程式中需要注意的所有項目，例如不相容的裝置、註冊更新以及啟用註冊。 iOS 公司入口網站應用程式已有此通知體驗。 擁有新的 [通知] 頁面表示，只要裝置已註冊，使用者每次啟動或繼續公司入口網站時，不會看到 [公司存取設定] 頁面。 如果您建立自己的使用者指南，您可能想要更新自己的文件以反映這項變更。 在[這裡](https://aka.ms/androidcpupdate)尋找已更新的螢幕擷取畫面。

- **iOS 公司入口網站應用程式的支援變更**

  iOS 的 Microsoft Intune 公司入口網站應用程式的所有使用者，現在都必須使用其最新版本。 新的使用者只能夠下載最新版本，而目前的使用者則必須更新它。 最新版本需要 iOS 8.0 或更新版本，因此在裝置更新至 iOS 8.0 或更新版本，再將公司入口網站應用程式更新至最新版本前，執行較舊 iOS 版本的裝置無法使用公司入口網站或註冊。 執行版本低於 iOS 8.0 的已註冊裝置會繼續由 Intune 管理主控台所管理及列示。

- **Windows Phone 8.1 公司入口網站應用程式新增意見反應按鈕**

  Windows Phone 8.1 公司入口網站應用程式可讓使用者使用新的 [傳送意見反應] 按鈕，傳送有關應用程式的意見反應。 若要尋找按鈕，使用者可點選公司入口網站應用程式畫面右下方的「三個點」功能表，然後點選 [傳送意見反應]。 收集的匿名意見反應會協助 Microsoft 改善使用者的公司入口網站應用程式體驗。

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Configuration Manager Technical Preview 1609 的新功能

Configuration Manager Technical Preview 1609 於 2016 年 9 月推出下列新的混合式功能。

- **設定項目設定的額外設定和改進體驗**

  Android、iOS 和 Windows 已新增新的設定，只有套用至您在 [支援的平台] 頁面上所選平台的設定，才會顯示在精靈中。 如需詳細資訊，請參閱 [TP 1609 中的設定項目新相容性設定](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items)。

- **DEP 設定檔的其他設定**

  TouchID、ApplePay 及 Zoom 已加入為 iOS 裝置之 DEP 設定檔可設定的設定值。

- **商務用 Windows 市集的付費 App**

  現在，您可以在商務用 Windows 市集中新增付費及免費的應用程式，並將它們部署到組織中的使用者。 如需詳細資訊，請參閱 [TP 1609 的商務用 Windows 市集增強功能](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager)。

- **Windows 10 VPN 設定檔的原生連接類型**

  您現在可以在 Configuration Manager 主控台中不使用 OMA URI，以 Microsoft Automatic、IKEv2 和 PPTP 連線類型建立 MDM 的 Windows 10 VPN 設定檔。

- **Intune 相容性圖表**

  您可以使用 [監視] 工作區中的新圖表，快速檢視整部裝置的相容性和不相容的主要原因。 如需詳細資訊，請參閱 [TP 1609 中的 Intune 相容性圖表](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts)。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

2016 年 9 月推出的下列新功能可用於 Microsoft Intune 和 Configuration Manager 1606 版 (最新分支) 的混合式部署。

- **iOS 10 支援**

  如果您有以所有 iOS 平台為目標的設定檔或設定項目，它們也會推送至 iOS 10。 我們也已經發行 Configuration Manager 1606 版的更新，讓您以個別 iOS 平台，包括 iOS 10 的設定檔和設定項目為目標。 您可以在 [管理] > [概觀] > [雲端服務] > [更新與服務]，使用 Configuration Manager 管理主控台安裝更新。 您可以在 [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616) 找到更新的詳細資訊。

## <a name="august-2016"></a>2016 年 8 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 8 月推出的下列 Intune 功能可在混合式部署中運作。

- **公司入口網站應用程式對 Android 7 的支援**

  Android 的 Intune 公司入口網站應用程式為即將推出的行動裝置 Android 7.0 作業系統提供「零時差」支援。

- **Google 移除了 Android 7.0 裝置上的遠端密碼重設功能**

  Google 正在移除 IT 系統管理員和使用者從遠端重設 Android 7.0 裝置密碼的能力。 過去，IT 系統管理員可以從遠端重設使用者的密碼，讓使用者從公司入口網站重設其密碼。

- **Samsung KNOX Standard 裝置的允許和封鎖應用程式原則**

  您現在可以設定 Samsung KNOX Standard 裝置的自訂原則，讓您建立下列其中一項：

  - 在裝置上封鎖執行的應用程式清單。 即使已安裝，封鎖清單中定義的應用程式也無法在裝置上啟動。
  - 允許裝置使用者從 Google Play 商店安裝的應用程式清單。 沒有任何其他應用程式可以從該商店安裝。

  這些設定只能供執行 Samsung KNOX Standard 的裝置使用。 如需詳細資訊，請參閱[使用自訂原則來允許及封鎖 Samsung KNOX Standard 裝置的應用程式](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps)。

- **從公司入口網站的意見反應連結到 Microsoft**

   公司入口網站可讓使用者點選頁面底部的新 [意見反應] 連結，將其有關站台經驗的意見傳送給 Microsoft。 收集的匿名意見反應會協助 Microsoft 改善使用者的公司入口網站體驗。

- **iOS Managed Browser 版本至少要更新至 8.0**

  iOS 的 Microsoft Intune Managed Browser 應用程式已更新為支援執行 iOS 8.0 或更新版本的裝置。 雖然 iOS 7.1 裝置仍可使用現有的 Managed Browser 應用程式，但建議使用者更新至 iOS 8.0 或更新版本，以存取並充分利用新的 Managed Browser 功能。

### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview 的新功能

Configuration Manager Technical Preview 2016 年 8 月未推出任何新的混合式功能。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

Configuration Manager 2016 年 8 月 (最新分支) 未推出任何新的混合式功能。

## <a name="july-2016"></a>2016 年 7 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能

2016 年 7 月推出的下列 Intune 功能可在混合式部署中運作。

- **Xamarin SDK for Intune 應用程式可供使用**

  Intune 應用程式 SDK Xamarin 元件可讓您在以 Xamarin 建置的 iOS 和 Android 行動應用程式中，啟用 Intune 行動應用程式管理功能。 您可以在 [Xamarin 市集](https://components.xamarin.com/view/Microsoft.Intune.MAM)或 [Microsoft Intune Github 頁面](https://github.com/msintuneappsdk)找到元件。

- **註冊 Windows 裝置之改善的使用者經驗**

  當您使用條件式存取時，公司入口網站中已明確說明 Windows 8.1、Windows 10 Desktop 和 Windows 10 行動裝置的註冊步驟。 如果發生工作場所聯結 (WPJ) 失敗，使用者現在會看到不同的**裝置註冊**和**工作場所聯結**步驟，可輕鬆查看裝置狀態並完成程序。 分開的步驟也可以簡化 IT 系統管理員的疑難排解程序。 以前，當使用者嘗試註冊，且除了 WPJ 以外的所有註冊步驟都成功時，註冊的裝置不會出現在裝置清單中供使用者識別，進而造成使用者混淆。

 - **Windows 10 裝置現在可使用完整抹除**

    可以抹除註冊為行動裝置的 Windows 10 電腦和膝上型電腦，將裝置重設回其原廠設定。 如需詳細資訊，請參閱 [How to protect your devices with remote wipe](/sccm/mdm/deploy-use/wipe-lock-reset) (如何保護裝置免於遠端抹除)。

- **iOS 公司入口網站應用程式中的裝置註冊管理員帳戶變更**

  為改善效能和延展性，Intune 不再於 iOS 公司入口網站應用程式的 [我的裝置] 窗格中，顯示所有裝置註冊管理員 (DEM) 裝置。 僅顯示執行應用程式的本機裝置，而且僅限透過公司入口網站應用程式註冊的本機裝置。

  DEM 使用者可在本機裝置上執行動作，但其他已註冊裝置的遠端管理只能從 Intune 管理主控台執行。 此外，Intune 會淘汰使用 Apple 裝置註冊方案或 Apple Configurator 工具的 DEM 帳戶。 這兩種註冊方法都支援共用 iOS 裝置的無使用者註冊。

  只有當共用裝置的無使用者註冊無法使用時，才使用 DEM 帳戶。 如需詳細資訊，請參閱[使用 Microsoft Intune 中的裝置註冊管理員註冊公司所擁有的裝置](../deploy-use/enroll-devices-with-device-enrollment-manager.md)。

- **Android 公司入口網站應用程式的變更**

  Android 使用者如果看到裝置缺少必要憑證的錯誤訊息，可以點選 「How to resolve this」 (問題解決方法) 按鈕，取得安裝所缺憑證的步驟。 如果使用者完成這些步驟，但看到其他「缺少憑證」錯誤訊息，就需要連絡 IT 系統管理員並提供此連結，訊息中包含 IT 系統管理員可用來解決憑證問題的步驟。

- **限制已註冊 Android 裝置的側載應用程式安裝**

  Android 裝置無法再透過公司入口網站來安裝應用程式，除非裝置已使用 Android 的 Intune 公司入口網站應用程式向 Intune 註冊。


### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview 的新功能

Configuration Manager Technical Preview 2016 年 7 月未推出任何新的混合式功能。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)

Configuration Manager Technical Preview 各版本過去提供的下列功能，目前可在 Intune 和 Configuration Manager 1606 版 (最新分支) 的混合式部署中使用。

* 從 Configuration Manager 主控台尋找、管理及散發 Windows 10 裝置的商務用 Windows 市集應用程式 ([1604](#new-in-1604-technical-preview))
*   適用於 Android 裝置的 SmartLock 設定 ([1604](#new-in-1604-technical-preview))
*   適用於 Windows 10 裝置的應用程式觸發的 VPN ([1605](#new-in-1605-technical-preview))
*   遠端裝置動作的全新體驗 ([1605](#new-in-1605-technical-preview))
*   商務用 Windows 市集應用程式 ([1605](#new-in-1605-technical-preview))
*   針對大量購買之應用程式的一般改進 ([1605](#new-in-1605-technical-preview))
*   Windows 資訊保護 (WIP) ([1605](#new-in-1605-technical-preview))
*   使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置 ([1605](#new-in-1605-technical-preview))
*   自動將裝置分類為集合 ([1606](#new-in-1606-technical-preview))

如需新功能的資訊，請參閱指定的 Technical Preview 版本文件。

## <a name="june-2016"></a>2016 年 6 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能
2016 年 6 月推出的下列 Intune 功能可在混合式部署中運作。

- **Intune 服務健全狀況**：Intune 服務健全狀況資訊已和其他 Microsoft 服務一起移至中央位置。 現在，可以在 Office 365 管理入口網站的 [服務健全狀況] 下找到這項資訊。 如需詳細資訊，請參閱此[部落格文章](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/)。

- **增強的 Windows 10 企業資料原則設定體驗**

  Intune 現在提供較佳的 Windows 10 資訊保護原則設定體驗。 增強功能包括以更好的方式來建立應用程式規則、指定網路界限定義，以及其他 Windows 資訊保護設定。 若要深入了解，請參閱[使用 Microsoft Intune 建立 Windows 資訊保護 (WIP) 原則](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune)。

- **適用於 Intune 的 Cisco ISE 網路存取控制原則**

  同時使用 Cisco Identity Service Engine (ISE) 2.1 及 Microsoft Intune 的客戶，可以在 ISE 中設定網路存取控制原則。使用此原則，則需要使用 WiFi 或 VPN 連接網路的裝置必須符合下列條件，才能獲准存取︰

  - 必須由 Intune 管理
  - 必須與所有已部署的 Intune 相容性原則相容

  會提示不相容裝置的使用者註冊，並修復任何相容性問題以獲得存取權。

- **瀏覽器的條件式存取**

  您可以設定 Exchange Online 和 SharePoint Online 條件式存取原則，以便只從受管理和相容的 iOS 和 Android 裝置上受支援的網頁瀏覽器存取它們。 嘗試使用 iOS 和 Android 裝置登入 Outlook Web Access (OWA) 和 SharePoint 網站的使用者，系統會提示他們向 Intune 註冊其裝置，以及必須修正所有不相容的問題才能完成登入。 如需詳細資訊，請參閱

  * [使用 Intune 限制對 Exchange Online 及新 Exchange Online Dedicated 的電子郵件存取](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [使用 Microsoft Intune 限制存取 SharePoint Online](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online 支援條件式存取**

  您可以設定 Dynamics CRM Online 的條件式存取原則，使它只能被受管理和相容的 iOS 和 Android 裝置存取。 嘗試登入 iOS 和 Android 的 Dynamics CRM 行動應用程式的使用者，系統會提示他們向 Intune 註冊，以及必須修復所有不相容的問題，才能完成登入。 如需詳細資訊，請參閱[使用 Intune 限制對 Dynamics CRM Online 的存取](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune)。

- **Android 公司入口網站應用程式更新**

  下列的 Intune 新原則會影響 Android 公司入口網站使用者︰   

  原則  |對使用者的影響  
  ---------|---------
  要求裝置不得安裝來源不明的應用程式 (Android 4.0+)     |  Android 4.0 或更新裝置的使用者會看到此訊息：「必須停用來自未知來源的安裝。」 使用者必須移至裝置的 [設定] > [安全性]，並關閉 [未知來源]。 相容性訊息中的連結可讓使用者取得訊息的詳細資訊，以及必須關閉設定的原因。
  要求裝置不得安裝來源不明的應用程式 (Android 4.0+)  |    Android 4.0 或更新裝置的使用者會看到此訊息：「掃描裝置中的安全性威脅。」 使用者必須移至裝置的 [設定] > [Google] > [安全性]，並開啟 [掃描裝置中的安全性威脅]。 相容性訊息中的連結可讓使用者取得訊息的詳細資訊，以及必須開啟設定的原因。     
  需要停用 USB 偵錯 (Android 4.2+)  | Android 4.2 或更新裝置的使用者會看到此訊息：「必須停用 USB 偵錯。」 使用者必須移至裝置的 [設定] > [開發人員選項]，並關閉 [USB 偵錯]。 相容性訊息中的連結可讓使用者取得訊息的詳細資訊，以及必須關閉設定的原因。
  Android 安全性修補程式等級下限 (Android 6.0+)  | Android 6.0 或更新裝置的使用者會看到此訊息：「此裝置不符合最低的 Android 安全性更新程式等級。」 使用者必須安裝必要的安全性修補程式。 相容性訊息中的連結可讓使用者取得如何安裝必要安全性修補程式的相關資訊，以及查看目前已安裝的安全性修補程式。

- **iOS 公司入口網站應用程式更新**

  * 現在當使用者安裝企業營運應用程式時，就會看到改善的應用程式安裝體驗。 如果應用程式安裝花很長的時間，使用者可以手動同步處理裝置，強制同步處理程序繼續執行。 若要檢閱使用者指示，請參閱＜手動同步 iOS 裝置＞。
  * 適用於 iOS 的 Microsoft Intune 公司入口網站應用程式已更新為支援 iOS 8.0 版和更新版本。 此更新表示唯有裝置執行的是 iOS 8.0 版或更新版本時，使用者才能安裝公司入口網站應用程式，並向 Intune 註冊新的裝置。 若使用者已經註冊在不支援的 iOS 版本中執行的裝置，則可繼續使用其裝置上的公司入口網站應用程式。


### <a name="new-in-1606-technical-preview"></a>1606 Technical Preview 的新功能
2016 年 6 月推出的下列新功能可用於 Intune 和 Configuration Manager Technical Preview 1606 的混合式部署。

- **自動將裝置分類為集合**

  您可以建立裝置類別，如此可在您使用 Configuration Manager 與 Intune 時自動將裝置放在裝置集合中。 使用者向 Intune 註冊裝置時，必須選擇裝置類別。 您也可以從 Configuration Manager 主控台中變更裝置類別。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1606 for System Center Configuration Manager ](/sccm/core/get-started/capabilities-in-technical-preview-1606) (System Center Configuration Manager Technical Preview 1606 的功能) 的 [Automatically categorize devices into collections](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) (自動將裝置分類為集合)。

  > [!IMPORTANT]
  > 這項功能適用於 Microsoft Intune 的 2016 年 6 月版。 請先確定已更新為此版，再嘗試這些程序。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)
Configuration Manager 2016 年 6 月 (最新分支) 未推出任何新的混合式功能。

##  <a name="may-2016"></a>2016 年 5 月  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能  
 2016 年 5 月推出的下列 Intune 功能可在混合式部署中運作。

- **MAM SDK︰支援 PIN 長度設定**

  您現在可以指定與裝置 PIN 相似的 MAM 應用程式 PIN 長度。 這需要使用者符合您設定的新限制。 PIN 螢幕為因應較長的輸入而略有修改。 如需詳細資訊，請參閱 [Microsoft Intune 中的 Android 行動應用程式管理原則設定](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings)和 [iOS 行動應用程式管理原則設定](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings)。  

- **適用於 iOS 和 Android 的商務用 Skype**

  您現在可以商務用 Skype 及[沒有註冊原則的 MAM](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune) 為目標。 一旦使用者登入，就會套用 MAM 原則。  

- **可以 MAM 原則管理的新應用程式**

  適用於 Android 的 Microsoft Word、Excel 和 PowerPoint 應用程式，現在可與未向 Intune 註冊的裝置上的 MAM 原則建立關聯。 如需支援的應用程式完整清單，請移至 [Microsoft Intune 應用程式合作夥伴](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx)頁面的 Microsoft Intune 行動應用程式庫。  

- **Android 公司入口網站應用程式︰使用者快顯通知**

  當使用者在公司入口網站註冊或移除裝置時，Android 公司入口網站應用程式就會顯示快顯通知。  

- **公司入口網站︰裝置識別橫幅會向使用者提供詳細資訊**

  現在當使用者使用公司入口網站時，會更容易識別他們選取的裝置。 如果選取了錯誤的裝置，他們可以點選首頁橫幅的 [點選這裡] 連結，選取正確的裝置。  


### <a name="new-in-1605-technical-preview"></a>1605 Technical Preview 的新功能  
 2016 年 5 月推出的下列新功能可用於 Intune 和 Configuration Manager Technical Preview 1605 的混合式部署。 這些功能都需要使用 Configuration Manager 主控台設定及管理。  

- **適用於 Windows 10 裝置的應用程式觸發型 VPN**

  針對使用 Configuration Manager 與 Intune 管理的 Windows 10 裝置，您可以加入會自動開啟 VPN 連線的應用程式清單，這個 VPN 連線是透過 Configuration Manager 管理主控台所設定。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (System Center Configuration Manager Technical Preview 1605 的功能) 中的 [App-triggered VPN for Windows 10 devices](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Windows 10 裝置的應用程式觸發型 VPN)。  

- **遠端裝置動作的全新體驗**

  從 Configuration Manager 主控台執行遠端裝置動作的體驗已改善。

  現在從 [資產與相容性] 工作區存取 [遠端裝置動作] 功能表即可找到 [淘汰/抹除]、[重設密碼]、[遠端鎖定] 和 [略過啟用鎖定] 等常見動作。

  如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (System Center Configuration Manager Technical Preview 1605 的功能) 中的 [New experience for remote device actions](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) (遠端裝置動作的新體驗)。  

- **商務用 Windows 市集應用程式**

  [商務用 Windows 市集](https://www.microsoft.com/en-us/business-store)是您可以在其中為您的組織尋找並個別或大量採購應用程式的地方。 藉由將市集連接到 Configuration Manager，您便可以從 Configuration Manager 主控台管理大量採購的應用程式。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (System Center Configuration Manager Technical Preview 1605 的功能) 中的 [Windows Store for Business apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) (商務應用程式的 Windows 市集)。  

- **針對大量採購應用程式的一般改進**

  商務用 Windows 市集和 iOS 應用程式市集的大量採購應用程式已合併到 [市集應用程式的授權資訊] 檢視。 此外，大量採購 iOS 應用程式的方式也已改良。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (System Center Configuration Manager Technical Preview 1605 的功能) 中的 [General improvements for volume-purchased apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) (大量採購應用程式的一般改進)。  

- **使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置**

  您現在可以透過匯入國際行動設備識別碼 (IMEI)，識別公司擁有的裝置。 您可以上傳一個包含裝置 IMEI 編號的逗號分隔值 (.csv) 檔案，也可以手動輸入裝置資訊。  您也可以匯入 iOS 裝置的序號。  如需詳細資訊，請參閱 [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (System Center Configuration Manager Technical Preview 1605 的功能) 中的 [Pre-declare corporate-owned devices with IMEI or iOS serial number](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) (使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置)。  

- **Windows 資訊保護 (WIP)**

  您可以建立讓您部署 Windows 資訊保護 (WIP) 原則的設定項目，包括讓您選擇受保護的應用程式、WIP 保護層級，以及如何在網路上尋找企業資料。 如需 WIP 的詳細資訊，請參閱下列主題：  

  -   [使用 Windows 資訊保護 (WIP) 保護您的企業資料](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [使用 System Center Configuration Manager 建立和部署 Windows 資訊保護 (WIP) 原則](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)  
 Configuration Manager 2016 年 5 月 (最新分支) 未推出任何新的混合式功能。  

##  <a name="april-2016"></a>2016 年 4 月  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能  
 2016 年 4 月推出的下列 Intune 功能可在混合式部署中運作。  

- **MAM 使用者相容性**

  您現在可以檢視 Azure Active Directory (AAD) 租用戶中任何使用者的應用程式管理原則狀態。  如需詳細資訊，請參閱 Intune 程式庫的[使用 Microsoft Intune 監視行動應用程式管理原則](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)。  

- **防止 Outlook 連絡人同步的 MAM 控制項 (Android)**

  現提供新設定，讓您防止應用程式同步處理 Android 裝置的原生通訊錄連絡人。 這個新的設定最初受 Android 裝置的 Outlook 應用程式支援。 如需詳細資訊，請參閱 Intune 程式庫的[使用 Microsoft Intune 建立及部署行動應用程式管理原則](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)。  

- **公司入口網站的增強功能**

  當 Windows 10 行動裝置和 Windows Phone 8.1 使用者安裝企業營運應用程式時，將會看到下列的新狀態，提供他們有關安裝狀態的更詳細資訊︰  

  -   **正在等候裝置同步** – 使用者點選了 [安裝]，裝置現嘗試同步處理 Intune 基礎結構。 必須先同步處理，才能完成安裝。 如果同步處理程序需要較長的時間或已停止，使用者也可以點選「正在等候裝置同步」訊息連結，查看如何手動同步處理裝置與 Intune 的指示。  

  -   **下載** – 正在處理使用者的下載要求，且裝置正在下載並安裝應用程式。  

- **Android 公司入口網站應用程式的增強功能**

  未向 Intune 註冊的裝置以及未安裝正確憑證的使用者，無法登入 Android 公司入口網站應用程式，並會看到此訊息：「由於您的裝置遺漏所需的憑證，因此您無法登入。」 此訊息包含「如何解決此問題」的連結，使用者可以點選它查看安裝憑證的指示。 若要查看解決此問題的使用者遵循步驟，請參閱 Intune 程式庫的[您的裝置遺漏必要的憑證](/intune/enduser/using-your-android-device-with-intune)。  

- **iOS 公司入口網站應用程式的增強功能**

  已對下拉即可重新整理動作加入支援，以重新整理主畫面內容，包括列出的應用程式、列出的裝置，以及 IT 連絡人資訊。 下拉即可重新整理動作不檢查相容性或原則資訊，而這項作業只要選取目前裝置的磚並點選 [同步] 按鈕即可完成。  

- **Windows 10 行動裝置和 Windows Phone 8.1 公司入口網站應用程式的增強功能**

  現在當使用者安裝企業營運應用程式時，就會看到改善的應用程式安裝體驗。 如果應用程式安裝花很長的時間，使用者可以手動同步處理裝置，強制同步處理程序繼續執行。 若要檢閱使用者指示，請參閱 Intune 程式庫中[手動同步裝置以加速安裝應用程式](/intune/enduser/using-your-windows-device-with-intune)。  

###  <a name="new-in-1604-technical-preview"></a>1604 Technical Preview 的新功能
 2016 年 4 月推出的下列新功能可用於 Intune 和 Configuration Manager Technical Preview 1604 的混合式部署。 這些功能都需要使用 Configuration Manager 主控台設定及管理。  

- **從 Configuration Manager 主控台尋找、管理及散發 Windows 10 裝置的商務用 Windows 市集應用程式**


  Configuration Manager Technical Preview 1604 提供商務用 Windows 市集的支援，可協助您尋找、管理及散發應用程式到您管理中的 Windows 10 裝置。 如需詳細資訊，請參閱 [Capabilities in Technical Preview 1604 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604) (System Center Configuration Manager Technical Preview 1604 的功能) 中的 [Manage volume-purchased apps from the Windows Store for Business](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) (從商務用 Windows 市集管理大量採購應用程式)。  

- **適用於 Android 裝置的 SmartLock 設定**

  Android 和 Samsung KNOX Standard 設定項目中已新增至新設定，可讓您控制相容 Android 裝置上的 SmartLock 功能。  您可以使用此設定來防止使用者設定 SmartLock。 請參閱 [Capabilities in Technical Preview 1604 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md) (System Center Configuration Manager Technical Preview 1604 的功能) 中的 [SmartLock setting for Android devices](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) (適用於 Android 裝置的 SmartLock 設定)。  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)  
 Configuration Manager 2016 年 4 月 (最新分支) 未推出任何新的混合式功能。  

##  <a name="march-2016"></a>2016 年 3 月  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 的新功能  
 2016 年 3 月推出的下列 Intune 功能可在混合式部署中運作。  

- **防止 Outlook 連絡人同步的 MAM 控制項 (iOS)**

  現提供新設定，讓您防止應用程式同步處理 iOS 裝置的原生通訊錄連絡人。 這個新的設定受 iOS 裝置的 Outlook 應用程式支援。 如需此設定及其他設定的詳細資訊，請參閱 Intune 程式庫的[使用 Microsoft Intune 建立及部署行動應用程式管理原則](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)。  

- **商務用 Skype Online 支援條件式存取**

  您可以設定商務用 Skype Online 的條件式存取原則，使它只能被受管理和相容的 iOS 和 Android 裝置存取。  如需詳細資訊，請參閱 Intune 程式庫的[管理商務用 Skype Online 的存取](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune)。  

- **支援 iOS 9.3**

  在 3 月 21 星期一，Apple 宣布 iOS 9.3 上市。 目前可管理 iOS 裝置的所有現有 Intune 功能，在使用者將裝置升級至 iOS 9.3 時，都會繼續順利運作。  

- **Windows 應用程式套件可以直接從公司入口網站取得**

  Windows 8、Windows 8.1 和 Windows RT 電腦的使用者現在可以直接從公司入口網站安裝 Windows 應用程式套件 (副檔名為 .appx)。 過去，您必須部署，或使用者必須在裝置上安裝公司入口網站應用程式，才能安裝應用程式。  

- **使用者可以從公司入口網站遠端鎖定裝置**

  公司入口網站新增了新的 [遠端鎖定] 選項，如果使用者的裝置遺失或遭竊，可讓他們從入口網站遠端鎖定裝置。  

- **協力廠商 MDM 解決方案中註冊的裝置，利用 iOS "Open-In"管理**

  您可以使用協力廠商行動裝置管理 (MDM) 廠商來利用 iOS "Open-In" 管理。 您可以在組態設定檔設定中設定限制，並使用 MDM 軟體部署。 當使用者安裝受管理的應用程式時，就會套用這些限制。 詳情請參閱 Intune 程式庫的 [Microsoft Intune 行動應用程式管理原則和 iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune)。  

- **支援 MAM 的 Microsoft 應用程式**

  可與 Intune 行動應用程式管理原則一起使用的 Microsoft 應用程式清單，已更新至包含最新的應用程式 (僅限向 Intune 註冊的裝置)。  

- **將 Adobe Reader for Microsoft Intune 部署到企業中 Intune 管理的 iOS 裝置**

  在已註冊裝置上的 Adobe Reader for iOS 應用程式現在可用 Intune 行動應用程式管理原則管理。  

- 支援 Android 的 Rights Management 共用應用程式

  IT 系統管理員可以部署行動應用程式管理原則，讓使用者可以更安全地檢視影像、AV 和 PDF 檔案，無論 IT 是否使用 Intune 來管理裝置。  

- **Android 和 iOS 公司入口網站應用程式的增強功能**

  -   當使用者啟動受行動應用程式管理 (MAM) 管理的應用程式時，會看到應用程式受公司管理的通知訊息。 使用者現在可以點選「Learn More」(深入了解) 連結，了解「受管理應用程式」意義的詳細資訊。 他們也可以點選「Don’t Show Again」(不要再顯示)，在啟動應用程式時不再顯示訊息。  

  -   已加入新畫面來引導使用者進行註冊程序，並提供使用者應該註冊的原因，以及 IT 系統管理員可在已註冊裝置上看見與否之內容的詳細資訊。  

  -   註冊錯誤訊息現在會顯示在公司入口網站應用程式中。  

### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview 的新功能  
 Configuration Manager Technical Preview 2016 年 3 月未推出任何新的混合式功能。  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager 的新功能 (最新分支)  
 2016 年 3 月推出的下列新功能可用於 Intune 和 Configuration Manager 1602 版 (最新分支) 的混合式部署。 這些功能都需要使用 Configuration Manager 主控台來設定及管理。  

- **iOS 應用程式設定原則**

  在 Configuration Manager 1602 版 (最新分支) 中您可以使用應用程式設定原則，提供使用者執行 iOS 應用程式時可能需要的設定。 如需詳細資訊，請參閱 [Configure iOS apps with app configuration policies in System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) (在 System Center Configuration Manager 中使用應用程式設定原則設定 iOS 應用程式)。  

- **管理大量採購的 iOS 應用程式**

  在 Configuration Manager 1602 版 (最新分支)中，您可從應用程式市集匯入授權資訊，並追蹤您已使用多少個授權，協助您部署和管理從 Apple 大量採購方案 (VPP) 大量購買的應用程式。 如需詳細資訊，請參閱 [Manage volume-purchased iOS apps with System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps) (使用 System Center Configuration Manager 管理大量採購的 iOS 應用程式)。  

- **自動建立 Office 行動應用程式**

  從 Configuration Manager 1602 版 (最新分支) 開始，當您從 1511 版升級時會建立下列 Android 和 iOS 版的 Microsoft Office 行動應用程式：  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (僅限 iOS)  
  -   Microsoft Outlook  

  您可以在 Configuration Manager 主控台的 [應用程式] 節點中找到這些應用程式。 如何有關部署應用程式的詳細資訊，請參閱[如何使用 System Center Configuration Manager 部署應用程式](../../apps/deploy-use/deploy-applications.md)。  

- **Android Samsung KNOX Standard 裝置的 Kiosk 模式設定**

  Kiosk 模式允許您限制裝置只能執行某些特定功能。  從 Configuration Manager 1602 版 (最新分支) 開始，您現在可以指定 Samsung KNOX Standard 裝置的 Kiosk 模式設定。 如需詳細資訊，請參閱[如何為不是使用 System Center Configuration Manager 用戶端所管理的 Android 和 Samsung KNOX Standard 裝置建立設定項目](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)。  

- **iOS 啟用鎖定**

  從 Configuration Manager 1602 版 (最新分支) 開始，您可以管理 iOS 啟用鎖定，這是 iOS 7.1 和更新版本裝置之「尋找我的 iPhone」應用程式中的功能。 當裝置上使用「尋找我的 iPhone」應用程式時，啟用鎖定會自動啟用。  如需詳細資訊，請參閱[使用 System Center Configuration Manager 管理 iOS 啟用鎖定](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock)。  
