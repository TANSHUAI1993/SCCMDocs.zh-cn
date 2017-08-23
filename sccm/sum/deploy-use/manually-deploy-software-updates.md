---
title: "手動部署軟體更新 | Microsoft Docs"
description: "若要手動部署更新，請從 Configuration Manager 主控台中選取更新並手動部署，或將更新新增至更新群組並部署群組。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: 2a0d5f12b99689749833c109d4fa399f99451d8a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_ManualDeploy"></a> 手動部署軟體更新  

適用於：System Center Configuration Manager (最新分支)

 在手動部署軟體更新的程序中，您將從 Configuration Manager 主控台選取軟體更新，然後手動啟動部署程序。 或者，您可以將選取的軟體更新新增到某個更新群組，然後手動部署更新群組。 您通常會使用手動部署方式以透過必要的軟體更新將用戶端裝置保持在最新狀態，然後才會建立 ADR 以管理進行中的每月軟體更新部署。 您也會使用手動方式來部署超出訊號範圍的軟體更新。 如果需要協助來判斷哪種部署方法最適合您，請參閱 [Deploy software updates](deploy-software-updates.md) (部署軟體更新)。

 下列各節會提供手動部署軟體更新的步驟。  

##  <a name="BKMK_1SearchCriteria"></a> 步驟 1：指定軟體更新的搜尋準則  
 在 Configuration Manager 主控台內，可能會顯示數以千計的軟體更新。 手動部署軟體更新工作流程的第一個步驟是找出您要部署的軟體更新。 例如，您可以提供某項準則，此一準則可擷取超過 50 個用戶端裝置需要的所有軟體更新，且包含 [安全性]  或 [重大]  軟體更新分類。  

> [!IMPORTANT]  
>  單一軟體更新部署內可容納的軟體更新數目上限為 1000。  

#### <a name="to-specify-search-criteria-for-software-updates"></a>指定軟體更新的搜尋準則  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫] 工作區中，展開 [軟體更新] ，然後按一下 [所有軟體更新] 。 隨即顯示已同步處理的軟體更新。  

    > [!NOTE]  
    >  在 [所有軟體更新] 節點上，Configuration Manager 只會顯示在過去 30 天內發行且分類為 [重大] 和 [安全性] 的軟體更新。  

3.  在搜尋窗格內使用以下其中一個步驟 (或兩個步驟都使用) 進行篩選，找出您需要的軟體更新。  

    -   在搜尋文字方塊中，輸入可篩選軟體更新的搜尋字串。 例如，輸入特定軟體更新的發行項識別碼或公告識別碼，或輸入會在數個軟體更新標題上出現的字串。  

    -   按一下 [新增準則] ，選取您要用來篩選軟體更新的準則，按一下 [新增] ，然後提供該準則的值。  

4.  按一下 [搜尋]  來篩選軟體更新：  

    > [!TIP]  
    >  您可使用選項，將篩選準則儲存在 [搜尋]  索引標籤和 [儲存]  群組內。  

##  <a name="BKMK_2UpdateGroup"></a> 步驟 2：建立含有軟體更新的軟體更新群組  
 軟體更新群組可提供您組織軟體更新的有效方法以準備進行部署。 您可以手動將軟體更新新增至軟體更新群組，或使用 ADR，Configuration Manager 會自動將軟體更新新增至全新或現有的軟體更新群組。 利用下列程序，將軟體更新手動新增至新的軟體更新群組。  

#### <a name="to-manually-add-software-updates-to-a-new-software-update-group"></a>手動將軟體更新新增至新的軟體更新群組  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫] 工作區中，按一下 [軟體更新] 。  

3.  選取要新增到新軟體群組的軟體更新。  

4.  在 [首頁]  索引標籤的 [更新]  群組中，按一下 [建立軟體更新群組] 。  

5.  指定軟體更新群組的名稱，並選擇是否要提供描述。 使用能為您提供足夠資訊的名稱和描述，來判斷哪一種類型的軟體更新應在軟體更新群組中。 若要進行，請按一下 [建立] 。  

6.  按一下 [軟體更新群組]  節點，顯示新的軟體更新群組。  

7.  選取軟體更新群組，然後在 [首頁]  索引標籤的 [更新]  群組中按一下 [顯示成員]  ，顯示此群組包括的軟體更新的清單。  

##  <a name="BKMK_3DownloadContent"></a> 步驟 3：下載軟體更新群組的內容  
 在部署軟體更新之前，您可以選擇下載已包含在軟體更新群組中的軟體更新內容。 您可以選擇執行此動作，以便您在部署軟體更新前先行確認該內容是否可在發佈點上使用。 這能協助您避免傳送內容時發生非預期問題。 您可以跳過此一步驟，即可將內容下載並複製到發佈點，作為部署程序的一部分。 利用下列程序，下載軟體更新群組中的軟體更新內容。  



#### <a name="to-download-content-for-the-software-update-group"></a>下載軟體更新群組內容
[!INCLUDE[下載更新](..\includes\downloadupdates.md)]
<!--- 1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group for which you want to download content.  

4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  

5.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  

7.  On the Distribution Settings page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**. --->

#### <a name="to-monitor-content-status"></a>若要監視內容狀態
1. 若要監視軟體更新的內容狀態，請按一下 Configuration Manager 主控台中的 [監視]。  

2. 在 [監視] 工作區中，展開 [發佈狀態] ，然後按一下 [內容狀態] 。  

3. 選取您之前找到的軟體更新套件，將軟體更新下載至軟體更新群組。  

4. 在 [首頁]  索引標籤的 [內容]  群組中，按一下 [檢視狀態] 。  

##  <a name="BKMK_4DeployUpdateGroup"></a> 步驟 4：部署軟體更新群組  
 在決定您要部署的軟體更新之後，將這些軟體更新新增到軟體更新群組，您就可以在軟體更新群組中手動部署軟體更新。 利用下列程序，將軟體更新手動部署至新的軟體更新群組。  

#### <a name="to-manually-deploy-the-software-updates-in-a-software-update-group"></a>在軟體更新群族內手動部署軟體更新  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫] 工作區中，展開 [軟體更新] ，並按一下 [軟體更新群組] 。  

3.  選出您要部署的軟體更新群組。  

4.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [部署] 。 這會開啟 [部署軟體更新精靈]  。  

5.  在 [一般] 頁面，指定以下設定：  

    -   **名稱**：指定部署的名稱。 部署必須擁有可描述部署目的的唯一名稱，並區隔其在 Configuration Manager 網站中的其他部署。 根據預設，Configuration Manager 會自動以下列格式提供部署名稱：**Microsoft Software Updates -** <日期><時間>。  

    -   **描述**：指定部署的描述。 描述會提供部署的概觀，以及其它可協助您在 Configuration Manager 網站內找出並區分的部署。 描述欄位是選用欄位，長度限制為 256 字元，預設為空白值。  

    -   **軟體更新/軟體更新群組**：確認顯示的軟體更新群組或軟體更新正確。  

    -   **選取部署範本**：指定是否要套用先前儲存的部署範本。 您可以設定一個部署範本以包含多個常見軟體更新部署內容，然後在部署後續軟體更新時套用範本，以確保相似部署之間的一致性，並可節省時間。  

    -   **集合**：在適用的情況下指定用於部署的集合。 集合內的成員會收到部署中定義的軟體更新。  

6.  在 [部署設定] 頁面，指定以下設定：  

    -   **部署的類型**：指定軟體更新部署的部署類型。 選取 [必要]  ，建立強制軟體更新部署，此時會在設定安裝期限前自動在用戶端上安裝軟體更新。 選取 [可用]  建立選用的軟體更新部署，以便使用者經由軟體中心進行安裝。  

        > [!IMPORTANT]  
        >  建立軟體更新部署後，您之後就不能變更部署類型。  

        > [!NOTE]  
        >  作為 [必要]  部署的軟體更新群組會在背景中下載，並在設有 BITS 設定的情況下加以執行。  
        > 不過，作為 [可用]  部署的軟體更新群組則會在幕前下載，並忽略 BITS 設定。  

    -   **使用網路喚醒來喚醒用戶端進行必要的部署**：指定是否於期限啟用網路喚醒，將喚醒封包傳送到在部署中需要一或多個軟體更新的電腦。 安裝期限時處於睡眠模式的任何電腦都會喚醒，如此即可起始軟體更新安裝。 在部署中處於睡眠狀態且不需要任何軟體更新的用戶端並不會啟動。 根據預設，並未啟用此設定，且僅於 [部署的類型]  設定至 [必要] 時才可使用。  

        > [!WARNING]  
        >  您必須為電腦和網路設定 [網路喚醒] 後，才可以使用此選項。  

    -   **詳細等級**：針對由用戶端電腦報告的狀態訊息，指定詳細等級。  

7.  在 [排程] 頁面，設定以下設定：  

    -   **排程評估**：指定是否要根據執行 Configuration Manager 主控台的電腦上 UTC 或本機時間，來評估可用的時間和安裝期限時間。  

        > [!NOTE]  
        >  當您選取本機時間，然後針對 [軟體可用時間] 或 [安裝期限] 選取 [盡快] 時，就會使用執行 Configuration Manager 主控台之電腦上的目前時間，來評估更新可用時間或更新安裝於用戶端的時間。 如果在用戶端位於其他時區，則會在用戶端的時間達到評估時間時，執行這些動作。  

    -   **軟體可用時間**：選取以下其中一種設定來指定用戶端可以使用軟體更新的時間：  

        -   **盡快**：選取此設定可讓部署中的軟體更新在最短時間內供用戶端使用。 建立部署時，會更新用戶端原則，用戶端則會察覺在下一個用戶端原則輪詢循環中的部署，然後就可以使用並安裝軟體更新。  

        -   **特定時間**：選取此設定可讓用戶端在特定日期和時間使用部署中的軟體更新。 建立部署時，會更新用戶端原則，用戶端則會察覺在下一個用戶端原則輪詢循環中的部署。 不過，在特定日期和時間前，無法使用並安裝部署中的軟體更新。  

    -   **安裝期限**：選取以下其中一種設定來指定部署中軟體更新的安裝期限。  

        > [!NOTE]  
        >  只有在 [部署設定] 頁面上的 [部署的類型]  設定為 [必要]  時，您才可以設定安裝期限設定。  

        -   **盡快**：選取此設定可在最短時間內自動安裝部署中的軟體更新。  

        -   **特定時間**：選取此設定可在特定日期和時間自動安裝部署中的軟體更新。  

        > [!NOTE]  
        >  實際安裝的期限時間是您所設定的特定時間，加上最多 2 小時的隨機總時間。 這能減少對同時在部署中安裝軟體更新之目的地集合裡所有用戶端電腦的潛在影響。  
        >   
        >  您可以設定 [電腦代理程式]  用戶端設定的 [停用期限隨機設定]  ，針對必要的軟體更新停用安裝隨機延遲。 如需詳細資訊，請參閱 [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent)。  

8.  在 [使用者經驗] 頁面，設定以下設定：  

    -   **使用者通知**：指定是否要在設定的 [軟體可用時間]  ，於用戶端電腦上 [軟體中心] 內顯示軟體更新的通知，以及是否要在用戶端電腦上顯示使用者通知。 [部署設定] 頁面上的 [部署的類型]  設定為 [可用]  時，您不能選取 [在軟體中心和所有通知中隱藏] 。  

    -   **期限行為**：*只有在 [部署設定] 頁面上的 [部署的類型] *設定為 [必要] *時才可使用。*   
    指定到達軟體更新部署期限時會出現的行為。 指定是否安裝部署中的軟體更新。 同時也指定是否於無論設定之維護期間為何的狀況下，只要軟體更新安裝完成，就執行系統重新啟動。 如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。  

    -   **裝置重新啟動行為**：*只有在 [部署設定] 頁面上的 [部署的類型] *設定為 [必要] *時才可使用。*    
    於安裝軟體更新，且需要重新啟動系統才能完成安裝的狀況下，指定是否抑制在伺服器和工作站上重新啟動系統。  

        > [!IMPORTANT]  
        >  在伺服器環境中，或者是您不想讓安裝軟體更新的電腦根據預設重新啟動時，抑制系統重新啟動是很有用的。 不過，如此一來就會讓電腦處於不安全的狀態，允許強制重新啟動則可協助確保軟體更新安裝能立即完成。

    -   **Windows Embedded 裝置的寫入篩選器處理**：將軟體更新部署至啟用寫入篩選器的 Windows Embedded 裝置時，您可以指定在暫時重疊上安裝軟體更新，並於稍後再認可變更，或是在安裝期限或維護期間認可變更。 當您在安裝期限或維護期間認可變更時，需要重新啟動裝置才能保存裝置的變更。  

        > [!NOTE]  
        >  當您將軟體更新部署至 Windows Enbedded 裝置時，請確認裝置是已設定維護期間之集合的成員。  

    - **重新啟動時的軟體更新部署重新評估行為**︰從 Configuration Manager 版本 1606 開始，選取此設定來設定軟體更新部署，讓用戶端能夠在用戶端安裝軟體更新和重新啟動之後立即執行軟體更新相容性掃描。 這可讓用戶端檢查是否有在用戶端重新啟動後變成適用的其他軟體更新，然後在同一個維護期間內安裝這些更新 (而變成相容)。

9. 於 [警示] 頁面上設定 Configuration Manager 和 System Center Operations Manager 如何針對此部署產生警示。 只有在 [部署設定] 頁面上的 [部署的類型]  設定為 [必要]  時，您才可以設定警示。  

    > [!NOTE]  
    >  您可經由 [軟體程式庫]  工作區中的 [軟體更新]  節點檢閱最新的軟體更新警示。  

10. 在 [下載設定] 頁面，設定以下設定：  

    - 指定當用戶端連線到速度較慢的網路，或使用後援內容位置時，是否要下載並安裝軟體更新。  

    - 指定無法在慣用發佈點使用軟體更新內容時，是否要讓用戶端從後援發佈點下載並安裝軟體更新。  

    - **允許用戶端與同一個子網路上的其他用戶端共用內容**：指定是否允許針對下載內容使用 BranchCache。 如需 BranchCache 的詳細資訊，請參閱[內容管理的概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)。  

    - **如果在目前、鄰近或網站群組的發佈點上找不到軟體更新，則從 Microsoft Update 下載內容**：選取這個設定可讓連線至內部網路的用戶端，在發佈點上找不到軟體更新時從 Microsoft Update 下載軟體更新。 可連上網際網路的用戶端隨時可移至 Microsoft Update 取得軟體更新內容。

    - 指定當用戶端使用計量付費網際網路連線時，是否在過了安裝期限後仍允許用戶端進行下載。 在您處於計量付費網際網路連線時，網際網路提供者有時會根據您傳送和接收的資料量來收取費用。  

    > [!NOTE]  
    >  用戶端會從部署內軟體更新的管理點來請求內容位置。 下載行為會根據您如何設定發佈點、部署套件和本頁設定而定。 如需詳細資訊，請參閱 [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  

11. 如果您已執行 [步驟 3：下載軟體更新群組的內容](#BKMK_3DownloadContent)，就不會顯示部署套件、發佈點和語言選擇頁面，所以您可以跳至精靈步驟 15。  

    > [!IMPORTANT]  
    >  先前已經下載到網站伺服器上內容庫的軟體更新，不能再次下載。 即使在您針對軟體更新建立新的部署套件時，也是一樣。 若之前已經先下載所有的軟體更新，精靈會跳到 [語言選擇]  頁面 (步驟 15)。  

12. 在 [部署套件] 頁面上選取現有部署套件，或進行以下設定，以指定新的部署套件：  

    1.  **名稱**：指定部署套件的名稱。 此名稱必須是描述套件內容的唯一名稱。 長度限制為 50 個字元。  

    2.  **描述**：指定描述，提供部署套件的相關資訊。 描述限制為 127 個字元。  

    3.  **套件來源**：指定軟體更新來源檔案的位置。  輸入來源位置的網路路徑，例如 **\\\伺服器\共用名稱\路徑**，或按一下 **[瀏覽]** 尋找網路位置。 您必須先建立部署套件來源檔案的共用資料夾，才能繼續前往下一個頁面。  

        > [!NOTE]  
        >  您指定的部署套件來源位置不能供另一個軟體部署套件使用。  

        > [!IMPORTANT]  
        >  SMS 提供者電腦帳戶和執行精靈下載軟體更新的使用者，都必須具有下載位置的 **寫入** NTFS 權限。 您應謹慎限制下載位置的存取權，以降低攻擊者竄改軟體更新來源檔案的風險。  

        > [!IMPORTANT]  
        >  您可以在 Configuration Manager 建立部署套件之後，變更部署套件內容中的套件來源位置。 不過，如果您這樣做，則必須先將內容從原始套件來源複製到新的套件來源位置。  

    4.  **傳送優先順序**：指定部署封裝的傳送優先順序。 Configuration Manager 將套件傳送到發佈點時，會針對部署套件使用傳送優先順序。 部署套件會依優先順序傳送：高、中或低。 優先順序相同的套件，會依照建立的順序傳送。 若沒有積存，則無論其優先順序為何，都會立即處理該套件。  

13. 在 [發佈點] 頁面上，指定將裝載軟體更新檔案的發佈點或發佈點群組。 如需發佈點的詳細資訊，請參閱[發佈點設定](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)。  

14. 在 [下載位置] 頁面上，指定要從網際網路或您的區域網路下載軟體更新檔案。 進行以下設定：  

    -   **從網際網路下載軟體更新**：選取此設定可從網際網路上指定的位置下載軟體更新。 預設會啟用此設定。  

    -   **從區域網路上的位置下載軟體更新**：選取此選項可從本機資料夾或共用網路資料夾下載軟體更新。 此設定在執行精靈的電腦沒有網際網路存取時很實用。 可以從具備網際網路存取的任何電腦上初步下載軟體更新，然後儲存在本機網路上的某個位置，以便後續存取進行安裝。  

15. 在 [語言選擇] 頁面上，選取選定之軟體更新所下載的語言。 軟體更新只會在有提供所選取的語言時才能下載。 無指定語言的軟體更新，則都會下載的。 根據預設，精靈會選取您在軟體更新點內容中設定的語言。 您必須至少選取一種語言才能繼續至下一頁。 如果您只選取軟體更新不支援的語言，則軟體更新下載將會失敗。  

16. 在 [摘要] 頁面上檢閱設定。 若要將設定儲存至部署範本，請按一下 [儲存成範本] ，輸入名稱，並選取要納入範本的設定，然後按一下 [儲存] 。 若要變更已經設定的設定，請按一下相關聯的精靈頁面，然後變更設定。  

    > [!WARNING]  
    >  範本名稱可以包含英數字 ASCII 字元以及 **\\** (反斜線) 或 **'** (單引號)。  

17. 按 [下一步]  部署軟體更新。  

 完成精靈後，Configuration Manager 會將軟體更新下載到站台伺服器的內容庫中，並將軟體更新發佈到設定的發佈點，接著將軟體更新群組部署到目標集合內的用戶端。 如需部署程序的詳細資訊，請參閱 [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess)。

## <a name="next-steps"></a>後續步驟
[監視軟體更新](monitor-software-updates.md)
