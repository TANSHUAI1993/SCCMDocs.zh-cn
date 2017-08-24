---
title: "在 Intune 中启用 Lookout MTP | Microsoft Docs"
description: "在 Intune 管理控制台中启用 Lookout Mobile Threat Protection。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: f9ddbcc981fa1274a41ae16a6a939c0cdf739c3e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>在 Intune 管理控制台中启用 Lookout MTP 连接

*适用范围：System Center Configuration Manager (Current Branch)*

本主题演示如何在 Intune 中启用 Lookout MTP 连接。 用户应在 Lookout 控制台中配置 Intune 连接器，然后才执行此步骤。  如果尚未执行此步骤，请执行[使用 Lookout Mobile Threat Protection 设置订阅](set-up-your-subscription-with-lookout.md)中所述的步骤。

若要在 Intune 中启用 Lookout MTP 连接，在 [Microsoft Intune 管理员控制台](https://manage.microsoft.com)中的“管理”页中，选择“第三方服务集成”。 选择“Lookout 状态”，然后使用切换按钮启用“与 MTP 同步”。

![突出显示了启用切换按钮的 Lookout 同步页屏幕截图](media/lookout-intune-synchronization.png)

这样就完成了在 Intune 管理员控制台中设置 Lookout 和 Intune 的集成。  下面的几个步骤可实现此解决方案，其中包括部署 [Lookout for Work 应用](configure-and-deploy-lookout-for-work-apps.md)和设置[合规性](enable-device-threat-protection-rule-compliance-policy.md)策略。

>[!IMPORTANT]
> **必须**先配置 Lookout for Work 应用，然后才创建合规性策略规则和配置条件性访问。 这确保了最终用户有权访问电子邮件和其他公司资源之前，应用已准备就绪并且可用。

## <a name="next-steps"></a>后续步骤
[配置 Lookout for Work 应用](configure-and-deploy-lookout-for-work-apps.md)
