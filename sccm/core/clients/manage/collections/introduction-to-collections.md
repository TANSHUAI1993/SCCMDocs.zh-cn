---
title: "集合简介 | Microsoft Docs"
description: "获取使用 System Center Configuration Manager 中的集合的简介。"
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: "8"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 547d231d48ccbc8241e9f1f8f71e3750b266b73e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的集合简介

*适用范围：System Center Configuration Manager (Current Branch)*

集合有助于将资源安排到可管理单位。 你可以创建集合来满足客户端管理需求，以及一次性在多个资源上执行操作。 

大多数管理任务依赖于或要求使用一个或多个集合。 尽管可以使用所有系统的内置集合，但将其用于管理任务并不是一种最佳做法。 创建自定义集合来更明确地标识某个任务的设备或用户。  

 内置和自定义集合会显示在 Configuration Manager 控制台中“资产和符合性”工作区内的“用户集合”和“设备集合”节点中。  

 最近查看过的集合会显示在“资产和符合性”工作区内的“用户”节点和“设备” 节点中。  

以下是集合使用的一些示例：  

|操作|示例|  
|---------|-------|  
|将资源分组|可以创建对基于组织层次结构的资源进行分组的集合。<br /><br /> 例如，可以创建位于伦敦总部 Active Directory 组织单位 (OU) 中的所有计算机的集合。 有关如何创建此类型的集合的详细信息，请参阅[如何在 System Center Configuration Manager 中创建集合](../../../../core/clients/manage/collections/create-collections.md)。<br /><br /> 然后可以将此集合用于某些操作，如配置 Endpoint Protection 设置、配置设备电源管理设置或安装 Configuration Manager 客户端。|  
|[应用程序部署]|可以创建未安装 Microsoft Office 2013 的计算机集合，然后将它部署到该集合中的所有计算机。<br /><br /> 你也可以使用应用程序要求来执行此任务。 有关详细信息，请参阅[如何使用 System Center Configuration Manager 创建应用程序](../../../../apps/deploy-use/create-applications.md)。|  
|[管理客户端设置](../../../../core/clients/deploy/about-client-settings.md)|尽管 Configuration Manager 中的默认客户端设置适用于所有设备和所有用户，你可以创建适用于某个设备集合或用户集合的自定义客户端设置。<br /><br /> 例如，如果想要在几乎所有设备上具有远程控制，需配置默认客户端设置以允许远程控制，然后配置不允许远程控制的自定义客户端设置，并将其部署到例外客户端集合中。 |  
|[电源管理](../power/introduction-to-power-management.md)|可以配置每个集合的特定电源设置。|  
|[基于角色的管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|使用集合来控制哪些用户组可以访问 Configuration Manager 控制台中的各种功能。|  
|[维护时段](../../../../core/clients/manage/collections/use-maintenance-windows.md)|借助维护时段，可以定义对设备集合成员进行各种 Configuration Manager 操作的时间段。 |  


## <a name="collection-types-in-configuration-manager"></a>Configuration Manager 中的集合类型  
 Configuration Manager 具有可用于常见操作的内置集合，你也可以创建自定义集合。   

### <a name="built-in-collections"></a>内置集合  
 默认情况下，Configuration Manager 包括以下集合，不能对它们进行修改。  

|**集合名称**|描述|  
|-------------------------|-----------------|  
|**所有用户组**|包含通过使用 Active Directory 安全组发现找到的用户组。|  
|**所有用户**|包含通过使用 Active Directory 用户发现找到的用户。|  
|**所有用户和用户组**|包含所有用户集合和所有用户组集合。 此集合包含最大范围的用户和用户组资源。|  
|**所有台式机和服务器客户端**|包含安装有 Configuration Manager 客户端的服务器和桌面设备。 通过检测信号发现维护成员身份。|  
|**所有移动设备**|包含由 Configuration Manager 管理的移动设备。 成员身份仅适用于成功分配到某站点或由 Exchange Server 连接器发现的那些移动设备。|  
|**所有系统**|包含所有台式机和服务器客户端、所有移动设备、所有未知计算机集合以及通过 Microsoft Intune 注册的所有移动设备。 此集合包含最大范围的设备资源。|  
|**所有未知计算机**|包含多个计算机平台的通用计算机记录。 你可以使用此集合通过任务序列和 PXE 启动、可启动媒体或预留媒体来部署操作系统。|  

### <a name="custom-collections"></a>自定义集合  
 在 Configuration Manager 中创建自定义集合时，由一个或多个集合规则确定该集合的成员身份，如[如何在 System Center Configuration Manager 中创建集合](../../../../core/clients/manage/collections/create-collections.md)中所述。 

