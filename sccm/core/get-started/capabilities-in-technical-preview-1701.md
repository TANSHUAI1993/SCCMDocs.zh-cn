---
title: "Technical Preview 1701 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1701 版中可用的功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b330c97a0853d1673f1cf7e0691891b72407fa51
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1701-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1701 中的功能

適用於︰System Center Configuration Manager (Technical Preview)



本文介紹 System Center Configuration Manager Technical Preview 1701 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    


**以下是您可以使用此版本試用的新功能。**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>軟體更新點的界限群組增強功能
從此 Preview 開始，您現在可以使用界限群組來建立用戶端與軟體更新點的關聯。 這是擴充界限群組變更來管理其他站台系統角色之持續性工作的一部分。  界限群組變更一開始是在 Technical Preview 1609 和 1610 版最新分支中引進。  

使用此 Preview，您可以使用新界限群組行為來管理用戶端可使用的軟體更新點，與如何管理用戶端可使用的發佈點類似︰  

- 您可以設定界限群組，來關聯可裝載軟體更新點的一或多部伺服器。
- 搜尋新軟體更新點的用戶端將嘗試使用與其目前界限群組建立關聯的軟體更新點。
- 如果用戶端無法連線到其目前軟體更新點，而且從其目前界限群組找不到軟體更新點，用戶端使用後援行為來擴充它可使用的可用軟體更新點集區。    

如需界限群組的詳細資訊，請參閱最新分支內容中的[界限群組](/sccm/core/servers/deploy/configure/boundary-groups)。

不過，使用此 Preview，只會局部實作軟體更新點的界限群組。 您可以新增軟體更新點並設定包含軟體更新點的鄰近界限群組，但尚未支援軟體更新點的後援時間，而且用戶端將等待兩個小時再啟動後援。

以下說明這個 Technical Preview 的軟體更新點行為︰  

-   **新的用戶端會使用界限群組來選取軟體更新點，**在安裝 1701 版之後安裝的用戶端，會從與用戶端界限群組建立關聯的軟體更新點中選取軟體更新點。

  這會取代先前行為，即用戶端從共用用戶端樹系的軟體更新點清單中隨機選取軟體更新點。   

-   **先前安裝的用戶端會繼續使用其目前軟體更新點，直到它們後援以找到新的軟體更新點。**
先前安裝的用戶端以及已有軟體更新點的用戶端將繼續使用該軟體更新點，直到它們後援。 這包括未與用戶端目前界限群組建立關聯的軟體更新點。 它們不會立即從其目前界限群組嘗試尋找並使用軟體更新點。

  只有在用戶端無法連線其目前軟體更新點之後，已有軟體更新點的用戶端才會開始使用這個新的界限群組行為，並啟動後援。
這項延遲在切換至新行為時是刻意設計的。 原因是用戶端與新的軟體更新點同步處理資料時，軟體更新點的變更可能會導致使用大量網路頻寬。 轉換延遲有助於避免讓網路飽和，讓所有用戶端同時切換至新的軟體會更新點。

-   **後援時間的設定：**此 Technical Preview 不支援用戶端在啟動後援來搜尋新軟體更新點時的設定。 這包括 [Fallback times (in minutes)]\(後援時間 (分鐘)) 和 [Never fallback]\(永不後援) 的設定，而您可以針對不同的界限群組關聯性設定這些項目。

  相反地，用戶端會保留其目前行為，即用戶端會先嘗試連線至其目前軟體更新點兩個小時，再啟動後援，來尋找它可使用的新軟體更新點。

  用戶端確實使用後援時，將會使用進行後援的界限群組設定，來建立可用軟體更新點集區。 此集區包括用戶端「目前界限群組」、「鄰近界限群組」和用戶端「站台預設界限群組」中的所有軟體更新點。

- **設定預設站台界限群組：**  
 請考慮將軟體更新點新增至 *Default-Site-Boundary-Group&lt;台碼>*。 這確保不是另一個界限群組成員的用戶端可以後援來尋找軟體更新點。


若要管理界限群組的軟體更新點，請使用[現行分支文件中的程序](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#procedures-for-boundary-groups)，但是，請記住您可能設定的後援時間尚未用於軟體更新點。


## <a name="hardware-inventory-collects-uefi-information"></a>硬體清查會收集 UEFI 資訊
新的硬體清查類別 (**SMS_Firmware**) 和屬性 (**UEFI**) 都可以協助您判斷是否以 UEFI 模式啟動電腦。 以 UEFI 模式啟動電腦時，**UEFI** 屬性設為 [TRUE]。 在硬體清查中，預設會啟用此項目。 如需硬體清查的詳細資訊，請參閱[如何設定硬體清查](/sccm/core/clients/manage/inventory/configure-hardware-inventory)。

## <a name="improvements-to-operating-system-deployment"></a>作業系統部署增強功能
我們已對作業系統部署進行下列改善，其中許多都是使用者意見反應的結果。
- [**Support for more applications for the Install Applications task sequence step**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t) (安裝應用程式工作順序步驟的多個應用程式支援)：我們已在 [安裝應用程式] 工作順序步驟中，將您可安裝的應用程式數目上限增加到 99。 先前的數目上限是 9 個應用程式。
- [**Select multiple apps in the Install App task sequence step**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step) (在安裝應用程式工作順序步驟中選取多個應用程式)：在工作順序編輯器中，將應用程式新增至 [安裝應用程式] 工作順序步驟時，現在可以從 [選取要安裝的應用程式] 窗格中選取多個應用程式。
- [**Expire standalone media**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media) (獨立媒體到期)：建立獨立媒體時，有新的選項可在媒體上設定選擇性開始和到期日。 預設會停用這些設定。 在獨立媒體執行之前，會將這些日期與電腦上的系統時間進行比較。 系統時間早於開始時間或晚於到期時間時，不會啟動獨立媒體。 使用 New-CMStandaloneMedia PowerShell Cmdlet，也可以使用這些選項。
- [**Support for additional content in stand-alone media**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic) (獨立媒體中其他內容的支援)：獨立媒體現在支援其他內容。 您可以選取要在媒體上分段的其他套件、驅動程式套件和應用程式，以及工作順序中所參考的其他內容。 先前，只會在獨立媒體上分段工作順序中所參考的內容。
- [**Configurable timeout for Auto Apply Driver task sequence step**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout) (自動套用驅動程式工作順序步驟的可設定逾時)：現在提供新的工作順序變數，可在提出 HTTP 類別目錄要求時於 [自動套用驅動程式] 工作順序步驟上設定逾時值。 下列是可用的變數和預設值 (秒)︰
   - SMSTSDriverRequestResolveTimeOut 預設：60
   - SMSTSDriverRequestConnectTimeOut 預設：60
   - SMSTSDriverRequestSendTimeOut 預設：60
   - SMSTSDriverRequestReceiveTimeOut 預設：480
- [**套件識別碼現在會顯示在工作順序步驟中**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste)：任何參考套件、驅動程式套件、作業系統映像、開機映像或作業系統升級套件的工作順序步驟現在會顯示所參考物件的套件識別碼。 工作順序步驟參考應用程式時，將會顯示物件識別碼。
- **組建版本所追蹤的 Windows 10 ADK**：組建版本現在會追蹤 Windows 10 ADK，確保自訂 Windows 10 開機映像時可提供更多的支援體驗。 例如，如果站台使用 Windows ADK for Windows 10 1607 版，則只能在主控台中自訂 10.0.14393 版的開機映像。 如需自訂 WinPE 版本的詳細資料，請參閱[自訂開機映像](/sccm/osd/get-started/customize-boot-images)。
- **無法再變更預設開機映像來源路徑**：預設開機映像是透過 Configuration Manager 所管理，而且無法再於 Configuration Manager 主控台中或使用 Configuration Manager SDK 來變更預設開機映像來源路徑。 您可以繼續設定自訂開機映像的自訂來源路徑。

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>在雲端式發佈點上裝載軟體更新
從此 Preview 版本開始，您可以使用雲端式發佈點來裝載軟體更新套件。 不過，因為您可以設定用戶端直接從 Microsoft Update 下載軟體更新，所以請考慮將軟體更新套件部署至雲端式發佈點可能造成的額外成本。

如需使用雲端式發佈點的資訊，請參閱 Configuration Manager 最新分支內容中的[使用雲端式發佈點](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)。

## <a name="validate-device-health-attestation-data-via-management-points"></a>透過管理點來驗證裝置健全狀況證明資料

從此 Preview 版本開始，您可以設定管理點來驗證雲端或內部部署健全狀況證明服務的健全狀況證明報告資料。 [管理點元件內容] 對話方塊中的新 [進階選項] 索引標籤可讓您 [新增]、[編輯] 或 [移除] [On-premises device health attestation service URL]\(內部部署裝置健全狀況證明服務 URL)。 您也可以將用戶端代理程式的 [自訂裝置設定] 指定為 [Use on-premises Health Attestation Service]\(使用內部部署健全狀況證明服務)。  此設定設為 [是] 時，將會啟用報告到內部部署管理點，而非雲端式服務。

### <a name="try-it-out"></a>試試看

- **在管理點上啟用內部部署裝置健全狀況證明**<br>  在 Configuration Manager 主控台中，瀏覽至管理點，並開啟 [管理點元件內容]，然後按一下 [進階選項] 索引標籤。 按一下 [新增]，然後指定內部部署 URL (例如，https://10.10.10.10) 作為 [On-premises device health attestation service URL]\(內部部署裝置健全狀況證明服務 URL)。
- **啟用用戶端代理程式的內部部署管理點健全狀況證明報告**<br>在 Configuration Manager 主控台中，選擇 [系統管理] > [用戶端設定]，然後按兩下或建立新的 [自訂裝置設定]。 選取 [電腦代理程式]，並將 [Use on-premises Health Attestation Service]\(使用內部部署健全狀況證明服務) 設為 [是]。 如果將 [Enable communication with Device Health Attestation Service]\(啟用與裝置健全狀況證明服務之間的通訊)  設為 [是]，並將 [Use on-premises Health Attestation]\(使用內部部署健全狀況證明) 設為 [否]，則管理點將會使用雲端式裝置健全狀況證明服務。

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>針對 Microsoft Azure Government 雲端使用 OMS 連接器
使用此 Technical Preview，您現在可以使用 Microsoft Operations Management Suite (OMS) 連接器連線至 Microsoft Azure Government 雲端上的 OMS 工作區。  

若要這樣做，您可以修改設定檔以指向 Government 雲端，然後安裝 OMS 連接器。

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>設定 Microsoft Azure Government 雲端的 OMS 連接器
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

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>混合式 MDM 的建立精靈無法再將目標設為 Android 與 iOS 版本

從混合式行動裝置管理 (MDM) 的這個技術預覽版開始，您在為受 Intune 管理的裝置建立新原則及設定檔時，不再需要以 Android 或 iOS 的特定版本為目標。 取而代之的是選擇下列其中一種裝置類型：

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
