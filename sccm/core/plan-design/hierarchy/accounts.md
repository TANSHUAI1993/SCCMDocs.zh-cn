---
title: "Configuration Manager 使用的帳戶 | Microsoft Docs"
description: "識別及管理 System Center Configuration Manager 中的 Windows 群組和帳戶。"
ms.custom: na
ms.date: 2/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a776667cc9f24bd4a468afea76e466c34ce66864
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="accounts-used-in-system-center-configuration-manager"></a>System Center Configuration Manager 中使用的帳戶

*適用對象：System Center Configuration Manager (最新分支)*

利用下列資訊可識別 System Center Configuration Manager 中使用的 Windows 群組及帳戶、其使用方式，以及任何需求。  

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a>Configuration Manager 建立及使用的 Windows 群組  
 Configuration Manager 會自動建立，而且在許多情況下，會自動維護下列 Windows 群組。  

> [!NOTE]  
>  當 Configuration Manager 在屬於網域成員的電腦上建立群組時，群組會是本機安全性群組。 如果電腦是網域控制站，群組會是網域中所有網域控制站之間共用的網域本機群組。  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess  
Configuration Manager 會使用此群組來授與軟體清查所收集之檔案的檢視權限。  

下表列出此群組的其他詳細資料：  

|詳細資料|詳細資訊|  
|------------|----------------------|  
|類型和位置|此群組為主要網站伺服器上建立的本機安全性群組。<br /><br /> 當您解除安裝網站時，此群組不會自動移除。 您必須手動刪除。|  
|成員資格|Configuration Manager 會自動管理群組成員資格。 成員資格包括系統管理使用者，會授與對指派的安全性角色中 [集合]  安全物件的 [檢視收集到的檔案]  權限。|  
|權限|根據預設，此群組具備站台伺服器上下列資料夾的 **Read** 權限： **%path%\Microsoft Configuration Manager\sinv.box\FileCol**。|  

### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  
 此群組是 Configuration Manager 在站台資料庫伺服器或資料庫複本伺服器上建立的本機安全性群組。 本項目目前尚未啟用，不過會保留供未來使用。  

### <a name="configmgr-remote-control-users"></a>ConfigMgr 遠端控制使用者  
 對於指派給每個用戶端的「允許的檢視者」清單，Configuration Manager 遠端工具會使用此群組來儲存您在清單中設定的帳戶和群組。  

 下表列出此群組的其他詳細資料：  

|詳細資料|詳細資訊|  
|------------|----------------------|  
|類型和位置|此群組是用戶端收到啟用遠端工具的原則時，在 Configuration Manager 用戶端上建立的本機安全性群組。<br /><br /> 停用用戶端的遠端工具後，此群組不會自動移除。 您必須從每部用戶端電腦中手動刪除。|  
|成員資格|根據預設，此群組中沒有成員。 當您新增使用者至 [允許的檢視者] 清單時，使用者會自動新增至此群組。<br /><br /> 您可以使用 [允許的檢視者] 清單來管理此群組的成員資格，而不要直接將使用者或群組新增到此群組。<br /><br /> 除了作為允許的檢視者之外，系統管理使用者還必須具備**集合**物件的**遠端控制**權限。 您可以使用 [遠端工具操作員] 安全性角色指派此權限。|  
|權限|根據預設，此群組沒有存取電腦上任何位置的權限。 它只能用來保存允許的檢視者清單。|  

### <a name="sms-admins"></a>SMS Admins  
 透過 Windows Management Instrumentation (WMI)，Configuration Manager 能使用此群組來授與 SMS 提供者的存取權限。 檢視及變更 Configuration Manager 主控台中的物件都需要存取 SMS 提供者。  

> [!NOTE]  
>  系統管理使用者之以角色為基礎的系統管理設定可決定他們在使用 Configuration Manager 主控台時可檢視和管理的物件。  

 下表列出此群組的其他詳細資料：  

|詳細資料|詳細資訊|  
|------------|----------------------|  
|類型和位置|此群組是每部擁有 SMS 提供者電腦上建立的本機安全性群組。<br /><br /> 當您解除安裝網站時，此群組不會自動移除。 您必須手動刪除。|  
|成員資格|Configuration Manager 會自動管理群組成員資格。 根據預設，階層中的每位系統管理使用者及網站伺服器電腦帳戶，都是網站中每部 SMS 提供者電腦的 SMS Admins 群組成員。|  
|權限|SMS Admins 的權限是在 WMI Control MMC 嵌入式管理單元中設定。 根據預設，會授與 SMS Admins 群組 Root\SMS 命名空間上的 **Enable Account** 和 **Remote Enable** 。 已驗證的使用者具有 **Execute Methods**、**Provider Write** 及 **Enable Account**。<br /><br /> 將使用遠端 Configuration Manager 主控台的系統管理使用者，需要站台伺服器電腦及 SMS 提供者電腦上的「遠端啟用 DCOM」權限。 最佳作法是將這些權限授與 SMS Admins 以簡化系統管理，而不要直接將這些權限授與使用者或群組。 如需詳細資訊，請參閱 [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) 主題中的 [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) 一節。|  

### <a name="smssitesystemtositeserverconnectionmpltsitecode"></a>SMS_SiteSystemToSiteServerConnection_MP_&lt;站台碼\>  
 站台伺服器的遠端 Configuration Manager 管理點會使用此群組來連接站台資料庫。 此群組提供網站伺服器和網站資料庫上 [收件匣] 資料夾的管理點存取。  

 下表列出此群組的其他詳細資料：  

|詳細資料|詳細資訊|  
|------------|----------------------|  
|類型和位置|此群組是每部擁有 SMS 提供者電腦上建立的本機安全性群組。<br /><br /> 當您解除安裝網站時，此群組不會自動移除。 您必須手動刪除。|  
|成員資格|Configuration Manager 會自動管理群組成員資格。 根據預設，成員資格包括擁有網站管理點之遠端電腦的電腦帳戶。|  
|權限|此群組預設會具有站台伺服器上 **%路徑%\Microsoft Configuration Manager\inboxes** 資料夾的**讀取**、**讀取與執行**及**列出資料夾內容**權限。 對於管理點寫入用戶端資料之 **inboxes** 下方的子資料夾，此群組具有額外的**寫入**權限。|  

### <a name="smssitesystemtositeserverconnectionsmsprovltsitecode"></a>SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;站台碼\>  
 站台伺服器的遠端 Configuration Manager SMS 提供者電腦會使用此群組連接站台伺服器。  

 下表列出此群組的其他詳細資料：  

|詳細資料|詳細資訊|  
|------------|----------------------|  
|類型和位置|此群組為網站伺服器上建立的本機安全性群組。<br /><br /> 當您解除安裝網站時，此群組不會自動移除。 您必須手動刪除。|  
|成員資格|Configuration Manager 會自動管理群組成員資格。 根據預設，成員資格包括從已安裝網站的 SMS 提供者的每一部遠端電腦連接至網站伺服器所使用的電腦帳戶或網域使用者帳戶。|  
|權限|此群組預設會具有站台伺服器上 **%路徑%\Microsoft Configuration Manager\inboxes** 資料夾的**讀取**、**讀取與執行**及**列出資料夾內容**權限。 對於 SMS 提供者須有權限才能存取之 **inboxes** 下方的子資料夾，此群組具有額外的**寫入**權限，或**寫入**和**修改**權限。<br /><br /> 此群組也具有站台伺服器 **%路徑%\Microsoft Configuration Manager\OSD\boot** 底下資料夾的**讀取**、**讀取與執行**、**列出資料夾內容**、**寫入**及**修改**權限，以及 **%路徑%\Microsoft Configuration Manager\OSD\Bin** 底下資料夾的**讀取**權限。|  

### <a name="smssitesystemtositeserverconnectionstatltsitecode"></a>SMS_SiteSystemToSiteServerConnection_Stat_&lt;站台碼\>  
 Configuration Manager 遠端站台系統電腦上的檔案發送管理員，會使用此群組來連接站台伺服器。  

 下表列出此群組的其他詳細資料：  

|詳細資料|詳細資訊|  
|------------|----------------------|  
|類型和位置|此群組為網站伺服器上建立的本機安全性群組。<br /><br /> 當您解除安裝網站時，此群組不會自動移除。 您必須手動刪除。|  
|成員資格|Configuration Manager 會自動管理群組成員資格。 根據預設，成員資格包括從執行檔案發送管理員的每一部遠端網站系統電腦連接至網站伺服器所使用的電腦帳戶或網域使用者帳戶。|  
|權限|此群組預設會具有站台伺服器上 **%path%\Microsoft Configuration Manager\inboxes** 資料夾及此位置底下子資料夾的**讀取**、**讀取與執行**及**列出資料夾內容**權限。 對於站台伺服器上的 **%path%\Microsoft Configuration Manager\inboxes\statmgr.box** 資料夾，此群組具有額外的**寫入**和**修改**權限。|  

### <a name="smssitetositeconnectionltsitecode"></a>SMS_SiteToSiteConnection_&lt;站台碼\>  
 Configuration Manager 會使用此群組在階層中的站台間啟用以檔案為基礎之複寫。 對於直接將檔案傳送到這個站台的每個遠端站台，這個群組具有設定為 [檔案複寫帳戶] 的帳戶。  

 下表列出此群組的其他詳細資料：  

|詳細資料|詳細資訊|  
|------------|----------------------|  
|類型和位置|此群組為網站伺服器上建立的本機安全性群組。|  
|成員資格|當您安裝新站台作為另一個站台的子站台時，Configuration Manager 會自動將新站台的電腦帳戶新增至父站台伺服器上的群組。 Configuration Manager 還會將父站台上的電腦帳戶新增至新站台伺服器上的群組。 如果您指定另一個帳戶進行檔案為基礎的傳輸，請將該帳戶新增至目的地網站伺服器上的此群組。<br /><br /> 當您解除安裝網站時，此群組不會自動移除。 您必須手動刪除。|  
|權限|根據預設，此群組可 **完全控制** **%path%\Microsoft Configuration Manager\inboxes\despoolr.box\receive** 資料夾。|  

## <a name="accounts-that-configuration-manager-uses"></a>Configuration Manager 使用的帳戶  
 您可以為 Configuration Manager 設定下列帳戶。  

### <a name="active-directory-group-discovery-account"></a>Active Directory 群組探索帳戶  
 **Active Directory 群組探索帳戶**可用來探索本機、全域和通用安全性群組、這些群組內的成員資格，以及 Active Directory Domain Services 中指定位置之發佈群組內的成員資格。 發佈群組不會探索為群組資源。  

 此帳戶可以是執行探索之網站伺服器的電腦帳戶，或是 Windows 使用者帳戶。 它必須具有指定進行探索之 Active Directory 位置的 [讀取]  存取權限。  

### <a name="active-directory-system-discovery-account"></a>Active Directory 系統探索帳戶  
 [Active Directory 系統探索帳戶]  用來探索 Active Directory 網域服務中指定位置的電腦。  

 此帳戶可以是執行探索之網站伺服器的電腦帳戶，或是 Windows 使用者帳戶。 它必須具有指定進行探索之 Active Directory 位置的 [讀取]  存取權限。  

### <a name="active-directory-user-discovery-account"></a>Active Directory 使用者探索帳戶  
 [Active Directory 使用者探索帳戶]  用來探索 Active Directory 網域服務中指定位置的使用者帳戶。  

 此帳戶可以是執行探索之網站伺服器的電腦帳戶，或是 Windows 使用者帳戶。 它必須具有指定進行探索之 Active Directory 位置的 [讀取]  存取權限。  

### <a name="active-directory-forest-account"></a>Active Directory 樹系帳戶  
 **Active Directory 樹系帳戶**可用來從 Active Directory 樹系探索網路基礎結構。 管理中心網站和主要網站也會使用它將站台資料發佈至樹系的 Active Directory Domain Services。  

> [!NOTE]  
>  次要網站一律使用次要網站伺服器電腦帳戶發佈至 Active Directory。  

> [!NOTE]  
>  Active Directory 樹系帳戶必須是通用帳戶，才能探索及發佈至不受信任的樹系。 如果您未使用網站伺服器的電腦帳戶，就只能選取通用帳戶。  

 此帳戶必須具有您要探索網路基礎結構所在之每個 Active Directory 樹系的 [讀取]  權限。  

 此帳戶必須具有您要發佈網站資料所在的每個 Active Directory 樹系中，系統管理容器及其所有子物件的 [完全控制]  權限。  

### <a name="asset-intelligence-synchronization-point-proxy-server-account"></a>Asset Intelligence 同步處理點 Proxy 伺服器帳戶  
 Asset Intelligence 同步處理點會使用 **Asset Intelligence 同步處理點 Proxy 伺服器帳戶**，經由需要驗證存取的 Proxy 伺服器或防火牆來存取網際網路。  

> [!IMPORTANT]  
>  為所需的 Proxy 伺服器或防火牆指定具備最低可能權限的帳戶。  

### <a name="certificate-registration-point-account"></a>憑證登錄點帳戶  
 **憑證登錄點帳戶**：可將憑證登錄點連線至 Configuration Manager 資料庫。 預設會使用憑證登錄點伺服器的電腦帳戶，但您可以改為設定使用者帳戶。 只要憑證登錄點位於網站伺服器的不受信任網域內，就必須指定使用者帳戶。 此帳戶僅需要網站資料庫的**讀取**權限，因為寫入操作會由狀況訊息系統處理。  

### <a name="capture-operating-system-image-account"></a>擷取作業系統映像帳戶  
 Configuration Manager 會使用**擷取作業系統映像帳戶**，存取部署作業系統時擷取之映像的儲存資料夾。 如果您將步驟 [擷取作業系統映像]  新增到工作順序，就需要此帳戶。  

 帳戶在儲存映像的網路共用上都必須擁有 [讀取]  與 [寫入]  權限。  

 如果 Windows 中帳戶的密碼變更，您必須以新密碼更新工作順序。 在用戶端接著下載用戶端原則時，Configuration Manager 用戶端會收到新的密碼。  

 如果您使用此帳戶，您可以建立一個具備最低權限的網域使用者帳戶，來存取所需的網路資源，並用在所有工作順序帳戶上。  

> [!IMPORTANT]  
>  請勿將互動式登入權限指派給此帳戶。  
>   
>  勿對此帳戶使用網路存取帳戶。  

### <a name="client-push-installation-account"></a>用戶端推入安裝帳戶  
 如果您使用用戶端推入安裝來部署用戶端，您可使用**用戶端推入安裝帳戶**來連線至電腦，並安裝 Configuration Manager 用戶端軟體。 若未指定此帳戶，則會使用網站伺服器帳戶來嘗試安裝用戶端軟體。  

 此帳戶必須是即將安裝 Configuration Manager 用戶端軟體之電腦的本機**系統管理員**群組成員。 此帳戶不需要**網域系統管理員**權限。  

 您可以指定一或多個用戶端推入安裝帳戶，Configuration Manager 會嘗試輪流使用這些用戶端，直到其中一個成功為止。  

> [!TIP]  
>  為更有效協調大型 Active Directory 部署中的帳戶更新，請以不同的名稱建立新的帳戶，然後將新的帳戶新增至 Configuration Manager 中用戶端推入安裝帳戶的清單。 應提供 Active Directory 網域服務足夠的時間複寫新帳戶，然後從 Configuration Manager 和 Active Directory 網域服務移除舊帳戶。  

> [!IMPORTANT]  
>  請勿將本機登入權限授與此帳戶。  

### <a name="enrollment-point-connection-account"></a>註冊點連線帳戶  
 **註冊點連線帳戶**：可將註冊點連線至 Configuration Manager 站台資料庫。 預設會使用註冊點的電腦帳戶，但您可以改為設定使用者帳戶。 只要註冊點位於網站伺服器的不受信任網域內，就必須指定使用者帳戶。 此帳戶需要網站資料庫的**讀取**和**寫入**權限。  

### <a name="exchange-server-connection-account"></a>Exchange Server 連線帳戶  
 [Exchange Server 連線帳戶]  會將站台伺服器連線到指定的 Exchange Server 電腦，以找出並管理連線到 Exchange Server 的行動裝置。 此帳戶需要提供給 Exchange Server 電腦必要權限的 Exchange PowerShell Cmdlet。 如需 Cmdlet 的詳細資訊，請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

### <a name="exchange-server-connector-proxy-server-account"></a>Exchange Server 連接器 Proxy 伺服器帳戶  
 Exchange Server 連接器會使用 **Exchange Server 連接器 Proxy 伺服器帳戶**，以經由需要經驗證存取的 Proxy 伺服器或防火牆來存取網際網路。  

> [!IMPORTANT]  
>  為所需的 Proxy 伺服器或防火牆指定具備最低可能權限的帳戶。  

### <a name="management-point-connection-account"></a>管理點連線帳戶  
 **管理點連線帳戶**：可用來將管理點連線到 Configuration Manager 站台資料庫，使其可以傳送和擷取用戶端的資訊。 預設會使用管理點的電腦帳戶，但您可以改為設定使用者帳戶。 只要管理點位於網站伺服器的不受信任網域內，就必須指定使用者帳戶。  

 在執行 Microsoft SQL Server 的電腦上建立低權限的本機帳戶。  

> [!IMPORTANT]  
>  請勿將互動式登入權限授與此帳戶。  

### <a name="multicast-connection-account"></a>多點傳送連線帳戶  
 針對多點傳送設定的發佈點會使用**多點傳送連線帳戶**，來讀取站台資料庫的資訊。 預設會使用發佈點的電腦帳戶，但您可以改為設定使用者帳戶。 只要網站資料庫位於不受信任的樹系中，就必須指定使用者帳戶。 例如，如果您的資料中心在網站伺服器和網站資料庫以外的樹系中擁有周邊網路，您可以使用此帳戶來讀取網站資料庫的多點傳送資訊。  

 如果建立了此帳戶，則在執行 Microsoft SQL Server 的電腦上建立低權限的本機帳戶。  

> [!IMPORTANT]  
>  請勿將互動式登入權限授與此帳戶。  

### <a name="network-access-account"></a>網路存取帳戶  
 用戶端電腦在無法使用其本機電腦帳戶來存取發佈點上的內容時，就會使用**網路存取帳戶**。 例如，這會套用至不受信任網域的工作群組用戶端和電腦。 當安裝作業系統的電腦沒有網域上的電腦帳戶時，此帳戶也會在作業系統部署期間使用。  

> [!NOTE]  
>  網路存取帳戶不能作為執行程式、安裝軟體更新或執行工作順序的安全性環境。 它只能用來存取網路上的資源。  

 請授與此帳戶用戶端存取軟體所需之內容的最低適當權限。 該帳戶在發佈點或包含套件內容的其他伺服器上，必須具有 [從網路存取這台電腦]  的權限 您可以在每個站台設定最多 10 個站台存取帳戶。  

> [!WARNING]  
>  當 Configuration Manager 嘗試使用 computername$ 帳戶下載內容卻失敗時，即使先前嘗試網路存取帳戶時失敗，還是會自動再次嘗試使用網路存取帳戶。  

 在任何提供必要的資源存取的網域中建立帳戶。 網路存取帳戶一律都必須包含網域名稱。 此帳戶不支援傳遞安全性。 如果您在多個網域中擁有發佈點，請在受信任網域中建立此帳戶。  

> [!TIP]  
>  為避免帳戶鎖定，請不要變更現有網域存取帳戶的密碼。 您可改為建立新帳戶，並且在 Configuration Manager 中設定新帳戶。 經過一段時間所有用戶端都已收到新帳戶的詳細資料後，從網路共用資料夾移除舊帳戶，並刪除該帳戶。  

> [!IMPORTANT]  
>  請勿將互動式登入權限授與此帳戶。
>   
>  不要授與此帳戶將電腦加入網域的權限。 如果您必須在工作順序期間將電腦加入網域，請使用工作順序編輯器網域加入帳戶。  

### <a name="package-access-account"></a>套件存取帳戶  
 **套件存取帳戶**可讓您設定 NTFS 權限，指定可以存取發佈點上套件資料夾的使用者和使用者群組。 根據預設，Configuration Manager 只會將存取權授與一般的**使用者**與**系統管理員**帳戶。 您可以使用其他 Windows 帳戶或群組，控制用戶端電腦的存取。 因為行動裝置一律會匿名擷取套件內容，所以這些裝置不會使用套件存取帳戶。  

 根據預設，當 Configuration Manager 在發佈點建立套件共用時，它會授與**讀取**存權限給本機**使用者**群組，和授與**完全控制**權限給本機**系統管理員**群組。 實際需要的權限則依套件而定。 如果有用戶端位於工作群組或不受信任的樹系中，這些用戶端會使用網路存取帳戶來存取套件內容。 請使用預設套件存取帳戶來確保網路存取帳戶有權限存取套件。  

 使用網域中可存取發佈點的帳戶。 如果您在建立套件後建立或變更帳戶，則必須重新發佈套件。 更新套件並不會變更套件上的 NTFS 權限。  

 您不需要將網路存取帳戶新增為套件存取帳戶，因為使用者群組的成員資格會自動新增該帳戶。 將套件存取帳戶限制為只有網路存取帳戶不會阻止用戶端存取套件。  

### <a name="reporting-services-point-account"></a>Reporting Services 點帳戶  
 SQL Server Reporting Services 使用 **Reporting Services 點帳戶**，從站台資料庫擷取 Configuration Manager 報告的資料。 您指定的 Windows 使用者帳戶和密碼皆經過加密，並且儲存在 SQL Server Reporting Services 資料庫中。  

### <a name="remote-tools-permitted-viewer-accounts"></a>遠端工具獲准檢視器帳戶  
 指定進行遠端控制的 [獲准檢視器]  是一份使用者清單，這些使用者均獲准使用用戶端上的遠端工具功能。  

### <a name="site-system-installation-account"></a>網站系統安裝帳戶  
 站台伺服器使用**站台系統安裝帳戶**來安裝、重新安裝、解除安裝和設定站台系統。 如果設定站台系統要求站台伺服器起始與此站台系統之間的連線，安裝站台系統和任何站台系統角色後，Configuration Manager 也會使用此帳戶從站台系統電腦提取資料。 每個網站系統的網站系統安裝帳戶可以不同，但您只能設定一個網站系統安裝帳戶管理該網站系統上的所有網站系統角色。  

 對於系統管理員即將安裝及設定的網站系統，此帳戶須有該系統的本機系統管理權限。 此外，在系統管理員即將安裝及設定的網站系統上，此帳戶須有安全性原則中**從網路存取這台電腦**的權限。  

> [!TIP]  
>  如果您有許多網域控制站，且將跨網域使用這些帳戶，請在設定網站系統前檢查這些帳戶是否已複寫。  
>   
>  在每個要管理的網站系統指定本機帳戶時，這種設定比使用網域帳戶更安全，因為它能夠有效降低攻擊者入侵帳戶時所造成的損失。 儘管如此，網域帳戶還是較容易管理。 請考慮安全性與系統管理效益之間的取捨。  

### <a name="smtp-server-connection-account"></a>SMTP 伺服器連線帳戶  
 當 SMTP 伺服器需要驗證存取時，站台伺服器會使用 **SMTP 伺服器連線帳戶**傳送電子郵件警示。  

> [!IMPORTANT]  
>  指定具備最低可能權限的帳戶來寄送電子郵件。  

### <a name="software-update-point-connection-account"></a>軟體更新點連線帳戶  
 站台伺服器使用**軟體更新點連線帳戶**進行下列兩種軟體更新服務：  

-   Windows Server Update Services (WSUS) Configuration Manager，會設定產品定義、分類及上游設定之類的設定值。  

-   WSUS Synchronization Manager，會要求與上游 WSUS 伺服器或 Microsoft Update 同步處理。  

網站系統安裝帳戶可以安裝軟體更新元件，但無法在軟體更新點上執行軟體更新專屬功能。 如果因為軟體更新點位於不受信任的樹系中而無法以網站伺服器電腦帳戶使用此功能，除了網站系統安裝帳戶外，還必須指定這個帳戶。  

此帳戶必須是安裝 WSUS 之電腦上的本機系統管理員。 它也必須是本機 WSUS 系統管理員群組的成員。  

### <a name="software-update-point-proxy-server-account"></a>軟體更新點 Proxy 伺服器帳戶  
 軟體更新點會使用**軟體更新點 Proxy 伺服器帳戶**，透過要求驗證存取的 Proxy 伺服器或防火牆存取網際網路。  

> [!IMPORTANT]  
>  為所需的 Proxy 伺服器或防火牆指定具備最低可能權限的帳戶。  

### <a name="source-site-account"></a>來源網站帳戶  
 移轉程序使用**來源站台帳戶**存取來源站台的 SMS 提供者。 此帳戶需要 [讀取]  權限以讀取來源網站中的網站物件，才能收集移轉作業所需的資料。  

 如果將擁有共置發佈點的 System Center Configuration Manager 發佈點或次要站台升級為 Configuration Manager 2007 發佈點，此帳戶也必須要有 [站台] 類別的**刪除**權限，才能在升級期間從 Configuration Manager 2007 站台中順利移除發佈點。  

> [!NOTE]  
>  來源站台帳戶與來源站台資料庫帳戶均識別為**移轉管理員**，其位於 Configuration Manager 主控台的 [管理] 工作區的 [帳戶] 節點中。  

### <a name="source-site-database-account"></a>來源網站資料庫帳戶  
 移轉程序使用**來源站台資料庫帳戶**存取來源站台的 SQL Server 資料庫。 若要從來源網站的 SQL Server 資料庫收集資料，來源網站資料庫帳戶必須要有來源網站 SQL Server 資料庫的**讀取**及**執行**權限。  

> [!NOTE]  
>  如果使用 System Center Configuration Manager 電腦帳戶，請確定此帳戶的下列條件皆成立：  
>   
> -   在 Configuration Manager 2007 站台所在的網域中為 **Distributed COM Users** 安全性群組的成員。  
> -   其為 [SMS Admins]  安全性群組的成員。  
> -   它具有所有 Configuration Manager 2007 物件的**讀取**權限。  

> [!NOTE]  
>  來源站台帳戶與來源站台資料庫帳戶均識別為**移轉管理員**，其位於 Configuration Manager 主控台的 [管理] 工作區的 [帳戶] 節點中。  

### <a name="task-sequence-editor-domain-joining-account"></a>工作順序編輯器網域加入帳戶  
 工作順序會中運用 [工作順序編輯器網域加入帳戶]  ，將新製作映像的電腦新增至網域中。 如果在工作順序中新增 [加入網域或工作群組]  步驟，然後選取 [加入網域] ，則必須要有此帳戶。 如果在工作順序中新增 [套用網路設定] 步驟，也可以設定此帳戶，但並非必要條件。  

 此帳戶會要求 [網域加入]  該電腦將加入的網域中。  

> [!TIP]  
>  如果需要此帳戶才能進行工作順序，您可以建立一個具備最小權限的網域使用者帳戶來存取必要的網路資源，並且在所有工作順序帳戶中使用該帳戶。  

> [!IMPORTANT]  
>  請勿將互動式登入權限指派給此帳戶。  
>   
>  勿對此帳戶使用網路存取帳戶。  

### <a name="task-sequence-editor-network-folder-connection-account"></a>工作順序編輯器網路資料夾連線帳戶  
 工作順序使用**工作順序編輯器網路資料夾連線帳戶**連線至網路上的共用資料夾。 如果在工作順序中新增 [連線至網路資料夾]  步驟，則一定要有此帳戶。  

 此帳戶須有指定之共用資料夾的存取權限。 它必須是使用者網域帳戶。  

> [!TIP]  
>  如果需要此帳戶才能進行工作順序，您可以建立一個具備最小權限的網域使用者帳戶來存取必要的網路資源，並且在所有工作順序帳戶中使用該帳戶。  

> [!IMPORTANT]  
>  請勿將互動式登入權限指派給此帳戶。  
>   
>  勿對此帳戶使用網路存取帳戶。  

### <a name="task-sequence-run-as-account"></a>工作順序執行身分帳戶  
 [工作順序執行身分帳戶]  用於在工作順序中執行命令列，以及使用本機系統帳戶以外的認證。 如果您在工作順序中新增 [執行命令列] 步驟，但不希望工作順序在受管理電腦上使用本機系統帳戶權限執行，則一定要有此帳戶。  

 設定帳戶權限，使其擁有執行工作順序指定之命令列所需的最小權限即可。 此帳戶需要互動式登入權限，而且通常需要安裝軟體及存取網路資源。  

> [!IMPORTANT]  
>  勿對此帳戶使用網路存取帳戶。  
>   
>  永不使帳戶成為網域系統管理員。  
>   
>  永不設定此帳戶的漫遊設定檔。 當工作順序執行時，它會下載帳戶的漫遊設定檔。 這會導致在本機電腦上存取該設定檔變成很容易的事。  
>   
>  限制帳戶的範圍。 例如，為每個工作順序建立不同的工作順序執行身分帳戶，一旦其中一個帳戶遭受入侵時，只有該帳戶能夠存取的用戶端電腦會出現風險。  
>   
>  如果命令列要求電腦的系統管理存取權限，請考慮在所有將執行該工作順序的電腦上建立單獨作為工作順序執行身分帳戶的本機系統管理員帳戶。 不需要此類帳戶時立即加以刪除。  
