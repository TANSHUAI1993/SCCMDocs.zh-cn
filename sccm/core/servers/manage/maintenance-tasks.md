---
title: "維護工作 | Microsoft Docs"
description: "了解要針對 Configuration Manager 站台和階層執行哪些維護工作，以及何時執行這些工作。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 90b6e4434abc5573a364c769bd835e08e5dff16d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager 的維護工作

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 站台與階層需要定期維護與監視，才能持續提供有效的服務。 定期維護可確保硬體、軟體與 Configuration Manager 資料庫能持續正確且有效率地運作。 最佳化效能可大幅降低失敗的風險。  

 若要設定警示，並使用狀態系統監視 Configuration Manager 的健全狀況，請參閱[使用 System Center Configuration Manager 的警示和狀態系統](../../../core/servers/manage/use-alerts-and-the-status-system.md)。  

-   [維護工作](#bkmk_MTs)  

##  <a name="bkmk_MTs"></a> 維護工作  
 定期維護對確保站台正常運作很重要。 維護記錄要記錄維護日期、維護工作執行人，以及有關工作的所有維護相關意見。  

### <a name="when-to-do-common-maintenance-tasks"></a>一般維護工作的執行時機  
 站台維護請考慮每日或每週維護。 有些工作可能需要不同的排程。 一般維護可包括內建維護工作與其他工作，如帳戶維護，以保持遵守公司原則。  

 使用以下資訊作為指南，協助您規劃執行不同維護工作的時機。 使用這些清單作為起始點，並新增可能需要的工作。  

**每日工作**   
以下是可能要考慮每天排程的維護工作：  

-   檢查排程每日執行的預先定義維護工作是否都成功執行。  

-   檢查 Configuration Manager 資料庫狀態。  

-   檢查網站伺服器狀態。  

-   檢查 Configuration Manager 站台系統收件匣中是否有檔案積存狀況。  

-   檢查網站系統狀態。  

-   檢查網站系統上的作業系統事件記錄檔。  

-   檢查網站資料庫電腦上的 SQL Server 錯誤記錄檔。  

-   檢查系統效能。  

-   檢查 Configuration Manager 警示。  

**每週工作**   
以下是可能要考慮每週排程的維護工作：  

-   檢查排程每週執行的預先定義維護工作是否都成功執行。  

-   從網站系統刪除不必要檔案。  

-   如有必要，產生並發佈使用者報告。  

-   備份應用程式、安全性與系統事件記錄檔，並將之清除。  

-   檢查站台資料庫大小，並檢查站台資料庫伺服器上是否有足夠的磁碟空間，讓站台資料庫有成長空間。  

-   根據您的 SQL Server 維護規劃，在站台資料庫上執行 SQL Server 資料庫維護。  

-   檢查所有網站系統上的可用磁碟空間。  

-   在所有網站系統上執行磁碟重組工具。  

**定期工作**   
有些不需要每日或每週執行的維護工作，對確保整體網站的健全狀況很重要。 這些工作也可以確保安全性與災害復原規劃都保持在最新狀態。 以下是可能要考慮定期排程，但不是每日或每週執行的維護工作：  

-   根據您的安全性規劃，若有必要，變更帳戶與密碼。  

-   檢閱維護規劃，以檢查確實根據已設定的站台組態，正確且有效率的排程已排程維護工作。  

-   檢閱 Configuration Manager 階層設計，找出必要的變更之處。  

-   檢查網路效能，確保未進行會影響網站運作的變更。  

-   檢查會影響網站運作的 Active Directory 設定並未變更。 例如，檢查指派至用來作為 Configuration Manager 站台界限之 Active Directory 站台的子網路並未變更。  

-   檢閱災害復原規劃，找出任何必要變更。  

-   根據測試實驗室中的災害復原規劃來執行站台復原，方法是使用由 [備份站台伺服器] 維護工作所建立之最新備份的備份複本。

-   檢查硬體，找出任何錯誤或可用的硬體更新。  

-   檢查網站整體健全狀況。  

###  <a name="BKMK_UseMTs"></a> 維護站台資料庫的操作健全狀況  
 在 Configuration Manager 站台與階層執行您排程與設定的工作時，站台元件會持續將資料新增到 Configuration Manager 資料庫中。 隨著資料量增加，資料庫內的資料庫效能與資料庫內的可用磁碟空間也會減少。 您可以設定站台維護工作，以移除您不需要的老舊資料。  

 Configuration Manager 提供預先定義的維護工作，您可以藉由這些工作維護 Configuration Manager 資料庫的健全狀況。 預設並非每個站台都提供所有的維護工作。 有些工作會啟用，有些則不會，它們都支援您設定的排程。  

 大部分維護工作都會定期從 Configuration Manager 資料庫移除過時資料。 移除不需要的資料來降低資料庫大小也能改善資料庫效能與整體性，並提升網站與階層效率。 其他工作，像是**重建索引**，有助於維護資料庫效率。 其他工作，像是**備份站台伺服器**工作，有助於準備災害復原。  

> [!IMPORTANT]  
>  規劃刪除資料工作的排程時，請考慮該資料跨階層的使用狀況。 在某個站台上執行刪除資料的工作時，會從 Configuration Manager 資料庫移除資訊，而這也會變更階層內所有站台的複寫。 此項刪除會影響依賴該資料的其他工作。 例如，在管理中心網站上，您可能設定探索每個月執行一次，找出非用戶端電腦。 您想要在探索到這些電腦的兩週內，安裝 Configuration Manager 用戶端。 不過，階層中有一個站台的系統管理員，設定每七天執行一次「刪除過時探索資料」工作。 結果在探索到非用戶端電腦的七天後，它們就從 Configuration Manager 資料庫中刪除。 回到管理中心網站，您準備好要在第 10 天於這些新電腦上推入安裝 Configuration Manager 用戶端。 不過，因為最近執行了 [刪除過時探索資料] 工作，並刪除 7 天以上的資料，導致您無法在資料庫上找到這些探索到的電腦。  

安裝 Configuration Manager 站台後，請檢閱可用的維護工作，並啟用進行操作所需要的工作。 檢閱每個工作的預設排程，並在必要時根據您的階層與環境設定排程以微調維護工作。 雖然每個工作的預設排程應能滿足絕大多數的環境，但仍請監視站台與資料庫的效能，並適時微調工作，以提升部署的效率。 規劃定期檢閱網站與資料庫效能，並重設維護工作與其排程以維護效率。  

#### <a name="set-up-maintenance-tasks"></a>設定維護工作  
 每個 Configuration Manager 站台都支援協助維護站台資料庫操作效率的維護工作。 根據預設，每個網站中啟用數個維護工作和所有工作都支援獨立的排程。 每個站台會各自設定維護工作，並套用到該站台資料庫。 不過，有些工作，像是**刪除過時探索資料**，會影響階層中所有站台的可用資訊。  

 只有您可以在站台中設定的維護工作才會顯示在 Configuration Manager 主控台中。 如需站台類型的完整維護工作清單，請參閱 [System Center Configuration Manager 的維護工作參考](../../../core/servers/manage/reference-for-maintenance-tasks.md)。  

 使用下列程序來協助您設定維護工作的一般設定。  

###### <a name="to-set-up-maintenance-tasks-for-configuration-manager"></a>為 Configuration Manager 設定維護工作  

1.  在 Configuration Manager 主控台中，移至 [系統管理] > [站台設定] >[站台]。  

2.  選擇您要設定維護工作的站台。  

3.  在 [首頁] 索引標籤的 [設定] 群組中，選擇 [站台維護]，然後選擇您要設定的維護工作。  

    > [!TIP]  
    >  只顯示所選站台提供的工作。  

4.  若要設定工作，請選擇 [編輯]，確保已選取 [啟用這項工作] 核取方塊並設定工作執行的排程。 如果工作也會刪除舊的資料，設定在工作執行時將會從資料庫刪除資料的存在時間。 選擇 [確定] 關閉工作 [內容]。  

    > [!NOTE]  
    >  針對**刪除過時狀態訊息**，設定您設定狀態篩選規則時要刪除資料的存在時間。  

5.  若要啟用或停用工作而不需要編輯工作內容，請選擇 [啟用] 或 [停用] 按鈕。 變更的按鈕標籤視工作的目前組態而定。  

6.  當您完成設定維護工作時，請選擇 [確定] 完成程序。
