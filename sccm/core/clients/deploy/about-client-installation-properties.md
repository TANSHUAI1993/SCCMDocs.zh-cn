---
title: "用戶端安裝內容 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的用戶端安裝內容。"
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: "15"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 36bcbbca4fdee3e95d293c436a105a41a6e3953e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>關於 System Center Configuration Manager 中的用戶端安裝內容

適用於：System Center Configuration Manager (最新分支)

您可以使用 System Center Configuration Manager CCMSetup.exe 命令，手動安裝 Configuration Manager 用戶端。  

##  <a name="aboutCCMSetup"></a> 關於 CCMSetup.exe  
 CCMSetup.exe 命令會下載所需的檔案，以從管理點或來源位置安裝用戶端。 這些檔案可能包含下列項目：  

-   安裝用戶端軟體的 Windows Installer 套件 Client.msi。  

-   Microsoft 背景智慧型傳送服務 (BITS) 安裝檔案。  

-   Windows Installer 安裝檔案。  

-   Configuration Manager 用戶端的更新和修正程式。  

> [!NOTE]  
>  在 Configuration Manager 中不能直接執行 Client.msi 檔案。  

 CCMSetup.exe 提供了可自訂安裝的[命令列內容](#ccmsetup-exe-command-line-properties)。 您也可以在 CCMSetup.exe 命令列上指定可修改 Client.msi 行為的內容。  

> [!IMPORTANT]  
>  請先指定 CCMSetup 的內容，再指定 Client.msi 的內容。  

 CCMSetup.exe 及其支援的檔案位於 Configuration Manager 站台伺服器之 Configuration Manager 安裝資料夾的 [Client] 資料夾中。 這個資料夾會以 **&lt;站台伺服器名稱\>\SMS_&lt;站台碼\>\Client** 路徑，與網路共用。  

 在命令列提示字元，CCMSetup.exe 命令會使用下列格式：  

 `CCMSetup.exe [<Ccmsetup properties>] [<client.msi setup properties>]`  

 範例：  

 'CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 此範例會執行下列動作：  

-   指定名為 SMSMP01 的管理點要求發佈點清單，以下載用戶端安裝檔案。  

-   指定如果電腦上已存在用戶端版本，則應停止安裝程序。  

-   指示 client.msi 將用戶端指派為網站碼 S01。  

-   指示 client.msi 使用名為 SMSFP01 的後援狀態點。  

> [!NOTE]  
>  如果內容包含空白字元，請使用引號將其括住。  


> [!IMPORTANT]  
>  如果您已擴充 Configuration Manager 的 Active Directory 架構，許多用戶端安裝內容會在 Active Directory 網域服務中發佈，並自動由 Configuration Manager 用戶端讀取。 如需 Active Directory 網域服務中發佈的用戶端安裝內容清單，請參閱 [關於 System Center Configuration Manager 中發佈至 Active Directory 網域服務的用戶端安裝內容](about-client-installation-properties-published-to-active-directory-domain-services.md)。  

##  <a name="ccmsetupexe-command-line-properties"></a>CCMSetup.exe 命令列內容  

### <a name=""></a>/?  

開啟 [CCMSetup]  對話方塊，顯示 ccmsetup.exe 的命令列內容。  

範例： **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;路徑\>  

 指定檔案的下載位置。 使用本機或 UNC 路徑。 系統會利用伺服器訊息區 (SMB) 通訊協定下載檔案。  若要使用 **/source**，則進行用戶端安裝的 Windows 使用者帳戶必須具有該位置的讀取權限。

> [!NOTE]  
>  您可以在命令列中多次使用 **/source** 內容，以指定替代的下載位置。  

 範例：**ccmsetup.exe /source:"\\\computer\folder"**  

### <a name="mpltcomputer"></a>/mp:&lt;電腦\>

 指定電腦連線的來源管理點，讓電腦找到安裝檔案的最近發佈點。 如果沒有發佈點或電腦在 4 小時後仍無法從發佈點下載檔案，用戶端便會從指定的管理點下載檔案。  

> [!IMPORTANT]  
>  您可以使用這個內容來指定初始管理點，讓電腦找到下載來源 (其可為任何站台中的任何管理點)。 此內容並不會將用戶端*指派*給管理點。   

 電腦會根據用戶端連線的網站系統角色設定，透過 HTTP 或 HTTPS 連線下載檔案。 系統會使用 BITS 節流進行下載 (如果已設定的話)。 如果您將所有發佈點和管理點設為僅供 HTTPS 用戶端連線，請確認用戶端電腦具備有效的用戶端憑證。  

您可以使用 **/mp** 命令列內容指定多個管理點，如此若電腦無法連線到第一個管理點，便會嘗試連線到下一個管理點，以此類推。 當您指定多個管理點時，請使用分號分隔這些值。

一般來說，如果用戶端使用 HTTPS 連線至管理點，您必須指定 FQDN，而不是電腦名稱。 此值必須符合管理點的 PKI 憑證主體或主體別名。 雖然 Configuration Manager 支援在憑證中使用電腦名稱以透過內部網路進行連線，但基於安全性最佳作法，建議使用 FQDN。

使用電腦名稱的範例為：`ccmsetup.exe /mp:SMSMP01`  

使用 FQDN 的範例為：`ccmsetup.exe /mp:smsmp01.contoso.com`  

### <a name="retryltminutes"></a>/retry:&lt;分鐘\>

若 CCMSetup.exe 無法下載安裝檔案時，重試的間隔時間。  CCMSetup 會持續重試，直到達到 **downloadtimeout** 內容所指定的限制為止。  

範例：`ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

防止 CCMSetup 以預設的服務形式執行。 當 CCMSetup 以服務的形式執行時，會在電腦本機系統帳戶的內容中執行，而這個帳戶的權限可能不足以存取安裝所需的網路資源。 若使用 **/noservice**，CCMSetup.exe 會在您用於啟動安裝的使用者帳戶內容中執行。 此外，如果您使用指令碼與 **/service** 內容來執行 CCMSetup.exe，CCMSetup.exe 會在服務啟動後結束，而且可能無法正確回報安裝詳細資料。   

範例：`ccmsetup.exe /noservice`  

### <a name="service"></a>/service

指定 CCMSetup 應以使用本機系統帳戶的服務形式執行。  

範例：`ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

指定應解除安裝用戶端軟體。 如需詳細資訊，請參閱 [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md)。  

範例：`ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

指定若已安裝任何版本的用戶端，則應停止用戶端安裝。  

範例：`ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 指定 CCMSetup 在完成安裝的必要情況下，應強制讓用戶端電腦重新啟動。 如果未指定此內容，CCMSetup 會在需要重新啟動時結束，然後在下一次手動重新啟動時繼續進行。  

 範例：`CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;優先順序\>

 指定當透過 HTTP 連線下載用戶端安裝檔案時的下載優先順序。 可能值如下所示：  

-   FOREGROUND  

-   HIGH  

-   NORMAL  

-   LOW  

 預設值為 NORMAL。  

 範例：`ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;分鐘\>

在停止下載前，CCMSetup 會嘗試下載安裝檔案的時間長度 (以分鐘為單位)。 預設值為 [1440]  分鐘 (1 天)。  

範例：`ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

 指定此內容時，用戶端會使用包含用戶端驗證的 PKI 憑證 (如果可用)。 如果找不到有效的憑證 (或未使用此內容時)，用戶端會使用 HTTP 連線和自我簽署的憑證。

> [!NOTE]  
>  某些情況下，您不需要在安裝用戶端時指定此內容，且仍可以使用用戶端憑證。 這些情況包括使用用戶端推入和以軟體更新點為基礎的用戶端安裝來安裝用戶端。 不過，當您手動安裝用戶端並使用 **/mp** 內容來指定設定為只接受 HTTPS 用戶端連線的管理點時，就必須指定此內容。 您還必須在安裝僅能進行網際網路通訊的用戶端時，利用 CCMALWAYSINF=1 內容指定此內容 (搭配以網際網路為基礎的管理點和網站碼的內容)。 如需以網際網路為基礎之用戶端管理的詳細資訊，請參閱 [System Center Configuration Manager 中端點之間的通訊](../../plan-design/hierarchy/communications-between-endpoints.md)中的[從網際網路或未受信任之樹系的用戶端通訊考量](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

 範例：`CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 指定用戶端在使用 PKI 憑證進行 HTTPS 通訊時，不需要檢查憑證撤銷清單 (CRL)。  

 若未指定此內容，用戶端會先檢查 CRL，再建立 HTTPS 連線。  

 如需用戶端 CRL 檢查的詳細資訊，請參閱 [Plan for Security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) 中的[Plan for security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)。  

 範例：`CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;組態檔\>

指定包含用戶端安裝內容的文字檔名稱。

- 如果您未指定 **/noservice** CCMSetup 內容，這個檔案就必須位於 CCMSetup 資料夾中，即 32 位元或 64 位元作業系統的 %Windir%\\Ccmsetup 資料夾。
- 如果指定 **/noservice** 內容，此檔案必須與您執行之 CCMSetup.exe 位於相同的資料夾。  

範例：`CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

使用站台伺服器電腦上 &lt;Configuration Manager 目錄\>\\bin\\&lt;平台\> 資料夾中的 mobileclienttemplate.tcf 檔案，以提供正確的檔案格式。 此檔案也包含各區段及其使用方式的相關註解。 在 [用戶端安裝] 區段中的下列文字後方指定用戶端安裝內容： **Install=INSTALL=ALL**。  

[用戶端安裝] 區段項目的範例：`Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;檔名\>

 指定 CCMSetup.exe 不可在安裝 Configuration Manager 用戶端時安裝指定的必要條件程式。 此內容支援輸入多個值。 使用分號字元 (;) 分隔每一個值。  


 範例：`CCMSetup.exe /skipprereq:silverlight.exe` 或 `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe`  

### <a name="forceinstall"></a>/forceinstall

 指定將解除安裝所有現有的用戶端，並安裝新的用戶端。  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;功能\>

指定 CCMSetup.exe 不會在安裝用戶端時安裝指定的功能。  

範例：`CCMSetup.exe /ExcludeFeatures:ClientUI` 不會在用戶端上安裝軟體中心。  

> [!NOTE]  
>  在此版本， **ClientUI** 是 **/ExcludeFeatures** 內容唯一支援的值。  

##  <a name="ccmsetupReturnCodes"></a> CCMSetup.exe 傳回碼  
 CCMSetup.exe 命令會提供下列已完成的傳回碼。 若要進行疑難排解，請檢視用戶端電腦上的 ccmsetup.log 檔案，以取得傳回碼的內容和其他詳細資料。  

|傳回碼|意義|  
|-----------------|-------------|  
|0|成功|  
|6|錯誤|  
|7|需要重新開機|  
|8|安裝程式已在執行中|  
|9|必要條件評估失敗|  
|10|安裝程式資訊清單雜湊驗證失敗|  

##  <a name="clientMsiProps"></a> Client.msi 內容  
 下列內容可以修改 client.msi 的安裝行為。 如果您使用用戶端推入安裝方法，您也可以在 [用戶端推入安裝內容]  對話方塊的 [用戶端]  索引標籤中指定內容。  

### <a name="ccmadmins"></a>CCMADMINS  

指定一個或多個 Windows 使用者帳戶或群組，授與用戶端設定和原則的存取權限。 如果 Configuration Manager 系統管理員在用戶端電腦上沒有本機系統管理認證，就很適合使用這個內容。 指定帳戶清單 (以分號分隔)。  

範例：`CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

指定允許電腦重新啟動下列用戶端安裝 (如有必要)。  

> [!IMPORTANT]  
>  即使使用者已登入，電腦也會重新啟動，而不顯示警告。  

範例： **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 設為 1 指定用戶端一定要是以網際網路為基礎，而且永遠不會連線到內部網路。 用戶端的連線類型會顯示 [永遠為網際網路] 。  

 此內容應搭配 CCMHOSTNAME 使用，用於指定以網際網路為基礎之管理點的 FQDN。 此內容也應與 CCMSetup 內容 /UsePKICert 和網站碼搭配使用。  

 如需以網際網路為基礎之用戶端管理的詳細資訊，請參閱 [System Center Configuration Manager 中端點之間的通訊](../../plan-design/hierarchy/communications-between-endpoints.md)中的[從網際網路或未受信任之樹系的用戶端通訊考量](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

 範例：`CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 指定憑證簽發者清單，此清單內含 Configuration Manager 站台信任的受信任根憑證 (CA) 授權單位的憑證。  

 如需憑證簽發者清單，以及憑證選取程序期間，用戶端如何使用清單的詳細資訊，請參閱 [Plan for Security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) 中的 [Plan for security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)。  

 根 CA 憑證中的主體屬性會區分大小寫。 這些屬性可使用逗號 (,) 或分號 (;) 分隔。 您可以使用分隔線來指定多個根 CA 憑證。 範例：  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  參考站台伺服器電腦上 &lt;Configuration Manager 目錄\>\bin\\&lt;平台\> 資料夾中的 mobileclient.tcf 檔案，複製針對站台設定的 **CertificateIssuers=&lt;字串\>**。  

### <a name="ccmcertsel"></a>CCMCERTSEL

 指定下列情況的憑證選擇準則：當用戶端有一個以上適用於 HTTPS 通訊的憑證時 (包含用戶端驗證能力的有效憑證)。  

 您可以在 [主體名稱] 或 [主體別名] 中搜尋完全相符的項目 (使用 **Subject:**) 或搜尋部分相符的項目 (使用 **SubjectStr:**)。 範例：  

 `CCMCERTSEL="Subject:computer1.contoso.com"` 可搜尋 [主體名稱] 或 [主體別名] 中含有與電腦名稱 "computer1.contoso.com" 完全相符的憑證。  

 `CCMCERTSEL="SubjectStr:contoso.com"` 可搜尋 [主體名稱] 或 [主體別名] 中含 "contoso.com" 的憑證。  

 您也可以在 [主體名稱] 或 [主體替代名稱] 屬性中使用物件識別碼 (OID) 或辨別名稱屬性，例如：  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` 會搜尋以物件識別碼表示並命名為 Computers 的組織單位屬性。  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` 會搜尋以辨別名稱表示並命名為 Computers 的組織單位屬性。  

> [!IMPORTANT]  
>  如果您使用 [主體名稱] 方塊，則 **Subject:** 區分大小寫，而**SubjectStr:** 不區分大小寫。  
>   
>  如果您使用 [主體別名] 方塊，則 **Subject:** 和 **SubjectStr:** 皆不區分大小寫。  

 憑證選取時，您可以使用的完整屬性清單會列於 [PKI 憑證選擇準則支援的屬性值](#BKMK_attributevalues)。  

 如果有一個以上的憑證符合搜尋，而且 CCMFIRSTCERT 內容已設定為 1，則會選取有效期最長的憑證。  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 指定下列情況的替代憑證存放區名稱：當用於 HTTPS 的用戶端憑證不在電腦存放區的預設 [個人] 憑證存放區中時。  

 範例：`CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  啟用偵錯記錄。 這些值可以設定為 0 (預設關閉) 或 1 (開啟)。 如此可讓用戶端記錄用於疑難排解的低階資訊。 基於最佳作法，請避免在實際執行的網站使用此內容，因為可能會產生過多記錄，不容易在記錄檔中找到相關資訊。 CCMENABLELOGGING 也必須設為 TRUE 才會啟用偵錯記錄。  

  範例：`CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  預設為 TRUE，並會啟用記錄。 記錄檔會儲存在 Configuration Manager 用戶端安裝資料夾的 [Logs] 資料夾中。 根據預設，此資料夾為 %Windir%\CCM\Logs。  

  範例：`CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 用戶端健全狀況評估工具 (ccmeval.exe) 執行的頻率。 可以是 **1** 到 **1440** 分鐘。 預設為一天執行一次。  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 用戶端健全狀況評估工具 (ccmeval.exe) 執行的時間，介於 **0** (午夜) 和 **23** (晚上 11 點) 之間。 預設為午夜執行。  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 如果設為 1，此內容會指定用戶端應選取有效期最長的 PKI 憑證。 如果您使用的是網路存取保護設定和 IPsec 強制，可能需要此設定。  

 範例：`CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  

### <a name="ccmhostname"></a>CCMHOSTNAME

 如果是透過網際網路管理用戶端，則指定以網際網路為基礎之管理點的 FQDN。  

 請勿指定此選項搭配 SMSSITECODE=AUTO 的安裝內容。 以網際網路為基礎的用戶端，必須直接指派給以網際網路為基礎的網站。  

 範例：`CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

### <a name="ccmhttpport"></a>CCMHTTPPORT

 指定用戶端在透過 HTTP 與網站系統伺服器通訊時應使用的連接埠。 預設設定為連接埠 80。  

 範例：`CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

指定用戶端在透過 HTTPS 與網站系統伺服器通訊時應使用的連接埠。 預設設定為連接埠 443。  

範例：`CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 識別安裝 Configuration Manager 用戶端檔案的資料夾，預設為 *%Windir%*\CCM。 無論這些檔案安裝在何處，Ccmcore.dll 檔案一律會安裝在 *%Windir%\System32* 資料夾中。 此外，Ccmcore.dll 檔案一律會安裝在 64 位元作業系統的 *%Windir%*\SysWOW64 資料夾中，以支援 32 位元的應用程式，這些應用程式會使用 Configuration Manager 軟體開發人員套件 (SDK) 的 32 位元版 Configuration Manager 用戶端 API。  

 範例：`CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

指定要寫入 Configuration Manager 記錄檔的詳細資料層級。 指定從 0 到 3 的整數，其中 0 是最詳細的記錄，而 3 只記錄錯誤。 預設為 1。  

範例：`CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

當 Configuration Manager 記錄檔的大小達到 250000 位元組 (或是由 CCMLOGMAXSIZE 內容所指定的值) 時，會將記錄檔重新命名以作為備份，並建立新的記錄檔。  

此內容可指定要保留多少個舊版的記錄檔。 預設值為 1。 如果這個值設定為 0，則不會保留舊的記錄檔。  

範例：`CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

最大的記錄檔大小 (以位元組為單位)。 當記錄成長到所指定的大小時，會將其重新命名為歷程記錄檔案，並建立新的檔案。 此內容必須設定為至少 10000 個位元組。 預設值為 250000 個位元組。  

範例：`CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 如果設定為 TRUE，則會停用具用戶端電腦之系統管理認證的使用者權限，使其無法變更用戶端 [控制台] 中 **Configuration Manager** 的 Configuration Manager 指派站台。  

 範例： **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

如果設定為 TRUE，則停用擁有用戶端電腦上系統管理認證的一般使用者，其在用戶端電腦的 [控制台] 中使用 Configuration Manager 變更 Configuration Manager 用戶端快取資料夾設定的能力。  

範例：`CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 指定用戶端的 DNS 網域以尋找在 DNS 中發佈的管理點。 當找到管理點時，會通知用戶端有關階層中的其他管理點。 意思就是，使用 DNS 發佈而找到的管理點不一定要來自用戶端的網站，它可以是階層中的任何管理點。  

> [!NOTE]  
>  如果用戶端在相同網域，您不必指定此內容為已發佈的管理點。 若是這種情況，會自動使用用戶端的網域來搜尋管理點的 DNS。  

 如需發佈為 Configuration Manager 用戶端服務位置方法之 DNS 的詳細資訊，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)中的[服務位置以及用戶端如何判斷其指派的管理點](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

> [!NOTE]  
>  根據預設，Configuration Manager 並未啟用 DNS 發佈功能。  

 範例：`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

指定後援狀態點，這些狀態點會接收及處理 Configuration Manager 用戶端電腦所傳送的狀態訊息。  

如需後援狀態點的詳細資訊，請參閱[判斷您是否需要後援狀態點](/sccm/core/clients/deploy/plan#determine-if-you-need-a-fallback-status-point)。  

範例：`CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 指定在安裝用戶端之前不檢查 Microsoft Application Virtualization (App-V) 版本是否符合最低需求。  

> [!IMPORTANT]  
>  如果安裝 Configuration Manager 用戶端而未安裝 App-V，則無法部署虛擬應用程式。  

 範例：`CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

指定要回報用戶端狀態，但不修復已發現的用戶端問題。  

範例：`CCMSetup.exe NOTIFYONLY=TRUE`  

如需詳細資訊，請參閱 [How to configure client status in System Center Configuration Manager](configure-client-status.md)。  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 如果 Configuration Manager 用戶端的 Configuration Manager 受信任根金鑰有誤，而無法連絡受信任管理點以接收新的受信任根金鑰時，您必須使用此內容手動移除舊的受信任根金鑰。 在您將用戶端從某個站台階層移至另一個站台階層時，就可能會發生這種情況。 此內容適用於使用 HTTP 和 HTTPS 用戶端通訊的用戶端。  

 範例：`CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

與 [SMSSITECODE](#smssitecode)= AUTO 搭配使用時，可啟用用戶端升級的自動站台重新指派。

範例：`CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

指定用戶端電腦上用戶端快取資料夾的位置，此位置用於儲存暫存檔。 根據預設，此位置為 *%Windir \ccmcache*。  

範例：`CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

此內容可搭配 SMSCACHEFLAGS 內容使用，以控制用戶端快取資料夾的位置。  

範例：`CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` 會將用戶端快取資料夾安裝在可用的最大用戶端磁碟機上。  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

為用戶端快取資料夾指定進一步的安裝詳細資料。 您可以個別或合併使用 SMSCACHEFLAGS 內容，並使用分號分隔。 如果未指定此內容，則會根據 SMSCACHEDIR 內容安裝用戶端快取資料夾，該資料夾不會壓縮，而 SMSCACHESIZE 值則是當作資料夾的大小 (以 MB 為單位) 來使用。  

當您升級現有的用戶端時，會忽略此設定。  

內容：  

-   PERCENTDISKSPACE：以總磁碟空間的百分比指定資料夾大小。 如果您指定這個內容，則也必須以要使用的百分比值指定 SMSCACHESIZE 內容。  

-   PERCENTFREEDISKSPACE：以可用磁碟空間的百分比指定資料夾大小。 如果您指定這個內容，則也必須以要使用的百分比值指定 SMSCACHESIZE 內容。 例如，若磁碟的可用空間為 10 MB，而 SMSCACHESIZE 指定為 50，則資料夾大小會設定為 5 MB。 您不能使用這個內容搭配 PERCENTDISKSPACE 內容使用。  

-   MAXDRIVE：指定資料夾應該安裝在最大的可用磁碟上。 如果已使用 SMSCACHEDIR 內容指定路徑，則會忽略這個值。  

-   MAXDRIVESPACE：指定資料夾應安裝在最多可用空間的磁碟機上。 如果已使用 SMSCACHEDIR 內容指定路徑，則會忽略這個值。  

-   NTFSONLY：指定資料夾只可安裝在 NTFS 磁碟機上。 如果已使用 SMSCACHEDIR 內容指定路徑，則會忽略這個值。  

-   COMPRESS：指定資料夾應以壓縮格式來保存。  

-   FAILIFNOSPACE：指定如果沒有足夠的空間可安裝該資料夾，則應移除用戶端軟體。  

範例：`CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> 從 Configuration Manager 1606 版開始，新的用戶端設定可用來指定用戶端快取資料夾的大小。 加入這些用戶端設定實際上會取代使用 SMSCACHESIZE 作為 client.msi 內容來指定用戶端快取大小。 如需詳細資訊，請參閱[快取大小的用戶端設定](about-client-settings.md#client-cache-settings)。  

對於 1602 和更早版本，SMSCACHESIZE 指定用戶端快取資料夾的大小 (以 MB 為單位)，如果使用 PERCENTDISKSPACE 或 PERCENTFREEDISKSPACE 內容，則以百分比指定。 如果未設定此內容，資料夾預設的大小上限為 5120 MB。 您可以指定的最小值為 1 MB。  

> [!NOTE]  
>  如果必須下載的新套件會導致資料夾超過大小上限，而且資料夾無法清除以取得足夠的可用空間時，則套件下載會失敗，而且不會執行程式或應用程式。  

當您升級現有的用戶端，以及當用戶端下載軟體更新時，會忽略此設定。  

範例：`CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  如果您重新安裝用戶端，則無法使用 SMSCACHESIZE 或 SMSCACHEFLAGS 安裝內容將快取大小設定為比先前設定更小的值。 如果您嘗試這麼做，系統會忽略您的值，並將快取大小自動設回之前所設的大小。  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

指定 Configuration Manager 安裝程式檢查組態設定的位置和順序。 此內容是包含一個或多個字元的字串，每一個字元都定義了特定的設定來源。 單獨或合併使用字元值 R、P、M 和 U：  

-   R：檢查登錄中的組態設定。  

   如需詳細資訊，請參閱[如何使用群組原則安裝 Configuration Manager 用戶端](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision)。  

-   P：檢查命令提示字元處所提供的安裝屬性中的組態設定。  

-   M：使用 Configuration Manager 用戶端軟體升級舊版用戶端時，檢查現有設定。  

-   U：將已安裝的用戶端升級至較新的版本 (且使用指派的站台碼)。  

 根據預設，用戶端安裝會先使用 `PU` 檢查安裝內容，再檢查現有的設定。  

 範例：`CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 指定用戶端是否可以使用 Windows 網際網路名稱服務 (WINS) 尋找接受 HTTP 連線的管理點。 用戶端在 Active Directory 網域服務或 DNS 中找不到管理點時，會使用此方法。  

 此內容不會影響用戶端是否使用 WINS 進行名稱解析。  

 您可以為此內容設定兩個不同的模式：  

-   NOWINS：對此屬性而言，這是最安全的設定，可避免用戶端在 WINS 中尋找管理點。  當您使用此設定時，用戶端必須使用替代方法來找出內部網路上的管理點，例如 Active Directory 網域服務或使用 DNS 發行。  

-   WINSSECURE (預設)：在此模式中，使用 HTTP 通訊的用戶端可以使用 WINS 尋找管理點。 不過，用戶端必須擁有受信任根金鑰的複本，才能順利與管理點連線。 如需詳細資訊，請參閱 [Plan for Security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 中的 [Plan for security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)。  


 範例：`CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

指定 Configuration Manager 用戶端要使用的初始管理點。  

> [!IMPORTANT]  
>  如果管理點只接受透過 HTTPS 的用戶端連線，您必須使用 https:// 作為管理點名稱的首碼。  

範例：`CCMSetup.exe SMSMP=smsmp01.contoso.com` 

範例：`CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 指定 Configuration Manager 受信任根金鑰 (在無法從 Active Directory Domain Services 擷取受信任根金鑰的情況下)。 此內容適用於使用 HTTP 和 HTTPS 用戶端通訊的用戶端。 如需詳細資訊，請參閱 [Plan for Security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 中的 [Plan for security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)。  

 範例：`CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 用於重新安裝 Configuration Manager 受信任根金鑰。 指定包含受信任根金鑰之檔案的完整路徑和檔案名稱。 此內容適用於使用 HTTP 和 HTTPS 用戶端通訊的用戶端。 如需詳細資訊，請參閱 [Plan for Security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 中的 [Plan for security 中的 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)。  

 範例：'CCMSetup.exe SMSROOTKEYPATH=&lt;完整路徑和檔案名稱\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 指定網站伺服器上匯出自我簽署憑證的完整路徑和 .cer 檔案名稱。  

 此憑證是儲存在 [SMS]  憑證存放區中，主體名稱為 [網站伺服器]  ，易記名稱為 [網站伺服器簽署憑證] 。  

 範例：**CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;完整路徑和檔案名稱\>**  

### <a name="smssitecode"></a>SMSSITECODE

 指定要指派 Configuration Manager 用戶端的目標 Configuration Manager 站台。 這可以是三個字元的站台碼或單字 AUTO。 如果指定 AUTO，或者未指定此內容，用戶端會嘗試從 Active Directory 網域服務或從指定的管理點判斷其 Configuration Manager 站台指派。 若要啟用用戶端升級 AUTO，您也必須將 [SITEREASSIGN](#sitereassign) 設為 TRUE。    

> [!NOTE]  
>  如果您也指定了以網際網路為基礎的管理點 (CCMHOSTNAME)，就不要使用 AUTO。 在這種情況下，您必須直接將用戶端指派給它的站台。  

 範例：`CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> PKI 憑證選擇準則支援的屬性值  
 Configuration Manager 支援下列 PKI 憑證選擇準則屬性值：  

|OID 屬性|辨別名稱屬性|屬性定義|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|網域元件|  
|1.2.840.113549.1.9.1|E 或 E-mail|電子郵件地址|  
|2.5.4.3|CN|一般名稱|  
|2.5.4.4|SN|主體名稱|  
|2.5.4.5|SERIALNUMBER|序號|  
|2.5.4.6|C|國碼 (地區碼)|  
|2.5.4.7|L|位置|  
|2.5.4.8|S 或 ST|省份名稱|  
|2.5.4.9|STREET|街道地址|  
|2.5.4.10|O|組織名稱|  
|2.5.4.11|OU|組織單位|  
|2.5.4.12|T 或 Title|標題|  
|2.5.4.42|G 或 GN 或 GivenName|指定的名稱|  
|2.5.4.43|I 或 Initials|縮寫|  
|2.5.29.17|(沒有值)|主體替代名稱|  
