---
title: "在 Intune 中启用 Lookout MTP | System Center Configuration Manager"
description: "在 Intune 管理控制台中启用 Lookout Mobile Threat Protection。"
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9536efdd-0f29-47a8-8283-0edea7714319
caps.latest.revision: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: a06f0b3a0080a06a0ccbfa7f3802c575aee2c9b7


---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>在 Intune 管理控制台中启用 Lookout MTP 连接

*适用范围：System Center Configuration Manager (Current Branch)*

本主题演示如何在 Intune 中启用 Lookout MTP 连接。 用户应在 Lookout 控制台中配置 Intune 连接器，然后才执行此步骤。  如果尚未执行此步骤，请执行[使用 Lookout Mobile Threat Protection 设置订阅](set-up-your-subscription-with-lookout.md)中所述的步骤。

若要在 Intune 中启用 Lookout MTP 连接，在 [Microsoft Intune 管理员控制台](https://manage.microsoft.com)中的“管理”页中，选择“第三方服务集成”。 选择“Lookout 状态”，然后使用切换按钮启用“与 MTP 同步”。

![突出显示了启用切换按钮的 Lookout 同步页屏幕截图](../media/lookout-intune-synchronization.png)

这样就完成了在 Intune 管理员控制台中设置 Lookout 和 Intune 的集成。  下面的几个步骤可实现此解决方案，其中包括部署 [Lookout for Work 应用](configure-and-deploy-lookout-for-work-apps.md)和设置[合规性](enable-device-threat-protection-rule-compliance-policy.md)策略。

>[!IMPORTANT]
> **必须**先配置 Lookout for Work 应用，然后才创建合规性策略规则和配置条件性访问。 这确保了最终用户有权访问电子邮件和其他公司资源之前，应用已准备就绪并且可用。

## <a name="next-steps"></a>后续步骤
[配置 Lookout for Work 应用](configure-and-deploy-lookout-for-work-apps.md)



<!--HONumber=Dec16_HO3-->


