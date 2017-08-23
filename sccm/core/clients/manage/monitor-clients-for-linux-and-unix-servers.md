---
title: "監視 Linux/UNIX 用戶端 - Configuration Manager | Microsoft Docs"
description: "在 System Center Configuration Manager 中監視 Linux 和 UNIX 伺服器上的用戶端。"
ms.custom: na
ms.date: 08/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 62843bd544217734c4566d656a7c3a35bd5613cb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中監視 Linux 和 UNIX 伺服器的用戶端

*適用於：System Center Configuration Manager (最新分支)*

您可以在 System Center Configuration Manager 主控台檢視來自 Linux 和 UNIX 伺服器的資訊，所使用的方法與用來檢視 Windows 用戶端資訊的方法相同。  

 您可以檢視的這些資訊包括：  

-   來自用戶端的狀態詳細資料，位於 Configuration Manager 主控台儀表板  

-   預設 Configuration Manager 報告中的用戶端詳細資料  

-   資源總管中的清查詳細資料  

 下列小節說明如何透過資源總管和報告取得這些詳細資訊。  

##  <a name="BKMK_UseResourceExpforLnU"></a> 使用資源總管來檢視 Linux 和 UNIX 伺服器的清查  

 Configuration Manager 用戶端將硬體清查提交給 Configuration Manager 站台之後，您可以使用資源總管檢視這項資訊。 Linux 和 UNIX 的 Configuration Manager 用戶端不會將新的清查類別或檢視新增至資源總管。 Linux 和 UNIX 清查資料對應至現有的 WMI 類別。 您可以使用資源總管，在 Windows 架構的分類中檢視 Linux 和 UNIX 伺服器的清查詳細資料。  

 例如，您可以收集 Linux 和 UNIX 伺服器上找到的所有原生安裝程式清單。 原生安裝程式的範例包括在 Linux 或 **.pkgs** Solaris 中的 **.rpms** 。 Linux 或 UNIX 用戶端已提交清查之後，您可以在 Configuration Manager 主控台的資源總管中檢視所有原生安裝的 Linux 或 UNIX 程式清單。  

 如需如何使用資源總管的相關資訊，請參閱[如何使用資源總管檢視 System Center Configuration Manager 中的硬體清查](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)。  

##  <a name="BKMK_UseReportsforLnU"></a> 如何使用報告檢視 Linux 和 UNIX 伺服器的資訊  
 Configuration Manager 的報告包含 Linux 和 UNIX 伺服器的資訊，以及 Windows 電腦的資訊。 不需其他組態，也能將 Linux 和 UNIX 資料整合在報表中。  

 例如，如果您執行名為 [計算作業系統版本] 的報表時，它會顯示不同的作業系統和執行每個作業系統的用戶端數目清單。 報告根據執行不同作業系統的不同 Configuration Manager 用戶端所傳送的硬體清查資訊而定。  

 此外，也可以建立 Linux 和 UNIX 伺服器資料特定的自訂報表。 硬體清查類別 **作業系統** 的 **標題** 屬性，是實用的屬性，可讓您識別在報表查詢中的特定作業系統。  

 如需 Configuration Manager 報告的相關資訊，請參閱 [System Center Configuration Manager 中的報告](../../../core/servers/manage/reporting.md)。  
