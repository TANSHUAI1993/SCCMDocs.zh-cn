---
title: "移轉資料 | Microsoft Docs"
description: "了解如何將資料從來源階層傳送至 System Center Configuration Manager 目的地階層。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: dface33392c2a2a662522656eabf0936b52b28fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="migrate-data-between-hierarchies-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 階層間移轉資料

*適用於：System Center Configuration Manager (最新分支)*

使用移轉，將資料從支援的來源階層傳送至您的 System Center Configuration Manager 目的地階層。  當您從來源階層移轉資料時︰  

-   您從來源基礎結構中所識別的站台資料庫存取資料，然後將該資料傳送到目前的環境。  

-   移轉並不會變更來源階層中的資料，而是會探索該資料並在目的地階層的資料庫中儲存資料複本。  

在規劃移轉策略時，請考慮下列事項：  

-   您可以將現有 Configuration Manager 2007 SP2 基礎結構移轉至 System Center Configuration Manager。  

-   您可以從來源站台移轉部分或所有支援的資料。  

-   您可以從單一來源站台將資料移轉至目的地階層中數個不同的站台。  

-   您可以將資料從多個來源站台移至目的地階層中的單一站台。  

##  <a name="BKMK_MigrationConcepts"></a> 移轉的概念  
 使用移轉時，可能會遇到下列概念和詞彙。  

|概念或詞彙|詳細資訊|  
|---------------------|----------------------|  
|來源階層|此階層會執行 Configuration Manager 的受支援版本，並包含您想要移轉的資料。 當您設定移轉時，會在指定來源階層的頂層站台時識別來源階層。 指定來源階層後，目的地階層的底層站台會從指定來源站台的資料庫收集資料，以識別您可以移轉的資料。<br /><br /> 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃來源階層策略](../../core/migration/planning-a-source-hierarchy-strategy.md)中的[來源階層](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies)。|  
|來源站台|來源階層中的站台，可以讓您用來將資料移轉到目的地階層。<br /><br /> 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃來源階層策略](../../core/migration/planning-a-source-hierarchy-strategy.md)中的[來源站台](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites)。|  
|目的地階層|System Center Configuration Manager 階層，是為了從來源階層匯入資料而執行移轉的位置。|  
|資料收集|正在進行對來源階層的識別程序，此來源階層可以移轉到目的地階層。 Configuration Manager 會定期檢查來源階層，識別來源階層中您之前移轉過的資訊有無任何變化，同時也會識別在目的地階層中您可能想要更新的資訊。<br /><br /> 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃來源階層策略](../../core/migration/planning-a-source-hierarchy-strategy.md)中的[資料收集](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)。|  
|移轉作業|設定移轉特定物件，然後管理將這些物件移轉至目的地階層的程序。<br /><br /> 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃移轉作業策略](../../core/migration/planning-a-migration-job-strategy.md)|  
|用戶端移轉|從來源站台的資料庫將用戶端使用的資訊傳送到目的地階層資料庫的程序。 此資料移轉後隨即會將裝置上用戶端軟體升級為目的地階層的用戶端軟體版本。<br /><br /> 如需詳細資訊，請參閱 [在 System Center Configuration Manager 中規劃移轉作業策略](../../core/migration/planning-a-client-migration-strategy.md)。|  
|共用發佈點|在移轉期間，來源階層中與目的地階層共用的發佈點。<br /><br /> 在移轉期間，指派至目的地階層之站台的用戶端可以透過共用發佈點取得資訊。<br /><br /> 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃內容部署移轉策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)中的[在來源與目的地階層間共用發佈點](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)。|  
|監視移轉|監視移轉活動的程序。 您可以在 [系統管理] 工作區的 [移轉] 節點監視移轉進度和成功與否。<br /><br /> 如需詳細資訊，請參閱[規劃在 System Center Configuration Manager 中監視移轉活動](../../core/migration/planning-to-monitor-migration-activity.md)。|  
|停止收集資料|停止從來源站台收集資料的程序。 當您不再需要從來源階層移轉資料，或者想要暫停進行移轉相關活動時，可以將目的地階層設定為停止從來源階層收集資料。<br /><br /> 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃來源階層策略](../../core/migration/planning-a-source-hierarchy-strategy.md)中的[資料收集](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)。|  
|清除移轉資料|移除從目的地階層資料庫移轉的相關資訊，以完成從來源階層進行移轉的程序。<br /><br /> 如需詳細資訊，請參閱 [規劃在 System Center Configuration Manager 中完成移轉](../../core/migration/planning-to-complete-migration.md)。|  

## <a name="typical-workflow-for-migration"></a>移轉的一般工作流程  
設定移轉的工作流程：

1.  指定受支援的來源階層。  

2.  設定資料收集。 資料收集可讓 Configuration Manager 收集可從來源階層移轉之資料的相關資訊。  

     在您停止資料收集程序之前，Configuration Manager 會自動按照簡單的排程重複資料收集程序。 根據預設，資料收集程序每四小時重複一次，以便 Configuration Manager 能夠在來源階層中識別到您可能要移轉的資料有何變化。 要在目的地階層共用來源階層的發佈點，資料收集也是必要的程序。  

3.  建立移轉作業，在來源和目的地階層之間移轉資料。  

4.  您隨時可以使用 [停止收集資料]  命令停止資料收集程序。 停止收集資料時，Configuration Manager 不會再識別來源階層中的資料有何變化，也不能再讓來源和目的地階層共用發佈點。 通常，當您不想再移轉資料或共用來源階層的發佈點時，就可以使用此動作。  

5.  來源階層中所有站台的資料收集皆停止後，您可以選擇使用 [清除移轉資料]  命令清除移轉資料。 這個命令會從目的地階層的資料庫中刪除從來源階層進行移轉的相關歷程資料。  

從不再用於管理環境的 Configuration Manager 來源階層移轉資料後，您可以解除委任該來源階層和基礎結構。  

##  <a name="BKMK_MigrationScenarios"></a> 移轉案例  
 Configuration Manager 支援下列移轉案例。  

> [!NOTE]  
>  將包含獨立站台的階層擴充為包含管理中心網站的階層並不屬於移轉。 如需階層擴充的相關資訊，請參閱[使用安裝精靈安裝站台](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)中的[擴充獨立主要站台](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)。  

### <a name="migration-from-configuration-manager-2007-hierarchies"></a>從 Configuration Manager 2007 階層移轉  
 當您使用移轉功能從 Configuration Manager 2007 移轉資料時，可以將投資保留在現有的站台基礎結構中，並且獲得下列優勢：  

|優勢|詳細資訊|  
|-------------|----------------------|  
|站台資料庫的改善|System Center Configuration Manager 資料庫支援完整 Unicode。|  
|站台間的資料庫複寫|System Center Configuration Manager 中的複寫是以 Microsoft SQL Server 為基礎。 這樣能夠提升站台對站台資料傳送的效能。|  
|使用者為中心的管理|使用者聚焦於 System Center Configuration Manager 中的管理工作。 例如，即使不知道使用者的裝置名稱，您仍然可以將軟體發佈給該使用者。 此外，System Center Configuration Manager 讓使用者能夠進一步控制要將哪些軟體安裝在其裝置中，以及安裝軟體的時間。|  
|階層簡化|在 System Center Configuration Manager 中，管理中心網站類型以及主要與次要站台的行為變更，可讓您建立較簡化的站台階層，使用的頻寬及需要的伺服器數量皆可減少。|  
|以角色為基礎的系統管理|System Center Configuration Manager 採用的這種中央安全性模式可用於根據您的系統管理及商務需求防護及管理整個階層。|  

> [!NOTE]  
>  因為 System Center 2012 Configuration Manager 中第一次引進的設計變更，所以您無法將 Configuration Manager 2007 基礎結構升級至 System Center Configuration Manager。 支援從 System Center 2012 Configuration Manager 就地升級至 System Center Configuration Manager。  

### <a name="migration-from-configuration-manager-2012-or-another-system-center-configuration-manager-hierarchy"></a>從 Configuration Manager 2012 或其他 System Center Configuration Manager 階層進行移轉  
 從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 階層移轉資料的程序相同。 其中包括從多個來源階層移轉至單一目的地階層，例如當公司取得由 Configuration Manager 管理的額外資源時。 此外，您可以將資料從測試環境移轉至 Configuration Manager 生產環境。 這樣可讓您將投資保存在 Configuration Manager 測試環境中。  

## <a name="additional-topics-for-migration"></a>其他的移轉主題：  

-   [規劃移轉至 System Center Configuration Manager](../../core/migration/planning-for-migration.md)  

-   [設定來源階層和來源站台以移轉到 System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [移轉至 System Center Configuration Manager 的作業](../../core/migration/operations-for-migration.md)  

-   [移轉至 System Center Configuration Manager 的安全性和隱私權](../../core/migration/security-and-privacy-for-migration.md)  

## <a name="see-also"></a>另請參閱  
 [開始使用 System Center Configuration Manager](../../core/servers/deploy/start-using.md)
