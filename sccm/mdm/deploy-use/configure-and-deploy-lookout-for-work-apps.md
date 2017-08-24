---
title: "部署 Lookout for Work 应用 | Microsoft Docs"
description: "配置和部署 Lookout for Work 应用。"
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
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>配置和部署 Lookout for Work 应用

*适用范围：System Center Configuration Manager (Current Branch)*

本文介绍如何为 Android 和 iOS 设备配置和部署 Lookout for Work 应用。

## <a name="android-google-play-store-app"></a>Android（Google Play 商店应用）
1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用程序”。

2.  在“部署软件向导”的“常规”  页上，指定以下信息：
  * 类型：选择“Google Play 上的 Android 应用程序包”。
  * 位置：复制此处粘贴的来自 Google Play 商店的 Lookout for Work 应用链接
  * 发行者：Lookout Mobile Security
  * 名称：Lookout for Work
  * 描述：Lookout 提供针对移动威胁的最佳保护，维护设备安全。 Lookout 应用在设备上安装后，该应用可保护设备不受威胁，如发现任何威胁，将向你和你的公司管理员发出警报。
  * 管理类别：计算机管理

  成功完成后，便可在应用程序列表中看到 Lookout for Work 应用。

3.  在“主页”选项卡的“部署”组中，选择“部署”，以向用户部署 Lookout for Work 应用。
>[!IMPORTANT]
>必须选择在 Lookout MTP 控制台中添加到“注册管理”选项的相同用户。

  选择“必需的安装”选项以要求在用户设备上安装 Lookout 应用。

## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS（企业签名版 Lookout 应用）

* **步骤 1：**确保已在设备上设置 **iOS 管理**。 有关如何针对 iOS 管理设置设备的说明，请参阅[设置 iOS 和 Mac 设备管理]()。

* **步骤 2：****重新签名** Lookout for Work iOS 应用。 Lookout 在 iOS App Store 外分发其 Lookout for Work iOS 应用。 **分发应用前**，必须使用 iOS 企业开发者证书对应用重新签名。 有关对 Lookout for Work iOS 应用重新签名的详细说明，请参阅 Lookout 网站中的 [Lookout for Work iOS 应用重新签名过程](https://personal.support.lookout.com/hc/en-us/articles/114094038714)。


* **步骤 3：**通过执行以下操作对 iOS 用户启用 Azure Active Directory 身份验证：
  1.  登录到 [Azure Active Directory 管理门户](https://manage.windowsazure.com)，然后导航到应用程序页。
  2.  添加**Lookout for Work iOS 应用**作为**本机客户端应用程序**。
  ![显示本机客户端应用选项的添加应用对话框的屏幕截图](media/aad-add-app.png)

  3. 使用对 IPA 签名时选择的客户捆绑 ID 替换 **com.lookout.enterprise.yourcompanyname**。
  4.  添加其他重定向 URI：**&lt;companyportal://code/>**，后跟 URL 编码版本的原始重定向 URI。
  5.  向应用添加**委派权限**。

  有关详细信息，请参阅[配置本机客户端应用程序](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application)。


* **步骤 4：**按[在 System Center Configuration Manager 中创建 iOS 应用程序](https://docs.microsoft.com/en-us/sccm/apps/get-started/creating-ios-applications)主题中所述方法上传重新签名后的 .ipa 文件。 将最低操作系统版本设为 iOS 8.0 或更高版本。


* **步骤 5：**按[在 System Center Configuration Manager 中使用移动应用配置策略配置 iOS 应用](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies)主题中所述方法创建托管应用配置策略。


* **步骤 6：****若要向用户部署应用**，在“主页”选项卡的“应用程序”页中选择 Lookout for Work 应用，然后在“部署”组中，选择“部署”。

  必须选择在 Lookout 控制台中添加到“注册管理”选项的相同用户。  
选择“必需的安装”选项以要求在用户设备上安装 Lookout 应用。

## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>在设备上打开已部署的应用时，会发生什么情况




当用户在设备上打开 Lookout for Work 应用时，系统将提示他们激活应用，并选择使用 Azure Active Directory 选项进行登录。 可在以下主题中找到具有最终用户流的详细演练：

* [系统提示在 Android 设备上安装 Lookout for Work](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [需要解决 Lookout for Work 在 Android 设备上发现的威胁](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## <a name="next-steps"></a>后续步骤
* [启用合规性策略中的设备威胁防护规则](enable-device-threat-protection-rule-compliance-policy.md)
