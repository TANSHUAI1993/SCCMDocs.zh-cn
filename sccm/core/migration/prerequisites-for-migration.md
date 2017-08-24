---
title: "迁移先决条件 | Microsoft Docs"
description: "了解支持的 Configuration Manager 版本、支持的源站点语言和迁移所需的配置。"
ms.custom: na
ms.date: 3/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: cd90f5462ac4bb4c0a2021e6d5dde65161b9c5f6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-migration-in-system-center-configuration-manager"></a>System Center Configuration Manager 中迁移的先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

若要从支持的源层次结构中进行迁移，必须拥有对每个适用的 Configuration Manager 源站点的访问权限以及 System Center Configuration Manager 目标站点内的权限，才能配置和运行迁移操作。  

 使用下列部分中的信息可帮助了解迁移支持的 Configuration Manager 版本以及必需的配置。  

-   [迁移支持的 Configuration Manager 版本](#BKMK_SupportedMigrationVersions)  

-   [迁移支持的源站点语言](#BKMK_SorceSiteLanguage)  

-   [迁移所需的配置](#BKMK_Required_Configurations)  

##  <a name="BKMK_SupportedMigrationVersions"></a> 迁移支持的 Configuration Manager 版本  
 可以从运行以下任何版本的 Configuration Manager 的源层次结构迁移数据：  

-   Configuration Manager 2007 SP2（对于迁移，不考虑使用源站点上的 Configuration Manager 2007 R2 或 R3。 只要源站点运行 SP2，就会支持将安装有 R2 或 R3 加载项的站点迁移到 System Center Configuration Manager）。  

-   System Center 2012 Configuration Manager SP2 或 System Center 2012 R2 Configuration Manager SP1。  

    > [!TIP]  
    >  除迁移外，还可以将运行 System Center 2012 Configuration Manager 的站点就地升级到 System Center Configuration Manager。  

-   相同或更低版本的 System Center Configuration Manager 的 System Center Configuration Manager 层次结构。  

  例如，如果具有运行 System Center Configuration Manager 1606 的目标层次结构，则可以使用迁移复制运行 1606 或 1602 版本的源层次结构中的数据。 但是不能迁移运行 1610 版的源层次结构中的数据。  


##  <a name="BKMK_SorceSiteLanguage"></a> 迁移支持的源站点语言  
 在 Configuration Manager 层次结构之间迁移数据时，数据将采用 System Center Configuration Manager 的语言中性格式存储在目标层次结构中。 由于 Configuration Manager2007 不采用语言中性格式存储数据，因此在从 Configuration Manager2007 迁移的过程中，迁移过程必须将对象转换为此格式。 因此，迁移只支持安装有以下语言的 Configuration Manager 2007 源站点：  

-   英语  

-   法语  

-   德语  

-   日语  

-   朝鲜语  

-   俄语  

-   简体中文  

-   繁体中文  

从 System Center 2012 Configuration Manager 或 System Center Configuration Manager 层次结构中迁移数据时，没有源站点语言限制。 源站点数据库中的对象已采用语言中性格式。  

##  <a name="BKMK_Required_Configurations"></a> 迁移所需的配置  
下面列出了使用迁移所需的配置以及迁移操作：  

-   **在 Configuration Manager 控制台中配置、运行和监视迁移：**  

     在目标站点中，必须为你的帐户分配基于角色的管理安全角色“基础结构管理员” 。 此安全角色授予用于管理所有迁移操作的权限，这些操作包括创建迁移作业、清理、监视以及共享和升级分发点的操作。  

-   **数据收集：**  

     要使目标站点能够收集数据，你必须配置以下两个源站点访问帐户以与每个源站点一起使用：  

    -   **源站点帐户：** 此帐户用于访问源站点的 SMS 提供程序。  

        -   对于 Configuration Manager2007 SP2 源站点，此帐户需要对所有源站点对象具有“读取”权限。  

        -   对于 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源站点，此帐户需要对所有源站点对象具有“读取”权限，可通过使用基于角色的管理向帐户授予此权限。 有关如何使用基于角色的管理的信息，请参阅 [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)。  

    -   **源站点数据库帐户：** 此帐户用于访问源站点的 SQL Server 数据库，并需要源站点数据库的 **Connect**、 **Execute**和 **Select** 权限。  

    你可以在配置新的源层次结构、其他源站点的数据收集或在为源站点重新配置凭据时配置这些帐户。 这些帐户可以使用域用户帐户，或者你可以指定目标层次结构的顶层站点的计算机帐户。  

    > [!IMPORTANT]  
    >  如果为任一访问帐户使用 Configuration Manager 计算机帐户，请确保此帐户是源站点所在域中“分布式 COM 用户”安全组的成员。  

    在收集数据时，将使用以下网络协议和端口：  

    -   NetBIOS/SMB - 445 (TCP)  

    -   RPC (WMI) - 135 (TCP)  

    -   SQL Server - 源站点数据库和目标站点数据库同时使用的 TCP 端口。  

-   **迁移软件更新：**  

     在迁移软件更新之前，你必须配置包含软件更新点的目标层次结构。 有关详细信息，请参阅[规划软件更新迁移](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates)。  

-   **共享分发点：**  

     要成功共享源站点中的任何分发点，目标层次结构中的至少一个主站点或管理中心站点必须为客户端请求使用与源站点一样的端口号。 有关客户端请求端口的信息，请参阅[如何在 System Center Configuration Manager 中配置客户端通信端口](../../core/clients/deploy/configure-client-communication-ports.md)  

     对于每个源站点，只会共享在使用 FQDN 配置的站点系统服务器上安装的分发点。  

     此外，要共享 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源站点中的分发点，“源站点帐户”（此帐户访问源站点服务器的 SMS 提供程序）必须具有对源站点上“站点”对象的“修改”权限。 通过使用基于角色的管理来向帐户授予此权限。 有关如何使用基于角色的管理的信息，请参阅 [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)。  


-   **升级或重新分配分发点：**  

     配置为从源站点的 SMS 提供程序中收集数据的“源站点访问帐户”  必须拥有以下权限：  

    -   若要升级 Configuration Manager2007 分发点，该帐户需要拥有对 Configuration Manager2007 站点服务器上“站点”类的“读取”、“执行”和“删除”权限，才能成功删除 Configuration Manager2007 源站点中的分发点  

    -   若要重新分配 System Center 2012 Configuration Manager 或 System Center Configuration Manager 分发点，该帐户必须对源站点上的“站点”对象具有“修改”权限。 通过使用基于角色的管理来向帐户授予此权限。 有关如何使用基于角色的管理的信息，请参阅 [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)。  

     若要成功将分发点升级或重新分配到新层次结构，为源层次结构中用于管理分发点的站点上的客户端请求配置的端口必须与为将用于管理分发点的目标站点上的客户端请求配置的端口匹配。 有关客户端请求端口的信息，请参阅[如何在 System Center Configuration Manager 中配置客户端通信端口](../../core/clients/deploy/configure-client-communication-ports.md)。  
