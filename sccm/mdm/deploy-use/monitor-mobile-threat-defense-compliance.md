---
title: 监视移动威胁防御符合性
titleSuffix: Configuration Manager
description: 监视来自 Configuration Manager 管理器控制台的移动威胁防御合作伙伴符合性状态
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b77fabc6ea4f5823777e932011313c5e2de1acf
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551309"
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**监视移动威胁防御符合性**

适用范围：  System Center Configuration Manager (Current Branch)

## <a name="to-monitor-the-overall-compliance-status"></a>监视整体符合性状态

监视移动威胁防御状态：

1.  在 Configuration Manager 控制台中，单击“监视”  工作区。

2.  在“监视”  工作区中，单击“安全”  节点。

可以看到含有不同威胁级别的符合性状态的摘要，该摘要以可视化图的形式显示。 可以单击图表的独立部分以查看详细信息，如： 

- 被平台报告为不符合的设备数
- 与设备符合性状态相关的任何错误

![设备威胁保护仪表板](device-threat-protection-dashboard.png)

## <a name="to-monitor-the-individual-compliance-status"></a>监视单个合规性状态

还可以看到各个设备状态：

1.  在 Configuration Manager 控制台中，单击“资产和符合性”  工作区。

2.  单击“设备”  。

> [!TIP] 
> 可以添加“设备威胁合规性”  和“设备威胁级别”  列，以查看状态。 默认情况下，这些列不会显示。

## <a name="device-threat-protection-tab"></a>设备威胁防护选项卡

此外，在“设备”  屏幕上，可以选择特定设备，然后单击“设备威胁防护”  选项卡，以提供有关设备符合性状态的更多信息。 查看下面的列说明及其预期值，以帮助你分析设备符合性状态。

> [!IMPORTANT] 
> 设备威胁防护选项卡仅在所选设备为移动设备时才会显示。

|列名称|默认情况下可见|描述| 
|-|-|-|
|**描述**| 是 | 有关移动威胁防御合作伙伴所提供的威胁的详细信息。 |
|**上次更新时间**| 是 | 移动威胁防御合作伙伴上一次向 Intune 发送有关威胁的已更新的详细信息的时间。 |
|**威胁严重性**| 是 | 威胁严重性是单个威胁的定义，它基于“移动威胁防御合作伙伴”控制台中的管理员的配置。 它具有三个值之一：**低**，**中等**或**高** |
|**威胁状态**| 是 | 设备上威胁的当前状态。 可能的状态：**Active**，**解析**或**忽略：** 指示用户将忽略其设备上的威胁但威胁仍然存在。 |
|**威胁类型**| 是 | 威胁的移动威胁防御合作伙伴类型。 可能的值：**应用程序**，**文件**或**OS** |
|**AAD 帐户 ID**| 否 | Azure Active Directory 唯一标识符。 |
|**分类**| 是 | 移动威胁防御合作伙伴提供了威胁的分类。 可能的值：**Root Enabler、 Riskware、 广告软件、 Chargeware、 DataLeak、 木马病毒、 蠕虫、 病毒，利用，后门，Bot、 AppDropper、 ClickFraud、 垃圾邮件、 间谍软件、 SurveillanceWare、 漏洞和未知，Root Jailbrake、 连接、 TollFraud、 SideloadedApp** |
|**设备 ID**| 否 | Azure Active Directory 对象 ID，表示包含威胁信息的已联接的设备的工作区。 |
|**威胁 ID**| 否 | 移动威胁防御合作伙伴生成的威胁的唯一标识符。 威胁 ID 用于跟踪解析。 |
|**威胁 URL**| 否 | 如果存在，则威胁 URL 链接回此特定威胁的移动威胁防御合作伙伴的管理控制台视图。 |

> [!TIP] 
> 请确保启用**默认情况下可见**的列，以查看有关你的设备的移动威胁防御符合性状态的详细信息。
