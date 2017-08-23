---
title: "使用 System Center Configuration Manager 啟用平台註冊 | Microsoft Docs"
description: "使用 System Center Configuration Manager 和 Microsoft Intune 啟用平台註冊。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9163b77-a67d-4139-8272-bb1dfdb8707c
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4b047aa752b638aeeb7dd363a66564800d00a8df
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="enable-platform-enrollment-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 啟用平台註冊

*適用於：System Center Configuration Manager (最新分支)*

不同的裝置平台需要額外的設定，才能啟用裝置註冊。
  - [iOS 和 Mac 註冊設定](enroll-hybrid-ios-mac.md)：取得 Apple MDM Push 憑證

  - [Windows 註冊設定](enroll-hybrid-windows.md)︰設定 DNS，並啟用 Windows 電腦、Windows 10 行動裝置版和 Windows Phone 裝置的註冊

  - [Android](enroll-hybrid-android.md)：Android 裝置不需要任何額外的步驟即可啟用註冊

啟用 MDM 管理之後，即可指定每位使用者可以註冊的裝置數目，每位使用者最多 15 個裝置。
