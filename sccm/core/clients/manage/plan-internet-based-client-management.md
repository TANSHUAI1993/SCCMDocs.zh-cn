---
title: "以網際網路為基礎的用戶端管理 | Microsoft Docs"
description: "在 System Center Configuration Manager 中建立方案以管理以網際網路為基礎的用戶端。"
ms.custom: na
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 90c30bfb22735f73422f1547301552bf42022bb9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-internet-based-client-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中以網際網路為基礎的用戶端管理規劃

*適用於：System Center Configuration Manager (最新分支)*

以網際網路為基礎的用戶端管理 (有時稱之為 IBCM) 可讓您在 System Center Configuration Manager 用戶端並未連線至您公司網路，但有標準網際網路連線時，管理這些用戶端。 這種安排有幾個優點，包括降低成本 (因為無須執行虛擬私人網路 (VPN))，且能以更即時的方式部署軟體更新。  

 因為在公用網路上管理用戶端電腦需要更高的安全性，以網際網路為基礎的用戶端管理就要求用戶端與用戶端連線的網站系統伺服器使用 PKI 憑證。 這可確保由獨立的單位驗證連線，且進出這些網站系統的資料都使用安全通訊端層 (SSL) 進行加密。  

 請利用以下各節來協助您規劃以網際網路為基礎的用戶端管理。  

##  <a name="features-that-are-not-supported-on-the-internet"></a>網際網路上「不」支援的功能  
 並非所有用戶端管理功能都可在網際網路上使用，因此，在網際網路上管理用戶端時，就不會支援某些功能。 網際網路管理不支援的功能，一般需依賴 Active Directory 網域服務，或不適合在公用網路上使用，例如網路探索和網路喚醒 (WOL)。  

 在網際網路上管理用戶端時，不支援以下功能：  

-   透過網際網路的用戶端部署，例如用戶端推入和以軟體更新為基礎的用戶端部署。 此時請改以手動方式進行用戶端安裝。  

-   自動網站指派。  

-   網路喚醒。  

-   作業系統部署。 不過，您可以部署並未部署作業系統的工作順序，例如在用戶端上執行指令碼與維護工作的工作順序。  

-   遠端控制。  

-   軟體部署至使用者，除非以網際網路為基礎的管理點可以使用 Windows 驗證 (Kerberos 或 NTLM) 來驗證 Active Directory 網域服務中的使用者。 當以網際網路為基礎的管理點信任使用者帳戶所在的樹系時，就可能出現這種狀況。  

 此外，以網際網路為基礎的管理不支援漫遊。 漫遊會讓用戶端總是找出最接近的發佈點來下載內容。 當網站系統設定為使用網際網路 FQDN，且網站系統角色允許來自網際網路的用戶端連線時，則在網際網路上受管理的用戶端會經由其指派的網站與網站系統進行通訊。 無論頻寬或實體位置為何，用戶端都會以不確定的方式選取其中一個以網際網路為基礎的網站系統。  

 當您擁有設定為接受來自網際網路的連線的軟體更新點時，Configuration Manager 在網際網路上以網際網路為基礎的用戶端一律皆會掃描此軟體更新點，藉以判斷所需的軟體更新。 不過，當這些用戶端位於網際網路上時，首先會嘗試從 Microsoft Update 下載軟體更新，而不是從以網際網路為基礎的發佈點下載。 只有在下載失敗後，才會嘗試從以網際網路為基礎的發佈點下載所需的軟體更新。 未針對以網際網路為基礎的用戶端管理設定的用戶端，永遠不會嘗試從 Microsoft Update 下載軟體更新，但會一直使用 Configuration Manager 發佈點。  

##  <a name="considerations-for-client-communications-from-the-internet-or-untrusted-forest"></a>從網際網路或未受信任之樹系的用戶端通訊考量  
 安裝在主要網站的下列網站系統角色支援來自不受信任位置 (例如網際網路或不受信任樹系) 的用戶端連線 (次要網站不支援來自不受信任位置的用戶端連線)：  

-   應用程式類別目錄網站點  

-   Configuration Manager 原則模組  

-   發佈點 (以雲端為基礎的發佈點需要 HTTPS)  

-   註冊 Proxy 點  

-   後援狀態點  

-   管理點  

-   軟體更新點  

 **關於網際網路對向的網站系統：**   
雖然用戶端的樹系與站台系統伺服器之間不需要具有信任關係，但當包含網際網路對向站台系統的樹系信任包含使用者帳戶的樹系時，此設定仍支援針對網際網路上的裝置使用以使用者為基礎的原則 (在啟用 [用戶端原則] 用戶端設定之 [從網際網路用戶端啟用使用者原則要求] 的情況下)。  

 例如，以下設定會說明何時以網際網路為基礎的用戶端管理會針對網際網路上的裝置，支援使用者原則。  

-   以網際網路為基礎的管理點位於唯讀網域控制站所在的中介網路，以驗證使用者，且中介防火牆允許 Active Directory 封包。  

-   使用者帳戶位於樹系 A (內部網路)，以網際網路為基礎的管理點則位於樹系 B (中介網路)。 樹系 B 信任樹系 A，且中介防火牆允許驗證封包。  

-   使用者帳戶與以網際網路為基礎的管理點位於樹系 A (內部網路)。 使用 Web Proxy 伺服器 (例如 Forefront Threat Management Gateway)，將管理點發佈至網際網路。  

> [!NOTE]  
>  若 Kerberos 驗證失敗，就會自動嘗試 NTLM 驗證。  

 如前一個範例所顯示的，當使用 Web Proxy 伺服器 (如 ISA 伺服器與 Forefront Treat Management Gateway) 將以網際網路為基礎的網站系統發佈到網際網路上時，您可以將這些網站置於內部網路內。 這些網站系統只能針對來自網際網路的用戶端連線，或來自網際網路與內部網路的用戶端連線，進行設定， 使用 Web Proxy 伺服器時，您可以設定其讓安全通訊端層 (SSL) 橋接至 SSL (較安全) 或 SSL 通道：  

-   **SSL 橋接至 SSL：**   
    針對以網際網路為基礎的用戶端管理使用 Proxy 網頁伺服器時的建議設定是 SSL 橋接至 SSL，這會透過驗證以啟用 SSL 終止。 必須使用電腦驗證來驗證用戶端電腦，並使用使用者驗證來驗證行動裝置舊版用戶端。 由 Configuration Manager 註冊的行動裝置並不支援 SSL 橋接。  

     在 Proxy 網頁伺服器進行 SSL 終止的優點是將來自網際網路的封包轉寄到內部網路前，都必須經過檢查。 Proxy 網頁伺服器會驗證來自用戶端的連線，將其終止，然後開啟一個連線到以網際網路為基礎之網站系統的全新已驗證連線。 Configuration Manager 用戶端使用 Proxy 網頁伺服器時，用戶端識別 (用戶端 GUID) 會安全地保存在封包裝載中，管理點就不用考慮讓 Proxy 網頁伺服器成為用戶端。 使用 HTTP 至 HTTPS 或從 HTTPS 至 HTTP 的 Configuration Manager 不支援橋接。  

-   **通道**：   
    若您的 Proxy 網頁伺服器無法支援 SSL 橋接的需求，或您想設定網際網路支援由 Configuration Manager 註冊的行動裝置，則也支援 SSL 通道。 這是比較危險的選項，因為來自網際網路的 SSL 封包會轉寄到沒有 SSL 終止的網站系統，因此無法檢查封包內是否存在惡意內容。 使用 SSL 通道時，Proxy 網頁伺服器不需要憑證。  

##  <a name="planning-for-internet-based-clients"></a>規劃以網際網路為基礎的用戶端  
 您必須判斷在網際網路上受管理的用戶端電腦是否要針對在內部網路與網際網路上受管理來進行設定，或是設定僅在網際網路內接受用戶端管理。 在安裝用戶端電腦時，您只能設定用戶端管理選項。 若您稍後改變心意，就必須重新安裝用戶端。  

> [!NOTE]  
>  如果您設定具有網際網路連線功能的管理點，連線至該管理點的用戶端，會在下一次重新整理它們的可用管理點清單時，成為具有網際網路連線功能。  

> [!TIP]  
>  您不需要限制設定僅在網際網路中進行的用戶端管理，您也可以將其用在內部網路上。  

 設定僅在網際網路上接受用戶端管理的用戶端，只會和針對來自網際網路之用戶端連線設定的網站系統進行通訊。 這個設定適合您已知從未連線至公司內部網路的電腦，例如在遠端位置的銷售點電腦。 當您要限制用戶端僅經由 HTTPS 進行通訊 (例如支援防火牆與受限制的安全性原則) 時，以及當您在中介網路上安裝以網際網路為基礎的網站系統，且要使用 Configuration Manager 用戶端管理這些伺服器時，也適合這個設定。  

 您要管理網際網路上的工作群組用戶端時，必須將這些用戶端安裝為僅在網際網路上進行通訊。  

> [!NOTE]  
>  當行動裝置用戶端設定為使用以網際網路為基礎的管理點時，會將行動裝置用戶端自動設定為僅在網際網路上進行通訊。  

 其他用戶端電腦則可以設定為接受網際網路與內部網路用戶端管理。 當它偵測到網路變更時，它們可以自動在以網際網路為基礎的用戶端管理與內部網路用戶端管理間進行切換。 若這些用戶端可以找到並連線至設定為在內部網路進行用戶端連線的管理點，就會將這些用戶端視為具備完整 Configuration Manager 管理功能的內部網路用戶端來進行管理。 若用戶端找不到或無法連線至設定為在內部網路進行用戶端連線的管理點，它們會嘗試連線到以網際網路為基礎的管理點，若成功，接著就會由這些用戶端之指定網站內以網際網路為基礎的網站系統來管理這些用戶端。  

 在以網際網路為基礎的用戶端管理，以及內部網路用戶端管理間進行自動切換的優點是：只要用戶端電腦連線至內部網路，且只要它們在網際網路上，就能繼續以基礎管理功能管理時，這些用戶端電腦就可以自動使用所有 Configuration Manager 功能。 此外，在網際網路上開始的下載可以在內部網路上順利恢復，反之亦然。  

##  <a name="prerequisites-for-internet-based-client-management"></a>以網際網路為基礎之用戶端管理的必要條件  
 Configuration Manager 中以網際網路為基礎的用戶端管理有以下外部相依性：  

-   將在網際網路上進行管理的用戶端必須具備網際網路連線。  

     Configuration Manager 使用現有網際網路服務提供者 (ISP) 連線來連線到網際網路，這可以是永久或暫時的連線。 用戶端行動裝置必須具備直接網際網路連線，但用戶端電腦可以具備直接網際網路連線，或使用 Proxy 網頁伺服器來連線。  

-   支援以網際網路為基礎之用戶端管理的網站系統必須具備連線至網際網路的能力，且必須位於 Active Directory 網域。  

     以網際網路為基礎的網站系統不需要和網站伺服器的 Active Directory 樹系間建立信任關係。 不過，在以網際網路為基礎的管理點可以使用 Windows 驗證來驗證使用者時，就支援使用者原則。 若 Windows 驗證失敗，則僅支援電腦原則。  

    > [!NOTE]  
    >  若要支援使用者原則，您也必須將兩個 [用戶端原則]  用戶端設定設定為 [True]  。  
    >   
    >  -   **啟用用戶端的使用者原則輪詢**  
    > -   **[從網際網路用戶端啟用使用者原則要求]**  

     以網際網路為基礎的應用程式類別目錄網站點也要求以 Windows 驗證來驗證使用者 (它們的電腦位於網際網路上時)。 這項要求獨立於使用者原則。  

-   您必須具備支援的公開金鑰基礎結構 (PKI) 以部署及管理用戶端要求的憑證，以及在網際網路和以網際網路為基礎的網站系統伺服器上進行管理的憑證。  

     如需 PKI 憑證的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

-   網站系統 (支援以網際網路為基礎的用戶端管理) 的網際網路完整網域名稱 (FQDN) 必須在公開 DNS 伺服器上登錄為主機項目。  

-   居中的防火牆或 Proxy 伺服器必須允許與以網際網路為基礎之站台系統相關聯的用戶端通訊。  

     用戶端通訊要求：  

    -   支援 HTTP 1.1  

    -   允許多部分 MIME 附件的 HTTP 內容類型 (多部分/混合和應用程式/octet-stream)。  

    -   針對以網際網路為基礎的管理點，允許以下動詞：  

        -   HEAD  

        -   CCM_POST  

        -   BITS_POST  

        -   GET  

        -   PROPFIND  

    -   針對以網際網路為基礎的發佈點，允許以下動詞：  

        -   HEAD  

        -   GET  

        -   PROPFIND  

    -   針對以網際網路為基礎的後援狀態點，允許以下動詞：  

        -   POST  

    -   針對以網際網路為基礎的應用程式類別目錄網站點，允許以下動詞：  

        -   POST  

        -   GET  

    -   針對以網際網路為基礎的管理點，允許以下 HTTP 標頭：  

        -   Range:  

        -   CCMClientID:  

        -   CCMClientIDSignature:  

        -   CCMClientTimestamp:  

        -   CCMClientTimestampsSignature:  

    -   針對以網際網路為基礎的發佈點，允許以下 HTTP 標頭：  

        -   Range:  

     如需支援這些要求的設定資訊，請參閱您的防火牆或 Proxy 伺服器說明文件。  

     如需您針對來自網際網路之用戶端連線使用軟體更新點時類似的通訊要求，請參閱 Windows Server Update Services (WSUS) 的說明文件。 例如，針對 Windows Server 2003 上的 WSUS，請參閱 [Appendix D: Security Settings (附錄 D：安全性設定)](http://go.microsoft.com/fwlink/p/?LinkId=143368)，安全性設定的部署附錄。
