---
title: "安裝程式參考 | Microsoft Docs"
description: "請檢閱此參考，協助您準備安裝 Configuration Manager 站台或階層。"
ms.custom: na
ms.date: 4/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: "22"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 739461a6cca0fd67431093524c1e8158afd80d0f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="reference-for-system-center-configuration-manager-setup"></a>System Center Configuration Manager 安裝程式參考

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 安裝程式提供下列各節中所述的數個主題連結。 此處呈現的資訊可協助您準備安裝 Configuration Manager 站台或階層，以及協助您準備好一些安裝期間必須做出的決策。  


##  <a name="bkmk_start"></a> 開始之前  
在安裝新的 Configuration Manager 站台之前，請務必已檢閱下列資訊，其可協助您設定成功部署設計的階段：  

-   [System Center Configuration Manager 的基礎](../../../../core/understand/fundamentals.md)  
-   [規劃 System Center Configuration Manager 基礎結構](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [準備安裝 System Center Configuration Manager 站台](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> 評估伺服器整備程度  
開始安裝新的站台之前，請確定預計為該站台使用的站台伺服器與遠端站台系統伺服器 (例如裝載站台資料庫的伺服器) 皆符合所有必要的設定。 文件庫中的下列主題可協助：  

-   [System Center Configuration Manager 的支援設定](../../../../core/plan-design/configs/supported-configurations.md)  
-   [必要條件檢查工具](prerequisite-checker.md)  

##  <a name="bkmk_Addclients"></a> 其他作業系統的用戶端  
您可從 Microsoft 下載中心下載適用於下列作業系統的 Configuration Manager 用戶端軟體：  

-   Mac (Apple)  
-   UNIX  
-   Linux  

使用下列連結可下載您使用之 Configuration Manager 版本的用戶端：  

-   請參閱 [Microsoft System Center Configuration Manager - 其他作業系統的用戶端](http://www.microsoft.com/download/details.aspx?id=47719)  

##  <a name="bkmk_usage"></a> 使用情形資料層級和設定  
安裝第一個 System Center Configuration Manager 站台時，會於站台伺服器上自動安裝 Configuration Manager 並會設定新的站台系統角色 (**服務連接點**)。 服務連接點具有這些預設設定：  

-   **線上** 模式 (也提供離線模式)  
-   **增強**的資料集合層級 (也提供其他兩個資料集合層級：基本與完整)  

當服務連線點站台系統角色為線上時，Microsoft 可自動從網際網路收集診斷與使用情況資訊。 所收集的資訊可幫助我們：  

-   識別及疑難排解問題  
-   改善產品和服務  
-   識別適用於您所使用之 Configuration Manager 版本的 Configuration Manager 更新  

### <a name="levels-of-data-collection"></a>資料收集層級  
資料收集包含三個層級：

-   **基本**層級包含安裝及升級的相關資料，例如站台數目，以及啟用的 Configuration Manager 功能。 不會傳輸任何個人識別資訊。  

-   **增強**層級除了包含「基本」層級設定的資料之外，還會傳輸階層的相關資料、每項功能的使用方式 (頻率和持續時間)，以及增強的診斷資訊，例如您的伺服器在系統當機或應用程式損毀時的記憶體狀態。 不會傳輸任何個人識別資料。  

-   **完整**層級除了包含「基本」與「增強」層級設定的資料之外，還會傳送進階診斷資訊，例如系統檔案和記憶體快照集等。 此選項可能包含個人識別資訊，但我們不會使用該資訊來識別或連絡您，或者推銷廣告給您。  

如需詳細資訊，包含每個層級所收集之詳細資料的揭露，請參閱 [System Center Configuration Manager 的診斷和使用方式資料](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)。  

若要在線上檢視 System Center Configuration Manager 隱私權聲明，請前往 [http://go.microsoft.com/fwlink/?LinkID=626527](http://go.microsoft.com/fwlink/?LinkID=626527)。
