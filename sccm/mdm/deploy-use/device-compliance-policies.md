---
title: "设备合规性策略 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中管理合规性策略以使设备符合条件访问策略。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
caps.latest.revision: "18"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: bcaa2a9b5474e06bf344dc4fd47dbb160ea36297
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的设备合规性策略

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的**合规性策略**定义设备必须遵从的规则和设置，以便被视为符合条件访问策略。 也可使用符合性策略来监视和修正独立于条件访问的设备符合性问题。  


> [!IMPORTANT]  
>  本文介绍了由 Microsoft Intune 管理的设备的合规性策略。    由 System Center Configuration Manager 管理的电脑的合规性策略在[管理对由 System Center Configuration Manager 管理的电脑的 O365 服务的访问](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)中进行了说明。  

 这些规则包括类似于下面这样的要求：  

-   用于访问设备的 PIN 和密码

-   存储在设备上的数据的加密

-   设备是否已越狱或取得 root 权限  

-   设备上的电子邮件是否由 Intune 策略管理，或者设备是否被 Windows 设备运行状况证明服务报告为不正常。
-   无法在设备上安装的应用。


 将符合性策略部署到用户集合。 将合规性策略部署到用户后，会对所有用户设备检查合规性。  

 下表列出了合规性策略支持的设备类型，也列出了当该策略与条件访问策略一起使用时托管不符合合规性的设置的方式。  

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

 **修正** = 法规遵从性由设备操作系统强制执行（例如，强制用户设置 PIN）。  设置永远不会不符合要求。  

 **已隔离** = 设备操作系统并不强制合规性（例如，Android 设备不强制用户加密设备）。  这种情况下：  

-   如果条件访问策略将用户作为目标，则会阻止设备。  

-   公司门户或 Web 门户将通知用户任何合规性问题。  


### <a name="next-steps"></a>后续步骤  
[创建和部署设备合规性策略](create-compliance-policy.md)
### <a name="see-also"></a>另请参阅  
 [在 System Center Configuration Manager 中管理对服务的访问](../../protect/deploy-use/manage-access-to-services.md)
