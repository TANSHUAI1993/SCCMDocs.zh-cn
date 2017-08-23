---
title: "建立工作順序以擷取和還原使用者狀態 | Microsoft Docs"
description: "使用 System Center Configuration Manager 工作順序來擷取和還原作業系統部署案例中的使用者狀態資料。"
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 4b3668094d576b1b8710f08b384aa2f7c5eb0cca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中建立工作順序以擷取和還原使用者狀態

*適用於︰System Center Configuration Manager (最新分支)*

您可以使用 System Center Configuration Manager 工作順序來擷取和還原作業系統部署案例 (您想保留目前作業系統的使用者狀態) 中的使用者狀態資料。 視您建立的工作順序類型而定，擷取和還原步驟可能會自動新增為工作順序的一部分。 在其他情況下，您可能需要手動新增擷取和還原步驟至工作順序中。 本主題提供必須新增到現有工作順序以擷取和還原使用者狀態資料的步驟。  

##  <a name="BKMK_CaptureRestoreUserState"></a> 如何擷取及還原使用者狀態資料  
 若要擷取及還原使用者狀態，您必須將下列步驟新增到工作順序中：  

-   **要求狀態存放區**：只有在您將使用者狀態儲存在狀態移轉點上時，才需要執行此步驟。  

-   **擷取使用者狀態**：此步驟會擷取使用者狀態資料，並使用連結將其儲存在狀態移轉點或本機。  

-   **還原使用者狀態**：此步驟會在目的地電腦上還原使用者狀態資料。 它可以從使用者狀態移轉點或從目的地電腦擷取資料。  

-   **釋放狀態存放區**：只有在您將使用者狀態儲存在狀態移轉點上時，才需要執行此步驟。 此步驟會將此資料從狀態移轉點移除。  

 使用下列程序，新增擷取使用者狀態和還原使用者狀態所需的工作順序步驟。 如需建立工作順序的詳細資訊，請參閱[管理工作順序以自動化工作](manage-task-sequences-to-automate-tasks.md)。  

#### <a name="to-add-task-sequence-steps-to-capture-the-user-state"></a>新增工作順序步驟以擷取使用者狀態  

1.  在 [工作順序]  清單中，選取工作順序，然後按一下 [編輯] 。  

2.  如果您是使用狀態移轉點來儲存使用者狀態，請新增 [要求狀態存放區]  步驟至工作順序。 在 [工作順序編輯器]  對話方塊中，按一下 [新增] ，指向 [使用者狀態] ，然後按一下 [要求狀態存放區] 。 針對 [要求狀態存放區]  步驟指定下列內容和選項，然後按一下 [套用] 。  

     在 [內容]  索引標籤上，指定下列選項：  

    -   為步驟輸入名稱和描述。  

    -   按一下 [從電腦擷取狀態] 。  

    -   在 [重試次數]  方塊中，指定工作順序在發生錯誤時嘗試擷取使用者狀態資料的次數。  

    -   在 [重試延遲 (以秒為單位)]  方塊中，指定工作順序在重試擷取資料前等待的秒數。  

    -   選取 [如果電腦帳戶無法連線到狀態存放區，則使用網路存取帳戶] 核取方塊，指定是否使用 Configuration Manager [網路存取帳戶](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#a-namebkmknaaa-network-access-account)連線至狀態存放區。  

     在 [選項]  索引標籤上，指定下列選項：  

    -   如果您想要工作順序在步驟失敗時繼續到下一步驟，選取 [發生錯誤時仍繼續]  核取方塊。  

    -   如果發生錯誤，指定讓工作順序繼續進行必須符合的所有條件。  

3.  新增 [擷取使用者狀態]  步驟至工作順序。 在 [工作順序編輯器]  對話方塊中，按一下 [新增] ，指向 [使用者狀態] ，然後按一下 [擷取使用者狀態] 。 針對 [擷取使用者狀態]  步驟指定下列內容和選項，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  當您新增此步驟至工作順序時，還要設定 [OSDStateStorePath]  工作順序變數，以指定儲存使用者狀態資料的位置。 如果將使用者狀態儲存在本機，請勿指定根資料夾，否則可能會導致工作順序失效。 當您將使用者資料儲存在本機時，請一律使用資料夾或子資料夾。 如需此變數的相關資訊，請參閱[擷取使用者狀態工作順序動作變數](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState)。  

     在 [內容]  索引標籤上，指定下列選項：  

    -   為步驟輸入名稱和描述。  

    -   指定包含用於擷取使用者狀態資料之 USMT 來源檔案的套件。  

    -   指定要擷取的使用者設定檔：  

        -   按一下 [使用標準選項擷取所有使用者設定檔]  ，擷取所有使用者設定檔。  

        -   按一下 [自訂要擷取的使用者設定檔]  ，指定要擷取的個別使用者設定檔。 選取包含使用者設定檔資訊的設定檔 (miguser.xml、migsys.xml 或 migapp.xml)。 您不能在此處使用 config.xml 設定檔，但可以使用 OSDMigrageAdditionalCaptureOptions 和 OSDMigrateAdditionalRestoreOptions 變數，將它手動加入 USMT 命令列。

    -   選取 [啟用詳細資訊記錄]  ，指定發生錯誤時要寫入多少資訊到記錄檔。  

    -   選取 [略過使用加密檔案系統 (EFS) 的檔案] 。  

    -   選取 [使用檔案系統存取權進行複製]  以指定下列設定：  

        -   **無法擷取部分檔案時仍繼續**：此設定讓工作順序步驟在無法擷取某些檔案的情況下，仍然可以繼續移轉程序。 如果您停用這個選項而且無法擷取某個檔案，工作順序步驟就會失敗。 這個選項預設為啟用。  

        -   **不複製檔案而改為使用連結在本機擷取**：此設定可讓您使用 USMT 4.0 提供的永久連結移轉功能。 如果您使用的 USMT 版本比 USMT 4.0 還舊，就會忽略這個選項。  

        -   **在離線模式中擷取 (僅限 Windows PE)**：此選項讓您不需開機至現有作業系統就可從 Windows PE 擷取使用狀態。 如果您使用的 USMT 版本比 USMT 4.0 還舊，就會忽略這個選項。  

    -   選取 [使用磁碟區陰影複製服務 (VSS) 擷取] 。 如果您使用的 USMT 版本比 USMT 4.0 還舊，就會忽略這個選項。  

     在 [選項]  索引標籤上，指定下列選項：  

    -   如果您想要工作順序在步驟失敗時繼續到下一步驟，選取 [發生錯誤時仍繼續]  核取方塊。  

    -   如果發生錯誤，指定讓工作順序繼續進行必須符合的所有條件。  

4.  如果您要使用狀態移轉點來儲存使用者狀態，請將[釋放狀態存放區](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)步驟新增至工作順序。 在 [工作順序編輯器]  對話方塊中，按一下 [新增] ，指向 [使用者狀態] ，然後按一下 [釋放狀態存放區] 。 為 [釋放狀態存放區]  步驟指定下列內容與選項，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  您必須先成功完成 [釋放狀態存放區]  步驟之前執行的工作順序動作，才能開始進行 [釋放狀態存放區]  步驟。  

     在 [內容]  索引標籤上，輸入步驟的名稱與說明。  

     在 [選項]  索引標籤上，指定下列選項。  

    -   如果您想要工作順序在步驟失敗時繼續到下一步驟，選取 [發生錯誤時仍繼續]  核取方塊。  

    -   發生錯誤時，指定讓工作順序繼續進行所必須符合的所有條件。  

 部署此工作順序以擷取目的地電腦上的使用者狀態。 如需如何部署工作順序的相關資訊，請參閱[部署工作順序](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。  

#### <a name="to-add-task-sequence-steps-to-restore-the-user-state"></a>如何新增工作順序步驟以還原使用者狀態。  

1.  在 [工作順序]  清單中，選取工作順序，然後按一下 [編輯] 。  

2.  將[還原使用者狀態](../understand/task-sequence-steps.md#BKMK_RestoreUserState)步驟新增至工作順序。 在 [工作順序編輯器]  對話方塊中，按一下 [新增] ，指向 [使用者狀態] ，然後按一下 [還原使用者狀態] 。 此步驟會建立與狀態移轉點的連線。 為 [還原使用者狀態]  步驟指定下列內容與選項，然後按一下 [確定] 。  

     在 [內容]  索引標籤上，指定下列內容：  

    -   為步驟輸入名稱和描述。  

    -   指定包含 USMT 的套件以還原使用者狀態資料。  

    -   指定要還原的使用者設定檔：  

        -   按一下 [使用標準選項還原所有擷取的使用者設定檔]  以還原所有使用者設定檔。  

        -   按一下 [自訂使用者設定檔還原] 以還原個別使用者設定檔。 選取包含使用者設定檔資訊的設定檔 (miguser.xml、migsys.xml 或 migapp.xml)。 您不能在此處使用 config.xml 設定檔，但可以使用 OSDMigrageAdditionalCaptureOptions 和 OSDMigrateAdditionalRestoreOptions 變數，將它手動加入 USMT 命令列。

    -   選取 [還原本機使用者設定檔]  ，為還原的設定檔提供新密碼。 您無法移轉本機設定檔的密碼。  

        > [!NOTE]  
        >  如果您擁有本機使用者帳戶，同時使用[擷取使用者狀態](../understand/task-sequence-steps.md#BKMK_CaptureUserState)步驟，並選取 [使用標準選項擷取所有使用者設定檔]，則必須選取[還原使用者狀態](../understand/task-sequence-steps.md#BKMK_RestoreUserState)步驟中的 [還原本機使用者設定檔] 設定，否則工作順序將會失敗。  

    -   如果無法還原檔案而您想要繼續執行 [還原使用者狀態]  步驟時，請選取 [無法還原部分檔案時仍繼續]  。  

         如果您使用本機連結還原使用者狀態，而且還原不成功，系統管理使用者可以手動刪除為了還原資料所建立的永久連結，或是可讓工作順序執行 USMTUtils 工具。 如果您使用 USMTUtils 刪除永久連結，請在執行 USMTUtils 後新增[重新啟動電腦](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)步驟。  

    -   選取 [啟用詳細資訊記錄]  ，指定發生錯誤時要寫入多少資訊到記錄檔。  

     在 [選項]  索引標籤上，指定下列選項：  

    -   如果您想要工作順序在步驟失敗時繼續到下一步驟，選取 [發生錯誤時仍繼續]  核取方塊。  

    -   如果發生錯誤，指定讓工作順序繼續進行必須符合的所有條件。  

3.  如果您要使用狀態移轉點來儲存使用者狀態，請將[釋放狀態存放區](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)步驟新增至工作順序。 在 [工作順序編輯器]  對話方塊中，按一下 [新增] ，指向 [使用者狀態] ，然後按一下 [釋放狀態存放區] 。 為 [釋放狀態存放區]  步驟指定下列內容與選項，然後按一下 [確定] 。  

    > [!IMPORTANT]  
    >  您必須先成功完成 [釋放狀態存放區]  步驟之前執行的工作順序動作，才能開始進行 [釋放狀態存放區]  步驟。  

     在 [內容]  索引標籤上，輸入步驟的名稱與說明。  

     在 [選項]  索引標籤上，指定下列選項。  

    -   如果您想要工作順序在步驟失敗時繼續到下一步驟，選取 [發生錯誤時仍繼續]  核取方塊。  

    -   發生錯誤時，指定讓工作順序繼續進行所必須符合的所有條件。  

 部署這項工作順序以還原目的地電腦上的使用者狀態。 如需部署工作順序的相關資訊，請參閱[部署工作順序](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。  

## <a name="next-steps"></a>後續步驟
[監視工作順序部署](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
