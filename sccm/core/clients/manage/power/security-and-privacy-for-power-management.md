---
title: 电源管理的安全和隐私
titleSuffix: Configuration Manager
description: 获取 System Center Configuration Manager 中电源管理的安全和隐私信息。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: a7bba23bf35d60d83fcff01acb20c8f404b6445d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123399"
---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中电源管理的安全和隐私

适用范围：System Center Configuration Manager (Current Branch)

本部分包含 System Center Configuration Manager 中电源管理的安全和隐私信息。  

## <a name="security-best-practices-for-power-management"></a>电源管理的最佳安全方案  
 电源管理没有相关的最佳安全方案。  

## <a name="privacy-information-for-power-management"></a>电源管理的隐私信息  
 电源管理使用内置于 Windows 监视电源使用情况和在营业时间和非工作时间期间将电源设置应用于计算机的功能。 Configuration Manager 收集计算机的电源使用情况信息，其中包括用户使用计算机时间的相关数据。 虽然 Configuration Manager 监视集合而不是每台计算机的电源使用情况，但集合可以只包含一台计算机。 默认情况下不启用电源管理，必须由管理员配置。  

 电源使用情况信息存储在 Configuration Manager 数据库中，不会发送给 Microsoft。 详细信息在数据库中保留 31 天，摘要信息保留 13 个月。 不能配置删除时间间隔。  

 在配置电源管理之前，请考虑隐私要求。  
