---
title: "混合 MDM 的设备注册方法 | Microsoft Docs"
description: "混合 MDM 的设备注册方法。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: e09e639e939b846cdc162681f9d7bd4c39cd6fbf
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="overview-of-device-enrollment-methods"></a>设备注册方法概述

*适用范围：System Center Configuration Manager (Current Branch)*

使用 Intune 扩展 Configuration Manager 后，可注册和管理公司拥有的设备或授予用户注册其个人设备的权限。 还可以使用 Configuration Manager 通过 Intune 管理公司拥有的设备。

下表显示了注册方法及其支持的功能。 这些功能包括：
- **擦除** - 恢复设备的出厂设置，删除所有数据。 [停用设备](../deploy-use/wipe-lock-reset-devices.md)
- **相关性** - 将设备与用户相关联。 需要移动应用程序管理 (MAM) 和对公司数据的条件性访问。 [用户关联](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **锁定** - 防止用户从管理中移除设备。 iOS 设备的锁定需要为受监督模式。 [远程锁定](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**iOS 注册方法**

| **方法** |  **擦除** |  **相关性**    |   **锁定** | **详细信息** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | 否|    是 |   否 | [更多](../deploy-use/enable-platform-enrollment.md)|
|**[DEM](#dem)**|   否 |否 |否  | [更多](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   是 |   可选 |  可选|[更多](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| 是 |   可选 |  否| [更多](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Windows 和 Android 的注册方法**

| **方法** |  **擦除** |  **相关性**    |   **锁定** | **详细信息**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | 否|    是 |   否 | [更多](../deploy-use/enroll-hybrid-windows.md)|
|**[DEM](#dem)**|   否 |否 |否  |[更多](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

关于可帮助用户找到正确方法的一系列问题，请参阅[选择如何注册设备](/intune/get-started/choose-how-to-enroll-devices1)。

## <a name="byod"></a>BYOD
“自带设备办公” (BYOD) 用户可安装公司门户应用并注册其设备。 这可以让用户连接到公司网络，加入域或 Azure Active Directory。 对于大多数平台，许多 COD 方案的先决条件之一都是要求启用 BYOD 注册。 请参阅[安装混合 MDM](../deploy-use/setup-hybrid-mdm.md)。 （[返回到表格](#overview-of-device-enrollment-methods)）

## <a name="corporate-owned-devices"></a>公司拥有的设备
可通过 Configuration Manager 控制台管理公司拥有的设备 (COD)。 可直接通过 Apple 提供的工具注册 iOS 设备。 管理员或主管可使用设备注册管理器注册所有设备类型。 还可识别具有 IMEI 号码的设备并将其标记为“公司拥有”来启用 COD 方案。

[注册公司拥有的设备](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
设备注册管理器是用来注册和管理多个公司拥有的设备的特殊用户帐户。 此管理器可以安装公司门户和注册多个无用户设备。 详细了解 [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md)。 （[返回到表格](#overview-of-device-enrollment-methods)）

### <a name="dep"></a>DEP
Apple 设备注册计划 (DEP) 管理允许用户创建“无线”策略并将其部署到通过 DEP 购买和管理的 iOS 设备。 设备将在用户第一次打开设备并运行 iOS 设置助理时注册。 此方法支持“iOS 受监督”模式，该模式反过来可启用：
  - 锁定的注册
  - 条件性访问
  - 破解检测
  - 移动应用程序管理

详细了解 [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md)。 （[返回到表格](#overview-of-device-enrollment-methods)）

### <a name="usb-sa"></a>USB-SA
通过 USB 连接的“设置助理注册”。 管理员创建策略并将其导出到 Apple Configurator。 使用策略准备好通过 USB 连接的公司拥有的设备。 管理员必须手动注册每个设备。 用户收到其设备并运行设置助理，便可注册其设备。 此方法支持“iOS 受监督”模式，该模式反过来可启用：
  - 条件性访问
  - 破解检测
  - 移动应用程序管理

详细了解[使用 Apple Configurator 进行设置助理注册](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)。 （[返回到表格](#overview-of-device-enrollment-methods)）

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>使用 Exchange ActiveSync 和 Configuration Manager 管理移动设备
可以使用 EAS MDM 策略通过 Intune 管理未注册但连接到 Exchange ActiveSync (EAS) 的移动设备。 Intune 使用 Exchange Connector 与本地或云托管的 EAS 通信。

[使用 Exchange ActiveSync 和 Intune 管理移动设备](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
