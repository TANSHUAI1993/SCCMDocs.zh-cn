---
title: 升级本地基础结构
titleSuffix: Configuration Manager
description: 了解如何升级基础结构（例如 SQL Server）和站点系统的操作系统。
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc433d63eb647ef7a0a88ada212f949783ac25c0
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "34474245"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>升级支持 System Center Configuration Manager 的本地基础结构

*适用范围：System Center Configuration Manager (Current Branch)*

使用本文中的信息来帮助升级运行 Configuration Manager 的服务器基础结构。  

 - 如果想要从早期版本的 Configuration Manager 升级到 System Center Configuration Manager（当前分支），请参阅[升级到 System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)。

- 如果想要将 System Center Configuration Manager （当前分支）基础结构更新为新版本，请参阅 [System Center Configuration Manager 的更新](/sccm/core/servers/manage/updates)。



##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a> 升级站点系统的操作系统  
 Configuration Manager 在以下情况中支持托管站点服务器的服务器操作系统 (OS) 和托管任何站点系统角色的远程服务器操作系统的就地升级：  

-   如果生成的 Windows 服务包级别仍受 Configuration Manager 支持，则会就地升级到更高版本的 Windows Server 服务包。  
-   就地升级：
    - 从 Windows Server 2012 R2 到 Windows Server 2016（[查看其他详细信息](#bkmk_2016)）。
    - Windows Server 2012 到 Windows Server 2016（[请参阅其他详细信息](#bkmk_2016)）。
    - 从 Windows Server 2012 到 Windows Server 2012 R2（[查看其他详细信息](#bkmk_2012r2)）。
    - 从 Windows Server 2008 R2 到 Windows Server 2012 R2（[查看其他详细信息](#bkmk_from2008r2)）。

    > [!WARNING]  
    >  升级到不同操作系统之前，必须从服务器卸载 WSUS。 可以保留 SUSDB，并在重新安装 WSUS 后将其重新附加。 有关此关键步骤的详细信息，请参阅 Windows Server 文档中 [Windows Server 更新服务概述](https://technet.microsoft.com/library/hh852345.aspx)中的“新增和更改的功能”部分。  

若要升级服务器，请使用要升级到的目标操作系统所提供的升级过程。 请参阅下列文章：
  -  Windows Server 文档中的 [Windows Server 2012 R2 的升级选项](https://technet.microsoft.com/library/dn303416.aspx)。  
  - Windows Server 文档中的 [Upgrade and conversion options for Windows Server 2016](/windows-server/get-started/supported-upgrade-paths)（Windows Server 2016 升级和转换选项）。

### <a name="bkmk_2016"></a>  将 Windows Server 2012 或 Windows Server 2012 R2 升级到 2016
将 Windows Server 2012 或 Windows Server 2012 R2 升级到 Windows Server 2016 时，下列规则适用：


#### <a name="before-upgrade"></a>升级之前  
-   删除 System Center Endpoint Protection (SCEP) 客户端。 Windows Server 2016 具有内置的 Windows Defender，它会代替 SCEP 客户端。 SCEP 客户端的存在会阻止升级到 Windows Server 2016。
-   如果已安装 WSUS 角色，则从服务器中将其删除。 可以保留 SUSDB，并在重新安装 WSUS 后将其重新附加。

#### <a name="after-upgrade"></a>升级之后   
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

-   如果要升级主站点服务器，请[运行站点重置](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset)。

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>远程 Configuration Manager 控制台的已知问题   
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

#### <a name="before-upgrade"></a>升级之前  
-   如果已安装 WSUS 角色，则从服务器中将其删除。 可以保留 SUSDB，并在重新安装 WSUS 后将其重新附加。

#### <a name="after-upgrade"></a>升级之后  
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

#### <a name="before-upgrade"></a>升级之前  
-   卸载 WSUS 3.2。  
    将服务器操作系统升级到 Windows Server 2012 R2 之前，必须从服务器中卸载 WSUS 3.2。 有关此关键步骤的信息，请参阅 Windows Server 文档中 [Windows Server 更新服务概述](https://technet.microsoft.com/library/hh852345.aspx)中的“新增和更改的功能”部分。

#### <a name="after-upgrade"></a>升级之后  
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

-   从支持的版本到 Windows 10 的 Windows 就地升级。 有关详细信息，请参阅[将 Windows 升级到最新版本](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)。  

-   Windows 10 的内部版本到内部版本服务升级。 有关详细信息，请参阅[管理 Windows 即服务](../../../osd/deploy-use/manage-windows-as-a-service.md)。  



##  <a name="BKMK_SupConfigUpgradeDBSrv"></a>升级站点数据库服务器上的 SQL Server  
  Configuration Manager 在站点数据库服务器上支持将 SQL Server 从受支持的 SQL 版本就地升级。 本节中的 SQL Server 升级方案均受 Configuration Manager 支持，并且包括每个方案的要求。

 有关 Configuration Manager 支持的 SQL Server 版本的详细信息，请参阅[对 SQL Server 版本的支持](../../../core/plan-design/configs/support-for-sql-server-versions.md)。  

 ### <a name="upgrade-the-service-pack-version-of-sql-server"></a>升级 SQL Server 的 Service Pack 版本    
 如果生成的 SQL Server 服务包级别仍受 Configuration Manager 支持，则 Configuration Manager 支持将 SQL Server 就地升级到更高的服务包版本。

 当在一个层次结构中具有多个 Configuration Manager 站点时，每个站点都可以运行不同版本的 SQL Server 服务包。 对站点升级用于站点数据库的 SQL Server 服务包版本的顺序没有限制。

### <a name="upgrade-to-a-new-version-of-sql-server"></a>升级到新版本的 SQL Server   
 Configuration Manager 支持将 SQL Server 就地升级到以下版本：

 - SQL Server 2017
 - SQL Server 2016  
 - SQL Server 2014  

升级托管站点数据库的 SQL Server 的版本时，必须在站点按以下顺序升级使用的 SQL Server 版本：

 1. 首先升级管理中心站点上的 SQL Server。
 2. 升级辅助站点，然后再升级辅助站点的父主站点。
 3. 最后升级父主站点。 这些站点包括向管理中心站点报告的子主站点和是层次结构的顶层站点的独立主站点。

### <a name="sql-server-cardinality-estimation-level-and-the-site-database"></a>SQL Server 基数估计级别和站点数据库   
从 SQL Server 早期版本升级站点数据库时，如果现有 SQL基数估计 (CE) 级别是此 SQL Server 实例允许的最小级别，则数据库会保留此级别。 使用兼容级别低于允许级别的数据库升级 SQL Server 会自动将数据库设置为 SQL Server 允许的最低兼容级别。

下表列出了 Configuration Manager 站点数据库的建议兼容级别：

|SQL Server 版本 | 受支持的兼容级别 |推荐级别|
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

若要标识站点数据库使用的 SQL Server CE 兼容级别，请在站点数据库服务器上运行以下 SQL 查询：  
`SELECT name, compatibility_level FROM sys.databases`

 有关 SQL CE 兼容级别及其设置方法的详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017)。


有关升级 SQL Server 的详细信息，请参阅以下 SQL Server 文档：
-   [升级到 SQL Server 2017](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)
-   [升级到 SQL Server 2016](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)
-   [升级到 SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>在站点数据库服务器上升级 SQL Server  

1.  停止站点上所有的 Configuration Manager 服务。  
2.  将 SQL Server 升级到支持的版本。  
3.  重新启动 Configuration Manager 服务。  

> [!NOTE]  
>  在管理中心站点上将使用的 SQL Server 版本从 Standard Edition 更改为 Datacenter 或 Enterprise Edition 时，限制层次结构支持的客户端数量的数据库分区不会更改。
