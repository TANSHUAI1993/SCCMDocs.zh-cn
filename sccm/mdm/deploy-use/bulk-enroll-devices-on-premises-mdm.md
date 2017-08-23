---
title: "大量註冊裝置 | Microsoft Docs | 內部部署 MDM"
description: "在 System Center Configuration Manager 中使用內部部署行動裝置管理，以自動方式大量註冊裝置。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
caps.latest.revision: "13"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: be9596537e9c80a6d78aa0685d33382bfd242afe
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中使用內部部署行動裝置管理大量註冊裝置

適用於：System Center Configuration Manager (最新分支)


System Center Configuration Manager 內部部署行動裝置管理中的大量註冊是一種比起使用者註冊更自動化的裝置註冊方式，使用者註冊需要使用者輸入認證來註冊裝置。  大量註冊使用註冊套件在註冊期間驗證裝置。 套件 (.ppkg 檔案) 包含憑證設定檔，以及選擇性地包含 Wi-Fi 設定檔，如果裝置需要內部網路連線才能支援註冊的話。  

> [!NOTE]  
>  Configuration Manager 的最新分支，支援執行下列作業系統的裝置在內部部署行動裝置管理中註冊：  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 團隊版  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 企業版   

下列工作說明如何為內部部署行動裝置管理大量註冊電腦和裝置：  

-   [建立憑證設定檔](#bkmk_createCert)  

-   [建立 Wi-Fi 設定檔](#CreateWifi)  

-   [建立註冊設定檔](#bkmk_createEnroll)  

-   [建立註冊套件 (ppkg) 檔案](#bkmk_createPpkg)  

-   [使用套件來大量註冊裝置](#bkmk_getPpkg)  

-   [確認裝置的註冊](#bkmk_verifyEnroll)  

##  <a name="bkmk_createCert"></a> 建立憑證設定檔  
 註冊套件的主要元件是憑證設定檔，它用來自動提供信任的根憑證給正在註冊的裝置。  裝置與內部部署行動裝置管理所需的站台系統角色之間進行信任通訊時，需要這個根憑證。 若沒有根憑證，裝置在它與裝載註冊點、註冊 Proxy 點、發佈點和裝置管理點站台系統角色的伺服器之間的 HTTPS 連線中便不會受到信任。  

 在針對內部部署行動裝置管理準備系統時，您匯出了一個根憑證，您可以在註冊套件的憑證設定檔中使用它。 如需如何取得受信任根憑證的指示，請參閱[將具有相同的根的憑證匯出為網頁伺服器憑證](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert)。  

 使用匯出的根憑證建立憑證設定檔。 如需相關指示，請參閱[如何在 System Center Configuration Manager 中建立憑證設定檔](../../protect/deploy-use/create-certificate-profiles.md)。  

##  <a name="CreateWifi"></a> 建立 Wi-Fi 設定檔  
 用於大量註冊之套件的另一個元件是 Wi-Fi 設定檔。 有些裝置在佈建網路設定之前，可能沒有支援註冊所需的網路連線。 在註冊套件中包含 Wi-Fi 設定檔提供了一種方法來建立裝置的網路連線。  

 若要在 Configuration Manager 中建立 Wi-Fi 設定檔，請依照[如何在 System Center Configuration Manager 中建立 Wi-Fi 設定檔](../../protect/deploy-use/create-wifi-profiles.md)中的指示進行。  

> [!IMPORTANT]  
>建立用於大量註冊的 Wi-Fi 設定檔時，請記住下列兩個問題：
>
> - Configuration Manager 的最新分支只支援進行內部部署行動裝置管理的下列 Wi-Fi 安全性設定：  
>   
>   - 安全性類型： **WPA2 Enterprise** 或 **WPA2 Personal**  
>   - 加密類型： **AES** 或 **TKIP**  
>   - EAP 類型： **智慧卡或其他憑證** 或 **PEAP**  
>
>
> - 雖然 Configuration Manager 在 Wi-Fi 設定檔中有 Proxy 伺服器資訊的設定，但不會在註冊裝置之後設定 Proxy。 如果您需要使用註冊的裝置來設定 Proxy 伺服器，您可以在註冊裝置之後使用設定項目來部署設定，或使用 Windows 映像處理與設定設計工具 (ICD) 建立第二個套件，以便與大量註冊套件一起部署。

##  <a name="bkmk_createEnroll"></a> 建立註冊設定檔  
 註冊設定檔可讓您指定裝置註冊所需的設定，包括會動態佈建信任根憑證給裝置的憑證設定檔，以及視需要佈建網路設定的 Wi-Fi 設定檔。  

 建立註冊設定檔之前，請確定您已建立憑證設定檔和 Wi-Fi 設定檔 (如果需要)。 如需詳細資訊，請參閱 [建立憑證設定檔](#bkmk_createCert) 和 [建立 Wi-Fi 設定檔](#CreateWifi)。  

#### <a name="to-create-an-enrollment-profile"></a>建立註冊設定檔  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] >[概觀] >[所有屬公司擁有的裝置] >[Windows] >[註冊設定檔]。  

2.  以滑鼠右鍵按一下 [註冊設定檔]  ，然後按一下 [建立設定檔] 。  

3.  在 [建立註冊設定檔精靈] 中，輸入設定檔的名稱、確定針對 [管理授權單位]  選取了 [內部部署] ，然後按一下 [下一步] 。  

4.  選取站台碼，然後按一下 [下一步] 。  

5.  選取 [僅限內部網路] 、選取裝置將用來啟動註冊程序的註冊 Proxy 點，然後按一下 [下一步] 。  

6.  選取包含受信任根憑證 (這是您在 [Create a certificate profile](#bkmk_createCert)中建立的設定檔) 的憑證設定檔，按一下 [下一步] 。  

7.  選取包含必要網路設定的 Wi-Fi 設定檔，以便裝置能連線到內部網路 (這是您在 [Create a Wi-Fi profile](#CreateWifi)建立的設定檔)，然後按一下 [下一步] 。  

    > [!NOTE]  
    >  如果您的註冊套件不使用 Wi-Fi 設定檔，請略過此步驟。  

8.  確認註冊設定檔的設定，然後按一下 [下一步]。 按一下 [關閉]  以結束精靈。  

##  <a name="bkmk_createPpkg"></a> 建立註冊套件 (ppkg) 檔案  
 註冊套件是您用來為內部部署行動裝置管理大量註冊裝置的檔案。  此檔案必須使用 Configuration Manager 建立。 您可以使用 Windows 映像處理與設定設計工具 (ICD) 建立類似類型的套件，但只有您在 Configuration Manager 建立的套件可用來全程為內部部署行動裝置管理註冊裝置。 使用 Windows ICD 建立的套件只能提供註冊所需的使用者主要名稱 (UPN)，而不能執行實際的註冊程序。  

 在 Windows 10 建立註冊套件的程序需要 Windows 評定及部署工具套件 (ADK)。  在執行 Configuration Manager 主控台的伺服器上，請確定您已安裝 1511 版的 Windows ADK。 如需詳細資訊，請參閱 [下載 Windows 10 的套件與工具](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)的＜ADK＞一節  

> [!TIP]  
>  如果您從 Configuration Manager 主控台移除註冊套件，它便無法用來註冊裝置。 您可以使用套件移除來管理您不想再用於大量註冊裝置的套件。  

#### <a name="to-create-an-enrollment-package-ppkg-file"></a>建立註冊套件 (ppkg) 檔案：  

1.  以滑鼠右鍵按一下剛才建立的設定檔 (在 [建立註冊設定檔](#bkmk_createEnroll)) 中，然後按一下 [匯出] 。  

2.  按一下 [瀏覽] 、找出您想要儲存 .ppkg 檔案的位置、輸入套件的名稱，然後按一下 [儲存] 。  

3.  如果您想要利用密碼保護套件，請按一下 [加密套件] 旁的核取方塊，然後按一下 [匯出]  ，並等待約 10 秒讓匯出完成。  

    > [!NOTE]  
    >  如果您已加密套件，Configuration Manager 會提供包含解密密碼的訊息。 請確定您儲存密碼資訊，因為您需要它才能在裝置上佈建套件。  

4.  按一下 [ **確定**]。  

##  <a name="bkmk_getPpkg"></a> 使用套件來大量註冊裝置  
 您可以在透過全新體驗 (OOBE) 程序佈建裝置之前或之後，使用套件註冊裝置。   註冊套件也可以包含為原始設備製造商 (OEM) 佈建套件的一部分。  

 套件必須實體傳遞給要用它來大量註冊的裝置。 您可以根據需求以各種方式傳遞註冊套件到裝置，包括：  

-   從檔案系統複製  

-   附加至電子郵件  

-   透過近距離無線通訊 (NFC) 連線複製  

-   從記憶卡複製  

-   掃描條碼  

-   從有行動網卡的裝置複製  

-   包含在 OEM 佈建套件中  

#### <a name="to-bulk-enroll-a-device"></a>大量註冊裝置：  

1.  在要註冊的裝置上，尋找註冊套件 (使用檔案總管) 並按兩下 .ppkg 檔案。  

2.  在 [使用者帳戶控制] 訊息中，按一下 [是]  。  

3.  在詢問您套件是否來自信任來源的對話方塊中，按一下 [是的，新增]。  

     註冊程序會開始，並需要大約 5 分鐘。  

4.  開啟 [設定] 。  

5.  按一下 [關閉]   > 的站台系統角色之間進行信任通訊時，需要這個根憑證。 註冊成功時，您會在 []   

6.  按一下該帳戶，然後按一下 [同步]，這會以 Configuration Manager 開始管理。  

##  <a name="bkmk_verifyEnroll"></a> 確認裝置的註冊  
 您可以在 Configuration Manager 主控台確認裝置已成功註冊。  

-   啟動 Configuration Manager 主控台。  

-   按一下 [關閉]  >  > 的站台系統角色之間進行信任通訊時，需要這個根憑證。 註冊的裝置會出現在清單中。  
