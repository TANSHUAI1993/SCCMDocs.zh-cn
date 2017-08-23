---
title: "使用 Asset Intelligence | Microsoft Docs"
description: "在 System Center Configuration Manager 中執行一般的 Asset Intelligence 工作。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 17168e26f13340847928f6e3623115cd4b55997b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-asset-intelligence-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中使用 Asset Intelligence

*適用對象：System Center Configuration Manager (最新分支)*

本主題包含的資訊可協助您管理 System Center Configuration Manager 階層中的一般 Asset Intelligence 工作︰  

##  <a name="BKMK_ViewInformation"></a> 檢視 Asset Intelligence 資訊  
 您可以在 [Asset Intelligence]  首頁上和 Asset Intelligence 報告中檢視 Asset Intelligence 資訊。  

###  <a name="BKMK_AssetIntelligenceHomePage"></a> Asset Intelligence 首頁  
 [Asset Intelligence]  首頁會顯示 Asset Intelligence 類別目錄資訊的摘要儀表板。 在首頁上，您可以檢視類別目錄同步處理和已清查之軟體狀態的相關資訊。 [Asset Intelligence]  首頁分為下列各區段：  

-   **類別目錄同步處理**：提供下列項目的相關資訊：是否啟用 Asset Intelligence、Asset Intelligence 同步處理點的目前狀態、同步處理排程、是否匯入客戶授權聲明、上次更新狀態的時間、下次排定的更新時間，以及安裝 Asset Intelligence 同步處理點站台系統之後發生的變更數目。  

    > [!NOTE]  
    >  只有在已安裝 Asset Intelligence 同步處理點站台系統角色時，才會顯示 [Asset Intelligence]  首頁的 Asset Intelligence 類別目錄同步處理區段。  

-   **已清查的軟體狀態**：提供由 Microsoft 所識別、系統管理使用者所識別、擱置線上識別或無法辨識但未擱置的已清查軟體、軟體類別目錄以及軟體系列的計數和百分比。 以表格格式顯示的資訊會顯示各項計數，而以圖表顯示的資訊會顯示各項百分比。  

 使用下列程序，在 [Asset Intelligence]  首頁上檢視 Asset Intelligence 資訊。  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>在 Asset Intelligence 首頁上檢視 Asset Intelligence 資訊  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] 。 即會顯示 Asset Intelligence 報告。  

###  <a name="BKMK_AssetIntelligenceReports"></a> Asset Intelligence 報告  
 有超過 60 份的 Asset Intelligence 報告顯示 Asset Intelligence 所收集的資訊。 這當中有許多報告可連結至更特定的報告，供您在其中查詢一般資訊，並向下鑽研至更詳細的資訊。 Asset Intelligence 報告位於 Configuration Manager 主控台之 [監視] 工作區的 [報告] 節點下。 這份報告提供硬體、授權管理和軟體的相關資訊。 如需 Configuration Manager 報告的詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。  

> [!NOTE]  
>  Asset Intelligence 報告中顯示的已安裝軟體項目數量及授權資訊的精確度，可能會與已安裝的實際軟體項目數目或環境中已使用的授權數量有所不同，因為與清查企業環境中已安裝軟體項目之軟體授權資訊的複雜相依性和限制。 Asset Intelligence 報告不應該作為判斷購買的軟體授權相容性的唯一來源。  

 使用下列程序，透過 Asset Intelligence 報告來檢視 Asset Intelligence 資訊。  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>使用 Asset Intelligence 報告來檢視所收集的 Asset Intelligence 資訊  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，依序展開 [報告] 和 [報告] ，然後按一下 [Asset Intelligence] 。 即會顯示 Asset Intelligence 報告。  

    > [!WARNING]  
    >  如果 [報告]  節點下沒有任何報告資料夾，請確認您已設定報告。 如需詳細資料，請參閱 [Configuring reporting in System Center Configuration Manager](../../../../core/servers/manage/configuring-reporting.md) (在 System Center Configuration Manager 中設定報告)。  

3.  選取您要執行的 Asset Intelligence 報告，然後在 [首頁]  索引標籤的 [報告群組]  群組中按一下 [執行] 。  

##  <a name="BKMK_SynchronizeTheCatalog"></a> 同步處理 Asset Intelligence 類別目錄  
 您可以同步處理本機 Asset Intelligence 類別目錄與 System Center Online，來擷取最新的軟體項目分類。 當您手動要求與 System Center Online 的類別目錄同步處理時，可能需要 15 分鐘或更長的時間才能完成與 System Center Online 的同步處理程序。 Configuration Manager 會使用同步處理成功完成時的目前時間來更新 [Asset Intelligence] 首頁上的 [上次成功更新] 設定。  

> [!NOTE]  
>  必須先使用這些程序來安裝 Asset Intelligence 同步處理點站台系統角色。 如需安裝 Asset Intelligence 同步處理點的資訊，請參閱 [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) (在 System Center Configuration Manager 中設定 Asset Intelligence)。  

 使用下列程序建立 Asset Intelligence 類別目錄的同步處理排程。  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>建立 Asset Intelligence 類別目錄的同步處理排程  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [同步處理] ，然後按一下 [排程同步處理] 。  

4.  在 [Asset Intelligence 同步處理點排程]  對話方塊中，選取 [啟用依排程同步處理] ，然後設定簡單或自訂排程。  

5.  按一下 [確定]  儲存變更。  

    > [!NOTE]  
    >  如需同步處理排程 (包含下一個排程的同步處理) 的相關資訊，請參閱階層最上層站台之 [資產與相容性]  工作區中的 [Asset Intelligence]  節點。  

 使用下列程序手動同步處理 Asset Intelligence 類別目錄。  

> [!WARNING]  
>  System Center Online 只會在 12 小時的期間內接受一個手動同步處理要求。  

###  <a name="BKMK_ManuallySynchronizeCatalog"></a> 手動同步處理 Asset Intelligence 類別目錄  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，依序按一下 [同步處理] 、[同步處理 Asset Intelligence 類別目錄] 和 [確定] 。  

##  <a name="BKMK_CustomizeCatalog"></a> 自訂 Asset Intelligence 類別目錄  
 接收自 System Center Online 的 Asset Intelligence 類別目錄分類資訊以唯讀權限儲存在站台資料庫中，無法進行修改或刪除。 不過，您可以建立、修改和刪除自訂軟體類別、軟體系列、軟體標籤和硬體需求類別目錄資訊。 然後，您可以使用自訂分類資料，而不是 System Center Online 針對現有或使用者定義軟體項目資訊所提供的資訊。 當您變更或新增分類資訊時，會將類別目錄資訊視為由使用者所定義。 使用者定義的分類資訊儲存在與已驗證之類別目錄資訊不同的資料庫資料表中。  

###  <a name="BKMK_SoftwareCategories"></a> 軟體類別  
 Asset Intelligence 軟體類別可用來廣泛分類已清查的軟體項目，也可作為更特定之軟體系列的高階分組。 例如，軟體類別可能是能源公司，而該軟體類別內的軟體系列可能是石油與天然氣或水力電氣。 Asset Intelligence 類別目錄中預先定義許多軟體類別，並且建立其他使用者定義的類別，以進一步定義已清查的軟體。 所有預先定義之軟體類別的驗證狀態一律是 [已驗證] ，而新增至 Asset Intelligence 類別目錄的自訂軟體類別資訊則是 [使用者定義] 。  

 使用下列程序建立使用者定義的軟體類別。  

##### <a name="to-create-a-user-defined-software-category"></a>建立使用者定義的軟體類別  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] ，然後按一下 [類別目錄] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立軟體類別] 。  

4.  在 [一般]  頁面上，輸入新軟體類別的名稱，並選擇性地輸入描述。  

    > [!NOTE]  
    >  所有新自訂軟體類別的驗證狀態一律設為 [使用者定義] 。  

     按一下 [下一步] 。  

5.  在 [摘要]  頁面上，檢閱設定，然後按一下 [下一步] 。  

6.  在 [完成]  頁面上，按一下 [關閉]  結束精靈。  

###  <a name="BKMK_SoftwareFamilies"></a> 軟體系列  
 Asset Intelligence 軟體系列可用來進一步定義軟體類別內已清查的軟體項目。 例如，軟體類別可能是能源公司，而該軟體類別內的軟體系列可能是石油與天然氣或水力電氣。 Asset Intelligence 類別目錄中預先定義許多軟體系列，並且建立其他使用者定義的系列，以定義已清查的軟體。 所有預先定義之軟體系列的驗證狀態一律是 [已驗證] ，而新增至 Asset Intelligence 類別目錄的自訂軟體系列資訊則是 [使用者定義] 。  

 使用下列程序建立使用者定義的軟體系列。  

##### <a name="to-create-a-user-defined-software-family"></a>建立使用者定義的軟體系列  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] ，然後按一下 [類別目錄] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立軟體系列] 。  

4.  在 [一般]  頁面上，輸入新軟體系列的名稱，並選擇性地輸入描述。  

    > [!NOTE]  
    >  所有新自訂軟體系列的驗證狀態一律設為 [使用者定義] 。  

5.  在 [摘要]  頁面上，檢閱設定，然後按一下 [下一步] 。  

6.  在 [完成]  頁面上，按一下 [關閉]  結束精靈。  

###  <a name="BKMK_SoftwareLabels"></a> 軟體標籤  
 Asset Intelligence 自訂軟體標籤可讓您建立篩選器以群組軟體項目，並使用 Asset Intelligence 報告來檢視它們。 例如，您可以建立稱為「共享軟體」的軟體標籤，並建立它與一些應用程式的關聯性，然後執行報告，以顯示具有共享軟體之軟體標籤的所有標題。 新增至 Asset Intelligence 類別目錄之所有自訂軟體標籤的驗證狀態是 [使用者定義]  。  

 使用下列程序建立使用者定義的自訂標籤。  

##### <a name="to-create-a-user-defined-software-label"></a>建立使用者定義的軟體標籤  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] ，然後按一下 [類別目錄] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立軟體標籤] 。  

4.  在 [一般]  頁面上，輸入新軟體系列的名稱，並選擇性地輸入描述。  

    > [!NOTE]  
    >  所有新自訂軟體標籤的驗證狀態一律設為 [使用者定義] 。  

5.  在 [摘要]  頁面上，檢閱設定，然後按一下 [下一步] 。  

6.  在 [完成]  頁面上，按一下 [關閉]  結束精靈。  

###  <a name="BKMK_HardwareRequirements"></a> 硬體需求  
 硬體需求資訊可協助您確認電腦符合軟體項目的硬體需求之後，再將它們設為軟體部署的目標。 Asset Intelligence 類別目錄提供許多預先定義的硬體需求，您也可以建立新的使用者定義硬體需求資訊，以符合自訂需求。 所有預先定義之硬體需求的驗證狀態一律是 [已驗證] ，而新增至 Asset Intelligence 類別目錄的使用者定義硬體需求資訊則是 [使用者定義] 。  

> [!IMPORTANT]  
>  Configuration Manager 主控台中顯示的硬體需求是擷取自本機電腦上的 Asset Intelligence 類別目錄，而不是根據 System Center 2012 Configuration Manager 用戶端中的已清查軟體項目資訊。 硬體需求的資訊不會與 System Center Online 同步處理程序一起更新。 針對沒有相關聯硬體需求的已清查軟體，您可以建立使用者定義的硬體需求。  

 使用下列程序建立使用者定義的硬體需求。  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>建立使用者定義的硬體需求  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] ，然後按一下 [硬體需求] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立硬體需求] 。  

4.  在 [一般]  頁面上，輸入下列資訊︰  

    1.  **軟體項目**：指定與硬體需求相關聯的軟體項目。 軟體項目不能存在於 Asset Intelligence 類別目錄中。  

    2.  **驗證狀態**：列出驗證狀態為 [使用者定義]  的硬體需求。 您無法修改這項設定。  

    3.  **CPU 下限 (MHz)**：指定軟體項目所需的最低處理器速度 (MHz)。  

    4.  **RAM 下限 (KB)**：指定軟體項目所需的最小 RAM (KB)。  

    5.  **磁碟空間下限 (KB)**：指定軟體項目所需的最小可用硬碟空間 (KB)。  

    6.  **磁碟大小下限 (KB)**：指定軟體項目所需的最小可用硬碟大小 (KB)。  

     按一下 [下一步] 。  

5.  在 [摘要]  頁面上，檢閱設定，然後按一下 [下一步] 。  

6.  在 [完成]  頁面上，按一下 [關閉]  結束精靈。  

###  <a name="BKMK_ModifyCategorization"></a> 修改已清查軟體的分類資訊  
 使用特定分類資訊 (例如產品名稱、廠商、軟體類別和軟體系列) 來設定 Asset Intelligence 類別目錄中的預先定義軟體。 預先定義的分類資訊不符合您的需求時，您可以修改軟體項目之內容中的資訊。 修改預先定義之軟體的分類資訊時，軟體的驗證狀態會從 [已驗證]  變更為 [使用者定義] 。  

> [!IMPORTANT]  
>  只能修改最上層站台上的分類資訊。  

 使用下列程序修改已清查軟體的分類資訊。  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>修改軟體項目的分類  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] ，然後按一下 [已清查的軟體] 。  

3.  選取軟體項目，或選取您要修改分類的多個軟體項目。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 [一般]  索引標籤上，您可以修改下列分類資訊：  

    -   **產品名稱**：指定已清查軟體項目的名稱。  

    -   **廠商**：指定開發已清查軟體項目的廠商名稱。  

    -   **類別**：指定目前指派給已清查軟體項目的軟體類別。  

    -   **系列**：指定目前指派給已清查軟體項目的軟體系列。  

6.  按一下 [確定]  儲存變更。  

 使用下列程序，將軟體還原為原始分類資訊。  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>將軟體的分類資訊還原為原始設定  
 Configuration Manager 會將取自 System Center Online 的分類資訊儲存至資料庫中。 無法刪除該資訊。 修改資訊之後，您可以將分類資訊還原回 System Center Online 分類。 不在 Asset Intelligence 類別目錄中的已清查軟體也可以還原回原始設定。  

 使用下列程序，將分類資訊還原為原始設定。  

##### <a name="to-revert-categorization-information-to-original-settings"></a>將分類資訊還原為原始設定  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] ，然後按一下 [已清查的軟體] 。  

3.  選取軟體項目，或選取您要還原為原始設定的多個軟體項目。 只能還原具有 [使用者定義]  狀態的軟體。  

    > [!TIP]  
    >  按一下要依驗證狀態排序的 [狀態]  資料行。 排序可讓您看到所有依驗證狀態的軟體，以及快速選取要還原為原始設定的多個項目。  

4.  在 [首頁]  索引標籤的 [產品]  群組中，按一下 [還原] 。  

5.  按一下 [是]  ，將軟體還原為原始分類資訊。  

6.  還原 Asset Intelligence 類別目錄中軟體的分類資訊時，驗證狀態會從 [使用者定義]  變更為 [已驗證] 。 還原不在類別目錄中的軟體時，驗證狀態會從 [使用者定義]  變更為 [未分類] 。  

##  <a name="BKMK_RequestCatalogUpdate"></a> 要求未分類軟體項目的類別目錄更新  
 未分類軟體項目資訊可以提交給 System Center Online，以進行研究和分類。 提交未分類的軟體項目之後，若有客戶對相同軟體項目提出 4 個以上的分類要求時，研究人員會識別、分類，然後將軟體項目分類資訊提供給所有使用 System Center Online 服務的客戶。 Microsoft 會將最高的分類優先順序提供給分類要求數最多的軟體項目。 自訂軟體和企業營運應用程式不太可能會收到分類，因此最佳做法是不要將這類軟體項目傳送給 Microsoft 進行分類。  

 將軟體項目資訊提交給 System Center Online 進行分類時，下列情況適用：  

-   基本軟體項目資訊傳輸至 System Center Online，而且可以在提交之前檢閱要分類的軟體項目資訊。  

-   永遠不會傳輸軟體授權資訊。  

-   所有上傳的軟體項目都會公開作為 System Center Online 類別目錄的一部分，而且可供其他客戶進行下載。  

-   軟體項目的來源不是儲存在 System Center Online 類別目錄中。 不過，不應該提交包含機密或專屬資訊的應用程式標題，供 System Center Online 進行分類。  

> [!NOTE]  
>  如需 Asset Intelligence 隱私權資訊的詳細資訊，請參閱 [Security and privacy for Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md) (System Center Configuration Manager 中 Asset Intelligence 的安全性與隱私權)。  

 使用下列程序，從 System Center Online 要求 Asset Intelligence 類別目錄軟體項目分類。  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>要求未分類軟體項目的類別目錄更新  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] ，然後按一下 [已清查的軟體] 。  

3.  選取產品名稱，或選取要提交給 System Center Online 進行分類的多個產品名稱。 只有未分類的已清查軟體項目才能提交給 System Center Online 進行分類。 如果系統管理員已分類已清查的軟體項目而導致使用者定義的狀態，您必須在已清查的軟體項目上按一下滑鼠右鍵，然後按一下 [還原]  先將軟體項目還原為 [未分類]  狀態，再將它提交給 System Center Online 進行分類。  

    > [!NOTE]  
    >  Configuration Manager 一次最多可以處理 100 個軟體項目來進行分類。 如果您選取 100 個以上的軟體項目，則只會處理前 100 個軟體項目。 您必須以小於 100 的批次來選取其餘的軟體項目進行分類。  

    > [!TIP]  
    >  按一下要依驗證狀態排序的 [狀態]  資料行。 這可讓您看到所有未分類的產品名稱，並快速地選取要提交進行分類的多個項目。  

4.  在 [首頁]  索引標籤的 [產品]  群組中，按一下 [要求類別目錄更新] 。  

5.  檢閱 System Center Online 分類提交隱私權訊息。 按一下 [詳細資料]  檢視將傳送給 System Center Online 的資訊。  

6.  選取 [我已經閱讀並了解此訊息] ，然後按一下 [確定]  允許提交選取的軟體項目進行分類。  

7.  確認提交給 System Center Online 進行分類的已清查軟體產品名稱狀態已從 [未分類]  變更為 [擱置] 。  

    > [!NOTE]  
    >  提交給 System Center Online 進行分類的軟體，其在管理中心網站上的驗證狀態為 [擱置]  ，但在子主要站台上仍會顯示 [未分類]  驗證狀態。  

##  <a name="BKMK_ResolveSoftwareDetails"></a> 解決軟體詳細資料衝突  
 從 System Center Online 接收到與現有軟體詳細資料資訊衝突的剛更新軟體分類詳細資料之後，即可選擇如何解決衝突。 具有目前衝突之軟體的驗證狀態為 [可更新] 。 解決軟體詳細資料衝突之後，會根據您指定的設定，將軟體分類資訊保留在 Asset Intelligence 類別目錄中。 除非在解決衝突之後變更 System Center Online 值，否則相同的軟體分類值不會再發生軟體詳細資料衝突。  

 使用下列程序解決軟體詳細資料衝突。  

#### <a name="to-resolve-a-software-details-conflict"></a>解決軟體詳細資料衝突  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [Asset Intelligence] ，然後按一下 [已清查的軟體] 。  

3.  檢閱處於 [可更新]  狀態之軟體項目的 [狀態]  資料行。  

4.  選取您需要解決衝突的軟體項目，並在 [首頁]  索引標籤的 [產品]  群組中，然後按一下 [解決衝突] 。  

5.  檢閱下列資訊：  

    -   **本機值**：指定 Asset Intelligence 類別目錄中與較新 System Center Online 軟體分類詳細資料發生衝突的現有軟體分類資訊。  

    -   **下載的值**：指定衝突的 Asset Intelligence 類別目錄軟體分類資訊的新 System Center Online 軟體分類資訊。  

6.  選取下列其中一個設定來解決軟體詳細資料衝突：  

    -   **不變更本機編輯類別目錄資訊值**：保留現有 Asset Intelligence 類別目錄軟體分類資訊，來解決軟體詳細資料衝突。 當您選取這個設定時，軟體項目狀態會從 [可更新]  變更為 [使用者定義] 。  

    -   **使用下載的 System Center Online 值覆寫本機編輯類別目錄資訊**：使用取自 System Center Online 的新資訊來覆寫現有 Asset Intelligence 類別目錄軟體分類資訊，來解決軟體詳細資料衝突。 當您選取這個設定時，軟體項目狀態會從 [可更新]  變更為 [已驗證] 。  

     按一下 [確定]  儲存衝突解決方法。  
