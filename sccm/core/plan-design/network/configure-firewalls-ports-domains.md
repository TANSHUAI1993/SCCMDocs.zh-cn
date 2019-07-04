---
title: 网络基础结构
titleSuffix: Configuration Manager
description: 设置防火墙、端口和域以准备 Configuration Manager 通信。
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60a24e06d650b0e25007fb8490eb0c7d8c1996a1
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285610"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Configuration Manager 的网络基础结构注意事项

适用范围：  System Center Configuration Manager (Current Branch)

要准备网络以支持 Configuration Manager，你可能需要配置一些基础结构组件。 例如，打开防火墙端口以传递 Configuration Manager 使用的通信。  

## <a name="ports-and-protocols"></a>端口和协议

不同的 Configuration Manager 功能使用不同的网络端口。 有些端口是必需的，有些可以自定义。

大多数 Configuration Manager 通信使用常见的端口，比如用于 HTTP 的端口 80 或用于 HTTPS 的端口 443。 某些站点系统角色支持使用自定义网站和自定义端口。 有关详细信息，请参阅[站点系统服务器网站](/sccm/core/plan-design/network/websites-for-site-system-servers)。

部署 Configuration Manager 之前，请确定计划使用的端口，并根据需要设置防火墙。

安装 Configuration Manager 后，如果需要更改端口，请勿忘记更新设备和网络上的防火墙。 还可以在 Configuration Manager 中更改端口的配置。

有关详细信息，请参阅下列文章：

- [如何配置客户端通信端口](/sccm/core/clients/deploy/configure-client-communication-ports)
- [Configuration Manager 中使用的端口](/sccm/core/plan-design/hierarchy/ports)


## <a name="internet-access-requirements"></a>Internet 访问要求

某些 Configuration Manager 功能依赖 Internet 连接来获取完整功能。 如果组织使用防火墙或代理设备限制与 Internet 的网络通信，请确保允许使用必要的终结点。

有关详细信息，请参阅 [Internet 访问要求](/sccm/core/plan-design/network/internet-endpoints)


## <a name="proxy-servers"></a>代理服务器

你可以对不同的站点系统服务器和客户端指定单独的代理服务器。 在安装站点系统角色或客户端时进行这些配置，或以后根据需要进行更改。

有关详细信息，请参阅[代理服务器支持](/sccm/core/plan-design/network/proxy-server-support)。
