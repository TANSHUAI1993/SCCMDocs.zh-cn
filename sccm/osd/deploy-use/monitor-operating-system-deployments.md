---
title: "監視作業系統部署 | Microsoft Docs"
description: "Configuration Manager 主控台提供警示、報告和各種狀態指標，協助您監視作業系統部署物件。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 154c0a286e6b9ccedc7545eb010967ac00d35407
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-operating-system-deployments-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中監視作業系統部署

*適用於：System Center Configuration Manager (最新分支)*

Configuration Manager 主控台提供下列方式協助您監視作業系統部署物件。  


##  <a name="BKMK_OSDAlerts"></a> 作業系統部署警示  
 您可以在工作順序部署設定中設定警示，在部署的相容性層級低於設定的百分比時通知系統管理使用者。  

 進行警示設定後，如果指定的條件發生，Configuration Manager 就會產生警示。 您可以在下列位置檢閱工作順序部署警示：  

1.  在 [軟體程式庫]  工作區的 [作業系統]  節點中檢閱最近的警示。  

2.  在 [監視]  工作區的 [警示]  節點中管理設定的警示。  

##  <a name="BKMK_TSDeployStatus"></a> 工作順序部署狀態  
 部署工作順序之後，您可以監視部署狀態。 使用下列程序監視工作順序的部署狀態。  

#### <a name="to-monitor-deployment-status"></a>若要監視部署狀態  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視] 工作區中，按一下 [部署] 。  

3.  按一下要監視部署狀態的工作順序。  

4.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [檢視狀態] 。  

##  <a name="BKMK_TSReports"></a> 作業系統部署報告  
 有許多預先定義的作業系統部署報告可供使用。 這些報告分成數種類別，可用以報告有關狀態移轉和工作順序部署的特定資訊。 除了使用預先設定的報告之外，您也可以根據企業需要建立自訂軟體更新報告。 如需詳細資訊，請參閱[報告作業和維護](../../core/servers/manage/operations-and-maintenance-for-reporting.md)。  

##  <a name="BKMK_MonitorContent"></a> 監視內容  
 您可以在 Configuration Manager 主控台中監視內容，檢閱與關聯發佈點相關之所有套件類型的狀態。 包括套件中內容的內容驗證狀態、指派至特定發佈點群組的內容狀態、指派至發佈點的內容狀態，以及每個發佈點的選用功能狀態 (內容驗證、PXE 和多點傳送)。  

###  <a name="BKMK_ContentStatus"></a> 內容狀態監視  
 [監視]  工作區中的 [內容狀態]  節點會提供有關內容套件的資訊。 您可以檢閱有關套件的一般資訊、套件的發佈狀態，以及有關套件的詳細狀態資訊。 利用下列程序可檢視內容狀態。  

#### <a name="to-monitor-content-status"></a>若要監視內容狀態  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視] 工作區中，展開 [發佈狀態] ，然後按一下 [內容狀態] 。 套件便會顯示。  

3.  選取要檢視其詳細狀態資訊的套件。  

4.  在 [首頁]  索引標籤上，按一下 [檢視狀態] 。 套件的詳細狀態資訊隨即顯示。  

###  <a name="BKMK_DPGroupStatus"></a> 發佈點群組狀態  
 [監視]  工作區中的 [發佈點群組狀態]  節點會提供有關發佈點群組的資訊。 您可以檢閱有關發佈點群組的一般資訊，例如發佈點群組狀態和相容性比率，以及發佈點群組的詳細狀態資訊。 利用下列程序可檢視發佈點群組狀態。  

#### <a name="to-monitor-distribution-point-group-status"></a>若要監視發佈點群組狀態  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視] 工作區中，展開 [發佈狀態] ，然後按一下 [發佈點群組狀態] 。 發佈點群組隨即顯示。  

3.  選取要檢視其詳細狀態資訊的發佈點群組。  

4.  在 [首頁]  索引標籤上，按一下 [檢視狀態] 。 發佈點群組的詳細狀態資訊隨即顯示。  

###  <a name="BKMK_DPConfigStatus"></a> 發佈點組態狀態  
 [監視]  工作區中的 [發佈點設定狀態]  節點會提供有關發佈點的資訊。 您可以檢閱已啟用的發佈點屬性，例如 PXE、多點傳送及內容驗證。 您也可以檢視發佈點的詳細狀態資訊。 利用下列程序可檢視發佈點設定狀態。  

#### <a name="to-monitor-distribution-point-configuration-status"></a>若要監視發佈點設定狀態  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視] 工作區中，展開 [發佈狀態] ，然後按一下 [發佈點設定狀態] 。 發佈點隨即顯示。  

3.  選取要檢視其發佈點狀態資訊的發佈點。  

4.  在結果窗格中，按一下 [詳細資料]  索引標籤。 發佈點的狀態資訊隨即顯示。  
