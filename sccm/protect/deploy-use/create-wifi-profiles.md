---
title: "如何建立 Wi-Fi 設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用 Wi-Fi 設定檔，將無線網路設定部署至組織中的使用者。"
ms.custom: na
ms.date: 12/11/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
caps.latest.revision: "13"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: f1ae976899de1fd3efcbde0c7268f071a5d0218b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-wi-fi-profiles"></a>建立 Wi-Fi 設定檔

*適用於：System Center Configuration Manager (最新分支)*


在 System Center Configuration Manager 中使用 Wi-Fi 設定檔，將無線網路設定部署至組織中的使用者。 部署這些設定，即可讓使用者更輕鬆地連線至 Wi-Fi。  

 例如，您想要讓所有 iOS 裝置連線到您的 Wi-Fi 網路。 建立 Wi-Fi 設定檔，內含連線到無線網路所需的設定。 然後，將設定檔部署到在您的階層中擁有 iOS 裝置的所有使用者。 iOS 裝置使用者可在無線網路清單中看見公司網路，並且可直接連線至該網路。  

 您可以使用 Wi-Fi 設定檔設定下列裝置類型：  

-   執行 Windows 8.1 32 位元的裝置  

-   執行 Windows 8.1 64 位元的裝置  

-   執行 Windows RT 8.1 的裝置  

-   執行 Windows 10 Desktop 或 Windows 10 行動裝置版的裝置  

[建立行動裝置的 Wi-Fi 設定檔](../../mdm/deploy-use/create-wifi-profiles.md)提供有關如何使用 Configuration Manager 中的 Wi-Fi 設定檔，將無線網路設定部署至行動裝置使用者的詳細資訊。

> [!IMPORTANT]  
>  若要將設定檔部署到 Android、iOS、Windows Phone 和已註冊的 Windows 8.1 或更新版本的裝置，必須在 Microsoft Intune 註冊這些裝置。 如需如何註冊裝置的相關資訊，請參閱[在 Intune 中註冊裝置以進行管理](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)。  

 建立 Wi-Fi 設定檔時，您可以加入多種安全性設定。 這些安全性設定包括使用 Configuration Manager 憑證設定檔推送的伺服器驗證和用戶端驗證憑證。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。  

## <a name="create-a-wi-fi-profile"></a>建立 Wi-Fi 設定檔  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [合規性設定] >  [公司資源存取] > [Wi-Fi 設定檔]。  

3.  在 [常用] 索引標籤的 [建立] 群組中，選擇 [建立 Wi-Fi 設定檔]。  

1.  在 [一般] 頁面上，輸入此 Wi-Fi 設定檔的唯一名稱和描述。  如果您想要使用另一個 Wi-Fi 設定檔的設定，請選取 **[從檔案匯入現有的 Wi-Fi 設定檔項目]**。  

    > [!IMPORTANT]  
    >  請確定您匯入的 Wi-Fi 設定檔包含 Wi-Fi 設定檔的有效 XML。 當您匯入檔案時，Configuration Manager 不會驗證設定檔。  

3.  在 [報告的不相容嚴重性] 中，指定在發現用戶端裝置上的 Wi-Fi 設定檔不相容時所報告的嚴重性層級 (例如，如果設定檔安裝失敗)。 可用的嚴重性層級如下：  

    -   **無**：不符合這項相容性規則的電腦不會回報 Configuration Manager 報告的失敗嚴重性。  

    -   **資訊**：不符合這項相容性規則的電腦會回報 Configuration Manager 報告的 [資訊] 失敗嚴重性。  

    -   **警告**：不符合這項相容性規則的電腦會回報 Configuration Manager 報告的 [警告] 失敗嚴重性。  

    -   **重大**：不符合這項相容性規則的電腦會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。  

    -   **重大事件**：不符合這項相容性規則的電腦會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。 此嚴重性層級也會在應用程式事件記錄檔中記錄為 Windows 事件。  

1.  在 [Wi-Fi 設定檔] 頁面上，提供裝置將顯示為網路名稱的名稱。  

    > [!IMPORTANT]  
    >  Configuration Manager 不支援在網路名稱中使用單引號 (**â€˜**) 或逗號 (**,**) 字元。  

2.  指定區分大小寫的 **SSID**
3.  選擇其他適當的連線選項，包括。   **在網路未廣播其名稱 (SSID) 時進行連線** (如果可能隱藏了 SSID)  

4.  在 [安全性設定] 頁面上，選取無線網路使用的安全性通訊協定，或在網路不安全時選取 [不驗證 (開放)]。
    > [!IMPORTANT]  
    >  如果您要建立 Wi-Fi 設定檔來進行內部部署行動裝置管理，則 Configuration Manager 的最新分支只支援下列 Wi-Fi 安全性設定：  
    >   
    >  安全性類型： **WPA2 Enterprise** 或 **WPA2 Personal**  
    > 加密類型： **AES** 或 **TKIP**  
    > EAP 類型： **智慧卡或其他憑證** 或 **PEAP**  

    > 針對 Android 裝置，不支援 [WPA Personal]、[WPA2 Personal] 和 [WEP] 安全性類型。  

2.  選取無線網路使用的加密方法。  

3.  選取用來進行無線網路驗證的 EAP 類型。  

     僅適用於 Windows Phone 裝置：不支援 [LEAP]  和 [EAP-FAST]  的 EAP 類型。  

4.  請按一下 [設定]  以指定所選取 EAP 類型的屬性。 此選項可能不適用於選取的某些 EAP 類型。  

    > [!IMPORTANT]  
    >  當您按一下 [設定] 時會開啟一個 Windows 對話方塊。 基於此原因，您必須確定執行 Configuration Manager 主控台之電腦的作業系統支援設定選取的 EAP類型。  
    >   
    >  針對 iOS 裝置，如果您選擇非 EAP 方法進行驗證，不論您選擇的方法為何，都會使用 MS-CHAP v2 進行連線。  

5.  如果您想要儲存使用者認證，以便使用者不需要在每次登入時輸入認證，請選取 [每次登入時記住使用者認證] 。  

6. **僅適用於 iOS 裝置：**  
 設定 Wi-Fi 連線所需要的任何憑證資訊。 您必須設定用戶端憑證，以及信任的伺服器憑證名稱或根憑證，如下所示：  

    -   **信任的伺服器憑證名稱**：如果裝置連線的伺服器使用伺服器驗證憑證來識別伺服器並協助保護通訊通道，請在該憑證的主體名稱或主體別名中輸入一個或多個名稱。 這些名稱通常是伺服器的完整網域名稱。 例如，如果伺服器憑證在憑證主體中的一般名稱是 srv1.contoso.com，則輸入 **srv1.contoso.com**。 如果伺服器憑證在主體別名中指定多個名稱，請使用分號分隔輸入的每個名稱。  

    > [!TIP]  
    >  如果您為 EAP 選取的用戶端憑證或 iOS 裝置的用戶端驗證將用來驗證遠端驗證撥入使用者服務 (RADIUS) 伺服器 (例如執行網路原則伺服器的伺服器)，您必須將 [主體別名] 設定為使用者主體名稱。  

    -   **選取根憑證以進行伺服器驗證**：如果裝置連線的伺服器使用裝置不信任的伺服器驗證憑證，請選取包含伺服器憑證之根憑證的憑證設定檔，以在裝置上建立信任的憑證鏈結。  

    -   **選取用戶端驗證的用戶端憑證**：如果伺服器或網路裝置需要用戶端憑證來驗證連接的裝置，選取包含用戶端驗證憑證的憑證設定檔。  

    > [!NOTE]  
    >  在選取根憑證和用戶端憑證之前，您必須先將其設定及部署為憑證設定檔。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。  

7.  在 [進階設定] 頁面上，指定 Wi-Fi 設定檔的進階設定，例如驗證模式、單一登入選項和美國聯邦資訊處理標準相容性。 如需這些選項的詳細資訊，請參閱您的 Windows 文件。 視您在精靈的 [安全性設定]  頁面上選取的選項而定，進階設定可能無法使用或者有所變動。  

1.  如果您的無線網路使用 Proxy 伺服器，請在 [Proxy 設定] 頁面上，選取 [設定此 Wi-Fi 設定檔的 Proxy 設定]，然後提供設定資訊。  

2. 在 [支援的平台] 頁面上，選取您要安裝 Wi-Fi 設定檔的作業系統。 或者，按一下 [全選]  將 Wi-Fi 設定檔安裝到所有可用的作業系統。  

### <a name="next-steps"></a>後續步驟
 如需如何部署 Wi-Fi 設定檔的資訊，請參閱 [How to deploy Wi-Fi profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) (如何在 System Center Configuration Manager 中部署 Wi-Fi 設定檔)。  
