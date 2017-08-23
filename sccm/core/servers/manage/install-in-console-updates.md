---
title: "主控台內更新 | Microsoft Docs"
description: "System Center Configuration Manager 會與 Microsoft 雲端進行同步處理以取得更新，讓您可在主控台內安裝這類更新。"
ms.custom: na
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: "36"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 2bbc8935bee306ed0bc312cc43b8f5374a8df7ff
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>安裝適用於 System Center Configuration Manager 的主控台內更新

*適用於︰System Center Configuration Manager (最新分支)*

System Center Configuration Manager 會與 Microsoft 雲端服務同步以取得更新。 您接著可以在 Configuration Manager 主控台內安裝這些更新。

## <a name="get-available-updates"></a>取得可用的更新
只會針對您的階層，下載並提供適用於您的基礎結構和版本的更新。 根據您設定階層服務連接點的方式而定，此同步處理可以自動或手動執行︰

-   在 **線上模式**中，服務連接點會自動連線到 Microsoft 雲端服務，並下載適用的更新。  

     根據預設，Configuration Manager 每隔 24 小時就會檢查新的更新。 您也可以在 Configuration Manager 主控台的 [系統管理] > [更新與服務] 節點中選擇 [檢查更新]，來立即檢查更新。 (在 1702 版之前，此節點是位於 [系統管理] > [雲端服務] 底下)。

-   在**離線模式**中，服務連接點不會連線到 Microsoft 雲端服務。 若要在下載後匯入可用的更新，請[使用 System Center Configuration Manager 的服務連接工具](../../../core/servers/manage/use-the-service-connection-tool.md)。  

> [!NOTE]  
>   您可以將頻外修正程式匯入主控台。 若要這樣做，可使用[更新註冊工具](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)。 這些頻外修正程式可補充您與 Microsoft 雲端服務同步處理時取得的更新。


在同步處理更新之後，您便可以在 Configuration Manager 主控台中，移至 [系統管理] > [更新與服務] 節點來檢視它們︰  

-   您尚未安裝的更新會顯示為 **[可用]**。

-   您已安裝的更新會顯示為 **[已安裝]**。  只顯示最近安裝的更新。 您可以選擇功能區上的 [歷程記錄] 按鈕以檢視先前安裝的更新。



請先了解並規劃服務連接點的其他用途，再設定服務連接點。 下列使用可能會影響您如何設定此站台系統角色︰  

-   服務連接點用來上傳您站台的使用資訊。 這項資訊可協助 Microsoft 雲端服務找出適用於您基礎結構之目前版本的更新。 如需詳細資訊，請參閱 [System Center Configuration Manager 的診斷和使用方式資料](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)。  

-   您可以使用服務連接點搭配 Microsoft Intune 與 Configuration Manager 內部部署行動裝置管理功能，來管理裝置。 如需詳細資訊，請參閱[搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)。  

若要進一步了解下載更新時會發生什麼情況，請參閱：  

-   [流程圖 - 下載 System Center Configuration Manager 的更新](../../../core/servers/manage/download-updates-flowchart.md)

-   [流程圖 - System Center Configuration Manager 的更新複寫](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>指派檢視及管理更新和功能的權限
若要在主控台中檢視更新，使用者必須具備以角色為基礎的系統管理安全性角色，其中包含安全性類別「更新套件」。 此類別會授與您存取權，在 Configuration Manager 主控台中檢視和管理更新。    

**關於更新套件類別：**  
依預設， **[更新套件]** (SMS_CM_Updatepackages) 屬於下列內建安全性角色的一部分，並具有所列的權限︰
 -  具有**修改** 和 **讀取** 權限的 **系統高權限管理員** ：
    -   如果使用者具有此安全性角色和「所有」安全性範圍的存取權限，即可檢視和安裝更新。 使用者也可以在安裝期間啟用功能，並可在安裝更新之後啟用個別功能。
    - 如果使用者具有此安全性角色和「預設」安全性範圍的存取權限，即可檢視和安裝更新。 使用者也可以在安裝期間啟用功能，並可在安裝更新之後檢視功能。 但此使用者無法在安裝更新之後啟用這些功能。

- 具有**讀取** 權限的 **唯讀分析師** ：
  -  如果使用者具有此安全性角色和**預設**範圍的存取權限，即可檢視更新，但不能安裝更新。 此使用者也可以在安裝更新之後檢視功能，但不能加以啟用。

**更新和服務的必要權限：**   
  - 請使用已指派安全性角色的帳戶，並具有 **[更新套件]** 類別的 **修改** 和 **讀取** 權限。
  - 帳戶必須指派 **預設** 範圍。

**僅檢視更新的權限**：
  - 請使用已指派安全性角色的帳戶，並僅具有 **[更新套件]** 類別的 **讀取** 權限。
  - 帳戶必須指派 **預設** 範圍。

**安裝更新後啟用功能所需的權限︰**
  -  請使用已指派安全性角色的帳戶，並具有 **[更新套件]** 類別的 **修改** 和 **讀取** 權限。
  -  帳戶必須獲得 **所有** 範圍的指派。



##  <a name="bkmk_beforeinstall"></a> 安裝主控台內更新之前  
 在 Configuration Manager 主控台內安裝更新之前，請檢閱下列步驟。  

###  <a name="bkmk_step1"></a> 步驟 1︰檢閱更新檢查清單  
請檢閱適用的更新檢查清單，以了解開始更新之前應採取的動作︰

- 更新為 1606：請參閱[安裝更新 1606 的檢查清單](../../../core/servers/manage/checklist-for-installing-update-1606.md)。  

- 從 1606 更新為 1610：請參閱[安裝更新 1610 的檢查清單](../../../core/servers/manage/checklist-for-installing-update-1610.md)。  

- 從 1606 或 1610 更新為 1702：請參閱[安裝更新 1702 的檢查清單](../../../core/servers/manage/checklist-for-installing-update-1702.md)。

<!-- Removed as update guidance 6/6/2017. The Test DB Upgrade details are no longer recommended nor required. They live on in a new topic for customers who still want to use them. -->

###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>步驟 2︰安裝更新之前，先執行必要條件檢查程式  
安裝更新之前，請考慮執行該更新的必要條件檢查。 如果您在安裝更新之前先執行必要條件：  

-   更新檔案會在安裝更新之前複寫到其他站台。  

-   先決條件檢查會在您選擇安裝更新時再次自動執行。  

稍後在安裝更新時，您可以設定更新以忽略先決條件檢查警告。  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>安裝更新之前先執行必要條件檢查工具  

1.  在 Configuration Manager 主控台中，移至 [系統管理] > [更新與服務]。   

2.  以滑鼠右鍵按一下您想要執行必要條件檢查的更新套件。  

3.  選擇 **[執行必要條件檢查]**。  

     當您執行必要條件檢查時，更新的內容會複寫到子站台。  您可以檢視站台伺服器上的 distmgr.log，確認該內容複寫成功。  

4.  若要檢視檢查的結果，可在 Configuration Manager 主控台中，移至 [監視] > [更新與服務狀態]，然後尋找必要條件狀態。 您也可以檢視站台伺服器上的 ConfigMgrPrereq.log，來取得更多詳細資料。  



##  <a name="bkmk_install"></a> 安裝主控台內更新  
 當您準備好從 Configuration Manager 主控台內安裝更新時，請先由階層的頂層站台開始。 這可能是管理中心網站或獨立主要站台。  

 建議您在正常上班時間以外針對各個站台安裝更新，以將對企業營運的影響降到最低。 這是因為安裝更新可能包含重新安裝站台元件和站台系統角色之類的動作。  

-   當管理中心網站完成安裝更新之後，子主要站台就會自動啟動更新。 這是預設的建議程序。 不過，當主要站台安裝更新時，您可以使用[站台伺服器的服務保留時間](/sccm/core/servers/manage/service-windows)來進行控制。  

-   當主要父站台更新完成之後，請從 Configuration Manager 主控台內手動更新次要站台。 不支援次要站台伺服器的自動更新。  

-   當您在站台更新之後使用 Configuration Manager 主控台時，系統會提示您更新主控台。  

-  站台伺服器已成功完成更新安裝之後，便會自動更新所有適用的站台系統角色。  唯一要注意的是有關發佈點。 安裝更新時，所有的發佈點不會同時重新安裝和離線更新。 反之，站台伺服器會使用站台的內容發佈設定，逐一將更新發佈至發佈點子集。 這樣一來，只有部分發佈點會設為離線以安裝更新。 未開始更新或已完成更新的發佈點可保持線上狀態，以提供內容給用戶端。


###  <a name="bkmk_overview"></a> 主控台內更新安裝概觀  
**1.開始安裝更新時**  
您會看到更新精靈，其中顯示更新所適用的產品區域清單。  

-   在精靈的 **[一般]** 頁面中，您可以設定 **[必要條件警告]**。  
      -   必要條件錯誤一律會停止安裝更新。 先修正錯誤，才能成功重試更新安裝。 如需詳細資訊，請參閱 [重試失敗更新的安裝](#bkmk_retry) 。  

    -   必要條件警告也會停止安裝更新。 請先修正警告，再重試安裝更新。 如需詳細資訊，請參閱[重試失敗更新的安裝](#bkmk_retry)。  
    -   [忽略任何先決條件檢查警告並安裝此更新 (不管遺漏的必要項)] 選項會設定更新安裝的條件以忽略先決條件警告。 這允許繼續安裝更新。 如果您未選取此選項，更新安裝會在遇到警告時停止。 除非您先前已針對某個站台執行先決條件檢查並修正先決條件警告，否則不建議使用此選項。  

      [管理] 和 [監視] 兩工作區的 [更新與服務] 節點，其功能區中皆包含名為 [忽略先決條件警告] 的按鈕。 當更新套件無法完成安裝時，會產生先決條件檢查警告，此按鈕即變成可用。 例如，您從 [更新精靈] 安裝更新時未使用忽略必要條件警告的選項。 該更新安裝會停止並處於先決條件警告 (但不含錯誤) 的狀態。 稍後，您可以選擇功能區中的 [忽略先決條件警告]，觸發自動接續安裝要忽略先決條件警告的這項更新。 使用此選項時，會在幾分鐘後自動繼續安裝更新。



-   當有適用於 Configuration Manager 用戶端的更新時，即會顯示特定選項，讓您透過有限的用戶端來測試用戶端更新。 如需詳細資訊，請參閱[如何測試 System Center Configuration Manager 的進入生產階段前集合用戶端升級](../../../core/clients/manage/upgrade/test-client-upgrades.md)。  

**2.安裝更新期間**  
在安裝更新期間，Configuration Manager 會執行下列動作：  

-   重新安裝站台系統角色或 Configuration Manager 主控台這類任何受影響的元件。  

-   依據您為試驗用戶端以及[自動用戶端升級](https://technet.microsoft.com/library/mt627885.aspx)所選的項目，來管理用戶端的更新。  

-   除非已將 .NET 安裝為站台系統角色先決條件的一部分，否則更新期間將不會重新啟動站台系統伺服器。  

> [!TIP]  
>  安裝更新之後，Configuration Manager 也會更新 CD.Latest 資料夾。 此資料夾是在站台復原期間使用。  

**3.安裝更新時，監視更新的進度**  
使用下列動作來監視進度︰  

-   在 Configuration Manager 主控台中：[系統管理] > [更新與服務] 節點。 此節點會顯示所有更新套件的安裝狀態。


-   在 Configuration Manager 主控台中：[監視] > [概觀] > [更新與服務狀態] 節點。 此節點只會顯示目前正在安裝之更新套件的安裝狀態。  

    更新套件安裝細分成下列階段，以簡化監視。 每個階段都提供額外的詳細資料，包括檢視哪個記錄檔案以取得詳細資訊：  
    -   **下載** (這個階段僅適用於服務連接點站台安裝所在的頂層站台)。   

    -   **複寫**   

    -   **必要條件檢查**   

    -   **安裝**    

    -   **後續安裝** ([後續安裝工作](#post-installation-tasks)從 1610 版開始提供)。  

-   您可以檢視 **&lt;Configuration Manger 安裝目錄>\Logs** 中的 **CMUpdate.log** 檔案  

**4.安裝更新完成時**  
當第一個站台更新完成安裝之後︰  

-   子主要站台會自動安裝更新。 不需要進行其他動作。  

-   次要站台必須從 Configuration Manager 主控台內手動更新。
> [!TIP]
> 雖然主控台不會顯示次要站台的版本，但是您可以使用 Configuration Manager SDK 來確認站台的版本。 請參閱 [SMS_Site Server WMI Class](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx) (SMS_Site Server WMI 類別)。


-   在階層中的所有站台都更新至新版本之前，您的階層仍會以混合版本模式運作。 如需詳細資訊，請參閱 [Interoperability between different versions of System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md)。  

**5. 更新 Configuration Manager 主控台**  
在管理中心網站或主要站台更新之後，連線至該站台的每個 Configuration Manager 主控台也必須更新。 系統會提示您更新主控台︰  

-   當您開啟主控台時。  

-   當您在開啟的主控台中移至新節點時。  

建議您立即安裝更新。  

當主控台更新完成之後，您可以確認主控台和站台版本是正確的。 請移至主控台左上角的 [關於 System Center Configuration Manager]。  

###  <a name="bkmk_toptier"></a> 在頂層站台上開始安裝更新  
在您階層的頂層站台上，於 Configuration Manager 主控台中，移至 [系統管理] > [更新與服務]、選取 [可用] 更新，然後按一下 [安裝更新套件]。  

###  <a name="bkmk_secondary"></a> 在次要站台上開始安裝更新  
在更新次要站台的父主要站台之後，您可從 Configuration Manager 主控台內更新次要站台。  若要這樣做，您可以使用 **[升級次要站台精靈]**。  

1.  在 Configuration Manager 主控台中，移至 [系統管理] > [站台設定] > [站台]，並選取要更新的站台，然後在 [常用] 索引標籤的 [站台] 群組中選擇 [升級]。  

2.  按一下 **[是]** 以開始更新次要站台。  

若要監視次要站台上的更新安裝，請選取次要站台伺服器。 然後在 [常用] 索引標籤的 [站台] 群組中，選擇 [顯示安裝狀態]。 您也可以在主控台顯示中新增 **[版本]** 欄，讓您能夠檢視每個次要站台的版本。  

在次要站台成功更新之後，如果主控台中的狀態未重新整理或顯示更新失敗，請使用 [重試安裝] 選項。 這個選項不會重新為次要站台安裝已成功安裝的更新，但會強制主控台更新狀態。

### <a name="post-installation-tasks"></a>後續安裝工作
從 1610 版開始，您可以檢視後續安裝工作的相關資訊。

當站台安裝更新，有幾項工作在更新於站台伺服器上完成安裝之前都無法啟動。 以下是站台與階層作業的重要後續安裝工作清單。 它們非常重要，所以會主動予以監視。 未直接監視的其他工作包括重新安裝站台系統角色。 若要檢視重要的後續安裝工作狀態，請在監視站台的更新安裝時，選取 [後續安裝] 工作。

並非所有的工作都會立即完成。 有些工作在每個站台完成安裝更新之前不會啟動。 因此，您預期的新功能可能會延遲到這些工作完成之後才顯示。 例如，因為在所有站台完成更新安裝之前，開啟的新功能將不會啟動，所以有段時間可能看不到新的功能。

後續安裝工作包括：

-   **安裝 SMS_EXECUTIVE 服務**
  -   在站台伺服器上執行的重要服務。
  -   重新安裝此服務應會快速完成。


-   **安裝 SMS_DATABASE_NOTIFICATION_MONITOR 元件**
  -   SMS_EXECUTIVE 服務的重要站台元件執行緒。
  -   重新安裝此服務應會快速完成。


-   **安裝 SMS_HIERARCHY_MANAGER 元件**
  -   在站台伺服器上執行的重要站台元件。
  -   負責在站台系統伺服器上重新安裝站台系統角色。  不會顯示重新安裝個別站台系統角色的狀態。
  -   重新安裝此服務應會快速完成。


-   **安裝 SMS_REPLICATION_CONFIGURATION_MONITOR 元件**
  -   在站台伺服器上執行的重要站台元件。
  -   重新安裝此服務應會快速完成。


-   **安裝 SMS_POLICY_PROVIDER 元件**
  -   只在主要站台上執行的重要站台元件。
  -   重新安裝此服務應會快速完成。


-   **正在監視複寫初始化**   
  -   這只會顯示在管理中心網站和子主要站台。
  -   依存於 SMS_REPLICATION_CONFIGURATION_MONITOR。
  -   應會快速完成。


-   **更新 Configuration Manager 用戶端生產階段前套件**    
  -   這即使在用戶端生產階段前 (也稱為用戶端試驗) 還不能使用時也會顯示。
  -   在階層中的所有站台都完成安裝更新之前無法啟動。


-   **更新站台伺服器上的用戶端資料夾**
  -   如果您在生產階段前使用用戶端，則不會顯示這一項。  
  -   應會快速完成。


-   **更新 Configuration Manager 用戶端套件**
  -   如果您在生產階段前使用用戶端，則不會顯示這一項。  
  -   只有在所有站台都安裝更新之後，才會完成。  


-   **開啟功能**
  -   這只會在階層的頂層站台顯示。
  -   在階層中的所有站台都完成安裝更新之前無法啟動。
  -   不會顯示個別功能。


##  <a name="bkmk_retry"></a> 重試失敗更新的安裝  
當更新安裝失敗時，請檢閱主控台內的意見反應，以找出適用於警告和錯誤的解決方式。 您也可以檢視站台伺服器上的 ConfigMgrPrereq.log，來取得更多詳細資料。 重試安裝更新之前，您必須先修正錯誤，並且應該修正警告。  

> [!TIP]  
> 如果無法下載或複寫某個更新，您可以使用[更新重設工具](/sccm/core/servers/manage/update-reset-tool)。 此工具會於執行 1706 版或更新版本的站台上提供。 

當您準備好要重試安裝更新時，請選取失敗的更新，然後選擇適用的選項。 更新安裝重試行為取決於您啟動重試的節點以及所使用的重試選項。  

1.  **重試階層安裝︰**  
當更新處於下列其中一種狀態時，您可以重試整個階層的更新安裝︰  

    -   已通過先決條件檢查但有一或多個警告，而且未在 [更新精靈] 中設定略過先決條件檢查警告的選項 ([更新與服務] 節點中 [忽略先決條件警告] 的更新值是 [否])。   
    -   必要條件失敗    
    -   安裝失敗
    -   將內容複寫至站台失敗   

    移至 [系統管理] > [更新與服務]、選取更新，然後選擇下列其中一個選項：  

    -   **重試**：當您從這個節點執行 [重試] 時，更新安裝會再次啟動，並自動忽略先決條件警告。 如果先前複寫失敗，也會重新複寫更新的內容。
    - **忽略先決條件警告** - 從 1606 版開始，如果因為警告導致更新安裝停止，您可以選擇 [忽略先決條件警告]。 此動作會在幾分鐘後繼續安裝更新，並使用忽略必要條件警告的選項。   

2.  **重試站台的安裝︰**  
 當更新處於下列其中一種狀態時，您可以在特定站台上重試更新安裝︰  

    -   已通過先決條件檢查但有一或多個警告，而且未在 [更新精靈] 中設定略過先決條件檢查警告的選項。 ([更新與服務] 節點中 [忽略先決條件警告] 的更新值為 [否])。  
    -   必要條件失敗    
    -   安裝失敗    

    移至 [監視] > [概觀] > [站台服務狀態]、選取更新，然後按一下以下其中一個選項：

       - **重試** - 當您從這個節點執行 [重試] 時，只會重新啟動該站台的更新安裝。 但這項重試與從 [更新與服務] 節點中執行 [重試] 不同，其不會忽略先決條件警告。
       -    **忽略先決條件警告** - 從 1606 版開始，如果因為警告導致更新安裝停止，您可以按一下 [忽略先決條件警告]。 此動作會在幾分鐘後繼續安裝更新，並使用忽略必要條件警告的選項。

##  <a name="bkmk_after"></a> 當站台安裝更新之後  
使用下列檢查清單，完成站台更新之後所做的一般工作和設定。   

**確認站台對站台複寫正在作用中：**在 Configuration Manager 主控台中，移至下列位置來檢視狀態，並確認複寫正在作用中：  

-   **[監視]** > **[概觀]** > **[站台階層]**  

-   **[監視]** > **[概觀]** > **[資料庫複寫]**  

如需詳細資訊，請參閱[監視 System Center Configuration Manager 的階層及複寫基礎結構](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md)和[關於複寫連結分析師](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA)。  

 **確認站台伺服器和遠端站台系統伺服器已重新啟動 (如有必要)︰**檢閱您的站台基礎結構，並確保適用的站台伺服器和站台系統伺服器已成功重新啟動。 通常只有在 Configuration Manager 將 .NET 安裝為站台系統角色的必要項目時，站台伺服器才會重新啟動。  

 **更新獨立 Configuration Manager 主控台︰**確保所有遠端 Configuration Manager 主控台都會更新為相同的版本。 系統會在下列時機提示您更新主控台︰  

-   您在主控台中移至新節點。  

-   您開啟主控台。

**在主要站台上重新設定管理點的資料庫複本：** 如果您在主要站台上使用管理點的資料庫複本，就必須先解除安裝資料庫複本，才能更新站台。 更新主要站台之後，請重新設定管理點的資料庫複本。 如需詳細資訊，請參閱 [System Center Configuration Manager 的管理點資料庫複本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

**重新設定您在更新之前停用的任何資料庫維護工作：**如果您已在安裝更新之前停用站台上資料庫的[維護工作](../../../core/servers/manage/maintenance-tasks.md)，請在站台上重新設定這些工作。 請使用更新前已存在的相同設定。  

**升級用戶端：**如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

**額外的設定︰**檢閱您在開始更新之前所做的變更，然後將這些設定還原至您的站台和階層。  

##  <a name="bkmk_options"></a> 從更新啟用選擇性功能  
更新包含一或多個選擇性功能時，有機會在您的階層中啟用這些功能。  您可以在安裝更新時啟用功能，或者稍後返回主控台並啟用選擇性功能。

若要檢視可用的功能及其狀態，請在主控台中瀏覽至 [系統管理] > [更新與服務] > [功能]。

若功能非為選擇性，就會自動安裝，且不會出現在 [功能] 節點中。  


當您啟用新功能或發行前功能時，Configuration Manager 階層管理員 (HMAN) 必須在該功能提供使用前，先處理變更。 變更的處理通常立即進行，但可能需要 30 分鐘的時間完成，時間長度取決於 HAMN 處理循環。 在處理變更後，您必須先重新啟動主控台，才能檢視該功能相關的新 UI。


##  <a name="bkmk_prerelease"></a> 使用更新的發行前版本功能
發行前版本功能隨附於「最新分支」，可用來在生產環境中進行早期測試。 您可以在生產環境中使用這些功能，但不可視為已準備好用於生產環境。 深入了解[發行前版本功能](/sccm/core/servers/manage/pre-release-features)，包括如何在您的環境中啟用它們。             


## <a name="known-issues"></a>已知問題

###  <a name="bkmk_faq"></a> 為什麼我在主控台中看不到特定的更新？  
 如果您在與 Microsoft 雲端服務成功同步處理之後在主控台中找不到特定更新，這可能是因為︰  

-   更新需要您的基礎結構未使用的設定，或者目前的產品版本未滿足接收更新的必要條件。  

     如果您認為已具備某項更新的必要設定和先決條件，但仍缺少該項更新，請確認您的服務連接點處於線上模式。 然後使用 [更新與服務] 節點中的 [檢查更新] 選項來強制執行檢查。  若您處於離線模式，就必須使用服務連線工具，手動與雲端服務進行同步。  

-   您的帳戶缺少以角色為基礎的正確系統管理權限，無法在 Configuration Manager 主控台中檢視更新。

    請參閱本主題中的[管理更新的權限](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features)，以了解如何從主控台內檢視更新並啟用功能的必要權限。

### <a name="why-do-i-see-two-updates-for-version-1610"></a>為何看到兩個 1610 版更新？
檢視主控台中的更新時，可能會看到兩個更新都會安裝 1610 版。 這些更新有不同的日期。 下列其中一項條件成立時，即會同時出現：   
-   在提供 1610 版之後，您安裝了較早的版本 (例如 1606)

-   您的階層執行 1511 或 1602 版，但您還不能下載 1606 版

1610 版有兩個更新版本是因為在某些檔案的二進位檔進行一些微幅的變更之後，重新發行了此更新。 這些變更不會影響 Configuration Manager 或更新的功能。

主控台中提供兩個更新時，建議您安裝日期較近的更新。 但因為這兩個更新都會提供相同的功能，當您已安裝其中之一時，則不需要採取進一步的動作。
-   如果您先前已安裝較舊的更新，則不需要安裝的日期較新的更新。 不過，如果您在安裝第一個更新之後，安裝較新的更新，則會更新有問題的二進位檔。 不會有其他變更，您也不需要採取任何其他動作。

-   如果先前安裝過最新的更新，然後再安裝日期較舊的更新，則不需要採取其他動作。 這是因為您已安裝過較新的二進位檔，而不會再從原始的更新覆寫這些相同的二進位檔。
