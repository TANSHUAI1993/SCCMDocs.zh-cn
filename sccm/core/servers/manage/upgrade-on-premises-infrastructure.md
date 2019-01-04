---
title: 升级本地基础结构
titleSuffix: Configuration Manager
description: 了解如何升级基础结构（例如 SQL Server）和站点系统的操作系统。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b51685d97aea766757034c6f41afa5d4c8a11ee
ms.sourcegitcommit: 32a257fafbb29aece8b4f435dd5614fcef305328
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2019
ms.locfileid: "54005460"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>升级支持 Configuration Manager 的本地基础结构

*适用于：System Center Configuration Manager (Current Branch)*

使用本文中的信息来帮助升级运行 Configuration Manager 的服务器基础结构。  

- 如果想从早期版本升级到 Configuration Manager Current Branch，请参阅[升级到 Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)。  

- 如果想将 Configuration Manager Current Branch基础结构更新为新版本，请参阅 [Configuration Manager 的更新](/sccm/core/servers/manage/updates)。  



## <a name="BKMK_SupConfigUpgradeSiteSrv"></a> 升级站点系统的操作系统  

Configuration Manager 在以下情况中支持托管站点服务器和任何站点系统角色的服务器 OS 的就地升级：  

- 如果 Configuration Manager 仍然支持生成的 Windows 服务包级别，它则支持就地升级到更高版本的 Windows Server 服务包。  

- 就地升级：  

    - Windows Server 2016 到 Windows Server 2019   

    - Windows Server 2012 R2 到 Windows Server 2019   

    - Windows Server 2012 R2 到 Windows Server 2016   

    - Windows Server 2012 到 Windows Server 2016   

    - Windows Server 2012 到 Windows Server 2012 R2   

    - Windows Server 2008 R2 到 Windows Server 2012 R2   

若要升级服务器，请使用要升级到的目标操作系统所提供的升级过程。 请参阅下列文章：  

- [Windows Server 升级中心](http://aka.ms/upgradecenter)  

- [适用于 Windows Server 2016 的升级和转换选项](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths)  

- [Windows Server 2012 R2 的升级选项](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))   


### <a name="bkmk_2016-2019"></a>升级到 Windows Server 2016 或 2019

使用本部分中的步骤进行以下任一升级方案：  

- 将 Windows Server 2012 R2 或 Windows Server 2016 升级到 Windows Server 2019  

- 将 Windows Server 2012 或 Windows Server 2012 R2 升级到 Windows Server 2016  


#### <a name="before-upgrade"></a>升级之前  
- （Windows Server 2012 或 Windows Server 2012 R2）：删除 System Center Endpoint Protection (SCEP) 客户端。 Windows Server 现在内置有 Windows Defender，它将替代 SCEP 客户端。 SCEP 客户端的存在会阻止升级到 Windows Server。  

- 如果安装了 WSUS 角色，请将它从服务器中删除。 可以保留 SUSDB，并在重新安装 WSUS 后将其重新附加。  

#### <a name="after-upgrade"></a>升级之后   
- 确保 Windows Defender 已启用、已设置为自动启动且正在运行。  

- 确保以下 Configuration Manager 服务正在运行：  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- 确保“Windows Process Activation”和“WWW/W3svc”服务已启用并且已设置为自动启动。 升级过程将禁用服务，因此请确保它们正在针对以下站点系统角色运行：  

    - 站点服务器  

    - 管理点  

    - 应用程序目录 Web 服务点  

    - 应用程序目录网站点  

- 请确保托管站点系统角色的每个服务器继续满足所有[先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。 例如，可能需要重新安装 BITS、WSUS 或为 IIS 配置特定设置。  

- 恢复任何缺少的先决条件后，再次重启服务器以确保服务已启动并且可操作。  

- 如果要升级主站点服务器，请[运行站点重置](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset)。  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>远程 Configuration Manager 控制台的已知问题   
在升级站点服务器或 SMS 提供程序的实例后，将无法与 Configuration Manager 控制台连接。 若要暂时解决此问题，必须手动还原 WMI 中“SMS 管理员”组的权限。 必须在此站点服务器以及每个托管 SMS 提供程序实例的远程服务器上设置权限：

1. 在适用的服务器上，打开 Microsoft 管理控制台 (MMC)，为“WMI 控件”添加管理单元，然后选择“本地计算机”。  

2. 在 MMC 中，打开“WMI 控件(本地)”的“属性”，然后选择“安全”选项卡。  

3. 展开“根”下的树形，选择“SMS”节点，然后选择“安全”。  确保“SMS 管理员”组具有以下权限：  

    - 启用帐户  

    - 远程启用  

4. 在“SMS”节点下方的“安全”选项卡中，选择“site_&lt;sitecode>”节点，然后选择“安全”。 确保“SMS 管理员”组具有以下权限：  

    - 执行方法  

    - 提供程序写入  

    - 启用帐户  

    - 远程启用  

5. 保存权限以还原 Configuration Manager 控制台的访问权限。  


#### <a name="known-issue-for-remote-site-systems"></a>已知的远程站点系统问题
在升级托管站点系统角色的服务器之后，下列注册表项中可能缺少值 `Software\Microsoft\SMS`：`HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths` 

如果在服务器上升级 Windows 后缺少此值，请手动添加它。 否则，站点系统角色可能在将文件上传到站点服务器收件箱时遇到问题。


### <a name="bkmk_2012r2"></a>升级到 Windows Server 2012 R2

从 Windows Server 2008 R2 或 Windows Server 2012 升级到 Windows Server 2012 R2 时，以下条件将适用：

#### <a name="before-upgrade"></a>升级之前  
- 在 Windows Server 2012 上：如果安装了 WSUS 角色，请将它从服务器中删除。 可以保留 SUSDB，并在重新安装 WSUS 后将其重新附加。  

- 在 Windows Server 2008 R2 上：升级到 Windows Server 2012 R2 之前，必须从服务器中卸载 WSUS 3.2。 可以保留 SUSDB，并在重新安装 WSUS 后将其重新附加。 有关详细信息，请参阅 [Windows Server 更新服务概述](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality)。  

#### <a name="after-upgrade"></a>升级之后  
- 升级过程将禁用 Windows 部署服务。 确保此服务已启动并且正在针对以下站点系统角色运行：  

    - 站点服务器  

    - 管理点  

    - 应用程序目录 Web 服务点  

    - 应用程序目录网站点  

- 确保“Windows Process Activation”和“WWW/W3svc”服务已启用并且已设置为自动启动。 升级过程将禁用服务，因此请确保它们正在针对以下站点系统角色运行：  

    - 站点服务器  

    - 管理点  

    - 应用程序目录 Web 服务点  

    - 应用程序目录网站点  

- 请确保托管站点系统角色的每个服务器继续满足所有[先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。 例如，可能需要重新安装 BITS、WSUS 或为 IIS 配置特定设置。  

    恢复任何缺少的先决条件后，再次重启服务器以确保服务已启动并且可操作。  


### <a name="unsupported-upgrade-scenarios"></a>不支持的升级方案

以下 Windows Server 升级方案经常被问及，但不受 Configuration Manager 支持：  

- Windows Server 2008 到 Windows Server 2012 或更高版本  

- Windows Server 2008 R2 到 Windows Server 2012  



##  <a name="BKMK_SupConfigUpgradeClient"></a>升级客户端的 OS  

以下情况中，Configuration Manager 支持就地升级 Configuration Manager 客户端的操作系统：  

- 如果 Configuration Manager 支持生成的服务包级别，它则支持就地升级到更高版本的 Windows 服务包。  

- 从支持的版本到 Windows 10 的 Windows 就地升级。 有关详细信息，请参阅[将 Windows 升级到最新版本](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)。  

- Windows 10 的内部版本到内部版本服务升级。 有关详细信息，请参阅[管理 Windows 即服务](/sccm/osd/deploy-use/manage-windows-as-a-service)。  



##  <a name="BKMK_SupConfigUpgradeDBSrv"></a>升级 SQL Server  

Configuration Manager 支持站点数据库服务器上 SQL Server 的就地升级。 

有关 Configuration Manager 支持的 SQL Server 版本的详细信息，请参阅[对 SQL Server 版本的支持](/sccm/core/plan-design/configs/support-for-sql-server-versions)。  


### <a name="upgrade-the-service-pack-version-of-sql-server"></a>升级 SQL Server 的 Service Pack 版本    

如果 Configuration Manager 仍然支持生成的 SQL Server 服务包级别，它则支持将 SQL Server就地升级到更高版本的服务包。

当在一个层次结构中具有多个 Configuration Manager 站点时，每个站点都可以运行不同的 SQL Server 服务包版本。 对站点升级 SQL Server 服务包版本的顺序没有限制。


### <a name="upgrade-to-a-new-version-of-sql-server"></a>升级到新版本的 SQL Server   

Configuration Manager 支持将 SQL Server 就地升级到以下版本：

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

升级托管站点数据库的 SQL Server 的版本时，必须按以下顺序升级在站点处使用的 SQL Server 版本：

1. 首先升级管理中心站点处的 SQL Server  

2. 首先升级辅助站点，然后再升级辅助站点的父主站点  

3. 最后升级父主站点。 这些站点包括向管理中心站点报告的子主站点和是层次结构的顶层站点的独立主站点。  


### <a name="sql-server-cardinality-estimation-level"></a>SQL Server 基数估计级别   

从 SQL Server 早期版本升级站点数据库时，如果现有 SQL基数估计级别是此 SQL Server 实例允许的最小级别，数据库则会保留此级别。 使用兼容级别低于允许级别的数据库升级 SQL Server 会自动将数据库设置为 SQL Server 允许的最低兼容级别。

下表列出了 Configuration Manager 站点数据库的建议兼容级别：

|SQL Server 版本 | 受支持的兼容级别 | 推荐级别 |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

若要标识为站点数据库使用的 SQL Server 基数估计，请在站点数据库服务器上运行以下 SQL 查询：  
```SQL
SELECT name, compatibility_level FROM sys.databases
```

有关 SQL CE 兼容级别及其设置方法的详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017)。


有关升级 SQL Server 的详细信息，请参阅以下 SQL Server 文章：  

- [升级到 SQL Server 2017](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [升级到 SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [升级到 SQL Server 2014](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>在站点数据库服务器上升级 SQL Server  

1. 停止站点处所有的 Configuration Manager 服务  

2. 将 SQL Server 升级到受支持的版本  

3. 重新启动 Configuration Manager 服务  

> [!NOTE]  
> 当将在管理中心站点处使用的 SQL Server 版本从 Standard 升级到 Datacenter 或 Enterprise 时，数据库分区不会更改。 此数据库分区会限制层次结构支持的客户端数量。  
