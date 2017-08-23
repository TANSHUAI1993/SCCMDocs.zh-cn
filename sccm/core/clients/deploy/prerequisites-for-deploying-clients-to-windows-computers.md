---
title: "Windows 用戶端部署必要條件 | Microsoft Docs"
description: "了解在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦的必要條件。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
caps.latest.revision: "16"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6636ce4d929326fad0210407d7634ea585eb0a2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦的必要條件

*適用於：System Center Configuration Manager (最新分支)*

在環境中部署 Configuration Manager 用戶端會擁有下列外部相依性和產品內的相依性。 此外，每一種用戶端部署方法都有自己的相依性，必須符合這些相依性用戶端安裝才能成功。  

  您同時務必檢閱 [System Center Configuration Manager 的支援設定](../../../core/plan-design/configs/supported-configurations.md)，確認裝置符合 Configuration Manager 用戶端的最低硬體和作業系統需求。  

 如需 Linux 和 UNIX Configuration Manager 用戶端必要條件的資訊，請參閱[在 System Center Configuration Manager 中規劃將用戶端部署至 Linux 和 UNIX 電腦](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)。  

> [!NOTE]  
>  本文章只列出最低需求的軟體版本號碼。  

##  <a name="BKMK_prereqs_computers"></a> 電腦用戶端的必要條件  
 使用下列資訊來判斷在電腦上安裝 Configuration Manager 用戶端時的必要條件。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  

|||  
|-|-|  
|Windows Installer 3.1.4000.2435 版|支援針對套件和軟體更新使用 Windows Installer 更新 (.msp) 檔案所需。|  
|[KB2552033](http://go.microsoft.com/fwlink/p/?LinkId=240048)|啟用用戶端推入安裝時，在執行 Windows Server 2008 R2 的站台伺服器上安裝此 Hotfix。|  
|Microsoft 背景智慧型傳送服務 (BITS) 2.5 版|需要在用戶端電腦和 Configuration Manager 站台系統之間進行節流資料傳送。 BITS 不會在用戶端安裝期間自動下載。 在電腦上安裝 BITS 時，通常需要重新啟動才能完成安裝。<br /><br /> 大部分作業系統都包含 BITS，如果沒有的話 (例如 Windows Server 2003 R2 SP2)，您必須先安裝 BITS，再安裝 Configuration Manager 用戶端。|  
|Microsoft 工作排程器|在用戶端上啟用此服務，以完成用戶端安裝。|  

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a>Configuration Manager 外部的相依性和安裝期間自動下載的相依性  
 Configuration Manager 用戶端可能會有一些外部相依性。 這些相依性取決於用戶端電腦上的作業系統和安裝的軟體。  

 如果完成用戶端安裝時需要這些相依性，則這些相依性會隨用戶端軟體自動安裝。  

|||  
|-|-|  
|Windows Update 代理程式 7.0.6000.363 版|Windows 支援更新偵測和部署所需。|  
|Microsoft Core XML Services (MSXML) 6.20.5002 版和更新版本|支援在 Windows 中處理 XML 文件所需。|  
|Microsoft 遠端差異壓縮 (RDC)|最佳化透過網路的資料傳輸所需。|  
|Microsoft Visual C++ 2013 可轉散發套件 12.0.21005.1 版|支援用戶端操作所需。 用戶端電腦上安裝此更新時，可能需要重新啟動以完成安裝。|  
|Microsoft Visual C++ 2005 可轉散發套件 8.0.50727.42 版|針對 1606 版和更早版本，支援 Microsoft SQL Server Compact 作業所需。|  
|Windows Imaging API 6.0.6001.18000|允許 Configuration Manager 管理 Windows 映像 (.wim) 檔案所需。|  
|Microsoft Policy Platform 1.2.3514.0|允許用戶端評估相容性設定所需。|  
|Microsoft Silverlight 5.1.41212.0 (從 Configuration Manager 1602 版開始)|支援應用程式類別目錄網站使用者經驗所需。|  
|Microsoft .NET Framework 4.5.2 版|支援用戶端操作所需。 如果未安裝 Microsoft .NET Framework 4.5 或更新版本，就會自動安裝在用戶端電腦上。 如需詳細資訊，請參閱 [關於 Microsoft.NET Framework 4.5.2 版的其他詳細資料](#dotNet)。|  
|Microsoft SQL Server Compact 3.5 SP2 元件|儲存用戶端操作相關資訊所需。|  
|Microsoft Windows Imaging 元件|適用於 64 位元電腦的 Windows Server 2003 或 Windows XP SP2 的 Microsoft .NET Framework 4.0 所需。|
|Microsoft Intune 電腦軟體用戶端|您無法在同一部電腦上執行 Intune 電腦軟體用戶端和 Configuration Manager 用戶端。 在安裝 Configuration Manager 用戶端之前，請確定已經移除 Intune 用戶端。|

####  <a name="dotNet"></a> 關於 Microsoft.NET Framework 4.5.2 版的其他詳細資料  

> [!NOTE]  
>  針對 .NET 4.0、4.5 與 4.5.1 的支援已於 2016 年 1 月 12 日到期。 如需詳細資訊，請參閱位於 support.microsoft.com 中的 [週期支援原則常見問題集 - Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) 。  

 可能需要重新開機才能完成安裝 Microsoft .NET Framework 4.5.2 版。 使用者會在系統匣中看到 [需要重新啟動]  的通知。  需要重新啟動用戶端電腦的常見案例：  

-   電腦執行多個 .NET 應用程式或服務。  

-   缺少 .NET 安裝需要的一或多個軟體更新。  

-   電腦還在等待重新啟動前一個安裝的 .NET Framework 軟體更新。  

 安裝好 .NET Framework 4.5.2 之後，或許還要陸續安裝其他的更新，這可能需要另外重新啟動電腦。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  
 如需下列站台系統角色的詳細資訊，請參閱[為 System Center Configuration Manager 用戶端判斷站台系統角色](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)。  

|||  
|-|-|  
|管理點|雖然部署 Configuration Manager 用戶端時不需要管理點，但是您必須要有管理點，才能在用戶端電腦與 Configuration Manager 伺服器之間傳送資訊。 若沒有管理點，就無法管理用戶端電腦。|  
|發佈點|發佈點在用戶端部署中是選用，但是建議使用網站系統角色。 所有發佈點都會裝載用戶端來源檔案，可在用戶端部署期間讓電腦找到最靠近的發佈點來下載用戶端來源檔案。 如果網站沒有發佈點，電腦就會從其管理點下載用戶端來源檔案。|  
|後援狀態點|後援狀態點在用戶端部署中是選用，但是建議使用網站系統角色。 後援狀態點會追蹤用戶端部署，並且在無法與管理點通訊時，讓 Configuration Manager 站台中的電腦傳送狀態訊息。|  
|Reporting Services 點|Reporting Services 點是選用但是建議使用網站系統角色，可顯示與用戶端部署和管理相關的報告。 如需詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。|  

### <a name="installation-method-dependencies"></a>安裝方法相依性  
 以下是各種用戶端安裝方法特定的必要條件。  

-   用戶端推入安裝  

    -   用戶端推入安裝帳戶用來連線至電腦以安裝用戶端，該帳戶是在 [用戶端推入安裝內容]  對話方塊的 [帳戶]  索引標籤上指定。 此帳戶必須是目的地電腦上本機系統管理員群組的成員。  

         如果您未指定用戶端推入安裝帳戶，就會使用網站伺服器電腦帳戶。  

    -   您安裝用戶端所在的電腦必須已經過至少一種 Configuration Manager 探索方法探索。  

    -   電腦擁有 ADMIN$ 共用。  

    -   如果您要將用戶端自動推入探索到的資源中，則必須選取 [用戶端推入安裝內容] 對話方塊中的 [Enable client push installation to assigned resources]\(對指派的資源啟用用戶端推入安裝)。  

    -   用戶端電腦必須能夠連絡發佈點或管理點，以便下載支援的檔案。  

     您必須具有下列安全性權限，才能使用用戶端推入安裝 Configuration Manager 用戶端：  

    -   設定用戶端推送安裝帳戶：[站台]  物件的 [修改]  及讀取權限。  

    -   使用用戶端推送將用戶端安裝到集合、裝置和查詢：集合物件的 [修改資源]  和 [讀取]  權限。  

     [基礎結構系統管理員]  安全性角色包括管理用戶端推入安裝的必要權限。  

-   以軟體更新點為基礎的安裝  

    -   如果 Active Directory 架構尚未擴充，或是您要安裝另一個樹系中的用戶端，則必須使用群組原則將 CCMSetup.exe 的安裝內容佈建至電腦的登錄中。 如需詳細資訊，請參閱  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision)。  

    -   Configuration Manager 用戶端必須發佈到軟體更新點。  

    -   用戶端電腦必須能夠連絡發佈點或管理點，以便下載支援的檔案。  

     如需管理 Configuration Manager 軟體更新所需的安全性權限，請參閱 [System Center Configuration Manager 軟體更新的必要條件](../../../sum/plan-design/prerequisites-for-software-updates.md)。  

-   群組原則為基礎的安裝  

    -   如果 Active Directory 架構尚未擴充，或是您要安裝另一個樹系中的用戶端，則必須使用群組原則將 CCMSetup.exe 的安裝內容佈建至電腦的登錄中。 如需詳細資訊，請參閱  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision)。  

    -   用戶端電腦必須能夠連絡管理點，以便下載支援的檔案。  

-   登入指令碼為基礎的安裝  

     除非您在命令提示字元中以命令列屬性 **ccmsetup /source**指定了 CCMSetup.exe，否則用戶端電腦必須能夠連絡發佈點或管理點，才能下載支援的檔案。  

-   手動安裝  

     除非您在命令提示字元中以命令列屬性 **ccmsetup /source**指定了 CCMSetup.exe，否則用戶端電腦必須能夠連絡發佈點或管理點，才能下載支援的檔案。  

-   工作群組電腦安裝  

     若要存取 Configuration Manager 站台伺服器網域的資源，必須針對該站台設定網路存取帳戶。  

     如需如何設定網路存取帳戶的詳細資訊，請參閱 [System Center Configuration Manager 中的內容管理基本概念](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)。  

-   軟體發佈為基礎的安裝 (僅適用於升級)  

    -   如果 Active Directory 架構尚未擴充，或是您要安裝另一個樹系中的用戶端，則必須使用群組原則將 CCMSetup.exe 的安裝內容佈建至電腦的登錄中。 如需詳細資訊，請參閱 [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision)。  

    -   用戶端電腦必須能夠連絡發佈點或管理點，以便下載支援的檔案。  

     如需使用應用程式管理來升級 Configuration Manager 用戶端所需的安全性權限，請參閱[應用程式管理的安全性與隱私權](../../../apps/plan-design/security-and-privacy-for-application-management.md)。  

-   自動用戶端升級  

     您必須是 [系統高權限管理員]  安全性角色的成員，才能設定自動用戶端升級。  

### <a name="firewall-requirements"></a>防火牆需求  
 如果站台系統伺服器與您要安裝 Configuration Manager 用戶端的電腦之間有防火牆，請參閱 [System Center Configuration Manager 中用戶端適用的 Windows 防火牆和連接埠設定](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md)。  

##  <a name="BKMK_prereqs_mobiledevices"></a> 行動裝置用戶端的必要條件  
 請利用下列資訊判斷在行動裝置上安裝 Configuration Manager 用戶端及使用 Configuration Manager 註冊行動裝置時的必要條件。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  

-   Microsoft 企業憑證授權單位 (CA)，其擁有用於部署及管理行動裝置所需憑證的憑證範本。  

     發行 CA 必須在註冊程序期間自動核准來自行動裝置使用者的憑證要求。  

     如需憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的憑證設定檔安全性和隱私權](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md)。  

-   安全性群組，其中包含可註冊其行動裝置的使用者。  

     此安全性群組用來設定行動裝置註冊期間所使用的憑證範本。  

-   選擇性但建議使用：名為 **ConfigMgrEnroll** 的 DNS 別名 (CNAME 記錄)，針對您要安裝註冊 Proxy 點的站台系統伺服器名稱所設定。  

     此 DNS 別名必須支援註冊服務的自動探索：如果您未設定此 DNS 記錄，使用者就必須在註冊程序中，手動指定註冊 Proxy 點的站台系統伺服器名稱。  

-   將執行註冊點和註冊 Proxy 點網站系統角色之電腦的網站系統角色相依性。  

     請參閱[支援的站台系統伺服器作業系統](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  
 如需下列站台系統角色的詳細資訊，請參閱[為 System Center Configuration Manager 用戶端判斷站台系統角色](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)。  

-   針對 HTTPS 用戶端連線設定且針對行動裝置啟用的管理點。  

     在行動裝置上安裝 Configuration Manager 用戶端時一律需要管理點。 除了 HTTPS 設定需求以及為行動裝置啟用之外，必須使用網際網路 FQDN 設定管理點並接受來自網際網路的用戶端連線。  

-   註冊點和註冊 Proxy 點  

     註冊 Proxy 點會管理來自行動裝置的註冊要求，註冊點則可完成註冊程序。 註冊點必須位於與網站伺服器相同的 Active Directory 樹系集中，但註冊 Proxy 點可以位於另一個樹系中。  

-   行動裝置註冊的用戶端設定  

     設定用戶端設定以允許使用者註冊行動裝置並設定至少一個註冊設定檔。  

-   Reporting Services 點  

     Reporting Services 點是選用服務，但建議使用可顯示行動裝置註冊與用戶端管理相關報告的網站系統角色。  

     如需詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。  

-   若要設定行動裝置的註冊，您必須擁有下列安全性權限：  

    -   加入、修改及刪除註冊站台系統角色：[站台]  物件的 [修改]  權限。  

    -   設定用於註冊的用戶端設定：預設用戶端設定需要 [站台]  物件的 [修改]  權限，自訂用戶端設定則需要 [用戶端代理程式]   權限。  

     [系統高權限管理員]  安全性角色包括設定註冊網站系統角色的必要權限。  

     若要管理已註冊的行動裝置，您必須擁有下列安全性權限：  

    -   抹除或淘汰行動裝置：[集合]  物件的 [刪除資源]  。  

    -   取消抹除或淘汰命令：[集合]  物件的 [刪除資源]  。  

    -   允許及封鎖行動裝置：[集合]  物件的 [修改資源]  。  

    -   遠端鎖定或重設行動裝置的密碼：[集合]  物件的 [修改]  資源。  

     [作業管理員]  安全性角色包括管理行動裝置的必要權限。  

     如需如何設定安全性權限的詳細資訊，請參閱 [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md) 和  [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md)。  

### <a name="firewall-requirements"></a>防火牆需求  
 例如路由器與防火牆以及 Windows Firewall (如適用) 等網路干擾裝置都必須允許與行動裝置註冊相關的流量：  

-   行動裝置與註冊 Proxy 點之間：HTTPS (預設為 TCP 443)  

-   註冊 Proxy 點與註冊點之間：HTTPS (預設為 TCP 443)  

 如果您使用 Proxy 網路伺服器，必須設定伺服器允許 SSL 通道作業；行動裝置不支援 SSL 橋接作業。  
