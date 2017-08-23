---
title: "條件式存取 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 中的條件式存取，以協助保護電子郵件及其他服務。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: "26"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: d6933a331bb229f7e378e8f0bfa511f6b0553ae9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>管理 System Center Configuration Manager 中的服務存取權

適用於：System Center Configuration Manager (最新分支)


## <a name="conditional-access-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的條件式存取
使用 [條件式存取]可依據您指定的條件，協助保護已向 Microsoft Intune 註冊之裝置上的電子郵件和其他服務。  

 如需**以 System Center Configuration Manager 管理並評估相容性之電腦的條件式存取**資訊，請參閱[管理 System Center Configuration Manager 所管理之電腦對 O365 服務的存取](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)。  


 條件式存取的標準流程大致如下：  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 您可以使用條件存取來管理下列服務的存取：  

-   Microsoft Exchange 內部部署  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated  

-   SharePoint Online  

-   商務用 Skype Online

-   Dynamics CRM Online

 若要實作條件式存取，可在 Configuration Manager 中設定兩種原則類型：  

-   **相容性原則** 不是必要的原則，可以部署到使用者集合，以及用於評估設定，例如：  

    -   密碼  

    -   加密  

    -   裝置為 jailbroken 或根目錄  

    -   裝置上的電子郵件是由 Configuration Manager 或 Intune 原則管理  

     **若未將相容性原則部署到裝置，所有適用的條件式存取原則皆會將裝置視為相容**。  

-   **條件式存取原則**會針對特定服務設定，並定義規則，例如哪些 Azure Active Directory 安全性使用者群組或 Configuration Manager 使用者集合將是目標，或是豁免。  

     您可設定 Configuration Manager 主控台的內部部署 Exchange 條件式存取原則。 不過，當您設定 Exchange Online 或 SharePoint Online 的原則時，這會開啟您用來設定原則的 Intune 管理主控台。  

     不同於其他 Intune 或 Configuration Manager 原則，您無須部署條件式存取原則。 這類原則只需要部署一次，就會套用到所有受管理的使用者。  

 當裝置不符合您設定的條件時，會將使用者導向註冊裝置及修正裝置不相容之問題的程序。  

在您開始使用條件式存取**之前**，請確定您已確實地了解**需求**：  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Exchange Online 的需求 (使用共用的多租用戶環境)
Exchange Online 條件式存取支援執行下列各項的裝置：
-   Windows 8.1 及更新版本 (已向 Intune 註冊)
-   Windows 7.0 或 Windows 8.1 (已加入網域時)
-   Windows Phone 8.1 和更新版本
-   iOS 7.1 和更新版本
-   Android 4.0 和更新版本、Samsung KNOX Standard 4.0 和更新版本

 **此外**：
-   裝置必須加入工作地點，以向 Azure Active Directory 裝置註冊服務 (AAD DRS) 註冊。<br />     
- 聯結網域的電腦必須透過群組原則或 MSI 自動向 Azure Active Directory 註冊。

  本主題中的 **電腦的條件存取** 一節將說明為電腦啟用條件存取的所有需求。<br />     
  Intune 和 Office 365 客戶將會自動啟用 AAD DRS。 已部署 ADFS 裝置註冊服務的客戶不會在其內部部署 Active Directory 中看到已註冊的裝置。
-   您必須使用包含 Exchange Online (例如 E3) 的 Office 365 訂閱，而且使用者必須具備 Exchange Online 授權。
-   您可選用 **Exchange Server 連接器**，其會將 Configuration Manager 連線至 Microsoft Exchange Online，並協助您透過 Configuration Manager 主控台，來監視裝置資訊 (請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md))。
您無須使用連接器，就能使用相容性原則或條件存取原則，但在執行報告必須使用，以協助您評估條件存取的影響。

## <a name="requirements-for-exchange-online-dedicated"></a>Exchange Online Dedicated 的需求
Exchange Online Dedicated 的條件存取支援執行下列平台的裝置：
-   Windows 8 及更新版本 (已向 Intune 註冊)
-   Windows 7.0 或 Windows 8.1 (已加入網域時)

  對網域的條件存取只會將電腦聯結至新的 Exchange Online 專用環境中的租用戶。
-   Windows Phone 8 和更新版本
-   所有使用 Exchange ActiveSync (EAS) 電子郵件用戶端的 iOS 裝置
-   Android 4 及更新版本
-   若是使用**舊版 Exchange Online Dedicated 環境**的租用戶：    

  您必須使用 **Exchange Server 連接器**，將 Configuration Manager 連線到 Microsoft Exchange 內部部署。 這可讓您管理行動裝置和啟用條件存取 (請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md))。
-   若是使用**新 Exchange Online Dedicated 環境**的租用戶：     
  選擇性的 **Exchange Server 連接器**會將 Configuration Manager 連線至 Microsoft Exchange Online，並協助您管理裝置資訊 (請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md))。 您無須使用連接器，就能使用相容性原則或條件存取原則，但在執行報告必須使用，以協助您評估條件存取的影響。  

## <a name="requirements-for-exchange-on-premises"></a>Exchange 內部部署的需求
Exchange 內部部署的條件式存取支援：
-   Windows 8 及更新版本 (已向 Intune 註冊)
-   Windows Phone 8 和更新版本
-   iOS 上的原生電子郵件應用程式
-   Android 4 或更新版本上的原生電子郵件應用程式
-   不支援 Microsoft Outlook 應用程式 (Android 和 iOS)。

**此外**：

-  Exchange 版本必須是 Exchange 2010 或更新版本。 支援 Exchange 伺服器用戶端存取伺服器 (CAS) 陣列。

> [!TIP]
> 如果您的 Exchange 環境位在 CAS 伺服器設定中，則您必須將內部部署 Exchange Connector 設定為指向其中一個 CAS 伺服器。
- 您必須使用 **Exchange Server 連接器**，將 Configuration Manager 連線到 Microsoft Exchange 內部部署。 這可讓您管理行動裝置和啟用條件存取 (請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md))。
  - 請確定您是使用最新版的 **內部部署 Exchange Connector**。 內部部署 Exchange 連接器應透過 Configuration Manager 主控台加以設定。 如需詳細的逐步解說，請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。
  - 連接器必定只能在 System Center Configuration Manager 主要站台上加以設定。</li><li>此連接器支援 Exchange CAS 環境。 <br />        設定連接器時，您必須加以設定，使該連接器可與其中一個 Exchange CAS 伺服器聯繫。

- Exchange ActiveSync 可以設定成具有憑證型驗證或使用者認證項目


## <a name="requirements-for-skype-for-business-online"></a>商務用 Skype Online 的需求
SharePoint Online 條件式存取支援執行下列各項的裝置：
 -   iOS 7.1 和更新版本
 -   Android 4.0 及更新版本
 -   Samsung KNOX Standard 4.0 或更新版本

**此外**，您也必須為商務用 Skype Online 啟用新式驗證。 請填寫這份 [Connect 表單](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) ，以註冊加入新式驗證計畫。

您的所有使用者都必須使用商務用 Skype Online。 如果您的部署同時包含商務用 Skype Online 與商務用 Skype 內部部署，則條件式存取原則將不會套用至處於內部部署中的使用者。

## <a name="requirements-for-sharepoint-online"></a>SharePoint Online 的需求
SharePoint Online 條件式存取支援執行下列各項的裝置：
 -   Windows 8.1 及更新版本 (已向 Intune 註冊)
 -   Windows 7.0 或 Windows 8.1 (已加入網域時)
 -   Windows Phone 8.1 和更新版本
 -   iOS 7.1 和更新版本
 -   Android 4.0 和更新版本、Samsung KNOX Standard 4.0 和更新版本

 **此外**：
 -   裝置必須加入工作地點，以向 Azure Active Directory 裝置註冊服務 (AAD DRS) 註冊。

 聯結網域的電腦必須透過群組原則或 MSI 自動向 Azure Active Directory 註冊。 本主題中的 **電腦的條件存取** 一節將說明為電腦啟用條件存取的所有需求。

 Intune 和 Office 365 客戶將會自動啟用 AAD DRS。 已部署 ADFS 裝置註冊服務的客戶不會在其內部部署 Active Directory 中看到已註冊的裝置。
 -   需要 SharePoint Online 訂閱，且使用者必須具備 SharePoint Online 授權。

 ### <a name="conditional-access-for-pcs"></a>電腦的條件存取

 您可以針對執行 Office 桌面應用程式的電腦安裝條件存取，以便針對符合下列需求的電腦存取 **Exchange Online** 和 **SharePoint Online** ：
 -   電腦必須執行 Windows 7.0 或 Windows 8.1。
 -   這部電腦必須已聯結網域或與網域相容。

 為了相容，此電腦必須在 Intune 註冊，並與該原則相容。

 已加入網域的電腦必須設為向 Azure Active Directory [自動註冊裝置](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) 。
 -   [必須啟用 Office 365 的數據機驗證](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)，以及具有所有最新的 Office 更新。<br />     新式驗證將 Active Directory 驗證程式庫 (ADAL) 登入整合到 Office 2013 Windows 用戶端中，並啟用更佳的安全性，例如 **多因素驗證**和 **憑證式驗證**。
 -   設定 ADFS 宣告規則來封鎖非新式驗證通訊協定。  

## <a name="next-steps"></a>後續步驟  
 閱讀下列主題，以了解如何針對您的需要設定相容性原則及條件存取原則：  

-   [在 System Center Configuration Manager 中管理裝置相容性原則](../../protect/deploy-use/device-compliance-policies.md)  

-   [管理 System Center Configuration Manager 中的電子郵件存取](../../protect/deploy-use/manage-email-access.md)  

-   [在 System Center Configuration Manager 中管理 SharePoint Online 存取](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [管理商務用 Skype Online 存取](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>請參閱  

 [在 System Center Configuration Manager 中開始使用相容性設定](../../compliance/get-started/get-started-with-compliance-settings.md)
