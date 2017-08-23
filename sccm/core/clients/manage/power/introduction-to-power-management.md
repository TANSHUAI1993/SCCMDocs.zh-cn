---
title: "電源管理簡介 | Microsoft Docs"
description: "了解 System Center Configuration Manager 的電源管理簡介。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
caps.latest.revision: "4"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f46c9479021c814b1102d72c7d493f21a7243bf1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 的電源管理簡介

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 的電源管理功能可滿足許多組織必須監視及降低電腦耗電量的需求。 此功能會利用 Windows 內建的電源管理功能，將相關且一致的設定套用至組織的電腦上。 電腦在營業時間和非營業時間可以套用不同的電源設定。 例如，您希望電腦在非營業時間套用限制較嚴格的電源計劃。 萬一電腦必須一直保持開啟狀態，您可以阻止套用電源管理設定。  

 Configuration Manager 的電源管理功能包含數份報告，可協助您分析組織的耗電量和電腦電源設定。 您也可以使用報告協助您疑難排解電源管理的問題。  

 如需如何設定和使用電源管理功能的詳細工作流程，請參閱 [System Center Configuration Manager 中電源管理的系統管理員檢查清單](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md)。  

> [!IMPORTANT]  
>  虛擬機器不支援 Configuration Manager 電源管理。 虛擬機器無法套用電源計劃，也不會回報其電源資料。  

## <a name="the-power-management-workflow"></a>電源管理工作流程  
 請使用下列三個階段來規劃及實作 Configuration Manager 電源管理功能。  

### <a name="monitoring-and-planning-phase"></a>監視和規劃階段  
 電源管理功能會使用 Configuration Manager 硬體清查，來收集站台電腦之電腦使用量和電源設定的資料。 有數份報告可用以分析這項資料，判斷電腦的最佳電源管理設定。 例如，在電源管理工作流程的監視和規劃階段，您可以根據 [電池容量]  報告包含的資料建立集合，並使用該資料找出不能進行電源管理的電腦。 然後，在電源管理中排除這些電腦。  

> [!IMPORTANT]  
>  在收集分析完用戶端電腦的電源資料前，請不要將電源計劃套用至站台的電腦。 如果您將新的電源管理設定套用至電腦，卻未先檢查現有的設定，可能會增加耗電量。  

### <a name="enforcement-phase"></a>強制執行階段  
 電源管理讓您建立可以套用到站台電腦集合的電源計劃。 這些電源計劃會在電腦上設定 Windows 電源管理設定。 您可以使用 Configuration Manager 隨附的電源計劃，或者設定自己的自訂電源計劃。 您可以使用於監視和規劃階段期間收集的電源資料為基準，協助您評估電腦套用電源計劃之後的省電成效。 如需詳細資訊，請參閱 [System Center Configuration Manager 中電源管理的系統管理員檢查清單](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md)。  

### <a name="compliance-phase"></a>相容性階段  
 在相容性階段中，您可以執行報告，協助您評估貴組織的用電量和電費節約成效。 您也可以執行報告，說明電腦 CO2 產量降低的成效。 另有報告協助您驗證該電源設定是否正確套用至電腦，並幫助您疑難排解與電源管理功能有關的問題。  
