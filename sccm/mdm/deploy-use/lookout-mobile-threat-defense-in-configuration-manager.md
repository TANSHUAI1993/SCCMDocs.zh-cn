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
ms.openlocfilehash: c8e984c6eb76716e031ed793a7753840842f0ea7
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584539"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>根据设备、网络和应用程序风险管理对公司资源的访问权限

*适用范围：System Center Configuration Manager (Current Branch)*

根据 Lookout 执行的风险评估，控制从移动设备对公司资源的访问。 Lookout 是与 Microsoft Intune 集成的设备威胁防护解决方案。 该风险基于 Lookout 服务所收集的数据。 它从设备收集有关 OS 漏洞、已安装的恶意软件和恶意网络配置文件的数据。 

可基于通过 Configuration Manager 符合性策略启用的 Lookout 风险评估来配置条件访问策略。 基于 Configuration Manager 是否在设备上检测到威胁而判定其不符合，这些策略会相应地允许或阻止设备。

> [!Important]  
> 自 2018 年 8 月 14 日起，混合移动设备管理[功能停用](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。 有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<!--Intune feature 2683117-->  



## <a name="how-does-it-work"></a>工作原理

混合 MDM 部署和 Lookout 设备威胁防护如何帮助保护公司资源？

Lookout 的移动应用 (Lookout for Work) 在移动设备上运行。 它可捕获文件系统、网络堆栈以及设备和应用程序的使用情况数据（如果有）。 应用程序将此数据发送到 Lookout 设备威胁防护云服务，从而计算出设备的累积移动威胁风险。 使用 Lookout 控制台可更改威胁的风险级别分类来满足要求。  

Configuration Manager 中的符合性策略现在包含针对 Lookout 移动威胁防护的新规则，其基于 Lookout 威胁风险评估。 当启用此规则时，Configuration Manager 会评估设备的符合性。

如果设备不符合符合性策略，则可使用条件访问策略阻止其访问 Exchange Online 和 SharePoint Online 等资源。 如果访问被阻止，最终用户会收到演练以帮助解决此问题，并获取对公司资源的访问权限。 用户通过 Lookout for Work 应用启动此演练。



## <a name="supported-platforms"></a>受支持的平台

- **Android 4.1 及更高版本**，且在 Microsoft Intune 中注册。  

- **iOS 8 及更高版本**，且在 Microsoft Intune 中注册。  


有关 Lookout 支持的平台和语言的信息，请参阅此 [Lookout 支持文章](https://personal.support.lookout.com/hc/articles/114094140253)。



## <a name="prerequisites"></a>先决条件

- [混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)  

- 订阅 Microsoft Intune 和 Azure Active Directory。  

- 对 Lookout Mobile Endpoint Security 的企业订阅。 有关详细信息，请参阅 [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)。  



## <a name="example-scenarios"></a>方案示例


### <a name="control-access-based-on-threat-from-malicious-apps"></a>根据来自恶意应用的威胁控制访问权限

当在设备上检测到恶意软件等恶意应用时，可阻止此类设备执行以下操作：

- 连接到公司电子邮件（在解决威胁前）  

- 使用 OneDrive for Work 应用同步公司文件  

- 访问业务关键应用  

#### <a name="access-blocked-when-malicious-apps-are-detected"></a>检测到恶意应用时阻止访问

![检测到恶意应用时阻止访问的条件访问策略](media/config-mgr-maliciousapps_blocked.png)

#### <a name="device-unblocked-and-is-able-to-access-company-resources-when-the-threat-is-remediated"></a>修正威胁后取消阻止设备使其能够访问公司资源

![设备合规时授予访问权限的条件访问策略](media/config-mgr-maliciousapps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>根据网络威胁控制访问权限

检测到中间人攻击等网络威胁时，根据设备风险限制对 WiFi 网络的访问。

#### <a name="access-to-network-through-wifi-blocked"></a>阻止通过 WiFi 访问网络

![根据网络威胁阻止 WiFi 访问的条件访问](media/config-mgr-network-wifi-blocked.png)

#### <a name="access-granted-on-remediation"></a>修正后授予访问权限

![修正威胁后允许访问的条件访问](media/config-mgr-network-wifi-unblocked.png)


### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>根据网络威胁控制对 SharePoint Online 的访问

检测到中间人攻击等网络威胁时，根据设备风险阻止对公司文件进行同步。

#### <a name="access-blocked-sharepoint-online-based-on-network-threat-detected-on-the-device"></a>根据设备上检测到的网络威胁阻止对 SharePoint Online 的访问

![阻止设备访问 SharePoint Online 的条件访问](media/config-mgr-network-spo-blocked.png)


#### <a name="access-granted-on-remediation"></a>修正后授予访问权限

![修正威胁后允许访问的条件访问](media/config-mgr-network-spo-unblocked.png)



## <a name="next-steps"></a>后续步骤

若要实施此解决方案，请使用以下步骤：  

1.  [使用 Lookout 移动威胁保护设置订阅](set-up-your-subscription-with-lookout.md)
2.  [在 Intune 中启用 Lookout MTP 连接](enable-lookout-connection-in-intune.md)
3.  [配置和部署 Lookout for Work 应用程序](configure-and-deploy-lookout-for-work-apps.md)
4.  [配置合规性策略](enable-device-threat-protection-rule-compliance-policy.md)
5.  [对 Lookout 集成进行故障排除](troubleshoot-lookout-integration.md)
