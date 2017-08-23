---
title: "更新和淘汰應用程式 | Microsoft Docs"
description: "使用 System Center Configuration Manager 修改、取代或解除安裝已部署的應用程式。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 805e04c447747b4d12350b692880dbc005bd7168
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 更新及淘汰應用程式

*適用於：System Center Configuration Manager (最新分支)*


最後，您可能會想要變更應用程式、解除安裝應用程式，或將已部署的應用程式取代為新的應用程式。 System Center Configuration Manager 提供下列功能，協助您更新和淘汰應用程式：  

-   **修訂應用程式**。 變更應用程式或部署類型時，Configuration Manager 會維護這些變更的歷程記錄。 您隨時都可以將應用程式還原到先前的修訂版本。 您也可以檢視其內容、還原之前的應用程式修訂，或刪除舊的修訂。  

  如需詳細資訊，請參閱[應用程式修訂](revise-and-supersede-applications.md#application-revisions)。  

-   **取代應用程式**。 您可以使用取代關聯性升級或取代現有應用程式。 當您取代應用程式時，您可以指定新的部署類型來取代被取代應用程式的部署類型。 您也可以設定是否要先升級或解除安裝已取代的應用程式，再安裝取代的應用程式。  

  如需詳細資訊，請參閱[應用程式取代](revise-and-supersede-applications.md#application-supersedence)。  

-   **解除安裝應用程式**。 Configuration Manager 可輕鬆地解除安裝應用程式。 這可以透過無訊息方式完成，而不需要應用程式或裝置使用者介入。  

  如需詳細資訊，請參閱[解除安裝應用程式](uninstall-applications.md)。  
