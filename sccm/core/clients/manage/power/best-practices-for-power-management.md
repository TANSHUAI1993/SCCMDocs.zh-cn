---
title: "電源管理的最佳做法 | Microsoft Docs"
description: "取得 System Center Configuration Manager 中電源管理的最佳做法。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d3cc24c7923141f039dcda26ac27489cb0143e89
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中電源管理的最佳做法

適用於：System Center Configuration Manager (最新分支)

請針對 System Center Configuration Manager 中的電源管理使用下列最佳做法。  

## <a name="perform-the-monitoring-phase-at-a-representative-time"></a>在代表性時間執行監視階段  
 電源管理的監視階段可提供組織中電腦之耗電量、活動、電源管理功能和環境衝擊的相關資訊。 請確定您選擇代表性時間來執行監視階段。 例如，在國定假日執行監視階段並未提供電腦耗電量的實際報告。  

## <a name="create-a-control-collection-of-computers-with-no-power-plans-applied"></a>建立未套用任何電源計劃之電腦的控制項集合  
 建立兩個電腦集合，協助您監視將電源計劃套用至電腦的效果。 第一個集合應該包含您想要套用電源設定的大部分電腦，而另一個集合 (控制項集合) 應該包含其餘的電腦。 將必要的電源管理計劃套用至包含大部分電腦的集合。 然後，您可以執行報告，來比較已套用電源設定之電腦的電源成本、耗電量和環境衝擊，與您尚未套用電源設定的控制項集合。  

## <a name="run-the-power-settings-report-before-you-apply-a-power-management-plan"></a>先執行 [電源設定] 報告，再套用電源管理計劃  
 將電源管理計劃套用至電腦集合之前，請執行 [電源設定]  報告，協助了解已在集合的電腦上設定的電源管理設定。 如果您將新的電源管理設定套用至電腦，而不需要先檢查現有設定，這可能會導致耗電量增加。  

## <a name="exclude-servers-from-power-management"></a>排除伺服器不進行電源管理  
 不支援執行 Windows Server 之電腦的電源管理 (雖然收集耗電量資料)。 請確定您將伺服器新增至集合，並排除它不進行電源管理。  

## <a name="exclude-computers-that-you-do-not-want-to-manage"></a>排除您不想要管理的電腦  
 如果您有不想要使用電源管理來管理的電腦，請將它們新增至集合，並確定排除集合不進行電源管理。  

 您可能想要排除不進行電源管理之電腦的範例包含：  

-   必須保持開啟的電腦。  

-   使用者需要使用遠端桌面連線所連線的電腦。  

-   無法使用電源管理的電腦。  

-   具有發佈點站台系統角色的電腦。  

-   公用電腦，例如 Kiosk 電腦、資訊顯示器，或必須一律開啟電腦與監視器的監視主控台。  

 如需詳細資訊，請參閱[在 System Center Configuration Manager 中設定電源管理](../../../../core/clients/manage/power/configuring-power-management.md)。  

## <a name="first-apply-power-plans-to-a-test-collection-of-computers"></a>先將電源計劃套用至測試電腦集合  
 一律測試對測試電腦集合套用電源管理計劃的效果，再將電源計劃套用至較大的電腦集合。  

 即使排除電腦不進行電源管理，套用至執行 Windows XP 或 Windows Server 2003 之電腦的電源設定還是不會還原為其原始值。 在新版的 Windows 上，排除電腦不進行電源管理會將所有電源設定還原成其原始值。 您無法將個別的電源設定還原為其原始值。  

## <a name="apply-power-plan-settings-individually"></a>個別套用電源計劃設定  
 監視套用每個電源設定的效果，再套用下一個電源計劃，以確保每個設定都有所需的效果。 如需電源計劃設定的詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立及套用電源計劃](../../../../core/clients/manage/power/create-and-apply-power-plans.md)主題中的[可用的電源管理計劃設定](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans)。  

## <a name="regularly-monitor-computers-to-see-if-they-have-multiple-power-plans-applied"></a>定期監視電腦，查看它們是否套用多個電源計劃  
 電源管理包括一份報告，其中顯示套用多個電源計劃的電腦。  

 如果電腦是多個集合的成員，而且各自套用不同的電源計劃，則會採取下列動作：  

-   電源計劃：如果電腦套用了電源設定的多個值，則會使用最不嚴格的值。  

-   喚醒時間：如果桌上型電腦套用多個喚醒時間，則會使用最接近午夜的時間。  

     如需詳細資訊，請參閱[如何監視和規劃 System Center Configuration Manager 的電源管理](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)主題中的[具有多個電源計劃的電腦](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Multiple)。 如需電源管理如何解決衝突的詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立及套用電源計劃](../../../../core/clients/manage/power/create-and-apply-power-plans.md)。  

## <a name="save-or-export-power-management-information-during-the-monitoring-and-planning-phase-of-power-management"></a>儲存或匯出電源管理之監視和規劃階段期間的電源管理資訊  
 每日報告所使用的電源管理資訊會在 Configuration Manager 站台資料庫中保留 31 天。  

 每月報告所使用的電源管理資訊會在 Configuration Manager 站台資料庫中保留 13 個月。  

 當您在電源管理的監視和規劃階段以及相容性階段執行報告時，請儲存或匯出想要保留資料以供日後比較的所有報告結果，以防 Configuration Manager 移除任何結果。  
