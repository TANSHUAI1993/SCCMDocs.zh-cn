---
title: "建立自訂報告 | Microsoft Docs"
description: "定義報告模型以符合商務需求，然後將報告模型部署至 Configuration Manager。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 9951dd9333ebef00c7acd5d72b20a02382e3206c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="creating-custom-report-models-for-system-center-configuration-manager-in-sql-server-reporting-services"></a>在 SQL Server Reporting Services 中建立 System Center Configuration Manager 的自訂報告模型

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中包含範例報告模型，但您也可以定義符合您商務需求的報告模型，然後再將報告模型部署至 Configuration Manager，以在建立以模型為基礎的新報告時使用。 下表提供建立及部署基本報表模型的步驟。  

> [!NOTE]  
>  如需建立更進階之報表模型的步驟，請參閱本主題中的 [在 SQL Server Reporting Services 中建立進階報表模型的步驟](#AdvancedReportModel) 一節。  

|步驟|說明|詳細資訊|  
|----------|-----------------|----------------------|  
|確認是否已安裝 SQL Server Business Intelligence Development Studio|報表模型是使用 SQL Server Business Intelligence Development Studio 設計及建置的。 確認您用於建立自訂報表模型的電腦上，是否已安裝 SQL Server Business Intelligence Development Studio。|如需有關 SQL Server Business Intelligence Development Studio 的詳細資訊，請參閱 SQL Server 2008 文件。|  
|建立報表模型專案|報表模型專案內含資料來源的定義 (.ds 檔案)、資料來源檢視的定義 (.dsv 檔案)，以及報表模型 (.smdl 檔案)。|如需詳細資訊，請參閱此主題中的＜ [建立報表模型專案](#BKMK_CreateReportModelProject) ＞一節。|  
|定義報表模型的資料來源|建立報表模型專案後，您必須定義一種要自其擷取商務資料的資料來源。 這一般是 Configuration Manager 站台資料庫。|如需詳細資訊，請參閱此主題中的＜ [若要定義報表模型的資料來源](#BKMK_DefineReportModelDataSource) ＞一節。|  
|定義報表模型的資料來源檢視|在報表模型專案中定義要使用的資料來源後，下一個步驟便是定義專案的資料來源檢視。 資料來源檢視是以一個或多個資料來源為基礎的邏輯資料模型。 資料來源檢視封裝了底層資料來源中所含對實體物件的存取，例如表格和檢視。 SQL Server Reporting Services 會從資料來源檢視產生報表模型。<br /><br /> 資料來源檢視為您所指定的資料提供了一個有用的呈現方式，方便您進行模型設計的程序。 不需要變更底層的資料來源，您就可以重新命名資料表和欄位，以及在資料來源檢視中新增彙總欄位和衍生資料表。 對於一個有效的模型，則只將您想要使用的資料表新增至資料來源檢視。|如需詳細資訊，請參閱此主題中的＜ [若要定義報表模型的資料來源檢視](#BKMK_DefineReportModelDataSourceView) ＞一節。|  
|建立報表模型|報表模型位於資料頂端層，用於識別企業實體、欄位和角色。 使用這些模型發佈時，報告產生器使用者可以在不需要熟悉資料庫結構，或瞭解及撰寫查詢的情況下製作報表。 這些模型是由幾組以好記名稱分組的相關報表項目所組成，在這些商務項目間使用預先定義的關聯性，並進行預先定義的計算。 這些模型是使用名為語意模型定義語言 (SMDL) 的 XML 語言所定義。 報表模型檔案的副檔名為 .smdl。|如需詳細資訊，請參閱此主題中的＜ [建立報表模型](#BKMK_CreateReportModel) ＞一節。|  
|發佈報表模型|若要使用剛才建立的模型建立報告，您必須將該模型發佈到報告伺服器。 當模型發佈時，其中會包含資料來源和資料來源檢視。|如需詳細資訊，請參閱此主題中的＜ [若要發佈在 SQL Server Reporting Services 中使用的報表模型](#BKMK_PublishReportModel) ＞一節。|  
|將報告模型部署到 Configuration Manager|您必須先將報告模型部署至 Configuration Manager，才能在 [建立報告精靈]中使用自訂報告模型，建立以模型為基礎的報告。|如需詳細資訊，請參閱此主題中的＜ [將自訂報表模型部署至 Configuration Manager](#BKMK_DeployReportModel) ＞一節。|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>在 SQL Server Reporting Services 中建立基本報告模型的步驟  
 您可以使用下列程序建立基本報告模型，站台的使用者可以根據 Configuration Manager 資料庫單一檢視中的資料，使用這些基本報告模型建立特定模型的報告。 您可以建立一個表示站台用戶端電腦之相關資訊的報表模型給報表作者。 此資訊是從 Configuration Manager 資料庫的 **v_R_System** 檢視取得。  

 在執行這些程序的電腦上，確定您是否已安裝 SQL Server Business Intelligence Development Studio，且電腦是否具有與 Reporting Services 點伺服器的網路連線能力。 如需有關 SQL Server Business Intelligence Development Studio 的詳細資訊，請參閱 SQL Server 2008 文件。  

###  <a name="BKMK_CreateReportModelProject"></a> To create the report model project  

1.  在桌面上，依序按一下 [開始] 和 [Microsoft SQL Server 2008] ，然後按一下 [SQL Server Business Intelligence Development Studio] 。  

2.  [SQL Server Business Intelligence Development Studio]  在 Microsoft Visual Studio 中開啟後，依序按一下 [檔案] 、[新增] 及 [專案] 。  

3.  在 [新增專案]  對話方塊中，選取 [範本]  清單中的 [報表模型專案]  。  

4.  在 [名稱]  方塊中，指定此報表模型的名稱。 針對此範例，輸入 **Simple_Model**。  

5.  若要建立報表模型專案，請按一下 [確定] 。  

6.  此時 [方案總管]  中會顯示 [Simple_Model] 解決方案。  

    > [!NOTE]  
    >  如果沒有看到 [方案總管]  窗格，請按一下 [檢視] ，再按一下 [方案總管] 。  

###  <a name="BKMK_DefineReportModelDataSource"></a> 若要定義報表模型的資料來源  

1.  在 [SQL Server Business Intelligence Development Studio]  的 [方案總管] 窗格中，以滑鼠右鍵按一下 [資料來源]  以選取 [新增資料來源] 。  

2.  在 [歡迎使用資料來源精靈]  頁面上，按 [下一步] 。  

3.  在 [選取如何定義連接]  頁面上，確認已選取 [依據現有的或新的連接建立資料來源]  ，然後按一下 [新增] 。  

4.  在 [連線管理員]  對話方塊中，為資料來源指定下列連線內容：  

    -   **伺服器名稱**：輸入 Configuration Manager 站台資料庫伺服器的名稱，或從清單中選取名稱。 如果您使用的是具名執行個體，而不是預設執行個體，請輸入 &lt;*資料庫伺服器*>\\&lt;*執行個體名稱*>。  

    -   選取 [使用 Windows 驗證] 。  

    -   在 [選取或輸入資料庫名稱] 清單中，選取 Configuration Manager 站台資料庫的名稱。  

5.  若要確認資料庫連線，請按一下 [測試連線] 。  

6.  如果連線成功，按一下 [確定]  關閉 [連線管理員]  對話方塊。 如果連線不成功，請確認所輸入的資訊是否正確，然後再按一下 [測試連線]  。  

7.  在 [選取如何定義連接]  頁面上，確認已選取 [依據現有的或新的連接建立資料來源]  ，確認已在 [資料連線] 中選取剛才所指定的資料來源，然後按 [下一步] 。  

8.  在 [資料來源名稱] 中，指定資料來源的名稱，然後按一下 [完成] 。 針對此範例，輸入 **Simple_Model**。  

9. 資料來源 [Simple_Model.ds]  現在會顯示在 [方案總管]  的 [資料來源]  節點下方。  

    > [!NOTE]  
    >  若要編輯現有資料來源的內容，請按兩下 [方案總管]  窗格的 [資料來源]  資料夾中的資料來源，在 [資料來源設計師] 中顯示資料來源內容。  

###  <a name="BKMK_DefineReportModelDataSourceView"></a> 若要定義報表模型的資料來源檢視  

1.  在 [方案總管] 中，以滑鼠右鍵按一下 [資料來源檢視]  ，選取 [加入新的資料來源檢視] 。  

2.  在 [歡迎使用資料來源檢視精靈]  頁面上，按 [下一步] 。 [選取資料來源]  頁面隨即顯示。  

3.  在 [關聯式資料來源]  視窗中，確認已選取 [Simple_Model]  資料來源，然後按 [下一步] 。  

4.  在 [選取資料表和檢視]  頁面上，在 [可用的物件]  清單中選取下列檢視以供報表模型使用： **v_R_System (dbo)**。  

    > [!TIP]  
    >  若要協助在 [可用的物件]  清單中找出檢視，請按一下清單頂端的 [名稱]  標題，依字母順序為物件排序。  

5.  選取檢視之後，按一下 [&gt;] **>** 將物件傳送至 [包含的物件]  。  

6.  如果顯示 [名稱比對]  頁面，請接受預設選取項目，然後按 [下一步] 。  

7.  當您選取完所需的物件時，請按 [下一步] ，然後指定資料來源檢視的名稱。 針對此範例，輸入 **Simple_Model**。  

8.  按一下 [完成] 。 此時 [Simple_Model.dsv]  資料來源檢視會顯示在 [方案總管]  的 [資料來源檢視] 資料夾中。  

###  <a name="BKMK_CreateReportModel"></a> To create the report model  

1.  在 [方案總管] 中，以滑鼠右鍵按一下 [報表模型]  ，選取 [加入新的報表模型] 。  

2.  在 [歡迎使用報表模型精靈]  頁面上，按 [下一步] 。  

3.  在 [選取資料來源檢視]  頁面上，在 [可用的資料來源檢視]  清單中選取資料來源檢視，然後按 [下一步] 。 針對此範例，選取 [Simple_Model.dsv] 。  

4.  在 [選取報表模型產生規則]  頁面上接受預設值，然後按 [下一步] 。  

5.  在 [收集模型統計資料]  頁面上，確認已選取 [更新模型統計資料再產生]  ，然後按 [下一步] 。  

6.  在 [正在完成精靈]  頁面上，指定報表模型的名稱。 針對此範例，確認已顯示 [Simple_Model]  。  

7.  若要完成精靈並建立報表模型，請按一下 [執行] 。  

8.  若要結束精靈，請按一下 [完成] 。 此時報表模型會顯示在 [設計] 視窗中。  

###  <a name="BKMK_PublishReportModel"></a> 若要發佈在 SQL Server Reporting Services 中使用的報表模型  

1.  在 [方案總管] 中，以滑鼠右鍵按一下報表模型，選取 [部署] 。 針對此範例，報表模型為 [Simple_Model.smdl] 。  

2.  在 [SQL Server Business Intelligence Development Studio]  視窗的左下角檢查部署狀態。 部署完成時，會顯示 [部署成功]  。 如果部署失敗，[輸出]  視窗會顯示失敗的原因。 現在 SQL Server Reporting Services 網站上有提供新的報表模型。  

3.  依序按一下 [檔案] 和 [全部儲存] ，然後關閉 [SQL Server Business Intelligence Development Studio] 。  

###  <a name="BKMK_DeployReportModel"></a> To deploy the custom report model to Configuration Manager  

1.  找到您建立報表模型專案的資料夾。 例如，%*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\*&lt;專案名稱\>*。  

2.  將下列檔案從報表模型專案資料夾複製到電腦上的暫存資料夾：  

    -   *&lt;模型名稱\>* **.dsv**  

    -   *&lt;模型名稱\>* **.smdl**  

3.  使用文字編輯器 (例如記事本) 開啟上述檔案。  

4.  在 *&lt;模型名稱\>***.dsv** 檔案中，找到檔案的第一行，其內容如下：  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

     編輯此行如下：  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine" xmlns:xsi="RelationalDataSourceView"\>**  

5.  將檔案的完整內容複製到 Windows 剪貼簿。  

6.  關閉 *&lt;模型名稱\>***.dsv** 檔案。  

7.  在 *&lt;模型名稱\>***.smdl** 檔案中，找到檔案的最後三行，其內容如下：  

     `</Entity>`  

     `</Entities>`  

     `</SemanticModel>`  

8.  直接將 *&lt;模型名稱\>***.dsv** 檔案的內容貼至檔案的最後一行前方 (**&lt;SemanticModel\>**)。  

9. 儲存後關閉 *&lt;模型名稱\>***.smdl** 檔案。  

10. 將 *&lt;模型名稱\>***.smdl** 檔案複製到 Configuration Manager 站台伺服器上的 *%programfiles%*\Microsoft Configuration Manager\AdminConsole\XmlStorage\Other 資料夾。  

    > [!IMPORTANT]  
    >  將報告模型檔案複製到 Configuration Manager 站台伺服器後，您必須先結束並重新啟動 Configuration Manager 主控台，才能在 [建立報告精靈] 中使用報告模型。  

##  <a name="AdvancedReportModel"></a> 在 SQL Server Reporting Services 中建立進階報表模型的步驟  
 您可以利用下列程序建立進階報告模型，您站台中的使用者可根據 Configuration Manager 資料庫中多個檢視的資料，使用該模型建立模型為基礎的特殊報告。 您建立的報表模型可對報告作者呈現有關用戶端電腦及電腦上所安裝作業系統的資訊。 此資訊是從 Configuration Manager 資料庫的下列檢視取得：  

-   **V_R_System**：包含有關探索到之電腦和 Configuration Manager 用戶端的資訊。  

-   **V_GS_OPERATING_SYSTEM**：包含有關用戶端電腦上所安裝作業系統的資訊。  

 從上述檢視中選取的項目會彙總至一個清單中，指定易記名稱，然後使用報告產生器對報告作者呈現以納入特殊報告。  

 在執行這些程序的電腦上，確定您是否已安裝 SQL Server Business Intelligence Development Studio，且電腦是否具有與 Reporting Services 點伺服器的網路連線能力。 如需有關 SQL Server Business Intelligence Development Studio 的詳細資訊，請參閱 SQL Server 文件。  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  在桌面上，依序按一下 [開始] 和 [Microsoft SQL Server 2008] ，然後按一下 [SQL Server Business Intelligence Development Studio] 。  

2.  [SQL Server Business Intelligence Development Studio]  在 Microsoft Visual Studio 中開啟後，依序按一下 [檔案] 、[新增] 及 [專案] 。  

3.  在 [新增專案]  對話方塊中，選取 [範本]  清單中的 [報表模型專案]  。  

4.  在 [名稱]  方塊中，指定此報表模型的名稱。 在此範例中，輸入 **Advanced_Model**。  

5.  若要建立報表模型專案，請按一下 [確定] 。  

6.  [Advanced_Model]  解決方案會在 [方案總管] 中顯示。  

    > [!NOTE]  
    >  如果沒有看到 [方案總管]  窗格，請按一下 [檢視] ，再按一下 [方案總管] 。  

#### <a name="to-define-the-data-source-for-the-report-model"></a>若要定義報表模型的資料來源  

1.  在 [SQL Server Business Intelligence Development Studio]  的 [方案總管] 窗格中，以滑鼠右鍵按一下 [資料來源]  以選取 [新增資料來源] 。  

2.  在 [歡迎使用資料來源精靈]  頁面上，按 [下一步] 。  

3.  在 [選取如何定義連接]  頁面上，確認已選取 [依據現有的或新的連接建立資料來源]  ，然後按一下 [新增] 。  

4.  在 [連線管理員]  對話方塊中，為資料來源指定下列連線內容：  

    -   **伺服器名稱**：輸入 Configuration Manager 站台資料庫伺服器的名稱，或從清單中選取名稱。 如果您使用的是具名執行個體，而不是預設執行個體，請輸入 &lt;*資料庫伺服器*>\\&lt;*執行個體名稱*>。  

    -   選取 [使用 Windows 驗證] 。  

    -   在 [選取或輸入資料庫名稱] 清單中，選取 Configuration Manager 站台資料庫的名稱。  

5.  若要確認資料庫連線，請按一下 [測試連線] 。  

6.  如果連線成功，按一下 [確定]  關閉 [連線管理員]  對話方塊。 如果連線不成功，請確認所輸入的資訊是否正確，然後再按一下 [測試連線]  。  

7.  在 [選取如何定義連接]  頁面上，確認已選取 [依據現有的或新的連接建立資料來源]  ，確認您剛才指定的資料來源已在 [資料連線]  清單方塊中選取，然後按 [下一步] 。  

8.  在 [資料來源名稱] 中，指定資料來源的名稱，然後按一下 [完成] 。 在此範例中，輸入 **Advanced_Model**。  

9. [Advanced_Model.ds]  資料來源會在 [方案總管]  中的 [資料來源]  節點下顯示。  

    > [!NOTE]  
    >  若要編輯現有資料來源的內容，請按兩下 [方案總管]  窗格的 [資料來源]  資料夾中的資料來源，在 [資料來源設計師] 中顯示資料來源內容。  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>若要定義報表模型的資料來源檢視  

1.  在 [方案總管] 中，以滑鼠右鍵按一下 [資料來源檢視]  ，選取 [加入新的資料來源檢視] 。  

2.  在 [歡迎使用資料來源檢視精靈]  頁面上，按 [下一步] 。 [選取資料來源]  頁面隨即顯示。  

3.  在 [關聯式資料來源]  視窗中，確認已選取 [Advanced_Model]  資料來源，然後按 [下一步] 。  

4.  在 [選取資料表和檢視表]  頁面上的 [可用的物件]  清單中，選取要在報表模型中使用的下列檢視：  

    -   **v_R_System (dbo)**  

    -   **v_GS_OPERATING_SYSTEM (dbo)**  

     選取每個檢視之後，按一下 [&gt;] **>** 將物件傳送至 [包含的物件]  。  

    > [!TIP]  
    >  若要協助在 [可用的物件]  清單中找出檢視，請按一下清單頂端的 [名稱]  標題，依字母順序為物件排序。  

5.  如果 [名稱比對]  對話方塊出現，請接受預設選項，然後按 [下一步] 。  

6.  選取您需要的物件之後，按 [下一步] ，然後指定資料來源檢視的名稱。 在此範例中，輸入 **Advanced_Model**。  

7.  按一下 [完成] 。 [Advanced_Model.dsv]  資料來源檢視會在 [方案總管]  的 [資料來源檢視] 資料夾中顯示。  

#### <a name="to-define-relationships-in-the-data-source-view"></a>若要在資料來源檢視中定義關聯性  

1.  在 [方案總管] 中，按兩下 [Advanced_Model.dsv]  開啟 [設計] 視窗。  

2.  以滑鼠右鍵按一下 [v_R_System]  視窗的標題列，選取 [取代資料表] ，然後按一下 [使用新具名查詢] 。  

3.  在 [建立具名查詢]  對話方塊中，按一下 [加入資料表]  圖示 (通常是功能區中的最後一個圖示)。  

4.  在 [加入資料表]  對話方塊中，按一下 [檢視表]  索引標籤，選取清單中的 [V_GS_OPERATING_SYSTEM]  ，然後按一下 [加入] 。  

5.  按一下 [關閉]  ，關閉 [加入資料表]  對話方塊。  

6.  在 [建立具名查詢]  對話方塊中，指定下列資訊：  

    -   **名稱：** 指定查詢的名稱。 在此範例中，輸入 **Advanced_Model**。  

    -   **描述：** 指定查詢的描述。 在此範例中，輸入 **Example Reporting Services report model**。  

7.  在 [v_R_System]  視窗中，於物件清單中選取下列要在報表模型中顯示的項目：  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  在 [v_GS_OPERATING_SYSTEM]  方塊中，於物件清單中選取下列要在報表模型中顯示的項目：  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. 若要以一份清單對報告作者呈現這些檢視表中的物件，您必須使用聯結指定兩個資料表或檢視表之間的關聯性。 您可以使用 [ResourceID] 物件聯結兩個檢視表，該物件會出現在這兩個檢視表中。  

10. 在 [v_R_System]  視窗中，按住 [ResourceID]  物件並將它拖曳至 [v_GS_OPERATING_SYSTEM]  視窗中的 [ResourceID]  物件。  

11. 按一下 [確定]   

12. [Advanced_Model]  視窗會取代 [v_R_System]  視窗，並且包含 [v_R_System]  和 [v_GS_OPERATING_SYSTEM]  檢視表中報表模型所需的所有必要物件。 現在您可以從 [資料來源檢視設計師] 中刪除 [v_GS_OPERATING_SYSTEM]  視窗。 以滑鼠右鍵按一下 [v_GS_OPERATING_SYSTEM]  視窗的標題列，選取 [從 DSV 刪除資料表] 。 在 [刪除物件]  對話方塊中，按一下 [確定]  確認刪除。  

13. 按一下 [檔案] ，然後按一下 [全部儲存] 。  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  在 [方案總管] 中，以滑鼠右鍵按一下 [報表模型]  ，選取 [加入新的報表模型] 。  

2.  在 [歡迎使用報表模型精靈]  頁面上，按 [下一步] 。  

3.  在 [選取資料來源檢視]  頁面上的 [可用的資料來源檢視]  清單中選取資料來源檢視，然後按 [下一步] 。 針對此範例，選取 [Simple_Model.dsv] 。  

4.  不要變更 [選取報表模型產生規則]  頁面上的預設值，然後按 [下一步] 。  

5.  在 [收集模型統計資料]  頁面上，確認已選取 [更新模型統計資料再產生]  ，然後按 [下一步] 。  

6.  在 [正在完成精靈]  頁面上，指定報表模型的名稱。 在此範例中，確認顯示的是 [Advanced_Model]  。  

7.  若要完成精靈並建立報表模型，請按一下 [執行] 。  

8.  若要結束精靈，請按一下 [完成] 。  

9. 此時報表模型會顯示在 [設計] 視窗中。  

#### <a name="to-modify-object-names-in-the-report-model"></a>若要修改報表模型中的物件名稱  

1.  在 [方案總管] 中，以滑鼠右鍵按一下報表模型，選取 [檢視表設計工具] 。 在此範例中，選取 [Advanced_Model.smdl] 。  

2.  在報表模型 [設計] 檢視中，以滑鼠右鍵按一下任何物件名稱，選取 [重新命名] 。  

3.  為選取的物件輸入新名稱，然後按 Enter。 例如，您可以將物件 [CSD_Version_0]  重新命名為 [Windows Service Pack Version] 。  

4.  完成物件重新命名時，按一下 [檔案] ，然後按一下 [全部儲存] 。  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>若要發佈在 SQL Server Reporting Services 中使用的報表模型  

1.  在 [方案總管] 中，以滑鼠右鍵按一下 [Advanced_Model.smdl]  ，選取 [部署] 。  

2.  在 [SQL Server Business Intelligence Development Studio]  視窗的左下角檢查部署狀態。 部署完成時，會顯示 [部署成功]  。 如果部署失敗，[輸出]  視窗會顯示失敗的原因。 現在 SQL Server Reporting Services 網站上有提供新的報表模型。  

3.  依序按一下 [檔案] 和 [全部儲存] ，然後關閉 [SQL Server Business Intelligence Development Studio] 。  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1.  找到您建立報表模型專案的資料夾。 例如，%*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\*&lt;專案名稱\>*。  

2.  將下列檔案從報表模型專案資料夾複製到電腦上的暫存資料夾：  

    -   *&lt;模型名稱\>* **.dsv**  

    -   *&lt;模型名稱\>* **.smdl**  

3.  使用文字編輯器 (例如記事本) 開啟上述檔案。  

4.  在 *&lt;模型名稱\>***.dsv** 檔案中，找到檔案的第一行，其內容如下：  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

     編輯此行如下：  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine" xmlns:xsi="RelationalDataSourceView"\>**  

5.  將檔案的完整內容複製到 Windows 剪貼簿。  

6.  關閉 *&lt;模型名稱\>***.dsv** 檔案。  

7.  在 *&lt;模型名稱\>***.smdl** 檔案中，找到檔案的最後三行，其內容如下：  

     `</Entity>`  

     `</Entities>`  

     `</SemanticModel>`  

8.  直接將 *&lt;模型名稱\>***.dsv** 檔案的內容貼至檔案的最後一行前方 (**&lt;SemanticModel\>**)。  

9. 儲存後關閉 *&lt;模型名稱\>***.smdl** 檔案。  

10. 將 *&lt;模型名稱\>***.smdl** 檔案複製到 Configuration Manager 站台伺服器上的 *%programfiles%*\Microsoft Configuration Manager\AdminConsole\XmlStorage\Other 資料夾。  

    > [!IMPORTANT]  
    >  將報告模型檔案複製到 Configuration Manager 站台伺服器後，您必須先結束並重新啟動 Configuration Manager 主控台，才能在 [建立報告精靈] 中使用報告模型。  
