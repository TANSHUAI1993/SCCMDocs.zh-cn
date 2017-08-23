---
title: "規劃 Linux 及 UNIX 電腦用戶端部署 | Microsoft Docs"
description: "規劃在 System Center Configuration Manager 中將用戶端部署至 Linux 和 UNIX 電腦。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
caps.latest.revision: "9"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 367ffb919a1adb9a0530f7357a0fcf1e6636af08
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-system-center-configuration-manager"></a>規劃將用戶端部署至 System Center Configuration Manager 中的 Linux 和 UNIX 電腦

*適用於：System Center Configuration Manager (最新分支)*

您可以在執行 Linux 或 UNIX 的電腦上安裝 System Center Configuration Manager 用戶端。 此用戶端是針對當作工作群組電腦運作的伺服器所設計，用戶端不支援與登入使用者互動。 當您安裝用戶端軟體，而且用戶端建立與 Configuration Manager 站台的通訊之後，就可以利用 Configuration Manager 主控台和報告來管理用戶端。  

> [!NOTE]  
>  適用於 Linux 和 UNIX 電腦的 Configuration Manager 用戶端不支援下列管理功能︰  
>   
>  -   用戶端推入安裝  
> -   作業系統部署  
> -   應用程式部署；您可以改用套件和程式部署軟體。  
> -   軟體清查  
> -   軟體更新  
> -   相容性設定  
> -   遠端控制  
> -   電源管理  
> -   用戶端狀態的用戶端檢查和補救  
> -   以網際網路為基礎的用戶端管理  

 如需支援的 Linux 和 UNIX 發佈以及支援 Linux 和 UNIX 用戶端所需硬體的資訊，請參閱 [System Center Configuration Manager 的建議硬體](../../../../core/plan-design/configs/recommended-hardware.md)。  

 本文中的資訊可協助您規劃部署適用於 Linux 和 UNIX 的 Configuration Manager 用戶端。  

##  <a name="BKMK_ClientDeployPrereqforLnU"></a> Linux 和 UNIX 伺服器的用戶端部署先決條件  
 使用下列資訊來判斷您必須以成功的必要條件安裝 Linux 和 UNIX 用戶端。  

###  <a name="BKMK_ClientDeployExternalforLnU"></a> 相依性外部功能至 Configuration Manager:  
 下列表格說明 UNIX 和 Linux 作業系統需求以及套件相依性。  

 **Red Hat Enterprise Linux ES 版本 4**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|glibc|C 標準程式庫|2.3.4-2|  
|Openssl|OpenSSL 程式庫；安全網路通訊協定|0.9.7a-43.1|  
|PAM|插入式驗證模組|0.77-65.1|  

 **Red Hat Enterprise Linux Server 5.1 版 (Tikanga)**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|glibc|C 標準程式庫|2.5-12|  
|Openssl|OpenSSL 程式庫；安全網路通訊協定|0.9.8b-8.3.el5|  
|PAM|插入式驗證模組|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server 第 6 版**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|glibc|C 標準程式庫|2.12-1.7|  
|Openssl|OpenSSL 程式庫；安全網路通訊協定|1.0.0-4|  
|PAM|插入式驗證模組|1.1.1-4|  

 **Solaris 9 SPARC**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|所需的作業系統修補程式|PAM 記憶體遺漏|112960-48|  
|SUNWlibC|Sun Workshop 編譯器配套 libC (sparc)|5.9,REV=2002.03.18|  
|SUNWlibms|適合開發人員一起共用 libm (sparc)|5.9,REV=2001.12.10|  
|Openssl|SMCosslg (sparc)<br /><br /> Sun 不提供適用 Solaris 9 SPARC 的 OpenSSL 版本。 Sunfreeware 則提供可用版本。|0.9.7g|  
|PAM|插入式驗證模組<br /><br /> SUNWcsl 核心 Solaris (共用程式庫) (sparc)|11.9.0,REV=2002.04.06.15.27|  

 **Solaris 10 SPARC**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|所需的作業系統修補程式|PAM 記憶體遺漏|117463-05|  
|SUNWlibC|Sun Workshop 編譯器配套 libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Math & Microtasking 程式庫 (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Math & Microtasking 程式庫 (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Core Solaris 程式庫 (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Core Solaris 程式庫 (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|Openssl|SUNopenssl-librararies (Usr)<br /><br /> Sun 有提供適用於 Solaris 10 SPARC 的 OpenSSL 程式庫。 它們都已和作業系統配套。|11.10.0,REV=2005.01.21.15.53|  
|PAM|插入式驗證模組<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|所需的作業系統修補程式|PAM 記憶體遺漏|117464-04|  
|SUNWlibC|Sun 研討會編譯器會搭配 libC (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Math & Microtasking 程式庫 (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|核心 Solaris、 (共用程式庫) (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|核心 Solaris 程式庫 (根) (i386)|11.10.0, REV=2005.01.21.16.34|  
|Openssl|SUNWopenssl 程式庫。OpenSSL 程式庫 (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|插入式驗證模組<br /><br /> SUNWcsr 核心 Solaris、 (Root)(i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop 編譯器配套 libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking 程式庫 (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris 程式庫 (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris，(共用程式庫)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris，(Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL 程式庫 (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|必要的套件|描述|最小版本|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop 編譯器配套 libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Math & Microtasking 程式庫 (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris 程式庫 (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris，(共用程式庫)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris，(Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|OpenSSL 程式庫 (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **SUSE Linux Enterprise Server 9 (i586)**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|Service Pack 4|SUSE Linux Enterprise Server 9||  
|OS Patch lib gcc-41.rpm|標準共用程式庫|41-4.1.2_20070115-0.6|  
|OS Patch lib stdc++-41.rpm|標準共用程式庫|41-4.1.2_20070115-0.6|  
|Openssl|OpenSSL 程式庫；安全網路通訊協定|0.9.7d-15.35|  
|PAM|插入式驗證模組|0.77-221-11|  

 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|glibc-2.4-31.30|C 標準共用程式庫|2.4-31.30|  
|Openssl|OpenSSL 程式庫；安全網路通訊協定|0.9.8a-18.15|  
|PAM|插入式驗證模組|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|C 標準共用程式庫|2.9-13.2|  
|PAM|插入式驗證模組|pam-1.0.2-20.1|  

 **Universal Linux (Debian 封裝) Debian，Ubuntu Server**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|libc6|C 標準共用程式庫|2.3.6|  
|Openssl|OpenSSL 程式庫；安全網路通訊協定|0.9.8 或 1.0|  
|PAM|插入式驗證模組|0.79-3|  

 **Universal Linux (RPM 封裝) CentOS，Oracle Linux**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|glibc|C 標準共用程式庫|2.5-12|  
|Openssl|OpenSSL 程式庫；安全網路通訊協定|0.9.8 或 1.0|  
|PAM|插入式驗證模組|0.99.6.2-3.14|  

 **IBM AIX 5L 5.3**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|OS 版本|作業系統版本|AIX 5.3，技術層次 6，Service Pack 5|  
|xlC.rte|XL C/C++ Runtime|9.0.0.2|  
|openssl.base|OpenSSL 程式庫；安全網路通訊協定|0.9.8.4|  

 **IBM AIX 6.1**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|OS 版本|作業系統版本|AIX 6.1，任何技術層次和 Service Pack|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|OpenSSL 程式庫；安全網路通訊協定|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|OS 版本|作業系統版本|AIX 7.1，任何技術層次和 Service Pack|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|OpenSSL 程式庫；安全網路通訊協定||  

 **HP-UX 11i v2 IA 64**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|HPUXBaseOS|基礎作業系統|B.11.23|  
|HPUXBaseAux|HP-UX 基礎作業系統輔助|B.11.23.0706|  
|HPUXBaseAux.openssl|OpenSSL 程式庫；安全網路通訊協定|A.00.09.07l.003|  
|PAM|插入式驗證模組|在 HP-UX 上，PAM 是核心作業系統元件的一部分。 沒有其他相依性。|  

 **HP-UX 11i v2 PA-RISC**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX 基礎作業環境|B.11.23.0706|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|相容開發工具程式庫|B.11.23|  
|HPUXBaseAux|HP-UX 基礎作業系統輔助|B.11.23.0706|  
|HPUXBaseAux.openssl|OpenSSL 程式庫；安全網路通訊協定|A.00.09.071.003|  
|PAM|插入式驗證模組|在 HP-UX 上，PAM 是核心作業系統元件的一部分。 沒有其他相依性。|  

 **HP-UX 11i v3 PA-RISC**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX 基礎作業環境|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE2-SHLIBS|特定 IA 模擬器程式庫|B.11.31|  
|openssl/Openssl.openssl|OpenSSL 程式庫；安全網路通訊協定|A.00.09.08d.002|  
|PAM|插入式驗證模組|在 HP-UX 上，PAM 是核心作業系統元件的一部分。 沒有其他相依性。|  

 **HP-UX 11i v3 IA64**  

|必要的套件|描述|最小版本|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX 基礎作業環境|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|特定 IA 開發程式庫|B.11.31|  
|SysMgmtMin|最低軟體開發工具|B.11.31.0709|  
|SysMgmtMin.openssl|OpenSSL 程式庫；安全網路通訊協定|A.00.09.08d.002|  
|PAM|插入式驗證模組|在 HP-UX 上，PAM 是核心作業系統元件的一部分。 沒有其他相依性。|  

 **Configuration Manager 相依性：**下表列出支援 Linux 和 UNIX 用戶端的站台系統角色。 如需這些站台系統角色的詳細資訊，請參閱[為 System Center Configuration Manager 用戶端判斷站台系統角色](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)。  

|Configuration Manager 網站系統|詳細資訊|  
|---------------------------------------|----------------------|  
|管理點|雖然安裝適用於 Linux 和 UNIX 的 Configuration Manager 用戶端時不需要管理點，但是您必須要有管理點，才能在用戶端電腦與 Configuration Manager 伺服器之間傳輸資訊。 若沒有管理點，就無法管理用戶端電腦。|  
|發佈點|安裝適用於 Linux 和 UNIX 的 Configuration Manager 用戶端時不需要發佈點。 不過，站台系統角色時需要您將軟體部署到 Linux 和 UNIX 伺服器。<br /><br /> 因為適用於 Linux 和 UNIX 的 Configuration Manager 用戶端不支援使用 SMB 的通訊，所以您搭配用戶端所使用的發佈點必須支援 HTTP 或 HTTPS 通訊。|  
|後援狀態點|安裝適用於 Linux 和 UNIX 的 Configuration Manager 用戶端時不需要後援狀態點。 但當 Configuration Manager 站台中的電腦無法與管理點通訊時，則需要仰賴後援狀態點才能夠傳送狀態訊息。 用戶端也可以將其安裝狀態傳送到回溯狀態點。|  

 **防火牆需求**:請確定防火牆不會在您指定為用戶端要求連接埠的連接埠上封鎖通訊。 Linux 和 UNIX 的用戶端會直接與管理點、發佈點及後援狀態點通訊。  

 如需用戶端通訊及用戶端要求連接埠的詳細資訊，請參閱  [設定 Linux 和 UNIX 用戶端來找出管理點](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP)。  

##  <a name="BKMK_PlanningforCommunicationsforLnU"></a> Linux 和 UNIX 伺服器通訊的規劃跨樹系信任  
 您使用 Configuration Manager 所管理的 Linux 和 UNIX 伺服器會作為工作群組用戶端運作，且需要具有與工作群組中以 Windows 為基礎之用戶端類似的設定。 如需工作群組中電腦通訊的詳細資訊，請參閱 [System Center Configuration Manager 中端點之間的通訊](../../../../core/plan-design/hierarchy/communications-between-endpoints.md)主題中的[跨 Active Directory 樹系的通訊](../../../../core/plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest)一節。  

###  <a name="BKMK_ServiceLocationforLnU"></a> 適用於 Linux 和 UNIX 用戶端服務位置  
 尋找服務提供給用戶端站台系統伺服器的工作被指服務位置。 不同於 Windows 架構的用戶端、 適用於 Linux 和 UNIX 用戶端不會使用 Active Directory 服務位置。 此外，適用於 Linux 和 UNIX 的 Configuration Manager 用戶端不支援會指定管理點網域尾碼的用戶端內容。 而是用戶端會學習安裝用戶端軟體時指派已知的管理點從用戶端提供服務的其他站台系統伺服器。  

 如需服務位置的詳細資訊，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)主題中的[服務位置以及用戶端如何判斷其指派的管理點](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)一節。  

##  <a name="BKMK_SecurityforLnU"></a> 規劃安全性和憑證 Linux 和 UNIX 伺服器  
 為了與 Configuration Manager 站台進行安全且已驗證的通訊，適用於 Linux 和 UNIX 的 Configuration Manager 用戶端會使用和 Windows 的 Configuration Manager 用戶端相同的模型來進行通訊。  

 當您安裝 Linux 和 UNIX 的用戶端時，可以將 PKI 憑證指派給用戶端，使其能夠使用 HTTPS 與 Configuration Manager 站台通訊。 如果未指派的 PKI 憑證，用戶端會建立自我簽署的憑證和只能透過 HTTP 進行通訊。  

 在安裝時所提供的 PKI 憑證用戶端使用 HTTPS 與管理點通訊。 找不到支援 HTTPS 管理點用戶端時，它會改為使用 HTTP 與所提供的 PKI 憑證。  

 Linux 或 UNIX 用戶端使用 PKI 憑證時不必核准它們。 當用戶端使用自我簽署憑證時，請檢視 Configuration Manager 主控台中階層設定的用戶端核准。 如果用戶端核准方法並不是 **自動核准所有電腦 (不建議)**, ，您必須手動都核准用戶端。  

 如需如何手動核准用戶端的詳細資訊，請參閱 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md) (如何在 System Center Configuration Manager 中管理用戶端) 主題中的 [Manage Clients from the Devices Node](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) (從裝置節點管理用戶端) 一節。  

 如需如何在 Configuration Manager 中使用憑證的資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

###  <a name="BKMK_AboutCertsforLnU"></a> 關於使用 Linux 和 UNIX 伺服器的憑證  
 適用於 Linux 和 UNIX 的 Configuration Manager 用戶端會使用自我簽署憑證或 X.509 PKI 憑證，如同以 Windows 為基礎的用戶端一樣。 管理 Linux 和 UNIX 用戶端時，Configuration Manager 站台系統的 PKI 需求不會有任何變更。  

 您使用於 Linux 和 UNIX 用戶端以跟 Configuration Manager 站台系統通訊的憑證，必須為公開金鑰憑證標準 (PKCS#12) 格式，而且必須知道密碼，才能在指定 PKI 憑證時將此憑證指定至用戶端。  

 適用於 Linux 和 UNIX 的 Configuration Manager 用戶端支援單一的 PKI 憑證，且不支援多個憑證。 因此，不會套用您為 Configuration Manager 站台設定的憑證選擇準則。  

###  <a name="BKMK_ConfigCertsforLnU"></a> 設定憑證以 Linux 和 UNIX 伺服器  
 若要將適用於 Linux 和 UNIX 伺服器的 Configuration Manager 用戶端設定為使用 HTTPS 通訊，您必須在安裝用戶端時，將用戶端設定為使用 PKI 憑證。 您無法佈建之前的用戶端軟體安裝的憑證。  

 當您安裝使用 PKI 憑證的用戶端時，您會使用命令列參數 **-UsePKICert** 指定位置和包含 PKI 憑證的 PKCS #12 檔案的名稱。 此外您必須使用命令列參數 **-certpw** 來指定憑證的密碼。  

 如果您未指定 **-UsePKICert**, ，用戶端會產生自我簽署的憑證並嘗試將站台系統伺服器只使用 HTTP 通訊。  

##  <a name="BKMK_NoSHA-256"></a> 關於 Linux 和 UNIX 作業系統的執行不支援 sha-256  
 下列 Linux 和 UNIX 作業系統作為 Configuration Manager 的用戶端而受到支援，其發行時包含不支援 SHA-256 的 OpenSSL 版本：  

-   Red Hat Enterprise Linux 版本 4 (x86/x64)  

-   Solaris 版本 9 (SPARC) 與 Solaris 10 (SPARC/x86)  

-   SUSE Linux Enterprise Server 9 版 (x86)  

-   HP-UX 版本 11iv2 (PA-RISH/IA64)  

 若要使用 Configuration Manager 管理這些作業系統，您必須安裝適用於 Linux 和 UNIX 的 Configuration Manager 用戶端，且其具有引導用戶端略過 SHA 256 驗證的命令列參數。 在這些作業系統版本上執行的 Configuration Manager 用戶端，其運作模式的安全性比支援 SHA-256 的用戶端低。 這種作業較不安全的模式有下列行為：  

-   用戶端不會驗證它們向管理點要求的原則相關聯的站台伺服器簽章。  

-   用戶端不會驗證它們從發佈點下載的封裝的雜湊。  

> [!IMPORTANT]  
>  **IgnoreSHA256validation** 選項可讓您在較不安全模式中執行適用於 Linux 和 UNIX 電腦用戶端。 這被為了在不含 sha-256 支援的舊平台上使用。 這是安全性覆寫並不建議使用 microsoft 但支援在安全且受信任的資料中心環境中使用。  

 適用於 Linux 和 UNIX 的 Configuration Manager 用戶端進行安裝時，安裝指令碼會檢查作業系統版本。 根據預設，如果作業系統版本被視為發行時不具有支援 SHA-256的 OpenSSL 版本，Configuration Manager 用戶端的安裝作業就會失敗。  

 若要在 Linux 和 UNIX 作業系統上安裝 Configuration Manager 用戶端，而該作業系統在發行時未隨附支援 SHA-256 的 OpenSSL 版本，您就必須使用安裝命令列參數 **ignoreSHA256validation**。 當您在適用的 Linux 或 UNIX 作業系統上使用此命令列選項時，Configuration Manager 用戶端會略過 SHA-256 驗證，且安裝完成後，用戶端不會使用 SHA-256 來簽署其使用 HTTP 提交到站台系統的資料。 如需將 Linux 和 UNIX 的用戶端設定為使用憑證的相關資訊，請參閱本主題中的 [Planning for Security and Certificates for Linux and UNIX Servers](#BKMK_SecurityforLnU) 。 如需 SHA-256 的資訊，請參閱[在 System Center Configuration Manager 中設定安全性](../../../../core/plan-design/security/configure-security.md)主題中的[設定簽署及加密](../../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption)一節。  

> [!NOTE]  
>  在命令列選項 **ignoreSHA256validation** 忽略執行 Linux 和 UNIX 發行的版本與支援 sha-256 OpenSSL 版本的電腦上。  
