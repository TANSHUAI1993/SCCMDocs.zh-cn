---
title: "工作順序內建變數 | Microsoft Docs"
description: "工作順序內建變數提供工作順序執行環境的相關資訊，並且可用於整個工作順序期間。"
ms.custom: na
ms.date: 03/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02bc6bd4-ca53-4e22-8b80-d8ee5fe72567
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 32b24b3637dfafe401ea1d9f51b3769aa749f544
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-built-in-variables-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的工作順序內建變數

*適用於：System Center Configuration Manager (最新分支)*


 工作順序內建變數是由 System Center Configuration Manager 所提供。 內建變數提供工作順序執行環境的相關資訊，而其值可用於整個工作順序中。 一般而言，內建變數會在執行工作順序步驟之前進行初始化。 例如，內建變數 **_SMSTSLogPath** 是環境變數，可指定 Configuration Manager 元件在工作順序執行時用來寫入記錄檔的路徑；任何工作順序步驟都可以存取這個環境變數。 不過，在每個步驟之前會評估一些變數，例如 &#95;SMSTSCurrentActionName。 內建變數的值是通常是唯讀的。 名稱開頭為底線之內建變數的值是唯讀的。  

## <a name="task-sequence-built-in-variable-list"></a>工作順序內建變數清單  
 下列清單描述 Configuration Manager 中可用的內建變數：  

|內建變數名稱|說明|  
|-----------------------------|-----------------|  
|_OSDDetectedWinDir|從 Configuration Manager 1602 版開始，當 Windows PE 啟動時，工作順序會掃描電腦的硬碟以取得舊版作業系統安裝。 [Windows] 資料夾位置會儲存在此變數中。 您可以設定工作順序從環境中擷取這個值，並用它來指定相同的 [Windows] 資料夾位置以用於新的作業系統安裝。|  
|_OSDDetectedWinDrive|從 Configuration Manager 1602 版開始，當 Windows PE 啟動時，工作順序會掃描電腦的硬碟以取得舊版作業系統安裝。  作業系統安裝所在的硬碟位置會儲存在此變數中。 您可以設定工作順序從環境中擷取這個值，並用它來指定相同的硬碟位置以用於新的作業系統。|  
|_SMSTSAdvertID|儲存目前正在執行的工作順序部署唯一識別碼。 它會使用與 Configuration Manager 軟體發佈部署識別碼相同的格式。 如果從獨立媒體執行工作順序，這個變數為未定義。<br /><br /> 範例：<br /><br /> **ABC20001**|  
|_TSAppInstallStatus|工作順序會以「安裝應用程式」工作順序步驟期間的應用程式安裝狀態設定 _TSAppInstallStatus 變數。 工作順序會使用下列其中一個值來設定變數：<br /><br /> 1.**未定義**：在「安裝應用程式」工作順序步驟未執行時設定。<br />2.**錯誤**：在「安裝應用程式」工作順序步驟期間，因發生錯誤而使至少一個應用程式失敗時設定。<br />3.**警告**：在「安裝應用程式」工作順序步驟期間未發生錯誤時設定，但有一或多個應用程式 (或必要的相依性) 並未安裝，原因是不符合需求。<br />4.**成功**：在「安裝應用程式」工作順序步驟期間未偵測到錯誤或警告時設定。|  
|_SMSTSBootImageID|如果開機映像套件與目前正在執行的工作順序相關聯，則儲存 Configuration Manager 開機映像套件識別碼。 如果沒有相關聯的 Configuration Manager 開機映像套件，則不會設定這個變數。<br /><br /> 範例：<br /><br /> **ABC00001**|  
|_SMSTSBootUEFI|工作順序會在偵測到電腦處於 UEFI 模式時，設定 SMSTSBootUEFI 變數。|  
|_SMSTSClientGUID|儲存 Configuration Manager 用戶端 GUID 的值。 如果從獨立媒體執行工作順序，則不會設定這個變數。<br /><br /> 範例：<br /><br /> **0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c**|  
|_SMSTSCurrentActionName|指定目前正在執行之工作順序步驟的名稱。 工作順序管理員執行每個步驟之前，會設定這個變數。<br /><br /> 範例：<br /><br /> **執行命令列**|  
|_SMSTSDownloadOnDemand|如果目前的工作順序以隨選下載模式執行，則設為 **true** ，表示工作順序管理員只有在必須存取內容時，才會在本機下載內容。|  
|_SMSTSInWinPE|當目前的工作順序步驟正在 Windows PE 環境中執行時，這個變數會設為 **true** ；否則會設為 **false** 。 您可以測試這個工作順序變數，以判斷目前的作業系統環境。|  
|_SMSTSLastActionRetCode|儲存上一個執行動作所傳回的傳回碼。 這個變數可做為決定是否要執行下一個步驟的條件。<br /><br /> 範例：<br /><br /> **0**|  
|_SMSTSLastActionSucceeded|如果上一個動作成功，這個變數會設為 **true** ；如果上一個動作失敗，則設為 **false** 。 如果由於步驟已停用或相關聯的條件評估為 **false**而略過上一個動作，則不會重設這個變數，表示它仍會保留上一個動作的值。|  
|_SMSTSLaunchMode|指定工作順序啟動方法。 工作順序可以包含下列值：<br /><br /> -   **SMS** - 指定使用 Configuration Manager 用戶端來啟動工作順序。<br />-   **UFD** - 指定使用在 Windows XP/2003 中所建立的 USB 媒體來啟動工作順序。<br />-   **UFD+FORMAT** - 指定使用在 Windows Vista 或更新版本中所建立的 USB 媒體來啟動工作順序。<br />-   **CD** - 指定使用 CD 來啟動工作順序。<br />-   **DVD** - 指定使用 DVD 來啟動工作順序。<br />-   **PXE** - 指定從 PXE 啟動工作順序。<br />-   **HD** - 指定從硬碟啟動工作順序 (僅限預先設置的媒體)。|  
|_SMSTSLogPath|儲存記錄檔目錄的完整路徑。 這可用來判斷動作的記錄位置。 沒有可用的硬碟時，不會設定這個值。|  
|_SMSTSMachineName|儲存並指定電腦名稱。 儲存工作順序用來記錄所有狀態訊息之電腦的名稱。 若要變更新作業系統中的電腦名稱，請使用 **OSDComputerName** 變數。<br /><br /> 範例：<br /><br /> **ABC**|  
|_SMSTSMDataPath|指定 SMSTSLocalDataDrive 變數所定義的路徑。 如果您在工作順序啟動之前定義 SMSTSLocalDataDrive (例如透過設定集合變數)，Configuration Manager 便會在工作順序啟動之後定義 _SMSTSMDataPath 變數。|  
|_SMSTSMediaType|指定用來起始安裝的媒體類型。 媒體類型範例包括開機媒體、完整媒體、PXE 和預先設置的媒體。|  
|_SMSTSMP|儲存 Configuration Manager 管理點的 URL 或 IP 位址。|  
|_SMSTSMPPort|儲存 Configuration Manager 管理點的管理點連接埠號碼。<br /><br /> 範例：<br /><br /> **80**|  
|_SMSTSOrgName|儲存在工作順序進度使用者介面對話方塊中顯示的商標標題名稱。<br /><br /> 範例：<br /><br /> **XYZ 組織**|  
|_SMSTSOSUpgradeActionReturnCode|儲存從安裝程式傳回的結束代碼值，以表示成功或失敗。  這個變數會在工作順序步驟的「作業系統升級」工作順序步驟期間設定。 在搭配 Windows 10 安裝程式命令列選項 /Compat 時非常有用。<br /><br /> 範例：<br /><br /> /Compat 完成時，您可以依據失敗或成功結束代碼來採取後續步驟動作。 成功時，您即可啟動升級。 或者，您可以在環境中設定標記 (例如新增檔案或設定登錄機碼)，然後用它來為準備好升級的電腦或必須採取動作才能升級的電腦建立集合。|  
|_SMSTSPackageID|儲存目前正在執行的工作順序識別碼。 這個識別碼使用與 Configuration Manager 軟體套件識別碼相同的格式。<br /><br /> 範例：<br /><br /> **HJT00001**|  
|_SMSTSPackageName|儲存 Configuration Manager 系統管理員在建立工作順序時所指定之目前正在執行的工作順序名稱。<br /><br /> 範例：<br /><br /> **部署 Windows 10 工作順序**|  
|_SMSTSSetupRollback|指定作業系統安裝程式是否執行復原作業。 變數的值可為 **true** 或 **false**。|  
|_SMSTSRunFromDP|如果目前的工作順序以從發佈點執行模式執行，則設為 **true** ，表示工作順序管理員會從發佈點取得所需的套件共用。|  
|_SMSTSSiteCode|儲存 Configuration Manager 站台的站台碼。<br /><br /> 範例：<br /><br /> **ABC**|  
|_SMSTSType|指定目前正在執行的工作順序類型。 它可以包含下列值：<br /><br /> **1** - 表示一般工作順序。<br /><br /> **2** - 表示作業系統部署工作順序。|  
|_SMSTSTimezone|_SMSTSTimezone 變數以下列格式 (不含空格) 儲存時區資訊：<br /><br /> Bias, StandardBias, DaylightBias, StandardDate.wYear, wMonth, wDayOfWeek, wDay, wHour, wMinute, wSecond, wMilliseconds, DaylightDate.wYear, wMonth, wDayOfWeek, wDay, wHour, wMinute, wSecond, wMilliseconds, StandardName, DaylightName<br /><br /> 範例：<br /><br /> 若是東部時間 (美國和加拿大)，這個值會是 **300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,東部標準時間,日光節約時間**|  
|_SMSTSUseCRL|指定工作順序使用安全通訊端層 (SSL) 憑證與管理點通訊時，是否使用憑證撤銷清單。|  
|_SMSTSUserStarted|指定使用者是否啟動工作順序。 只有在從軟體中心啟動工作順序時，才會設定這個變數。 例如，如果 **_SMSTSLaunchMode** 設為 **SMS**。 這個變數可以包含下列值：<br /><br /> -   **true** - 指定由使用者從軟體中心手動啟動工作順序。<br />-   **false** - 指定由 Configuration Manager 排程器自動起始工作順序。|  
|_SMSTSUseSSL|指定工作順序是否使用 SSL 來與 Configuration Manager 管理點通訊。 如果您的網站以原生模式執行，這個值會設為 **true**。|  
|_SMSTSWTG|指定電腦是否以 Windows To Go 裝置執行。|  
|OSDPreserveDriveLetter|從 Configuration Manager 1606 版開始，已取代這個工作順序變數。 在作業系統部署期間，Windows 安裝程式預設會決定使用最佳的磁碟機代號 (通常是 C:)。 <br /><br />在舊版中，OSDPreverveDriveLetter 變數決定工作順序將作業系統映像套用至目的地電腦時，是否要使用該映像 WIM 檔中所擷取的磁碟機代號。 您可以將此變數的值設為 **False** ，如此就可使用您在 **「套用作業系統」** 工作順序步驟中為 **目的地** 設定所指定的位置。 如需詳細資訊，請參閱 [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)。|  
|OSDSetupAdditionalUpgradeOptions|從 Configuration Manager 1602 版開始，您可以使用這個變數來指定其他 Windows 安裝程式升級選項。
|SMSTSAssignmentsDownloadInterval|使用這個變數，指定用戶端在上次嘗試 (未傳回原則) 之後，再次嘗試下載原則所需等待的秒數。 用戶端預設會等待 **0** 秒後再重試。<br /><br /> 您可以從媒體或 PXE 使用啟動前置命令來設定此變數。|  
|SMSTSAssignmentsDownloadRetry|使用這個變數，指定用戶端在第一次嘗試找不到原則之後，可以再次嘗試下載原則的次數。 用戶端預設會重試 **0** 次。<br /><br /> 您可以從媒體或 PXE 使用啟動前置命令來設定此變數。|  
|SMSTSAssignUsersMode|指定工作順序如何將使用者和目的地電腦產生關聯。 請將變數設為下列其中一個值。<br /><br /> -   自動：工作順序在將作業系統部署至目的地電腦時，會建立指定使用者和目的地電腦之間的關聯性。<br />-   擱置中：工作順序會建立指定使用者和目的地電腦之間的關聯性，但是會等候系統管理使用者核准，才設定關聯性。<br />-   已停用：工作順序在部署作業系統時，不會將使用者和目的地電腦產生關聯。|  
|SMSTSDownloadAbortCode|這個變數包含外部程式下載程式的中止程式碼值 (指定於 SMSTSDownloadProgram 變數)。 如果程式傳回等於 SMSTSDownloadAbortCode 變數值的錯誤碼，則內容下載會失敗，並且不再嘗試其他下載方法。
|SMSTSDownloadProgram|使用此變數指定工作順序的替代內容提供者，這是取代預設 Configuration Manager 下載程式用來下載內容的下載程式。 工作順序會檢查指定下載程式的變數，這是內容下載程序的一部分。 在指定之後，工作順序會執行程式以執行下載。|  
|SMSTSDownloadRetryCount|使用此變數指定 Configuration Manager 嘗試從發佈點下載內容的次數。 用戶端預設會重試 **2** 次。|  
|SMSTSDownloadRetryDelay|使用此變數指定 Configuration Manager 在重新嘗試從發佈點下載內容之前等待的秒數。 用戶端預設會等待 **15** 秒後再重試。|  
|SMSTSDriverReceiveTimeOut|使用此變數指定與伺服器的連線逾時之前的秒數。|
|SMSTSDriverRequestConnectTimeOut|使用此變數指定在「自動套用驅動程式」工作順序步驟期間，要求驅動程式目錄時等待 HTTP 伺服器連線的秒數。 如果連線時間超過逾時設定，便會取消要求。 根據預設，逾時設定為 60 秒。|  
|SMSTSDriverRequestReceiveTimeOut|使用此變數指定在「自動套用驅動程式」工作順序步驟期間，等待驅動程式目錄要求回應的秒數。 如果連線時間超過逾時設定，便會取消要求。 根據預設，逾時設定為 480 秒。|
|SMSTSDriverRequestResolveTimeOut|使用此變數指定在「自動套用驅動程式」工作順序步驟期間，等待驅動程式目錄要求 HTTP 名稱解析的秒數。 如果連線時間超過逾時設定，便會取消要求。 根據預設，逾時設定為 60 秒。|
|SMSTSDriverRequestSendTimeOut|使用此變數指定在「自動套用驅動程式」工作順序步驟期間，傳送驅動程式目錄要求時所要使用的秒數。 如果要求時間超過逾時設定，便會取消要求。 根據預設，逾時設定為 60 秒。|
|SMSTSErrorDialogTimeout|工作順序發生錯誤時，會顯示對話方塊，並在這個變數所指定的秒數後自動關閉。 預設會在 **900** 秒 (15 分鐘) 後自動關閉對話方塊。|  
| TSDisableProgressUI | 使用此變數以在不同的工作順序區段中隱藏或顯示工作順序進度。 | 
|TSErrorOnWarning|使用這個變數，指定工作順序引擎是否會考慮將「應用程式安裝」工作順序步驟期間所偵測到的警告視為錯誤。 當一或多個應用程式或必要的相依性由於不符合需求而未安裝時，工作順序會將 _TSAppInstallStatus 變數設為 [警告]  。 當您將 TSErrorOnWarning 變數設為 **True** 並將 _TSAppInstallStatus 變數設為 [警告] 時，這個警告會視為錯誤。 預設行為是 **False** 值。| 
|SMSTSLanguageFolder|使用此變數變更非語言相關開機映像的顯示語言。|  
|SMSTSLocalDataDrive|指定當工作順序正在執行時，暫存檔案儲存在目的地電腦上的位置。<br /><br /> 這個變數必須在工作順序啟動之前設定，例如透過設定集合變數。 Configuration Manager 會在工作順序啟動之後定義 _SMSTSMDataPath 變數。|  
|SMSTSMP|使用此變數指定 Configuration Manager 管理點的 URL 或 IP 位址。|  
|SMSTSMPListRequestTimeout|使用這個變數，指定工作順序從位置服務擷取管理點清單失敗後，到重新嘗試安裝應用程式或軟體更新之前等待的毫秒數。 根據預設，工作順序會等待 60,000 毫秒 (60 秒) 後再重試該步驟，且最多重試三次。 此變數只適用於 [安裝應用程式] 和 [安裝軟體更新] 工作順序步驟。|  
|SMSTSMPListRequestTimeoutEnabled|如果用戶端不在內部網路上，使用此變數可啟用重複的 MPList 要求以重新整理用戶端。 <br />根據預設，此變數設定為 True。 當用戶端在網際網路上時，您可以將此變數設定為 False，以避免不必要的延遲。 此變數只適用於「安裝應用程式」和「安裝軟體更新」工作順序步驟。|  
|SMSTSPeerDownload|使用此變數可讓用戶端使用 Windows PE 對等快取。<br /><br /> 範例：<br /><br /> SMSTSPeerDownload  = **TRUE** 可啟用這項功能。|  
|SMSTSPeerRequestPort|若您未使用在 [用戶端設定] 中設定的預設連接埠 (8004)，則必須將這個 Windows PE 對等快取變數設定為初始廣播所使用的自訂網路連接埠。|  
|SMSTSPersistContent|使用此變數暫時將內容保留在工作順序快取中。|  
|SMSTSPostAction|指定在完成工作順序後執行的命令。 例如，您可以使用這個變數，指定工作順序將作業系統部署至裝置之後，可在內嵌裝置上寫入篩選器的指令碼。|  
|SMSTSPreferredAdvertID|強制在目的地電腦上執行特定目標部署。 您可以從媒體或 PXE 使用啟動前置命令來設定這個變數。 如果設定這個變數，工作順序會覆寫任何所需的部署。|  
|SMSTSPreserveContent|這個變數會標幟工作順序中的內容，以在部署後將內容保留在 Configuration Manager 用戶端快取中。 這有別於使用 SMSTSPersistContent，SMSTSPersistContent 只會在工作順序持續期間保留內容，並會使用工作順序快取，而不是 Configuration Manager 用戶端快取。<br /><br /> 範例：<br /><br /> SMSTSPreserveContent = **TRUE** 可啟用這項功能。|  
|SMSTSRebootDelay|指定在電腦重新啟動之前要等待的秒數。 如果這個變數未設為 0，工作順序管理員會在重新開機之前顯示通知對話方塊。<br /><br /> 範例：<br /><br /> **0**<br /><br /> **30**|  
|SMSTSRebootMessage|指定要求重新啟動時，顯示在 [關機] 對話方塊中的訊息。 如果未設定這個變數，則會顯示預設訊息。<br /><br /> 範例：<br /><br /> **工作順序管理員正在重新啟動這部電腦**。|  
|SMSTSRebootRequested|表示完成目前的工作順序步驟之後會要求重新啟動。 如果需要重新啟動，只要將這個變數設為 **true**即可，工作順序管理員會在這個工作順序步驟之後重新啟動電腦。 如果需要重新啟動才能完成工作順序步驟，工作順序步驟必須設定這個工作順序變數。 重新啟動電腦之後，工作順序會從下一個工作順序步驟繼續執行。|  
|SMSTSRetryRequested|完成目前的工作順序步驟之後，要求重試。 如果設定這個工作順序變數，也必須將 **SMSTSRebootRequested** 設為 **true**。 重新啟動電腦之後，工作順序管理員會重新執行相同的工作順序步驟。|  
|SMSTSSoftwareUpdateScanTimeout| 讓您能夠在[安裝軟體更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)工作順序步驟期間，控制軟體更新掃描的逾時。 例如，如果有大量的軟體更新要安裝，您可以增加預設值。 預設值為 30 分鐘。 |
|SMSTSUDAUsers|指定目的地電腦的主要使用者。 請用下列格式指定使用者。 使用逗號 (,) 分隔多個使用者。<br /><br /> 範例：<br /><br /> **domain\user1, domain\user2, domain\user3**<br /><br /> 如需為使用者與目的地電腦建立關聯的詳細資訊，請參閱[為使用者與目的地電腦建立關聯](../get-started/associate-users-with-a-destination-computer.md)。|  
|SMSTSWaitForSecondReboot|從 Configuration Manager 1602 版開始，當軟體更新安裝需要兩次重新啟動時，可使用這項選擇性的工作順序變數來協助控制用戶端行為。 在[安裝軟體更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)步驟前必須先設定此變數，以防止工作順序因為軟體更新安裝的第二次重新啟動而失敗。<br /><br /> 以秒為單位來設定 SMSTSWaitForSecondReboot 值，指定在「安裝軟體更新」步驟期間電腦重新啟動時工作順序要暫停的時間長度，以在有第二次重新啟動時提供足夠的時間。 <br />例如，如果您將 SMSTSWaitForSecondReboot 設定為 600，工作順序就會在重新啟動後先暫停 10 分鐘，然後再執行其他的工作順序步驟。 在單一「安裝軟體更新」工作順序步驟中安裝數百個軟體更新時，這非常有用。|  
