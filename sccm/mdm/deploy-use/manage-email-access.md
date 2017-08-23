---
title: "管理電子郵件存取 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 條件存取，以管理 Exchange 電子郵件的存取。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
caps.latest.revision: "24"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: a5c2a8912cd2ef95a778b81d0b7f1f98315b8413
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-email-access-in-system-center-configuration-manager"></a>管理 System Center Configuration Manager 中的電子郵件存取

適用於：System Center Configuration Manager (最新分支)

使用 System Center Configuration Manager 條件存取，根據您指定的條件來管理 Exchange 電子郵件的存取。  

您可以管理下列項目的存取：  

-   Microsoft Exchange 內部部署  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated

您可以從下列平台的內建電子郵件用戶端，控制對 Exchange Online 及 Exchange 內部部署的存取：  

-   Android 4.0 和更新版本、Samsung KNOX Standard 4.0 和更新版本  

-   iOS 7.1 和更新版本  

-   Windows Phone 8.1 和更新版本  

-   Windows 8.1 及更新版本上的郵件應用程式

Office 桌面應用程式可以在執行下列項目的電腦上存取 Exchange Online：  

-   啟用 [新式驗證](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) 的 Office 2013 桌面應用程式和更新版本。  

-   Windows 7.0 或 Windows 8.1  

> [!NOTE]  
>  電腦應該要已加入網域或符合在 Intune 中設定的原則。  


## <a name="device-requirements"></a>裝置需求
 如果您設定條件式存取，則在使用者可連接到其電子郵件之前，他們使用的裝置必須：  

-   已向 Intune 註冊或是已加入網域的電腦。  

-   在 Azure Active Directory 中登錄裝置 (這會在向 Intune 註冊裝置時自動發生 (僅適用於 Exchange Online)。 此外，用戶端 Exchange ActiveSync 識別碼必須向 Azure Active Directory 登錄 (不適用於連線至 Exchange 內部部署的 Windows 和 Windows Phone 裝置)。  

     針對加入網域的電腦，您必須將其設為自動向 Azure Active Directory 登錄。  在[管理 System Center Configuration Manager 中的服務存取權](../../protect/deploy-use/manage-access-to-services.md)主題中的**電腦的條件式存取**一節中列出了啟用電腦條件式存取所需的完整需求。  

-   與所有部署到該裝置的 Configuration Manager 相容性原則相容  

 如果不符合條件式存取條件，使用者即會在登入時看見下列兩則訊息之一：  

-   如果裝置未向 Intune 註冊，或者未在 Azure Active Directory 中登錄，即會顯示一則訊息，其中包含如何安裝公司入口網站應用程式、註冊裝置，以及 (適用於 Android 和 iOS 裝置) 啟用電子郵件 (這會將裝置的 Exchange ActiveSync 識別碼關聯至 Azure Active Directory 中的裝置記錄) 的相關指示。  

-   如果裝置不相容，即會顯示一則訊息，將使用者引導至 Intune 入口網站，讓他們能夠在該處找到問題的相關資訊，以及如何修復問題的方法。  

**對於行動裝置：**

您可以在使用 **iOS** 和 **Android** 裝置的瀏覽器時，限制存取 Exchange Online 上的 **Outlook Web Access (OWA)** 。  存取將只能從支援的瀏覽器相容裝置上進行︰

* Safari (iOS)
* Chrome (Android)
* 受管理的瀏覽器 (iOS 和 Android)

將會封鎖不支援的瀏覽器。不支援適用於 iOS 和 Android 的 OWA 應用程式。  它們應該會透過 ADFS 宣告規則來封鎖︰
* 設定 ADFS 宣告規則來封鎖非新式驗證通訊協定。 案例 3 提供了詳細說明 - [封鎖對瀏覽器式應用程式以外的所有 Office 365 存取](https://technet.microsoft.com/library/dn592182.aspx)。

 **針對電腦：**  

-   如果條件式存取原則需求為允許 **已加入網域** 或 **相容**，即會顯示一則訊息，提供如何註冊裝置的相關指示。 如果電腦不符合上述任一需求，即會提示使用者以 Intune 註冊裝置。  

-   如果條件式存取原則需求設為僅允許已加入網域的 Windows 裝置，即會封鎖裝置並顯示一則用來連絡 IT 系統管理員的訊息。  

 您可以在下列平台上，從內建 Exchange ActiveSync 電子郵件用戶端的裝置上封鎖 Exchange 電子郵件的存取。  

-   Android 4.0 和更新版本、Samsung KNOX Standard 4.0 和更新版本  

-   iOS 7.1 和更新版本  

-   Windows Phone 8.1 和更新版本  

-   Windows 8.1 和更新版本上的 [郵件]  應用程式  

 只有 Exchange Online 才支援適用於 iOS 和 Android 的 Outlook 應用程式，以及 Outlook 2013 桌面應用程式和更新版本。  

 要讓條件存取正常運作，Configuration Manager 和 Exchange 之間需具備**內部部署 Exchange Connector**。  

 您可透過 Configuration Manager 主控台設定 Exchange 內部部署的條件存取原則。 當您為 Exchange Online 設定條件存取原則時，請從 Configuration Manager 主控台開始程序，其會啟動 Intune 主控台，以讓您在其中完成這項程序。  

## <a name="configure-conditional-access"></a>設定條件式存取
### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>步驟 1：評估條件式存取原則的效果  
 設定好**內部部署 Exchange Connector** 之後，您可以使用 Configuration Manager 的 [依條件存取狀態顯示的裝置清單] 報告，以識別在設定條件存取原則之後將遭到封鎖而無法存取 Exchange 的裝置。 此報告也需要：  

-   訂閱 Intune  

-   應設定和部署服務連接點  

 在報告參數中，選取您要評估的 Intune 群組，以及將套用該原則的裝置平台 (如有需要)。  

 如需如何執行報告的詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。  

 執行報表之後，請檢查下列四欄以判斷是否會封鎖使用者：  

-   **管理通道** - 指出裝置是否受到 Intune、Exchange ActiveSync 或兩者所管理。  

-   **已使用 AAD 登錄** - 指出是否已向 Azure Active Directory 登錄裝置 (又稱為「工作場所聯結」)。  

-   **相容性** - 指出裝置是否與您部署的任何相容性原則相容。  

-   **EAS 已啟用** - iOS 和 Android 裝置必須將其 Exchange ActiveSync 識別碼關聯至 Azure Active Directory 中的裝置登錄記錄。 這會在使用者按一下隔離電子郵件中的 [啟用電子郵件]  連結時發生。  

    > [!NOTE]  
    >  Windows Phone 裝置永遠都會在此欄中顯示值。  

 除非欄值符合下表所列的值，否則隸屬於目標群組或集合一部分的裝置將遭到封鎖而無法存取 Exchange：  

|管理通道|AAD 已登錄|相容|EAS 已啟用|產生的動作|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**受到 Microsoft Intune 和 Exchange ActiveSync 所管理**|是|是|會顯示**是** 或 **否** |允許電子郵件存取|  
|任何其他值|否|否|不會顯示任何值|封鎖電子郵件存取|  

 您可以匯出報表的內容，並使用 [電子郵件地址]  欄來協助您通知使用者他們即將遭到封鎖。  

### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>步驟 2：針對條件式存取原則設定使用者群組或集合  
 您可以根據原則類型，將條件式存取原則的目標設為不同的使用者群組或集合。 這些群組包含將成為原則目標的使用者，或是免套用此原則的使用者。 當使用者成為原則的目標時，他們使用的每個裝置都必須相容，才能存取電子郵件。  

-   **適用於 Exchange Online 原則** - 目標為 Azure Active Directory 安全性使用者群組。 您可以在 **Office 365 系統管理中心**或 **Intune 帳戶入口網站**中設定這些群組。  

-   **適用於 Exchange 內部部署原則** - 目標為 Configuration Manager 使用者集合。 您可在 [資產與相容性]  工作區中設定這些項目。  

 您可以在每個原則中指定兩種群組類型：  

-   **目標群組** - 套用原則的使用者群組或集合  

-   **免套用的群組** - 免套用原則的使用者群組或集合 (選擇性)  

 如果使用者隸屬於這兩個群組，他們將免套用原則。  

 系統只會評估條件式存取原則設定為目標的群組或集合是否可進行 Exchange 存取。  

### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>步驟 3：設定及部署相容性原則  
 請確定您已建立相容性原則並部署到 Exchange 條件式存取原則目標的所有裝置。  

 如需如何設定相容性原則的詳細資訊，請參閱 [Manage device compliance policies in System Center Configuration Manager](device-compliance-policies.md) (管理 System Center Configuration Manager 中的裝置相容性原則)。  

> [!IMPORTANT]  
>  若未部署相容性原則，但卻啟用了 Exchange 條件式存取原則，則將允許所有目標裝置進行存取。  

 當您就緒時，請繼續執行 **步驟 4**。  

### <a name="step-4-configure-the-conditional-access-policy"></a>步驟 4：設定條件式存取原則  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>適用於 Exchange Online (以及新的 Exchange Online Dedicated 環境中的租用戶)

>[!NOTE]
>您也可以在 Azure AD 管理主控台中建立條件存取原則。 Azure AD 管理主控台可讓您在其他條件式存取原則 (例如 Multi-Factor Authentication) 之外，建立 Intune 裝置條件式存取原則 (稱為 Azure AD 裝置型條件式存取原則)。 您也可以設定 Azure AD 支援的 Salesforce 和 Box 等協力廠商企業應用程式的條件式存取原則。 如需詳細資訊，請參閱[如何設定 Azure Active Directory 裝置型條件存取原則來控制對 Azure Active Directory 連線應用程式的存取](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/)。

 適用於 Exchange Online 的條件式存取原則會使用下列流程，來評估要允許還是封鎖裝置。  

 ![ConditionalAccess8 - 1](media/ConditionalAccess8-1.png)  

 若要存取電子郵件，裝置必須：  

-   向 Intune 註冊  

-   電腦必須已加入網域或已註冊並符合在 Intune 中設定的原則。  

-   在 Azure Active Directory 中登錄裝置 (這會在向 Intune 註冊裝置時自動發生)。  

     已加入網域的電腦必須設為向 Azure Active Directory [自動註冊裝置](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) 。  

-   已啟用電子郵件，其會將裝置的 Exchange ActiveSync 識別碼關聯至 Azure Active Directory 中的裝置記錄 (僅適用於 iOS 和 Android 裝置)。  

-   與所有部署的相容性原則相容  

 裝置狀態會根據評估的條件，儲存於授與或封鎖電子郵件存取的 Azure Active Directory 中。  

 如果不符合條件，使用者即會在登入時看見下列兩則訊息之一：  

-   如果裝置未註冊，或未在 Azure Active Directory 中登錄，即會顯示一則訊息，提供如何安裝公司入口網站應用程式並加以註冊的相關指示  

-   如果裝置不相容，即會顯示一則訊息，將使用者引導至 Intune 公司入口網站或公司入口網站應用程式，讓他們能夠在該處找到問題的相關資訊，以及如何修復問題的方法。  

-   針對電腦：  

    -   如果原則設定為需要加入網域，而電腦未加入網域，就會顯示連絡 IT 管理員的訊息。  

    -   如果原則設為需要加入或與網域相容，但電腦不符合任一要求，即會顯示訊息指示如何安裝及註冊公司入口網站應用程式。  

 此訊息會顯示於適用於 Exchange Online 使用者以及新 Exchange Online Dedicated 環境中租用戶的裝置上，並傳遞至適用於 Exchange 內部部署和舊版 Exchange Online Dedicated 裝置的使用者電子郵件收件匣。  

> [!NOTE]  
>  Configuration Manager 條件存取規則會覆寫、允許、封鎖及隔離在 Exchange Online 管理主控台中定義的規則。  

> [!NOTE]  
>  條件式存取原則必須在 Intune 主控台中設定。 下列步驟從透過 Configuration Manager 存取 Intune 主控台開始。 如果出現提示，請使用設定 Configuration Manager 與 Intune 之間服務連接點時所用的相同認證來登入。  

##### <a name="to-enable-the-exchange-online-policy"></a>啟用 Exchange Online 原則  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  依序展開 [相容性設定] 和 [條件式存取] ，然後按一下 [Exchange Online] 。  

3.  在 [常用]  索引標籤的 [連結]  群組中，按一下 [在 Intune 主控台中設定條件存取原則] 。 您可能需要提供以 Intune 服務的任何全域管理員身分連線到 Configuration Manager 時，所使用的帳戶使用者名稱和密碼。  

     Intune 管理主控台隨即開啟。  

4.  在 [Microsoft Intune 管理主控台](https://manage.microsoft.com)中，按一下 **[原則]** > **[條件式存取]** > **[Exchange Online 原則]**。  

     ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5.  在 **Exchange Online 原則** 頁面上，選取 **啟用 Exchange Online 的條件式存取原則**。 如果您檢查此情形，則裝置必為相容。 如果未檢查，則不會套用條件式存取。  

    > [!NOTE]  
    >  若未部署相容性原則，但卻啟用了 Exchange Online 原則，則所有目標裝置都會回報為相容。  
    >   
    >  所有使用者無論其相容性狀態如何，此原則皆會要求他們向 Intune 註冊其裝置。  

6.  在 **[應用程式存取]**下方，針對 Outlook 和其他使用新式驗證的應用程式，您可以選擇僅限與各個平台相容的裝置才有存取權。  Windows 裝置必須已加入網域，或已在 Intune 註冊且相容。  

    > [!TIP]  
    >  **新式驗證** 將 Active Directory 驗證程式庫 (ADAL) 登入整合到 Office 用戶端中。  
    >   
    >  -   ADAL 型驗證可讓 Office 用戶端進行以瀏覽器為基礎的驗證 (又稱為被動驗證)。  系統會將使用者導向登入網頁，以便進行驗證。  
    > -   這個新的登入方法可根據 [裝置合規性] 以及是否執行 [Multi-Factor Authentication] ，來啟用條件式存取等新案例。  
    >   
    >  這篇 [文章](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) 包含新式驗證運作方式的更詳細資訊。  

     使用 Exchange Online 搭配 Configuration Manager 和 Intune 時，您不僅可以管理具有條件式存取的行動裝置，也可以管理桌上型電腦。 電腦必須已加入網域，或已在 Intune 註冊且相容。 您可以設定下列需求：  

    -   **裝置必須已加入或與網域相容。** 電腦必須已加入網域或符合原則。 如果電腦不符合上述任一需求，即會提示使用者以 Intune 註冊裝置。  

    -   **裝置必須已加入網域。** 電腦必須已加入網域才能存取 Exchange Online。 如果電腦未加入網域，則會封鎖電子郵件的存取並提示使用者連絡 IT 系統管理員。  

    -   **裝置必須相容。** 電腦必須已在 Intune 註冊且相容。 如果電腦未註冊，則會顯示註冊指示訊息。  

7.  在 **Outlook web access (OWA)**，您可以選擇只允許透過支援的瀏覽器存取 Exchange Online︰Safari (iOS) 和 Chrome (Android)。 將會封鎖從其他瀏覽器進行的存取。 您選取的相同 Outlook 應用程式存取平台限制也適用於此處。

    在 **Android** 裝置上，使用者必須啟用瀏覽器存取。  若要完成這項動作，使用者必須啟用已註冊裝置上的 [啟用瀏覽器存取] 選項，如下所示：
     1. 啟動 **公司入口網站應用程式**。
     2. 透過三個點 (...) 或硬體功能表按鈕，移至 [設定] 頁面。
      3.    按下 **[啟用瀏覽器存取]** 按鈕。
      4.    在 Chrome 瀏覽器中，登出 Office 365 並重新啟動 Chrome。

     在 **iOS 和 Android** 平台上，Azure Active Directory 會將傳輸層安全性 (TLS) 憑證發行給裝置，以識別用來存取服務的裝置。  裝置會顯示憑證，並包含要使用者選取憑證的提示，如以下螢幕擷取畫面所示。 使用者必須選取此憑證，才能繼續使用瀏覽器。

     **iOS**

     ![iPad 上憑證提示的螢幕擷取畫面](media/mdm-browser-ca-ios-cert-prompt_v2.png)

    **Android**

    ![Android 裝置上憑證提示的螢幕擷取畫面](media/mdm-browser-ca-android-cert-prompt.png)

7.  針對 **[Exchange ActiveSync 郵件應用程式]**，您可以選擇在裝置不相容時，封鎖電子郵件對 Exchange Online 的存取，以及選取在 Intune 無法管理該裝置時，是要允許還是封鎖對電子郵件的存取。  

8.  在 [目標群組] 下方，選取要套用原則之使用者的 Active Directory 安全性群組。  

    > [!NOTE]  
    >  針對目標群組中的使用者，Intune 原則會取代 Exchange 規則和原則。  
    >   
    >  Exchange 只會在下列情況強制 Exchange 允許、封鎖及隔離規則以及 Exchange 原則：  
    >   
    >  -   使用者未取得使用 Intune 的授權。  
    > -   使用者已取得使用 Intune 的授權，但不屬於條件式存取原則中的任何目標安全性群組。  

9. 在 [免套用的群組] 下方，選取免套用此原則之使用者的 Active Directory 安全性群組。 如果使用者同時隸屬於目標群組及免套用的群組，則他們將免套用此原則，並可存取其電子郵件。  

10. 完成後，請按一下 [儲存] 。  

-   您不需部署條件式存取原則，它會立即生效。  

-   在使用者建立電子郵件帳戶之後，裝置會立即遭到封鎖。  

-   如果封鎖的使用者向 Intune 註冊裝置 (或修復不相容性)，則會在 2 分鐘內解除電子郵件存取的封鎖。  

-   如果使用者取消註冊其裝置，大約會在 6 小時後封鎖電子郵件。  

### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>適用於 Exchange 內部部署 (以及舊版 Exchange Online Dedicated 環境中的租用戶)  
 適用於 Exchange 內部部署以及舊版 Exchange Online Dedicated 環境中租用戶的條件式存取原則會使用下列流程，來評估要允許還是封鎖裝置。  

 ![ConditionalAccess8 - 2](media/ConditionalAccess8-2.png)  

##### <a name="to-enable-the-exchange-on-premises-policy"></a>啟用 Exchange 內部部署原則  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  依序展開 [相容性設定] 和 [條件式存取] ，然後按一下 [內部部署 Exchange] 。  

3.  在 [常用]  索引標籤的 [內部部署 Exchange]  群組中，按一下 [設定條件存取原則] 。  

4.  **從 Configuration Manager 1602 版開始**，在**設定條件存取原則精靈** 的 **一般** 頁面上，指定是否要覆寫 Exchange Active Sync 預設規則。 如果您想要讓已註冊且相容的裝置即使在預設規則設定為隔離或封鎖存取的情況下，仍一律可以存取電子郵件，請按一下此選項。  

    > [!NOTE]  
    >  這是 Android 裝置的預設覆寫問題。 如果 Exchange 伺服器的預設存取規則是設定為 **[封鎖]** ，並且搭配使用預設規則覆寫選項來啟用 Exchange 條件式存取原則，則目標使用者的 Android 裝置即使是在 Intune 中註冊且相容之後，也可能不會獲得解除封鎖。  若要解決這個問題，請將 Exchange 預設存取規則設為 **[隔離]**。 裝置預設無法存取 Exchange，系統管理員可以從 Exchange 伺服器取得已隔離之裝置清單的相關報告。  

     如果您在設定 Exchange Connector 時沒有設定通知電子郵件帳戶，就會在此頁面上看到警告，且 **[下一步]** 按鈕會停用。  您必須先在 Exchange Connector 中設定通知電子郵件設定，然後回到 **設定條件存取原則精靈** 來完成程序，才能繼續進行操作。  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

     按一下 [下一步] 。  

5.  在 [目標集合]  頁面上，加入一或多個使用者集合。 若要存取 Exchange，這些集合中的使用者必須向 Intune 註冊他們的裝置，也必須符合您部署的任何相容性原則。  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

     按一下 [下一步] 。  

6.  在 [豁免的集合]  頁面上，加入任何您想要豁免條件式存取原則的使用者集合。 這些群組中的使用者不需向 Intune 註冊其裝置，也不需要符合任何已部署的相容性原則，即可存取 Exchange。  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

     若使用者同時隸屬於目標及免套用的清單，則他們將免套用條件式存取原則。  

     按一下 [下一步] 。  

7.  在 [編輯使用者通知] 頁面上，設定 Intune 要傳送給使用者的電子郵件 (除了 Exchange 傳送的電子郵件之外)，內含如何解除封鎖裝置的指示。  

     您可以編輯預設的訊息，並使用 HTML 標記來格式化文字的顯示方式。 您也可以事先傳送電子郵件給您的員工，通知他們即將進行變更，並提供有關註冊其裝置的指示。  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    >  由於包含修復指示的 Intune 通知電子郵件是傳遞到使用者的 Exchange 信箱，因此，若使用者的裝置在收到此電子郵件訊息之前已遭到封鎖，他們就能夠使用解除封鎖的裝置或其他方法來存取 Exchange 並檢視該訊息。  

    > [!NOTE]  
    >  為了讓 Exchange 能夠傳送通知電子郵件，您必須設定將用來傳送通知電子郵件的帳戶。 請在設定 Exchange Server 連接器的內容時，進行此項作業。  
    >   
    >  如需詳細資訊，請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

     按一下 [下一步] 。  

8.  在 [摘要]   頁面上檢閱這些設定，然後完成精靈。  

-   您不需部署條件式存取原則，它會立即生效。  

-   使用者設定 Exchange ActiveSync 設定檔之後，可能需要 1-3 個小時才能封鎖裝置 (如果不是由 Intune 管理)。  

-   如果封鎖的使用者之後使用 Intune 註冊裝置 (或修復不相容性)，則會在 2 分鐘內解除電子郵件存取的封鎖。  

-   如果使用者從 Intune 取消註冊，則可能需要 1-3 個小時才能封鎖裝置。  

### <a name="see-also"></a>請參閱  
 [管理 System Center Configuration Manager 中的服務存取權](../../protect/deploy-use/manage-access-to-services.md)
