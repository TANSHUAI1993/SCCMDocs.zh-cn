---
title: "1610 版的檢查清單 | System Center Configuration Manager"
description: "了解更新至 System Center Configuration Manager 1610 版之前所採取的動作。"
ms.custom: na
ms.date: 6/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
caps.latest.revision: "7"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 54b243fd33ed13b8ccde48fa5e2525204455d96c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>安裝 System Center Configuration Manager 1610 更新的檢查清單

*適用對象：System Center Configuration Manager (最新分支)*

當您使用 System Center Configuration Manager 的最新分支時，您可以安裝 1610 版的主控台內更新，從 1606 版更新您的階層。 如果您的階層執行 1511、1602 或 1606 版，您可以更新至 1610 版。

若要取得 1610 版的更新，您必須在階層的頂層站台使用服務連接點站台系統角色。 這可以是線上或離線模式。 在您的階層從 Microsoft 下載更新套件之後，您可以在主控台中的 [管理]&gt; [概觀]&gt; [雲端服務]&gt; [更新與服務] 底下找到此套件。

-   當更新列為 [可用] 時，即表示更新已準備好安裝。 安裝 1610 版之前，請檢閱下列有關[安裝更新 1610](#about-installing-update-1610) 的資訊和[檢查清單](#checklist)，以了解開始更新之前應進行的設定。

-   如果更新顯示為 [正在下載] 且未變更，請檢閱 **hman.log** 和 **dmpdownloader.log** 中的錯誤。

    -   通常，您也可以在站台伺服器上重新啟動 **SMS_Executive** 服務，以重新開始下載更新的重新發佈檔案。

    -   另一個常見的下載問題發生於 Proxy 伺服器設定防止來自 <http://silverlight.dlservice.microsoft.com> 和 <http://download.microsoft.com> 的下載時。

如需安裝更新的詳細資訊，請參閱[主控台內更新及服務](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing)。

如需最新分支版本的資訊，請參閱 [System Center Configuration Manager 的更新](/sccm/core/servers/manage/updates)中的[基準和更新版本](/sccm/core/servers/manage/updates#bkmk_Baselines)。

## <a name="about-installing-update-1610"></a>關於安裝更新 1610

**站台：**  
更新 1610 只能安裝在階層的頂層站台。 這表示您從管理中心網站 (如果有的話) 或獨立主要站台起始安裝。 在頂層站台安裝更新之後，子站台會有下列更新行為：

-   當管理中心網站完成安裝更新之後，子主要站台就會自動安裝更新。 您可以使用服務保留時間來控制站台安裝更新的時間。 在 1606 版之前，維護時段稱為維護期間。 如需詳細資訊，請參閱[站台伺服器的服務保留時間](/sccm/core/servers/manage/service-windows)。

-   在主要父站台完成更新安裝後，您必須從 Configuration Manager 主控台內手動更新次要站台。 不支援次要站台伺服器的自動更新。

**站台系統角色︰**  
當站台伺服器安裝更新時，站台伺服器上以及遠端電腦上已安裝的站台系統角色會自動更新。 因此，安裝更新之前，請確定每個站台系統伺服器都符合任何使用新更新版本的新必要條件。

**Configuration Manager 主控台：**   
在完成更新後第一次使用 Configuration Manager 主控台時，系統會提示您更新該主控台。 若要這麼做，您必須在裝載該主控台的電腦上執行 Configuration Manager 安裝程式，並選擇更新主控台的選項。 建議您不要延遲安裝主控台更新。



## <a name="checklist"></a>檢查清單

**確定所有站台都執行支援的 System Center Configuration Manager 版本：**階層中的每個站台必須執行相同的 System Center Configuration Manager 版本 (1511、1602 或 1606 版)，才能開始安裝更新 1610。

**檢閱您的軟體保證或對等訂閱權限的狀態︰**   
您必須擁有使用中的軟體保證 (SA) 協議以安裝更新 1610。 當您安裝 1610 版時，您可以選擇 [授權] 索引標籤確認您的**軟體保證到期日**。

這是您可以指定來方便提醒授權到期日的選用值，安裝未來更新時會顯示此值。 如果您從 1606 版基準媒體安裝 Configuration Manager，先前可能已在安裝期間指定此值，或在 [階層設定] 的 [授權] 索引標籤上安裝站台後指定此值。

如需詳細資訊，請參閱 [System Center Configuration Manager 的授權與分支](/sccm/core/understand/learn-more-editions)。

**檢閱站台系統伺服器上已安裝的 Microsoft .NET 版本：**當站台安裝更新 1610 時，Configuration Manager 會自動在每一部裝載下列其中一個站台系統角色的電腦上安裝 .NET Framework 4.5.2 (當尚未安裝 .NET Framework 4.5 或更新版本時)：

-   註冊 Proxy 點
-   註冊點
-   管理點
-   服務連接點

這項安裝會讓站台系統伺服器處於重新開機擱置中狀態，並將錯誤回報給 Configuration Manager 元件狀態檢視器。 此外，伺服器上的 .NET 應用程式於伺服器重新啟動之前可能遇到隨機失敗。

如需詳細資訊，請參閱 [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) (站台和站台系統必要條件)。

**檢閱站台和階層狀態，並確認沒有任何未解決的問題：** 更新站台之前，請解決站台伺服器、站台資料庫伺服器和安裝在遠端電腦上的站台系統角色的所有操作問題。 網站更新會因為現有的操作問題而失敗。

如需詳細資訊，請參閱 [Use alerts and the status system for System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system)。

**檢閱站台間的檔案和資料複寫︰**   
確認站台之間的檔案和資料庫複寫正在運作且為最新狀態。 延遲或待辦項目可能會造成無法順暢並成功地更新。
針對資料庫複寫，您可以使用「複寫連結分析師」來協助您解決問題，再開始更新。

如需詳細資訊，請參閱[監視 System Center Configuration Manager 的階層及複寫基礎結構](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)中的[關於複寫連結分析師](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)。

**針對裝載站台、站台資料庫伺服器，以及遠端站台系統角色的電腦，安裝所有適用的作業系統重大更新：**安裝 Configuration Manager更新之前，請為每一個適用的站台系統安裝任何重大更新。 如果您安裝的更新需要重新啟動，請先重新啟動適用的電腦再開始進行 Configuration Manager 更新。

**在主要站台上停用管理點的資料庫複本：**   
Configuration Manager 無法成功更新具有已啟用管理點之資料庫複本的主要站台。 請停用資料庫複寫後，再安裝 Configuration Manager 的更新。

如需詳細資訊，請參閱 [System Center Configuration Manager 的管理點資料庫複本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)。

**將 SQL Server AlwaysOn 可用性群組設定為手動容錯移轉：**   
安裝更新之前 (像是 1610 版本)，請確定可用性群組已設為手動容錯移轉。 站台更新之後，您可以還原為自動容錯移轉。 如需詳細資訊，請參閱[站台資料庫的 SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。

**重新設定使用 NLB 的軟體更新點：**   
Configuration Manager 無法更新使用網路負載平衡 (NLB) 叢集來裝載軟體更新點的站台。

如果您將 NLB 叢集用於軟體更新點，請使用 Windows PowerShell 移除 NLB 叢集。
如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃軟體更新](/sccm/sum/plan-design/plan-for-software-updates)。

**停用站台更新安裝期間各站台的所有站台維護工作：**   
在您安裝更新之前，請停用任何可能在進行更新程序期間執行的站台維護工作。 這包括但不限於下列項目：

-   備份網站伺服器
-   刪除過時用戶端操作
-   刪除過時探索資料

於更新安裝期間執行站台資料庫維護工作，更新安裝可能會失敗。 在停用工作前，請將工作的排程記錄下來，以便在安裝更新後還原其設定。

如需詳細資訊，請參閱 [System Center Configuration Manager 的維護工作](/sccm/core/servers/manage/maintenance-tasks)和 [System Center Configuration Manager 的維護工作參考](/sccm/core/servers/manage/reference-for-maintenance-tasks)。

**在管理中心網站和主要站台建立站台資料庫的備份：** 更新站台之前，請備份站台資料庫，以確保您有可供災害復原使用的良好備份。

如需詳細資訊，請參閱 [System Center Configuration Manager 備份和復原](/sccm/protect/understand/backup-and-recovery)。

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a System Center Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.

-   We recommend that you test the site database upgrade process because when you upgrade a site, the site database might be modified.

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see [Step 2: Test the database upgrade before installing an update](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) from **Before you install an in-console update**.
-->

**規劃用戶端試驗：**   
當您安裝更新用戶端的更新時，可以在進入生產階段前先測試新的用戶端更新，再部署並升級所有使用中的用戶端。

若要利用這個選項，在開始安裝更新之前，您必須將您的站台設定為支援進入生產階段前自動升級。

如需詳細資訊，請參閱[在 System Center Configuration Manager 中升級用戶端](/sccm/core/clients/manage/upgrade/upgrade-clients)和[如何測試 System Center Configuration Manager 的進入生產階段前集合用戶端升級](/sccm/core/clients/manage/upgrade/test-client-upgrades)。

**規劃使用服務保留時間來控制站台伺服器安裝更新的時間：**   
您可以使用服務保留時間定義站台伺服器的更新要安裝的時段。

這可協助您控制階層中的站台要於何時安裝更新。 在 1606 版之前，維護時段稱為維護期間。 如需詳細資訊，請參閱[站台伺服器的服務保留時間](/sccm/core/servers/manage/service-windows)。

**執行安裝程式必要條件檢查工具：**   
當更新在主控台中列為 [可用] 時，您可以單獨執行必要條件檢查程式，再安裝更新 (當您在站台上安裝更新時，會再次執行必要條件檢查工具)。

若要從主控台執行必要條件檢查，請前往 [管理] > [概觀] > [雲端服務] > [更新與服務]。 接下來，以滑鼠右鍵按一下 [Configuration Manager 1610 更新套件]，然後選擇 [執行必要條件檢查]。

如需啟動後再監視必要條件檢查的詳細資訊，請參閱[安裝適用於 System Center Configuration Manager 的主控台內更新](/sccm/core/servers/manage/install-in-console-updates)主題中的**步驟 3：安裝更新之前，先執行必要條件檢查工具**。

> [!IMPORTANT]  
> 當必要條件檢查工具獨立執行時，或作為更新安裝的一部分執行時，處理序會更新站台維護作業所使用的部分產品來源檔案。 因此，執行必要條件檢查程式之後與安裝 1610 更新之前，如果您必須執行站台維護工作，請從站台伺服器上的 CD.Latest 資料夾執行 **Setupwpf.exe** (Configuration Manager 安裝程式)。

**更新站台︰**   
您現在已準備好開始安裝階層的更新。 如需安裝更新的資訊，請參閱[安裝主控台內更新](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

建議您規劃在正常上班以外的時間對各個站台安裝更新，在這些時間內安裝更新的程序及其重新安裝站台元件和站台系統角色的動作，對您的商務營運所產生的影響最小。

如需詳細資訊，請參閱 [System Center Configuration Manager 的更新](/sccm/core/servers/manage/updates)。
