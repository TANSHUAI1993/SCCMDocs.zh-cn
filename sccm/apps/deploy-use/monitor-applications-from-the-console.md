---
title: "從 System Center Configuration Manager 主控台監視應用程式 | Microsoft Docs"
description: "使用 Configuration Manager 的 [監視] 工作區，來監視軟體部署 (包括更新、相容性設定和應用程式)。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 42d21d10489bffe32b875384f8801686239a0ba4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>從 System Center Configuration Manager 主控台監視應用程式

*適用於：System Center Configuration Manager (最新分支)*


在 System Center Configuration Manager 中，您可以監視所有軟體的部署作業，包括軟體更新、相容性設定、應用程式、工作順序，以及套件和程式。 您可以使用 Configuration Manager 主控台的 [監視] 工作區，或使用報告，來監視部署。  

 Configuration Manager 中的應用程式支援狀態監視，可讓您追蹤使用者和裝置最近的應用程式部署狀態。 這些狀態訊息會顯示個別裝置的相關資訊。 例如，如果應用程式是部署至使用者集合，您可以在 Configuration Manager 主控台中檢視部署與部署目的的相容性狀態。  

## <a name="learn-about-compliance-states-in-system-center-configuration-manager"></a>了解 System Center Configuration Manager 中的合規性狀態
 應用程式部署狀態的相容性狀態為下列其中之一：  

-   **成功** – 應用程式部署成功或之前已安裝過。  

-   **進行中** – 正在部署該應用程式。  

-   **未知** – 無法判定應用程式部署狀態。 此狀態不適用於目的為 [可用] 的 部署。 通常會在尚未收到用戶端傳來的狀態訊息時顯示此狀態。  

-   **不符合需求** – 未部署應用程式，因為該應用程式與某個相依性或需求規則不相容，或者因為欲部署的作業系統不適用。  

-   **錯誤** – 應用程式部署失敗，因為發生錯誤。  

您可以檢視各個合規性狀態的其他資訊，包括合規性狀態中的子類別，以及此類別中的使用者和裝置數量。 例如，[錯誤]  相容性狀態包括下列子類別：  

-   評估需求時發生的錯誤  

-   內容相關的錯誤  

-   安裝錯誤  

 如有一個以上的相容性狀態符合應用程式部署作業，您會看見代表最低相容性的彙總狀態。 例如：  

    -   如果使用者登入兩個裝置，其中一個裝置順利安裝應用程式，另一個裝置卻安裝失敗，則該使用者看見的應用程式彙總部署狀態會顯示為 [錯誤]。  

    -   如果您將應用程式部署至登入某部電腦的所有使用者，則會收到該電腦的多個部署結果。 如果其中一項部署失敗，則該電腦的彙總部署狀態會顯示 [錯誤] 。  

系統不會彙總套件和程式部署的部署狀態。  

 請利用這些子類別快速識別應用程式部署所發生的任何重要問題。 如裝置的相容性狀態屬於特定子類別，您也可以檢視其他相關資訊。  

 Configuration Manager 中的應用程式管理包含數份內建報告，可讓您監視應用程式和部署的相關資訊。 這些報告的報告類別為 [軟體發佈 – 應用程式監視] 。  

 如需如何在 Configuration Manager 設定報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>在 Configuration Manager 主控台中監視應用程式的狀態  

1.  在 Configuration Manager 主控台中，選擇 [監視] > [部署]。  

3.  若要檢閱每個合規性狀態的部署詳細資訊及處於該狀態的裝置，請選取其中一個部署，然後在 [首頁] 索引標籤的 [部署] 群組中，選擇 [檢視狀態]，以開啟 [部署狀態] 窗格。 在此窗格中，您可以檢視各相容性狀態的資產。 只要選擇任一資產，即可深入檢視有關該資產部署狀態的詳細資訊。  

    > [!NOTE]  
    >  可以 [部署狀態]  窗格顯示的項目數限制為 20,000。 如果您需要查看更多項目，請使用 Configuration Manager 報告來檢視應用程式狀態資料。  
    >   
    >  部署類型的狀態會彙總顯示在 [部署狀態]  窗格中。 若要深入檢視與部署類型相關的詳細資訊，請使用 [軟體發佈 - 應用程式監視]  報告類別中的 [應用程式基礎結構錯誤] 報告。  

4.  若要檢閱應用程式部署之一般狀態的相關資訊，請選取任一部署，然後選擇 [選取的部署] 視窗中的 [摘要] 索引標籤。  

5.  若要檢閱應用程式部署類型的相關資訊，請選取任一部署，然後選擇 [選取的部署] 視窗中的 [部署類型] 索引標籤。  

在您選擇 [檢視狀態] 後，[部署狀態] 窗格中所顯示的資訊是 Configuration Manager 資料庫的即時資料。 [摘要] 索引標籤和 [部署類型] 索引標籤中顯示的資訊則是摘要資料。

如果 [摘要] 索引標籤和 [部署類型] 索引標籤中顯示的資料與 [部署狀態] 窗格中顯示的資料不一致，請選擇 [執行摘要] 以更新這些索引標籤中的資料。 您可以依照下列方式設定預設的應用程式部署摘要間隔：  

1. 在 Configuration Manager 主控台中，選擇 [管理] > [站台設定] > [站台]。

2. 從 [站台] 清單中，選取您要為其設定摘要間隔的目標站台，然後在 [首頁] 索引標籤的 [設定] 群組中，選擇 [狀態摘要器]。

3. 在 [狀態摘要器] 對話方塊中，依序選擇 [應用程式部署摘要器] 和 [編輯]。  

4. 在 [應用程式部署摘要器內容] 對話方塊中，設定所需的摘要間隔，然後選擇 [確定]。  
