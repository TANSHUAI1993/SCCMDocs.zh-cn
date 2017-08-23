---
title: "用戶端安全性和隱私權 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的用戶端安全性與隱私權。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
caps.latest.revision: "10"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1d871b0e1a2897c236d17211a23c9c7d93e42313
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-clients-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的用戶端安全性和隱私權

*適用對象：System Center Configuration Manager (最新分支)*

本文包含 System Center Configuration Manager 中的用戶端以及由 Exchange Server 連接器所管理之行動裝置的安全性與隱私權資訊：  

##  <a name="BKMK_Security_Cliients"></a> 用戶端的安全性最佳做法  
 當 Configuration Manager 接受來自執行 Configuration Manager 用戶端之裝置的資料時，可能會引發用戶端攻擊網站的風險。 例如傳送格式錯誤的清查，或者嘗試使網站系統超載。 因此，只能將 Configuration Manager 用戶端部署至您信任的裝置。 此外，使用以下安全性最佳作法有助於保護網站不受 Rogue 或遭盜用的裝置攻擊：  

 **使用公開金鑰基礎結構 (PKI) 憑證，以執行 IIS 的站台系統進行用戶端通訊。**  

-   作為網站內容，針對 [僅 HTTPS]  設定 [網站系統設定] 。  

-   以 **/UsePKICert** CCMSetup 內容安裝用戶端  

-   使用憑證撤銷清單 (CRL)，並且確保用戶端和通訊中的伺服器可以隨時存取憑證撤銷清單。  

 行動裝置用戶端以及網際網路上的用戶端電腦連線都需要這些憑證，因此，建議內部網路的所有用戶端連線也同樣使用這些憑證 (發佈點除外)。  

 如需 PKI 憑證需求及如何用以協助保護 Configuration Manager 的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

 **自動核准來自信任網域的用戶端電腦，並且手動檢查並核准其他電腦。**  

 您可以將階層的核准設定為手動、針對信任網域的電腦設為自動，或者針對所有的電腦設定為自動。 最安全的核准方法是自動核准信任網域成員的用戶端，並且手動檢查並核准所有其他用戶端。 除非有其他存取控制功能可預防不受信任的電腦存取您的網路，否則不建議自動核准所有用戶端。  

 當您無法使用 PKI 驗證時，核准時便會將您信任的電腦識別為受 Configuration Manager 管理。  

 如需如何手動核准電腦的詳細資訊，請參閱[從裝置節點管理用戶端](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)。  

 **請勿依賴以封鎖預防用戶端存取 Configuration Manager 階層**  

 Configuration Manager 基礎結構會拒絕被封鎖的用戶端，因此這些用戶端無法與站台系統通訊並下載原則、上傳清查資料或傳送狀態或狀態訊息。 不過，當網站系統接受 HTTP 用戶端連線時，請勿依賴用封鎖來保護 Configuration Manager 階層，以阻擋不信任電腦的存取。 在這個案例中，封鎖的用戶端可以用新的自我簽署憑證與硬體識別碼重新加入站台。 封鎖的設計是用來在您部署作業系統至用戶端時，以及在所有站台系統接受 HTTPS 用戶端連線時，封鎖遺失或遭到洩露的開機媒體。 如果您使用支援憑證撤銷清單 (CRL) 的公開金鑰基礎結構 (PKI)，請永遠將憑證撤銷視為對應可能遭到洩露之憑證的主要防線。 在 Configuration Manager 中封鎖用戶端是保護階層的第二條防線。  

 請參閱[判斷是否要在 System Center Configuration Manager 中封鎖用戶端](../../../../core/clients/deploy/plan/determine-whether-to-block-clients.md)。  

 **針對您的環境使用最安全實用的用戶端安裝方法：**  

-   對於網域電腦，群組原則用戶端安裝和以軟體更新為基礎的用戶端安裝方法，皆比用戶端推入安裝更安全。  

-   如果您套用存取控制與變更控制，建立映像與手動安裝是非常安全的方法。  

 所有用戶端安裝方法中，最不安全的是用戶端推入安裝，因為其中具有諸多相依性，包括本機系統管理權限、Admin$ 共用，以及諸多防火牆例外。 這些相依性會增加您的受攻擊面。  

 如需其他用戶端安裝方法的詳細資訊，請參閱 [System Center Configuration Manager 中的用戶端安裝方法](../../../../core/clients/deploy/plan/client-installation-methods.md)。  

 此外，盡可能選取需要 Configuration Manager 最少安全性權限的用戶端安裝方法，並且對於被指派包含可用於用戶端部署以外用途之權限的安全性角色，加以限制。 例如，自動用戶端升級需要 [系統高權限管理員]  安全性角色，而此角色會授與系統管理使用者所有的安全性權限。  

 如需各用戶端安裝方法所需之相依性和安全性權限的詳細資訊，請參閱[電腦用戶端的必要條件](../../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers)中的＜安裝方法相依性＞。  

 **如果您必須使用用戶端推入安裝，請採取以下步驟以保護用戶端推入安裝帳戶**  

 即使這個帳戶必須是每一部將要安裝 Configuration Manager 用戶端軟體的電腦本機 **Administrators** 群組成員，也絕不要將用戶端推入安裝帳戶新增至 **Domain Admins** 群組。 請建立全域群組，並且將全域群組新增至用戶端電腦上的本機 [系統管理員]  群組。 您也可以建立群組原則物件以新增受限群組設定，藉以將用戶端推入安裝帳戶新增至本機 [系統管理員]  群組。  

 如需額外的安全性，請建立多個用戶端推入安裝帳戶，其每一個帳戶對於有限數量電腦皆具有系統管理存取權，因此當一個帳戶遭到洩露時，則只有該帳戶可存取的用戶端電腦會遭到洩露。  

 **製作用戶端電腦映像前移除憑證**  

 如果您規劃要使用映像技術部署用戶端，在擷取映像之前，請一律先移除含有用戶端驗證及自我簽署憑證的憑證，例如 PKI 憑證。 如果沒有移除這些憑證，用戶端可能會互相模擬，您因而無法驗證各用戶端的資料。  

 如需有關使用 Sysprep 準備電腦以製作映像的詳細資訊，請參閱您的 Windows 部署文件。  

 **請確定 Configuration Manager 電腦用戶端取得以下憑證的授權複本：**  

-   Configuration Manager 受信任的根金鑰  

     如果您沒有針對 Configuration Manager 延伸 Active Directory 架構，而且用戶端在與管理點通訊時沒有使用 PKI 憑證，則用戶端會依賴 Configuration Manager 受信任的根金鑰來驗證有效的管理點。 在此案例中，除非用戶端使用受信任的根金鑰，否則無法驗證該管理點是否為階層的信任管理點。 在沒有受信任的根金鑰時，技術好的攻擊可以將用戶端導向至 Rogue 管理點。  

     當用戶端無法從通用類別目錄或藉由使用 PKI 憑證下載 Configuration Manager 受信任的根金鑰時，請以受信任的根金鑰預先佈建用戶端，以確保用戶端無法導向至 Rogue 管理點。 如需詳細資訊，請參閱 [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

-   網站伺服器簽署憑證  

     用戶端會使用網站伺服器簽署憑證，驗證網站伺服器是否已簽署從管理點下載的用戶端原則。 此憑證是由網站伺服器自我簽署，並且發佈至 Active Directory 網域服務。  

     當用戶端無法從通用分類目錄下載網站伺服器簽署憑證時，用戶端預設會從管理點下載該憑證。 當管理點暴露在不受信任的網路 (例如網際網路) 時，請在用戶端上手動安裝網站伺服器簽署憑證，藉以確保用戶端無法執行來自洩露之管理點的遭篡改用戶端原則。  

     若要手動安裝網站伺服器簽署憑證，請使用 CCMSetup client.msi 內容 **SMSSIGNCERT**。 如需詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端安裝內容](../../../../core/clients/deploy/about-client-installation-properties.md)。  

 **如果用戶端將從第一個接觸的管理點下載受信任的根金鑰，請勿使用自動網站指派**  

 此安全性最佳作法與前述項目連結。 若要避免新用戶端從 Rogue 管理點下載信任金鑰的風險，請只在以下情況使用自動網站指派：  

-   用戶端可以存取已發佈至 Active Directory 網域服務的 Configuration Manager 站台資訊。  

-   您以受信任的根金鑰預先佈建用戶端。  

-   您使用來自企業憑證授權單位的 PKI 憑證，在用戶端和管理點之間建立信任。  

 如需受信任之根金鑰的詳細資訊，請參閱 [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

 **使用 CCMSetup Client.msi 選項 SMSDIRECTORYLOOKUP=NoWINS 安裝用戶端電腦**  

 尋找網站與管理點的最安全服務位置方法為 Active Directory 網域服務。 如果無法使用此方法 (例如，因為無法針對 Configuration Manager 延伸 Active Directory 架構，或因為用戶端位於不受信任樹系或工作群組中)，您可以使用 DNS 發佈為替代服務位置方法。 如果這兩種方法都失敗，當管理點未針對 HTTPS 用戶端連線進行設定時，用戶端可能會切換回使用 WINS。  

 由於發佈至 WINS 比其他發佈方法更不安全，因此，請指定 SMSDIRECTORYLOOKUP=NoWINS 將用戶端電腦設定為不切換回使用 WINS。 如果您必須使用 WINS 作為伺服器位置，請使用 SMSDIRECTORYLOOKUP=WINSSECURE (預設設定)，如此便會使用 Configuration Manager 受信任的根金鑰驗證管理點的自我簽署憑證。  

> [!NOTE]  
>  當用戶端針對 SMSDIRECTORYLOOKUP=WINSSECURE 進行設定，並從 WINS 找到管理點時，用戶端會檢查其 WMI 中 Configuration Manager 受信任的根金鑰複本。 如果管理點憑證上的簽章符合用戶端上受信任的根金鑰複本，憑證便已通過驗證，用戶端則會和透過 WINS 找到的管理點通訊。 如果管理點憑證上的簽章不符合用戶端上受信任的根金鑰複本，憑證便會無效，用戶端則不會和透過 WINS 找到的管理點通訊。  

 **請確定維護期間值大到足以部署重要的軟體更新**  

 您可以設定用於裝置集合的維護期間，以限制 Configuration Manager 可以在這些裝置上安裝軟體的次數。 如果您將維護期間設定得太小，則用戶端可能無法安裝重要的軟體更新，導致用戶端容易遭受攻擊，因為安裝軟體更新可降低攻擊機率。  

 **針對具有寫入篩選器的 Windows Embedded 裝置，若 Configuration Manager 停用寫入篩選器以繼續進行軟體安裝和變更，則需採取額外的安全預防措施，以降低受攻擊面。**  

 當已在 Windows Embedded 裝置啟用寫入篩選器時，任何軟體安裝或變更只對重疊執行，在裝置重新啟動後都不會保存。 如果您使用 Configuration Manager 暫時停用寫入篩選器以保存軟體安裝和變更，在這段期間，內嵌裝置易受所有磁碟機變更的影響，包括共用資料夾。  

 雖然 Configuration Manager 在此期間會將電腦鎖定，只能由本機系統管理員登入，但是請盡可能採取額外的安全預防措施以保護電腦。 例如，啟用防火牆的其他限制，並中斷裝置與網路連接。  

 如果您使用維護期間保存變更，請小心規劃這些視窗，將寫入篩選器的停用時間降到最低，但時間長度仍足以完成軟體安裝與重新啟動。  

 **如果您使用以軟體更新為基礎的用戶端安裝，並且在網站上安裝較新版本的用戶端時，請更新在軟體更新點上發佈的軟體更新，使用戶端可接收最新的版本**  

 如果您在網站上安裝較新版本的用戶端 (例如將網站升級)，則用於發佈至軟體更新點之用戶端部署的軟體更新，便不會自動更新。 您必須將 Configuration Manager 用戶端重新發佈至軟體更新點，並按一下 [是] 以更新版本號碼。  

 如需詳細資訊，請參閱[如何使用以軟體更新為基礎的安裝來安裝 Configuration Manager 用戶端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP)中的＜將 Configuration Manager 用戶端發佈到軟體更新點＞程序。  

 **請只為您信任並已限制其實際存取權的電腦，將 [電腦代理程式] 用戶端裝置設定 [重新啟動時暫停輸入 BitLocker PIN] 設為 [永遠]。**  

 當您將這個用戶端設定值設定為 [永遠] 時，Configuration Manager 會完成軟體的安裝，以確保安裝重要的軟體更新，並且繼續服務。 不過，如果有攻擊者攔截重新啟動程序，則攻擊者可能會控制電腦。 只有在信任電腦並已限制電腦的實體存取時，才能使用此設定。 舉例來說，此設定可能適合用於資料中心內的伺服器。  

 **請勿將 [電腦代理程式] 用戶端裝置設定 [PowerShell 執行原則] 設為 [略過]。**  

 此用戶端設定允許 Configuration Manager 用戶端執行未簽署的 PowerShell 指令碼，如此可能會造成用戶端電腦執行惡意程式。 如果您必須選取此選項，請使用自訂用戶端設定，並只將其指派至必須執行未簽署之 PowerShell 指令碼的用戶端電腦。  

##  <a name="bkmk_mobile"></a> 行動裝置的安全性最佳做法  
 **您以 Configuration Manager 註冊且支援網際網路的行動裝置：將註冊 proxy 點安裝在周邊網路，並將註冊點安裝在內部網路**  

 此角色隔離有助於保護註冊點不受攻擊。 如果註冊點受到破壞，攻擊者可以取得憑證進行驗證，並且盜取註冊行動裝置的使用者認證。  

 **對於行動裝置：設定密碼設定以保護行動裝置不受他人擅自存取**  

 對於由 Configuration Manager 註冊的行動裝置：使用行動裝置設定項目設定 PIN 的密碼複雜性，以及預設的最小密碼長度。  

 對於沒有安裝 Configuration Manager 用戶端，但由 Exchange Server 連接器管理的行動裝置：設定 Exchange Server 連接器的 [密碼設定]，使密碼複雜性為 PIN，並且至少指定預設的密碼最小長度。  

 **對於行動裝置：只允許執行信任的公司簽署過的應用程式，不允許安裝未簽署的檔案，如此有助於預防清查資訊與狀態資訊遭到竄改**  

 對於由 Configuration Manager 註冊的更多行動裝置：使用行動裝置設定項目，將安全性設定 [未簽署的應用程式] 設定為 [禁止]，並將 [未簽署的檔案安裝] 設定為信任的來源。  

 對於沒有安裝 Configuration Manager 用戶端，但由 Exchange Server 連接器管理的行動裝置：設定 Exchange Server 連接器的 [應用程式設定]，將 [未簽署的檔案安裝] 與 [未簽署的應用程式] 設定為 [禁止]。  

 **對於行動裝置：鎖定未使用的行動裝置，有助於預防權限提高攻擊**  

 對於由 Configuration Manager 註冊的更多行動裝置：使用行動裝置設定項目，設定密碼設定 [鎖定行動裝置前允許的閒置時間 (分鐘)]。  

 對於沒有安裝 Configuration Manager 用戶端，但由 Exchange Server 連接器管理的行動裝置：設定 Exchange Server 連接器的 [密碼設定]，以設定 [鎖定行動裝置前允許的閒置時間 (分鐘)]。  

 **對於行動裝置：限制可註冊行動裝置的使用者，有助於預防權限提高攻擊。**  

 使用自訂用戶端設定而非預設用戶端設定，只允許已獲得授權的使用者註冊其行動裝置。  

 **對於行動裝置：在下列情況下，請勿將應用程式部署到使用 Configuration Manager 或 Microsoft Intune 註冊行動裝置的使用者：**  

-   當行動裝置由一個以上的人使用時。  

-   當系統管理員代替使用者註冊裝置時。  

-   當裝置傳送至其他使用者，而沒有先淘汰再重新註冊裝置時。  

 註冊期間會建立使用者裝置親和性關聯性，以將註冊的使用者對應到行動裝置。 如果有其他使用者使用行動裝置，則該使用將可以執行您部署至原始使用者的應用程式，如此可能導致權限提高。 同樣地，如果系統管理員為使用者註冊行動裝置，則將不會在行動裝置上安裝部署至使用者的應用程式，而會安裝部署至系統管理員的應用程式。  

 有別於 Windows 電腦的使用者裝置親和性，您不能為 Microsoft Intune 所註冊的行動裝置手動定義使用者裝置親和性資訊。  

 如果轉移 Intune 所註冊的行動裝置擁有權，則請將行動裝置從 Intune 淘汰以移除使用者裝置親和性，然後要求目前使用者再次註冊裝置。  

 **對於行動裝置：確定使用者使用 Microsoft Intune 註冊他們的行動裝置**  

 由於在註冊期間所建立的使用者裝置親和性關聯，會將註冊的使用者對應至行動裝置，因此，如果系統管理員為使用者註冊行動裝置，則部署至使用者的應用程式將不會安裝在行動裝置上，而會安裝部署至系統管理員的應用程式。  

 **對於 Exchange Server 連接器：請確定 Configuration Manager 站台伺服器與 Exchange Server 電腦之間的連線已受到保護**  

 如果是內部部署的 Exchange Server，則使用 IPsec；裝載的 Exchange 會自動使用 SSL 保護連線。  

 **對於 Exchange Server 連接器：針對連接器使用最低權限準則**  

 如需 Exchange Server 連接器所需之基本 Cmdlet 的清單，請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

##  <a name="bkmk_macs"></a> Mac 的安全性最佳做法  
 **對於 Mac 電腦：儲存和存取來自安全位置的用戶端來源檔案。**  

 Configuration Manager 不會確認用戶端來源檔案是否已遭竄改。 請從信任的來源下載這些檔案並且以安全的方式儲存和存取。  

 **對於 Mac 電腦：獨立於 Configuration Manager，監控並追蹤註冊至使用者之憑證的有效期間。**  

 為確保業務連續性，請監視並追蹤您用於 Mac 電腦的憑證有效期。 Configuration Manager 不支援此憑證的自動更新，憑證即將到期時也不會對您提出警告。 通常有效期限為 1 年。  

 如需如何更新憑證的資訊，請參閱  [Renewing the Mac Client Certificate Manually](../../../../core/clients/deploy/deploy-clients-to-macs.md#renewing-the-mac-client-certificate)。  

 **對於 Mac 電腦：您可以考慮只設定信任的根 CA 憑證至 SSL 通訊協定，以防權限提升。**  

 當您註冊 Mac 電腦時，會自動安裝管理 Configuration Manager 用戶端的使用者憑證，以及使用者憑證所鏈結的信任根憑證。 如果您想要將此根憑證的信任限制在 SSL 通訊協定，您可以使用以下程序。  

 在您完成此程序之後，根憑證在驗證 SSL 以外的通訊協定時就不會受信任 - 例如安全郵件 (S/MIME)、可延伸的驗證 (EAP) 或者程式碼簽署。  

> [!NOTE]  
>  如果您安裝獨立於 Configuration Manager 之外的用戶端憑證，您也可以使用此程序。  

 將根 CA 憑證限制為僅 SSL 通訊協定：  

1.  在 Mac 電腦上，開啟終端機視窗。  

2.  輸入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

3.  在 [金鑰鏈存取]  對話方塊的 [金鑰鏈]  區段中，按一下 [系統] ，然後按一下 [類別]  區段中的 [憑證] 。  

4.  找出並按兩下 Mac 用戶端憑證的根 CA 憑證。  

5.  在根 CA 憑證的對話方塊中，展開 [信任]  區段，然後進行下列變更：  

    1.  對於 [使用此憑證時]  設定，將 [永遠信任]  預設值改為 [使用系統預設值] .  

    2.  對於 [安全通訊端層 (SSL)]  設定，將 [未指定值]  變更為 [永遠信任] 。  

6.  關閉對話方塊，然後在收到提示時輸入系統管理員的密碼，然後按一下 [更新設定]。  

##  <a name="BKMK_SecurityIssues_Clients"></a> Configuration Manager 用戶端的安全性問題  
 以下安全性問題並未降低：  

-   狀態訊息未經驗證  

     未針對狀態訊息執行驗證。 當管理點接受 HTTP 用戶端連線時，任何裝置皆可傳送狀態訊息至管理點。 如果管理點只接受 HTTPS 用戶端連線，則裝置必須從信任的根憑證授權單位取得有效用戶端驗證憑證，但無法傳送任何狀態訊息。 如果用戶端傳送無效的狀態訊息，則會遭到捨棄。  

     有數種方式可能針對此漏洞進行攻擊。 攻擊者可傳送假的狀態訊息，以取得以狀態訊息查詢為基礎之集合中的成員資格。 任何用戶端都可能對管理點湧入大量狀態訊息，以啟動阻斷服務。 如果狀態訊息觸發狀態訊息篩選規則中的動作，則攻擊者便可能觸發狀態訊息篩選規則。 攻擊者也可能傳送會導致報告資訊轉譯錯誤的狀態訊息。  

-   原則可能會被重定至非目標的用戶端  

     攻擊者可以利用數種方式，將以一個用戶端為目標的原則套用至完全不同的用戶端。 例如，攻擊者可能會在信任的用戶端傳送錯誤的清查或探索資訊，將電腦加入到不應加入的集合，再接收該集合的所有部署。 雖然有控制項可預防攻擊者直接修改原則，但攻擊者仍可將現有的原則重新格式化，並將作業系統重新部署，再傳送至不同的電腦，藉以建立阻斷服務。 這些類型的攻擊需要具備準確的時間控制，以及多方的 Configuration Manager 基礎結構知識。  

-   用戶端記錄檔可供使用者存取  

     所有用戶端記錄檔皆允許使用者「讀取」存取，並且允許互動式使用者「寫入」存取。 如果您啟用詳細資訊記錄，攻擊者可能會讀取記錄檔，尋找有關相容性或系統漏洞的資訊。 如軟體安裝等執行於使用者內容的程序，一律都可用低權限使用者帳戶來寫入記錄檔。 這代表攻擊者也可以利用低權限帳戶寫入記錄檔。  

     最重大的風險是，攻擊者可能會將記錄檔中系統管理員用於稽核以及偵測入侵者的資訊移除。  

-   電腦可用於取得專為行動裝置註冊而設計的憑證  

     當 Configuration Manager 處理註冊要求時，無法確認要求是源自於行動裝置，而不是電腦。 如果要求是來自電腦，則可以安裝 PKI 憑證，允許電腦向 Configuration Manager 登錄。 在此案例中，若要預防權限提高攻擊，就只能讓信任的使用者註冊行動裝置，並謹慎監視註冊活動。  

-   如果您封鎖用戶端，則用戶端對管理點的連線不會中斷，封鎖的用戶端可能會以保持運作訊息的方式，繼續傳送用戶端通知封包至管理點  

     當您封鎖不再信任的用戶端，而該用戶端已建立用戶端通知通訊時，Configuration Manager 不會中斷與工作階段的連線。 封鎖的用戶端可以繼續傳送封包至其管理點，直到用戶端與網路中斷連線為止。 這些封包只是小型的保持運作封包，而且這些用戶端在被解除封鎖之前，都無法由 Configuration Manager 進行管理。  

-   當您使用自動用戶端升級，而且用戶端已導向至管理點以下載用戶端來源檔案時，管理點不會被驗證為信任的來源  

-   使用者第一次註冊 Mac 電腦時，可能有 DNS 詐騙的風險  

     當 Mac 電腦在註冊期間連線至註冊 Proxy 點時，Mac 電腦通常不具有根 CA 憑證。 此時，伺服器不會受到 Mac 電腦信任，並且會提示使用者繼續。 如果 Rogue DNS 伺服器解析註冊 Proxy 點的完整名稱，則可能會將 Mac 電腦導向至 Rogue 註冊 Proxy 點，並且安裝來自不信任來源的憑證。 為降低此風險，請遵循最佳作法以免環境中出現 DNS 詐騙。  

-   Mac 註冊不會限制憑證要求  

     每次要求新用戶端憑證時，使用者都可以重新註冊 Mac 電腦。 Configuration Manager 不會檢查是否有多個要求，或限制來自單一電腦要求的憑證數目。 Rogue 使用者可以執行重複命令列註冊要求的指令碼，促使在網路上或發行憑證授權單位 (CA) 上拒絕服務。 為降低此風險，請小心監視發行 CA 此類可疑的行為。 Configuration Manager 階層應要立即封鎖有此類行為的電腦。  

-   抹除認可並不會確認裝置是否已成功抹除  

     當您對行動裝置起始抹除動作，並且 Configuration Manager 顯示抹除狀態為認可時，驗證方式為確認 Configuration Manager 是否成功傳送訊息，而不是對其進行動作的裝置。 此外，對於由 Exchange Server 連接器管理的行動裝置，抹除認可會確認命令是否由 Exchange 接收，而非裝置。  

-   如果您使用選項認可 Windows Embedded 裝置上的變更，則可能會以比預期更快將帳戶鎖定  

     如果 Windows Embedded 裝置在執行 Windows 7 之前的作業系統，而且使用者嘗試在停用寫入篩選器時登入，以認可 Configuration Manager 所做的變更時，帳戶鎖定前所允許的錯誤登入次數會有效減半。 例如，假設 [帳戶鎖定閾值]  設定為 6，而使用者輸入錯誤密碼 3 次，便會鎖定帳戶，以有效建立服務阻斷情況。  在此案例中，如果使用者必須登入內嵌裝置，請警告使用者鎖定閥值可能會降低。  

##  <a name="BKMK_Privacy_Cliients"></a> Configuration Manager 用戶端的隱私權資訊  
 當您部署 Configuration Manager 用戶端時，會啟用用戶端設定，如此就可以使用 Configuration Manager 管理功能。 無論 Configuration Manager 階層中的用戶端是直接連線至公司網路、透過遠端工作階段連線，或是連線至網路網路 (受 Configuration Manager 支援)，您用來設定功能的設定皆可套用至階層中的所有用戶端。  

 存放在 Configuration Manager 資料庫中的用戶端資訊，不會傳送給 Microsoft。 資訊會保留在資料庫裡，直到每 90 天由網站維護工作 [刪除過時探索資料]  刪除為止。 您可以設定刪除間隔。  

 在設定 Configuration Manager 用戶端之前，請考慮您的隱私需求。  

### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>由 Configuration Manager 註冊的行動裝置隱私權資訊  
 如需以 Configuration Manager 註冊行動裝置時的隱私權資訊，請參閱 [System Center Configuration Manager 隱私權聲明 - 行動裝置增補](../../../../core/misc/privacy/privacy-statement-mobile-device-addendum.md)。  

### <a name="client-status"></a>用戶端狀態  
 Configuration Manager 會監視用戶端活動並定期評估與補救 Configuration Manager 用戶端與其相依性。 用戶端狀態預設為啟用，而且會使用伺服器端的度量來測量用戶端活動檢查、自我檢查用戶端動作、補救以及傳送用戶端狀態資訊到 Configuration Manager 站台。 用戶端會根據您可以設定的排程以執行自我檢查。 用戶端會將檢查結果傳送至 Configuration Manager 站台。 這項資訊會在傳輸過程中加密。  

 存放在 Configuration Manager 資料庫中的用戶端狀態資訊，不會傳送給 Microsoft。 此資訊不會以加密格式儲存在網站資料庫內。 並且會保留在資料庫中，直到根據針對 [保留以下指定天數內的用戶端狀態歷程]  用戶端狀態設定所設定的值進行刪除為止。 此設定的預設值為每 31 天。  

 透過用戶端狀態檢查安裝 Configuration Manager 用戶端之前，請考量您的隱私權需求。  

##  <a name="BKMK_Privacy_ExchangeConnector"></a> 使用 Exchange Server 連接器所管理的行動裝置隱私權資訊  
 Exchange Server 連接器會藉由 ActiveSync 通訊協定尋找並管理連接至 Exchange Server (內部部署或託管) 的裝置。 Exchange Server 連接器找到的記錄會儲存在 Configuration Manager 資料庫內。 此資訊會從 Exchange Server 進行收集。 伺服器不包含來自行動裝置傳送至 Exchange Server 的任何額外資訊。  

 行動裝置資訊不會傳送給 Microsoft。 行動裝置資訊儲存在 Configuration Manager 資料庫中。 資訊會保留在資料庫裡，直到每 90 天由網站維護工作 [刪除過時探索資料]  刪除為止。 您可以設定刪除間隔。  

 安裝並設定 Exchange Server 連接器之前，請考量您的隱私權需求。  
