---
title: "先决条件检查 | Microsoft Docs"
description: "查看 System Center Configuration Manager 的可用先决条件检查。 包括安全权限检查"
ms.custom: na
ms.date: 4/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
caps.latest.revision: "12"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 14834f62ffaa8fcba5ddb7536a0b76e18b557e53
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="list-of-prerequisite-checks-for-system-center-configuration-manager"></a>System Center Configuration Manager 的先决条件检查列表

*适用范围：System Center Configuration Manager (Current Branch)*

下列部分详细介绍了可用的先决条件检查。

有关使用先决条件检查程序的信息，请参阅[先决条件检查程序](prerequisite-checker.md)。  

##  <a name="BKMK_Security"></a> 针对安全权限的先决条件检查  
下表列出了先决条件检查程序针对安全权限执行的先决条件检查。

|已执行的检查|说明|严重性|站点适用性|
|---|---|---|---|
|**管理中心站点上的管理员权限**|验证运行 Configuration Manager 安装程序的用户帐户在管理中心站点计算机上是否有**管理员**权限。 |错误|主站点|
|**扩展主站点上的管理权限**|验证运行安装程序的用户帐户在将扩展的独立主站点上是否有**管理员**权限。|错误|管理中心站点|
|**站点系统上的管理权限**|验证运行 Configuration Manager 安装程序的用户帐户在站点服务器计算机上是否有**管理员**权限。 |错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**扩展主站点上的 CAS 计算机管理权限**|验证管理中心站点的计算机帐户在将扩展的独立主站点上是否有**管理员**权限。|错误|管理中心站点|
|**连接到管理中心站点上的 SQL Server**|验证在主站点上运行 Configuration Manager 安装程序以加入现有层次结构的用户帐户在管理中心站点的 SQL Server 实例上是否有 **sysadmin** 角色。|错误|主站点|
|**站点服务器计算机帐户管理权限**|验证站点服务器计算机帐户在 SQL Server 和管理点计算机上是否有**管理员**权限。|错误|主站点、 <br>SQL Server|
|**站点系统与 SQL Server 的通信**| 对于配置为针对用于承载 Configuration Manager 站点数据库的 SQL Server 实例运行 SQL Server 服务的帐户，验证是否为该帐户在 Active Directory 域服务中注册了有效的服务主体名称 (SPN)。 必须在 Active Directory 域服务中注册有效的 SPN 才能支持 Kerberos 身份验证。|警告|辅助站点、 <br>管理点|
|**SQL Server 安全模式**|验证是否针对 Windows 身份验证安全配置了 SQL Server。|警告|SQL Server|
|**SQL Server sysadmin 权限**|验证运行 Configuration Manager 安装程序的用户帐户在为站点数据库安装选择的 SQL Server 实例上是否有 **sysadmin** 角色。 当安装程序无法访问 SQL Server 的实例来验证权限时，此检查也会失败。|错误|SQL Server|
|**引用站点的 SQL Server sysadmin 权限**|验证运行 Configuration Manager 安装程序的用户帐户在选作引用站点数据库的 SQL Server 角色实例上是否有 **sysadmin** 角色。 需要 SQL Server **sysadmin** 角色权限才能修改站点数据库。|错误|SQL Server|

##  <a name="BKMK_Dependencies"></a> 针对 Configuration Manager 依赖关系的先决条件检查
下表列出了先决条件检查程序针对 Configuration Manager 依赖关系执行的先决条件检查。

|已执行的检查|说明|严重性|站点适用性|
|---|---|---|---|
|**目标主站点上的活动迁移映射**|验证是否不存在到主站点的活动迁移映射。|错误|管理中心站点|
|**活动复本 MP**|检查活动管理点副本。|错误|主站点|
|**分发点上的管理权限**|验证运行安装程序的用户帐户在分发点计算机上是否有**管理员**权限。|警告|分发点|
|**管理点上的管理权限**|验证站点服务器的计算机帐户在管理点和分发点计算机上是否有**管理员**权限。|警告|管理点|
|**管理共享（站点系统）**|验证站点系统计算机上是否存在所需的管理共享。|警告|管理点|
|**应用程序兼容性**|验证当前应用程序是否符合应用程序架构。|警告|管理中心站点、 <br>主站点|
|**已启用 BITS**|验证管理点站点系统计算机上是否安装了后台智能传输服务 (BITS)。 如果此检查失败，则不会安装 BITS，计算机或远程 IIS 主机上不会安装适用于 IIS 7.0 的 Internet Information Services (IIS) 6.0 Windows Management Instrumentation (WMI) 兼容性组件，或者由于站点服务器计算机上未安装 IIS 公共组件，安装程序无法验证远程 IIS 设置。|错误|管理点|
|**已安装 BITS**|验证 IIS 中是否安装了 BITS。|警告|管理点|
|**SQL Server 上不区分大小写的排序规则**|验证 SQL Server 安装是否使用不区分大小写的排序规则，例如 SQL_Latin1_General_CP1_CI_AS。|错误|SQL Server|
|**检查现有独立主站点的版本和站点代码**|验证计划扩展的主站点是否为独立主站点，并验证其是否具有相同版本的 Configuration Manager，但其站点代码与要安装的管理中心站点不同。|错误|管理中心站点、 <br>主站点|
|**检查不兼容的集合引用**|在升级期间，此检查会验证集合是否仅引用具有相同类型的其他集合。|错误|管理中心站点|  
|**管理点计算机上的客户端版本**|验证是否在未安装不同版本的 Configuration Manager 客户端的计算机上安装管理点。|错误|管理点|
|**SQL Server 内存使用的配置**|检查是否为 SQL Server 配置了不受限制的内存使用。 你应将 SQL Server 内存配置为具有最大限制。|警告|SQL Server|
|**专用的 SQL Server 实例**|检查是否配置了专用 SQL Server 实例来承载 Configuration Manager 站点数据库。 如果另一个站点使用该实例，你必须选择其他实例以供新站点使用。 或者，可以卸载其他站点或将其数据库转移到 SQL Server 的其他实例。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**服务器上现有的 Configuration Manager 服务器组件**|验证站点服务器或站点系统角色是否尚未安装在为站点安装选择的计算机上。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**针对 SQL Server 的防火墙例外**|检查 Windows 防火墙是否已禁用，或者 SQL Server 是否存在相关的 Windows 防火墙例外。 必须允许远程访问 Sqlservr.exe 或所需的 TCP 端口。 默认情况下，SQL Server 侦听 TCP 端口 1433，SQL Server Service Broker (SSB) 使用 TCP 端口 4022。|错误|管理中心站点、 <br>主站点、 <br>辅助站点、 <br>管理点|
|**针对 SQL Server（独立主站点）的防火墙例外**|检查 Windows 防火墙是否已禁用，或者 SQL Server 是否存在相关的 Windows 防火墙例外。 必须允许远程访问 Sqlservr.exe 或所需的 TCP 端口。 默认情况下，SQL Server 侦听 TCP 端口 1433，SSB 使用 TCP 端口 4022。|警告|主站点（仅独立）|
|**管理点 SQL Server 的防火墙例外**|检查 Windows 防火墙是否已禁用，或者 SQL Server 是否存在相关的 Windows 防火墙例外。|警告|管理点|
|**IIS HTTPS 配置**|验证 HTTPS 通信协议的 IIS 网站绑定。 如果安装需要 HTTPS 的站点角色，则必须使用有效的公钥基础结构 (PKI) 证书在指定服务器上配置 IIS 站点绑定。|警告|管理点、 <br>分发点|
|**IIS 服务正在运行**|验证在要安装管理点或分发点的计算机上 IIS 是否已安装并正在运行。|错误|管理点、 <br> 分发点|
|**匹配扩展主站点的排序规则**|验证将扩展的独立主站点的站点数据库是否与管理中心站点上的站点数据库具有相同的排序规则。|错误|管理中心站点|
|**已注册 Microsoft 远程差分压缩 (RDC) 库**|验证 RDC 库是否在 Configuration Manager 站点服务器上注册。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**Microsoft Windows Installer**|验证 Windows Installer 版本。 如果此检查失败，安装程序将无法验证版本或已安装版本是否不符合 Windows Installer 4.5 的最低要求。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**Microsoft XML Core Services 6.0 (MSXML60)**|验证计算机上是否安装了 MSXML 6.0 或更高版本。|警告|管理中心站点、 <br>主站点、 <br>辅助站点、 <br>Configuration Manager 控制台、 <br>管理点、 <br>分发点|
|**Configuration Manager 控制台的最低 Minimum .NET Framework 版本**|检查 Configuration Manager 控制台计算机上是否安装了 Microsoft .NET Framework 4.0。 可从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/p/?LinkId=189149)下载 .NET Framework 4.0。|错误|Configuration Manager 控制台|
|**Configuration Manager 站点服务器的最低 .NET Framework 版本**|检查 Configuration Manager 站点服务器上是否安装了 .NET Framework 3.5。 对于 Windows Server 2008，可以从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/p/?LinkId=185604)下载 Microsoft .NET Framework 3.5。 对于 Windows Server 2008 R2，可以将 .NET Framework 3.5 启用为服务器管理器内的功能。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**Configuration Manager 辅助站点 SQL Server Express 版本安装的最低 .NET Framework 版本**|验证 Configuration Manager 辅助站点计算机上是否安装了 .NET Framework 4.0，以安装 SQL Server Express。|错误|辅助站点|
|**父/子数据库排序规则**|验证站点数据库的排序规则是否与父站点数据库的排序规则匹配。 层次结构中的所有站点都必须使用相同的数据库排序规则。|错误|主站点、 <br>辅助站点|
|**站点服务器上的 PowerShell 2.0**|验证 Configuration Manager Exchange 连接器的站点服务器上是否安装了 Windows PowerShell 2.0 或更高版本。 有关 PowerShell 2.0 的详细信息，请参阅 Microsoft 知识库 [文章 968930](http://go.microsoft.com/fwlink/p/?LinkId=226450) 。|警告|主站点|
|**主 FQDN**|使用完全限定的域名 (FQDN)，验证计算机的 NetBIOS 名称是否与计算机的本地主机名（FQDN 的第一个标签）匹配。|错误|管理中心站点、 <br>主站点、 <br>辅助站点、 <br>SQL Server|
|**辅助站点上到 WMI 的远程连接**|检查安装程序是否能够在辅助站点服务器上建立与 WMI 的远程连接。|警告|辅助站点|
|**所需的 SQL Server 排序规则**|验证 SQL Server 和 Configuration Manager 站点数据库的实例（如果已安装）是否配置为使用 SQL_Latin1_General_CP1_CI_AS 排序规则，除非正在使用中文版操作系统并且需要 GB18030 支持。<br><br>有关更改 SQL Server 实例和数据库排序规则的信息，请参阅 SQL Server 2008 R2 联机丛书中的[设置和更改排序规则](http://go.microsoft.com/fwlink/p/?LinkID=234541) 。  有关启用 GB18030 支持的信息，请参阅 [System Center Configuration Manager 的国际支持](../../../../core/plan-design/hierarchy/international-support.md)。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**安装程序源文件夹**|验证辅助站点的计算机帐户是否具有安装程序源文件夹和共享的 **“读取”** NTFS 文件系统权限和 **“读取”** 共享权限。<br><br>**注意**：如果使用管理共享（例如，C$ 和 D$），则辅助站点计算机帐户必须是该计算机的**管理员**用户。|错误|辅助站点|
|**安装程序源版本**|验证为辅助站点安装指定的源文件夹中的 Configuration Manager 版本是否与主站点的 Configuration Manager 版本匹配。|错误|辅助站点|
|**站点代码正在使用中**|检查在 Configuration Manager 层次结构中是否已不使用指定的站点代码。 你必须为此站点指定唯一的站点代码。|错误|主站点|
|**SMS 提供程序计算机与站点服务器具有相同的域**|检查运行 SMS 提供程序实例的计算机是否与站点服务器具有相同的域。|错误|SMS 提供程序|
|**SQL Server 版本**|检查站点上的 SQL Server 版本是否并非 SQL Server Express。|错误|SQL Server|
|**辅助站点上的 SQL Server Express**|检查 SQL Server Express 是否可成功安装在辅助站点的站点服务器计算机上。|错误|辅助站点|
|**辅助站点计算机上的 SQL Server**|检查 SQL Server 是否安装在辅助站点计算机上。 不能在远程站点系统上安装 SQL Server。<br><br>**警告**：只有在选择让安装程序使用现有 SQL Server 实例时，此检查才适用。|错误|辅助站点|
|**SQL Server 进程内存分配**|验证 SQL Server 是否至少为管理中心站点和主站点保留 8 GB 的内存，并至少为辅助站点保留 4 GB 的内存。 若要深入了解如何通过使用 SQL Server Management Studio 设置固定内存量，请参阅[如何设置固定内存量 (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759)。<br><br>**注意**：此检查不适用于辅助站点上的 SQL Server Express，其保留内存只能为 1 GB。|警告|SQL Server|
|**SQL Server 服务运行帐户**|验证 SQL Server 服务的登录帐户不是本地用户帐户或 LOCAL SERVICE。 你必须将 SQL Server 服务配置为使用有效的域帐户、NETWORK SERVICE 或 LOCAL SYSTEM。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**SQL Server TCP 端口**|检查是否已为 SQL Server 实例启用了 TCP，并且设置为使用静态端口。|错误|SQL Server|
|**SQL Server 版本**|验证指定站点数据库服务器上是否安装了支持的 SQL Server 版本。 有关详细信息，请参阅[对 System Center Configuration Manager 的 SQL Server 版本的支持](../../../../core/plan-design/configs/support-for-sql-server-versions.md)。|错误|SQL Server|
|**升级所不支持的站点系统操作系统版本**|进行升级时，此规则检查运行 Windows Server 2008 或更早版本的计算机上是否安装了除分发点以外的站点系统角色。<br><br>**注意**：因为该检查无法解析将 Intune 和 Configuration Manager 集成后，Azure 中安装的或者是为 Microsoft Intune 使用的云存储安装的站点系统角色的状态，所以可以将这些角色的警告作为误报而忽略。|警告|主站点、 <br>辅助站点|
|**在扩展主站点上不受支持的“资产智能同步点”站点系统角色**|检查资产智能同步点站点系统角色是否未安装在要扩展的独立主站点上。|错误|管理中心站点|
|**在扩展主站点上不受支持的“Endpoint Protection 点”站点系统角色**|检查 Endpoint Protection 点站点系统角色是否未安装在要扩展的独立主站点上。|错误|管理中心站点|
|**在扩展主站点上不受支持的“Microsoft Intune 连接器”站点系统角色**|检查 Microsoft Intune 连接器站点系统角色是否未安装在要扩展的独立主站点上。|错误|管理中心站点|
|**已安装用户状态迁移工具 (USMT)**|检查是否安装了适用于 Windows 8.1 的 Windows 评估和部署工具包 (ADK) 的用户状态迁移工具 (USMT) 组件。|错误|管理中心站点、 <br>主站点（仅独立）|  
|**验证 SQL Server 计算机的 FQDN**|检查你为 SQL Server 计算机指定的 FQDN 是否有效。|错误|SQL Server|
|**验证管理中心站点版本**|检查管理中心站点是否具有相同的 Configuration Manager 版本。|错误|主站点|
|**验证站点服务器发布到 Active Directory 的权限**|验证站点服务器的计算机帐户对 Active Directory 域中的 **“系统管理”** 容器是否具有 **“完全控制”** 权限。 有关配置所需权限的选项的详细信息，请参阅[为站点发布准备 Active Directory](../../../../core/plan-design/network/extend-the-active-directory-schema.md)。<br><br>**注意**：如果已手动验证权限，则可以忽略此警告。|警告|管理中心站点、 <br>主站点、 <br>辅助站点|
|**已安装 Windows 部署工具**|检查是否安装了适用于 Windows 10 的 Windows ADK 的 Windows 部署工具组件。|错误|SMS 提供程序|
|**Windows 故障转移群集**|检查具有管理点或分发点的计算机是否并非 Windows 群集的一部分。|错误|管理点<br>分发点|
|**已安装 Windows 预安装环境**|检查是否安装了适用于 Windows 10 的 Windows ADK 的 Windows 预安装环境组件。|错误|SMS 提供程序|
|**Windows 远程管理 (WinRM) 1.1 版**|验证主站点服务器或 Configuration Manage 控制台计算机上是否安装了 WinRM 1.1 以运行带外管理控制台。 有关如何下载 WinRM 1.1 的详细信息，请参阅 Microsoft 知识库 [文章 936059](https://support.microsoft.com/en-us/kb/936059) 。|警告|主站点、 <br>Configuration Manager 控制台|
|**站点服务器上的 WSUS**|验证站点服务器上是否安装了 Windows Server Update Services (WSUS) 3.0 Service Pack 2 (SP2)。 在不是站点服务器上的计算机上使用软件更新点时，必须在站点服务器上安装 WSUS 管理控制台。 有关 WSUS 的详细信息，请参阅 [Windows Server 更新服务](http://go.microsoft.com/fwlink/p/?LinkID=79477)。|警告|管理中心站点、 <br>主站点|  

##  <a name="BKMK_Requirements"></a> 针对系统需求的先决条件检查  
下表列出了先决条件检查程序针对系统需求执行的检查。  

|已执行的检查|说明|严重性|站点适用性|
|---|---|---|---|
|**Active Directory 域功能级别检查**|验证 Active Directory 域功能级别是否最低为 Windows Server 2008 R2。|警告|管理中心站点、 <br>主站点|
|**检查服务器服务是否正在运行**|验证服务器服务是否已启动。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|  
|**域成员身份**|验证 Configuration Manager 计算机是否为 Windows 域的成员。|错误|管理中心站点、 <br>主站点、 <br>辅助站点、 <br>SMS 提供程序、 <br>SQL Server|
|**域成员身份**|验证 Configuration Manager 计算机是否为 Windows 域的成员。|警告|管理点、 <br>分发点|
|**站点服务器上的 FAT 驱动器**|检查是否已使用 FAT 文件系统格式化了磁盘驱动器。 为提高安全性，在使用 NTFS 文件系统格式化的磁盘驱动器上安装站点服务器组件。|警告|主站点|
|**站点服务器上的可用磁盘空间**|为安装站点服务器，站点服务器计算机至少必须有 15 GB 的可用磁盘空间。 如果将 SMS 提供程序站点系统角色安装在同一台计算机上，则必须有 1 GB 的额外可用空间。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**正在等待系统重启**|检查在你运行安装程序之前另一个程序是否需要重启服务器。|错误|管理中心站点、 <br>主站点、 <br>辅助站点、 <br>Configuration Manager 控制台、 <br>SMS 提供程序、 <br>SQL Server、 <br>管理点、 <br>分发点|
|**只读域控制器**|只读域控制器 (RODC) 上不支持站点数据库服务器和辅助站点服务器。 有关详细信息，请参阅 Microsoft 知识库中的 [You may encounter problems when installing SQL Server on a domain controller](http://go.microsoft.com/fwlink/p/?LinkId=264856)（在域控制器上安装 SQL Server 时可能会遇到的问题）。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**架构扩展**|确定 Active Directory 域服务架构是否已扩展，如果已扩展，则确定所使用的架构扩展的版本。 对于站点服务器安装，不要求进行 Configuration Manager Active Directory 架构扩展，但是建议执行此操作以便充分使用 Configuration Manager 的所有功能。 有关扩展架构的优势的详细信息，请参阅[为站点发布准备 Active Directory](../../../../core/plan-design/network/extend-the-active-directory-schema.md)。|警告|管理中心站点、 <br>主站点|
|**站点服务器 FQDN 长度**|检查站点服务器计算机的 FQDN 的长度。|错误|管理中心站点、 <br>主站点、 <br>辅助站点|
|**不受支持的 Configuration Manager 控制台操作系统**|验证 Configuration Manager 控制台是否可安装在运行支持的操作系统版本的计算机上。 有关详细信息，请参阅 [System Center Configuration Manager 控制台支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-consoles)。|错误|Configuration Manager 控制台|
|**安装程序不支持的站点服务器操作系统版本**|验证服务器上是否运行支持的操作系统。 有关详细信息，请参阅 [System Center Configuration Manager 站点系统服务器支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)。|错误|管理中心站点、 <br>主站点、 <br>辅助站点、 <br>Configuration Manager 控制台、 <br>管理点、 <br>分发点|
|**验证数据库一致性**|从 1602 版开始，此检查用于验证数据库一致性。|错误|管理中心站点、 <br>主站点|  
