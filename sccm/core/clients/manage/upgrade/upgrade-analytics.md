---
title: Upgrade Readiness | System Center Configuration Manager
description: "整合 Upgrade Readiness 與 Configuration Manager。 在管理主控台中存取升級相容性資料。 設定要升級或修復的目標裝置。"
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angerobe
ms.date: 7/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: b1f4cd4a6f19a02d2b2dc3f9a841aeeb2a1403dd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>整合 Upgrade Readiness 與 System Center Configuration Manager

適用於：System Center Configuration Manager (最新分支)

更新整備小幫手 (先前稱為 Upgrade Analytics) 可讓您評估及分析裝置針對 Windows 10 的整備程度。 整合 Upgrade Readiness 與 Configuration Manager，以在 Configuration Manager 管理主控台中存取用戶端升級相容性資料。 您可以從裝置清單中設定要升級或修復的目標裝置。

Upgrade Readiness 是 Microsoft Operations Management Suite (OMS) 中的解決方案。 您可以在 [Get started with Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) (開始使用 Upgrade Readiness) 中閱讀更多有關 Upgrade Readiness 的資訊。

## <a name="configure-clients"></a>設定用戶端

您必須採取數個設定步驟，確保您的用戶端可以將資料提供給 Upgrade Readiness︰

-  如[在您的組織中設定 Windows 遙測](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization)中所述，進行用戶端遙測設定。
-  安裝[開始使用更新整備小幫手](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) \(英文\) 的＜部署相容性更新和相關知識庫＞一節中所述的知識庫。

    > [!NOTE]
    > 您可以下載自動化許多用戶端設定工作的指令碼。 如需指令碼的資訊，請參閱 [Get started with Upgrade Readiness](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) (開始使用 Upgrade Readiness) 中的 *Run the Upgrade Readiness deployment script* (執行 Upgrade Readiness 部署指令碼) 一節。

## <a name="connect-to-upgrade-readiness"></a>連線到更新整備小幫手

### <a name="prerequisites"></a>先決條件

從最新分支 1706 版開始，Azure 服務精靈可用來簡化要搭配 Configuration Manager 使用之 Azure 服務的設定程序。 若要使用精靈，您需要設定 Azure Web 應用程式。 如需詳細資訊，請參閱 [Azure 服務精靈](/sccm/core/servers/deploy/configureazure-services-wizard)。

### <a name="use-the-azure-wizard-to-create-the-connection"></a>使用 Azure 精靈建立連線

1.  在 Configuration Manager 主控台的 [系統管理] 工作區中，展開 [雲端服務]，然後按一下 [Azure 服務]。
2.  在 [首頁] 索引標籤的 [Azure 服務] 群組中，按一下 [設定 Azure 服務]。
3.  在 [Azure 服務] 頁面上輸入易記名稱。 您也可以輸入描述。 接著選取 [更新整備小幫手連接器]，並按一下 [下一步]。
4.  在 [應用程式] 頁面上指定您的 Azure 環境。 按一下 [瀏覽] 來設定伺服器應用程式。
5.  按一下 [匯入] 來連線到您在 Azure 中的 Web 應用程式。
    -  輸入 [Azure AD 租用戶名稱]。
    -  輸入 [Azure AD 租用戶識別碼]。
    -  輸入 [應用程式名稱]。
    -  輸入 [用戶端識別碼]。
    -  輸入 [祕密金鑰]。
    -  選取 [祕密金鑰的到期日] 的日期。
    -  針對 [應用程式識別碼 URI] 輸入任何的 URL。
    -  按一下 [確認]，然後按一下 [確定]。

6.  在 [設定] 頁面上，指定更新整備小幫手的連線。 選取下列值：  
    -  Azure 訂用帳戶
    -  Azure 資源群組
    -  Windows Analytics 工作區
8.  按一下 [下一步] 。 您可以在 [摘要] 頁面中檢閱您的連線。 

## <a name="complete-upgrade-readiness-tasks"></a>完成 Upgrade Readiness 工作  

在您建立連線之後，請依[開始使用更新整備小幫手](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) \(英文\) 中所述的內容執行這些工作。  

1. 將 UpgradeReadiness 服務新增至 OMS 工作區。  
2. 產生商業識別碼。  
3. 訂閱 Upgrade Readiness。   

## <a name="use-the-upgrade-readiness-deployment-script"></a>使用 Upgrade Readiness 部署指令碼  

您可以自動化許多 Upgrade Readiness 工作，並針對 Microsoft **Upgrade Readiness 部署指令碼**的資料共用問題進行疑難排解。  
Upgrade Readiness 部署指令碼執行下列動作︰  

- 設定商業識別碼 + CommercialDataOptIn + RequestAllAppraiserVersions 索引鍵。  
- 確認使用者電腦可以將資料傳送給 Microsoft。  
- 檢查電腦是否有擱置重新啟動。   
- 確認已安裝最新版的知識庫套件 10.0.x (需要 10.0.14913 或後續版本)。  
- 啟用時，會開啟詳細資訊模式來進行疑難排解。  
- 起始收集 Microsoft 評估組織升級整備所需的遙測資料。  
- 啟用時，cmd 視窗中會顯示指令碼的進度。 這能提供問題上的檢視 (每個步驟的成功或失敗) 和/或針對記錄檔的寫入。  

## <a name="to-run-the-upgrade-readiness-deployment-script"></a>執行 Upgrade Readiness 部署指令碼：  

1. 下載 [Upgrade Readiness deployment script](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) (Upgrade Readiness 部署指令碼)，並解壓縮 UpgradeReadiness.zip。 只有在您想要以疑難排解模式執行指令碼時，才需要 [診斷] 資料夾中的檔案。  
2. 在 RunConfig.bat 中編輯這些參數︰  
- 記錄資訊的存放位置。 範例：%SystemDrive%\URDiagnostics。 您可以在遠端檔案共用或本機目錄上儲存記錄資訊。 如果封鎖指令碼無法建立所指定路徑的記錄檔，則會建立具有 Windows 目錄之磁碟機中的記錄檔。  
- 商業識別碼。  
- 根據預設，指令碼會將記錄資訊同時傳送到主控台和記錄檔。 若要變更預設行為，請使用下列其中一個選項︰  
    - logMode = 0 僅記錄到主控台  
    - logMode = 1 記錄到檔案和主控台  
    - logMode = 2 僅記錄到檔案  
    - 如需疑難排解，請將 **isVerboseLogging** 設定為 **$true** 以產生可協助診斷問題的記錄資訊。 根據預設，**isVerboseLogging** 設定為 **$false**。 請確定 [診斷] 資料夾安裝在與使用此模式之指令碼相同的目錄。  
    - 如果使用者需要重新啟動電腦，請通知使用者。 根據預設，這會設定為 off。  

3. 完成編輯 RunConfig.bat 中的參數之後，請以系統管理員身分執行指令碼。  


## <a name="view-microsoft-upgrade-readiness-properties-in-configuration-manager"></a>在 Configuration Manager 中檢視 Microsoft Upgrade Readiness 內容  

1.  在 Configuration Manager 主控台中，瀏覽至 [雲端服務]，然後選擇 [OMS 連接器] 開啟 [OMS Connection Properties]\(OMS 連線內容) 頁面。  

2.  此頁面有兩個索引標籤︰
  * [Azure Active Directory] 索引標籤會顯示您的 [租用戶]、[用戶端識別碼]、[用戶端祕密金鑰到期]，並可讓您在用戶端祕密金鑰到期時「確認」[用戶端祕密金鑰]。
  * [Upgrade Readiness] 索引標籤會顯示 [Azure 訂用帳戶]、[Azure 資源群組] 和 [Operations Management Suite 工作區]。

## <a name="view-and-use-the-upgrade-information"></a>檢視和使用升級資訊

在您整合 Upgrade Readiness 與 Configuration Manager 之後，即可檢視用戶端升級整備的分析，然後採取動作。

1. 在 Configuration Manager 主控台中，選擇 [監視] > [概觀] > [Upgrade Readiness]。
2. 檢閱資料，其中包括升級整備狀態以及回報遙測之 Windows 裝置的百分比。
3. 您可以篩選儀表板來檢視特定集合中裝置的資料。
4. 您可以檢視處於特定整備狀態的裝置，以及建立那些裝置的動態集合，以升級這些就緒的裝置，或採取動作，使其進入整備狀態。

## <a name="create-a-connection-to-upgrade-readiness-1702-and-earlier"></a>建立更新整備小幫手的連線 (1702 和較舊版本)

在 Configuration Manager 的 1706 分支之前，若要建立更新整備小幫手的連線，需要下列步驟。

### <a name="prerequisites"></a>先決條件

- 若要新增連線，您的 Configuration Manager 環境必須先以[線上模式](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/)設定[服務連接點](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。 當您將連線新增至環境時，也會在執行此站台系統角色的電腦上安裝 Microsoft Monitoring Agent。
- 將 Configuration Manager 註冊為「Web 應用程式和/或 Web API」管理工具，並且取得[來自此註冊的用戶端識別碼](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/)。
- 在 Azure Active Directory 中，為已註冊的管理工具建立用戶端金鑰。
- 在 Azure 入口網站中，為已註冊的 Web 應用程式提供 OMS 存取權限，如[為 Configuration Manager 提供 OMS 的權限](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms)中所述。

    > [!IMPORTANT]
    > 設定 OMS 存取權限時，請務必選擇 [參與者] 角色，並將所註冊應用程式之資源群組的權限指派給它。

### <a name="create-the-connection"></a>建立連線

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [雲端服務] > [Upgrade Readiness Connector]\(升級整備連接器) > [建立 Upgrade Analytics 的連線] 來啟動 [新增 Upgrade Analytics 連線精靈]。
3.  在 [Azure Active Directory] 畫面上，提供 [租用戶]、[用戶端識別碼] 和 [用戶端祕密金鑰]，然後選取 [下一步]。
4.  在 [Upgrade Readiness] 畫面上，填入 [Azure 訂用帳戶]、[Azure 資源群組] 和 [Operations Management Suite 工作區] 以提供連線設定。
5.  確認 [摘要] 畫面上的連線設定，然後選取 [下一步]。

    > [!NOTE]
    > 您必須將 Upgrade Readiness 連線至階層中的頂層站台。 如果您將 Upgrade Readiness 連線至獨立主要站台，然後將管理中心網站新增至環境，則必須在新的階層內刪除並重新建立 OMS 連線。
