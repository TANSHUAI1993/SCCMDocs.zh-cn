---
title: "集合简介 | System Center Configuration Manager"
description: "获取使用 System Center Configuration Manager 中的集合的简介。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: 8
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 47574218dec5069205f9dba5608c6f136fb032bc


---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的集合简介

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的集合使用户可以将资源组织到可管理的单元，从而创建在逻辑上表示要执行的任务类型的组织结构。 集合还用于一次性在多个资源上执行 Configuration Manager 操作。 下表显示了如何使用 Configuration Manager 中的集合的示例：  

|操作|示例|  
|---------|-------|  
|将资源分组|可以创建对基于组织层次结构的资源进行逻辑分组的集合。<br /><br /> 例如，可以创建位于伦敦总部 Active Directory 组织单位 (OU) 中的所有计算机的集合。 有关如何创建此类型的集合的详细信息，请参阅[如何在 System Center Configuration Manager 中创建集合](../../../../core/clients/manage/collections/create-collections.md)。<br /><br /> 然后可以使用此集合来执行某些操作，如配置 Endpoint Protection 设置、配置设备电源管理设置或安装 Configuration Manager 客户端。|  
|应用程序部署|可以创建未安装 Microsoft Office 2013 的计算机集合，然后将此软件部署到该集合中的所有计算机。<br /><br /> 你也可以使用应用程序要求来执行此任务。 有关详细信息，请参阅[如何使用 System Center Configuration Manager 创建应用程序](../../../../apps/deploy-use/create-applications.md)。|  
|管理客户端设置|尽管 Configuration Manager 中的默认客户端设置适用于所有设备和所有用户，你可以创建适用于某个设备集合或用户集合的自定义客户端设置。<br /><br /> 例如，如果你想要在几乎所有设备上具有远程控制，需配置默认客户端设置以允许远程控制，然后配置不允许远程控制的自定义客户端设置。 将这些自定义客户端设置部署到包含将不使用远程控制的计算机的集合。<br /><br /> 有关如何将集合用于客户端设置的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../../../core/clients/deploy/about-client-settings.md)。|  
|电源管理|对于创建的每个集合，可以配置电源设置，如当集合中的计算机处于非活动状态时多长时间会进入睡眠模式。<br /><br /> 有关如何使用集合与电源管理的详细信息，请参阅[电源管理简介](../power/introduction-to-power-management.md)。|  
|基于角色的管理|可以结合基于角色的管理来使用集合，控制哪些用户组可以访问 Configuration Manager 控制台中的各种功能。<br /><br /> 有关如何配置集合以实现基于角色的管理的详细信息，请参阅[为 System Center Configuration Manager 配置基于角色的管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)。|  
|维护时段|维护时段提供了一种方法，利用该方法，管理用户可以定义对设备集合成员进行各种 Configuration Manager 操作的时间段。 可以使用维护时段来帮助确保在不会影响组织工作效率的时间段进行客户端配置更改。<br /><br /> 有关维护时段的详细信息，请参阅[如何在 System Center Configuration Manager 中使用维护时段](../../../../core/clients/manage/collections/use-maintenance-windows.md)。|  

 大多数管理任务依赖于使用一个或多个集合。 例如，必须标识一个软件更新部署的集合，才可以将软件更新部署到设备。 尽管可以使用所有系统的内置集合，使用此集合来管理任务并不是一种最佳做法。 在几乎所有测试环境中，通常可利用自己创建的自定义集合来更明确地标识要管理的设备和用户。  

 内置和自定义集合会显示在 Configuration Manager 控制台中“资产和符合性”工作区内的“用户集合”和“设备集合”节点中。  

 最近查看过的集合会显示在Configuration Manager 控制台中“资产和符合性”  工作区内的“用户”  节点和“设备”  节点中。  

## <a name="collection-types-in-configuration-manager"></a>Configuration Manager 中的集合类型  
 Configuration Manager 有一些可用于常见操作的内置集合。 此外，可以创建自己的集合，该集合对特定于你业务需求的资源进行分组的。  

### <a name="built-in-collections"></a>内置集合  
 默认情况下，Configuration Manager 包括以下集合，不能对它们进行修改。  

|**集合名称**|描述|  
|-------------------------|-----------------|  
|**所有用户组**|包含通过使用 Active Directory 安全组发现找到的用户组。|  
|**所有用户**|包含通过使用 Active Directory 用户发现找到的用户。|  
|**所有用户和用户组**|包含所有用户集合和所有用户组集合。 此集合不能进行修改，其包含最大范围的用户和用户组资源。|  
|**所有台式机和服务器客户端**|包含安装有 Configuration Manager 客户端的服务器和桌面设备。 通过检测信号发现维护成员身份。|  
|**所有移动设备**|包含由 Configuration Manager 管理的移动设备。 成员身份仅适用于成功分配到某站点或由 Exchange Server 连接器发现的那些移动设备。|  
|**所有系统**|包含所有台式机和服务器客户端、所有移动设备、所有未知计算机集合以及通过 Microsoft Intune 注册的所有移动设备。<br /><br /> 此集合不能进行修改，其包含最大范围的设备资源。|  
|**所有未知计算机**|包含多个计算机平台的通用计算机记录。 你可以使用此集合通过任务序列和 PXE 启动、可启动媒体或预留媒体来部署操作系统。|  

### <a name="custom-collections"></a>自定义集合  
 在 Configuration Manager 中创建自定义集合时，由一个或多个集合规则确定该集合的成员身份。 有关如何配置集合规则的信息，请参阅[如何在 System Center Configuration Manager 中创建集合](../../../../core/clients/manage/collections/create-collections.md)。 你可以使用以下四种规则：  

#### <a name="direct-rule"></a>直接规则  
 直接规则使你可以选择要作为成员添加到集合的用户或计算机。 此规则使你可以直接控制哪些资源是集合的成员。 该成员身份不会自动更改，除非从 Configuration Manager 中删除资源。 Configuration Manager 必须先发现资源或是用户必须先导入资源，然后才能将它们添加到直接规则集合。 直接规则集合的管理开销高于查询规则集合，因为你必须手动对此集合类型进行更改。  

#### <a name="query-rule"></a>查询规则  
 查询规则基于 Configuration Manager 按计划运行的查询来动态更新集合的成员身份。 例如，可以创建一个用户集合，其中的用户是 Active Directory 域服务中的人力资源组织单位的成员。 与直接规则集合不同，此集合成员身份会在向人力资源组织单位添加新用户或从中删除用户时自动更新。 查询规则通过直接规则删除手动向该集合添加设备的管理开销。 但是，它们降低了你对向该集合添加哪些计算机的控制。 基于查询的规则示例包括：  

-   指定 OU 中的所有用户  

-   运行 Windows 8 的所有计算机  

-   具有超过 20 GB 可用磁盘空间的所有计算机  

#### <a name="include-collections-rule"></a>包括集合规则  
 包括集合规则允许包括 Configuration Manager 集合中其他集合的成员。 如果所含集合的成员身份更改，Configuration Manager 会按计划更新当前集合的成员身份。  

#### <a name="exclude-collections-rule"></a>排除集合规则  
 通过排除集合规则，可从一个 Configuration Manager 集合中排除其他集合的成员。 如果已排除的集合的成员身份更改，Configuration Manager 会按计划更新当前集合的成员身份。  

> [!NOTE]  
>  如果集合同时包含包括集合和排除集合规则，并且存在冲突，则排除规则优先于包括规则。  

## <a name="incremental-collection-updates"></a>增量集合更新  
 启用集合的增量更新时，Configuration Manager 会定期从以前的集合评估中扫描新资源或更改的资源，并用这些资源更新集合成员身份，而与完整的集合评估无关。 默认情况下，启用增量集合更新时，它将每 5 分钟运行一次，在没有完整的集合评估开销下帮助用户使集合保持为最新。  

> [!NOTE]  
>  创建一个新的集合时，增量更新在默认情况下处于禁用状态。  



<!--HONumber=Nov16_HO1-->


