---
title: "匯入設定資料 | Microsoft Docs"
description: "如果設定資料包含在封包檔格式中，並遵循支援的服務模組化語言結構描述，即可匯入設定資料。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 60d0642618a3074fc50a848f1189f4d6559ca916
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="import-configuration-data-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 匯入設定資料

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 主控台中，您除了可以建立設定基準和設定項目，還可以匯入設定資料 (當設定資料包含在封包檔格式 (.cab) 中，並遵循支援的 SML 結構描述的情況下)。 您可以透過下列項目，匯入設定資料：  

-   從 Microsoft 或其他軟體廠商網站下載組態資料 (組態套件) 最佳做法。  

-   已從 System Center 2012 Configuration Manager 和更新版本匯出的設定資料。  

-   外部撰寫且符合 SML 結構描述的設定資料。  

 如需可協助您管理 System Center 2012 Configuration Manager 站台伺服器角色的相容性組態組件範例，請參閱 [System Center 2012 Configuration Manager 組態套件](http://www.microsoft.com/en-us/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all)。  

當您匯入組態基準時，封包檔可能也會包含組態基準中所參考的部分或全部組態項目。 在匯入過程中，Configuration Manager 會驗證設定基準中參考的所有設定項目是同時包含在封包檔中，還是早就在 Configuration Manager 站台中。 如果您嘗試匯入的設定基準參考了 Configuration Manager 找不到的設定資料，則匯入程序會失敗。  

匯入程序可能失敗的其他情況包括：  

-   設定資料參考了 Configuration Manager 找不到的設定資料；這些資料可能在其資料庫或封包檔案當中。  

-   設定資料已在 Configuration Manager 資料庫中，名稱及設定資料版本皆相同，但內容版本不同。  

-   設定資料已在 Configuration Manager 資料庫中，內容版本相同，但雜湊計算將其識別為不同。  

-   已有同名的較新版本設定資料，或最近已從 Configuration Manager 資料庫刪除。  

-   在多站台的 Configuration Manager 階層中，設定資料原本是從父站台匯入。 它必須從相同的站台更新，不能從子站台更新。  

### <a name="import-configuration-data"></a>匯入設定資料  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [設定項目] 或 [設定基準]。
2.  在 [常用] 索引標籤中，按一下 [建立] 群組中的 [匯入設定資料]。  
3.  在 [匯入組態資料精靈]  的 [選取檔案] 頁面中，按一下 [新增] ，然後在 [開啟]  對話方塊中，選取要匯入的 .cab 檔案。  
4.  如果想要在 Configuration Manager 主控台中編輯匯入的設定資料，請選取 [建立已匯入的設定基準和設定項目的新複本] 核取方塊。  
5.  在 [摘要] 頁面上，檢閱將採取的動作，然後完成精靈。  

匯入的設定資料會顯示在 [資產與相容性] 工作區的 [相容性設定] 節點中。  
