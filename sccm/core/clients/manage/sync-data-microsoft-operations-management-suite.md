---
title: "同步處理資料 | Microsoft Docs | Microsoft Operations Management Suite "
description: "將資料從 System Center Configuration Manager 同步處理至 Microsoft Operations Management Suite。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: "9"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 608a9893011c6500d5d4cd2f756a124db66b1858
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>將資料從 Configuration Manager 同步處理至 Microsoft Operations Management Suite

適用於：System Center Configuration Manager (最新分支)

您可使用「Azure 服務精靈」來設定從 Configuration Manager 到 Operations Management Suite (OMS) 雲端服務的連線。 從 1706 版開始，此精靈會取代先前設定此連線的工作流程。 針對較舊的版本，請參閱[將資料從 Configuration Manager 同步處理至 Microsoft Operations Management Suite (1702 和較舊版本)](#Sync-data-from-Configuration-Manager-to-the-Microsoft-Operations-Management-Suite-(1702-and-earlier))。

-   此精靈可用來設定 Configuration Manager 的雲端服務，例如 OMS、「商務用 Windows 市集」(WSfB) 及 Azure Active Directory (Azure AD)。  

-   Configuration Manager 會連線到 OMS 以使用 [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) 或[升級整備](/sccm/core/clients/manage/upgrade/upgrade-analytics)等功能。

## <a name="prerequisites-for-the-oms-connector"></a>OMS 連接器的先決條件
設定與 OMS 之連線的先決條件與[針對最新分支版本 1702 記載的先決條件](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites)相同。 以下重述該資訊：  

-   在您於 Configuration Manager 中安裝 OMS 連接器之前，您必須為 Configuration Manager 提供 OMS 的權限。 具體來說，您必須將「參與者存取權」授與包含 OMS Log Analytics 工作區的 Azure「資源群組」。 完成此動作的程序已記載於 Log Analytics 內容中。 請參閱 OMS 文件中的[為 Configuration Manager 提供 OMS 的權限](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)。

-   OMS 連接器必須安裝在裝載處於[線上模式](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation)之[服務連接點](/sccm/core/servers/deploy/configure/about-the-service-connection-point)的電腦上。

-   您必須在服務連接點上安裝適用於 OMS 的 Microsoft Monitoring Agent，以及 OMS 連接器。 Monitoring Agent 和 OMS 連接器必須設定為使用相同的「OMS 工作區」。 若要安裝代理程式，請參閱 OMS 文件中的[下載並安裝代理程式](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent)。
-   在您安裝連接器和代理程式之後，您必須設定 OMS 以使用 Configuration Manager 資料。 若要這樣做，請在 OMS 入口網站中[匯入 Configuration Manager 集合](/azure/log-analytics/log-analytics-sccm#import-collections)。

## <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>使用 Azure 服務精靈來設定與 OMS 的連線

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

## <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite-1702-and-earlier"></a>將資料從 Configuration Manager 同步處理至 Microsoft Operations Management Suite (1702 和較舊版本)


適用於：System Center Configuration Manager (1702 和先前版本)

您可以使用 Microsoft Operations Management Suite (OMS) 連接器同步處理資料 (例如從 System Center Configuration Manager 到 Microsoft Azure 中 OMS Log Analytics 的收集)。 這可在 OMS 中顯示 Configuration Manager 部署中的資料。
> [!TIP]
> OMS 連接器是發行前版本的功能。 若要深入了解，請參閱[使用更新的發行前版本功能](/sccm/core/servers/manage/pre-release-features)。

從 1702 版開始，您可以使用 OMS 連接器來連接到 Microsoft Azure Government Cloud 上的 OMS 工作區。 這需要您在安裝 OMS 連接器之前修改組態檔。 請參閱本主題中的[使用 OMS 連接器與 Azure Government Cloud](#fairfaxconfig)。

### <a name="prerequisites"></a>先決條件
- 在您於 Configuration Manager 中安裝 OMS 連接器之前，您必須為 Configuration Manager 提供 OMS 的權限。 具體來說，您必須將「參與者存取權」授與包含 OMS Log Analytics 工作區的 Azure「資源群組」。 完成此動作的程序已記載於 Log Analytics 內容中。 請參閱 OMS 文件中的[為 Configuration Manager 提供 OMS 的權限](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)。

- OMS 連接器必須安裝在裝載處於[線上模式](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation)之[服務連接點](/sccm/core/servers/deploy/configure/about-the-service-connection-point)的電腦上。

  如果您已將 OMS 連線到獨立主要站台，且計畫將管理中心網站新增至您的環境，您必須刪除目前的連線，然後在新的管理中心網站重新設定連接器。

- 您必須在服務連接點上安裝適用於 OMS 的 Microsoft Monitoring Agent，以及 OMS 連接器。  Monitoring Agent 和 OMS 連接器必須設定為使用相同的「OMS 工作區」。 若要安裝代理程式，請參閱 OMS 文件中的[下載並安裝代理程式](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent)。

- 在您安裝連接器和代理程式之後，您必須設定 OMS 以使用 Configuration Manager 資料。  若要這樣做，請在 OMS 入口網站中[匯入 Configuration Manager 集合](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections)。



### <a name="install-the-oms-connector"></a>安裝 OMS 連接器  
1. 在 Configuration Manager 主控台中，設定[階層以使用發行前版本功能](/sccm/core/servers/manage/pre-release-features)，然後啟用 OMS 連接器。  

2. 接下來，移至 [系統管理] > [雲端服務] > [OMS 連接器]。 在功能區中，按一下 [建立與 Operations Management Suite 的連線]。 這會開啟 「Connection to Operation Management Suite Wizard」 (與 Operations Management Suite 的連線精靈)。 選取 [下一步]。  


3.  在 [一般] 頁面上，確認您擁有下列資訊，然後選取 [下一步]。  
  - 將 Configuration Manager 註冊為「Web 應用程式和/或 Web API」管理工具，而且您擁有[來自此註冊的用戶端識別碼](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)。  
  - 在 Azure Active Directory 中，為已註冊的管理工具建立用戶端金鑰。  

  - 在 Azure 管理入口網站中，為已註冊的 Web 應用程式提供 OMS 存取權限 (如[為 Configuration Manager 提供 OMS 的權限](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)中所述)。  

4.  在 [Azure Active Directory] 頁面上，透過提供 [租用戶]、[用戶端識別碼] 和 [用戶端祕密金鑰] 設定 OMS 連線設定，然後選取 [下一步]。  

5.  在 [OMS 連線設定] 頁面上，填入 [Azure 訂用帳戶]、[Azure 資源群組] 和 [Operations Management Suite 工作區] 以提供連線設定。  工作區必須符合針對安裝在服務連接點上之 Microsoft 管理代理程式所設定的工作區。  

6.  確認 [摘要] 頁面上的連線設定，然後選取 [下一步]。 [進度] 頁面將會顯示連線狀態，然後應該會 [完成]。

將 Configuration Manager 連結至 OMS 之後，可以新增或移除集合，以及檢視 OMS 連線的內容。

### <a name="verify-the-oms-connector-properties"></a>確認 OMS 連接器屬性
1.  在 Configuration Manager 主控台中，移至 [系統管理] > [雲端服務]，然後選擇 [OMS 連接器] 以開啟 [OMS 連線]** 頁面。
2.  此頁面有兩個索引標籤︰
  - **Azure Active Directory：**   
    此索引標籤會顯示您的 [租用戶]、[用戶端識別碼]、[用戶端祕密金鑰到期日]，並可讓您確認用戶端祕密金鑰是否到期。

  - **OMS 連接屬性：**  
    此索引標籤會顯示 [Azure 訂用帳戶]、[Azure 資源群組]、[Operations Management Suite 工作區]，以及 Operations Management Suite 可取得其資料的裝置集合清單。 使用 [新增] 和 [移除] 按鈕修改允許的集合。

### <a name="fairfaxconfig"> </a> 使用 OMS 連接器與 Azure Government Cloud


1.  在任何已安裝 Configuration Manager 主控台的電腦上，編輯下列設定檔以指向 Government 雲端：&lt;CM 安裝路徑>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config

  **編輯︰**

    將設定名稱 *FairFaxArmResourceID* 的值變更為等於 “https://management.usgovcloudapi.net/”

   - **原始：** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;>&lt;/value>   
      &lt;/設定>

   - **已編輯：**     
      &lt;設定名稱="FairFaxArmResourceId" serializeAs="String"> &lt;>https://management.usgovcloudapi.net/&lt;/值>  
      &lt;/設定>

  將設定名稱 *FairFaxAuthorityResource* 的值變更為等於 "https://login.microsoftonline.com/"

  - **原始：**&lt;設定名稱="FairFaxAuthorityResource" serializeAs="String">   
    &lt;>&lt;/value>

    - **已編輯：**&lt;設定名稱="FairFaxAuthorityResource" serializeAs="String">   
    &lt;值>https://login.microsoftonline.com/&lt;/值>

2.  儲存具有這兩項變更的檔案之後，請重新啟動相同電腦上的 Configuration Manager 主控台，然後使用該主控台來安裝 OMS 連接器。 若要安裝連接器，請使用[將資料從 Configuration Manager 同步處理至 Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) 中的資訊，然後選取 Microsoft Azure Government 雲端上的 [Operations Management Suite 工作區]。

3.  安裝 OMS 連接器之後，即可在使用任何連線至該站台的主控台時連線 Government 雲端。
