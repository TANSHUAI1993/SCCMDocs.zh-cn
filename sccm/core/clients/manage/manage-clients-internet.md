---
title: "在 Internet 上管理客户端 - Configuration Manager | Microsoft Docs"
description: "了解如何通过云管理网关和 Configuration Manager 中的基于 Internet 的客户端管理来管理客户端。"
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1b6752be448e1062c97a3225db4fa8af9f4832a6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>在 Internet 上使用 Configuration Manager 管理客户端

*适用范围：System Center Configuration Manager (Current Branch)*

通常，Configuration Manager 中受管理的多数计算机和服务器与执行管理功能的站点系统服务器物理上位于同一内部专用或公司网络中。 但如果客户端计算机连接到了 Internet，则可在公司网络外部对其进行管理，无需通过虚拟专用网络连接客户端，到达站点系统服务器。

Configuration Manager 提供两种方法来管理连接了 Internet 的客户端：

-   云管理网关

-   基于 Internet 的客户端管理

## <a name="cloud-management-gateway"></a>云管理网关

从 1610 版本起，Configuration Manager 引入了云管理网关。 通过这一新方法可结合使用部署到 Microsoft Azure 的云服务和与该服务通信的新站点系统角色来管理基于 Internet 的客户端。 然后客户端可使用该服务与 Configuration Manager 通信。

优点：

-   无需额外的基础结构投资。

-   不会将本地基础结构公开至 Internet。

-   运行服务的云虚拟机由 Azure 完全管理且免维护。

-   可轻松在 Configuration Manager 控制台中进行设置和配置。

缺点：

-   云订阅费用。

-   通过云服务发送的管理数据。

有关详细信息，请参阅[规划云管理网关](plan-cloud-management-gateway.md)。

## <a name="internet-based-client-management"></a>基于 Internet 的客户端管理

此方法依赖于面向 Internet 的站点系统服务器，为了进行管理，客户端会与该服务器通信。 此方法要求配置客户端和站点系统服务器，实现基于 Internet 的管理。

优点：

-   无云服务依赖关系。

-   无与云订阅关联的费用。

-   可完全控制提供服务的服务器和角色。

缺点：

-   需要额外的基础结构投资。

-   额外基础结构的日常管理费用和运营费用。

-   必须向 Internet 公开基础结构。

有关详细信息，请参阅[规划基于 Internet 的客户端管理](plan-internet-based-client-management.md)。
