---
title: "管理發行集 | Microsoft Docs"
description: "使用 System Center Updates Publisher 以發行集的形式管理軟體更新群組。"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: ddea7af935d5be880b96e383401061f8aa11e6da
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-publications-in-updates-publisher"></a>在 Updates Publisher 中管理發行集

*適用於：System Center Updates Publisher*

您可以使用發行集來以單一物件形式管理更新與配套群組。 這包含將更新發行到管理伺服器，並以群組的形式匯出發行集，來與另一個 Updates Publisher 安裝搭配使用。

## <a name="create-publications"></a>建立發行集
建立發行集的方式有兩種：

-   當您在 [更新工作區] 中管理更新和配套時，可以將它們[指派](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)給當時建立的新發行集。

-   在 [發行集工作區] 中，您可以使用功能區 [發行集] 索引標籤上的 [建立] 按鈕。 此方法可讓您建立發行集以供日後使用。 稍後當您指派更新時，便可以使用此發行集。

## <a name="rename-a-publication"></a>將發行集重新命名
若要將發行集重新命名，請從 [發行集工作區] 內選取發行集，然後在功能區的 [發行集] 索引標籤上，選擇 [編輯]。

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>變更發行集中更新的發行集類型
從 [發行集工作區] 中，您可修改指派到發行集的更新和配套的 [發行集類型]。

1. 選取包含您要修改之更新的發行集，然後從 [所有 &lt;發行集名稱> 成員更新] 清單中選取一或多個更新或配套。

2. 接下來，在 [常用] 索引標籤上，選擇下列其中一個選項。 可用的選項取決於您所選取之更新的發行集類型。

  -   **自動**
  -   **完整內容**
  -   **僅中繼資料**

做出變更之後，您可能需要重新整理發行集檢視以查看新的值。

如需不同發行集類型的相關資訊，請參閱[將更新與配套指派到發行集](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)。

> [!TIP]    
> 設定配套的發行集類型之後，該配套中的所有軟體更新都會以該配套的發行集類型進行發行。

## <a name="remove-updates-from-a-publication"></a>從發行集中移除更新
若要從發行集移除更新或配套，請在 [發行集工作區] 中選取要修改的發行集，然後選取您要移除的更新和配套。 接下來，在功能區的 [常用] 索引標籤上，選擇 [移除]。

當更新從發行集中移除後，仍可以在 Updates Publisher 存放庫中取得它們。

## <a name="publish-publications"></a>發行發行集
當您發行更新與配套時，Updates Publisher 會將有關那些更新與配套的資訊 (中繼資料) 或甚至可能是更新的二進位檔案 (完整內容) 新增到更新伺服器，以便部署到裝置。

您必須先設定 Updates Publisher 的[更新伺服器](/sccm/sum/tools/updates-publisher-options#update-server)選項，才能使用發行選項。 若要開啟此設定選項，請移至 [更新工作區] &gt;[概觀] 並選取 [設定 WSUS 與簽署憑證]。 您也可以移至 Updates Publisher 選項中的 [更新伺服器] 頁面。

> [!NOTE]   
> Updates Publisher 只能發行大小不超過 375 MB 的更新。

### <a name="to-publish-a-publication"></a>發行發行集

1.  移至 [發行集工作區]，然後選取包含要發行或匯出之更新或配套群組的發行集。 接著，從功能區的 [常用] 索引標籤選擇 [發行]。

2.  在 [發行] 精靈的 [選取] 頁面上，您可以選擇使用新的發行憑證簽署所有更新，但是無法變更發行集類型。

3.  完成精靈。

  若發行失敗，系統會顯示 UpdatesPublisher.log 檔案的連結給您，以提供更詳細的資訊。

## <a name="export-a-publication"></a>匯出發行集
您可以從 Updates Publisher 存放庫中匯出發行集。 這麼做會匯出已指派到該發行集的更新和配套，並建立更新目錄。 然後您可以[新增](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs)目錄並將它[匯入](/sccm/sum/tools/updates-publisher-catalogs#mport-updates)到另一個 Updates Publisher 執行個體。 您也可以[匯出](/sccm/sum/tools/manage-updates-with-updates-publisher#export-updates)不是發行集之一部分的更新。

若要匯出更新，請移至 [發行集工作區] 並選取包含要匯出之更新的發行集。 一次只能選取一個發行集。

選取發行集之後，從功能區的 [常用] 索引標籤選擇 [匯出]，然後提供目錄匯出的路徑與檔案名稱。

您也可以將相依軟體更新做為匯出的一部分一起匯出。

## <a name="rename-a-publication"></a>將發行集重新命名
若要將發行集重新命名，請從 [發行集工作區] 選取發行集，然後從功能區的 [發行集] 索引標籤上選擇 [編輯]。

## <a name="delete-a-publication"></a>刪除發行集
若要刪除發行集，請從 [發行集工作區] 選取發行集，然後從功能區的 [發行集] 索引標籤上選擇 [刪除]。

當更新從 Updates Publisher 移除之後，發行集中的更新仍可在 Updates Publisher 存放庫中取得。

## <a name="expire-or-reactivate-updates-and-bundles"></a>使更新和配套到期，或是重新啟動更新和配套
您可以使用 [更新工作區] 來選取更新和配套，並使它們到期或是重新啟動它們。 您可以任意次數地使更新和配套到期並重新啟動它們。

-   **若要使更新或配套到期**，請在 [更新工作區] 中選取一或多個未過期的更新或配套，然後從 [常用] 索引標籤選擇 [到期]。 在您將更新或配套以到期的狀態發行到 Configuration Manager 之前，都可以重新啟動它們。

    在您可以將自訂更新或配套從 Configuration Manager 移除 (刪除) 之前，必須先使它到期，並將其到期狀態發行到 Configuration Manager。 更新或配套在 Configuration Manager 中到期之後，您就無法再部署或重新啟動該更新或配套。

-   **若要將更新或配套重新啟動**，請在 [更新工作區] 中選取一或多個已到期的更新，然後從工作區的 [常用] 索引標籤選取 [重新啟動]。 如果已到期的更新先前已經以到期的狀態發行到 Configuration Manager，您就無法將它重新啟動。
