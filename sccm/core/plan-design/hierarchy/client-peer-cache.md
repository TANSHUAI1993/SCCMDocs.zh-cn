---
title: "用戶端對等快取 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager 部署內容時，針對用戶端內容來源位置使用對等快取。"
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 89fcd16887ae77299f9d18472ee6a1ba56794eca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Configuration Manager 用戶端的對等快取

*適用於：System Center Configuration Manager (最新分支)*

從 System Center Configuration Manager 版本 1610 開始，您可以使用**對等快取**，以協助管理將內容部署至遠端位置的用戶端。 對等快取是一個內建的 Configuration Manager 解決方案，可讓用戶端直接將其本機快取的內容與其他用戶端共用。   

> [!TIP]  
> 對等快取和用戶端資料來源儀表板，都是在版本 1610 引進的發行前版本功能。 若要啟用它們，請參閱[使用更新的發行前版本功能](/sccm/core/servers/manage/pre-release-features)。

## <a name="overview"></a>概觀
對等快取用戶端是可以使用對等快取的 Configuration Manager 用戶端。 具有可與其他用戶端共用之內容的對等快取用戶端為對等快取來源。
 -  您可以使用用戶端設定，讓使用端能夠使用對等快取。
 -  若要以對等快取來源的形式共用內容，對等快取用戶端必須：
    -  已加入網域。 不過，未加入網域的用戶端仍可以從已加入網域的對等快取來源取得內容。
    -  為正在尋找內容之用戶端的目前界限群組成員。 當用戶端使用後援來搜尋鄰近界限群組的內容時，鄰近界限群組中的對等快取用戶端不會包含於可用內容來源位置的集區中。 如需目前和鄰近界限群組的詳細資訊，請參閱[界限群組](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups)。
 - Configuration Manager 用戶端快取中保存的每種內容類型，都可利用對等快取提供給其他的用戶端。
 -  對等快取不會取代其他解決方案 (例如 BranchCache) 的使用，而是可並行運作來提供您更多選項以擴充傳統內容部署解決方案。 這是一個不依賴 BranchCache 的自訂解決方案，所以就算不啟用或使用 Windows BranchCache，這個解決方案仍能運作。

### <a name="operations"></a>作業

將啟用對等快取的用戶端設定部署至集合之後，該集合的成員就能做為同一個界限群組中其他用戶端的對等內容來源：
 -  以對等內容來源運作的用戶端會向其管理點提交可用的快取內容清單。
 -  然後，當該界限群組中的下一個用戶端要求該內容時，就會傳回具有該內容的每個對等快取來源以做為潛在的內容來源，以及該界限群組中的發佈點與其他內容來源位置。
 -  針對每個標準作業程序，搜尋內容的用戶端會從提供給它的來源集區中選取一個內容來源，然後繼續嘗試取得內容。

> [!NOTE]
> 如果對內容的鄰近界限群組發生了後援，就不會將來自鄰近界限群組的對等快取內容來源位置新增至用戶端潛在內容來源位置的集區。  


雖然您可以讓所有用戶端以對等快取來源的身分參與，但最理想的做法是只選擇最適合作為對等快取來源的用戶端。  您可以根據用戶端的底座類型、磁碟空間、網路連線能力及更多項目來評估用戶端的適用性。 如需可協助您選取最適合用於對等快取的最佳用戶端詳細資訊，請參閱[這個由 Microsoft 顧問所維護的部落格](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/)。

**限制存取對等快取來源**  
從 1702 版開始，當對等快取來源電腦符合下列任一條件時，對等快取來源電腦將會拒絕內容要求︰  
  -  處於電力偏低模式。
  -  CPU 負載會在要求內容時超過 80%。
  -  磁碟 I/O 的 *AvgDiskQueueLength* 超過 10。
  -  無法再連線至電腦。   

當您使用 System Center Configuration Manager SDK 時，可以使用對等來源功能的用戶端設定伺服器 WMI 類別來進行這些設定 (*SMS_WinPEPeerCacheConfig*)。

電腦拒絕內容要求時，提出要求的電腦會繼續在其可用內容來源位置集區中的替代來源搜尋內容。   



### <a name="monitoring"></a>監視   
為了協助您了解對等快取的用法，您可以檢視 [用戶端資料來源] 儀表板。 請參閱[用戶端資料來源儀表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。

從 1702 版開始，您可以使用下列三份報告來檢視對等快取使用情況。 在主控台中，移至 [監視] >  [報告] > [報告]。 所有報告的類型都是 [軟體發佈內容]：
1.  **對等快取來源內容拒絕**：  
您可以使用此報告來了解界限群組中的對等快取來源拒絕內容要求的頻率。
 - **已知問題︰**向下鑽研 *MaxCPULoad* 或 *MaxDiskIO* 之類的結果時，您可能會收到錯誤，暗示找不到報告或詳細資料。 若要解決這個問題，請使用下列兩種報告，直接顯示結果。

2. **對等快取來源內容拒絕條件**：  
您可以使用此報告來了解所指定界限群組或拒絕類型的詳細拒絕資料。 您可以指定

  - **已知問題︰**您無法從可用的參數中選取，而必須改為手動輸入。 如同在第一份報告中所見，輸入 [界限群組名稱] 和 [拒絕類型] 的值。 例如，您可能會在 [拒絕類型] 輸入 *MaxCPULoad* 或 *MaxDiskIO*。

3. **對等快取來源內容拒絕詳細資料**：   
  您可以使用此報告來了解所要求但遭到拒絕的內容。

 - **已知問題︰**您無法從可用的參數中選取，而必須改為手動輸入。 如同在第一份報告 (對等快取來源內容拒絕) 中所見，輸入 [拒絕類型] 的值，然後針對您需要詳細資訊的內容來源輸入其 [資源識別碼]。  尋找內容來源的資源識別碼︰  

    1. 尋找如同第 2 份報告 (依條件拒絕對等快取來源內容) 結果中的 [對等快取來源] 所示的電腦名稱。  
    2. 接下來，移至 [資產與合規性] > [裝置]，然後搜尋該電腦的名稱。 使用 [資源識別碼] 欄中的值。  


## <a name="requirements-and-considerations-for-peer-cache"></a>對等快取的需求與考量
-   在任何支援做為 Configuration Manager 用戶端的 Windows 作業系統上都支援對等快取。 非 Windows 作業系統不支援對等快取。

-   用戶端只能從其目前界限群組中的對等快取用戶端傳輸內容。

-   在 1706 版之前，用戶端使用對等快取所在的每個站台都必須設有[網路存取帳戶](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account)。 從 1706 版開始，該帳戶已非必要，唯一的例外是：  當用戶端使用對等快取從軟體中心取得並執行工作順序，而該工作順序會將用戶端重新開機至 WinPE 時。  在此情況下，用戶端在 WinPE 時仍需要網路存取帳戶，才能存取對等快取來源以取得內容。

    當有需要網路存取帳戶時，對等快取來源電腦會使用此帳戶來驗證對等的下載要求，而針對此目的，只需要網域使用者權限。

-   因為目前的對等快取內容來源界限是根據該用戶端的上次硬體清查提交所決定，所以，若用戶端漫遊至位於不同界限群組的網路位置，基於對等快取的目的，仍然可能被視為是其先前界限群組的成員。 這會導致提供給用戶端的對等快取內容來源不在其中繼網路位置上。 我們建議您排除有此設定傾向的用戶端，不要讓它以對等快取來源的身分參與。

## <a name="to-configure-client-peer-cache-client-settings"></a>設定用戶端對等快取的用戶端設定
1.  在 Configuration Manager 主控台中，移至 [系統管理] > [用戶端設定]，然後開啟您要使用的裝置用戶端設定物件。 您也可以修改 [預設用戶端設定] 物件。
2.  從可用的設定清單中，選擇 [用戶端快取設定]。
3.  將 [在完整作業系統中啟用 Configuration Manager 用戶端以共用內容] 設為 [是]。
4.  設定下列設定來定義您想要用於對等快取的連接埠：  
  -  **用於初始網路廣播的連接埠**
  -  **為用戶端對等通訊啟用 HTTPS**
  -  **用於從對等節點下載內容的連接埠 (HTTP/HTTPS)**

在為對等快取啟用的每一部電腦上，如果 Windows 防火牆正在使用中，Configuration Manager 就會設定它，以便使用您設定的連接埠。
