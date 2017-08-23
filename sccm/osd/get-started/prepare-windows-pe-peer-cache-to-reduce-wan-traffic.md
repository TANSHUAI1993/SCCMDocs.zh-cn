---
title: "準備 Windows PE 對等快取以減少 WAN 流量 | Microsoft Docs"
description: "Windows PE 對等快取作用於 Windows PE，以從本機對等取得內容，並在沒有本機發佈點時，將 WAN 流量降至最低。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
caps.latest.revision: "11"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 814c6133a30b1116d05aaeafddb0dfb7fe2a390e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-system-center-configuration-manager"></a>準備 Windows PE 對等快取，以降低 System Center Configuration Manager 中的 WAN 流量

*適用於：System Center Configuration Manager (最新分支)*

當您在 System Center Configuration Manager 中部署新的作業系統時，執行工作順序的電腦可使用 Windows PE 對等快取，從本機對等裝置 (對等快取來源) 取得內容，而不是從發佈點下載內容。 這有助於在分公司沒有本機發佈點的案例中，降低廣域網路 (WAN) 流量。  

 Windows PE 對等快取類似 [Windows BranchCache](http://technet.microsoft.com/library/mt617255\(TechNet.10\).aspx#bkmk_branchcache)，但可在 Windows 預先安裝環境 (Windows PE) 中運作。 如果您從作業系統內容 (例如從用戶端的軟體中心) 啟動工作順序，則不會使用 Windows PE 對等快取。 下列字詞用以描述使用 Windows PE 對等快取的用戶端：  

-   **對等快取用戶端** 是設定為使用 Windows PE 對等快取的電腦。  

-   **對等快取來源** 是設定成使用對等快取的用戶端，也是提供內容給其他要求該內容之對等快取用戶端的用戶端。  

使用下列各節管理對等快取。

##  <a name="BKMK_PeerCacheObjects"></a> 存放在對等快取來源的物件  
 在 Windows PE 中執行工作順序時，其設定為會使用 Windows PE 對等快取可以取得下列內容物件：  

-   作業系統映像  

-   驅動程式套件  

-   套件和程式 (當用戶端繼續在完整作業系統中執行工作順序時，如果工作順序原本是針對在 Windows PE 中執行時的對等快取所設定，用戶端就會從對等快取來源取得此內容。)  

-   其他開機映像  

 下列內容物件一律不會使用對等快取傳輸。 下列內容物件永遠不會透過對等快取傳輸，也不會從發佈點傳輸，或在環境中已設定 Windows BranchCache 時由 Windows BranchCache 傳送：  

-   應用程式  

-   軟體更新  

##  <a name="BKMK_PeerCacheWork"></a> Windows PE 對等快取運作方式為何？  
 假設分公司沒有發佈點，但允許幾個用戶端使用 Windows PE 對等快取的情況。 您部署的工作順序，設定為對設定成是對等快取來源一部分的數個用戶端，使用對等快取。 第一個執行工作順序的用戶端，會為具備該內容的對等，廣播一則要求。 因為找不到任何項目，所以會從 WAN 中的發佈點取得內容。 用戶端會安裝新映像，然後將內容儲存在其 Configuration Manager 用戶端快取中，以作為其他用戶端的對等快取來源。 當下一個用戶端執行工作順序時，它會在對等快取來源的子網路上廣播要求，而第一個用戶端會回應並提供其快取內容。  

##  <a name="BKMK_PeerCacheDetermine"></a> 決定哪些用戶端將隸屬於 Windows PE 對等快取來源  
 為協助您判斷哪些電腦要選取為 Windows PE 對等快取來源，您應該考量一些情況：  

-   Windows PE 對等快取來源應為一直開機且對等快取用戶端可以使用的桌上型電腦。  

-   Windows PE 對等快取的用戶端快取大小，足以儲存映像。  

##  <a name="BKMK_PeerCacheRequirements"></a> 使用 Windows PE 對等快取來源的用戶端需求  
 若是使用 Windows PE 對等快取來源的用戶端，必須符合下列需求：  

-   Configuration Manager 用戶端必須能夠跨網路上的下列連接埠進行通訊：  

    -   用於初始網路廣播以尋找對等快取來源的連接埠。 根據預設，此連接埠是 8004。  

    -   用於從對等快取來源 (HTTP 和 HTTPS) 下載內容的連接埠。 根據預設，此連接埠是 8003。  

        > [!TIP]  
        >  用戶端會使用 HTTPS 下載可供使用的內容。 但會為 HTTP 或 HTTPS 使用相同的連接埠號碼。  

-   在用戶端上[Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) 以確保用戶端有足夠的空間可保存及儲存所部署的映像。 Windows PE 對等快取不會影響用戶端快取的設定或行為。  

-   工作順序部署的 [部署] 選項，必須設定為 [工作順序需要時將內容下載到本機]。  

##  <a name="BKMK_PeerCacheConfigure"></a> 設定 Windows PE 對等快取  
 您可以使用下列方法，利用對等快取內容來佈建用戶端，使其可成為對等快取來源：  

-   找不到具有內容之對等快取來源的對等快取用戶端會從發佈點下載內容。  如果用戶端收到的用戶端設定啟用對等快取，並將工作順序設定為保留快取內容，則用戶端會變成對等快取來源。  

-   對等快取用戶端可以從另一個對等快取用戶端 (對等快取來源) 取得內容。  由於用戶端已設定為使用對等快取，因此當它執行設定為保留快取內容的工作順序時，用戶端會變成對等快取來源。  

-   用戶端執行的工作順序，包括選用步驟 [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)，其用於預先設置內含於 Windows PE 對等快取工作順序中的相關內容。 當您使用這個方法時：  

    -   用戶端不需要安裝正在部署的映像。  

    -   除了 [下載套件內容]  選項之外，工作順序還必須使用 [Configuration Manager 用戶端快取]  選項。 您可以使用這個選項將內容儲存在用戶端快取中，以便用戶端可以做為其他對等快取用戶端的對等快取來源。  

 下列程序將協助您在用戶端上設定 Windows PE 對等快取，並設定支援對等快取的工作順序。  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>設定 Windows PE 對等快取來源電腦  

1.  在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [用戶端設定]，然後建立新的 [自訂用戶端裝置設定] 或編輯現有的設定物件。 您也可以針對 [預設用戶端設定]  物件進行這項設定。  

    > [!TIP]  
    >  自訂設定物件可用來管理哪些用戶端會收到這項組態。 例如，您可能想要在使用者經常移動的膝上型電腦上避免進行這項設定。 具備高度機動性的系統並不適合做為提供內容給其他對等快取用戶端的來源。  
    >   
    >  另請記住，當您將這項設定設定為 [預設用戶端設定] 的一部分時，該項組態會套用到您環境中的所有用戶端。  

2.  在 [Windows PE 對等快取] 下，將 [允許完整作業系統中的 Configuration Manager 共用內容]  設定為 [是] 。  

    -   預設只會啟用 HTTP。 如果您想要讓用戶端能夠透過 HTTPS 下載內容，請將 [啟用 HTTPS 進行用戶端對等通訊]  設定為 [是] 。  

    -   根據預設，用於廣播的連接埠會設定為 8004，而用於下載內容的連接埠會設定為 8003。 您可以變更這兩者。  

3.  對選取作為對等快取來源的用戶端，儲存用戶端設定並加以部署。  

 使用這個設定物件設定裝置之後，會將裝置設定為對等快取來源。 這些設定應該部署到潛在的對等快取用戶端，以便設定必要的連接埠和通訊協定。  

###  <a name="BKMK_PeerCacheConfigureTS"></a> 為 Windows PE 對等快取設定工作順序  
 當您設定工作順序時，請使用下列工作順序變數作為部署工作順序所在之集合上的集合變數：  

-   **SMSTSPeerDownload**  

     值：TRUE  

     可讓用戶端使用 Windows PE 對等快取。  

-   **SMSTSPeerRequestPort**  

     值：<連接埠號碼\>  

     當您未使用在 [用戶端設定] 中設定的預設連接埠 (8004) 時，您必須將這個變數設定為初始廣播所要使用的自訂網路連接埠值。  

-   **SMSTSPreserveContent**  

     值：TRUE  

     這會標幟工作順序中的內容，以在部署後將內容保留在 Configuration Manager 用戶端快取中。 這有別於使用 SMSTSPersisContent，SMSTSPersisContent 只會在工作順序持續期間保留內容，並會使用工作順序快取，而不是 Configuration Manager 用戶端快取。  

 如需詳細資訊，請參閱[工作順序內建變數](../understand/task-sequence-built-in-variables.md)。  

###  <a name="BKMK_PeerCacheValidate"></a> 確認順利使用 Windows PE 對等快取  
 使用 Windows PE 對等快取部署工作順序且加以安裝之後，可以透過檢視執行工作順序之用戶端上的 **smsts.log** ，來確認程序中已順利使用該對等快取。  

 在記錄檔中，尋找類似如下的項目，其中 <*SourceServerName*> 可識別用戶端取得內容的來源電腦。 這部電腦應該是對等快取來源，而不是發佈點伺服器。 其他詳細資料會依您的本機環境和組態而有所不同。  

-   *<![LOG[Downloaded file from http:// <SourceServerName\>:8003/SCCM_BranchCache$/SS10000C/sccm?/install.wim to C:\\_SMSTaskSequence\Packages\SS10000C\install.wim ]LOG]!><time="14:24:33.329+420" date="06-26-2015" component="ApplyOperatingSystem" context="" type="1" thread="1256" file="downloadcontent.cpp:1626">*  
