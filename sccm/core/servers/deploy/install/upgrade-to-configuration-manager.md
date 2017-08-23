---
title: "升級至 System Center Configuration Manager | Microsoft Docs"
description: "了解從執行 System Center 2012 Configuration Manager 的站台和階層中執行成功就地升級的步驟。"
ms.custom: na
ms.date: 6/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
caps.latest.revision: "21"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1166b739e1e8d667172d97883f484fdbc3a142c1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-to-system-center-configuration-manager"></a>升級至 System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*

您可以從執行 System Center 2012 Configuration Manager 的站台和階層中執行就地升級以升級至 System Center Configuration Manager。  

 從 System Center 2012 Configuration Manager 升級之前，您必須準備站台，這需要您移除可能會讓升級無法成功的特定設定，然後在涉及多個站台時依照升級的順序。  

 > [!TIP]
 > 管理 System Center Configuration Manager 站台及階層基礎結構時，「升級」、「更新」及「安裝」等詞彙是用來描述三種不同的概念。 若要了解如何使用每個詞彙，請參閱[關於升級、更新和安裝](/sccm/core/understand/upgrade-update-install)。

##  <a name="bkmk_path"></a> 就地升級路徑  

**升級到 1702 版**   
當您具有 1702 版基準媒體時，可以將下列產品升級至 System Center Configuration Manager 1702 版的完整授權版本：   
-     System Center Configuration Manager 1702 版的評估版安裝
-     System Center 2012 Configuration Manager (含 Service Pack 1)
-     System Center 2012 Configuration Manager (含 Service Pack 2)
-     System Center 2012 R2 Configuration Manager
-     System Center 2012 R2 Configuration Manager (含 Service Pack 1)

**升級至 1606 版**  
在 2016 年 12 月 15 日，發行 1606 版的基準媒體，以新增額外升級案例的支援。 這個新版本支援將下列產品升級至 System Center Configuration Manager 1606 版的完整授權版本：  
-   System Center Configuration Manager 1606 版的評估版安裝
-   System Center Configuration Manager 的候選版安裝  
-   System Center 2012 Configuration Manager (含 Service Pack 1)  
-   System Center 2012 Configuration Manager (含 Service Pack 2)  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager (含 Service Pack 1)  

如果您使用在 2016 年 12 月 15 日之前下載的 1606 版基準媒體，則只可以將下列產品升級至 System Center Configuration Manager 1606 版的完整授權版本：
-   System Center Configuration Manager 1606 版的評估版安裝
-   System Center 2012 Configuration Manager (含 Service Pack 2)
-   System Center 2012 R2 Configuration Manager (含 Service Pack 1)

<!-- Version 1511 has now dropped out of support
**Upgrade to version 1511**  
When you have version 1511 baseline media, you can upgrade the following to a fully licensed  version of System Center Configuration Manager version 1511:  
-   An evaluation install of System Center Configuration Manager version 1511
-   A release candidate install of System Center Configuration Manager  
-   System Center 2012 Configuration Manager with Service Pack 1  
-   System Center 2012 Configuration Manager with Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager with Service Pack 1  
-->


> [!TIP]  
>  當您從 System Center 2012 Configuration Manager 版本升級至最新分支時，可能可以簡化升級程序。 如需詳細資訊，請參閱下列各項：  
>   
>  -   [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)中的[基準和更新版本](../../../../core/servers/manage/updates.md#bkmk_Baselines)一節  
>  -   [System Center Configuration Manager 的 CD.Latest 資料夾](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **不支援下列項目：**  
-   不支援將 System Center Configuration Manager 的 Technical Preview 升級至完整授權安裝。  Technical Preview 版本只能升級至較新版的 Technical Preview。  

-   不支援從 Technical Preview 移轉至完整授權版本。  

##  <a name="bkmk_checklist"></a> 升級檢查清單  
 下列檢查清單可協助您規劃順利升級至 System Center Configuration Manager。  

### <a name="before-you-upgrade"></a>升級之前  

**檢閱您的 System Center 2012 Configuration Manager 環境**，並解決 KB4018655 中所述的問題︰[由於週期性重試工作，Configuration Manager 用戶端會每隔五小時重新安裝，而且可能會導致意外的用戶端升級](https://support.microsoft.com/help/4018655)。

**確認您的運算環境符合升級至 System Center Configuration Manager 所需的支援設定：**  

檢閱用來裝載站台系統角色的伺服器作業系統：  

-   System Center Configuration Manager 不支援 System Center 2012 Configuration Manager 支援的某些舊版作業系統，而且必須先重新放置或移除這些作業系統上的站台系統角色才能升級。 請檢閱[站台系統伺服器支援的作業系統](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)文件。   
-   Configuration Manager 的必要條件檢查程式不會驗證站台伺服器或遠端站台系統上的站台系統角色必要條件  

請檢閱裝載站台系統角色之每部電腦的必要條件：  

-   例如，為了部署作業系統，System Center Configuration Manager 使用 Windows 10 評定及部署套件 (Windows ADK)。 在執行安裝程式之前，您必須在站台伺服器和執行 SMS 提供者執行個體的每部電腦上，下載並安裝 Windows 10 ADK。  

如需支援的平台和必要條件設定的一般資訊，請參閱 [Supported configurations for System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)。  

如需搭配使用 Windows ADK 與 Configuration Manager 的資訊，請參閱 [System Center Configuration Manager 中作業系統部署的基礎結構需求](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

**檢閱站台和階層狀態，並確認沒有任何未解決的問題：**  
在升級網站之前，請先針對網站伺服器、網站資料庫伺服器，以及安裝在遠端電腦上的網站系統角色，解決所有操作問題。 網站升級會因為現有的操作問題而失敗。  

**在裝載站台、站台資料庫伺服器和遠端站台系統角色的電腦上，安裝其作業系統適用的所有重大更新：**  
在升級網站之前，為每個適用的網站系統安裝任何重大更新。 如果您安裝的更新需要重新啟動，請先重新啟動適用的電腦再開始進行 Service Pack 更新。  

如需詳細資訊，請參閱 [Windows Update](http://go.microsoft.com/fwlink/p/?LinkId=105851)。  

**解除安裝 System Center Configuration Manager 不支援的站台系統角色：**  
下列站台系統角色無法再用於 System Center Configuration Manager，必須先解除安裝才能從 System Center 2012 Configuration Manager 升級：  

-   超出訊號範圍管理點  
-   系統健全狀況驗證程式點  

**在主要站台上停用管理點的資料庫複本：**  
Configuration Manager 無法成功升級具有已啟用管理點之資料庫複本的主要站台。 在下列情況之前先停用資料庫複寫：  

-   建立站台資料庫的備份以測試資料庫升級  
-   將生產站台升級至 System Center Configuration Manager  

如需詳細資訊，請參閱下列各項：  
-   System Center 2012 Configuration Manager：[設定管理點的資料庫複本](https://technet.microsoft.com/library/hh846234.aspx)  
-   System Center Configuration Manager：[System Center Configuration Manager 的管理點資料庫複本](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

**重新設定使用 NLB 的軟體更新點：**  
Configuration Manager 無法升級使用網路負載平衡 (NLB) 叢集的站台以裝載軟體更新點。  

如果您將 NLB 叢集用於軟體更新點，請使用 PowerShell 移除 NLB 叢集。 (從 System Center 2012 Configuration Manager SP1 開始，Configuration Manager 主控台中沒有選項可以設定 NLB 叢集)  

**停用站台升級期間各站台的所有站台維護工作：**  
在您升級至 System Center Configuration Manager 之前，請停用任何可能在進行升級程序期間執行的站台維護工作。 這包括但不限於下列項目：  

-   備份網站伺服器  
-   刪除過時用戶端操作  
-   刪除過時探索資料  

當網站資料庫維護工作在升級期間執行時，網站升級可能會失敗。  

在停用工作前，請將工作的排程記錄下來，以便在網站升級完成後您可以還原其設定。  

如需有關站台維護工作的詳細資訊，請參閱：  

-   System Center 2012 Configuration Manager：[規劃 Configuration Manager 的維護工作](https://technet.microsoft.com/library/gg712686.aspx)  
-   System Center Configuration Manager：[System Center Configuration Manager 的維護工作參考](../../../../core/servers/manage/reference-for-maintenance-tasks.md)  

**執行安裝程式必要條件檢查工具**：  
在升級站台之前，您可以在安裝程式之外獨立執行 **必要條件檢查工具** ，以驗證您的站台是否符合必要條件。 稍後，在升級站台之前，必要條件檢查程式會再次執行。  

如果您使用 2016 年 10 月發行版中的 1606 版基準媒體，獨立必要條件檢查會評估站台，以升級到 System Center Configuration Manage 的最新分支和長期維護分支 (LTSB)。 因為 LTSB 不支援某些功能，所以您可能會在 *ConfigMgrPrereq.log* 中看到與下列類似的項目：
 - 資訊: 站台是 LTSB 版本。
 - LTSB 版本不支援站台系統角色「Asset Intelligence 同步處理點」;    錯誤;    Configuration Manager 偵測到已安裝「Asset Intelligence 同步處理點」。 LTSB 版本不支援 Asset Intelligence。 您必須先解除安裝 Asset Intelligence 同步處理點站台系統角色，才能繼續。

如果您想要升級至最新分支，則可以放心略過 LTSB 版本的錯誤。 只有在您想要升級至 LTSB 時，它們才適用。

稍後，當您執行 Configuration Manager 安裝程式來進行升級時，必要條件檢查會再次執行，並根據您選擇安裝之 System Center Configuration Manager 的分支 (最新分支或 LTSB) 來評估站台。 如果您選擇升級至最新分支，則不會執行 LTSB 不支援之功能的檢查。

如需詳細資訊，請參閱[必要條件檢查程式](/sccm/core/servers/deploy/install/prerequisite-checker)和 [System Center Configuration Manager 的必要條件檢查清單](/sccm/core/servers/deploy/install/list-of-prerequisite-checks)。  

**為 System Center Configuration Manager 下載必要條件檔案和可轉散發檔案：**    
使用**安裝程式下載程式**以下載必要的可轉散發檔案、語言套件以及 System Center Configuration Manager 的最新產品更新。  

如需詳細資訊，請參閱[安裝程式下載程式](/sccm/core/servers/deploy/install/setup-downloader)。  

**規劃伺服器和用戶端語言的管理**：  
當您升級站台時，站台升級只會安裝您在升級期間選取的語言組件版本。  

-   安裝程式會檢閱站台目前的語言設定，然後在儲存先前所下載之必要條件檔案的資料夾中識別可用的語言套件。  
-   然後您就可以確認目前選取的伺服器和用戶端語言套件，或變更這些選擇以新增或移除語言的支援。  
-   您只能選取在執行安裝程式 (您會與下載的必要條件檔案一起取得) 時使用的語言套件。  

> [!NOTE]  
>  您無法使用 System Center 2012 Configuration Manager 的語言套件，來啟用 System Center Configuration Manager 站台的語言。  

如需語言套件的詳細資訊，請參閱 [System Center Configuration Manager 的語言套件](../../../../core/servers/deploy/install/language-packs.md)。  

**檢閱站台升級的考慮事項**：  
當您升級網站時，部分功能和設定會重設為預設設定。 為了幫助您準備這些及相關的變更，請檢閱  [升級時的考量](#bkmk_considerations)中的資訊。  

**在管理中心網站和主要站台上建立站台資料庫的備份：**  
在升級網站之前，請備份網站資料庫以確認您已成功備份，以供災害復原使用。  

請參閱 [System Center Configuration Manager 的備份和復原](../../../../protect/understand/backup-and-recovery.md)。  

**備份自訂的 Configuration.mof 檔案**：  
如果您使用自訂的 Configuration.mof 檔案來定義您搭配硬體清查使用的資料類別，請建立此檔案的備份，然後再升級站台。 接著，在升級之後，將這個檔案還原到您的站台。 如需使用此檔案的詳細資訊，請參閱[如何擴充 System Center Configuration Manager 中的硬體清查](../../../../core/clients/manage/inventory/extend-hardware-inventory.md)。  

**在最新站台資料庫備份的複本上測試資料庫升級程序：**  
在升級 Configuration Manager 管理中心網站或主要站台之前，請先在站台資料庫複本上進行站台資料庫升級程序的測試。  

-   您應該測試站台資料庫升級程序，因為當您升級站台時，可能會修改站台資料庫  
-   測試資料庫升級並非必要，但是可以在您的生產資料庫受到影響之前找出升級問題  
-   站台資料庫升級失敗可能會造成站台資料庫無法運作，且可能需要站台復原才能恢復功能  
-   雖然站台資料庫在階層中的網站之間共用，您仍需要在升級該網站之前先規劃每個適用站台上的資料庫測試  
-   如果您在主要站台上使用管理點的資料庫複本，請在建立站台資料庫的備份之前停用複寫  

Configuration Manager 不支援次要站台的備份或次要站台資料庫的測試升級。  

這不支援在生產網站資料庫上執行測試資料庫升級。 在網站資料庫上進行這類升級可能會造成網站無法運作。  

如需詳細資訊，請參閱 [測試站台資料庫升級](#bkmk_test)。  

**重新啟動站台伺服器以及每部裝載站台系統角色的電腦**：  
完成這項作業可確認目前的更新安裝或必要條件中沒有擱置中的動作，而且是公司特有的內部程序。  

**升級站台**的完整授權版本：  
從階層中的頂層站台開始，從 System Center Configuration Manager 來源媒體執行 Setup.exe。  

頂層站台完成升級之後，您就可以開始升級每個子站台。 請先完成每個站台的升級，再開始升級下一個站台  

在階層中的所有站台都升級至 System Center Configuration Manager 之前，您的階層仍會以混合的版本模式運作。  

如需如何執行升級的資訊，請參閱[升級站台](#bkmk_upgrade)。  

### <a name="after-you-upgrade"></a>升級之後  
**升級獨立 Configuration Manager 主控台**：  
當您升級管理中心網站或主要站台時，安裝預設也會升級已安裝在站台伺服器上的 Configuration Manager 主控台。 不過，針對在站台伺服器以外的電腦上安裝的每個主控台，您必須手動進行升級。  

> [!TIP]  
>  在您啟動升級之前，請關閉已開啟的主控台。  

如需詳細資訊，請參閱[安裝 System Center Configuration Manager 主控台](../../../../core/servers/deploy/install/install-consoles.md)。  

**在主要站台上重新設定管理點的資料庫複本：**  
如果您在主要網站上使用管理點的資料庫複本，必須先解除安裝資料庫複本才能升級網站。 升級主要網站後，請重新設定管理點的資料庫複本。   
如需詳細資訊，請參閱  [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

**重新設定您在升級前停用的任何資料庫維護工作：**  
如果您在升級前已停用站台的資料庫 [System Center Configuration Manager 的維護工作參考](../../../../core/servers/manage/reference-for-maintenance-tasks.md)，請使用升級前相同的設定值重新設定站台的這些工作。  

**升級用戶端**：  
所有站台都升級至 System Center Configuration Manager 之後，規劃升級用戶端。  

升級用戶端時會解除安裝目前的用戶端軟體，並且安裝新版的用戶端軟體。 若要升級用戶端，可以使用 Configuration Manager 支援的任何方法。  

> [!TIP]  
>  將階層的頂層網站升級為新的 Service Pack 時，也會更新階層中每個發佈點上的用戶端安裝套件。 升級主要網站時，會同時更新該主要網站提供的用戶端升級套件。  

如需如何升級現有用戶端以及如何安裝新用戶端的資訊，請參閱[如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

##  <a name="bkmk_considerations"></a> 升級時的考量  
**自動動作**：  
當您升級至 System Center Configuration Manager 時，會自動執行下列動作：  

-   網站會執行網站重設，包括重新安裝所有網站系統角色。  
-   如果該網站為階層的頂層網站，便會更新階層中每個發佈點的用戶端安裝套件。 站台也會更新預設開機映像以使用包含於 Windows 評定及部署套件 8.1 的新版 Windows PE。 不過，該升級不會升級與映像部署搭配使用的現有媒體。  
-   如果網站為主要網站，則會更新該網站的用戶端升級套件。  

**升級後的系統管理員手動動作**   
升級站台之後，請確定已執行下列動作：  

-   確定指派至每個主要站台的用戶端皆升級並安裝新版本用戶端軟體  
-   升級連線至該站台及在站台伺服器遠端之電腦上執行的每個 Configuration Manager 主控台。  
-   在使用管理點資料庫複本的主要站台上，重新設定資料庫複本  
-   網站升級之後，您必須先手動升級如 CD 與 DVD 或 USB 快閃磁碟機的 ISO 檔案實體媒體，或預先設置用於 Windows To Go 部署的媒體，以及提供給硬體廠商的媒體。 雖然站台更新可更新預設開機映像，但它無法升級這些媒體檔案，或是使用於 Configuration Manager 外部的裝置。  
-   當您不需要 Windows PE 原始 (舊版) 版本時，規劃更新非預設的開機映像。  

**影響設定的動作**   
站台升級至 System Center Configuration Manager 時，有些設定會在升級後消失，或者是設定為新的預設設定。 下表為會消失或改變的設定值，並提供詳細資料以協助您在站台升級期間進行規劃：  

-   **軟體中心：**  
    下列軟體中心項目會重設為預設值：  
    -   [工作資訊] 的工作時間會從星期一到星期五 [上午 5.00]  重設為 [下午 10.00]  Monday 重設為 [下午 10.00] Friday.  
    -   [電腦維護]  的值會設為 [當電腦在簡報模式時暫停軟體中心活動] 。  
    -   [遠端控制]  的值會設為指派至電腦之用戶端設定中的值。  
-   **軟體更新摘要排程：**  
     軟體更新或軟體更新群組的自訂摘要排程會重設為預設值 (1 小時)。 升級結束後，請將自訂摘要值重設為所需的頻率。  

##  <a name="bkmk_test"></a> 測試站台資料庫升級  
只有在將 System Center 2012 Configuration Manager 這類舊版本升級到 System Center Configuration Manager 時，下列資訊才會適用。

請先測試要進行升級的站台資料庫複本，再升級該站台。  

若要測試要進行升級的資料庫，可先將站台資料庫的複本還原至未裝載 Configuration Manager 站台的 SQL Server 執行個體。 您用來裝載資料庫複本的 SQL Server 版本，必須與來源資料庫複本的 Configuration Manager 版本所支援的 SQL Server 版本相同。  

接著，在還原站台資料庫後，請在 SQL Server 電腦上使用 **/TESTDBUPGRADE** 命令列選項，從 System Center Configuration Manager 的來源媒體資料夾執行 Configuration Manager 安裝程式。  

-   如需如何建立和還原站台資料庫備份的資訊，請參閱[安裝程式的命令列選項](../../../../core/servers/deploy/install/command-line-options-for-setup.md)。  
-   如需 **/TESTDBUPGRADE** 命令列選項的資訊，請參閱[安裝程式的命令列選項](../../../../core/servers/deploy/install/command-line-options-for-setup.md)中的資料表。  
-   如需所支援 SQL Server 版本的資訊，請參閱 [System Center Configuration Manager 的 SQL Server 版本支援](../../../../core/plan-design/configs/support-for-sql-server-versions.md)主題。  

> [!TIP]  
>  如果您整合 Microsoft Intune 與 Configuration Manager：  
>   
>  當您在 5 天或更多天的站台資料庫複本上執行測試資料庫升級時，可能會收到下列訊息：  
>   
>  -   警告：升級會強制完整同步處理至雲端。  
>  -   錯誤：資料庫升級將會強制完整同步處理至雲端。  
>   
> 兩種都可以在資料庫升級測試期間放心忽略，因為它們並不表示測試升級失敗或發生問題。 相反地，它們表示在實際升級期間，來自 **Cloud** 資料庫複寫群組的資料可能與 Microsoft Intune 同步處理。  

在您規劃升級的各個管理中心網站和主要站台執行下列程序。  

#### <a name="to-test-a-site-database-for-upgrade"></a>測試站台資料庫以進行升級  

1.  製作站台資料庫複本，然後將該複本還原到與您的站台資料庫所使用相同的版本，且未裝載 Configuration Manager 站台的 SQL Server 執行個體。 例如，若站台資料庫執行於 Enterprise Edition 的 SQL Server 執行個體上，請務必將資料庫還原到也是執行 Enterprise Edition 之 SQL Server 的 SQL Server 執行個體。  

2.  在您還原資料庫複本後，請從 System Center Configuration Manager 的來源媒體執行安裝程式。 當您執行安裝程式時，請使用 **/TESTDBUPGRADE** 命令列選項。 如果裝載資料庫複本的 SQL Server 執行個體不是預設的執行個體，您還需要提供命令列引數，以識別裝載站台資料庫複本的執行個體。  

     例如，您想要升級資料庫名稱為 SMS_ABC 的站台資料庫。 您會將此站台資料庫的複本，還原到執行個體名稱為 DBTest 的受支援 SQL Server 執行個體。 若要測試此站台資料庫複本的升級，請使用下列命令列： **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     您可在 System Center Configuration Manager 來源媒體的下列位置找到 Setup.exe：**SMSSETUP\BIN\X64**。  

3.  在您執行資料庫升級測試的 SQL Server 執行個體上，監視位於系統磁碟機根目錄中的 ConfigMgrSetup.log 以了解進度及成功與否：  

    -   如果測試升級失敗，請解決與站台資料庫升級失敗相關的問題，建立新的站台資料庫備份，然後再測試新的站台資料庫複本的升級。  
    -   順利進行所有程序後，便可以刪除資料庫複本。  

        > [!NOTE]  
        >  不支援還原您用於測試升級的站台資料庫複本，以當成任何站台上的站台資料庫使用。  

在您順利升級站台資料庫複本後，請繼續進行 Configuration Manager 站台及其站台資料庫的升級。  

##  <a name="bkmk_upgrade"></a> 升級站台  
在完成站台升級前的設定、在資料庫複本測試站台資料庫的升級，以及下載您想要安裝之 Service Pack 版本的必要條件檔案及語言套件後，就可以準備升級您的 Configuration Manager 站台。  

當您升級階層中的某個站台時，會先升級階層的頂層站台。 這個頂層站台可能是管理中心網站或獨立主要站台。 完成管理中心網站的升級後，您可以依所需的任何順序，升級子主要站台。 升級主要站台後，您可以升級該站台的子次要站台，或先升級其他主要站台再升級次要站台。  

若要升級管理中心網站或主要站台，您可以從 System Center Configuration Manager 來源媒體執行安裝程式。 不過，您不需要執行安裝程式就能升級次要站台。 您可以在完成主要父站台的升級後，改用 Configuration Manager 主控台升級次要站台。  

在升級站台之前，先關閉站台伺服器上安裝的 Configuration Manager 主控台，直到完成站台升級。 同時，也請關閉非站台伺服器電腦上執行的每個 Configuration Manager 主控台。 您可以在站台升級完成後，讓主控台重新連線。 不過，在將 Configuration Manager 主控台升級至 Configuration Manager 新版本後，該主控台才可以顯示 Configuration Manager 新版本中可用的部分物件和資訊。  

請使用下列程序來升級 Configuration Manager 站台：  

#### <a name="to-upgrade-a-central-administration-site-or-primary-site"></a>升級管理中心網站或主要站台  

1.  確認執行安裝程式的使用者具有以下安全性權限：  

    -   站台伺服器電腦上的本機系統管理員權限。  
    -   站台的遠端站台資料庫伺服器上的本機系統管理員權限 (如果位於遠端)。    </br></br>

2.  在站台伺服器電腦上，開啟 Windows 檔案總管，並瀏覽至 **&lt;ConfigMgSourceMedia\>\SMSSETUP\BIN\X64**。  

3.  按兩下 **Setup.exe**。 [Configuration Manager 安裝精靈] 隨即開啟。  

4.  在 [ **開始之前** ] 頁面上，按 [ **下一步**]。  

5.  在 [開始使用]  頁面上，選取 [升級此 Configuration Manager 站台] ，然後按 [下一步] 。  

6.  在 [產品金鑰]  頁面上，按 [下一步] 。  

     如果您先前曾安裝過 Configuration Manager 評估版，即可選取 [安裝此產品的授權版]，然後輸入完整安裝之 Configuration Manager 的產品金鑰，將站台轉換為完整版。  

     從 System Center Configuration Manager 的 1606 版 2016 年 10 月版基準媒體開始，您可以指定軟體保證合約的到期日。 您也可以選擇指定授權合約的「軟體保證到期日」，以方便提醒您該日期。 如果您未在安裝期間輸入這個項目，則稍後可以從 Configuration Manager 主控台予以指定。

     >  [!NOTE]   
     >  Microsoft 不會驗證您輸入的到期日，亦不會將這個日期用於授權驗證。  相反地，您可以將它作為到期日的提醒。 這項功能很實用，因為 Configuration Manager 會定期檢查線上提供的新軟體更新，因此您應該維持最新的軟體保證授權狀態，才能保有使用其他更新的資格。    

     如需詳細資訊，請參閱 [System Center Configuration Manager 的授權與分支](/sccm/core/understand/learn-more-editions)。

7.  在 [Microsoft 軟體授權條款]  頁面上，閱讀並接受授權條款，然後按 [下一步] 。  

8.  在 [必要條件授權]  頁面上，閱讀並接受必要條件軟體的授權條款，然後按 [下一步] 。 安裝程式會在需要時，於網站系統或用戶端上下載並自動安裝軟體。 您必須選取所有核取方塊，才能繼續進入下一頁。  

9. 在 [必要條件下載]  頁面上，指定是否要讓安裝程式從網際網路下載最新版的必要條件可轉散發檔案、語言套件，以及最新的產品更新，或者使用先前下載的檔案，然後按 [下一步] 。 如果您先前使用安裝程式下載程式下載檔案，請選取 [使用先前下載的檔案]  並指定下載資料夾。 如需詳細資訊，請參閱[安裝程式下載程式](/sccm/core/servers/deploy/install/setup-downloader)。

    > [!NOTE]  
    >  當您使用先前下載的檔案時，請確認下載資料夾的路徑內含最新版的檔案。  

10. 在 [伺服器語言選擇]  頁面上，檢視站台目前安裝的語言清單。 選取這個站台可用的其他語言供 Configuration Manager 主控台和報告使用，或清除不想再於這個站台支援的語言，然後按 [下一步]。 預設選取 [英文]，無法移除。  

    > [!IMPORTANT]  
    >  各版本的 Configuration Manager 皆無法使用舊版 Configuration Manager 的語言套件。 若要在您升級的 Configuration Manager 站台啟用語言支援，您必須使用該新版本的語言套件版本。 例如，從 System Center 2012 Configuration Manager 升級至 System Center Configuration Manager 期間，如果下載的必要條件檔案中未含 System Center Configuration Manager 版本的語言套件，則無法安裝該語言的支援檔案。  

11. 在 [用戶端語言選擇]  頁面上，檢視站台目前安裝的語言清單。 選取此站台上可供用戶端電腦使用的其他語言，或清除不想再於此站台支援的語言。 指定是否要針對行動裝置用戶端啟用所有用戶端語言，然後按 [下一步] 。 預設選取 [英文]，無法移除。  

    > [!IMPORTANT]  
    >  各版本的 Configuration Manager 皆無法使用舊版 Configuration Manager 的語言套件。 若要在您升級的 Configuration Manager 站台啟用語言支援，您必須使用該新版本的語言套件版本。 例如，從 System Center 2012 Configuration Manager 升級至 System Center Configuration Manager 期間，如果下載的必要條件檔案中未含 System Center Configuration Manager 版本的語言套件，則無法安裝該語言的支援檔案。  

12. 在 [設定摘要]  頁面上按 [下一步]  執行必要條件檢查工具，以確認站台升級的伺服器整備。  

13. 在 [必要條件安裝檢查]  頁面上，若沒有列出任何問題，請按 [下一步]  升級站台及站台系統角色。 若必要條件檢查工具找出問題，請按一下清單上的某個項目，以了解如何解決問題的詳細資訊。 請先解決清單中具 [錯誤]  狀態的所有項目，再繼續執行安裝程式。 解決問題後，請按一下 [執行檢查]  以重新開始必要條件檢查。 您也可以開啟系統磁碟機根目錄中的 ConfigMgrPrereq.log 檔案，檢閱必要條件檢查工具的結果。 記錄檔可能包含未在使用者介面中顯示的其他資訊。 如需取得安裝的必要條件規則清單與說明，請參閱[必要條件檢查工具](/sccm/core/servers/deploy/install/list-of-prerequisite-checks)。  

安裝程式會在 [升級]  頁面上顯示整體的進度狀態。 安裝程式完成核心網站伺服器與網站系統安裝時，您就可以關閉精靈。 網站設定會繼續在背景中進行。  

#### <a name="to-upgrade-a-secondary-site"></a>升級次要站台  

1.  確認執行安裝程式的系統管理使用者具有以下安全性權限：  

    -   次要站台電腦上的本機系統管理員權限  
    -   父主要站台上的基礎結構系統管理員或系統高權限管理員安全性角色  
    -   次要站台之站台資料庫上的系統管理員 (SA) 權限  
    </br>
2.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

3.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。  

4.  選取您要升級的次要站台，然後在 [首頁]  索引標籤的 [站台]  群組中，按一下 [升級] 。  

5.  按一下 [是]  確認您的決定，並開始升級次要站台。  

次要站台升級的程序會在背景執行。 完成升級後，您可以在 Configuration Manager 主控台中確認狀態。 若要確認狀態，請選取次要站台伺服器，然後在 [首頁]  索引標籤的 [站台]  群組中，按一下 [顯示安裝狀態] 。  

##  <a name="BKMK_PostUpgrade"></a> 執行升級後工作  
將站台升級至新的 Servcie Pack 後，可能必須完成其他工作，才能完成升級或重新設定站台。 這些工作可能包括 Configuration Manager 用戶端或 Configuration Manager 主控台的升級、重新啟用管理點的資料庫複寫，或還原您所使用且在升級 Service Pack 後已不存在之 Configuration Manager 功能的設定。  

**次要站台的已知問題：**  
- **當您升級至 1511 版時：**若要確保次要站台上的用戶端可以從次要站台尋找管理點 (Proxy 管理點)，請手動將管理點新增至也包含次要站台上發佈點的界限群組。  

- **當您升級至 1606 版或更新版本時：**Proxy 管理點會自動新增至包含次要站台上發佈點的界限群組。
