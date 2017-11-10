---
title: "注册用户拥有的设备以用于混合部署"
titleSuffix: Configuration Manager
description: "了解使用 Configuration Manager 注册用户拥有的设备以用于混合部署的不同方法。"
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
caps.latest.revision: "13"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9bc0e23680ff2c7a5099938e546e50e03f998f5e
ms.sourcegitcommit: 1132886e07d0c0a87dcc7eeef4577dd8d8840023
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2017
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>使用 Configuration Manager 注册用户拥有的设备以用于混合部署

*适用范围：System Center Configuration Manager (Current Branch)*

注册用户拥有的设备以便管理，通常将这一过程称为“携带自己的设备”，简称“BYOD”。 用户实现此过程的方式如下：在设备（iOS、macOS 和 Android）上安装公司门户应用并登录，或向设备添加工作或学校帐户并加入域 (Windows)。 此过程向 Intune 注册设备，授予用户访问 Intune 所托管的资源的权限，并使 Intune 管理某些设备设置，如要求 PIN 等。

要将设备纳入管理，作为管理员，必须首先[设置移动设备管理](setup-hybrid-mdm.md)并[启用注册](enable-platform-enrollment.md)。 一旦启用了注册，用户便可以注册自己的设备。 要与用户共享的注意事项和步骤，请参阅[如何使最终用户了解 Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate)。

购买设备的公司或学校可以利用可[管理公司拥有的设备](enroll-company-owned-devices.md)的程序。
