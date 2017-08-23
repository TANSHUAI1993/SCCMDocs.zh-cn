---
title: "移轉檢查清單 | Microsoft Docs"
description: "使用系統管理員檢查清單可協助您規劃 System Center Configuration Manager 的移轉策略。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 36f7c37e4da3f2bce64a25d266dae57d9fe98c36
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="administrator-checklists-for-migration-planning-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的系統管理員移轉規劃檢查清單

*適用於：System Center Configuration Manager (最新分支)*

使用下列系統管理員檢查清單可協助您規劃 System Center Configuration Manager 的移轉策略。

##  <a name="Checklist_Migraiton_Planning"></a> 系統管理員移轉規劃檢查清單  
 請使用下列移轉前規劃步驟檢查清單。  

-   **評估目前的環境：**  

     找出來源階層可能符合的現有商業需求，並且研發在目的地階層中仍能繼續符合這些需求的計劃。  

-   **檢閱所用之 Configuration Manager 版本的功能和變更，運用這項資訊輔助設計目的地階層：**  

    如需詳細資訊，請參閱 [System Center Configuration Manager 的基礎](../../core/understand/fundamentals.md) 和 [System Center Configuration Manager 的新功能](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)。  


-   **判斷以角色為基礎的系統管理適用的系統管理安全性模式：**  

    如需詳細資訊，請參閱 [System Center Configuration Manager 以角色為基礎之系統管理的基礎](../../core/understand/fundamentals-of-role-based-administration.md)。  

-   **評估網路及 Active Directory 拓撲：**檢閱現有的網域結構和網路拓撲，並且考量這些資訊對於階層設計和移轉作業會造成的影響。  

-   **完成目的地階層最終設計：**  

    決定管理中心網站、主要站台、次要站台及內容發佈選項的位置。  

-   **將階層對應於目的地階層中作為站台和站台伺服器的電腦：**  

    找出站台和站台系統伺服器在目的地階層中將使用的電腦，然後確定這些電腦的容量足以符合現有及未來的運作需求。  

-   **規劃物件移轉策略：**  

    規劃以可用的移轉作業移轉不同物件，包括站台界限、集合、公告及部署。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃移轉作業策略](../../core/migration/planning-a-migration-job-strategy.md)中的[移轉作業的類型](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration)。  

    Configuration Manager 只會移轉您選取的物件。 如未移轉目的地階層中所需的物件，即須在目的地階層中重新建立該物件。  

    當您設定移轉作業時，會顯示可移轉的物件。  

-   **規劃用戶端移轉策略：**  

    規劃使用能在您將用戶端移轉至目的地階層時，限制網路頻寬和伺服器處理需求的控制方法來移轉用戶端。 如需規劃用戶端移轉策略的詳細資訊，請參閱[在 System Center Configuration Manager 中規劃用戶端移轉策略](../../core/migration/planning-a-client-migration-strategy.md)。  

-   **規劃清查和相容性資料：**  

    Configuration Manager 不支援移轉硬體清查、軟體清查，也不支援移轉軟體更新或用戶端所需的設定管理相容性資料。  

    反之，用戶端移轉至設計階層中的新站台並接收這些組態的原則後，就會將此資訊提交至指派的站台。 此動作會在目的地站台資料庫中填入目前的清查和相容性資料。  

-   **規劃完成從來源階層移轉的作業：**  

    決定移轉物件和用戶端的時間。 移轉完成後，即可規劃解除委任來源階層中的站台伺服器。  

##  <a name="Checklist_Hierarchy_for_migration"></a> 系統管理員階層移轉檢查清單  
開始移轉前，請使用下列檢查清單輔助規劃目的地階層。  

-   **找出要在目的地階層中使用的電腦：**  

    Configuration Manager 不支援從 Configuration Manager 2007 基礎結構就地升級。 因此，請改用移轉，將資料從 Configuration Manager 2007 移至 System Center Configuration Manager。 您需要使用並存部署，並在新電腦上安裝 System Center Configuration Manager。  

    同樣地，從另一個 System Center Configuration Manager 階層移轉時，必須安裝並存部署至來源階層的新目的地階層。  

-   **建立目的地階層：**  

    若要準備移轉，請安裝並設定包含主要站台的 System Center Configuration Manager 目的地階層。 例如：  

    -   安裝管理中心網站，然後至少安裝一個子主要站台。  

    -   如果不想使用管理中心網站，請安裝獨立主要站台。  

-   **如果想移轉與軟體更新相關的資訊，請在目的地階層中設定軟體更新點，然後同步處理軟體更新：**  

    您必須先在目的地階層中設定及同步處理軟體更新，才能從來源階層移轉軟體更新資訊。  


-   **在目的地階層中安裝與設定其他站台系統角色：**  

    設定您需要的其他站台系統角色和站台系統。  

-   **檢查目的地階層中的操作功能：**  

    檢查下列項目：  

    -   如果目的地階層包含多個站台，請確認站台之間的資料庫複寫功能是否可正常運作。 資料庫複寫不適用於獨立主要站台。  

    -   確認已安裝的站台系統角色均可正常操作。  

    -   確認安裝至目的地階層的 Configuration Manager 用戶端可順利與指派的站台通訊。  


##  <a name="Checklisit_Migration"></a> 系統管理員移轉檢查清單  
請依照下列檢查清單，將來源階層的資料移轉至目的地階層。  

-   **啟用目的地階層中的移轉功能：**  

    指定來源階層的頂層站台，以設定來源階層。 如需指定來源站台的詳細資訊，請參閱[在 System Center Configuration Manager 中規劃來源階層策略](../../core/migration/planning-a-source-hierarchy-strategy.md)。  

-   **來源階層執行 Configuration Manager 2007 SP2 時，請選取並設定來源階層中的其他站台：**  

    若要從 Configuration Manager 2007 SP2 來源階層中的其他站台收集資料，必須一一設定每個站台的資料收集認證。 在您設定每個來源站台時，收集程序會立即開始，一直持續到移轉期間內停止收集該站台的資料為止。 資料收集可確保您能夠在來源階層中移轉自上次資料收集程序之後所更新或新增的物件。

    > [!NOTE]  
    >  來源階層執行 System Center 2012 Configuration Manager 或更新版本時，不需要設定其他來源站台。  

-   **設定發佈點共用：**  

    您可以共用兩個階層的發佈點，讓目的地階層中的用戶端能夠取得您所移轉之物件的內容。 這樣可以確保兩個階層中的用戶端均取得同樣的內容，而且您在停止收集資料並完成移轉之前都能夠繼續保存該內容。  

    如需共用發佈點的詳細資訊，請參閱[在 System Center Configuration Manager 中規劃內容部署移轉策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)中的[在來源和目的地階層之間共用發佈點](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)。  

-   **建立並執行移轉作業，以移轉與來源階層中之用戶端相關聯的物件：**  

    建立移轉作業，在兩個階層之間移轉物件。 每個移轉作業所需的設定可能會依該作業所移轉的資料而有所不同。  

    例如，當您移轉內容時，無論使用哪一項移轉作業，都必須指派目的地階層中的站台管理該內容。 指派的站台將從原始來源檔案位置存取該內容，並且必須負責將該內容發佈至目的地階層中的發佈點。  

    如需詳細資訊，請參閱[移轉到 System Center Configuration Manager 的作業](../../core/migration/operations-for-migration.md)中的[建立和編輯 System Center Configuration Manager 的移轉作業](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs)。  

-   **將用戶端移轉至目的地階層：**  

    用戶端移轉程序會依移轉案例而有所不同：  

    -   若要移轉的用戶端與目的地階層使用不同版本的用戶端，就必須升級用戶端軟體。 若要升級，就必須移除目前的 Configuration Manager 用戶端，接著再安裝符合目的地站台的新用戶端版本。  

    -   若要移轉的用戶端和目的地階層使用相同版本的用戶端，則不需要升級或重新安裝用戶端。 用戶端反而會重新指派至目的地階層中的主要站台。  

    將用戶端移轉至目的地階層時，該用戶端會與先前已移轉至該目的地階層且屬於該用戶端的資料建立關聯。  

    如需詳細資訊，請參閱 [在 System Center Configuration Manager 中規劃移轉作業策略](../../core/migration/planning-a-client-migration-strategy.md)。  

-   **升級或重新指派共用發佈點：**  

    當您不再需要支援來源階層中的用戶端時，您可以從 Configuration Manager 2007 來源站台升級共用發佈點，或者從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源站台重新指派共用發佈點。 升級或重新指派發佈點時，站台系統角色會轉換至目的地階層中的主要站台，也會從來源階層中的來源站台移除該發佈點。 升級或重新指派共用發佈點時，內容依然會在發佈點電腦上，您不需要將內容重新部署至目的地階層中的新發佈點。  

    您也可以升級次要站台伺服器上共置的 Configuration Manager 2007 發佈點。 這會移除次要站台且導致目的地階層中只有一個發佈點。  

    如需共用發佈點的詳細資訊，請參閱[在 System Center Configuration Manager 中規劃內容部署移轉策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)中的[在來源和目的地階層之間共用發佈點](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)。  

-   **完成移轉︰**  

    移轉來源階層中所有站台的資料和用戶端，並且升級可用的發佈點後，即可完成移轉。 若要完成移轉，則必須停止在來源階層中的每個來源站台收集資料。 之後，您可以移除不需要的移轉資訊，並且解除委任來源階層基礎結構。 如需詳細資訊，請參閱 [規劃在 System Center Configuration Manager 中完成移轉](../../core/migration/planning-to-complete-migration.md)。  
