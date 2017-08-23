---
title: "探索裝置與使用者資源 |Microsoft Docs"
description: "閱讀以了解探索程序及探索資料記錄的概觀。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
caps.latest.revision: "20"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 647826e9d340d3ef97abab0dba51041a3727dedc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="run-discovery-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 執行探索

*適用於︰System Center Configuration Manager (最新分支)*

您可以使用 System Center Configuration Manager 中的一或多種探索方法，尋找您可管理的裝置與使用者資源。 您也可以使用 [探索] 來找出環境中的網路基礎結構。 您可使用多種不同的方法來探索不同的事物，且每個方法都有其自己的設定與限制。  

## <a name="overview-of-discovery"></a>探索概觀  
 探索是一種過程，Configuration Manager 會透過這個過程來了解可供您管理的項目。 下列是可用的探索方法：  

-   Active Directory 樹系探索  

-   Active Directory 群組探索  

-   Active Directory 系統探索  

-   Active Directory 使用者探索  

-   活動訊號探索  

-   網路探索  

-   伺服器探索  

> [!TIP]  
>  您可以在 [About discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md) (關於 System Center Configuration Manager 的探索方法) 了解個別的探索方法。  
>   
>  如需選取使用方法以及階層中哪個站台之協助，請參閱 [選取在 System Center Configuration Manager 使用的探索方法](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)。  

 為充分運用探索方法，您必須在站台啟用該方法，並將它設定為搜尋特定網路或 Active Directory 位置。 執行探索方法時，其會查詢指定的位置是否有可供 Configuration Manager 管理之裝置或使用者的相關資訊。 當探索方法成功找到某項資源的相關資訊時，會將該資訊置於稱作探索資料記錄 (DDR) 的檔案內。 主要站台或管理中心網站接著會處理該檔案。 處理 DDR 時會在站台資料庫中為新探索到的資源建立新記錄，或是以新資訊更新現有記錄。  

 有些探索方法可能會產生大量的網路流量，而其所產生的 DDR，會在處理時耗用大量的 CPU 資源。 因此，請只規劃使用達成您目標所需的探索方法。 您可以從只使用一或兩個探索方法開始，之後再以節制的方式啟用其他方法來延伸您環境中的探索層級。  

 將探索資訊新增到站台資料庫之後，接著不論該資訊的探索或處理站台是為何，會將該資訊複寫到階層中個每個站台。 因此，若在不同的站台為探索方法設定不同的排程與設定，在單一站台上可能可執行特定的探索方法。 如此可減少因為重複的探索動作而使用網路頻寬的情況，並會降低於多個站台上處理多餘的探索資料。  

 您可以使用探索資料，建立之自訂集合與查詢，依邏輯方式分組管理工作資源。 例如：  

-   發行用戶端安裝或升級。  

-   將內容佈署到使用者或裝置。  

-   部署用戶端設定以及相關設定。

##  <a name="BKMK_DDRs"></a> 關於探索資料記錄  
 DDR 是由探索方法所建立的檔案。 其包含可於 Configuration Manager 中管理之資源的相關資訊，例如電腦、使用者，某些情況下還有網路基礎結構。 這些資訊會在主要站台或管理中心網站上處理。 當 DDR 中的資源資訊輸入到資料庫後，就會將 DDR 刪除，並會複寫資訊以當作階層中所有站台的全域資料。  

 站台所處理的 DDR，取決於其所含的資訊：  

-   新探索的資源 DDR 若不在資料庫中，便會在階層的頂層站台處理。 頂層網站會在資料庫中建立新的資源記錄，並為其指派唯一的識別碼。 DDR 會經由以檔案為基礎的複寫傳輸，直到其到達頂層站台為止。  

-   先前探索之物件的 DDR，會在主要站台上處理。 子主要站台不會在 DDR 包含已存在於資料庫之資源的相關資訊時，將 DDR 傳送到管理中心網站。  

-   次要站台不會處理 DDR，而是一律會採用以檔案為基礎的複寫方式，將它們傳送到其父主要站台。  

DDR 檔案是以 .ddr 副檔名作為識別，檔案大小通常約 1 KB。  

## <a name="get-started-with-discovery"></a>開始使用探索：  
 在使用 Configuration Manager 主控台來設定探索之前，應先了解各種方法之間的差異、各種方法的功能，以及就某些方法而言，有何限制。  

下列主題可建立將協助您順利使用探索方法的基礎：  

-   [About discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md) (關於 System Center Configuration Manager 的探索方法)  

-   [Select discovery methods to use for System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md) (選取用於 System Center Configuration Manager 的探索方法)  

然後，當您了解想要使用的方法後，在[設定 System Center Configuration Manager 的探索方法](../../../../core/servers/deploy/configure/configure-discovery-methods.md)內，尋找設定每一種方法的指引。  
