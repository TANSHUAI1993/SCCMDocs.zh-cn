---
title: "工作順序動作變數 | Microsoft Docs"
description: "使用順序動作變數 (例如網路設定變數) 指定 Configuration Manager 工作順序中單一步驟的組態設定。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2269031-0977-4f01-a274-420e00630575
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 6049ec2369e0a97b21ce6523ba8448335385ab9a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的工作順序動作變數

*適用於：System Center Configuration Manager (最新分支)*

工作順序動作變數指定 System Center Configuration Manager 工作順序中單一步驟所使用的組態設定。 根據預設，工作順序步驟所使用的設定會先進行初始化，再執行該步驟，並且只能在執行相關聯的工作順序步驟時使用。 換句話說，工作順序變數設定會先新增至工作順序環境，再執行工作順序步驟，並在執行工作順序步驟之後從工作順序環境中移除值。  

## <a name="action-variable-example"></a>動作變數範例  
 例如，您可以使用 [執行命令列]  工作順序步驟來指定命令列動作的開始目錄。 這個步驟包含 [開始]  屬性，其預設值以 **WorkingDirectory** 變數形式儲存在工作順序環境中。 會先初始化 **WorkingDirectory** 環境變數，再執行 [執行命令列]  工作順序動作。 在 [執行命令列]  步驟期間，可以透過 [開始]  屬性存取 **WorkingDirectory** 值。 然後，在完成工作順序步驟之後，會從工作順序環境中移除 **WorkingDirectory** 變數的值。 如果序列包含另一個 [執行命令列]  工作順序步驟，則新的 **WorkingDirectory** 變數會初始化並設為該工作順序步驟的起始值。  

 如果在執行工作順序步驟時具有工作順序動作設定的預設值，則順序中的多個步驟都可以使用您設定的任何新值。 如果您使用其中一個工作順序變數建立方法來覆寫內建變數值，則新值會保留在環境中，並覆寫工作順序中其他步驟的預設值。 在上述範例中，如果將 [設定工作順序變數] 步驟新增為工作順序的第一個步驟，並將 **WorkingDirectory** 環境變數設為值 **C:\\**，則工作順序中的兩個 [執行命令列] 步驟都會使用新的起始目錄值。  

## <a name="action-variables-for-task-sequence-actions"></a>工作順序動作的動作變數  
 Configuration Manager 工作順序變數是與其相關聯的工作順序動作群組在一起。 使用下列連結來收集與特定動作相關聯之動作變數的相關資訊。 工作順序變數主導了工作順序動作的運作方式。 工作順序動作則會讀取並使用您標示為輸入變數的變數。 或者，您也可以在執行階段中使用「設定工作順序變數」動作或 TSEnvironment COM 物件來設定變數。 只有工作順序動作會將變數標示為輸出變數，以供工作順序中稍後執行的動作讀取。  

> [!NOTE]  
>  並非所有工作順序動作都會與一組工作順序變數相關聯。 例如，雖然具有與 [啟用 BitLocker] 動作相關聯的變數，但是沒有與 [停用 BitLocker] 動作相關聯的變數。  

###  <a name="BKMK_ApplyDataImage"></a> 套用資料映像工作順序動作變數  
 這個動作的變數指定 WIM 檔案的哪一個映像套用至目的地電腦，以及是否刪除目的地磁碟分割上的檔案。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[套用資料映像工作順序步驟](task-sequence-steps.md#BKMK_ApplyDataImage)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (input)|指定套用至目的地電腦之映像的索引值。|  
|OSDWipeDestinationPartition<br /><br /> (input)|指定是否刪除目的地磁碟分割上的檔案。<br /><br /> 有效值：<br /><br /> **"true"** (預設值)<br /><br /> **"false"**|  

###  <a name="BKMK_ApplyDriverPackage"></a> 套用驅動程式套件工作順序動作變數  
 這個動作的變數指定大型存放驅動程式安裝以及是否安裝未簽署驅動程式的相關資訊。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[套用驅動程式套件](task-sequence-steps.md#BKMK_ApplyDriverPackage)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (input)|指定要從驅動程式封裝安裝之大型儲存裝置驅動程式的內容識別碼。 如果未指定這個值，則不會安裝任何大型存放驅動程式。|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (input)|指定要安裝之大型存放驅動程式的 INF 檔案。<br /><br /> <br /><br /> 如果設定 OSDApplyDriverBootCriticalContentUniqueID，則需要這個工作順序變數。|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (input)|指定是否安裝大量存放裝置驅動程式，這必須是 **scsi**。<br /><br /> <br /><br /> 如果設定 OSDApplyDriverBootCriticalContentUniqueID，則需要這個工作順序變數。|  
|OSDApplyDriverBootCriticalID<br /><br /> (input)|指定要安裝之大型儲存裝置驅動程式的開機關鍵識別碼。 這個識別碼會列在裝置驅動程式之 txtsetup.oem 檔案的 "**scsi**" 區段中。<br /><br /> <br /><br /> 如果設定 OSDApplyDriverBootCriticalContentUniqueID，則需要這個工作順序變數。|  
|OSDAllowUnsignedDriver<br /><br /> (input)|指定是否設定 Windows 允許未簽署裝置驅動程式的安裝。 部署 Windows Vista 和更新版本的作業系統時，不會使用這個工作順序變數。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  

###  <a name="BKMK_ApplyNetworkSettings"></a> 套用網路設定工作順序動作變數  
 這個動作的變數指定目的地電腦的網路設定 (例如，電腦網路介面卡設定、網域設定和工作群組設定)。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[套用網路設定步驟](task-sequence-steps.md#BKMK_ApplyNetworkSettings)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (input)|這個工作順序變數是陣列變數。 陣列中的每個項目都代表電腦上單一網路介面卡的設定。 針對每個介面卡所定義之設定的存取方式，是合併具有以零為起始之網路介面卡索引的陣列變數名稱與屬性名稱。<br /><br /> <br /><br /> 如果將使用這個工作順序動作來設定多張網路介面卡，則會在變數名稱中使用其索引來定義第二張網路介面卡的屬性；例如，OSDAdapter1EnableDHCP、OSDAdapter1IPAddressList、OSDAdapter1DNSDomain、OSDAdapter1WINSServerList、OSDAdapter1EnableWINS 等。<br /><br /> <br /><br /> 例如，下列變數名稱可以用來定義這個工作順序動作將設定之第一張網路介面卡的屬性：<br /><br /> <ul><li>**OSDAdapter0EnableDHCP** - true 以啟用介面卡的動態主機設定通訊協定 (DHCP)。<br />    需要此設定。 可能的值: True 或 False。</li><li>**OSDAdapter0IPAddressList** - 介面卡的 IP 位址清單 (以逗號分隔)。 除非 **EnableDHCP** 設為 **false**，否則會忽略這個屬性。<br />    需要此設定。</li><li>**OSDAdapter0SubnetMask** - 子網路遮罩清單 (以逗號分隔)。 除非 **EnableDHCP** 設為 **false**，否則會忽略這個屬性。<br />    需要此設定。</li><li>**OSDAdapter0Gateways** - IP 閘道位址清單 (以逗號分隔)。 除非 **EnableDHCP** 設為 **false**，否則會忽略這個屬性。<br />    需要此設定。</li><li>**OSDAdapter0DNSDomain** - 介面卡的網域名稱系統 (DNS) 網域。</li><li>**OSDAdapter0DNSServerList** - 介面卡的 DNS 伺服器清單 (以逗號分隔)。<br />    需要此設定。</li><li>**OSDAdapter0EnableDNSRegistration** - **true** 以在 DNS 中登錄介面卡的 IP 位址。</li><li>**OSDAdapter0EnableFullDNSRegistration** - **true** 以在電腦的完整 DNS 名稱下於 DNS 中登錄介面卡的 IP 位址。</li><li>**OSDAdapter0EnableIPProtocolFiltering** - **true** 以在介面卡上啟用 IP 通訊協定篩選。</li><li>**OSDAdapter0IPProtocolFilterList** - 允許透過 IP 執行的通訊協定清單 (以逗號分隔)。 如果 **EnableIPProtocolFiltering** 設為 **false**，則會忽略這個屬性。</li><li>**OSDAdapter0EnableTCPFiltering** - **true** 以啟用介面卡的 TCP 連接埠篩選。</li><li>**OSDAdapter0TCPFilterPortList** - 要授與 TCP 之存取權的連接埠清單 (以逗號分隔)。 如果 **EnableTCPFiltering** 設為 **false**，則會忽略這個屬性。</li><li>**OSDAdapter0TcpipNetbiosOptions** - NetBIOS over TCP/IP 的選項。 可能值如下所示：<br /><br /> <ul><li>0 使用 DHCP 伺服器中的 NetBIOS 設定。</li><li>1 啟用 NetBIOS over TCP/IP。</li><li>2 停用 NetBIOS over TCP/IP。</li></ul></li><li>**OSDAdapter0EnableWINS** - **true** 以使用 WINS 進行名稱解析。</li><li>**OSDAdapter0WINSServerList** - WINS 伺服器 IP 位址清單 (以逗號分隔)。 除非 **EnableWINS** 設為 **true**，否則會忽略這個屬性。</li><li>**OSDAdapter0MacAddress** - 用來比對實體網路介面卡設定的媒體存取控制站 (MAC) 位址。</li><li>**OSDAdapter0Name** - 出現在 [控制台] 的 [網路連線] 程式中的網路連線名稱。 名稱的長度介於 0 到 255 個字元之間。</li><li>**OSDAdapter0Index** - 設定陣列中網路介面卡設定的索引。<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (input)|指定目的地電腦上安裝的網路介面卡數目。 設定 **OSDAdapterCount** 值時，必須設定每張介面卡的所有組態選項。 例如，如果您設定特定介面卡的 **OSDAdapterTCPIPNetbiosOptions** 值，則也必須設定該介面卡的所有值。<br /><br /> <br /><br /> 如果未指定這個值，則會忽略所有 **OSDAdapter** 值。|  
|OSDDNSDomain<br /><br /> (input)|指定目的地電腦所使用的主要 DNS 伺服器。|  
|OSDDomainName<br /><br /> (input)|指定目的地電腦所加入之 Windows 網域的名稱。 指定的值必須是有效的 Active Directory 網域服務網域名稱。|  
|OSDDomainOUName<br /><br /> (input)|指定目的地電腦所加入之組織單位 (OU) 的 RFC 1779 格式名稱。 指定時，值必須包含完整路徑。<br /><br /> 範例：<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (input)|指定是否啟用 TCP/IP 篩選。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|OSDJoinAccount<br /><br /> (input)|指定用來將目的地電腦新增至 Windows 網域的網路帳戶。|  
|OSDJoinPassword<br /><br /> (input)|指定用來將目的地電腦新增至 Windows 網域的網路密碼。|  
|OSDNetworkJoinType<br /><br /> (input)|指定目的地電腦是否加入 Windows 網域或工作群組。<br /><br /> **"0"** 表示目的地電腦加入 Windows 網域。 **"1"** 指定電腦加入工作群組。<br /><br /> 有效值：<br /><br /> **"0"**<br /><br /> **"1"**|  
|OSDDNSSuffixSearchOrder<br /><br /> (input)|指定目的地電腦的 DNS 搜尋順序。|  
|OSDWorkgroupName<br /><br /> (input)|指定目的地電腦所加入之工作群組的名稱。<br /><br /> 您必須指定這個值或 **OSDDomainName** 值。 工作群組名稱不可超過 32 個字元。<br /><br /> 範例：<br /><br /> **"Accounting"**|  

###  <a name="BKMK_ApplyOperatingSystem"></a> 套用作業系統映像工作順序動作變數  
 這個動作的變數指定您要在目的地電腦上安裝之作業系統的設定。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[套用作業系統映像](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (input)|指定與作業系統部署封裝相關聯之作業系統部署回應檔案的檔案名稱。|  
|OSDImageIndex<br /><br /> (input)|指定套用至目的地電腦之 WIM 檔案的映像索引值。|  
|OSDInstallEditionIndex<br /><br /> (input)|指定已安裝之 Windows Vista 或更新版本的作業系統版本。 如果未指定版本，Windows 安裝程式將使用參照的產品金鑰來決定要安裝的版本。<br /><br /> 如果符合下列情況，請僅使用值 0：<br /><br /> -   您將安裝 Windows Vista 之前的作業系統<br />-   您將安裝 Windows Vista 或更新版本的大量授權版本，且未指定產品金鑰。<br /><br /> 有效值：<br /><br /> **"0"** (預設值)|  
|OSDTargetSystemDrive (output)|指定包含作業系統檔案之磁碟分割的磁碟機代號。|  

###  <a name="BKMK_ApplyWindowsSettings"></a> 套用 Windows 設定工作順序動作變數  
 這個動作的變數指定目的地電腦的 Windows 設定 (例如電腦名稱、Windows 產品金鑰、已註冊的使用者和組織，以及本機系統管理員密碼)。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (input)|指定目的地電腦的名稱。<br /><br /> 範例：<br /><br /> **"%_SMSTSMachineName%"** (預設值)|  
|OSDProductKey<br /><br /> (input)|指定 Windows 產品金鑰。 指定的值必須介於 1 到 255 個字元。|  
|OSDRegisteredUserName<br /><br /> (input)|指定新作業系統中的預設註冊使用者名稱。 指定的值必須介於 1 到 255 個字元。|  
|OSDRegisteredOrgName<br /><br /> (input)|指定新作業系統中的預設註冊組織名稱。 指定的值必須介於 1 到 255 個字元。|  
|OSDTimeZone<br /><br /> (input)|指定新作業系統中的預設時區設定。|  
|OSDServerLicenseMode<br /><br /> (input)|指定使用的 Windows Server 授權模式。<br /><br /> 有效值：<br /><br /> **"PerSeat"**<br /><br /> **"PerServer"**|  
|OSDServerLicenseConnectionLimit<br /><br /> (input)|指定允許的連線次數上限。 指定的數字必須在 5 到 9999 個連線的範圍內。|  
|OSDRandomAdminPassword<br /><br /> (input)|指定新作業系統中針對系統管理員帳戶所隨機產生的密碼。 如果設為 **true**，將會停用目標電腦上的本機系統管理員帳戶。 如果設為 **false**，將會啟用目標電腦上的本機系統管理員帳戶，並會將 **OSDLocalAdminPassword** 變數的值指派給本機系統管理員帳戶密碼。<br /><br /> 有效值：<br /><br /> **"true"** (預設值)<br /><br /> **"false"**|  
|OSDLocalAdminPassword<br /><br /> (input)|指定本機系統管理員密碼。 如果啟用 [隨機產生本機系統管理員密碼並在所有支援的平台上停用帳戶]  選項，則會忽略這個值。 指定的值必須介於 1 到 255 個字元。|  

###  <a name="BKMK_AutoApplyDrivers"></a> 自動套用驅動程式工作順序動作變數  
 這個動作的變數指定目的地電腦上安裝的 Windows 驅動程式，以及是否安裝未簽署的驅動程式。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[自動套用驅動程式](task-sequence-steps.md#BKMK_AutoApplyDrivers)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (input)|驅動程式類別目錄類別唯一識別碼清單 (以逗號分隔)。 指定時，[自動套用驅動程式]  工作順序動作只會考慮安裝驅動程式時位於至少其中一個類別的驅動程式。 這個值是選擇性的，預設並不會進行設定。 列舉站台上的 **SMS_CategoryInstance** 物件清單，即可取得可用的類別識別碼。|  
|OSDAllowUnsignedDriver<br /><br /> (input)|指定是否設定 Windows 允許安裝未簽署的裝置驅動程式。 部署 Windows Vista 和更新版本的作業系統時，不會使用這個工作順序變數。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (input)|指定驅動程式類別目錄中有多個與硬體裝置相容的裝置驅動程式時的工作順序動作用途。 如果設為 **"true"**，則只會安裝最適合的裝置驅動程式。  如果為 **false**，將安裝所有相容的裝置驅動程式，而且作業系統將選擇要使用的最適合驅動程式。<br /><br /> 有效值：<br /><br /> **"true"** (預設值)<br /><br /> **"false"**|  

###  <a name="BKMK_CaptureNetworkSettings"></a> 擷取網路設定工作順序動作變數  
 這個動作的變數指定是否擷取網路介面卡設定 (TCP/IP、DNS 和 WINS) 組態資訊，以及是否在作業系統部署時移轉工作群組或網域成員資格資訊。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[擷取網路設定](task-sequence-steps.md#BKMK_CaptureNetworkSettings)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (input)|指定是否擷取網路介面卡設定 (TCP/IP、DNS 和 WINS) 組態資訊。<br /><br /> 範例：<br /><br /> **"true"** (預設值)<br /><br /> **"false"**|  
|OSDMigrateNetworkMembership<br /><br /> (input)|指定是否在作業系統部署時移轉工作群組或網域成員資格資訊。<br /><br /> 範例：<br /><br /> **"true"** (預設值)<br /><br /> **"false"**|  

###  <a name="BKMK_CaptureOperatingSystemImage"></a> 擷取作業系統映像工作順序動作變數  
 這個動作的變數指定所擷取作業系統映像的相關資訊 (例如映像儲存位置、映像建立者，以及映像描述)。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[擷取作業系統映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (input)|指定具有在網路共用上儲存所擷取映像之權限的 Windows 帳戶名稱。|  
|OSDCaptureAccountPassword<br /><br /> (input)|指定用來在網路共用上儲存所擷取映像之 Windows 帳戶的密碼。|  
|OSDCaptureDestination<br /><br /> (input)|指定儲存所擷取作業系統映像的位置。 目錄名稱長度上限為 255 個字元。|  
|OSDImageCreator<br /><br /> (input)|已建立映像之使用者的選用名稱。 這個名稱儲存在 WIM 檔案中。 使用者名稱長度上限為 255 個字元。|  
|OSDImageDescription<br /><br /> (input)|所擷取作業系統映像的選擇性使用者定義描述。 這個描述儲存在 WIM 檔案中。 描述長度上限為 255 個字元。|  
|OSDImageVersion<br /><br /> (input)|選用的使用者定義的版本號碼，可指派給所擷取的作業系統映像。 這個版本號碼儲存在 WIM 檔案中。 這個值可以是任意字母組合，且長度上限為 32 個字元。|  
|OSDTargetSystemRoot<br /><br /> (input)|指定參照電腦上已安裝作業系統之 Windows 目錄的路徑。 這個作業系統驗證為 Configuration Manager 所擷取的受支援作業系統。|  

###  <a name="BKMK_CaptureUserState"></a> 擷取使用者狀態工作順序動作變數  
 這個動作的變數指定使用者狀態移轉工具 (USMT) 所使用的資訊 (例如，儲存使用者狀態的資料夾、USMT 的命令列選項，以及用來控制使用者設定檔擷取的設定檔案)。  如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[擷取使用者狀態](task-sequence-steps.md#BKMK_CaptureUserState)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|儲存使用者狀態之資料夾的 UNC 或本機路徑名稱。 無預設值。|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (input)|指定擷取使用者狀態時所使用但未公開在 Configuration Manager 使用者介面中的使用者狀態移轉工具 (USMT) 命令列選項。 以附加至自動產生之 USMT 命令列的字串形式指定其他選項。<br /><br /> <br /><br /> 在執行工作順序之前，不會驗證使用這個工作順序變數所指定之 USMT 選項的正確性。|  
|OSDMigrateMode<br /><br /> (input)|可讓您自訂 USMT 所擷取的檔案。 如果這個變數設為 "Simple"，則只會使用標準 USMT 設定檔案。 如果這個變數設為 "Advanced"，則工作順序變數 OSDMigrateConfigFiles 會指定 USMT 所使用的設定檔案。<br /><br /> 有效值：<br /><br /> **"Simple"**<br /><br /> **"Advanced"**|  
|OSDMigrateConfigFiles<br /><br /> (input)|指定用來控制使用者設定檔擷取的組態檔案。 只有在 OSDMigrateMode 設為 "Advanced" 時，才會使用這個變數。 這個逗號分隔的清單值設為執行自訂的使用者設定檔移轉。<br /><br /> 範例：miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (input)|可允許在無法擷取部分檔案時繼續進行使用者狀態擷取。<br /><br /> 有效值：<br /><br /> **"true"** (預設值)<br /><br /> **"false"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|啟用 USMT 的詳細資訊記錄。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (input)|指定是否擷取加密檔案。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|_OSDMigrateUsmtPackageID<br /><br /> (input)|指定將包含 USMT 檔案之 Configuration Manager 套件的套件識別碼。 這是必要變數。|  

###  <a name="BKMK_CaptureWindowsSettings"></a> 擷取 Windows 設定工作順序動作變數  
 這個動作的變數指定特定 Windows 設定是否移轉至目的地電腦 (例如電腦名稱、註冊組織名稱和時區資訊)。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[擷取 Windows 設定](task-sequence-steps.md#BKMK_CaptureWindowsSettings)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (input)|指定是否移轉電腦名稱。<br /><br /> 有效值：<br /><br /> **"true"** (預設值)<br /><br /> **"false"**<br /><br /> 如果值為 "true"，則 OSDComputerName 變數會設為電腦的 NetBIOS 名稱。|  
|OSDComputerName<br /><br /> (output)|設為電腦的 NetBIOS 名稱。 只有在 OSDMigrateComputerName 變數設為 "true" 時，才會設定這個值。|  
|OSDMigrateRegistrationInfo<br /><br /> (input)|指定是否移轉電腦使用者和組織資訊。<br /><br /> 有效值：<br /><br /> **"true"** (預設值)<br /><br /> **"false"**<br /><br /> 如果值為 "true"，則 OSDRegisteredOrgName 變數會設為電腦的註冊組織名稱。|  
|OSDRegisteredOrgName<br /><br /> (output)|設為電腦的註冊組織名稱。 只有在 OSDMigrateRegistrationInfo 變數設為 "true" 時，才會設定這個值。|  
|OSDMigrateTimeZone<br /><br /> (input)|指定是否移轉電腦時區。<br /><br /> 有效值：<br /><br /> **"true"** (預設值)<br /><br /> **"false"**<br /><br /> 如果值為 "true"，則 OSDTimeZone 變數會設為電腦的時區。|  
|OSDTimeZone<br /><br /> (output)|設為電腦的時區。 只有在 OSDMigrateTimeZone 變數設為 "true" 時，才會設定這個值。|  

###  <a name="BKMK_ConnecttoNetworkFolder"></a> 連線至網路資料夾工作順序動作變數  
 這個動作的變數指定網路上資料夾的相關資訊 (例如，用來連線至網路資料夾的帳戶和密碼、資料夾的磁碟機代號，以及資料夾的路徑)。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[連線至網路資料夾](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (input)|指定用來連線至網路共用的系統管理員帳戶。|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (input)|指定要連線的目標網路磁碟機代號。 這個值是選擇性的；未指定時，網路連線不會對應至磁碟機代號。 如果指定這個值，則值必須在 D: 到 Z: 的範圍內。  此外，請不要使用 X:，因為它是 Windows PE 在 Windows PE 階段期間所使用的磁碟機代號。<br /><br /> 範例：<br /><br /> **"D:"**<br /><br /> **"E:"**|  
|SMSConnectNetworkFolderPassword<br /><br /> (input)|指定用來連線至網路共用的網路密碼。|  
|SMSConnectNetworkFolderPath<br /><br /> (input)|指定連線的網路路徑。<br /><br /> 範例：<br /><br /> **"\\\servername\sharename"**|  

###  <a name="BKMK_ConvertDisk"></a> 將磁碟轉換成動態磁碟工作順序動作變數  
 這個動作的變數指定要從基本轉換成動態磁碟的實體磁碟數目。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[將磁碟轉換成動態磁碟](task-sequence-steps.md#BKMK_ConvertDisktoDynamic)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDConvertDiskIndex<br /><br /> (input)|指定已轉換的實體磁碟編號。|  

###  <a name="BKMK_EnableBitLocker"></a> 啟用 BitLocker 工作順序動作變數  
 這個動作的變數指定用來在目的地電腦上啟用 BitLocker 的修復密碼和啟動金鑰選項。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[啟用 BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (input)|[啟用 BitLocker]  工作順序動作會使用指定的值作為修復密碼，而不是產生隨機修復密碼。 值必須是有效的數值 BitLocker 修復密碼。|  
|OSDBitLockerStartupKey<br /><br /> (input)|[啟用 BitLocker] 工作順序動作會使用信賴平台模組 (TPM) 作為啟動金鑰，而不是針對金鑰管理選項 [僅 USB 上的啟動金鑰] 產生隨機啟動金鑰。 值必須是有效的 256 位元 Base64 編碼的 BitLocker 啟動金鑰。|  

###  <a name="BKMK_FormatPartitionDisk"></a> 格式化和分割磁碟工作順序動作變數  
 這個動作的變數指定格式化和分割實體磁碟的資訊 (例如，磁碟編號以及磁碟分割設定陣列)。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[格式化和分割磁碟](task-sequence-steps.md#BKMK_FormatandPartitionDisk)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (input)|指定要分割的實體磁碟編號。|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (input)|指定分割硬碟以與特定類型的 BIOS 相容時，是否停用快取對齊最佳化。 部署 Windows XP 或 Windows Server 2003 作業系統時，這可能是必要作業。 如需詳細資訊，請參閱 Microsoft 知識庫中的 [文章 931760](http://go.microsoft.com/fwlink/?LinkId=134081) 和 [文章 931761](http://go.microsoft.com/fwlink/?LinkId=134082) 。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|OSDGPTBootDisk<br /><br /> (input)|指定是否在 GPT 硬碟上建立 EFI 磁碟分割，以作為 EFI 電腦的啟動磁碟。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|OSDPartitions<br /><br /> (input)|指定磁碟分割設定陣列；請參閱 SDK 主題來存取工作順序環境中的陣列變數。<br /><br /> 這個工作順序變數是陣列變數。 陣列中的每個項目都代表硬碟上單一磁碟分割的設定。 針對每個磁碟分割所定義的設定的存取方式，是合併具有以零為起始之磁碟分割編號的陣列變數名稱與屬性名稱。<br /><br /> 例如，下列變數名稱可以用來定義這個工作順序動作將在硬碟上建立之第一個磁碟分割的屬性：<br /><br /> - **OSDPartitions0Type** - 指定磁碟分割類型。 這是必要屬性。 有效值為 "**Primary**"、"**Extended**"、"**Logical**" 和 "**Hidden**"。<br />-   **OSDPartitions0FileSystem** - 指定要在格式化磁碟分割時使用的檔案系統類型。 這是選擇性屬性；如果未指定任何檔案系統，則不會格式化磁碟分割。 有效值為 "**FAT32**" 和 "**NTFS**"。<br />-   **OSDPartitions0Bootable** - 指定是否為可開機磁碟分割。 這是必要屬性。 如果 MBR 磁碟的這個值設為 "**TRUE**"，則會將這個 MBR 磁碟設為使用中磁碟分割。<br />-   **OSDPartitions0QuickFormat** - 指定所使用格式的類型。 這是必要屬性。 如果這個值設為 "**TRUE**"，則會執行快速格式化；否則將會執行完整格式化。<br />-   **OSDPartitions0VolumeName** - 指定格式化磁碟區時指派給磁碟區的名稱。 這是選擇性屬性。<br />-   **OSDPartitions0Size** - 指定磁碟分割大小。 單位是透過 **OSDPartitions0SizeUnits** 變數所指定。 這是選擇性屬性。 如果未指定這個屬性，則會使用所有剩餘的可用空間來建立磁碟分割。<br />-   **OSDPartitions0SizeUnits** - 指定解譯 **OSDPartitions0Size** 工作順序變數時將使用的單位。 這是選擇性屬性。 有效值為 "**MB**" (預設值)、"**GB**" 和 "**Percent**"。<br />-   **OSDPartitions0VolumeLetterVariable** - 建立磁碟分割時，磁碟分割一律會使用 Windows PE 中的下一個可用磁碟機代號。 使用這個選擇性屬性來指定另一個工作順序變數的名稱，以用來儲存新的磁碟機代號，供日後參考。<br /><br /> <br /><br /> 如果將使用這個工作順序動作定義多個磁碟分割，則可以在變數名稱中使用其索引來定義第二個磁碟分割的屬性；例如，**OSDPartitions1Type**、**OSDPartitions1FileSystem**、**OSDPartitions1Bootable**、**OSDPartitions1QuickFormat**、**OSDPartitions1VolumeName** 等。|  
|OSDPartitionStyle<br /><br /> (input)|指定分割磁碟時要使用的磁碟分割樣式。 "**MBR**" 表示主開機記錄磁碟分割樣式，而 "**GPT**" 表示 GUID 磁碟分割表格樣式。<br /><br /> 有效值：<br /><br /> **"GPT"**<br /><br /> **"MBR"**|  

###  <a name="BKMK_InstallSoftwareUpdates"></a> 安裝軟體更新工作順序動作變數  
 這個動作的變數指定安裝所有更新還是只安裝必要更新。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[安裝軟體更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱<br /><br /> (input)|說明|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (input)|指定安裝所有更新還是只安裝必要更新。<br /><br /> 有效值：<br /><br /> **"All"**<br /><br /> **"Mandatory"**|  

###  <a name="BKMK_JoinDomainWorkgroup"></a> 加入網域或工作群組工作順序動作變數  
 這個動作的變數指定將目的地電腦新增至 Windows 網域或工作群組所需的資訊。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[加入網域或工作群組](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (input)|指定目的地電腦用來加入 Windows 網域的帳戶。 加入網域時，這是必要變數。|  
|OSDJoinDomainName<br /><br /> (input)|指定目的地電腦所加入之 Windows 網域的名稱。 Windows 網域名稱的長度必須介於 1 到 255 個字元。|  
|OSDJoinDomainOUName<br /><br /> (input)|指定目的地電腦所加入之組織單位 (OU) 的 RFC 1779 格式名稱。 指定時，值必須包含完整路徑。 Windows 網域 OU 名稱的長度必須介於 0 到 32,767 個字元。 如果 **OSDJoinType** 變數設為 "1" (加入工作群組)，則不會設定這個值。<br /><br /> 範例：<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (input)|指定目的地電腦用來加入 Windows 網域的網路密碼。 如果未指定這個變數，則會嘗試空白密碼。 如果 **OSDJoinType** 變數設為 "**0**" (加入網域)，則這是必要值。|  
|OSDJoinSkipReboot<br /><br /> (input)|指定是否要在目的地電腦加入網域或工作群組之後略過重新啟動。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"**|  
|OSDJoinType<br /><br /> (input)|指定目的地電腦是否加入 Windows 網域或工作群組。 若要將目的地電腦加入 Windows 網域，請指定 "**0**"。 若要將目的地電腦加入工作群組，請指定 "**1**"。<br /><br /> 有效值：<br /><br /> **"0"**<br /><br /> **"1"**|  
|OSDJoinWorkgroupName<br /><br /> (input)|指定目的地電腦所加入之工作群組的名稱。 工作群組名稱的長度必須介於 1 到 32 個字元。<br /><br /> 範例：<br /><br /> **"Accounting"**|  

###  <a name="BKMK_PrepareWindowsCapture"></a> 準備 Windows 以進行擷取工作順序動作變數  
 這個動作的變數指定用來從目標電腦中擷取 Windows 作業系統的資訊。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[準備 ConfigMgr 用戶端以進行擷取](task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (input)|指定 sysprep 是否建置大量儲存裝置驅動程式清單。 這個設定僅適用於 Windows XP 和 Windows Server 2003。 它會將要擷取之映像所支援的所有大型存放驅動程式相關資訊填入 sysprep.inf 的 [SysprepMassStorage] 區段。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|OSDKeepActivation<br /><br /> (input)|指定 sysprep 是否重設產品啟動旗標。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|OSDTargetSystemRoot<br /><br /> (output)|指定參照電腦上已安裝作業系統之 Windows 目錄的路徑。 這個作業系統驗證為 Configuration Manager 所擷取的受支援作業系統。|  

###  <a name="BKMK_ReleaseStateStore"></a> 釋放狀態存放區工作順序動作變數  
 這個動作的變數指定用來釋放所儲存之使用者狀態的資訊。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[釋放狀態存放區](task-sequence-steps.md#BKMK_ReleaseStateStore)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|從中還原使用者狀態之位置的 UNC 或本機路徑名稱。 [擷取使用者狀態]  工作順序動作和 [還原使用者狀態]  工作順序動作都使用這個值。|  

###  <a name="BKMK_RequestState"></a> 要求狀態存放區工作順序動作變數  
 這個動作的變數指定用來要求所儲存之使用者狀態的資訊 (例如，狀態移轉點上儲存使用者資料的資料夾)。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[釋放狀態存放區](../../osd/understand/task-sequence-steps.md#BKMK_ReleaseStateStore)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (input)|指定電腦帳戶無法連線至狀態移轉點時，是否將網路存取帳戶用作後援。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|OSDStateSMPRetryCount<br /><br /> (input)|指定工作順序步驟在步驟失敗之前嘗試尋找狀態移轉點的次數。 指定的計數必須介於 0 到 600。|  
|OSDStateSMPRetryTime<br /><br /> (input)|指定工作順序步驟在重試嘗試之間的秒數。 秒數上限為 30 個字元。|  
|OSDStateStorePath<br /><br /> (output)|狀態移轉點上儲存使用者狀態之資料夾的 UNC 路徑。|  

###  <a name="BKMK_RestartComputer"></a> 重新啟動電腦工作順序動作變數  
 這個動作的變數指定用來重新啟動目的地電腦的資訊。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[重新啟動電腦](task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (input)|指定重新啟動目的地電腦之前要顯示給使用者的訊息。 如果未設定這個變數，則會顯示預設訊息文字。 指定的訊息不得超過 512 個字元。<br /><br /> 範例：<br /><br /> -   "This computer will be restarted; please save your work."|  
|SMSRebootTimeout<br /><br /> (input)|指定重新啟動電腦之前向使用者顯示之警告的秒數。 指定零秒，表示未顯示任何重新開機訊息。<br /><br /> 範例：<br /><br /> **"0"** (預設值)<br /><br /> **"5"**<br /><br /> **"10"**|  

###  <a name="BKMK_RestoreUserState"></a> 還原使用者狀態工作順序動作變數  
 這個動作的變數指定用來還原目的地電腦之使用者狀態的資訊 (例如，從中還原使用者狀態之資料夾的路徑名稱，以及是否還原本機電腦帳戶)。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[還原使用者狀態](task-sequence-steps.md#BKMK_RestoreUserState)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|從中還原使用者狀態之資料夾的 UNC 或本機路徑名稱。|  
|OSDMigrateContinueOnRestore<br /><br /> (input)|指定即使無法還原部分檔案，還是會繼續進行使用者狀態還原。<br /><br /> 有效值：<br /><br /> **"true"** (預設值)<br /><br /> **"false"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|啟用 USMT 工具的詳細資訊記錄。 這個動作需要這個值；它必須設為 "true" 或 "false"。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|OSDMigrateLocalAccounts<br /><br /> (input)|指定是否還原本機電腦帳戶。<br /><br /> 有效值：<br /><br /> **"true"**<br /><br /> **"false"** (預設值)|  
|OSDMigrateLocalAccountPassword<br /><br /> (input)|如果 **OSDMigrateLocalAccounts** 變數為 "true"，這個變數必須包含指派給所有已移轉之本機帳戶的密碼。 因為將相同的密碼指派給所有已移轉的本機帳戶，所以會將它視為 Configuration Manager 作業系統部署以外的某種方法稍後將變更的暫時密碼。|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (input)|指定還原使用者狀態時所使用的其他使用者狀態移轉工具 (USMT) 命令列選項。 以附加至自動產生之 USMT 命令列的字串形式指定其他選項。 在執行工作順序之前，不會驗證使用這個工作順序變數所指定之 USMT 選項的正確性。|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (input)|指定包含 USMT 檔案之 Configuration Manager 套件的套件識別碼。 這是必要變數。|  

###  <a name="BKMK_RunCommand"></a> 執行命令列工作順序動作變數  
 這個動作的變數指定用來從命令列執行命令的資訊 (例如，執行命令的工作目錄)。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[執行命令列](task-sequence-steps.md#BKMK_RunCommandLine)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱|說明|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (input)|根據預設，在 64 位元作業系統上執行時，會使用 WOW64 檔案系統重新導向器來尋找和執行命令列中的程式，這樣才能找到 32 位元版本的作業系統程式和 DLL。 將這個變數設為 "true" 時會停用 WOW64 檔案系統重新導向器，這樣才能找到原生 64 位元版本的作業系統程式和 DLL。 在 32 位元作業系統上執行時，這個變數沒有作用。|  
|WorkingDirectory<br /><br /> (input)|指定命令列動作的起始目錄。 指定的目錄名稱不得超過 255 個字元。<br /><br /> 範例：<br /><br /> -   **"C:\\"**<br />-   **"%SystemRoot%"**|  
|SMSTSRunCommandLineUserName<br /><br /> (input)|指定用來執行命令列的帳戶。 值是「使用者名稱」或「網域\使用者名稱」形式的字串。|  
|SMSTSRunCommandLinePassword<br /><br /> (input)|指定 SMSTSRunCommandLineUserName 變數所指定帳戶的密碼。|  

### <a name="set-dynamic-variables"></a>設定動態變數  
 當您新增設定動態變數的工作順序步驟時，會自動設定此動作的變數。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[設定動態變數](task-sequence-steps.md#BKMK_SetDynamicVariables)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱<br /><br /> (input)|說明|  
|----------------------------------------|-----------------|  
|_SMSTSMake|指定的電腦。|  
|_SMSTSModel|指定電腦的型號。|  
|_SMSTSMacAddresses|指定的電腦所使用的 MAC 位址。|  
|_SMSTSIPAddresses|指定的電腦所使用的 IP 位址。|  
|_SMSTSSerialNumber|指定電腦的序號。|  
|_SMSTSAssetTag|指定電腦的資產標記。|  
|_SMSTSUUID|指定電腦的 UUID。|  
|_SMSTSDefaultGateways|指定的電腦所使用的預設閘道。|  

###  <a name="BKMK_SetupWindows"></a> 設定 Windows 和 ConfigMgr 工作順序動作變數  
 這個動作的變數指定安裝 Configuration Manager 用戶端時所使用的用戶端安裝內容。 如需與這些變數相關聯之工作順序步驟的詳細資訊，請參閱[設定 Windows 和 ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱<br /><br /> (input)|說明|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (input)|指定安裝 Configuration Manager 用戶端時使用的用戶端安裝內容。|  

### <a name="upgrade-operating-system"></a>升級作業系統  
 這個動作的變數指定將 Configuration Manager 主控台中無法使用的其他命令列選項新增至安裝程式來進行 Windows 10 升級。 如需與這個變數相關聯之工作順序步驟的詳細資訊，請參閱[升級作業系統](task-sequence-steps.md#BKMK_UpgradeOS)。  

#### <a name="details"></a>詳細資料  

|動作變數名稱<br /><br /> (input)|說明|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (input)|指定在 Windows 10 升級期間新增至安裝程式的其他命令列選項。 未驗證命令列選項。 因此，請檢查您輸入的選項正確。<br /><br /> 如需詳細資訊，請參閱 [Windows 安裝程式命令列選項](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx)。|  
