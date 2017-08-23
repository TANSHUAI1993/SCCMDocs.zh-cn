---
title: "Configuration Manager 2012 的變更 | Microsoft Docs "
description: "識別 System Center Configuration Manager 與 System Center 2012 Configuration Manager 中的變更與新功能。"
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: "51"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0a3eb93a99533a1569d8f72ca01d6dfcdc75da20
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>System Center Configuration Manager 和 System Center 2012 Configuration Manager 之間的變更

*適用於：System Center Configuration Manager (最新分支)*


 System Center Configuration Manager 的最新分支推出 System Center 2012 Configuration Manager 的重要變更。 本主題識別 System Center Configuration Manager 基準版本 1511 內的重大變更和新功能。 若要了解 System Center Configuration Manager 後續更新中推出的變更，請參閱 [System Center Configuration Manager 累加版本的新功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)。



 2015 年 12 月發行的 System Center Configuration Manager (版本 1511) 是 Microsoft 目前 Configuration Manager 產品的初始版本。 通常稱之為 System Center Configuration Manager 最新分支。 「最新分支」指出這是支援產品累加式更新的版本。 它也提供一個方法來區別此版本與舊版 Configuration Manager。  

 System Center Configuration Manager：  

-   不同於 Configuration Manager 2007 或 System Center 2012 Configuration Manager 等舊版，產品名稱中不使用年份或產品識別碼。

-   支援累加式產品中更新 (也稱為更新版本)。 初始版本為版本 1511。 後續版本透過主控台內更新的方式於一年中發行數次 (例如版本 1610)。
-   使用基準版本進行安裝。 雖然 1511 是原始的基準版本，但新的基準版本會不定時發行，例如 1702。 基準版本可用來安裝新的 System Center Configuration Manager 站台和階層，或從支援的 Configuration Manager 2012 版本進行升級。




##  <a name="bkmk_updates"></a> Configuration Manager 的主控台中更新  
 System Center Configuration Manager 使用稱為**更新和服務**的主控台內服務方式，可輕鬆尋找並安裝建議的更新。  

 某些版本只以現有站台的更新形式提供 (從 Configuration Manager 主控台內)，無法用來安裝新的 Configuration Manager 站台。   
例如，1610 更新只能從 Configuration Manager 主控台內取得。 它是用來更新已執行某版本的 System Center Configuration Manager 的站台。

另外，也會定期發行更新版本做為新的基準版本，例如更新 1702。 這種更新可以用來安裝新的階層而不需要從較舊的基準版本 (例如 1511) 開始，也無須升級至最新版本。


如需使用更新的詳細資訊，請參閱 [Updates for System Center Configuration Manager](../../../core/servers/manage/updates.md) (System Center Configuration Manager 的更新)。  
如需基準的詳細資訊，請參閱[基準和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)。

##  <a name="bkmk_servicepoint"></a> 新的站台系統角色：服務連接點  
 **Microsoft Intune 連接器**已為啟用額外功能 (**服務連接點**) 的新站台系統角色所取代。 服務連接點：  

-   整合 Intune 與 System Center Configuration Manager 內部部署行動裝置管理時，取代 Microsoft Intune 連接器。  

-   作為您管理之裝置的連絡點。  

-   將您部署的相關使用方式資料上傳到 Microsoft 雲端服務。  

-   讓套用至部署的更新可從 Configuration Manager 主控台內取用。  

此站台系統角色支援線上和離線操作模式。 如需詳細資訊，請參閱 [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md)。  

##  <a name="bkmk_usage"></a> 使用量資料收集  
 System Center Configuration Manager 會收集您站台和基礎結構的使用方式資料。 這項資訊是透過服務連接點編譯並提交給 Microsoft 雲端服務。 需要有這項資訊才能讓 Configuration Manager 下載套用至您所使用 Configuration Manager 版本之部署的更新。 當您設定服務連接點時，可以指定資料收集層級，以及這是自動進行提交 (線上模式) 還是手動進行提交 (離線模式)。  

 如需詳細資訊，請參閱[使用方式資料層級和設定](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage)。  

##  <a name="bkmk_AMT"></a> Intel 主動管理技術 (AMT) 支援  
 使用 System Center Configuration Manager，即已從 Configuration Manager 主控台內移除 AMT 型電腦的原生支援。 當您使用 [Microsoft System Center Configuration Manager 的 Intel SCS 附加元件](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)時，仍會完全管理 AMT 電腦。 附加元件可讓您存取管理 AMT 的最新功能，同時移除 Configuration Manager 併入那些變更之前所引入的限制。  

移除的 System Center Configuration Manager 整合 AMT 包括頻外管理。 頻外管理點站台系統角色已不再使用，也無法再使用。  

請注意，這項變更不會影響 System Center 2012 Configuration Manager 中的頻外管理。

##  <a name="bkmk_out"></a> 已過時功能  
 某些功能 (例如 [Intel 主動管理技術 (AMT) 型電腦的原生支援](#bkmk_AMT)已從 Configuration Manager 主控台移除。 其他功能 (例如網路存取保護) 則已完整移除。 此外，不再支援一些較舊的 Microsoft 產品 (如 Windows Vista、Windows Server 2008 和 SQL Server 2008)。  

 如需已取代之功能的清單，請參閱 [System Center Configuration Manager 的已移除和已淘汰功能](../../../core/plan-design/changes/removed-and-deprecated-features.md)。  

 如需所支援產品、作業系統和設定的詳細資訊，請參閱 [Supported configurations for System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md) (System Center Configuration Manager 的支援設定)。  

## <a name="client-deployment"></a>用戶端部署  
 System Center Configuration Manager 引入新的功能，可用於先測試 Configuration Manager 用戶端的新版本，再使用新的軟體升級站台的其餘部分。 您可以設定用來試驗新用戶端的進入生產階段前集合。 在您滿意進入生產階段前的新用戶端軟體之後，即可升級用戶端，以使用新的版本來自動升級站台的其餘部分。  

 如需如何測試用戶端的詳細資訊，請參閱[如何測試 System Center Configuration Manager 的進入生產階段前集合用戶端升級](../../../core/clients/manage/upgrade/test-client-upgrades.md)。  

## <a name="operating-system-deployment"></a>作業系統部署  

請注意下列作業系統部署變更：

-   在 [建立工作順序精靈] 的 [從升級套件升級作業系統] 中，有新的工作順序類型可供使用。 它會建立將電腦從 Windows 7、Windows 8 或 Windows 8.1 升級至 Windows 10 的步驟。 如需詳細資訊，請參閱 [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)。  

-   部署作業系統時，現在可以使用 Windows PE 對等快取。 執行工作順序來部署作業系統的電腦可使用 Windows PE 對等快取，從本機對等裝置 (對等快取來源) 取得內容，而不是從發佈點下載內容。 這有助於在分公司沒有本機發佈點的案例中，降低廣域網路 (WAN) 流量。 如需詳細資訊，請參閱 [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic)。  

-   您現在可以檢視 Windows 的狀態 (如同環境中的服務一般)。 您也可以建立服務方案，以確立部署更新步調，並確保在新組建發行時，Windows 10 最新分支電腦保持為最新狀態。 此外，您可以檢視當 Windows 10 用戶端即將結束最新分支 (CB) 或最新商務分支 (CBB) 的建置支援時所發出的警示。 如需詳細資訊，請參閱 [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md)。  

## <a name="application-management"></a>應用程式管理  

請注意下列應用程式管理變更：

-   System Center Configuration Manager 可讓您部署執行 Windows 10 和更新版本之裝置的通用 Windows 平台 (UWP) 應用程式。 請參閱[使用 System Center Configuration Manager 建立 Windows 應用程式](../../../apps/get-started/creating-windows-applications.md)。  

-   軟體中心有全新的時尚外貌。 應用程式先前只出現在應用程式類別目錄 (使用者可用的應用程式)，而現在會出現於軟體中心的 [應用程式] 索引標籤下。 這讓使用者更容易找到這些部署，而不需要參考應用程式類別目錄。 此外，也不再需要已啟用 Silverlight 的瀏覽器。 請參閱[在 System Center Configuration Manager 中規劃和設定應用程式管理](../../../apps/plan-design/plan-for-and-configure-application-management.md)。  

-   透過 MDM 應用程式的新 Windows Installer 類型可讓您建立以 Windows Installer 為基礎的應用程式，並部署到執行 Windows 10 的已註冊電腦上。 請參閱[使用 System Center Configuration Manager 建立 Windows 應用程式](../../../apps/get-started/creating-windows-applications.md)。  

-   當您建立內部 iOS 應用程式的應用程式時，只需要指定應用程式的安裝程式 (.ipa) 檔案。 您不再需要指定對應的屬性清單 (.plist) 檔案。 請參閱[使用 System Center Configuration Manager 建立 iOS 應用程式](../../../apps/get-started/creating-ios-applications.md)。  

-   在 Configuration Manager 2012 中，若要指定 Windows 市集中應用程式的連結，您可以直接指定連結，或瀏覽至已安裝應用程式的遠端電腦。 在 System Center Configuration Manager 中，您仍然可以直接輸入連結，但現在，您可以直接從 Configuration Manager 主控台瀏覽市集中的應用程式，而不是瀏覽至參照電腦。  

## <a name="software-updates"></a>軟體更新  

請注意下列軟體更新變更：

-   System Center Configuration Manager 現在可以偵測出電腦軟體更新管理方法之間的差異。 明確來說，它可以分辨連線至 Windows Update for Business (WUfB) 以進行軟體更新管理的 Windows 10 電腦，以及連線至 Windows Server Update Services (WSUS) 以進行軟體更新管理的電腦。 **UseWUServer** 是新屬性，並指定是否使用 WUfB 管理電腦。 您可以在集合中使用此設定，以移除這些電腦不進行軟體更新管理。 如需詳細資訊，請參閱 [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)。  

-   您現在可從 Configuration Manager 主控台排程及執行 WSUS 清理工作。 在 [軟體更新點元件] 內容中，當您選取執行 WSUS 清理工作時，它會在下一次軟體更新同步處理時執行。 到期的軟體更新在 WSUS 伺服器上會設為拒絕狀態，而電腦上的 Windows Update 代理程式將不再掃描這些軟體更新。 如需詳細資訊，請參閱 [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md)。  

## <a name="compliance-settings"></a>相容性設定  

請注意下列合規性設定變更：

-   System Center Configuration Manager 改進了建立設定項目的工作流程。 現在，當您建立設定項目並選取支援的平台時，只能使用與該平台相關的設定。 請參閱[在 System Center Configuration Manager 中開始使用相容性設定](../../../compliance/get-started/get-started-with-compliance-settings.md)。  

-   [建立設定項目精靈] 現在可讓您更輕鬆地選擇您想要建立的設定項目類型。 此外，新增和更新的設定項目適用於：  

    -   使用 Configuration Manager 用戶端管理的 Windows 10 裝置。  

    -   使用 Configuration Manager 用戶端管理的 Mac OS X 裝置。  

    -   使用 Configuration Manager 用戶端管理的 Windows 桌上型電腦和伺服器電腦。  

    -   不使用 Configuration Manager 用戶端管理的 Windows 8.1 和 Windows 10 裝置。  

    -   不使用 Configuration Manager 用戶端管理的 Windows Phone 裝置。  

    -   不使用 Configuration Manager 用戶端管理的 iOS 和 Mac OS X 裝置。  

    -   不使用 Configuration Manager 用戶端管理的 Android 和 Samsung KNOX Standard 裝置。  

 請參閱[如何建立 System Center Configuration Manager 的組態項目](../../../compliance/deploy-use/create-configuration-items.md)。  

-   支援管理向 Microsoft Intune 註冊或使用 Configuration Manager 用戶端管理的 Mac OS X 電腦設定。 請參閱[如何為不是使用 System Center Configuration Manager 用戶端所管理的 iOS 和 Mac OS X 裝置建立組態項目](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)。  

## <a name="protect-data-and-site-infrastructure"></a>保護資料和站台的基礎結構  
System Center Configuration Manager 可讓您與 Windows Hello 企業版 (原 Microsoft Passport for Windows) 整合。 Windows Hello 企業版是使用 Active Directory 或 Azure Active Directory 帳戶取代執行 Windows 10 之裝置上的密碼、智慧卡或虛擬智慧卡的替代登入方法。 請參閱　[Windows Hello for Business settings in System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md) (System Center Configuration Manager 的 Windows Hello 企業版設定)。

## <a name="mobile-device-management-with-microsoft-intune"></a>使用 Microsoft Intune 的行動裝置管理  
 System Center Configuration Manager 引入行動裝置管理體驗的增強功能，包括：  

-   限制使用者可以註冊的裝置數目。  

-   指定公司入口網站使用者在註冊或使用應用程式之前必須接受的條款和條件。  

-   新增可協助管理大量裝置的裝置註冊管理員角色。  

如需 Configuration Manager 及 Intune 的行動裝置管理功能的詳細資訊，請參閱 [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md) (搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM))。  

## <a name="on-premises-mobile-device-management"></a>內部部署行動裝置管理  
 您現在可以使用內部部署 Configuration Manager 基礎結構管理行動裝置。 所有裝置管理和管理資料都是在內部部署進行處理，且不屬於 Microsoft Intune 或其他雲端服務。 這種類型的裝置管理不需要用戶端軟體。 Configuration Manager 會使用裝置作業系統的內建功能來管理裝置。  

 若要進一步了解，請參閱[在 System Center Configuration Manager 中使用內部部署基礎結構管理行動裝置](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。
