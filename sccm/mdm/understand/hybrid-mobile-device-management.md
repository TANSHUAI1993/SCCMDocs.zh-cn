---
title: "混合移动设备管理 (MDM) - Configuration Manager 和 Microsoft Intune | Microsoft Docs"
description: "了解使用 System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)。"
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
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)

*适用范围：System Center Configuration Manager (Current Branch)*


可使用 Configuration Manager 和 Microsoft Intune 管理 iOS、Windows 和 Android 设备。 可通过 Configuration Manager 控制台处理所有管理任务，还可处理通过 Internet 与 Microsoft Intune 联机服务无缝集成的其余管理任务。  可借助 Configuration Manager 允许用户以安全的托管方式访问其设备上的公司资源。 通过使用设备管理，你可以保护公司数据，同时允许用户注册其个人设备或公司拥有的设备，以访问公司数据。 设备上的管理功能：

-   停用和擦除设备
-   配置密码、安全性、漫游、加密和无线通信等符合性设置
-   将业务线 (LOB) 应用部署到设备
-   将应用部署到连接到 Windows 应用商店、Windows Phone 应用商店、应用商店或 Google Play 的设备
-   收集硬件清单
-   使用内置报表收集软件清单

若要阅读有关哪些新功能可用于混合 MDM 的信息，请参阅[混合移动设备管理中的新增功能](../understand/whats-new-in-hybrid-mobile-device-management.md)。

本文假设你正在使用 Configuration Manager 管理计算机，并且对使用 Intune 扩展 Configuration Manager 控制台来管理移动设备感兴趣。 若要了解 Intune 和混合移动设备管理之间的差异，请参阅[在 Microsoft Intune 独立版和使用 System Center Configuration Manager 的混合移动设备管理之间选择](choose-between-standalone-intune-and-hybrid-mobile-device-management.md)。

使用 Intune 扩展 Configuration Manager 后，可注册和管理公司拥有的设备或授予用户注册其个人设备的权限。 还可以使用 Configuration Manager 通过 Intune 管理公司拥有的设备。

## <a name="hybrid-mdm-enrollment"></a>混合 MDM 注册
若要对设备进行混合管理，设备必须向该服务注册。 设备的注册方式取决于设备类型、所有权和所需的管理级别。
- “自带设备办公”(BYOD) 注册允许用户注册其个人电话、平板电脑或电脑。
- 公司拥有的设备 (COD) 注册启用管理方案，如远程擦除、共享的设备或设备的用户关联。
- 如果使用本地或在云中托管的 [Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager)，则无需注册即可启用简单的 Intune 管理。 还可使用 [Intune 客户端软件](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune)管理 Windows 电脑。
