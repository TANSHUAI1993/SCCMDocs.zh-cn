---
title: "移轉作業 | Microsoft Docs"
description: "建立並執行作業，將資料和用戶端移轉至 System Center Configuration Manager。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: fb8a292c4fecbe5744e2cd09bc1442fab11046bc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="operations-for-migrating-to-system-center-configuration-manager"></a>移轉到 System Center Configuration Manager 的作業

*適用於：System Center Configuration Manager (最新分支)*

若在 System Center Configuration Manager 中進行移轉，在您成功從支援來源階層中的來源站台收集資料後，即可移轉資料和用戶端。 使用下列各節中的資訊建立和執行可移轉資料和用戶端的移轉作業，然後完成移轉程序。  

-   [建立和編輯移轉作業](#Create_Edit_migration_Jobs)  

-   [執行移轉作業](#Run_Migration_Jobs)  

-   [升級或重新指派共用發佈點](#BKMK_ProcUpgrdSS)  

-   [在移轉工作區中監視移轉活動](#Monitor_MIgration)  

-   [移轉用戶端](#BKMK_MigrateClients)  

-   [完成移轉](#Complete_Migration)  

##  <a name="Create_Edit_migration_Jobs"></a> 建立和編輯移轉作業  
 請依照下列程序建立移轉作業、編輯以集合為基礎的移轉作業之排除清單、設定共用發佈點，以及編輯移轉作業排程。  

> [!NOTE]  
>  下列程序適用於建立依集合移轉的移轉作業，僅適用於執行可支援 Configuration Manager 2007 之版本的來源階層。 從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層移轉時，不會提供集合式的移轉作業類型。  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>建立依集合移轉的移轉作業  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [移轉]，然後選擇 [移轉作業]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立移轉作業]。  

4.  在 [建立移轉作業精靈] 的 [一般] 頁面上設定下列各項，然後選擇 [確定]：  

    -   指定移轉作業的名稱。  

    -   在 [作業類型]  下拉式清單中選取 [集合移轉] 。  

5.  在 [選取集合] 頁面上設定下列各項，然後選擇 [下一步]：  

    -   選取要移轉的集合。  

    -   如果只要移轉集合，而不移轉與這些集合相關聯的物件，請取消核取 [移轉與指定的集合相關聯的物件]。 如果取消核取此選項，此作業不會移轉任何相關聯的物件，您也可以略過步驟 6 和 7。  

6.  在 [選取物件] 頁面上，取消核取所有物件類型，或您不要移轉的特定可用物件。 預設會選取所有相關聯物件類型和可用物件。 選擇 [下一步]。  

7.  在 [內容擁有權] 頁面上，將每個所列來源站台的內容擁有權指派至目的地階層中的站台，然後選擇 [下一步]。  

8.  在 [安全性範圍] 頁面上，選取一個或多個以角色為基礎的系統管理安全性範圍，指派至此移轉作業中要移轉的物件，然後選擇 [下一步]。  

9. 在 [集合限制] 頁面上，設定目的地階層的集合以限制每個所列集合的範圍，然後選擇 [下一步]。 如果未列出任何集合，請選擇 [下一步]。  

10. 在 [站台碼取代] 頁面上，指派目的地階層的站台碼以取代每個所列集合的 Configuration Manager 2007 站台碼，然後選擇 [下一步]。 如果未列出任何集合，請選擇 [下一步]。  

11. 在 [檢閱資訊] 頁面上，選擇 [儲存到檔案]，儲存顯示的資訊供之後檢視。 準備好繼續進行時，請選擇 [下一步]。  

12. 在 [設定] 頁面上，設定移轉作業執行時間，並選擇此移轉作業所需的任何其他設定，然後選擇 [下一步]。  

13. 確認設定並完成精靈。  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>建立依物件移轉的移轉作業  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [移轉]，然後選擇 [移轉作業]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立移轉作業]。  

4.  在 [建立移轉作業精靈] 的 [一般] 頁面上設定下列各項，然後選擇 [下一步]：  

    -   指定移轉作業的名稱。  

    -   在 [作業類型]  下拉式清單中選取 [物件移轉] 。  

5.  在 [選取物件]  頁面中，選取要移轉的物件類型。 根據預設，您每選取一種物件類型，也會一併選取其所有可用物件。  

6.  在 [內容擁有權] 頁面上，將每個所列來源站台的內容擁有權指派至目的地階層中的站台，然後選擇 [下一步]。 如果未列出任何來源站台，請選擇 [下一步]。  

7.  在 [安全性範圍] 頁面上，選取一個或多個以角色為基礎的系統管理安全性範圍，指派至此移轉作業中的物件，然後選擇 [下一步]。  

8.  在 [檢閱資訊] 頁面上，選擇 [儲存到檔案]，儲存顯示的資訊供之後檢視。 準備好繼續進行時，請選擇 [下一步]。  

9. 在 [設定] 頁面上，設定移轉作業執行時間，以及選擇此移轉作業所需的任何其他設定。 然後選擇 [下一步]。  

10. 確認設定並完成精靈。  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>建立移轉已變更物件的移轉作業  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [移轉]，然後選擇 [移轉作業]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立移轉作業]。  

4.  在 [建立移轉作業精靈] 的 [一般] 頁面上設定下列各項，然後選擇 [下一步]：  

    -   指定移轉作業的名稱。  

    -   在 [作業類型] 下拉式清單中選取 [移轉後修改的物件]。  

5.  在 [選取物件]  頁面中，選取要移轉的物件類型。 根據預設，您每選取一種物件類型，也會一併選取其所有可用物件。  

6.  在 [內容擁有權] 頁面上，將每個所列來源站台的內容擁有權指派至目的地階層中的站台，然後選擇 [下一步]。 如果未列出任何來源站台，請選擇 [下一步]。  

7.  在 [安全性範圍] 頁面上，選取一個或多個以角色為基礎的系統管理安全性範圍，指派至此移轉作業中的物件，然後選擇 [下一步]。  

8.  在 [檢閱資訊] 頁面上，選擇 [儲存到檔案]，儲存顯示的資訊供之後檢視。 準備好繼續進行時，請選擇 [下一步]。  

9. 在 [設定] 頁面上，設定移轉作業執行時間，以及選擇此移轉作業所需的任何其他設定。 不同於其他移轉作業類型，此移轉作業必須覆寫 System Center Configuration Manager 資料庫中先前移轉的物件。 選擇 [下一步]。  

10. 確認設定，然後完成精靈。  

###  <a name="BKMK_Modify_Exclusion_List"></a> 修改移轉排除清單  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，選擇 [移轉] 以存取排除清單。 您也可以從 [來源階層]  或 [移轉作業]  節點存取排除清單。  

3.  在 [首頁] 索引標籤的 [移轉] 群組中，選擇 [編輯排除清單]。  

4.  在 [編輯排除清單] 對話方塊中，選取要從排除清單中移除的排除物件，然後選擇 [移除]。  

5.  選擇 [確定] 儲存變更，並且完成編輯。 若要取消目前的變更並還原已移除的所有物件，請選擇 [取消]，然後選擇 [否]。 這樣會取消移除物件，並且關閉 [編輯排除清單]  對話方塊。  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>共用來源階層的發佈點  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [移轉]，並選擇 [來源階層]，然後選取要設定的來源站台。  

3.  在 [首頁] 索引標籤的 [來源站台] 群組中，選擇 [設定]。  

4.  在 [來源站台認證] 對話方塊上，選取 [啟用來源站台伺服器的發佈點共用]，然後選擇 [確定]。  

5.  資料收集完成時，請選擇 [關閉]。  

#### <a name="change-the-schedule-of-a-migration-job"></a>變更移轉作業的排程  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [移轉]，然後選擇 [移轉作業]。  

3.  選擇要變更的移轉作業。 在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

4.  在移轉作業的內容中，選取 [設定] 索引標籤，並變更移轉作業的執行時間，然後選擇 [確定]。  

##  <a name="Run_Migration_Jobs"></a> 執行移轉作業  
 利用下列程序執行尚未開始的移轉作業。  


1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [移轉]，然後選擇 [移轉作業]。  

3.  選擇要執行的移轉作業。 在 [首頁] 索引標籤的 [移轉作業] 群組中，選擇 [開始]。  

4.  選擇 [是]，開始移轉作業。  

##  <a name="BKMK_ProcUpgrdSS"></a> 升級或重新指派共用發佈點  
 您可以升級 Configuration Manager 2007 來源站台所共用的支援發佈點，也可以將 System Center Configuration Manager 來源站台所共用的支援發佈點重新指派為目的地階層中的發佈點。  

> [!IMPORTANT]  
>  升級 Configuration Manager 2007 子目錄發佈點之前，必須解除安裝子目錄發佈點電腦上的 Configuration Manager 2007 用戶端軟體。 如果在嘗試升級發佈點時安裝 Configuration Manager 2007 用戶端軟體，升級會失敗，並且會自電腦移除先前部署至子目錄發佈點的內容。  

> [!CAUTION]  
>  升級或重新指派共用發佈點時，會自來源站台移除發佈點站台系統角色和站台系統電腦，並新增為所選目的地階層中站台的發佈點。  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>升級或重新指派共用發佈點  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [移轉]，然後選擇 [來源階層]。  

3.  選取擁有要升級之發佈點的站台，並選擇 [共用發佈點] 索引標籤，然後選取要升級或重新指派的合格發佈點。  

4.  在 [發佈點] 索引標籤的 [發佈點] 群組中，選擇 [重新指派]。  

5.  在 [重新指派共用發佈點精靈] 中指定設定，如同要安裝新的目的地階層發佈點，只不過再增加下列步驟：  

    -   在 [內容轉換] 頁面上，檢閱轉換現有內容所需空間的指引。 接著，在精靈的 [磁碟機設定] 頁面上，確定所選發佈點電腦的磁碟機包含所需的可用磁碟空間量。  

6.  確認設定，然後完成精靈。  

##  <a name="Monitor_MIgration"></a> 在移轉工作區中監視移轉活動  
 使用 Configuration Manager 主控台監視移轉。  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [移轉]，然後選擇 [移轉作業]。  

3.  選擇要監視的移轉作業。  

4.  在 [摘要]  和 [作業中的物件] 索引標籤中，檢視有關所選移轉作業的詳細資料和狀態。  

##  <a name="BKMK_MigrateClients"></a> 移轉用戶端  
 您在階層之間移轉用戶端的資料之後，但是尚未完成移轉之時，請規劃將用戶端移轉至目的地階層。 在階層之間移轉用戶端時會需要解除安裝指派至來源階層之電腦上的 Configuration Manager 用戶端軟體，然後從目的地階層安裝 Configuration Manager 用戶端軟體。 當您從目的地階層安裝用戶端時，您也會將用戶端指派至該階層的主要站台。 如需移轉用戶端的詳細資訊，請參閱[規劃 System Center Configuration Manager 的用戶端移轉策略](../../core/migration/planning-a-client-migration-strategy.md)。  

##  <a name="Complete_Migration"></a> 完成移轉  
 使用此程序完成從來源階層移轉的作業。  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [移轉]，然後選擇 [來源階層]。  

3.  若為 Configuration Manager 2007 來源階層，請選取位於來源階層底層的來源站台。 針對 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層，選取可用的來源站台。  

4.  在 [首頁] 索引標籤的 [清理] 群組中，選擇 [停止收集資料]。  

5.  選擇 [是] 確認該動作。  

6.  繼續下個步驟前，針對 Configuration Manager 2007 來源階層重複步驟 3、4 和 5。 從階層底部到頂端，在階層的每個站台中執行這些步驟。 針對 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層，繼續下個步驟。  

7.  在 [首頁] 索引標籤的 [清理] 群組中，選擇 [清理移轉資料]。  

8.  在 [清理移轉資料] 對話方塊上，從 [來源階層] 下拉式清單中選取來源階層頂層站台的站台碼和站台伺服器，然後選擇 [確定]。  

9. 選擇 [是] 完成來源階層的移轉程序。  
