---
title: "混合式行動裝置管理 (MDM) - Configuration Manager & Microsoft Intune | Microsoft Docs"
description: "了解搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM)。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: "34"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: e54478a03807c939ffa64ff39a21ef6f9ea4ae2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

*適用於：System Center Configuration Manager (最新分支)*


您可以使用 Configuration Manager 和 Microsoft Intune 管理 iOS、Windows 和 Android 裝置。 您可從 Configuration Manager 主控台來處理所有管理工作，並透過網際網路執行與 Microsoft Intune 線上服務緊密整合的其他管理工作。  您可以使用 Configuration Manager，讓使用者在其裝置上透過安全的受管理方式來存取公司資源。 使用裝置管理功能時，您可以保護公司資料，同時讓使用者能夠註冊其個人或公司擁有的裝置以便存取公司資料。 裝置管理功能：

-   淘汰或抹除裝置
-   設定包括密碼、安全性、漫遊、加密和無線通訊等相容性設定。
-   將商務營運 (LOB) 應用程式部署到裝置
-   將 App 部署到連線 Windows 市集、Windows Phone 市集、App Store 或 Google Play 的裝置。
-   收集硬體清查
-   使用內建報告來收集軟體清查

若要了解混合式 MDM 有哪些新功能，請參閱 [What's new in hybrid mobile device management](../understand/whats-new-in-hybrid-mobile-device-management.md) (混合式行動裝置管理的新功能)。

本文件假設您使用 Configuration Manager 來管理電腦，且有意搭配 Intune 來擴充 Configuration Manager 主控台以管理行動裝置。 若要了解 Intune 和混合式行動裝置管理之間的差異，請參閱 [Choose between Microsoft Intune standalone and hybrid mobile device management with System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md) (在搭配 System Center Configuration Manager 使用 Microsoft Intune 獨立或混合式行動裝置管理之間進行選擇)。

在使用 Intune 來擴充 Configuration Manager 之後，您即可註冊並管理公司擁有的裝置，或賦予使用者註冊其個人裝置的權限。 您也可以使用 Configuration Manager，搭配 Intune 來管理公司擁有的裝置。

## <a name="hybrid-mdm-enrollment"></a>混合式 MDM 註冊
若要對裝置採取混合式管理，您必須為這些裝置註冊服務。 透過裝置來進行裝置註冊的方式，取決於裝置類型、擁有權和所需的管理層級。
- 「自備裝置」(BYOD) 註冊方式可讓使用者註冊其個人電話、平板電腦或電腦。
- 公司擁有的裝置 (CYOD) 註冊方式可啟用遠端抹除、共用裝置或裝置使用者親和性這類管理案例。
- 如果您使用 [Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager) (不論內部部署或裝載在雲端中)，即可啟用簡單的 Intune 管理功能，而不需要註冊。 您也可以使用 [Intune 用戶端軟體](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune)來管理 Windows 電腦。
