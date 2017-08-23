---
title: "監視複寫 | Microsoft Docs"
description: "了解如何使用主控台中的 [監視] 工作區，監視 Configuration Manager 的基礎結構和操作。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fab4d67-8d2a-45ce-8b06-471280102cf6
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 132803a1aa9aad5c5462686bd656688418e47d07
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-hierarchy-and-replication-infrastructure-in-system-center-configuration-manager"></a>監視 System Center Configuration Manager 的階層及複寫基礎結構

*適用對象：System Center Configuration Manager (最新分支)*

若要監視 System Center Configuration Manager 的基礎結構和作業，請使用 Configuration Manager 主控台的 [監視] 工作區。  

> [!NOTE]  
>  此位置的例外狀況為移轉，移轉可以直接在 [系統管理]  工作區的 [移轉]  節點中進行監視。 如需詳細資訊，請參閱 [移轉到 System Center Configuration Manager 的作業](../../../core/migration/operations-for-migration.md)。  

 除了使用 Configuration Manager 主控台進行監視，您還可以使用 Configuration Manager 報告，或檢視 Configuration Manager 元件的 Configuration Manager 記錄檔。 如需報告的資訊，請參閱 [System Center Configuration Manager 中的報告](../../../core/servers/manage/reporting.md)。 如需記錄檔的資訊，請參閱 [System Center Configuration Manager 中的記錄檔](../../../core/plan-design/hierarchy/log-files.md)。  

 當您在監視站台時，可尋找指出有問題需要您處理的記號。 例如：  

-   站台伺服器和站台系統上的積存檔案。  

-   指出錯誤或問題的狀態訊息。  

-   無法進行站台內通訊。  

-   伺服器上系統事件記錄中的錯誤和警告訊息。  

-   Microsoft SQL Server 錯誤記錄中的錯誤和警告訊息。  

-   長時間未回報的站台或用戶端。  

-   SQL Server 資料庫的回應緩慢。  

-   硬體故障的跡象。  

為了要使站台故障的風險降至最低，如果監視工作發現有任何出現問題的跡象，請調查問題的來源，並盡快修復問題。  



##  <a name="BKMK_MonintorMgmtTasks"></a> 監視 Configuration Manager 的一般管理工作  
 Configuration Manager 從 Configuration Manager 主控台內提供內建的監視。 您可以監視許多工作，包括與軟體更新、電源管理，以及整個階層中的內容部署相關的工作。  

 請參考下列資訊來協助您監視常見的 Configuration Manager 工作：  

 **警示**  
   請參閱 [使用 System Center Configuration Manager 的警示和狀態系統](../../../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorAlerts) 中的 [監視 Configuration Manager 的狀態系統](../../../core/servers/manage/use-alerts-and-the-status-system.md)。  

 **相容性設定**  
   請參閱[如何在 System Center Configuration Manager 中監視相容性設定](../../../compliance/deploy-use/monitor-compliance-settings.md)。  

 **內容部署**  
   如需監視內容的一般資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

如需監視特定類型內容部署的詳細資訊：
-   若要監視應用程式，請參閱[使用 System Center Configuration Manager 監視應用程式](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  

-   若要監視封裝和程式，請參閱 [System Center Configuration Manager 中的封裝和程式](../../../apps/deploy-use/packages-and-programs.md)中的如何管理封裝和程式。  

**Endpoint Protection**  
   請參閱[如何監視 System Center Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)。  

**監視電源管理**  
 請參閱[如何監視和規劃 System Center Configuration Manager 的電源管理](../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)。  

**監視軟體計量**  
請參閱[在 System Center Configuration Manager 中使用軟體計量監視應用程式使用量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

**監視軟體更新**  
 請參閱[在 System Center Configuration Manager 中監視軟體更新](../../../sum/deploy-use/monitor-software-updates.md)。  


##  <a name="BKMK_MonitorInfrastructure"></a> 監視 Configuration Manager 的階層基礎結構  
Configuration Manager 提供數種可監視階層狀態和操作的方法。 您可以檢查整個階層上站台的系統狀態、監視來自站台階層或地理檢視的站台內複寫、監視站台間資料庫複寫的複寫連結，以及使用複寫連結分析師工具補救複寫問題。  

###  <a name="BKMK_SH_Node"></a> 關於站台階層節點  
[監視] 工作區的 [站台階層] 節點提供您 Configuration Manager 階層和站台間連結的概觀。 您可以使用兩種檢視：  

-   **階層圖**：此檢視會以拓撲圖顯示您的階層，該圖已簡化為只顯示重要資訊。  

-   **地理檢視**：此檢視會以地圖顯示您的站台，顯示您所設定的站台位置。  

使用 [站台階層]  節點監視各站台的健全狀況、站台內複寫連結，以及其與外在因素的關聯性，例如地理位置。  

由於站台狀態和站台內連線狀態會複寫為站台資料，而不是全域資料，因此當您將 Configuration Manager 主控台連線到子主要站台時，無法檢視其他主要站台或其子次要站台的站台或連結狀態。 例如，在多重主要站台階層中，當您的 Configuration Manager 主控台連線到主要站台時，您可以檢視子次要站台、主要站台和管理中心網站的狀態，但您無法查看管理中心網站下方階層中其他節點的狀態。  

 請使用 [設定設定值]  命令控制站台階層顯示的呈現方式。 當 Configuration Manager 主控台連線到一個站台時，對 [站台階層] 節點所進行的設定都會複寫到所有其他站台。  

#### <a name="hierarchy-diagram"></a>階層圖  
 階層圖會以拓撲圖顯示您的站台。 在此檢視中，您可以從該站台選取站台和檢視狀態訊息摘要切入以檢視狀態訊息，以及存取站台的 [內容]  對話方塊。  

 此外，您可以將滑鼠指標暫停在站台或站台間的複寫連結上，以檢視該物件的高階狀態。 由於複寫連線狀態不會進行全域複寫，因此在內含多重主要站台的階層中，您必須將 Configuration Manager 主控台連線到管理中心網站，如此才能檢視所有站台間的複寫連結詳細資。  

 下列選項可修改階層圖：  

-   **群組**：您可以設定在階層圖中觸發變更的主要站台和次要站台數目，圖中會將這些站台合併為單一物件。 當多個站台合併為單一物件，您就可以查看站台的總數，以及狀態訊息和站台狀態的高階彙總。 群組設定不會影響地理檢視。  

-   **我的最愛站台**：您可以將個別站台指定為我的最愛站台。 階層圖會以星號圖示識別我的最愛站台。 我的最愛站台不會在您使用群組時與其他站台合併，而且永遠會個別顯示。  

#### <a name="geographical-view"></a>地理檢視  
 地理檢視會以地圖顯示各站台的位置。 只會顯示使用位置設定的站台。 當您在此檢視中選取站台時，會顯示複寫到父站台或子站台的連結。 和階層圖檢視不同的是，您不能在此檢視中顯示站台狀態訊息或複寫連結詳細資料。  

> [!NOTE]  
>  若要使用地理檢視，您的 Configuration Manager 主控台所連線的電腦必須已安裝 Internet Explorer，並且能夠使用 HTTP 通訊協定存取 Bing 地圖服務。  

下列選項可修改地理檢視。  

-   **站台位置**：您可以為每個站台指定地理位置。 您可以將位置指定為街道地址、地圖名稱 (如城市名稱)，或緯度和經度座標。 例如，若要使用 Redmond Washington 的緯度和經度，您可以指定 **N 47 40 26.3572 W 122 7 17.4432** 作為站台的位置。 您不需要指定經度或緯度的度數、分鐘或秒數的符號。 Configuration Manager 會使用 Bing 地圖服務，在地理檢視上顯示位置。 這讓您可以選擇檢視與地理位置相關的階層，深入瞭解可能會影響到特定站台或站台內複寫的地區問題。  

     當您指定某個位置時，可使用 [位置]  方塊來搜尋階層中的特定站台。 選取站台之後，請在 [位置]  資料行輸入位置的縣 (市) 名稱或街道地址。 Configuration Manager 使用 Bing 地圖服務以解析此位置。  

###  <a name="BKMK_MonitorRepLinksAndStatuss"></a> 如何監視資料庫複寫連結和複寫狀態  
 除了從 [監視]  工作區的 [站台階層]  節點存取高階詳細資料， 您也可以在使用 [監視]  工作區的 [資料庫複寫]  節點時，監視資料庫複寫的詳細資料。 您可以從 [資料庫複寫] 監視站台間複寫連結的狀態，以及您的 Configuration Manager 主控台所連線之站台上複寫群組的初始化詳細資料和複寫詳細資料。  

> [!TIP]  
>  雖然 [資料庫複寫]  節點也會顯示在 [系統管理]  工作區的 [階層設定]  節點中，但您無法從該位置檢視資料庫複寫連結的複寫狀態。  

####  <a name="BKMK_MonitorReplicationLinks"></a> 複寫連結狀態  
站台間的資料庫複寫包含多組資訊的複寫，稱為複寫群組。 每個複寫群組會以不同複寫優先順序進行複寫。 根據預設，複寫群組中包含的資料和複寫的頻率都無法修改。  

 當複寫連結在使用中時，而且沒有失敗或降級的狀態時，會及時複寫所有的複寫群組。 當一個或多個複寫群組無法在預訂的時間內完成複寫時，該連結會顯示為降級狀態。 降級的連結仍然可以運作，但您應該監視這些連結，確定它們是否返回使用中狀態，或調查它們以確定未發生其他降級或複寫失敗情形。  

 您可以為每個複寫連結指定當複寫群組在複寫不成功時可重試複寫的次數，之後連結的狀態就會設定為降級或失敗。 即使所有複寫群組的複寫只有一個複寫群組失敗，連結的狀態就會設定為降級或失敗，因為在指定的嘗試次數內有一個複寫群組無法完成複寫。 如需複寫閾值的資訊，請參閱 [System Center Configuration Manager 中的站台間資料傳輸](../../../core/servers/manage/data-transfers-between-sites.md)主題中的[資料庫複寫閾值](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds)一節。  

 使用下表中的資訊可瞭解需要進一步調查的複寫連結狀態。  

|連結描述|詳細資訊|  
|----------------------|----------------------|  
|**連結使用中**|未偵測到問題，連結通訊正進行中。|  
|**連結已降級**|複寫正常運作，但至少有一個複寫物件或群組發生延遲。 監視處於此狀態的連結，並檢閱連結上兩個站台的資訊，確定連結是否發生失敗的情形。<br /><br /> 當站台接收到的複寫資料無法快速將資料認可到資料庫時，連結可能也會顯示降級的狀態。 在進行大量資料複寫時，可能會發生此情況。 例如，若部署軟體更新到大量電腦，連結上的父站台可能需要一些時間來處理大量的資料複寫。 父站台上的處理延隔，可能會導致連結狀態設為降級，直到父站台順利處理資料的積存為止。|  
|**連結已失敗**|複寫無法運作。 複寫連結有可能在沒有進一步動作的情況下復原。 您可以使用複寫連結分析師來調查及協助補救此連結上的複寫。<br /><br /> 此狀態也可能表示複寫連結上父站台和子站台之間發生實體網路的問題。|  

 當父站台正在升級到新的 Service Pack，而且您正在從子站台檢視連結狀態時，連結狀態會顯示為使用中。 升級後，要等到子站台與父站台使用相同的 Service Pack 時，從父站台檢視時連結狀態會顯示為使用中，而從子站台檢視時會顯示為已設定。  

####  <a name="BKMK_MonitorReplicationStatus"></a> 複寫狀態  
 您可以使用 [監視]  工作區的 [資料庫複寫]  節點來檢視複寫連結的複寫狀態，以及檢視與複寫連結上各個站台的站台資料庫相關詳細資料。 您也可以檢視與複寫群組相關的詳細資料。 若要檢視詳細資料，請選取複寫連結，然後針對您要檢視的複寫狀態選取適當的索引標籤。 以下是複寫狀態之各種不同索引標籤的相關詳細資料。  

 **摘要**  
 檢視與站台資料的複寫以及連結上兩個站台間全域資料相關的層級資訊。  

 您也可以按一下 [檢視歷史流量資料的報告]  ，檢視顯示與透過複寫連結進行複寫所使用網路頻寬相關的詳細資料報告。  

 **父站台**  
 針對複寫連結上的父站台，檢視與資料庫相關的詳細資料，包括：  

-   SQL Server 的防火牆連接埠  

-   可用磁碟空間  

-   資料庫檔案位置  

-   憑證  

**子站台**  
 針對複寫連結上的子站台，檢視與資料庫相關的詳細資料，包括：  

-   SQL Server 的防火牆連接埠  

-   可用磁碟空間  

-   資料庫檔案位置  

-   憑證  

**初始化詳細資料**    
 檢視透過複寫連結進行複寫的複寫群組初始化狀態。 此資訊可協助您識別初始化複寫資料正在進行中或已失敗。  

 此外，您可以使用此資訊來識別站台進入互通性模式的時間。 互通性模式會在子站台與父站台不是使用相同版本的 Configuration Manager 時發生。  

**複寫詳細資料**    
 檢閱每個跨連結複寫之複寫群組的複寫狀態。 利用這項資訊可幫助您識別複寫特定資料時的問題或延遲，並且有助於判斷適合此連結的資料庫複寫臨界值。 如需資料庫複寫閾值的資訊，請參閱 [System Center Configuration Manager 中的站台間資料傳輸](../../../core/servers/manage/data-transfers-between-sites.md)主題中的[資料庫複寫閾值](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds)一節。  

> [!TIP]  
>  站台資料的複寫群組只會從子站台傳送至父站台。 全域資料的複寫群組則會雙向複寫。  

###  <a name="BKMK_RLA"></a> 關於複寫連結分析師  
 Configuration Manager 包含**複寫連結分析師**，可用來分析及修復複寫問題。 您可以使用複寫連結分析師在複寫失敗時，以及在複寫停止運作但尚未回報失敗時，補救複寫連結錯誤。 複寫連結分析師可用來補救 Configuration Manager 階層中下列電腦之間的複寫問題 (複寫失敗的方向沒有影響)：  

-   站台伺服器和站台資料庫伺服器之間。  

-   每一個站台的站台資料庫伺服器和另一個站台的站台資料庫電腦之間 (站台間複寫)。  

您可以在 Configuration Manager 主控台或命令提示字元中執行複寫連結分析師：  

-   在 Configuration Manager 主控台中執行：在 [監視] 工作區中按一下 [資料庫複寫] 節點，選取您要分析的複寫連結，然後在 [首頁] 索引標籤的 [資料庫複寫] 群組中，選取 [複寫連結分析師]。  

-   若要在命令提示字元中執行，請輸入下列命令：**%路徑%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe &lt;來源站台伺服器 FQDN\> &lt;目的地站台伺服器 FQDN\>**。  

當您執行複寫連結分析師時，它會使用一系列診斷規則和檢查偵測問題。 當工具執行時，您可以檢視工具識別出的問題。 如果已知有解決問題的指示，則會顯示。 如果複寫連結分析器可自動補救問題，就會對您顯示該選項。 複寫連結分析器完成時，會將結果儲存到下列 XML 報告中，以及執行工具的使用者桌面上的記錄檔中：  

-   ReplicationAnalysis.xml  

-   ReplicationLinkAnalysis.log  

當複寫連結分析師執行時，會在補救問題時停止下列服務，並且在補救完成後重新啟動這些服務：  

-   SMS_SITE_COMPONENT_MANAGER  

-   SMS_EXECUTIVE  

如果複寫連結分析師補救失敗，請檢閱站台伺服器並重新啟動這些服務 (如果已停止)。  

成功和不成功的調查與補救動作都會加以記錄，以提供工具介面上未顯示的其他詳細資料。  

**使用複寫連結分析師的必要條件：**  

-   您用來執行複寫連結分析師的帳戶，必須具有複寫連結中所包含每一部電腦上的本機系統管理員權限。 帳戶不需要特定角色為基礎的系統管理安全性角色。 因此，有權存取 [資料庫複本] 節點的系統管理使用者可以在 Configuration Manager 主控台執行此工具，或是對每部電腦有足夠權限的系統管理員可以在命令提示字元執行此工具。  

-   您用來執行複寫連結分析師的帳戶，必須具有複寫連結中所包含每一個 SQL Server 的 sysadmin 權限。  

**複寫連結分析師的已知問題：**  

-   隨著 System Center Configuration Manager 1511 版的發行，複寫連結分析師在從 System Center 2012 Configuration Manager 升級的主要站台中會產生 SQL Server Service Broker 憑證錯誤。 這是因為 1511 版本導入了憑證名稱變更，但複寫連結分析師尚未更新。 忽略這些錯誤並無大礙。  

###  <a name="BKMK_ProcsforMonitoringReplication"></a> 監視資料庫複寫的程序  

##### <a name="to-monitor-high-level-site-to-site-database-replication-status"></a>若要監視高階站台對站台資料庫複寫狀態    
1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，按一下 [站台階層]  開啟 [階層圖]  檢視。  

3.  將滑鼠指標短暫暫停於兩個站台之間的線上，即可檢視這些站台的全域和站台資料複寫的狀態。  

##### <a name="to-monitor-the-replication-status-for-a-replication-link"></a>若要監視複寫連結的複寫狀態    
1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，按一下 [資料庫複寫] ，然後選取您要監視之連結的複寫連結。 然後在工作區中，選取適當的索引標籤檢視有關該連結之複寫狀態的各種不同詳細資料。  
