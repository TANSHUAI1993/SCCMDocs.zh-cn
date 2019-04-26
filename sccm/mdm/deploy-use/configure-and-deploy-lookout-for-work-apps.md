---
title: 为工作应用部署 Lookout
titleSuffix: Configuration Manager
description: 配置和部署 Lookout for Work 应用。
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4e829d92b099be3fbf77796ea604d9d33db252c
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62273637"
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>配置和部署 Lookout for Work 应用

适用范围：System Center Configuration Manager (Current Branch)

本文介绍如何为 Android 和 iOS 设备配置和部署 Lookout for Work 应用。



## <a name="android-google-play-store-app"></a>Android（Google Play 商店应用）
1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用程序”。  

2.  在“部署软件向导”的“常规”  页上，指定以下信息：  
    - 类型：选择“Google Play 上的 Android 应用程序包”。
    - 位置：复制此处粘贴的来自 Google Play 商店的 Lookout for Work 应用链接
    - 发布者：Lookout Mobile Security
    - 名称：Lookout for Work
    - 描述:Lookout 提供针对移动威胁保护你的设备的安全的最佳保护。 安装 Lookout 应用后，此应用可保护设备免受威胁的侵害。 它在找到威胁时会向你和你的 IT 管理员发送警报。
    - 管理类别：计算机管理  

    成功完成后，即可在应用程序列表中看到 Lookout for Work 应用。  

3.  在“主页”选项卡的“部署”组中，选择“部署”，以向用户部署 Lookout for Work 应用。   
    >[!IMPORTANT]  
    >必须选择在 Lookout MTP 控制台中添加到“注册管理”选项的相同用户。  

    选择“必需安装”选项。 此选项要求在用户的设备上安装 Lookout 应用。  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS（Lookout 应用的企业签名版）

1. 请确保已在设备上设置 iOS 管理。 若要了解如何设置设备进行 iOS 管理，请参阅[设置 iOS 和 Mac 设备管理](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)。  

2. 重新签名 Lookout for Work iOS 应用。 Lookout 在 iOS App Store 外分发其 Lookout for Work iOS 应用。 分发应用前，必须使用 iOS 企业开发者证书对应用重新签名。 有关对 Lookout for Work iOS 应用重新签名的详细说明，请参阅 Lookout 网站中的 [Lookout for Work iOS 应用重新签名过程](https://personal.support.lookout.com/hc/articles/114094038714)。  

3. 为 iOS 用户启用 Azure Active Directory (Azure AD) 身份验证。
   1.  登录到 [Azure 门户的 Azure AD 边栏选项卡](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)，再导航到应用注册页面。  
   2.  将名称指定为“Lookout for Work iOS 应用”，并选择“本机”作为应用程序类型。  
   ![显示本机客户端应用选项的添加应用对话框的屏幕截图](media/aad-add-app-reg.png)

   3.  请使用以下格式的重定向 URI：`lookoutwork://com.lookout.enterprise.<yourcompanyname>`，将 `<yourcompanyname>` 替换为你的公司名称。 例如：`lookoutwork://com.lookout.enterprise.contoso`
   4. 单击“创建”以创建应用。 
   5.  打开新应用、单击“设置”，再添加其他重定向 URI。 使用格式 `companyportal://code/<originalURI>`，其中 `<originalURI>` 是原始重定向 URI 的 URL 编码版本。 例如 `companyportal://code/lookoutwork%3A%2F%2Fcom.lookout.enterprise.contoso`
   6.  在应用设置中转到“所需权限”并单击“添加”。 选择以下委托的权限：  

       | API  | 权限  |
       |---------|---------|
       | Lookout MTP     | 访问 Lookout MTP         |
       | Microsoft Graph     | 登录和读取用户配置文件        |  

   有关详细信息，请参阅[配置本机客户端应用程序](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application)。  


4. 在 Configuration Manager 中上传重新签名的 .ipa 文件。 将最低操作系统版本设为 iOS 8.0 或更高版本。 有关详细信息，请参阅[创建 iOS 应用程序](/sccm/apps/get-started/creating-ios-applications)。   


5. 创建托管应用配置策略。 有关详细信息，请参阅[使用移动应用配置策略配置 iOS 应用](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies)。  


6. 向用户部署 Lookout for Work 应用。 有关详细信息，请参阅[部署应用程序](/sccm/apps/deploy-use/deploy-applications)。  

   选择在 Lookout 控制台中添加到“注册管理”选项的用户。 选择“必需安装”选项。 此选项要求在用户的设备上安装 Lookout 应用。



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>在设备上打开已部署的应用时，会发生什么情况

当用户在设备上打开 Lookout for Work 时，系统将提示他们激活应用。 用户应选择通过 Azure AD 选项登录。 请参阅以下文章，了解有关最终用户流程的详细演练：

- [系统提示在 Android 设备上安装 Lookout for Work](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [需要解决 Lookout for Work 在 Android 设备上发现的威胁](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>后续步骤
- [启用合规性策略中的设备威胁防护规则](enable-device-threat-protection-rule-compliance-policy.md)
