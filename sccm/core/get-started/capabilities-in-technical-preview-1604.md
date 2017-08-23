---
title: "Technical Preview 1604 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1604 版中可用的功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 26b0d8ea7b3e841c48945df55f8860394a98a29f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1604-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1604 中的功能

適用於︰System Center Configuration Manager (Technical Preview)

本文介紹 System Center Configuration Manager Technical Preview 1604 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。      安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。  

 以下是您可以使用此版本試用的新功能。  

##  <a name="BKMK_WindowsVPP"></a> 從商務用 Windows 市集管理大量購買的應用程式  
 [商務用 Windows 市集](https://www.microsoft.com/en-us/business-store)是您可以在其中為您的組織尋找並個別或大量採購應用程式的地方。 藉由將市集連線到 Configuration Manager，您便可以從 Configuration Manager 主控台管理大量採購應用程式，例如：  

-   您可以將已購買的應用程式清單與 Configuration Manager 進行同步處理  

-   已同步處理的應用程式會出現在 Configuration Manager 主控台中，您可以部署這些應用程式，就像部署任何其他應用程式一樣  

-   您可以在 Configuration Manager 主控台中追蹤有多少授權可用，以及有多少授權已在使用中  

### <a name="try-it-out"></a>試試看！  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>案例 1︰設定「商務用 Windows 市集」同步處理  

1.  在 Azure Active Directory 中，將 Configuration Manager 登錄為 [Web 應用程式和/或 Web API] 管理工具。 這會提供您一個稍後將會需要的用戶端識別碼。  

    1.  在 [https://manage.windowsazure.com](https://manage.windowsazure.com) 的 [Active Directory] 節點中，選取您的 Azure Active Directory，然後按一下 [應用程式] > [新增]。  

    2.  按一下 [加入我的組織正在開發的應用程式]。  

    3.  輸入應用程式的名稱，選取 [Web 應用程式] 和/或 [Web API]，然後按一下 [下一步] 箭號。  

    4.  為 [登入 URL] 和 [應用程式識別碼 URI] 輸入相同的 URL。  URL 可以是任何內容，不需要解析為實際的位址。 例如，您可以輸入 **https://&lt;您的網域\>/sccm**。  

    5.  完成精靈。  

2.  在 Azure Active Directory 中，為已註冊的管理工具建立用戶端金鑰。  

    1.  反白選取您剛才建立的應用程式，然後按一下 [設定]。  

    2.  從 [金鑰] 底下的清單中選取持續時間，然後按一下 [儲存]。  這會建立一個新的用戶端金鑰。  在您成功將商務用 Windows 市集連線到 Configuration Manager 之前，請勿離開此頁面。  

3.  在商務用 Windows 市集中，將 Configuration Manager 設定為市集管理工具。  

    1.  開啟 [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools)，並在出現提示時登入。  

    2.  視需要接受使用條款  

    3.  在 [管理工具] 底下，按一下 [Add a management tool]\ (新增管理工具)。  

    4.  在 [Search for the tool by name]\(依名稱搜尋工具) 中，輸入您先前在 AAD 中所建立應用程式的名稱，然後按一下 [新增]。  

    5.  按一下您剛才匯入之應用程式旁邊的 [啟用]。  

    6.  如果您想要允許購買離線授權的應用程式，請在 [Show Offline-Licensed Apps Wizard]\(顯示離線授權的應用程式精靈) 中，按一下 [是]。  

4.  從「商務用 Windows 市集」至少購買一個應用程式。  

5.  在 Configuration Manager 主控台的 [系統管理] 工作區中，展開 [雲端服務]，然後按一下 [商務用 Windows 市集]。  

6.  在 [常用] 索引標籤的 [建立] 群組中，按一下 [新增商務用 Windows 市集帳戶]。  

7.  從 Azure Active Directory 中，加入您的租用戶識別碼、用戶端識別碼及用戶端金鑰，然後完成精靈。  

8.  完成之後，您就會在 Configuration Manager 主控台的 [商務用 Windows 市集帳戶] 清單中看到您設定的帳戶。  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>案例 2：從商務用 Windows 市集離線授權的應用程式建立和部署 Configuration Manager 應用程式  

1.  在 Configuration Manager 主控台的 [軟體程式庫] 工作區中，展開 [應用程式管理]，然後按一下 [市集應用程式的授權資訊]。  

2.  [已購買的商務用 Windows 市集應用程式] 清單會顯示已從市集同步處理的應用程式清單。 選擇要部署的應用程式，然後在 [常用] 索引標籤的 [建立] 群組中，按一下 [建立應用程式]。  

3.  建立 Configuration Manager 應用程式以包含商務用 Windows 市集應用程式。 然後可以如處理任何其他 Configuration Manager 應用程式一樣，部署及監視此應用程式。  

##  <a name="BKMK_PFW"></a> 對 Microsoft Passport for Work 管理的改進  
 您現在可以將 Passport for Work 原則部署到已加入網域且受 Configuration Manager 用戶端管理的 Windows 10 裝置。  

##  <a name="bkmk_switchsup"></a> 可供用戶端切換到新軟體更新點的選項  
 在 1604 Technical Preview 中，您可以啟用可供 Configuration Manager 用戶端在主動式軟體更新點發生問題時切換到新軟體更新點的選項。 針對此選項，主要站台上必須要有多個軟體更新點。 您可以在裝置集合中啟用此選項，而且一旦啟用，集合中的用戶端就會在無法順利連線到主動式軟體更新點時，於下次掃描尋找另一個軟體更新點。 根據 WSUS 組態設定 (更新分類、產品等)，切換到新軟體更新點將會產生額外的網路流量。 因此，您應該只在必要時才使用此選項。  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>啟用切換軟體更新點的選項  

1.  在 Configuration Manager 主控台中，移至 **[資產與相容性] > [概觀] > [裝置集合]**。  

2.  在 **[首頁]** 索引標籤的 **[集合]** 群組中，按一下 **[用戶端通知]**，然後按一下 **[切換至下一個軟體更新點]**。  

> [!NOTE]  
>  只有在具有多個軟體更新點的站台上才會提供此選項。  

##  <a name="bkmk_peercache"></a> 可管理用戶端快取設定和用戶端對等快取的用戶端設定  
 Technical Preview 版本 1604 導入了兩個影響用戶端快取使用的新裝置用戶端設定。 兩者可個別使用，但是是在相同的用戶端設定屬性工作表上設定，並且可相結合來協助您管理對遠端位置中用戶端的內容部署。  

-   首先是**用戶端對等快取**，這是一個內建的 Configuration Manager 解決方案，可讓用戶端直接從其本機快取將內容與其他用戶端共用。 若要讓「對等快取」用戶端共用內容，它們必須是相同界限群組的成員。 對等快取不會取代其他解決方案 (例如 BranchCache) 的使用，而是可並行運作來提供您更多選項以擴充傳統內容部署解決方案 (例如發佈點)。  

     將啟用對等快取的用戶端設定部署至集合之後，該集合的成員可以作為其界限群組中其他用戶端的對等內容來源。  以對等內容來源運作的用戶端將會提交已快取至其管理點的可用內容清單。 之後，當該界限群組中的下一個用戶端要求該內容時，就會以潛在內容來源及形式提供對等快取來源，並將所有發佈點設定為快速。 用戶端會從這個合併的內容來源集區中隨機選取內容來源。 如果界限群組中沒有快速發佈點或對等快取來源，用戶端只會從設定為慢速的發佈點搜尋內容。  

-   第二項新設定可讓您**管理用戶端上的快取大小**。 您可以設定讓快取擁有以 MB 為單位的大小上限，以及以用戶端磁碟機空間百分比表示的大小上限。  用戶端會強制執行先到達的設定。  

為了協助您了解用戶端對等快取的用法，您可以檢視 [Client Data Sources]\(用戶端資料來源) 儀表板。 在主控台中，移至 [監視] > [用戶端狀態] > [Client Data Sources]\(用戶端資料來源)。 您可以在這裡選取一個要套用到儀表板的時段。 然後，在顯示中，您可以選取您想要檢視資訊的界限群組或套件。 檢視資訊時，您可以將滑鼠游標暫留在介面上，以查看有關不同內容或原則來源的更多詳細資料。  

 您也可以使用新報告「用戶端資料來源 - 摘要」來檢視每個界限群組的用戶端資料來源摘要。   
**使用對等快取的需求︰**  

-   您必須為您的站台設定一個**網路存取帳戶**，此帳戶要能夠**完全控制**每個用戶端上的快取資料夾。 此資料夾預設為 **%windir%\ccmcache**  

-   當用戶端為相同界限群組的成員時，它們只能使用「對等快取」來傳輸內容。  

#### <a name="to-configure-client-peer-cache-client-settings"></a>設定用戶端對等快取的用戶端設定  

1.  這兩項設定會在相同的用戶端設定頁面上進行。 在 Configuration Manager 主控台中，移至 [系統管理] > [用戶端設定]，然後開啟您要使用的裝置用戶端設定物件。 您也可以修改 [預設用戶端設定] 物件。  

2.  從可用的設定清單中，選取 [用戶端快取設定]。  

3.  若要管理快取的大小，請將 [設定用戶端快取大小] 設定為 [是]。 然後您可以設定最大快取大小，並以 MB 和用戶端磁碟機空間百分比為單位。  

4.  若要讓用戶端參與用戶端對等快取，請將 [在完整作業系統中啟用 Configuration Manager 用戶端以共用內容] 設定為 [是]。 然後您可以設定用戶端所使用的連接埠，包括是否將以 HTTP 或 HTTPS 連接。  

### <a name="try-it-out"></a>試試看！  
 請嘗試完成下列工作，然後使用本主題頂端附近的意見反應資訊，告訴我們工作的成效：  

1.  修改用戶端設定，以指定新的用戶端快取大小，然後在用戶端上確認這項設定。  

2.  使用用戶端設定來設定要使用對等快取的多個用戶端  

3.  將內容部署到用戶端，讓一些或大多數用戶端可以透過使用對等快取從另一個用戶端取得該內容。  您可以檢視新儀表板來確認使用的內容來源。  

    > [!NOTE]  
    >  若要使用 Technical Preview 和單一發佈點來完成這項工作，請針對您所有用戶端的網路連線，將發佈點設定成慢一點。 然後，將內容發佈到單一用戶端。  在該用戶端取得內容之後，您可以將內容發佈到額外的用戶端，這些用戶端應該會先找到本機對等電腦來做為內容來源，然後才使用從用戶端位置被視為太慢的發佈點。  

##  <a name="bkmk_passport"></a> 對以 Passport for Work 做為 KSP 的支援  
 System Center Configuration Manager 可讓您與 Microsoft Passport for Work 整合，這是一個使用 Active Directory 或 Azure Active Directory 帳戶來取代密碼、智慧卡或虛擬智慧卡的替代登入方法。  
Passport 可讓您使用使用者筆勢登入，而不使用密碼。 使用者筆勢可能是簡單的 PIN、生物識別驗證 (例如 Windows Hello) 或外部裝置 (例如指紋辨識器)。  

-   您可以使用 Configuration Manager 來控制使用者可以和不可以使用哪些筆勢來進行登入，以及設定 PIN 複雜度需求。  

-   您可以將驗證憑證儲存在 Passport for Work 金鑰儲存提供者 (KSP) 中。  

當使用者建立 Passport PIN 時，Windows 會傳送 Configuration Manager 會接聽的通知。  這可讓 Configuration Manager 快速察覺哪些使用者已建立 Passport PIN。 如果 Passport 被用來當作憑證設定檔中的「金鑰儲存提供者」，Configuration Manager 便可接著一併發行新的憑證給這些使用者。  

##  <a name="bkmk_onpremdha"></a> 內部部署裝置健康情況證明  
 Windows 10 裝置的健康情況證明現在可以設定為使用內部部署基礎結構來進行通訊。  系統管理員可以指定是要透過雲端還是內部部署資源來執行報告。  如果選取 [內部部署] 來執行健康情況證明報告，便可接著指定服務的 URI。 這可讓無法存取網際網路的用戶端電腦使用健康情況證明來啟用和管理裝置。  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>為內部部署裝置啟用健康情況證明  

1.  在 Configuration Manager 主控台中，瀏覽至 **[系統管理]** > **[概觀]** > **[用戶端設定]**，然後將 **[使用內部部署健康情況證明服務]** 設定為 **[是]**。  

2.  指定 **[內部部署健康情況證明服務 URL]**，然後按一下 **[確定]**。  

若要試試看，請使用用戶端代理程式設定來設定內部部署「健康情況證明服務」。  

##  <a name="BKMK_Smart"></a> 適用於 Android 裝置的 SmartLock 設定  
 新的設定 [允許 SmartLock 和其他信任代理程式] 已新增至 [Android 和 Samsung KNOX] 設定項目，可讓您控制相容 Android 裝置上的 SmartLock 功能。 此電話功能 (有時也稱為信任代理程式) 可讓您在裝置位於受信任的位置 (例如連線到特定的藍牙裝置或靠近 NFC 標記) 時，停用或略過裝置鎖定畫面密碼。 您可以使用此設定來防止使用者設定 SmartLock。  
