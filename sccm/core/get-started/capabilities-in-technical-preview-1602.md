---
title: "Technical Preview 1602 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1602 版中的可用功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 2354f885aaf69683004ad78f0e1978e78fee9145
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1602-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1602 版中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了 System Center Configuration Manager Technical Preview 1602 版中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。  

 以下是可以试用的此版本的新功能。  

##  <a name="BKMK_MDM"></a>对移动设备管理的改进  

### <a name="ios-activation-lock"></a>iOS 激活锁定  
 System Center Configuration Manager 可以帮助你管理 iOS 激活锁定，这是适用于 iOS 7.1 及更高版本设备的“查找我的 iPhone”应用的功能。 当设备上使用了“查到我的 iPhone”应用时，激活锁定自动启用。 启用后，任何人都必须先输入用户的 Apple ID 和密码，然后才能执行以下操作：  

-   关闭“查找我的 iPhone”  

-   擦除设备  

-   重新激活设备  

 Configuration Manager 可以请求运行 iOS 7.1 和更高版本的已监管设备和非监管设备的激活锁定状态。 对于监管设备而言，Intune 可以检索绕过激活锁定代码并直接将代码发布到设备。  

 有关详细信息，请参阅[通过 Configuration Manager 的绕过激活锁定帮助保护 iOS 设备](/sccm/mdm/deploy-use/manage-ios-activation-lock)  

##  <a name="BKMK_SC1601"></a>版本 1602 中对软件中心的改进  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>从软件中心刷新 PC 计算机和用户策略  
 已将新选项“同步策略”添加到软件中心的“选项” > “计算机维护”页面，该操作可让电脑刷新其 Configuration Manager 计算机和用户策略。  

##  <a name="BKMK_Win10Servicing"></a>对 Windows 10 维护服务的改进  
 在 1602 Technical Preview 中，我们为 Windows 10 维护服务添加了以下改进：  

-   用于维护服务计划的新的筛选器选项。  现在可以筛选“语言”、“必需”和“标题”。 只有满足指定条件的升级项才会添加到关联部署中。  

-   选择软件更新同步的“升级”分类时，将显示一个警告对话框，告知需要 WSUS [修补程序 3095113](https://support.microsoft.com/kb/3095113) 才能成功同步软件更新，并且 Windows 10 维护服务才能正常工作。  从该对话框，你可以转到该修补程序的知识库文章。  

-   可用的 Windows 10 升级现在仅显示在 Configuration Manager 控制台的“Windows 10 维护服务” \ “所有 Windows 10 更新”节点中。 这些更新不再显示在“软件更新” \ “所有软件更新”节点中。  

-   启动 Windows 10 升级包的最终用户将会收到一个提示对话框，告知用户将升级自己的操作系统。  
