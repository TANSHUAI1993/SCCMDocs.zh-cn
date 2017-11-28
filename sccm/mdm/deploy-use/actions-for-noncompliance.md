---
title: "针对非符合性的操作"
titleSuffix: Configuration Manager
description: "了解如何通过 Configuration Manager 设置针对非符合性的操作"
ms.custom: na
ms.date: 11/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
caps.latest.revision: "18"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 1dd10d9452fae85f2ecc3d3077fba420454ef337
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="set-up-actions-for-non-compliance"></a>设置针对非符合性的操作

针对非符合性的操作允许配置一系列以时间排序的应用于不合规设备的操作。 例如，可以将电子邮件发送到不合规设备的最终用户，并且/或者将这些设备标记为不合规。

## <a name="before-you-begin"></a>在开始之前

> [!IMPORTANT]
> 至少需要创建一个设备符合性策略来设置针对非符合性的操作。

以下是受支持的针对非符合性的操作：

- 向最终用户发送电子邮件
- 将设备标记为不合规

### <a name="send-e-mail-to-end-user"></a>向最终用户发送电子邮件

可以选择预先创建的默认电子邮件模板，也可以创建完全自定义电子邮件通知。 Configuration Manager 使你可以自定义主题、邮件正文，包括公司徽标、联系信息和其他收件人。

### <a name="mark-devices-non-compliant"></a>将设备标记为不合规

可以订立日程表，其中某些天将阻止设备访问公司资源。 这可以立即施行，但你也可以为用户提供宽限期，使之符合设备符合性策略。

### <a name="supported-platforms"></a>受支持的平台

[通过 Intune 托管的所有平台](https://docs.microsoft.com/intune/supported-devices-browsers)均提供支持。

## <a name="to-add-an-email-template"></a>添加电子邮件模板

Configuration Manager 提供电子邮件模板，但也可以创建自己的模板。 电子邮件模板稍后会在创建针对非符合性操作的过程中使用，以便与用户进行沟通。

1. 在 Configuration Manager 控制台中，选择“资产和符合性”。

2. 在“资产和符合性”工作区中，展开“符合性设置”，然后选择“符合性通知模板”。

3. 在“主页”选项卡上的“创建符合性通知模板”中。

4. 必须输入以下信息：a. 名称：电子邮件模板名称。
    b. 发件人：发送电子邮件通知的电子邮件地址。
    c. 主题：解释正在发送的电子邮件通知的主题。
    d. 邮件正文：有关电子邮件通知的更多详情。

    > [!TIP] 
    > 还可以在电子邮件标题中包含公司徽标，或在电子邮件页脚中包含公司名称和联系信息。 可以在 Intune 订阅的属性中对此进行编辑。

5. 单击“确定”保存新电子邮件模板。

6. 可以在“添加操作”页面上，从列表中选择新的电子邮件模板。

7. 选择电子邮件模板后，请单击“确定”。

## <a name="to-create-actions-for-non-compliance"></a>创建针对非符合性的操作

1. 在 Configuration Manager 控制台中，选择“资产和符合性”。

2. 在“资产和符合性”工作区中，展开“符合性设置”，然后选择“符合性策略”。

3. 在“主页”选项卡上的“创建”组中，选择“创建符合性策略”。

4. 选择所需的支持平台，然后单击两次“下一步”。 可以跳过“规则”页面。

5. 在“非合规性操作”页面上，定义在设备变得不合规时将发生的情况，并单击“新建”。
6. 可以选择这两个选项：“向最终用户发送电子邮件”或“将设备标记为不合规”。

7. 如果选择“向最终用户发送电子邮件”，则必须输入以下：a. 宽限期(以天数计)：可以输入 0 - 365 天。
    b. 其他收件人(通过电子邮件) c. 选择邮件模板：可以选择默认电子邮件模板或添加的自定义电子邮件模板。
    
    > [!TIP] 
    > 在添加“向最终用户发送电子邮件”操作时，通过从“添加操作”页面添加“新建:”，也可添加新的电子邮件模板。

8. 如果选择“将设备标记为不合规”，则必须输入：a. 宽限期(以天数计)：可以输入 0 - 365 天。

9. 选择操作并输入设置后，请单击两次“下一步”，然后选择“关闭”。


