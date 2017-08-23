---
title: "診斷資料集合 | Microsoft Docs"
description: "了解 System Center Configuration Manager 如何收集本身的診斷及使用方式資料。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9c0165212fe34f460be2ce870d0542b616f3bc4d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>System Center Configuration Manager 如何收集診斷和使用方式資料

*適用於：System Center Configuration Manager (最新分支)*

為了收集 System Center Configuration Manager 的診斷和使用方式資料，每個主要站台每週都會執行 SQL Server 查詢。 在多站台階層中，會將資料複寫至管理中心網站。  

在頂層站台中，服務連接點站台系統角色會在檢查是否有更新時送出這項資訊。 服務連接點的模式決定資料傳輸方式︰  

-   **在線上模式中** ：會自動從服務連接點每週傳送一次診斷和使用方式資料給雲端服務。  

-   **在離線模式中︰** 需使用服務連線工具，以手動方式，傳送診斷和使用方式資料。 如需詳細資訊，請參閱 [使用 System Center Configuration Manager 的服務連接工具](../../../core/servers/manage/use-the-service-connection-tool.md)。  

如需詳細資訊，請參閱 [關於 System Center Configuration Manager 中的服務連線點](../../../core/servers/deploy/configure/about-the-service-connection-point.md)。  
