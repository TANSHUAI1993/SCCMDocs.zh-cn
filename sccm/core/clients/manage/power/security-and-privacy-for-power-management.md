---
title: "电源管理的安全和隐私 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中电源管理的安全和隐私信息。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: f72059973057e707f58cb6b7aa495226b6c1962c


---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中电源管理的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*

本部分包含 System Center Configuration Manager 中电源管理的安全和隐私信息。  

## <a name="security-best-practices-for-power-management"></a>电源管理的最佳安全方案  
 电源管理没有相关的最佳安全方案。  

## <a name="privacy-information-for-power-management"></a>电源管理的隐私信息  
 电源管理利用 Windows 中的内置功能在营业时间和非营业时间监视电源使用情况并将电源设置应用于计算机。 Configuration Manager 收集计算机的电源使用情况信息，其中包括用户使用计算机时间的相关数据。 虽然 Configuration Manager 监视集合而不是每台计算机的电源使用情况，但集合可以只包含一台计算机。 默认情况下不启用电源管理，必须由管理员配置。  

 电源使用情况信息存储在 Configuration Manager 数据库中，不会发送给 Microsoft。 详细信息在数据库中保留 31 天，摘要信息保留 13 个月。 不能配置删除时间间隔。  

 在配置电源管理之前，请考虑隐私要求。  



<!--HONumber=Dec16_HO3-->


