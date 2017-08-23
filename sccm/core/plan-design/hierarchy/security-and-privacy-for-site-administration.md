---
title: "站台管理安全性和隱私權 | Microsoft Docs"
description: "最佳化 System Center Configuration Manager 中網站管理的安全性和隱私權。"
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a60b8c103a303dcae0bd66f3060d5a8f17d1cef9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-site-administration-in-system-center-configuration-manager"></a>System Center Configuration Manager 中網站管理的安全性和隱私權

*適用於︰System Center Configuration Manager (最新分支)*

本主題包含 System Center Configuration Manager 站台及階層的安全性與隱私權資訊。

##  <a name="BKMK_Security_Sites"></a> 站台管理的安全性最佳做法  
 使用下列安全性最佳作法，協助您保護 System Center Configuration Manager 站台和階層。  

 **只從受信任來源執行安裝程式，並保護安裝程式媒體與站台伺服器之間的通訊通道。**  

 若要協助防止有人竄改來源檔案，請從受信任來源執行安裝程式。 如果在網路上儲存檔案，請保護網路位置。  

 如果是從網路位置執行安裝程式，若要防止攻擊者竄改透過網路傳送的檔案，可在安裝程式檔案的來源位置與站台伺服器之間使用 IPsec 或伺服器訊息區 (SMB) 簽署。  

 此外，若您使用安裝程式下載程式下載安裝程式所需的檔案，請確定儲存這些檔案的位置也有受到保護，並在執行安裝程式時保護此位置的通訊通道。  

 **延伸 System Center Configuration Manager 的 Active Directory 架構，並將站台發佈到 Active Directory 網域服務。**  

 執行 System Center Configuration Manager 時不需要進行架構延伸，但它們可以建立更安全的環境，因為 Configuration Manager 用戶端和站台伺服器可以從受信任來源擷取資訊。  

 如果用戶端位於不受信任的網域，請在用戶端的網域部署下列站台系統角色：  

-   管理點  

-   發佈點  

-   應用程式類別目錄網站點  

> [!NOTE]  
>  Configuration Manager 的受信任網域需要進行 Kerberos 驗證。 這表示，如果用戶端位於另一個樹系，且該樹系與站台伺服器的樹系間未採用雙向樹系信任，這些用戶端將被視為位於不受信任的網域。 外部信任無法滿足此用途。  

 **使用 IPsec 在站台系統伺服器及站台間進行安全通訊。**  

 雖然 Configuration Manager 可以在站台伺服器與執行 SQL Server 的電腦之間進行安全通訊，但 Configuration Manager 無法在站台系統角色與 SQL Server 之間進行安全通訊。 只有某些站台系統 (註冊點和應用程式類別目錄 Web 服務點) 可以針對 HTTPS 進行站台內通訊的設定。  

 如果您沒有使用其他控制項來保護這些伺服器對伺服器的通道，攻擊者便可以針對站台系統進行各種詐騙和攔截式攻擊。 當您無法使用 IPsec 時可使用 SMB 簽署。  

> [!NOTE]  
>  這對於保護站台伺服器與封裝來源伺服器之間的通訊通道特別重要。 這類通訊都會使用 SMB。 如果您無法使用 IPsec 保護此通訊，請使用 SMB 簽署來確定檔案在用戶端下載及執行之前並未遭到竄改。  

 **請勿變更 Configuration Manager 針對站台系統通訊所建立及管理的安全性群組。**  

 安全性群組：  

-   **SMS_SiteSystemToSiteServerConnection_MP_&lt;站台碼\>**  

-   **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;站台碼\>**  

-   **SMS_SiteSystemToSiteServerConnection_Stat_&lt;站台碼\>**  

Configuration Manager 會自動建立及管理這些安全性群組。 這包括在移除站台系統角色時移除電腦帳戶。  

為了要確保服務持續性及最低權限，請勿手動編輯這些群組。  

**如果用戶端無法查詢通用類別目錄伺服器以取得 Configuration Manager 資訊，請管理受信任根金鑰佈建程序。**  

如果用戶端無法查詢通用類別目錄以取得 Configuration Manager 資訊，這些用戶端必須仰賴受信任根金鑰來驗證有效的管理點。 受信任根金鑰會儲存在用戶端登錄中，並可使用群組原則或手動設定進行設定。  

如果用戶端未在第一次與管理點連絡時提供受信任根金鑰的複本，該用戶端會信任第一個與其通訊的管理點。 若要降低攻擊者將用戶端誤導至未經授權管理點的風險，您可以使用受信任的根金鑰預先佈建用戶端。 如需詳細資訊，請參閱[規劃受信任的根金鑰](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

**使用非預設的連接埠號碼。**  

因為非預設連接埠號碼可讓攻擊者較難在準備攻擊時探索環境，所以使用非預設連接埠號碼可以提供額外的安全性。 如果您決定使用非預設的連接埠，請在安裝 Configuration Manager 前先進行規劃，然後在階層的所有站台一致地使用。 用戶端要求連接埠和網路喚醒，都是您可以使用非預設連接埠的範例。  

**在站台系統上使用角色隔離。**  

雖然您可以在單一電腦上安裝所有站台系統角色，但此作法很少用在實際執行的網路，因為如此做會建立單一失敗點。  

**減少受攻擊面。**  

在不同伺服器上隔離各個站台系統角色，可減少針對一個站台系統漏洞進行攻擊，並轉用於攻擊不同站台系統的機會。 許多站台系統角色需要在站台系統上安裝 Internet Information Services (IIS)，如此做會增加受攻擊面。 如果您必須合併站台系統角色以減少硬體支出，請只合併 IIS 站台系統角色與其他站台需要 IIS 的系統角色。  

> [!IMPORTANT]  
>  後援狀態點角色是一項例外。 由於此站台系統角色接受來自用戶端的未經驗證資料，因此建議您永遠不要將後援狀態點角色指派給任何其他 Configuration Manager 站台系統角色。  


**依照 Windows Server 的安全性最佳作法，並在所有站台系統上執行安全性設定精靈。**  

安全性設定精靈 (SCW) 可協助您建立可套用在網路上任何伺服器的安全性原則。 安裝 System Center Configuration Manager 範本之後，SCW 就會辨識 Configuration Manager 站台系統角色、服務、連接埠和應用程式。 接著，它會准許 Configuration Manager 所需的通訊，並封鎖不需要的通訊。  

[資訊安全設定精靈] 隨附於 System Center 2012 Configuration Manager 的工具組，您可以從 Microsoft 下載中心下載此工具組：[System Center 2012 - Configuration Manager Component Add-ons and Extensions](http://go.microsoft.com/fwlink/p/?LinkId=251931) (System Center 2012 - Configuration Manager 元件的附加元件和延伸模組)。  

**為站台系統設定靜態 IP 位址。**  

靜態 IP 位址較容易保護名稱解析攻擊。  

靜態 IP 位址也會使 IPsec 的設定較為簡單。 使用 IPsec 是在 Configuration Manager 的站台系統間進行安全通訊的安全性最佳做法。  

**請勿在站台系統伺服器上安裝其他應用程式。**  

當您在站台系統伺服器上安裝其他應用程式時，您會增加 Configuration Manager 的攻擊面及不相容問題的風險。  

**設定要求簽署及啟用加密為站台選項。**  

為站台啟用簽署和加密選項。 確定所有用戶端皆可以支援 SHA-256 雜湊演算法，然後啟用 [需要 SHA-256] 選項。  

**限制和監視 Configuration Manager 系統管理使用者，以及使用以角色為基礎的系統管理，授與這些使用者所需的最小權限。**  

只對信任的使用者授與系統管理存取 Configuration Manager 權限，然後使用內建的安全性角色或自訂安全性角色，授與他們最小的權限。 可以建立、修改和部署應用程式、工作順序、軟體更新、設定項目和設定基準的系統管理使用者，也許可以控制 Configuration Manager 階層中的裝置。  

定期稽核系統管理使用者指派及其授權層級，以確認所需的變更。  

如需有關設定以角色為基礎之系統管理的詳細資訊，請參閱 [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md)。  

**當您在備份及還原時，請保護 Configuration Manager 備份和通訊通道。**  

當您備份 Configuration Manager 時，此資訊會包含憑證和其他可由攻擊者用於模擬的機密資料。  

當您透過網路傳送此資料以及保護備份位置時，請使用 SMB 簽署或 IPsec。  

**無論您是要從 Configuration Manager 主控台匯出或匯入物件至網路位置，請保護該位置和網路通道。**  

限制誰可以存取網路資料夾。  

在網路位置與站台伺服器之間，以及執行 Configuration Manager 主控台的電腦與站台伺服器之間，使用 SMB 簽署或 IPsec，以防止攻擊者竄改匯出的資料。 在網路上使用 IPsec 為資料加密，以防止洩露資訊。  

**如果站台系統未適當地進行解除安裝或停止運作，並且無法還原，請手動從其他 Configuration Manager 伺服器移除此伺服器的 Configuration Manager 憑證。**  

若要移除原本使用站台系統和站台系統角色所建立的 PeerTrust，請手動在其他站台系統伺服器的**受信任的人**憑證存放區中，移除失敗伺服器的 Configuration Manager 憑證。 如果您重新調整伺服器而未對其進行重新格式化，這是非常重要的程序。  

如需這些憑證的詳細資訊，請參閱 [System Center Configuration Manager 的密碼編譯控制項技術參考](../../../protect/deploy-use/cryptographic-controls-technical-reference.md)中的＜伺服器通訊的密碼編譯控制項＞一節。  

**請勿將以網際網路為基礎的站台系統，設定為橋接周邊網路及內部網路。**  

請勿將站台系統伺服器設定為多重主目錄，使其與周邊網路及內部網路連線。 雖然此設定可讓以網際網路為基礎的站台系統接受來自網際網路和內部網路的用戶端連線，但它也消除了周邊網路及內部網路的安全性界限。  

**如果站台系統伺服器位於不受信任網路 (例如周邊網路)，請將站台伺服器設定為起始與站台系統的連線。**  

根據預設，站台系統會起始與站台伺服器的連線以傳送資料，如此做可能會在從不受信任的網路起始與受信任網路的連線時，造成安全性風險。 當站台系統接受來自網際網路或不受信任樹系的連線時，請設定 [要求站台伺服器起始與此站台系統的連線]  站台系統選項，以便在安裝站台系統及任何站台系統角色後，從受信任網路起始所有連線。  

**如果您使用 Web Proxy 伺服器進行以網際網路為基礎的用戶端管理，請透過終止與驗證，以使用 SSL 橋接至 SSL。**  

 當您在 Proxy Web 伺服器上設定 SSL 終止時，來自網際網路的封包會先接受檢查，再轉送到內部網路。 Proxy 網頁伺服器會驗證來自用戶端的連線，將其終止，然後開啟一個連線到以網際網路為基礎之網站系統的全新已驗證連線。  

 當 Configuration Manager 用戶端電腦使用 Proxy Web 伺服器連線到以網際網路為基礎的站台系統時，用戶端識別 (用戶端 GUID)會安全地包含在封包裝載內，使管理點不會將 Proxy Web 伺服器視為用戶端。 如果您的 Proxy Web 伺服器無法支援 SSL 橋接的需求，則也會支援 SSL 通道。 這是較不安全的選項，因為它會將來自網際網路的 SSL 封包轉送到站台系統，而不會終止該封包，因此無法檢查其中是否包含惡意內容。  

 如果您的 Proxy Web 伺服器無法支援 SSL 橋接的需求，則可使用 SSL 通道。 不過，這是較不安全的選項，因為它會將來自網際網路的 SSL 封包轉送到站台系統，而不會終止該封包，因此無法檢查其中是否包含惡意內容。  

> [!WARNING]  
>  由 Configuration Manager 註冊的行動裝置無法使用 SSL 橋接，且必須只使用 SSL 通道。  

**將站台設定為喚醒電腦以安裝軟體時應使用的組態。**  

-   如果您使用傳統的喚醒封包，請使用單點傳播而非子網路導向的廣播。  

-   如果您必須使用子網路導向的廣播，請將路由器設定為只允許來自站台伺服器的 IP 導向的廣播，且只能在非預設連接埠號碼使用。  

如需不同網路喚醒技術的詳細資訊，請參閱[規劃如何在 System Center Configuration Manager 中喚醒用戶端](../../../core/clients/deploy/plan/plan-wake-up-clients.md)。

**如果使用電子郵件通知，請設定對 SMTP 郵件伺服器的已驗證存取權限。**  

只要可行，就請使用支援已驗證存取的郵件伺服器，並使用站台伺服器的電腦帳戶進行驗證。 如果必須指定使用者帳戶進行驗證，請使用具備最低權限的帳戶。  

##  <a name="BKMK_Security_SiteServer"></a> 站台伺服器的安全性最佳做法  
 使用以下安全性最佳作法，協助您保護 Configuration Manager 站台伺服器。  

 **將 Configuration Manager 安裝在成員伺服器，而非網域控制站上。**  

 Configuration Manager 站台伺服器和站台系統不需要安裝在網域控制站上。 除了網域資料庫外，網域控制站沒有本機安全性帳戶管理 (SAM) 資料庫。 將 Configuration Manager 安裝在成員伺服器上時，您可以在本機 SAM 資料庫而非網域資料庫中維護 Configuration Manager 帳戶。  

 此作法也會減少網域控制站上的攻擊面。  

 **安裝次要站台時，避免將檔案透過網路複製到次要站台伺服器。**  

 執行安裝程式並建立次要站台時，請不要選取從父站台複製檔案到次要站台的選項，也不要使用網路來源位置。 透過網路複製檔案時，僅管進行攻擊的時機很難掌握，有經驗的攻擊者仍可以劫持次要站台安裝套件，並在安裝檔案前竄改檔案。 只要在傳輸檔案時使用 IPsec 或 SMB，就可以緩解這種攻擊。  

 不要在次要站台伺服器上透過網路複製檔案，而是將來源檔案從媒體資料夾複製到本機資料夾。 接著，執行安裝程式以建立次要站台時，在 [安裝來源檔] 頁面上選取 [使用位於次要站台電腦上下列位置的來源檔案 (最安全)]，然後指定此資料夾。  

 如需詳細資訊，請參閱 [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (使用安裝精靈安裝站台) 主題中的[Install a secondary site](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary) (安裝次要站台)。  

##  <a name="BKMK_Security_SQLServer"></a> SQL Server 的安全性最佳做法  
 Configuration Manager 使用 SQL Server 作為後端資料庫。 如果資料庫遭到入侵，攻擊者可以略過 Configuration Manager，並直接存取 SQL Server 以經由 Configuration Manager 發動攻擊。 考量攻擊 SQL Server 會造成很高的風險，並且適當地進行消減。  

 使用以下安全性最佳作法，協助您保護 SQL Server for Configuration Manager。  

 **請不要使用 Configuration Manager 站台資料庫伺服器來執行其他 SQL Server 應用程式。**  

 增加存取 Configuration Manager 站台資料庫伺服器時，這會對您的 Configuration Manager 資料增加更多風險。 如果 Configuration Manager 站台資料庫遭到入侵，相同 SQL Server 電腦上的其他應用程式接著也會有危險。  

 **設定 SQL Server 使用 Windows 驗證。**  

 儘管 Configuration Manager 會使用 Windows 帳戶和 Windows 驗證來存取站台資料庫，仍可以設定 SQL Server 使用 SQL Server 混合模式。 SQL Server 混合模式可允許其他 SQL 登入來存取資料庫，不過這並非必要，且會增加受攻擊面。  

 **請採取額外步驟來確保使用 SQL Server Express 的次要站台有最新的軟體更新。**  

 安裝主要站台時，Configuration Manager 會從 Microsoft 下載中心下載 SQL Server Express，並將檔案複製到主要站台伺服器。 安裝次要站台，並選取安裝 SQL Server Express 的選項時，Configuration Manager 會安裝先前下載的版本，不會檢查是否有可用的新版本。 若要確保次要站台有最新版本，請執行下列其中一項工作：  

-   安裝次要站台後，請在次要站台伺服器上執行 Windows Update。  

-   在您安裝次要站台前，請在將執行次要站台伺服器的電腦上安裝 SQL Server Express，並確保安裝最新版本以及所有軟體更新。 接著，安裝次要站台，並選取使用現有 SQL Server 執行個體的選項。  

定期針對這些站台與所有安裝的 SQL Server 版本執行 Windows Update，以確保均擁有最新的軟體更新。  

**遵循 SQL Server 的最佳作法。**  

找出並遵循您的 SQL Server 版本適用的最佳作法。 不過，請將下列 Configuration Manager 需求納入考量：  

-   站台伺服器的電腦帳戶必須是執行 SQL Server 之電腦上的系統管理群組成員。 如果您遵循 SQL Server 建議「明確佈建系統管理員主體」，則用來在站台伺服器上執行安裝程式的帳戶就必須是 SQL 使用者群組的成員。  

-   如果您使用網域使用者帳戶來安裝 SQL Server，請確定已針對發佈至 Active Directory 網域服務的服務主體名稱 (SPN) 設定站台伺服器電腦帳戶。 若無 SPN，Kerberos 驗證會失敗，Configuration Manager 安裝程式也會失敗。  

##  <a name="BKMK_Security_IIS"></a> 執行 IIS 之站台系統的安全性最佳做法  
Configuration Manager 中有多個網站系統角色需要 IIS。 保護 IIS 的程序可讓 Configuration Manager 正常運作，並降低受到安全性攻擊的風險。 在實務上，請將需要 IIS 的伺服器數量降至最低。 例如，執行的管理點數目僅為需要支援用戶端的基礎，同時將高可用性以及針對網際網路型用戶端管理的網路隔離都納入考量。  

 使用以下安全性最佳作法，協助您保護執行 IIS 的站台伺服器。  

 **停用不需要的 IIS 功能。**  

 僅針對安裝的站台系統角色安裝最少的 IIS 功能。 如需詳細資訊，請參閱 [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (站台和站台系統必要條件)。  

 **設定站台系統角色為要求 HTTPS。**  

 用戶端使用 HTTP 而非 HTTPS 連線至站台伺服器時，會使用 Windows 驗證，但可能會回復為使用 NTLM 驗證，而非 Kerberos 驗證。 使用 NTLM 驗證時，用戶端可能會連線至 Rogue 伺服器 (惡意伺服器)。  

 這種安全性最佳作法的例外可能是發佈點，因為設定發佈點要求 HTTPS 時，套件存取帳戶會無法運作。 套件存取帳戶會為內容提供授權，如此您就能限制哪些使用者可以存取內容。 如需詳細資訊，請參閱[內容管理的安全性最佳做法](../../../core/plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement)。  

**針對站台系統角色，設定 IIS 中的憑證信任清單 (CTL)。**  

站台系統角色  

-   設定為要求 HTTPS 的發佈點  

-   設定為要求 HTTPS 且啟用為支援行動裝置的管理點

憑證信任清單 (CTL) 是受信任根憑證授權單位的定義清單。 搭配群組原則與公開金鑰基礎結構 (PKI) 部署使用 CTL 時，CTL 可讓您增補網路上所設定的現有受信任根憑證授權單位，例如自動隨 Microsoft Windows 一起安裝，或經由 Windows 企業根憑證授權單位新增的單位。 不過，在 IIS 中設定 CTL 時，它會定義這些受信任根憑證授權單位的子集。  

此子集提供您更多的安全性控制，因為 CTL 會限制僅接受由 CTL 中憑證授權單位所發出的用戶端憑證。 例如，Windows 隨附數個著名的協力廠商憑證授權單位憑證，如 VeriSign 與 Thawte。

根據預設，執行 IIS 的電腦會信任鏈結至這些著名憑證授權單位的憑證。 在您並未針對列出的站台系統角色使用 CTL 設定 IIS 時，擁有從這些憑證授權單位發出之用戶端憑證的裝置都會獲得接受，成為有效的 Configuration Manager 用戶端。 如果您使用未包含這些憑證授權單位的 CTL 來設定 IIS，若憑證鏈結至這些憑證授權單位，就會拒絕用戶端連線。 不過，為了針對列出的站台系統角色讓 Configuration Manager 用戶端獲得接受，您必須使用指定 Configuration Manager 用戶端所使用之憑證授權單位的 CTL 來設定 IIS。  

> [!NOTE]  
>  只有列出的站台系統角色才會要求您在 IIS 中設定 CTL。 Configuration Manager 用於管理點的憑證簽發者清單會在用戶端電腦連線至 HTTPS 管理點時提供該電腦相同的功能。  

如需有關如何在 IIS 中設定受信任憑證授權單位清單的詳細資訊，請參閱您的 IIS 說明文件。  

**請不要將站台伺服器置於搭載 IIS 的電腦。**  

角色分離可協助降低攻擊設定檔，並提昇可復原性。 此外，站台伺服器的電腦帳戶一般都會在所有站台系統角色上 (若您使用用戶端推入安裝，則可能會在 Configuration Manager 用戶端上) 具備系統管理權限。  

**為 Configuration Manager 使用專屬的 IIS 伺服器。**  

儘管您可以在 Configuration Manager 也使用的 IIS 伺服器上裝載多個 Web 式應用程式，這種作法會明顯增加攻擊面。 設定糟糕的應用程式可能會讓攻擊者控制 Configuration Manager 站台系統，甚至進一步取得階層的控制。  

如果您必須在 Configuration Manager 站台系統上執行其他 Web 式應用程式，請為 Configuration Manager 站台系統建立自訂網站。  

**使用自訂網站。**  

針對執行 IIS 的站台系統，您可以設定 Configuration Manager 為使用自訂網站，而非 IIS 的預設網站。 如果您必須在站台系統上執行其他 Web 應用程式，必須使用自訂網站。 這種設定是一種全站台設定，而非針對特定站台系統的設定。  

除了提供額外安全性外，如果您在站台系統上執行其他 Web 式應用程式，還必須使用自訂網站。  

**如果您在安裝任何發佈點角色後，從預設網站切換到自訂網站，請移除預設虛擬目錄。**  

當您從使用預設網站變成使用自訂網站時，Configuration Manager 不會移除舊的虛擬目錄。 移除 Configuration Manager 原本在預設網站下建立的虛擬目錄。  

例如，以下是要針對發佈點移除的虛擬目錄：  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**遵循 IIS 伺服器的最佳作法。**  

找出並遵循您的 IIS 伺服器版本適用的最佳作法。 不過，請將 Configuration Manager 對於特定站台系統角色的所有需求納入考量。 如需詳細資訊，請參閱 [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (站台和站台系統必要條件)。  

##  <a name="BKMK_Security_ManagementPoint"></a> 管理點的安全性最佳做法  
 管理點是裝置與 Configuration Manager 間的主要介面。 考量管理點與管理點執行的伺服器可能受到的攻擊，這方面的風險極高，並且適當地進行消減。 採用所有適合的安全性最佳作法，並監控所有異常的活動。  

 使用以下安全性最佳作法，協助您保護 Configuration Manager 中的管理點。  

**在管理點上安裝 Configuration Manager 時，將其指派至該管理點的站台。**  

 請避免發生「將位於管理點站台系統的 Configuration Manager 用戶端指派到管理點站台以外的其他站台」這種情況。  

 如果您是從舊版移轉至 System Center Configuration Manager，請儘速將管理點上的用戶端軟體移轉至 System Center Configuration Manager。  

##  <a name="BKMK_Security_FSP"></a> 後援狀態點的安全性最佳做法  
 如果您在 Configuration Manager 安裝後援狀態點，請使用以下安全性最佳作法。  

 如需有關安裝後援狀態點時的安全性考量的詳細資訊，請參閱 [Determine Whether You Require a Fallback Status Point](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md#determine-if-you-need-a-fallback-status-point)。  


**請不要在站台系統上執行其他站台系統角色，也不要將後援狀態點安裝在網域控制站上。**  

 由於後援狀態點設計為會接受來自其他電腦未經驗證的通訊，以其他站台系統角色或在網域控制站上執行此站台系統角色，會對該伺服器造成極大的風險。  

**針對在 Configuration Manager 中的用戶端通訊使用 PKI 憑證時，請在安裝用戶端前安裝後援狀態點。**  

 如果 Configuration Manager 站台系統不接受 HTTP 用戶端通訊，您可能會因為與 PKI 相關的憑證問題，導致您不知道用戶端不受管理。 不過，如果將用戶端指派至後援狀態點，後援狀態點就會回報這些憑證問題。  

 基於安全原因，您無法在安裝用戶端後指派其後援狀態點。 而是只能在用戶端安裝期間指派此角色。  

**避免在周邊網路使用後援狀態點。**  

 根據設計，後援狀態點會接受來自任何用戶端的資料。 雖然周邊網路的後援狀態點可協助您疑難排解網際網路用戶端的問題，您仍必須衡量疑難排解的好處與站台系統於公開存取網路內接受未認證資料的風險。  

 如果您確定要在周邊網路或任何不受信任網路中安裝後援狀態點，請設定站台伺服器起始資料傳輸，而不是使用允許後援狀態點起始與站台的連線的預設設定。  

##  <a name="BKMK_SecurityIssues_Clients"></a> 站台管理的安全性問題  
 檢閱下列 Configuration Manager 安全性問題：  

-   Configuration Manager 無法防禦使用 Configuration Manager 攻擊網路的授權系統管理使用者。 未授權系統管理使用者有較高的安全性風險，可能會發動各種攻擊，包括下列策略：  

    -   在企業內每個 Configuration Manager 用戶端電腦上使用軟體部署以自動安裝並執行惡意軟體。  

    -   未取得用戶端權限，使用遠端控制以取得 Configuration Manager 用戶端的遠端控制。  

    -   設定快速輪詢間隔與大量清查數量以對用戶端與伺服器建立阻絕服務攻擊。  

    -   使用階層中的一個站台以將資料寫入另一個站台的 Active Directory 資料。  

    站台階層為安全性界限。 請僅將站台視為管理界限。  

    稽核所有系統管理使用者活動並定期檢閱稽核記錄。 要求所有 Configuration Manager 系統管理使用者執行背景檢查後再進行僱用，並要求定期重新檢查作為僱用條件。  

-   如果註冊點受到破壞，攻擊者可以取得憑證進行驗證，並且盜取註冊行動裝置的使用者認證。  

    註冊點與憑證授權單位通訊，並且可以建立、修改以及刪除 Active Directory 物件。 絕不要在周邊網路中安裝註冊點，並且一律會監視不尋常活動。  

-   如果您允許網際網路用戶端管理的使用者原則，或是在使用者登入網際網路時設定應用程式類別目錄網站點，則會提高受攻擊的風險。  

    除了使用用戶端對伺服器連線的 PKI 憑證之外，這些設定需要 Windows 驗證，而連線可能會切換回使用 NTLM 授權，而不是 Kerberos 授權。 NTLM 授權會輕易受到模擬和重新執行攻擊。 若要成功驗證網際網路上的使用者，您必須允許來自網際網路站台系統的伺服器連線到網域控制站。  

-   站台系統伺服器上需要 Admin$ 共用。  

    Configuration Manager 站台伺服器使用 Admin$ 共用以連線至站台系統並且執行服務作業。 切勿停用或移除 Admin$ 共用。  

-   Configuration Manager 使用名稱解析服務以連線至其他電腦，這些服務很難以防護安全攻擊，例如詐騙、竄改、否認、資訊洩漏、阻絕服務以及提高權限。  

    辨識與留意您用以進行名稱解析的 DNS 與 WINS 版本的所有安全最佳實作。  

##  <a name="BKMK_Privacy_Cliients"></a> 探索的隱私權資訊  
 探索會建立網路資源的記錄並且將其儲存在 System Center Configuration Manager 資料庫中。 探索資料記錄包含電腦資訊，例如 IP 位址、作業系統和電腦名稱。 您也可以設定 Active Directory 探索方法以探索儲存在 Active Directory 網域服務中的所有資訊。  

 預設啟用的唯一探索方法為活動訊號探索，但是這個方法只會探索已經安裝 System Center Configuration Manager 用戶端軟體的電腦。  

 探索資訊不會傳送給 Microsoft。 相反地，它是儲存在 Configuration Manager 資料庫中。 資訊會保留在資料庫裡，直到每 90 天由站台維護工作 [刪除過時探索資料] 刪除為止。  

 設定額外探索方法或延伸 Active Directory 探索之前，請考量您的隱私權需求。  
