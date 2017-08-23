---
title: "規劃站台系統角色 | Microsoft Docs"
description: "規劃 System Center Configuration Manager 階層時，考量站台系統伺服器和站台系統角色。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
caps.latest.revision: "11"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0a3704a2d3b75ed7e0a7f718b681448ab6fc078d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 規劃站台系統伺服器和站台系統角色

*適用於︰System Center Configuration Manager (最新分支)*

您安裝的每個 System Center Configuration Manager 站台都包含站台伺服器，即**站台系統伺服器**。 站台亦可包含從站台伺服器遠端到電腦上的其他站台系統伺服器。 站台系統伺服器 (站台伺服器或遠端站台系統伺服器) 支援 **站台系統角色**。


##  <a name="bkmk_siteservers"></a> 站台系統伺服器  
 當您在電腦上安裝站台系統角色時，該電腦會變成站台系統伺服器。 您可以在每個站台安裝一或多個額外的站台系統伺服器。 您也可以選擇不要安裝額外的站台系統伺服器，而是在站台伺服器電腦上直接執行所有的站台系統角色。 每部站台系統伺服器都會支援一或多個站台系統角色。 藉由共用伺服器上站台系統角色的 CPU 處理負載，額外的伺服器能協助擴充站台的功能和容量。  

 在考慮加入站台系統伺服器時，請確認伺服器符合預期用途的先決條件。 將站台伺服器加入頻寬足夠與預期端點通訊的網路位置也是個不錯的主意，端點包括站台伺服器、網域資源、雲端位置、站台系統伺服器和用戶端。  

 如果您要設定具有 Proxy 的站台系統伺服器以供站台系統角色使用，請參閱[可使用 Proxy 伺服器的站台系統角色](#bkmk_proxy)。  

##  <a name="bkmk_planroles"></a> Site system roles  
 站台系統角色會安裝在電腦上，以提供站台額外的功能。 範例包括：  

-   額外的管理點，讓站台可以支援更多裝置，直至站台支援的容量。  

-   額外的發佈點，以展開內容基礎結構，改善裝置與使用者的內容發佈效能。  

-   一或多個站台系統角色專屬功能。 例如，軟體更新點可用來管理受管理裝置的軟體更新，Reporting Services 點可讓您執行報表來監視及了解或分享部署資訊。  


不同的 Configuration Manager 站台可以支援不同的站台系統角色集合。 支援的站台系統角色組合取決於站台類型 (管理中心網站、主要站台或次要站台)。 階層的拓撲可限制特定站台類型上放置某些角色。 例如，只有階層的最上層站台才支援服務連接點，該站台可能是管理中心網站或獨立主要站台。 子主要站台或次要站台不支援此角色。  

安裝站台之後，您可以將部分站台系統角色的位置從站台伺服器上的預設位置移動到到另一部伺服器。 例如，預設會安裝在主要或次要站台伺服器上的管理點或發佈點即符合前文敘述。 您也可以安裝某些其他的站台系統角色以擴充站台功能 (提供更多服務給用戶端) 並滿足業務需求。 有些角色是必要的，有些則是選擇性的。  

-   **Configuration Manager 站台伺服器。** 這個角色會識別執行 Configuration Manager 安裝程式的伺服器以安裝站台，或是您安裝次要站台的伺服器。 等解除安裝站台後，才能移動或解除安裝此角色。  

-   **Configuration Manager 站台系統。** 這個角色會指派給您安裝站台或安裝站台系統角色的任何電腦。 等電腦移除最後一個站台系統角色後，才能移動或解除安裝這個角色。  

-   **Configuration Manager 元件站台系統角色。** 這個角色會識別執行 SMS Executive 服務執行個體的站台系統，而且是用於支援其他角色 (例如管理點) 時的必要角色。 等電腦移除最後一個適用站台系統角色後，才能移動或解除安裝這個角色。  

-   **Configuration Manager 站台資料庫伺服器。** 這個角色會指派給包含站台之站台資料庫執行個體的站台系統伺服器。 此角色只能透過修改站台，使其使用不同的 SQL Server 執行個體來裝載站台資料庫，才能移動至新的伺服器。  

-   **SMS 提供者。** SMS 提供者角色會指派給每一部裝載 SMS 提供者執行個體的電腦，是 Configuration Manager 主控台與站台資料庫之間的介面。 根據預設，該角色會自動安裝在管理中心網站和主要站台的站台伺服器上。 您可以在每個站台上安裝額外的執行個體，以提供存取權限給額外的系統管理使用者。  

     若要安裝額外的提供者，請在站台伺服器上執行 Configuration Manager 安裝程式以[管理 SMS 提供者](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)。 接著，您可以在其他電腦上安裝額外的提供者。 您只能在一部電腦上安裝一個 SMS 提供者執行個體，且該電腦必須與站台伺服器位於相同的網域。  

-   **應用程式類別目錄 Web 服務點。** 一種網站系統角色，其提供軟體程式庫的軟體資訊給應用程式類別目錄網站。 雖然只在主要站台支援這個角色，但您可以在一個站台或是相同階層中的多個站台，安裝此角色的多個執行個體。  

-   **應用程式類別目錄網站點。** 一種網站系統角色，其提供使用者一份應用程式類別目錄的可用軟體清單。 雖然只在主要站台支援這個角色，但您可以在一個站台或是相同階層中的多個站台，安裝此角色的多個執行個體。  

     應用程式類別目錄支援網際網路上的用戶端電腦時，作為安全性最佳作法，請將應用程式類別目錄網站點安裝在周邊網路中以確保安全，而將應用程式類別目錄 Web 服務點安裝在內部網路上。  

-   **Asset Intelligence 同步處理點。** 連接 Microsoft 以下載 Asset Intelligence 類別目錄資訊的站台系統角色。 這個角色也會上傳未分類的標題，以便未來加入類別目錄中。 階層只支援此角色的單一執行個體，且必須位於階層的最上層站台 (管理中心網站或獨立主要站台)。 如果您擴充獨立主要站台到較大的階層時，必須從主要站台解除安裝此角色，然後在管理中心網站安裝此角色。   如需詳細資訊，請參閱 [Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md) (System Center Configuration Manager 中的 Asset Intelligence)。  

-   **憑證登錄點。** 與執行網路裝置註冊服務之伺服器通訊的站台系統角色。 此角色會管理使用簡單憑證註冊通訊協定 (SCEP) 的裝置憑證要求。 只有主要站台和管理中心網站支援這個角色。

     即使單一憑證登錄點即可提供功能給整個階層，不過您也可以在站台以及相同階層中的多個站台安裝此角色的多個執行個體。 這將有助於保持負載平衡。 當多個執行個體存在於階層中時，用戶端會隨機指派到其中一個憑證登錄點。  

     每個憑證登錄點都需存取個別的網路裝置註冊服務執行個體。 您不能將兩個 (含) 以上的憑證登錄點設定為使用同一個網路裝置註冊服務。 此外，憑證登錄點不能安裝在執行網路裝置註冊服務的同一部伺服器上。  

- **雲端管理閘道連接器端點。** 與[雲端管理閘道](/sccm/core/clients/manage/setup-cloud-management-gateway)通訊的站台系統角色。

-   **發佈點。** 一種網站系統角色，其包含可供用戶端下載的來源檔案，例如應用程式內容、軟體套件、軟體更新、作業系統映像和開機映像。 依預設，這個角色在站台安裝時會安裝到新的主要及次要站台的站台伺服器電腦上。 管理中心網站不支援該角色。 您可以在支援的站台和相同階層中的多個站台，安裝此角色的多個執行個體。 如需詳細資訊，請參閱 [Fundamental concepts for content management in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) (System Center Configuration Manager 的內容管理基本概念) 和[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

-   **後援狀態點。** 一種網站系統角色，其可協助您監視安裝，並且識別因無法與其管理點通訊而未受管理的用戶端。 雖然只在主要站台支援這個角色，但您可以在一個站台和在相同階層中的多個站台，安裝此角色的多個執行個體。     


-   **Endpoint Protection 點。** 一種網站系統角色，Configuration Manager 用於接受 Endpoint Protection 授權條款，以及設定雲端保護服務的預設成員資格。 階層只支援此角色的單一執行個體，且必須位於階層的最上層站台 (管理中心網站或獨立主要站台)。 如果您擴充獨立主要站台到較大的階層時，必須從主要站台解除安裝此角色，然後在管理中心網站安裝此角色。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

-   **註冊點。** 一種站台系統角色，它會使用 Configuration Manager PKI 憑證註冊行動裝置及 Mac 電腦。 雖然只在主要站台支援這個角色，但您可以在一個站台或是相同階層中的多個站台，安裝此角色的多個執行個體。  

     如果使用者使用 Configuration Manager 註冊行動裝置，且其 Active Directory 帳戶位於站台伺服器樹系不信任的樹系中，則您必須在使用者樹系中安裝註冊點。 這樣才能驗證使用者。  

-   **註冊 Proxy 點。** 一種網站系統角色，可管理來自行動裝置和 Mac 電腦的 Configuration Manager 註冊要求。 雖然只在主要站台支援這個角色，但您可以在一個站台或是相同階層中的多個站台，安裝此角色的多個執行個體。  

     支援網際網路上的行動裝置時，請將註冊 Proxy 點安裝在周邊網路中以確保安全，而將註冊點安裝在內部網路上。  

-   **Exchange Server 連接器。** 如需該角色的相關資訊，請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

-   **管理點。** 一種網站系統角色，其提供原則和服務位置資訊給用戶端，並接收來自用戶端的設定資料。  

    依預設，這個角色在站台安裝時會安裝到新的主要及次要站台的站台伺服器電腦上。 主要站台支援此角色的多個執行個體。 次要站台支援單一管理點，以提供用戶端本機連絡點來取得電腦及使用者原則 (位於次要站台的管理點稱為 Proxy 管理點)。  

     管理點可設定為支援 HTTP 或 HTTPS，以及支援您使用 System Center Configuration Manager 內部部署行動裝置管理所管理的行動裝置。 您可以使用 [System Center Configuration Manager 管理點的資料庫複本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)，依管理點來協助降低站台資料庫伺服器上的 CPU 負載，因為服務要求來自用戶端。  

-   **Reporting Services 點。** 此網站系統角色可與 SQL Server Reporting Services 整合，以建立及管理 Configuration Manager 的報告。 主要站台和管理中心網站支援這個角色，且您可以在支援的站台上安裝此角色的多個執行個體。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的報表規劃](../../../core/servers/manage/planning-for-reporting.md)。  

-   **服務連接點。** 一種站台系統角色，您可用來透過 Microsoft Intune 及內部部署 MDM 來管理行動裝置。 這個角色也會從您的站台上傳使用資料，並且需要此角色才能讓 Configuration Manager 更新可在 Configuration Manager 主控台中使用。 階層只支援此角色的單一執行個體，且必須位於階層的最上層站台 (管理中心網站或獨立主要站台)。 如果您擴充獨立主要站台到較大的階層時，必須從主要站台解除安裝此角色，然後在管理中心網站安裝此角色。 如需詳細資訊，請參閱 [關於 System Center Configuration Manager 中的服務連線點](../../../core/servers/deploy/configure/about-the-service-connection-point.md)。  

-   **軟體更新點。** 此網站系統角色可與 Windows Server Update Services (WSUS) 整合，以提供軟體更新給 Configuration Manager 用戶端。 所有站台都支援此角色︰  

    -   在管理中心網站中安裝此站台系統，以同步處理 WSUS。  

    -   在子主要站台設定此角色的每個執行個體，以便與管理中心網站同步。  

    -   跨網路傳輸資料速度變慢時，請考量將軟體更新點安裝在次要站台上。  

    如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md)。  

-   **狀態移轉點。** 一種網站系統角色，其會在電腦移轉至新的作業系統時儲存使用者狀態資料。 主要站台和次要站台均支援此角色。 您可以在站台和相同階層中的多個站台，安裝此角色的多個執行個體。 如需在部署作業系統時儲存使用者狀態的詳細資訊，請參閱[在 System Center Configuration Manager 中管理使用者狀態](../../../osd/get-started/manage-user-state.md)。  

-   **系統健全狀況驗證程式點。** 雖然此站台系統角色仍會出現在 Configuration Manager 主控台中，不過已不再使用。  

###  <a name="bkmk_proxy"></a> 可使用 Proxy 伺服器的站台系統角色  
 某些 Configuration Manager 站台系統角色需要連線到網際網路，且當裝載角色的站台系統伺服器已設定使用 Proxy 伺服器時就會使用 Proxy 伺服器。 通常，會在電腦 (即安裝站台系統角色之電腦) 的**系統**內容中建立此連線。 該連線無法使用一般使用者帳戶的 Proxy 設定。 當需要使用 Proxy 伺服器完成與網際網路的連線時，您必須設定電腦才能使用 Proxy 伺服器：  

-   安裝站台系統角色時，您可以設定 Proxy 伺服器。  

-   當您使用 Configuration Manager 主控台時，您可以新增或修改 Proxy 伺服器設定。  

-   可使用 Proxy 伺服器設定之站台系統伺服器上的所有站台系統角色，都會使用相同的 Proxy 伺服器設定。 如果您需要不同的網站系統角色來使用不同的 Proxy 伺服器，就必須將網站系統角色安裝在不同的網站系統伺服器電腦上。  

-   如果您修改 Proxy 伺服器設定，或在已經具有 Proxy 伺服器設定的電腦上安裝新的站台系統角色，新的設定會覆寫原始設定。  


如需設定站台系統角色 Proxy 伺服器的程序，請參閱[為 System Center Configuration Manager 新增站台系統角色](../../../core/servers/deploy/configure/add-site-system-roles.md)主題。  

下列是可使用 Proxy 伺服器的站台系統角色：  

-   **Asset Intelligence 同步處理點。** 此網站系統角色會連線到 Microsoft，並且會在裝載 Asset Intelligence 同步處理點的電腦上使用 Proxy 伺服器設定。  

-   **雲端發佈點。** 當您使用雲端發佈點時，管理雲端發佈點的主要網站必須能夠連線到 Microsoft Azure，才能佈建、監視及發佈內容到發佈點。 如果此連線需要 Proxy 伺服器，您必須在主要網站伺服器上設定 Proxy 伺服器。 您無法在 Azure 的雲端式發佈點上設定 Proxy 伺服器。 如需詳細資訊，請參閱[在 Microsoft Azure 中，安裝 System Center Configuration Manager 的雲端架構發佈點](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)主題中的[為管理雲端服務的主要站台設定 Proxy 設定值](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud)一節。  

-   **Exchange Server 連接器。** 此網站系統角色會連線到 Exchange Server，並且會在裝載 Exchange Server 連接器的電腦上使用 Proxy 伺服器設定。  

-   **軟體更新點。** 此網站系統角色可以要求連線至 Microsoft Update 以下載修補程式，並同步處理有關更新的資訊。 一般來說，在您設定 Proxy 伺服器時，支援使用 Proxy 伺服器之電腦上的每個網站系統角色都會使用 Proxy 伺服器。 無需進行其他設定。 其中一個例外狀況是軟體更新點。 根據預設，軟體更新點並不使用可用的 Proxy 伺服器，除非您在設定軟體更新點時也啟用下列選項：  

    -   **同步處理軟體更新時使用 Proxy 伺服器**  

    -   **使用自動部署規則在下載內容時使用 Proxy 伺服器**  

    > [!TIP]  
    >  您必須先在裝載軟體更新點的網站系統伺服器上設定 Proxy 伺服器，才能選取其中一個選項。 Proxy 伺服器僅用於您選取的特定選項。  

 如需軟體更新點之 Proxy 伺服器的詳細資訊，請參閱[安裝軟體更新點](../../../sum/get-started/install-a-software-update-point.md)主題中的「Proxy 伺服器設定」一節。  

-   **服務連接點。** 當設定為在線上 (而非離線) 時，此站台系統角色會連線至 Microsoft Intune 和 Microsoft 雲端服務。  
