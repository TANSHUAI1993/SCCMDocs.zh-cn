---
title: "启用符合性策略中的设备防护规则 | Microsoft Docs"
description: "启用设备合规性策略中的移动威胁防护规则。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: faa92e150686e615164ce3f5435b77a65305aab3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>启用合规性策略中的设备威胁防护规则

*适用范围：System Center Configuration Manager (Current Branch)*

Intune with Lookout 移动威胁防护使用户能够在设备上检测移动威胁并进行风险评估。 可以在 Configuration Manager 中创建合规性策略规则，以包含确定设备是否合规的风险评估。 然后可以使用条件访问策略，根据设备合规性来允许或阻止对 Exchange、SharePoint 和其他服务的访问。

若要使 Lookout 设备威胁检测作用于设备的合规性策略：

* 必须在合规性策略上启用**设备威胁防护**规则。

* “Intune 管理员控制台”中的“Lookout 状态”页必须显示为“活动”。 请参阅[在 Intune 中启用 Lookout MTP 连接](enable-lookout-connection-in-intune.md)主题，了解有关如何激活 Lookout 集成的详细信息和说明。


在合规性策略中创建设备威胁防护规则之前，建议[使用 Lookout 设备威胁防护设置订阅](set-up-your-subscription-with-lookout.md)、[在 Intune 中启用 Lookout 连接](enable-lookout-connection-in-intune.md)，以及[配置 Lookout for Work 应用](configure-and-deploy-lookout-for-work-apps.md)。 仅当设置完成后，才会执行合规性规则。

若要启用设备威胁防护规则，可使用现有合规性策略或创建新的合规性策略。

作为 Lookout 设备威胁防护设置过程的一部分，你会在 [Lookout 控制台](https://aad.lookout.com)中创建一个策略，该策略将各种威胁分类为高级别、中等级别和低级别。 在 Intune 合规性策略中，将使用威胁级别来设置允许的最大威胁级别。

在合规性策略向导的“规则”页中，使用以下信息定义新规则：
  * 条件：设备威胁防护最大风险级别。
  * 值：可以是下列值之一：
    * “无(安全)”：这是最安全的选项。 这意味着设备不能有任何威胁。 如果发现了任何级别的威胁，设备都将视为不合规。
    * “低”：如果只有低级别的威胁存在，设备将视为合规。 高于此级别的威胁均会使设备处于不合规状态。
    * “中等”：如果设备上发现的威胁为低级别或中等级别，设备将视为合规。 如果检测到高级别威胁，则设备会被确定为不合规。
    * “高”：这是最不安全的选项。 实际上，这将允许所有威胁级别，并且可能只有在将此解决方案用于报告用途时才有用。

如果为 Office 365 和其他服务创建条件访问策略，则应将上述合规性评估纳入考虑范围，并且在威胁解决前阻止非合规性设备访问公司资源。

设备威胁防护状态显示在“监视”工作区中的“安全性”节点上。
可视化图表中显示了各种威胁级别的状态摘要。 可以单击图表的各个部分查看详细信息，如按平台报告为不合规的设备数量和报告的任何错误。
还可以在“资产和符合性”工作区中的“设备”下查看单个设备状态。  可以添加“设备威胁合规性”和“设备威胁级别”列，以查看状态。  默认情况下，这些列不会显示。
