---
title: "监视移动威胁防御符合性 | System Center Configuration Manager"
description: "监视来自 Configuration Manager 管理器控制台的移动威胁防御合作伙伴符合性状态"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 8edf83a0f761dfc16274ce49c3aa2b878c7fe6cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**监视移动威胁防御符合性**

*适用范围：System Center Configuration Manager (Current Branch)*

## <a name="to-monitor-the-overall-compliance-status"></a>监视整体符合性状态

监视移动威胁防御状态：

1.  在 Configuration Manager 控制台中，单击“监视”工作区。

2.  在“监视”工作区中，单击“安全”节点。

可以看到含有不同威胁级别的符合性状态的摘要，该摘要以可视化图的形式显示。 可以单击图表的独立部分以查看详细信息，如： 

- 被平台报告为不符合的设备数
- 与设备符合性状态相关的任何错误

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>监视单个合规性状态

还可以看到各个设备状态：

1.  在 Configuration Manager 控制台中，单击“资产和符合性”工作区。

2.  单击“设备”。

> [!TIP] 
> 可以添加“设备威胁合规性”和“设备威胁级别”列，以查看状态。 默认情况下，这些列不会显示。

## <a name="device-threat-protection-tab"></a>设备威胁防护选项卡

此外，在“设备”屏幕上，可以选择特定设备，然后单击“设备威胁防护”选项卡，以提供有关设备符合性状态的更多信息。 查看下面的列说明及其预期值，以帮助你分析设备符合性状态。

> [!IMPORTANT] 
> 设备威胁防护选项卡仅在所选设备为移动设备时才会显示。

|列名称|默认情况下可见|描述| 
|-|-|-|
|**描述**| 是 | 有关移动威胁防御合作伙伴所提供的威胁的详细信息。 |
|**上次更新时间**| 是 | 移动威胁防御合作伙伴上一次向 Intune 发送有关威胁的已更新的详细信息的时间。 |
|**威胁严重性**| 是 | 威胁严重性是单个威胁的定义，它基于“移动威胁防御合作伙伴”控制台中的管理员的配置。 它具有三个值：**低**、**中**或**高** |
|**威胁状态**| 是 | 设备上威胁的当前状态。 可能的状态：**激活**、**已解决**或**已忽略：**表示用户忽略了设备上的威胁，但是威胁仍然存在。 |
|**威胁类型**| 是 | 威胁的移动威胁防御合作伙伴类型。 可能的值：**应用**、**文件**或**操作系统** |
|**AAD 帐户 ID**| 否 | Azure Active Directory 唯一标识符。 |
|**分类**| 是 | 移动威胁防御合作伙伴提供了威胁的分类。 可取值：**Root Enabler、Riskware、Adware、Chargeware、DataLeak、Trojan、Worm、Virus、Exploit、Backdoor、Bot、AppDropper、ClickFraud、Spam、Spyware、SurveillanceWare、Vulnerability、Unknown、Root Jailbrake、Connectivity、TollFraud、SideloadedApp** |
|**设备 ID**| 否 | Azure Active Directory 对象 ID，表示包含威胁信息的已联接的设备的工作区。 |
|**威胁 ID**| 否 | 移动威胁防御合作伙伴生成的威胁的唯一标识符。 威胁 ID 用于跟踪解析。 |
|**威胁 URL**| 否 | 如果存在，则威胁 URL 链接回此特定威胁的移动威胁防御合作伙伴的管理控制台视图。 |

> [!TIP] 
> 请确保启用**默认情况下可见**的列，以查看有关你的设备的移动威胁防御符合性状态的详细信息。
