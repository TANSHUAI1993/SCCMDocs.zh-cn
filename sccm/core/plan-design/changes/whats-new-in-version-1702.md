---
title: "1702 新版 |Microsoft Docs"
description: "下列各節提供 System Center Configuration Manager 1702 版中的變更和推出的新功能。"
ms.custom: na
ms.date: 05/02/2017
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a2954b3c6f9a09b7246347e780c4cfc49ba39ca1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>System Center Configuration Manager 1702 版的新功能

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager Update 1702 最新分支以主控台內更新形式提供，適用於先前安裝、執行 1602、1606 或 1610 版本的站台。 它也當作基準版本來提供，可用於安裝新的部署。

> [!TIP]  
> 若要安裝新的站台，您必須使用 Configuration Manager 的基準版本。  
>  深入了解：    
>   - [安裝新的站台](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [在站台安裝更新](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [基準和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

下列各節提供 Configuration Manager 1702 版中的變更和推出的新功能詳細資料。  

## <a name="deprecated-features-and-operating-systems"></a>已淘汰的功能和作業系統
在於[已移除和已淘汰的功能](/sccm/core/plan-design/changes/removed-and-deprecated-features)中實作支援變更之前，先了解這些變更。

1702 版已捨棄對下列產品的支援：
- **SQL Server 2008 R2** (適用於站台資料庫伺服器)。 [首次宣佈](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-support-for-sql-server-versions-as-a-site-database)淘汰支援是在 2015 年 7 月 10 日。 當您使用 1702 版之前的 Configuration Manager 版本時，仍可支援此版本的 SQL Server。
- **Windows Server 2008 R2** (適用於站台系統伺服器和大多數站台系統角色)。 [首次宣佈](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems)淘汰支援是在 2015 年 7 月 10 日。 當您使用 1702 版之前的 Configuration Manager 版本時，仍可支援此版本的 Windows。  
- **Windows Server 2008** (適用於站台系統伺服器和大多數站台系統角色)。 [首次宣佈](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems)淘汰支援是在 2015 年 7 月 10 日。
- **Windows XP Embedded** (作為用戶端作業系統)。 [首次宣佈](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems)淘汰是在 2015 年 7 月 10 日。 當您使用 1702 版之前的 Configuration Manager 版本時，仍可支援此版本的 Windows。




## <a name="site-infrastructure"></a>站台基礎結構

### <a name="improvements-for-in-console-search"></a>主控台內搜尋的新增功能
以下是針對在 Configuration Manager 主控台中使用搜尋所做的一些改進︰
 - **物件路徑︰**  
  許多物件現在都支援名為 [物件路徑] 的欄。  當您搜尋並將此欄位包含在顯示結果時，您可以檢視每個物件的路徑。 例如，如果您對 [應用程式] 節點中的應用程式執行搜尋，而且也搜尋子節點，則結果窗格中的 [物件路徑] 欄會顯示所傳回之每個物件的路徑。   

- **保留搜尋文字︰**  
  當您在搜尋文字方塊中輸入文字，然後在搜尋子節點和目前節點之間切換時，您所輸入的文字現在會保存並可供新搜尋使用，而不必重新輸入。

- **保留搜尋子節點的決定︰**  
 當您變更所使用的節點時，現在會保存您針對搜尋「目前節點」或「所有子節點」所選擇的選項。 這個新行為意謂著當您在主控台中四處移動時，不需要經常重設這項決定。 根據預設，當您開啟主控台時，選項會是只搜尋目前的節點。


### <a name="send-feedback-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台傳送意見反應

 您可以使用主控台內的意見反應選項，將意見反應直接傳送給開發小組。

 您可以找到 [意見反應] 選項：
 -  在功能區中，於每個節點的 [常用] 索引標籤的最左邊。  
    ![功能區](./media/feedback-home.png)

 -  以滑鼠右鍵按一下主控台中的任何物件時。   
     ![按一下滑鼠右鍵選項](./media/feedback-option.png)   

 選擇 [意見反應] 會開啟瀏覽器並進入 [Configuration Manager UserVoice 意見反應網站](https://go.microsoft.com/fwlink/?linkid=617029)。


###  <a name="changes-for-updates-and-servicing"></a>更新與服務的變更
以下是 [更新與服務] 的變更：

- **節點位置**   
  安裝 1702 版之後，[更新與服務] 節點會顯示為 [系統管理] 底下的最上層節點。 它已不再是 [雲端服務] 底下的子節點。

- **新的更新狀態**  
  當您在主控台中檢視可用的更新時，有兩種新狀態：  
  - **可供安裝** - 這是已下載且已經可以安裝的更新。
  - **可供下載** - 此更新可供使用，但尚未下載。 您可以選擇下載此更新，但已有較新的更新取代它。


- **更為簡單的更新選項**  
  下次您的基礎結構可以進行兩個以上的更新時，只會下載最新的更新。 例如，如果您的目前站台版本是比可用的最新版本還要舊兩個以上版本的版本，則只會自動下載該最新更新版本。  

  您可以選擇下載並安裝其他可用的更新，即使它們並非最新的版本。 如果您下載較舊的更新，您將會收到已有較新的更新取代該項更新的警告。 若要下載 [可供下載] 的更新，請選取主控台中的更新，然後按一下 [下載]。

- **改善較舊更新的清理**   
  我們已新增自動清理函式，可刪除站台伺服器的 'EasySetupPayload' 資料夾中不需要的下載。 由於這是隨 1702 版導入的，因此在安裝後續更新 (例如更新彙總套件或未來的更新版本) 之後，清理才會開始發揮作用。  


### <a name="data-warehouse-service-point"></a>資料倉儲服務點
 使用資料倉儲服務點來儲存並報告您的 Configuration Manager 部署的長期歷程記錄資料。

 資料倉儲支援高達 2 TB 的資料，其含有變更追蹤的時間戳記。 資料儲存可透過從 Configuration Manager 站台資料庫自動同步處理至資料倉儲資料庫來完成。 然後即可從您的 Reporting Services 點存取此資訊。

 如需詳細資訊，請參閱[資料倉儲服務點](/sccm/core/servers/manage/data-warehouse)。


### <a name="peer-cache-improvements"></a>對等快取改善
 從 1702 版開始，當對等快取來源電腦符合下列任一條件時，對等快取來源電腦將會拒絕內容要求︰  
  -  處於電力偏低模式。
  -  CPU 負載會在要求內容時超過 80%。
  -  磁碟 I/O 的 *AvgDiskQueueLength* 超過 10。
  -  無法再連線至電腦。   
如需詳細資訊，請參閱 [Configuration Manager 用戶端的對等快取](/sccm/core/plan-design/hierarchy/client-peer-cache)中的 ＜受限的對等快取來源存取＞。   

此外，還在您的報告點新增了三個新報告。 您可以使用這些報告來了解有關被拒絕之內容要求的更多詳細資料，包括涉及的界限群組、電腦及內容是哪一個。 請參閱對等快取主題中的[監視](/sccm/core/plan-design/hierarchy/client-peer-cache#monitoring)。

### <a name="content-library-cleanup-tool"></a>內容庫清理工具
 當內容已不再與應用程式關聯時，您可以使用[內容庫清理工具](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool)將該內容從發佈點中移除。


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>使用 OMS 連接器搭配 Azure Government Cloud
您可以使用 OMS 連接器來連接到 Microsoft Azure Government Cloud 中的 OMS Log Analytics。 這需要您在安裝 OMS 連接器之前先修改組態檔，以便讓連接器能夠與 Government Cloud 搭配運作。 如需詳細資訊，請參閱[使用 OMS 連接器搭配 Azure Government Cloud](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig)。

### <a name="software-update-points-are-added-to-boundary-groups"></a>將軟體更新點新增到界限群組
從 1702 版開始，用戶端會使用界限群組來尋找新的軟體更新點，並在目前的軟體更新點已不再可供存取的情況下，尋找新的軟體更新點來遞補。 您可以將個別的軟體更新點新增到不同的界限群組，以控制用戶端可以尋找的伺服器。 如需詳細資訊，請參閱[設定界限群組](/sccm/core/servers/deploy/configure/boundary-groups)主題中的[軟體更新點](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>相容性設定

### <a name="new-compliance-settings-for-ios"></a>iOS 裝置的新合規性設定

我們已為 iOS 裝置新增許多新設定以符合 Microsoft Intune 所提供的設定。
如需所有可用設定的清單，請參閱[建立使用 Intune 進行管理之 iOS 與 Mac OS X 裝置的設定項目](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)。


## <a name="application-management"></a>應用程式管理

### <a name="improved-support-for-windows-store-for-business-apps"></a>對商務用 Windows 市集應用程式的改進支援

您現在可以從「商務用 Windows 市集」，將線上授權應用程式部署到您使用 Configuration Manager 用戶端來管理的 Windows 10 電腦。
如需詳細資訊，請參閱[從商務用 Windows 市集管理應用程式](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)。

### <a name="check-for-running-executable-files-before-installing-an-application"></a>在安裝應用程式之前檢查執行中可執行檔

在部署類型的 [內容] 對話方塊中，於 [安裝行為] 索引標籤上，您現在可以指定一或多個如果執行就會封鎖部署類型安裝程序的可執行檔。 使用者必須先關閉執行中可執行檔 (或者會針對必要部署而自動予以關閉)，才能安裝部署類型。

如果應用程式已部署為 [可用]，而且使用者嘗試安裝應用程式，則會提示他們在繼續安裝之前關閉任何您指定的執行中可執行檔。

如果應用程式已部署為 [必要]，並且選取 [自動關閉您在部署類型屬性對話方塊之 [安裝行為] 索引標籤上所指定且正在執行的可執行檔] 選項，則他們會看到一個對話方塊，通知他們在到達應用程式安裝期限時會自動關閉您指定的可執行檔。

### <a name="app-management-improvements-for-hybrid-mdm"></a>混合式 MDM 的應用程式管理增強功能

- [將大量採購的 iOS 應用程式部署至裝置集合](#deploy-volume-purchased-ios-apps-to-device-collections)
- [對 iOS Volume Purchase Program for Education (教育單位大量採購方案) 的支援](#support-for-ios-volume-purchase-program-for-education)
- [對多個大量採購方案權杖的支援](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>作業系統部署

### <a name="expire-stand-alone-media"></a>讓獨立媒體到期
當您建立獨立媒體時，有新的選項可供您在媒體上設定選擇性的開始日和到期日。 預設會停用這些設定。 在獨立媒體執行之前，會將這些日期與電腦上的系統時間進行比較。 系統時間早於開始時間或晚於到期時間時，不會啟動獨立媒體。 使用 New-CMStandaloneMedia PowerShell Cmdlet，也可以使用這些選項。 如需詳細資料，請參閱[建立獨立媒體](/sccm/osd/deploy-use/create-stand-alone-media)。

### <a name="package-id-displayed-in-task-sequence-steps"></a>在工作順序步驟中顯示套件識別碼
任何工作順序步驟只要是參考了套件、驅動程式套件、作業系統映像、開機映像或作業系統升級套件，現在都將顯示所參考物件的套件識別碼。 當工作順序步驟參考應用程式時，它將會顯示物件識別碼。

### <a name="support-for-additional-content-in-stand-alone-media"></a>對獨立媒體中其他內容的支援
獨立媒體中現在可支援其他內容。 您可以選取要在媒體上分段的其他套件、驅動程式套件和應用程式，以及工作順序中所參考的其他內容。 先前，只會在獨立媒體上分段工作順序中所參考的內容。 如需詳細資料，請參閱[建立獨立媒體](/sccm/osd/deploy-use/create-stand-alone-media)。

### <a name="hardware-inventory-collects-uefi-information"></a>硬體清查會收集 UEFI 資訊
新的硬體清查類別 (**SMS_Firmware**) 和屬性 (**UEFI**) 都可以協助您判斷是否以 UEFI 模式啟動電腦。 以 UEFI 模式啟動電腦時，**UEFI** 屬性設為 [TRUE]。 在硬體清查中，預設會啟用此項目。 如需硬體清查的詳細資訊，請參閱[如何設定硬體清查](/sccm/core/clients/manage/inventory/configure-hardware-inventory)。

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>改善針對具有強烈影響之工作順序的軟體中心警告訊息
這個版本針對具有強烈影響之部署工作順序的軟體中心警告訊息，包括了下列改善：

- 在工作順序的內容中，您現在可以將任何工作順序 (包括非作業系統工作順序) 設定為高風險部署。 任何符合特定條件的工作順序都會自動定義為具有強烈影響。 如需詳細資料，請參閱[管理高風險部署](/sccm/protect/understand/settings-to-manage-high-risk-deployments)。
- 在工作順序的內容中，您可以選擇使用預設通知訊息，或建立您自己的自訂通知訊息來進行具有強烈影響的部署。
- 在工作順序的內容中，您可以設定軟體中心內容，包括進行必要的重新啟動、工作順序的下載大小，以及估計的執行階段。
- 就地升級之預設具有強烈影響的部署訊息現在指出會自動移轉您的應用程式、資料和設定。 先前，任何作業系統安裝的預設訊息指出將會遺失所有應用程式、資料和設定，但這不適用於就地升級。

如需詳細資料，請參閱[設定具有強烈影響的工作順序設定](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>工作順序失敗時返回上一頁
當您執行工作順序並失敗時，現在可以返回上一頁。 在此版本之前，您必須在失敗時重新啟動工作順序。 例如，您可以在下列情況下使用 [上一步] 按鈕：

- 當電腦在 Windows PE 中啟動時，在工作順序可用之前，可能會顯示工作順序啟動程序對話方塊。 當您在此情況下按一下 [下一步] 時，工作順序的最後一頁會顯示訊息，指出沒有工作順序可用。 現在，您可以按一下 [上一步] 重新搜尋可用的工作順序。 您可以重複此程序直到工作順序可用為止。
- 當您執行工作順序，但發佈點上尚未提供相依內容套件時，工作順序將會失敗。 您現在可以發佈遺失內容 (如果尚未發佈) 或等候發佈點上的內容可供使用，然後按一下 [上一步] 讓工作順序再次搜尋內容。

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>預先快取可用的部署和工作順序內容
從 1702 版開始，針對工作順序的可用部署，您可以選擇使用預先快取內容。 預先快取內容可讓您選擇允許用戶端在一收到部署時，就只下載適用的內容。 因此，當使用者在軟體中心按一下 [安裝] 時，由於內容是在本機硬碟上，因此內容已就緒且安裝會快速開始。 如需詳細資料，請參閱[設定預先快取內容](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)。

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>在就地升級期間從 BIOS 轉換至 UEFI
Windows 10 Creators Update 引進一個簡單的轉換工具，能夠為支援 UEFI 的硬體自動執行硬碟重新分割程序，並將轉換工具整合至 Windows 7 到 Windows 10 的就地升級程序中。 當您將此工具與您的作業系統升級工作順序，以及將韌體從 BIOS 轉換至 UEFI 的 OEM 工具結合時，您可以在就地升級至 Windows 10 Creators Update 的期間，將您的電腦從 BIOS 轉換至 UEFI。 如需詳細資訊，請參閱[管理 BIOS 到 UEFI 轉換的工作順序步驟](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)。

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>對安裝應用程式工作順序步驟的改進
此版本已導入下列各項改進：
- 在 [安裝應用程式] 工作順序步驟中，已將您可安裝的應用程式數目上限增加到 99。 先前的數目上限是 9 個應用程式。
- 當您在工作順序編輯器中，將應用程式新增至 [安裝應用程式] 工作順序步驟時，現在可以從 [選取要安裝的應用程式] 窗格中選取多個應用程式。

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>對自動套用驅動程式工作順序的改進
現在有新的工作順序變數可用，可在提出 HTTP 類別目錄要求時，於 [自動套用驅動程式] 工作順序步驟上設定逾時值。 下列是可用的變數和預設值 (秒)︰
   - SMSTSDriverRequestResolveTimeOut  
     預設值：60
   - SMSTSDriverRequestConnectTimeOut  
     預設值：60
   - SMSTSDriverRequestSendTimeOut  
     預設值：60
   - SMSTSDriverRequestReceiveTimeOut  
     預設值︰480

### <a name="windows-10-adk-tracked-by-build-version"></a>由組建版本追蹤 Windows 10 ADK
現在可由組建版本追蹤 Windows 10 ADK，以確保在自訂 Windows 10 開機映像時提供支援性更佳的體驗。 例如，如果站台使用 Windows ADK for Windows 10 1607 版，則只能在主控台中自訂 10.0.14393 版的開機映像。 如需自訂 WinPE 版本的詳細資料，請參閱[自訂開機映像](/sccm/osd/get-started/customize-boot-images)。

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>預設開機映像來源路徑已不再可變更
預設開機映像會由 Configuration Manager 管理，您已不再能夠於 Configuration Manager 主控台中或使用 Configuration Manager SDK 來變更預設開機映像來源路徑。 您可以繼續設定自訂開機映像的自訂來源路徑。

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>將 Configuration Manager 升級至新版本後，預設開機映像即會重新產生
自這一版起，在您升級 Windows ADK 版本並使用 [更新與服務] 安裝最新版的 Configuration Manager 時，Configuration Manager 會重新產生預設開機映像。 這包括來自更新的 Windows ADK 的新 Window PE 版本、新版 Configuration Manager 用戶端、驅動程式及自訂等等。不會修改自訂開機映像。 如需詳細資料，請參閱[管理開機映像](/sccm/osd/get-started/manage-boot-images#BKMK_BootImageDefault)。

## <a name="software-updates"></a>軟體更新

### <a name="deploy-office-365-apps-to-clients"></a>將 Office 365 應用程式部署至用戶端
從 1702 版開始，您可以從 [Office 365 用戶端管理] 儀表板啟動「Office 365 安裝程式」，此安裝程式可讓您設定 Office 365 安裝設定、從 Office 內容傳遞網路 (CDN) 下載檔案，以及在 Configuration Manager 中將檔案當作應用程式來部署。 如需詳細資料，請參閱[管理 Office 365 ProPlus 更新](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)。

> [!IMPORTANT]
> 您使用 Configuration Manager 中的「Office 365 應用程式精靈」來建立和部署的 Office 365 應用程式並不會自動由 Configuration Manager 管理，除非您再次啟用 [啟用管理 Office 365 用戶端代理程式] 軟體更新用戶端代理程式設定。 如需詳細資料，請參閱[關於用戶端設定](/sccm/core/clients/deploy/about-client-settings)。

### <a name="manage-express-installation-files-for-windows-10-updates"></a>管理適用於 Windows 10 更新的快速安裝檔案
從 1702 版開始，Configuration Manager 支援適用於 Windows 10 更新的快速安裝檔案。 當您使用支援的 Windows 10 版本時，您可以使用 Configuration Manager 設定來只下載目前月份的「Windows 10 累積更新」與上個月更新之間的變更。 如果沒有快速安裝檔案，Configuration Manager 就會每月下載完整的「Windows 10 累積更新」(包括先前月份的所有更新)。 使用快速安裝檔案可在用戶端提供較小的下載項目及更快速的安裝時間。 如需詳細資料，請參閱[管理適用於 Windows 10 更新的快速安裝檔案](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)。


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>行動裝置管理

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>混合式 MDM 的建立精靈無法再將目標設為 Android 與 iOS 版本

從混合式行動裝置管理 (MDM) 的 1702 版開始，您在為受 Intune 管理的裝置建立新原則及設定檔時，不再需要以 Android 和 iOS 的特定版本為目標。 取而代之的是，您需選擇下列其中一種裝置類型：

- Android
- Samsung KNOX 標準 4.0 及更新版本
- iPhone
- iPad

這項變更會影響精靈建立下列項目︰

- 設定項目
- 相容性原則
- 憑證設定檔
- 電子郵件設定檔
- VPN 設定檔
- Wi-Fi 設定檔

透過這項變更，混合式部署可更快為 Android 及 iOS 版本提供支援，而不需要新的 Configuration Manager 版本或延伸模組。 一旦 Intune 獨立版支援新版本，使用者就能將其行動裝置更新為該版本。

為了防止升級舊版 Configuration Manager 時發生問題，這些項目的屬性頁面中還是會有行動作業系統版本。 如果您仍有需要將特定版本設為目標，可以建立新項目，然後在新建項目的屬性頁面上指定設為目標的版本。

### <a name="android-for-work-support"></a>Android for Work 支援
從 1702 版開始，使用 Microsoft Intune 的混合式行動裝置管理現在支援 Android for Work 裝置註冊和管理。 受管理的 Android for Work 裝置指引：

- [註冊 Android for Work 裝置](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)
- [核准和部署 Android for Work 應用程式](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [建立 Android for Work 設定項目](/sccm/mdm/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-for-work-configuration-items)
- [Android for Work 裝置上的選擇性抹除](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)
- [Android for Work 的電子郵件設定檔](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Android for Work 的合規性政策](/sccm/mdm/deploy-use/create-compliance-policy)


### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>將大量採購的 iOS 應用程式部署至裝置集合

您現在不但可將授權的應用程式部署到使用者，還可部署到裝置。 視應用程式是否能夠支援裝置授權而定，當您部署應用程式時，系統會要求適當的授權，如下︰

|||||
|-|-|-|-|
|Configuration Manager 版本|應用程式是否支援裝置授權？|部署集合類型|要求的授權|
|1702 之前|是|使用者|使用者授權|
|1702 之前|否|使用者|使用者授權|
|1702 之前|是|裝置|使用者授權|
|1702 之前|否|裝置|使用者授權|
|1702 和更新版本|是|使用者|使用者授權|
|1702 和更新版本|否|使用者|使用者授權|
|1702 和更新版本|是|裝置|裝置授權|
|1702 和更新版本|否|裝置|使用者授權|

如需有關大量採購之 iOS 應用程式的詳細資訊，請參閱[管理大量採購的 iOS 應用程式](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)。

### <a name="support-for-ios-volume-purchase-program-for-education"></a>對 iOS Volume Purchase Program for Education (教育單位大量採購方案) 的支援

您現在也可以部署和追蹤從 iOS Volume Purchase Program for Education (教育單位大量採購方案) 購買的應用程式。
如需有關大量採購之 iOS 應用程式的詳細資訊，請參閱[管理大量採購的 iOS 應用程式](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)。

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>對多個大量採購方案權杖的支援

您現在可以將多個 Apple 大量採購方案權杖與 Configuration Manager 建立關聯。
如需有關大量採購之 iOS 應用程式的詳細資訊，請參閱[管理大量採購的 iOS 應用程式](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)。

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>對商務用 Windows 市集中企業營運應用程式的支援

您現在可以從「商務用 Windows 市集」同步處理自訂的企業營運應用程式。

### <a name="conditional-access-device-compliance-policy-improvements"></a>條件式存取裝置合規性政策改善

使用者所使用的應用程式為不符合規範的應用程式清單一部分時，新的裝置合規性政策規則是可用來協助您封鎖存取可支援條件式存取的公司資源。 新增符合規範規則 [無法安裝的應用程式] 時，系統管理員可以定義不符合規範的應用程式清單。 將應用程式新增至不符合規範的清單時，此規則需要系統管理員輸入 [應用程式名稱]、[應用程式識別碼] 和 [應用程式發行者]\ (選擇性)。 這項設定僅適用於 iOS 和 Android 裝置。

此外，這可協助組織透過不安全的應用程式來降低資料外洩，並透過特定應用程式來避免過多的資料使用。

- 深入了解[裝置合規性政策運作方式](/sccm/mdm/deploy-use/device-compliance-policies)。
- 深入了解[建立和部署裝置合規性政策](/sccm/mdm/deploy-use/create-compliance-policy)。

### <a name="new-mobile-threat-defense-monitoring-tools"></a>新的 Mobile Threat Defense 監視工具

從 1702 版開始，您可以透過新的方式來監視與您 Mobile Threat Defense 服務提供者的合規性狀態。

- 深入了解[如何監視 Mobile Threat Defense 合規性](https://docs.microsoft.com/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance)。

## <a name="protect-devices"></a>保護裝置

### <a name="detect-outdated-antimalware-client-versions"></a>偵測過期的反惡意程式碼用戶端版本
從 1702 版開始，您可以設定警示來確保 Endpoint Protection 用戶端未過期。 如需詳細資訊，請參閱[到期惡意程式碼用戶端的警示](/sccm/protect/deploy-use/endpoint-configure-alerts#detect-outdated-antimalware-client-versions)。

### <a name="device-health-attestation-updates"></a>裝置健康情況證明更新
現在從管理端點，即可設定及管理內部部署用戶端的裝置健康情況證明服務。 如需詳細資訊，請[健康情況證明](/sccm/core/servers/manage/health-attestation)。

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Windows Hello 企業版的憑證設定檔

如果您打算將憑證設定檔儲存在「Windows Hello 企業版」金鑰容器中，而且憑證設定檔使用「智慧卡登入」EKU，您就必須為金鑰註冊設定權限，以確保能夠正確地驗證憑證。
如需詳細資訊，請參閱 [Windows Hello 企業版設定](/sccm/protect/deploy-use/windows-hello-for-business-settings)。

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>新增針對使用者的 Windows Hello 企業版通知
新的 Windows 10 通知會告知使用者為完成 Windows Hello 企業版安裝程式所需採取的其他動作 (例如設定 PIN 碼)。
