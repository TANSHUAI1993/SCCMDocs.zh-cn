---
title: 远程同步已注册 Intune 的设备上的策略
titleSuffix: Configuration Manager
description: 了解如何从 Configuration Manager 控制台中远程同步已注册 Intune 的设备上的策略
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eab8f812b8772be0812437359275b80702f5760c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137739"
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台中远程同步已注册 Intune 的设备上的策略

适用范围：System Center Configuration Manager (Current Branch)


可以从 Configuration Manager 控制台中为已注册 Intune 的设备请求策略同步，而无需在设备本身的公司门户应用中请求同步。 

要执行此操作：

1.  在“资产和符合性” > “概述” > “设备”下选择一个设备。
2.  在“远程设备操作”菜单中，单击“发送同步请求”。


5 到 10 分钟后，策略中的任何更改都将同步到设备。 可以在设备视图的新列中查看同步请求的状态信息（即“远程同步状态”），也可在每个设备的“属性”对话框中的发现数据部分查看。
