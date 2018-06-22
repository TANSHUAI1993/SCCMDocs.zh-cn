---
title: 设置附加管理
titleSuffix: Configuration Manager
description: 使用 System Center Configuration Manager 设置其他管理。
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a61dffbdd9b04d3e872e23f88ddc0ac864f99d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346339"
---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 设置其他管理

*适用范围：System Center Configuration Manager (Current Branch)*

（可选）注册设备之前，可以设置附加管理。 可以注册设备之后创建并部署这些管理解决方案，不过许多组织更希望在将设备纳入管理时部署它们。

通过**配置项目**可以基于设备平台在注册的设备上管理设置（如要求 PIN 或要求加密）：
- [Windows 10 和 Windows 8.1 设备](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Windows Phone 设备](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [iOS 和 Mac 设备](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Android 和 Samsung KNOX Standard 设备](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

**应用程序**可以部署到托管设备：
- [iOS 应用程序](creating-ios-applications.md)
- [Mac 应用程序](../../apps/get-started/creating-mac-computer-applications.md)
- [Windows 电脑应用程序](../../apps/get-started/creating-windows-applications.md)
- [Windows Phone 应用程序](creating-windows-phone-applications.md)
- [Android 应用程序](creating-android-applications.md)

通过**条件访问**可以管理对公司资源的访问，包括：  
- [电子邮件访问](manage-email-access.md)
- [SharePoint 访问](manage-sharepoint-online-access.md)
- [Skype for Business 访问](manage-skype-for-business-online-access.md)
- [Dynamic CRM Online](manage-dynamics-crm-online-access.md)

**多重身份验证 (MFA)** 需要使用多个验证方法，为用户登录和事务额外提供一层重要的安全保障。
以前，你会转到 Intune 控制台或 Configuration Manager 控制台，以设置 MFA 用于 Intune 注册。 现在可使用 Intune凭据登录 [Microsoft Azure 门户](https://manage.windowsazure.com)，并通过 Azure AD 配置 MFA 设置。 若要了解详细信息，请参阅 [Microsoft Intune 的多重身份验证](https://aka.ms/mfa_ad)。

> [!div class="button"]
[< 上一步](enable-platform-enrollment.md)  [下一步 >](verify-mdm-configuration.md)
