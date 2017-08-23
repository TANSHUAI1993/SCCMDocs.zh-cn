---
title: "管理更新 | Microsoft Docs"
description: "管理您使用 System Center Updates Publisher 部署並建立的更新"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 1d6c3b1db14867bdbc5cae8ded099d9024a79549
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-software-updates-in-updates-publisher"></a>在 Updates Publisher 中管理軟體更新

*適用於：System Center Updates Publisher*     

在 System Center Updates Publisher 中，您可以使用 [更新工作區] 來管理您匯入到存放庫的軟體更新與配套。  

管理工作包含複製及編輯更新與配套、設定更新與配套的到期日或將其重新啟用，以及將更新與配套指派到發行集。 您也可以匯出自訂類別目錄，以搭配其他 Updates Publisher 安裝使用。

取得您可以管理的更新：
-  [新增更新類別目錄](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs)到您的 Updates Publisher 安裝
-  將更新從該類別目錄[匯入](/sccm/sum/tools/updates-publisher-catalogs#import-updates)到您的存放庫。

您也可以[建立自己的更新](/sccm/sum/tools/create-updates-with-updates-publisher)。



## <a name="create-a-duplicate-of-an-update"></a>建立更新的重複項
您可以為存放庫中的更新建立重複項 (或稱複本)。 接著，您可以修改該複本，而非修改原始更新。 您無法建立更新配套的複本。

若要建立複本，請在 [更新工作區]中選取更新，然後選擇 [建立複本]。 更新的複本會出現在 [更新工作區] 中的相同位置，且其名稱會附加「複本」字樣。

您建立的新複本會具有「未到期」狀態，但其他則會維持原始更新的設定。

## <a name="edit-updates-and-bundles"></a>編輯更新與配套
您可以選取存放庫中的更新與配套來修改它們。

在 [更新工作區] 中，選取更新或配套，然後從 [常用] 索引標籤選取 [編輯] 以開啟編輯精靈。 更新與配套各有彼此獨立但密切相關的精靈，它們會呈現與[建立更新](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard)或[建立配套](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-bundle-wizard)精靈相同的選項。

編輯時，您可以變更與更新或配套有關的任何可用詳細資料，以便它可以在您的環境中使用。 例如，您可以編輯適用性或優先順序規則，或變更語言。 您也可以變更產品與廠商以將更新或配套移至自訂資料夾，以根據您自己的用途將更新組成群組。

## <a name="assign-updates-and-bundles-to-a-publication"></a>將更新與配套指派到發行集
您可以在 [更新工作區] 中選取更新與配套，然後從 [常用] 索引標籤選擇 [指派]，以將它們新增到發行集。 這樣會啟動 [指派軟體更新] 精靈。
-  如需有關如何以單一工作形式選取及發行更新與配套的詳細資訊，請參閱[發行更新與配套](#publish-updates-and-bundles-from-the-updates-workspace)。
-  如需有關如何以單一物件形式管理更新與配套群組的詳細資訊，請參閱[管理發行集](/sccm/sum/tools/updates-publisher-publications)。 將更新指派到發行集之後，您可以管理該發行集，而該發行集接著會包含所有其受指派的更新。

當您將更新指派到發行集時：

-   您可以在相同的發行集中包括已到期與未到期的更新與配套。

-   指定發行集類型：

    -   **完整內容** – 這會將更新的完整內容發行到您的 WSUS 伺服器。 這包括中繼資料與更新二進位檔案。

    -   **僅中繼資料** – 這只會發行中繼資料，不會發行更新二進位檔案。 當您想要收集合規性資料時，可以選擇此選項。

    -   **自動** – 只有當您已將 Updates Publisher 連線到 Configuration Manager 時，才能使用此模式 (請參閱 [ConfigMgr Server](/sccm/sum/tools/updates-publisher-options#configmgr-server) 選項)。

    使用此類型時，Updates Publisher 會查詢 Configuration Manager 以判斷應該以 [完整內容] 或 [僅中繼資料] 選項發行更新或配套。 只有當更新符合 [要求的用戶端計數閾值] 與 [套件來源大小閾值]\(在 Updates Publisher 選項的 [ConfigMgr Server] 頁面所指定) 時，才會發行更新的完整內容。

-   選取發行集：

    -   當您已建立想要使用的發行集時，請使用 [指派軟體更新至現有發行集]。 必須至少有一個發行集存在，此選項才能使用。

    -   當您沒有適用的發行集時，請使用 [指派軟體更新至新發行集]。 這樣會以您指定的名稱建立新發行集。

將更新指派至發行集之後，您可以使用 [發行集工作區] 以群組方式[發行](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations)或[匯出](/sccm/sum/tools/updates-publisher-publications#export-a-pubilcation)發行集。

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>從 [更新工作區] 發行更新與配套
當您發行更新與配套時，Updates Publisher 會將有關那些更新與配套的資訊 (中繼資料) 或甚至可能是更新的二進位檔案 (完整內容) 新增到更新伺服器，以便部署到裝置。

您必須先設定 Updates Publisher 的[更新伺服器](/sccm/sum/tools/updates-publisher-options#update-server)選項，才能使用發行選項。 若要開啟此設定選項，請移至 [更新工作區] &gt;[概觀] 並選取 [設定 WSUS 與簽署憑證]。 您也可以移至 Updates Publisher 選項中的 [更新伺服器] 頁面。

發行更新與配套有兩種方式：
-   直接從 [更新工作區] 發行 (請參閱下列程序：「發行更新與配套」)。
-   從 [發行集工作區] 以[發行集](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations)形式發行。  

> [!NOTE]   
> Updates Publisher 只能發行大小不超過 375 MB 的更新。

### <a name="to-publish-updates-and-bundles"></a>發行更新與配套
1.  移至 [更新工作區] 並選取您要發行的一或多個更新與配套。 接著，從功能區的 [常用] 索引標籤選擇 [發行]。

2.  在 [發行精靈] 的 [選取] 頁面上，選取更新發行方式。 選項與用於[指派更新](#assign-updates-and-bundles-to-a-publication)的選項相同：[完整內容]、[僅中繼資料] 或 [自動]。

    您也可以選擇使用新的發行憑證來簽署所有更新。

3.  完成精靈。

若發行失敗，系統會顯示 UpdatesPublisher.log 檔案的連結給您，以提供更詳細的資訊。

## <a name="export-updates"></a>匯出更新
您可以從 Updates Publisher 存放庫匯出更新與配套，以建立自訂更新類別目錄。 接著，您可以[新增](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs)類別目錄並將它[匯入](/sccm/sum/tools/updates-publisher-catalogs#mport-updates)到另一個 Updates Publisher 執行個體 (您也可以[將更新匯出為發行集](/sccm/sum/tools/updates-publisher-publications##export-a-publication))。

若要直接匯出，請移至 [更新工作區] > [所有軟體更新]，並選取一或多個更新與配套。 您無法匯出廠商或產品資料夾，但可以選取某個資料夾，然後選取該資料夾中的更新來匯出。

選取一或多個更新之後，從功能區的 [常用] 索引標籤選擇 [匯出]，然後為類別目錄匯出作業提供路徑與檔案名稱。

您將可以找到用於匯出 (包括) 相依軟體更新的選項。

## <a name="delete-updates-and-bundles"></a>刪除更新與配套
您可以刪除更新與更新的配套，以將它們從 Updates Publisher 存放庫移除。

移至 [更新工作區]  > [所有軟體更新]，並選取一或多個個別更新。 接著，從功能區的 [常用] 索引標籤選擇 [刪除]。

-   若您的選取範圍只包含尚未發行或已到期的更新或配套，系統會要求您確認刪除再將它們移除。

-   若您的選取範圍包括已發行且尚未到期的更新或配套，系統會顯示警告。 您應該將那些更新設定為[到期](/sccm/sum/tools/updates-publisher-pubilcations#expire-or-reactivate-updates-and-bundles)並發行該變更，再將它們從存放庫刪除。  

若將某個更新或配套從廠商刪除並重新匯入該類別目錄，該更新會還原到您的存放庫。

## <a name="manage-vendor-and-product-folders"></a>管理廠商與產品資料夾
若要檢視廠商清單，以及您已匯入或建立更新之每個廠商的產品，請移至 [更新工作區] > [概觀] > [所有軟體更新]。

當您使用精靈來匯入或建立軟體更新或配套時，廠商與產品的資料夾會自動由 Updates Publisher 建立。 您也可以手動建立這些資料夾。

-   若要建立廠商資料夾，請在 [更新工作區] 的瀏覽窗格中，在 [所有軟體更新] 上按一下滑鼠右鍵，然後選擇 [建立廠商]。

-   若要在廠商資料夾下建立產品資料夾，請在廠商資料夾上按一下滑鼠右鍵，然後選擇 [建立產品]。

除了建立資料夾之外，您也可以重新命名或刪除存放庫中的任何廠商或產品資料夾。 若要這樣做，請在資料夾上按一下滑鼠右鍵，然後選擇您要的選項 ([重新命名] 或 [刪除])。 刪除資料夾會移除資料夾中的所有更新與配套，並將其產品資料夾從 Updates Publisher 存放庫移除。

您可以在廠商與產品資料夾 (包括您建立的資料夾) 中移動更新。 若要將更新或配套移動到新資料夾，您必須選取更新或配套，然後 [編輯] 更新或配套。 接著，在 [編輯更新] 精靈的 [資訊] 頁面上，您可以重新指派廠商與產品。 當 [編輯更新] 精靈完成時，會套用變更並將更新移動到新資料夾。

## <a name="view-the-xml-of-an-update-or-bundle"></a>檢視更新或配套的 XML
您可以在 [更新工作區] 中選取單一更新或配套，然後選擇 [檢視] XML 以顯示該更新的 XML 結構。 沒有任何選項可用來直接編輯 XML 結構。
