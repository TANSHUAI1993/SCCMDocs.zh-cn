---
title: "部署 Lookout for Work 應用程式 | Microsoft Docs"
description: "設定和部署 Lookout for Work 應用程式。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 59f43c922d1d3bc64625733014b0def1e42c4d2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>設定和部署 Lookout for Work 應用程式

*適用於：System Center Configuration Manager (最新分支)*

本文說明如何為 Android 和 iOS 裝置設定和部署 Lookout for Work 應用程式。

## <a name="android-google-play-store-app"></a>Android (Google Play 商店應用程式)
1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] > [應用程式管理] > [應用程式]。

2.  在 [部署軟體精靈] 的 [一般]  頁面上，指定下列資訊：
  * 類型：選取 [Google Play 上的 Android 應用程式套件]。
  * 位置︰從 Google Play 商店複製 Lookout for Work 應用程式連結並貼到這裡
  * 發行者︰Lookout Mobile Security
  * 名稱：Lookout for Work
  * 描述：Lookout 提供對抗行動威脅的最佳保護，維持您裝置的安全。 在裝置上安裝 Lookout 應用程式後，該應用程式會保護您的裝置免於威脅，並在找到任何威脅時，發出警示給您及您公司的系統管理員。
  * 系統管理類別︰電腦管理

  成功完成時，您現在會在應用程式清單中看到 Lookout for Work 應用程式。

3.  在 [首頁] 索引標籤的 [部署] 群組中，選擇 [部署] 將 Lookout for Work 應用程式部署給使用者。
>[!IMPORTANT]
>您必須選取新增至 Lookout MTP 主控台中 [註冊管理] 選項的相同使用者。

  選擇 [必要安裝] 選項，要求必須在使用者的裝置上安裝 Lookout 應用程式。

## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (Lookout 應用程式的企業簽署版本)

* **步驟 1：**確定您的裝置上已設定 **iOS 管理**。 如需如何設定裝置以進行 iOS 管理的指示，請參閱[設定 iOS 和 Mac 裝置管理]()。

* **步驟 2：** **重新簽署** Lookout for Work iOS 應用程式。 Lookout 會在 iOS App Store 外部發佈其 Lookout for Work iOS 應用程式。 **發佈應用程式之前**，您必須使用 iOS 企業開發人員憑證重新簽署應用程式。 如需重新簽署 Lookout for Work iOS 應用程式的詳細指示，請參閱 Lookout 網站上的 [Lookout for Work iOS 應用程式重新簽署程序](https://personal.support.lookout.com/hc/en-us/articles/114094038714)。


* **步驟 3：**執行下列動作為 iOS 使用者啟用 Azure Active Directory 驗證：
  1.  登入 [Azure Active Directory 管理入口網站](https://manage.windowsazure.com)，並瀏覽至應用程式頁面。
  2.  新增 **Lookout for Work iOS 應用程式**作為**原生用戶端應用程式**。
  ![顯示 [原生用戶端應用程式] 選項的 [新增應用程式] 對話方塊螢幕擷取畫面](media/aad-add-app.png)

  3. 以您簽署 IPA 時所選取的客戶配套識別碼取代 **com.lookout.enterprise.yourcompanyname**。
  4.  新增其他重新導向 URI：**&lt;公司入口網站 ://code/>**，後面接著原始重新導向 URI 的 URL 編碼版本。
  5.  新增**委派的權限**至您的應用程式。

  如需詳細資訊，請參閱[設定原生用戶端應用程式](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application)。


* **步驟 4：**如[使用 System Center Configuration Manager 建立 iOS 應用程式](https://docs.microsoft.com/en-us/sccm/apps/get-started/creating-ios-applications)主題中所述，上傳重新簽署的 .ipa 檔案。 將最低作業系統版本設定為 iOS 8.0 或更新版本。


* **步驟 5：**如[在 System Center Configuration Manager 中使用行動應用程式設定原則設定 iOS 應用程式](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies)主題中所述，建立受管理的應用程式設定原則。


* **步驟 6：****若要將應用程式部署給使用者**，請在 [應用程式] 頁面中選取 Lookout for Work 應用程式，然後從 [首頁] 索引標籤的 [部署] 群組選擇 [部署]。

  您必須選取新增至 Lookout 主控台中 [註冊管理] 選項的相同使用者。  
選擇 [必要安裝] 選項，要求必須在使用者的裝置上安裝 Lookout 應用程式。

## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>在裝置上開啟已部署的應用程式時，會發生什麼事




當使用者在裝置上開啟 Lookout for Work 時，系統會提示他們啟用應用程式，並選擇 [使用 Azure Active Directory 登入] 選項。 您可以在下列主題中找到使用者流程的詳細逐步解說：

* [系統提示您在 Android 裝置上安裝 Lookout for Work](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [您必須解決 Lookout for Work 在 Android 裝置上找到的威脅](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## <a name="next-steps"></a>後續步驟
* [啟用合規性政策中的裝置威脅保護規則](enable-device-threat-protection-rule-compliance-policy.md)
