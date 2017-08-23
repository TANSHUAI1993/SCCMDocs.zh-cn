---
title: "設定站台 | Microsoft Docs"
description: "請參閱這份檢查清單，確保考慮到對站台和階層皆有影響的最常見設定。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: "15"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 862f420c063cb44c419d4904fbb4696efb739758
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 設定站台與階層

*適用對象：System Center Configuration Manager (最新分支)*

安裝第一個 System Center Configuration Manager 站台，或將其他站台新增到您的階層之後，使用下列檢查清單可確保您考慮到會影響站台與階層的最常見設定。  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>新站台與和其他站台的一般組態檢查清單  
請留意下列適用於多數部署的設定相關備註：

-   但有些選項是彼此相依的，例如 Active Directory 樹系探索、界限以及界限群組。  

-   其中有一些組態有預設值，無須任何設定變更即可使用 (至少暫時如此)。  

-   而其他組態 (例如界限群組與發佈點群組) 則必須先設定之後才可使用。  

|動作|詳細資料|  
|------------|-------------|  
|設定以角色為基礎的系統管理|分隔系統管理的指派，以控制哪些系統管理使用者可以在 Configuration Manager 環境中檢視及管理不同的物件與資料。<br /><br /> 階層中的所有站台，會共用以角色為基礎之系統管理的組態。   <br/><br/>如需詳細資訊，請參閱[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)。|  
|發佈站台資料至 Active Directory 網域服務 (AD DS)|讓用戶端輕鬆找到服務，並有效率地使用站台資源。<br /><br /> 您必須先[擴充 System Center Configuration Manager 的 Active Directory 架構](../../../../core/plan-design/network/extend-the-active-directory-schema.md)，接著必須個別設定各個站台，以[發佈 System Center Configuration Manager 的站台資料](../../../../core/servers/deploy/configure/publish-site-data.md)|  
|設定服務連接點|規劃在階層的頂層站台安裝及設定服務連接點。 如需詳細資訊，請參閱 [關於 System Center Configuration Manager 中的服務連線點](../../../../core/servers/deploy/configure/about-the-service-connection-point.md)。|  
|新增站台系統角色|為各個站台安裝一個或多個額外的站台系統角色。  如需詳細資訊，請參閱[為 System Center Configuration Manager 新增站台系統角色](../../../../core/servers/deploy/configure/add-site-system-roles.md)。|  
|設定界限與界限群組|指定界限以在您的內部網路上定義網路位置，其中可包含您要管理的裝置。 然後設定界限群組，讓位於那些網路位置的用戶端可以找到 Configuration Manager 資源。 如需詳細資訊，請參閱[為 System Center Configuration Manager 定義站台界限和界限群組](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。|  
|設定發佈點群組|設定發佈點的邏輯群組，讓管理部署更容易。 如需詳細資訊，請參閱[為 System Center Configuration Manager 安裝及設定發佈點](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)中的[管理發佈點群組](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md)。|  
|執行探索工作|執行探索以在網路上尋找資源，包括網路基礎結構、裝置與使用者。<br /><br /> 如需詳細資訊，請參閱 [為 System Center Configuration Manager 執行探索](../../../../core/servers/deploy/configure/run-discovery.md)。|  
|為管理基礎結構的管理員新增備援及容量|安裝其他 SMS 提供者與 Configuration Manager 主控台，為管理基礎結構的系統管理員擴充容量：<br /><br /> **安裝額外的 SMS 提供者**可為連絡點提供備援，以管理站台與階層。 如需詳細資訊，請參閱[修改您的 System Center Configuration Manager 基礎結構](../../../../core/servers/manage/modify-your-infrastructure.md)中的[管理 SMS 提供者](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)。<br /><br /> **安裝其他 Configuration Manager 主控台**可為額外的系統管理使用者提供存取。 如需詳細資訊，請參閱[安裝 Configuration Manager 主控台](../../../../core/servers/deploy/install/install-consoles.md)。|  
|設定站台元件|在每個站台設定站台元件，以修改站台系統角色與站台狀態報告的行為。 如需詳細資訊，請參閱 [System Center Configuration Manager 的站台元件](../../../../core/servers/deploy/configure/site-components.md)。|  
|建立自訂集合|請使用探索到的裝置與使用者相關資訊，建立物件的自訂集合，以簡化日後的管理工作。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../../../core/clients/manage/collections/create-collections.md)。|  
|設定管理高風險部署的設定|在站台進行設定，在系統管理使用者建立高風險的工作順序部署時對其發出警告。  如需詳細資訊，請參閱[管理 System Center Configuration Manager 高風險部署的設定](../../../../protect/understand/settings-to-manage-high-risk-deployments.md)。|  
|為管理點設定資料庫複本|設定資料庫複本，以減少管理點在服務來自用戶端的要求時，加諸站台資料庫伺服器的 CPU 負載。 如需詳細資訊，請參閱 [System Center Configuration Manager 的管理點資料庫複本](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。|  
|設定 SQL Server AlwaysOn 可用性群組來裝載站台資料庫|從 1602 版開始，即可將可用性群組設定為在主要站台及管理中心網站裝載站台資料庫的高可用性和災害復原方案。 如需詳細資訊，請參閱[適用於 System Center Configuration Manager 之高可用性站台資料庫的 SQL Server AlwaysOn](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。|  
|修改站台間的複寫|請參閱 [System Center Configuration Manager 中的站台間資料傳輸](../../../../core/servers/manage/data-transfers-between-sites.md)以了解下列主題：<br /><br /> 設定次要站台之間的[檔案式複寫](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute)<br /><br /> 設定[資料庫複寫連結](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> 設定[分散式檢視](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  
