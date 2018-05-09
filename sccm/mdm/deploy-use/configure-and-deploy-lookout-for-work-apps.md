---
title: 为工作应用部署 Lookout
titleSuffix: Configuration Manager
description: 配置和部署 Lookout for Work 应用。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a812ed059bc0d96c23af986c2051416c26f6a15a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>配置和部署 Lookout for Work 应用

*适用范围：System Center Configuration Manager (Current Branch)*

本文介绍如何为 Android 和 iOS 设备配置和部署 Lookout for Work 应用。

## <a name="android-google-play-store-app"></a>Android（Google Play 商店应用）
1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用程序”。

2.  在“部署软件向导”的“常规”  页上，指定以下信息：  
    - 类型：选择“Google Play 上的 Android 应用程序包”。
    - 位置：复制此处粘贴的来自 Google Play 商店的 Lookout for Work 应用链接
    - 发行者：Lookout Mobile Security
    - 名称：Lookout for Work
    - 描述：Lookout 提供针对移动威胁的最佳保护，维护设备安全。 安装 Lookout 应用后，此应用可保护设备免受威胁的侵害。 它在找到威胁时会向你和你的 IT 管理员发送警报。
    - 管理类别：计算机管理  

    成功完成后，即可在应用程序列表中看到 Lookout for Work 应用。

3.  在“主页”选项卡的“部署”组中，选择“部署”，以向用户部署 Lookout for Work 应用。   
    >[!IMPORTANT]  
    >必须选择在 Lookout MTP 控制台中添加到“注册管理”选项的相同用户。  

    选择“必需安装”选项。 此选项要求在用户的设备上安装 Lookout 应用。  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS（Lookout 应用的企业签名版）

- **步骤 1：**确保已在设备上设置 **iOS 管理**。 若要了解如何针对 iOS 管理设置设备，请参阅[设置 iOS 和 Mac 设备管理](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)。

- **步骤 2：****重新签名** Lookout for Work iOS 应用。 Lookout 在 iOS App Store 外分发其 Lookout for Work iOS 应用。 **分发应用前**，必须使用 iOS 企业开发者证书对应用重新签名。 有关对 Lookout for Work iOS 应用重新签名的详细说明，请参阅 Lookout 网站中的 [Lookout for Work iOS 应用重新签名过程](https://personal.support.lookout.com/hc/articles/114094038714)。


- 步骤 3：通过执行以下操作对 iOS 用户启用 Azure Active Directory 身份验证：
  1.  登录 [Azure Active Directory 管理门户](https:/portal.azure.com)，然后导航到应用程序页。
  2.  添加**Lookout for Work iOS 应用**作为**本机客户端应用程序**。
  ![显示本机客户端应用选项的添加应用对话框的屏幕截图](media/aad-add-app.png)

  3. 使用对 IPA 签名时选择的客户捆绑 ID 替换 **com.lookout.enterprise.yourcompanyname**。
  4.  添加其他重定向 URI：**&lt;companyportal://code/>**，后跟 URL 编码版本的原始重定向 URI。
  5.  向应用添加**委派权限**。

  有关详细信息，请参阅[配置本机客户端应用程序](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application)。


- **步骤 4：**按[在 System Center Configuration Manager 中创建 iOS 应用程序](/sccm/apps/get-started/creating-ios-applications)主题中所述方法上传重新签名后的 .ipa 文件。 将最低操作系统版本设为 iOS 8.0 或更高版本。


- **步骤 5：**按[在 System Center Configuration Manager 中使用移动应用配置策略配置 iOS 应用](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies)主题中所述方法创建托管应用配置策略。


- 步骤 6：若要向用户部署应用，请在“主页”选项卡的“应用程序”页中选择 Lookout for Work 应用，然后在“部署”组中，选择“部署”。

  选择在 Lookout 控制台中添加到“注册管理”选项的用户。 选择“必需安装”选项。 此选项要求在用户的设备上安装 Lookout 应用。



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>在设备上打开已部署的应用时，会发生什么情况

当用户在设备上打开 Lookout for Work 时，系统将提示他们激活应用。 用户应选择通过 Azure Active Directory 选项登录。 请参阅以下文章，了解有关最终用户流程的详细演练：

- [系统提示在 Android 设备上安装 Lookout for Work](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [需要解决 Lookout for Work 在 Android 设备上发现的威胁](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>后续步骤
- [启用合规性策略中的设备威胁防护规则](enable-device-threat-protection-rule-compliance-policy.md)
