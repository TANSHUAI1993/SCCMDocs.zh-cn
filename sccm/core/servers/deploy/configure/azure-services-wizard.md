---
title: "Azure 服務精靈 | Microsoft Docs"
description: "關於 System Center Configuration Manager 的 Azure 服務精靈。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 22203b358830903cf2e531c0532ae3111b8265fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>設定要與 Configuration Manager 搭配使用的 Azure 服務

適用於：System Center Configuration Manager (最新分支)

從最新分支 1706 版開始，**Azure 服務精靈** 可用來簡化設定搭配 Configuration Manager 使用之 Azure 服務的程序。

此精靈透過 **Azure Web 應用程式** 提供訂用帳戶和設定詳細資料，以提供一般設定經驗。 每次您使用 Azure 設定新的 Configuration Manager 元件或服務時，Web 應用程式會替換輸入這筆相同資訊。

使用設定 Azure 服務精靈時，會設定下列 Azure 服務：
-   **雲端管理**   
    [可讓用戶端使用 Azure Active Directory (Azure AD) 進行驗證]()。 您也可以[設定 Azure AD 使用者探索](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)。
-   **OMS Connector**
    [連線到 Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS)，並將資料 (如集合) 同步處理到 OMS Log Analytics。
-   **升級整備**
    [連線到升級整備](/sccm/core/clients/manage/upgrade/upgrade-analytics)，並檢視用戶端升級相容性資料。
-   **商務用 Windows 市集**連線至[商務用 Windows 市集](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)的線上市集，並取得您組織適用的應用程式以搭配 Configuration Manager 部署。

當您使用精靈設定服務時，有幾個常見的動作。
它們包括：
-   設定 Azure 環境：在精靈的 [應用程式] 頁面中，選取您使用的 [Azure 環境]。 請參閱每個服務的內容，了解服務是否僅支援公用 Azure 雲端，或可支援私人雲端。
-   建立或匯入伺服器應用程式：在精靈的 [應用程式] 頁面中，您可以**建立**和**匯入** Azure Web 應用程式。 可用的選項取決於您所設定的服務。  此外，某些服務可能需要額外的應用程式。 例如，服務可能也需要**原生用戶端應用程式**。


如需 Azure Web 應用程式的詳細資訊，請參閱 [Azure App Service 中的驗證與授權](/azure/app-service/app-service-authentication-overview)，以及 [Web Apps 概觀](/azure/app-service-web/app-service-web-overview)。


## <a name="webapp"></a>建立要與 Configuration Manager 搭配使用的 Azure Web 應用程式

Azure 服務的 Web 應用程式會將您的 Configuration Manager 站台連線至 Azure AD，而且是搭配使用 Azure 服務和您的基礎結構的必要條件。 若要這樣做：

1.  在 Configuration Manager 主控台的 [系統管理] 工作區中，展開 [雲端服務]，然後按一下 [Azure 服務]。
2.  在 [首頁] 索引標籤的 [Azure 服務] 群組中，按一下 [設定 Azure 服務]。
3.  在「Azure 服務精靈」的 [Azure 服務] 頁面上，選取 [雲端管理] 以允許用戶端使用 Azure AD 向階層進行驗證。
4.  在精靈的 [一般] 頁面上，為您的 Azure 服務指定名稱和描述。
5.  在精靈 [應用程式] 頁面上，從清單中選取您的 Azure 環境，然後按一下 [瀏覽] 來選取將用來設定 Azure 服務的 *Web 應用程式*和*原生用戶端應用程式*。     
    **Web 應用程式：**瀏覽會開啟 [伺服器應用程式] 視窗。    
      在 [伺服器應用程式] 視窗中選取您要使用的伺服器應用程式，然後按一下 [確定]。 伺服器應用程式是 Azure Web 應用程式，內含您 Azure 帳戶的設定，包括租用戶識別碼、用戶端識別碼和用戶端的祕密金鑰。
    如果您沒有可用的應用程式，請使用下列其中一項︰
        - **建立**︰若要建立新的伺服器應用程式，請按一下 [建立]。 接著，提供好記的應用程式名稱、首頁 URL、應用程式識別碼 URI 及祕密金鑰有效期間。 根據預設，祕密金鑰有效期間是一年。

         若要繼續，有些人現在必須登入 Azure 才能完成在 Azure 中建立 Web 應用程式的任務。 用來登入 Azure 的帳戶不需和執行 Azure 服務精靈的帳戶相同。 登入 Azure 後，Configuration Manager 會為您在 Azure 中建立 Web 應用程式，包括和 Web 應用程式搭配使用的用戶端識別碼及祕密金鑰。 您稍後可從 Azure 入口網站加以檢視。

         當您建立使用 [建立] 設定 Web 應用程式時，Configuration Manager 可以在 Azure AD 中為您建立 Web 應用程式。
        - **匯入**︰若要使用您 Azure 訂用帳戶中已存在的 Web 應用程式，請按一下 [匯入]。 提供應用程式與租用戶的易記名稱，然後針對您要讓 Configuration Manager 使用的 Azure Web 應用程式，為其指定租用戶識別碼、用戶端識別碼及祕密金鑰。 在您「驗證」資訊之後，請按一下 [確定] 來繼續進行操作。

          此選項不適用於您可能會設定的所有服務。

   **原生用戶端應用程式：**瀏覽會開啟 [用戶端應用程式] 視窗。  
     在 [用戶端應用程式] 視窗中，選取您要使用的用戶端應用程式，然後按一下 [確定]。

     如果您沒有可用的用戶端應用程式，請使用下列其中一項︰
     - **建立**︰若要建立新的用戶端應用程式，請按一下 [建立]。 提供好記的應用程式名稱和回覆 URL。

          若要繼續，有些人現在必須登入 Azure 才能完成在 Azure 中建立用戶端應用程式的任務。 用來登入 Azure 的帳戶不需和執行 Azure 服務精靈的帳戶相同。 登入 Azure 後，Configuration Manager 會為您在 Azure 中建立原生用戶端應用程式，包括和 Web 應用程式搭配使用的用戶端識別碼。 您稍後可從 Azure 入口網站加以檢視。
          當您使用 [建立] 設定應用程式時，Configuration Manager 可以在 Azure AD 中為您建立原生用戶端應用程式。
     - **匯入**︰若要使用您 Azure 訂用帳戶中已存在的用戶端應用程式，請按一下 [匯入]。 提供好記的應用程式名稱和用戶端識別碼。 接著按一下 [確定] 繼續。
           此選項不適用於您可能會設定的所有服務。

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  在精靈的 [探索] 頁面，按一下 [啟用 Azure Active Directory 使用者探索]，然後按一下 [設定]。
在 [Azure AD 使用者探索設定] 對話方塊中，設定進行探索的排程。 您也可以啟用差異探索，這將只檢查 Azure AD 中新的或已變更的帳戶。 深入了解 [Azure AD 使用者探索](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)。
 
 7. 完成精靈。

此時，您已將 Configuration Manager 站台連線到 Azure AD。

## <a name="view-the-configuration-of-an-azure-service"></a>檢視 Azure 服務的設定
您可以檢視設定要使用之 Azure 服務的屬性。

在主控台中，移至 [管理] > [概觀] > [雲端服務] > [Azure 服務]。 接著，選擇您想要檢視或編輯的服務，然後按一下 [屬性]。
