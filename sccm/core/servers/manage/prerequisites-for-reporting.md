---
title: "报告的先决条件"
titleSuffix: Configuration Manager
description: "了解影响在 System Center Configuration Manager 中使用报表的各种依赖关系。"
ms.custom: na
ms.date: 01/29/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: 
caps.handback.revision: 
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 3feafa8a20bedfba381c29a5d7fe80a47517b6ab
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager 中报告的先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的报表具有产品外部依赖关系和产品内依赖关系。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系  
 下表列出了报表的外部依赖关系。  

|先决条件|更多信息|  
|------------------|----------------------|  
|SQL Server Reporting Services|必须安装和配置 SQL Server Reporting Services，然后才能在 Configuration Manager 中使用报表。<br /><br /> 有关在你的环境中规划和部署 Reporting Services 的信息，请参阅 SQL Server 2008 联机丛书中的 [Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) 部分。|  
|运行 Reporting Services 点的计算机的站点系统角色依赖关系。|[System Center Configuration Manager 支持的配置](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Configuration Manager 的内部依赖关系  
 下表列出了 Configuration Manager 中的报表的依赖关系。  

|先决条件|更多信息|  
|------------------|----------------------|  
|Reporting Services 点|必须配置 Reporting Services 点站点系统角色，然后才能在 Configuration Manager 中使用报表。 有关如何安装和配置 Reporting Services 点的详细信息，请参阅[在 Configuration Manager 中配置报表](../../../core/servers/manage/configuring-reporting.md)。|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Reporting Services 点支持的 SQL Server 版本  
 可以将 Reporting Services 数据库安装在 64 位 SQL Server 安装的默认实例或已命名实例上。 SQL Server 实例可与站点系统服务器共存，或位于远程计算机上。  

 下表列出了 Reporting Services 点支持的 SQL Server 版本。  

|SQL Server 版本|Reporting Services 点|  
|------------------------|------------------------------|
|SQL Server 2017（至少包含累积更新 2）<br /><br /> -   Standard<br />-   Enterprise|是，从 Configuration Manager 1710 版开始|  
|SQL Server 2016 SP1<br /><br /> -   Standard<br />-   Enterprise|是| 
|SQL Server 2016<br /><br /> -   Standard<br />-   Enterprise|是|
|SQL Server 2014 with SP2<br /><br /> -   Standard<br />-   Enterprise|是|
|SQL Server 2014 with SP1<br /><br /> -   Standard<br />-   Enterprise|是|
|SQL Server 2012 with SP4 <br /><br /> -   Standard<br />-   Enterprise|是|  
|SQL Server 2012 with SP3 <br /><br /> -   Standard<br />-   Enterprise|是|  
|SQL Server 2008 R2 with SP3<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|是，针对 Configuration Manager 1702 版之前的支持版本。|  
|SQL Server Express 2008 R2 with SP3|不支持| 




## <a name="next-steps"></a>后续步骤
[报表的操作和维护](operations-and-maintenance-for-reporting.md)
