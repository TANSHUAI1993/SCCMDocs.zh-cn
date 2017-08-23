---
title: "站台復原 | Microsoft Docs"
description: "了解在 System Center Configuration Manager 中復原站台。"
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 49eea15ea2888f8f93c33eb771c09147ba21529e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="recover-a-configuration-manager-site"></a>復原 Configuration Manager 站台

*適用於︰System Center Configuration Manager (最新分支)*

在站台資料庫發生 Configuration Manager 站台失敗或資料遺失的狀況之後，執行 Configuration Manager 站台復原。 修復和重新同步處理資料是網站復原的核心工作，也是避免操作中斷的必要手段。

本主題中的各節可協助您復原 Configuration Manager 站台。 若要建立備份，請參閱[備份 Configuration Manager](/sccm/protect/understand/backup-and-recovery)。

## <a name="considerations-before-recovering-a-site"></a>復原站台前的考量
**您必須使用相同的 SQL Server 版本：**例如，不支援將 SQL Server 2014 上執行的資料庫還原至 SQL Server 2016。 同樣地，不支援將 SQL Server 2016 Standard 版上執行的站台資料庫還原至 SQL Server 2016 Enterprise 版。
-   SQL Server 絕不能設為 **單一使用者模式**。
-   確定 .MDF 和 .LDF 檔案有效。 復原站台時，不會檢查正要還原的檔案狀態。

**如果您使用 SQL Server Always On 可用性群組裝載站台資料庫：**請根據[準備使用 SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery) 中所述來修改復原計劃。

**使用資料庫複本時：**在您還原為資料庫複本設定的網站資料庫之後，必須先重新設定每個資料庫複本並重建發佈及訂閱，才能使用資料庫複本。

## <a name="determine-your-recovery-options"></a>決定您的復原選項
針對 Configuration Manager 主要站台伺服器和管理中心網站復原，有兩大重點考量：「站台伺服器」與「站台資料庫」。
下列各節可協助您為復原案例選取最佳選項。

> [!NOTE]   
> 安裝程式在伺服器上偵測到現有的 Configuration Manager 站台時，您就可以啟動站台復原，不過站台伺服器的復原選項有限。 例如，若您在現有網站伺服器上執行安裝程式，當您選擇復原時，就可以復原網站資料庫伺服器，但會停用復原網站伺服器的選項。

### <a name="site-server-recovery-options"></a>站台伺服器復原選項
從您在 Configuration Manager 安裝資料夾外部所建立的 **CD.Latest** 資料夾複本中啟動安裝程式。
-   如果您從站台伺服器的 [開始] 功能表執行 Configuration Manager 安裝程式，就無法使用 [復原站台] 選項。
-   如果在您進行備份之前，已在 Configuration Manager 主控台內安裝任何更新，則可能無法順利從安裝媒體或 Configuration Manager 安裝路徑使用安裝程式來重新安裝站台。

然後選取 [復原站台] 選項。 針對失敗的站台伺服器，您有以下復原選項：

-   **使用現有備份復原站台伺服器**：如果您在站台失敗前，已於「備份站台伺服器」維護工作期間，在站台伺服器上建立了 Configuration Manager 站台伺服器的備份，請使用此選項。 此時會重新安裝網站，並根據備份的網站來設定網站設定。
-   **重新安裝站台伺服器**：若您沒有站台伺服器的備份，請使用此選項。 此時會重新安裝網站伺服器，且您必須指定網站設定，如同您進行初始安裝時一樣。
  -   您必須使用失敗的站台第一次安裝時使用的相同站台碼和站台資料庫名稱。
  -   您可以在執行新作業系統的新電腦上重新安裝站台。
  -   電腦必須使用和原始站台伺服器相同的名稱 (FQDN)。   

### <a name="site-database-recovery-options"></a>網站資料庫復原選項
執行安裝程式時，針對網站資料庫，您有以下復原選項：
-   **使用備份組復原站台資料庫**：如果您在站台資料庫失敗前，已於站台上執行「備份站台伺服器」維護工作期間，建立了 Configuration Manager 站台資料庫的備份，請使用此選項。 若您有階層，則會從主要網站的管理中心網站，或管理中心網站的參照主要網站，擷取最後一次進行網站資料庫備份後，對網站資料庫所做的變更。 當您復原獨立主要網站的網站資料庫時，您會遺失最後一次備份後的網站變更。

   當您復原階層中某個網站的網站資料庫時，管理中心網站與主要網站的復原行為不同，並且上次備份是在 SQL Server 變更追蹤保留期間內或保留期間外，復原行為也不一樣。 如需詳細資訊，請參閱本主題中的＜ [網站資料庫復原案例](##site-database-recovery-scenarios) ＞一節。
  > [!NOTE]   
  > 若您選取使用備份集來還原網站資料庫，但已經存在網站資料庫，則復原就會失敗。  

-   **為此站台建立新的資料庫**：若您沒有 Configuration Manager 站台資料庫的備份，請使用此選項。 您有階層時，會建立新的網站資料庫，使用從主要網站的管理中心網站或管理中心網站的參照主要網站的複寫資料，就會復原資料。 若您復原獨立主要網站或沒有主要網站的管理中心網站，就無法使用此選項。

-   **使用手動復原的站台資料庫**：如果您已復原 Configuration Manager 站台資料庫，但必須完成復原程序，請使用此選項。
    -   Configuration Manager 可以從 Configuration Manager 備份維護工作，或從您使用 DPM 或其他程序執行的站台資料庫備份，來復原站台資料庫。 在您使用 Configuration Manager 以外的方法復原站台資料庫後，您必須執行安裝程式，然後選取這個選項來完成站台資料庫復原。

    > [!NOTE]   
    > 使用 DPM 備份站台資料庫時，在 Configuration Manager 中繼續還原程序前，請使用 DPM 程序將站台資料庫還原到指定的位置。 如需 DPM 的詳細資訊，請參閱 TechNet 上的 [Data Protection Manager Documentation Library (Data Protection Manager 文件庫)]() 。    

    -   若您有階層，則會從主要網站的管理中心網站，或管理中心網站的參照主要網站，擷取最後一次進行網站資料庫備份後，對網站資料庫所做的變更。 當您復原獨立主要網站的網站資料庫時，您會遺失最後一次備份後的網站變更。     


-   **略過資料庫復原**：若 Configuration Manager 站台資料庫伺服器上並沒出現資料遺失的狀況，請使用此選項。 只有在網站資料庫位於不同電腦而不是在您正在復原的網站伺服器上時，這個選項才有效。

### <a name="sql-server-change-tracking-retention-period"></a>SQL Server 變更追蹤保留期間
變更追蹤會在 SQL Server 的網站資料庫中啟用。 變更追蹤可讓 Configuration Manager 查詢有關上次時間點後，資料庫資料表中已經出現之變更的資訊。 保留期間會指定保留變更追蹤資訊的時間長度。 根據預設，會將網站資料庫設定為 5 天的保留期間。 復原網站資料庫時，您的備份是在保留期間內或保留期間外，復原程序的進行方式也隨之不同。 例如，若網站資料庫伺服器失敗，而上次備份是 7 天以前，表示備份是在保留期間外。

如需 SQL Server 變更追蹤本質的詳細資訊，請參閱來自 SQL Server 團隊的下列部落格︰[Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) (變更追蹤清除 - 第 1 部分) 和 [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2) (變更追蹤清除 - 第 2 部分)。

### <a name="reinitialization-of-site-or-global-data"></a>重新初始化站台或全域資料
重新初始化網站或全域資料的程序，會以來自另一個網站資料庫的資料取代網站資料庫中的現有資料。 例如，若網站 ABC 重新初始化來自網站 XYZ 的資料，會發生以下步驟：
-   資料從網站 XYZ 複製到 ABC。
-   網站 XYZ 的現有資料會從網站 ABC 上的網站資料庫中移除。
-   從網站 XYZ 複製的資料會插入網站 ABC 的網站資料庫。

#### <a name="example-scenario-1"></a>範例案例 1
**主要站台重新初始化來自管理中心網站的全域資料**：復原程序會從主要站台資料庫移除主要站台的現有全域資料，並以從管理中心網站複製的全域資料加以取代。

#### <a name="example-scenario-2"></a>範例案例 2
**管理中心網站重新初始化來自主要站台的站台資料**：復原程序會從管理中心網站資料庫中移除該主要站台的現有站台資料，並以從主要站台複製的站台資料加以取代。 其他主要網站的網站資料則不受影響。

### <a name="site-database-recovery-scenarios"></a>網站資料庫復原案例
從備份還原站台資料庫後，Configuration Manager 會嘗試還原站台內上次資料庫備份後的變更以及全域資料。 下文說明從備份還原站台資料庫之後，Configuration Manager 會啟動的動作。

**復原的站台是管理中心網站：**
-   **變更追蹤保留期間內的資料庫備份**
    -   **全域資料：** 所有主要站台複寫備份之後全域資料中的變更。
    -   **站台資料：** 從所有主要站台複寫備份之後站台資料中的變更。


-   **比變更追蹤保留期間還舊的資料庫備份**
    -   **全域資料：** 如有指定，管理中心網站會重新初始化參照主要站台的全域資料。 接著，所有其他主要網站會重新初始化來自管理中心網站的全域資料。 若沒有指定任何參照網站，則所有主要網站都會重新初始化來自管理中心網站的全域資料 (從備份還原的資料)。
    -   **站台資料：** 管理中心網站會重新初始化每個主要站台的站台資料。


**復原的站台是主要站台：**
-   **變更追蹤保留期間內的資料庫備份**
    -   **全域資料：** 從管理中心站台複寫備份之後全域資料中的變更。
    -   **站台資料：** 管理中心站台會重新初始化主要站台的站台資料。 備份後的變更會遺失，但把資訊傳送到主要站台的用戶端會重新產生大部分的資料。


-   **比變更追蹤保留期間還舊的資料庫備份**
    -   **全域資料：** 主要站台會重新初始化管理中心站台的全域資料。
    -   **站台資料：** 管理中心站台會重新初始化主要站台的站台資料。 備份後的變更會遺失，但把資訊傳送到主要站台的用戶端會重新產生大部分的資料。

## <a name="site-recovery-procedures"></a>網站復原程序
使用以下其中一種程序來協助您復原網站伺服器和網站資料庫。

### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>在安裝精靈中啟動網站復原
1.  將 [CD.Latest 資料夾](/sccm/core/servers/manage/the-cd.latest-folde)複製到 Configuration Manager 安裝資料夾外部的位置。
從 CD.Latest 資料夾的複本執行 [Configuration Manager 安裝精靈]。

2.  在 [開始使用]  頁面上，選取 [復原網站] ，然後按 [下一步] 。

3.  使用適合復原網站的選項來完成精靈。

  -   在復原期間，安裝程式會識別 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 在復原期間，請勿變更此連接埠設定，否則在復原完成後，會無法正常執行資料複寫。

  -   您可以在 [安裝精靈] 指定用於 Configuration Manager 安裝的原始或新路徑。

### <a name="to-start-an-unattended-site-recovery"></a>啟動自動網站復原
  1.    針對復原網站時所需的選項，準備自動安裝指令碼。  請參閱[自動站台復原指令碼檔案索引鍵](/sccm/protect/understand/unattended-site-recovery-script-file-keys)。

  2.    使用命令 **/script** 選項執行 Configuration Manager 安裝程式。 例如，若您將安裝程式初始設定檔命名為 ConfigMgrUnattend.ini，並儲存在您要執行安裝程式之電腦的 C:\Temp 目錄中，則命令如下所示： **Setup /script C:\temp\ConfigMgrUnattend.ini**。

  > [!NOTE]   
  >  復原管理中心網站後，可能無法建立某些從子站台複寫過來的站台資料。 這可能包括硬體清查、軟體清查和狀態訊息。
  >
  >  如果發生這種情況，您必須為資料庫複寫重新初始化 **ConfigMgrDRSSiteQueue** 。  若要這樣做，請使用 **SQL Server Manager** 在管理中心網站的 Configuration Manager 站台資料庫上執行下列查詢：
  >
  >  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**
  >
  >  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**


## <a name="post-recovery-tasks"></a>復原後的工作
復原網站後，有幾項後續復原工作必須納入考量，網站復原才算完成。 利用下面各節可幫助您完成網站復原程序。

### <a name="re-enter-user-account-passwords"></a>重新輸入使用者帳戶密碼
網站伺服器復原後，必須重新輸入為網站所指定使用者帳戶的密碼，因為在網站復原期間會重設這些密碼。 網站復原完成後，帳戶會列在 [安裝精靈] 的 [已完成]  頁面上，並且儲存到已復原網站伺服器的 C:\ConfigMgrPostRecoveryActions.html。

#### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>在網站復原後重新輸入使用者帳戶的密碼

1.  開啟 Configuration Manager 主控台並連線至復原的站台。

2.  在 Configuration Manager 主控台中，按一下 [系統管理] 。

3.  在 [系統管理]  工作區中，展開 [安全性] ，然後按一下 [帳戶] 。

4.  針對重新輸入其密碼的每個帳戶執行下列操作：

    1.  從網站復原後識別的帳戶清單中選取帳戶。 您可以在已復原網站伺服器的 C:\ConfigMgrPostRecoveryActions.html 中找到此清單。

    2.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容]  開啟帳戶內容。

    3.  在 [一般]  索引標籤上按一下 [設定] ，然後重新輸入帳戶的密碼。

    4.  按一下 [確認] ，為所選取使用者帳戶選取適當的資料來源，然後按一下 [測試連線]  確認使用者帳戶能夠連線至資料來源。

    5.  按一下 [確定]  儲存密碼變更，然後按一下 [確定] 。

### <a name="re-enter-sideloading-keys"></a>重新輸入側載金鑰
網站伺服器復原後，您必須重新輸入指定給網站的 Windows 側載金鑰，因為在網站復原期間會重設這些金鑰。 重新輸入側載金鑰之後，Configuration Manager 主控台中 Windows 側載金鑰的 [已使用的啟用數量] 欄中的計數便會重設。 例如，假設在站台失敗前，您的 [啟用總數] 計數設為 [100]，而代表裝置已用金鑰數目的 [已使用的啟用數量] 是 [90]。 在網站復原之後，[啟用總數]  欄仍會顯示 [100] ，但是 [已使用的啟用數量]  欄會不正確地顯示 [0] 。 不過，在 10 個新裝置使用側載金鑰之後，就不會有任何剩餘的側載金鑰，因此下一個裝置將無法套用側載金鑰。

### <a name="recreate-the-microsoft-intune-subscription"></a>重新建立 Microsoft Intune 訂閱
 如果在站台伺服器重新製作映像後才復原 Configuration Manager 站台伺服器，就不會還原 Microsoft Intune 訂閱。 您必須在復原站台後，重新連線到訂閱。  請不要建立新的 APN 要求，而改為上傳目前有效的 .pem，也就是上次設定或更新 iOS 管理所上傳的檔案。 如需詳細資訊，請參閱 [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription)。

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>為使用 IIS 的網站系統角色設定 SSL
當您復原執行 IIS 且在失敗前設定為使用 HTTPS 的網站系統時，必須重新設定 IIS 使用 Web 伺服器憑證。

### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>重新安裝已復原網站伺服器中的 Hotfix
網站復原後，您必須重新安裝之前套用至網站伺服器的任何 Hotfix。 站台復原之後，在 [安裝精靈] 的 [已完成] 頁面上檢視先前所安裝 Hotfix 的清單。 此清單也會儲存到已復原站台伺服器上的 **C:\ConfigMgrPostRecoveryActions.html** 中。

### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>復原執行 Reporting Services 之電腦上的自訂報告
當您已建立自訂 Reporting Services 報告，而 Reporting Services 失敗時，若您已備份報告伺服器，則可以復原報告。 如需還原 Reporting Services 中自訂報告的詳細資訊，請參閱《SQL Server 2008 線上叢書》中的 [Reporting Services 安裝的備份與還原作業](http://go.microsoft.com/fwlink/p/?LinkId=228724) 。

### <a name="recover-content-files"></a>復原內容檔案
 網站資料庫包含內容檔案在網站伺服器上儲存位置的相關資訊，但是內容檔案不會隨備份或復原程序備份或還原。 若要完整復原內容檔案，您必須將內容庫及套件來源檔案還原至原始位置。 您可利用數種方法復原內容檔案，但是最簡單的方法是從網站伺服器的檔案系統備份還原檔案。

 如果您沒有套件來源檔案的檔案系統備份，則必須手動複製或下載套件來源檔案，就如同初次建立套件一般。 您可以在 SQL Server 中執行以下查詢，找出所有套件和應用程式的套件來源位置： `SELECT * FROM v_Package`。 您可以查看封裝識別碼的前三個字元，藉此識別封裝來源站台。 例如，如果封裝識別碼為 CEN00001，則來源站台的站台碼為 CEN。 當您還原套件來源檔案時，檔案必須還原到失敗前所在的相同位置。

 如果沒有包含內容庫的檔案系統備份，您可以選擇下列還原方式：

-   **匯入預先設置的內容檔案**：如果您有 Configuration Manager 階層，則可以建立包含另一個位置的所有套件及應用程式的預先設置內容檔案，然後匯入預先設置的內容檔案，以便在站台伺服器上復原內容庫。

-   **更新內容**：您對封裝或應用程式部署類型開始進行更新內容動作時，內容會從封裝來源複製到內容庫。 原始位置中必須有套件來源檔案，此動作才能成功完成。 您必須在每個套件及應用程式上執行此動作。

### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>在執行更新發行者的電腦上復原自定軟體更新
若備份計劃包含 Updates Publisher 資料庫檔案，一旦執行 Updates Publisher 的電腦發生故障，就可以復原該資料庫。 如需更新發行者的詳細資訊，請參閱 System Center TechCenter 文件庫中的 [System Center Updates Publisher 2011 (System Center 更新發行者 2011)](http://go.microsoft.com/fwlink/p/?LinkId=228726) 。

使用以下程序來還原 Updates Publisher 資料庫。

#### <a name="to-restore-the-updates-publisher-2011-database"></a>還原更新發行者 2011 年資料庫
1.  在復原的電腦上重新安裝 Updates Publisher。

2.  將資料庫檔案 (Scupdb.sdf) 從備份目的地複製到執行 Updates Publisher 之電腦上的 %*使用者設定檔*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\。

3.  如果電腦中有一位以上的使用者執行 Updates Publisher，必須將每個資料庫檔案複製到適當的使用者設定檔位置。

### <a name="user-state-migration-data"></a>使用者狀態移轉資料
指定用於儲存使用者狀態移轉資料的資料庫，作為狀態移轉點網站系統內容。 復原含使用者狀態移轉資料資料夾的伺服器後，必須將伺服器上的使用者狀態移轉資料手動還原至故障前儲存這些資料的資料夾。

### <a name="regenerate-the-certificates-for-distribution-points"></a>重新產生用於發佈點的憑證
還原站台後，distmgr.log 可能包含下列一或多個發佈點項目： **無法解密憑證 PFX 資料**。 此項目指出站台無法解密發佈點憑證資料。 若要解決此問題，您必須針對受影響的發佈點重新產生或重新匯入憑證。 這可利用 PowerShell Cmdlet [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) 加以完成。

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>更新用於雲端發佈點的憑證
 Configuration Manager 需要使用管理憑證讓站台伺服器與雲端發佈點通訊。 復原網站後，必須更新用於雲端發佈點的憑證。

## <a name="recover-a-secondary-site"></a>復原次要站台
 Configuration Manager 不支援次要站台的資料庫備份，但可透過重新安裝次要站台支援復原。 Configuration Manager 次要站台故障時，必須復原次要站台。

### <a name="requirements-for-reinstalling-a-secondary-site"></a>重新安裝次要站台的需求
-   電腦必須符合所有次要網站必要條件，而且必須設定適當的安全性權限。
-   您必須使用先前在故障站台中使用的安裝路徑。
-   您使用的電腦必須和故障電腦擁有相同的設定 (例如其 FQDN)，才能順利復原次要網站。
-   電腦必須和失敗的站台擁有相同的 SQL Server 設定。
  -   復原次要站台時，如果電腦中尚未安裝 SQL Server Express，Configuration Manager 不會進行安裝。
  -   您必須使用次要網站資料庫故障前所使用的 SQL Server 版本及相同的 SQL Server 執行個體。

### <a name="to-recover-a-secondary-site"></a>復原次要站台：
從 Configuration Manager主控台的 [站台] 節點，使用 [復原次要站台] 動作，即可復原次要站台。 不同於管理中心網站或主要網站的復原，復原次要網站不會使用備份檔案，而是改為在已失敗的次要網站電腦上重新安裝次要網站檔案。 重新安裝站台之後，從父主要站台資料上重新初始化次要站台資料。

復原過程中，Configuration Manager 會驗證次要站台電腦上是否有內容庫，以及是否有適當的內容。 如果有適當的內容，次要網站會使用現有內容庫。 否則，若要復原已復原的次要網站內容庫，您需要重新發佈或預先設置該已復原網站的內容。

如果發佈點不在次要網站上，復原次要網站時可以不重新安裝發佈點。 復原次要網站後，網站會自動與發佈點同步。

您可以從 Configuration Manager 主控台的 [站台] 節點，使用 [顯示安裝狀態] 動作來確認次要站台復原的狀態。
