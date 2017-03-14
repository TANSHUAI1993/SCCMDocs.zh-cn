---
title: "新版本 1702 |Microsoft Docs"
description: "获取有关 System Center Configuration Manager 的 1702 版中引入的更改和新功能的详细信息。"
ms.custom: na
ms.date: 03/27/2017
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: 473ba742bea74cbfdf8cab550244ccd522523718
ms.lasthandoff: 03/04/2017

---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>System Center Configuration Manager 版本 1702 中的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager Current Branch 的更新 1702 作为控制台内更新提供，用于运行版本 1606 或 1610 的以前安装的站点。 安装新部署时，也可将其作为基准版本使用。

> [!TIP]  
> 若要安装新站点，必须使用 Configuration Manager 的基准版本。  
>  了解详细信息：    
>  -   [安装新站点](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [在站点上安装更新](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [基准和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

以下各节提供有关 Configuration Manager 版本 1702 中引入的更改和新功能的详细信息。  


## <a name="data-warehouse-service-point"></a>数据仓库服务点
使用数据仓库服务点存储和报告关于 Configuration Manager 部署的长期历史数据。

数据仓库最多支持 2 TB 数据，且具有跟踪更改的时间戳。 通过从 Configuration Manager 站点数据库自动同步到数据仓库数据库可实现数据存储。 然后，可从 Reporting Services 点访问此信息。



有关详细信息，请参阅[数据仓库服务点](/sccm/core/servers/manage/data-warehouse)。

