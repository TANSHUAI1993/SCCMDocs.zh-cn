---
title: "移轉物件 | Microsoft Docs"
description: "了解如何規劃 System Center Configuration Manager 環境中各階層之間的物件移轉。"
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 17f3955aa7c63a13bab03b46002f7de0b0ec38fe
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-system-center-configuration-manager"></a>規劃將 Configuration Manager 物件移轉至 System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*

若使用 System Center Configuration Manager，您就可以移轉在某來源站台找到之與不同功能相關聯的許多不同物件。 使用以下各節有助於規劃各階層之間的物件移轉。  

-   [規劃移轉軟體更新](#Plan_migrate_Software_updates)  

-   [規劃移轉內容](#Plan_Migrate_content)  

-   [規劃移轉集合](#BKMK_MigrateCollections)  

-   [規劃移轉作業系統部署](#Plan_migrate_OSD)  

-   [規劃移轉 Desired Configuration Management](#Plan_Migrate_Compliance_settings)  

-   [規劃移轉界限](#Plan_migrate_Boundaries)  

-   [規劃移轉報告](#Plan_Migrate_reports)  

-   [規劃移轉組織與搜尋資料夾](#Plan_Migrate_Org_Folders)  

-   [規劃移轉 Asset Intelligence 自訂項目](#Plan_Migrate_AI)  

-   [規劃移轉軟體計量規則自訂項目](#Plan_Migrate_SWM_Rules)  

##  <a name="Plan_migrate_Software_updates"></a> 規劃移轉軟體更新  
 您可以移轉軟體更新物件，例如軟體更新套件和軟體更新部署。  

 若要成功移轉軟體更新物件，您必須先設定目的地階層，使其設定與來源階層環境相符。 您需要執行下列動作：  

-   在目的地階層中部署主動式軟體更新點  

-   設定與來源階層的設定相符的產品類別目錄和語言  

-   同步目的地階層中的軟體更新點與 Windows Server Update Services (WSUS)  

當您移轉軟體更新時，請考慮下列各項：  

-   如果您尚未同步目的地階層中的資訊，使其符合來源階層的設定，則軟體更新物件的移轉可能會失敗。  

    > [!WARNING]  
    >  Configuration Manager 不支援使用 WSUSutil 工具在來源與目的地階層之間同步資料。  

-   您無法移轉使用 System Center 更新發行者發佈的自訂更新。 您必須將自訂更新重新發佈至目的地階層。  

當您從 Configuration Manager 2007 來源階層移轉時，移轉程序會將某些軟體更新物件修改為目的地階層使用的格式。 使用下表有助於規劃從 Configuration Manager 2007 移轉軟體更新物件。  

|Configuration Manager 2007 物件|移轉後的物件名稱|  
|-----------------------------------|---------------------------------|  
|軟體更新清單|軟體更新清單會轉換成軟體更新群組。|  
|軟體更新部署|軟體更新部署會轉換成部署和更新群組。<br /><br /> 從 Configuration Manager 2007 移轉軟體更新部署後，必須先在目的地階層啟用，才能進行部署。|  
|軟體更新套件|軟體更新套件仍舊是軟體更新套件。|  
|軟體更新範本|軟體更新範本仍舊是軟體更新範本。<br /><br /> Configuration Manager 2007 部署範本中的 [持續時間] 值不會移轉。|  

從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層移轉物件時，不會修改軟體更新物件。  

##  <a name="Plan_Migrate_content"></a> 規劃移轉內容  
 您可以從支援的來源階層將內容移轉至您的目的地階層。 若是 Configuration Manager 2007 來源階層，此內容會包含軟體發佈套件和程式以及虛擬應用程式，例如 Microsoft Application Virtualization (App-V)。 針對 System Center 2012 Configuration Manager 和 System Center Configuration Manager 來源階層，此內容會包含應用程式與 App-V 虛擬應用程式。 當您在階層之間移轉內容時，壓縮的來源檔案會移轉至目的地階層。  

### <a name="packages-and-programs"></a>封裝和程式  
 當您移轉套件和程式時，移轉作業不會修改它們。 不過在您移轉它們之前，必須先設定每個套件使用通用命名慣例 (UNC) 路徑作為其來源檔案位置。 在設定移轉套件和程式時，您必須指派目的地階層中的網站管理此內容。 內容不會從指派的站台移轉，而是在移轉後，指派的站台會使用 UNC 對應存取原始來源檔案位置。  

 您將套件和程式移轉至目的地階層後，如果從來源階層移轉的作業仍在進行中，您可以使用共用發佈點對該階層中的用戶端提供內容。 若要使用共用發佈點，內容必須在來源網站發佈點上保持可存取狀態。 如需共用發佈點的詳細資訊，請參閱[規劃 System Center Configuration Manager 中的內容部署移轉策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)中的[在來源和目的地階層之間共用發佈點](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)。  

 對於已移轉的內容，如果來源階層或目的地階層中的內容版本變更，用戶端就無法再從目的地階層的共用發佈點存取內容。 在此案例中，您必須重新移轉內容，使版本的套件來源階層和目的地階層之間的一致性。 此項資訊會在資料收集週期的期間，進行同步。  

> [!TIP]  
>  請針對您移轉的每個套件，更新目的地階層中的套件。 這個動作可防止將套件部署至目的地階層中的發佈點時發生問題。 不過，當您更新目的地階層中發佈點的套件時，該階層中的用戶端將不再能夠從共用發佈點取得該套件。 若要更新目的地階層的套件，請在 Configuration Manager 主控台移至 [軟體程式庫]，並以滑鼠右鍵按一下套件，然後選取 [更新發佈點]。 請針對您移轉的每個套件執行這項動作。  

> [!TIP]  
>  您可以使用 Microsoft System Center Configuration Manager Package Conversion Manager，將套件和程式轉換成 System Center Configuration Manager 應用程式。 請從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/p/?LinkId=212950) 網站下載 Package Conversion Manager。 如需詳細資訊，請參閱 [Configuration Manager Package Conversion Manager](http://go.microsoft.com/fwlink/p/?LinkId=247245)。  

### <a name="virtual-applications"></a>虛擬應用程式  
從支援的 Configuration Manager 2007 站台移轉 App-V 套件時，移轉程序會將這些套件轉換成目的地階層中的應用程式。 另外，還會根據 App-V 套件的現有公告，在目的地階層中建立下列部署類型：  

-   如果沒有公告，則會建立一個使用預設部署類型設定的部署類型。  

-   如果有一個公告存在，則會建立一個與 Configuration Manager 2007 公告使用相同設定的部署類型。  

-   如果有多個公告，則會使用每個 Configuration Manager 2007 公告的設定為該公告建立一個部署類型。  

> [!IMPORTANT]  
>  如果您移轉先前已移轉的 Configuration Manager 2007 App-V 套件，則移轉作業會因為虛擬應用程式套件不支援覆寫移轉行為而失敗。 在此案例中，您必須從目的地階層刪除已移轉的虛擬應用程式套件，然後建立新的移轉作業來移轉虛擬應用程式。  

> [!NOTE]  
>  在您移轉 App-V 套件後，可以使用 [更新內容精靈] 變更 App-V 部署類型的來源路徑。 如需如何更新部署類型內容的詳細資訊，請參閱 [System Center Configuration Manager 應用程式的管理工作](../../apps/deploy-use/management-tasks-applications.md)中的＜如何管理部署類型＞。  

當您從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層移轉時，除了 App-V 部署類型和應用程式之外，您還可以移轉 App-V 虛擬環境的物件。 如需 App-V 環境的詳細資訊，請參閱[使用 System Center Configuration Manager 部署 App-V 虛擬應用程式](../../apps/get-started/deploying-app-v-virtual-applications.md)。  

### <a name="advertisements"></a>公告  
您可以使用以集合為基礎的移轉，將公告從支援的 Configuration Manager 2007 來源站台移轉至目的地階層。 如果您升級用戶端，它會保留之前所執行公告的歷程記錄，以避免用戶端再次執行已移轉的公告。  

> [!NOTE]  
>  您無法移轉虛擬套件的公告。 這是移轉公告的例外狀況。  

### <a name="applications"></a>應用程式  
 您可以將應用程式從支援的 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層移轉至目的地階層。 如果您將用戶端從來源階層重新指派至目的地階層，用戶端會保留之前所安裝應用程式的歷程記錄，以避免用戶端再次執行已移轉的應用程式。  

##  <a name="BKMK_MigrateCollections"></a> 規劃移轉集合  
 您可以從支援的 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層移轉集合準則。 若要這麼做，您可以使用以物件為基礎的移轉作業。 當您移轉集合時，會移轉集合的規則，而不是有關集合成員的資訊或是與集合成員相關的資訊或物件。  

 從 Configuration Manager 2007 來源階層移轉時，不支援移轉集合物件。  

##  <a name="Plan_migrate_OSD"></a> 規劃移轉作業系統部署  
您可以從支援的來源階層移轉下列作業系統部署物件：  

-   作業系統映像和套件。 開機映像的來源路徑會更新為目的地站台上 Windows 系統管理安裝套件 (Windows AIK) 的預設映像位置。 以下是移轉作業系統映像和套件的需求和限制：  

    -   若要成功移轉映像檔，目的地階層的頂層站台上 SMS 提供者伺服器的電腦帳戶，其必須擁有來源站台 Windows AIK 位置之映像來源檔案的 [讀取] 和 [寫入] 權限。  

    -   當您移轉作業系統安裝套件時，請確認來源站台上套件的設定指向包含 WIM 檔案的資料夾，而不是 WIM 檔案本身。 如果安裝套件指向 WIM 檔案，安裝套件的移轉將會失敗。  

    -   當您從 Configuration Manager 2007 來源站台移轉開機映像套件時，套件的套件識別碼不會保留在目的地站台中。 這樣做的結果會是目的地階層中的用戶端無法使用共用發佈點上提供的開機映像套件。  

-   工作順序。 當您移轉包含用戶端安裝套件參照的工作順序時，該參照會取代為目的地階層的用戶端安裝套件參照。  

    > [!NOTE]  
    >  當您移轉工作順序時，Configuration Manager 可能會移轉目的地階層中不需要的物件。 這些物件包括開機映像和 Configuration Manager 2007 用戶端安裝套件。  

-   驅動程式和驅動程式套件。 當您移轉驅動程式套件，目的地階層中的 SMS 提供者電腦帳戶必須具有套件來源的完全控制權限。

##  <a name="Plan_Migrate_Compliance_settings"></a> 規劃移轉 Desired Configuration Management  
您可以移轉設定項目和設定基準。  

> [!NOTE]  
>  移轉作業不支援 Configuration Manager 2007 來源階層中未解譯的設定項目。 您無法移轉或將這些設定項目匯入到目的地階層。 如需未解譯設定項目的詳細資訊，請參閱 Configuration Manager 2007 文件庫中 [About Configuration Items in Desired Configuration Management](http://go.microsoft.com/fwlink/?LinkId=103846) (關於 Desired Configuration Management 的設定項目) 主題的＜Uninterpreted Configuration Item＞(未解譯的設定項目)。  

您可以匯入 Configuration Manager 2007 設定套件。 匯入程序會自動轉換設定套件，使其與 System Center Configuration Manager 相容。  

##  <a name="Plan_migrate_Boundaries"></a> 規劃移轉界限  
 您可以移轉階層之間的界限。 當您從 Configuration Manager 2007 移轉界限時，來源站台的每個界限都會同時移轉，並新增至目的地階層中建立的新界限群組中。 當您從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 階層移轉界限時，您選取的每個界限都會新增至目的地階層中的新界限群組。  

 將針對內容位置啟用每個自動建立的界限群組，但並未針對網站指派啟用。 如此可避免網站指派時，來源和目的地階層間發生界限重疊。 從 Configuration Manager 2007 來源站台移轉，有助於防止新安裝的 Configuration Manager 2007 用戶端被不當指派至目的地階層。 System Center Configuration Manager 用戶端預設不會自動指派至 Configuration Manager 2007 站台。  

 若您在移轉期間與目的地階層共用發佈點，任何與該發佈相關聯的界限都將自動移轉至目的地階層。 在目的地階層中，移轉會為每個共用的發佈點新建一個唯讀界限群組。 若您變更來源階層中發佈點的界限，目的地階層中的界限群組會在下次資料收集週期期間更新這些變更。  

##  <a name="Plan_Migrate_reports"></a> 規劃移轉報告  
Configuration Manager 不支援報告的移轉。 反之，它會使用 SQL Server Reporting Services 報表產生器將報告從來源階層中匯出，然後再將其匯入至目的地階層。  

> [!NOTE]  
>  因為 Configuration Manager 2007 與 System Center Configuration Manager之間的報告架構已變更，所以請針對您從 Configuration Manager 2007 階層匯入的每份報告進行測試以確保報告如預期運作。  

如需報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。  

##  <a name="Plan_Migrate_Org_Folders"></a> 規劃移轉組織與搜尋資料夾  
 您可以將組織資料夾和搜尋資料夾從支援的來源階層移轉至目的地階層。 此外，您還可以將已儲存搜尋的準則從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層移轉至目的地階層。  

 依預設，在進行移轉時，移轉程序會維持物件和集合的搜尋資料夾和系統管理資料夾架構。 不過，在 [建立移轉作業精靈] 中的 [設定] 頁面上，您可以藉由取消核取此選項的方塊，將移轉作業設定為不移轉物件的組織架構。 集合的組織架構一律不變。  

 唯一例外狀況是當搜尋資料夾包含虛擬應用程式時。 當您移轉 App-V 套件時，會在 System Center Configuration Manager 中將此 App-V 套件轉換為應用程式。 在移轉搜尋資料夾之後僅找到剩餘的套件，而且搜尋資料夾也找不到 App-V 套件，原因是移轉 App-V 套件時，會將 App-V 套件轉換為應用程式。  

 當您從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層移轉已儲存的搜尋時，所移轉的是搜尋的準則，而非搜尋結果的相關資訊。 已儲存搜尋的移轉不適用於 Configuration Manager 2007 來源站台。  

##  <a name="Plan_Migrate_AI"></a> 規劃移轉 Asset Intelligence 自訂項目  
 您可以將 Asset Intelligence 自訂項目從支援的來源階層移轉至目的地階層。 Configuration Manager 2007 與 System Center Configuration Manager 之間的 Asset Intelligence 自訂項目架構並沒有重大變更。  

> [!NOTE]  
>  System Center Configuration Manager 不支援從使用 Asset Intelligence Service 2.0 (AIS 2.0) 的 Configuration Manager 2007 站台移轉 Asset Intelligence 物件。  

##  <a name="Plan_Migrate_SWM_Rules"></a> 規劃移轉軟體計量規則自訂項目  
 Configuration Manager 2007 與 System Center Configuration Manager 之間的軟體計量並沒有重大變更。 您可以將軟體計量規則從支援的來源階層移轉至目的地階層。  

 依預設，您移轉至目的地階層的軟體計量規則與目的地階層中的特定網站並無關聯，因此這些規則可套用至階層中的所有用戶端。 若要將軟體計量規則套用至特定網站中的用戶端，您必須在移轉後編輯該計量規則。  
