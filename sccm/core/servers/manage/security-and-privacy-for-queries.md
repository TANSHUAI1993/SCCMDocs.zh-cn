---
title: "查询的安全和隐私 | Microsoft Docs"
description: "从站点数据库查询信息时，请了解最佳安全做法和隐私。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e42b13c68ecaeac94245838c2f42e2790799de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的查询的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的查询允许基于指定条件从站点数据库中检索信息。 Configuration Manager 会在标准操作过程中收集站点数据库信息。 例如，通过使用从发现或清单收集的信息，可以配置查询来标识满足指定条件的设备。  

 有关查询的详细信息，请参阅 [System Center Configuration Manager 中的查询简介](../../../core/servers/manage/introduction-to-queries.md)。 有关 Configuration Manager 操作（收集可使用查询检索的信息）的最佳安全做法和隐私信息的详情，请参阅 [System Center Configuration Manager 的安全和隐私](../../../core/plan-design/security/security-and-privacy.md)。  

## <a name="security-best-practices-for-queries"></a>查询的最佳安全方案  
 可将以下最佳安全方案用于查询。  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|当导出或导入保存到网络位置的查询时，请保护该位置和网络通道的安全。|限制可访问网络文件夹的人员。<br /><br /> 在网络位置与站点服务器之间使用服务器消息块 (SMB) 签名或 Internet 协议安全性 (IPsec)，以防止攻击者在查询数据导入之前篡改它。|  

## <a name="see-also"></a>另请参阅  
 [System Center Configuration Manager 的查询技术参考](../../../core/servers/manage/queries-technical-reference.md)
