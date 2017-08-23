---
title: "建立 Exchange ActiveSync 電子郵件設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中建立和設定與 Microsoft Intune 搭配運作的電子郵件設定檔。"
ms.custom: na
ms.date: 07/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: "4"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 7434c98f2217cf63fdcd250b91e772de72daaea9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Exchange ActiveSync 電子郵件設定檔

*適用於：System Center Configuration Manager (最新分支)*

您可以使用 Microsoft Intune 和 Exchange ActiveSync，為裝置設定電子郵件設定檔和限制。 這可讓您的使用者只需以最少的安裝步驟，即可存取其裝置上的公司電子郵件。  

 您可以使用電子郵件設定檔設定下列裝置類型：  

- Windows 10
- Windows Phone 8.1
- Windows Phone 8.0
- 執行 iOS 5、iOS 6、iOS 7 和 iOS 8 的 iPhone  
- 執行 iOS 5、iOS 6、iOS 7 和 iOS 8 的 iPad  
- Samsung KNOX Standard (4 及更新版本)
- Android for Work

若要將電子郵件設定檔部署至裝置，您必須在 Intune 中註冊裝置。 如需如何取得已註冊裝置的相關資訊，請參閱 [使用 Microsoft Intune 管理行動裝置](https://technet.microsoft.com/en-us/library/dn646962.aspx)。

> [!NOTE]
> Intune 提供兩個 Android for Work 電子郵件設定檔，分別用於 Gmail 電子郵件應用程式和 Nine Work 電子郵件應用程式。 這些應用程式都可從 Google Play 商店取得，並支援連線到 Exchange。 若要啟用電子郵件連線功能，請將其中一個電子郵件應用程式部署到使用者的裝置後，再建立及部署適當的設定檔。 Nine Work 之類的電子郵件應用程式可能不是免費的。 請檢閱應用程式的授權詳細資料，如有任何問題，請連絡應用程式公司。

 除了在裝置上設定電子郵件帳戶外，您也可以設定連絡人、行事曆和工作的同步處理設定。  

 建立電子郵件設定檔時，您可以加入多種安全性設定。 這些設定包括使用 System Center Configuration Manager 憑證設定檔所設定的身分識別、加密和簽署憑證。 如需憑證設定檔的詳細資訊，請參閱 [System Center Configuration Manager 中的憑證設定檔](/sccm/protect/deploy-use/introduction-to-certificate-profiles.md)。    

## <a name="create-an-exchange-activesync-email-profile"></a>建立 Exchange ActiveSync 電子郵件設定檔  

若要建立設定檔，您可以使用 [建立 Exchange ActiveSync 電子郵件設定檔精靈]。 

1.  在 Configuration Manager 主控台中，選擇 [資產與相容性]。  

2.  在 [資產與相容性] 工作區中，依序展開 [相容性設定]和 [公司資源存取]，然後選擇 [電子郵件設定檔]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立 Exchange ActiveSync 電子郵件設定檔] 啟動精靈。

4.  在精靈的 [一般] 頁面上，設定下列資訊：

    - **名稱**。 提供電子郵件設定檔的描述性名稱。

    - **描述**。 (選擇性) 提供可協助您在 Configuration Manager 主控台中識別此電子郵件設定檔的描述。

    - **此電子郵件設定檔適用於 Android for Work**： 如果您只會將此電子郵件設定檔部署至 Android for Work 裝置，請選擇此選項。 如果您核取此方塊，不會顯示 [支援的平台] 精靈頁面。 只會設定 Android for Work 電子郵件設定檔。

4.  在精靈的 [Exchange ActiveSync] 頁面上，指定下列資訊：  

    -   **Exchange ActiveSync 主機**： 指定託管 Exchange ActiveSync 服務之公司 Exchange 伺服器的主機名稱。  

    -   **帳戶名稱**： 指定在使用者裝置上向使用者顯示的電子郵件帳戶顯示名稱。  

    -   **帳戶使用者名稱**： 選擇用戶端裝置上之電子郵件帳戶使用者名稱的設定方式。 您可以從下拉式清單中選擇下列其中一個選項：  

        -   **使用者主體名稱**： 使用完整使用者主體名稱登入 Exchange。  

        -   **帳戶名稱**： 使用 Active Directory 中的完整使用者帳戶名稱。

        -   **主要 SMTP 位址**： 使用使用者的主要 SMTP 位址登入 Exchange。  

    -   **電子郵件地址**： 選擇每個用戶端裝置上使用者的電子郵件地址的產生方式。 您可以從下拉式清單中選擇下列其中一個選項：  

        -   **主要 SMTP 位址**： 使用使用者的主要 SMTP 位址登入 Exchange。  

        -   **使用者主體名稱**： 使用完整使用者主體名稱作為電子郵件地址。  

    -   **帳戶網域**： 選擇下列其中一個選項：  

        -   **從 Active Directory 取得**  

        -   **自訂**  

         只有當選取 [帳戶使用者名稱] 下拉式清單中的 **sAMAccountName** 時，這個欄位才適用。  

    -   **驗證方法**： 選擇要用來驗證 Exchange ActiveSync 連線的下列其中一個驗證方法：  

        -   **憑證**： 要用來驗證 Exchange ActiveSync 連線的身分識別憑證。  

        -   **使用者名稱和密碼**： 裝置使用者必須提供用來連線至 Exchange ActiveSync 的密碼 (使用者名稱已設定為電子郵件設定檔的一部分)。  

    -   **身分識別憑證**： 選擇 [選取]，然後選擇要用於身分識別的憑證。  

         身分識別憑證必須是 SCEP 憑證，不得使用 PFX 憑證。  若要深入了解，請參閱 [System Center Configuration Manager 中的憑證設定檔](/sccm/protect/deploy-use/introduction-to-certificate-profiles)。  

         只有當選擇 [驗證方法] 下方的 [憑證] 時，才能使用這個選項。  

    -   **使用 S/MIME**： 使用 S/MIME 加密傳送外寄電子郵件。 這個選項僅適用於 iOS 裝置。 選擇下列選項：

        -   **簽署憑證**。  選擇 [選取]，然後選擇要用於加密的憑證設定檔。  

            設定檔可以是 SCEP 或 PFX 憑證。  不過，如果同時使用簽署和加密，您必須選取用於簽署和加密*兩者*的 PFX 憑證設定檔。

        -   **加密憑證**： 選擇 [選取]，然後選擇要用於加密的憑證。 您只能選擇一個 PFX 憑證作為加密憑證。

        -   若要加密 iOS 裝置上的所有郵件訊息，請啟用 [需要加密] 核取方塊。    

         您必須先建立憑證設定檔，才能在此選擇。  若要深入了解，請參閱 [System Center Configuration Manager 中的憑證設定檔](/sccm/protect/deploy-use/introduction-to-certificate-profiles)。  

## <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>進行 Exchange ActiveSync 電子郵件設定檔的同步處理設定  

在 [建立 Exchange ActiveSync 電子郵件設定檔精靈] 的 [設定同步處理設定]  頁面上，指定下列資訊：  

-   **排程**。 選擇裝置用來同步 Exchange 伺服器中資料的排程。 這個選項僅適用於 Windows Phone 裝置。 從下列選項進行選擇：  

    -   **未設定**： 不會強制執行同步處理排程。 這個選項可讓使用者設定自己的同步處理排程。  

    -   **郵件送達時**： 電子郵件和行事曆項目等資料送達時，會自動進行同步。  

    -   **15 分鐘**： 每隔 15 分鐘會自動同步電子郵件和行事曆項目等資料。  

    -   **30 分鐘**： 每隔 30 分鐘會自動同步電子郵件和行事曆項目等資料。  

    -   **60 分鐘**： 每隔 60 分鐘會自動同步電子郵件和行事曆項目等資料。  

    -   **手動**： 裝置使用者必須手動起始同步處理。  

-   **要同步處理的電子郵件天數**： 從下拉式清單中，選擇您要同步電子郵件的天數。 選擇下列其中一個值：  

    -   **未設定**： 不會強制執行設定。 這個選項可讓使用者設定要下載至其裝置的電子郵件數目。  

    -   **無限制**： 同步所有可用的電子郵件。  

    -   **1 天**  

    -   **3 天**  

    -   **1 週**  

    -   **2 週**  

    -   **1 個月**  

-   **允許將郵件移到其他電子郵件帳戶**： 選擇這個選項可讓使用者在其裝置上所設定的不同帳戶之間移動電子郵件訊息。 這個選項僅適用於 iOS 裝置。  

-   **允許從協力廠商應用程式傳送電子郵件**： 選擇這個選項可讓使用者從特定非預設的協力廠商電子郵件應用程式傳送電子郵件。 這個選項僅適用於 iOS 裝置。  

-   **同步處理最近使用的電子郵件地址**： 選擇這個選項可同步裝置上最近使用的電子郵件地址清單。 這個選項僅適用於 iOS 裝置。  

-   **使用 SSL**： 選擇這個選項可在傳送電子郵件、接收電子郵件，以及與 Exchange 伺服器通訊時，使用安全通訊端層 (SSL) 通訊。  

-   **要同步處理的內容類型**： 選擇您想要與裝置同步的內容類型。 這個選項僅適用於 Windows Phone 裝置。 從下列選項進行選擇：  

    -   **電子郵件**  

    -   **連絡人**  

    -   **行事曆**  

    -   **工作**  

## <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>指定 Exchange ActiveSync 電子郵件設定檔的支援平台  

1.  在 [建立 Exchange ActiveSync 電子郵件設定檔精靈] 的 [支援的平台] 頁面上，選擇將安裝電子郵件設定檔的作業系統。 或者，選擇 [全選] 將電子郵件設定檔安裝到所有可用的作業系統。  

2.  完成精靈。

如需如何部署 Exchange ActiveSync 電子郵件設定檔的相關資訊，請參閱[如何在 System Center Configuration Manager 中部署設定檔](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)。  
