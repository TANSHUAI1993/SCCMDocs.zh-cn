---
title: "報告的必要條件 | Microsoft Docs"
description: "了解影響您在 System Center Configuration Manager 中使用報告的各種相依性。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2e624eb2ea061a4eb7d92365410fada335640224
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager 中報告的必要條件

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的報告具有外部相依性和產品內的相依性。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  
 下表列出報告的外部相依性。  

|必要條件|詳細資訊|  
|------------------|----------------------|  
|SQL Server Reporting Services|您必須先安裝和設定 SQL Server Reporting Services，才能在 Configuration Manager 中使用報告。<br /><br /> 如需有關在您的環境中規劃和部署 Reporting Services 的詳細資訊，請參閱《SQL Server 2008 線上叢書》中的 [Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) 一節。|  
|執行 Reporting Services 點之電腦的站台系統角色相依性。|[System Center Configuration Manager 的支援設定](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Configuration Manager 內部的相依性  
 下表列出 Configuration Manager 中報告的相依性。  

|必要條件|詳細資訊|  
|------------------|----------------------|  
|Reporting Services 點|您必須先設定 Reporting Services 點站台系統角色，才能在 Configuration Manager 中使用報告。 如需如何安裝和設定 Reporting Services 點的詳細資訊，請參閱[在 System Center Configuration Manager 中設定報告](../../../core/servers/manage/configuring-reporting.md)。|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Reporting Services 點支援的 SQL Server 版本  
 Reporting Services 資料庫可以安裝在 64 位元 SQL Server 安裝的預設執行個體或具名執行個體上。 SQL Server 執行個體可以與站台系統伺服器共置，或是位於遠端電腦上。  

 下表列出 Reporting Services 點所支援的 SQL Server 版本。  

|SQL Server 版本|Reporting Services 點|  
|------------------------|------------------------------|  
|SQL Server 2008 SP2 並至少加裝累計更新 9<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|是|  
|SQL Server 2008 SP3 並至少加裝累計更新 4<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|是|  
|SQL Server 2008 R2 SP1 並至少加裝累計更新 6<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|是|  
|SQL Server 2008 R2 SP2<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|是|  
|SQL Server Express 2008 R2 SP1 並至少加裝累計更新 4|不支援|  
|SQL Server Express 2008 R2 SP2|不支援|  
|SQL Server 2012 並至少加裝累計更新 2<br /><br /> -   Standard<br />-   Enterprise|是|  
|SQL Server 2012 SP1 並且沒有累計更新最低要求<br /><br /> -   Standard<br />-   Enterprise|是|  
|SQL Server 2014<br /><br /> -   Standard<br />-   Enterprise|是|
|SQL Server 2016<br /><br /> -   Standard<br />-   Enterprise|是|
|SQL Server 2016 SP1<br /><br /> -   Standard<br />-   Enterprise|是|
## <a name="next-steps"></a>後續步驟
[報告作業和維護](operations-and-maintenance-for-reporting.md)
