---
title: "远程同步已注册 Intune 的设备上的策略 | Microsoft Docs"
description: "了解如何从 Configuration Manager 控制台中远程同步已注册 Intune 的设备上的策略"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: 18
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dcdccc34fa55ce3d3e4459d209c7aeb74752214b
ms.openlocfilehash: c6496e9694314f1910ca944f6c083a9f3fd2bf79
ms.contentlocale: zh-cn
ms.lasthandoff: 12/16/2016

---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台中远程同步已注册 Intune 的设备上的策略

*适用范围：System Center Configuration Manager (Current Branch)*


可以从 Configuration Manager 控制台中为已注册 Intune 的设备请求策略同步，而无需在设备本身的公司门户应用中请求同步。 

要执行此操作：

1.    在“资产和符合性” > “概述” > “设备”下选择一个设备。
2.    在“远程设备操作”菜单中，单击“发送同步请求”。


5 到 10 分钟后，策略中的任何更改都将同步到设备。 可以在设备视图的新列中查看同步请求的状态信息（即“远程同步状态”），也可在每个设备的“属性”对话框中的发现数据部分查看。

