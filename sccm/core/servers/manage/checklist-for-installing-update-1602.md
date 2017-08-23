---
title: "1602 版的檢查清單 | Microsoft Docs"
description: "了解從 System Center Configuration Manager 1511 版更新至 1602 版之前所採取的動作。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
caps.latest.revision: "13"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 3e0de56b7a592b105e6a61b3d6654b1d0142584d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="checklist-for-installing-update-1602-for-system-center-configuration-manager"></a>安裝 System Center Configuration Manager 1602 更新的檢查清單

*適用對象：System Center Configuration Manager (最新分支)*

從 System Center Configuration Manager 1511 版更新至 1602 版之前，請檢閱下列資訊和檢查清單，以了解開始更新之前應採取的動作。  

 **關於安裝更新 1602：**  

 更新 1602 只能安裝在階層的頂層站台。 這表示您從管理中心網站 (如果有的話) 或獨立主要站台起始安裝。  

-   管理中心網站完成安裝更新之後，子主要站台會自動安裝更新。 站台安裝更新時，您可以使用維護時段來控制。 自 1602 更新發行開始，維護時段已重新命名為「服務保留時間」。 如需詳細資訊，請參閱[站台伺服器的服務保留時間](/sccm/core/servers/manage/service-windows)。  

-   在主要父站台完成安裝更新後，您必須從 Configuration Manager 主控台內手動更新次要站台。 不支援自動更新次要站台伺服器。  

當站台伺服器安裝更新時，站台伺服器上以及遠端電腦上已安裝的站台系統角色會自動更新。 因此，安裝更新之前，請確定每個站台系統伺服器都符合任何使用新更新版本的新必要條件。  

在完成更新後第一次使用 Configuration Manager 主控台時，系統會提示您更新該主控台。 若要這麼做，您必須在裝載該主控台的電腦上執行 Configuration Manager 安裝程式，並選擇更新主控台的選項。 建議您不要延遲安裝主控台更新。  

 **檢查清單：**  

 **確定所有站台都執行支援的 System Center Configuration Manager 版本：**階層中的每個站台伺服器必須執行 System Center Configuration Manager 1511 版，才能開始安裝更新 1602。  

 **檢閱站台系統伺服器上安裝的 Microsoft .NET 版本：**當站台安裝更新 1602 時，Configuration Manager 會自動在每一部裝載下列其中一個站台系統角色的電腦上安裝 .NET Framework 4.5.2 (如果尚未安裝 .NET Framework 4.5 或更新版本)：  

-   註冊 Proxy 點  

-   註冊點  

-   管理點  

-   服務連接點  

此安裝會讓站台系統伺服器處於重新開機擱置中狀態，並回報錯誤給 Configuration Manager 元件狀態檢視器。 此外，伺服器上的 .NET 應用程式於伺服器重新啟動之前可能遇到隨機失敗。  

 如需詳細資訊，請參閱 [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (站台和站台系統必要條件)。  

 **檢閱站台和階層狀態，並確認沒有任何未解決的問題：** 更新站台之前，請解決站台伺服器、站台資料庫伺服器和安裝在遠端電腦上的站台系統角色的所有操作問題。 網站更新會因為現有的操作問題而失敗。  

如需詳細資訊，請參閱 [使用 System Center Configuration Manager 的警示和狀態系統](../../../core/servers/manage/use-alerts-and-the-status-system.md)。  

 **檢閱站台間的檔案和資料複寫：**  確認站台之間的檔案和資料庫複寫正在運作且為最新狀態。 延遲或待辦項目可能會造成無法順暢並成功地更新。    

針對資料庫複寫，您可以使用「複寫連結分析師」來協助您解決問題，再開始更新。    

 如需詳細資訊，請參閱[監視 System Center Configuration Manager 的階層及複寫基礎結構](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md)主題中的[關於複寫連結分析師](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA)。  

 **針對裝載站台、站台資料庫伺服器，以及遠端站台系統角色的電腦，安裝所有適用的作業系統重大更新：**安裝 Configuration Manager更新之前，請為每一個適用的站台系統安裝任何重大更新。 如果您安裝的更新需要重新啟動，請先重新啟動適用的電腦再開始進行更新。  

 **停用主要站台的管理點資料庫複本：**如果主要站台已啟用管理點資料庫複本，Configuration Manager 即無法成功更新此主要站台。 在下列情況之前先停用資料庫複寫：  

-   建立站台資料庫的備份以測試資料庫升級。  

-   安裝 Configuration Manager 的更新。  

如需詳細資訊，請參閱 [System Center Configuration Manager 的管理點資料庫複本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

 **重新設定使用 NLB 的軟體更新點：**如果站台是使用網路負載平衡 (NLB) 叢集來裝載軟體更新點，Configuration Manager 即無法更新此站台。  如果您將 NLB 叢集用於軟體更新點，請使用 Windows PowerShell 移除 NLB 叢集。    

 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md)。  

 **於站台安裝更新期間停用各站台的所有站台維護工作：**在您安裝更新之前，請停用任何可能在進行更新程序期間執行的站台維護工作。 這些工作包括 (但不限於) 以下幾項：  

-   備份網站伺服器  

-   刪除過時用戶端操作  

-   刪除過時探索資料  

於更新安裝期間執行站台資料庫維護工作，更新安裝可能會失敗。 在停用工作前，請將工作的排程記錄下來，以便在安裝更新後您可以還原其設定。  

 如需詳細資訊，請參閱 [System Center Configuration Manager 的維護工作](../../../core/servers/manage/maintenance-tasks.md)和 [System Center Configuration Manager 的維護工作參考](../../../core/servers/manage/reference-for-maintenance-tasks.md)。  

 **在管理中心網站和主要站台建立站台資料庫的備份：** 更新站台之前，請備份站台資料庫，以確保您有可供災害復原使用的良好備份。   

如需詳細資訊，請參閱 [System Center Configuration Manager 備份和復原](../../../protect/understand/backup-and-recovery.md)。  

 **備份自訂的 Configuration.mof 檔案：** 如果您使用自訂的 Configuration.mof 檔案來定義搭配硬體清查使用的資料類別，請先建立此檔案的備份，再更新站台。 更新之後，請將這個檔案還原到 1602 版站台。 更新站台時，原始 (預設值) 版本的檔案會覆寫目前的檔案。 如需使用此檔案的詳細資訊，請參閱 [How to extend hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md) (如何擴充 System Center Configuration Manager 中的硬體清查)。  

 **在最新的站台資料庫備份複本上測試資料庫升級：**在更新 System Center Configuration Manager 管理中心網站或主要站台之前，請在站台資料庫複本上測試站台資料庫升級程序。  

-   您應該測試站台資料庫升級程序，因為當您升級站台時，站台資料庫可能會經過修改。  

-   測試資料庫升級並非必要，但是可以在您的生產資料庫受到影響之前找出升級問題。  

-   網站資料庫升級失敗可能會造成網站資料庫無法運作，且可能需要網站復原才能恢復功能。  

-   雖然網站資料庫在階層中的網站之間共用，您仍需要在升級該網站之前先規劃每個適用網站上的資料庫測試。  

-   如果您在主要網站上使用管理點的資料庫複本，請在建立網站資料庫的備份之前停用複寫。  

Configuration Manager 不支援次要站台的備份，也不支援次要站台資料庫的測試升級。   
請勿在生產網站資料庫上執行測試資料庫升級。 在站台資料庫上進行這類更新可能會造成站台無法運作。 如需詳細資訊，請參閱＜安裝主控台內更新之前＞中的[步驟 2︰安裝更新之前，先測試資料庫升級](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2)。  

 **規劃試驗的用戶端︰**當您安裝更新用戶端的更新時，可以在進入生產階段前先測試新的用戶端更新，再部署並升級所有使用中的用戶端。   

 若要利用這個選項，在開始安裝更新之前，您必須將您的站台設定為支援進入生產階段前自動升級。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中升級用戶端](../../../core/clients/manage/upgrade/upgrade-clients.md)和   
[如何測試 System Center Configuration Manager 的進入生產階段前集合用戶端升級](../../../core/clients/manage/upgrade/test-client-upgrades.md)。  

 **規劃使用維護時段來控制站台伺服器安裝更新的時機：**您可以使用維護時段定義站台伺服器的更新要安裝的時段。 這可協助您控制階層中的站台要於何時安裝更新。   

自 1602 更新發行開始，維護時段已重新命名為「服務保留時間」。 如需詳細資訊，請參閱[站台伺服器的服務保留時間](/sccm/core/servers/manage/service-windows)。  

 **執行安裝程式必要條件檢查工具：**安裝更新 1602 之前，您可以在更新安裝程序之外獨立執行必要條件檢查工具。 當您在站台上安裝更新時，會再次執行必要條件檢查工具。  

如需詳細資訊，請參閱 [System Center Configuration Manager 的更新](../../../core/servers/manage/updates.md)主題中的**步驟 3：安裝更新之前執行必要條件檢查工具**。  

> [!IMPORTANT]  
>  當必要條件檢查工具獨立執行時，或作為更新安裝的一部分執行時，處理序會更新站台維護作業所使用的部分產品來源檔案。 因此，在執行必要條件檢查程式之後、安裝 1602 更新之前，如果您必須執行站台維護工作，請從站台伺服器上的 CD.Latest 資料夾執行 **Setupwfe.exe** (Configuration Manager 安裝程式)。  

 **更新站台：** 您現在已準備好開始安裝階層的更新。 建議您規劃在正常上班以外的時間對各個站台安裝更新，在這些時間內安裝更新的程序及其重新安裝站台元件和站台系統角色的動作，對您的商務營運所產生的影響最小。

如需詳細資訊，請參閱 [System Center Configuration Manager 的更新](../../../core/servers/manage/updates.md)。  

## <a name="see-also"></a>請參閱  
 [System Center Configuration Manager 的更新](../../../core/servers/manage/updates.md)
