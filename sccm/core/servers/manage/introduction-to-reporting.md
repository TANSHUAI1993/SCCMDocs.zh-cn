---
title: "报告简介 | Microsoft Docs"
description: "了解在 Configuration Manager 中管理报表可使用的工具和资源集。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
caps.latest.revision: "7"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5846ca3c91626491b03b36dd17b454bb9382a8dc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的报表简介

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的报表提供了一套工具和资源，可帮助用户使用 SQL Server Reporting Services (SSRS) 的高级报表功能和 Reporting Services 报表生成器提供的丰富创作体验。 报表有助于收集、整理和显示组织中用户、硬件和软件清单、软件更新、应用程序、站点状态和其他 Configuration Manager 操作的相关信息。 “报表”为你提供了许多预定义的报表，你可以使用这些报表而不用做任何更改，或者可以进行修改以满足你的需求，并且，你可以创建自定义报表。 使用以下部分有助于在 Configuration Manager 中管理报表。  

##  <a name="BKMK_SQLServerReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services 提供大量可以使用的工具和服务以帮助你创建、部署和管理组织的报表，并且提供了编程功能，允许你扩展和自定义报表功能。 Reporting Services 是基于服务器的报表平台，它为各种数据源提供综合性报表功能。  

 Configuration Manager 将 SQL Server Reporting Services 用作其报表解决方案。 与 Reporting Services 的集成提供了以下优点：  

-   使用行业标准报告系统查询 Configuration Manager 数据库。  

-   使用 Configuration Manager 报表查看器或报表管理器显示报表，这是基于 Web 连接到报表的连接。  

-   提供高性能、可用性和可伸缩性。  

-   提供用户可订阅的报表的订阅；例如，经理可以订阅以每天自动通过电子邮件接收详述软件更新发布状态的报表。  

-   导出用户可以选择的各种常见格式的报表。  

 有关 Reporting Services 的详细信息，请参阅 SQL Server 2008 联机丛书中的 [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=212032) 。  

##  <a name="BKMK_ReportingServicesPoint"></a> Reporting Services 点  
 Reporting Services 点是安装在运行 Microsoft SQL Server Reporting Services 的服务器上的站点系统角色。 Reporting Services 点将 Configuration Manager 报表定义复制到 Reporting Services，基于报表类别创建报表文件夹，根据 Configuration Manager 管理用户基于角色的权限对报表文件夹和报表设置安全策略。 Reporting Services 点按 10 分钟的间隔连接到 Reporting Services 以重新应用更改的安全策略，例如通过使用报表管理器来应用。 有关如何规划和安装 Reporting Services 点的详细信息，请参阅以下文档：  

-   [规划 System Center Configuration Manager 中的报表](planning-for-reporting.md)  

-   [配置 System Center Configuration Manager 中的报表](configuring-reporting.md)  

##  <a name="BKMK_ConfigurationManagerReports"></a> Configuration Manager 报表  
 Configuration Manager 为 50 多个报表文件夹中的 400 多个报表提供报表定义，并在 Reporting Services 点安装过程中将其复制到 SQL Server Reporting Services 内的根报表文件夹。 这些报表显示在 Configuration Manager 控制台中，并根据报表类别在子文件夹中进行组织。 报表不会在 Configuration Manager 层次结构中向上或向下传播，它们只能针对创建报表的站点上的数据库运行。 但是，因为 Configuration Manager 在整个层次结构中复制全局数据，所以用户可以访问层次结构范围的信息。 当报表从站点数据库中检索数据时，它可以访问当前站点和子站点的站点数据，以及层次结构中每个站点的全局数据。 与其他 Configuration Manager 对象一样，管理用户必须具有合适的权限来运行或修改报表。 为了运行报表，管理用户必须具有对对象的“运行报表”  权限。 为了创建或修改报表，管理用户必须具有对对象的“修改报表”  权限。  

###  <a name="BKMK_CreatingReports"></a> 创建和修改报表  
 Configuration Manager 使用 Microsoft SQL Server 报表生成器作为创作和编辑基于模型和 SQL 的报表的专用工具。 在 Configuration Manager 控制台中创建或编辑报表时，会打开报表生成器。 有关管理报表的详细信息，请参阅 [System Center Configuration Manager 中报表的操作和维护](operations-and-maintenance-for-reporting.md)。  

###  <a name="BKMK_RunningReports"></a> 运行报表  
 在 Configuration Manager 控制台中运行报表时，报表查看器将会打开并连接到 Reporting Services。 指定任何所需报表参数后，那么 Reporting Services 会检索数据并在查看器中显示结果。 你也可以连接到 SQL Services Reporting Services，连接到站点的数据源，以及运行报表。  

###  <a name="BKMK_ReportPrompts"></a> 报表提示  
 Configuration Manager 中的报表提示或报表参数是可以在创建或修改报表时配置的报表属性。 系统创建报表提示以限制报表检索的数据或确定报表检索的目标数据。 只要提示名称唯一且只包含符合标识符的 SQL Server 规则的字母数字字符，报表就可以包含多个提示。  

 运行报表时，提示会请求输入所需参数的值，并根据该值检索报表数据。 例如，?特定计算机的计算机信息?  报表检索特定计算机的计算机信息，并提示管理用户输入计算机名称。 Reporting Services 将指定的值传递给在报表的 SQL 语句中定义的变量。  

###  <a name="BKMK_ReportLinks"></a> 报表链接  
 Configuration Manager 中的报表链接用于源报表，供管理用户轻松地访问其他数据，如关于源报表中每个项的更多详细信息。 如果目标报表需要运行一个或多个提示，则源报表必须包含一个具有每个提示的合适值的列。 你必须指定为提示提供值的列号。 例如，你可以将列出最近发现的计算机的报表链接至列出针对特定计算机接收的最近消息的列表。 创建链接时，你可以指定源报表中的列 2 包含计算机名称，这是一个必需的提示，用于提示输入目标报表。 运行源报表时，链接图标会出现在每个数据行的左边。 当你单击行上的图标时，报表查看器会针对该行传递指定列中的值，并将其作为显示目标报表所需的提示值。 可以将报表配置为只包含一个链接，该链接仅连接到单一目标资源。  

> [!WARNING]  
>  如果将目标报表移到其他报表文件夹，则目标报表的位置会发生更改。 系统未使用新位置自动更新源报表中的报表链接，此报表链接在源报表中将不工作。  

##  <a name="BKMK_ReportFolders"></a> 报表文件夹  
 System Center Configuration Manager 中的报表文件夹提供了一种对 Reporting Services 中存储的报表进行排序和筛选的方法。 当有许多报表要管理时，报表文件夹特别有用。 安装 Reporting Services 点时，报表将复制到 Reporting Services 并组织成 50 多个报表文件夹。 报表文件夹是只读的。 无法在 Configuration Manager 控制台中修改它们。  

##  <a name="BKMK_ReportSubscriptions"></a> 报表订阅  
 Reporting Services 中的报表订阅是一个定期请求，此请求用于请求在特定时间提供报表或者响应某个事件，并且采用你在订阅中指定的应用程序文件格式。 订阅提供按需运行报表的一种替代方法。 按需报表要求你在每次想要查看报表时有效地选择报表。 相比之下，订阅可用于进行计划，然后自动提供报表。  

 可以在 Configuration Manager 控制台中管理报表订阅。 它们是在报表服务器上处理的。 系统使用部署在服务器上的传递扩展插件分发订阅。 默认情况下，你可以创建订阅以将报表发送到共享文件夹或发送到电子邮件地址。 有关管理报表订阅的详细信息，请参阅 [System Center Configuration Manager 中报表的操作和维护](operations-and-maintenance-for-reporting.md)。  

##  <a name="BKMK_ReportBuilder"></a> 报表生成器  
 Configuration Manager 使用 Microsoft SQL Server Reporting Services 报表生成器作为创作和编辑基于模型和 SQL 的报表的专用工具。 启动操作在 Configuration Manager 控制台中创建或编辑报表时，会打开报表生成器。 首次创建或修改报表时，会自动安装报表生成器。 当运行或编辑报表时，会打开与安装的 SQL Server 版本关联的报表生成器版本。  

 报表生成器安装会为 20 多种语言添加支持。 运行报表生成器时，它会以本地计算机上运行的操作系统的语言来显示数据。 如果报表生成器不支持该语言，则会用英文显示数据。 报表生成器支持 SQL Server 2008 Reporting Services 的所有功能，包括以下功能：  

-   提供一个直观的报表创作环境，其外观与 Microsoft Office 的外观类似。  

-   提供了 SQL Server 2008 报表定义语言 (RDL) 的灵活报表布局。  

-   提供了各种形式的数据可视化，包括图表和仪表。  

-   提供了格式丰富的文本框。  

-   导出到 Microsoft Word 格式。  

 你还可以从 SQL Server Reporting Services 打开报表生成器。  

##  <a name="BKMK_ReportModels"></a> SQL Server Reporting Services 中的报表模型  
 Configuration Manager 中的 SQL Reporting Services 使用报表模型帮助管理用户从数据库中选择要包含在基于模型的报表中的项。 对于生成报表的管理用户，报表模型仅公开指定的视图和项以供选择。 要创建基于模型的报表，至少必须有一个报表模型可用。 报表模型具有以下功能：  

-   你可以提供数据库字段和视图逻辑业务名称，以便于生成报表。 生成报表不需要了解数据库结构。  

-   项目可以进行逻辑分组。  

-   你可以定义项之间的关系。  

-   你可以保护模型元素，以便管理用户只能看到他们有权查看的数据。  

 虽然 Configuration Manager 提供了样本报表模型，但也可以定义报表模型来满足自己的业务要求。 有关如何创建报表模型的详细信息，请参阅[在 SQL Server Reporting Services 中对 System Center Configuration Manager 创建自定义报表模型](creating-custom-report-models-in-sql-server-reporting-services.md)。  

## <a name="next-steps"></a>后续步骤
[规划报表](planning-for-reporting.md)
