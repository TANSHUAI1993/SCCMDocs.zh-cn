---
title: "診斷資料常見問題集 | Microsoft Docs"
description: "尋找與 System Center Configuration Manager 的診斷和使用方式資料有關的常見問題集。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 177a30a30f6b8579fa1956d28581d4f9d3a11838
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>與 System Center Configuration Manager 的診斷和使用方式資料有關的常見問題集

*適用於：System Center Configuration Manager (最新分支)*

以下是與 System Center Configuration Manager 的診斷和使用方式資料有關的常見問題集：  

###  <a name="bkmk_off"></a> 如何關閉遙測？  
無法關閉遙測。 但可選擇收集遙測資料的層級。 您也可以在離線模式使用服務連接點，協助您管理送出遙測資料的時機。

Configuration Manager 的最新分支需要定期更新，才可支援新版 Windows 10 和 Microsoft Intune。 Microsoft 至少需要「基本」層級的診斷和使用方式資料，才能確保產品保持在最新狀態、改善更新體驗，以及提升產品的品質和安全性。

###  <a name="bkmk_retention"></a> 什麼是資料保留期間？  
 診斷和使用方式資料會保留一年。  

###  <a name="bkmk_update"></a> 安裝或更新產品時，是否會傳送診斷和使用方式資料？  
 不會。 只有在安裝完站台並正常運作之後，才會傳送診斷和使用方式資料。  

###  <a name="bkmk_frequency"></a> 多久傳送一次資料？  
 SQL 預存程序每 7 天執行一次 (從安裝站台的那天算起)。 在線上模式中，服務連接點是設定為在執行查詢之後上傳資料。 在離線模式中，系統管理員會使用服務連線工具來上傳資料。 (注意︰資料一開始並不可供離線使用，必須等到安裝完站台 7 天後，才可供離線使用。)  

###  <a name="bkmk_network"></a> 是否可以使用資料來形成網路地圖？  
 如 System Center Configuration Manager 的診斷使用方式資料收集層級描述中所示，站台詳細資料包括每個站台的時區資訊。 這資訊可讓您深入了解階層中站台的廣泛地理位置和全球散佈情況。 但並不會收集任何網路詳細資料 (例如 IP 位址或更詳細的地理資訊)。
 - [1511 的診斷資料](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [1602 的診斷資料](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [1606 的診斷資料](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [1610 的診斷資料](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="bkmk_tables"></a> 您是否可以看到自訂資料表中的資料？  
 不會。 收集診斷和使用方式資料時，是透過 SQL 預存程序依據資料庫中的預設產品資料表 (首碼皆為 **TEL_**) 來收集。 在進行 SQL 結構描述偵測查詢的過程中，所有資料表名稱都會經過雜湊處理，以便與已知的預設值做比較。 這可以判斷自訂資料表存在於資料庫中 (資料庫結構描述延伸自預設值)，但無法判斷這些資料表內包含的任何資料。  

###  <a name="bkmk_databases"></a> 您是否可以看到其他資料庫的名稱，或是看到其他資料庫中的資料？  
 不會。 用來收集資料的預存程序會被限制在站台資料庫。  

## <a name="see-also"></a>請參閱  
 [System Center Configuration Manager 的診斷和使用方式資料](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)
