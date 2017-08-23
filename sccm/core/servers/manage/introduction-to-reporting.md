---
title: "報告簡介 | Microsoft Docs"
description: "了解在 Configuration Manager 中可讓您用來管理報告的工具組和資源。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
caps.latest.revision: "7"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5846ca3c91626491b03b36dd17b454bb9382a8dc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager 的報告簡介

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 中的報告功能提供一組工具和資源，可協助您使用 SQL Server Reporting Services (SSRS) 的進階報告功能，並體驗 Reporting Services 報表產生器提供的豐富撰寫功能。 報告功能可協助您收集、整理並展示使用者、硬體/軟體清查、軟體更新、應用程式、站台狀態以及組織中其他 Configuration Manager 操作的資訊。 報告會提供您多個預先定義的報告，不必變更就可以使用，您也可以修改報告以符合需求，並且可建立自訂報告。 下列各節可協助您管理 Configuration Manager 中的報告功能。  

##  <a name="BKMK_SQLServerReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services 提供一套完備的立即可用工具與服務，可協助您建立、部署和管理您組織的報告，以及可讓您延伸和自訂報告功能的程式設計功能。 Reporting Services 是一個以伺服器為基礎的報告平台，可針對各種資料來源提供完整的報告功能。  

 Configuration Manager 使用 SQL Server Reporting Services 作為報告解決方案。 與 Reporting Services 整合可提供以下優勢：  

-   使用業界標準報告系統，查詢 Configuration Manager 資料庫。  

-   使用 Configuration Manager 報表檢視器或使用報表管理員 (透過 Web 連線至報告) 顯示報告。  

-   提供高效能、 可用性和延展性。  

-   提供使用者可以訂閱的報告訂閱功能，例如，管理員可以每天自動接收詳細記錄軟體更新首度發行狀態的電子郵件報告。  

-   匯出使用者可用各種常見格式選取的報告。  

 如需有關 Reporting Services 的詳細資訊，請參閱 SQL Server 2008 線上叢書中的 [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=212032) 。  

##  <a name="BKMK_ReportingServicesPoint"></a> Reporting Services 點  
 Reporting Services 點是安裝在執行 Microsoft SQL Server Reporting Services 之伺服器上的站台系統角色。 Reporting Services 點會將 Configuration Manager 報告定義複製到 Reporting Services、根據報告類別建立報告資料夾，並設定報告資料夾與報告上的安全性原則 (以 Configuration Manager 系統管理使用者的角色型權限為依據)。 在 10 分鐘的間隔時間之中，如果安全性原則有所變更 (例如使用報表管理員)，則 Reporting Services 點會連線至 Reporting Services 以重新套用安全性原則。 如需有關如何規劃及安裝 Reporting Services 點的詳細資訊，請參閱下列文件：  

-   [System Center Configuration Manager 中的報告規劃](planning-for-reporting.md)  

-   [設定 System Center Configuration Manager 中的報表](configuring-reporting.md)  

##  <a name="BKMK_ConfigurationManagerReports"></a> Configuration Manager 報告  
 Configuration Manager 可提供 50 多個報告資料夾，其中含有 400 多份報告的報告定義，而在 Reporting Services 點安裝期間，這些報告定義皆會複製到 SQL Server Reporting Services 中的根報告資料夾。 報告會顯示在 Configuration Manager 主控台中，並且會根據報告類別歸類到子資料夾中。 報告不會在 Configuration Manager 階層向上或向下散佈，而只會依據建立報告的站台資料庫來執行。 不過，由於 Configuration Manager 會複製整個階層的全域資料，因此您可以存取整個階層的資訊。 當有報告從站台資料庫擷取資料時，報告會具有目前站台和子站台的站台資料存取權，以及階層中每個站台的全域資料存取權。 就像其他 Configuration Manager 物件一樣，系統管理使用者必須具有執行或修改報告所需的適當權限。 若要執行報告，系統管理使用者必須具有物件的 [執行報告]  權限。 若要建立或修改報告，系統管理使用者必須具有物件的 [修改報告]  權限。  

###  <a name="BKMK_CreatingReports"></a> 建立與修改報告  
 Configuration Manager 會將 Microsoft SQL Server 報表產生器作為專用的撰寫與編輯工具，來處理模型式與 SQL 式報告。 當您在 Configuration Manager 主控台建立或編輯報告時，會開啟報表產生器。 如需管理報表的詳細資訊，請參閱 [System Center Configuration Manager 中的報表作業和維護](operations-and-maintenance-for-reporting.md)。  

###  <a name="BKMK_RunningReports"></a> 執行報表  
 當您在 Configuration Manager 主控台執行報告時，報表檢視器會開啟並連線到 Reporting Services。 在您指定任何必要的報告參數後，Reporting Services 便會擷取資料，並在檢視器中顯示結果。 您也可以連線到 SQL Services Reporting Services，連線到站台的資料來源，然後執行報告。  

###  <a name="BKMK_ReportPrompts"></a> 報告提示  
 Configuration Manager 中的報告提示或報告參數，是建立或修改報告時可讓您設定的報告內容。 報告提示可用於限制報告擷取的資料，或將報告擷取資料設為目標。 報告可以包含一個以上的提示，前提是提示名稱必須是獨一無二的，而且只包含符合 SQL Server 識別碼規則的英數字元。  

 當您執行報告時，提示會要求一個必要參數的值，並會根據該值擷取報告資料。 例如，[特定電腦的電腦資訊]  報告會擷取特定電腦的電腦資訊，並且會提示系統管理使用者輸入電腦名稱。 Reporting Services 會將指定的值傳遞至報告的 SQL 陳述式中所定義的變數。  

###  <a name="BKMK_ReportLinks"></a> 報告連結  
 來源報告中會使用 Configuration Manager 的報告連結，方便系統管理使用者存取其他資料，例如有關來源報告各個項目的詳細資訊。 如果目的地報告需要執行一個或多個提示，則來源報告必須包含具有各提示適用之值的資料欄。 您必須指定提供各提示值的欄編號。 例如，您可以將列出最近發現之電腦的報告，連結至列出特定電腦所接收最新訊息的報告。 建立連結時，您可以指定來源報告中的欄 2 包含目的地報告提示所需的電腦名稱。 執行來源報告時，各資料列左方會顯示連結圖示。 當您按一下某列的圖示時，報表檢視器會將該列指定欄中的值當成顯示目的地報告所需的提示值來傳遞。 報告只能用一個連結來設定，而且該連結只能連線至單一個目的地資源。  

> [!WARNING]  
>  如果您將目的地報告移動至不同的報告資料夾，則目的地報告的位置會因而變更。 來源資料夾中的報告連結不會自動更新為新的位置，而且報告連結在來源報告中沒有作用。  

##  <a name="BKMK_ReportFolders"></a> 報告資料夾  
 System Center Configuration Manager 中的報告資料夾可提供一個方法，來排序與篩選儲存在 Reporting Services 中的報告。 報告資料夾在有許多報告要管理時特別管用。 當您安裝 Reporting Services 點時，會將報告複製到 Reporting Services，並組織為 50 個以上的報告資料夾。 報告資料夾是唯讀的。 您無法在 Configuration Manager 主控台中修改報告資料夾。  

##  <a name="BKMK_ReportSubscriptions"></a> 報告訂閱  
 Reporting Services 的報告訂閱式是一種週期性的要求，會在特定時間或發生特定事件後，以您在訂閱中指定的應用程式檔案格式傳遞報告。 訂閱可提供您隨選執行報告的替代方式。 使用隨選報告需要主動在每次想要撿視報告時選取報告。 相較之下，訂閱則可以用於排程，並自動傳遞報告。  

 您可以在 Configuration Manager 主控台中管理報告訂閱。 報告訂閱會在報告伺服器上處理。 訂閱會利用部署在伺服器上的傳遞延伸模組來發佈。 根據預設，您可以建立的訂閱可將報告傳送至共用資料夾或電子郵件地址。 如需管理報表訂閱的詳細資訊，請參閱 [System Center Configuration Manager 中的報表作業和維護](operations-and-maintenance-for-reporting.md)。  

##  <a name="BKMK_ReportBuilder"></a> 報表產生器  
 Configuration Manager 會將 Microsoft SQL Server Reporting Services 報表產生器作為專用的撰寫與編輯工具，來處理模型式與 SQL 式報告。 當您在 Configuration Manager 主控台起始動作以建立或編輯報告時，會開啟報表產生器。 當您初次建立或修改報告時，便會自動安裝報表產生器。 當您執行或編輯報告時，會開啟與已安裝之 SQL Server 版本關聯的報表產生器版本。  

 報表產生器安裝可新增超過 20 種語言的支援。 當您執行報表產生器時，顯示的資料會以本機上執行的作業系統語言顯示。 如果報表產生器不支援該語言，則資料會以英文顯示。 報表產生器支援 SQL Server  2008 Reporting Services 的完整功能，其包括下列功能：  

-   提供外觀類似 Microsoft Office 的直覺化報告撰寫環境。  

-   提供 SQL Server  2008 報告定義語言 (RDL) 的彈性化報告版面配置。  

-   提供包括圖表和量表在內的各種資料虛擬化格式。  

-   提供格式豐富的文字方塊。  

-   匯出為 Microsoft Word 格式。  

 您也可以從 SQL Server Reporting Services 開啟報表產生器。  

##  <a name="BKMK_ReportModels"></a> SQL Server Reporting Services 中的報告模型  
 Configuration Manager 中的 SQL Reporting Services 會使用報告模型，協助系統管理使用者從資料庫選取要包含在模型式報告中的項目。 對於正在產生報告的系統管理使用者，報告模型只會顯示可供選擇的指定檢視和項目。 若要建立模型式報告，至少必須有一個可用的報告模型。 報告模型具有下列功能：  

-   您可以提供資料庫欄位與檢視邏輯商務名稱，以加快產生報告的速度。 不需要對資料庫結構有所瞭解就能產生報告。  

-   您可以用邏輯方式為項目分組。  

-   您可以定義項目之間的關聯性。  

-   您可以保護模型元素，使系統管理使用者只能查看權限內的資料。  

 即使 Configuration Manager 提供範例報告模型，您也可以自行定義報告模型，以符合商務需求。 如需如何建立報表模型的詳細資訊，請參閱[在 SQL Server Reporting Services 中建立 System Center Configuration Manager 的自訂報表模型](creating-custom-report-models-in-sql-server-reporting-services.md)。  

## <a name="next-steps"></a>後續步驟
[報告規劃](planning-for-reporting.md)
