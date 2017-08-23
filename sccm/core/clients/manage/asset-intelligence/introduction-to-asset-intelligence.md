---
title: "Asset Intelligence 簡介 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的 Asset Intelligence 簡介。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 879dc3f04f361af955afbc4db180d097073e8d41
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-asset-intelligence-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Asset Intelligence 簡介

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 中的 Asset Intelligence 可讓您使用 Asset Intelligence 類別目錄，清查和管理整個企業的軟體授權使用情形。 豐富的硬體清查 Windows Management Instrumentation (WMI) 類別可提升所使用之硬體和軟體項目相關收集資訊的全面性， 並提供 60 多種格式簡單好用的報告以呈現這項資訊。 這當中有許多報告可連結至更特定的報告，供您在其中查詢一般資訊，並向下鑽研至更詳細的資訊。 您可以將自訂資訊新增至 Asset Intelligence 類別目錄，例如自訂的軟體類別、軟體系列、軟體標籤和硬體需求。 您也可以連線至 System Center Online，以可用的最新資訊動態更新 Asset Intelligence 類別目錄。 Microsoft 客戶可以將軟體授權資訊匯入 Configuration Manager 站台資料庫，以協調企業軟體授權使用量與已使用的購買軟體授權。  

##  <a name="BKMK_AssetIntelligenceCatalog"></a> Asset Intelligence 類別目錄  

 Configuration Manager Asset Intelligence 類別目錄是一組儲存在站台資料庫中的資料庫資料表，其中包含超過 300,000 種軟體項目及版本的分類和識別資訊。 這些資料庫資料表也可用來管理特定軟體項目的硬體需求。  

 Asset Intelligence 類別目錄提供正在使用之軟體項目的軟體授權資訊，包括 Microsoft 和非 Microsoft 軟體。 Asset Intelligence 類別目錄也提供一組軟體項目的預先定義硬體需求，您可以建立新的使用者定義硬體需求資訊，以符合自訂需求。 此外，您可以自訂 Asset Intelligence 類別目錄中的資訊，並將軟體項目資訊上傳至 System Center Online 以進行分類。  

 您可以定期下載內含新發行軟體的 Asset Intelligence 類別目錄更新，以執行大量類別目錄更新。 或者，您可以使用 Asset Intelligence 同步處理點站台系統角色來動態更新類別目錄。  

###  <a name="BKMK_SoftwareCategories"></a> 軟體類別  
 Asset Intelligence 軟體類別可用來廣泛分類已清查的軟體項目，也可作為更特定之軟體系列的高階分組。 例如，軟體類別可能是能源公司，而該軟體類別內的軟體系列可能是石油與天然氣或水力電氣。 Asset Intelligence 類別目錄中有預先定義許多軟體類別，您可以建立使用者定義的分類，以進一步定義已清查的軟體。 所有預先定義之軟體類別目錄的驗證狀態一律是 [已驗證] ，而新增至 Asset Intelligence 類別目錄的自訂軟體類別目錄資訊則是 [使用者定義] 。 如需如何管理軟體類別的詳細資訊，請參閱[設定 System Center Configuration Manager 中的 Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

> [!NOTE]  
>  Asset Intelligence 類別目錄中儲存的預先定義軟體類別目錄資訊是唯讀，而且無法將其變更或刪除。 系統管理使用者可以新增、修改或刪除使用者定義的軟體類別。  

###  <a name="BKMK_SoftwareFamilies"></a> 軟體系列  
 Asset Intelligence 軟體系列可用來定義軟體類別中已清查的軟體項目。 Asset Intelligence 類別目錄中有預先定義許多軟體系列，您可以建立使用者定義的分類，以進一步定義已清查的軟體。 所有預先定義之軟體系列的驗證狀態一律是 [已驗證] ，而新增至 Asset Intelligence 類別目錄的自訂軟體系列資訊則是 [使用者定義] 。 如需如何管理軟體系列的詳細資訊，請參閱[設定 System Center Configuration Manager 中的 Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

> [!NOTE]  
>  預先定義的軟體系列資訊是唯讀，而且無法變更。 系統管理使用者可以新增、修改或刪除使用者定義的軟體系列。  

###  <a name="BKMK_CustomLabels"></a> 軟體標籤  
 Asset Intelligence 自訂軟體標籤可讓您建立篩選器以群組軟體項目，並使用 Asset Intelligence 報告來檢視它們。 您可以使用軟體標籤，建立共用相同屬性之軟體項目的使用者定義群組。 比方說，您可以建立一個稱為「共享軟體」的軟體標籤，再將該軟體標籤與已清查的共享軟體項目建立關聯，並執行報告以顯示具有相關聯「共享軟體」軟體標籤的所有軟體項目。 系統不提供預先定義的軟體標籤。 因此，軟體標籤的驗證狀態一律是 [使用者定義] 。 如需如何管理軟體標籤的詳細資訊，請參閱[設定 System Center Configuration Manager 中的 Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

###  <a name="BKMK_HardwareRequirements"></a> 硬體需求  
 您可以使用硬體需求的資訊，確認電腦符合軟體項目的硬體需求之後，再將它們設為軟體部署的目標。 您可以在 [資產與相容性]  工作區中 [Asset Intelligence]  節點下的 [硬體需求]  節點，管理軟體項目的硬體需求。 Asset Intelligence 類別目錄提供許多預先定義的硬體需求，您也可以建立新的使用者定義硬體需求資訊，以符合自訂需求。 所有預先定義之硬體需求的驗證狀態一律是 [已驗證] ，而新增至 Asset Intelligence 類別目錄的使用者定義硬體需求資訊則是 [使用者定義] 。 如需如何管理硬體需求的詳細資訊，請參閱[設定 System Center Configuration Manager 中的 Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

> [!NOTE]  
>  Configuration Manager 主控台中顯示的硬體需求是擷取 Asset Intelligence 類別目錄，而不是以 System Center 2012 Configuration Manager 用戶端中的已清查軟體項目資訊為依據。 硬體需求的資訊不會與 System Center Online 同步處理程序一起更新。 針對沒有相關聯硬體需求的已清查軟體，您可以建立使用者定義的硬體需求。  

 根據預設，每個列出的硬體需求會顯示下列資訊：  

-   **軟體項目**：指定與硬體需求相關聯的軟體項目。  

-   **CPU 下限 (MHz)**：指定軟體項目所需的最低處理器速度 (MHz)。  

-   **RAM 下限 (KB)**：指定軟體項目所需的最小 RAM (KB)。  

-   **磁碟空間下限 (KB)**：指定軟體項目所需的最小可用硬碟空間 (KB)。  

-   **磁碟大小下限 (KB)**：指定軟體項目所需的最小可用硬碟大小 (KB)。  

-   **驗證狀態**：指定硬體需求的驗證狀態。  

 儲存在 Asset Intelligence 類別目錄中的預先定義硬體需求是唯讀，而且無法刪除。  系統管理使用者可以新增、修改或刪除未儲存在 Asset Intelligence 類別目錄中的使用者定義之軟體項目硬體需求。  

##  <a name="BKMK_InventoriedSoftwareTitles"></a> 已清查的軟體項目  
 您可以在 [資產與相容性]  工作區中 [Asset Intelligence]  節點下的 [已清查的軟體]  節點，檢視已清查的軟體項目資訊。 硬體清查用戶端代理程式會依據儲存在 Asset Intelligence 類別目錄中的軟體項目，從 Configuration Manager 用戶端收集已清查的軟體資訊。  

> [!WARNING]  
>  硬體清查用戶端代理程式會根據您啟用的 Asset Intelligence 報告類別，來收集清查項目。 如需如何啟用報告類別的詳細資訊，請參閱[設定 System Center Configuration Manager 中的 Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

 根據預設，每個列出的已清查軟體項目會顯示下列資訊：  

-   **名稱**：指定已清查軟體項目的名稱。  

-   **廠商**：指定開發已清查軟體項目的廠商名稱。  

-   **版本**：指定已清查軟體項目的產品版本。  

-   **類別**：指定目前指派給已清查軟體項目的軟體類別。  

-   **系列**：指定目前指派給已清查軟體項目的軟體系列。  

-   **標籤** [**1**、 **2**和 **3**]：指定與軟體項目相關聯的自訂標籤。 已清查的軟體項目最多可以有三個與其相關聯的自訂標籤。  

-   **計數**：指定已清查軟體項目的 Configuration Manager 用戶端數目。  

-   **狀態**：指定已清查軟體項目的驗證狀態。  

> [!NOTE]  
>  您僅可變更階層中頂層網站的已清查軟體分類資訊 (產品名稱、廠商、軟體類別與軟體系列)。 修改預先定義的軟體分類資訊之後，軟體的驗證狀態會從 [已驗證]  變更為 [使用者定義] 。  

##  <a name="AssetIntelligenceSycnronizationPoint"></a> Asset Intelligence 同步處理點  
 Asset Intelligence 同步處理點是一種 Configuration Manager 站台系統角色，其可用來連線至 System Center Online (使用 TCP 連接埠 443)，以動態管理 Asset Intelligence 類別目錄資訊的更新。 此站台角色只能安裝在階層的頂層網站上。 您必須使用連線至頂層網站的 Configuration Manager 主控台，來設定所有 Asset Intelligence 類別目錄的自訂項目。 雖然您必須在頂層站台中設定所有更新，但系統會將 Asset Intelligence 類別目錄資訊複寫到階層中的其他站台。 Asset Intelligence 同步處理點站台角色可讓您要求隨選同步處理 System Center Online 或排程自動類別目錄同步處理。 除了下載新的 Asset Intelligence 類別目錄資訊，Asset Intelligence 同步處理點還可以將自訂軟體項目資訊上傳至 System Center Online 以便分類。 Microsoft 會將所有上傳至 System Center Online 的軟體項目分類為公用資訊。 因此，請確認您自訂的軟體項目不含機密或專利資訊。  

> [!NOTE]  
>  未分類的軟體項目提交之後，若有客戶對相同軟體項目提出 4 個以上的分類要求時，System Center Online 研究人員會識別、分類，然後將軟體項目分類資訊提供給所有使用線上服務的客戶。 分類要求數最多的軟體項目，其分類優先順序最高。 自訂軟體和企業營運應用程式不太可能會收到分類，因此最佳做法是不要將這類軟體項目傳送給 Microsoft 進行分類。  

> [!NOTE]  
>  需具備 Asset Intelligence 同步處理點站台系統角色，才能連線到 System Center Online。 如需如何安裝 Asset Intelligence 同步處理點的資訊，請參閱[設定 System Center Configuration Manager 中的 Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

##  <a name="BKMK_AssetIntelligenceHomePage"></a> Asset Intelligence 首頁  
 [資產與相容性] 工作區中的 [Asset Intelligence] 節點即為 Configuration Manager 的 Asset Intelligence 首頁。 [Asset Intelligence]  首頁會顯示 Asset Intelligence 類別目錄資訊的摘要儀表板檢視。  

> [!NOTE]  
>  在檢視 [Asset Intelligence]  首頁期間，首頁不會自動更新。  

 [Asset Intelligence]  首頁包括下列區段：  

-   **類別目錄同步處理**：提供是否啟用 Asset Intelligence 以及 Asset Intelligence 同步處理點目前狀態的相關資訊。 本區段也提供同步處理排程、客戶授權聲明是否匯入、上次更新狀態的時間、下次排定的更新時間，以及安裝 Asset Intelligence 同步處理點站台系統之後發生的變更數目。  

    > [!NOTE]  
    >  僅有安裝 Asset Intelligence 同步處理點站台系統角色之後，[Asset Intelligence]  首頁的 Asset Intelligence 類別目錄同步處理區段才會顯示。  

-   **已清查的軟體狀態**：提供由 Microsoft 識別、系統管理員識別、擱置的線上識別或無法辨識但未擱置的已清查軟體、軟體類別及軟體系列的計數和百分比。 這些資訊會以表格格式顯示各項計數，並以圖表顯示各項百分比。  

##  <a name="BKMK_AssetIntelligenceReports"></a> Asset Intelligence 報告  
 在 Configuration Manager 主控台中，Asset Intelligence 報告位於 [監視] 工作區之 [報告]  節點下的 Asset Intelligence 資料夾中。 這份報告提供硬體、授權管理和軟體的相關資訊。 如需 Configuration Manager 報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../../../core/servers/manage/reporting.md)。  

> [!NOTE]  
>  Asset Intelligence 報告中顯示的已安裝軟體項目數量及授權資訊的精確度，可能會與已安裝的實際軟體項目數量或環境中已使用的授權數量有所不同。 因為要清查企業環境中安裝的軟體項目之軟體授權資訊涉及到複雜的相依性與限制，因此會造成這項差異。 請不要將 Asset Intelligence 報告作為判斷購買的軟體授權相容性的唯一來源。  

###  <a name="BKMK_HardwareReports"></a> Asset Intelligence 硬體報告  
 Asset Intelligence 硬體報告提供組織中硬體資產的相關資訊。 Asset Intelligence 硬體報告可藉由使用速度、記憶體、週邊裝置等硬體清查資訊，呈現 USB 裝置與必須升級的硬體等相關資訊，包括尚未準備好進行特定軟體升級的電腦相關資訊。  

> [!NOTE]  
>  Asset Intelligence 硬體報告會從系統安全性事件記錄檔中收集部分使用者資料。 為保障較佳的報告精確度，建議您在重新指派電腦給新使用者時清除此記錄檔。  

###  <a name="BKMK_LicenseManagementReports"></a> Asset Intelligence 授權管理報告  
 Asset Intelligence 授權管理報告提供正在使用的授權相關資料。 授權分類帳報告會使用與 Microsoft 授權聲明 (MLS) 一致的格式列出已安裝的 Microsoft 應用程式。 這是一種方便的方法，可供您比對已使用授權和所購買的授權。 其他授權管理報告則提供作為執行金鑰管理服務 (KMS) 之伺服器的電腦相關資訊，以取得作業系統啟用統計資料。  

> [!IMPORTANT]  
>  若干 Asset Intelligence 授權管理報告會顯示 KMS 函式的相關資訊，其為管理大量授權的方法。 如果尚未實作 KMS 伺服器，有些報告可能不會傳回任何資料。 如需 KMS 的詳細資訊，請在 [Microsoft TechNet](http://go.microsoft.com/fwlink/?linkid=3225)上搜尋 KMS。  

###  <a name="BKMK_SoftwareReports"></a> Asset Intelligence 軟體報告  
 Asset Intelligence 軟體報告提供安裝在組織電腦上的軟體系列、類別以及特定軟體項目等相關資訊。 軟體報告顯示瀏覽器協助程式物件與自動啟動的軟體等相關資訊。 這些報告可用來識別廣告軟體、間諜軟體及其他惡意程式碼，並識別軟體備援，以協助簡化軟體購買及支援。  

###  <a name="BKMK_SoftwareIdTagReports"></a> Asset Intelligence 軟體識別標記報告  
 Asset Intelligence 軟體識別標記報告提供包含符合 ISO/IEC 19770-2 之軟體識別標記的軟體相關資訊。 軟體識別標記會提供用來識別已安裝軟體的授權資訊。 在您啟用 SMS_SoftwareTag Asset Intelligence 硬體清查報告類別時，Configuration Manager 即會收集包含軟體識別標記之軟體的相關資訊。 下列報告提供軟體相關資訊：  

-   **軟體 14A – 搜尋已啟用軟體識別標記的軟體**：這份報告提供具有啟用軟體識別標記的已安裝軟體計數。  

-   **軟體 14B – 安裝啟用特定軟體識別標記之軟體的電腦**：這份報告列出已安裝啟用了特定軟體識別標記之軟體的所有電腦。  

-   **軟體 14C – 特定電腦上安裝的已啟用軟體識別標記的軟體**：此報告會列出在特定電腦上已啟用特定軟體識別標記的所有已安裝軟體。  

###  <a name="BKMK_ReportingLImitations"></a> Asset Intelligence 報告限制  
 Asset Intelligence 報告提供已安裝軟體項目與正在使用之購買軟體授權的大量相關資訊。 不過，您不應該將這項資訊作為判斷購買之軟體授權相容性的唯一來源。  

####  <a name="BKMK_ExampleDependencies"></a> 相依性範例  
 Asset Intelligence 報告中顯示的已安裝軟體項目數量及授權資訊的精確度，可能會與目前已使用的實際數量有所不同。 因為要清查企業環境中所使用的軟體項目之軟體授權資訊涉及到複雜的相依性，因此會造成這項差異。 下列範例說明使用 Asset Intelligence 清查企業中已安裝軟體涉及的相依性，其可能會影響 Asset Intelligence 報告的精確度：  

 **用戶端硬體清查相依性**  
 Asset Intelligence 已安裝軟體報告的資料收集來源是 Configuration Manager 用戶端，作法是藉由擴充硬體清查來啟用 Asset Intelligence 報告。 這種硬體清查報告的相依性導致 Asset Intelligence 報告僅會反映來自下列用戶端的資料：順利完成硬體清查處理程序且已啟用必要 Asset Intelligence WMI 報告類別的 Configuration Manager 用戶端。 此外，由於 Configuration Manager 用戶端是依據系統管理使用者所定義的排程來執行硬體清查處理程序，因此資料報告時可能會發生延遲並影響 Asset Intelligence 報告的精確度。 比方說，在用戶端成功完成硬體清查週期後，其中某個已清查的授權軟體項目可能被解除安裝。 不過，直到用戶端下一個排定的硬體清查報告週期為止，Asset Intelligence 報告都會將該軟體項目顯示為已安裝。  

 **軟體封裝相依性**  
 由於 Asset Intelligence 報告的依據是使用標準 Configuration Manager 用戶端硬體清查處理程序收集的已安裝軟體項目資料，因此部分軟體項目資料的收集可能有誤。 例如，不符合標準安裝處理程序的軟體安裝，或在安裝以前有所變更的軟體安裝，都可能會導致不正確的 Asset Intelligence 報告。  

####  <a name="BKMK_LegalLimitations"></a> 法律限制  
 Asset Intelligence 報告顯示的資訊可能會有許多限制，其中顯示的資訊亦不代表法律、會計或其他方面的專業意見。 Asset Intelligence 報告所提供的資訊僅供參考，不應作為判斷軟體授權使用量相容性的唯一資訊來源。  

 下列為使用 Asset Intelligence 清查企業中已安裝軟體與授權使用量涉及的限制範例，其可能會影響 Asset Intelligence 報告的精確度：  

 **Microsoft 授權使用數量限制**  
 -   購買的 Microsoft 軟體授權數量是以系統管理員提供的資訊為依據，因此，您應仔細檢閱以確保提供的軟體授權數目正確。  

-   回報的 Microsoft 軟體授權數量僅包含透過大量授權方案取得之 Microsoft 軟體授權的相關資訊，並不會反映透過零售、OEM 或其他軟體授權銷售通路取得之軟體授權的資訊。  

-   由於軟體轉銷商的報告需求和排程所致，回報的 Microsoft 軟體授權數量可能不會納入前 45 天內取得的軟體授權。  

-   因公司合併或收購導致的軟體授權移轉可能不會反映在 Microsoft 軟體授權數量中。  

-   Microsoft 大量授權 (MVLS) 協議中的非標準條款及條件可能會影響回報的軟體授權數目，因此，可能需由 Microsoft 代表再行審閱。  

 **已安裝的軟體項目數量限制**  
 Configuration Manager 用戶端必須成功完成硬體清查報告週期，Asset Intelligence 報告才能準確地回報已安裝的軟體項目數量。 此外，在成功的硬體清查報告之後，如果 Asset Intelligence 報告在用戶端回報下一個排定硬體清查之前執行，報告就不會反映安裝或解除安裝已授權的軟體項目之間的延遲。  

 **授權對帳限制**  
 購買的軟體授權數量與已安裝軟體項目的對帳數量計算方式如下：依據系統管理員設定的排程，比較系統管理員指定的授權數量和從 Configuration Manager 用戶端硬體清查收集的已安裝軟體項目數量。 這項比較不代表 Microsoft 的最終授權定位結論。 實際的授權定位取決於特定軟體項目授權和授權條款授與的使用量權限。  

##  <a name="BKMK_ValidationStates"></a> Asset Intelligence 驗證狀態  
 Asset Intelligence 驗證狀態代表 Asset Intelligence 類別目錄資訊的來源和目前驗證狀態。 下表說明可能的 Asset Intelligence 驗證狀態，以及會造成這些狀態的系統管理員動作。  

|**狀態**|**定義**|**系統管理員動作**|**註解**|  
|---------------|--------------------|------------------------------|-----------------|  
|**Validated**|System Center Online 研究人員已定義類別目錄項目。|無。|最佳狀態。|  
|**User Defined**|System Center Online 研究人員未定義類別目錄項目。|自訂本機類別目錄資訊。|此狀態會顯示在 Asset Intelligence 報告中。|  
|**擱置**|System Center Online 研究人員未定義類別目錄項目，但項目已提交給 System Center Online 進行分類。|System Center online 已要求分類。|類別目錄項目會維持此狀態，直到 System Center Online 研究人員分類好項目並同步處理 Asset Intelligence 類別目錄為止。|  
|**可更新**|System Center Online 在後續的類別目錄同步處理期間，已使用不同的方式分類使用者定義的類別目錄項目。|自訂本機 Asset Intelligence 類別目錄，以將項目分類為使用者定義。|您可以使用 [解決衝突] 動作決定要使用新的分類資訊或使用之前的使用者定義值。 如需如何解決衝突的詳細資訊，請參閱 [System Center Configuration Manager 中 Asset Intelligence 的作業](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)。|  
|**未分類**|System Center Online 研究人員尚未定義類別目錄項目、項目未提交至 System Center Online 以進行分類，以及系統管理員尚未指派使用者定義的分類值。|無。|要求分類或自訂本機類別目錄資訊。<br /><br /> 如需要求分類的詳細資訊，請參閱 [System Center Configuration Manager 中 Asset Intelligence 的作業](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)。<br /><br /> 如需如何變更軟體項目之類別目錄的詳細資訊，請參閱 [System Center Configuration Manager 中 Asset Intelligence 的作業](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)。|  

> [!NOTE]  
>  提交至 System Center Online 以進行分類的類別目錄項目，其在管理中心網站上的驗證狀態皆為 [擱置中]  ，但在子主要站台上會繼續顯示 [未分類]  驗證狀態。  

> [!NOTE]  
>  分類衝突解決後，只要之後的分類更新沒有導入新的項目資訊，就不會再將項目驗證為衝突。  

 如需何時會轉換驗證狀態的範例，請參閱 [System Center Configuration Manager 的 Asset Intelligence 驗證狀態轉換範例](../../../../core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence.md)。  
