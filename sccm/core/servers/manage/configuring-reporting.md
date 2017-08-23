---
title: "設定報告 | Microsoft Docs"
description: "了解如何在 Configuration Manager 階層中設定報告，包括 SQL Server Reporting Services 的相關資訊。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
caps.latest.revision: "6"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 7ae6bac23e585d6f61aff0f3155d050f1b537620
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configuring-reporting-in-system-center-configuration-manager"></a>設定 System Center Configuration Manager 中的報表

*適用對象：System Center Configuration Manager (最新分支)*

您必須先執行一些設定工作，才能在 System Center Configuration Manager 主控台建立、修改和執行報告。 使用本主題中的以下各節，協助您在 Configuration Manager 階層中設定報告：  

 請先檢閱下列 Configuration Manager 報告主題，再繼續於階層中安裝及設定 Reporting Services：  

-   [System Center Configuration Manager 的報告簡介](../../../core/servers/manage/introduction-to-reporting.md)  

-   [System Center Configuration Manager 中的報告規劃](../../../core/servers/manage/planning-for-reporting.md)  

##  <a name="BKMK_SQLReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services 是一個以伺服器為基礎的報告平台，可針對各種資料來源提供完整的報告功能。 在 Configuration Manager 與 SQL Server Reporting Services 通訊的 Reporting Services 點中，將 Configuration Manager 報告複製到指定的報告資料夾、進行 Reporting Services 設定，以及進行 Reporting Services 安全性設定。 Reporting Services 會連線至 Configuration Manager 站台資料庫，以擷取當您執行報告時傳回的資料。  

 您必須先在裝載 Reporting Service 點站台系統角色的站台系統上安裝及設定 SQL Server Reporting Services，才能在 Configuration Manager 站台中安裝 Reporting Services 點。 如需有關安裝 Reporting Services 的資訊，請參閱 [SQL Server TechNet 技術文件庫](http://go.microsoft.com/fwlink/p/?LinkId=266389)。  

 使用下列程序，確認是否已安裝及正確執行 SQL Server Reporting Services。  

#### <a name="to-verify-that-sql-server-reporting-services-is-installed-and-running"></a>確認已安裝及執行 SQL Server Reporting Services  

1.  在桌面上，依序按一下 [開始] 、[所有程式] 、[Microsoft SQL Server 2008 R2] 、[組態工具] 和 [Reporting Services 組態管理員] 。  

2.  在 [Reporting Services 組態連接]  對話方塊中，指定裝載 SQL Server Reporting Services 的伺服器名稱，並在功能表上選取已安裝 SQL Reporting Services 的 SQL Server 執行個體，然後按一下 [連線] 。 此時會開啟 [Reporting Services 組態管理員]。  

3.  在 [報表伺服器狀態]  頁面上，確認 [報告服務狀態]  設定為 [已啟動] 。 如果不是，請按一下 [啟動] 。  

4.  在 [Web 服務 URL]  頁面上，按一下 [報表服務 Web 服務 URL]  中的 URL，測試與報告資料夾的連線。 此時可能會開啟 [Windows 安全性]  對話方塊，提示您輸入安全性認證。 預設會顯示您的使用者帳戶。 輸入您的密碼，按一下 [確定] 。 確認已順利開啟該網頁。 關閉瀏覽器視窗。  

5.  在 [資料庫]  頁面上，確認已使用 [原生]  設定 [報表伺服器模式] 設定。  

6.  在 [報表管理員 URL]  頁面上，按一下 [報表管理員網站識別]  中的 URL，測試與報表管理員虛擬目錄的連線。 此時可能會開啟 [Windows 安全性]  對話方塊，提示您輸入安全性認證。 預設會顯示您的使用者帳戶。 輸入您的密碼，按一下 [確定] 。 確認已順利開啟該網頁。 關閉瀏覽器視窗。  

    > [!NOTE]  
    >  Configuration Manager 中的報告不需要使用 Reporting Services 報表管理員，但如果您要在網際網路瀏覽器上執行報告，或使用報表管理員管理報告，則需要使用它。  

7.  按一下 [結束] 關閉 Reporting Services Configuration Manager。  

##  <a name="BKMK_ReportBuilder3"></a> 設定報表以使用 Report Builder 3.0  

#### <a name="to-change-the-report-builder-manifest-name-to-report-builder-30"></a>將報告產生器資訊清單名稱變更為 Report Builder 3.0  

1.  在執行 Configuration Manager 主控台的電腦上，開啟 Windows 登錄編輯程式。  

2.  瀏覽至 **HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting**。  

3.  按兩下 **ReportBuilderApplicationManifestName** 機碼以編輯值資料。  

4.  將 [ReportBuilder_2_0_0_0.application]  變更為 [ReportBuilder_3_0_0_0.application] ，然後按一下 [確定] 。  

5.  關閉 Windows 登錄編輯程式。  

##  <a name="BKMK_InstallReportingServicesPoint"></a> 安裝 Reporting Services 點  
 必須在站台上安裝 Reporting Services 點，才能在站台管理報告。 Reporting Services 點會將報告資料夾和報告複製到 SQL Server Reporting Services、為報告和資料夾套用安全性原則，以及在 Reporting Services 中設定組態設定。 您必須先設定 Reporting Services 點，才能讓報告顯示在 Configuration Manager 主控台中，以及在 Configuration Manager 中管理報告。 Reporting Services 點是必須伺服器上以安裝並執行之 Microsoft SQL Server Reporting Services 進行設定的站台系統角色。 如需必要條件的詳細資訊，請參閱 [Configuration Manager 中的報表必要條件](prerequisites-for-reporting.md)。  

> [!IMPORTANT]  
>  選取站台以安裝 Reporting Services 點時，請注意，存取報告的使用者所在的安全性範圍，必須與安裝 Reporting Services 點的站台相同。  

> [!NOTE]  
>  在您於站台伺服器上安裝 Reporting Services 點之後，請勿變更報告伺服器的 URL。 例如，若您建立了 Reporting Services 點，然後在 Reporting Services 組態管理員中修改報表伺服器的 URL，則 Configuration Manager 主控台將會繼續使用舊的 URL，而您將無法從主控台執行、編輯或建立報告。 當您必須變更 URL 報告伺服器時，請先移除 Reporting Services 點、變更 URL，然後重新安裝 Reporting Services 點。  

> [!IMPORTANT]    
> 當您安裝 Reporting Services 點時，必須指定 Reporting Services 點帳戶。 之後，當不同網域的使用者嘗試執行報告時，除非在網域之間建立雙向信任，否則報告將會無法執行。

 利用下列程序安裝 Reporting Services 點。  

#### <a name="to-install-the-reporting-services-point-on-a-site-system"></a>在站台系統上安裝 Reporting Services 點  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [伺服器和網站系統角色] 。  

    > [!TIP]  
    >  若只要列出裝載 Reporting Services 點站台角色的站台系統，請以滑鼠右鍵按一下 [伺服器和站台系統角色]  選取 [Reporting Services 點] 。  

3.  使用相關的步驟，將 Reporting Services 點站台系統角色新增至新的或現有的站台系統伺服器：  

    > [!NOTE]  
    >  如需設定站台系統的詳細資訊，請參閱 [Add site system roles for System Center Configuration Manager](../deploy/configure/add-site-system-roles.md) (為 System Center Configuration Manager 新增站台系統角色)。  

    -   **新增站台系統伺服器**：在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立站台系統伺服器] 。 隨即開啟 [建立站台系統伺服器精靈]  。  

    -   **現有站台系統**：在要安裝 Reporting Services 點站台系統角色的伺服器上按一下。 按一下伺服器時，就會在結果窗格中顯示已經安裝在該伺服器上的網站系統角色清單。  

         在 [首頁]  索引標籤的 [伺服器]  群組中，按一下 [新增網站系統角色] 。 隨即開啟 [新增站台系統角色精靈]  。  

4.  在 [一般]  頁面上，指定網站系統伺服器的一般設定。 將 Reporting Services 點新增到現有的站台系統伺服器時，請確認您之前設定的值。  

5.  在 [系統角色選取]  頁面上，在可用角色的清單中選取 [Reporting Services 點]  ，然後按 [下一步] 。  

6.  在 [Reporting Services 點]  頁面上，設定下列設定：  

    -   **站台資料庫伺服器名稱**：指定裝載 Configuration Manager 站台資料庫的伺服器名稱。 通常，精靈會自動擷取伺服器的完整網域名稱 (FQDN)。 若要指定資料庫執行個體，請使用 &lt;伺服器名稱>\&lt;執行個體名稱> 的格式。  

    -   **資料庫名稱**：指定 Configuration Manager 站台資料庫名稱，然後按一下 [驗證]，確認精靈可存取站台資料庫。  

        > [!IMPORTANT]  
        >  建立 Reporting Services 點的使用者帳戶，必須擁有站台資料庫的 **讀取** 權限。 如果連線測試失敗，則會顯示紅色警告圖示。 將游標移至此圖示上方，即可讀取失敗的詳細資料。 更正錯誤，然後再按一下 [測試]  。  

    -   **資料夾名稱**：指定在 Reporting Services 中所建立以及用於裝載 Configuration Manager 報告的資料夾名稱。  

    -   **Reporting Services 伺服器執行個體**：在清單中選取 Reporting Services 的 SQL Server 執行個體。 根據預設，如果只有找到一個執行個體，則會列出並選取該執行個體。 如果找不到執行個體，請確認已安裝且設定 SQL Server Reporting Services，而且已在站台系統啟動 SQL Server Reporting Services 服務。  

        > [!IMPORTANT]  
        >  Configuration Manager 會在目前使用者的內容中，建立與所選站台系統之 Windows Management Instrumentation (WMI) 的連線，以擷取 Reporting Services 的 SQL Server 執行個體。 目前的使用者必須擁有站台系統上 WMI 的 **讀取** 權限，否則會無法擷取 Reporting Services 執行個體。  

    -   **Reporting Services 點帳戶**：按一下 [設定]，然後選取 Reporting Services 點上的 SQL Server Reporting Services 連線到 Configuration Manager 站台資料庫時，用以擷取顯示在報告中資料的帳戶。 選取 [現有的帳戶] 以指定之前設定為 Configuration Manager 帳戶的 Windows 使用者帳戶，或選取 [新增帳戶] 以指定目前未設定為 Configuration Manager 帳戶的 Windows 使用者帳戶。 Configuration Manager 會自動授與指定之使用者存取站台資料庫的權限。 顯示在 [系統管理]  工作區中 [安全性]  節點之 [帳戶]  子資料夾中的使用者，具有 [ConfigMgr Reporting Services 點]  帳戶名稱。  

         執行 Reporting Services 的帳戶必須隸屬於網域本機安全性群組 [Windows Authorization Access Group] ，且將 [Read tokenGroupsGlobalAndUniversal]  權限設定為 [允許] 。 除了 Reporting Servicies 點帳戶之外，還必須為來自不同網域的使用者建立雙向信任，才能成功執行報告。

         指定的 Windows 使用者帳戶和密碼會經過加密，並儲存於 Reporting Services 資料庫中。 Reporting Services 會使用此帳戶和密碼，擷取來自站台資料庫的報告資料。  

        > [!IMPORTANT]  
        >  您所指定的帳戶在裝載 Reporting Services 資料庫的電腦上，必須擁有 **本機登入** 權限。  

7.  在 [Reporting Services 點]  頁面上，按 [下一步] 。  

8.  在 [摘要]  頁面上確認設定，然後按 [下一步]  安裝 Reporting Services 點。  

     精靈完成後會建立報告資夾，並將 Configuration Manager 報告複製到指定的報告資料夾。  

    > [!NOTE]  
    >  當建立報告資料夾，並將報告複製到報表伺服器時，Configuration Manager 會判斷物件的適用語言。 如果站台上已安裝關聯的語言套件，Configuration Manager 會以和站台上報表伺服器所執行作業系統相同的語言來建立物件。 如果沒有可用的語言，則會以英文建立和顯示報告。 當您在不含語言套件的站台上安裝 Reporting Services 點時，會安裝英文版的報告。 如果在安裝 Reporting Services 點後安裝語言套件，您必須先解除安裝再重新安裝 Reporting Serivces 點，才能使用具適當語言套件的報告。 如需語言套件的詳細資訊，請參閱 [Language Packs in System Center Configuration Manager](../deploy/install/language-packs.md) (System Center Configuration Manager 的語言套件)。  

###  <a name="BKMK_FileInstallationAndSecurity"></a> 檔案安裝與報表資料夾安全性權限  
 Configuration Manager 會執行下列動作，安裝 Reporting Services 點和設定 Reporting Services：  

> [!IMPORTANT]  
>  以下所列出的動作，可利用已針對 SMS_Executive 服務設定之帳戶的認證來執行，其通常是站台伺服器本機系統帳戶。  

-   安裝 Reporting Services 點站台角色。  

-   在 Reporting Services 中，使用您在精靈中指定的儲存認證來建立資料來源。 這是 Reporting Services 在您執行報告時用於連線到站台資料庫的 Windows 使用者帳戶和密碼。  

-   在 Reporting Services 中建立 Configuration Manager 根資料夾。  

-   在 Reporting Services 中新增 [ConfigMgr 報告使用者]  和 [ConfigMgr 報告系統管理員]  安全性角色。  

-   建立子資料夾並將 Configuration Manager 報告從 %ProgramFiles%\SMS_SRSRP 部署至 Reporting Services。  

-   在 Reporting Services 中，針對 Configuration Manager 中所有具有**站台讀取**權限的使用者帳戶新增 **Configuration Manager 報告使用者**角色至根資料夾。  

-   在 Reporting Services 中，針對 Configuration Manager 中所有具有**站台修改**權限的使用者帳戶新增 **Configuration Manager 報告管理**角色至根資料夾。  

-   擷取報告資料夾與 Configuration Manager 安全物件類型 (保存於 Configuration Manager 站台資料庫中) 之間的對應。  

-   為 Configuration Manager 中的系統管理使用者設定 Reporting Services 中特定報告資料夾的下列權限：  

    -   針對具有 Configuration Manager 物件之**執行報告**權限的系統管理使用者新增使用者，並將 **Configuration Manager 報告使用者**角色指派至相關聯的報告資料夾。  

    -   針對具有 Configuration Manager 物件之**修改報告**權限的系統管理使用者新增使用者，並將 **Configuration Manager 報告管理**角色指派至相關聯的報告資料夾。  

     Configuration Manager 會連接至 Reporting Services，並設定使用者對 Configuration Manager 及 Reporting Services 根資料夾與特定報告資料夾的權限。 Reporting Services 點初始安裝完成後，Configuration Manager 會以 10 分鐘間隔連接至 Reporting Services，確認報告資料夾上設定的使用者權限與針對 Configuration Manager 使用者設定的權限相關聯。 使用 Reporting Services 報表管理員在報告資料夾上新增使用者或修改使用者權限時，Configuration Manager 會使用儲存在站台資料庫中以角色為基礎的指派來覆寫這些變更。 Configuration Manager 也會移除沒有 Configuration Manager 報告權限的使用者。  

##  <a name="BKMK_SecurityRoles"></a> Configuration Manager 的 Reporting Services 安全性角色  
 當 Configuration Manager 安裝 Reporting Services 點時，會在 Reporting Services 中新增下列安全性角色：  

-   **Configuration Manager 報告使用者**：獲派此安全性角色的使用者，只可執行 Configuration Manager 報表。  

-   **Configuration Manager 報告管理員**：獲派此安全性角色的使用者，可執行與 Configuration Manager 報告相關的所有工作。  

##  <a name="BKMK_VerifyReportingServicesPointInstallation"></a> 確認 Reporting Services 點安裝  
 新增 Reporting Services 點站台角色後，您可以查看特定狀態訊息及記錄檔項目確認安裝。 利用下列程序確認 Reporting Services 點安裝成功。  

> [!WARNING]  
>  如果報告顯示在 Configuration Manager 主控台的 [監視] 工作區之 [報告] 節點的 [報告] 子資料夾中，則可略過這個程序。  

#### <a name="to-verify-the-reporting-services-point-installation"></a>若要確認 Reporting Services 點安裝  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [系統狀態] ，然後按一下 [元件狀態] 。  

3.  按一下元件清單中的 [SMS_SRS_REPORTING_POINT]  。  

4.  在 [首頁]  索引標籤的 [元件]  群組中，按一下 [顯示訊息] ，然後按一下 [全部] 。  

5.  指定安裝 Reporting Services 點之前某一期間的日期及時間，然後按一下 [確定] 。  

6.  確認狀態訊息識別碼 1015 列出，表示 Reporting Services 點成功安裝。 或者，您可以開啟位於 &lt;Configuration Manager 安裝路徑>\Logs 中的 Srsrp.log 檔案，並尋找 [安裝成功]。  

     在 Windows 檔案總管中，瀏覽至 &lt;Configuration Manager 安裝路徑>\Logs。  

7.  開啟 Srsrp.log，並從 Reporting Services 點成功安裝的時間開始逐步查看記錄檔。 確認報告資料夾已建立，報告已部署，且每個資料夾上的安全性原則已確認。 尋找安全原則確認最後一行後面的 「Successfully checked that the SRS web service is healthy on server」  (成功確認伺服器上的 SRS Web 服務狀況良好)。  

##  <a name="BKMK_Certificate"></a> 設定 Configuration Manager 主控台電腦的自我簽署憑證  
 您有許多選項可用來撰寫 SQL Server Reporting Services 報告。 當您在 Configuration Manager 主控台中建立或編輯報告時，Configuration Manager 會開啟報表產生器作為撰寫環境使用。 無論您撰寫 Configuration Manager 報告的方式為何，都需要自我簽署憑證才能對站台資料庫伺服器進行伺服器驗證。 Configuration Manager 會在站台伺服器以及已安裝 SMS 提供者的電腦上自動安裝憑證。 因此，從其中一部電腦執行 Configuration Manager 主控台時，您就可以建立或編輯報告。 不過，當您從安裝在不同電腦的 Configuration Manager 主控台建立或修改報告時，必須從站台伺服器匯出憑證，再將它新增至執行 Configuration Manager 主控台電腦的**受信任的人**憑證存放區。  

> [!NOTE]  
>  如需有關其他 SQL Server Reporting Services 報告撰寫環境的詳細資訊，請參閱《SQL Server 2008 線上叢書》中的 [比較報表撰寫環境](http://go.microsoft.com/fwlink/p/?LinkId=242805) 。  

 利用下列程序作為範例，了解當兩部電腦都執行 Windows Server 2008 R2 時，如何將自我簽署憑證複本從站台伺服器傳送至另一部執行 Configuration Manager 主控台的電腦。 如果您使用不同的作業系統版本而無法依照此程序執行，請參閱作業系統文件中相同的程序。  

#### <a name="to-transfer-a-copy-of-self-signed-certificate-from-the-site-server-to-another-computer"></a>若要從站台伺服器將自我簽署憑證的副本傳送至另一部電腦  

1.  在站台伺服器上執行下列步驟將自我簽署憑證匯出：  

    1.  依序按一下 [開始] 與 [執行] ，然後輸入 **mmc.exe**。 在空白主控台中，按一下 [檔案] ，然後按一下 [新增/移除嵌入式管理單元] 。  

    2.  在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選取 [憑證] ，然後按一下 [新增] 。  

    3.  在 [憑證嵌入式管理單元]  對話方塊中，選取 [電腦帳戶] ，然後按 [下一步] 。  

    4.  在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後按一下 [完成] 。  

    5.  在 [新增或移除嵌入式管理單元]  對話方塊中，按一下 [確定] 。  

    6.  在主控台中，依序展開 [憑證 (本機電腦)] 和 [受信任的人] ，然後選取 [憑證] 。  

    7.  以滑鼠右鍵按一下易記名稱為 &lt;站台伺服器的 FQDN> 的憑證，按一下 [所有工作]，然後選取 [匯出]。  

    8.  使用預設選項完成 [憑證匯出精靈]  ，然後以 [.cer]  副檔名儲存憑證。  

2.  在執行 Configuration Manager 主控台的電腦上執行下列步驟，將自我簽署憑證新增至 [受信任的人] 憑證存放區：  

    1.  重複上述步驟 1.a 到 1.e， 在管理點電腦上設定**憑證**嵌入式MMC。  

    2.  在主控台中，依序展開 [憑證 (本機電腦)] 和 [受信任的人] ，以滑鼠右鍵按一下 [憑證] ，選取 [所有工作] ，然後選取 [匯入]  ，啟動 [憑證匯入精靈] 。  

    3.  在 [匯入檔案]  頁面上，選取步驟 1.h 中儲存的憑證，然後按 [下一步] 。  

    4.  在 [憑證存放區]  頁面上，選取 [將所有憑證放入以下的存放區] ，並將 [憑證存放區]  設為 [受信任的人] ，然後按 [下一步] 。  

    5.  按一下 [完成]  關閉精靈，並完成電腦上的憑證設定。  

##  <a name="BKMK_ModifyReportingServicesPoint"></a> 修改 Reporting Services 點設定  
 安裝 Reporting Services 點之後，您可以在 Reporting Services 點內容中修改站台資料庫連接及驗證設定。 利用下列程序修改 Reporting Services 點設定。  

#### <a name="to-modify-reporting-services-point-settings"></a>若要修改 Reporting Services 點設定  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [站台設定] ，然後按一下 [伺服器和站台系統角色]  列出站台系統。  

    > [!TIP]  
    >  若只要列出裝載 Reporting Services 點站台角色的站台系統，請以滑鼠右鍵按一下 [伺服器和站台系統角色]  選取 [Reporting Services 點] 。  

3.  選取裝載您要修改設定之 Reporting Services 點的站台系統，然後在 [站台系統角色]  中選取 [Reporting Service 點] 。  

4.  在 [網站角色]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 [Reporting Services 點內容]  對話方塊中，您可以修改下列設定：  

    -   **站台資料庫伺服器名稱**：指定裝載 Configuration Manager 站台資料庫的伺服器名稱。 通常，精靈會自動擷取伺服器的完整網域名稱 (FQDN)。 若要指定資料庫執行個體，請使用 &lt;伺服器名稱>\&lt;執行個體名稱> 的格式。  

    -   **資料庫名稱**：指定 System Center 2012 Configuration Manager 站台資料庫名稱，然後按一下 [驗證]，確認精靈可存取站台資料庫。  

        > [!IMPORTANT]  
        >  要用來建立 Reporting Services 點的使用者帳戶必須具有站台資料庫的「讀取」存取權限。 如果連線測試失敗，則會顯示紅色警告圖示。 將游標移至此圖示上方，即可讀取失敗的詳細資料。 更正錯誤，然後再按一下 [測試]  。  

    -   **使用者帳戶**：按一下 [設定]，然後選取要在 Reporting Services 點上的 SQL Server Reporting Services 連線到 Configuration Manager 站台資料庫時，用以擷取顯示在報告中資料的帳戶。 選取 [現有的帳戶] 以指定具有現有 Configuration Manager 權限的 Windows 使用者帳戶，或選取 [新增帳戶] 以指定目前尚未具有 Configuration Manager 權限的 Windows 使用者帳戶。 Configuration Manager 會自動授與指定之使用者帳戶存取站台資料庫的權限。 此帳戶會在 [系統管理]  工作區中 [安全性]  節點的 [帳戶]  子資料夾中顯示為 [ConfigMgr SRS 報告點]  帳戶。  

         指定的 Windows 使用者帳戶和密碼會經過加密，並儲存於 Reporting Services 資料庫中。 Reporting Services 會使用此帳戶和密碼，擷取來自站台資料庫的報告資料。  

        > [!IMPORTANT]  
        >  若站台資料庫位於遠端站台系統上，您指定的帳戶就必須具有該電腦的 [本機登入]  權限。  

6.  按一下 [確定]  儲存變更並結束對話方塊。  

## <a name="upgrading-sql-server"></a>升級 SQL Server  
 您升級 SQL Server 及作為 Reporting Services 點資料來源的 SQL Server Reporting Services 後，可能會在從 Configuration Manager 主控台執行或編輯報告時發生錯誤。 為了可從 Configuration Manager 主控台正常執行報告，您必須移除站台的 Reporting Services 點站台系統角色，然後重新安裝。 不過升級後，您可以繼續從網際網路瀏覽器成功執行及編輯報告。  

##  <a name="BKMK_ConfigureReportOptions"></a> 設定報表選項  
 使用 Configuration Manager 站台的報告選項選取預設 Reporting Services 點，用來管理您的報告。 雖然一個站台可以有多個 Reporting Services 點，但是只有報告選項中選取的預設報告伺服器會用來管理報告。 利用下列程序設定站台的報告選項。  

#### <a name="to-configure-report-options"></a>若要設定報告選項  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [報告] ，然後按一下 [報告] 。  

3.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [報告選項] 。  

4.  在清單中選取預設報告伺服器，然後按一下 [確定] 。 如果清單中未列出 Reporting Services 點，請確認您已在站台中成功安裝及設定 Reporting Services 點。  

## <a name="next-steps"></a>後續步驟
[報告作業和維護](operations-and-maintenance-for-reporting.md)
