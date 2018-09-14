---
title: 基于风险限制访问权限
titleSuffix: Configuration Manager
description: 根据设备、网络和应用程序风险限制对公司资源的访问权限。
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a00a4e8140548c4f503e3467626b8d6cbab69ee3
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584622"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>根据设备、网络和应用程序风险管理对公司资源的访问权限

*适用范围：System Center Configuration Manager (Current Branch)*

通过移动威胁防御连接器，可以将选定的移动威胁防御供应商用作符合性策略和条件访问规则的信息源。 由此，可以增强组织资源（如 Exchange 和 Sharepoint）的安全性，特别是易受攻击的移动设备的安全性。

> [!Important]  
> 自 2018 年 8 月 14 日起，混合移动设备管理[功能停用](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。 有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<!--Intune feature 2683117-->  



## <a name="what-problem-does-this-solve"></a>此功能可解决什么问题？

组织需要保护敏感数据免遭潜在的威胁，包括物理威胁、基于应用的威胁和基于网络的威胁，以及操作系统漏洞。

过去，组织在保护电脑免受攻击方面一直比较主动，而移动设备则没有监控和保护。 尽管移动平台内置有保护（如应用隔离和审查使用者应用商店），但这些平台仍易受到复杂攻击。 如今，更多员工使用设备完成工作，并需要访问敏感信息。 因此，需要保护设备免受日益复杂的攻击。



## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Intune 移动威胁防御连接器如何工作？

该连接器会在 Intune 和所选的移动威胁防御供应商之间创建信道，进而保护组织资源。 Intune 移动威胁防御合作伙伴为移动设备提供了直观且易于部署的应用程序，可主动扫描和分析威胁信息与 Intune 共享。 可出于报告或强制目的使用此信息。 

例如，连接的移动威胁防御应用向移动威胁防御供应商报告设备当前连接到易受中间人攻击的网络。 此信息用于共享并分类为适当的风险级别：低，中或高。 将此风险与 Intune 中配置的风险级别限额进行比较，以确定在设备受到威胁时，是否应撤消对你选择的某些资源的访问权限。



## <a name="sample-scenarios"></a>示例方案

移动威胁防御解决方案判定设备受到感染时：

![移动威胁防御检测到的感染设备](../media/mtp/MTD-image-1.png)

修正设备时授予访问权限：

![移动威胁防御授予的访问权限](../media/mtp/MTD-image-2.png)



## <a name="next-steps"></a>后续步骤

了解如何根据设备、网络和应用程序风险，通过以下工具保护对公司资源的访问：

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)