---
title: Technical Preview 1705 | Microsoft Docs
description: "了解 System Center Configuration Manager Technical Preview 1705 版中可用的功能。"
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b977a79baec73999caa21648adcb6fcfec4a4935
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1705-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1705 中的功能

適用於︰System Center Configuration Manager (Technical Preview)

本文介紹 System Center Configuration Manager Technical Preview 1705 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    

**此 Technical Preview 的已知問題：**
-   **Operations Manager Suite 連接器未升級**。 當您從已設定 OMS 連接器的舊版 Technical Preview 升級時，該連接器未升級且在已不在主控台中。 升級之後，您必須[使用 Azure 服務精靈](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms)，並重新建立與 OMS 工作區的連線。
-   **Surface 驅動程式未成功同步**。 儘管 Technical Preview 之 Configuration Manager 主控台中的 [新功能] 已列出對 Surface 驅動程式的支援，但此功能尚未如預期般運作。
-   **無法建立 Windows Update for Business 延遲原則**。 儘管 Technical Preview 之 Configuration Manager 主控台中的 [新功能] 已列出設定 Windows Update for Business 延遲原則的功能，但精靈並未開啟，因此您無法設定任何原則。


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**以下是您可以使用此版本試用的新功能。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>更新重設工具  
您可以使用「Configuration Manager 更新重設工具」**CMUpdateReset.exe**，來修正主控台內更新無法進行下載或複寫的問題。 此工具隨附於 Technical Preview 1705 版。 您可以在安裝該 Technical Peview 之後，在 Technical Peview 站台之站台伺服器上的 ***\cd.latest\SMSSETUP\TOOLS*** 資料夾中找到此工具。

您可以將此工具與 Technical Preview 1606 版或更新版本搭配使用。 由於提供了這項回溯支援，因此這個工具能夠與一系列 Technical Preview 更新案例搭配使用，而不需等到有下一個 Technical Preview 可供使用。

您可以在主控台內更新尚未安裝且處於失敗狀態時使用此工具。 失敗狀態可能是指更新下載仍在進行中，但已停滯且花費的時間過長，可能比您以往對相同大小之更新套件的預期時間還長數小時。 它也可能是指將更新複寫到子主要站台失敗。  

當您執行此工具時，它會針對您指定的更新執行。 此工具預設不會刪除已成功安裝或下載的更新。  

### <a name="prerequisites"></a>先決條件
您用來執行此工具的帳戶需要有下列權限：
-   對管理中心網站之站台資料庫及您階層中每個主要站台的「讀取」和「寫入」權限。 若要設定這些權限，您可以新增使用者帳戶作為每個站台之 Configuration Manager 資料庫上 **db_datawriter** 和 **db_datareader** [固定資料庫角色](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles)的成員。 此工具不會與次要站台進行互動。
-   您階層之最上層站台上的「本機系統管理員」。
-   裝載服務連接點之電腦上的「本機系統管理員」。

您將需要有所要重設之更新套件的 GUID。 取得 GUID：
-   在主控台中，移至 [系統管理] > [更新與服務]，在顯示窗格內其中一個資料行 (例如 [狀態]) 的標題上按一下滑鼠右鍵，然後選取 [套件 GUID]。 這會將該資料行新增到顯示中，而資料行會顯示更新套件 GUID。

> [!TIP]  
> 若要複製 GUID，請選取您想要重設之更新套件的資料列，然後使用 CTRL+C 來複製該資料列。 如果您將所複製的選取範圍貼到文字編輯器中，則可以接著僅複製 GUID，以在執行工具時作為命令列參數。

### <a name="run-the-tool"></a>執行工具    
此工具必須在階層的最上層站台上執行。

當您執行此工具時，需使用命令列參數來指定位於階層最上層站台的 SQL Server、站台資料庫名稱，以及想要重設的更新套件 GUID。 此工具會接著根據更新狀態，識別所需存取的其他伺服器。   

如果更新套件處於 [下載後] 狀態，此工具就不會清除套件。 您可以選擇使用強制刪除參數 (請參閱本主題稍後的命令列參數)，來強制移除已成功下載的更新。

在執行此工具之後：
-   如果已刪除套件，請重新啟動最上層站台 SMS_Executive 服務，然後檢查更新以重新下載套件。
-   如果未刪除套件，則不需要採取任何動作，因為更新將會重新初始化並重新啟動複寫或安裝。

**命令列參數：**  

| 參數        |說明                 |  
|------------------|----------------------------|  
|**-S &lt;您最上層站台之 SQL Server 的 FQDN>** | *必要* <br> 針對階層最上層站台的站台資料庫，您必須指定裝載這些資料庫的 SQL Server FQDN。    |  
| **-D &lt;資料庫名稱>**                        | *必要* <br> 您必須指定最上層站台資料庫的名稱。  |  
| **-P &lt;套件 GUID>**                         | *必要* <br> 您必須指定所要重設之更新套件的 GUID。   |  
| **-I &lt;SQL Server 執行個體名稱>**             | *選擇性* <br> 使用此參數來識別裝載站台資料庫的 SQL Server 執行個體。 |
| **-FDELETE**                              | *選擇性* <br> 使用此參數來強制刪除已成功下載的更新套件。 |  
 **範例：**  
 在典型的案例中，您想要重設有下載問題的更新。 您的 SQL Server FQDN 為*server1.fabrikam.com*，站台資料庫位於*CM_XYZ*，而套件 GUID 是*61F16B3C-F1F6-4F9F-8647-2A524B0C802C*。  您需執行：***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 在較極端的案例中，您想要強制刪除有問題的更新套件。 您的 SQL Server FQDN 為*server1.fabrikam.com*，站台資料庫位於*CM_XYZ*，而套件 GUID 是*61F16B3C-F1F6-4F9F-8647-2A524B0C802C*。  您需執行：***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>使用 Technical Preview 來測試此工具  
您可以將此工具與 Technical Preview 1606 版或更新版本搭配使用。 由於提供了這項回溯支援，因此這個工具能夠與更多的 Technical Preview 更新案例搭配使用，而不需等到有下一個 Technical Preview 可供使用。

請先在 Technical Preview 的更新套件上執行此工具，再讓該更新完成其先決條件檢查。 [系統管理] > [更新與服務] 中的下列其中一個套件「狀態」即代表已完成先決條件檢查的狀態：  
-   **先決條件檢查通過**
-   **先決條件檢查通過，但出現警告**
-   **先決條件檢查失敗**


## <a name="high-dpi-console-support"></a>高 DPI 主控台支援

在此版本中，應該已修正有關在高 DPI 裝置 (例如 Surface Book) 上檢視 UI 時，Configuration Manager 主控台如何縮放及顯示不同 UI 部分的問題。


## <a name="peer-cache-improvements"></a>對等快取改善
從此 Technical Preview 開始，「對等快取」[已不再使用網路存取帳戶](/sccm/core/plan-design/hierarchy/client-peer-cache)來驗證來自同儕節點的下載要求。


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>對 SQL Server Always On 可用性群組的改進  
在此版本中，您現在可以在與 Configuration Manager 搭配使用的 SQL Server Always On 可用性群組中使用非同步認可複本。  這意謂著您可以將額外的複本新增到可用性群組來作為離站 (遠端) 備份，然後在災害復原案例中使用這些備份。  

-   Configuration Manager 支援使用非同步認可複本來復原您的同步複本。  如需有關如何完成此操作的資訊，請參閱＜備份與復原＞主題中的[站台資料庫復原選項](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption)。

-   此版本不支援容錯移轉成使用非同步認可複本作為您的站台資料庫。
> [!CAUTION]  
> 由於 Configuration Manager 並不會驗證非同步認可複本的狀態來確認它是否為最新版，並且[這類複本在設計上即可能不同步](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes)，因此使用非同步認可複本作為站台資料庫將可能讓您站台和資料的完整性面臨風險。  

-   您可以在可用性群組中使用的複本數量和類型，與您所用 SQL Server 版本所支援的複本數量和類型相同。   (先前的支援僅限使用兩個同步認可複本)。

### <a name="configure-an-asynchronous-commit-replica"></a>設定非同步認可複本
若要將非同步複本新增到[與 Configuration Manager 搭配使用的可用性群組](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)，您並不需要執行設定同步複本所需的設定指令碼。 (這是因為不支援使用該非同步複本作為站台資料庫)。如需有關如何將次要複本新增到可用性群組的資訊，請參閱 [SQL Server 文件](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot))。

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>使用非同步複本來復原您的站台
在您使用非同步複本來復原站台資料庫之前，必須先停止作用中的主要站台，以防止使用者對站台資料庫進行額外的寫入。 在停止該站台之後，您可以使用非同步複本來取代使用[手動復原的資料庫](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption)。

若要停止該站台，您可以使用[階層維護工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)來停止站台伺服器上的主要服務。 請使用命令列：**Preinst.exe /stopsite**   

停止該站台相當於停止站台伺服器上後面接著 SMS_Executive 服務的「站台元件管理員」服務 (sitecomp)。

> [!TIP]  
> 如果您使用主要被動複本 (在此 Technical Preview 中是以[站台伺服器角色高可用性](#site-server-role-high-availability)的形式引進)，則不需要停止被動複本。 只需停止作用中的主要站台。



## <a name="improved-user-notifications-for-office-365-updates"></a>適用於 Office 365 更新的改良式使用者通知
我們已進行一些改進，可在用戶端安裝 Office 365 更新時，運用 Office 的「隨選即用」使用者體驗。 這包括快顯和應用程式內通知，以及倒數計時體驗。 在此版本之前，當系統將 Office 365 更新傳送給用戶端時，已開啟的 Office 應用程式會不顯示警告便自動關閉。 在此更新之後，Office 應用程式將不再意外關閉。

### <a name="prerequisites"></a>先決條件
此更新適用於 Office 365 ProPlus 用戶端。

### <a name="known-issues"></a>已知問題
當用戶端第一次評估 Office 365 更新指派，而該項更新的期限是排定在過去、立即執行或在 30 分鐘內時，Office 365 使用者體驗可能會不一致。 例如，用戶端可能會收到該項更新的 30 分鐘倒數計時對話方塊，但實際的強制執行可能在倒數計時結束之前即已開始。 若要避免此行為，請考量採用下列做法：
- 部署 Office 365 更新時，將期限排定在超過目前時間的 60 分鐘之前。
- 在集合上設定一個不在上班時間內的維護期間，或在部署上設定一個強制執行寬限期。

### <a name="try-it-out"></a>試試看！
請嘗試完成下列工作，然後從功能區的 [首頁] 索引標籤中傳送 [意見反應] 給我們，讓我們了解運作情況：
- 在用戶端上部署一個 Office 365 更新，其中將期限至少排定在目前時間的 60 分鐘之前。 觀察用戶端上的新行為。


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>設定及部署 Windows Defender 應用程式防護原則

[Windows Defender 應用程式防護](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)是一個新的 Windows 功能，可藉由在作業系統其他部分所無法存取的安全隔離容器中開啟未受信任的網站，來協助保護您的使用者。 在此 Technical Preview 中，我們已新增支援，可使用您所設定並接著部署到集合的 Configuration Manager 合規性設定來設定此功能。
此功能將在 64 位元版「Windows 10 建立者的更新」(代號：RS2) 的預覽版中發行。 若要立即測試此功能，您必須使用此更新的預覽版本。


### <a name="before-you-start"></a>開始之前

若要建立及部署「Windows Defender 應用程式防護」原則，必須為您要部署原則的 Windows 10 裝置設定網路隔離原則。 如需其他詳細資料，請參閱稍後引用的部落格文章。
此功能只能與最新的「Windows 10 測試人員組建」搭配運作。 若要測試它，您的用戶端必須執行最新的「Windows 10 測試人員組建」。

### <a name="try-it-out"></a>試試看！

請確定您已閱讀部落格文章來了解「Windows Defender 應用程式防護」的相關基本知識。

建立原則並瀏覽至可用的設定：

1.  在 Configuration Manager 主控台中，選擇 [資產與相容性]。
2.  在 [資產與合規性] 工作區中，選擇 [概觀] > [Endpoint Protection] > [Windows Defender 應用程式防護]。
3.  在 [首頁] 索引標籤的 [建立] 群組中，按一下 [建立 Windows Defender 應用程式防護原則]。
4.  藉由使用部落格文章作為參考，您可以瀏覽並設定可用的設定以試用此功能。
5.  完成操作時，請完成精靈步驟，然後將原則部署到一或多個 Windows 10 裝置。

### <a name="further-reading"></a>延伸閱讀

若要深入了解「Windows Defender 應用程式防護」請參閱[這篇部落格文章]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)。
此外，若要深入了解「Windows Defender 應用程式防護」獨立模式，請參閱[這篇部落格文章](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)。




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Azure AD 和雲端管理的新功能

在此版本中，您可以設定讓雲端服務使用 Azure AD 來支援下列案例：

- 從網際網路手動安裝 Configuration Manager 用戶端，並將它指派給 Configuration Manager 站台。
- 使用 Intune 將 Configuration Manager 用戶端部署到網際網路上的裝置。

### <a name="advantages"></a>優點

使用雲端服務和 Azure AD 便不需使用用戶端驗證憑證。

您可以深入站台中探索 Azure AD 使用者，以在集合及其他 Configuration Manager 作業中使用。

### <a name="before-you-start"></a>開始之前

- 您必須擁有 Azure AD 租用戶。
- 您的裝置必須執行 Windows 10 並加入 Azure AD。  用戶端除了加入 Azure AD 之外，也可以加入網域。
- 除了管理點站台系統角色的[現有先決條件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)之外，您還必須確定在裝載此站台系統角色的電腦上啟用 **ASP.NET 4.5** (以及任何其他隨此選項自動選取的選項)。
- 使用 Microsoft Intune 來部署 Configuration Manager 用戶端：
    - 您必須擁有有效的 Intune 租用戶 (Configuration Manager 與 Intune 不需要連接)。
    - 在 Intune 中，您已建立並部署包含 Configuration Manager 用戶端的應用程式。 如需有關如何執行此操作的詳細資料，請參閱＜如何將用戶端安裝至受 Intune MDM 管理的 Windows 裝置＞。
- 使用 Configuration Manager 來部署用戶端：
    - 必須為 HTTPS 模式至少設定一個管理點。
    - 您必須設定「雲端管理閘道」。


### <a name="set-up-the-cloud-management-gateway"></a>設定雲端管理閘道

設定「雲端管理閘道」以讓用戶端從網際網路存取您的 Configuration Manager 站台，而無需使用憑證。

您將可以在下列主題中找到與此做法相關的說明：

- [在 Configuration Manager 中進行雲端管理閘道規劃](/sccm/core/clients/manage/plan-cloud-management-gateway)。
- [設定 Configuration Manager 的雲端管理閘道](/sccm/core/clients/manage/setup-cloud-management-gateway)。
- [在 Configuration Manager 中監視雲端管理閘道](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)。

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>在 Configuration Manager 雲端服務中設定 Azure 服務應用程式

這會將您的 Configuration Manager 站台連線到 Azure AD，這也是本節中所有其他作業的先決條件。 若要這樣做：

1.  在 Configuration Manager 主控台的 [系統管理] 工作區中，展開 [雲端服務]，然後按一下 [Azure 服務]。
2.  在 [首頁] 索引標籤的 [Azure 服務] 群組中，按一下 [設定 Azure 服務]。
3.  在「Azure 服務精靈」的 [Azure 服務] 頁面上，選取 [雲端管理] 以允許用戶端使用 Azure AD 向階層進行驗證。
4.  在精靈的 [一般] 頁面上，為您的 Azure 服務指定名稱和描述。
5.  在精靈 [應用程式] 頁面上，從清單中選取您的 Azure 環境，然後按一下 [瀏覽] 來選取將用來設定 Azure 服務的伺服器和用戶端應用程式：
    - 在 [伺服器應用程式] 視窗中選取您要使用的伺服器應用程式，然後按一下 [確定]。 伺服器應用程式是 Azure Web 應用程式，內含您 Azure 帳戶的設定，包括租用戶識別碼、用戶端識別碼和用戶端的祕密金鑰。 如果您沒有可用的伺服器應用程式，請使用下列其中一項︰
        - **建立**︰若要建立新的伺服器應用程式，請按一下 [建立]。 提供應用程式和租用戶的易記名稱。 接著，您登入 Azure 後，Configuration Manager 會為您在 Azure 中建立 Web 應用程式，包括和 Web 應用程式搭配使用的用戶端識別碼及祕密金鑰。 您稍後可從 Azure 入口網站加以檢視。
        - **匯入**︰若要使用您 Azure 訂用帳戶中已存在的 Web 應用程式，請按一下 [匯入]。 提供應用程式與租用戶的易記名稱，然後針對您要讓 Configuration Manager 使用的 Azure Web 應用程式，為其指定租用戶識別碼、用戶端識別碼及祕密金鑰。 在您「驗證」資訊之後，請按一下 [確定] 來繼續進行操作。 此 Technical Preview 目前尚未提供此選項。
    - 針對用戶端應用程式重複相同的程序。

  使用「應用程式匯入」時，您必須授與「讀取目錄資料」應用程式權限，才能在入口網站中設定正確的權限。 如果使用「應用程式建立」，則權限會隨著應用程式自動建立，但您仍然需要在 Azure 入口網站中對應用程式表示同意。
6.  在精靈的 [探索] 頁面，視需要啟用 [啟用 Azure Active Directory 使用者探索]，然後按一下 [設定]。
在 [Azure AD 使用者探索設定] 對話方塊中，設定進行探索的排程。 您也可以啟用差異探索，這將只檢查 Azure AD 中新的或已變更的帳戶。
7.  完成精靈。

此時，您已將 Configuration Manager 站台連線到 Azure AD。


### <a name="install-the-cm-client-from-the-internet"></a>從網際網路安裝 CM 用戶端

在開始之前，請先確定用戶端安裝來源檔案儲存在您想要安裝用戶端的裝置本機。
接著，參考[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually)中的指示，使用下列安裝命令列 (以您自己的值取代範例中的值)：

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT  CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso  AADCLIENTAPPID=<GUID> AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck**：如果您的管理點或雲端管理閘道使用非公用伺服器憑證，則用戶端可能會無法連線到 CRL 位置。
- **/Source**：本機資料夾：用戶端安裝檔的位置。
- **CCMHOSTNAME**：您網際網路管理點的名稱。 您可以從受管理用戶端上的命令提示字元執行 **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** 來找出此資訊。
- **SMSMP**：您查閱管理點 (可能位於您的內部網路) 的名稱。
- **SMSSiteCode**：您 Configuration Manager 站台的站台碼。
- **AADTENANTID**、**AADTENANTNAME**：您連結到 Configuration Manager 之 Azure AD 租用戶的識別碼和名稱。 您可以從已加入 Azure AD 之裝置上的命令提示字元執行 dsregcmd.exe /status 來找出此資訊。
- **AADCLIENTAPPID**：Azure AD 用戶端應用程式識別碼。 如需有關如何尋找此資訊的說明，請參閱[使用入口網站來建立能夠存取資源的 Azure Active Directory 應用程式和服務主體](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key)。
- **AADResourceUri**：已上線之 Azure AD 伺服器應用程式的識別碼 URI。

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>使用 Azure 服務精靈來設定與 OMS 的連線
從 1705 Technical Preview 版本開始，您需使用「Azure 服務精靈」來設定從 Configuration Manager 到 Operations Management Suite (OMS) 雲端服務的連線。 此精靈會取代先前的工作流程來設定此連線。

-   此精靈可用來設定 Configuration Manager 的雲端服務，例如 OMS、「商務用 Windows 市集」(WSfB) 及 Azure Active Directory (Azure AD)。  

-   Configuration Manager 會連線到 OMS 以使用 [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) 或[升級整備](/sccm/core/clients/manage/upgrade/upgrade-analytics)等功能。

### <a name="prerequisites-for-the-oms-connector"></a>OMS 連接器的先決條件
設定與 OMS 之連線的先決條件與[針對最新分支版本 1702 記載的先決條件](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites)相同。 以下重述該資訊：  

-   將 Configuration Manager 權限提供給 OMS。

-   OMS 連接器必須安裝在裝載處於[線上模式](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation)之[服務連接點](/sccm/core/servers/deploy/configure/about-the-service-connection-point)的電腦上。

-   您必須在服務連接點上安裝適用於 OMS 的 Microsoft Monitoring Agent，以及 OMS 連接器。 Monitoring Agent 和 OMS 連接器必須設定為使用相同的「OMS 工作區」。 若要安裝代理程式，請參閱 OMS 文件中的[下載並安裝代理程式](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent)。
-   在您安裝連接器和代理程式之後，您必須設定 OMS 以使用 Configuration Manager 資料。 若要這樣做，請在 OMS 入口網站中[匯入 Configuration Manager 集合](/azure/log-analytics/log-analytics-sccm#import-collections)。

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>使用 Azure 服務精靈來設定與 OMS 的連線

1.  在主控台中，移至 [系統管理] > [概觀] > [雲端服務] > [Azure 服務]，然後從功能區的 [首頁] 索引標籤中選擇 [設定 Azure 服務]，來啟動「Azure 服務精靈」。

2.  在 [Azure 服務] 頁面上，選取 [Operation Management Suite] 雲端服務。 提供「Azure 服務名稱」的易記名稱和選擇性的描述，然後按 [下一步]。

3.  在 [應用程式] 頁面上，指定您的 Azure 環境 (Technical Preview 僅支援 [公用雲端])。 接著，按一下 [瀏覽] 以開啟 [伺服器應用程式] 視窗。

4.  選取一個 Web 應用程式：

    -   **匯入**︰若要使用您 Azure 訂用帳戶中已存在的 Web 應用程式，請按一下 [匯入]。 提供應用程式與租用戶的易記名稱，然後針對您要讓 Configuration Manager 使用的 Azure Web 應用程式，為其指定租用戶識別碼、用戶端識別碼及祕密金鑰。 **驗證**資訊後，請按一下 [確定] 繼續。   

    > [!NOTE]   
    > 當您使用此預覽來設定 OMS 時，OMS 僅支援 Web 應用程式 的「匯入」功能。 不支援建立新的 Web 應用程式。 同樣地，您也無法針對 OMS 重複使用現有的應用程式。

5.  如果您成功完成所有其他程序，則 [OMS 連線設定] 畫面上的資訊將會自動顯示在此頁面上。 應該會顯示適用於您 [Azure 訂用帳戶]、[Azure 資源群組] 及 [Operations Management Suite 工作區] 的連線設定資訊。

6.  精靈會使用您已輸入的資訊來連線到 OMS 服務。 選取要與 OMS 同步的裝置集合，然後按一下 [新增]。

7.  確認 [摘要] 畫面上的連線設定，然後選取 [下一步]。 [進度] 畫面會顯示連線狀態，然後應該為 [完成]。

8.  在精靈完成後，Configuration Manager 主控台會顯示您已將 [Operation Management Suite] 設定為 [雲端服務類型]。
