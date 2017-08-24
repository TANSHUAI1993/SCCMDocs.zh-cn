---
title: "配置站点 | Microsoft Docs"
description: "查阅此清单以确保你考虑到会同时影响站点和层次结构的最常见配置。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: "15"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 862f420c063cb44c419d4904fbb4696efb739758
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>配置 System Center Configuration Manager 的站点和层次结构

*适用范围：System Center Configuration Manager (Current Branch)*

在安装首个 System Center Configuration Manager 站点或将附加站点添加到层次结构后，请使用以下清单确保已考虑会同时影响站点和层次结构的最常见配置。  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>全新站点和附加站点的常见配置清单  
请记住有关配置的以下说明，这些说明适用于大多数部署：

-   某些选项相互依赖，例如 Active Directory 林发现、边界和边界组。  

-   一些配置有默认值，你可以使用这些默认值而不进行配置更改，至少暂时可以这样做。  

-   如边界组和分发点组等附加配置则需要你进行配置，之后才能使用它们。  

|操作|详细信息|  
|------------|-------------|  
|配置基于角色的管理|分离管理分配，从而控制哪些管理用户可在 Configuration Manager 环境中查看和管理不同对象和数据。<br /><br /> 配置基于角色的管理与层次结构中的所有站点共享。   <br/><br/>有关详细信息，请参阅[为 System Center Configuration Manager 配置基于角色的管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)。|  
|将站点数据发布到 Active Directory 域服务 (AD DS)|让客户端轻松查找服务并高效使用站点资源。<br /><br /> 必须首先[扩展 System Center Configuration Manager 的 Active Directory 架构](../../../../core/plan-design/network/extend-the-active-directory-schema.md)，然后每个站点必须被单独配置为[发布 System Center Configuration Manager 的站点数据](../../../../core/servers/deploy/configure/publish-site-data.md)|  
|配置服务连接点|在层次结构的顶层站点上，计划安装和配置服务连接点。 有关详细信息，请参阅[关于 System Center Configuration Manager 服务连接点](../../../../core/servers/deploy/configure/about-the-service-connection-point.md)。|  
|添加站点系统角色|为单独的站点安装一个或多个附加站点系统角色。  有关详细信息，请参阅[添加 System Center Configuration Manager 的站点系统角色](../../../../core/servers/deploy/configure/add-site-system-roles.md)。|  
|配置站点边界和边界组|指定定义 Intranet 上网络位置的边界，其中包含要管理的设备。 然后配置边界组，使处于这些网络位置的客户端可以查找 Configuration Manager 资源。 有关详细信息，请参阅[为 System Center Configuration Manager 定义站点边界和边界组](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。|  
|配置分发点组|配置分发点的逻辑组可简化部署的管理。 有关详细信息，请参阅[为 System Center Configuration Manager 安装和配置分发点](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md)中的[管理分发点组](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)。|  
|运行发现|运行发现可查看网络中的资源，其中包括网络基础结构、设备和用户。<br /><br /> 有关详细信息，请参阅 [Run discovery for System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md)。|  
|为管理基础结构的管理员添加冗余和容量|可以通过安装附加 SMS 提供程序和 Configuration Manager 控制台来扩展容量，以便管理员管理基础结构：<br /><br /> **安装附加 SMS 提供程序**可提供冗余，以便联系点管理站点和层次结构。 有关详细信息，请参阅[修改 System Center Configuration Manager 基础结构](../../../../core/servers/manage/modify-your-infrastructure.md)中的[管理 SMS 提供程序](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)。<br /><br /> **安装附加 Configuration Manager 控制台**以提供访问其他管理用户的权限。 有关详细信息，请参阅[安装 Configuration Manager 控制台](../../../../core/servers/deploy/install/install-consoles.md)。|  
|配置站点组件|配置每个站点中的站点组件，修改站点系统角色和站点状态报告的行为。 有关详细信息，请参阅 [Site components for System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md)。|  
|创建自定义集合|使用发现的关于设备和用户的信息，创建对象的自定义集合以简化未来的管理任务。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中创建集合](../../../../core/clients/manage/collections/create-collections.md)。|  
|配置设置以管理高风险部署|在站点中配置设置，这些设置会在管理用户创建高风险任务序列部署时警告他们。  有关详细信息，请参阅[用于管理 System Center Configuration Manager 的高风险部署的设置](../../../../protect/understand/settings-to-manage-high-risk-deployments.md)。|  
|配置管理点的数据库副本|配置数据库副本，以减少管理点在处理来自客户端的请求时放在站点数据库服务器上的 CPU 负载。 有关详细信息，请参阅 [System Center Configuration Manager 管理点的数据库副本](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。|  
|配置 SQL Server AlwaysOn 可用性组以承载站点数据库|从版本 1602 开始，可将可用性组配置为高可用性和灾难恢复解决方案，以承载主站点和管理中心站点上的站点数据库。 有关详细信息，请参阅[通过 SQL Server AlwaysOn 实现适用于 System Center Configuration Manager 的高可用性站点数据库](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。|  
|修改站点之间的复制|请参阅 [System Center Configuration Manager 中的站点间数据传输](../../../../core/servers/manage/data-transfers-between-sites.md)以了解有关以下主题：<br /><br /> 在辅助站点之间配置[基于文件的复制](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute)<br /><br /> 配置[数据库复制链接](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> 配置[分布式视图](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  
