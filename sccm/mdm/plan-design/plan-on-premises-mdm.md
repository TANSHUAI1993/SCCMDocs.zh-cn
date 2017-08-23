---
title: "規劃內部部署 MDM | Microsoft Docs"
description: "在 System Center Configuration Manager 中規劃內部部署行動裝置管理來管理行動裝置。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 544c3bea0c7df96887ee1717f061c39c64b82d01
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的內部部署行動裝置管理規劃

*適用對象：System Center Configuration Manager (最新分支)*

在準備 Configuration Manager 基礎結構來處理內部部署行動裝置管理之前，請先考量下列需求。

##  <a name="bkmk_devices"></a> 支援的裝置  
 內部部署行動裝置管理可讓您使用裝置作業系統內建的管理功能來管理行動裝置。  管理功能是以 Open Mobile Alliance (OMA) 裝置管理 (DM) 標準為基礎，且許多裝置平台都使用這項標準管理裝置。  我們稱之為**現代化裝置** (在文件和 Configuration Manager 主控台使用者介面中)，以和需要使用 Configuration Manager 用戶端加以管理的其他裝置加以區別。  

 > [!NOTE]  
>  Configuration Manager 最新分支，支援執行下列作業系統的裝置在內部部署行動裝置管理中註冊︰  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 團隊版 \(從 Configuration Manager 1602 版開始\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 企業版   

##  <a name="bkmk_intune"></a> 使用 Microsoft Intune 訂閱  
 若要開始使用內部部署行動裝置管理，您需要 Microsoft Intune 訂閱。 訂閱只有在追蹤裝置授權時才需要，不會用來管理或儲存裝置的管理資訊。 所有的管理都是貴組織企業使用內部部署的 Configuration Manager 基礎結構來處理。  

 > [!NOTE]  
 > 從 1610 版開始，Configuration Manager 支援同時使用 Microsoft Intune 和內部部署 Configuration Manager 基礎結構來管理行動裝置。   

 如果站台有使用網際網路連線的裝置，即可使用 Intune 服務通知裝置來檢查原則更新的裝置管理點。 Intune 嚴格限用於對網際網路對向裝置的通知。 不使用網際網路連線且無法透過 Intune 連絡的裝置，依賴設定輪詢間隔以站台系統角色簽入取得管理功能。  

> [!TIP]  
>  建議您先設定 Intune，再安裝必要的站台系統角色，讓站台系統角色使用最短的時間開始運作。  

 如需如何設定 Intune 訂閱的資訊，請參閱 [為 System Center Configuration Manager 中的內部部署行動裝置管理設定 Microsoft Intune 訂閱](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)。  

##  <a name="bkmk_roles"></a> 必要的站台系統角色  
 內部部署行動裝置管理需要下列的站台系統角色，每種至少一個：  

-   **註冊 Proxy 點** ，以支援註冊要求。  

-   **註冊點** ，以支援裝置註冊。  

-   **裝置管理點** ，用於傳遞原則。 這個站台系統角色是管理點角色的變化，後者已設定為允許管理行動裝置。  

-   **發佈點** ，用於傳遞內容。  

-   **服務連接點**，用於連接到 Intune 以通知防火牆外的裝置。  

 這些站台系統角色可以安裝在單一站台系統伺服器，或分別在不同的伺服器上執行，視貴組織需求而定。 每個用於內部部署行動裝置管理的站台系統伺服器都必須設定為 HTTPS 端點來與受信任的裝置通訊。 如需詳細資訊，請參閱 [必要的信任通訊](#bkmk_trustedComs)。  

 如需規劃站台系統角色的詳細資訊，請參閱 [規劃 System Center Configuration Manager 的站台系統伺服器和站台系統角色](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)。  

 如需如何加入必要站台系統角色的詳細資訊，請參閱 [在 System Center Configuration Manager 中為內部部署行動裝置管理安裝站台系統角色](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)。  

##  <a name="bkmk_trustedComs"></a> 必要的信任通訊  
 內部部署行動裝置管理需有站台系統角色才能取得 HTTPS 通訊。 您可以根據本身的需求，使用貴企業的憑證授權單位 (CA) 建立伺服器和裝置間的受信任連接，或者使用公眾可取得的 CA 作為受信任的授權單位。  不管哪種方式，您都需要使用 IIS 設定的 Web 伺服器憑證，此憑證位在裝載了必要站台系統角色的站台系統伺服器上；而且您還需要此 CA 的根憑證，此 CA 是安裝在必須連接這些伺服器的裝置上。  

 如果使用貴企業的 CA 建立信任的通訊，您必須執行下列工作：  

-   在 CA 上建立及發行 Web 伺服器憑證範本。  

-   要求每個裝載了必要站台系統角色站台的站台系統伺服器 Web 伺服器憑證。  

-   設定站台系統伺服器上的 IIS，以使用要求的 Web 伺服器憑證。  

 至於已加入公司 Active Directory 網域的裝置，裝置上已有用於信任連接的企業 CA 根憑證。 這表示使用站台系統伺服器的 HTTPS 連線會自動信任已加入網域的裝置 (例如桌上型電腦)。 不過，未加入網域的裝置 (通常是行動裝置) 不會安裝必要的根憑證。 這些裝置需要手動安裝根憑證，才能成功與支援內部部署行動裝置管理的站台系統伺服器通訊。  

 您必須匯出發行 CA 的根憑證供個別裝置使用。 若要取得根憑證檔案，您可以使用 CA 匯出；更簡單的方法是使用 CA 發行的 Web 伺服器憑證擷取根目錄，再建立根憑證檔案。   然後，根憑證必須傳遞到裝置。  範例傳遞方法包括  

-   檔案系統  

-   電子郵件附件  

-   記憶卡  

-   行動網卡  

-   雲端存放裝置 (例如 OneDrive)  

-   近距離無線通訊 (NFC) 連線  

-   條碼掃描器  

-   全新體驗 (OOBE) 佈建套件  

 如需詳細資訊，請參閱 [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

##  <a name="bkmk_enrollment"></a> 註冊考量  
 若要啟用內部部署行動裝置管理裝置註冊，使用者必須授與註冊權限，他們的裝置也必須和裝載必要站台系統角色的站台系統伺服器有信任的通訊。  

 在 Configuration Manager 用戶端設定中設定註冊設定檔，即可完成授與使用者註冊權限。 您可以使用預設的用戶端設定，將註冊設定檔推送至所有探索到的使用者，或在自訂用戶端設定中設定註冊設定檔，將此設定推送到一個或多個使用者集合。  

 授與使用者註冊權限之後，使用者就可以註冊自己的裝置。 若要註冊，使用者的裝置必須有發行 Web 伺服器憑證之憑證授權單位 (CA) 的根憑證，此 Web 伺服器憑證使用在裝載了必要站台系統角色的站台系統伺服器上。  

 除了使用者起始註冊之後，您也可以設定大量註冊套件，讓裝置註冊不需要使用者介入。 將這個套件傳遞至裝置的時機，可以在開始佈建使用裝置之前，或裝置進入其 OOBE 流程之後。  

 如需如何設定和註冊裝置的詳細資訊，請參閱  

-   [設定 System Center Configuration Manager 中內部部署行動裝置管理的裝置註冊](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

-   [在 System Center Configuration Manager 中註冊裝置以進行內部行動裝置管理](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)  
