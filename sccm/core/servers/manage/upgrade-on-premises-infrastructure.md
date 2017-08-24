---
title: "升级本地基础结构 | Microsoft Docs"
description: "了解如何升级基础结构（例如 SQL Server）和站点系统的站点操作系统。"
ms.custom: na
ms.date: 06/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 188b7f2537dd0e569a5c00995620124512cf311b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>升级支持 System Center Configuration Manager 的本地基础结构

*适用范围：System Center Configuration Manager (Current Branch)*

使用本主题中的信息来帮助升级运行 System Center Configuration Manager 的服务器基础结构。  

 - 如果想要从早期版本的 Configuration Manager 升级到 System Center Configuration Manager，请参阅[升级到 System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)。

- 如果想要将 System Center Configuration Manager 基础结构更新为新版本，请参阅 [System Center Configuration Manager 的更新](/sccm/core/servers/manage/updates)。

##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a>升级站点系统的操作系统  
 Configuration Manager 在以下情况中支持托管站点服务器的服务器操作系统和托管任何站点系统角色的远程服务器操作系统的就地升级：  

-   如果生成的 Windows 服务包级别仍受 Configuration Manager 支持，则会就地升级到更高版本的 Windows Server 服务包。  
-   就地升级：
    - 从 Windows Server 2012 R2 到 Windows Server 2016（[查看其他详细信息](#bkmk_2016)）。
    - Windows Server 2012 到 Windows Server 2016（[请参阅其他详细信息](#bkmk_2016)）。
    - 从 Windows Server 2012 到 Windows Server 2012 R2（[查看其他详细信息](#bkmk_2012r2)）。
    - 使用 Configuration Manager 版本 1602 或更高版本时，还支持将 Windows Server 2008 R2 升级到 Windows Server 2012 R2（[请参阅其他详细信息](#bkmk_from2008r2)）。

    > [!WARNING]  
    >  升级到 Windows Server 2012 R2 之前， *必须从服务器中卸载 WSUS 3.2* 。  
    >   
    >  有关此关键步骤的信息，请参阅 Windows Server 文档中 [Windows Server Update Services 概述](https://technet.microsoft.com/library/hh852345.aspx)中的“新增和更改的功能”部分。  

若要升级服务器，请使用要升级到的目标操作系统所提供的升级过程。  参阅以下内容：
  -  Windows Server 文档中的 [Windows Server 2012 R2 的升级选项](https://technet.microsoft.com/library/dn303416.aspx)。  
  - Windows Server 文档中的 [Upgrade and conversion options for Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths)（Windows Server 2016 升级和转换选项）。

### <a name="bkmk_2016"></a>  将 Windows Server 2012 或 Windows Server 2012 R2 升级到 2016
将 Windows Server 2012 或 Windows Server 2012 R2 升级到 Windows Server 2016 时，下列规则适用：


**升级之前：**  
-   删除 System Center Endpoint Protection (SCEP) 客户端。 Windows Server 2016 具有内置的 Windows Defender，它会代替 SCEP 客户端。 SCEP 客户端的存在会阻止升级到 Windows Server 2016。

**升级之后：**
-   确保 Windows Defender 已启用、设置为自动启动且正在运行。
-   确保正在运行以下 Configuration Manager 服务：
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   确保针对以下站点系统角色，**Windows Process Activation** 和 **WWW/W3svc** 服务已启用、设置为自动启动且正在运行（升级期间会禁用这些服务）：
  -     站点服务器
  -     管理点
  -     应用程序目录 Web 服务点
  -     应用程序目录网站点

-   确保用于托管站点系统角色的每个服务器继续满足所有在该服务器上运行的[站点系统角色的所有先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。 例如，可能需要重新安装 BITS、WSUS 或为 IIS 配置特定设置。

-   恢复缺少的先决条件后，再次重启该服务器，以确保所有服务已启动并可操作。

**远程 Configuration Manager 控制台的已知问题：**  
将托管 SMS_Provider 实例的站点服务器或服务器升级到 Windows Server 2016 后，管理员用户可能无法将 Configuration Manager 控制台连接到该站点。 若要解决此问题，必须手动还原 WMI 中 SMS 管理员组的权限。 必须在此站点服务器以及每个托管 SMS_Provider 实例的远程服务器上设置权限：

1. 在适用的服务器上，打开 Microsoft 管理控制台 (MMC)，为“WMI 控件”添加管理单元，然后选择“本地计算机”。
2. 在 MMC 中，打开“WMI 控件(本地)”的“属性”，然后选择“安全”选项卡。
3. 展开“根”下的树形，选择“SMS”节点，然后选择“安全”。  确保“SMS 管理员”组具有下列权限：
  -     启用帐户
  -     远程启用
4. 在“SMS”节点下方的“安全”选项卡中，选择“site_&lt;sitecode>”节点，然后选择“安全”。 确保“SMS 管理员”组具有下列权限：
  -   执行方法
  -   提供程序写入
  -   启用帐户
  -   远程启用
5. 保存权限以还原 Configuration Manager 控制台的访问权限。

### <a name="bkmk_2012r2"></a> Windows Server 2012 到 Windows Server 2012 R2

**升级之前：**
-  不同于支持的其他方案，此方案升级前没有特别的注意事项。

**升级之后：**
  - 请确保针对以下站点系统角色，Windows 部署服务已启动，且正在运行（升级期间会停止该服务）：
    - 站点服务器
    - 管理点
    - 应用程序目录 Web 服务点
    - 应用程序目录网站点

  -     确保针对以下站点系统角色，**Windows Process Activation** 和 **WWW/W3svc** 服务已启用、设置为自动启动且正在运行（升级期间会禁用这些服务）：
    -   站点服务器
    -   管理点
    -   应用程序目录 Web 服务点
    -   应用程序目录网站点


  -     确保用于托管站点系统角色的每个服务器继续满足所有在该服务器上运行的[站点系统角色的所有先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。 例如，可能需要重新安装 BITS、WSUS 或为 IIS 配置特定设置。

  恢复缺少的先决条件后，再次重启该服务器，以确保所有服务已启动并可操作。

### <a name="bkmk_from2008r2"></a>  将 Windows Server 2008 R2 升级到 Windows Server 2012 R2
此操作系统升级方案需满足以下条件：  

**升级之前：**
-   卸载 WSUS 3.2。  
    将服务器操作系统升级到 Windows Server 2012 R2 之前，必须从服务器中卸载 WSUS 3.2。 有关此关键步骤的信息，请参阅 Windows Server 文档中 Windows Server 更新服务概述中的“新增和更改的功能”部分。

**升级之后：**
  - 请确保针对以下站点系统角色，Windows 部署服务已启动，且正在运行（升级期间会停止该服务）：
    - 站点服务器
    - 管理点
    - 应用程序目录 Web 服务点
    - 应用程序目录网站点


  -     确保针对以下站点系统角色，**Windows Process Activation** 和 **WWW/W3svc** 服务已启用、设置为自动启动且正在运行（升级期间会禁用这些服务）：
    -   站点服务器
    -   管理点
    -   应用程序目录 Web 服务点
    -   应用程序目录网站点


  -     确保每个托管站点系统角色的服务器将继续满足在该服务器上运行的[站点系统角色的所有先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。 例如，可能需要重新安装 BITS、WSUS 或为 IIS 配置特定设置。

  恢复缺少的先决条件后，再次重启该服务器，以确保所有服务已启动并可操作。


### <a name="unsupported-upgrade-scenarios"></a>不支持的升级方案
以下 Windows Server 升级方案经常被问及，但不受 Configuration Manager 支持：  

-   Windows Server 2008 到 Windows Server 2012 或更高版本  
-   Windows Server 2008 R2 到 Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a>升级 Configuration Manager 客户端的操作系统  
 以下情况中，Configuration Manager 支持就地升级 Configuration Manager 客户端的操作系统：  

-   如果生成的服务包级别仍受 Configuration Manager 支持，则会就地升级到更高版本的 Windows 服务包。  

-   从支持的版本到 Windows 10 的 Windows 就地升级。 有关详细信息，请参阅[使用 System Center Configuration Manager 将 Windows 升级到最新版本](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)。  

-   Windows 10 的内部版本到内部版本服务升级。  有关详细信息，请参阅[使用 System Center Configuration Manager 将 Windows 作为服务进行管理](../../../osd/deploy-use/manage-windows-as-a-service.md)。  

##  <a name="BKMK_SupConfigUpgradeDBSrv"></a>升级站点数据库服务器上的 SQL Server  
  Configuration Manager 在站点数据库服务器上支持将 SQL Server 从受支持的 SQL 版本就地升级。 本节中的 SQL Server 升级方案均受 Configuration Manager 支持，并且包括每个方案的要求。

 有关 Configuration Manager 支持的 SQL Server 版本的详细信息，请参阅[对 System Center Configuration Manager 的 SQL Server 版本支持](../../../core/plan-design/configs/support-for-sql-server-versions.md)。  

 **升级 SQL Server 的服务包版本：**    
 如果生成的 SQL Server 服务包级别仍受 Configuration Manager 支持，则 Configuration Manager 支持将 SQL Server 就地升级到更高的服务包版本。

 层次结构中有多个 Configuration Manager 站点时，每个站点可以运行不同的 SQL Server 的服务包版本，并且站点升级用于站点数据库的 SQL Server 的 Service Pack 版本没有顺序限制。

 **升级到新版本的 SQL Server：**   
 Configuration Manager 支持将 SQL Server 就地升级到以下版本：

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

升级托管站点数据库的 SQL Server 的版本时，必须在站点按以下顺序升级使用的 SQL Server 版本：

 1. 首先升级管理中心站点上的 SQL Server。
 2. 升级辅助站点，然后再升级辅助站点的父主站点。
 3. 最后升级父主站点。 这包括向管理中心站点报告的子主站点和是层次结构的顶层站点的独立主站点。

**SQL Server 基数估计级别和站点数据库：**   
从 SQL Server 早期版本升级站点数据库时，如果现有 SQL基数估计 (CE) 级别是此 SQL Server 实例允许的最小级别，则数据库会保留此级别。 使用兼容级别低于允许级别的数据库升级 SQL Server 会自动将数据库设置为 SQL Server 允许的最低兼容级别。

下表列出了 Configuration Manager 站点数据库的建议兼容级别：

|SQL Server 版本 | 受支持的兼容级别 |推荐级别|
|----------------|--------------------|--------|
| SQL Server 2016| 130, 120, 110, 100 | 130|
| SQL Server 2014| 120, 110, 100      | 110|

若要标识站点数据库使用的 SQL Server CE 兼容级别，请在站点数据库服务器上运行以下 SQL 查询：**SELECT name, compatibility_level FROM sys.databases**

 有关 SQL CE 兼容级别及其设置方法的详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)。


有关 SQL Server 的详细信息，请参阅 TechNet 上的 SQL Server 文档：
-   [升级到 SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110))
-   [升级到 SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  
-   [升级到 SQL Server 2016](https://technet.microsoft.com/library/bb677622(v=sql.130))



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>在站点数据库服务器上升级 SQL Server  

1.  停止站点上所有的 Configuration Manager 服务。  
2.  将 SQL Server 升级到支持的版本。  
3.  重新启动 Configuration Manager 服务。  

> [!NOTE]  
>  在管理中心站点上将使用的 SQL Server 版本从 Standard Edition 更改为 Datacenter 或 Enterprise Edition 时，限制层次结构支持的客户端数量的数据库分区不会更改。
