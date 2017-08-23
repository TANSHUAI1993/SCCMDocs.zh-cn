---
title: "備份站台 | Microsoft Docs"
description: "了解如何在發生失敗或資料遺失之前，在 System Center Configuration Manager 中備份您的站台。"
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: "22"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7deb00d4b67eabf3238907b337a9d0367c3d99cc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="back-up-a-configuration-manager-site"></a>備份 Configuration Manager 站台

適用於：System Center Configuration Manager (最新分支)

準備備份和復原方法，以避免資料遺失。 對於 Configuration Manager 站台，備份和復原方法有助於您在遺失最少資料的情況下更快復原站台和階層。  

本主題的章節可協助您備份站台。 若要復原站台，請參閱 [Configuration Manager 的復原](/sccm/protect/understand/recover-sites)。  

## <a name="considerations-before-creating-a-backup"></a>建立備份前的考量  
-   **如果您使用 SQL Server Always On 可用性群組來裝載站台資料庫：**請根據[準備使用 SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup) 中所述來修改備份和復原計劃。

-   Configuration Manager 可以從 Configuration Manager 備份維護工作，或從您使用其他程序建立的站台資料庫備份，以復原站台資料庫。   

    例如，您可以使用 Microsoft SQL Server 維護計畫建立的備份還原站台資料庫。 您也可以使用以 Data Protection Manager 建立的備份來備份站台資料庫 (DPM)。

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>使用 Data Protection Manager 備份網站資料庫
您可以使用 System Center 2012 Data Protection Manager (DPM) 來備份站台資料庫。

您必須在網站資料庫電腦的 DPM 中建立新的保護群組。 在 [建立新保護群組精靈] 的 [選擇群組成員]  頁面上，您可以從資料來源清單選取 SMS 寫入器服務，然後選取網站資料庫作為適當的成員。 如需使用 DPM 備份網站資料庫的詳細資訊，請參閱 TechNet 上的 [Data Protection Manager Documentation Library (Data Protection Manager 文件庫)](http://go.microsoft.com/fwlink/?LinkId=272772) 。  

> [!IMPORTANT]  
>  Configuration Manager 不支援為使用具名執行個體的 SQL Server 叢集執行 DPM 備份，但支援在使用 SQL Server 預設執行個體的 SQL Server 叢集上執行 DPM 備份。  

 在您還原網站資料庫後，請依照安裝程式中的步驟還原網站。 選取 [使用手動復原的站台資料庫] 復原選項，以使用您透過 Data Protection Manager 復原的站台資料庫。  

## <a name="backup-maintenance-task"></a>備份維護工作
您可以藉由排程預先定義的「備份站台伺服器」維護工作，自動備份 Configuration Manager 站台。 這項工作：

-   依排程執行
-   備份站台資料庫
-   備份特定的登錄機碼
-   備份特定的資料夾和檔案
-   備份 [CD.Latest 資料夾](/sccm/core/servers/manage/the-cd.latest-folder)   

規劃至少每隔 5 天執行預設站台備份工作。 這是因為 Configuration Manager 使用 5 天的 *SQL Server 變更追蹤保留期間*。  (請參閱復原站台主題中的 [SQL Server 變更追蹤保留期間](/sccm/protect/understand/recover-sites#bkmk_SQLretention))。

若要簡化備份程序，您可以建立 **AfterBackup.bat** 檔案，自動在順利執行備份維護工作後執行備份後動作。 AfterBackup.bat 檔案通常用來將備份快照封存到安全的位置。 您也可以使用 AfterBackup.bat 檔案將檔案複製到備份資料夾，並開始進行其他增補的備份工作。  

您可以備份管理中心網站和主要網站，但不支援次要網站或網站系統伺服器的備份。

當 Configuration Manager 備份服務執行時，會依照備份控制檔案 (**&lt;ConfigMgrInstallationFolder\>\Inboxes\Smsbkup.box\Smsbkup.ctl**) 中定義的指示進行。 您可以修改備份控制檔案，以變更備份服務的行為。  

站台備份狀態資訊會寫入至 **Smsbkup.log** 檔案。 此檔案會在您於「備份網站伺服器」維護工作內容中指定的目的地資料夾中建立。  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>啟用網站備份維護工作  

1.  在 Configuration Manager 主控台中，開啟 [系統管理] > [站台設定] > [站台]。  

2.  選取您要啟用網站備份維護工作的網站。  

3.  在 [常用] 索引標籤的 [設定] 群組中，選擇 [站台維護工作]。  

4.  選擇 [備份站台伺服器]  >  [編輯]。  

5.  選擇 [啟用此工作] > [設定路徑] 以指定備份目的地。 下列選項可供您選擇：  

    > [!IMPORTANT]  
    >  若要預防備份檔案遭到竄改，請將檔案儲存在安全的位置。 最安全的備份路徑是本機磁碟機，因此您可以在資料夾上設定 NTFS 檔案系統權限。 Configuration Manager 不會加密儲存在備份路徑中的備份資料。  

    -   **用於站台資料和資料庫的站台伺服器本機磁碟機**：指定將站台和站台資料庫的備份檔案儲存在站台伺服器本機磁碟上指定的路徑。 您必須先建立本機資料夾才可以執行備份工作。 網站伺服器的本機系統帳戶必須擁有網站伺服器備份本機資料夾的 **寫入** NTFS 檔案系統權限。 電腦若是執行 SQL Server，其本機系統帳戶必須擁有網站資料庫備份資料夾的 **寫入** NTFS 權限。  

    -   **用於站台資料和資料庫的網路路徑 (UNC 名稱)**：指定將站台和站台資料庫的備份檔案儲存在指定的 UNC 路徑。 您必須先建立共用才可以執行備份工作。 網站伺服器的電腦帳戶和 SQL Server 的電腦帳戶 (如果 SQL Server 安裝在其他電腦上) 必須擁有共用網路資料夾的 **寫入** NTFS 和共用權限。  

    -   **站台伺服器和 SQL Server 上的本機磁碟機**：指定將站台的備份檔案儲存在站台伺服器本機磁碟機上指定的路徑，並將站台資料庫的備份檔案儲存在站台資料庫伺服器本機磁碟機上指定的路徑。 您必須先建立本機資料夾才可以執行備份工作。 網站伺服器的電腦帳戶必須擁有您在網站伺服器上建立之資料夾的 **寫入** NTFS 權限。 SQL Server 的電腦帳戶必須擁有您在網站資料庫伺服器上建立之資料夾的 **寫入** NTFS 權限。 此選項僅在網站伺服器上未安裝網站資料庫時適用。  

    > [!NOTE]  
    >   只有在您指定備份目的地的 UNC 路徑時才可以使用瀏覽備份目的地的選項。

    > 用於不支援使用 Unicode 字元之備份目的地的資料夾名稱或共用名稱。  

6.  為站台備份工作設定排程。 基於最佳作法，請考慮將備份排程在非工作時間執行。 如果您有階層，請考慮將排程設在一週至少執行二次，以確保在發生網站失敗時可以保留較多的資料。  

    當您在與設定備份相同的站台伺服器上執行 Configuration Manager 主控台時，「備份站台伺服器」維護工作會使用當地時間進行排程。 當您從來自設定要進行備份的遠端站台電腦執行 Configuration Manager 主控台時，「備份站台伺服器」維護工作會使用 UTC 進行排程。  

7.  選擇是否要在站台備份工作失敗時建立警示，按一下 [確定]，再按一下 [確定]。 選取時，Configuration Manager 會建立備份失敗的重大警示，您可以在 [監視] 工作區的 [警示] 節點中檢閱該警示的內容。  

 接下來，確認「備份站台伺服器」維護工作正在執行，以確定備份已建立。  

#### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>確認備份站台伺服器維護工作正在執行  
藉由檢閱下列任一項，確認「站台備份」維護工作正在執行：  

-   檢查此工作所建立備份目的地資料夾中檔案的時間戳記。 確認時間戳記的時間已更新為符合此工作上次排程執行的時間。  

-   在 [監視]  工作區的 [元件狀態]  節點中，檢閱 SMS_SITE_BACKUP 的狀態訊息。 當網站備份順利完成時，您會看到訊息識別碼 5035，表示網站備份已順利完成且沒有發生錯誤。  

-   當「備份網站伺服器」維護工作設定為在備份失敗時建立警示時，您可以在 [監視]  工作區的 [警示]  節點中檢查備份失敗的內容。  

-   在 &lt;*ConfigMgrInstallationFolder*>\Logs 中，查看 Smsbkup.log 中的警示及錯誤。 當網站備份順利完成時，您會看到含有時戳的 `Backup completed` ，以及訊息識別碼 `STATMSG: ID=5035`。  

    > [!TIP]  
    >  當備份維護工作失敗時，您可以藉由停止再重新啟動 SMS_SITE_BACKUP 服務，重新啟動備份工作。  

## <a name="archive-the-backup-snapshot"></a>封存備份快照  
第一次執行「備份網站伺服器」維護工作時，它會建立一個備份快照，您可以在發生失敗時使用這個備份快照復原您的網站。 當備份工作在後續的週期中再次執行時，它會建立新的備份快照，並使用該備份快照覆寫先前的快照。 因此網站只有一個備份快照，您無法擷取舊版的備份快照。  

作為最佳作法，請針對以下原因保留多個備份快照封存：  

-   備份媒體失敗、錯置，或僅包含部分備份，都是常見狀況。 從過去的備份復原失敗的獨立主要網站總比完全沒有備份要來得好。 對於階層中的網站伺服器，備份必須是在 SQL Server 變更追蹤保留期間內，否則就不需要備份。  

-   有可能在數個備份週期中都偵測不到網站損毀。 您可能必須使用站台損毀前的備份快照。 這可套用至獨立主要站台以及其備份是在 SQL Server 變更追蹤保留期間內的階層中站台。  

-   例如，如果備份網站伺服器維護工作失敗，網站就可能完全沒有備份快照。 由於備份工作會在開始備份現有資料前將過去的備份快照全部移除，如此就會沒有有效的備份快照。  

## <a name="using-the-afterbackupbat-file"></a>使用 AfterBackup.bat 檔案  
順利備份站台之後，備份站台伺服器工作會自動嘗試執行名為 AfterBackup.bat 的檔案。 您必須在 &lt;*ConfigMgrInstallationFolder*>\Inboxes\Smsbkup 中手動建立 AfterBackup.bat 檔案。 如果 AfterBackup.bat 檔案存在，且儲存在正確的資料夾中，則會在備份工作完成後自動執行。

AfterBackup.bat 檔案可讓您在每次備份操作結束時封存備份快照，並自動執行其他非備份網站伺服器維護工作的備份後工作。 AfterBackup.bat 檔案會整合封存與備份操作，如此即可確保封存每個新的備份快照。

若 AfterBackup.bat 檔案不存在，則備份工作就會將其略過，而對於備份操作沒有任何影響。 若要確認網站備份工作是否已成功執行 AfterBackup.bat 檔，請參閱 [監視]  工作區內的 [元件狀態]  節點，並檢閱 SMS_SITE_BACKUP 的狀態訊息。 工作成功啟動 Afterbackup.bat 命令檔時，您會看見訊息 ID 5040。  

> [!TIP]  
>  若要建立 AfterBackup.bat 檔案以封存您的站台伺服器備份檔案，您必須在批次檔中使用複製命令工具，例如 [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408)。 例如，您可以建立 AfterBackup.bat 檔，然後在第一行加入如下的內容：`Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

 雖然 AfterBackup.bat 的用途是封存備份快照，您也可以建立 AfterBackup.bat 檔，在每次備份操作結束時執行額外工作。  

##  <a name="supplemental-backup-tasks"></a>增補的備份工作  
備份網站伺服器維護工作為網站伺服器檔案和網站資料庫提供備份快照，但在您建立備份策略時，還有其他項目並未備份，這是必須納入考慮的。 使用下列各節可協助您完成 Configuration Manager 備份策略。  

### <a name="back-up-custom-reporting-services-reports"></a>支持自訂 Reporting Services 報告  
您已經修改預先定義或建立自訂的 Reporting Services 報告時，針對報告伺服器資料庫檔案建立備份也是備份策略中很重要的部分。 報告伺服器備份必須包含報告和模組、加密金鑰、自訂組件或延伸、設定檔案、自訂報告中所使用之自訂 SQL Server 檢視、自訂儲存程序等的來源檔備份。  

> [!IMPORTANT]  
>  Configuration Manager 升級到較新版本時，新報告可能會覆寫預先定義的報告。 如果您修改預先定義的報告，請先備份報告，然後在 Reporting Services 中還原。  

 如需備份 Reporting Services 中的自訂報告的詳細資訊，請參閱《SQL Server 2014 線上叢書》中的 [Reporting Services 安裝的備份與還原作業](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) 。  

### <a name="back-up-content-files"></a>備份內容檔案  
Configuration Manager 中的內容庫是儲存軟體更新、應用程式、作業系統部署等之所有內容檔案的位置。 內容庫位於站台伺服器和每個發佈點上。 備份網站伺服器維護工作並不包括內容庫或套件來源檔案的備份。 網站伺服器失敗時，內容庫檔案相關資訊會還原至網站資料庫，但您必須在網站伺服器上還原內容庫和套件來源檔案。  

-   **內容庫**：必須先還原內容庫，您才能將內容重新發佈至發佈點。 當您開始重新發佈內容時，Configuration Manager 會從站台伺服器的內容庫將檔案複製到發佈點。 站台伺服器的內容庫位於 SCCMContentLib 資料夾中，這個資料夾一般位於安裝站台時可用磁碟空間最大的磁碟機上。  

-   **封裝來源檔案**：必須先還原封裝來源檔案，您才能在發佈點上更新內容。 當您開始進行內容更新時，Configuration Manager 會從套件來源將新的或修改過的檔案複製到內容庫，接著將檔案複製到關聯的發佈點。 您可以在 SQL Server 中執行以下查詢，找出所有套件和應用程式的套件來源位置： `SELECT * FROM v_Package`。 您可以查看封裝識別碼的前三個字元，藉此識別封裝來源站台。 例如，如果封裝識別碼為 CEN00001，則來源站台的站台碼為 CEN。 當您還原套件來源檔案時，檔案必須還原到失敗前所在的相同位置。  

 確認您在網站伺服器的檔案系統備份中同時包含內容庫和套件來源位置。  

### <a name="back-up-custom-software-updates"></a>備份自訂的軟體更新  
 System Center Updates Publisher 2011 是一種獨立工具，可讓您將自訂軟體更新發佈到 Windows Server Update Services (WSUS)、將軟體更新同步處理至 Configuration Manager、評估軟體更新合規性，以及將自訂軟體更新部署至用戶端。 Updates Publisher 會使用本機資料庫作為其軟體更新存放庫。 使用 Updates Publisher 管理自訂軟體更新時，需判斷是否應將 Updates Publisher 資料庫納入備份計畫中。 如需更新發行者的詳細資訊，請參閱 System Center TechCenter 文件庫中的 [System Center Updates Publisher 2011 (System Center 更新發行者 2011)](http://go.microsoft.com/fwlink/p/?LinkId=228726) 。  

 使用以下程序來備份 Updates Publisher 資料庫。  

#### <a name="to-back-up-the-updates-publisher-2011-database"></a>備份更新發行者 2011 資料庫  

1.  在執行 Updates Publisher 的電腦上，瀏覽至 %*使用者設定檔*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\ 中的 Updates Publisher 資料庫檔案 (Scupdb.sdf)。 每個執行 Updates Publisher 的使用者都有不同的資料庫檔案。  

2.  將資料庫檔案複製到備份目的地。 例如，若備份目的地是 E:\ConfigMgr_Backup，您可以將 Updates Publisher 資料庫檔案複製到 E:\ConfigMgr_Backup\SCUP2011。  

    > [!TIP]  
    >  電腦上有一個以上的資料庫檔案時，請考慮將檔案儲存於指出與資料庫檔案關聯之使用者設定檔的子資料夾中。 例如，您可以在 E:\ConfigMgr_Backup\SCUP2011\User1 中有一個資料庫檔案，而在 E:\ConfigMgr_Backup\SCUP2011\User2 中有另一個資料庫檔案。  

## <a name="user-state-migration-data"></a>使用者狀態移轉資料  
您可以使用 Configuration Manager 工作順序來擷取和還原作業系統部署案例 (您想保留目前作業系統的使用者狀態) 中的使用者狀態資料。 儲存使用者狀態資料的資料夾會列在狀態移轉點的內容中。 此使用者狀態移轉資料並不會備份為網站伺服器備份維護工作的一部分。 作為您備份計畫的一部分，您必須手動備份所指定用來儲存使用者狀態移轉資料的資料夾。   

### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>判斷用來儲存使用者狀態移轉資料的資料夾  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理] 工作區中，展開 [站台設定]，然後選擇 [伺服器和站台系統角色]。  

3.  選取裝載狀態移轉角色的站台系統，然後選擇 [站台系統角色] 中的 [狀態移轉點]。  


4.  在 [網站角色]  索引標籤的 [內容]  群組中，按一下 [內容] 。  
5.  儲存使用者狀態移轉資料的資料夾會列在 [一般]  索引標籤上的 [資料夾詳細資料]  區段中。  



## <a name="about-the-sms-writer-service"></a>關於 SMS 寫入器服務  
SMS 寫入器是一個服務，會在備份程序進行期間與磁碟區陰影複製服務 (VSS) 互動。 Configuration Manager 站台備份必須執行 SMS 寫入器服務才可以順利完成。  

### <a name="purpose"></a>目的  
SMS 寫入器會登錄至 VSS 服務，並繫結至其介面和事件。 當 VSS 廣播事件或傳送特定通知到 SMS 寫入器時，SMS 寫入器會回應通知，並採取適當的動作。 SMS 寫入器會讀取位於 &lt;ConfigMgr 安裝路徑>\inboxes\smsbkup.box 的備份控制檔案 (smsbkup.ctl)，並決定所備份的檔案及資料。 SMS 寫入器會根據此資訊與來自 SMS 登錄機碼及子機碼的特定資料建立由各種元件組成的中繼資料。 它會在收到要求時將中繼資料傳送至 VSS。 VSS 接著會傳送中繼資料給提出要求的應用程式，即 Configuration Manager 備份管理員。 備份管理員會選取已備份的資料，並經由 VSS 將此資料傳送給 SMS 寫入器。 SMS 寫入器會採取適當的步驟來進行備份的準備。 稍後當 VSS 準備好建立快照時會傳送一個事件，此時 SMS 寫入器會停止所有 Configuration Manager 服務，並確定 Configuration Manager 活動在建立快照時已遭到凍結。 在快照建立完成後，SMS 寫入器會重新啟動服務和活動。  

SMS 寫入器服務會自動進行安裝。 當 VSS 應用程式要求備份或還原時，SMS 寫入器必須處於執行中狀態。  

### <a name="writer-id"></a>寫入器 ID  
SMS 寫入器的寫入器 ID 為：03ba67dd-dc6d-4729-a038-251f7018463b。  

### <a name="permissions"></a>權限  
SMS 寫入器服務必須在本機系統帳號戶下執行。  

### <a name="volume-shadow-copy-service"></a>磁碟區陰影複製服務  
VSS 是一組 COM API，其中實作了一個架構以允許進行磁碟區備份時系統上的應用程式仍能繼續寫入磁碟區。 VSS 提供一致的介面，可在磁碟上更新資料的使用者應用程式 (SMS 寫入器服務) 與備份應用程式 (備份管理員服務) 之間進行協調。 如需詳細資訊，請參閱 Windows Server TechCenter 中的[磁碟區陰影複製服務](http://go.microsoft.com/fwlink/p/?LinkId=241968) \(英文\) 主題。  

## <a name="next-steps"></a>後續步驟
建立備份之後，請使用該備份來練習[站台復原](/sccm/protect/understand/recover-sites)。 這有助於您在需要仰賴復原程序之前先加以熟悉，並可協助確認備份是否針對其預定用途成功執行。  
