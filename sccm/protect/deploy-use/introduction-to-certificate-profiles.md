---
title: "憑證設定檔簡介 | Microsoft Docs"
description: "了解如何搭配使用 System Center Configuration Manager 中的憑證設定檔與 Active Directory 憑證服務。"
ms.custom: na
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: "7"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 7b1c0e449f3d1ef42e279e8707df6bf1df163b3f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>簡介 System Center Configuration Manager 中的憑證設定檔

適用於：System Center Configuration Manager (最新分支)


憑證設定檔與 Active Directory 憑證服務和網路裝置註冊服務角色搭配運作，以佈建受管理裝置的驗證憑證，讓使用者可以順暢地存取公司資源。 例如，您可以建立和部署憑證設定檔，以提供必要的憑證讓使用者起始 VPN 和無線網路連線。 

憑證設定檔可以自動設定使用者裝置，如此不需要手動安裝憑證或使用超出訊號範圍的程序，就能存取 Wi-Fi 網路和 VPN 伺服器等公司資源。 憑證設定檔也有助於維持公司資源的安全性，因為您可以使用更多您的企業公開金鑰基礎結構 (PKI) 支援的安全設定。 例如，您可以對所有 Wi-Fi 和 VPN 連線進行伺服器驗證，因為您已在受管理的裝置上佈建所需的憑證。   

憑證設定檔提供下列管理功能：  

-   為執行 iOS、Windows 8.1、Windows RT 8.1、Windows 10 Desktop 與行動裝置版和 Android 的裝置，註冊憑證以及從企業憑證授權單位 (CA) 更新憑證。 然後，這些憑證就可以用於 Wi-Fi 和 VPN 連線。  

-   部署信任根 CA 憑證和中繼 CA 憑證，以便在需要伺服器驗證時在裝置上針對 VPN 和 Wi-Fi 連線設定信任鏈結。  

-   監視和報告已安裝的憑證。  

**範例：** 所有員工都必須可以連線到多個公司位置中的 Wi-Fi 熱點。 部署連線至 Wi-Fi 所需的憑證，並部署參考憑證的 Wi-Fi 設定檔以啟用順暢的使用者連線。  

**範例：** 您已備妥 PKI，且想改用更具彈性且更安全的方法來佈建憑證，讓使用者能從個人裝置存取公司資源，又不會危及安全性。 使用特定裝置平台所支援的設定及通訊協定來設定憑證設定檔。 裝置之後可以自動向網際網路對向註冊伺服器要求這些憑證。 接著，將 VPN 設定檔設定為使用這些憑證讓裝置可以存取公司資源。  

## <a name="types-of-certificate-profiles"></a>憑證設定檔的類型  
 有三種類型的憑證設定檔：  

-   **信任的 CA 憑證** - 可讓您部署受信任根 CA 或中繼 CA 憑證，以在裝置必須驗證伺服器時形成憑證信任鏈。  

-   **簡單憑證註冊通訊協定 (SCEP)** - 可讓您在執行 Windows Server 2012 R2 的伺服器上，使用 SCEP 通訊協定和「網路裝置註冊服務」來要求裝置或使用者的憑證。

    若要建立 [簡單憑證註冊通訊協定 (SCEP)] 憑證設定檔，您必須先建立 [信任的 CA 憑證] 憑證設定檔。

-   **個人資訊交換 (.pfx)** - 可讓您要求裝置或使用者的 .pfx (也稱為 PKCS #12) 憑證。

    您可以透過從現有憑證[匯入認證](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md)，或是透過[定義憑證](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md)授權單位以處理要求，來建立 PFX 憑證設定檔。

    從 1706 版開始，您可以使用 Microsoft 或 Entrust 作為**個人資訊交換 (.pfx)** 憑證的憑證授權單位。


## <a name="requirements-and-supported-platforms"></a>需求和支援的平台  
若要部署使用 SCEP 的憑證設定檔，您必須在管理中心網站或主要站台中的站台系統伺服器上，安裝憑證登錄點。 您也必須以 Active Directory 憑證服務角色和需要憑證的裝置可存取的作用中 NDES，將用於 NDES 的原則模組 (即 Configuration Manager 原則模組) 安裝在執行 Windows Server 2012 R2 的伺服器上。 若是由 Microsoft Intune 註冊的裝置，則需要可以從網際網路存取的 NDES，例如遮蔽式子網路 (也稱為 DMZ)。  

PFX 憑證在管理中心網站或主要站台中的站台系統伺服器上也需要憑證登錄點。  您也必須針對憑證指定憑證授權單位 (CA)，並指定相關的存取認證。  從 1706 版開始，您可以將 Microsoft 或 Entrust 指定為憑證授權單位。  

如需網路裝置註冊服務如何支援原則模組，以供 Configuration Manager 部署憑證的詳細資訊，請參閱[使用原則模組和網路裝置註冊服務](http://go.microsoft.com/fwlink/p/?LinkId=328657)。  

Configuration Manager 可根據需求、裝置類型和作業系統，將憑證部署至不同的憑證存放區。 支援下列裝置和作業系統：  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop 與行動裝置版  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  若要將設定檔部署到 Android、iOS、Windows Phone 和已註冊的 Windows 8.1 或更新版本的裝置，必須在 [Microsoft Intune 註冊](https://technet.microsoft.com/en-us/library/dn646962.aspx)這些裝置。   

以 System Center Configuration Manager 來說，如果連線是使用 EAP-TLS、EAP-TTLS 和 PEAP 驗證通訊協定以及 IKEv2、L2TP/IPsec 和 Cisco IPsec VPN 通道通訊協定，一般都會安裝信任的根 CA 憑證以驗證 Wi-Fi 和 VPN 伺服器。  

您必須確保企業根 CA 憑證已安裝在裝置上，裝置才能使用 SCEP 憑證設定檔要求憑證。  

您可以在 SCEP 憑證設定檔中指定各種設定，以針對不同的環境或連線需求要求自訂的憑證。 [建立憑證設定檔精靈]  中包含兩個頁面的註冊參數。 第一個頁面 [SCEP 註冊] 包含註冊要求以及憑證安裝位置的設定。 第二個頁面 [憑證內容] 則說明要求的憑證本身。  

## <a name="deploying-certificate-profiles"></a>部署憑證設定檔  
 當您部署憑證設定檔時，設定檔中的憑證檔案會安裝在用戶端裝置上。 系統也會部署任何 SCEP 參數，並且會在用戶端裝置上處理 SCEP 要求。 您可以將憑證設定檔部署至使用者或裝置集合，並且指定各個憑證的目的地存放區。 適用性規則會決定憑證是否可以安裝在裝置上。 當憑證設定檔部署至使用者集合時，使用者裝置親和性會決定要以使用者的哪個裝置安裝憑證。 當含有使用者憑證的憑證設定檔部署至裝置集合時，預設會將憑證安裝在使用者的各個主要裝置上。 您可以在 [建立憑證設定檔精靈] 的 [SCEP 註冊] 頁面上，將此行為修改為安裝憑證至使用者的任何裝置上。 此外，使用者憑證將不會部署至工作群組電腦的裝置。  

## <a name="monitoring-certificate-profiles"></a>監視憑證設定檔  

您可以檢視合規性結果或報告來監視憑證設定檔部署。 [如何監視憑證設定檔](/sccm/protect/deploy-use/monitor-certificate-profiles)描述這些方式。


## <a name="automatic-revocation-of-certificates"></a>憑證的自動撤銷  
 在下列情況下， System Center Configuration Manager 會自動撤銷使用憑證設定檔建立的使用者和電腦憑證：  

-   System Center Configuration Manager 管理功能已將裝置淘汰。  

-   已選擇抹除裝置。  

-   System Center Configuration Manager 管理功能已封鎖裝置。  

 網站伺服器會傳送撤銷命令到發行憑證授權單位，以撤銷憑證。 撤銷的原因是 [操作停止] 。  