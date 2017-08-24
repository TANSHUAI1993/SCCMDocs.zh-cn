---
title: "在 System Center Configuration Manager 中管理应用程序 | Microsoft Docs"
description: "在 System Center Configuration Manager 中管理应用程序。"
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
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

通过 Microsoft Intune 或 Configuration Manager 在本地设备管理中管理设备时，还可以管理以下应用程序类型：
- Windows Phone 应用包（*.xap 文件）
- iOS 应用包（*.ipa 文件）
- Android 应用包（*.apk 文件）
- “Google Play 上的 Android 应用包”
- Windows Phone 应用包（在 Windows Phone 应用商店中）
- 通过 MDM 的 Windows 安装程序
- Web 应用程序

本部分详细介绍使用混合 MDM 或本地 MDM 创建和管理应用程序。

[System Center Configuration Manager 应用程序的管理任务](../../apps/deploy-use/management-tasks-applications.md)提供有关管理 System Center Configuration Manager 应用程序和部署类型的其他常规信息。

## <a name="deploying-and-monitoring-apps"></a>部署和监视应用

在 System Center Configuration Manager 中部署和监视应用程序对移动设备和现场设备（如笔记本电脑和台式机）是一样的过程。 可以阅读以下主题，了解有关部署和监视应用程序的一般信息：

- [在 System Center Configuration Manager 中部署应用程序](../../apps/deploy-use/deploy-applications.md)
- [在 System Center Configuration Manager 中监视应用程序](../../apps/deploy-use/monitor-applications-from-the-console.md)

以下是特定于移动设备管理的部署和监视应用程序时需要牢记的一些注意事项。

- 已注册 MDM 的设备不支持模拟部署、用户体验或计划设置。

- 可以将该部署与 iOS 应用配置策略（如果已配置）相关联。 请参阅[使用应用配置策略配置 iOS 应用](configure-ios-apps-with-app-configuration-policies.md)。

### <a name="next-steps"></a>后续步骤

最后，建议更改、卸载应用程序，或者将已部署的应用程序替换为新的应用程序。 请参阅[使用 System Center Configuration Manager 更新和停用应用程序](../../apps/deploy-use/update-and-retire-applications.md)以了解这些功能。
