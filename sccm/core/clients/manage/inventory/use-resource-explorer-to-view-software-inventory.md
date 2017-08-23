---
title: "檢視軟體清查 | Microsoft Docs | 資源總管"
description: "在 System Center Configuration Manager 中，使用資源總管檢視軟體清查。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b76bcf65c61b0a2690a468d375ac95b1334d5298
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>如何使用資源總管檢視 System Center Configuration Manager 的軟體清查

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 中使用資源總管，檢視從階層中電腦所收集的軟體清查相關資訊。  

> [!NOTE]  
>  資源總管會等待軟體清查週期在用戶端上執行之後，才會顯示所有的清查資料。  

 資源總管提供下列軟體清查資訊：  

-   **軟體**：  

    -   **收集到的檔案** - 在軟體清查期間收集到的檔案。  

    -   **檔案詳細資料** - 在軟體清查期間清查到與特定產品或製造商無關聯的檔案。  

    -   **上次軟體掃描** - 用戶端電腦上次執行軟體清查和檔案收集的日期和時間。  

    -   **產品詳細資料** - 軟體清查所清查且依製造商分組的軟體產品。  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台執行資源總管  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性]

2.  在 [資產與合規性] 工作區中，選擇 [裝置] 或開啟顯示裝置的任何集合。  

3.  選擇您想要檢視、包含清查的電腦，然後在 [首頁] 索引標籤 > [裝置] 群組中，選擇 [開始] > 資源總管。

4.  您可以在資源總管視窗的右窗格中，以滑鼠右鍵按一下任何項目，然後選擇 [內容] 以更容易閱讀的格式檢視收集到的清查資訊。  
 
