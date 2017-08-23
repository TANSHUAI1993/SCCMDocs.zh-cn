---
title: "Technical Preview 1703 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1703 版中可用的功能。"
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bb1b96a56db68dcea22270855b899ba3a90afd0d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1703-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1703 中的功能

*適用於︰System Center Configuration Manager (Technical Preview)*

本文介紹 System Center Configuration Manager Technical Preview 1703 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    


**以下是您可以使用此版本試用的新功能。**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>將大量採購的 iOS 應用程式部署至裝置集合

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

## <a name="direct-links-to-applications-in-software-center"></a>應用程式的軟體中心直接連結

現在您可以提供使用者應用程式的軟體中心直接連結。 這表示使用者不再需要開啟軟體中心及搜尋應用程式，仍可加以安裝。 這僅適用於 Configuration Manager 應用程式，並不包括套件和程式或工作順序。

### <a name="try-it-out"></a>試試看                 

使用下列 URL 格式開啟軟體中心並連至特定應用程式︰

**Softwarecenter:SoftwareId =*應用程式識別碼***

### <a name="how-to-get-the-application-identifier-of-an-application"></a>如何取得應用程式的應用程式識別碼。

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。
2.  在 [軟體程式庫] 工作區中，展開 [應用程式管理]，然後按一下 [應用程式]。
3.  在 [應用程式] 檢視中，以滑鼠右鍵按一下其中一個資料行標頭，然後從清單中選取 [CI 唯一識別碼]。 您會看到清單現在顯示每個應用程式的唯一識別碼。
4.  請注意您想要提供連結之應用程式的 **CI 唯一識別碼**，例如︰**ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5.  然後，移除接在應用程式 GUID 後方的所有文字，在此案例為 **/2**。 剩下的便是您的應用程式識別碼。
6.  最後，在前面加上  **=**，以完成建構連結。 使用上述範例，最終連結顯示如下︰**Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**。

終端使用者可使用此連結，開啟軟體中心並直接連至您指定的應用程式。


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Configuration Manager Windows 用戶端電腦的 PFX 憑證

您現在可以部署您匯入執行 Windows 10 之 Configuration Manager 用戶端電腦的 PFX 憑證設定檔。

### <a name="try-it-out"></a>試試看

使用[如何建立 PFX 憑證設定檔](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)中的指示來匯入 PFX 檔、部署設定檔，然後檢查是否已安裝目標使用者的憑證。



## <a name="configure-azure-services-wizard"></a>設定 Azure 服務精靈
Technical Preview 1703 引入**設定 Azure 服務**精靈。 此精靈取代個別的工作流程並提供通用的設定經驗，以設定您搭配 Configuration Manager 所使用的雲端服務。 這項作業透過使用 **Azure Web 應用程式**完成，進而提供訂用帳戶和設定詳細資料，讓您無須每次向 Azure 設定新的 Configuration Manager 元件或服務時都需輸入。

對於 Technical Preview 1703 版，只有商務用 Windows 市集 (WSfB) 會使用此精靈進行設定。  其他雲端服務使用其個別工作流程進行設定。

-   使用本預覽主題中的資訊，取代最新分支主題[使用 System Center Configuration Manager 管理從商務用 Windows 市集購買的應用程式](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)的章節[設定商務用 Windows 市集同步處理](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#set-up-windows-store-for-business-synchronization)中的設定步驟資訊。

-   如需 Web 應用程式的詳細資訊，請參閱 [Azure App Service 中的驗證與授權](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)，以及 [Web Apps 概觀](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)。

### <a name="prerequisites-and-planning"></a>必要條件與規劃
設定 Configuration Manager 和商務用 Windows 市集之間的連線時，您必須提供一個資料夾來存放從市集同步處理的應用程式內容。 若要保障此資料夾的安全且其內容可順利部署到裝置，請確定下列權限都已就緒：
-   使用 **Computer$** 帳戶時，安裝服務連接點站台系統角色 (階層中的頂層站台) 的電腦，必須具有指定資料夾的讀取和寫入權限。  

-   應用程式作者必須具有指定資料夾的讀取權限。  

-   裝載 SMS 提供者執行個體的每部電腦，其 **Computer$** 帳戶必須能夠使用您指定的資料夾。

在 Azure Active Directory 中，將 Configuration Manager 註冊為 Web 應用程式或 Web API 管理工具。 這會建立您稍後所需的用戶端識別碼。

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>使用精靈來設定 WSfB 雲端服務

1. 在主控台中，移至 [管理] > [概觀] > [雲端服務管理] > [Azure] > [Azure 服務]，然後選擇 [設定 Azure 服務] 啟動 [Azure 服務精靈]。

2. 在 [Azure 服務] 頁面上，選取您想要設定的服務，然後按一下 [下一步]。 在此預覽中只可設定 WSfB。

3. 在 [一般] 頁面上，提供 **Azure 服務名稱**的易記名稱和選擇性的描述，然後按一下 [下一步]。

4. 在 [應用程式] 頁面上，指定您的 Azure 環境，然後按一下 [瀏覽] 開啟 [伺服器應用程式] 視窗。

5. 在 [伺服器應用程式] 視窗中選取您要使用的伺服器應用程式，然後按一下 [確定]。
伺服器應用程式是 Azure Web 應用程式，內含您 Azure 帳戶的設定，包括租用戶識別碼、用戶端識別碼和用戶端的祕密金鑰。 如果您沒有可用的伺服器應用程式，請使用下列其中一項︰
  - **建立**︰若要建立新的伺服器應用程式，請按一下 [建立]。 提供應用程式和租用戶的易記名稱。 接著，您登入 Azure 後，Configuration Manager 會為您在 Azure 中建立 Web 應用程式，包括和 Web 應用程式搭配使用的用戶端識別碼及祕密金鑰。 您稍後可從 Azure 入口網站加以檢視。
  - **匯入**︰若要使用您 Azure 訂用帳戶中已存在的 Web 應用程式，請按一下 [匯入]。 提供應用程式與租用戶的易記名稱，然後針對您要讓 Configuration Manager 使用的 Azure Web 應用程式，為其指定租用戶識別碼、用戶端識別碼及祕密金鑰。 **驗證**資訊後，請按一下 [確定] 繼續。  </br></br>

6. 檢閱 [資訊] 頁面，並依指示完成任何額外的步驟和設定。 搭配使用此服務與 Configuration Manager 需要這些設定。
例如，若要設定 WSfB：

  1. 您必須在 Azure 中將 Configuration Manager 註冊為 Web 應用程式或 Web API，並記錄用戶端識別碼。 您同時指定用戶端金鑰，供管理工具 (也就是 Configuration Manager) 使用。

  2.    在 WSfB 主控台中，您必須將 Configuration Manager 設定為存放區管理工具、啟用支援離線授權的應用程式，並接著購買至少一個應用程式。   </br>

  準備好繼續進行時，請按一下 [下一步] 。

7. 在 [應用程式設定] 頁面上，完成這項服務的應用程式目錄和語言設定，然後按一下 [下一步]。
8. 在精靈完成後，Configuration Manager 主控台會顯示您已將 [商務用 Windows 市集] 設定為 [雲端服務類型]。

您現在可以使用[最新分支內容](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)的其餘部分，進而從 WSfB 管理應用程式，以同步處理、建立和部署，以及監視商務用 Windows 市集應用程式。

### <a name="modify-a-cloud-service-configuration"></a>修改雲端服務設定
您可以檢視和編輯雲端服務的內容來修改設定。

在主控台中，移至 [管理] > [概觀] > [雲端服務管理] > [Azure] > [Azure 服務]，然後選擇 [設定 Azure 服務]，再選取雲端服務並接著選擇 [內容]。

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>在就地升級期間從 BIOS 轉換至 UEFI
Windows 10 Creators Update 引進一個簡單的轉換工具，能夠為支援 UEFI 的硬體自動執行硬碟重新分割程序，並將轉換工具整合至 Windows 7 到 Windows 10 的就地升級程序中。 當您將此工具與您的作業系統升級工作順序，以及將韌體從 BIOS 轉換至 UEFI 的 OEM 工具結合時，您可以在就地升級至 Windows 10 Creators Update 的期間，將您的電腦從 BIOS 轉換至 UEFI。 如需詳細資訊，請參閱[管理 BIOS 到 UEFI 轉換的工作順序步驟](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)。

## <a name="collapsible-task-sequence-groups"></a>可摺疊的工作順序群組
此版本引入展開和摺疊工作順序群組的功能。 您可以個別或一次展開或摺疊所有群組。


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>設定 Windows Analytics 進行升級整備用的用戶端設定
自這一版起，您可以使用裝置用戶端設定來簡化使用 [Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) 解決方案 (像是搭配 Configuration Manager 的[升級整備](/sccm/core/clients/manage/upgrade/upgrade-analytics)) 所需的 Windows 遙測設定。 Configuration Manager 可以從 Windows Analytics 擷取資料，根據用戶端電腦所報告的 Windows 遙測資料，提供目前環境狀態的深入解析。 Windows 遙測資料是由用戶端電腦向 Windows 遙測服務報告，相關資料後續會傳輸至 Windows Analytics 解決方案 (裝載於組織 OMS 工作區之一)。 「升級整備」是一種 Windows Analytics 解決方案，可針對受管理的裝置，協助您排定 Windows 升級的優先順序。

如需 Windows 遙測設定資訊，請參閱[在您的組織中設定 Windows 遙測](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization)。

### <a name="prerequisites"></a>先決條件
- 您必須將站台設定為使用「升級整備」雲端服務。 如需詳細資訊，請參閱[升級整備](/sccm/core/clients/manage/upgrade/upgrade-analytics)

### <a name="configure-windows-analytics-client-settings"></a>設定 Windows Analytics 用戶端設定
若要設定 Windows Analytics，請在 Configuration Manager 主控台中移至 [管理] > [用戶端設定]，按兩下 [建立自訂裝置用戶端設定]，然後選取 [Windows Analytics]。  

接著，移至 [Windows Analytics] 設定索引標籤，以進行下列設定：
- **商業識別碼**  
商業識別碼索引鍵會將您所管理裝置的資訊，對應至裝載組織 Windows Analytics 資料的 OMS 工作區。 如果您已設定商業識別碼索引鍵以供「升級整備」之用，請使用該識別碼。 如果您還沒有商業識別碼索引鍵，請參閱[產生商業識別碼索引鍵 (英文)]( https://technet.microsoft.com /itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key)。

- 設定 **Windows 10 裝置的遙測層級**   
如需每個 Windows 10 遙測層級所收集項目的資訊，請參閱[設定組織的 Windows 遙測 (英文)]( https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels)。

- 選擇**加入 Windows 7、8 和 8.1 裝置的商業資料收集**   
如需在您選擇加入後這些作業系統所收集資料的資訊，請參閱及下載 Microsoft 的 PDF 檔案 [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Windows 7、Windows 8 和 Windows 8.1 評鑑員遙測事件和欄位)。

- **設定 Internet Explorer 資料收集** 在執行 Windows 8.1 或更舊版本的裝置上，Internet Explorer 資料收集可讓「升級整備」偵測 Web 應用程式的不相容性，以便能夠順利地升級至 Windows 10。 您可以依照網際網路區域，決定是否啟用 Internet Explorer 資料收集。 如需網際網路區域的詳細資訊，請參閱[關於 URL 安全性區域 (英文)](https://msdn.microsoft.com/en-us/library/ms537183(v=vs.85).aspx)。