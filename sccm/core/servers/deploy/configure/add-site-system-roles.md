---
title: "新增站台系統角色 | Microsoft Docs"
description: "了解 Configuration Manager 站台系統角色，以及如何新增角色以擴充站台的功能和容量。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1ad4abf1f06ed24bd1d505648280b5e5d80220c7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 新增站台系統角色

*適用對象：System Center Configuration Manager (最新分支)*

每個 System Center Configuration Manager 站台都支援多個站台系統角色。 每個角色都會擴充站台的功能與容量，以提供服務給站台以及管理裝置與使用者。 站台系統伺服器上的每個站台系統角色，都必須來自相同的站台。   

Configuration Manager 不支援單一站台系統伺服器上多個站台的站台系統角色。  

> [!TIP]  
>  如果您不熟悉站台系統角色的基本概念，或不熟悉站台伺服器、站台系統伺服器與站台系統角色之間的差異，請參閱 [Configuration Manager 的基礎](../../../../core/understand/fundamentals.md)。  

 下列主題將詳細說明安裝站台系統角色的程序與相關詳細資料：  

-   [為 System Center Configuration Manager 安裝站台系統角色](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     本主題提供基本指導，讓您了解如何使用兩個主控台內部精靈安裝新站台系統角色。  

-   [在 Microsoft Azure 中，安裝 System Center Configuration Manager 的雲端架構發佈點](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    若您想使用 Microsoft Azure 來裝載部署至用戶端的內容，本主題的資訊能協助您設定必要的憑證檔案，讓 Configuration Manager 與 Microsoft Azure 通訊及使用您的 Microsoft Azure 訂用帳戶。 此外，您必須設定名稱解析，好讓用戶端找到您的雲端式發佈點。  

-   [為 System Center Configuration Manager 中的內部部署行動裝置管理安裝站台系統角色](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     本主題將協助您順利設定您的站台系統角色，以使用 Configuration Manager 內部部署 MDM 來支援管理現代裝置。  

-   [System Center Configuration Manager 之站台系統角色的設定選項](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     有些站台系統角色支援需要更多詳細資料的設定，但使用者介面不足以說明。 本主題提供這些詳細資料。  
