---
title: "Wi-Fi 和 VPN 配置文件安全和隐私 | Microsoft Docs"
description: "了解在 System Center Configuration Manager 中管理设备的 Wi-Fi 和 VPN 配置文件的安全最佳做法。"
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 6d1d0a393a2ce614ae5f819475bd47b05e699b45
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中 Wi-Fi 和 VPN 配置文件的安全性和隐私

*适用范围：System Center Configuration Manager (Current Branch)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Wi-Fi 和 VPN 配置文件的安全最佳做法  
 在管理设备的 Wi-Fi 和 VPN 配置文件时，请使用下列安全最佳做法。  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|请尽可能选择 Wi-Fi 和 VPN 基础结构和客户端操作系统支持的最安全选项。|Wi-Fi 和 VPN 配置文件提供了一种简便的方法来集中分发和管理设备已支持的 Wi-Fi 和 VPN 设置。 Configuration Manager 不会添加 Wi-Fi 或 VPN 功能。<br /><br /> 确定、实施和遵循已为你的设备和基础结构推荐的任何最佳安全方案。|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Wi-Fi 配置的隐私信息  
 可以使用 Wi-Fi 和 VPN 配置文件来配置客户端设备以连接到 Wi-Fi 和 VPN 服务器，然后评估这些设备在应用配置文件后是否具有符合性。 管理点会将符合性信息发送到站点服务器，该信息存储在站点数据库中。 设备在将信息发送到管理点时会对其进行加密，但信息不会以加密格式存储在站点数据库中。 数据库将保留该信息，直到站点维护任务“删除过期的配置管理数据”  将其删除为止。 默认删除间隔是 90 天，但你可以更改它。 符合性信息不会被发送到 Microsoft。  

 默认情况下，设备不评估 Wi-Fi 和 VPN 配置文件。 此外，必须对配置文件进行配置，然后将其部署到用户。  

 配置 Wi-Fi 或 VPN 配置文件前，请考虑隐私要求。  
