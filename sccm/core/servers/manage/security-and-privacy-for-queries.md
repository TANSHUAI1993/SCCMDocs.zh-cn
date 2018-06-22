---
title: 查询的安全和隐私
titleSuffix: Configuration Manager
description: 从站点数据库查询信息时，请了解最佳安全做法和隐私。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2d84385782df17d4019d6de65bcc7006aeab8b24
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337609"
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的查询的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的查询允许基于指定条件从站点数据库中检索信息。 Configuration Manager 会在标准操作过程中收集站点数据库信息。 例如，通过使用已从发现或清单收集的信息，可以配置标识设备满足指定的条件的查询。  

 有关查询的详细信息，请参阅 [System Center Configuration Manager 中的查询简介](../../../core/servers/manage/introduction-to-queries.md)。 有关 Configuration Manager 操作（收集可使用查询检索的信息）的最佳安全做法和隐私信息的详情，请参阅 [System Center Configuration Manager 的安全和隐私](../../../core/plan-design/security/security-and-privacy.md)。  

## <a name="security-best-practices-for-queries"></a>查询的最佳安全方案  
 可将以下最佳安全方案用于查询。  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|当导出或导入保存到网络位置的查询时，请保护该位置和网络通道的安全。|限制可访问网络文件夹的人员。<br /><br /> 在网络位置与站点服务器之间使用服务器消息块 (SMB) 签名或 Internet 协议安全性 (IPsec)，以防止攻击者在查询数据导入之前篡改它。|  

## <a name="see-also"></a>另请参阅  
 [System Center Configuration Manager 的查询技术参考](../../../core/servers/manage/queries-technical-reference.md)
