---
title: "監視軟體更新 | Microsoft Docs"
description: "System Center Configuration Manager 主控台提供警示與狀態，以監視更新及相容性。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 11/10/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: 956ef263a1c178b5ab5926705859f4b2d0ae5bc7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-software-updates-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中監視軟體更新

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 提供多種方式幫助您監視軟體更新物件、程序和相容性資訊。 您可以使用下列各區段來監視軟體更新。

## <a name="software-updates-dashboard"></a>軟體更新儀表板
從 Configuration Manager 1610 版開始，您可以使用軟體更新儀表板檢視貴組織裝置目前的合規性狀態，並快速分析資料查看哪些裝置有風險。 若要檢視儀表板，請瀏覽至 [監視] > [概觀] > [安全性] > 「Software Updates Dashboard」 (軟體更新儀表板)。   

##  <a name="BKMK_SUAlerts"></a> 軟體更新的警示  
 您可以設定軟體更新的警示，在軟體更新部署的相容性層級低於設定的百分比時通知系統管理使用者。 您可以在下列位置設定軟體更新部署的警示：  

-   ADR 設定：您可以在 [自動部署規則精靈] 和 ADR 內容中設定警示設定。  

-   部署設定：您可以在 [部署軟體更新精靈] 和部署內容中設定警示設定。  

進行警示設定後，如果指定的條件發生，Configuration Manager 就會產生警示。 您可以在下列位置檢閱軟體更新警示：  

1.  在 [軟體程式庫]  工作區的 [軟體更新]  節點中檢閱最近的警示。  

2.  在 [監視]  工作區的 [警示]  節點中管理設定的警示。  

##  <a name="BKMK_SUSyncStatus"></a> 軟體更新同步處理狀態  
 初始化同步處理程序後，您可以從 Configuration Manager 主控台監視階層中所有軟體更新點的同步處理程序。 利用下列程序監視軟體更新同步處理程序。  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>若要監視軟體更新同步處理程序  

- 在 Configuration Manager 主控台中，瀏覽至 [監視] > [概觀] > [軟體更新點同步處理狀態]。  

    Configuration Manager 階層中的軟體更新點會顯示在結果窗格中。 從此檢視中，您可以監視所有軟體更新點的同步處理狀態。 若要查看同步處理程序的詳細資訊，您可以檢閱 wsyncmgr.log 檔案，該檔案位於各站台伺服器的 <Configuration Manager 安裝路徑>\Logs 中。  

##  <a name="BKMK_SUDeployStatus"></a> 軟體更新部署狀態  
 您在軟體更新群組中部署軟體更新或部署個別軟體更新後，可以監視部署狀態。 利用下列程序監視軟體更新群組或軟體更新的部署狀態。  

#### <a name="to-monitor-deployment-status"></a>若要監視部署狀態  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視] > [概觀] > [部署]。  

2.  按一下您要監視其部署狀態的軟體更新群組或軟體更新。  

3.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [檢視狀態] 。  

##  <a name="BKMK_SUReports"></a> 軟體更新報告  
 軟體更新的狀態訊息會提供有關軟體更新相容性，以及有關軟體更新部署的評估和強制執行狀態的資訊。 您可以執行軟體更新報告顯示這些狀態訊息。 有超過 30 種預先定義的軟體更新報告可供您使用。 這些報告分成數種類別，可以用來報告有關軟體更新和部署的特定資訊。 除了使用預先設定的報告之外，您也可以根據企業需要建立自訂軟體更新報告。 如需詳細資訊，請參閱[報告作業和維護](../../core/servers/manage/operations-and-maintenance-for-reporting.md)。  

##  <a name="BKMK_MonitorContent"></a> 監視內容  
 您可以在 Configuration Manager 主控台中監視內容，檢閱與關聯發佈點相關之所有套件類型的狀態。 包括套件中內容的內容驗證狀態、指派至特定發佈點群組的內容狀態、指派至發佈點的內容狀態，以及每個發佈點的選用功能狀態 (內容驗證、PXE 和多點傳送)。  

###  <a name="BKMK_ContentStatus"></a> 內容狀態監視  
 [監視]  工作區中的 [內容狀態]  節點會提供有關內容套件的資訊。 您可以檢閱有關套件的一般資訊、套件的發佈狀態，以及有關套件的詳細狀態資訊。 利用下列程序可檢視內容狀態。  

#### <a name="to-monitor-content-status"></a>若要監視內容狀態  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視] > [概觀] > [發佈狀態] > [內容狀態]。 套件便會顯示。  

2.  選取要檢視其詳細狀態資訊的套件。  

3.  在 [首頁]  索引標籤上，按一下 [檢視狀態] 。 套件的詳細狀態資訊隨即顯示。  

###  <a name="BKMK_DPGroupStatus"></a> 發佈點群組狀態  
 [監視]  工作區中的 [發佈點群組狀態]  節點會提供有關發佈點群組的資訊。 您可以檢閱有關發佈點群組的一般資訊，例如發佈點群組狀態和相容性比率，以及發佈點群組的詳細狀態資訊。 利用下列程序可檢視發佈點群組狀態。  

#### <a name="to-monitor-distribution-point-group-status"></a>若要監視發佈點群組狀態  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視] > [概觀] > [發佈狀態] > [發佈點群組狀態]。 發佈點群組隨即顯示。  

2.  選取要檢視其詳細狀態資訊的發佈點群組。  

3.  在 [首頁]  索引標籤上，按一下 [檢視狀態] 。 發佈點群組的詳細狀態資訊隨即顯示。  

###  <a name="BKMK_DPConfigStatus"></a> 發佈點組態狀態  
 [監視]  工作區中的 [發佈點設定狀態]  節點會提供有關發佈點的資訊。 您可以檢閱已啟用的發佈點屬性，例如 PXE、多點傳送及內容驗證。 您也可以檢視發佈點的詳細狀態資訊。 利用下列程序可檢視發佈點設定狀態。  

#### <a name="to-monitor-distribution-point-configuration-status"></a>若要監視發佈點設定狀態  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視] > [概觀] > [發佈狀態] > [發佈點設定狀態]。 發佈點隨即顯示。  

2.  選取要檢視其發佈點狀態資訊的發佈點。  

3.  在結果窗格中，按一下 [詳細資料]  索引標籤。 發佈點的狀態資訊隨即顯示。  
