---
title: "注册公司拥有的设备 - Configuration Manager | Microsoft Docs"
description: "了解使用 Configuration Manager 注册公司拥有的设备以用于混合部署的不同方法。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
caps.latest.revision: "13"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: f0b503d8c9eba2dd1b6eb4c41ec40c001b727326
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>使用 Configuration Manager 注册公司拥有的设备以用于混合部署

*适用范围：System Center Configuration Manager (Current Branch)*

组织或公司拥有的设备 (COD) 可通过多种方法进行管理，具体取决于设备及其购买方式。  

## <a name="enroll-device-enrollment-program-ios-devices"></a>注册设备注册计划 iOS 设备  
 将“无线”注册配置文件部署到通过 Apple 设备注册计划购买的设备。 用户在设备上运行设置助理时，设备将在 Intune 中注册。  用户无法注销通过 DEP 注册的设备。 请参阅[使用 Configuration Manager 注册 iOS 设备注册计划 (DEP) 以进行混合部署](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md)。  

## <a name="enroll-ios-devices-with-apple-configurator"></a>使用 Apple Configurator 注册 iOS 设备  
 此方法要求管理员用 USB 将 iOS 设备连接到运行 Apple Configurator 的 Mac 计算机以预配置注册。 随后设备将交付给运行设置助理进程的用户，用户用其工作或学校凭据配置设备并完成注册进程。 请参阅[配合使用 Configuration Manager 和 Apple Configurator 进行的 iOS 混合注册](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)。  

## <a name="device-enrollment-manager"></a>设备注册管理器  
 组织可以使用 Intune 来管理大量带有单一用户帐户（名为注册管理器帐户）的移动设备。 创建设备注册管理器帐户之后，管理器可使用该帐户注册五个以上标准设备（普通用户默认允许注册五个标准设备）。 使用设备注册管理器注册设备仅适用于未被特定用户所用的设备。 例如，这些设备适用于销售点或实用程序应用，但不适用于需要访问电子邮件或公司资源的用户。 请参阅[使用 Configuration Manager 通过设备注册管理器注册设备](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md)。  

## <a name="user-affinity-for-managed-devices"></a>托管设备的用户关联  
 在配置公司拥有的设备的配置文件时，管理员可以指定托管设备是否可以支持“用户关联”（用于标识设备的特定用户）。 配置了“用户关联”的设备可以安装和运行公司门户应用，以下载应用和管理设备。 请参阅 [Configuration Manager 中混合托管设备的用户关联](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md)。  

## <a name="manage-devices-with-activation-lock"></a>使用激活锁定管理设备  
 Microsoft Intune 可以帮助管理 iOS 激活锁定，这是适用于 iOS 7.1 及更高版本设备的“查找我的 iPhone”应用的功能。 当设备上使用了“查到我的 iPhone”应用时，激活锁定自动启用。 请参阅[使用 System Center Configuration Manager 管理 iOS 激活锁定](../../mdm/deploy-use/manage-ios-activation-lock.md)。

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>预声明具有 IMEI 或 iOS 序列号的设备

可通过导入公司拥有设备的国际移动设备识别 (IMEI) 码或 iOS 序列号对此类设备进行识别。 可上传包含设备 IMEI 码的逗号分隔值 (.csv) 文件，或者手动输入设备信息。  请参阅[使用硬件 ID 号预声明设备](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md)。
