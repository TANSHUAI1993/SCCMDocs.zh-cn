---
title: "防火墙和域 | Microsoft Docs"
description: "设置防火墙、端口和域以准备 System Center Configuration Manager 通信。"
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4a2a8f96a900a2c4959ae3ff59232771ece95991
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>为 System Center Configuration Manager 设置防火墙、端口和域

*适用范围：System Center Configuration Manager (Current Branch)*

若要准备网络以支持 System Center Configuration Manager，请计划设置基础结构（如防火墙）以传递 Configuration Manager 所使用的通信。  

|注意事项|详细信息|  
|-------------------|-------------|  
|不同的 Configuration Manager 功能所使用的**端口和协议**。 某些端口是必需的，而其他的**域和服务**则可以自定义。|大多数 Configuration Manager 通信使用常见的端口，比如用于 HTTP 通信的端口 80 或用于 HTTPS 通信的端口 443。 但是，[某些站点系统角色支持使用自定义网站](/sccm/core/plan-design/network/websites-for-site-system-servers)和自定义端口。<br /><br /> **部署 Configuration Manager 之前**，请确定计划使用的端口并相应地设置防火墙。<br /><br /> 安装 Configuration Manager 后，**如果需要更改端口**，请勿忘记更新设备和网络上的防火墙，以及从 Configuration Manager 中更改端口的配置。<br /><br /> 有关详细信息，请参阅： </br>- [如何配置客户端通信端口](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Configuration Manager 中使用的端口](../../../core/plan-design/hierarchy/ports.md) </br>- [服务连接点的 Internet 访问要求](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|站点服务器和客户端可能需要使用的**域和服务**。|Configuration Manager 功能可能需要站点服务器和客户端有权访问 Internet 上的特定服务和域，如 Windowsudpate.microsoft.com 或 Microsoft Intune 服务。<br /><br /> 如果将使用 Microsoft Intune 管理移动设备，那么还必须设置对 [Intune 所需的端口和域](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)的访问权限。|  
|用于站点系统服务器和用于客户端通信的**代理服务器** 。 你可以对不同的站点系统服务器和客户端指定单独的代理服务器。|因为这些配置是在安装站点系统角色或客户端时所做的，因此只需注意代理服务器配置，以供将来配置站点系统角色和客户端时参考。<br /><br /> 如果不能确定你的部署是否将需要使用代理服务器，请查看 [System Center Configuration Manager 中的代理服务器支持](../../../core/plan-design/network/proxy-server-support.md)以了解可以使用代理服务器的站点系统角色和客户端操作的相关信息。|   
|  
