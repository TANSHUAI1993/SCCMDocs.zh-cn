---
title: "对 Lookout 集成进行故障排除 | System Center Configuration Manager"
description: "本主题介绍如何解决 Lookout 集成中的常见问题。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4fd2d3b8aae6a2f42e7c6a87723d16368be30984
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="troubleshoot-lookout-integration-with-intune"></a>使用 Intune 对 Lookout 集成进行故障排除

*适用范围：System Center Configuration Manager (Current Branch)*

## <a name="troubleshoot-login-errors"></a>解决登录错误
### <a name="403-errors"></a>403 错误
在登录 [Lookout MTP 控制台](https://aad.lookout.com)时，可能会看到 403 错误：**无权访问该服务**当指定的用户名不是配置为访问 Lookout MTP 的 Azure Active Directory (Azure AD) 组的成员时，可能会发生这种情况。

Lookout MTP 配置为仅允许来自已配置的 Azure AD 组的用户访问。 如果不确定哪一组配置有访问 Lookout MTP 的权限，请联系 Lookout 支持。

可以通过以下方式联系 Lookout 支持：

* 电子邮件：enterprisesupport@lookout.com
* 登录 [MTP 控制台](http://aad.lookout.com)，导航到“支持”模块。
* 转到：https://enterprise.support.lookout.com/hc/en-us/requests，提出支持请求。

### <a name="unable-to-sign-in"></a>无法登录
在 Azure AD 全局管理员用户尚未接受初始 Lookout 安装程序时，可能会看到以下错误。

![Lookout 登录屏幕的屏幕截图显示登录出错](media/lookout-consent-not-accepted-error.png)

若要解决此问题，全局管理员用户必须登录 https://aad.lookout.com/les?action=consent，接受启动安装程序的提示。 有关更详细的信息，请参阅[使用 Lookout MTP 设置订阅](set-up-your-subscription-with-lookout.md)主题

## <a name="troubleshoot-device-status-issues"></a>解决设备状态问题

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>设备不显示在 Lookout MTP 控制台设备列表中

在以下其中一个情况中可能出现此问题：
* 当拥有此设备的用户不在“Lookout MTP 控制台”中指定的“注册组”中时。  从“系统”模块转到“Intune 连接器”选项卡，然后查看“注册管理”设置。  应看到一个或多个为注册配置的 Azure AD 组。  验证拥有缺失设备的用户是否属于其中一个指定的 Azure AD 组。  新用户添加到注册组后，要看到设备在 Lookout MTP 控制台的“设备”模块中显示，需要的时间最多为配置的轮询间隔（默认为 5 分钟）。

* 如果设备不受 Lookout MTP 支持。  不受支持的设备将在 Lookout MTP 控制台连接器设置的“托管的设备”部分显示。

### <a name="device-continues-to-be-reported-as-pending"></a>设备继续报告为“挂起”

设备显示为“挂起”意味着最终用户尚未打开 Lookout for Work 应用，也尚未点击“激活”按钮。 有关在 Lookout for Work 应用中激活设备的更多详细信息，请参阅以下主题：

[系统提示在 Android 设备上安装 Lookout for Work](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>在 Lookout MTP 控制台中，某设备显示为活动状态，但不具有设备 ID。
这表明拥有此设备的用户不在“Lookout MTP控制台”指定的“注册组”中。   如果拥有此设备的用户已从注册组删除或者该用户所属的注册组已删除，设备会进入此状态。

从 Lookout MTP 控制台的“系统”模块转到“Intune 连接器”选项卡，然后查看“注册”设置。  应看到一个或多个为注册配置的 Azure AD 组。  验证拥有设备的用户是否属于其中一个指定的 Azure AD 组。

在设备处于此状态时，Lookout 将继续通知用户任何检测到的威胁，但不会向 Intune 发送任何威胁信息。

### <a name="device-shows-disconnected-state"></a>设备显示“已断开连接”状态

“已断开连接”表明 Lookout MTP 超过预配置的时间间隔（默认值为 30 天，至少为 7 天）仍未收到来自设备的消息。 这表明 Company Portal 应用或 Lookout for Work 应用未安装在该设备上或已被卸载。 重新安装该应用应当能够解决此问题。 用户打开 Lookout for Work 并激活该应用时，设备便与 Lookout MTP 和 Intune 重新同步。

### <a name="forcing-a-resync-on-the-device"></a>在设备上强制重新同步
在 Lookout MTP 控制台的“设备”模块中，管理员可以选择该设备，然后选择将其删除。   设备所有者下一次打开 Lookout for Work 应用并点击“激活”时，设备状态将执行完整的重新同步。

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>设备的所有者将不能再使用此设备
必须擦除设备并要求新用户按[本主题](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe)中所述方法进行注册。


此外，可转到 Lookout MTP 控制台的“设备”模块，然后选择“删除”。

只要新用户属于在 Lookout MTP 控制台中指定的注册组之一，Azure AD 将该设备与新用户关联后，即可显示该设备。

## <a name="compliance-remediation-workflows"></a>合规性修正工作流
[系统提示在 Android 设备上安装 Lookout for Work]( http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[需要解决 Lookout for Work 在 Android 设备上发现的威胁](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)
