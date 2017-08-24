---
title: "管理 iOS 激活锁定 | Microsoft Docs"
description: "使用 System Center Configuration Manager 管理 iOS 激活锁定。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2745bac-e1b4-4dac-8ac7-32f1c820bc9c
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 88bef04a52f716ae13afc21c25d33dea06a3fc9c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-ios-activation-lock-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理 iOS 激活锁定

*适用范围：System Center Configuration Manager (Current Branch)*


System Center Configuration Manager 可以帮助你管理 iOS 激活锁定，这是适用于 iOS 7.1 及更高版本设备的“查找我的 iPhone”应用的功能。 启用激活锁定后，任何人都必须先输入用户的 Apple ID 和密码，然后才能执行以下操作：

- 关闭“查找我的 iPhone”
- 擦除设备
- 重新激活设备

在 **无人监督** 的设备上，当使用了“查找我的 iPhone”应用时，激活锁定会自动启用。

在 **监督** 的设备上，必须通过使用 Configuration Manager 符合性设置激活激活锁定。

> [!TIP]
> 在 iOS 设备的监管模式下，你可以使用 Apple 配置器工具来锁定设备，以将设备的功能限制为完成特定的业务目的。 监管模式通常仅适用于公司拥有的设备。

尽管激活锁定可帮助保护 iOS 设备的安全，并可提高在设备丢失和被盗时的找回几率，但对于 IT 管理员来说，此功能仍然带来了许多挑战。 例如：

- 你的其中一个用户在设备上设置了激活锁定。 该用户之后离开了公司并返回使用其设备。 如果不提供用户的 Apple ID 和密码，即使将其擦除，也不能重新激活该设备。
- 你需要报告启用了激活锁定的所有设备。
- 更新你组织中的设备分配情况时，如果你希望将某些设备分配给另一个部门， 你只能重新分配未启用激活锁定的设备。


为了帮助解决这些问题，Apple 在 iOS 7.1 中引入了绕过激活锁定。 借助此功能，你无需用户的 Apple ID 和密码即可删除监管设备中的激活锁定。 监管设备可以生成设备特定的绕过激活锁定代码，该代码存储在 Apple 的激活服务器上。

可以在 [此处](https://support.apple.com/HT201365)阅读有关激活锁定的详细信息。

## <a name="how-configuration-manager-helps-you-manage-activation-lock"></a>Configuration Manager 如何帮助你管理激活锁定

Configuration Manager 可以以下两种方法帮助你管理激活锁定：

1. 在受到监督的设备上启用激活锁定。
2. 在受到监督的设备上绕过激活锁定。

> [!IMPORTANT]
> 在无人监督的设备上不能绕过激活锁定。

对于企业自有设备，这个的业务优点是：



- 用户能够获得“查到我的 iPhone”应用所具有的安全优势
- 你可以让用户在知道如下事实的情况下进行工作：当需要重新调整设备的用途时，你可以停用或解锁设备


## <a name="enable-activation-lock-on-supervised-devices"></a>在受监督的设备上启用激活锁定

使用 Configuration Manager 符合性设置来创建和部署 **iOS 和 Mac OS X** 类型的配置项目以在受到监督的设备上启用激活锁定：

1. 使用[如何为没有使用 System Center Configuration Manager 客户端管理的 iOS 和 Mac OS X 设备创建配置项目](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)主题中的信息来创建 **iOS 和 Mac OS X** 类型的配置项目。
2. 在创建配置项目向导的“系统安全”页中，将设置“允许激活锁定（仅限受监督模式）”配置为“允许”。
3. [将配置项目添加到配置基线](/sccm/compliance/deploy-use/create-configuration-baselines)。
4. [部署此配置基线](/sccm/compliance/deploy-use/deploy-configuration-baselines)到包含你想要启用激活锁定的 iOS 设备的集合。

> [!IMPORTANT]
> 在执行此过程之前，请确保你实际拥有该设备。 如果没有，将绕过激活锁定，并且任何拥有此设备的人都将可以完全访问它，从而使他们可以关闭“查找我的 iPhone”、擦除设备或将其重新激活。

仅可以在受监督设备上绕过激活锁定，或者检索激活锁定绕过代码；尝试在无人监督的设备上绕过激活锁定或在错误中查看绕过代码结果。



## <a name="view-the-activation-lock-bypass-code"></a>查看绕过激活锁定代码

1. 在 Configuration Manager 控制台中，单击“资产和符合性” 。
2. 在“资产和符合性”  工作区中，单击“设备” 。
3. 选择在受监督模式下已启用激活锁定的注册设备。
4. 在“主页”选项卡上，在“设备”组中，单击“远程设备操作” > “查看激活锁定绕过代码”。
5. “激活锁定绕过代码”对话框中将显示所选设备的绕过代码。

## <a name="bypass-activation-lock"></a>绕过激活锁定

1. 在 Configuration Manager 控制台中，单击“资产和符合性” 。
2. 在“资产和符合性”  工作区中，单击“设备” 。
3. 选择在受监督模式下已启用激活锁定的注册设备。
3. 在“主页”选项卡上，在“设备”组中，单击“远程设备操作” > “绕过激活锁定”。
5. 阅读警告对话框中的消息，在准备好继续操作后，单击“是”。
6. 你可以从以下位置检查解锁请求的状态：

    - 设备属性对话框中设备的发现数据。
    - “设备”视图中“激活锁定绕过状态”列（默认情况下隐藏此列）。
    - 细节窗格的“摘要”选项卡中的“远程设备操作信息”部分（当设备处于选中状态）。
