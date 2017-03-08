---
title: "启用合规性策略中的设备保护规则 | System Center Configuration Manager"
description: "启用设备合规性策略中的移动威胁防护规则。"
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 020f43e8-738e-4a82-91be-27b10cda9665
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 498b8c02dbf1391e6331c8b9ad7b6ef0fdef22d0
ms.openlocfilehash: 319289c9b211935ba10cb6d3da386ffed3c0153e
ms.lasthandoff: 02/23/2017


---
# <a name="create-a-lookout-device-threat-protection-rule"></a>创建 Lookout 设备威胁防护规则

*适用范围：System Center Configuration Manager (Current Branch)*

## <a name="before-you-begin"></a>在开始之前

Intune with Lookout 移动威胁防护使用户能够在设备上检测移动威胁并进行风险评估。 可在 Configuration Manager 中创建符合性策略规则，内附确定设备是否符合要求的风险评估。 然后可以使用条件访问策略，根据设备合规性来允许或阻止对 Exchange、SharePoint 和其他服务的访问。

若要使 Lookout 设备威胁检测作用于设备的合规性策略：

-   必须在符合性策略上启用**设备威胁防护**规则。

-   “Intune 管理员控制台”中的“Lookout 状态”页必须显示为“活动”。 请参阅[在 Intune 中启用 Lookout MTP 连接](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)主题，了解有关如何激活 Lookout 集成的详细信息和说明。

在符合性策略中创建设备威胁防护规则之前，建议执行以下操作：

1.  [设置订阅以使用 Lookout 设备威胁保护](https://docs.microsoft.com/sccm/protect/deploy-use/set-up-your-subscription-with-lookout)

2.  [在 Intune 中启用 Lookout 连接](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)

3.  [配置 Lookout for Work 应用](https://docs.microsoft.com/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps)

>[!NOTE]
>仅在设置完成后，才会执行符合性规则。

## <a name="to-create-a-device-threat-protection-rule"></a>创建设备威胁防护规则

作为 Lookout 设备威胁防护设置过程的一部分，你会在 [Lookout 控制台](https://aad.lookout.com)中创建一个策略，该策略将各种威胁分类为高级别、中等级别和低级别。 在 Intune 符合性策略中，将使用威胁级别来设置允许的最大威胁级别。

创建 Lookout 设备威胁防护规则：

1.  在 Configuration Manager 控制台中，单击“资产和符合性”工作区。

2.  在“资产和符合性”中，展开“符合性策略”。

3.  右键单击“符合性策略”，然后选择“创建符合性策略”。

4.  输入符合性策略名称，然后选择“不使用 Configuration Manager 客户端管理的设备的符合性规则”。

5.  选择将使用符合性策略预配的 OS 平台（Android 4.1 及更高版本和/或 iOS 8 及更高版本）。

6.  在“规则”页上，单击“新建”为符合的设备指定规则。

7.  在“添加规则”页上，使用以下信息定义新规则：
    1.  条件：设备威胁防护最大风险级别。
    
    2.  值：可以是下列值之一：
        1.  “无(安全)”：这是最安全的选项。 这意味着设备不能有任何威胁。 如果发现了任何级别的威胁，设备都将视为不符合要求。
        2.  “低”：如果只有低级别的威胁存在，设备将视为合规。 高于此级别的威胁均会使设备处于不合规状态。
        3.  “中等”：如果设备上发现的威胁为低级别或中等级别，设备将视为合规。 如果检测到高级别威胁，则设备会被确定为不合规。
        4.  “高”：这是最不安全的选项。 实际上，这将允许所有威胁级别，并且可能只有在将此解决方案用于报告用途时才有用。

>[!IMPORTANT]
>如果为 Office 365 和其他服务创建条件访问策略，则应将上述合规性评估纳入考虑范围，并且在威胁解决前阻止非合规性设备访问公司资源。
