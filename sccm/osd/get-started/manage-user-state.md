---
title: "管理使用者狀態 - Configuration Manager| Microsoft Docs"
description: "System Center Configuration Manager 以使用者狀態移轉工具來擷取及還原作業系統部署案例中的使用者狀態資料。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: a0bd86587669c32377b1eafa6a890d37e10ac3f6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-user-state-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理使用者狀態

*適用對象：System Center Configuration Manager (最新分支)*

您可以使用 System Center Configuration Manager 工作順序來擷取和還原作業系統部署案例 (您想保留目前作業系統的使用者狀態) 中的使用者狀態資料。 例如：  

-   您想要從某部電腦擷取使用者狀態，並將其還原到另一部電腦上的部署。  

-   更新部署，在這類部署中您會在同一部電腦上擷取和還原使用者狀態。  

 Configuration Manager 以使用者狀態移轉工具 (USMT) 10.0 來管理在作業系統安裝完成後，從來源電腦將使用者狀態資料移轉至目的地電腦。 如需 USMT 10.0 一般移轉案例的相關資訊，請參閱  [常見移轉案例](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)。  

 請使用下列區段以利擷取與還原使用者資料。


##  <a name="BKMK_StoringUserData"></a> 儲存使用者狀態資料  
 當您擷取使用者狀態時，可以在目的地電腦上或狀態移轉點上儲存使用者狀態資料。 若要在使用者狀態移轉點上儲存使用者狀態，您必須使用裝載狀態移轉點站台系統角色的 Configuration Manager 站台系統伺服器。 若要在目的地電腦上儲存使用者狀態，您必須將工作順序設定為使用連結在本機儲存資料。  

> [!NOTE]  
>  用於在本機儲存使用者狀態的連結，稱為永久連結。 永久連結是 USMT 10.0 的一項功能，會掃描電腦的使用者檔案和設定，然後針對這些檔案建立永久連結的目錄。 接著，您可以在部署新的作業系統後，使用永久連結來還原使用者資料。  

> [!IMPORTANT]  
>  您不能同時使用狀態移轉點和永久連結來儲存使用者狀態資料。  

 擷取到使用者狀態資訊後，可以運用下列任一方法儲存擷取到的資訊：  

-   您可以設定狀態移轉點來遠端存放使用者狀態資料。 [擷取]  工作順序會將資料傳送至狀態移轉點。 等到作業系統部署完畢後，[還原]  工作順序就會擷取資料並還原目的地電腦上的使用者狀態。  

-   您可以將使用者狀態資料存放在本機的特定位置。 在此案例中，[擷取]  工作順序會將使用者資料複製到目的地電腦上的特定位置。 等到作業系統部署完畢後，[還原]  工作順序便會從該位置擷取使用者資料。  

-   您可以指定能用於將使用者資料還原至原始位置的永久連結。 在此案例中，移除舊的作業系統後，使用者資料仍保留在磁碟中。 接著，等到新的作業系統部署完畢後，[還原]  工作順序會利用永久連結將使用者狀態資料還原至原始位置。  

###  <a name="BKMK_UserDataSMP"></a> 在狀態移轉點上儲存使用者資料  
 若要在狀態移轉點上儲存使用者狀態資料，您必須執行下列作業：  

1.  [Configure a state migration point](#BKMK_StateMigrationPoint) 以儲存使用者狀態資料。  

2.  在來源電腦和目的地電腦之間[Create a computer association](#BKMK_ComputerAssociation) 。 您必須先建立此關聯，才可以在來源電腦上擷取使用者狀態。  

3.  [在 System Center Configuration Manager 中建立工作順序以擷取和還原使用者狀態](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)。 具體來說，您必須新增下列工作順序步驟，以從電腦擷取使用者資料、將使用者資料儲存在狀態移轉點上，然後將使用者資料還原到電腦：  

    -   [要求狀態存放區](../understand/task-sequence-steps.md#BKMK_RequestStateStore)要求在從電腦擷取狀態，或是將狀態還原至電腦時，能夠存取狀態移轉點。  

    -   [擷取使用者狀態](../understand/task-sequence-steps.md#BKMK_CaptureUserState)擷取和還原狀態移轉點上的使用者狀態資料。  

    -   [還原使用者狀態](../understand/task-sequence-steps.md#BKMK_RestoreUserState)從使用者狀態移轉點擷取資料，在目的地電腦上還原使用者狀態。  

    -   [釋放狀態存放區](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)通知狀態移轉點，擷取或還原動作已完成。  

###  <a name="BKMK_UserDataDestination"></a> 在本機儲存使用者資料  
 若要在本機儲存使用者狀態資料，您必須執行下列作業：  

-   [建立工作順序擷取和還原使用者狀態](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)。 具體來說，您必須新增下列工作順序步驟，以從電腦擷取使用者資料，然後使用永久連線將使用者資料還原到電腦：  

    -   [擷取使用者狀態](../understand/task-sequence-steps.md#BKMK_CaptureUserState)使用永久連結，擷取和儲存使用者狀態資料至本機資料夾。  

    -   [還原使用者狀態](../understand/task-sequence-steps.md#BKMK_RestoreUserState)以使用永久連結擷取資料，在目的地電腦上還原使用者狀態。  

        > [!NOTE]  
        >  永久連結參照的使用者狀態資料在工作順序移除舊的作業系統後，仍會保留在電腦上。 這個資料在部署新的作業系統後，可用來還原使用者狀態。  

##  <a name="BKMK_StateMigrationPoint"></a> Configure a state migration point  
 狀態移轉點會儲存在某台電腦上擷取到的使用者狀態資料，再將資料還原至另一台電腦。 不過，當您擷取同一部電腦之作業系統部署的使用者設定時 (例如目的地電腦的部署，在此重新整理作業系統)，您可以使用永久連結將資料儲存在同一部電腦，或是在狀態移轉點上。 進行部分電腦部署時，若要建立狀態存放區，Configuration Manager 會自動在狀態存放區和目的地電腦之間建立關聯。 您可以使用下列方法，將狀態移轉點設定為儲存使用者狀態資料：  

-   使用 [建立站台系統伺服器精靈]  ，為狀態管理點建立新的站台系統伺服器。  

-   使用 [新增站台系統角色精靈]  ，將狀態移轉點新增至現有伺服器。  

 當您使用這些精靈時，系統會提示您為狀態移轉點提供下列資訊：  

-   用於儲存使用者狀態資料的資料夾。  

-   狀態移轉點上可儲存資料的用戶端數目上限。  

-   狀態移轉點用於儲存使用者狀態資料的最小可用空間。  

-   角色的刪除原則。 您可以指定是要在還原於電腦後立刻刪除使用者狀態資料，或是在將使用者資料還原到電腦後的特定天數後再將其刪除。  

-   狀態移轉點是否只回應還原使用者狀態資料的要求。 當您啟用此選項時，將無法使用狀態移轉點來儲存使用者狀態資料。  

 如需狀態移轉點和其設定步驟的詳細資訊，請參閱[狀態移轉點](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)。  

##  <a name="BKMK_ComputerAssociation"></a> Create a computer association  
 當您在新硬體上安裝作業系統，而且想要擷取及還原使用者資料和設定時，請建立電腦關聯以定義來源電腦和目的電腦之間的關聯性。 來源電腦是 Configuration Manager 管理的現有電腦。 當您將新的作業系統部署至目的地電腦時，來源電腦會包含移轉至目的地電腦的使用者狀態。  

> [!NOTE]  
>  您無法在位於 Configuration Manager 父站台的電腦與位於子站台的電腦之間建立電腦關聯。 電腦關聯為站台特定，且不會複寫。  

#### <a name="to-create-a-computer-association"></a>建立電腦關聯  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [使用者狀態移轉] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立電腦關聯] 。  

4.  在 [電腦關聯內容]  對話方塊的 [電腦關聯]  索引標籤上，指定要擷取其使用者狀態的來源電腦，以及要還原使用者狀態資料的目的地電腦。  

5.  在 [使用者帳戶]  索引標籤上，指定要移轉至目的地電腦的使用者帳戶。 指定下列其中一項設定：  

    -   **擷取和還原所有使用者帳戶**：此設定會擷取和還原所有使用者帳戶。 使用此設定建立多個與相同來源電腦的關聯。  

    -   **擷取所有使用者帳戶並還原指定的帳戶**：此設定會擷取來源電腦上的所有使用者帳戶，並只還原您在目的地電腦上指定的帳戶。 另外，若想要與相同來源電腦建立多個關聯，您可以使用此設定。  

    -   **擷取和還原指定的使用者帳戶**：此設定只會擷取及還原您所指定的帳戶。 您無法在選取此設定時，對相同來源電腦建立多個關聯。  

##  <a name="BKMK_MigrationFails"></a> 在作業系統部署失敗時還原使用者狀態資料  
 如果作業系統部署失敗，可使用 USMT 10.0 LoadState 功能以擷取在部署程序中所擷取的使用者狀態資料。 這包括在狀態移轉點上儲存的資料，或是本機儲存在目的地電腦上的資料。 如需 USMT 功能的詳細資訊，請參閱 [LoadState 語法](https://technet.microsoft.com/library/mt299188\(v=vs.85\).aspx)。  
