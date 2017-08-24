---
title: "证书配置文件安全和隐私 | Microsoft Docs"
description: "了解在 System Center Configuration Manager 中为用户和设备管理证书配置文件的最佳安全做法。"
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: c51787ad3fa0bdb285017cfab1ca6931afba9ea6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中证书配置文件的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*


##  <a name="security-best-practices-for-certificate-profiles"></a>证书配置文件的最佳安全方案  
 在为用户和设备管理证书配置文件时，请使用下列最佳安全方案。  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|确定并遵循网络设备注册服务的下列任何最佳安全方案，包括在 Internet Information Services (IIS) 中将网络设备注册服务网站配置为需要 SSL 和忽略客户端证书。|请参阅 TechNet 上 Active Directory 证书服务库中的 [Network Device Enrollment Service Guidance（网络设备注册服务指导）](http://go.microsoft.com/fwlink/p/?LinkId=309016) 。|  
|在配置 SCEP 证书配置文件时，请选择设备和基础结构可支持的最安全选项。|确定、实施和遵循已为你的设备和基础结构推荐的任何最佳安全方案。|  
|手动指定用户设备相关性，而不是允许用户确定其主设备。 此外，不要启用基于使用情况的配置。|如果在 SCEP 证书配置文件中单击“仅允许在用户主设备上进行证书注册”  选项，请不要考虑从用户处或从要成为权威设备的设备中收集的信息。 如果随此配置一起部署 SCEP 证书配置文件，并且受信任的管理用户未指定用户设备相关性，则未授权用户可能会收到提升的权限，并且会被授予身份验证证书。<br /><br /> **注意：**如果确实启用基于使用情况的配置，则会使用未受 System Center Configuration Manager 保护的状态消息收集此信息。 为了帮助减轻此威胁，请在客户端计算机和管理点之间使用 SMB 签名或 IPsec。|  
|不要为用户将“读取”和“注册”权限添加到证书模板，或者配置证书注册点以跳过证书模板检查。|尽管在为用户添加“读取”和“注册”安全权限的情况下，Configuration Manager 支持其他检查，并且可以在无法进行身份验证的情况下配置证书注册点以跳过此检查，但任何一种配置都不是最佳安全做法。 有关详细信息，请参阅[为 System Center Configuration Manager 中证书配置文件规划证书模板权限](../../protect/plan-design/planning-for-certificate-template-permissions.md)。|  

## <a name="privacy-information-for-certificate-profiles"></a>证书配置文件的隐私信息  
 你可以使用证书配置文件来部署根证书颁发机构 (CA) 和客户端证书，然后评估那些设备在应用了配置文件后是否变为符合。 管理点会将符合性信息发送到站点服务器，System Center Configuration Manager 会在站点数据库中存储该信息。 符合性信息包括诸如使用者名称和指纹等证书属性。 设备在将信息发送到管理点时会对其进行加密，但信息不会以加密格式存储在站点数据库中。 数据库将保留信息，直到 90 天默认间隔过后站点维护任务“删除过期的配置管理数据”  将其删除为止。 可以配置删除间隔。 符合性信息不会被发送到 Microsoft。  

 证书配置文件使用 Configuration Manager 通过发现收集的信息。 有关发现的隐私信息的详细信息，请参阅 **Security and privacy for System Center Configuration Manager** 中的 [有关发现的隐私信息](../../core/plan-design/security/security-and-privacy.md)部分。  

> [!NOTE]  
>  颁发给用户或设备的证书可能允许访问机密信息。  

 默认情况下，设备不评估证书配置文件。 此外，你必须配置证书配置文件，然后将它们部署到用户或设备。  

 在配置证书配置文件之前，请考虑隐私要求。  
