---
title: 设备合规性策略
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中管理符合性策略以使设备符合条件访问策略。
ms.date: 03/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e225b7ab54a1061387d1c8ee369641f68bd7889
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196868"
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的设备合规性策略

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 中的符合性策略定义了设备必须遵守哪些规则和设置才能被视为符合条件访问策略。 也可使用符合性策略来监视和修正独立于条件访问的设备符合性问题。  


> [!IMPORTANT]  
>  本文介绍了由 Microsoft Intune 管理的设备的合规性策略。 中介绍了由 Configuration Manager 客户端管理的设备的合规性策略[管理对 Office 365 服务的 Configuration Manager 管理的设备访问](/sccm/protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)。  

 这些规则包括类似于下面这样的要求：  

-   用于访问设备的 PIN 和密码  

-   存储在设备上的数据的加密  

-   设备是否已越狱或取得 root 权限  

-   设备上的电子邮件是否由 Intune 策略管理，或者设备是否被 Windows 设备运行状况证明服务报告为不正常。  

-   无法在设备上安装的应用。  


 将符合性策略部署到用户集合。 将合规性策略部署到用户后，会对所有用户设备检查合规性。  



## <a name="supported-device-types"></a>支持的设备类型

 下表列出了符合性策略支持的设备类型，同时列出了当该策略与条件访问策略一起使用时如何管理不符合条件的设置。  

|规则|Windows 8.1 及更高版本|Windows Phone 8.1 及更高版本|iOS 6.0 及更高版本|Android 4.0 及更高版本、Samsung KNOX Standard 4.0 及更高版本、Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**PIN 或密码配置**|已修正|已修正|已修正|已隔离|  
|**设备加密**|不适用|已修正|已修正（通过设置 PIN）|已隔离<br>（Android for Work 始终加密）|  
|**已越狱或取得 root 权限的设备**|不适用|不适用|已隔离（非设置）|已隔离（非设置）|  
|**电子邮件配置文件**|不适用|不适用|已隔离|不适用|  
|**最低操作系统版本**|已隔离|已隔离|已隔离|已隔离|  
|**最高操作系统版本**|已隔离|已隔离|已隔离|已隔离|  
|**设备运行状况证明（1602 更新）**|设置不适用于 Windows 8.1<br /><br /> Windows 10 和 Windows 10 移动版已隔离。|不适用|不适用|不适用|  
|**不能安装的应用**|不适用|不适用|已隔离|已隔离|

 **已修正** = 设备操作系统强制执行符合性规则。 例如，强制用户设置 PIN。 设置绝不会不符合要求。  

 **已隔离** = 设备操作系统不强制执行符合性规则。 例如，Android 设备不强制用户加密设备。 这种情况下：  

-   如果条件访问策略将用户作为目标，则设备将被阻止。  

-   公司门户或 Web 门户将就任何符合性问题通知用户。  



## <a name="devices-without-any-assigned-compliance-policy"></a>未分配有任何符合性策略的设备
<!--2520152-->
从 2018 年 7 月开始，配置是否有任何已分配符合性策略的所有设备都视为符合还是不符合标准。 未分配有符合性策略的设备被默认视为符合条件。 可按以下步骤在 Azure 门户中更改此设置：

1. 登录到 [Azure 门户上的 Intune](https://aka.ms/intuneportal)。  

2. 选择“设备符合性”，然后选择设置组中的“符合性策略设置”。  

3. 对于“将未分配有符合性策略的设备标记为”设置，选择下述某个选项：  

     - 符合（默认设置）- 未分配有符合性策略的设备被视为符合策略。 如果启用条件访问，则这些设备有权访问内部资源。  

     - 不符合- 未分配有符合性策略的设备被视为不符合策略。 如果启用条件访问，则按照条件访问策略中的条件阻止这些设备访问内部资源。  

4. 单击保存。  

强烈建议至少在每个平台中向环境中的所有用户部署一个符合性策略。 然后将此设置配置为“不符合”，从而确保内部资源的安全性。 有关详细信息，请参阅 [Intune 服务中的安全性增强功能](https://aka.ms/compliance_policies)博客文章。



## <a name="next-steps"></a>后续步骤  
[创建和部署设备合规性策略](/sccm/mdm/deploy-use/create-compliance-policy)

### <a name="see-also"></a>另请参阅  
 [在 Configuration Manager 中管理服务的访问权限](/sccm/protect/deploy-use/manage-access-to-services)
