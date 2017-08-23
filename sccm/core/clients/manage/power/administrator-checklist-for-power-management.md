---
title: "電源管理的系統管理員檢查清單 | Microsoft Docs"
description: "使用系統管理員檢查清單幫助您規劃及實作 System Center Configuration Manager 電源管理。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e6a7a0b853be930b558cdd739b90285ebb8538e7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="administrator-checklist-for-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中電源管理的系統管理員檢查清單

*適用對象：System Center Configuration Manager (最新分支)*

這個系統管理員檢查清單提供在組織中使用 System Center Configuration Manager 電源管理的建議步驟。  

## <a name="configuring-power-management"></a>設定電源管理  
 使用下列步驟可協助您設定階層，以收集來自用戶端電腦的電源管理資訊。  

> [!IMPORTANT]  
>  除非您已經收集並分析用戶端電腦的電源資料，否則請不要將電源計劃套用至階層中的電腦。 如果您將新的電源管理設定套用至電腦，而不需要先檢查現有設定，這可能會導致耗電量增加。  

|工作|詳細資料|  
|----------|-------------|  
|請檢閱 Configuration Manager 文件庫中的電源管理概念。|請參閱[電源管理簡介](introduction-to-power-management.md)。|  
|請檢閱 Configuration Manager 文件庫中的電源管理必要條件。|請參閱[電源管理的必要條件](prerequisites-for-power-management.md)。|  
|請檢閱電源管理的最佳做法資訊。|請參閱[電源管理的最佳做法](best-practices-for-power-management.md)。|  
|設定集合以從環境中的電腦管理電源消耗。|使用 [Collection for reporting of baseline data] \(基準資料報告集合)、[Collection for reporting of baseline data] \(基準資料報告集合)、[Collection of computers incapable of power management] \(無法管理電源的電腦集合)、[Collections of computers to which power plans will be applied] \(要套用電源計劃的電腦集合)、[Collections of computers to which power plans will be applied] \(要套用電源計劃的電腦集合) 和 [Collections of computers that are running Windows Server] \(執行 Windows Server 的電腦集合) 幫助您管理階層中的電腦電源設定。 您可以建立多個集合，並將不同的電源計劃套用至每個集合。|  
|啟用電源管理。|您必須先啟用電源管理，並設定必要的用戶端設定，才能開始使用電源管理。 如需詳細資訊，請參閱[設定電源管理](configuring-power-management.md)。|  
|收集來自用戶端電腦的電源管理資訊。|用戶端會透過 Configuration Manager 硬體清查來報告電源管理資訊。 根據您已設定的硬體清查排程，可能需要一些時間來擷取所有用戶端電腦中的清查。|  

## <a name="monitoring-and-planning-phase"></a>監視和規劃階段  

|工作|詳細資料|  
|----------|-------------|  
|執行報告 [電腦活動] 。|[電腦活動]  報告顯示圖形來表示所指定集合在指定時段的監視器、電腦和使用者活動。 這個報告會連結到 [電腦活動詳細資料]  報告，以顯示指定集合中電腦的睡眠和喚醒功能清單。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  
|執行報告 [能源消耗]  或 [每日能源消耗] 。|[能源消耗]  和 [每日能源消耗]  報告顯示指定集合在指定時段的每月總耗電量，單位為每小時千瓦 (kWh)。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  
|執行報告 [環境衝擊]  或 [每日環境衝擊]  。|[環境衝擊]  和 [每日環境衝擊]  報告顯示圖形來表示指定電腦集合在指定時段所儲存的二氧化碳 (CO2) 排放量。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  
|執行報告 [能源成本]  或 [每日能源成本] 。|[能源成本]  和 [每日能源成本]  報告顯示指定時段的總耗電量成本。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  
|執行報告 [電池容量] 。|[電池容量]  報告顯示指定集合中電腦的電源管理功能。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  
|執行報告 [電源設定] 。|[電源設定]  報告顯示指定集合中電腦所使用的目前電源設定彙總清單。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  
|排除任何必要的電腦集合不進行電源管理。|請參閱[設定電源管理](configuring-power-management.md)。|  

> [!IMPORTANT]  
>  請確定您儲存監視和規劃階段期間所產生之電源管理報告中的資訊。 您可以比較這個資料與強制執行和相容性階段期間所產生的電源管理資訊，協助評估將電源計劃套用至階層中的電腦所省下的耗電量、電源成本和環境衝擊。  

## <a name="enforcement-phase"></a>強制執行階段  

|工作|詳細資料|  
|----------|-------------|  
|針對組織中的電腦集合，選取現有電源計劃，或建立新的電源計劃。|請參閱 [How to create and apply power plans](create-and-apply-power-plans.md) (如何建立及套用 Configuration Manager 的電源計劃)。|  
|將這些電源計劃套用至電腦。|請參閱 [How to create and apply power plans](create-and-apply-power-plans.md) (如何建立及套用 Configuration Manager 的電源計劃)。|  

## <a name="compliance-phase"></a>相容性階段  

|工作|詳細資料|  
|----------|-------------|  
|執行報告 [電腦活動] 。|[電腦活動]  報告顯示圖形來表示所指定集合在指定時段的監視器、電腦和使用者活動。 這個報告會連結到 [電源電腦活動詳細資料]  報告，以顯示指定集合中電腦的睡眠和喚醒功能清單。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  
|執行報告 [能源消耗]  或 [每日能源消耗] 。|[能源消耗]  和 [每日能源消耗]  報告顯示指定集合在指定時段的每月總耗電量，單位為每小時千瓦 (kWh)。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  
|執行報告 [環境衝擊]  或 [每日環境衝擊] 。|[環境衝擊]  和 [每日環境衝擊]  報告顯示圖形來表示指定電腦集合在指定時段所儲存的二氧化碳 (CO2) 排放量。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  
|執行報告 [能源成本]  或 [每日能源成本] 。|[能源成本]  和 [每日能源成本]  報告顯示指定時段的總耗電量成本。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  

## <a name="troubleshooting"></a>疑難排解  

|工作|詳細資料|  
|----------|-------------|  
|如果階層中的電腦尚未進入睡眠或休眠，請執行報告 [無法休眠報告]  來顯示可能的原因。|[無法休眠報告]  顯示妨礙電腦進入睡眠或休眠狀態的常見原因清單，以及在指定時段每個原因所影響的電腦數目。 如需詳細資訊，請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。|  
|如果將多個電源計劃套用至一部電腦，則會套用最不嚴格的電源計劃。 執行報告 [具有多個電源計劃的電腦]  ，查看已套用多個電源計劃的電腦。|請參閱 [How to monitor and plan for power management](monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理 ) 中的 **Computers with Multiple Power Plans** (具有多個電源計劃的電腦)。|  
