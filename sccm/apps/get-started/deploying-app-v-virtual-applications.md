---
title: "部署 App-V 虛擬應用程式 | Microsoft Docs"
description: "查看在您建立及部署虛擬應用程式時，必須考慮什麼事項。"
ms.custom: na
ms.date: 02/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
caps.latest.revision: "11"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 0808edbb9a0433dd658d37e8d005c89a4778735c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="deploy-app-v-virtual-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 部署 App-V 虛擬應用程式

適用對象：System Center Configuration Manager (最新分支)

當您使用 Configuration Manager 來管理虛擬應用程式時，會獲得下列好處：  

-   單一管理基礎結構  

-   延展性、部署和內容發佈功能，例如集合及使用者裝置親和性  

-   進階應用程式管理功能  

-   作業系統部署、軟體和硬體清查、軟體計量，以及 Asset Intelligence，以支援虛擬應用程式  

如需如何使用 Microsoft Application Virtualization (App-V) 建立與排序應用程式的詳細資訊，請參閱 TechNet 文件庫中的 [Application Virtualization](https://technet.microsoft.com/library/cc843848.aspx)。  

建立和部署虛擬應用程式時，除了用來建立應用程式的其他 System Center Configuration Manager 需求和程序之外，還必須考慮下列項目：

-   若要將虛擬應用程式部署至電腦，您必須在您的電腦上先安裝 Configuration Manager 用戶端和 App-V 用戶端。 用戶端裝置可包含桌面和可攜式電腦以及虛擬桌面基礎結構 (VDI) 用戶端。 Configuration Manager 搭配 App-V 用戶端軟體一起運作，以傳遞、尋找並啟動虛擬應用程式套件。 Configuration Manager 用戶端可管理將虛擬應用程式套件傳遞至 App-V 用戶端的程序。 App-V 用戶端便會在用戶端上執行虛擬應用程式。  

-   若要部署虛擬應用程式，您必須先使用 App-V Application Virtualization Sequencer 建立虛擬應用程式。 此排序器會監控應用程式的安裝以及設定程序，並且記錄在虛擬環境中執行應用程式所需的資訊。 您也可以使用排序器，來設定要將哪些檔案和設定套用至所有使用者，以及使用者可以自訂哪些設定。  

-   當您排序應用程式時，您必須將套件儲存至 Configuration Manager 可以存取的位置。 然後，您可以建立含有此虛擬應用程式的應用程式部署。  

-   Configuration Manager 不支援使用 App-V 的共用唯讀快取功能。  

-   Configuration Manager 支援 App-V 5 中的共用內容存放區功能。  

-   當您建立虛擬應用程式的部署類型時，Configuration Manager 會使用應用程式資訊清單檔案的內容建立部署類型。 這是一個 XML 檔案，其中含有關於虛擬應用程式的資訊。 此外，Configuration Manager 會根據 App-V .osd 檔案的內容 (其中包含有關虛擬應用程式支援的作業系統資訊) 建立部署類型的需求。  

-   為了在 Configuration Manager 中部署虛擬應用程式，用戶端電腦必須安裝至少 App-V 4.6 SP1 或更新版本的用戶端。  

-   您必須先使用知識庫文章 [2645225](https://support.microsoft.com/kb/2645225) 中所述的 Hotfix 來更新 App-V 用戶端，才能成功部署虛擬應用程式。  

-   當您在 App-V 5.0 中使用連線群組時，您已部署的虛擬應用程式便可在用戶端電腦上共用相同的檔案系統和登錄。 不同於標準的虛擬應用程式，這些應用程式可以互相共用資料。 此外，連線群組會為其所包含的應用程式保存使用者設定。 Configuration Manager 中的 App-V 虛擬環境可用來設定用戶端電腦上的連線群組。 當已安裝應用程式或是在用戶端下次評估已安裝的應用程式時，用戶端電腦上便會建立或變更虛擬環境。 您可以設定這些應用程式的優先權，當有多個應用程式嘗試變更檔案系統或登錄值時，具有最高優先權的應用程式便會優先變更。 如需詳細資訊，請參閱[建立 App-V 虛擬環境](../../apps/deploy-use/create-app-v-virtual-environments.md)。  

##  <a name="supported-app-v-versions"></a>支援的 APP-V 版本  
 Configuration Manager 支援以下 App-V 版本︰  

-   **App-V 4.6**：若要在 Configuration Manager 中使用虛擬應用程式，用戶端電腦必須安裝 App-V 4.6 SP1、App-V 4.6 SP2 或 App-V 4.6 SP3 用戶端。  

     您也必須先使用知識庫文章 [2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) 中所述的 Hotfix 來更新 App-V 4.6 SP1 用戶端，才能成功部署虛擬應用程式。  

-   **App-V 5、App-V 5.0 SP1、App-V 5.0 SP2、App-V 5.0 SP3 和 App-V 5.1**：對於 App-V 5.0 SP2，您必須安裝 [Hotfix 套件 5](https://support.microsoft.com/en-us/kb/2963211) 或使用 App-V 5.0 SP3。  
-   **App-V 5.2**︰這內建於 Windows 10 Enterprise (年度更新版和更新版本)。

如需 Windows 10 中 App-V 的詳細資訊，請參閱下列主題：

- [App-V 的新功能](https://technet.microsoft.com/itpro/windows/manage/appv-about-appv)
- [開始使用 App-V for Windows 10](https://technet.microsoft.com/itpro/windows/manage/appv-getting-started)
- [Upgrading to App-V for Windows 10 from an existing installation](https://technet.microsoft.com/itpro/windows/manage/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation) (從現有安裝升級至 App-V for Windows 10)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>管理 App-V 虛擬應用程式的步驟  
 若要管理 App-V 虛擬應用程式，請遵循下列步驟：  

1.   **排序**：排序是指使用 App-V 排序器，將應用程式轉換為虛擬應用程式的程序。

2.   **建立**：使用 [建立部署類型精靈]，將已排序的應用程式匯入至 Configuration Manager 部署類型，以供稍後新增至應用程式。 您也可同時建立虛擬環境以允許多個虛擬應用程式共用設定。

3.   **發佈**：發佈是讓 App-V 應用程式在 Configuration Manager 發佈點上可供使用的程序。

4.   **部署**：部署是讓應用程式在用戶端電腦上可供使用的程序。 這在 App-V 完整基礎結構中稱為串流。  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Configuration Manager 虛擬應用程式傳遞方法  
Configuration Manager 支援兩個將虛擬應用程式傳遞至用戶端的方法︰串流傳遞和本機傳遞 (下載並執行)。

在決定要使用哪個傳遞方法時，您可先行比較︰串流傳遞時磁碟空間需求較低，本機傳遞時則可保證 App-V 應用程式的可用性。 進行本機傳遞時需要增加用戶端磁碟空間，這樣可能會比串流傳遞好，這樣使用者就可以隨時從任何位置使用應用程式。  

###  <a name="streaming-delivery"></a>串流傳遞
當您使用 Configuration Manager 來管理 App-V 用戶端時，其支援透過 HTTP 或 HTTPS，從發佈點進行虛擬應用程式的串流處理。 預設會啟用透過 HTTP 或 HTTPS 進行串流處理，並在用於發佈點內容的對話方塊中加以設定。 當您將虛擬應用程式部署至用戶端電腦，且有使用者執行該虛擬應用程式時，Configuration Manager 用戶端會與管理點連絡以決定應使用的發佈點。 接著，從該發佈點串流處理應用程式。  

使用下表中的資訊，協助您決定串流傳遞是否為最佳的傳遞方法：

|優點|缺點|  
|----------------|-------------------|  
|此方法使用標準的網路通訊協定，從發佈點串流套件內容。<br /><br /> 虛擬應用程式的程式捷徑會叫用發佈點的連線，如此虛擬應用程式便可隨選即用。<br /><br /> 此方法適用於具有高頻寬發佈點連線的用戶端。<br /><br /> 分散於整個企業的虛擬應用程式若有更新，用戶端可於接收到通知目前版本已被取代的原則時，僅下載舊版的變更。<br /><br /> 存取權限會在發佈點定義，以避免使用者存取未獲授權的應用程式或套件。|在使用者首次執行應用程式之後，虛擬應用程式才會進行串流動作。 在此案例中，使用者會先接收虛擬應用程式的程式捷徑，接著由網路斷線，才可首次執行該虛擬應用程式。 若使用者在用戶端離線時試圖執行該虛擬應用程式，使用者就看見錯誤訊息且無法執行該虛擬應用程式，原因是 Configuration Manager 發佈點不可用來進行應用程式的串流處理。 應用程式將無法使用，除非使用者重新連線至網路並執行應用程式。<br /><br /> 若要避免這種情形，您可以使用本機傳遞方法來傳遞虛擬應用程式給用戶端，或者您可以啟用以網際網路為基礎的用戶端管理以使用串流傳遞。|  

###  <a name="local-delivery-download-and-execute"></a>本機傳遞 (下載並執行)  
當您使用本機傳遞方法時，Configuration Manager 用戶端第一次會將整個虛擬應用程式套件下載至 Configuration Manager 用戶端快取。 Configuration Manager 接著會指示 APP-V 用戶端，將應用程式從 Configuration Manager 快取串流處理至 APP-V 快取。 如果您將虛擬應用程式部署至用戶端電腦，而其內容不在 App-V 快取中，App-V 用戶端會從 Configuration Manager 用戶端快取，將應用程式內容串流至 App-V 快取中，然後執行該應用程式。 當應用程式成功執行之後，您可以設定 Configuration Manager 用戶端於下個刪除週期刪除任何舊版套件，或將它們保存在 Configuration Manager 用戶端快取中。  

使用下表中的資訊，協助您決定本機傳遞是否為最佳的傳遞方法：   

|優點|缺點|  
|----------------|-------------------|  
|此標準發佈點功能可透過背景智慧型傳送服務 (BITS) 來下載套件。<br /><br /> 虛擬應用程式套件內容是在本機傳遞給用戶端。 這表示使用者能夠在其電腦未連線到網路時執行它們。<br /><br /> 此方法適用於速度較慢或不穩定的網路連線，以及偶爾才會連線到網路的電腦。<br /><br /> Configuration Manager 會在虛擬應用程式套件內容更新時，使用遠端差異壓縮 (RDC)，僅將檔案中已變更的位元組傳送給用戶端。 Configuration Manager 用戶端會依據目前版本的套件及任何傳送給用戶端的變更，使用 RDC 建立一個新的虛擬應用程式套件版本。<br /><br /> 此方法可為行動使用者或已中斷連線使用者提供應用程式恢復功能。 若虛擬應用程式是使用安裝動作進行部署，系統管理員就能選擇在傳遞後將套件保存在 Configuration Manager 快取中。 Configuration Manager 用戶端快取中的套件可在 App-V 用戶端將套件提取至快取時，作為一個可靠的本機串流來源。|若要將虛擬應用程式保存在 Configuration Manager 快取中，用戶端上的磁碟空間必須為虛擬應用程式套件大小的兩倍以上。|  

###  <a name="deployment-from-an-image"></a>從映像部署

您也可在電腦上預先安裝虛擬應用程式，接著建立該電腦的映像以用來部署至其他電腦。 但若虛擬應用程式套件建立在不同站台中，則不會使用二進位差異複寫來將更新下載至應用程式。 此選項對於虛擬桌面基礎結構可能很有用，尤其是在您希望應用程式立即可用時，不需等到使用者登入後才下載應用程式。    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a>將 App-V 基礎結構移轉至 Configuration Manager 和 App-V 基礎結構  
使用下列表格中的資訊來協助您規劃將現有的 App-V 基礎結構移轉至 Configuration Manager 的虛擬應用程式管理。  

|步驟|詳細資訊|  
|----------|----------------------|  
|檢查您目前的虛擬應用程式，以選擇要移轉至 Configuration Manager 基礎結構的應用程式。|沒有其他資訊。|  
|評估使用者和裝置，以用於部署虛擬應用程式。|建立 Configuration Manager 集合來將使用者和裝置分組在一起，以用於部署虛擬應用程式。 請參閱[集合簡介](/sccm/core/clients/manage/collections/introduction-to-collections)。|  
|將 App-V 5 連線群組移轉至 Configuration Manager 虛擬環境。|請參閱此主題中的[將 App-V 5 連線群組移轉至 Configuration Manager 虛擬環境](/sccm/apps/get-started/deploying-app-v-virtual-applications#migrate-app-v-5-connection-groups-to-configuration-manager-virtual-environments)一節。|  
|調查並找出在您的 Configuration Manager 基礎結構中，是否有任何虛擬應用程式以完整應用程式存在。|為了方便管理，您可將該虛擬應用程式新增為現有完整應用程式的一個新部署類型。 請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。|  
|建立可用來取代現有 App-V 套件的應用程式。|請參閱[應用程式管理簡介](/sccm/apps/understand/introduction-to-application-management)和[建立應用程式](../../apps/deploy-use/create-applications.md)。|  
|Configuration Manager 將在首次部署虛擬應用程式之後，開始在用戶端上管理虛擬應用程式。 從此之後，Configuration Manager 必須管理該電腦上的所有 App-V 應用程式。|沒有其他資訊。|  
|將內容發佈至適當的發佈點，以啟用應用程式的本機傳遞。|請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。|  
|部署應用程式到 Configuration Manager 用戶端。<br /><br /> 如果您使用不會建立資訊清單 XML 檔案的舊版排序器來建立 App-V 應用程式，則可以使用較新版的排序器來開啟並儲存該應用程式以建立檔案。 使用 Configuration Manager 部署虛擬應用程式時需要用到此檔案。<br /><br /> App-V 支援以 SoftGrid 4.1 SP1 或 4.2 版排序器建立的虛擬應用程式套件。<br /><br /> 若應用程式之前已在本機安裝，您必須先解除安裝，才能部署該應用程式的虛擬版本。|請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。|  
|System Center Configuration Manager 不再支援使用包含虛擬應用程式的套件和程式。 當您從 Configuration Manager 2007 移轉至 System Center Configuration Manager 時，Configuration Manager 會將這些套件轉換成應用程式。<br /><br /> Configuration Manager 2007 公告也將轉換成下列部署類型︰<br /><br /> - 移轉不具有公告的 App-V 套件：一個使用預設部署類型設定的部署類型。<br /><br /> - 移轉具有一個公告的 App-V 套件：使用與 <br />                Configuration Manager 2007 公告相同設定的部署類型。<br /><br /> - 移轉包含多個公告的 App-V 套件︰針對每個 <br />                Configuration Manager 2007 公告的部署類型，會使用該公告的設定。|請參閱[規劃將 Configuration Manager 物件移轉至 System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)。|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>將 App-V 5 連線群組移轉至 Configuration Manager 虛擬環境  
Configuration Manager 中的 App-V 虛擬環境可允許您所部署的虛擬應用程式，共用用戶端電腦的相同檔案系統和登錄。 這表示這些應用程式之間可共用資料，有別於標準的虛擬應用程式。 當已安裝應用程式或是在用戶端下次評估已安裝的應用程式時，用戶端電腦上便會建立或變更虛擬環境。 虛擬環境類似於獨立 App-V 5 中的連線群組。  

當您將連線群組從獨立 App-V 5 移轉至 Configuration Manager 虛擬環境時，必須確保 Configuration Manager 會正確管理用戶端電腦上既存的連線群組，並保留這些連線群組中的使用者環境。  

將 App-V 5 連線群組轉換成 Configuration Manager 虛擬環境：  

1.  為存在於 App-V 的所有應用程式建立 Configuration Manager 應用程式。  

2.  配合 [必要] 部署目的將應用程式部署到使用者或裝置。 對使用者的部署，必須部署到在 APP-V 中使用該應用程式的同一位使用者。 對電腦的部署，必須部署到在 APP-V 中擁有該應用程式的同一部電腦。  

3.  完成部署後，根據在獨立 App-V 中發佈的連線群組，建立相符的虛擬環境。 虛擬環境必須以相同順序包含相同的套件 (尤其是 App-V 5 部署類型)。  

如需如何建立 App-V 虛擬環境的資訊，請參閱[如何在 Configuration Manager 中建立 App-V 虛擬環境](../../apps/deploy-use/create-app-v-virtual-environments.md)。  

或者，您可以在透過 Configuration Manager 部署應用程式之前，從 App-V 用戶端刪除所有連線群組。 但是，這樣將會失去使用者可能已儲存在 App-V 連線群組中的任何設定。  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>App-V 4.6 中的動態套件組合  
動態套件組合是一項功能，您可用來將某個虛擬應用程式套件定義為相依於另一個虛擬應用程式套件。 應用程式執行時，App-V 用戶端會在應用程式的相同虛擬環境中裝載主要套件和相依的套件。  

若要透過 Configuration Manager 使用此功能，您必須同時部署這兩個套件並向 App-V 用戶端註冊。 為了確保相依套件內容會本機裝載於用戶端電腦上，請設定應用程式部署以進行本機傳遞 (下載與執行)。  

如需 App-V 動態套件組合的詳細資訊，請參閱 App-V 說明文件。  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a>將 App-V 4.6 應用程式轉換為 App-V 5 應用程式  
App-V 4.6 與 App-V 5 之間的應用程式封裝格式已變更。 不再支援使用 App-V 4.6 排序的應用程式。 但是，App-V 5 提供一種可讓您用來轉換應用程式的套件轉換工具。 如需詳細資訊，請參閱 [App-V 5 說明文件](http://technet.microsoft.com/library/jj713472.aspx)。  

利用下列步驟以轉換 App-V 4.6 應用程式為 App-V 5 應用程式：  

1.  轉換或重新排序 App-V 4.6 套件為 App-V 5 格式。  

2.  將 App-V 5 用戶端部署至階層內的電腦。  

3.  建立包含 App-V 5 應用程式部署類型的新應用程式，並且建立取代規則以取代 App-V 4.6 應用程式。  

4.  按照需求建立虛擬環境。  

5.  部署新的 App-V 5 應用程式至電腦。  

##  <a name="user-and-deployment-configuration-files"></a>使用者與部署組態檔案  
使用者與部署設定檔案具備控制應用程式行為的設定。 您可以使用這些檔案來變更應用程式設定，而不需重新排序應用程式。  

標準的 App-V 5 應用程式可包含下列檔案：  

-   應用程式套件 (.appv) 檔  

-   使用者設定檔  

-   部署設定檔  

使用者設定檔具備只會套用至登入使用者的設定。 例如，您可以編輯設定檔，以變更將部署至使用者的應用程式捷徑相關資訊。 您也可以利用多個部署類型來建立 Configuration Manager 應用程式。 每種部署類型均可包含不同的使用者設定檔，並使用需求規則來確保這些規則已針對相關使用者進行安裝。  

部署設定檔具備套用至電腦的設定，例如登錄設定。 此檔案也具備要套用至所有使用者的使用者設定。  

如果您要使用 Configuration Manager 部署 App-V 5 虛擬應用程式，則在建立 App-V 5 部署類型時，這三個檔案都必須位於相同資料夾中。 如果資料夾內有多個檔案，Configuration Manager 將使用最新的檔案。  

如需詳細資訊，請參閱 [App-V 5 說明文件](http://technet.microsoft.com/library/jj713466.aspx)。  

##  <a name="app-v-local-interaction"></a>APP-V 本機互動  
在部分應用程式部署案例中，應用程式會本機安裝於用戶端電腦上，而其他應用程式則是當作虛擬應用程式部署至相同的用戶端電腦。 根據預設，本機上所安裝的應用程式無法偵測到虛擬應用程式並直接與其進行通訊。 這預期是 App-V 所提供的應用程式隔離行為。 本機互動是 App-V 用戶端的一項功能，您可以為每個應用程式啟用此功能，以允許在用戶端電腦上執行的本機安裝應用程式能夠查看虛擬化應用程式並與其通訊。 Configuration Manager 與 App-V 可完整支援本機互動。  

如需 App-V 本機互動功能的詳細資訊，請參閱您的 App-V 說明文件。  

##  <a name="app-v-5-shared-content-store"></a>APP-V 5 共用內容存放區  
Configuration Manager 支援 App-V 5 共用內容存放區功能。 如需詳細資訊，請參閱 [規劃 App-V 5.0 共用內容存放區 (SCS)](http://technet.microsoft.com/library/jj713431.aspx)。  

##  <a name="monitoring-virtual-applications"></a>監視虛擬應用程式  

### <a name="virtual-application-reports"></a>虛擬應用程式報告  
您可以使用下列報告以監視在您 Configuration Manager 環境內的 App-V：  

|報表名稱|說明|  
|-----------------|-----------------|  
|App-V 虛擬環境結果|如果選取的虛擬環境狀態與所選集合指定的狀態相符，則顯示與該環境有關的資訊 (僅限 App-V 5)。|  
|資產的 App-V 虛擬環境結果|如果選取的虛擬環境與所選虛擬環境指定的資產和任何部署類型相符，則顯示與該環境有關的資訊 (僅限 App-V 5)。|  
|App-V 虛擬環境狀態|針對選取的集合顯示所選虛擬環境的相容性資訊。 此報告中的 [已保留] 欄顯示已經無法再套用之前設定的虛擬環境資產，但已經保留以便應用程式內的使用者設定可持續在虛擬環境中執行 (僅限 App-V 5)。|  
|具有特定虛擬應用程式的電腦|顯示具有使用 Application Virtualization Management Sequencer 建立的指定 App-V 應用程式捷徑的電腦摘要 (僅限 App-V 4.6)。|  
|具有特定虛擬應用程式套件的電腦|顯示已安裝指定 App-V 應用程式套件的電腦清單 (僅限 App-V 4.6)。|  
|計算虛擬應用程式套件的所有執行個體|顯示所有已偵測到的 App-V 應用程式套件的計數 (僅限 App-V 4.6)。|  
|計算虛擬應用程式的所有執行個體|顯示所有已偵測到的 App-V 應用程式的計數 (僅限 App-V 4.6)。|  

### <a name="log-files"></a>記錄檔  
Configuration Manager 將有關虛擬應用程式部署的資訊記錄在記錄檔內。 如需虛擬應用程式和 Configuration Manager 應用程式管理所使用的記錄檔相關資訊，請參閱 [System Center Configuration Manager 中的記錄檔](../../core/plan-design/hierarchy/log-files.md)。  

如果是 Windows Vista、Windows 7 及 Windows 8，您可以在 C:\ProgramData\Microsoft\Application Virtualization Client 中找到 App-V 用戶端的記錄檔。  
