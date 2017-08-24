---
title: "设置混合 MDM | Microsoft Docs"
description: "使用 Configuration Manager 和 Intune 设置混合设备注册。"
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
ms.openlocfilehash: c494fcc38955571c06507278a1ae88e5777b5708
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 设置混合移动设备管理 (MDM)

*适用范围：System Center Configuration Manager (Current Branch)*


必须先向 Intune 注册 iOS、Windows 和 Android 设备，然后才能使用 Configuration Manager 管理它们。 按照以下步骤可使用 Intune，通过 Configuration Manager 设置混合设备注册。 通过完成以下步骤，你会为用户启用“自带设备办公”(BYOD) 注册。 这些步骤也是[注册 BYOD设备](enroll-hybrid-ios-mac.md)和[注册公司拥有的设备](enroll-company-owned-devices.md)的先决条件。

 |步骤|详细信息|  
 |-----------|-------------|  
 |**步骤 1：**[创建 MDM 集合](create-mdm-collection.md)|创建 Configuration Manager 用户集合，其中的用户的设备可以进行注册|  
 |**步骤 2：**[域名要求](confirm-dns.md)|确认组织的域名服务 (DNS) 和 Active Directory 用户管理满足 MDM 要求|
 |**步骤 3：**[配置 Intune 订阅](configure-intune-subscription.md)|Intune 服务使你可以通过 Internet 管理设备。|  
 |**步骤 4：**[添加条款和条件](terms-and-conditions.md)| 创建用户必须同意才能使用公司门户应用的条款和条件|
 |**步骤 5：**[创建服务连接点](create-service-connection-point.md)|服务连接点将设置和软件部署信息发送到 Configuration Manager，并从移动设备中检索状态和清单消息。 |  
 |**步骤 6：**[启用平台注册](enable-platform-enrollment.md)|针对 iOS 和 Windows 设备的 MDM 注册需要执行附加步骤，以便在服务与设备之间进行通信。 Android 不需要附加配置。|  
 |**步骤 7：**[设置附加管理](set-up-additional-management.md)|（可选）为已注册的设备设置配置项目和条件访问|
 |**步骤 8：**[验证 MDM 配置](verify-mdm-configuration.md)|查看日志文件，以确认服务连接点已成功创建并且用户帐户在进行同步。|

需要 Intune 而不使用 Configuration Manager？
> [!div class="button"]
[查看 Intune 文档 >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>注册设备
完成混合部署后，可以在 Configuration Manager 中通过多种方式注册设备：
- **公司拥有的 (COD) 设备：**有关用于注册公司拥有的设备的不同平台特定方法的指导，请参阅[注册公司拥有的设备](enroll-company-owned-devices.md)。
- **用户拥有的 (BYOD) 设备：**有关注册用户拥有的设备的方法的指导，请参阅[注册用户拥有的 (BYOD) 设备](enroll-hybrid-ios-mac.md)。
