---
title: "使用界限和界限群組 | Microsoft Docs"
description: "使用界限和界限群組來為您管理的裝置，定義網路位置與可存取的站台系統。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fea1dece0768a2b7bcd3fcedc2288ea2d52e73d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 定義站台界限和界限群組

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 的界限會在您的內部網路上定義網路位置，其中可包含您要管理的裝置。 界限群組是您所設定界限的邏輯群組。

 階層可以包含任意數目的界限群組，每個界限群組可包含下列界限類型的任意組合：  

-   IP 子網路、  
-   Active Directory 站台名稱  
-   IPv6 首碼  
-   IP 位址範圍  

內部網路上的用戶端會評估其目前網路位置，然後使用該資訊來識別所屬界限群組。  

 用戶端將界限群組用於：  
-   **尋找指派的站台：** 界限群組可讓用戶端在主要站台尋找用戶端指派 (自動站台指派)。  
-   **尋找可用的特定站台系統角色：**當您將界限群組與特定站台系統角色建立關聯時，該界限群組會為用戶端提供站台系統清單，以供用於內容位置和作為慣用的管理點。  

位於內部網路上的用戶端或設為僅限內部網路的用戶端不會使用界限資訊。 這些用戶端無法使用自動站台指派，並且一律會在發佈點設定為允許網際網路用戶端連線時，從其指派的站台內任何發佈點下載內容。  

**開始著手：**
- 首先，[將網路位置定義成界限](/sccm/core/servers/deploy/configure/boundaries)。
- 然後，繼續[設定界限群組](/sccm/core/servers/deploy/configure/boundary-groups)，將這些界限中的用戶端與其可用的站台系統伺服器建立關聯。



##  <a name="BKMK_BoundaryBestPractices"></a> 界限和界限群組的最佳做法  

-   **使用符合您需求的最少界限混合︰**  
   在過去，我們會建議優先使用某些界限類型。 現在因為改善效能的變更，我們建議您使用所選的任一界限類型，只要適合您的環境並可讓您使用最少的界限簡化管理工作。      

-   **避免自動站台指派的重複界限：**  
     雖然每個界限群組都同時支援站台指派設定和內容位置組態，最佳的做法仍是建立僅適用於站台指派的個別界限群組。 意義：確保界限群組中的每個界限不屬於另一個具有不同站台指派的界限群組。 原因：  

    -   單一界限可包含在多個界限群組中  

    -   每個界限群組都可以和不同主要站台建立關係以進行站台指派  

    -   界限上屬於兩個不同界限群組且站台指派互異的用戶端，會隨機選取站台加入，而這不一定會是您希望用戶端加入的站台。  此組態稱為重複界限。  

     重複界限對於內容位置而言不是問題而是想要的組態，可提供用戶端其他資源，或可用的內容位置。  
