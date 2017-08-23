---
title: "集合簡介 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用集合的簡介。"
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: "8"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 547d231d48ccbc8241e9f1f8f71e3750b266b73e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager 的集合簡介

*適用於：System Center Configuration Manager (最新分支)*

集合可協助您將資源組織成可管理的單位。 您可以建立集合來符合用戶端管理需求，以及一次執行多個資源上的作業。 

大部分的管理工作會依賴或需要使用一或多個集合。 雖然您可以使用內建的 [所有系統] 集合，但使用此集合來執行管理工作並非最佳做法。 建立自訂集合，更明確地識別工作的裝置或使用者。  

 內建和自訂的集合都會顯示在 Configuration Manager 主控台下 [資產與相容性] 工作區中的 [使用者集合] 及 [裝置集合] 節點中。  

 您最近檢視過的集合都會顯示在 [資產與相容性] 工作區中的 [使用者] 節點及 [裝置] 節點中。  

以下是一些集合使用範例：  

|作業|範例|  
|---------|-------|  
|群組化資源|您可以建立集合，根據組織階層來群組資源。<br /><br /> 例如，您可以建立所有位於倫敦總部 Active Directory 組織單位 (OU) 之電腦的集合。 如需如何建立這種集合類型的詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../../../core/clients/manage/collections/create-collections.md)。<br /><br /> 您可以使用此集合來進行 Endpoint Protection 設定、設定裝置電源管理設定，或安裝 Configuration Manager 用戶端之類的作業。|  
|[應用程式部署]|您可以建立未安裝 Microsoft Office 2013 的所有電腦的集合，接著將其部署至該集合中的所有電腦。<br /><br /> 您也可以使用應用程式需求以執行此工作。 如需詳細資訊，請參閱[如何使用 System Center Configuration Manager 建立應用程式](../../../../apps/deploy-use/create-applications.md)。|  
|[管理用戶端設定](../../../../core/clients/deploy/about-client-settings.md)|雖然 Configuration Manager 中的預設用戶端設定套用到所有的裝置及使用者，您可以建立自訂用戶端設定，套用至裝置或使用者的集合。<br /><br /> 例如，如果您想要在大多數裝置上使用遠端控制、設定預設用戶端設定以允許遠端控制，接著設定不允許遠端控制的自訂用戶端設定，然後將其部署到例外狀況用戶端的集合。 |  
|[電源管理](../power/introduction-to-power-management.md)|您可以針對每個集合設定專屬的電源設定。|  
|[以角色為基礎的系統管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|使用集合來控制哪些使用者群組可以在 Configuration Manager 主控台中存取各種功能。|  
|[維護期間](../../../../core/clients/manage/collections/use-maintenance-windows.md)|透過維護期間，當裝置集合的成員上可執行多種 Configuration Manager 作業時，您就能定義時間週期。 |  


## <a name="collection-types-in-configuration-manager"></a>Configuration Manager 中的集合類型  
 Configuration Manager 具備一般作業的內建集合，而您也可以建立自訂集合。   

### <a name="built-in-collections"></a>內建集合  
 根據預設，Configuration Manager 包含下列無法修改的集合。  

|**集合名稱**|說明|  
|-------------------------|-----------------|  
|**所有使用者群組**|包含使用 Active Directory 安全性群組探索所探索到的使用者群組。|  
|**所有使用者**|包含使用 Active Directory 使用者探索所探索到的使用者。|  
|**所有使用者及使用者群組**|包含所有使用者及所有使用者群組集合。 此集合包含使用者及使用者群組資源的最大範圍。|  
|**所有桌面及伺服器用戶端**|包含安裝 Configuration Manager 用戶端的伺服器及桌面裝置。 成員資格是由活動訊號探索維護。|  
|**所有行動裝置**|包含由 Configuration Manager 管理的行動裝置。 成員資格僅限於成功指派至站台或由 Exchange Server 連接器所探索到的這些行動裝置。|  
|**所有系統**|包含所有桌面和伺服器用戶端、所有行動裝置、所有未知電腦集合，以及由 Microsoft Intune 所註冊的所有行動裝置。 此集合包含裝置資源的最大範圍。|  
|**所有未知電腦**|包含多個電腦平台的一般電腦記錄。 您可以透過此集合使用工作順序和 PXE 開機、 可開機媒體，或預先設置的媒體以部署作業系統。|  

### <a name="custom-collections"></a>自訂集合  
 當您在 Configuration Manager 中建立自訂集合時，該集合的成員資格是由一或多個集合規則所決定，如[如何在 System Center Configuration Manager 中建立集合](../../../../core/clients/manage/collections/create-collections.md)中所述。 

