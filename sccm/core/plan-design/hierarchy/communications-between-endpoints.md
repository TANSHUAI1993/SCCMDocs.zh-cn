---
title: "端點之間的通訊 | Microsoft Docs"
description: "了解 System Center Configuration Manager 站台系統與元件如何透過網路通訊。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: cd94f9ccc7e196b30e5dc7ae9368d073b7cff5d2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="communications-between-endpoints-in-system-center-configuration-manager"></a>System Center Configuration Manager 中端點之間的通訊

適用於：System Center Configuration Manager (最新分支)


##  <a name="Planning_Intra-site_Com"></a> 站台內站台系統之間的通訊  
 當 Configuration Manager 站台系統或元件透過網路與其他站台系統或站台中的 Configuration Manager 元件通訊時，會根據站台設定方式來使用下列其中一項通訊協定：  

-   伺服器訊息區 (SMB)  

-   HTTP  

-   HTTPS  

除了從站台伺服器到發佈點的通訊以外，站台中伺服器對伺服器的通訊可能會在任何時間發生，並且不會使用任何機制控制網路頻寬。 由於您無法控制站台系統之間的通訊，請確保將站台系統伺服器安裝在快速且網路連線良好的位置。  

協助您管理從站台伺服器到發佈點的內容傳送：  

-   設定網路頻寬控制與排程的發佈點。 這些控制項與站台間位址所使用的設定相似，當傳送內容至遠端網路位置是您主要的頻寬考量時，通常可使用此設定，而不需安裝另一個 Configuration Manager 站台。  

-   您可以將發佈點安裝為預先設置的發佈點。 預先設置的發佈點可讓您使用以手動方式放置於發佈點伺服器的內容，並可免除透過網路傳送內容檔案的需求。  

如需詳細資訊，請參閱[管理內容管理的網路頻寬](manage-network-bandwidth.md)。


##  <a name="Planning_Client_to_Site_System"></a> 從用戶端到站台系統和服務的通訊  
用戶端會起始與站台系統角色、Active Directory 網域服務及線上服務的通訊。 若要啟用這些通訊，防火牆必須允許用戶端和其通訊端點之間的網路流量。 端點包括：  

-   **應用程式類別目錄網站點**：支援 HTTP 和 HTTPS 通訊

-   **雲端資源**：包括 Microsoft Azure 和 Microsoft Intune  

-   **Configuration Manager 原則模組 (NDES)**：支援 HTTP 和 HTTPS 通訊

-   **發佈點**：支援 HTTP 和 HTTPS 通訊，而雲端發佈點需要 HTTPS  

-   **後援狀態點**：支援 HTTP 通訊  

-   **管理點**：支援 HTTP 和 HTTPS 通訊  

-   **Microsoft Update**  

-   **軟體更新點**：支援 HTTP 和 HTTPS 通訊  

-   **狀態移轉點**：支援 HTTP 和 HTTPS 通訊  

-   **各種網域服務**  

用戶端必須先使用服務位置找到支援用戶端通訊協定 (HTTP 或 HTTPS) 的站台系統角色，才能與站台系統角色通訊。 根據預設，用戶端會使用最安全的可用方法：  

-   若要使用 HTTPS，您必須具有公開金鑰基礎結構 (PKI)，並且必須在用戶端與伺服器上安裝 PKI 憑證。 如需如何使用憑證的資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

-   在部署使用網際網路資訊服務 (IIS) 並支援從用戶端進行通訊的網站系統角色時，您必須指定用戶端要使用 HTTP 或 HTTPS 連線至網站系統。 如果您使用 HTTP，您也必須考慮簽署和加密選擇。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃安全性](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption)中的[規劃簽署與加密](../../../core/plan-design/security/plan-for-security.md)。  

如需用戶端服務位置的資訊，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

如需用戶端與這些端點進行通訊時所用的連接埠和通訊協定的詳細資訊，請參閱 [System Center Configuration Manager 中使用的連接埠](../../../core/plan-design/hierarchy/ports.md)。  

###  <a name="BKMK_clientspan"></a> 從網際網路或未受信任之樹系的用戶端通訊考量  
安裝在主要站台的下列站台系統角色支援來自不受信任位置 (例如網際網路或不受信任樹系) 的用戶端連線。 (次要站台不支援來自不受信任位置的用戶端連線)  

-   應用程式類別目錄網站點  

-   Configuration Manager 原則模組  

-   發佈點 (以雲端為基礎的發佈點需要 HTTPS)  

-   註冊 Proxy 點  

-   後援狀態點  

-   管理點  

-   軟體更新點  

**關於網際網路對向的站台系統：**   
用戶端樹系與站台系統伺服器之間不需要有信任。 不過，當包含網際網路對向站台系統的樹系信任包含使用者帳戶的樹系時，此設定仍支援針對網際網路上的裝置使用以使用者為基礎的原則 (在啟用 [用戶端原則] 用戶端設定之 [從網際網路用戶端啟用使用者原則要求] 的情況下)。  

例如，以下設定會說明何時以網際網路為基礎的用戶端管理會針對網際網路上的裝置，支援使用者原則。  

-   以網際網路為基礎的管理點位於唯讀網域控制站所在的中介網路，以驗證使用者，且中介防火牆允許 Active Directory 封包。  

-   使用者帳戶位於樹系 A (內部網路)，以網際網路為基礎的管理點則位於樹系 B (中介網路)。 樹系 B 信任樹系 A，且中介防火牆允許驗證封包。  

-   使用者帳戶與以網際網路為基礎的管理點位於樹系 A (內部網路)。 使用 Web Proxy 伺服器 (例如 Forefront Threat Management Gateway)，將管理點發佈至網際網路。  

> [!NOTE]  
>  若 Kerberos 驗證失敗，就會自動嘗試 NTLM 驗證。  

如前一個範例所顯示的，當使用 Web Proxy 伺服器 (如 ISA 伺服器與 Forefront Treat Management Gateway) 將以網際網路為基礎的網站系統發佈到網際網路上時，您可以將這些網站置於內部網路內。 這些站台系統只能針對來自網際網路的用戶端連線，或來自網際網路與內部網路的用戶端連線，進行設定。 使用 Web Proxy 伺服器時，您可以設定其讓安全通訊端層 (SSL) 橋接至 SSL (較安全) 或 SSL 通道，如下所示：  

-   **SSL 橋接至 SSL：**   
    針對以網際網路為基礎的用戶端管理使用 Proxy 網頁伺服器時的建議設定是 SSL 橋接至 SSL，這會透過驗證以啟用 SSL 終止。 必須使用電腦驗證來驗證用戶端電腦，並使用使用者驗證來驗證行動裝置舊版用戶端。 由 Configuration Manager 註冊的行動裝置並不支援 SSL 橋接。  

     在 Proxy 網頁伺服器進行 SSL 終止的優點是將來自網際網路的封包轉寄到內部網路前，都必須經過檢查。 Proxy 網頁伺服器會驗證來自用戶端的連線，將其終止，然後開啟一個連線到以網際網路為基礎之網站系統的全新已驗證連線。 Configuration Manager 用戶端使用 Proxy 網頁伺服器時，用戶端識別 (用戶端 GUID) 會安全地保存在封包裝載中，管理點就不用考慮讓 Proxy 網頁伺服器成為用戶端。 使用 HTTP 至 HTTPS 或從 HTTPS 至 HTTP 的 Configuration Manager 不支援橋接。  

-   **通道**：   
    若您的 Proxy 網頁伺服器無法支援 SSL 橋接的需求，或您想設定網際網路支援由 Configuration Manager 註冊的行動裝置，則也支援 SSL 通道。 這是比較危險的選項，因為來自網際網路的 SSL 封包會轉寄到沒有 SSL 終止的網站系統，因此無法檢查封包內是否存在惡意內容。 使用 SSL 通道時，Proxy 網頁伺服器不需要憑證。  

##  <a name="Plan_Com_X-Forest"></a> 跨 Active Directory 樹系的通訊  
System Center Configuration Manager 支援跨 Active Directory 樹系的站台與階層。  

Configuration Manager 也支援不在相同 Active Directory 樹系作為站台伺服器的網域電腦，以及工作群組內的電腦：  

-   **若要支援樹系中站台伺服器樹系不信任的網域電腦**，您可以：  

    -   在該不受信任的樹系中安裝站台系統角色，並可選擇是否將站台資訊發佈至 Active Directory 樹系  

    -   管理這些電腦，如同它們是工作群組電腦一樣。  

  在不受信任的 Active Directory 樹系中安裝站台系統伺服器時，會將樹系中來自用戶端的用戶端到伺服器通訊保留在該樹系內，而且 Configuration Manager 可以使用 Kerberos 驗證電腦。 將站台資訊發佈至用戶端樹系時，用戶端可以從其 Active Directory 樹系擷取網站資訊 (如可用管理點清單)，而不用從其指派的管理點下載此資訊。  

  > [!NOTE]  
  >  若想管理網際網路上的裝置，您可以在網站系統伺服器位於 Active Directory 樹系時，在您的周邊網路中安裝網際網路型網站系統角色。 此狀況並不需要在周邊網路與站台伺服器的樹系間建立雙向信任。  

-   **若要支援工作群組中的電腦**，您必須：  

    -   在工作群組電腦使用 HTTP 用戶端連線到站台系統角色時，手動核准工作群組電腦。 原因是 Configuration Manager 無法使用 Kerberos 來驗證這些電腦。  

    -   請設定工作群組用戶端使用網路存取帳戶，這些電腦才能從發佈點擷取內容。  

    -   提供工作群組用戶端尋找管理點的替代機制。 您可以使用 DNS 發佈、WINS，或直接指派管理點。 原因是這些用戶端無法從 Active Directory 網域服務擷取站台資訊。  

    這個內容庫中的相關資源：  

    -   [管理 Configuration Manager 用戶端的衝突記錄](../../../core/clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

    -   [網路存取帳戶](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

    -   [如何在工作群組電腦上安裝 Configuration Manager 用戶端](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

###  <a name="bkmk_span"></a> 可支援跨多個網域和樹系之站台或階層的案例  

#### <a name="communication-between-sites-in-a-hierarchy-that-spans-forests"></a>跨樹系階層中網站間的通訊  
此案例需要支援 Kerberos 驗證的雙向樹系信任。  如果您沒有支援 Kerberos 驗證的雙向樹系信任，Configuration Manager 就不支援遠端樹系中的子站台。  

 **Configuration Manager 支援在遠端樹系中 (需要父站台樹系內的雙向信任) 安裝子站台**  

-   例如，只要存在所需的信任，您可以在與主要父站台不同的樹系中放置次要站台。  

> [!NOTE]  
>  子站台可以是主要站台 (其中管理中心網站是父站台) 或次要站台。  

Configuration Manager 中的站台間通訊使用資料庫複寫和以檔案為基礎的傳輸。 安裝站台時，必須指定帳戶，以便在指定伺服器上安裝站台。 此帳戶也會建立與維護網站間的通訊。  

網站成功安裝並起始以檔案為基礎的傳輸與資料庫複寫後，就不需要為了與網站通訊設定其他項目。  

**存在雙向樹系信任時，Configuration Manager 就不需要任何其他設定步驟。**  

根據預設，安裝新站台作為另一個站台的子站台時，Configuration Manager 會設定以下項目：  

-   每個站台以檔案為基礎的站台間複寫路由 (其使用站台伺服器電腦帳戶)。 Configuration Manager 會將每部電腦的電腦帳戶加入目的地電腦的 **SMS_SiteToSiteConnection_&lt;站台碼\>** 群組中。  

-   每個網站上 SQL Server 間的資料庫複寫。  

也必須設定以下設定：  

-   中介防火牆和網路裝置必須允許 Configuration Manager 要求的網路封包。  

-   樹系間的名稱解析必須能夠運作。  

-   若要安裝網站或網站系統角色，您必須指定一個在指定電腦上具備本機系統管理權限的帳戶。  

#### <a name="communication-in-a-site-that-spans-forests"></a>跨樹系站台中的通訊  
此案例不需要雙向樹系信任。  

**主要站台支援將站台系統角色安裝到遠端樹系的電腦上**。  

-   應用程式類別目錄 Web 服務點是唯一的例外。  只有與站台伺服器相同的樹系中才予以支援。  

-   網站系統角色接受來自網際網路的連線時，做為安全性最佳作法，請將這些網站系統角色安裝在樹系界限會為網站伺服器提供保護的位置 (例如周邊網路中)。  

**在不受信任之樹系中的電腦上安裝站台系統角色：**  

-   您必須指定**站台系統安裝帳戶**，以用來安裝站台系統角色。 (帳戶必須具有本機系統管理認證才能連接。)然後在指定電腦上安裝站台系統角色。  

-   您必須選取 [要求網站伺服器起始與此網站系統的連線] 網站系統選項。 若要這麼做，網站伺服器必須建立和網站系統伺服器間的連線，以傳輸資料。 這可防止位於不受信任位置的電腦起始與受信任網路內之站台伺服器的聯繫。 這些連線會使用 **網站系統安裝帳戶**。  

**若要使用安裝在不受信任之樹系中的站台系統角色，** 防火牆必須允許網路流量，即使站台伺服器會起始資料傳輸亦同。  

此外，下列網站系統角色需要直接存取網站資料庫。 因此，防火牆必須允許來自不受信任的樹系到站台 SQL Server 的適用流量：  

-   Asset Intelligence 同步處理點  

-   Endpoint Protection 點  

-   註冊點  

-   管理點  

-   Reporting Service 點  

-   狀態移轉點  

如需詳細資訊，請參閱 [System Center Configuration Manager 中使用的連接埠](../../../core/plan-design/hierarchy/ports.md)。  

**您可能需要設定站台系統角色對站台資料庫的存取權：**  

管理點和註冊點站台系統角色都會連線到站台資料庫。  

-   根據預設，安裝這些站台系統角色時，Configuration Manager 會設定新站台系統伺服器的電腦帳戶作為站台系統角色的連線帳戶，並將該帳戶新增到適當的 SQL Server 資料庫角色。  

-   在不受信任的網域中安裝這些網站系統角色時，您必須設定網站系統角色連線帳戶啟用網站系統角色，以便從資料庫取得資訊。  

如果您將網域使用者帳戶設定為這些站台系統角色的連線帳戶，請確定網域使用者帳戶能正確存取該站台上的 SQL Server 資料庫：  

-   管理點： **管理點資料庫連線帳戶**  

-   註冊點： **註冊點連線帳戶**  

在您規劃其他樹系中的網站系統角色時，請考量以下其他資訊：  

-   如果您執行 Windows 防火牆，請設定適用的防火牆設定檔，以便在站台資料庫伺服器和安裝有遠端站台系統角色的電腦間傳遞通訊。 如需防火牆設定檔的資訊，請參閱[了解防火牆設定檔](http://go.microsoft.com/fwlink/p/?LinkId=233629)。  

-   以網際網路為基礎的管理點信任包含使用者帳戶的樹系時，就支援使用者原則。 不存在信任時，就僅支援電腦原則。  

#### <a name="communication-between-clients-and-site-system-roles-when-the-clients-are-not-in-the-same-active-directory-forest-as-their-site-server"></a>用戶端並未與站台伺服器處於相同 Active Directory 樹系時，用戶端與站台系統角色間的通訊  
當用戶端與其站台的站台伺服器不在相同的樹系中時，Configuration Manager 支援以下情況：  

-   在用戶端樹系與站台伺服器樹系間存在雙向樹系信任。  

-   站台系統角色伺服器位於與用戶端相同的樹系中。  

-   用戶端位於網域電腦上，該電腦和站台伺服器間不存在雙向樹系信任，而在用戶端樹系中未安裝站台系統角色。  

-   用戶端位於工作群組電腦上。  

加入網域之電腦上用戶端的站台發佈到其 Active Directory 樹系時，這些用戶端就可以使用服務位置的 Active Directory 網域服務。  

若要將站台資訊發佈至另一個 Active Directory 樹系，您必須：  

-   指定樹系，然後在 [系統管理]  工作區的 [Active Directory 樹系]  節點中啟用發佈至該樹系。  

-   設定每個站台將其資料發佈至 Active Directory 網域服務。 此設定可啟用該樹系中的用戶端，以擷取網站資訊和找出管理點。 針對無法使用服務位置之 Active Directory 網域服務的用戶端，您可以使用 DNS、WINS，或用戶端指派的管理點。  

###  <a name="bkmk_xchange"></a> 將 Exchange Server 連接器放在遠端樹系中  
若要支援此案例，請確認名稱解析可在樹系之間運作 (例如設定 DNS 轉寄)，並在您設定 Exchange Server 連接器時指定 Exchange Server 的內部網路 FQDN。 如需詳細資訊，請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  
