---
title: "管理來自商務用 Windows 市集的應用程式 | Microsoft Docs"
description: "使用 System Center Configuration Manager，從商務用 Windows 市集管理和部署應用程式。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 369b6a82a20a90ca534f9484c0be71096dd35a30
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理從商務用 Windows 市集購買的應用程式
[商務用 Windows 市集](https://www.microsoft.com/business-store)是您可以在其中為您的組織尋找並個別或大量購買 Windows 應用程式的地方。 藉由將市集連線到 Configuration Manager，您便可以同步使用 Configuration Manager 購買的應用程式清單。 您接著便可以在 Configuration Manager 主控台中檢視這些應用程式，並如同部署任何其他應用程式般加以部署。


## <a name="online-and-offline-apps"></a>線上和離線應用程式

商務用 Windows 市集支援兩種應用程式類型：

- **線上** - 此授權類型需要使用者和裝置連線到市集，以取得應用程式及其授權。 Windows 10 裝置必須已加入 Azure Active Directory 網域。
- **離線** - 讓您快取應用程式及授權，以直接在內部部署網路內部署，而不須連線到市集，也不必有網際網路連線。

[深入了解](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview?f=255&MSPPError=-2147217396)商務用 Windows 市集。

Configuration Manager 支援在執行 Configuration Manager 用戶端的 Windows 10 裝置上，以及在向 Microsoft Intune 註冊的 Windows 10 裝置上 (又稱為混合設定)，管理商務用 Windows 市集應用程式。 Configuration Manager 提供線上和離線應用程式的下列功能。

> [!IMPORTANT]
> 若要使用這項功能，Windows 10 裝置必須執行 2015 年 11 月 (1511) 版或更新版本。


|功能|離線應用程式|線上應用程式|
|------------|------------|------------|
|將應用程式資料同步處理至 Configuration Manager<br>(每隔 24 小時同步處理一次)|[是]|是|
|從市集應用程式建立 Configuration Manager 應用程式|是|[是]|
|支援市集中的免費應用程式|[是]|是|
|支援市集中的付費應用程式|否|是|
|支援使用者或裝置集合的必要部署|是|是|
|支援使用者或裝置集合的可用部署|是|是|
|支援市集中的企業營運應用程式|是|是|

若要使用 Configuration Manager 用戶端將 線上授權的應用程式部署至 Windows 10 電腦，它們必須執行 Windows 10 Creators Update 或更新版本。

## <a name="deploying-online-apps-using-the-windows-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>使用商務用 Windows 市集在執行 Configuration Manager 用戶端的電腦部署線上應用程式
將商務用 Windows 市集應用程式部署到執行完整 Configuration Manager 用戶端的電腦前，請考慮下列各點：

- 如需完整的功能，電腦必須執行 Windows 10 Creators Update 或更新版本。
- 電腦必須已加入 Azure Active Directory 工作場所，並在您將商務用 Windows 市集應用程式註冊為管理工具所在的相同 AAD 租用戶中。
- 當電腦使用內建的 Administrator 帳戶登入時，就無法存取商務用 Windows 市集應用程式。
- 電腦必須使用即時網際網路連線到商務用 Windows 市集。

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>執行舊版 Windows 10 電腦的注意事項
電腦若執行 Creators Update (含 Configuration Manager 用戶端) 之前的 Windows 10 版本，適用下列功能︰


- 因使用者安裝應用程式、應用程式達到其安裝期限，或後續安裝重新評估所需部署，而強制安裝時：
    - 啟動商務用 Windows 市集應用程式將會「強制」執行該應用程式。 
    - 應用程式安裝前，終端使用者必須再從市集完成安裝
    - Configuration Manager 主控台中的應用程式狀態將報告為失敗，而錯誤為「Windows 市集應用程式已在用戶端電腦上開啟，正在等候使用者完成安裝。」
- 在下一個應用程式評估週期︰
    - 如果終端使用者從市集安裝應用程式，應用程式會報告狀態**成功**。 
    - 如果使用者未嘗試從市集安裝應用程式︰
        - 所需部署將嘗試啟動市集，並再次強制安裝應用程式。
        - 可用的部署不會重新強制執行。

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>執行舊版 Windows 10 電腦的進一步注意事項：

- 您無法從商務用 Windows 市集部署企業營運應用程式
- 當您從市集部署付費應用程式時，終端使用者必須登入市集並自行購買應用程式。
- 如果您已部署禁止存取 Windows 市集取用者版本的群組原則，即使已啟用商務用 Windows 市集，仍無法從商務用 Windows 市集部署。


## <a name="set-up-windows-store-for-business-synchronization"></a>設定商務用 Windows 市集同步處理

### <a name="for-configuration-manager-versions-prior-to-1706"></a>針對 1706 之前的 Configuration Manager 版本

**在 Azure Active Directory 中，將 Configuration Manager 登錄為 [Web 應用程式和/或 Web API] 管理工具。這個動作會提供您用戶端識別碼，以供稍後使用。**
1. 在 [https://manage.windowsazure.com](https://manage.windowsazure.com) 的 [Active Directory] 節點中，選取您的 Azure Active Directory，然後按一下 [應用程式] > [新增]。
2.  按一下 [加入我的組織正在開發的應用程式]。
3.  輸入應用程式的名稱，選取 [Web 應用程式] 和/或 [Web API]，然後按一下 [下一步] 箭號。
4.  為 [登入 URL] 和 [應用程式識別碼 URI] 輸入相同的 URL。 URL 可以是任何內容，不需要解析為實際的位址。 例如，您可以輸入 *https://yourdomain/sccm*。
5.  完成精靈。

**在 Azure Active Directory 中，為登錄的管理工具建立用戶端金鑰**
1.  反白您所建立的應用程式，然後按一下 [設定]。
2.  從 [金鑰] 底下的清單中選取持續時間，然後按一下 [儲存]。 此動作會建立新的用戶端金鑰。 在您成功將商務用 Windows 市集連線到 Configuration Manager 之前，請勿離開此頁面。

**在商務用 Windows 市集中，將 Configuration Manager 設定為市集管理工具**
1.  開啟 [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools)，並在出現提示時登入。
2.  視需要接受使用條款。
3.  在 [管理工具] 底下，按一下 [Add a management tool]\(新增管理工具)。
4.  在 [Search for the tool by name]\(依名稱搜尋工具) 中，輸入您先前在 AAD 中所建立應用程式的名稱，然後按一下 [新增]。
5.  按一下您匯入之應用程式旁邊的 [啟用]。
6.  如果您想要允許購買離線授權的應用程式，請在 [管理] > [帳戶資訊]頁面中，選取 [Show Offline-Licensed Apps]\(顯示離線授權的應用程式)。

**將市集帳戶新增至 Configuration Manager**

1. 請確認您已從商務用 Windows 市集至少購買一個應用程式。 在 Configuration Manager 主控台的 [系統管理] 工作區中，展開 [雲端服務]，然後按一下 [商務用 Windows 市集]。
2.  在 [常用] 索引標籤的 [商務用 Windows 市集] 群組中，按一下 [新增商務用 Windows 市集帳戶]。 
3.  從 Azure Active Directory 中，加入您的租用戶識別碼、用戶端識別碼及用戶端金鑰，然後完成精靈。
4. 完成之後，您就可在 Configuration Manager 主控台的 [商務用 Windows 市集] 清單中看到您設定的帳戶。

### <a name="for-configuration-manager-version-1706-and-later"></a>針對 Configuration Manager 版本 1706 和更新版本

1. 在主控台中，移至 [管理] > [概觀] > [雲端服務管理] > [Azure] > [Azure 服務]，然後選擇 [設定 Azure 服務] 啟動 [Azure 服務精靈]。
2. 在 [Azure 服務] 頁面上，選取您想要設定的服務，然後按一下 [下一步]。
3. 在 [一般] 頁面上，提供 Azure 服務名稱的易記名稱和選擇性的描述，然後按一下 [下一步]。
4. 在 [應用程式] 頁面上，指定您的 Azure 環境，然後按一下 [瀏覽] 以開啟 [伺服器應用程式] 視窗。
5. 在 [伺服器應用程式] 視窗中選取您要使用的伺服器應用程式，然後按一下 [確定]。 伺服器應用程式是 Azure Web 應用程式，內含您 Azure 帳戶的設定，包括租用戶識別碼、用戶端識別碼和用戶端的祕密金鑰。 如果您沒有可用的伺服器應用程式，請使用下列其中一項︰
    - **建立︰**若要建立新的伺服器應用程式，請按一下 [建立]。 提供應用程式和租用戶的易記名稱。 接著，您登入 Azure 後，Configuration Manager 會為您在 Azure 中建立 Web 應用程式，包括和 Web 應用程式搭配使用的用戶端識別碼及祕密金鑰。 您稍後可從 Azure 入口網站加以檢視。
    - **匯入︰**若要使用您 Azure 訂用帳戶中已存在的 Web 應用程式，請按一下 [匯入]。 提供應用程式與租用戶的易記名稱，然後針對您要讓 Configuration Manager 使用的 Azure Web 應用程式，為其指定租用戶識別碼、用戶端識別碼及祕密金鑰。 **驗證**資訊後，請按一下 [確定] 繼續。 
6. 檢閱 [資訊] 頁面，並依指示完成任何額外的步驟和設定。 搭配使用此服務與 Configuration Manager 需要這些設定。 例如，若要設定商務用 Windows 市集：
    - 您必須在 Azure 中將 Configuration Manager 註冊為 Web 應用程式或 Web API，並記錄用戶端識別碼。 您同時指定用戶端金鑰，供管理工具 (也就是 Configuration Manager) 使用。
    - 在商務用 Windows 市集主控台中，您必須將 Configuration Manager 設定為存放區管理工具、啟用對於離線授權應用程式的支援，然後至少購買一個應用程式。 
7. 準備好繼續進行時，請按一下 [下一步] 。
8. 在 [應用程式設定] 頁面上，完成這項服務的應用程式目錄和語言設定，然後按一下 [下一步]。
9. 在精靈完成後，Configuration Manager 主控台會顯示您已將 [商務用 Windows 市集] 設定為 [雲端服務類型]。




## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>從商務用 Windows 市集應用程式建立和部署 Configuration Manager 應用程式。
1.  在 Configuration Manager 主控台的 [軟體程式庫] 工作區中，展開 [應用程式管理]，然後按一下 [市集應用程式的授權資訊]。
2.  選擇要部署的應用程式，然後在 [常用] 索引標籤的 [建立] 群組中，按一下 [建立應用程式]。
建立 Configuration Manager 應用程式以包含商務用 Windows 市集應用程式。 然後可以如處理任何其他 Configuration Manager 應用程式一樣，部署及監視此應用程式。

> [!IMPORTANT]
> 若裝置已向 Intune 註冊，只有原先註冊裝置的使用者才能使用已部署的應用程式。 其他任何使用者都無法存取此應用程式。

## <a name="next-steps"></a>後續步驟

在 [軟體程式庫] 工作區中，展開 [應用程式管理]，然後按一下 [市集應用程式的授權資訊]。

針對您管理的每個市集應用程式，您可以檢視應用程式的相關資訊，包括其名稱、平台、您擁有之應用程式的授權數目，以及您可以使用的授權數目。
