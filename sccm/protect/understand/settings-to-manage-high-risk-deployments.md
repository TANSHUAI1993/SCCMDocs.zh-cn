---
title: "管理高風險部署 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中設定站台設定，於系統管理員建立高風險部署時發出警告。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8b5564f39f07a67a3c9278379ed59ca415603d21
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="settings-to-manage-high-risk-deployments-for-system-center-configuration-manager"></a>管理 System Center Configuration Manager 高風險部署的設定

*適用於：System Center Configuration Manager (最新分支)*


您可以使用 System Center Configuration Manager 設定站台設定，於系統管理員建立高風險工作順序部署時發出提醒。 高風險部署的定義：  

-   自動安裝的部署  

-   有可能會導致非預期的結果  

 例如，以**必要**用途部署作業系統的工作順序，會被視為高風險。  

 若要降低不需要的高風險部署所帶來的風險，您可以設定這些部署驗證設定中的大小限制：  

-   **限制集合大小**：當您建立部署時，隱藏所含用戶端數目超過限制的集合。  

    -   **預設大小**：當您建立部署時，此設定預設會隱藏所含用戶端數目超過限制的集合。 您仍然可以在建立部署時看到這些集合，但預設會予以隱藏。 預設值為 100。 輸入的值為 0 時可忽略此設定。  

    -   **大小上限**：當您建立部署時，此設定一律會隱藏所含用戶端數目超過限制的集合。 預設值是 0，忽略此設定。 [大小上限]  的值必須大於 [預設大小]  的值。  

     例如，將 [預設大小] 設為 100，而 [大小上限] 設為 1000。 當您建立高風險部署時，[選取集合] 視窗只會顯示所含用戶端少於 100 個的集合。 如果您清除 [隱藏成員計數大於站台大小上限設定的集合] 設定，則此視窗會顯示所含用戶端少於 1000 個的集合。  

-   **包含站台系統伺服器的集合**：當目標集合包含具有站台系統角色的電腦時封鎖部部署，或在建立部署之前要求驗證。 當部署遭到封鎖時，您必須選取另一個符合部署驗證準則的集合。  

> [!NOTE]  
>  高風險的部署一律限制於自訂集合、您建立的集合，以及內建的 [未知的電腦]  集合。 當您建立高風險的部署時，您無法選取 [所有系統] 這類的內建集合。  

### <a name="to-configure-deployment-verification-for-a-site"></a>設定站台的部署驗證  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [站台設定] > [站台]，然後選取要設定的主要站台。  

2.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]，然後選擇 [部署驗證] 索引標籤。  

3.  設定您要使用的組態設定之後，請選擇 [確定] 儲存設定。  

### <a name="see-also"></a>請參閱  
 [為 System Center Configuration Manager 設定站台和階層](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)
