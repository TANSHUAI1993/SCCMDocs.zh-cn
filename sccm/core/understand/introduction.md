---
title: "簡介 | Microsoft Docs"
description: "了解 System Center Configuration Manager 的簡介基本資訊。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
caps.latest.revision: "16"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 76f907b17df0dd2f102e34ca3cfb3ffc813c0004
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-system-center-configuration-manager"></a>Introduction to System Center Configuration Manager (System Center Configuration Manager 簡介)

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager (Microsoft System Center 管理解決方案套件中的產品) 可協助您在內部部署和雲端中管理裝置和使用者。  

**您可以使用 Configuration Manager 協助：**   
-   透過減少手動工作，並讓您專注於高價值專案，來提高 IT 生產力與效率。  
-   最大化硬體和軟體投資。  
-   適時提供正確的軟體，來加強使用者產能。  

**Configuration Manager 可協助您提供更高效益的 IT 服務，方法是啟用：**  

-   安全且可擴充的軟體部署。  
-   合規性設定管理。  
-   伺服器、桌上型電腦、膝上型電腦和行動裝置的全面性資產管理。  

**可擴充並與現有的 Microsoft 技術和解決方案搭配使用。**  

例如，Configuration Manager 可整合：  

-   Microsoft Intune 以管理各種行動裝置平台。  
-   Windows Server Update Services (WSUS) 來管理軟體更新。  
-   憑證服務。  
-   Exchange Server 和 Exchange Online。  
-   Windows 群組原則。
-   DNS。   
-   Windows Automated Deployment Kit (Windows ADK) 和使用者狀態移轉工具 (USMT)。  
-   Windows 部署服務 (WDS)。  
-   遠端桌面和遠端協助。  

Configuration Manager 也會使用：  

-   Active Directory 網域服務提供安全性、服務位置和組態，以及探索您要管理的使用者和裝置。  
-   Microsoft SQL Server 作為分散式變更管理資料庫，並與 SQL Server Reporting Services (SSRS) 整合以產生報告，用來管理及追蹤管理活動。  
-   擴充管理功能並使用 Internet Information Services (IIS) 的 Web 服務的站台系統角色。
-   背景智慧型傳送服務 (BITS) 和 BranchCache 可協助管理可用的網路頻寬。  

若要成功運用 Configuration Manager，您必須先徹底規劃並測試管理功能，再於生產環境中使用 Configuration Manager。 Configuration Manager 是功能強大的管理應用程式，因此可能會影響組織中的每一部電腦。 若您部署及管理 Configuration Manager 時仔細規劃並考量業務需求，Configuration Manager 就能減少您的系統管理負荷與整體擁有成本。  

請使用下列主題以及本主題的其他各節，深入了解 Configuration Manager。  


**本文件庫中的相關主題：**  

-   [System Center Configuration Manager 的功能](../../core/plan-design/changes/features-and-capabilities.md)  
-   [選擇 System Center Configuration Manager 的裝置管理解決方案](../../core/plan-design/choose-a-device-management-solution.md)  
-   [System Center Configuration Manager 和 System Center 2012 Configuration Manager 之間的變更](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
-   [System Center Configuration Manager 的基礎](../../core/understand/fundamentals.md)  
-   [建置專屬實驗室環境來評估 System Center Configuration Manager](/sccm/core/get-started/set-up-your-lab)
-   [尋找使用 System Center Configuration Manager 的說明](../../core/understand/find-help.md)  
-   [System Center Configuration Manager 的已移除和已淘汰功能](../../core/plan-design/changes/removed-and-deprecated-features.md)  

##  <a name="BKMK_Console"></a> Configuration Manager 主控台  
 在您安裝 Configuration Manager 之後，可使用 Configuration Manager 主控台設定站台和用戶端，並執行和監視管理工作。 此主控台是主要系統管理點，可讓您管理多個網站。  

 您可以使用主控台執行次要主控台，以支援特定用戶端管理工作，例如：  

-   **資源總管**，可檢視硬體和軟體清查資訊。  
-   **遠端控制**，可從遠端連線至用戶端電腦執行疑難排解工作。  

您可以在其他電腦上安裝 Configuration Manager 主控台，並使用以 Configuration Manager 角色為基礎的系統管理來限制存取權，以及系統管理使用者可以在主控台中查看哪些項目。  

如需詳細資訊，請參閱[安裝 System Center Configuration Manager 主控台](../../core/servers/deploy/install/install-consoles.md)。

##  <a name="BKMK_ApplicationCatalog"></a> 應用程式類別目錄、軟體中心和公司入口網站  
 **「應用程式類別目錄」** 是一個網站，使用者可在該網站上瀏覽，針對其 Windows 電腦要求軟體。 若要使用「應用程式類別目錄」，您必須為站台安裝「應用程式類別目錄」Web 服務點和「應用程式類別目錄」網站點。  

 **「軟體中心」**是一種應用程式，其會在 Windows 電腦安裝 Configuration Manager 用戶端時一併安裝。 使用者會執行此應用程式來要求軟體，以及管理 Configuration Manager 部署給他們的軟體。 「軟體中心」可讓使用者執行下列作業：  

-   從「應用程式類別目錄」瀏覽及安裝軟體。  
-   檢視其軟體要求歷程記錄。  
-   設定 Configuration Manager 可以在何時將軟體安裝在裝置上。  
-   如果系統管理使用者啟用遠端控制，則可以設定遠端控制的存取設定。  

**公司入口網站**是一個提供與「應用程式類別目錄」類似功能的應用程式或網站，但不適用於以 Microsoft Intune 註冊的行動裝置。  

如需詳細資訊，請參閱[開始使用 System Center Configuration Manager 的應用程式管理](../../apps/understand/introduction-to-application-management.md)。  

###  <a name="BKMK_Client"></a> Configuration Manager 內容 (在 Windows 電腦上)  
 在 Windows 電腦上安裝 Configuration Manager 用戶端時，會將 Configuration Manager 安裝在控制台中。 因為用戶端設定是在 Configuration Manager 主控台中執行，所以通常您不需要設定此應用程式。 此應用程式可幫助系統管理使用者和技術服務人員解決個別用戶端的問題。  

 如需用戶端部署的詳細資訊，請參閱 [System Center Configuration Manager 中的用戶端安裝方法](../../core/clients/deploy/plan/client-installation-methods.md)。  

##  <a name="BKMK_ExampleScenarios"></a> Configuration Manager 的範例案例  
 下列範例案例示範 Trey Research 這家公司如何使用 System Center Configuration Manager，讓使用者能夠：  

-   更具生產力。  
-   統一裝置的合規性管理，以提供更流暢的系統管理體驗。
-   簡化裝置管理以降低 IT 作業成本。  

在所有案例中，Adam 是 Configuration Manager 的主要系統管理員。  

###  <a name="BKMK_ScenarioEmpower"></a> 範例案例：確保使用者能夠從任何裝置存取應用程式  
 Trey Research 想要確保員工能夠而且盡可能有效率地存取需要的應用程式。 Adam 將這些公司需求對應到下列案例：  

|需求|目前的用戶端管理狀態|未來的用戶端管理狀態|  
|-----------------|-------------------------------------|------------------------------------|  
|新員工一上任就能有效率地執行工作。|當員工進入公司時，初次登入後需等候安裝應用程式。|當員工進入公司時，一登入，應用程式就已安裝且立即可用。|  
|員工可快速且輕鬆地要求其他需要的軟體。|員工需要其他應用程式時，就會向技術支援人員提出票證。 然後，他們通常會等待兩天來處理票證以及安裝應用程式。|員工需要其他應用程式時，可以從網站要求它們。 如果沒有授權限制，則會立即安裝它們。 如果有授權限制，使用者必須先請求核准，才能安裝應用程式。<br /><br /> 網站只會向使用者顯示允許其安裝的應用程式。|  
|如果裝置符合受監視且強制執行的安全性原則，員工可以在工作時使用行動裝置。<br /><br /> 這些原則包括強制執行強式密碼、在裝置處於非使用狀態一段時間之後將裝置鎖定，以及從遠端抹除遺失或遭竊的裝置。|員工可將其行動裝置連線至 Exchange Server 以便使用電子郵件服務。 但是，在預設 Exchange ActiveSync 信箱原則中，只有少數報告可確認其符合安全性原則。 個人使用行動裝置可能遭到禁止，除非 IT 能夠確認與原則相符。|IT 組織可透過必要的設定報告行動裝置的安全性相容性。 這項確認可讓使用者繼續在工作時使用其行動裝置。 如果行動裝置遺失或遭竊，使用者可從遠端抹除，技術服務人員亦可抹除任何報告為遺失或遭竊的使用者行動裝置。<br /><br /> 提供於 PKI 環境中註冊行動裝置的功能，以獲得額外的安全性與控制。|  
|即使員工不在辦公桌附近，也能提高生產力。|員工不在辦公桌附近且沒有可攜式電腦時，就無法使用可在整個公司內使用的 Kiosk 電腦存取其應用程式。|員工可使用 Kiosk 電腦存取其應用程式和資料。|  
|通常，企業永續性優先於安裝必要的應用程式和軟體更新。|必要的應用程式和軟體更新會在白天安裝，且經常中斷使用者的工作，因為其電腦變慢或在安裝期間重新啟動。|使用者可設定其工作時間，避免在其使用電腦時安裝必要的軟體。|  

 為了要符合需求，Adam 會使用這些 Configuration Manager 管理功能和設定選項：  

-   應用程式管理  
-   行動裝置管理  

他使用下表中的設定步驟實作這些選項：  

|設定步驟|結果|  
|-------------------------|-------------|  
|Adam 確定新使用者在 Active Directory 中擁有使用者帳戶，並在 Configuration Manager 中為這些使用者建立新的查詢式集合。 他接著建立一個對應使用者帳戶與他們將使用之主要電腦的檔案，為這些使用者定義裝置親和性，然後將此檔案匯入至 Configuration Manager。<br /><br /> Configuration Manager 中已建立新使用者必須具備的應用程式。 他接著將具有必要用途的應用程式部署至包含新使用者的集合。|由於已採用使用者裝置親和性資訊，因此可在使用者登入前，將應用程式安裝至每一個使用者的主要電腦。<br /><br /> 應用程式隨時可在使用者順利登入後立即使用。|  
|Adam 安裝及設定應用程式類別目錄網站系統角色，讓使用者可以瀏覽要安裝的應用程式。 他接著建立這些具有可用之用途的應用程式部署，然後將這些應用程式部署至包含新使用者的集合。<br /><br /> 對於具有受限制授權數目的應用程式，Adam 設定這些應用程式以要求核准。|使用者現在可以使用應用程式類別目錄來瀏覽允許他們安裝的應用程式。 使用者接著可以立即安裝應用程式，或要求核准，並返回應用程式類別目錄，以便在技術服務人員核准其要求後返回要安裝它們的應用程式類別目錄。|  
|Adam 在 Configuration Manager 中建立 Exchange Server 連接器，用來管理連線至公司內部部署 Exchange Server 的行動裝置。 他使用安全性設定來設定此連接器，包括要求設定強式密碼，以及要求在一段期間內未活動後鎖定行動裝置。<br /><br /> 為了執行 Windows Phone 8、Windows RT 和 iOS 的裝置進行其他管理，Adam 取得 Microsoft Intune 訂閱。 他接著會安裝服務連接點站台系統角色。 此行動裝置管理解決方案可為公司提供針對這些裝置進行較佳的管理支援。 這包括讓使用者能夠在這些裝置上安裝應用程式，以及廣泛地設定管理。 此外，行動裝置連線會使用由 Intune 自動建立及部署的 PKI 憑證來進行保護。<br /><br /> 設定好要搭配使用 Configuration Manager 的服務連接點和訂閱之後，Adam 傳送一封電子郵件給擁有這些行動裝置的使用者，讓他們按一下連結即可啟動註冊程序。<br /><br /> 針對由 Microsoft Intune 註冊的行動裝置，Adam 使用相容性設定來為這些行動裝置設定安全性設定。 這些設定包括要求設定強式密碼，以及要求在一段期間內未活動後鎖定行動裝置。|使用這兩種行動裝置管理解決方案，IT 組織現在可以提供有關將在公司網路上使用之行動裝置，以及使用已設定安全性設定之相容性的報告資訊。<br /><br /> 使用者可以查看當行動裝置遺失或遭竊時，如何使用應用程式類別目錄或公司入口網站，從遠端抹除行動裝置。 技術服務人員也可以使用 Configuration Manager 主控台，指示使用者如何從遠端抹除行動裝置。<br /><br /> 此外，對於由 Microsoft Intune 註冊的行動裝置，Adam 現在可以為使用者部署要安裝的行動應用程式、從這些裝置收集更多清查資料，以及藉由存取更多設定，對這些裝置進行較佳的管理控制。|  
|Trey Research 有好幾部 kiosk 電腦，供造訪辦公室的員工使用。 員工想要在登入時使用他們的應用程式。 不過，Adam 不想要在每一部電腦的本機上安裝所有應用程式。<br /><br /> 為了達成此目的，Adam 建立了包含兩種部署類型的必要應用程式：<br /><br /> **第一個：**一個完整的本機安裝應用程式，其要求為只能安裝在使用者的主要裝置上。<br /><br /> **第二個：**一個虛擬版本的應用程式，其要求為不得安裝在使用者的主要裝置上。|當造訪員工登入 kiosk 電腦時，kiosk 電腦的桌面上會顯示其所需的應用程式圖示。 當他們執行應用程式時，是以虛擬應用程式的方式進行串流處理。 透過這種方式，他們可以執行的工作就像是坐在他們的桌上型電腦前一樣。|  
|Adam 讓使用者瞭解他們可以在軟體中心內設定工作時間，並且可以選取選項，以防止在此期間以及在簡報模式時，進行軟體部署活動。|由於使用者可以控制 Configuration Manager 將軟體部署至電腦的時間，因此使用者在工作日時可以保有較佳的生產力。|  

 這些設定步驟和結果，讓 Trey Research 能確實從任何裝置存取應用程式，以順利對員工授權。  

###  <a name="BKMK_ScenarioUnify"></a> 範例案例：整合裝置的相容性管理  
 Trey Research 想要整合用戶端管理解決方案，以確定他們的電腦執行的防毒軟體會自動保持最新狀態。 即：  

-   [Windows 防火牆] 已啟用。  
-   已安裝重大軟體更新。  
-   已設定特定登錄機碼。  
-   受管理的行動裝置無法安裝或執行未簽署的應用程式。  

公司還想要將此防護擴充至網際網路，以保護從內部網路移至網際網路的膝上型電腦。  

Adam 將這些公司需求對應到下列案例：  

|需求|目前的用戶端管理狀態|未來的用戶端管理狀態|  
|-----------------|-------------------------------------|------------------------------------|  
|所有電腦執行的反惡意程式碼軟體皆已更新定義檔，並啟用 Windows 防火牆。|不同的電腦會執行不一定會保持最新狀態的不同反惡意程式碼解決方案。 雖然預設會啟用 Windows 防火牆，但是使用者有時會予以停用。<br /><br /> 如果在電腦上偵測到惡意程式碼，系統會要求使用者與技術服務人員聯繫。|所有執行相同反惡意程式碼解決方案的電腦，會自動下載最新的定義更新檔，並在使用者停用時自動重新啟用 Windows 防火牆。<br /><br /> 如果偵測到惡意程式碼，技術支援人員會自動收到通知。|  
|所有電腦在發行的第一個月內安裝重大軟體更新。|雖然已在電腦上安裝軟體更新，但許多電腦並未自動安裝重大軟體更新，直到發行後的兩到三個月才會安裝。 如此一來，在此期間內受到攻擊的可能性便會提高。<br /><br /> 對於未安裝重大軟體更新的電腦，技術支援人員會先送出電子郵件，要求使用者安裝更新。 對於保持不相容的電腦，工程師會從遠端連線至這些電腦，並手動安裝遺失的軟體更新。|在指定的當月內改善目前的合規率超過 95%，而不是傳送電子郵件或要求技術協助人員手動進行安裝。|  
|可定期檢查特定應用程式的安全性設定，並視需要進行補救。|執行複雜啟動指令碼的電腦，需仰賴電腦群組成員資格來重設特定應用程式的登錄值。<br /><br /> 由於這些指令碼只會在啟動時執行，某些電腦會保留好幾天，因此技術支援人員無法根據時間檢查設定漂移。|會檢查登錄值並自動進行補救，而不需仰賴電腦群組成員資格或重新啟動電腦。|  
|行動裝置無法安裝或執行不安全的應用程式。|系統會要求使用者不要從網際網路下載及執行可能不安全的應用程式。 但沒有控制項可以用於監視或強制執行此設定。|使用 Microsoft Intune 或 Configuration Manager 所管理的行動裝置，會自動防止安裝或執行未簽署的應用程式。|  
|從內部網路移至網際網路的膝上型電腦，必須保持安全狀態。|對於旅行的使用者，他們經常無法每天透過 VPN 連線進行連線。 這些膝上型電腦會不符合安全性需求的規範。|網際網路連線是膝上型電腦用來保持相容性與安全性需求的唯一方法。 使用者不需要登入或使用 VPN 連線。|  

 為了要符合需求，Adam 會使用這些 Configuration Manager 管理功能和設定選項：  

-   Endpoint Protection  
-   軟體更新  
-   相容性設定  
-   行動裝置管理  
-   以網際網路為基礎的用戶端管理  

他使用下表中的設定步驟實作這些選項：  

|設定步驟|結果|  
|-------------------------|-------------|  
|Adam 設定了 Endpoint Protection。 他也啟用用戶端設定以解除安裝其他反惡意程式碼解決方案，以及啟用 Windows 防火牆。 他設定了自動部署規則，使電腦會定期檢查及安裝最新的定義更新。|單一反惡意程式碼解決方案可協助保護所有電腦，方法是使用最小的系統管理負荷。 由於技術支援人員會在偵測到反惡意程式碼時自動收到電子郵件通知，因此可以快速地解決問題。 這有助於防止其他電腦遭到攻擊的情形。|  
|為了要協助提供合規率，Adam 使用了自動部署規則、定義伺服器的維護期間，以及調查針對休眠的電腦使用網路喚醒的優缺點。|重大軟體更新的相容性會增加及降低使用者或技術支援人員手動安裝軟體更新的需求。|  
|Adam 會使用相容性設定來檢查指定的應用程式是否存在。 當偵測到應用程式時，設定項目接著會檢查登錄值，並在不符合合規性時自動進行補救。|使用部署至所有電腦的設定項目及設定基準，以及每天檢查合規性，就不再需要仰賴電腦成員資格的個別指令碼，也不需要重新啟動電腦。|  
|Adam 會針對已註冊的行動裝置使用相容性設定，並設定 Exchange Server 連接器，使得未經簽署的應用程式無法在行動裝置上安裝及執行。|藉由禁止未經簽署的應用程式，行動裝置會自動保護它們不受可能有害的應用程式所影響。|  
|Adam 確定站台系統伺服器和電腦具有 Configuration Manager 為進行 HTTPS 連線所需的 PKI 憑證。 它接著會在接受網際網路用戶端連線的周邊網路中安裝其他站台系統角色。|從內部網路移至網際網路的電腦，會在使用網際網路連線時，自動繼續接受 Configuration Manager 的管理。 這些電腦不需要使用者登入他們的電腦或連線至 VPN 連線。<br /><br /> 這些電腦會繼續受到反惡意程式碼和 Windows 防火牆、軟體更新和設定項目的管理。 如此一來，相容性層級便會自動提高。|  

 這些設定步驟和結果，使得 Trey Research 能順利整合裝置的相容性管理。  

###  <a name="BKMK_ScenarioSimplify"></a> 範例案例：簡化裝置的用戶端管理  
 Trey Research 想要讓所有新電腦自動安裝公司的 Windows 7 基礎電腦映像。 在這些電腦上安裝作業系統映像後，必須管理及監視使用者在這些電腦上安裝的其他軟體。 儲存高度機密資訊的電腦，比其他電腦需要限制更多的管理原則。 例如，技術支援工程師不得從遠端進行連線、必須輸入 BitLocker PIN 才能重新啟動，以及只有本機系統管理員可以安裝軟體。  

 Adam 將這些公司需求對應到下列案例：  

|需求|目前的用戶端管理狀態|未來的用戶端管理狀態|  
|-----------------|-------------------------------------|------------------------------------|  
|新電腦已安裝 Windows 7。|技術支援人員為使用者安裝及設定 Windows 7，然後將電腦傳送到對應的位置。|新電腦直接進入最終目的地、加入網路，並自動安裝及設定 Windows 7。|  
|電腦必須能接受管理和監視。 這包括收集硬體和軟體清查資料，以協助判斷授權需求。|Configuration Manager 用戶端是使用自動用戶端推入安裝進行部署。 技術支援人員會調查為何安裝失敗，以及用戶端為何未在預期時間內傳送清查資料的原因。<br /><br /> 因為未符合安裝相依性，同時用戶端上的 WMI 可能已損壞，所以失敗頻率很高。|從電腦收集的用戶端安裝和清查資料較為可靠，技術支援人員介入的需求較少。 報告中會顯示授權資訊的軟體使用量。|  
|某些電腦必須使用較嚴格的管理原則。|由於這些電腦需使用較嚴格的管理原則，因此目前並未受到 Configuration Manager 的管理。|使用 Configuration Manager 管理這些電腦來容納例外狀況，而不造成額外的系統管理成本。|  

 為了要符合需求，Adam 會使用這些 Configuration Manager 管理功能和設定選項：  

-   作業系統部署  
-   用戶端部署和用戶端狀態  
-   相容性設定  
-   用戶端設計  
-   清查方法和 Asset Intelligence  
-   以角色為基礎的系統管理  

他使用下表中的設定步驟實作這些選項：  

|設定步驟|結果|  
|-------------------------|-------------|  
|Adam 從一台電腦擷取作業系統映像，該電腦已安裝 Windows 7 並已依照公司規格進行設定。 接著使用未知的電腦支援和 PXE，將作業系統部署到新電腦。 同時他也將 Configuration Manager 用戶端安裝為作業系統部署的一部分。|沒有技術服務人員的介入，新電腦已啟動並以更快的速度執行。|  
|Adam 設定自動全站台用戶端推入安裝，自動於任何探索到的電腦上安裝 Configuration Manager 用戶端。 如此便可確保即使用戶端未製作任何電腦的映像，該電腦仍會自動安裝用戶端，並可由 Configuration Manager 管理。<br /><br /> Adam 設定用戶端狀態在探索到任何用戶端問題時，自動加以補救。 他同時設定用戶端設定以啟用必要清查資料的收集，也設定 Asset Intelligence。|同時安裝用戶端與作業系統的速度較快且較可靠，不需等 Configuration Manager 探索到該電腦之後，才試著將用戶端來源檔案安裝到電腦上。 不過，將自動用戶端推入選項保留啟用，對已安裝作業系統的電腦來說，可作為備份方法，提供該電腦在連線到網路時自動安裝用戶端。<br /><br /> 用戶端設定可確保用戶端定期將清查資訊傳送到網站。 此設定加上用戶端狀態測試，可協助在幾乎沒有技術服務人員介入情況下，使用戶端持續執行。 例如，在偵測到 WMI 損毀時自動加以補救。<br /><br /> Asset Intelligence 報告可協助監視軟體使用和授權。|  
|Adam 為需要較嚴密原則設定的電腦建立一個集合。 接著為此集合建立自訂用戶端裝置設定，以停用遠端控制、啟用 BitLocker PIN 輸入以及僅允許本機系統管理員安裝軟體。<br /><br /> Adam 設定了以角色為基礎的系統管理，如此一來技術服務人員便無法看到這些電腦的集合。 這樣有助於確保這些電腦不會被意外當成一般標準電腦來管理。|這些電腦現在是由 Configuration Manager 管理，但具有不需要新站台的專用設定。<br /><br /> 技術服務人員看不到這些電腦的集合。 這有助於減少電腦不小心傳送標準電腦之部署和指令碼的可能性。|  

 Trey Research 報告顯示這些設定步驟和結果已成功地簡化裝置的用戶端管理。  

##  <a name="BKMK_NextSteps"></a> 後續步驟  
 安裝 Configuration Manager 之前，請先熟悉一些專屬於 Configuration Manager 的基本概念和詞彙。  

-   如果您已熟悉 System Center 2012 Configuration Manager，請參閱 [System Center Configuration Manager 和 System Center 2012 Configuration Manager 之間的變更](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)以了解新功能。  
-   如需 System Center Configuration Manager 的高階技術概觀，請參閱 [System Center Configuration Manager 的基礎](../../core/understand/fundamentals.md)。  

若您已熟悉這些基本概念，請使用 System Center Configuration Manager 文件來協助您成功地部署與使用 Configuration Manager。  
