---
title: "密碼編譯控制項技術參考 | Microsoft Docs"
description: "了解簽署和加密在 System Center Configuration Manager 中如何協助防止攻擊讀取資料。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c63dcc5-a1bd-4037-959a-2e6ba0fd1b2c
caps.latest.revision: "6"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 09d319ce817c925ac002a27733d2ce35464eeca7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="cryptographic-controls-technical-reference"></a>密碼編譯控制項技術參考

*適用於：System Center Configuration Manager (最新分支)*


System Center Configuration Manager 使用簽署和加密來協助保護 Configuration Manager 階層中的裝置管理。 使用簽署時，如果資料在轉換時遭到變更，則會予以捨棄。 加密則可藉由使用網路通訊協定解析程式，協助防止攻擊者讀取資料。  

 Configuration Manager 用來簽署的主要雜湊演算法是 SHA-256。 當兩個 Configuration Manager 站台彼此通訊時，會使用 SHA-256 來簽署其通訊。 Configuration Manager 中實作的主要加密演算法是 3DES。 這個演算法用於將資料儲存於 Configuration Manager 資料庫中，也用於進行用戶端 HTTP 通訊。 當您使用透過 HTTPS 的用戶端通訊時，可將公開金鑰基礎結構 (PKI) 設定為使用 RSA 憑證，該憑證具備 [System Center Configuration Manager 的 PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)中所記錄的最大雜湊演算法和金鑰長度。  

 針對大多數 Windows 作業系統的密碼編譯作業，Configuration Manager 使用取自 Windows CryptoAPI 程式庫 rsaenh.dll 的 SHA-2、3DES 和 AES 以及 RSA 演算法。  

> [!IMPORTANT]  
>  有關因應 SSL 弱點的建議變更資訊，請參閱[關於 SSL 弱點](#about-ssl-vulnerabilities)。  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Configuration Manager 作業的密碼編譯控制項  
 無論您是否搭配使用 PKI 憑證與 Configuration Manager，都可以簽署與加密 Configuration Manager 中的資訊。  

### <a name="policy-signing-and-encryption"></a>原則簽署和加密  
 用戶端原則指派是由自我簽署的網站伺服器簽署憑證來進行簽署，以防止出現遭入侵的管理點寄送已被竄改的原則的安全性風險。 如果您正在使用網際網路用戶端管理，這就十分重要，原因是這種環境會要求在網際網路通訊中公開的管理點。  

 包含敏感性資料的原則會使用 3DES 加密。 包含敏感性資料的原則只會寄給獲授權的用戶端。 沒有敏感性資料的原則不會加密。  

 儲存在用戶端的原則會使用資料保護應用程式開發介面 (DPAPI) 加密。  

### <a name="policy-hashing"></a>原則雜湊  
 Configuration Manager 用戶端要求原則時，首先會收到原則指派，如此用戶端才會知道其套用的原則是哪一種，然後只要求這些原則的本文。 每種原則指派都包含相對應原則本文的計算雜湊。 用戶端會擷取適用的原則本文，然後計算本文上的雜湊。 若下載原則本文上的雜湊與原則指派中的雜湊不相符，用戶端會捨棄該原則本文。  

 原則的雜湊演算法是 SHA-1 和 SHA-256。  

### <a name="content-hashing"></a>內容雜湊  
 網站伺服器上的發佈管理員服務會針對所有封裝雜湊內容檔案。 原則提供者會將雜湊納入軟體發佈原則中。 Configuration Manager 用戶端下載內容時，用戶端會在本機重新產生雜湊，並與原則中提供的雜湊進行比對。 若雜湊相符，表示內容並未遭到變更，用戶端會安裝內容。 只要內容中有一個位元遭到變更，雜湊就不相符，也不會安裝軟體。 這項檢查有助於確保安裝正確的軟體，因為是利用原則進行實際內容的交叉檢查。  

 內容的預設雜湊演算法是 SHA-256。 若要變更此預設值，請參閱 Configuration Manager 軟體開發套件 (SDK) 的說明文件。  

 並非所有裝置都支援內容雜湊。 例外狀況包括：  

-   Windows 用戶端串流 APP-V 內容時。  

-   Windows Phone 用戶端：但這些用戶端會驗證經由信任來源簽署之應用程式的簽章。  

-   Windows RT 用戶端：但這些用戶端會驗證經由信任來源簽署之應用程式的簽章，同時也使用套件完整名稱 (PFN) 驗證。  

-   iOS：但這些裝置會驗證經由信任來源之任何開發人員憑證所簽署應用程式的簽章。  

-   Nokia 用戶端：但這些用戶端會驗證使用自我簽署憑證之應用程式的簽章。 或者，來自信任來源之憑證的簽章和憑證可以簽署 Nokia Symbian Installation Source (SIS) 應用程式。  

-   Android。 此外，這些裝置並不針對應用程式安裝使用簽章驗證。  

-   在不支援 SHA-256 的 Linux 和 UNIX 版本上執行的用戶端。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃將用戶端部署至 Linux 和 UNIX 電腦](../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)。  

### <a name="inventory-signing-and-encryption"></a>清查簽署和加密  
 無論裝置是透過 HTTP 或 HTTPS 與管理點通訊，都是由裝置簽署用戶端傳送至管理點的清查。 若使用 HTTP，您可以選擇加密此資料，這是安全性的最佳作法。  

### <a name="state-migration-encryption"></a>狀態移轉加密  
 儲存在作業系統部署之狀態移轉點的資料，一律都是由使用者狀態移轉工具 (USMT) 使用 3DES 來加密。  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>加密多點傳送套件以部署作業系統  
 針對每個作業系統部署套件，您可以在使用多點傳送將套件傳輸至電腦時啟用加密。 加密使用進階加密標準 (AES)。 若啟用加密，就不需要額外的憑證設定。 啟用多點傳送的發佈點會自動產生對稱金鑰，以便加密套件。 每個套件都有不同的加密金鑰。 金鑰會經由使用標準 Windows API，儲存在啟用多點傳送的發佈點。 用戶端連線至多點傳送工作階段時，會在使用 PKI 發行之用戶端驗證憑證 (用戶端使用 HTTPS 時) 或自我簽署憑證 (用戶端使用 HTTP 時) 加密的通道上產生金鑰交換。 用戶端會將金鑰儲存於記憶體中，僅用於多點傳送工作階段。  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>加密媒體以部署作業系統  
 使用媒體部署作業系統並指定密碼來保護媒體時，會使用進階加密標準 (AES) 來加密環境變數。 媒體上的其他資料，包括應用程式的套件與內容，則不會加密。  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>將裝載於雲端發佈點的內容加密  
 從 System Center 2012 Configuration Manager SP1 開始，使用雲端發佈點時，會使用具備 256 位元金鑰大小的進階加密標準 (AES) 來加密您上傳至這些發佈點的內容。 只要您更新內容，就會將內容重新加密。 用戶端下載內容時，會以 HTTPS 連線來進行加密與保護。  

### <a name="signing-in-software-updates"></a>在軟體更新中簽署  
 所有軟體更新都必須由信任的發行者來簽署，以避免遭到竄改。 在用戶端電腦上，Windows Update 代理程式 (WUA) 會掃描類別目錄的更新，但如果在本機電腦的 [信任的發行者] 存放區中找不到數位憑證，就不會安裝更新。 若使用自我簽署憑證 (如 WSUS 發行者自我簽署) 來發行更新類別目錄，則憑證也必須在本機電腦的「受信任的根憑證授權單位」憑證存放區中，以驗證該憑證是否有效。 WUA 也會檢查本機電腦上是否啟用 [允許來自內部網路 Microsoft 更新服務位置的已簽署內容群組原則]  設定。 必須為 WUA 啟用此原則設定，以掃描使用更新發行者建立與發行的更新。  

 在 System Center 更新發行者中發行軟體更新時，只要軟體更新發行至某部更新伺服器，數位憑證就會簽署該軟體更新。 您可以指定 PKI 憑證，或設定更新發行者產生自我簽署憑證，來簽署軟體更新。  

### <a name="signed-configuration-data-for-compliance-settings"></a>相容性設定的已簽署設定資料  
 匯入設定資料時，Configuration Manager 會驗證檔案的數位簽章。 若尚未簽署檔案，或數位簽章驗證檢查失敗，就會向您發出警告，並提示您是否要繼續匯入。 除非您明確信任發行者與檔案的完整性，否則請不要繼續匯入設定資料。  

### <a name="encryption-and-hashing-for-client-notification"></a>用戶端通知的加密和雜湊  
 若您使用用戶端通知，則所有通訊都會使用 TLS，以及伺服器與用戶端作業系統可以交涉的最高等級加密。 例如，執行 Windows 7 的用戶端電腦與執行 Windows Server 2008 R2 的管理點可以支援 128 位元 AES 加密，而執行 Vista 的用戶端電腦也可與相同的管理點通訊，但會向下交涉至 3DES 加密。 同樣的交涉會發生在雜湊於用戶端通知期間 (使用 SHA-1 或 SHA-2) 傳輸的封包上。  

##  <a name="certificates-used-by-configuration-manager"></a>Configuration Manager 使用的憑證  
 如需可由 Configuration Manager 使用之公開金鑰基礎結構 (PKI) 憑證清單、任何特殊需求或限制，以及憑證使用方式，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。 這份清單包含受支援的雜湊演算法和金鑰長度。 大部分憑證支援 SHA-256 和 2048 位元金鑰長度。  

> [!NOTE]  
>  Configuration Manager 使用的所有憑證，其主體名稱或主體別名都必須只能包含單一位元組字元。  

 以下案例中需要 PKI 憑證：  

-   管理網際網路上的 Configuration Manager 用戶端時。  

-   管理行動裝置上的 Configuration Manager 用戶端時。  

-   管理 Mac 電腦時。  

-   使用雲端發佈點時。  

-   管理超出訊號範圍的 Intel ATM 型電腦時。  

 針對需要憑證進行驗證、簽署或加密的大多數其他 Configuration Manager 通訊，Configuration Manager 會自動使用 PKI 憑證 (若憑證可用)。 若不可用，Configuration Manager 會產生自我簽署憑證。  

 Configuration Manager 使用 Exchange Server 連接器管理行動裝置時，不使用 PKI 憑證。  

### <a name="mobile-device-management-and-pki-certificates"></a>行動裝置管理和 PKI 憑證  
 若行動電信業者並未鎖定行動裝置，您可以使用 Configuration Manager 或 Microsoft Intune 來要求並安裝用戶端憑證。 此憑證可提供行動裝置上的用戶端與 Configuration Manager 站台系統或 Microsoft Intune 服務間的相互驗證。 如果行動裝置遭到鎖定，就不能使用 Configuration Manager 或 Intune 部署憑證。  

 如果您啟用行動裝置的硬體清查，Configuration Manager 或 Intune 也會清查安裝在行動裝置上的憑證。  

### <a name="out-of-band-management-and-pki-certificates"></a>頻外管理和 PKI 憑證  
 Intel AMT 型電腦的超出訊號範圍管理會使用至少兩種類型的 PKI 發行憑證：AMT 佈建憑證和 Web 伺服器憑證。  

 超出訊號範圍服務點會使用 AMT 佈建憑證來準備電腦進行超出訊號範圍管理。 即將佈建的 AMT 型電腦必須信任由超出訊號範圍管理點提出的憑證。 根據預設，電腦製造商會設定 AMT 型電腦，以使用外部憑證授權單位 (CA)，如 VeriSign、Go Daddy、Comodo 和 Starfield。 若您向其中一個外部 CA 購買佈建憑證，並設定 Configuration Manager 使用此佈建憑證，AMT 型電腦會信任佈建憑證的 CA，佈建也會成功。 但是，使用您自己的內部 CA 來發行 AMT 佈建憑證才是安全性最佳的作法。  

 AMT 型電腦會在其防火牆內執行 Web 伺服器元件，而該 Web 伺服器元件會使用傳輸層安全性 (TLS) 來加密與超出訊號範圍服務間的通訊通道。 由於使用者無法介入 AMT BIOS 來手動設定憑證，您必須有 Microsoft 企業憑證授權單位，以自動核准 AMT 型電腦提出的憑證要求。 針對要求格式，此要求會使用 PKCS#10，接著使用 PKCS#7 將憑證資訊傳輸至 AMT 型電腦。  

 雖然是由管理 AMT 型電腦的電腦完成驗證，但執行管理的電腦上還是沒有相對應的用戶端 PKI 憑證。 這些通訊則是使用 Kerberos 或 HTTP Digest 驗證。 使用 HTTP Digest 時，會使用 TLS 進行加密。  

 管理超出訊號範圍的 AMT 型電腦時，可能還需要其他類型的憑證：以 802.1X 驗證之有線網路與無線網路的選用用戶端憑證。 AMT 型電腦驗證至 RADIUS 伺服器時，可能需要用戶端憑證。 針對 EAP-TLS 驗證設定 RADIUS 伺服器時，一律都需要用戶端憑證。 針對 EAP-TTLS/MSCHAPv2 或 PEAPv0/EAP-MSCHAPv2 設定 RADIUS 伺服器時，RADIUS 設定會指定是否需要用戶端憑證。 AMT 型電腦會使用與 Web 伺服器憑證要求相同的程序來要求憑證。  

### <a name="operating-system-deployment-and-pki-certificates"></a>作業系統部署和 PKI 憑證  
 使用 Configuration Manager 部署作業系統，且管理點需要 HTTPS 用戶端連線時，即使用戶端電腦是在轉換階段 (如從工作順序媒體或支援 PXE 的發佈點開機)，也必須有憑證才能與管理點通訊。 為支援此案例，您必須建立 PKI 用戶端驗證憑證，並連同私密金鑰匯出，然後將其匯入站台伺服器內容，同時新增管理點的受信任根 CA 憑證。  

 如果您建立可開機媒體，在您建立可開機媒體時需匯入用戶端驗證憑證。 在可開機媒體上設定密碼，有助於保護在工作順序中設定的私密金鑰與其他敏感性資料。 經由可開機媒體開機的每部電腦都會對用戶端功能 (如請求用戶端原則) 所需的管理點出示相同的憑證。  

 如果您使用 PXE 開機，則要將用戶端驗證憑證匯入支援 PXE 的發佈點，且針對從該支援 PXE 的發佈點開機的每個用戶端使用相同的憑證。 作為安全性最佳作法，請要求將電腦連線至 PXE 服務的使用者提供密碼，以協助保護工作順序中的私密金鑰和其他敏感性資料。  

 如果這些用戶端驗證憑證的任何一個遭到入侵，請在 [系統管理]  工作區的 [憑證]  節點、[安全性]  節點封鎖憑證。 若要管理這些憑證，您必須擁有 [管理作業系統部署憑證]  權限。  

 部署作業系統並安裝 Configuration Manager 後，用戶端會要求本身擁有的 PKI 用戶端驗證憑證來進行 HTTPS 用戶端通訊。  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>ISV Proxy 解決方案和 PKI 憑證  
 獨立軟體廠商 (ISV) 可以建立延伸 Configuration Manager 的應用程式。 例如，ISV 可建立擴充功能以支援非 Windows 用戶端平台 (如 Macintosh 或 UNIX 電腦)。 不過，如果站台系統需要 HTTPS 用戶端連線，這些用戶端也必須使用 PKI 憑證與站台進行通訊。 Configuration Manager 包含將憑證指派給 ISV Proxy 的功能，讓 ISV Proxy 用戶端和管理點之間能夠進行通訊。 如果您使用需要 ISV Proxy 憑證的擴充功能，請參閱該產品的說明文件。 如需如何建立 ISV Proxy 憑證的詳細資訊，請參閱 Configuration Manager 軟體開發商套件 (SDK)。  

 若 ISV 憑證遭到入侵，請在 [系統管理]  工作區的 [憑證]  節點、[安全性]  節點封鎖憑證。  

### <a name="asset-intelligence-and-certificates"></a>Asset Intelligence 和憑證  
 Configuration Manager 會安裝 Asset Intelligence 同步處理點所使用的 X.509 憑證以連線至 Microsoft。 Configuration Manager 使用此憑證來向 Microsoft 憑證服務中心要求用戶端驗證憑證。 用戶端驗證憑證會安裝在 Asset Intelligence 同步處理點網站系統伺服器上，用來驗證連線至 Microsoft 的伺服器。 Configuration Manager 會使用用戶端驗證憑證來下載 Asset Iintelligence 類別目錄和上傳軟體標題。  

 此憑證的金鑰長度為 1024 位元。  

### <a name="cloud-based-distribution-points-and-certificates"></a>雲端發佈點和憑證  
 從 System Center 2012 Configuration Manager SP1 開始，雲端發佈點需要您上傳至 Microsoft Azure 的管理憑證 (自我簽署或 PKI)。 這個管理憑證需要伺服器驗證功能和長度為 2048 位元的憑證金鑰。 此外，您必須針對每個雲端發佈點設定服務憑證 (這不能自我簽署)，並且也必須擁有伺服器驗證功能和長度至少為 2048 位元的憑證金鑰。  

> [!NOTE]  
>  自我簽署的管理憑證僅供測試用，不可用在產品網路上。  

 用戶端不需要用戶端 PKI 憑證即可使用雲端發佈點；它們使用自我簽署憑證或用戶端 PKI 憑證來針對管理進行驗證。 管理點接著會向用戶端發出 Configuration Manager 存取權杖，用戶端必須向雲端發佈點出示該權杖。 權杖的有效時間為 8 小時。  

### <a name="the-microsoft-intune-connector-and-certificates"></a>Microsoft Intune 連接器和憑證  
 當 Microsoft Intune 註冊行動裝置時，您可以藉由建立 Microsoft Intune 連接器，在 Configuration Manager 中管理這些行動裝置。 連接器使用具備用戶端驗證功能的 PKI 憑證，來驗證 Configuration Manager 至 Microsoft Intune，並使用 SSL 在這兩者間傳輸所有資訊。 憑證金鑰大小為 2048 位元，並使用 SHA-1 雜湊演算法。  

 安裝連接器時，系統會在網站伺服器上建立及儲存側載金鑰的簽署憑證，並在憑證登錄點上建立及儲存加密憑證，以便對簡單憑證註冊通訊協定 (SCEP) 挑戰進行加密。 這些憑證的金鑰大小也是 2048 位元，並使用 SHA-1 雜湊演算法。  

 Intune 註冊行動裝置時，會將 PKI 憑證安裝至行動裝置。 憑證具備用戶端驗證功能，使用大小為 2048 位元的金鑰，並使用 SHA-1 雜湊演算法。  

 Microsoft Intune 會自動要求、產生並安裝這些 PKI 憑證。  

### <a name="crl-checking-for-pki-certificates"></a>PKI 憑證的 CRL 檢查  
 PKI 憑證撤銷清單 (CRL) 會增加系統管理和處理的負荷，但是更為安全。 不過，如果啟用了 CRL 檢查，但無法存取 CRL，則 PKI 連線會失敗。 如需詳細資訊，請參閱 [System Center Configuration Manager 的安全性和隱私權](../../core/plan-design/security/security-and-privacy.md)。  

 根據預設，憑證撤銷清單 (CRL) 檢查在 IIS 中為啟用狀態，因此，如果您搭配 PKI 部署使用 CRL，就不需要在大部分執行 IIS 的 Configuration Manager 站台系統上進行其他設定。 例外的是軟體更新，這需要手動步驟來啟用 CRL 檢查，以驗證軟體更新檔案上的簽章。  

 根據預設，當用戶端電腦使用 HTTPS 用戶端連線時，就會針對用戶端電腦啟用 CRL 檢查。 當您執行超出訊號範圍管理主控台以連線至 AMT 型電腦時，根據預設，並未啟用 CRL 檢查，不過您可以啟用這個選項。 在 Configuration Manager SP1 或更新版本中，您無法對 Mac 電腦上的用戶端停用 CRL 檢查。  

 在 Configuration Manager 中的以下連線，並不支援 CRL 檢查：  

-   伺服器對伺服器連線。  

-   Configuration Manager 註冊的行動裝置。  

-   由 Microsoft Intune 註冊的行動裝置。  

##  <a name="cryptographic-controls-for-server-communication"></a>伺服器通訊的密碼編譯控制項  
 Configuration Manager 會針對伺服器通訊使用以下密碼編譯控制項。  

### <a name="server-communication-within-a-site"></a>站台內的伺服器通訊  
 每個站台系統伺服器都會使用憑證將資料傳輸到相同 Configuration Manager 站台內的其他站台系統。 某些網站系統角色也會使用憑證進行驗證。 例如，若您在一部伺服器上安裝了註冊 Proxy 點，在另一部伺服器上安裝註冊點，它們可使用此身分識別憑證來彼此驗證。 Configuration Manager 使用憑證進行此種通訊時，若有具備伺服器驗證功能的 PKI 憑證可用，Configuration Manager 就會自動使用該憑證；如果沒有，則 Configuration Manager 會產生自我簽署的憑證。 此自我簽署的憑證擁有伺服器驗證功能，並使用 SHA-256，且具有 2048 位元的金鑰長度。 Configuration Manager 會將憑證複製到可能需要信任該站台系統之其他站台系統伺服器上的「受信任的人」存放區。 如此，網站系統就可以使用這些憑證和 PeerTrust 彼此信任。  

 除了每部站台系統伺服器上的此一憑證之外，Configuration Manager 還會針對大部分站台系統角色產生自我簽署憑證。 在相同網站中出現一個以上的網站系統角色執行個體時，則會共用相同憑證。 例如，在相同網站中，您可能有多個管理點或多個註冊點。 這種自我簽署憑證也使用 SHA-256，金鑰長度同樣為 2048 位元。 此外，憑證也會複製到可能需要信任該憑證之網站系統伺服器上的受信任人存放區。 以下網站系統角色會產生此種憑證：  

-   應用程式類別目錄 Web 服務點  

-   應用程式類別目錄網站點  

-   Asset Intelligence 同步處理點  

-   憑證登錄點  

-   Endpoint Protection 點  

-   註冊點  

-   後援狀態點  

-   管理點  

-   啟用多點傳送的發佈點  

-   超出訊號範圍服務點  

-   Reporting Services 點  

-   軟體更新點  

-   狀態移轉點  

-   系統健全狀況驗證程式點  

-   Microsoft Intune 連接器  

 Configuration Manager 會自動管理這些憑證，並且必要時會自動產生這些憑證。  

 Configuration Manager 也會使用用戶端驗證憑證，從發佈點傳送狀態訊息至管理點。 若僅針對 HTTPS 用戶端連線設定管理點，則必須使用 PKI 憑證。 如果管理點接受 HTTPS 連線，您可以使用 PKI 憑證或選取選項以使用自我簽署憑證 (該憑證具備用戶端驗證功能、使用 SHA-256，且金鑰長度為 2048 位元)。  

### <a name="server-communication-between-sites"></a>站台間的伺服器通訊  
 Configuration Manager 使用資料庫複寫和檔案為基礎的複寫在網站之間傳送資料。 如需詳細資訊，請參閱 [System Center Configuration Manager 中端點間的通訊](../../core/plan-design/hierarchy/communications-between-endpoints.md)。  

 Configuration Manager 會自動在站台間設定資料庫複寫，並且若有具備伺服器驗證功能的 PKI 憑證，便會使用這些憑證；如果沒有，則 Configuration Manager 會建立自我簽署憑證來進行伺服器驗證。 無論是哪一種狀況，都會經由使用 PeerTrust 之受信任人存放區的憑證來建立網站間的驗證。 這個憑證存放區是用來確保只有 Configuration Manager 階層使用的 SQL Server 電腦會參與站台對站台複寫。 由於主要網站與管理中心網站可以將設定變更複寫至階層中的所有網站，因此次要網站只能將設定變更複寫到其父網站。  

 網站伺服器會使用自動出現的安全金鑰交換來建立網站對網站通訊。 傳送端的網站伺服器會產生雜湊，並以其私密金鑰簽署。 接收端的網站伺服器會使用公開金鑰檢查簽章，並以本機產生的數值比對雜湊。 如果相符，接收端的網站會接受複寫的資料。 如果值不相符，Configuration Manager 會拒絕複寫資料。  

 Configuration Manager 中的資料庫複寫使用 SQL Server Service Broker，經由以下機制在站台間傳輸資料：  

-   SQL Server 至 SQL Server 連線：此機制經由進階加密標準 (AES) 使用 Windows 認證進行伺服器驗證，並使用長度為 1024 位元的自我簽署憑證簽署並加密資料。 若有具備伺服器驗證功能的 PKI 憑證可用，則會使用這些憑證。 憑證必須放在電腦憑證存放區的個人存放區內。  

-   SQL Service Broker：此機制經由進階加密標準 (AES) 使用長度為 2048 位元的自我簽署憑證進行驗證，以及簽署與加密資料。 憑證必須放在 SQL Server Master 資料庫中。  

 以檔案為基礎的複寫會使用伺服器訊息區 (SMB) 通訊協定，並使用 SHA-256 簽署未加密但也未包含任何敏感性資料的此資料。 如果您要加密此資料，可以使用 IPsec，且必須獨立於 Configuration Manager 來執行。  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>針對使用 HTTPS 與站台系統通訊的用戶端的密碼編譯控制項  
 網站系統角色接受用戶端連線時，您可以將其設定為接受 HTTPS 與 HTTP 連線，或僅接受 HTTPS 連線。 接受網際網路連線的網站系統角色僅接受透過 HTTPS 的用戶端連線。  

 透過 HTTPS 的用戶端連線能整合公開金鑰基礎結構 (PKI)，提供更高等級的安全性，以協助保護用戶端至伺服器的通訊。 不過，設定 HTTPS 用戶端連線時若對 PKI 規劃、部署和作業沒有透徹了解，則還是無濟於事。 例如，如果您未保護根 CA 的安全，攻擊者就可以入侵破壞整個 PKI 基礎結構的信任。 使用受控制與受保護的程序卻無法部署和管理 PKI 憑證，可能會導致出現無法接受重大軟體更新或封包的未受管理用戶端。  

> [!IMPORTANT]  
>  用於用戶端通訊的 PKI 憑證僅保護用戶端與部份網站系統間的通訊， 該憑證不會保護網站伺服器與網站系統間或網站伺服器間的通訊通道。  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>用戶端使用 HTTPS 通訊時未加密的通訊  
 用戶端使用 HTTPS 與網站系統通訊時，通常透過 SSL 加密通訊。 不過，在以下狀況中，用戶端可以不使用加密，就與網站系統進行通訊：  

-   網站系統允許此設定時，用戶端無法在內部網路建立 HTTPS 連線，退而求其次使用 HTTP  

-   與以下網站系統角色的通訊：  

    -   用戶端傳送狀態訊息至後援狀態點  

    -   用戶端向支援 PXE 的發佈點傳送 PXE 要求  

    -   用戶端傳送通知資料至管理點  

 設定 Reporting Services 點獨立於用戶端通訊節點，使用 HTTP 或 HTTPS。  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>針對使用 HTTP 與站台系統通訊的用戶端的密碼編譯控制項  
 用戶端對站台系統角色使用 HTTP 通訊時，可以使用 PKI 憑證或 Configuration Manager 產生的自我簽署憑證進行用戶端驗證。 當 Configuration Manager 產生自我簽署憑證時，憑證中會有用於簽署及加密的自訂物件識別碼，而這些憑證也會用來唯一識別用戶端。 對於所有支援的作業系統 (Windows Server 2003 除外)，這些自我簽署憑證會使用 SHA-256，且金鑰長度為 2048 位元。 如果是 Windows Server 2003，則會使用 SHA1，而金鑰長度為 1024 位元。  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>作業系統部署和自我簽署憑證  
 使用 Configuration Manager 部署具備自我簽署憑證的作業系統時，即使電腦是在轉換階段 (如從工作順序媒體或支援 PXE 的發佈點開機)，也必須有憑證才能與管理點通訊。 為支援此種案例以進行 HTTP 用戶端連線，Configuration Manager 會產生自我簽署憑證時，憑證中具有用於簽署及加密的自訂物件識別碼，而這些憑證也會用來唯一識別用戶端。 對於所有支援的作業系統 (Windows Server 2003 除外)，這些自我簽署憑證會使用 SHA-256，且金鑰長度為 2048 位元。 如果是 Windows Server 2003，則會使用 SHA1，而金鑰長度為 1024 位元。 ‎如果這些自我簽署憑證遭到入侵，為了避免攻擊者使用這些憑證模擬受信任的用戶端，請在 [系統管理]  工作區的 [憑證]  節點、[安全性]  節點上封鎖憑證。  

### <a name="client-and-server-authentication"></a>用戶端和伺服器驗證  
 用戶端透過 HTTP 連線時，會使用 Active Directory 網域服務或 Configuration Manager 受信任的根金鑰驗證管理點。 用戶端並不會驗證其他網站系統角色，例如狀態移轉點或軟體更新點。  

 管理點第一次使用自我簽署用戶端憑證驗證用戶端時，由於任何電腦皆可產生自我簽署憑證，因此該機制提供的安全性並不高。 在此案例中，必須在經過核准後增強用戶端識別程序。 只能核准受信任的電腦，並且必須由 Configuration Manager 自動核准，或是由系統管理員手動核准。 如需詳細資訊，請參閱 [System Center Configuration Manager 中端點間的通訊](../../core/plan-design/hierarchy/communications-between-endpoints.md)中的核准一節。  

##  <a name="about-ssl-vulnerabilities"></a>關於 SSL 弱點  
 我們建議您停用 SSL 3.0、啟用 TLS 1.1 和 1.2 並重新排序 TLS 相關的加密套件，以改善 Configuration Manager 伺服器的安全性。 若想了解如何執行這些動作，請參閱 [這篇知識庫文章](https://support.microsoft.com/en-us/kb/245030/)。 這個動作不會影響 Configuration Manager 的功能。  
