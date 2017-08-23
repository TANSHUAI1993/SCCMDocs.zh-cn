---
title: "使用 System Center Configuration Manager 建立獨立媒體 | Microsoft Docs"
description: "使用獨立媒體，在未連線至 Configuration Manager 站台或網路的電腦上部署作業系統。"
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
caps.latest.revision: "21"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 98f902429ad1b9965a0dc4cc2e1bd071ad5c0779
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立獨立媒體

*適用於︰System Center Configuration Manager (最新分支)*

Configuration Manager 中的獨立媒體包含在未連線至 Configuration Manager 站台或使用網路的電腦上部署作業系統所需的一切。 搭配使用獨立媒體與下列作業系統部署案例：  

-   [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

-   [將 Windows 升級至最新版本](upgrade-windows-to-the-latest-version.md)  

獨立媒體包含工作順序，會將安裝作業系統和所有其他必要內容的步驟自動化，包括開機映像、作業系統映像，以及裝置驅動程式。 由於部署作業系統所需的全部內容都儲存在獨立媒體中，因此獨立媒體比其他類型的媒體需要更大的磁碟空間。 當您在管理中心網站上建立獨立媒體時，用戶端會從 Active Directory 擷取其指派的站台碼。 建立於子站台上的獨立媒體會將該站台的站台碼自動指派給用戶端。  

##  <a name="BKMK_CreateStandAloneMedia"></a> 建立獨立媒體  
使用 [建立工作順序媒體精靈] 建立獨立媒體之前，請先確定符合下列條件：  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>建立部署作業系統的工作順序
作為獨立媒體的一部分，您必須指定工作順序以部署作業系統。 如需建立新工作順序的步驟，請參閱[在 System Center Configuration Manager 中建立工作順序以安裝作業系統](create-a-task-sequence-to-install-an-operating-system.md)。

獨立媒體不支援下列動作：
- 工作順序中的自動套用驅動程式步驟。 不支援自動從驅動程式類別目錄套用裝置驅動程式，但您可以選擇 [套用驅動程式封裝] 步驟，讓 Windows 安裝程式可以使用一組指定的驅動程式。
- 工作順序中的下載套件內容步驟。 管理點資訊無法在獨立媒體上使用，因此嘗試列舉內容位置的步驟將會失敗。
- 安裝軟體更新。
- 在部署作業系統之前安裝軟體。
- 非作業系統部署的工作順序。
- 為使用者與目的地電腦建立關聯，以支援使用者裝置親和性。
- 動態套件會透過 [安裝套件] 工作來進行安裝。
- 動態應用程式會透過 [安裝應用程式] 工作來進行安裝。

> [!NOTE]    
> 如果您部署作業系統的工作順序包含[安裝套件](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage)步驟，而且您在管理中心網站建立獨立媒體，就有可能會發生錯誤。 管理中心網站並未包含執行工作順序期間啟用軟體發佈代理程式所需的所有用戶端設定原則。 CreateTsMedia.log 檔案中，可能會出現下列錯誤：    
>     
> "WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"    
> 
> 若獨立媒體包含 [安裝套件] 步驟，您必須在啟用軟體發佈代理程式的主要站台建立獨立媒體，或是在工作順序中[設定 Windows 和 ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) 步驟之後、第一個**安裝套件**步驟之前新增[執行命令列](../understand/task-sequence-steps.md#BKMK_RunCommandLine)步驟。 [執行命令列]  步驟會執行 WMIC 命令，在第一個安裝套件步驟執行之前啟用軟體發佈代理程式。 您可以在 [執行命令列]  工作順序中使用下列內容：    
>    
> *WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE*


> [!IMPORTANT]    
> 當您在作業系統工作順序中使用「設定 Windows 和 ConfigMgr」工作順序步驟時，請勿為獨立媒體選取 [使用生產前的用戶端封裝 (如可使用)] 設定。 如果選取了此設定，且有可用的生產前用戶端封裝，則將會用於獨立媒體中。 不支援這麼做。 如需與此設定相關的詳細資訊，請參閱[設定 Windows 和 ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)。


### <a name="distribute-all-content-associated-with-the-task-sequence"></a>發佈與工作順序相關聯的所有內容
您必須將工作順序所需的所有內容都發佈到至少一個發佈點。 這包括開機映像、作業系統映像，以及其他相關聯的檔案。 精靈會在建立獨立媒體時從發佈點收集資訊。 您必須擁有該發佈點上內容庫的 **[讀取]** 存取權限。  如需詳細資訊，請參閱[發佈工作順序所參考的內容](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS)。

### <a name="prepare-the-removable-usb-drive"></a>準備卸除式 USB 磁碟機
*針對抽取式 USB 磁碟機：*

如果您即將使用卸除式 USB 磁碟機，USB 磁碟機必須連接至精靈執行所在的電腦，並作為卸除式裝置讓 Windows 能夠偵測到。 精靈會在建立媒體時直接寫入 USB 磁碟機。 獨立媒體使用 FAT32 檔案系統。 您無法在內容包含大小超過 4 GB 的檔案的 USB 快閃磁碟機上建立獨立媒體。

### <a name="create-an-output-folder"></a>建立輸出資料夾
*針對 CD/DVD 組：*

在您執行 [建立工作順序媒體精靈] 建立 CD 或 DVD 組的媒體之前，必須先為精靈所建立的輸出檔案建立資料夾。 針對 CD 或 DVD 組所建立的媒體會做為 .iso 檔直接寫入該資料夾中。


 利用下列程序，建立卸除式 USB 磁碟機或 CD/DVD 組的獨立媒體。  

## <a name="to-create-stand-alone-media"></a>建立獨立媒體  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序媒體]  以啟動 [建立工作順序媒體精靈]。  

4.  在 [選取媒體類型]  頁面指定下列選項，然後按 [下一步] 。  

    -   選取 [獨立媒體] 。  

    -   如果您想要允許作業系統在不需使用者輸入的情況下進行部署，便可選取 [允許自動部署作業系統] 。 當您選取此選項時，系統不會提示使用者輸入網路設定資訊或選用的工作順序。 不過，如果媒體已設定為使用密碼保護，仍會提示使用者輸入密碼。  

5.  在 [媒體類型]  頁面上，指定媒體是快閃磁碟機還是 CD/DVD 組，然後按一下以設定下列項目：  

    > [!IMPORTANT]  
    >  獨立媒體使用 FAT32 檔案系統。 您無法在內容包含大小超過 4 GB 的檔案的 USB 快閃磁碟機上建立獨立媒體。  

    -   如果您選取 [USB 快閃磁碟機] ，請指定要在其中儲存內容的磁碟機。  

    -   如果您選取 [CD/DVD 組] ，請指定媒體容量及輸出檔案的名稱和路徑。 精靈會將輸出檔案寫入此位置。 例如︰**\\\servername\folder\outputfile.iso**  

         如果媒體容量太小，無法儲存整個內容，則會建立多個檔案，而且您必須將內容儲存到多個 CD 或 DVD 上。 需要多個媒體時，Configuration Manager 會在其建立的每個輸出檔案名稱上新增序號。 此外，如果您同時部署應用程式與作業系統，且應用程式無法完全安裝在單一媒體上，Configuration Manager 會將應用程式儲存在多個媒體上。 獨立媒體執行時，Configuration Manager 會提示使用者儲存應用程式的下一個媒體。   

         > [!IMPORTANT]  
         >  如果您選取現有的 .iso 映像，[工作順序媒體精靈] 會在您繼續進行精靈的下一頁時從磁碟機或共用刪除映像。 即使您取消精靈，還是會刪除現有映像。  

     按一下 [下一步] 。  

6.  在 [安全性] 頁面上，從下列設定中選擇，然後按 [下一步]：
    - **使用密碼保護媒體**︰輸入一個強式密碼以協助保護媒體。 如果您指定密碼，則需要密碼才能使用媒體。  

        > [!IMPORTANT]  
        >  在獨立媒體上，只有工作順序步驟與其變數會進行加密。 剩餘的媒體內容則不會加密，因此切勿在工作順序指令碼中包括任何敏感資訊。 使用工作順序變數儲存與實作所有敏感資訊。  

    - **為獨立媒體選取有效的時間範圍** (從版本 1702 開始)︰在媒體上設定選擇性的開始和到期日期。 預設會停用這些設定。 在獨立媒體執行之前，會將這些日期與電腦上的系統時間進行比較。 系統時間早於開始時間或晚於到期時間時，不會啟動獨立媒體。 使用 New-CMStandaloneMedia PowerShell Cmdlet，也可以使用這些選項。
7.  在 [獨立 CD/DVD]  頁面上，指定部署作業系統的工作順序，然後按 [下一步] 。 選擇 [偵測相關聯的應用程式相依性，並將其新增至此媒體] 以針對應用程式相依性將內容加入至獨立媒體。
    > [!TIP]
    > 如果看不到預期的應用程式相依性，請取消選取 [偵測相關聯的應用程式相依性，並將其新增至此媒體] 設定並重新選取，以重新整理清單。

    精靈只會讓您選取與開機映像相關聯的工作順序。  

8. 在 [選取應用程式] 頁面 (自版本 1702 起開始提供) 中，指定要包含在媒體檔案中的應用程式內容，然後按 [下一步] 。
9. 在 [選取應用程式] 頁面 (從版本 1702 起開始提供) 中，指定要包含在媒體檔案中的應用程式內容，然後按 [下一步] 。
10. 在 [選取驅動程式套件] 頁面 (從版本 1702 起開始提供) 中，指定要包含在媒體檔案中的驅動程式套件內容，然後按 [下一步] 。
11.  在 **[發佈點]** 頁面上，指定包含工作順序所需內容的發佈點，然後按一下 **[下一步]**。  

     Configuration Manager 只會顯示擁有內容的發佈點。 您必須先將所有與工作順序相關聯的內容 (開機映像、作業系統映像等) 發佈到至少一個發佈點，才能繼續。 發佈內容之後，您可以重新啟動精靈，或移除在這個頁面上已選取的任何發佈點，移至前一頁，然後再回到 **[發佈點]** 頁面，以重新整理發佈點清單。 如需發佈內容的詳細資訊，請參閱[發佈工作順序所參考的內容](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS)。 如需發佈點和內容管理的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

    > [!NOTE]  
    >  您必須擁有該發佈點上內容庫的 **[讀取]** 存取權限。  

12. 在 [自訂]  頁面指定下列資訊，然後按 [下一步] 。  

    -   指定工作順序用於部署作業系統的變數。  

    -   指定您想要在工作順序之前執行的任何啟動前置命令。 啟動前置命令是在執行工作順序以安裝作業系統前，能夠在 Windows PE 中與使用者互動的指令碼或可執行檔。 如需媒體之啟動前置命令的詳細資訊，請參閱 [System Center Configuration Manager 中工作順序媒體的啟動前置命令](../understand/prestart-commands-for-task-sequence-media.md)。  

         您也可以選取 [包含啟動前置命令的檔案]  ，加入任何啟動前置命令所需的檔案。  

        > [!TIP]  
        >  在建立工作順序媒體時，工作順序會將套件識別碼和啟動前置命令列 (包括任何工作順序變數的值) 寫入執行 Configuration Manager 主控台之電腦的 CreateTSMedia.log 記錄檔中。 您可以檢閱這個記錄檔來驗證工作順序變數的值。  

13. 完成精靈。  

 獨立媒體檔案 (.iso) 已於目的地資料夾中建立。 如果您已選取 **[獨立 CD/DVD]**，現在就可以將輸出檔案複製到一組 CD 或 DVD 上。  

##  <a name="BKMK_StandAloneMediaTSExample"></a> 獨立媒體工作順序範例  
 當您建立工作順序來使用獨立媒體將作業系統部署，請使用下表做為指南。 資料表會協助您決定您的工作順序步驟及如何組織和組織成邏輯群組的那些工作順序步驟的一般順序。 您所建立的工作順序可能會因這個範例並可以包含更多或較少的工作順序步驟和群組。  

> [!NOTE]  
>  您永遠必須使用工作序列媒體精靈 來建立獨立的媒體。  

|工作序列群組或步驟|說明|  
|---------------------------------|-----------------|  
|擷取檔案和設定 - **(新工作順序群組)**|建立工作序列群組。 工作序列群組會保持在一起的較佳的組織及錯誤控制類似的工作順序步驟。|  
|擷取 Windows 設定|您可以使用此工作順序步驟來識別擷取自之前重新安裝映像，目的地電腦上的現有作業系統的 Microsoft Windows 設定。 您可以擷取電腦名稱、 使用者和組織資訊和時區設定。|  
|擷取網路設定|您可以使用此工作順序步驟來擷取接收工作順序的電腦的網路設定。 您可以擷取該電腦和網路介面卡設定資訊的網域或工作群組成員資格。|  
|擷取使用者檔案和設定 - **(新工作順序子群組)**|建立工作序列群組內的工作序列群組。 這個子群組包含擷取使用者狀態資料從現有作業系統之前重新安裝映像的目的地電腦上所需的步驟。 類似的初始群組您加入這個子群組會保持類似工作順序步驟在一起，以進一步組織及錯誤控制。|  
|設定本機狀態的位置|您可以使用此工作順序步驟來指定使用受保護的路徑的工作順序變數的本機位置。 使用者狀態會儲存在硬碟上受保護的目錄。|  
|擷取使用者狀態|您可以使用此工作順序步驟來擷取使用者檔案和設定您想要移轉至新的作業系統。|  
|安裝作業系統- **(新工作順序群組)**|建立另一個工作序列子群組。 這個子群組包含安裝作業系統所需的步驟。|  
|重新開機到 Windows PE 或硬碟|您可以使用此工作順序步驟來指定會接收此工作順序的電腦重新啟動選項。 此步驟中會顯示訊息給使用者指出如此才能繼續安裝將會重新啟動電腦。<br /><br /> 此步驟中使用唯讀 **_SMSTSInWinPE** 工作順序變數。 如果相關聯的值等於 **false** 工作順序步驟將會繼續。|  
|套用作業系統|您可以使用此工作順序步驟來安裝到目的地電腦上的作業系統映像。 這項步驟會刪除該磁碟區上的所有檔案 (除了 Configuration Manager 特定控制項檔案之外)，然後將 WIM 檔案中包含的所有磁碟區映像套用至相對應循序磁碟區。 您也可以指定 **sysprep** 回應檔案來設定要用於安裝的磁碟分割。|  
|套用 Windows 設定|您可以使用此工作順序步驟來設定目的地電腦的 Windows 設定組態資訊。 您可以將套用的 windows 設定是使用者和組織資訊、 產品或授權金鑰資訊、 時區、 和本機系統管理員密碼。|  
|套用網路設定|您可以使用此工作順序步驟來指定目的地電腦的網路或工作群組組態資訊。 您也可以指定電腦使用 DHCP 伺服器是否可靜態指派 IP 位址資訊。|  
|套用驅動程式套件|若要讓 Windows 安裝程式可供使用驅動程式套件中所有的裝置驅動程式中使用此工作順序步驟。 在獨立的媒體上都必須包含所有必要的裝置驅動程式。|  
|安裝作業系統 - **(新工作順序群組)**|建立另一個工作序列子群組。 這個子群組包含安裝 Configuration Manager 用戶端所需的步驟。|  
|[安裝套件]|使用此工作順序步驟來安裝 Configuration Manager 用戶端軟體。 Configuration Manager 會安裝並註冊 Configuration Manager 用戶端 GUID。 您可以在 **[安裝內容]** 視窗中指派必要的安裝參數。|  
|還原使用者檔案和設定 - **(新工作順序群組)**|建立另一個工作序列子群組。 這個子群組包含還原使用者狀態所需的步驟。|  
|還原使用者狀態|您可以使用此工作順序步驟來起始使用者狀態移轉工具 (USMT) 從擷取使用者狀態動作的使用者狀態和已擷取的設定還原至目的電腦。|  
