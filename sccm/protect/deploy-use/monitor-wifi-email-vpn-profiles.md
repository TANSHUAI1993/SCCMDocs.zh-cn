---
title: "監視電子郵件、Wi-Fi 和 VPN 設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中監視電子郵件、Wi-Fi 和 VPN 設定檔的相容性狀態。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
caps.latest.revision: "4"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 73d941633d270cf9628f8be14e1e56f3c78624b6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中監視電子郵件、Wi-Fi 和 VPN 設定檔

*適用對象：System Center Configuration Manager (最新分支)*

將 System Center Configuration Manager 電子郵件、Wi-Fi 或 VPN 設定檔部署至階層中的使用者之後，您就可以使用下列程序監視設定檔的相容性狀態：  

-   [如何在 Configuration Manager 主控台中檢視相容性結果](#BKMK_console)  

-   [如何使用報告檢視相容性結果](#BKMK_Reports)  

##  <a name="BKMK_console"></a> 如何在 Configuration Manager 主控台中檢視相容性結果  
 使用這個程序，在 System Center Configuration Manager 主控台中檢視已部署設定檔的相容性詳細資料。  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>在 Configuration Manager 主控台中檢視相容性結果  

1.  在 System Center Configuration Manager 主控台中，按一下 [監視]。  

2.  在 [監視]  工作區中按一下 [部署] 。  

3.  在 [部署] 清單中，選取您要檢閱相容性資訊的設定檔部署。  

4.  您可以在主頁面檢閱有關設定檔部署相容性的摘要資訊。 若要檢視更詳細的資訊，請選取設定檔部署，然後在 [首頁] 索引標籤的 [部署] 群組中，按一下 [檢視狀態] 以開啟 [部署狀態] 頁面。  

     [部署狀態]  頁面包含下列索引標籤：  

    -   **相容：**根據受影響的資產數目，顯示設定檔的相容性。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點，其中包含與此設定檔相容的所有使用者。 [資產詳細資料] 窗格會顯示與設定檔相容的使用者。 按兩下清單中的使用者以顯示其他資訊。  

        > [!IMPORTANT]  
        >  如果設定檔在用戶端裝置上不適用，就不會進行評估；不過，會傳回為相容。  

    -   **錯誤：**根據受影響的資產數目，顯示所選設定檔部署的所有錯誤清單。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點，其中包含因此設定檔而產生錯誤的所有使用者。 當您選取使用者時，[資產詳細資料]  窗格會顯示受到所選問題影響的使用者。 按兩下清單中的使用者以顯示與此問題有關的其他資訊。  

    -   **不相容**：根據受影響的資產數目，顯示一份設定檔中所有不相容規則的清單。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點，其中包含與此設定檔不相容的所有使用者。 當您選取使用者時，[資產詳細資料]  窗格會顯示受到所選問題影響的使用者。 按兩下清單中的使用者以顯示與此問題有關的進一步資訊。  

    -   **未知：**顯示未回報所選設定檔部署相容性的所有使用者清單，以及裝置目前用戶端狀態。  

5.  在 [部署狀態] 頁面中，您可以檢閱與部署之設定檔相容性有關的詳細資訊。 [部署]  節點下方會建立一個臨時節點以協助您更快再找到此資訊。  

##  <a name="BKMK_Reports"></a> 如何使用報告檢視相容性結果  
 相容性設定包含 System Center Configuration Manager 中的設定檔，亦包含數個內建報告，可讓您監視關於設定檔的資訊。 這些報告具有 [相容性和設定管理] 的報告類別。  

> [!IMPORTANT]  
>  當您在相容性設定報告中使用 [裝置篩選器]  和 [使用者篩選器]  參數時，必須使用萬用字元 (%)。  

 如需如何在 System Center Configuration Manager 設定報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。  
