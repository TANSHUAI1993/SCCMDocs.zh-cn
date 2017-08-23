---
title: "設定 Asset Intelligence | Microsoft Docs"
description: "在 System Center Configuration Manager 中設定 Asset Intelligence。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: d2704e0f93ad9748f7eb06d714b3754463cb3bdb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>設定 System Center Configuration Manager 中的 Asset Intelligence

*適用於：System Center Configuration Manager (最新分支)*

Asset Intelligence 清查和管理軟體授權使用量。   

## <a name="steps-to-configure-asset-intelligence"></a>設定 Asset Intelligence 的步驟  
   

- **步驟 1**︰若要收集 Asset Intelligence 報告所需的清查資料，您必須啟用硬體清查用戶端代理程式，如[如何擴充 System Center Configuration Manager 中的硬體清查](../../../../core/clients/manage/inventory/extend-hardware-inventory.md)中所述。
- **步驟 2**：[啟用 Asset Intelligence 硬體清查報告類別](#BKMK_EnableAssetIntelligence)。  
- **步驟 3**：[安裝 Asset Intelligence 同步處理點](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **步驟 4**：[啟用成功登入事件的稽核](#BKMK_EnableSuccessLogonEvents)  
- **步驟 5**：[匯入軟體授權資訊](#BKMK_ImportSoftwareLicenseInformation)  
- **步驟 6**：[設定 Asset Intelligence 維護工作](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 若要在 Configuration Manager 站台中啟用 Asset Intelligence，您必須啟用一或多個 Asset Intelligence 硬體清查報告類別。 您可以在 [Asset Intelligence]  首頁上啟用類別，或是透過 [管理]  工作區中 [用戶端設定]  節點的用戶端設定屬性，來啟用類別。 請利用下列其中一項程序。  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>若要從 Asset Intelligence 首頁啟用 Asset Intelligence 硬體清查報告類別  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [Asset Intelligence]。  

3.  在 [首頁] 索引標籤的 [Asset Intelligence]  群組中，選擇 [編輯清查類別]。   

4.  若要啟用 Asset Intelligence 報告，請選取 [啟用所有 Asset Intelligence 報告類別]，或選取 [僅啟用選取的 Asset Intelligence 報告類別]，然後從顯示的類別中選取至少一個報告類別。  

    > [!NOTE]  
    >  在用戶端掃描並傳回硬體清查之後，透過此程序啟用之硬體清查類別的相關 Asset Intelligence 報告才會顯示資料。  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>若要從用戶端設定屬性啟用 Asset Intelligence 硬體清查報告類別  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] >  [用戶端設定] > [預設用戶端代理程式設定]。 如果您已經建立自訂用戶端設定，您可以改為選取它們。  

3.  在 [首頁] 索引標籤 > [內容] 群組中，選擇 [內容]。   

4.  選擇 [硬體清查] > [設定類別]。 。  

5.  選擇 [依類別篩選] > [Asset Intelligence 報告類別]。 系統僅會以 Asset Intelligence 硬體清查類別來重新整理類別清單。  

6.  從清單中選取至少一個報告類別。  

    > [!NOTE]  
    >  在用戶端掃描並傳回硬體清查之後，透過此程序啟用之硬體清查類別的相關 Asset Intelligence 報告才會顯示資料。  
  

###  <a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

Asset Intelligence 同步處理點站台系統角色可用來將 Configuration Manager 站台連線至 System Center Online，以同步處理 Asset Intelligence 類別目錄資訊。 Asset Intelligence 同步處理點僅可安裝在位於 Configuration Manager 階層最上層站台的站台系統中，而且需要使用 TCP 連接埠 443 存取網際網路才能與 System Center Online 同步。

除了下載新的 Asset Intelligence 類別目錄資訊，Asset Intelligence 同步處理點還可以將自訂軟體項目資訊上傳至 System Center Online 以便分類。 Microsoft 會將所有上傳的軟體標題視為公用資訊。 請確認您自訂的軟體項目不含機密或專利資訊。 如需要求軟體產品分類的詳細資訊，請參閱[要求未分類的軟體產品型錄更新](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate)。  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>若要安裝 Asset Intelligence 同步處理點站台系統角色  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]> [站台設定] > [伺服器和站台系統角色]。  

3.  將 Asset Intelligence 同步處理點站台系統角色新增至新的或現有的站台系統伺服器：  

    -  針對**新的站台系統伺服器**：在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立站台系統伺服器]，啟動精靈。   

        > [!NOTE]  
        >  根據預設，當 Configuration Manager 安裝站台系統角色時，安裝檔會安裝到擁有最多可用硬碟空間的第一部可用 NTFS 格式化硬碟機上。 若要避免 Configuration Manager 安裝到特定磁碟機上，請建立名為 No_sms_on_drive.sms 的空檔案，並將它複製到磁碟機的根資料夾，再安裝站台系統伺服器。  

    -  針對**現有的站台系統伺服器**：選擇您要安裝 Asset Intelligence 同步處理點站台系統角色的伺服器。 選擇伺服器時，就會在詳細資料窗格中顯示已經安裝在該伺服器上的站台系統角色清單。  

         在 [首頁] 索引標籤的 [伺服器] 群組中，選擇 [新增站台系統角色]，啟動精靈。  

4.  完成 [一般] 頁面。 將 Asset Intelligence 同步處理點新增到現有的站台系統伺服器時，請確認之前設定的值。  

5.  在 [系統角色選取] 頁面上，從可用角色清單中選取 [Asset Intelligence 同步處理點]。  

6.  在 [Asset Intelligence 同步處理點連線設定] 頁面上，選擇 [下一步]。  

     預設會選取 [使用這個 Asset Intelligence 同步處理點]  設定，因此無法在此頁面上進行設定。 System Center Online 僅接受使用 TCP 連接埠 443 的網路流量，因此您無法在精靈的這個頁面上設定 [SSL 連接埠號碼]  。  

7.  您也可以選擇指定 System Center Online 驗證憑證檔案 (.pfx) 的路徑。 一般來說，您不需要指定憑證路徑，因為站台角色安裝期間會自動佈建連線憑證。  

8.  在 [Proxy 伺服器設定] 頁面上，指定 Asset Intelligence 同步處理點是否要在連線 System Center Online 以同步處理類別目錄時使用 Proxy 伺服器，以及是否要使用認證連接 Proxy 伺服器。  

    > [!WARNING]  
    >  如果必須使用 Proxy 伺服器才能連線 System Center Online，則在針對 Proxy 伺服器驗證所設的使用者帳戶密碼過期時，可能也會刪除連線憑證。  

9. 在 [同步處理排程]  頁面上，指定是否要同步處理 Asset Intelligence 類別目錄的排程。 如果您啟用同步處理排程，則可以指定簡易或自訂同步處理排程。 在排定的同步處理期間，Asset Intelligence 同步處理點會連線 System Center Online 以擷取最新的 Asset Intelligence 類別目錄。 您可以在 Configuration Manager 主控台中手動同步處理 Asset Intelligence 類別目錄中的 Asset Intelligence 節點。 如需手動同步處理 Asset Intelligence 類別目錄的步驟，請參閱 [System Center Configuration Manager 中的 Asset Intelligence 作業](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)中的[手動同步處理 Asset Intelligence 類別目錄](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog)一節。  

10. 完成精靈 

###  <a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 系統提供四種 Asset Intelligence 報告，以顯示在用戶端電腦上收集到的 Windows 安全性事件記錄檔資訊。 以下是如何設定電腦的安全性原則登入設定，以啟用成功登入事件的稽核。  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>使用本機安全性原則啟用成功登入事件記錄  

1.  在 Configuration Manager 用戶端電腦上，選擇 [開始] > [系統管理工具] > [本機安全性原則]。  

2.  在 [本機安全性原則] 對話方塊的 [安全性設定] 下方，展開 [本機原則]，然後選擇 [稽核原則]。  

3.  在 [結果] 窗格中，按兩下 [稽核登入事件]，確認選取 [成功] 核取方塊，然後選擇 [確定]。  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>使用 Active Directory 網域安全性原則啟用成功登入事件記錄  

1.  在網域控制站電腦上，選擇 [開始]，指向 [系統管理工具]，然後選擇 [網域安全性原則]。  

2.  在 [本機安全性原則] 對話方塊的 [安全性設定] 下方，展開 [本機原則]，然後選擇 [稽核原則]。  

3.  在 [結果] 窗格中，按兩下 [稽核登入事件]，確認選取 [成功] 核取方塊，然後選擇 [確定]。  

###  <a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 下列章節說明使用 [匯入軟體授權精靈] 將 Microsoft 和一般軟體授權資訊匯入 Configuration Manager 站台資料庫的必要程序。 當您從授權聲明檔案將軟體授權資訊匯入站台資料庫時，站台伺服器電腦帳戶需具備 NTFS 檔案系統與用來匯入軟體授權資訊之檔案共用的 [完全控制]  權限。  

> [!IMPORTANT]  
>  將軟體授權資訊匯入站台資料庫時，即會覆寫現有的軟體授權資訊。 請確定您搭配 [匯入軟體授權精靈] 使用的軟體授權資訊檔案，其中包含所有必要軟體授權資訊的完整清單。  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>若要將軟體授權資訊匯入 Asset Intelligence 類別目錄  

1.  在 [資產與合規性] 工作區中，選擇 [Asset Intelligence]。  

2.  在 [首頁] 索引標籤的 [Asset Intelligence] 群組中，選擇 [匯入軟體授權]。   

4.  在 [匯入]  頁面上，指定要匯入 Microsoft 大量授權 (MVLS) 檔案 (.xml 或 .csv) 或一般授權聲明檔案 (.csv)。 如需建立一般授權聲明檔案的詳細資訊，請參閱本主題稍後的 [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) 。  

    > [!WARNING]  
    >  若要下載 .csv 格式的 MVLS 檔案，以匯入 Asset Intelligence 類別目錄，請參閱 [Microsoft 大量授權服務中心](http://go.microsoft.com/fwlink/p/?LinkId=226547)。 若要存取這項資訊，您必須在該網站上註冊帳戶。 如需如何取得 .xml 格式之 MVLS 檔案的相關資訊，請連絡您的 Microsoft 客戶代表。  

5.  輸入授權聲明檔案的 UNC 路徑，或選擇 [瀏覽] 以選取網路共用資料夾和檔案。  

    > [!NOTE]  
    >  您應妥善保護共用的資料夾，以防止授權資訊檔案受到未經授權的存取，且執行精靈之電腦的電腦帳戶必須擁有包含授權匯入檔案之共用的 [完全控制] 權限。  

6. 完成精靈。  

###  <a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 您也可以手動建立以逗號分隔之檔案格式 (.csv) 的授權匯入檔案，將一般授權聲明匯入 Asset Intelligence 類別目錄中。  

> [!NOTE]  
>  雖然只有 [名稱] 、[發行者] 、[版本] 和 [EffectiveQuantity]  欄位必須包含資料，但授權匯入檔案第一個資料列上的所有欄位都必須輸入。 所有日期欄位應顯示為下列格式：月/日/年，例如 08/04/2008。  

Asset Intelligence 會使用產品名稱和產品版本來比對您在一般授權聲明中指定的產品，而不是發行者名稱。 您在一般授權聲明中使用的產品名稱必須與儲存在站台資料庫中的產品名稱完全相符。 Asset Intelligence 會採用一般授權聲明中指定的 **EffectiveQuantity** 數目來和 Configuration Manager 清查中找到的安裝產品數目進行比較。  

> [!TIP]  
>  若要取得儲存在 Configuration Manager 站台資料庫中的完整產品名稱清單，您可以在站台資料庫上執行下列查詢：SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE。  

 您可以指定產品的正確版本，或指定部分版本，例如僅指定主要版本。 下列範例產生的版本結果符合特定產品之一般授權聲明的版本項目。  

|一般授權聲明項目|比對站台資料庫項目|  
|-------------------------------------|------------------------------------|  
|名稱："MySoftware"，ProductVersion0:"2"|ProductName0: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.10.1234"|  
|名稱："MySoftware"，版本："2.05"|ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|名稱："MySoftware"，版本："2"<br /><br /> 名稱："MySoftware"，版本："2.05"|匯入期間發生錯誤。 若有多個項目符合相同的產品版本，則匯入會失敗。|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>若要使用 Microsoft Excel 建立一般授權聲明匯入檔案  

1.  開啟 Microsoft Excel，並建立新的試算表。  

2.  在新試算表的第一個資料列，輸入所有軟體授權資料欄位名稱。  

3.  在新試算表的第二個和後續資料列，輸入所需的軟體授權資訊。 請務必確認要匯入之每個軟體授權的所有必要軟體授權資料欄位，都有輸入後續資料列中。 試算表中輸入的軟體項目名稱，必須與執行硬體清查之後用戶端電腦的資源總管中顯示的軟體項目相同。  

4.  將檔案儲存成 .csv 格式。  

5.  將 .csv 檔案複製到用來將軟體授權資訊匯入 Asset Intelligence 類別目錄的檔案共用。  

6.  在 Configuration Manager 主控台中，使用 [匯入軟體授權精靈] 匯入新建立的 .csv 檔案。  

7.  執行 Asset Intelligence **授權 15A - 協力廠商軟體對帳報告**，確認授權資訊已成功匯入 Asset Intelligence 類別目錄。  

> [!NOTE]  
>  如需可用於測試用途的一般軟體授權檔案的範例，請參閱 [Example Asset Intelligence general license import file in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md) (System Center Configuration Manager 中的 Asset Intelligence 一般授權匯入檔範例)。  

#### <a name="sample-table-to-describe-software-licenses"></a>描述軟體授權的範例資料表  
 當建立一般授權聲明匯入檔案時，下表的資訊可用來描述要匯入 Asset Intelligence 類別目錄的軟體授權。  

|欄名|資料類型|必要|範例|  
|-----------------|---------------|--------------|-------------|  
|Name|最多 255 個字元|是|軟體項目|  
|發行者|最多 255 個字元|是|軟體發行者|  
|版本|最多 255 個字元|是|軟體項目版本|  
|語言|最多 255 個字元|是|軟體項目語言|  
|EffectiveQuantity|整數值|是|購買的授權數量|  
|PONumber|最多 255 個字元|否|採購單資訊|  
|ResellerName|最多 255 個字元|否|轉銷商資訊|  
|DateOfPurchase|日期值，格式如下：MM/DD/YYYY|否|授權採購日期|  
|SupportPurchased|位元值|否|0 或 1：輸入 0 表示 Yes，輸入 1 表示 No|  
|SupportExpirationDate|日期值，格式如下：MM/DD/YYYY|否|購買支援的結束日期|  
|註解|最多 255 個字元|否|選擇性註解|  

###  <a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 下列為 Asset Intelligence 提供的維護工作：  

-   **使用清查資訊檢查應用程式標題**：確認軟體清查中回報的軟體項目與 Asset Intelligence 類別目錄中的軟體項目一致。 預設會啟用這項工作並排程於星期六凌晨 12:00 之後、 上午 5:00 之前執行。 這項維護工作僅適用於 Configuration Manager 階層的頂層站台。  

-   **摘述已安裝的軟體資料**：提供在 [資產與合規性] 工作區 [Asset Intelligence] 節點下 [已清查的軟體] 節點中顯示的資訊。 執行工作時，Configuration Manager 會收集所有已清查的主要站台軟體項目計數。 預設會啟用這項工作並排程於每天凌晨 12:00 之後、 上午 5:00 之前執行。 這項維護工作僅適用於主要站台。  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>若要設定 Asset Intelligence 維護工作  

1.  在 Configuration Manager 主控台中，選擇 [管理] > [站台設定] > [站台]。  

3.  選取要在其中設定 Asset Intelligence 維護工作的站台。  

4.  在 [首頁] 索引標籤的 [設定] 群組中，選擇 [站台維護]。 選取一項工作，然後選擇 [編輯] 修改設定。 

    我們建議，您將時段設為站台的離峰時間。 該時段即為可執行工作的時間間隔。 您可在 [工作內容]  對話方塊中以 [由此開始]  和 [最晚的開始時間]  來指定時段。  

    您可以選取目前的日期，並將 [由此開始]  時間設為目前時間過後幾分鐘，以立即啟動工作。  

7.  選擇 [確定] 儲存設定。 現在，即會根據排程來執行工作。  

    > [!NOTE]  
    >  若第一次嘗試時無法執行工作，Configuration Manager 會嘗試重新執行工作直到工作執行成功，或直到可執行工作的時段已過為止。  
