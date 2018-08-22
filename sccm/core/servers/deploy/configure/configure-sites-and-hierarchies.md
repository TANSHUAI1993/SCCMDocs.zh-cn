---
title: 卸载站点和层次结构
titleSuffix: Configuration Manager
description: 查阅此清单以确保你考虑到会同时影响站点和层次结构的最常见配置。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 051958c5fa524c97de0e42784cdab73288a24b82
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383705"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>配置 Configuration Manager 的站点和层次结构

*适用范围：System Center Configuration Manager (Current Branch)*

在安装首个 Configuration Manager 站点或将附加站点添加到层次结构后，请使用此清单确保已考虑会同时影响站点和层次结构的最常见配置。  

以下配置说明适用于大多数部署：  

- 某些选项相互依赖，例如 Active Directory 林发现、边界和边界组。  

- 一些配置有默认值，无需更改配置即可使用，至少可以启动。  

- 边界组和分发点组等其他配置则需要进行配置之后才能使用。  

| 操作 | 详细信息 |  
|------------|-------------|  
| 配置基于角色的管理 | 分离管理分配，从而控制哪些管理用户可在 Configuration Manager 环境中查看和管理不同对象和数据。<br /><br /> 配置基于角色的管理与层次结构中的所有站点共享。   <br/><br/>有关详细信息，请参阅[配置基于角色的管理](/sccm/core/servers/deploy/configure/configure-role-based-administration)。 |  
| 将站点数据发布到 Active Directory 域服务 | 让客户端轻松查找服务并高效使用站点资源。<br /><br /> 首先[扩展 Active Directory 架构](/sccm/core/plan-design/network/extend-the-active-directory-schema)。 然后单独配置每个站点以[发布站点数据](/sccm/core/servers/deploy/configure/publish-site-data) |  
| 配置服务连接点 | 在层次结构的顶级站点上，计划安装和配置服务连接点。 有关详细信息，请参阅[关于服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。 |  
| 添加站点系统角色 | 为单独的站点安装一个或多个附加站点系统角色。 有关详细信息，请参阅[添加站点系统角色](/sccm/core/servers/deploy/configure/add-site-system-roles)。 |  
| 配置站点边界和边界组 | 指定定义 Intranet 上网络位置的边界，其中包含要管理的设备。 然后配置边界组，使处于这些网络位置的客户端可以查找 Configuration Manager 资源。 有关详细信息，请参阅[定义站点边界和边界组](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups)。 |  
| 配置分发点组 | 配置分发点的逻辑组可简化部署的管理。 有关详细信息，请参阅[管理分发点组](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage)。 |  
| 运行发现 | 运行发现可查看网络中的资源，包括网络基础结构、设备和用户。<br /><br /> 有关详细信息，请参阅[运行发现](/sccm/core/servers/deploy/configure/run-discovery)。 |  
| 为管理员添加冗余和容量 | 可以通过安装附加 SMS 提供程序和 Configuration Manager 控制台来扩展容量，以便管理员管理基础结构：<br /><br /> 安装其他 SMS 提供程序，以便为站点的控制台和 API 连接提供冗余。 有关详细信息，请参阅[管理 SMS 提供程序](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider)。<br /><br /> **安装附加 Configuration Manager 控制台**以提供访问其他管理用户的权限。 有关详细信息，请参阅[安装 Configuration Manager 控制台](/sccm/core/servers/deploy/install/install-consoles)。 |  
| 配置站点组件 | 配置每个站点中的站点组件，修改站点系统角色和站点状态报告的行为。 有关详细信息，请参阅[站点组件](/sccm/core/servers/deploy/configure/site-components)。 |  
| 创建自定义集合 | 使用站点发现的关于设备和用户的信息，创建对象的自定义集合以简化未来的管理任务。 有关详细信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections)。 |  
| 配置设置以管理高风险部署 | 在站点上配置设置，以便在管理员创建高风险部署时向其发出警告。 有关详细信息，请参阅[用于管理高风险部署的设置](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments)。 |  
| 配置管理点的数据库副本 | 配置数据库副本，以减少管理点在处理来自客户端的请求时放在站点数据库服务器上的处理器负载。 有关详细信息，请参阅[管理点的数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)。 |  
| 配置 SQL Server Always On 可用性组 | 将可用性组配置为高可用性和灾难恢复解决方案，以承载主站点和管理中心站点上的站点数据库。 有关详细信息，请参阅[高可用性站点数据库的 SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。 |  
| 修改站点之间的复制 | 请参阅[站点间数据传输](/sccm/core/servers/manage/data-transfers-between-sites)以了解以下主题：<br /><br /> 在辅助站点之间配置[基于文件的复制](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_fileroute)<br /><br /> 配置[数据库复制链接](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_Dblinks)<br /><br /> 配置[分布式视图](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews) |  
| 在被动模式下配置站点服务器 | 从版本 1806 开始，为每个主站点和管理中心站点配置处于被动模式的站点服务器。 此功能提供高度可用的站点服务器。 有关详细信息，请参阅[站点服务器高可用性](/sccm/core/servers/deploy/configure/site-server-high-availability)。 |  
