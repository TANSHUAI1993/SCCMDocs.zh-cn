---
title: "安裝和設定軟體更新點 | Microsoft Docs"
description: "主要站台需要管理中心網站上的軟體更新點才能進行軟體更新相容性評估，以及將軟體更新部署至用戶端。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 05/30/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 7d369384d133c90a15e01df50ac53992d61f3873
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="install-and-configure-a-software-update-point"></a>安裝及設定軟體更新點  

*適用於：System Center Configuration Manager (最新分支)*


> [!IMPORTANT]  
>  您必須驗證伺服器是否符合必要的相依性，並判定站台上的軟體更新點基礎結構，再安裝軟體更新點站台系統角色。 如需如何規劃軟體更新及判定軟體更新點基礎結構的詳細資訊，請參閱[規劃軟體更新](../plan-design/plan-for-software-updates.md)。  

 管理中心網站和主要站台上需要軟體更新點才能啟用軟體更新相容性評估，以及將軟體更新部署至用戶端。 軟體更新點在次要站台上是選用項目。 您必須在已安裝 WSUS 的伺服器上建立軟體更新點站台系統角色。 軟體更新點會與 WSUS 服務互動，以設定軟體更新設定，並要求同步處理軟體更新中繼資料。 當您擁有 Configuration Manager 階層時，可以先在管理中心網站上安裝及設定軟體更新點，然後在子主要站台或可選擇在次要站台上安裝及設定軟體更新點。 當您擁有的是獨立主要站台而非管理中心網站時，請先在主要站台安裝及設定軟體更新點，再選擇是否要在次要站台安裝及設定軟體更新點。 某些設定只有當您在頂層站台上設定軟體更新點時才能使用。 您必須根據安裝軟體更新點的位置，考慮不同的選項。  

> [!IMPORTANT]  
>  您可以在站台上安裝一個以上的軟體更新點。 您安裝的第一個軟體更新點會設定為同步處理來源，同步處理來自 Microsoft Update 或上游同步處理來源的更新。 站台的其他軟體更新點，會設定為第一個軟體更新點的複本。 因此，某些設定在您安裝及設定初始軟體更新點後將無法使用。  

> [!IMPORTANT]  
>  不支援在已設定並且用來作為獨立 WSUS 伺服器的伺服器上安裝軟體更新點站台系統角色，或使用軟體更新點直接管理 WSUS 用戶端。 現有的 WSUS 伺服器僅支援作為主動式軟體更新點的上游同步處理來源。 請參閱[從上游資料來源位置同步處理](#BKMK_wsussync)

 您可以將軟體更新點站台系統角色新增至現有站台系統伺服器，或建立新的站台系統伺服器。 在 [建立站台系統伺服器精靈]  或 [新增站台系統角色精靈]  的 [系統角色選取]  頁面上，根據您是否要將站台系統角色新增至新的或現有的站台伺服器來選取 [軟體更新點] ，然後在精靈中設定軟體更新點設定。 這些設定會因使用不同的 Configuration Manager 版本而異。 如需安裝站台系統角色方式的詳細資訊，請參閱[安裝站台系統角色](../../core/servers/deploy/configure/install-site-system-roles.md)。  

 下列各節提供有關站台上軟體更新點設定的資訊。  

## <a name="proxy-server-settings"></a>Proxy 伺服器設定  
 您可以根據所使用的 Configuration Manager 版本，在 [建立站台系統伺服器精靈] 或 [新增站台系統角色精靈] 的不同頁面上設定 Proxy 伺服器設定。  

-   您必須先設定 Proxy 伺服器，然後再指定使用 Proxy 伺服器進行軟體更新的時間。 進行以下設定：  

    -   在精靈的 [Proxy]  頁面上，或在 [站台系統內容] 的 [Proxy]  索引標籤上，設定 Proxy 伺服器設定。 Proxy 伺服器設定為站台系統範圍的設定，這表示所有站台系統角色都會使用您所指定的 Proxy 伺服器設定。  

    -   指定是否要在 Configuration Manager 同步處理軟體更新及其使用自動部署規則下載內容時，使用 Proxy 伺服器。 請在精靈的 [Proxy 和帳戶設定]  頁面上，或在 [軟體更新點內容] 的 [Proxy 和帳戶設定]  索引標籤上，設定軟體更新點 Proxy 伺服器設定。  

        > [!NOTE]  
        >  [在使用自動部署規則下載內容時使用 Proxy 伺服器]  設定可正常使用，但不適用於次要站台上的軟體更新點。 只有管理中心網站和主要站台上的軟體更新點，會從 Microsoft Update 頁面下載內容。  

> [!IMPORTANT]  
>  預設會使用建立自動部署規則的伺服器 [本機系統]  帳戶與網際網路連線，並在執行自動部署規則時下載軟體更新。 當此帳戶無法存取網際網路時，將無法下載軟體更新，並且會在 ruleengine.log 中記錄下列項目：**無法從網際網路下載更新。錯誤 = 12007**。 設定認證後，便可在 [本機系統] 帳戶無法存取網際網路時用它來連線 Proxy 伺服器。  


## <a name="wsus-settings"></a>WSUS 設定  
 您必須根據所使用的 Configuration Manager 版本，在 [建立站台系統伺服器精靈] 或 [新增站台系統角色精靈] 的不同頁面上設定 WSUS 設定，而在某些情況下，只需在軟體更新點的內容 (也稱為「軟體更新點元件內容」) 中進行設定。 使用以下各節中的資訊，設定 WSUS 設定。  

### <a name="BKMK_wsusport"></a>WSUS 連接埠設定  
 您必須在精靈的 [軟體更新點] 頁面，或在軟體更新點的內容中，設定 WSUS 連接埠設定。 請使用下列程序判斷 WSUS 使用的連接埠設定。  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>判斷 IIS 中的連接埠設定  

 1.  在 WSUS 伺服器上，開啟 Internet Information Services (IIS) Manager。  

 2.  展開 [網站] ，以滑鼠右鍵按一下 WSUS 伺服器的網站，然後按一下 [編輯繫結] 。 在 [站台繫結] 對話方塊中，HTTP 和 HTTPS 連接埠的值都會顯示在 [連接埠]  欄中。


### <a name="configure-ssl-communications-to-wsus"></a>設定與 WSUS 的 SSL 通訊  
 您可以在精靈的 [一般]  頁面或在軟體更新點內容的 [一般]  索引標籤上，設定 SSL 通訊。  

 如需如何使用 SSL 的詳細資訊，請參閱 [Decide whether to configure WSUS to use SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL)。  

### <a name="wsus-server-connection-account"></a>WSUS 伺服器連線帳戶  
 您可以設定帳戶，以供站台伺服器在連線到軟體更新點上執行的 WSUS 時使用。 當您未設定此帳戶時，Configuration Manager 會使用電腦帳戶讓站台伺服器與 WSUS 連線。 在精靈的 [Proxy 和帳戶設定]  頁面或在 [軟體更新點內容] 的 [Proxy 和帳戶設定]  索引標籤上，設定 WSUS 伺服器連線帳戶。  您可以根據所使用的 Configuration Manager 版本，在精靈的不同位置中設定該帳戶。  

 如需 Configuration Manager 帳戶的詳細資訊，請參閱 [System Center Configuration Manager 中使用的帳戶](../../core/plan-design/hierarchy/accounts.md)。  

## <a name="synchronization-source"></a>同步處理來源  
 您可以在精靈的 [同步處理來源]  頁面，或者 [軟體更新點元件內容] 中的 [同步處理設定]  標籤上，設定軟體更新同步處理的上游同步處理來源。 您的同步處理來源選項會依站台而有所不同。  

 當您設定站台的軟體更新點時，請使用下表的可用選項。  

|網站|可用的同步處理來源選項|  
|----------|----------------------------------------------|  
|-   管理中心網站<br />-   獨立主要站台|-   從 Microsoft Update 網站同步處理<br />-   從上游資料來源位置同步處理<br />-   不要從 Microsoft Update 或上游資料來源同步處理|  
|-   站台的其他軟體更新點<br />-   子主要站台<br />-   次要站台|-   從上游資料來源位置同步處理|  

 以下清單提供有關可以作為同步處理來源使用的各個選項的詳細資訊：  

-   **從 Microsoft Update 同步處理**：使用此設定可從 Microsoft Update 同步處理軟體更新中繼資料。 管理中心網站必須具有網際網路存取權，否則同步處理將會失敗。 此設定只有當您在頂層站台設定軟體更新點時才能使用。  

    > [!NOTE]  
    >  當軟體更新點與網際網路之間有防火牆時，可能需要將防火牆設定為接受用於 WSUS 網站的 HTTP 與 HTTPS 連接埠。 您也可以選擇將防火牆上的存取權限制在有限的網域。 如需如何規劃支援軟體更新之防火牆的詳細資訊，請參閱 [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls)。  

-   **<a name="BKMK_wsussync"></a>從上游資料來源位置同步處理**：使用此設定可從上游同步處理來源來同步處理軟體更新中繼資料。 子主要站台與次要站台會自動設定為對此設定使用父站台 URL。 您可以選擇從現有的 WSUS 伺服器同步處理軟體更新。 指定 URL，例如 https://WSUSServer:8531 ，其中 8531 是用於連線至 WSUS 伺服器的連接埠。  

-   **不要從 Microsoft Update 或上游資料來源同步處理**：使用此設定可在頂層站台的軟體更新點從網際網路中斷連線時，手動同步處理軟體更新。 如需詳細資訊，請參閱[從已中斷連線的軟體更新點同步處理軟體更新](synchronize-software-updates-disconnected.md)。  

> [!NOTE]  
>  當軟體更新點與網際網路之間有防火牆時，可能需要將防火牆設定為接受用於 WSUS 網站的 HTTP 與 HTTPS 連接埠。 您也可以選擇將防火牆上的存取權限制在有限的網域。 如需如何規劃支援軟體更新之防火牆的詳細資訊，請參閱 [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls)。  

 您也可以在精靈的 [同步處理來源]  頁面或 [軟體更新點元件內容] 的 [同步處理設定]  索引標籤上，設定是否要建立 WSUS 報告事件。 Configuration Manager 不會使用這些事件；因此，您通常可以選擇預設設定 [不要建立 WSUS 報告事件]。  

## <a name="synchronization-schedule"></a>同步處理排程  
 在精靈的 [同步處理排程]  頁面上或 [軟體更新點元件內容] 中設定同步處理排程。 此設定只有在頂層站台軟體更新點上設定。  

 如果您啟用排程，就可以設定週期性的簡易或自訂同步處理排程。 當您設定簡易排程，會在建立排程時根據執行 Configuration Manager 主控台電腦的本機時間設定開始時間。 當您設定自訂排程的開始時間時，會根據執行 Configuration Manager 主控台電腦的本機時間設定。  

> [!TIP]  
>  排程軟體更新同步處理會使用適合您環境的時間範圍來執行。 常見的情形是設定為在 Microsoft 每個月的第二個星期二 (一般稱為 Patch Tuesday (周二修補日)) 的定期安全性更新發行後，馬上執行軟體更新同步處理。 另一種常見的情形是將軟體更新同步處理排程，設定為在每天當您使用軟體更新執行 Endpoint Protection 定義和引擎更新時執行。  

> [!NOTE]  
>  當您選擇不在排程上啟用軟體更新同步處理時，您可以從 [軟體程式庫] 工作區中的 [所有軟體更新]  或 [軟體更新群組]  節點手動同步處理軟體更新。 如需詳細資訊，請參閱[同步處理軟體更新](synchronize-software-updates.md)。  

## <a name="supersedence-rules"></a>取代規則  
 在精靈的 [取代規則]  頁面或 [軟體更新點元件內容] 的 [取代規則]  標籤上設定取代設定。 您只能在頂層站台設定取代規則。  

 在此頁面上，您可以指定已取代的軟體更新立即到期 (以免包含在新的部署中)，並且將現有的部署加上旗標，以表示已取代的軟體更新中含有一個或多個到期的軟體更新。 或者，您也可以指定已取代的軟體更新經過多久以後到期，如此可讓您繼續部署已取代的軟體更新。 如需詳細資訊，請參閱 [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules)。  

> [!NOTE]  
>  精靈的 [取代規則]  頁面只有在您設定站台的第一個軟體更新點時才能使用。 當您安裝額外的軟體更新點時，不會顯示此頁面。  

## <a name="classifications"></a>分類  
 在精靈的 [分類]  頁面或 [軟體更新點元件內容] 的 [分類]  標籤上設定分類設定。 如需軟體更新分類的詳細資訊，請參閱 [Update classifications](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications)。  

> [!NOTE]  
>  精靈的 [分類]  頁面只有在您設定站台的第一個軟體更新點時才能使用。 當您安裝額外的軟體更新點時，不會顯示此頁面。  

> [!TIP]  
>  當您首次在頂層站台安裝軟體更新點時，請清除所有軟體更新分類。 在初次軟體更新同步處理之後，請從更新的清單設定分類，然後重新起始同步處理。 此設定只有在頂層站台軟體更新點上設定。  

## <a name="products"></a>產品  
 在精靈的 [產品]  頁面或 [軟體更新點元件內容] 的 [產品]  標籤上設定產品設定。  

> [!NOTE]  
>  精靈的 [產品]  頁面只有在您設定站台的第一個軟體更新點時才能使用。 當您安裝額外的軟體更新點時，不會顯示此頁面。  

> [!TIP]  
>  當您首次在頂層站台安裝軟體更新點時，請清除所有產品。 在初次軟體更新同步處理之後，請從更新的清單設定產品，然後重新起始同步處理。 此設定只有在頂層站台軟體更新點上設定。  

## <a name="languages"></a>語言  
 在精靈的 [語言]  頁面或 [軟體更新點元件內容] 的 [語言]  標籤上設定語言設定。 請指定您要同步處理軟體更新檔案和摘要詳細資料的語言。 [軟體更新檔案] 設定會在 Configuration Manager 階層中的各個軟體更新點設定。 [摘要詳細資料]  設定只會在頂層站台軟體更新點設定。 如需詳細資訊，請參閱 [Languages](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages)。  

> [!NOTE]  
>  精靈的 [語言]  頁面只有當您在管理中心網站安裝軟體更新點時才能使用。 您可以從 [軟體更新點元件內容] 中的 [語言]  標籤設定子站台的軟體更新檔案語言。  

## <a name="next-steps"></a>後續步驟
您已從 Configuration Manager 階層的最上層站台開始安裝軟體更新點。 請重複本主題中的程序，在子站台上安裝軟體更新點。

安裝好軟體更新點之後，請移至[同步處理軟體更新](synchronize-software-updates.md)。
