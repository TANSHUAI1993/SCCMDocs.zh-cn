---
title: Technical Preview 1706 | Microsoft Docs
description: "了解 System Center Configuration Manager Technical Preview 1706 版中可用的功能。"
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d45f504dfe0a4c7852b0e2c8ff60d54005346c02
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1706-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1706 中的功能

適用於︰System Center Configuration Manager (Technical Preview)

本文介紹 System Center Configuration Manager Technical Preview 1706 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**此 Technical Preview 的已知問題：**

-   **移動發佈點** - 主控台中用來在站台間移動發佈點的選項不能與此版本搭配使用，因為 Technical Preview 限制使用單一主要站台。

-   **裝置合規性設定** - 使用下列兩個新裝置合規性設定時，您可能會遇到相反的行為：
    - **封鎖裝置上的 USB 偵錯**
    - **封鎖來自不明來源的應用程式**

        例如，如果系統管理員將 [封鎖裝置上的 USB 偵錯] 設定為 [true]，則所有未啟用 USB 偵錯的裝置都會標示為不符合規範。

**以下是您可以使用此版本試用的新功能。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>改進的軟體更新點界限群組
<!-- 1324591 -->
此版本包含對軟體更新點與界限群組搭配運作方式的改進。 以下摘要說明新的後援行為：
-   軟體更新點的後援現在使用一段可設定的時間來切換至後援的鄰近界限群組，可設定的時間下限為 120 分鐘。

-   不論後援設定為何，用戶端會在 120 分鐘內持續嘗試連線到最後所使用的軟體更新點。 在持續 120 分鐘都無法連線到該伺服器之後，用戶端就會檢查其集區中可用的軟體更新點，以便找出新的更新點。

  -   用戶端目前界限群組中的所有軟體更新點都會立即新增到用戶端的集區。

  -   由於用戶端在 120 分鐘內都會持續嘗試使用其原始伺服器，然後才會尋找新的伺服器，因此必須等到 2 小時過後，才會與其他伺服器連線。

  -   針對切換至後援的鄰近群組，如果設定了 120 分鐘下限，來自該鄰近界限群組的軟體更新點就會成為用戶端可用伺服器集區的一部分。

-   在持續兩小時都無法連線到其原始伺服器之後，用戶端就會切換到較短的新軟體更新點連線週期。

    這意謂著如果用戶端無法與新伺服器連線，它會迅速從可用伺服器集區中選取下一部伺服器，然後嘗試與該伺服器連線。

  -   這個週期會持續下去，直到用戶端連線到它可以使用的軟體更新點為止。
  -   在用戶端找到軟體更新點之前，當達到每個鄰近界限群組的後援時間時，系統會將額外的伺服器新增到可用伺服器集區。

如需詳細資訊，請參閱「最新分支」之＜界限群組＞主題中的[軟體更新點](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。


## <a name="site-server-role-high-availability"></a>站台伺服器角色高可用性
<!-- 1128774 -->
站台伺服器角色的高可用性是一個以 Configuration Manager 為基礎的解決方案，能夠安裝「被動」模式的額外主要站台伺服器。 被動模式站台伺服器是除了您現有「主動」模式主要站台伺服器以外的站台伺服器。 被動模式站台伺服器可在需要時立即可供使用。

被動模式的主要站台伺服器：
-   會使用與您主動站台伺服器相同的站台資料庫。
-   會接收一份主動站台伺服器內容庫複本，然後保持同步。
-   只要處於被動模式，便不會將資料寫入至站台資料庫。
-   只要處於被動模式，便不支援安裝或移除選用的站台系統角色。

若要將被動模式站台伺服器變成您的主動模式站台伺服器，您需以手動方式將它升階。 這會將主動站台伺服器切換成被動站台伺服器。 原始主動模式站台伺服器上可用的站台系統角色仍然可供使用，只要該電腦可供存取即可。 在主動與被動模式之間切換的只有站台伺服器角色。

若要安裝被動模式站台伺服器，您需使用「建立站台系統伺服器精靈」來設定 [類型] 為 [主要站台伺服器] 且 [模式] 為 [被動] 的新站台伺服器。 此精靈會接著在指定的伺服器上執行「Configuration Manager 安裝程式」，以安裝被動模式的新站台伺服器。 安裝完成之後，主動模式站台伺服器會讓被動模式站台伺服器及其內容庫與您對主動站台伺服器所做的變更或設定保持同步。

### <a name="prerequisites-and-limitations"></a>先決條件和限制
-   每個主要站台都支援一個被動模式的站台伺服器。

-   被動模式的站台伺服器可以是內部部署的站台伺服器，也可以是 Azure 中的雲端式站台伺服器。

-   主動模式與被動模式站台伺服器必須位於相同的網域中。

-   主動模式與被動模式站台伺服器必須使用相同的站台資料庫，此資料庫必須位於每部站台伺服器之電腦的遠端。

    -   裝載資料庫的 SQL Server 可以使用預設執行個體、具名執行個體、SQL Server 叢集或「Always On 可用性群組」。

    -   被動模式的站台伺服器已設定為使用與主動模式站台伺服器相同的站台資料庫。 不過，被動模式站台伺服器必須在升階為主動模式之後，才會使用該資料庫。

-   將執行被動模式站台伺服器的電腦：

    -   必須符合[安裝主要站台的必要條件](https://docs.microsoft.com/en-us/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site)。

    -   會使用與主動模式站台伺服器版本相符的來源檔案來進行安裝。

    -   在安裝被動模式站台之前，不能有來自任何站台的站台系統角色。

-   主動與被動模式站台伺服器電腦可以執行不同的作業系統或 Service Pack 版本，只要您的 Configuration Manager 版本同時支援它們兩者即可。

-   將被動模式站台伺服器升階為主動模式伺服器需手動執行。 並沒有任何自動容錯移轉機制。

-   站台系統角色只能安裝在主動模式的站台伺服器上。

    -   主動模式的站台伺服器支援所有站台系統角色。 您無法在處於被動模式的伺服器上安裝站台系統角色。

    -   使用資料庫 (例如報告點) 的站台系統角色必須讓該資料庫所在伺服器位於主動模式與被動模式站台伺服器的遠端。

    -   SMS_Provider 並不會在被動模式的站台伺服器上進行安裝。 由於您必須連線到該站台的 SMS_Provider，才能手動將被動模式站台伺服器升階為主動模式，因此建議您在額外的電腦上[至少安裝一個額外的提供者執行個體](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)。

**已知問題**：   
在此版本中，下列情況的「狀態」在主控台中會以數值的形式而不是以可讀的文字顯示：
-   131071 - 站台伺服器安裝失敗
-   720895 - 站台伺服器角色解除安裝失敗
-   851967 - 容錯移轉失敗

### <a name="add-a-site-server-in-passive-mode"></a>新增被動模式的站台伺服器
1.  在主控台中，移至 [系統管理] > [站台設定] > [站台]，然後啟動[新增站台系統角色精靈](/sccm/core/servers/deploy/configure/install-site-system-roles)。 您也可以使用「建立站台系統伺服器精靈」。

2.  在 [一般] 頁面上，指定將裝載被動模式站台伺服器的伺服器。 您指定的伺服器在安裝被動模式的站台伺服器之前，不能裝載任何站台系統角色。

3.  在 [系統角色選取] 頁面上，僅選取 [被動模式的主要站台]。

4.  為了完成精靈步驟，您必須提供下列資訊，這些資訊會用來在指定的伺服器上執行安裝程式並安裝站台伺服器角色：
    -   選擇將安裝檔案從主動站台伺服器複製到新的被動模式站台伺服器，或是指定一個包含主動站台伺服器之 [CD.Latest] 資料夾的位置路徑。

    -   指定與主動模式站台伺服器所用相同的站台資料庫伺服器和資料庫名稱。

5.  Configuration Manager 會接著在指定的伺服器上安裝被動模式的站台伺服器。

如需了解詳細的安裝狀態，請移至 [系統管理] > [站台設定] > [站台]。
-   被動模式站台伺服器的狀態會顯示為 [正在安裝]。

-   選取該伺服器，然後按一下 [顯示狀態] 來開啟 [站台伺服器安裝狀態]，以了解更多詳細資訊。



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>將被動模式站台伺服器升階為主動模式
當您想要將被動模式站台伺服器變更為主動模式時，需從 [系統管理] > [站台設定] > [站台] 中的 [節點] 窗格執行此操作。 只要您能夠存取 SMS_Provider 的執行個體，便能夠存取該站台來進行這項變更。
1.  在 Configuration Manager 主控台的 [節點] 窗格中，選取被動模式的站台伺服器，然後從功能區中選擇 [升階為主動]。

2.  您正在升階之伺服器的簡單 [狀態] 會在 [節點] 窗格中顯示為 [升階]。

3.  升階完成之後，新 [主動] 模式站台伺服器和新 [被動] 模式站台伺服器的 [狀態] 資料行都會顯示 [正常]。

4.  在 [系統管理] > [站台設定] > [站台] 中，主要站台伺服器的名稱現在會顯示新 [主動] 模式站台伺服器的名稱。
如需了解詳細狀態，請移至 [監視] > [站台伺服器狀態]。
    -   [模式] 資料行會指出哪一部伺服器為 [主動] 或 [被動]。

    -   將伺服器從被動模式升階為主動模式時，請選取要升階為主動的站台伺服器，然後從功能區中選擇 [顯示狀態]。 這會開啟 [站台伺服器升階狀態] 視窗，當中會顯示有關該程序的其他詳細資料。

當主動模式的站台伺服器切換到被動模式時，只有站台系統角色會變成被動。 所有安裝在該電腦上的其他站台系統角色仍然保持主動，並且可供其他用戶端存取。


### <a name="daily-monitoring"></a>每天監視
當您有被動模式的主要站台時，請每天監視它，以確保它與主動模式站台伺服器保持同步並且可供使用。 若要這樣做，請移至 [監視] > [站台伺服器狀態]。 您可以在此處同時檢視主動模式與被動模式站台伺服器。

[摘要] 索引標籤：
-   [模式] 資料行會指出哪一部伺服器為 [主動] 或 [被動]。
-   當被動模式伺服器與主動模式伺服器同步時，[狀態] 資料行會列出 [正常]。
-   若要檢視有關內容同步處理狀態的其他詳細資料，請從 [內容同步狀態] 按一下 [顯示狀態]。 這會開啟 [內容庫] 索引標籤，您可以在此處嘗試修正內容同步問題。

[內容庫] 索引標籤：
-   檢視從主動站台伺服器同步至被動模式站台伺服器之內容的 [狀態]。
-   您可以選取 [狀態] 為 [失敗] 的內容，然後從功能區中選擇 [同步處理所選項目]。 此動作會嘗試將該內容從內容來源重新同步至被動模式站台伺服器。 在復原期間，[狀態] 會顯示為 [進行中]，當同步時，則會顯示為 [成功]。

### <a name="try-it-out"></a>試試看！
請嘗試完成下列工作，然後從功能區的 [首頁] 索引標籤中傳送 [意見反應] 給我們，讓我們了解運作情況：
-   我可以安裝被動模式的主要站台。
-   我可以使用主控台將被動模式站台伺服器升階為主動模式站台伺服器，並確認這兩部站台伺服器的狀態變更。


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>在 Device Guard 原則中包含對特定檔案和資料夾的信任
<!-- 1324676 -->
在此版本中，我們已在 [Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) 原則管理中新增進一步的功能

您現在可以視需要在 Device Guard 原則中新增對特定檔案或資料夾的信任。 這可讓您：

1.  克服與受管理安裝程式相關的問題
2.  信任無法以 Configuration Manager 部署的商務營運應用程式
3.  信任作業系統部署映像中所包含的應用程式。

### <a name="try-it-out"></a>試試看！

1.  在您建立 Device Guard 原則時，於「建立 Device Guard 原則」精靈中，按一下 [新增]。
2.  在 [新增信任的檔案或資料夾] 對話方塊中，指定您想要信任的檔案或資料夾相關資訊。 您可以指定本機檔案或資料夾路徑，或是連線到您具備連線權限的遠端裝置，然後指定該裝置上的檔案或資料夾。
3.  完成精靈。


## <a name="hide-task-sequence-progress"></a>隱藏工作順序進度
<!-- 1354291 -->
在此版本中，您可以使用新的變數來控制對使用者顯示工作順序進度的時機。 請在您的工作順序中，使用 [設定工作順序變數] 步驟來設定 **TSDisableProgressUI** 變數的值，以隱藏或顯示工作順序進度。 您可以在工作順序中多次使用 [設定工作順序變數] 步驟，以變更此變數的值。 這可讓您在不同的工作順序區段中隱藏或顯示工作順序進度。

#### <a name="to-hide-task-sequence-progress"></a>隱藏工作順序進度
請在工作順序編輯器中，使用[設定工作順序變數](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)步驟，將 **TSDisableProgressUI** 變數的值設定為 **True**，以隱藏工作順序進度。

#### <a name="to-display-task-sequence-progress"></a>顯示工作順序進度
請在工作順序編輯器中，使用[設定工作順序變數](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)步驟，將 **TSDisableProgressUI** 變數的值設定為 **False**，以顯示工作順序進度。

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>針對安裝內容和解除安裝內容指定不同的內容位置
<!-- 1097546 -->
在現今的 Configuration Manager 中，您需指定包含應用程式安裝檔的安裝位置。 指定安裝位置時，這也會用來作為應用程式內容的解除安裝位置。
根據您的意見反應，當您想要將已部署的應用程式解除安裝，而該應用程式內容不在用戶端電腦上時，則用戶端會先重新下載所有應用程式安裝檔，然後才將應用程式解除安裝。
為了解決此問題，您現在可以指定安裝內容位置，也可以指定選用的解除安裝內容位置。 此外，您還可以選擇不指定解除安裝內容位置。

### <a name="try-it-out"></a>試試看！

1. 在應用程式的部署類型屬性中，按一下 [內容] 索引標籤。
2. 依照一般方式設定「安裝內容位置」。
3. 針對 [解除安裝內容設定]，選擇下列其中一個選項：
    - **與安裝內容相同** - 不論您是要進行應用程式安裝還是解除安裝，都會使用相同的內容位置。
    - **沒有解除安裝內容** - 如果您不想要提供應用程式的解除安裝內容位置，請選擇此選項。
    - **與安裝內容不同** - 如果您想要指定與安裝內容位置不同的解除安裝內容位置，請選擇此選項。
5. 如果您選取了 [與安裝內容不同]，請瀏覽至或輸入將用來將應用程式解除安裝的應用程式內容位置。
6. 按一下 [確定] 關閉部署類型內容對話方塊。


## <a name="accessibility-improvements"></a>協助工具改進  
<!--1253000 -->
此預覽版針對 Configuration Manager 主控台中的[協助工具功能](/sccm/core/understand/accessibility-features)引進數個改進。 它們包括：     

**可在整個主控台中四處移動的新鍵盤快速鍵：**
-   Ctrl + M - 將焦點設定在主要 (中央) 窗格上。
-   Ctrl + T - 將焦點設定至瀏覽窗格中的最上層節點。 如果焦點已經在該窗格中，則會將焦點設定至您瀏覽的最後一個節點。
-   Ctrl + I - 將焦點設定至功能區下的階層連結列。
-   Ctrl + L - 將焦點設定至 [搜尋] 欄位 (如果可用)。
-   Ctrl + D - 將焦點設定至詳細資料窗格 (如果可用)。
-   Alt - 將焦點在功能區內外切換。

**一般改進：**
-   改進當您輸入節點名稱的字母時在瀏覽窗格中的瀏覽。
-   在主要檢視和功能區的鍵盤瀏覽現在是採用循環方式。
-   在詳細資料窗格中的鍵盤瀏覽現在是採用循環方式。 若要返回上一個物件或窗格，請使用 Ctrl + D，然後使用 Shift + TAB。
-   重新整理 [工作區] 檢視之後，焦點會設定至該工作區的主要窗格。
-   修正問題，讓螢幕助讀程式能夠朗讀清單項目的名稱。
-   為頁面上多個控制項新增可存取的名稱，讓螢幕助讀程式能夠朗讀重要資訊。


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>為支援升級整備而對 Azure 服務精靈進行的變更
<!-- 1353331 -->
從此版本開始，請使用「Azure 服務精靈」來設定從 Configuration Manager 到[升級整備](/sccm/core/clients/manage/upgrade/upgrade-analytics)的連線。 使用此精靈可透過使用相關 Azure 服務的通用精靈，來簡化連接器的設定。   

雖然設定連線的方法已變更，但連線的先決條件及「升級整備」的使用方式仍維持不變。   

### <a name="prerequisites-for-upgrade-readiness"></a>升級整備的先決條件
[建立升級整備的連線](/sccm/core/clients/manage/upgrade/upgrade-analytics#create-a-connection-to-upgrade-readiness)的先決條件與針對 Configuration Manager 之「最新分支」詳述的先決條件相同。 為了方便起見，才在這裡重述：  

**先決條件**
-   若要新增連線，您的 Configuration Manager 環境必須先以[線上模式](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation)設定[服務連接點](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。 當您將連線新增至環境時，也會在執行此站台系統角色的電腦上安裝 Microsoft Monitoring Agent。
-   將 Configuration Manager 註冊為「Web 應用程式和/或 Web API」管理工具，並且取得[來自此註冊的用戶端識別碼](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/)。
-   在 Azure Active Directory 中，為已註冊的管理工具建立用戶端金鑰。
-   在 Azure 管理入口網站中，為已註冊的 Web 應用程式提供 OMS 存取權限 (如[為 Configuration Manager 提供 OMS 的權限](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms)中所述)。

> [!IMPORTANT]       
> 設定 OMS 存取權限時，請務必選擇 [參與者] 角色，並將所註冊應用程式之資源群組的權限指派給它。

設定完先決條件之後，您即已準備好使用此精靈來建立連線。

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>使用 Azure 服務精靈來設定升級整備
1.  在主控台中，移至 [系統管理] > [概觀] > [雲端服務] > [Azure 服務]，然後從功能區的 [首頁] 索引標籤中選擇 [設定 Azure 服務]，來啟動「Azure 服務精靈」。

2.  在 [Azure 服務] 頁面上，選取 [升級整備連接器]，然後按 [下一步]。

3.  在 [應用程式] 頁面上，指定您的 [Azure 環境] \(Technical Preview 僅支援 [公用雲端])。 然後，按一下 [匯入] 來開啟 [匯入應用程式] 視窗。

4.  在 [匯入應用程式] 視窗中，指定您 Azure AD 中已存在之 Web 應用程式的詳細資料。
    -   為 [Azure AD 租用戶名稱] 提供一個易記的名稱。 然後，指定 [租用戶識別碼]、[用戶端識別碼]、Azure Web 應用程式的祕密金鑰，以及 [應用程式識別碼 URI]。
    -   按一下 [驗證]，如果成功，請按一下 [確定] 來繼續作業。

5.   在 [設定] 頁面上，指定您想要與這個「升級整備」連線搭配使用的訂用帳戶、資源群組及「Windows Analytics 工作區」。  

6.  按 [下一步] 以移至 [摘要] 頁面，然後完成精靈步驟來建立連線。


## <a name="new-client-settings-for-cloud-services"></a>雲端服務的新用戶端設定
<!-- 1319883 -->

在此版本中，我們在 Configuration Manager 中新增了兩個新的用戶端設定。 您將在 [雲端服務] 區段中找到這些設定。  這些設定可提供您下列功能：

- 控制哪些 Configuration Manager 用戶端可以存取已設定的雲端管理閘道。
- 自動向 Azure Active Directory 註冊已加入網域的 Windows 10 Configuration Manger 用戶端。

這些新設定可協助您完成 [Configuration Manager 1705 Technical Preview](/sccm/core/get-started/capabilities-in-technical-preview-1705#new-capabilities-for-azure-ad-and-cloud-management) 中所述的功能。

### <a name="before-you-start"></a>開始之前

您必須已在內部部署 Active Directory 與 Azure AD 租用戶之間安裝並設定 Azure AD Connect。

如果您移除連線，系統並不會將裝置取消註冊，但將不會註冊任何新裝置。

### <a name="try-it-out"></a>試試看！

1. 使用[如何設定用戶端設定](/sccm/core/clients/deploy/configure-client-settings)中的資訊來設定下列用戶端設定 (可在 [雲端服務] 中找到) 區段。
    -   **自動向 Azure Active Directory 註冊新加入 Windows 10 網域的裝置** - 設定為 [是]\ (預設值) 或 [否]。
    -   **允許用戶端使用雲端管理閘道** - 設定為 [是] \(預設值) 或 [否]。
2.  將用戶端設定部署至所需的裝置集合。

若要確認裝置是否已加入 Azure AD，請在命令提示字元視窗中執行 **dsregcmd.exe /status** 命令。 如果裝置已加入 Azure AD 網域，結果中的 **AzureAdjoined** 欄位將會顯示 **YES**。

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台建立及執行 PowerShell 指令碼
<!-- 1236459 -->

在 Configuration Manager 中，您可以使用套件和程式將指令碼部署至用戶端裝置。 在此 Technical Preview 中，我們已新增可讓您採取下列動作的新功能：

- 將 PowerShell 指令碼匯入到 Configuration Manager
- 從 Configuration Manager 主控台編輯指令碼 (僅適用於未簽署的指令碼)
- 將指令碼標示為 [已核准] 或 [已拒絕] 以提升安全性
- 在 Windows 用戶端電腦及內部部署受管理 Windows 電腦的集合上執行指令碼。 您不須部署指令碼，它們會以近乎即時的方式在用戶端裝置上執行。
- 在 Configuration Manager 主控台中檢查指令碼所傳回的結果。


### <a name="prerequisites"></a>先決條件

若要使用指令碼，您必須是適當 Configuration Manager 安全性角色的成員。

- **若要匯入及撰寫指令碼** - 您的帳戶必須具備「合規性設定管理員」安全性角色中「SMS 指令碼」的「建立」權限。
- **若要核准或拒絕指令碼** - 您的帳戶必須具備「合規性設定管理員」安全性角色中「SMS 指令碼」的「核准」權限。
- **若要執行指令碼** - 您的帳戶必須具備「合規性設定管理員」安全性角色中「集合」的「執行指令碼」權限。

如需有關 Configuration Manager 安全性角色的詳細資訊，請參閱[以角色為基礎之系統管理的基礎](/sccm/core/understand/fundamentals-of-role-based-administration)。

使用者預設無法核准自己所撰寫的指令碼。 由於指令碼相當強大、用途廣泛且可部署至許多裝置，因此我們引進了能夠將指令碼撰寫者與指令碼核准者之角色分開的新概念。 這可針對執行指令碼而未受監督的情況提供一層額外的安全性。 您可以關閉這個次要核准功能以方便進行測試，特別是在 Technical Preview 版本期間。

允許使用者核准自己的指令碼：

1. 在 Configuration Manager 主控台中，按一下 [系統管理] 。
2. 在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。
3. 在站台清單中，選擇您的站台，然後在 [首頁] 索引標籤上的 [站台] 群組中，按一下 [階層設定]。
4. 在 [階層設定內容] 對話方塊的 [一般] 索引標籤上，取消選取 [不允許指令碼作者核准自己的指令碼]。


### <a name="try-it-out"></a>試試看！

#### <a name="import-and-edit-a-script"></a>匯入及編輯指令碼

1. 在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。
2. 在 [軟體程式庫] 工作區中，按一下 [指令碼]。
3. 在 [首頁] 索引標籤上的 [建立] 群組中，按一下 [建立指令碼]。
4. 在 [建立指令碼] 精靈的 [指令碼] 頁面上，設定下列資訊：
    - **指令碼名稱** - 輸入指令碼的名稱。 雖然可以使用相同名稱來建立多個指令碼，但這會讓您更難在 Configuration Manager 主控台中找出所需的指令碼。
    - **指令碼語言** - 目前僅支援 **PowerShell** 指令碼。
    - **匯入** - 將 PowerShell 指令碼匯入到主控台。 指令碼會顯示在 [指令碼] 欄位中。
    - **清除** - 將目前的指令碼從 [指令碼] 欄位中清除。
    - **指令碼** - 顯示目前已匯入的指令碼。 您可以視需要編輯此欄位中的指令碼。
5. 完成精靈。 新指令碼會顯示在 [指令碼] 清單中，其狀態為 [等候核准]。 您必須先核准此指令碼，才能在用戶端裝置上執行它。


#### <a name="approve-or-deny-a-script"></a>核准或拒絕指令碼



您必須先核准指令碼，才能執行它。 核准指令碼：

1. 在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。
2. 在 [軟體程式庫] 工作區中，按一下 [指令碼]。
3. 在 [指令碼] 清單中，選擇您想要核准或拒絕的指令碼，然後在 [首頁] 索引標籤上的 [指令碼] 群組中，按一下 [核准/拒絕]。
4. 在 [核准或拒絕指令碼] 對話方塊中，[核准] 或 [拒絕] 指令碼，並視需要輸入與您決策相關的註解。 如果您拒絕某個指令碼，它就無法在用戶端裝置上執行。
5. 完成精靈。 在 [指令碼] 清單中，[核准狀態] 資料行會隨著您採取的動作而發生變更。

#### <a name="run-a-script"></a>執行指令碼

指令碼經核准之後，就能在您選擇的集合上執行。

1. 在 Configuration Manager 主控台中，按一下 [資產與合規性]。
2. 在 [資產與相容性]  工作區中，按一下 [裝置集合] 。
3. 在 [裝置集合] 清單中，按一下要用來作為指令碼執行位置的裝置集合。
3. 在 [首頁] 索引標籤的 [所有系統] 群組中，按一下 [執行指令碼]。
4. 在 [執行指令碼] 精靈的 [指令碼] 頁面上，從清單中選擇一個指令碼。 此清單只會顯示已核准的指令碼。 按一下 [下一步] 完成精靈。

#### <a name="monitor-a-script"></a>監視指令碼

對用戶端裝置執行指令碼之後，請使用此程序來監視作業是否成功。

1. 在 Configuration Manager 主控台中，按一下 [監視] 。
2. 在 [監視] 工作區中，按一下 [指令碼結果]。
3. 在 [指令碼結果] 清單中，您可以檢視在用戶端裝置上執行之每個指令碼的結果。 指令碼結束代碼 **0** 通常表示指令碼已成功執行。

## <a name="pxe-network-boot-support-for-ipv6"></a>適用於 IPv6 的 PXE 網路開機支援
<!-- 1269793 -->
您現在可以啟用適用於 IPv6 的 PXE 網路開機支援，以開始工作順序作業系統部署。 當您使用此設定時，支援 PXE 的發佈點將可同時支援 IPv4 和 IPv6。 此選項不需要 WDS，並且如果 WDS 存在，就會將其停止。

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>啟用適用於 IPv6 的 PXE 開機支援
請使用下列程序來為 PXE 啟用支援 IPv6 的選項。

1. 在 Configuration Manager 主控台中，移至 [系統管理] > [概觀] > [發佈點]，然後按一下支援 PXE 之發佈點的 [內容]。
2. 在 [PXE] 索引標籤上，選取 [支援 IPv6] 來為 PXE 啟用 IPv6 支援。

## <a name="manage-microsoft-surface-driver-updates"></a>管理 Microsoft Surface 驅動程式更新
<!-- 1098490 -->
您現在可以使用 Configuration Manager 來管理 Microsoft Surface 驅動程式更新。

### <a name="prerequisites"></a>先決條件
所有軟體更新點都必須執行 Windows Server 2016。

### <a name="try-it-out"></a>試試看！
請嘗試完成下列工作，然後從功能區的 [首頁] 索引標籤中傳送 [意見反應] 給我們，讓我們了解運作情況：
1. 啟用 Microsoft Surface 驅動程式的同步處理。 請使用[設定分類和產品](/sccm/sum/get-started/configure-classifications-and-products)中的程序，並在 [分類] 索引標籤上選取 [包含 Microsoft Surface 驅動程式與韌體更新]，來啟用 Surface 驅動程式。
2. [同步處理 Microsoft Surface 驅動程式](/sccm/sum/get-started/synchronize-software-updates.md)。
3. [部署已同步處理的 Microsoft Surface 驅動程式](/sccm/sum/deploy-use/deploy-software-updates)

## <a name="configure-windows-update-for-business-deferral-policies"></a>設定 Windows Update for Business 延遲原則
<!-- 1290890 -->
您現在可以為 Windows Update for Business 直接管理的 Windows 10 裝置，設定 Windows 10「功能更新」或「品質更新」的延遲原則。 您可以在 [軟體程式庫] > [Windows 10 服務] 底下的新 [Windows Update for Business 原則] 節點中管理延遲原則。

### <a name="prerequisites"></a>先決條件
Windows Update for Business 所管理的 Windows 10 裝置必須能夠連線到網際網路。

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>建立 Windows Update for Business 延遲原則
1. 在 [軟體程式庫] > [Windows 10 服務] > [Windows Update for Business 原則] 中
2. 在 [首頁] 索引標籤的 [建立] 群組中，選取 [建立 Windows Update for Business 原則] 以開啟「建立 Windows Update for Business 原則精靈」。
3. 在 [一般] 頁面上，提供原則的名稱和描述。
4. 在 [延遲原則] 頁面上，設定是要延遲還是暫停「功能更新」。    
    「功能更新」通常是 Windows 的新功能。 在設定 [分支整備層級] 設定之後，您可以接著定義在 Microsoft 提供「功能更新」之後，是否要延遲接收「功能更新」，以及要延遲多久。
    - **分支整備層級**：設定裝置將接收其 Windows 更新的分支 (「最新分支」或「最新商務分支」)。
    - **延遲期 (天)**：指定「功能更新」的延遲天數。 您可以將這些「功能更新」的接收延遲 180 天 (自其發行日算起)。
    - **暫停功能更新開始**：選取是否要讓裝置在自暫停更新日算起最長可達 60 天的期間內，暫停接收「功能更新」。 在過了天數上限之後，暫停功能將自動失效，裝置將會掃描 Windows Update 是否有適用的更新。 進行此掃描之後，您可以再次暫停更新。 您可以取消選取此核取方塊來取消暫停「功能更新」。   
5. 選擇是要延遲還是暫停「功能更新」。     
    「品質更新」通常是對現有 Windows 功能的修正和改進，並且通常是在每個月的第一個星期二發佈，但是可由 Microsoft 隨時發行。 您可以定義在「品質更新」可供使用之後，是否要延遲接收「品質更新」，以及要延遲多久。
    - **延遲期 (天)**：指定「功能更新」的延遲天數。 您可以將這些「功能更新」的接收延遲 180 天 (自其發行日算起)。
    - **暫停品質更新開始**：選取是否要讓裝置在自暫停更新日算起最長可達 35 天的期間內，暫停接收「品質更新」。 在過了天數上限之後，暫停功能將自動失效，裝置將會掃描 Windows Update 是否有適用的更新。 進行此掃描之後，您可以再次暫停更新。 您可以取消選取此核取方塊來取消暫停「品質更新」。
6. 選取 [安裝來自其他 Microsoft 產品的更新]，以啟用讓延遲設定適用於 Microsoft Update 及 Windows Update 的群組原則設定。
7. 選取 [包含 Windows Update 的驅動程式] 以自動從 Windows Update 更新驅動程式。 如果您取消選取此設定，就不會從 Windows Update 下載驅動程式更新。
8. 完成精靈步驟以建立新的延遲原則。

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>部署 Windows Update for Business 延遲原則
1. 在 [軟體程式庫] > [Windows 10 服務] > [Windows Update for Business 原則] 中
2. 在 [首頁] 索引標籤的 [部署] 群組中，選取 [部署 Windows Update for Business 原則]。
3. 進行以下設定：
    - **要部署的設定原則**：選取您要部署的 Windows Update for Business 原則。
    - **集合**：按一下 [瀏覽] 以選取您要部署原則的集合。
    - **支援時補救不符合規範的規則**：選取此選項即可針對 Windows Management Instrumentation (WMI)、登錄、指令碼以及 Configuration Manager 所註冊行動裝置的所有設定，自動補救所有不符合規範的原則。
    - **允許在維護期間以外補救**：如果已針對您部署原則的集合設定維護期間，啟用此選項即可讓合規性設定在維護期間之外補救值。 如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](/sccm/core/clients/manage/collections/use-maintenance-windows)。
    - **產生警示**：設定一個警示，以在設定基準合規性於指定的日期和時間低於指定百分比時產生警示。 您也可以指定是否要將警示傳送至 System Center Operations Manager。
    - **隨機延遲 (小時)**：指定一個延遲時間範圍，以避免「網路裝置註冊服務」的處理時間過長。 預設值是 64 小時。
    - **排程**：指定在用戶端電腦上評估已部署之設定檔時所依據的合規性評估排程。 此排程可以是簡易或自訂排程。 當使用者登入時，用戶端電腦會評估此設定檔。
4.  完成精靈步驟以部署設定檔。



## <a name="support-for-entrust-certification-authorities"></a>針對 Entrust 憑證授權單位的支援
<!-- 1350740 -->
Configuration Manager 現在支援 Entrust 憑證授權單位；這使 PFX 憑證得以傳送到已在 Microsoft Intune 中註冊的裝置。

當您在 Configuration Manager 中新增「憑證登錄點」角色時，便可以將 Entrust 設定成憑證授權單位。 當新增發行 PFX 憑證的憑證設定檔時，您可以選取 Microsoft 或 Entrust 憑證授權單位。

**已知問題**：在 1706 Technical Preview 中，不會為 Microsoft 憑證授權單位發行 PFX 憑證。 這不會影響匯入的 PFX 憑證或 SCEP 設定檔。


## <a name="cisco-ipsec-support-for-macos-vpn-profiles"></a>針對 macOS VPN 設定檔的 Cisco (IPsec) 支援
<!-- 1321367 -->

您可以建立以 Cisco (IPsec) 作為連線類型的 macOS VPN 設定檔。 如需詳細資訊，請參閱[建立 VPN 設定檔](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles)。


## <a name="new-windows-configuration-item-settings"></a>新的 Windows 組態項目設定
<!-- 1354715 -->

在此版本中，我們新增了下列可供您在 Windows 設定項目中使用的新設定：

### <a name="password"></a>密碼

- **裝置加密**

### <a name="device"></a>裝置

- **修改區域設定 (僅限桌面)**
- **修改電源及睡眠設定**
- **修改語言設定**
- **修改系統時間**
- **修改裝置名稱**

### <a name="store"></a>市集

- **自動更新來自市集的應用程式**
- **僅使用私人市集**
- **啟動來自市集的應用程式**

### <a name="microsoft-edge"></a>Microsoft Edge

- **禁止存取 about: 旗標**
- **防止 SmartScreen 提示覆寫**
- **對檔案防止 SmartScreen 提示覆寫**
- **WebRTC localhost IP 位址**
- **預設搜尋引擎**
- **OpenSearch XML URL**
- **首頁 (僅限桌面)**

如需有關合規性設定的詳細資訊，請參閱[確定裝置合規性](/sccm/compliance/understand/ensure-device-compliance)。


## <a name="new-device-compliance-policy-rules"></a>新的裝置合規性政策規則

* **必要的密碼類型**。 指定使用者必須建立英數密碼還是數值密碼。 如果是英數密碼，您還需指定密碼必須包含的字元集數目下限。 字元集共有四種：小寫字母、大寫字母、符號和數字。

    **支援於：**
    * Windows Phone 8 或更新版本
    * Windows 8.1+
    * iOS 6 或更新版本
<br></br>
* **封鎖裝置上的 USB 偵錯**。 您不需要進行此設定，因為 Android for Work 裝置上已停用 USB 偵錯。

    **支援於：**
    * Android 4.0+
    * Samsung KNOX Standard 4.0 或更新版本
<br></br>
* **封鎖來自不明來源的應用程式**。 要求裝置必須防止來自不明來源的應用程式安裝。 您不需要進行此設定，因為 Android for Work 裝置一律會限制來自不明來源的安裝。

    **支援於：**
    * Android 4.0+
    * Samsung KNOX Standard 4.0 或更新版本
<br></br>
* **需要對應用程式進行威脅掃描**。 此設定會指定在裝置上啟用 [驗證應用程式] 功能。

    **支援於：**
    * Android 4.2 到 4.4
    * Samsung KNOX Standard 4.0 或更新版本

若要試用新的裝置合規性規則，請參閱[建立和部署裝置合規性政策](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy)。

## <a name="new-mobile-application-management-policy-settings"></a>新的行動應用程式管理原則設定
從此版本開始，您可以使用三個新的行動應用程式管理 (MAM) 原則設定：

- **封鎖螢幕擷取 (僅限 Android 裝置)：**指定在使用此應用程式時，封鎖裝置的螢幕擷取功能。

- **停用連絡人同步：**防止應用程式將資料儲存至裝置上的原生「連絡人」應用程式。

- **停用列印：**防止應用程式列印公司或學校資料。

若要試用新的應用程式保護原則設定，請參閱[使用 Configuration Manager 中的應用程式保護原則來保護應用程式](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies)。

## <a name="android-and-ios-enrollment-restrictions"></a>Android 和 iOS 的註冊限制
<!-- 1290826 -->
從此版本開始，系統管理員現在可以指定使用者不能在其混合式環境中註冊個人的 Android 或 iOS 裝置。 這可讓您將註冊的裝置僅限於已預先宣告的公司擁有裝置，或是透過「裝置註冊計劃」註冊的 iOS 裝置。

### <a name="try-it-out"></a>試試看
1. 在 Configuration Manager 主控台的 [系統管理] 工作區中，移至 [雲端服務] > [Microsoft Intune 訂閱]。
2. 在 [首頁] 索引標籤的 [訂閱] 群組中，選擇 [設定平台]，然後選取 [Android] 或 [iOS]。
3. 選取 [只允許在 Intune 中註冊預先宣告的裝置]。

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Android for Work 的應用程式複製貼上管理原則
我們已更新 Android for Work 之 [允許工作和個人設定檔之間的資料共用] 設定項目的設定描述。

|在 1706 Technical Preview 之前 | 新的選項名稱 | 行為|
|-|-|-|
|禁止跨邊界共用| 預設共用限制| 公司到個人：預設 (預期在所有版本上都封鎖) <br>個人到公司：預設 (在 6.x 以上的版本上允許，在 5.x 版本上封鎖)|
|沒有限制|   個人設定檔中的應用程式可以處理來自工作設定檔的共用要求| 公司到個人：允許  <br>個人到公司：允許|
|公司設定檔中的應用程式，可以處理來自個人設定檔的共用要求 |公司設定檔中的應用程式，可以處理來自個人設定檔的共用要求 |公司到個人：預設<br>個人到公司：允許<br>(僅適用於封鎖個人到公司的 5.x 版環境)|

這些選項全都不會直接防止複製貼上行為。 我們已在 1704 中將一個自訂設定新增到服務與「公司入口網站」應用程式，可用來防止複製貼上。 您可以透過自訂 URI 來進行此設定。

-   OMA-URI：./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
-   值類型：布林值

將 DisallowCrossProfileCopyPaste 設定為 true 可防止 Android for Work 個人與工作設定檔之間的複製貼上行為。

### <a name="try-it-out"></a>試試看
1. 在 Configuration Manager 主控台中，選取 [資產與合規性] > [概觀] > [合規性設定] > [設定項目]。
2. 選擇 [建立] 以建立新的設定項目，然後指定 [名稱] 和 [Android for Work]。
3. 在要設定的裝置設定群組中，選取 [工作設定檔]，然後選擇 [下一步]。
4. 選取 [允許工作與個人設定檔之間的資料共用] 的值，然後完成精靈步驟。

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>條件式存取之合規性政策的裝置健康情況證明評估
<!-- 1097546 -->
從此版本開始，您可以使用「裝置健康情況證明」狀態作為對公司資源進行條件式存取時的合規性政策規則。

### <a name="try-it-out"></a>試試看
選取某個「裝置健康情況證明」規則作為合規性政策評估的一部分。
