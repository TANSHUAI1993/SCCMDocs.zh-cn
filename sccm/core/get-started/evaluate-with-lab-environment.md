---
title: "評估 Configuration Manager | Microsoft Docs"
description: "建立實驗室環境，以評估貴組織使用 System Center Configuration Manager 的效能。"
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: "25"
caps.handback.revision: "0"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d7ea785ab1beee09b9adda735a87f89bc9481620
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>建置專屬實驗室環境來評估 System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*

 了解如何建立實驗室環境，以評估貴組織使用 System Center Configuration Manager 的效能。  

 System Center Configuration Manager 是管理使用者、裝置和軟體的工具，複雜且功能強大。 最好先完成 System Center Configuration Manager 的全面評估再進行完整部署，以便結合概念性的了解與實際操作練習。  

 本指南主要適用對象為評估 Configuration Manager 在公司環境中使用效能的系統管理員。  

-   想要全面管理電腦、伺服器和行動裝置之解決方案的系統管理員  

-   要求內部部署裝置管理安全性及雲端式裝置管理靈活性之高安全性產業的系統管理員  

-   想要管理相應增加之內部部署伺服器架構的系統管理員  

## <a name="what-this-lab-does"></a>這個實驗室可以達成的目標  
 建立這個實驗室環境的主要目標是提供開始使用 Configuration Manager 的一般知識，以及加強對 Configuration Manager 的了解。 您將使用兩部伺服器來逐步完成 Configuration Manager 目前版本的快速組件：  

-   一部裝載 Active Directory、網域控制站和 DNS 伺服器  

-   一部裝載 Configuration Manager 和所有相關聯的 SQL Server 元件  

用戶端電腦已安裝在 Hyper-V 內。 實驗室本身也可以當成完全虛擬化的系統，在單一伺服器上執行。  

## <a name="what-this-lab-does-not-do"></a>這個實驗室無法達成的目標  
 這個實驗室不會帶您完成所有 Configuration Manager 案例。 其設計宗旨也不是立即移轉至使用中環境。  

 當您建置這個實驗室時，您會有可以運作的功能環境。 但是這個環境不會為系統效能、硬碟空間管理和 SQL Server 存放裝置這類因素進行最佳化。  

##  <a name="BKMK_EvalRec"></a> 建置實驗室之前的建議閱讀  
 [Documentation for System Center Configuration Manager 文件](http://docs.microsoft.com/sccm/)提供豐富的內容。 建議您在開始建置實驗室之前先閱讀本文件庫中的下列主題︰  

-   如需了解 Configuration Manager 主控台、使用者入口網站和範例案例的核心概念，請參閱 [System Center Configuration Manager 簡介](../../core/understand/introduction.md)。  

-   如需了解 Configuration Manager 的主要管理功能，請參閱 [System Center Configuration Manager 的功能](../../core/plan-design/changes/features-and-capabilities.md)。  

-   閱讀 [System Center Configuration Manager 的基礎](../../core/understand/fundamentals.md)以充實知識。  

-   如需了解安全性角色的重要性，請參閱 [System Center Configuration Manager 以角色為基礎的系統管理基本概念](../../core/understand/fundamentals-of-role-based-administration.md)。  

-   如需了解內容管理，請參閱[內容管理的概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)。  

-   如需了解如何成功支援整個部署的每日作業，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  
