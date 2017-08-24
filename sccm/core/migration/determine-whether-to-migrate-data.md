---
title: "选择要迁移的内容 | Microsoft Docs"
description: "了解可以迁移的数据以及不能迁移到 System Center Configuration Manager 的数据。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9dc5f6c9f58e1fc33b2dc9dd76737ae23af81993
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="determine-whether-to-migrate-data-to-system-center-configuration-manager"></a>确定是否将数据迁移到 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中，迁移提供了一个进程，用于将从 Configuration Manager 的受支持版本中创建的数据和配置迁移到新的层次结构。  可用它来执行以下操作：  

-   将多个层次结构合为一个。  

-   将数据和配置从实验室部署移动到生产部署中。

-   从没有指向 System Center Configuration Manager 的升级路径的早期版本 Configuration Manager（如 Configuration Manager 2007）或是从 System Center 2012 Configuration Manager（支持指向 System Center Configuration Manager 的升级路径）移动数据和配置。  

除了分发点站点系统角色和承载分发点的计算机外，没有基础结构（包括站点、站点系统角色或承载站点系统角色的计算机）会迁移、传输或可在层次结构之间共享。  

 尽管你无法迁移服务器基础结构，但可以在层次结构之间迁移 Configuration Manager 客户端。 客户端迁移涉及将客户端使用的数据从源层次结构迁移到目标层次结构，然后将安装或重新分配客户端软件以便客户端随后可向新层次结构报告。

将客户端安装到新层次结构并且客户端提交其数据后，其唯一的 Configuration Manager ID 可帮助 Configuration Manager 将以前迁移的数据与每台客户端计算机关联。  

 迁移提供的功能有助于维护在配置和部署中进行的投资，同时使用户能够充分利用在 System Center 2012 Configuration Manager 中首次引入且在 System Center Configuration Manager 中继续使用的产品核心更改。 这些更改包括使用更少的站点和资源的简化 Configuration Manager 层次结构，以及通过使用运行于 64 位硬件上的本机 64 位代码改善了处理。  

 有关迁移支持的 Configuration Manager 的版本信息，请参阅 [System Center Configuration Manager 中迁移的先决条件](../../core/migration/prerequisites-for-migration.md)。  

 下列部分可帮助规划可迁移或无法迁移的数据：  

-   [可迁移到 System Center Configuration Manager 的数据](#Can_Migrate)  

-   [无法迁移到 System Center Configuration Manager 的数据](#Cannot_migrate)  

##  <a name="Can_Migrate"></a>可迁移到 System Center Configuration Manager 的数据  
 迁移可在支持的 Configuration Manager 层次结构之间迁移大多数对象。 必须对从支持的 Configuration Manager 2007 版本中迁移的某些对象实例进行修改，以符合 System Center 2012 Configuration Manager 架构和对象格式。

这些修改不影响源站点数据库中的数据。 从受支持版本的 System Center 2012 Configuration Manager 或 System Center Configuration Manager 迁移的对象无需修改。  

 下面是基于源层次结构中的 Configuration Manager 版本可迁移的对象。 某些对象（与查询）不会迁移。 如果要继续使用这些不迁移的对象，你必须在新层次结构中重新创建它们。 当在新层次结构中管理客户端时，会在该层次结构中自动重新创建其他对象（包括某些客户端数据）。  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-system-center-configuration-manager-current-branch"></a>可以从 System Center 2012 Configuration Manager 或 System Center Configuration Manager Current Branch 迁移的对象

-   播发  

-   适用于 System Center 2012 Configuration Manager 及更高版本的应用程序  

-   适用于 System Center 2012 Configuration Manager 及更高版本的 App-V 虚拟环境  

-   资产智能自定义项  

-   边界  

-   集合：若要从支持的 System Center 2012 Configuration Manager 或 System Center Configuration Manager 版本迁移集合，可以使用对象迁移作业。  

-   符合性设置：  

    -   配置基线  

    -   配置项目  

-   操作系统部署：  

    -   启动映像  

    -   驱动程序包  

    -   驱动程序  

    -   映像  

    -   包  

    -   任务序列  

-   搜索结果：保存的搜索条件  

-   软件更新：  

    -   部署  

    -   部署包  

    -   模板  

    -   软件更新列表  

-   软件分发包  

-   软件计数规则  

-   虚拟应用程序包  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>可以从 Configuration Manager 2007 SP2 迁移的对象

-   播发  

-   适用于 System Center 2012 Configuration Manager 及更高版本的应用程序  

-   适用于 System Center 2012 Configuration Manager 及更高版本的 App-V 虚拟环境  

-   资产智能自定义项  

-   边界  

-   集合：可使用集合迁移作业从支持的 Configuration Manager 2007 版本迁移集合。  

-   符合性设置（在 Configuration Manager 2007 中称为所需的配置管理）：  

    -   配置基线  

    -   配置项目  

-   操作系统部署：  

    -   启动映像  

    -   驱动程序包  

    -   驱动程序  

    -   映像  

    -   包  

    -   任务序列  

-   搜索结果：搜索文件夹  

-   软件更新：  

    -   部署  

    -   部署包  

    -   模板  

    -   软件更新列表  

-   软件分发包  

-   软件计数规则  

-   虚拟应用程序包  

##  <a name="Cannot_migrate"></a>不可迁移到 System Center Configuration Manager 的数据  
 你无法迁移下列类型的对象：  

-   AMT 客户端设置信息  

-   客户端上的文件，包括：  

    -   客户端清单和历史记录数据  

    -   客户端缓存中的文件  

-   查询  

-   Configuration Manager 2007 安全权限以及站点和对象的实例  

-   SQL Server Reporting Services 中的 Configuration Manager 2007 报表  

-   Configuration Manager 2007 Web 报表  

-   System Center 2012 Configuration Manager 和 System Center Configuration Manager 报表  

-   System Center 2012 Configuration Manager 和 System Center Configuration Manager 基于角色的管理：  

    -   安全角色  

    -   安全作用域  
