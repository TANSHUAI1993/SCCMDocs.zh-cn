---
title: 站点服务器弃用的内容
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 站点服务器不再支持的产品和操作系统。
ms.date: 01/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88b192163ac7a947f73ff658f7bafbfc1bfd5e14
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285878"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Configuration Manager 站点服务器已删除和已弃用的内容

适用范围：  System Center Configuration Manager (Current Branch)

本文介绍 Configuration Manager 站点服务器的支持中删除的，或者将在未来更新中删除（弃用）的产品和操作系统。 针对可能会影响使用 Configuration Manager 的将来更改提出早期通知。  

此信息以后可能会有所更改。 它可能不包括每个已弃用的功能、产品或操作系统。  



## <a name="server-os"></a>服务器 OS  

|**操作系统**|**首次宣布弃用**|**删除的支持** |  
|-|-|-| 
|Windows Server 2008 R2 SP1|2015 年 10 月| 版本 1702 <sup>[注释 1](#bkmk_note1)</sup>| 
|带 SP2 的 Windows Server 2008|2015 年 10 月|版本 1511 <sup>[注释 2](#bkmk_note2)</sup>|  

#### <a name="bkmk_note1"></a> 注释 1：Windows Server 2008 R2 SP1
站点服务器或大多数站点系统角色不再支持带有服务包 1 的 Windows Server 2008 R2。 分发点角色仍支持此 OS。 此支持包括拉取分发点、PXE 和多播。 

> [!Important]  
> Windows Server 2008 R2 SP1 的扩展支持结束日期为 2020 年 1 月 14 日。 此日期之后，Configuration Manager 不支持将此操作系统用作任何站点系统角色。 

可以将站点服务器 OS 从 Windows Server 2008 R2 升级到 Windows Server 2012 R2。 有关详细信息，请参阅[就地升级运行 Windows Server 2008 R2 的站点服务器的操作系统](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#BKMK_SupConfigUpgradeSiteSrv)。  


#### <a name="bkmk_note2"></a> 注释 2：带 SP2 的 Windows Server 2008
站点服务器或大多数站点系统角色不再支持带有服务包 2 的 Windows Server 2008。 分发点角色仍支持此 OS。 此支持包括拉取分发点、PXE 和多播。 

> [!Important]  
> Windows Server 2008 SP2 的扩展支持结束日期为 2020 年 1 月 14 日。 此日期之后，Configuration Manager 不支持将此操作系统用作任何站点系统角色。  



## <a name="sql-server"></a>SQL Server   

|**SQL Server 版本**|**首次宣布弃用**|**删除的支持**|   
|-|-|-| 
|SQL Server 2008 R2|2015 年 10 月|版本 1702| 
|SQL Server 2008|2015 年 10 月|版本 1511|  


如果需要升级 SQL Server 版本，建议采用以下由易到难的方法：

1. [就地升级 SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#BKMK_SupConfigUpgradeDBSrv)（推荐）。  

2. 在一台新计算机上安装 SQL Server 的新版本。 然后使用 Configuration Manager 安装程序的[数据库移动选项](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_dbconfig)指向新 SQL Server 上的站点服务器。  

3. 使用[备份和恢复](/sccm/protect/understand/backup-and-recovery)。  



## <a name="more-information"></a>更多信息

有关详细信息，请参阅下列文章： 

- [已删除和已弃用的项](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)  

- [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)  

- [对 Configuration Manager Current Branch 版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)  

