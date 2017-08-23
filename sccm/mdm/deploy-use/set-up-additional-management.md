---
title: "使用 System Center Configuration Manager 設定其他管理 | Microsoft Docs"
description: "使用 System Center Configuration Manager 設定其他管理。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 947d2a85f2ac68c7ccaf9a1237fd60e89e7d1d10
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 設定其他管理

*適用對象：System Center Configuration Manager (最新分支)*

(選擇性) 註冊裝置之前，您可以設定額外的管理。 在註冊裝置之後，即可建立和部署這些管理解決方案，雖然許多組織都想要在管理裝置時部署裝置。

**設定項目**可讓您管理設定，例如，根據裝置平台，可能需要 PIN 或需要加密註冊裝置︰
- [Windows 10 和 Windows 8.1 裝置](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Windows Phone 裝置](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [iOS 和 Mac 裝置](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Android 和 Samsung KNOX Standard 裝置](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

**應用程式**可以部署至受管理裝置：
- [iOS 應用程式](creating-ios-applications.md)
- [Mac 應用程式](../../apps/get-started/creating-mac-computer-applications.md)
- [Windows PC 應用程式](../../apps/get-started/creating-windows-applications.md)
- [Windows Phone 應用程式](creating-windows-phone-applications.md)
- [Android 應用程式](creating-android-applications.md)

**條件式存取**可讓您管理對公司資源的存取，包含：  
- [電子郵件存取](manage-email-access.md)
- [SharePoint 存取](manage-sharepoint-online-access.md)
- [商務用 Skype 存取](manage-skype-for-business-online-access.md)
- [Dynamic CRM Online](manage-dynamics-crm-online-access.md)

**Multi-Factor Authentication (MFA)** 可讓您要求多個驗證方法，為使用者登入和交易增加重要的第二層安全性。
您之前會移至 Intune 主控台或 Configuration Manager 主控台，來設定用於 Intune 註冊的 MFA。 您現在將會使用 Intune 認證登入 [Microsoft Azure 入口網站](https://manage.windowsazure.com)，並透過 Azure AD 進行 MFA 設定。 若要深入了解，請參閱 [Microsoft Intune 的 Multi-Factor Authentication](https://aka.ms/mfa_ad)。

> [!div class="button"]
[< 上一個步驟](enable-platform-enrollment.md)  [下一個步驟 >](verify-mdm-configuration.md)
