---
title: "維護工作的參考 | Microsoft Docs"
description: "請詳讀每個 System Center Configuration Manager 站台維護工作的詳細資料，並了解預設是否會啟用這些工作。"
ms.custom: na
ms.date: 3/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
caps.latest.revision: "16"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a2d4420c2274a9b1ceb47ffd267849fdb5a55a61
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="reference-for-maintenance-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager 的維護工作參考

*適用對象：System Center Configuration Manager (最新分支)*

本主題列出每個 System Center Configuration Manager 站台維護工作的詳細資料，以及指定哪些站台類型提供這些工作。 每個項目也會指出工作是否為啟用，還是預設為未啟用。 如需規劃及設定站台以執行維護工作的資訊，請參閱 [System Center Configuration Manager 的維護工作](../../../core/servers/manage/maintenance-tasks.md)。  

**備份站台伺服器**︰使用此工作準備重要資料的復原。 您可以建立重要資訊的備份，以還原站台及 Configuration Manager 資料庫。 如需詳細資訊，請參閱 [System Center Configuration Manager 備份和復原](../../../protect/understand/backup-and-recovery.md)。  

-   **管理中心網站** - 已啟用    
-   **主要站台** - 未啟用    
-   次要站台：無法使用  

**使用清查資訊檢查應用程式標題**：使用此工作可維護軟體清查中所報告之軟體標題與 Asset Intelligence 類別目錄中的軟體標題之間的一致性。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的 Asset Intelligence 簡介](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**清除安裝旗標**：使用此工作可針對未在 **用戶端重新探索** 期間提交「活動訊號探索」記錄的用戶端，移除已安裝旗標。 已安裝旗標可避免在已具備作用中 Configuration Manager 用戶端的電腦上進行自動用戶端推入安裝。  

-   管理中心網站：無法使用    
-   **主要站台**：未啟用    
-   次要站台：無法使用  

**刪除過時應用程式要求資料**：使用此工作可從資料庫中，刪除過時的應用程式要求。 如需應用程式要求的詳細資訊，請參閱[使用 System Center Configuration Manager 建立和部署應用程式](/sccm/apps/get-started/create-and-deploy-an-application)。  

-   管理中心網站：無法使用
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時用戶端下載歷程記錄**：使用此工作可刪除有關用戶端所使用下載來源的歷史資料。 下載來源資訊會用來填入[用戶端資料來源儀表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。  
-  管理中心網站 - 無法使用
-    **主要站台** - 已啟用
-  次要站台 - 無法使用

**刪除過時用戶端操作**：使用此工作可從站台資料庫中，刪除過時的用戶端操作資料。 比方說，這包括過時或過期的用戶端通知資料 (例如電腦或使用者原則的下載要求)，以及 Endpoint Protection 資料 (例如系統管理使用者要讓用戶端執行掃描或下載更新定義的要求)。

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時用戶端顯示狀態歷程記錄**：使用此工作可刪除比指定時間舊的用戶端線上狀態相關歷程記錄資訊 (由用戶端通知所記錄)。 如需用戶端通知的詳細資訊，請參閱[如何在 System Center Configuration Manager 中監視用戶端](../../../core/clients/manage/monitor-clients.md)。  

-   **管理中心網站** - 已啟用   
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時的雲端管理閘道流量資料**：使用此工作可從站台資料庫中，刪除所有通過[雲端管理閘道](/sccm/core/clients/manage/plan-cloud-management-gateway)，且與過時資料相關的流量。 例如，其中包含有關要求數量、總要求位元組、總回應位元組、失敗的要求數量，以及目前要求的最大數量。  
- **管理中心網站** - 已啟用
- **主要站台** - 已啟用
- 次要站台 - 無法使用


**刪除過時收集檔案**：使用此工作可從資料庫中，刪除已收集檔案的相關過時資訊。 此工作也會從選定網站的網站伺服器資料夾結構中刪除收集檔案。 根據預設，會將 5 個收集檔案的最新複本儲存在 **Inboxes\sinv.box\FileCol** 目錄的網站伺服器上。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的軟體清查簡介](/sccm/core/clients/manage/inventory/introduction-to-software-inventory)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時電腦關聯資料**：使用此工作可從資料庫中，刪除過時的「作業系統部署」電腦關聯資料。 此資訊用來作為完成使用者狀態還原的一部分。 如需電腦關聯的詳細資訊，請參閱[在 System Center Configuration Manager 中管理使用者狀態](../../../osd/get-started/manage-user-state.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時刪除偵測資料**：使用此工作可從資料庫中，刪除由「擷取檢視」建立的過時資料。 預設會停用擷取檢視。 您可利用 Configuration Manager SDK 加以啟用。 除非啟用 Extraction Views，否則此工作就沒有可刪除的資料。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時裝置抹除記錄**：使用此工作可從資料庫中，刪除過時的行動裝置抹除動作相關資料。 如需抹除行動裝置的詳細資訊，請參閱 [使用 System Center Configuration Manager 透過遠端抹除、鎖定或密碼重設來協助保護資料](/sccm/mdm/deploy-use/wipe-lock-reset-devices)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除受 Exchange Server 連接器管理的過時裝置**：使用此工作可刪除透過 Exchange Server 連接器來管理之行動裝置的相關過時資料。 此資料會根據 Exchange Server 連接器內容之 [探索] 索引標籤上的 [略過未使用達指定天數以上的行動裝置] 選項所設定的間隔時間進行刪除。 如需詳細資訊，請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

-   管理中心網站：無法使用   
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時探索資料**：使用此工作可從資料庫中，刪除過時的探索資料。 此資料包括經由活動訊號探索、網路探索與 Active Directory Domain Services 探索方式 (系統、使用者與群組) 所得到的記錄。 在某個站台執行這項工作時，會刪除與該站台關聯的資料，並且這些變更會複寫到其他站台。 如需探索的詳細資訊，請參閱 [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時發佈點使用量資料**：使用此工作可從資料庫中，刪除儲存時間超過指定時間的過時發佈點資料。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時 Endpoint Protection 健康情況狀態歷程記錄資料**：使用此工作可從資料庫中，刪除過時的 Endpoint Protection 狀態資訊。 如需 Endpoint Protection 狀態資訊的詳細資訊，請參閱[如何監視 System Center Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除已註冊但過時的裝置**︰從 1602 的更新開始，預設會停用此工作。 您可以使用這項工作，從站台資料庫刪除有一段指定時間尚未對站台回報任何資訊的行動裝置有關的過時資料。

此工作適用於由 Microsoft Intune (混合式) 註冊的裝置，或已使用 Configuration Manager 內部部署行動裝置管理功能的裝置。 如需由 Configuration Manager 或 Intune 註冊的裝置作業系統資訊，請參閱 [Supported operating systems for clients and devices for System Center Configuration Manager](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) (System Center Configuration Manager 支援的用戶端和裝置作業系統) 中的[由 Microsoft Intune 註冊的行動裝置](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mobile-devices-enrolled-by-microsoft-intune)一節。

-   管理中心網站：無法使用    
-   **主要站台**：未啟用    
-   次要站台：無法使用  

**刪除過時清查歷程記錄**：使用此工作可從資料庫中，刪除儲存時間超過指定時間的清查資料。 如需清查歷程記錄的資訊，請參閱[如何使用資源總管檢視 System Center Configuration Manager 中的硬體清查](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時記錄檔資料**使用此工作可從資料庫中，刪除用來進行疑難排解的過時記錄檔資料。 此一資料與 Configuration Manager 元件運作無關。  

> [!IMPORTANT]  
> 根據預設，此一工作會在每個網站上每日執行。 在管理中心網站與主要網站上，這個工作會刪除超過 30 天的資料。 在次要網站上使用 SQL Server Express 時，請確保這個工作每日執行，並刪除 7 天未使用的資料。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   **次要站台**：已啟用  

**刪除過時通知工作歷程記錄**：使用此工作可從站台資料庫中，刪除已達一段指定時間未更新的用戶端通知工作資訊。 如需用戶端通知的詳細資訊，請參閱 [Client deployment tasks for System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時複寫摘要資料**：使用此工作可從站台資料庫中，刪除已達一段指定時間未更新的過時複寫摘要資料。 如需詳細資訊，請參閱 [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) 主題中的 [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) 一節。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   **次要站台**：已啟用  

**刪除過時的密碼記錄**：在您階層的頂層網站使用此工作，可刪除 Android 和 Windows Phone 裝置之「密碼重設」的資料。 「密碼重設」資料會經過加密，但不會包含裝置的 PIN 碼。 預設會啟用此工作並刪除超過 1 天的資料。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時複寫追蹤資料**：使用此工作可從資料庫中，刪除 Configuration Manager 站台之間資料庫複寫的過時資料。 變更這項維護工作的設定時，設定會套用到階層中的每個可應用網站。 如需詳細資訊，請參閱 [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) 主題中的 [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) 一節。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   **次要站台**：已啟用  

**刪除過時軟體計量資料**：使用此工作可從資料庫中，刪除儲存時間超過指定時間的過時軟體計量資料。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的軟體計量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時軟體計量摘要資料**：使用此工作可從資料庫中，刪除儲存時間超過指定時間的過時軟體計量摘要資料。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的軟體計量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時狀態訊息**：使用此工作可依據狀態篩選規則設定，從資料庫刪除過時的狀態訊息資料。 如需詳細資訊，請參閱[使用 System Center Configuration Manager 的警示和狀態系統](../../../core/servers/manage/use-alerts-and-the-status-system.md)主題中的＜監視 Configuration Manager 的狀態系統＞一節。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時威脅資料**：使用此工作可從資料庫中，刪除儲存時間超過指定時間的過時 Endpoint Protection 威脅資料。 如需 Endpoint Protection 的資訊，請參閱 [System Center Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時的未知電腦** - 使用此工作可從站台資料庫中，刪除已達一段指定時間未更新的未知電腦資訊。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的未知電腦部署準備](../../../osd/get-started/prepare-for-unknown-computer-deployments.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時使用者裝置親和性資料**：使用此工作可從資料庫中，刪除過時的「使用者裝置親和性」資料。 如需詳細資訊，請參閱 [System Center Configuration Manager 的連結使用者和裝置與使用者裝置親和性](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過期的 MDM 大量註冊套件記錄**：使用此工作，在註冊憑證過期後刪除舊的大量註冊憑證及對應的設定檔。 如需詳細資訊，請參閱[建立憑證設定檔](/sccm/protect/deploy-use/create-certificate-profiles)。
-   **管理中心網站**：已啟用
-   **主要站台**：已啟用
-   次要站台：無法使用

**刪除非使用中用戶端探索資料**：使用此工作可從資料庫中，刪除非使用中用戶端的探索資料。 用戶端標記為已過時，且針對用戶端進行此設定時，就會將用戶端標記為非使用中。

此工作僅會在 Configuration Manager 用戶端資源上運作。 這與刪除任何過時探索資料記錄的**刪除過時探索資料**工作不同。 在某個網站上執行此工作時，會從階層內所有網站的資料庫內移除資料。 如需詳細資訊，請參閱 [How to configure client status in System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md)。  

> [!IMPORTANT]  
> 啟用此工作時，請設定此工作以大於 [活動訊號探索] 排程的間隔執行。 這會啟用使用中用戶端傳送活動訊號探索記錄，將用戶端記錄標記為使用中，此工作就不會將其刪除。  

-   管理中心網站：無法使用    
-   **主要站台**：未啟用    
-   次要站台：無法使用  

**刪除過時警示**：使用此工作可從資料庫中，刪除儲存時間超過指定時間的過期警示。 如需詳細資訊，請參閱 [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md)。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除過時用戶端探索資料**：使用此工作可從資料庫中，刪除過時用戶端記錄。 標記為過時的記錄通常會由相同用戶端較新的記錄來取代。 新的記錄就會成為用戶端目前的記錄。 如需探索的詳細資訊，請參閱 [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md)。  

> [!IMPORTANT]  
> 啟用此工作時，請將此工作的間隔執行設定為超過活動訊號探索的排程。 這會啟用用戶端傳送正確設定過時狀態的活動訊號探索記錄。  

-   管理中心網站：無法使用    
-   **主要站台**：未啟用    
-   次要站台：無法使用  

**刪除過時樹系探索站台和子網路**：使用此工作可刪除過去 30 天內，Active Directory 樹系探索方法未探索出的 Active Directory 站台、子網路及網域的相關資料。 這會移除探索資料，但不會影響此探索資料建立的界限。 如需詳細資訊，請參閱 [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md)。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**刪除孤立的用戶端部署狀態記錄**：使用此工作可定期清除包含用戶端部署狀態資訊的資料表。 此工作可清理有關已淘汰或已退役裝置的記錄。  
-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   次要站台：無法使用

**刪除未使用的應用程式修訂**：使用此工作可刪除已不再參考的應用程式修訂。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中修改和取代應用程式](../../../apps/deploy-use/revise-and-supersede-applications.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**評估集合成員**：您可以將「集合成員資格評估」設定為站台元件。 如需網站元件的資訊，請參閱 [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**監視索引鍵**：使用此工作可監視 Configuration Manager 資料庫主索引鍵的完整性。 主索引鍵是一個資料行 (或多重資料行的組合)，可找出唯一個資料列以及區分該資料列與 Microsoft SQL Server 資料庫資表中的其他列。  

-   **管理中心網站** - 已啟用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**重建索引**：使用此工作可重建 Configuration Manager 資料庫索引。 索引是建立在資料庫表上以加速資料擷取的資料庫結構。 例如，搜尋索引欄通常會比搜尋未索引的欄還快。

為了改善效能，系統會經常更新 Configuration Manager 資料庫索引，以與儲存在資料庫內經常變更的資料同步。 此工作會在至少 50％ 專屬的資料庫欄上建立索引，捨棄少於 50％ 專屬的欄上索引，並且重建所有符合資料專屬性標準的現有索引。  

-   **管理中心網站**：未啟用    
-   **主要站台**：未啟用    
-   **次要站台**：未啟用  

**摘述已安裝的軟體資料**：使用此工作可將來自多筆記錄的已安裝軟體資料摘述成一筆一般記錄。 資料摘要可以壓縮儲存在 Configuration Manager 資料庫中的資料量。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的軟體清查簡介](../../clients/manage/inventory\introduction-to-software-inventory.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**摘述軟體計量檔案使用資料**：使用此工作可將多筆軟體計量檔案使用記錄的資料摘述成一筆一般記錄。 資料摘要可以壓縮儲存在 Configuration Manager 資料庫中的資料量。

您可以搭配使用**摘述軟體計量每月使用資料**工作與本工作，以摘述軟體計量資料，並節省 Configuration Manager 資料庫的磁碟空間。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的軟體計量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**摘述軟體計量每月使用資料**：使用此工作可將多筆軟體計量每月使用記錄的資料摘述成一筆一般記錄。 資料摘要可以壓縮儲存在 Configuration Manager 資料庫中的資料量。

您可以搭配使用**摘述軟體計量檔案使用資料**工作與本工作，以摘述軟體計量資料，並節省 Configuration Manager 資料庫的空間。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的軟體計量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**更新應用程式可用目標**：使用此工作可讓 Configuration Manager 依據集合中的資源，重新計算原則與應用程式部署的對應。 當您將原則或應用程式部署到集合時，Configuration Manager 會在您部署的物件與集合成員之間建立初始對應。

這些對應會儲存在資料表中以供快速參考。 當集合成員資格變更時，這些預存的對應會更新以反映這些變更。 但這些對應有可能會變得不同步。 例如，如果站台無法正確地處理通知檔案，該項變更可能就不會反映在對對應所做的變更中。 此工作會根據目前的集合成員資格來重新整理該對應。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  

**更新應用程式類別目錄資料表**：使用此工作，可同步處理應用程式類別目錄網站資料庫快取與最新的應用程式資訊。 變更這項維護工作的設定時，設定會套用到階層中的所有主要網站。  

-   管理中心網站：無法使用    
-   **主要站台**：已啟用    
-   次要站台：無法使用  
