---
title: "管理軟體更新同步處理 | Microsoft Docs"
description: "使用下列步驟，以排程軟體更新同步處理、手動啟動軟體更新同步處理，以及監視軟體更新同步處理。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
ms.openlocfilehash: e68170a16a6a908e035247ed9c0f3cc6cdbe1983
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_SUMSync"></a> 同步處理軟體更新

適用於：System Center Configuration Manager (最新分支)

 Configuration Manager 中的軟體更新同步處理是擷取符合您所設定準則的軟體更新中繼資料的程序。 這包含特定產品、分類和語言。 一般而言，管理中心網站或獨立主要站台上的軟體更新點，會從 Microsoft Update 擷取中繼資料。 接著，頂層站台會將同步處理要求傳送至其他站台。 當站台接收到來自父站台的同步處理要求時，站台的軟體更新點會從其上游[同步處理來源](../plan-design/plan-for-software-updates.md#BKMK_SyncSource)擷取軟體更新中繼資料。 如需軟體更新同步處理程序的詳細資訊，請參閱[軟體更新同步處理](../understand/software-updates-introduction.md#BKMK_Synchronization)。

您可以在頂層站台上將軟體更新同步處理設定成根據軟體更新點內容的排程來執行。 在您設定同步處理排程後，通常在一般操作中不會再變更排程。 不過，必要時您可以手動起始軟體更新同步處理。

  > [!NOTE]  
  >  軟體更新點必須連線到它們的上游同步處理來源，以同步處理軟體更新。 當軟體更新點與其上游同步處理來源中斷連線時，您可以使用匯出和匯入方法來同步處理軟體更新。 如需詳細資訊，請參閱[從已中斷連線的軟體更新點同步處理軟體更新](synchronize-software-updates-disconnected.md)。  

## <a name="schedule-software-updates-synchronization"></a>排程軟體更新同步處理
當您設定軟體更新同步處理的排程時，頂層軟體更新點會在排程的日期和時間與 Microsoft Update 開始同步處理。 自訂排程則可讓您在 WSUS 伺服器、站台伺服器和網路的需求量較低的日期和時間同步處理軟體更新。 例如，您可以設定排程，以在每週凌晨 2:00 同步處理軟體更新。 在排程的同步處理期間，會將從上一次排程同步處理以來對所有軟體更新中繼資料所做的變更，插入站台資料庫中。 這包括新的軟體更新中繼資料，或已修改、移除或現已到期的中繼資料。

在頂層站台使用下列程序，排程軟體更新同步處理。  

#### <a name="to-schedule-software-updates-synchronization"></a>若要排程軟體更新同步處理  

  1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

  2.  在 [系統管理] 工作區中，展開 [站台設定] ，然後按一下 [站台] 。  

  3.  在結果窗格中，按一下管理中心網站或獨立主要網站。  

  4.  在 [首頁]  索引標籤的 [設定]  群組中，展開 [設定網站元件] ，然後按一下 [軟體更新點] 。  

  5.  在 [軟體更新點元件內容] 對話方塊中，選取 [啟用依排程同步處理] ，然後指定同步處理排程。  

## <a name="manually-start-software-updates-synchronization"></a>手動啟動軟體更新同步處理
您可以在頂層站台的 Configuration Manager 主控台中，從 [軟體程式庫] 工作區的 [所有軟體更新] 節點手動起始軟體更新同步處理。  

在頂層站台使用下列程序，手動起始軟體更新同步處理。  

#### <a name="to-manually-start-software-updates-synchronization"></a>手動啟動軟體更新同步處理  

  1.  在與管理中心網站或獨立主要站台連線的 Configuration Manager 主控台中，按一下 [軟體程式庫]。  

  2.  在 [軟體程式庫] 工作區中，展開 [軟體更新]  ，並按一下 [所有軟體更新]  或 [軟體更新群組] 。  

  3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [同步處理軟體更新] 。 在對話方塊中按一下 [是]  ，確認您想要起始同步處理程序。  

   在軟體更新點上起始同步處理程序後，您可以從階層中所有軟體更新點的 Configuration Manager 主控台監視同步處理程序。 利用下列程序監視軟體更新同步處理程序。  


## <a name="monitor-software-updates-synchronization"></a>監視軟體更新同步處理
在您起始同步處理程序之後，就可以使用 Configuration Manager 主控台監視階層中所有軟體更新點的程序。 利用下列程序監視軟體更新同步處理程序。 如需監視軟體更新 (包括同步處理程序) 的詳細資訊，請參閱[監視軟體更新](../deploy-use/monitor-software-updates.md)。

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>若要監視軟體更新同步處理程序  

  1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

  2.  在 [監視]  工作區中，按一下 [軟體更新點同步處理狀態] 。  

    Configuration Manager 階層中的軟體更新點會顯示在結果窗格中。 從此檢視中，您可以監視所有軟體更新點的同步處理狀態。 當您需要更多同步處理程序的詳細資訊時，您可以檢閱每一部站台伺服器上位於 <Configuration Manager 安裝路徑>\Logs 的 wsyncmgr.log 檔案。  

## <a name="next-steps"></a>後續步驟
在您第一次同步處理軟體更新之後，或有新的分類或產品可用之後，必須[設定新的分類和產品](configure-classifications-and-products.md)，使用新的準則來同步處理軟體更新。

使用您需要的準則同步處理軟體更新之後，請[管理軟體更新的設定](manage-settings-for-software-updates.md)。  
