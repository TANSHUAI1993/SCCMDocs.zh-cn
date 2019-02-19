---
title: 管理 Internet 上的客户端
titleSuffix: Configuration Manager
description: 了解如何通过 Configuration Manager 中的云管理网关和基于 Internet 的客户端管理来管理客户端。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5cac59462b037ecf857792d06b690e57ddcf6e89
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132793"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>使用 Configuration Manager 管理 Internet 上的客户端

适用范围：System Center Configuration Manager (Current Branch)

通常，Configuration Manager 中的多数托管计算机和服务器与执行管理功能的站点系统服务器物理上位于同一内部网络中。 但是，当客户端连接到 Internet 时，你可以在内部网络外对其进行管理。 此功能不需要客户端通过 VPN 连接到站点系统服务器。

Configuration Manager 提供两种方法来管理连接了 Internet 的客户端：

-   云管理网关

-   基于 Internet 的客户端管理


## <a name="cloud-management-gateway"></a>云管理网关

云管理网关可管理基于 Internet 的客户端。 它将 Microsoft Azure 云服务以及与该服务通信的新站点系统角色结合使用。 基于 Internet 的客户端使用该云服务与本地 Configuration Manager 进行通信。

#### <a name="advantages"></a>优点  

-   无需额外的基础结构投资。  

-   不会向 Internet 公开本地基础结构。  

-   运行服务的云虚拟机由 Azure 完全管理且免维护。  

-   可轻松在 Configuration Manager 控制台中进行设置和配置。  

#### <a name="disadvantages"></a>缺点  

-   云订阅费用。  

-   通过云服务发送的管理数据。  

有关详细信息，请参阅[规划云管理网关](plan-cloud-management-gateway.md)。  



## <a name="internet-based-client-management"></a>基于 Internet 的客户端管理

此方法依赖于面向 Internet 的站点系统服务器，为了进行管理，客户端会与这些服务器通信。 它要求配置客户端和站点系统服务器，实现基于 Internet 的管理。

#### <a name="advantages"></a>优点  

-   无云服务依赖关系。  

-   无与云订阅关联的费用。  

-   可完全控制提供服务的服务器和角色。  

#### <a name="disadvantages"></a>缺点  

-   需要额外的基础结构投资。  

-   额外基础结构的日常管理费用和运营费用。  

-   必须向 Internet 公开基础结构。  

有关详细信息，请参阅[规划基于 Internet 的客户端管理](plan-internet-based-client-management.md)。  
