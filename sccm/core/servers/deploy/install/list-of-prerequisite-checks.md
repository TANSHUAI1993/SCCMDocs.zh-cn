---
title: 先决条件检查
titleSuffix: Configuration Manager
description: Configuration Manager 更新特定先决条件检查的参考。
ms.date: 04/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 79730167346490350a7536c6badb5f0bc0fa85f4
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2019
ms.locfileid: "67252279"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Configuration Manager 先决条件检查列表

适用范围：  System Center Configuration Manager (Current Branch)

本文详细介绍了安装或更新 Configuration Manager 时运行的先决条件检查。 有关详细信息，请参阅[先决条件检查程序](/sccm/core/servers/deploy/install/prerequisite-checker)。  



## <a name="errors"></a>错误

### <a name="active-migration-mappings-on-the-target-primary-site"></a>目标主站点上的活动迁移映射

适用范围：  管理中心站点

不存在到主站点的活动迁移映射。

### <a name="active-replica-mp"></a>活动副本 MP

适用范围：  主站点

具有活动的管理点副本。

### <a name="administrative-rights-on-expand-primary-site"></a>扩展主站点上的管理权限

适用范围：  管理中心站点

将主站点扩展到层次结构时，运行安装程序的用户帐户在独立主站点服务器上具有管理员权限  。

### <a name="administrative-rights-on-site-system"></a>站点系统上的管理权限

适用范围：  管理中心站点、主站点、辅助站点

运行 Configuration Manager 安装程序的用户帐户在站点服务器上具有管理员权限  。

### <a name="administrator-rights-on-central-administration-site"></a>管理中心站点上的管理员权限

适用范围：  主站点

运行 Configuration Manager 安装程序的用户帐户在管理中心站点服务器上具有管理员权限  。

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>扩展主站点上的资产智能同步点

适用范围：  管理中心站点

将主站点扩展到层次结构时，独立主站点上未安装资产智能同步点角色。

### <a name="bits-enabled"></a>已启用 BITS

适用范围：  管理点

管理点上安装了后台智能传输服务 (BITS)。 由于以下原因之一，此检查可能会失败：

- 未安装 BITS  

- 服务器或远程 IIS 主机上未安装 IIS 7.0 的 IIS 6.0 WMI 兼容性组件  

- 安装程序无法验证远程 IIS 设置。 站点服务器上未安装 IIS 通用组件。  

### <a name="case-insensitive-collation-on-sql-server"></a>SQL Server 上不区分大小写的排序规则

适用范围：  站点数据库服务器

SQL Server 安装使用不区分大小写的排序规则，例如 SQL_Latin1_General_CP1_CI_AS  。

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>扩展主站点上的管理中心站点服务器管理权限

适用范围：  管理中心站点

将主站点扩展到层次结构时，管理中心站点服务器的计算机帐户在独立主站点服务器上具有管理员权限  。

### <a name="client-version-on-management-point-computer"></a>管理点计算机上的客户端版本

适用范围：  管理点

你将在安装了相同版本的 Configuration Manager 客户端的服务器上安装管理点。

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>扩展的主站点上的云管理网关

适用范围：  管理中心站点

将主站点扩展到层次结构时，独立主站点上未安装云管理网关角色。

### <a name="connection-to-sql-server-on-central-administration-site"></a>连接到管理中心站点上的 SQL Server

适用范围：  主站点

在主站点上运行 Configuration Manager 安装程序以加入现有层次结构的用户帐户在管理中心站点的 SQL Server 实例上具有 sysadmin 角色  。

### <a name="custom-client-agent-settings-have-nap-enabled"></a>自定义客户端代理设置已启用 NAP

适用范围：  管理中心站点、主站点

没有可启用网络访问保护 (NAP) 的自定义客户端设置。

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>在扩展主站点上的数据仓库服务点

适用范围：  管理中心站点

将主站点扩展到层次结构时，独立主站点上未安装数据仓库服务点角色。

### <a name="dedicated-sql-server-instance"></a>专用的 SQL Server 实例

适用范围：  管理中心站点、主站点、辅助站点

已配置 SQL Server 的专用实例来承载 Configuration Manager 站点数据库。

如果另一个站点使用该实例，则必须为新站点选择其他实例。 还可以卸载其他站点或将其数据库转移到 SQL Server 的其他实例。

### <a name="default-client-agent-settings-have-nap-enabled"></a>默认客户端代理设置已启用 NAP

适用范围：  管理中心站点、主站点

默认客户端设置不启用网络访问保护 (NAP)。

### <a name="domain-membership-error"></a>域成员身份（错误）

适用范围：  管理中心站点、主站点、辅助站点、SMS 提供程序、SQL Server

Configuration Manager 计算机是 Windows 域的成员。

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>扩展主站点上的 Endpoint Protection 点

适用范围：  管理中心站点

将主站点扩展到层次结构时，独立主站点上未安装 Endpoint Protection 点角色。

### <a name="existing-configuration-manager-server-components-on-server"></a>服务器上现有的 Configuration Manager 服务器组件

适用范围：  管理中心站点、主站点、辅助站点

为站点安装选择的服务器上尚未安装站点服务器或站点系统角色。

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>现有独立主站点的版本和站点代码

适用范围：  管理中心站点、主站点

你计划扩展的主站点是独立的主站点。 它与管理中心站点安装相同版本的 Configuration Manager，但站点代码不同。

### <a name="firewall-exception-for-sql-server"></a>针对 SQL Server 的防火墙例外

适用范围：  管理中心站点、主站点、辅助站点、管理点

Windows 防火墙被禁用，或者 SQL Server 存在相关的 Windows 防火墙例外。

允许远程访问 Sqlservr.exe 或所需的 TCP 端口。 默认情况下，SQL Server 侦听 TCP 端口 1433，SQL Server Service Broker (SSB) 使用 TCP 端口 4022。

### <a name="free-disk-space-on-site-server"></a>站点服务器上的可用磁盘空间

适用范围：  管理中心站点、主站点、辅助站点

要安装站点服务器，必须至少具有 15 GB 的可用磁盘空间。 如果在同一服务器上安装 SMS 提供程序，则需要额外的 1 GB 可用空间。

### <a name="iis-service-running"></a>IIS 服务正在运行

适用范围：  管理点、分发点

用于管理点或分发点的 IIS 已在服务器上安装并运行。

### <a name="incompatible-collection-references"></a>不兼容的集合引用

适用范围：  管理中心站点

在升级期间，集合仅引用相同类型的其他集合。

### <a name="match-collation-of-expand-primary-site"></a>匹配扩展主站点的排序规则

适用范围：  管理中心站点

将主站点扩展到层次结构时，独立主站点的站点数据库与管理中心站点上的站点数据库具有相同的排序规则。

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性组的最大文本副本大小

适用范围：  站点数据库服务器

使用 SQL Server Always On 时，“最大文本副本大小”设置必须配置正确  。 有关详细信息，请参阅[准备将 SQL Server Always On 可用性组与 Configuration Manager 配合使用](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>扩展主站点上的 Microsoft Intune 连接器

适用范围：  管理中心站点

将主站点扩展到层次结构时，独立主站点上未安装 Microsoft Intune 连接器角色。

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>已注册 Microsoft 远程差分压缩 (RDC) 库

适用范围：  管理中心站点、主站点、辅助站点

RDC 库已在 Configuration Manager 站点服务器上注册。

### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer

适用范围：  管理中心站点、主站点、辅助站点

验证 Windows Installer 版本。

如果此检查失败，安装程序将无法验证版本或已安装版本是否不符合最低要求 Windows Installer 4.5 版。

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Configuration Manager 控制台的最低 .NET Framework 版本

适用范围：  Configuration Manager 控制台

Configuration Manager 控制台计算机上已安装 Microsoft .NET Framework 4.0。

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Configuration Manager 站点服务器的最低 .NET Framework 版本

适用范围：  管理中心站点、主站点、辅助站点

Configuration Manager 站点服务器上已安装或启用 .NET Framework 3.5。

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Configuration Manager 辅助站点 SQL Server Express 版本安装的最低 .NET Framework 版本

适用范围：  辅助站点

Configuration Manager 辅助站点服务器上已安装或启用 .NET Framework 4.0。 SQL Server Express 需要此版本。

### <a name="parent-database-collation"></a>父数据库排序规则

适用范围：  主站点、辅助站点

站点数据库的排序规则与父站点数据库的排序规则匹配。 层次结构中的所有站点都必须使用相同的数据库排序规则。

### <a name="parent-site-replication-status"></a>父站点复制状态

适用范围：  管理中心站点、主站点

父站点的复制状态为“活动复制”（状态 125）   。

### <a name="pending-system-restart"></a>正在等待系统重启

适用范围：  管理中心站点、主站点、辅助站点

在运行安装程序之前，另一个程序需要重启服务器。

从版本 1810 开始，此检查更加灵活。 为了查看计算机是否处于挂起的重启状态，它会检查以下注册表位置：<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>主 FQDN

适用范围：  管理中心站点、主站点、辅助站点、站点数据库服务器

计算机的 NetBIOS 名称与完全限定的域名 (FQDN) 中的本地主机名匹配。

### <a name="read-only-domain-controller"></a>只读域控制器

适用范围：  管理中心站点、主站点、辅助站点

只读域控制器 (RODC) 上不支持站点数据库服务器和辅助站点服务器。

有关详细信息，请参阅有关[在域控制器上安装 SQL Server 时可能会遇到的问题](https://support.microsoft.com/help/2032911)的 Microsoft 支持文章。

### <a name="required-sql-server-collation"></a>所需的 SQL Server 排序规则

适用范围：  管理中心站点、主站点、辅助站点

SQL Server 实例配置为使用 SQL_Latin1_General_CP1_CI_AS 排序规则  。

如果已安装 Configuration Manager 站点数据库，则此检查也适用于数据库。 有关更改 SQL Server 实例和数据库排序规则的信息，请参阅 [SQL 排序规则及 unicode 支持](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support)。

如果使用的是中文操作系统且需要 GB18030 支持，则此检查不适用。 有关启用 GB18030 支持的详细信息，请参阅[国际支持](/sccm/core/plan-design/hierarchy/international-support)。

### <a name="server-service-is-running"></a>服务器服务正在运行

适用范围：  管理中心站点、主站点、辅助站点

服务器服务已启动并运行。

### <a name="setup-source-folder"></a>安装程序源文件夹

适用范围：  辅助站点

辅助站点的计算机帐户对安装源文件夹和共享具有以下权限：

- 读取 NTFS 文件系统的权限   

- 读取共享权限   

> [!Note]  
> 如果你使用管理共享（例如，C$ 和 D$），则辅助站点计算机帐户必须是服务器上的管理员  。  

### <a name="setup-source-version"></a>安装程序源版本

适用范围：  辅助站点

为辅助站点安装指定的源文件夹中的 Configuration Manager 版本与主站点的 Configuration Manager 版本匹配。

### <a name="site-code-in-use"></a>站点代码正在使用中

适用范围：  主站点

Configuration Manager 层次结构中已不使用指定的站点代码。 请为此站点指定唯一的站点代码。

### <a name="site-server-computer-account-administrative-rights"></a>站点服务器计算机帐户管理权限

适用范围：  主站点、站点数据库服务器

站点服务器计算机帐户在 SQL Server 和管理点计算机上具有管理员权限  。

### <a name="site-server-fqdn-length"></a>站点服务器 FQDN 长度

适用范围：  管理中心站点、主站点、辅助站点

站点服务器的 FQDN 的长度。

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>扩展主站点中的被动模式下的站点服务器

适用范围：  管理中心站点

将主站点扩展到层次结构时，独立主站点上未安装被动模式下的站点服务器角色。

### <a name="sms-provider-in-same-domain-as-site-server"></a>SMS 提供程序与站点服务器位于同一域中

适用范围：  SMS 提供程序

SMS 提供程序的任何实例与站点服务器都位于同一域中。

### <a name="software-update-point-in-nlb-configuration"></a>NLB 配置中的软件更新点

适用范围：*软件更新点*

该站点不使用网络负载均衡 (NLB) 与活动软件更新点的任何虚拟位置。

### <a name="software-update-point-using-a-load-balancer"></a>使用负载均衡器的软件更新点

适用范围：*软件更新点*

Configuration Manager 不支持网络 (NLB) 上的软件更新点或硬件负载均衡器 (HLB)。

### <a name="sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性组

适用范围：  站点数据库服务器

使用 SQL Server Always On 时，其必须满足承载可用性组的最低要求。 有关详细信息，请参阅[准备将 SQL Server Always On 可用性组与 Configuration Manager 配合使用](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>为可读辅助副本配置的 SQL Server 可用性组

适用范围：  站点数据库服务器

使用 SQL Server Always On 时，请查看可用性组副本的辅助副本读取状态。

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>为手动故障转移配置的 SQL Server 可用性组

适用范围：  站点数据库服务器

使用 SQL Server Always On 时，配置可用性组副本以进行手动故障转移。

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>默认实例的 SQL Server 可用性组副本

适用范围：  站点数据库服务器

使用 SQL Server Always On 时，可用性组副本位于默认实例。

### <a name="sql-server-configuration-for-site-upgrade"></a>用于站点升级的 SQL Server 配置

适用范围：  站点数据库服务器

SQL Server 满足站点升级的最低要求。 有关详细信息，请参阅[支持的 SQL Server 版本](/sccm/core/plan-design/configs/support-for-sql-server-versions)。

### <a name="sql-server-edition"></a>SQL Server 版本

适用范围：  站点数据库服务器

站点上的 SQL Server 不是 SQL Server Express。

### <a name="sql-server-express-on-secondary-site"></a>辅助站点上的 SQL Server Express

适用范围：  辅助站点

SQL Server Express 可在辅助站点服务器上成功安装。

### <a name="sql-server-on-the-secondary-site-server"></a>辅助站点服务器上的 SQL Server

适用范围：  辅助站点

SQL Server 安装在辅助站点服务器上。 无法在辅助站点的远程站点系统上安装 SQL Server。

> [!Warning]  
> 只有在选择让安装程序使用现有 SQL Server 实例时，此检查才适用。  

### <a name="sql-server-service-running-account"></a>SQL Server 服务运行帐户

适用范围：  管理中心站点、主站点、辅助站点

SQL Server 服务的登录帐户不是本地用户帐户或 LOCAL SERVICE  。

将 SQL Server 服务配置为使用有效的域帐户、NETWORK SERVICE 或 LOCAL SYSTEM   。

### <a name="sql-server-site-database-consistency"></a>SQL Server 站点数据库一致性

适用范围：  站点数据库服务器

验证数据库一致性。

### <a name="sql-server-sysadmin-rights"></a>SQL Server sysadmin 权限

适用范围：  站点数据库服务器

运行 Configuration Manager 安装程序的用户帐户在为站点数据库安装选择的 SQL Server 实例上具有 sysadmin 角色  。 当安装程序无法访问 SQL Server 的实例来验证权限时，此检查也会失败。

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>引用站点的 SQL Server sysadmin 权限

适用范围：  站点数据库服务器

运行 Configuration Manager 安装程序的用户帐户在选作引用站点数据库的 SQL Server 角色实例上具有 sysadmin 角色  。 需要 SQL Server **sysadmin** 角色权限才能修改站点数据库。

### <a name="sql-server-tcp-port"></a>SQL Server TCP 端口

适用范围：  站点数据库服务器

已为 SQL Server 实例启用了 TCP，并且已设置为使用静态端口。

### <a name="sql-server-version"></a>SQL Server 版本

适用范围：  站点数据库服务器

指定站点数据库服务器上已安装了支持的 SQL Server 版本。

有关详细信息，请参阅 [SQL Server 版本支持](/sccm/core/plan-design/configs/support-for-sql-server-versions)。

### <a name="unsupported-os-for-configuration-manager-console"></a>Configuration Manager 控制台不支持的操作系统

适用范围：  Configuration Manager 控制台

在运行支持的操作系统版本的计算机上安装 Configuration Manager 控制台。

有关详细信息，请参阅 [Configuration Manager 控制台支持的操作系统版本](/sccm/core/plan-design/configs/supported-operating-systems-consoles)。

### <a name="unsupported-os-for-site-server"></a>站点服务器不支持的操作系统

适用范围：  管理中心站点、主站点、辅助站点、Configuration Manager 控制台、管理点、分发点

服务器运行支持的操作系统版本。

有关详细信息，请参阅[支持 Configuration Manager 站点系统服务器的操作系统版本](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)。

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>不受支持的站点系统角色：带外数据服务点

适用范围：  主站点

带外服务点站点系统角色未安装。

### <a name="unsupported-site-system-role-system-health-validation-point"></a>不受支持的站点系统角色：系统健康验证点

适用范围：  主站点

系统健康验证点站点系统角色未安装。

### <a name="unsupported-upgrade-path"></a>不支持的升级路径

适用范围：  管理中心站点、主站点

层次结构中的所有站点服务器都满足升级所需的 Configuration Manager 最低版本。

### <a name="usmt-installed"></a>已安装 USMT

适用范围：  管理中心站点、主站点（仅独立）

已安装适用于 Windows 的 Windows 评估和部署工具包 (ADK) 的用户状态迁移工具 (USMT) 组件。

### <a name="validate-fqdn-of-sql-server"></a>验证 SQL Server 的 FQDN

适用范围：  站点数据库服务器

已为 SQL Server 计算机指定有效的 FQDN。

### <a name="verify-central-administration-site-version"></a>验证管理中心站点版本

适用范围：  主站点

管理中心站点具有相同的 Configuration Manager 版本。

### <a name="verify-database-consistency"></a>验证数据库一致性

适用范围：  管理中心站点、主站点

验证 SQL Server 中站点数据库的一致性。  

### <a name="windows-deployment-tools-installed"></a>已安装 Windows 部署工具

适用范围：  SMS 提供程序

已安装 Windows ADK 的 Windows 部署工具组件。

### <a name="windows-failover-cluster"></a>Windows 故障转移群集

适用范围：  站点服务器、管理点、分发点

具有站点服务器、管理点或分发点角色的服务器不是 Windows 群集的一部分。

从版本 1810 开始，Configuration Manager 设置进程不再阻止在具有适用于故障转移群集的 Windows 角色的计算机上安装站点服务器角色。 SQL Always On 需要此角色，因此，以前你无法在站点服务器上共置站点数据库。 进行此更改后，你可以通过在被动模式下使用 SQL Always On 和站点服务器创建具有更少服务器的高可用站点。 有关详细信息，请参阅[高可用性选项](/sccm/core/servers/deploy/configure/high-availability-options)。 <!--1359132-->  

### <a name="windows-pe-installed"></a>已安装 Windows PE

适用范围：  SMS 提供程序

已安装 Windows ADK 的 Windows 预安装环境 (PE) 组件。



## <a name="warnings"></a>警告

### <a name="active-directory-domain-functional-level"></a>Active Directory 域功能级别

适用范围：  管理中心站点、主站点

Active Directory 域功能级别最低为 Windows Server 2008 R2。

### <a name="administrative-rights-on-distribution-point"></a>分发点上的管理权限

适用范围：  分发点

运行安装程序的用户帐户在分发点上具有管理员权限  。

### <a name="administrative-rights-on-management-point"></a>管理点上的管理权限

适用范围：  管理点、分发点

站点服务器的计算机帐户在管理点和分发点上具有管理员权限  。

### <a name="administrative-share-site-system"></a>管理共享（站点系统）

适用范围：  管理点

站点系统计算机上存在所需的管理共享。

### <a name="application-compatibility"></a>应用程序兼容性

适用范围：  管理中心站点、主站点

当前应用程序符合应用程序架构。

### <a name="backlogged-inboxes"></a>囤积的收件箱

适用范围：  管理中心站点、主站点

站点服务器正在及时处理关键收件箱。 收件箱不包含超过一天的文件。

它会检查以下收件箱文件夹：

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

若要解析此警告，请查看 Despooler 和计划程序站点系统组件是否正在运行。

### <a name="bits-installed"></a>已安装 BITS

适用范围：  管理点

在 IIS 中安装并启用后台智能传输服务 (BITS)。

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>云管理网关需要基于令牌的身份验证或 HTTPS 管理点

适用范围：*云管理网关*

在某些版本的 Configuration Manager 中，无法使用配置有云管理网关 (CMG) 的 HTTP 管理点。 为 HTTPS 配置 CMG，或者将站点配置为增强型 HTTP。 有关详细信息，请参阅[规划云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)。

### <a name="configuration-for-sql-server-memory-usage"></a>SQL Server 内存使用的配置

适用范围：  站点数据库服务器

为 SQL Server 配置不受限制的内存使用。 将 SQL Server 内存配置为具有最大限制。

### <a name="distribution-point-package-version"></a>分发点包版本

适用范围：*分发点*

站点中的所有分发点都具有最新版本的软件分发包。

### <a name="domain-membership-warning"></a>域成员身份（警告）

适用范围：  管理点、分发点

Configuration Manager 计算机是 Windows 域的成员。

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>针对 SQL Server（独立主站点）的防火墙例外

适用范围：  主站点（仅独立）

Windows 防火墙被禁用，或者 SQL Server 存在相关的 Windows 防火墙例外。

允许远程访问 Sqlservr.exe 或所需的 TCP 端口。 默认情况下，SQL Server 侦听 TCP 端口 1433，Server Service Broker (SSB) 使用 TCP 端口 4022。

### <a name="firewall-exception-for-sql-server-for-management-point"></a>管理点 SQL Server 的防火墙例外

适用范围：  管理点

Windows 防火墙被禁用，或者 SQL Server 存在相关的 Windows 防火墙例外。

### <a name="iis-https-configuration"></a>IIS HTTPS 配置

适用范围：  管理点、分发点

IIS 网站具有 HTTPS 通信协议的绑定。

如果安装需要 HTTPS 的站点角色，则使用有效的公钥基础结构 (PKI) 证书在指定服务器上配置 IIS 站点绑定。

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60)

适用于管理中心站点、主站点、辅助站点、Configuration Manager 控制台、管理点、分发点 

验证是否安装了 MSXML 6.0 或更高版本。

### <a name="network-access-protection-nap-is-no-longer-supported"></a>不再支持网络访问保护 (NAP)

适用范围：  主站点

没有为 NAP 启用的软件更新。

### <a name="ntfs-drive-on-site-server"></a>站点服务器上的 NTFS 驱动器

适用范围：  主站点

必须用 NTFS 文件系统格式化磁盘驱动器。 为提高安全性，在使用 NTFS 文件系统格式化的磁盘驱动器上安装站点服务器组件。

### <a name="bkmk_pending-policy"></a> 待处理的配置项目策略更新

<!--SCCMDocs-pr issue 2814-->

适用范围：  主站点

从版本 1806 开始，如果要从版本 1706 或更高版本进行更新，且你拥有许多应用程序部署，而其中至少一个需要批准，则可能看到此警告。

可以使用两个选项：  

- 忽略警告并继续更新。 此操作会导致更新期间在站点服务器上进行更多处理，因为它会处理策略。 更新后，管理点上的处理器负载可能更重。  

- 修改某个没有要求或有特定 OS 要求的应用程序。 预处理当时站点服务器上的某些负载。 审阅 **objreplmgr.log**，然后监视的管理点上的处理器。 处理完成后，更新站点。 更新后将仍有一些额外的处理，除非你选中第一个选项并忽略警告。  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>正在等待远程 SQL Server 上的系统重启

适用范围：  版本 1902 和更高版本的远程 SQL Server

在运行安装程序之前，另一个程序需要重启服务器。

为了查看计算机是否处于挂起的重启状态，它会检查以下注册表位置：<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>站点服务器上的 PowerShell 2.0

适用范围：  具有 Exchange 连接器的主站点

Configuration Manager Exchange 连接器的站点服务器上已安装 Windows PowerShell 2.0 或更高版本。

### <a name="remote-connection-to-wmi-on-secondary-site"></a>辅助站点上到 WMI 的远程连接

适用范围：  辅助站点

安装程序可以在辅助站点服务器上建立与 WMI 的远程连接。

### <a name="schema-extensions"></a>架构扩展

适用范围：  管理中心站点、主站点

Active Directory 架构已扩展。 如果该架构已扩展，则使用的就是该架构的扩展版本。

Configuration Manager 不需要 Active Directory 架构扩展来安装站点服务器。 Microsoft 建议应充分利用所有 Configuration Manager 功能。 有关扩展架构的优势的详细信息，请参阅[为站点发布准备 Active Directory](/sccm/core/plan-design/network/extend-the-active-directory-schema)。

### <a name="share-name-in-package"></a>包中的共享名

适用范围：  管理中心站点、主站点

包中的共享名不具有无效字符，例如 `#`。

### <a name="site-system-to-sql-server-communication"></a>站点系统与 SQL Server 的通信

适用范围：  辅助站点、管理点

为站点数据库实例运行 SQL Server 服务所配置的帐户在 Active Directory 域服务中具有有效的服务主体名称 (SPN)。 在 Active Directory 中注册有效的 SPN 以支持 Kerberos 身份验证。

### <a name="bkmk_changetracking"></a> SQL Server 更改跟踪清除

适用范围：  站点数据库服务器

从版本 1810 开始，将检查站点数据库是否有 SQL 更改跟踪数据积压工作 (backlog)。<!--SCCMDocs-pr issue 3023-->  

可通过在站点数据库中运行诊断存储过程来手动验证此检查。 首先，为站点数据库创建[诊断连接](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017)。 最简单的方法是使用 SQL Server Management Studio 的数据库引擎查询编辑器，并连接到 `admin:<instance name>`。

在专用管理员连接查询窗口中，运行以下命令：

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

根据数据库的大小和积压工作 (backlog) 大小，此存储过程运行时间为几分钟或几个小时。 完成查询后，会看到与积压工作 (backlog) 相关的两部分数据。 首先查看 CT_Days_Old  。 此值会指出 syscommittab 表中最旧条目的时间（天）。 根据 Configuration Manager 的默认值，此天数应为 5 天。 请勿更改此默认值。 在大量数据处理或复制的情况下，syscommittab 中最旧的条目可能超过五天。 如果此值超过七天，请手动清除更改跟踪数据。  

要清除更改跟踪数据，请在专用管理连接中运行以下命令：

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

此命令将启动 syscommittab 和所有关联的辅助表的清理。 运行时间为几分钟或几个小时。 要监视其进度，请查询 vLogs 视图  。 要查看当前进度，请运行以下查询：

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 更新 SQL Server Native Client 可能需要重启，这可能会影响站点安装进程。

此检查可确保站点具有受支持的 SQL Native Client 版本。 从版本 1810 开始，最低版本是 SQL 2012 SP4 (`11.*.7001.0`)。

此 SQL Native Client 版本支持 TLS 1.2。 有关详细信息，请参阅下列文章：

- [支持 Microsoft SQL Server 的 TLS 1.2](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [如何启用 Configuration Manager 的 TLS 1.2](/sccm/core/plan-design/security/enable-tls-1-2)  

Configuration Manager 对以下站点系统角色使用 SQL Server Native Client：<!-- SCCMDocs issue 1150 -->

- 站点数据库服务器
- 站点服务器：管理中心站点、主站点或辅助站点
- 管理点
- 设备管理点
- 状态迁移点
- SMS 提供程序
- 软件更新点
- 启用多播的分发点
- 资产智能更新服务点
- Reporting Services 点
- 应用程序目录 Web 服务
- 注册点
- Endpoint Protection 点
- 服务连接点
- 证书注册点
- 数据仓库服务点

### <a name="sql-server-process-memory-allocation"></a>SQL Server 进程内存分配

适用范围：  站点数据库服务器

SQL Server 至少为管理中心站点和主站点保留 8 GB 的内存，并至少为辅助站点保留 4 GB 的内存。

有关详细信息，请参阅[如何使用 SQL Server Management Studio 配置内存选项](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-)。

> [!NOTE]  
> 此检查不适用于辅助站点上的 SQL Server Express。 此版本仅限制为保留 1 GB 内存。  

### <a name="sql-server-security-mode"></a>SQL Server 安全模式

适用范围：  站点数据库服务器

针对 Windows 身份验证安全配置了 SQL Server。

### <a name="unsupported-site-system-os-version-for-upgrade"></a>用于升级的不受支持的站点系统操作系统版本

适用范围：  主站点、辅助站点

运行 Windows Server 2012 或更高版本的服务器上安装了除分发点之外的站点系统角色。

有关详细信息，请参阅 [Configuration Manager 站点系统服务器支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)。

> [!NOTE]  
> 此检查无法解析 Azure 中安装的站点系统角色的状态或 Microsoft Intune 使用的云存储的状态。 请忽略这些角色的警告，将其当做误报。

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>不支持升级评估工具包

适用范围：  管理中心站点、主站点

未安装升级评估工具包。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>验证发布到 Active Directory 的站点服务器权限

适用范围：  管理中心站点、主站点、辅助站点

站点服务器的计算机帐户对 Active Directory 域中的“系统管理”容器具有“完全控制”权限   。

有关详细信息，请参阅[为站点发布准备 Active Directory](/sccm/core/plan-design/network/extend-the-active-directory-schema)。

> [!NOTE]  
> 如果手动验证权限，则可以忽略此警告。

### <a name="windows-remote-management-winrm-v11"></a>Windows 远程管理 (WinRM) 1.1 版

适用范围：  主站点、Configuration Manager 控制台

主站点服务器或 Configuration Manager 控制台计算机上已安装 WinRM 1.1 以运行带外管理控制台。

有关如何下载 WinRM 1.1 的详细信息，请参阅[支持文章 936059](https://support.microsoft.com/help/936059)。

### <a name="wsus-on-site-server"></a>站点服务器上的 WSUS

适用范围：  管理中心站点、主站点

站点服务器上安装了受支持的 Windows Server Update Services (WSUS) 版本。

在不是站点服务器上的服务器使用软件更新点时，必须在站点服务器上安装 WSUS 管理控制台。 有关 WSUS 的详细信息，请参阅 [Windows Server 更新服务](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)。
