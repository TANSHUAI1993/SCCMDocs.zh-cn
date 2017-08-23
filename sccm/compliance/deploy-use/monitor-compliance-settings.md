---
title: "監視合規性設定 | Microsoft Docs"
description: "使用本主題中的一或多個程序，顯示設定基準的相容性狀態。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 75cd7e811262633d81d978265f21ec7ed3b61a58
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-compliance-settings-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中監視相容性設定

*適用於：System Center Configuration Manager (最新分支)*

將 System Center Configuration Manager 設定基準部署至階層中的電腦之後，即可使用本主題中的一個或多個程序來顯示設定基準的相容性狀態：

> [!NOTE]  
>  相容性設定報告中的驗證準則欄位 (用戶端報告上的對等項目是 [條件約束] 顯示基礎服務模型語言 (SML)。 這讓在 Configuration Manager 主控台中編寫設定項目的系統管理員在沒有 SML 知識時很難了解什麼是驗證準則。 在這個情況下，使用 Configuration Manager 主控台中的 [監視] 工作區，來檢視設定項目和其驗證準則的內容。  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>在 Configuration Manager 主控台中檢視相容性結果  
 使用這個程序，在 Configuration Manager 主控台中檢視已部署之設定基準相容性的詳細資料。  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>在 Configuration Manager 主控台中檢視相容性結果  

1.  在 Configuration Manager 主控台中，按一下 [監視] > [部署]。  

3.  在 [部署]  清單中，選取您想要檢閱其相容性資訊的組態基準部署。  

4.  您可以在主頁面檢閱有關組態基準部署相容性的摘要資訊。 若要檢視更詳細的資訊，請選取組態基準部署，然後在 [首頁]  索引標籤的 [部署]  群組中，按一下 [檢視狀態]  開啟 [部署狀態]  頁面。  

     [部署狀態]  頁面包含下列索引標籤：  

    -   **相容性**：根據受影響的資產數目，顯示組態基準的相容性。 您可以按一下規則，在 [資產與相容性]  工作區的 [使用者]  或 [裝置]  節點下方建立臨時節點，其中包含與這項規則相容的所有使用者或裝置。 [資產詳細資料]  窗格會顯示與組態基準相容的使用者或裝置。 按兩下清單中的使用者或裝置以顯示其他資訊。  

        > [!IMPORTANT]  
        >  如果在用戶端裝置上偵測不到設定項目或其不適用，就不會進行評估；不過，會將規則傳回為相容。  

    -   **錯誤**：根據受影響的資產數目，顯示一份所選組態基準部署的所有錯誤清單。 您可以按一下規則，在 [資產與相容性]  工作區的 [使用者]  或 [裝置]  節點下方建立臨時節點，其中包含因這項規則而產生錯誤的所有使用者或裝置。 當您選取使用者或裝置時，[資產詳細資料]  窗格會顯示受到所選問題影響的使用者或裝置。 按兩下清單中的使用者或裝置以顯示這個問題的其他資訊。  

    -   **不相容**：根據受影響的資產數目，顯示一份組態基準中所有不相容規則的清單。 您可以按一下規則，在 [資產與相容性]  工作區的 [使用者]  或 [裝置]  節點下方建立臨時節點，其中包含與這項規則不相容的所有使用者或裝置。 當您選取使用者或裝置時，[資產詳細資料]  窗格會顯示受到所選問題影響的使用者或裝置。 按兩下清單中的使用者或裝置以顯示這個問題的進一步資訊。  

    -   **不明**：顯示未針對所選組態基準部署回報相容性的所有使用者和裝置清單，以及裝置目前的用戶端狀態。  

5.  您可以在 [部署狀態]  頁面檢閱有關部署之組態基準相容性的詳細資訊。 [部署]  節點下方會建立一個臨時節點以協助您更快再找到此資訊。  

##  <a name="view-compliance-results-by-using-reports"></a>使用報告檢視相容性結果  
 Configuration Manager 中的相容性設定包含數份內建報告，可讓您監視關於設定項目、設定基準和部署的資訊。 這些報告具有 [相容性和設定管理] 的報告類別。  

> [!IMPORTANT]  
>  當您在相容性設定報告中使用 [裝置篩選器]**%****和 [使用者篩選器] 參數時，必須使用萬用字元 (** )。  

 如需如何在 Configuration Manager 設定報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。  

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>在 Configuration Manager Windows 用戶端電腦上檢視相容性結果

> [!NOTE]  
>  如果您是使用網域 Guest 帳戶進行登入，則無法在 Configuration Manager Windows 用戶端上檢視資訊。    

1.  瀏覽至用戶端電腦控制台中的 [Configuration Manager]  ，然後連按兩下它以開啟其內容。  

2.  按一下 [設定]  索引標籤，然後檢視已部署之組態基準的清單。  

3.  檢視每個組態基準的 [相容性狀態]  ：  

    > [!IMPORTANT]  
    >  快取用戶端上 15 分鐘的評估結果。 如果您在 15 分鐘期間內起始重新評估，則會從這個快取中傳回相容性結果 ，而不是新的評估。 因此，如果您在用戶端上進行可能影響相容性評估結果的變更，請先等待 15 分鐘，再起始重新評估。  

    -   **相容**：用戶端電腦與評估的組態基準相容。  

    -   **不相容**：用戶端電腦與評估的組態基準不相容。  

    -   **不明**：用戶端電腦尚未評估組態基準。 如果您想要在相容性評估排程之外起始評估，請選取要評估的組態基準，然後按一下 [評估] 。  

        > [!NOTE]  
        >  如果您擁有用戶端電腦的本機系統管理員認證，則可以檢視每個已評估之組態基準的詳細資料，來判斷哪一個組態項目報告不相容狀態。 若要這樣做，請選取組態基準，然後按一下 [檢視報告] 。  

4.  按一下 [ **確定**]。  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>根據設定基準相容性建立集合  
 使用下列程序，根據具有所指定相容性的裝置來建立 Configuration Manager 集合。 您可以根據下列相容性狀態來建立集合：  

-   **相容性**  

-   **錯誤**  

-   **Non-compliant**  

-   **不明**  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [設定基準]。  

3.  在 [組態基準]  清單中，選取您想要用來建立集合的組態基準。  

4.  在 [部署]  索引標籤的 [部署群組] 中，按一下 [建立新集合]  ，然後在下拉式清單中選取您想要用來建立集合的相容性層級。  

5.  根據組態項目部署至使用者或裝置，來開啟 [建立使用者集合精靈]  或 [建立裝置集合精靈]  。 這個精靈會自動填入建立集合的正確值；不過，您可以編輯這些值。  

6.  完成這個精靈之後，集合會顯示在 [資產與相容性]  工作區的 [使用者集合]  或 [裝置集合]  節點中。  
