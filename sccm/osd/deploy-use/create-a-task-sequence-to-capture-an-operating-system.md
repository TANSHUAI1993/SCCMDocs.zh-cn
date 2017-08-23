---
title: "建立工作順序以擷取作業系統 | Microsoft Docs"
description: "組建和擷取工作順序會建立參照電腦，包含特定的驅動程式和軟體更新與作業系統。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
caps.latest.revision: "19"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: e9320e40b8e5031ffa3da5e5149c7da718cc87d5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-to-capture-an-operating-system-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 建立工作順序以擷取作業系統

*適用對象：System Center Configuration Manager (最新分支)*

當您使用工作順序將作業系統部署到 System Center Configuration Manager 中的電腦時，電腦會安裝您在工作順序中指定的作業系統映像。 若要自訂作業系統映像，使其包含特定驅動程式、應用程式、軟體更新等，您可以使用組建和擷取工作順序，以建立參照電腦，然後從參照電腦擷取作業系統映像。 如果您已經有用於擷取的參照電腦，您可以建立自訂工作順序，以擷取作業系統。 您可以使用下列章節來擷取自訂的作業系統。  

##  <a name="BKMK_BuildCaptureTS"></a> 使用工作順序來建立和擷取參照電腦  
 組建和擷取工作順序會分割並格式化參照電腦、安裝作業系統，以及安裝 Configuration Manager 用戶端、應用程式和軟體更新，然後從參照電腦擷取作業系統。 建立組建和擷取工作順序之前，在發佈點上必須先有與工作順序相關聯的套件，例如應用程式。  

###  <a name="BKMK_CreatePackages"></a> 準備作業系統部署  
 有很多案例可用於將作業系統部署到您環境中的電腦。 在大部分情況下，您將建立工作順序，然後在 [建立工作順序精靈] 中選取 [安裝現有的映像套件]  來安裝作業系統、移轉使用者設定、套用軟體更新及安裝應用程式。 建立工作順序以安裝作業系統之前，下列項目必須先準備就緒：  

-   **必要**  

    -   在 Configuration Manager 主控台中必須有[開機映像](../get-started/manage-boot-images.md)。  

    -   在 Configuration Manager 主控台中必須有[作業系統映像](../get-started/manage-operating-system-images.md)。  

-   **必要 (如果有用到)**  

    -   Configuration Manager 主控台中必須有[驅動程式套件](../get-started/manage-drivers.md)，其包含必要的 Windows 驅動程式，以支援參照電腦上的硬體。 如需管理驅動程式的工作順序步驟詳細資訊，請參閱[使用工作順序來安裝裝置驅動程式](../get-started/manage-drivers.md#BKMK_TSDrivers)。  

    -   [軟體更新](../../sum/get-started/synchronize-software-updates.md)必須在 Configuration Manager 主控台中進行同步處理。  

    -   Configuration Manager 主控台中必須新增[應用程式](../../apps/deploy-use/create-applications.md)。  

###  <a name="BKMK_CreateBuildCaptureTS"></a> 建立組建和擷取工作順序  
 請使用下列程序，以使用工作順序建立參照電腦和擷取作業系統。  

#### <a name="to-create-a-task-sequence-that-builds-and-captures-an-operating-system-image"></a>建立組建和擷取作業系統映像的工作順序  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序]  啟動 [建立工作順序精靈]。  

4.  在 [建立新的工作順序]  頁面上，選取 [建立並擷取參照作業系統映像] 。  

5.  在 [工作順序資訊]  頁面上指定下列設定，然後按 [下一步] 。  

    -   **工作順序名稱**：指定識別工作順序的名稱。  

    -   **描述**：指定工作順序所執行工作的描述，例如工作順序所建立作業系統的描述。  

    -   **開機映像**：指定安裝作業系統映像的開機映像。  

        > [!IMPORTANT]  
        >  開機映像的架構必須與目的地電腦的硬體架構相容。  

6.  在 [安裝 Windows]  頁面上指定下列設定，然後按 [下一步] 。  

    -   **映像套件**：指定包含安裝作業系統所需檔案的作業系統映像套件。  

    -   **映像索引**：指定要安裝的作業系統。 如果作業系統映像包含多個版本，則選取您想要安裝的版本。  

    -   **產品金鑰**：指定要安裝之 Windows 作業系統的產品金鑰。 您可以指定編碼的大量授權金鑰和標準產品金鑰。 如果您使用非編碼的產品金鑰，則必須以破折號 (-) 分隔字元，每 5 個字元為一組。 例如： *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **伺服器授權模式**：指定伺服器授權為 [按照基座] 、[按照伺服器] ，或者不指定授權。 如果伺服器授權為 [按照伺服器] ，請同時指定伺服器連線數目上限。  

    -   指定如何處理部署作業系統時使用的系統管理員帳戶。  

        -   **隨機產生本機系統管理員密碼，並停用所有支援平台上的帳戶**：指定是否要讓 Configuration Manager 建立本機系統管理員帳戶的隨機密碼，並在部署作業系統時停用此帳戶。  

        -   **啟用帳戶並指定本機系統管理員密碼**：指定是否在部署作業系統的所有電腦上，使用相同的本機系統管理員帳戶密碼。  

7.  在 [設定此網路]  頁面指定下列設定，然後按 [下一步] 。  

    -   **加入工作群組**：指定是否在部署作業系統時，將目的地電腦加入工作群組。  

    -   **加入網域**：指定是否在部署作業系統時，將目的地電腦加入網域。 在 [網域] 中，指定網域名稱。  

        > [!IMPORTANT]  
        >  您可以進行瀏覽，尋找本機樹系中的網域，但是必須指定遠端樹系的網域名稱。  

         您也可以指定組織單位 (OU)。 這是選用設定，會指定要建立電腦帳戶所在 OU 的 LDAP X.500 辨別名稱 (如果帳戶尚未存在)。  

    -   **帳戶**：指定具有加入指定網域權限之帳戶的使用者名稱和密碼。 例如： *網域\使用者* 或 *%變數%*。  

        > [!IMPORTANT]  
        >  如果您打算移轉網域設定或工作群組設定，則必須輸入適當的網域認證。  

8.  在 [安裝 Configuration Manager] 頁面上，指定包含來源檔案的 Configuration Manager 用戶端套件，以安裝 Configuration Manager 用戶端，並新增安裝用戶端所需的任何其他內容，然後按一下 [下一步]。  

     如需可用來安裝用戶端的內容詳細資訊，請參閱[關於 Configuration Manager 中的用戶端安裝內容](../../core/clients/deploy/about-client-installation-properties.md)。  

9. 在 [包含更新]  頁面上，指定要安裝必要的軟體更新、所有軟體更新或不安裝軟體更新，然後按 [下一步] 。 如果您指定安裝軟體更新，Configuration Manager 只會將目標軟體更新安裝至目的地電腦為其成員的集合。  

10. 在 [安裝應用程式]  頁面上，指定要安裝在目的地電腦上的應用程式，然後按 [下一步] 。 如果您指定多個應用程式，也可以指定工作順序在特定應用程式安裝失敗時繼續執行。  

11. 在 [系統準備]  頁面指定下列設定，然後按 [下一步] 。  

    -   **套件**：指定內含適當版本 Sysprep 的 Configuration Manager 套件，以用於擷取參照電腦設定。  

         如果您執行的作業系統版本為 Windows Vista 或更新版本，Sysprep 會自動安裝在電腦上，您不需要指定套件。  

12. 在 [映像內容]  頁面上，指定下列作業系統映像的設定，然後按 [下一步] 。  

    -   **建立者**：指定建立作業系統映像的使用者名稱。  

    -   **版本**：指定與作業系統映像相關聯的使用者定義版本號碼。  

    -   **描述**：指定作業系統電腦映像之使用者定義描述。  

13. 在 [擷取映像]  頁面上指定下列設定，然後按 [下一步] 。  

    -   **路徑**：指定用於存放輸出 .WIM 檔案的共用網路資料夾。 此檔案內含的作業系統映像，取決於您利用此精靈所指定的設定。 如果指定內含現有 .WIM 檔案的資料夾，就會覆寫現有檔案。  

    -   **帳戶**：指定 Windows 帳戶，該帳戶擁有儲存映像之網路共用的使用權限。  

14. 完成精靈。  

15. 若要將其他步驟新增至工作順序，請選取您要建立的工作順序，並按一下 [編輯] 。 如需如何編輯工作順序的資訊，請參閱[編輯工作順序](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence)。  

 請使用下列方法之一將工作順序部署至參照電腦：  

-   如果參照電腦為 Configuration Manager 用戶端，則可將組建和擷取工作順序部署至包含參照電腦的集合。 如需如何部署作業系統映像的資訊，請參閱 [Create a task sequence to install an operating system](create-a-task-sequence-to-install-an-operating-system.md) (建立工作順序以安裝作業系統)。  

    > [!NOTE]  
    >  如果工作順序具有磁碟分割工作順序步驟，請勿在部署工作順序時選取 [下載程式]  選項。  

-   如果參照電腦不是 Configuration Manager 用戶端，或如果您想要在參照電腦上手動執行工作順序，請執行 [建立工作順序媒體精靈] 以建立可開機媒體。 如需如何建立可開機媒體的資訊，請參閱[建立可開機媒體](create-bootable-media.md) 。  

##  <a name="BKMK_CaptureExistingRefComputer"></a> 從現有的參照電腦擷取作業系統映像  
 如果您已經有要擷取的參照電腦，您可以建立從參照電腦擷取作業系統的工作順序。 您將使用 [擷取作業系統映像]  工作順序步驟，從參照電腦擷取一或多個映像，並將其存放在指定網路共用上的映像檔 (.wim) 中。 會在 Windows PE 中使用開機映像啟動此參照電腦，並將此參照電腦上的每個硬碟都擷取成 .wim 檔案內的個別映像。 如果參照的電腦中有多個磁碟機，所產生的 .wim 檔案將會包含每個磁碟區的個別映像。 只會擷取格式化為 NTFS 或 FAT32 的磁碟區。 會略過其他格式的磁碟區和 USB 磁碟區。  

 請使用下列程序，從現有的參照電腦擷取作業系統映像。  

#### <a name="to-capture-an-operating-system-from-an-existing-reference-computer"></a>從現有的參照電腦擷取作業系統  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序]  啟動 [建立工作順序精靈]。  

4.  在 [建立新的工作順序]  頁面上，選取 [建立新的自訂工作順序] 。  

5.  在 [工作順序資訊]  頁面上，指定工作順序的名稱和工作順序的描述。  

6.  指定工作順序的開機映像。 此開機映像用於以 Windows PE 啟動參照電腦。  如需詳細資訊，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

7.  完成精靈。  

8.  在 [工作順序] 中，選取自訂工作順序，然後在 [首頁]  索引標籤的 [工作順序]  群組中，按一下 [編輯]  ，以開啟 [工作順序編輯器]。  

9. 只有參照電腦上已安裝 Configuration Manager 用戶端時，才使用此步驟。  

     依序按一下 [新增] 和 [映像]，然後按一下 [[準備 ConfigMgr 用戶端以進行擷取]](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)。 此工作順序步驟會採用參照電腦上的 Configuration Manager 用戶端，並準備此用戶端，以便在執行映像建立程序時進行擷取。  

10. 依序按一下 [新增] 和 [映像]，然後按一下 [[準備 Windows 以進行擷取]](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture)。 此工作順序動作會執行 Sysprep，然後使電腦重新開機至為工作順序指定的 Windows PE 開機映像。 參照電腦絕不能加入網域中，才能順利完成這個動作。  

11. 依序按一下 [新增] 和 [映像]，然後按一下 [[擷取作業系統映像]](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)。  此工作順序步驟將只從 Windows PE 執行，以擷取參照電腦上的硬碟。 請設定工作順序步驟的下列設定。  

    -   **名稱** 和 **描述**：(選擇性) 您可以變更工作順序步驟的名稱，並提供描述。  

    -   **目的地**：指定用於存放輸出 .WIM 檔案的共用網路資料夾。 此檔案內含的作業系統映像，取決於您利用此精靈所指定的設定。 如果指定內含現有 .WIM 檔案的資料夾，就會覆寫現有檔案。  

    -   **描述**、 **版本**和 **建立者**：(選擇性) 提供將擷取映像的詳細資料。  

    -   **擷取作業系統映像帳戶**：指定 Windows 帳戶，該帳戶擁有您所指定網路共用的使用權限。 按一下 [設定]  ，以指定該 Windows 帳戶的名稱。  

     按一下 [確定]  ，結束 [工作順序編輯器]。  

 請使用下列方法之一將工作順序部署至參照電腦：  

-   如果參照電腦為 Configuration Manager 用戶端，則可將工作順序部署至包含參照電腦的集合。 如需如何部署作業系統映像的資訊，請參閱 [Create a task sequence to install an operating system](create-a-task-sequence-to-install-an-operating-system.md) (建立工作順序以安裝作業系統)。  

-   如果參照電腦不是 Configuration Manager 用戶端，或如果您想要在參照電腦上手動執行工作順序，請執行 [建立工作順序媒體精靈] 以建立可開機媒體。 如需如何建立可開機媒體的資訊，請參閱[建立可開機媒體](create-bootable-media.md) 。  

##  <a name="BKMK_BuildandCaptureTSExample"></a> 建立並擷取作業系統映像的工作順序範例  
 使用下表做為指南，您在建立工作順序來建置和擷取作業系統映像。 資料表會協助您決定您的工作順序步驟及如何組織和組織成邏輯群組的那些工作順序步驟的一般順序。 您所建立的工作順序可能與此範例不同，而且可能包含更多或更少的工作順序步驟和群組。  

> [!IMPORTANT]  
>  請一律使用 [建立工作順序精靈] 來建立此類型的工作順序。  

 當您使用 [新增工作順序]  來建立這個新的工作順序時，如果您手動將這些工作順序步驟加入現有工作順序，則此工作順序步驟的某些名稱會與其原本應有的名稱不同。 下表顯示這些名稱的差異：  

|新的工作順序精靈工作順序步驟名稱|對等項目工作序列編輯器中的步驟名稱|  
|------------------------------------------------------|-----------------------------------------------|  
|在 Windows PE 中重新啟動|重新開機到 Windows PE 或硬碟|  
|磁碟分割磁碟 0|格式化和分割磁碟|  
|套用裝置驅動程式|自動套用驅動程式|  
|安裝更新|安裝軟體更新|  
|加入群組|加入網域或工作群組|  
|準備 ConfigMgr 用戶端|準備 ConfigMgr 用戶端以進行擷取|  
|準備作業系統|準備 Windows 以進行擷取|  
|擷取參考機器|擷取作業系統映像|  

|工作順序群組/步驟|參考|  
|-------------------------------|---------------|  
|建立參照電腦- **(新的工作序列群組)**|建立工作序列群組。 工作順序群組會一同保留類似的工作順序步驟，以取得較佳的組織及錯誤控制。<br /><br /> 這個群組包含建置參照電腦時所需的動作。|  
|在 Windows PE 中重新啟動|您可以使用此工作順序步驟來指定目的地電腦的重新啟動選項。 此步驟中會顯示訊息給使用者的電腦將會重新啟動以便繼續進行安裝。<br /><br /> 此步驟中使用唯讀 **_SMSTSInWinPE** 工作順序變數。 如果相關聯的值等於 **false** ，則工作順序步驟將會繼續。|  
|磁碟分割磁碟 0|使用此工作順序步驟指定的動作需要在目的地電腦上的將硬碟格式化。 預設的磁碟編號是 **0**。<br /><br /> 此步驟中使用唯讀 **_SMSTSClientCache** 工作順序變數。 如果 Configuration Manager 用戶端快取不存在，則會執行此步驟。|  
|套用作業系統|使用此工作順序步驟在目的電腦上安裝指定的作業系統映像。 在刪除該磁碟區上的有檔案後，此步驟會將包含於 WIM 檔案中的磁碟區映像套用至目標電腦上對應的循序磁碟區 (但 Configuration Manager 特定控制檔案除外)。|  
|套用 Windows 設定|請使用這項工作順序步驟，設定目的電腦的 Windows 設定組態資訊。|  
|套用網路設定|您可以使用此工作順序步驟來指定目的地電腦的網路或工作群組組態資訊。|  
|套用裝置驅動程式|您他的工作順序步驟來比對並安裝驅動程式做為作業系統部署的一部分。 您可以讓 Windows 安裝程式來搜尋所有現有的驅動程式類別目錄 **考慮所有類別的驅動程式** 或限制哪些驅動程式類別 Windows 安裝程式會藉由選取搜尋 **限制只考慮選取的類別目錄中的驅動程式的驅動程式比對**。<br /><br /> 此步驟中使用唯讀 **_SMSTSMediaType** 工作順序變數。 如果相關聯的值不等於 **FullMedia** 會執行此工作順序步驟。|  
|[安裝套件]|使用此工作順序步驟來安裝 Configuration Manager 用戶端軟體。 Configuration Manager 會安裝並註冊 Configuration Manager 用戶端 GUID。 您可以在 **[安裝內容]** 視窗中指派必要的安裝參數。|  
|安裝更新|若要指定目的地電腦上安裝軟體更新的方式使用此工作順序步驟。 在執行此工作順序步驟之前，不會評估目的地電腦適用的軟體更新。 此時，會評估目的地電腦是否有類似於任何其他 Configuration Manager 管理用戶端的軟體更新。<br /><br /> 此步驟中使用唯讀 **_SMSTSMediaType** 工作順序變數。 如果相關聯的值不等於 **FullMedia** 會執行此工作順序步驟。|  
|擷取參照電腦- **(新的工作序列群組)**|建立另一個工作序列群組。 這個群組包含必要的步驟來準備和擷取參照電腦。|  
|加入群組|您可以使用此工作順序步驟來指定已加入工作群組的目的地電腦所需的資訊。|  
|準備 ConfigMgr 用戶端以進行擷取|使用此步驟準備擷取參照電腦的 Configuration Manager 用戶端，作為映像處理程序的一部分。|  
|準備作業系統|您可以使用此工作順序步驟來指定擷取從參照電腦的 Windows 設定時所要使用的 Sysprep 選項。 此工作順序步驟執行 Sysprep，然後讓電腦重新開機至指定的工作順序的 Windows PE 開機映像。|  
|擷取作業系統映像|使用此工作順序步驟來輸入特定的現有網路共用和。儲存映像時要使用 WIM 檔案。 使用 [新增作業系統映像套件精靈] ，新增作業系統映像套件時，這個位置用作為套件來源位置。|  

 在您從參照電腦擷取映像後，由於在初始化設定期間會建立登錄項目，因此請勿從參照電腦擷取其他作業系統映像。 您每一次擷取作業系統映像，都會建立新的參照電腦。 如果您打算使用相同的參照電腦來建立未來的作業系統映像，請先解除安裝 Configuration Manager 用戶端，然後再重新安裝 Configuration Manager 用戶端。  

## <a name="next-steps"></a>後續步驟  
[部署企業作業系統的方法](methods-to-deploy-enterprise-operating-systems.md)
