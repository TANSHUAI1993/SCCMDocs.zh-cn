---
title: "移动威胁防御 | System Center Configuration Manager"
description: "根据设备、网络和应用程序风险，通过 Configuration Manager 和 Intune 移动威胁防御合作伙伴保护对公司资源的访问"
ms.custom: na
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 298d879638a2d20d421b19752cb5f20f6725df14
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="intune-mobile-threat-defense-connectors-in-configuration-manager"></a>Configuration Manager 中的 Intune 移动威胁防御连接器

*适用范围：System Center Configuration Manager (Current Branch)*

[混合 MDM 部署（SCCM 与 Intune）](https://docs.microsoft.com/en-us/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)与 Intune 和移动威胁防御合作伙伴之间的集成使你可根据设备风险评估，控制对公司资源和数据的访问。

通过 Intune 移动威胁防御连接器，可利用所选的移动威胁防御供应商作为符合性策略和条件性访问规则的信息源。 由此，IT 管理员可增强公司资源（如 Exchange 和 Sharepoint）的安全性，特别是易受攻击的移动设备的安全性。

## <a name="what-problem-does-this-solve"></a>此功能可解决什么问题？

公司需要保护敏感数据免受以下新威胁的攻击：物理威胁、基于应用的威胁和基于网络的威胁，以及操作系统漏洞。
过去，公司在保护电脑免受攻击方面一直比较主动，但并未监视和保护移动设备。 尽管移动平台内置有保护（如应用隔离和审查使用者应用商店），但这些平台仍易受到复杂攻击。 如今，更多员工使用设备完成工作，并需要访问敏感信息。 因此，需要保护设备免受日益复杂的攻击。

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Intune 移动威胁防御连接器如何工作？

该连接器会在 Intune 和所选的移动威胁防御供应商之间创建信道，进而保护公司资源。 Intune 移动威胁防御合作伙伴为移动设备提供了直观且易于部署的应用程序，可出于报告或强制目的主动扫描和分析威胁信息并与 Intune 共享。 例如，如果连接的移动威胁防御应用向移动威胁防御供应商报告，称你网络上的某电话当前连接到易受中间人攻击的网络，则此信息将进行共享并分类为相应的风险级别（中/低/高），然后可将该级别与 Intune 中配置的允许风险级别限额进行比较，确定设备受到威胁时是否应取消你对某些所选资源的访问。

## <a name="sample-scenarios"></a>示例方案

移动威胁防御解决方案判定设备受到感染时：

![](http://i.imgur.com/Li1WUOU.png)

修正设备时授予访问权限：

![](http://i.imgur.com/VCIwpdz.png)

## <a name="mobile-threat-defense-partners"></a>移动威胁防御合作伙伴

了解如何根据设备、网络和应用程序风险，通过以下工具保护对公司资源的访问：

- [Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)