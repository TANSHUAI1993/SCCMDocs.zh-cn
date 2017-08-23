---
title: "檢視硬體清查 | Microsoft Docs | 資源總管"
description: "在 System Center Configuration Manager 中，使用資源總管檢視硬體清查。"
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: "7"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: e39fa60a5d215fa1b0a98d4463058497e63a4d4f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>如何使用資源總管檢視 System Center Configuration Manager 中的硬體清查

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 中使用資源總管，檢視從階層中用戶端所收集的硬體清查相關資訊。  

> [!NOTE]  
>  資源總管不會顯示資料直到硬體清查週期已在用戶端執行您要連接到任何清查。  

 資源總管包含與硬體清查相關的下列區段：  

-   **硬體** - 包含從指定的用戶端裝置收集來的最新硬體清查。  **工作站狀態** - 包含裝置上次執行硬體清查的日期和時間。  

-   **硬體歷程記錄** - 包含上次發生硬體清查後所變更的清查項目之歷程記錄。 每個項目都包含**目前**節點以及一或多個 <日期\> 節點。 您可以比較目前節點與其中一個歷程記錄節點中的資訊，以探索已變更的項目。  

    > [!NOTE]  
    >  Configuration Manager 會將硬體清查歷程記錄，保留 [刪除過時清查歷程記錄] 站台維護工作中所指定的天數  

> [!NOTE]  
>  如需如何檢視執行 Linux 與 UNIX 之用戶端的硬體清查資訊，請參閱 [如何在 System Center Configuration Manager 中監視 Linux 和 UNIX 伺服器的用戶端](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md)。  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>如何從 Configuration Manager 主控台執行資源總管  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [裝置]，或開啟顯示裝置的任何集合。  

3.  選擇您想要檢視、包含清查的電腦，然後在 [首頁] 索引標籤 > [裝置] 群組中，選擇 [開始] >  資源總管。   

4.  在資源總管視窗的右窗格中，以滑鼠右鍵按一下任何項目，然後選擇 [內容] 開啟 [<項目名稱\> 內容] 對話方塊，以更容易閱讀的格式檢視收集到的清查資訊。  

