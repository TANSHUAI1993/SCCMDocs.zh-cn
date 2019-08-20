---
title: 监视数据库复制
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 层次结构中监视 SQL Server 复制。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 69550b35-bcdb-4b47-bbec-b3c8bc92bb7b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f8312202b4877ebcd9a30f5dd40858d119a123de
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957837"
---
# <a name="monitor-database-replication"></a>监视数据库复制

适用范围：  System Center Configuration Manager (Current Branch)

使用 Configuration Manager 控制台“监视”工作区中的“数据复制”节点监视数据库复制的详细信息   。 可以监视站点之间的复制链接的状态。 还显示要连接到的站点的复制组的初始化和复制。  

> [!TIP]  
> 尽管“数据库复制”  节点还出现在“管理”  工作区的“层次结构配置”  节点下，但你无法从该位置中查看数据库复制链接的复制状态。  

## <a name="BKMK_MonitorReplicationLinks"></a> 复制链接状态  

站点之间的数据库复制涉及到若干组信息的复制，称为复制组  。 每个复制组发送和接收具有不同优先级的数据。 默认情况下，无法修改复制组中包含的数据以及复制的频率。  

当复制链接处于活动状态且其状态未处于失败或降级状态时，所有组都可以快速复制。 如果一个或多个组在预期的时间段中无法完成复制，则链接将显示为降级  。 降级的链接仍然可以正常工作，但应对其监视以确保它们返回到活动状态。 调查这些链接，以确保不会发生其他降级或复制失败情况。  

为每个复制链接指定未成功复制的组重试的次数。 在达到此重试次数后，站点将链接的状态设置为降级或失败。 即使除了一个组之外的所有组均成功复制，则该站点也会将链接的状态设置为降级或失败。 设置为此状态，因为一个复制组无法在指定的尝试次数内完成复制。 有关详细信息，请参阅[数据库复制阈值](/sccm/core/plan-design/hierarchy/database-replication#BKMK_DBRepThresholds)。  

使用以下信息来了解可能需要进一步调查的复制链接的状态：  

### <a name="link-is-active"></a>链接处于活动状态

未检测到任何问题，并且链接上的通信正在进行。

当父站点正在升级到新版本，并且你从子站点中查看链接状态时，链接状态将显示为活动。 更新之后，直到子站点与父站点的版本相同。当从父站点查看时，链接状态显示为活动。 从子站点查看时，链接显示为已配置。  

### <a name="link-is-degraded"></a>链接已降级

复制正常运行，但至少一个复制对象或组已延迟。 监视处于此状态的链接。 查看链接上两个站点中的信息了解链接可能失败的迹象。

当收到复制的数据的站点无法将数据快速提交到数据库时，链接也可能显示降级状态。 在复制大量数据时，会发生这种情况。 例如，将软件更新部署到大量计算机。 链接上的父站点可能需要一些时间来处理此复制的数据量。 父站点上的处理延迟会导致将链接状态设置为降级，直至它可成功处理积压数据为止。

### <a name="link-has-failed"></a>链接已失败

复制无法正常工作。 复制链接可能无需进行进一步操作便可恢复。 若要调查并帮助修正此链接上的复制，则可以使用复制链接分析器 (RLA)。

此状态也可能指示复制链接上父站点和子站点之间的物理网络的问题。


## <a name="BKMK_MonitorReplicationStatus"></a> 监视复制状态

使用“监视”  工作区中的“数据复制”  节点以查看复制链接的状态。 在复制链接的每个站点上查看有关数据库的详细信息。 你还可以查看有关复制组的详细信息。 要查看这些详细信息，请选择复制链接，然后为要查看的复制状态选择相应的选项卡。

以下部分详细介绍复制状态的不同选项卡：

### <a name="summary"></a>摘要

查看有关链接上两个站点之间的站点数据和全局数据复制的高级信息。  

选择“查看历史流量数据报表”  来查看一个报表，其中显示有关链接上的复制所使用的网络带宽的详细信息。  

### <a name="parent-site"></a>父站点

对于复制链接上的父站点，查看有关数据库的详细信息，其中包括：  

- SQL Server 的防火墙端口  

- 可用磁盘空间  

- 数据库文件位置  

- 证书  

### <a name="child-site"></a>子站点

对于复制链接上的子站点，查看有关数据库的详细信息，其中包括：  

- SQL Server 的防火墙端口  

- 可用磁盘空间  

- 数据库文件位置  

- 证书  

### <a name="initialization-detail"></a>初始化详细信息

查看通过链接进行复制的组的初始化状态。 此信息可帮助你确定复制数据的初始化何时正在进行或已失败。  

使用此信息来确定站点何时可能处于互操作性模式  。 当子站点运行的 Configuration Manager 版本与父站点不同时，将会出现互操作性模式。  

### <a name="replication-detail"></a>复制详细信息

查看通过链接进行复制的每个组的复制状态。 使用此信息来帮助确定特定数据复制的问题或延迟。 它可以帮助确定此链接的相应数据库复制阈值。 有关详细信息，请参阅[数据库复制阈值](/sccm/core/plan-design/hierarchy/database-replication#BKMK_DBRepThresholds)。  

> [!TIP]  
> 站点数据的复制组只会从子站点发送到父站点。 全局数据的复制组则以双向方式复制。  


## <a name="BKMK_RLA"></a> 复制链接分析器

Configuration Manager 包括复制链接分析器  (RLA)，你使用该分析器来分析和修复复制问题。 复制失败时，使用 RLA 修正链接失败。 当复制停止工作但该站点尚未将其报告为失败时，RLA 也非常有用。

使用 RLA 修正层次结构中以下计算机之间的复制问题：  

- 站点服务器和站点数据库服务器之间  

- 站点的数据库服务器和另一个站点的数据库计算机之间，也称为站点间复制  

> [!Note]  
> 复制失败的方向无关紧要。

在 Configuration Manager 控制台中或命令提示符处运行 RLA：  

- 在 Configuration Manager 控制台中运行：转到“监视”工作区，选择“数据库复制”节点   。 选择要分析的复制链接，然后在功能区中，选择“复制链接分析器”  。  

- 要在命令提示符处运行，请键入以下命令：`%ProgramFiles(x86)%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe <source site server FQDN> <destination site server FQDN>`  

运行 RLA 时，它将使用一系列诊断规则和检查来检测问题。 查看该工具确定的问题。 在 RLA 有解决问题的说明时，则会将其显示出来。 如果 RLA 可以自动修正问题，则会显示该选项。

当 RLA 完成时，它将结果保存在以下基于 XML 的报表以及运行该工具的用户桌面上的一个日志文件中：  

- ReplicationAnalysis.xml  

- ReplicationLinkAnalysis.log  

RLA 在修正某些问题时会停止以下服务。 修正完成后，它会重启这些服务：  

- SMS_SITE_COMPONENT_MANAGER  

- SMS_EXECUTIVE  

如果 RLA 无法完成修正，请在必要时在站点服务器上重启这些服务。  

RLA 记录所有调查和修正操作，以提供其未在向导中显示的其他详细信息。  

### <a name="rla-prerequisites"></a>RLA 先决条件

用于运行 RLA 的帐户必须具有下列权限：

- 复制链接中涉及的每台计算机上的本地管理员权限。

- 复制链接中涉及的每个 SQL Server 数据库上的 Sysadmin 权限。  

> [!Note]  
> 此帐户不需要特定的基于 Configuration Manager 角色的管理安全角色。 有权访问“数据库复制”  的管理用户可在 Configuration Manager 控制台中运行该工具。 对每台计算机有足够权限的系统管理员可以在命令提示符处运行该工具。  

### <a name="rla-known-issue"></a>RLA 的已知问题

RLA 为从 System Center 2012 Configuration Manager 升级的主站点生成 SQL Server Service Broker (SSB) 证书错误。 由于 Configuration Manager 当前分支中的证书名称发生了更改，导致产生此问题。 可以放心地忽略这些错误。  


## <a name="BKMK_ProcsforMonitoringReplication"></a> 监视数据库复制  

### <a name="monitor-high-level-site-to-site-database-replication-status"></a>监视高级别站点到站点数据库复制状态

1. 在 Configuration Manager 控制台中，转到“监视”  工作区。  

2. 选择“站点层次结构”  节点以打开“层次结构关系图”  视图。  

3. 将鼠标指针悬停在两个站点之间的线上。 查看这些站点的全局数据复制和站点数据复制的状态。  

### <a name="monitor-the-status-of-a-replication-link"></a>监视复制链接的状态

1. 在 Configuration Manager 控制台中，转到“监视”  工作区。  

2. 选择“数据库复制”  节点，然后选择要监视的复制链接。 然后，选择相应的选项卡以查看有关该链接的复制状态的不同详细信息。  
