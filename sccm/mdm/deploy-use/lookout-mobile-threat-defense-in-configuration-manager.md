---
title: "基于风险限制访问权限 | Microsoft Docs"
description: "根据设备、网络和应用程序风险限制对公司资源的访问权限。"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 21841d97387f07f53993d957641f9ad892d723c2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>根据设备、网络和应用程序风险管理对公司资源的访问权限

*适用范围：System Center Configuration Manager (Current Branch)*

根据 Lookout （一种与 Microsoft Intune 集成的设备威胁防护解决方案）所做的风险评估，可以控制从移动设备对公司资源进行访问的权限。 风险基于 Lookout 服务从设备的操作系统 (OS) 漏洞、已安装恶意应用以及恶意网络配置文件收集的遥测。 

根据通过 System Center Configuration Manager (SCCM) 合规性策略启用的 Lookout 所报告的风险评估，可以配置条件访问策略并允许或阻止因在其上检测到威胁而确定为不合规的那些设备。

[混合 MDM 部署（SCCM 与 Intune）](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)根据诸如 Lookout 等设备威胁防护解决方案所提供的风险评估，让你能够控制对公司资源的访问。

## <a name="how-do-the-hybrid-mdm-deployment-and-lookout-device-threat-protection-help-protect-company-resources"></a>混合 MDM 部署和 Lookout 设备威胁防护如何帮助保护公司资源？
在移动设备上运行的 Lookout 移动应用 (Lookout for work) 可捕获文件系统、网络堆栈、设备和应用程序遥测（如果可用），并将其发送到 Lookout 设备威胁防护云服务，以便计算移动威胁的合计设备风险。 还可以在 Lookout 控制台中更改威胁的风险级别分类来满足要求。  

SCCM 中的合规性策略现在包含针对 Lookout Mobile Threat Protection 的新规则，其基于 Lookout 威胁风险评估。 启用此规则后，将会评估设备的合规性。

如果确定设备不符合合规性策略，则可使用条件访问策略阻止对 Exchange Online 和 SharePoint Online 等资源的访问。 阻止访问后，会向最终用户提供演练以帮助解决此问题，从而获取对公司资源的访问权限。 该演练通过 Lookout for Work 应用推出。

## <a name="supported-platforms"></a>支持的平台：
* **Android 4.1 及更高版本**，且在 Microsoft Intune 中注册。
* **iOS 8 及更高版本**，且在 Microsoft Intune 中注册。
有关 Lookout 支持的平台和语言的信息，请参阅此[文章](https://personal.support.lookout.com/hc/en-us/articles/114094140253)。

## <a name="prerequisites"></a>先决条件：
* [混合 MDM 部署](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)
* 订阅 Microsoft Intune 和 Azure Active Directory。
* 对 Lookout Mobile Endpoint Security 的企业订阅。  有关详细信息，请参阅 [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="example-scenarios"></a>方案示例
以下是一些常见方案：
### <a name="control-access-based-on-threat-from-malicious-apps"></a>根据来自恶意应用的威胁控制访问权限：
在设备上检测到恶意软件等恶意应用时，可阻止此类设备执行以下操作：
* 解决威胁前连接到公司电子邮件。
* 使用 OneDrive for Work 应用同步公司文件。
* 访问业务关键应用。

**检测到恶意应用时阻止访问：**

![关系图：显示在设备因其上的恶意应用而被确定为不合规时阻止访问的条件访问策略](media/config-mgr-maliciousapps_blocked.png)

**修正威胁时取消阻止设备并能够访问公司资源：**

![关系图：显示设备在修正后被确定为合规时授予访问权限的条件访问策略](media/config-mgr-maliciousapps-unblocked.png)
### <a name="control-access-based-on-threat-to-network"></a>根据网络威胁控制访问权限：
检测到中间人攻击等网络威胁时，根据设备风险限制对 WiFi 网络的访问。

**阻止通过 WiFi 访问网络的权限：**

![关系图：显示根据网络威胁阻止 WiFi 访问的条件访问策略](media/config-mgr-network-wifi-blocked.png)

**修正后授予访问权限：**

![关系图：显示修正威胁后允许访问的条件访问策略](media/config-mgr-network-wifi-unblocked.png)
### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>根据网络威胁控制对 SharePoint Online 的访问：

检测到中间人攻击等网络威胁时，根据设备风险阻止对公司文件进行同步。

**根据设备上检测到的网络威胁阻止对 SharePoint Online 的访问：**

![关系图：显示根据威胁检测阻止设备访问 SharePoint Online 的条件访问策略](media/config-mgr-network-spo-blocked.png)


**修正后授予访问权限：**

![关系图：显示修正网络威胁后允许访问的条件访问策略](media/config-mgr-network-spo-unblocked.png)

## <a name="next-steps"></a>后续步骤
以下是实现此解决方案必须执行的主要步骤：
1.  [使用 Lookout 移动威胁保护设置订阅](set-up-your-subscription-with-lookout.md)
2.  [在 Intune 中启用 Lookout MTP 连接](enable-lookout-connection-in-intune.md)
3.  [配置和部署 Lookout for Work 应用程序](configure-and-deploy-lookout-for-work-apps.md)
4.  [配置合规性策略](enable-device-threat-protection-rule-compliance-policy.md)
5.  [对 Lookout 集成进行故障排除](troubleshoot-lookout-integration.md)
