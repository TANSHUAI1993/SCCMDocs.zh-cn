---
title: "修改基礎結構 | Microsoft Docs"
description: "了解如何變更或採取可影響所部署 Configuration Manager 基礎結構的動作。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
caps.latest.revision: "19"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a5228c4984347be4b115bfa5563791fa2fb7319c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="modify-your-system-center-configuration-manager-infrastructure"></a>修改您的 System Center Configuration Manager 基礎結構

*適用於：System Center Configuration Manager (最新分支)*

安裝一個或多個站台之後，您可能需要修改組態，或採取會影響您部署之基礎結構的動作。  


##  <a name="BKMK_ManageSMSprovider"></a> 管理 SMS 提供者  
 SMS 提供者 (動態連結程式庫檔案：smsprov.dll) 會提供一個或多個 Configuration Manager 主控台的系統管理連絡點。 當您安裝多重 SMS 提供者時，可提供連絡點複本以管理站台和階層。  

 在每個 Configuration Manager 站台上，您可以重新執行安裝程式，進而執行下列程序：  

-   新增 SMS 提供者的其他執行個體 (每個 SMS 提供者的其他執行個體必須位於個別的電腦上)  

-   移除 SMS 提供者的執行個體 (若要移除站台的最後一個 SMS 提供者，您必須解除安裝站台)  

 您可以在執行安裝程式的站台伺服器根資料夾中檢視 ConfigMgrSetup.log  ，以監視 SMS 提供者的安裝或移除。  

 在修改站台上的 SMS 提供者之前，請先熟悉[規劃 System Center Configuration Manager 的 SMS 提供者](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)中的資訊。  

#### <a name="to-manage-the-sms-provider-configuration-for-a-site"></a>管理站台的 SMS 提供者設定  

1.  從 **&lt;Configuration Manager 站台安裝資料夾\>\BIN\X64\setup.exe** 執行「Configuration Manager 安裝程式」。  

2.  在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台] ，然後按 [下一步]   

3.  在 [站台維護]  頁面上，選取 [修改 SMS 提供者設定] ，然後按 [下一步] 。  

4.  在 [管理 SMS 提供者]  頁面上，選取下列其中一個選項，並使用下列其中一個選項完成精靈：  

    -   若要在此站台新增其他 SMS 提供者：  

         選取 [新增 SMS 提供者] ，指定將裝載 SMS 提供者且目前未裝載 SMS 提供者的電腦 FQDN，然後按 [下一步] 。  

    -   若要從伺服器移除 SMS 提供者：  

         選取 [解除安裝指定的 SMS 提供者] ，選取您要移除 SMS 提供者的電腦名稱，然後按 [下一步] ，然後確認動作。  

        > [!TIP]  
        >  若要移除兩部電腦間的 SMS 提供者，您必須將 SMS 提供者安裝到新電腦，然後從原始位置移除 SMS 提供者。 目前在單一程序中，沒有可以在電腦間移動 SMS 提供者的專用選項。  

 安裝精靈完成後，就會完成 SMS 提供者設定。 在站台 [內容]  對話方塊的 [一般]  索引標籤上，您可以確認是否有已為站台安裝 SMS 提供者的電腦。  

##  <a name="bkmk_Console"></a> 管理 Configuration Manager 主控台  
 以下是您可以執行來管理 Configuration Manager 主控台的工作：  

-   **修改 Configuration Manager 主控台中顯示的語言** - 若要修改已安裝的語言，請參閱本主題中的[管理 Configuration Manager 主控台語言](#BKMK_ManageConsoleLanguages)。  

-   **安裝其他主控台** - 若要安裝其他主控台，請參閱[安裝 System Center Configuration Manager 主控台](/sccm/core/servers/deploy/install/install-consoles)。  

-   **設定 DCOM** - 若要設定 DCOM 權限，以讓該站台伺服器的遠端主控台進行連線，請參閱本主題中的[設定遠端 Configuration Manager 主控台的 DCOM 權限](#BKMK_ConfigDCOMforRemoteConsole)。  

-   **修改權限來限制系統管理使用者可以在主控台中查看哪些項目** - 若要修改系統管理權限，限制使用者可以在主控台中查看並執行的項目，請參閱[修改系統管理使用者的系統管理範圍](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_ModAdminUser)。     

###  <a name="BKMK_ManageConsoleLanguages"></a> 管理 Configuration Manager 主控台語言  
 在站台伺服器安裝期間，Configuration Manager 主控台安裝檔案和站台的支援語言套件，皆會複製到站台伺服器上的 **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup** 子資料夾。  

-   當您從站台伺服器的這個資料夾啟動 Configuration Manager 主控台安裝時，Configuration Manager 主控台和支援的語言套件檔案皆會複製到電腦  

-   當語言套件可供電腦上的目前語言設定使用時，Configuration Manager 主控台會以該語言開啟  

-   如果 Configuration Manager 主控台無法使用相關聯的語言套件，則主控台便會以英文開啟  

例如，從支援英文、德文與法文的站台伺服器安裝 Configuration Manager 主控台的案例。 如果您在設定之語言設定為法文的電腦上開啟 Configuration Manager 主控台，主控台會以法文開啟。 如果您在設定之語言設定為日文的電腦上開啟 Configuration Manager 主控台，則主控台會以英文開啟，因為未提供日文語言套件。  

 每次開啟 Configuration Manager 主控台時，主控台會判斷電腦已設定的語言設定，確認 Configuration Manager 主控台是否有相關聯的語言套件可用，然後使用適當的語言套件開啟主控台。 如果您想要以英文開啟 Configuration Manager 主控台，則無論電腦上已設定的語言設定為何，都必須手動移除或重新命名電腦上的語言套件檔案。  

 無論電腦上已設定的地區設定為何，都可使用下列程序以英文啟動 Configuration Manager 主控台。  

##### <a name="to-install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>在電腦上安裝僅英文版的 Configuration Manager 主控台  

1.  在 Windows 檔案總管中，瀏覽至 **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup\LanguagePack**  

2.  重新命名 **.msp** 和 **.mst** 檔案。 例如，您可以將 **&lt;檔案名稱\>.MSP** 變更為 **&lt;檔案名稱\>.MSP.disabled**。  

3.  在電腦上安裝 Configuration Manager 主控台。  

    > [!IMPORTANT]  
    >  為站台伺服器設定新的伺服器語言時，會將 .msp 與 .mst 檔案重新複製到 **LanguagePack** 資料夾，而您必須重複此程序，僅以英文安裝新的 Configuration Manager 主控台。  

##### <a name="to-temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>在現有 Configuration Manager 主控台安裝時暫時停用主控台語言  

1.  在執行 Configuration Manager 主控台的電腦上，關閉 Configuration Manager 主控台。  

2.  在 Windows 檔案總管中，瀏覽至 Configuration Manager 主控台電腦上的 &lt;*ConsoleInstallationPath*>\Bin\。  

3.  針對電腦上已設定的語言，重新命名適當的語言資料夾。 例如，若電腦的語言設定已設為德文，您可以將 [de]  資料夾重新命名為 [de.disabled] 。  

4.  若要以為電腦設定的語言開啟 Configuration Manager 主控台，請將資料夾重新命名為原始名稱。 例如，將 [de.disabled]  重新命名為 [de] 。  

##  <a name="BKMK_ConfigDCOMforRemoteConsole"></a> 設定遠端 Configuration Manager 主控台的 DCOM 權限  
 執行 Configuration Manager 主控台的使用者帳戶，需要擁有可以使用 SMS 提供者存取站台資料庫的權限。 不過，使用遠端 Configuration Manager 主控台的系統管理使用者，在下列電腦上也需要 [遠端啟用] DCOM 權限：  

-   網站伺服器電腦  

-   裝載 SMS 提供者執行個體的每部電腦  

 名為 **SMS Admins** 的安全性群組，會授與在電腦上存取 SMS 提供者的權限，也可用於授與必要的 DCOM 權限。 (當 SMS 提供者在成員伺服器上執行時，此群組位於電腦本機，而當 SMS 提供者在網域控制站上執行時，此群組便會是網域本機群組。)  

> [!IMPORTANT]  
>  Configuration Manager 主控台會使用 Windows Management Instrumentation (WMI) 連線到 SMS 提供者，而 WMI 內部則會使用 DCOM。 因此，如果 Configuration Manager 主控台在與 SMS 提供者電腦不同的電腦上執行，則 Configuration Manager 需要權限才能在 SMS 提供者電腦上啟動 DCOM 伺服器。 根據預設，遠端啟用只會授與內建 Administrators 群組的成員。 如果您允許 SMS Admins 群組擁有遠端啟用權限，此群組的成員可能會對 SMS 提供者電腦進行 DCOM 攻擊。 此設定也會增加電腦的攻擊面。 若要減輕威脅，請仔細監視 SMS Admins 群組的成員資格。  

 使用下列程序，設定各管理中心網站、主要站台伺服器，以及安裝 SMS 提供者的電腦，以授與系統管理使用者遠端 Configuration Manager 主控台存取權。  

#### <a name="to-configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>設定遠端 Configuration Manager 主控台連線的 DCOM 權限  

1.  執行  **Dcomcnfg.exe** 以開啟 [元件服務] 。  

2.  在 **[元件服務]**中，按一下 **[主控台根目錄]** >  **[元件服務]** > **[電腦]**，然後按一下 **[我的電腦]**中的資訊。 在 [動作]  功能表上，按一下 [內容] 。  

3.  在 [我的電腦內容]  對話方塊的 [COM 安全性]  索引標籤上，按一下 [啟動和啟用權限]  區段中的 [編輯限制] 。  

4.  在 [啟動和啟用權限]  對話方塊中，按一下 [新增] 。  

5.  在 [選取使用者、電腦、服務帳戶或群組]  對話方塊的 [輸入要選取的物件名稱 (範例)]  方塊中，輸入 **SMS Admins**，然後按一下 [確定] 。  

    > [!NOTE]  
    >  您可能必須變更 [從這個位置]  的設定，才能找到 SMS Admins 群組。 當 SMS 提供者在成員伺服器上執行時，此群組位於電腦本機，而當 SMS 提供者在網域控制站上執行時，此群組便會是網域本機群組。  

6.  在 [SMS Admins 的權限]  區段中，若要允許遠端啟用，請選取 [遠端啟用]  核取方塊。  

7.  按一下 [確定]  後再按一次 [確定]  ，然後關閉 [電腦管理] 。 您的電腦現在已設定為允許遠端 Configuration Manager 主控台存取 SMS Admins 群組的成員。  

 在每一部可能會支援遠端 Configuration Manager 主控台的 SMS 提供者電腦上，重複執行此程序。  

##  <a name="bkmk_dbconfig"></a> 修改站台資料庫組態  
 安裝某個站台後，您可以經由在管理中心網站伺服器或主要站台伺服器上執行安裝程式，來修改站台資料庫和站台資料庫伺服器的設定。 您可以將站台資料庫移到相同電腦上的 SQL Server 新執行個體，或移到執行受支援 SQL Server 版本的另一台電腦上。 次要站台資料庫設定不支援這些變更及相關的變更。  

 如需支援限制的詳細資訊，請參閱 [Support policy for manual database changes in a Configuration Manager environment](https://support.microsoft.com/kb/3106512)(在 Configuration Manager 環境中手動變更資料庫的支援原則)。  

> [!NOTE]  
>  修改站台的資料庫設定時，Configuration Manager 會在與資料庫通訊的站台伺服器和遠端站台系統伺服器上，重新啟動或重新安裝 Configuration Manager 服務。  

**若要修改資料庫組態**，您必須在站台伺服器上執行安裝程式，並選取 [執行站台維護或重設此站台] 選項。 接著，選取 [修改 SQL Server 設定]  選項 您可以變更以下站台資料庫設定：  

-   裝載資料庫的 Windows 伺服器。  

-   在裝載 SQL Server 資料庫的伺服器上使用的 SQL Server 執行個體。  

-   資料庫名稱。  

-   Configuration Manager 正在使用 SQL Server 連接埠  

-   Configuration Manager 正在使用 SQL Server Service Broker 連接埠  

**如果您移動站台資料庫，就必須設定以下項目：**  

-   **設定存取權：** 將站台資料庫移到新電腦時，請將站台伺服器的電腦帳戶新增至執行 SQL Server 之電腦上的 [本機系統管理者]  群組。 如果您使用站台資料庫的 SQL Server 叢集，則必須將電腦帳戶新增至每個 Windows Server 叢集節點電腦的 [本機系統管理者]  群組。  

-   **啟用 Common Language Runtime (CLR) 整合：**  將資料庫移到 SQL Server 上的新執行個體，或移到新的 SQL Server 電腦時，您必須啟用 Common Language Runtime (CLR) 整合。 若要啟用 CLR，請使用 **SQL Server Management Studio** 連線到裝載站台資料庫的 SQL Server 執行個體，並以查詢方式執行以下預存程序：**sp_configure 'clr enabled',1; reconfigure**。  
-  **確認新的 SQL Server 可存取備份位置：**將資料庫移至新的伺服器 (包括移動 SQL Server AlwaysOn 可用性群組或移至 SQL Server 叢集) 之後，若要使用 UNC 儲存站台資料庫備份，請確定新的 SQL Server 電腦帳戶具有**寫入** UNC 位置的權限。  


> [!IMPORTANT]  
>  移動管理點有一或多個資料庫複本的資料庫時，必須先移除資料庫複本。 完成資料庫移動後，就可以重新設定資料庫複本。 如需詳細資訊，請參閱 [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

##  <a name="bkmk_SPN"></a> 管理站台資料庫伺服器的 SPN  
您可以選擇執行該站台資料庫之 SQL 服務的帳戶：  

-   若該服務使用電腦系統帳戶執行，將會自動為您登錄 SPN。  

-   若該服務使用網域本機使用者帳戶執行，您就必須手動註冊 SPN，以確保 SQL 用戶端和其他站台系統可以執行 Kerberos 驗證。 若無 Kerberos 驗證，與資料庫的通訊可能會失敗。  

SQL Server 文件可協助您 [手動註冊 SPN](https://technet.microsoft.com/library/ms191153\(v=sql.120\).aspx)，並提供有關 SPN 和 Kerberos 連接的其他背景資訊。  

> [!IMPORTANT]  
>  -   建立叢集 SQL Server 的 SPN 時，必須指定 SQL Server 叢集的虛擬名稱，作為 SQL Server 電腦名稱  
> -   註冊 SQL Server 具名執行個體之 SPN 的命令，與您註冊預設執行個體的 SPN 時所使用的相同，不同的是連接埠號碼必須與具名執行個體所使用的連接埠相符。  

您可以使用 **Setspn** 工具註冊站台資料庫伺服器的 SQL Server 服務帳戶 SPN。 您必須在 SQL Server 網域的電腦上執行 Setspn 工具，且必須使用網域系統管理員認證執行。  

 請使用以下程序作為如何管理在 Windows Server 2008 R2 上使用 Setspn 工具之 SQL Server 服務帳戶 SPN 的範例。 如需 Setspn 的特定指南，請參閱 [Setspn Overview (Setspn 概觀)](http://go.microsoft.com/fwlink/p/?LinkId=226343)，或您的作業系統特定的類似說明文件。  

> [!NOTE]  
>  以下程序參照 Setspn 命令列工具。 從產品光碟或 [Microsoft Download Center (Microsoft 下載中心)](http://go.microsoft.com/fwlink/p/?LinkId=100114)安裝 Windows Server 2003 支援工具時，會包含 Setspn 命令列工具。 如需如何從產品光碟安裝 Windows 支援工具的詳細資訊，請參閱 [安裝 Windows 支援工具](http://go.microsoft.com/fwlink/p/?LinkId=62270)。  

#### <a name="to-manually-create-a-domain-user-service-principal-name-spn-for-the-sql-server-service-account"></a>手動建立 SQL Server 服務帳戶的網域使用者服務主體名稱 (SPN)  

1.  在 [開始]  功能表上按一下 [執行] ，然後在 [執行] 對話方塊內輸入 cmd  。  

2.  於命令列瀏覽至 Windows Server 支援工具安裝目錄。 根據預設，這些工具均位於 **C:\Program Files\Support Tools** 目錄。  

3.  輸入有效命令來建立 SPN。 若要建立 SPN，您可以使用執行 SQL Server 之電腦的 NetBIOS 名稱或完整網域名稱 (FQDN)。 不過，您必須為 NetBIOS 名稱和 FQDN 建立一個 SPN。  

    > [!IMPORTANT]  
    >  建立叢集 SQL Server 的 SPN 時，必須指定 SQL Server 叢集的虛擬名稱，作為 SQL Server 電腦名稱。  

    -   若要建立 SQL Server 電腦之 NetBIOS 名稱的 SPN，請輸入以下命令：**setspn -A MSSQLSvc/&lt;SQL Server 電腦名稱\>:1433 &lt;網域\帳戶>**  

    -   若要建立 SQL Server 電腦之 FQDN 的 SPN，請輸入以下命令：**setspn -A MSSQLSvc/&lt;SQL Server FQDN\>:1433 &lt;網域\帳戶>**  

    > [!NOTE]  
    >  註冊 SQL Server 具名執行個體之 SPN 的命令與您註冊預設執行個體的 SPN 時所使用的相同，不同的是連接埠號碼必須與具名執行個體所使用的連接埠相符。  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-by-using-the-setspn-command"></a>使用 Setspn 命令確認網域使用者 SPN 是否正確註冊  

1.  在 [開始]  功能表上按一下 [執行] ，然後在 [執行]  對話方塊內輸入 cmd  。  

2.  在命令提示字元中輸入以下命令：**setspn -L &lt;網域\SQL 服務帳戶>**。  

3.  檢閱註冊的 ServicePrincipalName  ，以確保已經為 SQL Server 建立有效的 SPN。  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-when-using-the-adsiedit-mmc-console"></a>使用 ADSIEdit MMC 主控台時確認網域使用者 SPN 是否正確註冊  

1.  在 [開始]  功能表上按一下 [執行] ，然後輸入 adsiedit.msc  以啟動 ADSIEdit MMC 主控台。  

2.  如有必要，請連線至站台伺服器的網域。  

3.  在主控台窗格中，依序展開站台伺服器的網域、[DC=&lt;伺服器辨別名稱\>] 和 [CN=使用者]，並以滑鼠右鍵按一下 [CN=&lt;服務帳戶使用者\>]，然後按一下 [內容]。  

4.  在 [CN=&lt;服務帳戶使用者\> 內容] 對話方塊中，檢閱 **servicePrincipalName** 值，以確保已建立有效 SPN，且與正確的 SQL Server 電腦相關聯。  

#### <a name="to-change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>將 SQL Server 服務帳戶從本機系統變更至網域使用者帳戶  

1.  建立或選取您要用作 SQL Server 服務帳戶的網域或本機系統使用者帳戶。  

2.  開啟 [SQL Server 組態管理員] 。  

3.  按一下 [SQL Server 服務]，然後連按兩下 [SQL Server&lt;執行個體名稱\>]。  

4.  在 [登入]  索引標籤上選取 [此帳戶] ，然後輸入在步驟 1 建立之網域使用者帳戶的使用者名稱和密碼，或按一下 [瀏覽]  找出 Active Directory 網域服務中的使用者帳戶，然後按一下 [套用] 。  

5.  在 [確認帳戶變更]  對話方塊中按一下 [是]  ，確認服務帳戶變更，並重新啟動 SQL Service 服務。  

6.  成功變更服務帳戶後，按一下 [確定]  。  

##  <a name="bkmk_reset"></a> 執行站台重設  
 當重設的站台在管理中心網站或主要站台執行時，此站台：  

-   重新套用預設 Configuration Manager 檔案和登錄權限  

-   重新安裝該站台上所有站台元件和所有站台系統角色  

次要站台不支援站台重設。  

您可以選擇手動執行站台重設，但也可以在修改站台組態之後自動執行。  

例如，如果已使用 Configuration Manager 元件變更帳戶，您應該考慮手動站台重設，以確保站台元件更新為使用新的帳戶詳細資料。 但是，如果您修改該站台上的用戶端或伺服器語言，因為需要先重設，站台才能使用此變更，所以 Configuration Manager 會自動執行站台重設。  

> [!NOTE]  
>  站台重設並不會重設非 Configuration Manager 物件的存取權限。  

當站台重設執行時：  

1.  會停止安裝程式，並重新啟動 [SMS_SITE_COMPONENT_MANAGER]  服務與 [SMS_EXECUTIVE]  服務的執行緒元件。  

2.  安裝程式會移除然後重新建立，本機電腦和遠端站台系統電腦上的站台系統共用資料夾和 [SMS Executive]  元件。  

3.  安裝程式重新啟動 [SMS_SITE_COMPONENT_MANAGER]  服務後，此服務會安裝 [SMS_EXECUTIVE]  和 [SMS_SQL_MONITOR]  服務  

此外，站台重設會還原以下物件：  

-   [SMS]  或 [NAL]  登錄機碼，以及這些機碼下的任何預設子機碼。  

-   Configuration Manager 檔案目錄樹狀結構，以及此檔案目錄樹狀結構中的任何預設檔案或子目錄。  

**執行站台重設的必要條件**  

用於執行站台重設的帳戶必須具備下列權限：  

-   用於執行站台重設的帳戶必須具備下列權限：  

    -   **管理中心網站**：您在此站台執行站台重設的帳戶必須是管理中心網站上的本機系統管理員，而且必須和以 [系統高權限管理員]  角色為基礎的系統管理安全性角色具備對等的權限。  

    -   **主要站台**：您在此站台執行站台重設的帳戶必須是主要站台伺服器上的本機系統管理員，而且必須和以 [系統高權限管理員]  角色為基礎的系統管理安全性角色具備對等的權限。 如果主要站台位於管理中心網站階層中，則此帳戶也必須是該管理中心網站站台伺服器上的本機系統管理員。  

**站台重設的限制**
  - 從 1602 版開始，您就無法使用站台重設來變更站台上所安裝的伺服器或用戶端語言套件，只要階層設定成支援[測試進入生產階段前集合中的用戶端升級](/sccm/core/clients/manage/upgrade/test-client-upgrades)。

#### <a name="to-perform-a-site-reset"></a>執行站台重設  

1.  從 **&lt;Configuration Manager 站台安裝資料夾\>\BIN\X64\setup.exe** 執行「Configuration Manager 安裝程式」。  

    > [!TIP]  
    >  您也可以在站台伺服器電腦的 [開始] 功能表或 Configuration Manager 來源媒體上啟動 Configuration Manager 安裝程式，執行站台重設。  

2.  在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台] ，然後按 [下一步] 。  

3.  在 [站台維護]  頁面上，選取 [在不變更設定的情況下重設站台] ，然後按 [下一步] 。  

4.  按一下 [是]  開始站台重設。  

完成站台重設後，按一下 [關閉]  完成此程序。  

##  <a name="bkmk_sitelang"></a> 管理站台的語言套件  
在站台安裝之後，您可以變更正在使用中的伺服器和用戶端語言套件：  

**伺服器語言套件：**  

-   **適用於：**  

     Configuration Manager 主控台安裝  

     適用站台系統角色的新安裝  

-   **詳細資料:**  

     更新站台上的伺服器語言套件後，可以將語言套件支援新增至 Configuration Manager 主控台。  

     若要將伺服器語言套件支援新增至 Configuration Manager 主控台，必須從站台伺服器的 **ConsoleSetup** 資料夾 (其中包含您要使用的語言套件) 安裝 Configuration Manager 主控台。 如果已安裝 Configuration Manager 主控台，必須先解除安裝，新的安裝程式才能識別目前可支援的語言套件清單。  

**用戶端語言套件：**  

-   **適用於：**  

     變更用戶端語言套件會更新用戶端安裝來源檔案，使新用戶端安裝和升級新增用戶端語言更新的清單支援。  

-   **詳細資料:**  

     更新站台上的用戶端語言套件後，必須使用包含用戶端語言套件的來源檔案安裝每個將使用這些語言套件的用戶端。  

如需 Configuration Manager 所支援用戶端和伺服器語言的相關資訊，請參閱 [System Center Configuration Manager 中的語言套件](../../../core/servers/deploy/install/language-packs.md)。  

#### <a name="to-modify-the-language-packs-that-are-supported-at-a-site"></a>修改站台支援的語言套件  

1.  在站台伺服器上，從 **&lt;Configuration Manager 站台安裝資料夾\>\BIN\X64\setup.exe** 執行 Configuration Manager 安裝程式。  

2.  在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台] ，然後按 [下一步] 。  

3.  在 [站台維護]  頁面上，選取 [修改語言設定] ，然後按 [下一步] 。  

4.  在 [必要條件下載]  頁面中，選取 [下載必要檔案]  以取得語言套件的更新，或者選取 [使用先前下載的檔案]  ，使用先前下載的檔案 (檔案中包含您要新增至站台的語言套件)。 按 [下一步]  驗證檔案並繼續。  

5.  在 [伺服器語言選擇]  頁面中，選取此站台支援之伺服器語言的核取方塊，然後按 [下一步] 。  

6.  在 [用戶端語言選擇]  頁面中，選取此站台支援之用戶端語言的核取方塊，然後按 [下一步] 。  

7.  按 [下一步] 修改該站台支援的語言。  

    > [!NOTE]  
    >  Configuration Manager 會起始站台重設，同時重新安裝站台上的所有站台系統角色。  

8.  按一下 [關閉]  完成此程序。  

##  <a name="BKMK_ModDBAlert"></a> 修改資料庫伺服器警示閾值  
 根據預設，Configuration Manager 會在站台資料庫伺服器的可用磁碟空間變少時產生警示。 預設設定為當可用磁碟空間在 10 GB 或以下時產生警告，而可用磁碟空間在 5 GB 或以下，則產生重大警示。 您可以針對每個網站修改這些值或是停用警示。  

 若要變更這些設定：  

1.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。  

2.  選取您要設定的站台，然後開啟該站台的 [內容]。  

3.  在站台的 [內容] 對話方塊中，選取 [警示] 索引標籤，然後編輯設定。  

4.  按一下 [確定]  以關閉網站 [內容] 對話方塊。  
