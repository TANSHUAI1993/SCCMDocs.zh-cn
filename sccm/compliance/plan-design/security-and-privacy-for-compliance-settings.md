---
title: "符合性设置的安全和隐私 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中符合性设置的安全最佳方案。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e7dc554ffcd23978eed44819b525f6cc239b2135
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-compliance-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的符合性设置的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*


## <a name="security-best-practices-for-compliance-settings"></a>符合性设置的最佳安全方案  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|不监视敏感数据。|为了帮助避免信息泄露，不配置配置项目来监视潜在敏感信息。|  
|不配置符合性规则，它使用可由最终用户修改的数据。|如果基于用户可以修改的数据（如配置选项的注册表设置）创建符合性规则，则符合性结果会不可靠。|  
|仅当相应内容具有来自受信任发布者的有效数字签名时，才从外部源导入 Microsoft System Center 配置包和其他配置数据。|已发布的配置数据可以进行数字签名，以便你可以验证发布源并确保数据未被篡改。 如果数字签名验证检查失败，你将收到警告，并提示你继续导入。 如果你无法验证数据的来源和完整性，则不要导入未签名的数据。|  
|实现访问控制来保护引用计算机。|确保当管理用户通过浏览到引用计算机来配置注册表或文件系统设置时，引用计算机未受侵害。|  
|在浏览到引用的计算机时，确保信道安全。|为了防止数据在通过网络传输时被篡改，请在运行 Configuration Manager 控制台的计算机与引用计算机之间使用 Internet 协议安全性 (IPsec) 或服务器消息块 (SMB)。|  
|限制和监视被授予基于符合性设置管理员角色的安全角色的管理用户。|被授予“合规性设置管理员”  角色的管理用户可以将配置项目部署到层次结构中的所有设备和所有用户。 配置项目可以非常强大，例如可以包括脚本和注册表重新配置。|  

## <a name="privacy-information-for-compliance-settings"></a>符合性设置的隐私信息  
 可以使用符合性设置评估客户端设备是否符合在配置基线中部署的配置项目。 某些设置可以在不符合要求时自动修正。 管理点会将符合性信息会发送到站点服务器，并存储在站点数据库中。 设备在将信息发送到管理点时会对其进行加密，但信息不会以加密格式存储在站点数据库中。 信息将保留在数据库中，直到每 90 天站点维护任务“删除过期的配置管理数据”  将其删除。 可以配置删除间隔。 符合性信息不会被发送到 Microsoft。  

 默认情况下，设备不评估符合性设置。 此外，必须对配置项目和配置基线进行配置，然后将它们部署到设备。  
