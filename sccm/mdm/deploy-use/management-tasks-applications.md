---
title: "在 System Center Configuration Manager 中管理應用程式 | Microsoft Docs"
description: "在 System Center Configuration Manager 中管理應用程式。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: bc7bb99bc526ed0bbaaad15fc9af39fa8b7c3893
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理應用程式

*適用於：System Center Configuration Manager (最新分支)*

當您透過 Microsoft Intune 或 Configuration Manager 內部部署裝置管理功能來管理裝置時，可以管理下列其他應用程式類型：
- Windows Phone 應用程式套件 (*.xap 檔案)
- iOS 應用程式套件 (*.ipa 檔案)
- Android 應用程式套件 (*.apk 檔案)
- Google Play 上的 Android 應用程式套件
- Windows Phone 應用程式套件 (在 Windows Phone 市集中)
- 透過 MDM 的 Windows Installer
- Web 應用程式

本節提供有關使用混合式 MDM 或內部部署 MDM 來建立及管理應用程式的詳細資訊。

[System Center Configuration Manager 應用程式的管理工作](../../apps/deploy-use/management-tasks-applications.md)提供更多有關管理 System Center Configuration Manager 應用程式與部署類型的一般資訊。

## <a name="deploying-and-monitoring-apps"></a>部署及監視應用程式

在 System Center Configuration Manager 中部署及監視應用程式的程序，和適用於站上裝置 (例如膝上型電腦和桌上型電腦) 的行動裝置相同。 您也可以閱讀下列主題，以取得部署及監視應用程式的一般資訊︰

- [在 System Center Configuration Manager 中部署應用程式](../../apps/deploy-use/deploy-applications.md)
- [在 System Center Configuration Manager 中監視應用程式](../../apps/deploy-use/monitor-applications-from-the-console.md)

以下是針對行動裝置管理，在部署及監視應用程式時要牢記在心的一些考量。

- MDM 註冊裝置不支援模擬部署、使用者體驗或排程設定。

- 如果您已經設定 iOS 應用程式設定原則，您可以將部署與該原則相關聯。 請參閱[使用應用程式設定原則設定 iOS 應用程式](configure-ios-apps-with-app-configuration-policies.md)。

### <a name="next-steps"></a>後續步驟

您最終可能會想要對應用程式做出變更、將應用程式解除安裝，或將已部署的應用程式取代為新的應用程式。 請參閱[使用 System Center Configuration Manager 更新及淘汰應用程式](../../apps/deploy-use/update-and-retire-applications.md)，以了解這些功能。
