---
title: "管理更新目錄 | Microsoft Docs"
description: "管理 System Center Updates Publisher 的軟體更新目錄"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 7451d699e0e5e146b0538a57deca595188d113bf
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>在 Updates Publisher 中管理軟體更新目錄

*適用於：System Center Updates Publisher*

使用 [目錄工作區] 來管理軟體更新目錄。 這包括新增新的目錄、管理現有的目錄訂閱，以及從目錄將更新的相關資訊匯入至 Updates Publisher 存放庫。

軟體更新目錄包含由非 Microsoft 的其他組織所建立的相關更新資訊。 其他組織包含您本身的組織，以及已向 Microsoft 註冊其目錄的第三方軟體廠商。 軟體廠商的已註冊目錄稱為「合作夥伴目錄」。 由您所建立且未向 Microsoft 註冊的目錄稱為「使用者」目錄。

## <a name="add-software-update-catalogs"></a>新增軟體更新目錄
您必須將更新目錄新增至 Updates Publisher，才能管理其包含的更新。 當您新增一個目錄時，Updates Publisher 會：
-   將訂閱建立至該目錄，使它能檢查針對該目錄的更新。
-   將目錄新增至 [目錄工作區] 的 [我的軟體更新目錄] 視窗中的清單。  

每個已訂閱目錄的相關資訊可在主控台中取得。 資訊包含下載 URL 或位置、建立目錄的公司或組織名稱，以及最後一次匯入或修改的時間。

Updates Publisher 可在每次啟動時自動檢查訂閱以確認是否有變更。 這是以[進階選項](/sccm/sum/tools/updates-publisher-options#advanced)進行設定。 設定之後，Updates Publisher 會參考訂閱的下載 URL 或位置資訊，並在目錄自上次匯入存放庫後出現變更的情況下警示您。

若要手動檢查目錄更新，請從 [我的軟體更新目錄] 清單選取目錄，然後從功能區選擇 [重新整理]。

除了新增目錄，以及檢視已訂閱目錄的相關資訊之外，您還可以：
-  「編輯」使用者目錄的資訊。
-  從 Updates Publisher「刪除」 (移除) 目錄。
-  從目錄將更新「匯入」Updates Publisher 存放庫。 當您匯入更新時，會匯入該目錄中的所有更新。 之後，您可以在 [更新工作區] 中檢視更新，並在其中選取更新並將更新發行至更新伺服器。

> [!NOTE]   
> 從 Updates Publisher 刪除目錄，會導致該目錄中的更新從您的存放庫中移除。 這不會影響您已經發行至更新伺服器的更新。 若要從更新伺服器移除已不在存放庫中的更新，請參閱[使未參考的軟體更新到期](/sccm/sum/tools/updates-publisher-options#expire-unreferenced-software-updates)。

## <a name="manage-update-catalogs"></a>管理更新目錄
您可以在 [目錄工作區] 的 [我的軟體更新目錄] 視窗中檢視您已匯入的清單目錄。 從此工作區，您可以：

-   **新增合作夥伴目錄**：使用下列其中一項來尋找新的合作夥伴目錄：

    -   在主控台中，移至 [更新工作區] > [概觀]。 在 [開始使用] 視窗中，選擇 [新增合作夥伴軟體更新目錄]。

    -   在主控台中，移至 [目錄工作區] > [我的目錄]。 然後，從功能區選擇 [新增目錄]。

-   **新增使用者目錄**：在主控台中，移至 [目錄工作區] > [我的目錄]。 然後，從功能區選擇 [新增目錄]。 除了 .cab 檔案的位置之外，您必須指定發行者、名稱和描述來識別目錄。


-   **檢查目錄的更新**：選取一或多個目錄，然後從功能區選擇 [重新整理]。

-   **編輯使用者目錄**：選取「使用者」目錄，然後從功能區選擇 [編輯]。 您可以接著修改使用者定義的屬性。

-   **刪除目錄**：選取一或多個目錄，然後從功能區選擇 [移除]。 這會從您的 Updates Publisher 存放庫移除該目錄、您的訂閱，以及那些目錄中的更新。

-   **將目錄中的更新新增至您的存放庫**：從功能區選擇 [匯入] 來啟動 [匯入目錄] 精靈。 如需詳細資訊，請參閱[匯入更新](#import-updates)

## <a name="import-updates"></a>匯入更新
當您匯入目錄時，Updates Manager 會將該目錄中的更新新增至 Updates Publisher 存放庫。 匯入更新後，您可以將它們發行至您的更新伺服器，以供受管理裝置使用。

### <a name="to-import-updates"></a>匯入更新
1.  若要啟動 [匯入目錄] 精靈，請在下列其中一個工作區中，從功能區選擇 [匯入]：

    -   目錄工作區

    -   更新工作區

2.  在 [匯入類型] 頁面上，選取一或多個已新增至 Updates Publisher 的目錄，或指定尚未新增為訂閱的目錄路徑。 選擇 [下一步] 以檢視摘要畫面，並在準備好時，選擇 [下一步] 以開始匯入。

3.  在 [安全性警告 – 目錄驗證] 視窗上檢閱目錄憑證，並在準備好時，選擇 [接受] 以匯入更新。

    > [!CAUTION]    
    > 僅接受來自您所信任之發行者的更新。 當搜尋更新時，來自不受信任之發行者的軟體更新可能會危害用戶端電腦。

    >  如果您不再信任某個發行者，請將該發行者從信任的發行者清單中移除。 若要尋找接受目錄的詳細資訊，請按一下 [安全性警告 – 目錄驗證] 對話方塊中的 [顯示詳細資訊]。

    如果您選擇一律接受某個發行者的目錄，該發行者會新增至[信任的發行者清單](/sccm/sum/tools/updates-publisher-options#trusted-publishers)。 您可以將此清單做為 Updates Publisher 選項進行檢閱與編輯。

4.  當更新已存在於存放庫中，且符合下列其中一種情況時，匯入程序會略過該更新的匯入：

    -   更新從上次匯入後並未變更。

    -   更新已編輯，並具有新的數位雜湊。 編輯更新可防止新的更新覆寫原始的更新，因為這麼做可能會覆寫您已經部署的變更。

5.  在 [確認] 頁面上檢閱匯入結果。

6.  按一下 [關閉] 以完成精靈。 您現在可以在 Updates Workspace 中檢閱此目錄的更新。

## <a name="next-steps"></a>後續步驟
匯入更新之後，常見的動作包括︰
-   [管理更新](/sccm/sum/tools/manage-updates-with-updates-publisher)以對它們進行配套及指派，並將它們部署至您的更新伺服器。
-   [建立適用性規則](/sccm/sum/tools/updates-publisher-applicability-rules)，以協助判斷更新部署至更新伺服器的時機。
