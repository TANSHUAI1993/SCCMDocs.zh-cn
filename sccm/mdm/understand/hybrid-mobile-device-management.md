---
title: Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune
description: "了解使用 System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 22e673122f0f664d1240c11451b7e6db78481b26
ms.openlocfilehash: 83832465e93997a2893e024c565ee00f471036d1

---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

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
若要对设备进行混合管理，设备必须向该服务注册。 设备的注册方式取决于设备类型、所有权和所需的管理级别。 “自带设备办公”(BYOD) 注册允许用户注册其个人电话、平板电脑或电脑。 公司拥有的设备 (COD) 注册启用管理方案，如远程擦除、共享的设备或设备的用户关联。

 如果使用本地或在云中托管的 [Exchange ActiveSync](#mobile-device-management-with-exchange-activesync-and-configuration-manager)，则无需注册即可启用简单的 Intune 管理。 还可使用 [Intune 客户端软件](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune)管理 Windows 电脑。

## <a name="overview-of-device-enrollment-methods"></a>设备注册方法概述

 下表显示了注册方法及其支持的功能。 这些功能包括：
 - **擦除** - 恢复设备的出厂设置，删除所有数据。 [停用设备](../deploy-use/wipe-lock-reset-devices.md)
 - **相关性** - 将设备与用户相关联。 需要移动应用程序管理 (MAM) 和对公司数据的条件性访问。 [用户关联](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
 - **锁定** - 防止用户从管理中移除设备。 iOS 设备的锁定需要为受监督模式。 [远程锁定](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

 **iOS 注册方法**

| **方法** |  **擦除** |  **相关性**    |   **锁定** | **详细信息** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | 否|    是 |   否 | [更多](../deploy-use/setup-hybrid-mdm.md#step-6-enable-platform-enrollment)|
|**[DEM](#dem)**|   否 |否 |否  | [更多](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   是 |   可选 |  可选|[更多](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| 是 |   可选 |  否| [更多](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Windows 和 Android 的注册方法**

| **方法** |  **擦除** |  **相关性**    |   **锁定** | **详细信息**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | 否|    是 |   否 | [更多](../deploy-use/setup-hybrid-mdm.md#set-up-device-management)|
|**[DEM](#dem)**|   否 |否 |否  |[更多](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

关于可帮助用户找到正确方法的一系列问题，请参阅[选择如何注册设备](/intune/get-started/choose-how-to-enroll-devices1)。

## <a name="byod"></a>BYOD
“自带设备办公”用户可安装公司门户应用并注册其设备。 这可以让用户连接到公司网络，加入域或 Azure Active Directory。 对于大多数平台，许多 COD 方案的先决条件之一都是要求启用 BYOD 注册。 请参阅[安装混合 MDM](../deploy-use/setup-hybrid-mdm.md)。 （[返回到表格](#overview-of-device-enrollment-methods)）

## <a name="corporate-owned-devices"></a>公司拥有的设备
可通过 Configuration Manager 控制台管理公司拥有的设备 (COD)。 可直接通过 Apple 提供的工具注册 iOS 设备。 管理员或主管可使用设备注册管理器注册所有设备类型。 还可识别具有 IMEI 号码的设备并将其标记为“公司拥有”来启用 COD 方案。

[注册公司拥有的设备](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
设备注册管理器是用来注册和管理多个公司拥有的设备的特殊用户帐户。 此管理器可以安装公司门户和注册多个无用户设备。 详细了解 [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md)。 （[返回到表格](#overview-of-device-enrollment-methods)）

### <a name="dep"></a>DEP
Apple 设备注册计划 (DEP) 管理允许用户创建“无线”策略并将其部署到通过 DEP 购买和管理的 iOS 设备。 设备将在用户第一次打开设备并运行 iOS 设置助理时注册。 此方法支持“iOS 受监督”模式，该模式反过来可启用：
   -    锁定的注册
   -    条件性访问
   -    破解检测
   -    移动应用程序管理

详细了解 [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md)。 （[返回到表格](#overview-of-device-enrollment-methods)）

### <a name="usb-sa"></a>USB-SA
通过 USB 连接的“设置助理注册”。 管理员创建策略并将其导出到 Apple Configurator。 使用策略准备好通过 USB 连接的公司拥有的设备。 管理员必须手动注册每个设备。 用户收到其设备并运行设置助理，便可注册其设备。 此方法支持“iOS 受监督”模式，该模式反过来可启用：
   -    条件性访问
   -    破解检测
   -    移动应用程序管理

详细了解[使用 Apple Configurator 进行设置助理注册](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)。 （[返回到表格](#overview-of-device-enrollment-methods)）

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>使用 Exchange ActiveSync 和 Configuration Manager 管理移动设备
可以使用 EAS MDM 策略通过 Intune 管理未注册但连接到 Exchange ActiveSync (EAS) 的移动设备。 Intune 使用 Exchange Connector 与本地或云托管的 EAS 通信。

[使用 Exchange ActiveSync 和 Intune 管理移动设备](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)


##  <a name="supported-device-platforms"></a>受支持的设备平台

Configuration Manager 混合 MDM 可以管理以下设备平台：

[!INCLUDE[../includes/mdm-supported-devices](../includes/mdm-supported-devices.md)]

## <a name="next-steps"></a>后续步骤
 - [设备注册的先决条件](../deploy-use/setup-hybrid-mdm.md)
 - [管理公司拥有的设备](../deploy-use/enroll-company-owned-devices.md)



<!--HONumber=Nov16_HO1-->


