---
title: "管理軟體更新的設定 | Microsoft Docs"
description: "深入了解安裝軟體更新點後，適合網站更新軟體的用戶端設定。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/26/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
ms.openlocfilehash: fe4a8f56e0b554e206bcc4503a0268dc761ded81
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_ManageSUSettings"></a> 管理軟體更新的設定  

*適用於：System Center Configuration Manager (最新分支)*

在 Configuration Manager 中同步處理軟體更新後，設定並確認下列各區段中的設定。

##  <a name="BKMK_ClientSettings"></a> 軟體更新的用戶端設定  
在您安裝軟體更新點後，用戶端上會預設啟用軟體更新，而且用戶端設定中 [軟體更新]  頁面上的設定會包含預設值。 用戶端設定可用於全網站，並會影響掃描軟體更新相容性的時機，以及在用戶端電腦上安裝軟體更新的方式和時機。 部署軟體更新之前，請先確認用戶端設定是否適合您網站上的軟體更新。  

> [!IMPORTANT]  
>  預設會啟用 [在用戶端上啟用軟體更新]  設定。 如果您清除此設定，Configuration Manager 會從用戶端移除現有部署原則。  

如需如何設定用戶端設定的資訊，請參閱[如何在 Configuration Manager 中設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。  

如需用戶端設定的詳細資訊，請參閱[關於 Configuration Manager 中的用戶端設定](../../core/clients/deploy/about-client-settings.md)。  

##  <a name="BKMK_GroupPolicy"></a> 軟體更新的群組原則設定  
用戶端電腦上有 Windows Update 代理程式 (WUA) 所使用的特定群組原則設定，這些設定用來連線至軟體更新點上執行的 WSUS。 這些群組原則設定也會用來成功掃描軟體更新相容性，並且自動更新軟體更新和 WUA。

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>指定近端內部網路 Microsoft 更新服務之位置的本機原則  
建立站台的軟體更新點時，用戶端會收到提供軟體更新點伺服器名稱，以及在電腦上設定 [指定近端內部網路 Microsoft 更新服務的位置]  本機原則的電腦原則。 WUA 會擷取 [設定偵測更新的近端內部網路更新服務]  設定中指定的伺服器名稱，然後在掃描軟體更新相容性時連線至此伺服器。 建立 [指定近端內部網路 Microsoft 更新服務的位置]  設定的網域原則時，它會覆寫本機原則，而 WUA 可能會連線至軟體更新點以外的伺服器。 如果發生這種情形，用戶端可能會根據不同的產品、分類和語言掃描軟體更新相容性。 因此，您應該不要設定用戶端電腦的 Active Directory 原則。  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>允許來自內部網路 Microsoft 更新服務位置的已簽署內容群組原則  
您必須先啟用 [允許來自內部網路 Microsoft 更新服務位置的已簽署內容]  群組原則設定，電腦上的 WUA 才會掃描透過 System Center 更新發行者建立和發佈軟體更新。 啟用此原則設定時，如果軟體更新已在本機電腦上的 [受信任的發行者]  憑證存放區中簽署，則 WUA 將接受透過近端內部網路位置接收的軟體更新。 如需更新發行者所需群組原則設定的詳細資訊，請參閱 [Updates Publisher 2011 Documentation Library (更新發行者 2011 文件庫)](http://go.microsoft.com/fwlink/p/?LinkId=232476)。  

### <a name="automatic-updates-configuration"></a>自動更新設定  
自動更新允許在用戶端電腦上接收安全性更新和其他重要的下載。 自動更新是透過 [設定自動更新]  群組原則設定，或透過本機電腦上的 [控制台] 設定。 當自動更新啟用時，用戶端電腦將接收更新通知，而且用戶端電腦將根據所設的設定下載及更新所需的更新。 如果自動更新與軟體更新並存，每一部用戶端電腦都可顯示通知圖示，並且快顯相同更新的通知。 另外，需要重新啟動時，每一部用戶端電腦可顯示相同更新的重新啟動對話方塊。  

### <a name="self-update"></a>自行更新  
若用戶端電腦上啟用自動更新，則在提供較新版本或 WUA 元件發生問題時，WUA 會自動執行自行更新。 若未設定或停用自動更新，且用戶端電腦使用舊版 WUA，則用戶端電腦必須執行 WUA 安裝檔案。  

## <a name="software-updates-properties"></a>軟體更新內容
軟體更新內容可提供有關軟體更新與相關聯內容的資訊。 您也可以使用這些內容設定軟體更新的設定。 當您開啟多個軟體更新的內容時，只會顯示 [執行時間上限]  和 [自訂嚴重性]  索引標籤。   

利用下列程序開啟軟體更新內容。  

#### <a name="to-open-software-update-properties"></a>開啟軟體更新內容  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  
2.  在 [軟體程式庫] 工作區中，展開 [軟體更新] ，然後按一下 [所有軟體更新] 。  
3.  選取一個或多個軟體更新，然後在 [首頁]  索引標籤上，按一下 [內容]  群組中的 [內容]  。  

   > [!NOTE]  
   >  在 [所有軟體更新] 節點 上，Configuration Manager 只會顯示在過去 30 天內發行且分類為 [重大] 和 [安全性] 的軟體更新。  

###  <a name="BKMK_SoftwareUpdatesInformation"></a> 檢閱軟體更新資訊  
在軟體更新內容中，您可以檢閱有關軟體更新的詳細資訊。 當您選取一個以上的軟體更新時不會顯示詳細資訊。 以下章節將說明適用於所選取軟體更新的資訊。  

####  <a name="BKMK_SoftwareUpdateDetails"></a> 軟體更新詳細資料  
在 [更新詳細資料]  索引標籤中，您可以檢視以下有關所選取軟體更新的摘要資訊：  

- **公告識別碼**：指定已與安全性軟體更新建立關聯的公告識別碼。 您可以在 [TechNet 資訊安全技術中心](http://go.microsoft.com/fwlink/p/?LinkId=58313) 網頁搜尋公告識別碼來尋找資訊安全佈告欄的詳細資料。  

- **發行項識別碼**：指定軟體更新的發行項識別碼。 參照的發行項能提供更多關於軟體更新的詳細資訊，以及軟體更新修正或改善的問題。  

- **修訂日期**：指定上次修改軟體更新的日期。  

- **最大嚴重性等級**：指定由廠商定義的軟體更新嚴重性等級。  

- **描述**：提供軟體更新修正或改進狀況的概觀。  

- **適用的語言**：列出軟體更新適用的語言。  

- **受影響的產品**：列出軟體更新適用的產品。  

####  <a name="BKMK_ContentInformation"></a> 內容資訊  
在 [內容資訊]  索引標籤中，檢閱以下與所選軟體更新相關聯之內容的相關資訊。  

-   **內容識別碼**：指定軟體更新的內容識別碼。  

-   **已下載**：指出 Configuration Manager 是否已經下載軟體更新檔案。  

-   **語言**：指定軟體更新的語言。  

-   **來源路徑**：指定軟體更新來源檔案的路徑。  

-   **大小 (MB)**：指定軟體更新來源檔案的大小。  

####  <a name="BKMK_CustomBundleInformation"></a> 自訂配套資訊  
在 [自訂配套資訊]  索引標籤中，檢閱軟體更新的自訂配套資訊。 所選取的軟體更新包含納入軟體更新檔案的配套軟體更新時，會在 [配套資訊]  區段中顯示出來。 此索引標籤不會顯示 [內容資訊]  索引標籤中所顯示的配套軟體更新，例如不同語言的更新檔案。  

####  <a name="BKMK_SupersedenceInformation"></a> 取代資訊  
您可以在 [取代資訊]  索引標籤上，檢視軟體更新取代的下列資訊：  

- **此更新已由下列更新取代**：指定取代此更新的軟體更新，這表示列出的更新較新。 在大部分情況下，您將部署其中一種取代軟體更新的軟體更新。 顯示在清單中的軟體更新包含網頁的超連結，提供更多有關軟體更新的詳細資訊。 若此更新並未被取代，則會顯示 [無]  。  

- **此更新取代以下更新**：指定由此軟體更新取代的軟體更新，這表示此軟體更新較新。 在大部分情況下，您將部署此軟體更新來替代已遭取代的軟體更新。 顯示在清單中的軟體更新包含網頁的超連結，提供更多有關軟體更新的詳細資訊。 若此更新未取代任何其他更新，則會顯示 [無]  。  

###  <a name="BKMK_SoftwareUpdatesSettings"></a> 設定軟體更新設定  
在內容中，您可以針對一或多個軟體更新設定軟體更新設定。 您可以只在管理中心網站或獨立主要網站上設定大部分的軟體更新設定。 以下各節將協助您設定軟體更新的設定。  

####  <a name="BKMK_SetMaxRunTime"></a> 設定執行階段上限  
於 [執行時間上限]  索引標籤中，設定在用戶端電腦上完成軟體更新所配置的時間上限。 如果更新所需的時間大於執行時間上限值，Configuration Manager 會建立狀態訊息，並停止監視軟體更新安裝的部署。 您可以只在管理中心網站或獨立主要網站上設定此設定。  

Configuration Manager 也使用此設定來判斷是否要在設定的維護期間內起始軟體更新的安裝。 如果執行時間上限值超過維護期間中剩下的時間，則會延遲安裝軟體更新，直到下一個維護期間開始為止。 若有多個軟體更新要安裝在已設定維護期間 (時間範圍) 的用戶端電腦上時，會先安裝具備最低執行時間上限的軟體更新，接著會安裝具備次低執行時間上限的軟體更新，以此類推。 安裝每個軟體更新前，用戶端會驗證可用維護期間是否提供足夠時間來安裝軟體更新。 軟體更新開始安裝後，即使安裝超過維護期間尾端，仍會繼續安裝。 如需維護時段的詳細資訊，請參閱[如何使用 System Center Configuration Manager 的維護時段](../../core/clients/manage/collections/use-maintenance-windows.md)。  

在 [執行時間上限]  索引標籤上，您可以檢視並設定以下設定：  

- **執行時間上限**：指定在 Configuration Manager 不再監視安裝前，為完成軟體更新安裝所配置的分鐘數上限。 此設定也會用來判斷在維護期間結束前，剩下的時間是否足夠安裝更新。 Service Pack 的預設設定為 60 分鐘。 對於其他軟體更新類型，如果您安裝的是 Configuration Manager 1511 版或更新版本的全新安裝，預設值是 10 分鐘，而當您從舊版升級時，則為 5 分鐘。 值的範圍為 5 到 9999 分鐘。  

> [!IMPORTANT]  
>  請確定將執行時間上限值設定為小於設定的維護期間。 否則會永遠無法起始軟體更新安裝。  

####  <a name="BKMK_SetCustomSeverity"></a> 設定自訂嚴重性  
在軟體更新的內容中，您可以使用 [自訂嚴重性]  索引標籤，設定軟體更新的自訂嚴重性值。 若預先定義的嚴重性值不符合您的需求時，這就是必要項目。 自訂值會列在 Configuration Manager 主控台的 [自訂嚴重性] 欄內。 您可利用已定義的自訂嚴重性值來排序軟體更新，也可以建立能篩選這些值的查詢和報告。 您可以只在管理中心網站或獨立主要網站上設定此設定。  

您可以在 [自訂嚴重性]  索引標籤上設定以下設定。  

- **自訂嚴重性**：設定軟體更新的自訂嚴重性值。 從清單選取 [重大] 、[重要] 、[一般] 或 [低]  。 根據預設，自訂嚴重性值為空白。

## <a name="crl-checking-for-software-updates"></a>軟體更新的 CRL 檢查
根據預設，在驗證 System Center Configuration Manager 軟體更新的簽章時，不會檢查憑證撤銷清單 (CRL)。 每次使用憑證時皆檢查，提供比使用已撤銷憑證更多的安全性，但同時也會造成連線延遲，以及對執行 CRL 檢查的電腦產生額外的處理需求。  

如果使用此方法，則必須在處理軟體更新的 Configuration Manager 主控台啟用 CRL 檢查。  

#### <a name="to-enable-crl-checking"></a>啟用 CRL 檢查  
在執行 CRL 檢查的電腦上，從產品 DVD 及命令列提示字元執行下列動作：**\SMSSETUP\BIN\X64\\**<語言>**\UpdDwnldCfg.exe /checkrevocation**。  

例如，針對英文 (美國) 版執行 **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe /checkrevocation**。  
