---
title: "檢視診斷資料 | Microsoft Docs"
description: "檢視診斷和使用方式資料，確認 System Center Configuration Manager 階層不包含任何機密資訊。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0932e2b2a4f3e13c35d6b7b0446083f1c233ce03
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>如何檢視 System Center Configuration Manager 的診斷和使用方式資料

*適用對象：System Center Configuration Manager (最新分支)*

您可以檢視 System Center Configuration Manager 階層的診斷和使用方式資料，以確認未包含任何機密或可識別資訊。 遙測資料會彙總並儲存在站台資料庫的 **TEL_TelemetryResults** 資料表中，而且會格式化為可以程式設計方式使用且更有效率。 雖然下列選項可讓您檢視傳送至 Microsoft 的精確資料，但並不適用於其他用途，例如資料分析。  

下列 SQL 命令可用來檢視這個資料表的內容，並顯示已傳送的精確資料。 (您也可以將這份資料匯出成文字檔)：  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  在安裝 1602 版之前，儲存遙測資料的資料表是 **TelemetryResults**。  

當服務連接點處於離線模式時，您可以使用服務連接工具，將目前的診斷和使用方式資料匯出成逗點分隔值 (CSV) 檔案。 請使用 **-Export** 參數在服務連接點上執行服務連接工具。  

##  <a name="bkmk_hashes"></a> 單程雜湊  
一些資料是由隨機英數字元字串所組成。 Configuration Manager 使用採用單程雜湊的 SHA-256 演算法，以確保不會收集可能的敏感性資料。 此演算法會將資料維持在仍可用於進行相互關聯和比較的狀態。 例如，單程雜湊會針對每個資料表名稱擷取，而不是收集站台資料庫中的資料表名稱。 如此可確保不會顯示您所建立的自訂資料表名稱或其他人的產品附加元件。 然後，我們可以對產品預設隨附的 SQL 資料表名稱進行相同的單程雜湊，再比較兩個查詢結果，以判斷您的資料庫結構描述與產品預設值的差異。 此資訊可接著用來改進需要變更 SQL 結構描述的更新。  

檢視未經處理的資料時，每個資料列都會出現一個通用的雜湊值。 這是階層識別碼。 此雜湊值是用來確保資料與相同的階層相互關聯，但不識別客戶或來源。  

#### <a name="to-see-how-the-one-way-hash-works"></a>了解單程雜湊的運作方式  

1.  在 SQL Management Studio 中針對 Configuration Manager 資料庫執行下列 SQL 陳述式來取得階層識別碼︰**select [dbo].[fnGetHierarchyID]\(\)**  

2.  使用下列 Windows PowerShell 指令碼來執行從資料庫取得之 GUID 的單程雜湊。 然後，您可以將此識別碼與未經處理資料中的階層識別碼做比較，以了解我們如何遮蔽此資料。  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  
