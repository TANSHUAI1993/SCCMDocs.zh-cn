---
title: "尋找站台資源 | Microsoft Docs"
description: "了解 System Center Configuration Manager 用戶端如何和何時使用服務位置來尋找站台資源。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1c9e7ada6a8aa228b30e58865baae0f6e529e6af
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="learn-how-clients-find-site-resources-and-services-for-system-center-configuration-manager"></a>了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務

*適用於︰System Center Configuration Manager (最新分支)*

System Center Configuration Manager 用戶端使用稱為*服務位置*的處理序尋找可與其通訊的站台系統伺服器，而該伺服器會提供指示用戶端使用的服務。 了解用戶端使用服務位置以尋找站台資源的方法與時機，這些資源有助於您設定站台以順利支援用戶端工作。 這些設定會要求站台與 Active Directory Domain Services (AD DS) 和 DNS 之類的網域和網路設定進行互動， 也可能會要求您設定更複雜的替代方案。  

 提供服務的站台系統角色範例包括︰

 - 用戶端核心站台系統伺服器。
 - 管理點。
 - 能與用戶端通訊的其他站台系統伺服器，如發佈點和軟體更新點。  



##  <a name="bkmk_fund"></a> Fundamentals of service location  
 使用服務位置找到與其進行通訊的管理點時，用戶端會評估其目前網路位置、通訊協定喜好設定和指派的站台。  

 **用戶端與管理點通訊︰**  
-   下載站台其他管理點的相關資訊，讓它們建置已知的管理點清單 (稱為「管理組件 (MP) 清單」)，用於未來服務位置循環。  
-   上傳設定詳細資料 (例如清查和狀態)。  
-   下載原則，可在用戶端上進行設定，並通知用戶端有關它可以或必須安裝的軟體和其他相關工作。  
-   針對提供用戶端已設定要使用之服務的其他站台系統角色，要求角色的相關資訊。 範例包括用戶端可安裝之軟體的發佈點，或取得更新的來源軟體更新點。  

**Configuration Manager 用戶端提出服務位置要求：**  
-   每 25 個小時的連續作業。  
-   用戶端偵測到其網路設定或位置的變更時。  
-   電腦上的 **ccmexec.exe** 服務 (核心用戶端服務) 啟動時。  
-   用戶端必須找出提供所需服務的站台系統角色時。  

**用戶端嘗試尋找裝載站台系統角色的伺服器時**，會使用服務位置找到支援用戶端通訊協定 (HTTP 或 HTTPS) 的站台系統角色。 根據預設，用戶端會使用最安全的可用方法。 請考慮下列事項：  

-   若要使用 HTTPS，您必須具有公開金鑰基礎結構 (PKI)，並且必須在用戶端與伺服器上安裝 PKI 憑證。 如需如何使用憑證的資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

-   在部署使用網際網路資訊服務 (IIS) 並支援從用戶端進行通訊的網站系統角色時，您必須指定用戶端要使用 HTTP 或 HTTPS 連線至網站系統。 如果您使用 HTTP，您也必須考慮簽署和加密選擇。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃安全性](../../../core/plan-design/security/plan-for-security.md)中的[規劃簽署和加密](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption)。  

##  <a name="BKMK_Plan_Service_Location"></a> 服務位置以及用戶端如何判斷其指派的管理點  
用戶端第一次指派至主要站台時，它會為該站台選取預設管理點。 主要站台支援多個管理點，且每個用戶端會獨立地將管理點識別為其預設管理點。 這個預設管理點接著會變成用戶端指派的管理點。 (您也可以使用用戶端安裝命令，來設定用戶端於安裝時指派的管理點。)  

用戶端會依據用戶端目前的網路位置與界限群組組態，選取要通訊的管理點。 用戶端即使有指派的管理點，可能也不是用戶端所使用的管理點。  

    > [!NOTE]  
    >  A client always uses the assigned management point for registration messages and certain policy messages, even when other communications are sent to a proxy or local management point.  

您可以使用慣用的管理點。 慣用的管理點都是用戶端指派的站台管理點，與用戶端用來找出站台系統伺服器的界限群組相關聯。 慣用管理點做為站台系統伺服器與界限群組之間的關聯，類似於發佈點或狀態移轉點與界限群組相關聯的方式。 當用戶端從其指派的站台使用管理點時，如果您啟用此階層慣用的管理點，它就會先嘗試使用慣用的管理點，然後才從其指派的站台使用其他管理點。  

您也可以使用 TechNet.com 之[管理點親和性](http://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx)部落格中的資訊，來設定管理點親和性。 管理點親和性會為指派的管理點覆寫預設行為，並讓用戶端能使用一個或多個特定的管理點。  

用戶端每次需要連絡管理點時會檢查管理組件 (MP) 清單，其儲存在本機 Windows Management Instrumentation (WMI) 中。 在安裝用戶端時，它會建立初始的管理組件 (MP) 清單。 接著，用戶端會定期更新清單及階層中每個管理點的相關詳細資料。  

當用戶端在管理組件 (MP) 清單中找不到有效的管理點時，就會依序搜尋下列服務位置來源，直到找到可使用的管理點：  

1.  管理點  
2.  AD DS  
3.  DNS  
4.  WINS  

在用戶端順利找出並連絡管理點之後，它會下載階層中目前可用的管理點清單，並更新本機管理組件 (MP) 清單。 這同樣適用於加入網域及未加入網域的用戶端。  

例如，當位於網際網路的 Configuration Manager 用戶端連線到以網際網路為基礎的管理點時，管理點即會將站台中以網際網路為基礎的可用管理點清單傳送給該用戶端。 同樣地，加入網域或工作群組中的用戶端也會收到可使用的管理點清單。  

若不是針對網際網路設定的用戶端，就不會提供僅限網際網路對向的管理點。 針對網際網路設定的工作群組用戶端只會與網際網路對向管理點通訊。  

##  <a name="BKMK_MPList"></a> 管理組件 (MP) 清單  
管理組件清單是用戶端偏好的服務位置來源，因為它是用戶端先前所識別管理點的優先使用清單。 當用戶端更新清單時，這份清單即會依每個用戶端的網路位置排序，並本機儲存在 WMI 中的用戶端上。  

### <a name="building-the-initial-mp-list"></a>建立初始管理組件 (MP) 清單  
在用戶端安裝期間，下列規則可用來建立用戶端的初始管理組件 (MP) 清單：  

-   初始清單包含在用戶端安裝期間指定的管理點 (使用 **SMSMP**= 或 **/MP** 選項)。  
-   用戶端會查詢 AD DS 以取得發佈的管理點。 若要從 AD DS 進行識別，管理點必須來自用戶端指派的站台，且必須與用戶端的產品版本相同。  
-   如果在用戶端安裝期間未指定任何管理點，且 Active Directory 架構未擴充，用戶端會檢查 DNS 與 WINS 以取得發佈的管理點。  
-   當用戶端建立初始清單時，階層中某些管理點的相關資訊可能是未知狀態。  

### <a name="organizing-the-mp-list"></a>組織管理組件 (MP) 清單  
用戶端會使用下列分類來組織管理點清單：  

-   **Proxy**：次要站台的管理點。  
-   **本機**：與用戶端目前網路位置相關聯的任何管理點 (根據站台界限所定義)。 請注意以下界限相關資訊︰
    -   當用戶端屬於多個界限群組時，本機管理點清單會由包含目前用戶端網路位置之所有界限的聯合而定。  
    -   一般而言，本機管理點是用戶端指派的管理點的子集，除非用戶端位於與其他網站 (其管理點適用於該用戶端的界限群組) 相關聯的網路位置上。   


-   **已指派**：任何屬於用戶端指派之站台的站台系統的任何管理點。  

您可以使用慣用的管理點。 不與界限群組相關聯之站台的管理點，或不在未與用戶端目前站台位置相關聯之界限群組的管理點，都不會當成慣用管理點。 它們會在用戶端無法識別可用的慣用管理點時使用。  

### <a name="selecting-a-management-point-to-use"></a>選取要使用的管理點  
若是一般通訊，用戶端會根據用戶端的站台位置並以下列分類順序來嘗試使用管理點：  

1.  Proxy  
2.  本機  
3.  指派的  

不過，即使其他通訊會傳送至 Proxy 或本機管理點，針對登錄訊息與特定原則訊息，用戶端一律會使用指派的管理點。  

在每個分類 (Proxy、本機或已指派) 中，用戶端會嘗試根據喜好設定並以下列順序使用管理點：  

1.  在受信任樹系或本機樹系中支援的 HTTPS (當用戶端設定為 HTTPS 通訊)  
2.  不在受信任樹系或本機樹系中支援的 HTTPS (當用戶端設定為 HTTPS 通訊)  
3.  在受信任樹系或本機樹系中支援的 HTTP  
4.  不在受信任樹系或本機樹系中支援的 HTTP  

在依據喜好設定排序的一組管理點當中，用戶端會嘗試使用清單上的第一個管理點。 此管理點清單是隨機排序，並不會按照順序。 每當用戶端更新管理組件 (MP) 清單時，清單順序即會變更。  

當用戶端無法連絡第一個管理點時，它會嘗試清單上每個後續的管理點。 它會嘗試分類中每個慣用的管理點，然後再嘗試非慣用的管理點。 如果用戶端無法順利與分類中的任何管理點進行通訊，即會嘗試從下一個分類中連絡慣用的管理點，直到用戶端找到可用的管理點，依此類推。  

用戶端與管理點建立通訊之後，會繼續使用相同的管理點，除非發生下列情況：  

-   已過了 25 個小時。  
-   用戶端在 10 分鐘的期間內嘗試管理點通訊失敗五次。

接下來，用戶端會隨機選擇要使用的新管理點。  

##  <a name="bkmk_ad"></a> Active Directory  
加入網域的用戶端可以使用適用於服務位置的 AD DS。 若要這麼做，需具備可 [將資料發佈至 Active Directory](http://technet.microsoft.com/library/hh696543.aspx)的網站。  

當下列任何條件成立時，用戶端可以使用適用於服務位置的 AD DS：  

-   Active Directory [架構已經過擴充](https://technet.microsoft.com/library/mt345589.aspx)，或已為 System Center 2012 Configuration Manager 進行擴充。  
-   [Active Directory 樹系設定為支援發佈](http://technet.microsoft.com/library/hh696542.aspx)，且 Configuration Manager 網站設定為可發佈項目。  
-   用戶端電腦是 Active Directory 網域的成員，並可存取通用類別目錄伺服器。  

如果用戶端無法從 AD DS 找到要用於服務位置的管理點，就會嘗試使用 DNS。  

##  <a name="bkmk_dns"></a> DNS  
內部網路上的用戶端可以使用適用於服務位置的 DNS。 若要這麼做，階層中至少需具備一個可將管理點相關資訊發佈至 DNS 的網站。  

當下列任何條件成立時，請考慮使用適用於服務位置的 DNS：
-   未擴充 AD DS 架構以支援 Configuration Manager。
-   內部網路上的用戶端位於未啟用 Configuration Manager 發行的樹系中。  
-   用戶端位於工作群組電腦上，而且未設定為僅限網際網路用戶端管理。 (針對網際網路設定的工作群組用戶端只會與網際網路對向的管理點通訊，而且不會使用適用於服務位置的 DNS。)  
-   您可以 [設定用戶端從 DNS 尋找管理點](http://technet.microsoft.com/library/gg682055)。  

若網站會將管理點的服務位置記錄發佈到 DNS：  

-   發佈作業只適用於接受來自內部網路之用戶端連線的管理點。  
-   發佈作業會在管理點電腦的 DNS 區域中，新增服務位置資源記錄 (SRV RR)。 該電腦的 DNS 中必須有對應的主機項目。  

根據預設，加入網域的用戶端會從用戶端的本機網域搜尋 DNS 以取得管理點記錄。 您可以設定用戶端內容，針對已將管理點資訊發佈到 DNS 的網域指定網域尾碼。  

如需如何設定 DNS 尾碼用戶端內容的詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端電腦使用 DNS 發行尋找管理點](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md)。  

如果用戶端無法從 DNS 找到要用於服務位置的管理點，即會嘗試使用 WINS。  

### <a name="publish-management-points-to-dns"></a>將管理點發佈至 DNS  
若要將管理點發佈至 DNS，下列兩種條件必須成立：  

-   您的 DNS 伺服器支援服務位置資源記錄，方法是使用 8.1.2 以上版本的 BIND。  
-   在 Configuration Manager 中為管理點指定的內部網路 FQDN，在 DNS 中擁有主機項目 (例如，A 記錄)。  

> [!IMPORTANT]  
>  Configuration Manager DNS 發行不支援脫離的命名空間。 如果有脫離的命名空間，您可以手動將管理點發佈到 DNS，或使用本節中說明的其他服務位置方法的其中之一。  

**當您的 DNS 伺服器支援自動更新時**，可以將 Configuration Manager 設定為自動在內部網路將管理點發行到 DNS，或者手動將這些記錄發行到 DNS。 將管理點發佈到 DNS 時，會在服務位置 (SRV) 記錄中發佈其內部網路 FQDN 和連接埠號碼。 您可在 [管理點元件內容] 中設定網站的 DNS 發佈功能。 如需詳細資訊，請參閱 [System Center Configuration Manager 的站台元件](../../../core/servers/deploy/configure/site-components.md)。  

**當您的 DNS 區域針對動態更新設為「限安全」時**，只有第一個要發佈到 DNS 的管理點可使用預設權限順利完成。

如果只有一個管理點可以順利地發佈和變更其 DNS 記錄，且該管理點伺服器狀況良好，用戶端就能從該管理點取得完整的管理組件 (MP) 清單，並找出其慣用的管理點。


**當您的 DNS 伺服器不支援自動更新，但支援服務位置記錄時**，您可以手動將管理點發佈到 DNS。 若要完成此動作，您必須手動在 DNS 中指定服務位置資源記錄 (SRV RR)。  

Configuration Manager 支援服務位置記錄的 RFC 2782。 這些記錄的格式如下：*_Service._Proto.Name TTL 類別 SRV 優先順序權重連接埠目標*  

若要將管理點發行到 Configuration Manager，請指定下列值：  

-   **_Service**：輸入 **_mssms_mp**_&lt;sitecode\>，其中 &lt;sitecode\> 是管理點的站台碼。  
-   **._Proto**：指定 **._tcp**。  
-   **.Name**：輸入管理點的 DNS 尾碼，例如 **contoso.com**。  
-   **TTL**：輸入 **14400**，表示四小時。  
-   **類別**：指定 **IN** (符合 RFC 1035 規範)。  
-   **優先順序**：Configuration Manager 不使用此欄位。
-   **權重**：Configuration Manager 不使用此欄位。  
-   **連接埠**：輸入管理點所使用的連接埠號碼，例如 HTTP 為 **80** ，而 HTTPS 為 **443** 。  

    > [!NOTE]  
    >  SRV 記錄連接埠應符合管理點所使用的通訊埠。 根據預設，HTTP 通訊為 **80**，HTTPS 通訊為 **443**。  

-   **目標**：輸入為使用管理點網站角色設定之網站系統所指定的內部網路 FQDN。  

如果您使用的是 Windows Server DNS，便可以使用下列程序，為內部網路管理點輸入此 DNS 記錄。 如果使用不同的 DNS 實作，請使用本節中有關欄位值的資訊，並參閱 DNS 文件以調整此程序。  

##### <a name="to-configure-automatic-publishing"></a>若要設定自動發佈功能：  

1.  在 Configuration Manager 主控台中，展開 [系統管理] > [站台設定] > [站台]。  

2.  選取您的網站，然後選擇 [設定網站元件]。  

3.  選擇 [管理點]。  

4.  選取您想要發佈的管理點。 (此選項亦適用於發佈至 AD DS 與 DNS。)  

5.  勾選方塊，以發佈至 DNS。 這個方塊︰  

    -   可讓您選取要發佈至 DNS 的管理點。  

    -   不會設定發佈至 AD DS。  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>在 Windows Server 上手動將管理點發佈到 DNS  

1.  在 Configuration Manager 主控台中，指定站台系統的內部網際網路 FQDN。  

2.  在 DNS 管理主控台中，選取管理點電腦的 DNS 區域。  

3.  確認其中有網站系統內部網路 FQDN 的主機記錄 (A 或 AAA)。 如果此記錄不存在，請建立此記錄。  

4.  使用 [新增其他記錄] 選項，選擇 [資源記錄類型] 對話方塊中的 [服務位置 (SRV)]，選擇 [建立記錄]，輸入下列資訊，然後選擇 [完成]：  

    -   **網域**：請視需要輸入管理點的 DNS 尾碼，例如 **contoso.com**。  
    -   **服務**：輸入 **_mssms_mp**_&lt;sitecode\>，其中 &lt;sitecode\> 是管理點的站台碼。  
    -   **通訊協定**：輸入 **_tcp**。  
    -   **優先順序**：Configuration Manager 不使用此欄位。  
    -   **權重**：Configuration Manager 不使用此欄位。  
    -   **連接埠**：輸入管理點所使用的連接埠號碼，例如 HTTP 為 **80** ，而 HTTPS 為 **443** 。  

        > [!NOTE]  
        >  SRV 記錄連接埠應符合管理點所使用的通訊埠。 根據預設，HTTP 通訊為 **80**，HTTPS 通訊為 **443**。  

    -   **提供這項服務的主機**：輸入為使用管理點網站角色設定之網站系統所指定的內部網路 FQDN。  

針對內部網路上要發佈到 DNS 的各管理點，重複執行這些步驟。  

##  <a name="bkmk_wins"></a> WINS  
當其他服務位置機制失敗時，用戶端可檢查 WINS 以尋找初始管理點。  

根據預設，主要網站會在網站上將針對 HTTP 和 HTTPS 設定的第一個管理點發佈到 WINS。  

如果您不想讓用戶端找到 WINS 中的 HTTP 管理點，請使用 CCMSetup.exe Client.msi 內容 **SMSDIRECTORYLOOKUP=NOWINS**來設定用戶端。  
