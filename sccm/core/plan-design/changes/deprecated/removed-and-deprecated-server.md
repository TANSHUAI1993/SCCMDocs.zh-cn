---
title: Configuration Manager 站点服务器中已弃用的项
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager 站点服务器不再支持的产品和操作系统。
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b92eb8083ce886fcab4d9957b2a79999d72a1a5a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="removed-and-deprecated-for-system-center-configuration-manager-site-servers"></a>System Center Configuration Manager 站点服务器中已删除和已弃用的项

*适用范围：System Center Configuration Manager (Current Branch)*

本文介绍 System Center Configuration Manager 站点服务器的支持中删除的，或者将在未来更新中删除（弃用）的产品和操作系统。 本文预告了可能会影响 Configuration Manager 的使用的未来变更。  

此信息在将来版本中可能有所变化，并且可能不会包括每一个弃用的功能、产品或操作系统。  


## <a name="deprecated-server-operating-systems"></a>已弃用的服务器操作系统  

|**操作系统**|**首次宣布弃用**|**删除的支持** |  
|-|-|-| 
|Windows Server 2008 R2|2015 年 10 月| 版本 1702（请参阅注释 1）| 
|Windows Server 2008|2015 年 10 月|版本 1511 </br></br>删除了作为站点系统的支持。 （请参阅注释 2）。|  

>[!NOTE]
>-   从 1702 版本开始，站点服务器或大多数站点系统角色不再支持 Windows Server 2008 R2。 但会继续支持使用 1702 之前的版本。 此操作系统仍然支持分发点站点系统角色（包括拉取分发点，而且适用于 PXE 和多播），直到宣布弃用支持，或者操作系统的扩展支持期到期。 从版本 1602 开始，可以对站点服务器的操作系统进行就地升级，从 Windows Server 2008 R2 升级到 Windows Server 2012 R2。  
>- 有关站点服务器操作系统就地升级的详细信息，请参阅 [升级支持 System Center Configuration Manager 的本地基础结构](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)中的[就地升级运行 Windows Server 2008 R2 的站点服务器的操作系统](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2)部分。

>[!NOTE]
>-   除分发点和拉取分发点外，站点服务器或站点系统角色均不支持 Windows Server 2008。 可以继续使用操作系统作为分发点，直到支持被宣布弃用或者操作系统的扩展支持期到期为止。 有关详细信息，请参阅 [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095)（在 Windows Server 2008 上安装 System Center Configuration Manager CB 和 LTSB 失败）。

## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>SQL Server 版本作为站点数据库的已弃用支持  

|**SQL Server 版本**|**首次宣布弃用**|**删除的支持**|   
|-|-|-| 
|SQL Server 2008 R2|2015 年 10 月|版本 1702| 
|SQL Server 2008|2015 年 10 月|版本 1511|  


如果需要升级 SQL Server 版本，建议采用以下由易到难的方法。
1. [就地升级 SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server)（推荐）。
2. 在一台新计算机上安装 SQL Server 的新版本。 然后使用 Configuration Manager 设置的[数据库移动选项](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration)指向新SQL Server 上的站点服务器。
3. 使用[备份和恢复](/sccm/protect/understand/backup-and-recovery)。


## <a name="more-information"></a>更多信息
有关详情，请参阅：
 - [已删除和已弃用的项](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)网站。
 - [对 Configuration Manager Current Branch 版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)。