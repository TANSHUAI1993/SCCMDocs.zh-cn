---
title: "軟體清查 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的軟體清查簡介。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 969f2d28649853ddc95860fe72597d6d2c9a94e9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的軟體清查簡介

*適用於：System Center Configuration Manager (最新分支)*

軟體清查可用來收集用戶端裝置上檔案的相關資訊。 軟體清查也可以從用戶端裝置收集檔案，並將這些檔案儲存到站台伺服器。 選擇用戶端設定中的 [在用戶端上啟用軟體清查] 設定時，會收集軟體清查，而您也可以在用戶端設定中排定作業。  

在啟用軟體清查且用戶端執行軟體清查週期之後，用戶端會將資訊傳送至用戶端站台中的一個管理點。 管理點接著會將清查資訊轉送至 Configuration Manager 站台伺服器，再由該伺服器將資訊儲存到站台資料庫。   

 以下是檢視軟體清查資料的方法︰  

-   [建立查詢](../../../../core/servers/manage/queries-technical-reference.md)，以傳回具有所指定檔案的裝置。   

-   建立[查詢式集合](../../../../core/clients/manage/collections/introduction-to-collections.md)，以傳回具有所指定檔案的裝置。   

-   [執行報告](../../../../core/servers/manage/reporting.md)，以提供裝置上檔案的詳細資料。

-   使用[資源總管](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)，檢查從用戶端裝置清查及收集之檔案的詳細資訊。   

 當軟體清查在用戶端裝置上執行時，第一份報告是完整清查。 後續報告只會包含差異清查資訊。 站台伺服器會依差異資訊收到的順序來進行處理。 如果遺漏用戶端的差異資訊，站台伺服器會拒絕之後的差異資訊，並指示該用戶端執行完整清查。  

 Configuration Manager 可以探索雙重開機電腦，但只會傳回清查時仍作用中的作業系統清查資訊。  

**行動裝置︰**如需有關收集行動裝置所安裝之應用程式清查的詳細資訊，請參閱[向 Microsoft Intune 註冊之行動裝置的軟體清查](../../../../mdm/deploy-use/software-inventory-mobile-devices.md)。
