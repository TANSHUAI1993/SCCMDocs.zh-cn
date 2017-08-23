---
title: "電源管理的必要條件 | Microsoft Docs"
description: "取得 System Center Configuration Manager 中電源管理的必要條件。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
caps.latest.revision: "4"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 711ef491899846b86bfed0355ac7fd0f9d509c4f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 中電源管理的必要條件

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的電源管理具有外部相依性和產品內的相依性。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  
 下表列出 Configuration Manager 外部使用電源管理的相依性。  

|相依性|詳細資訊|  
|----------------|----------------------|  
|用戶端電腦必須可以支援必要的電源狀態|若要使用電源管理的所有功能，用戶端電腦必須可以支援睡眠、休眠、從睡眠喚醒，以及從休眠喚醒的動作。 您可以使用 [電源功能]  報告，判斷電腦是否可支援這些動作。 如需詳細資訊，請參閱[如何監視和規劃 System Center Configuration Manager 的電源管理](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)主題中的[電源管理報告](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites)。|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  
 下表列出 Configuration Manager 內部使用電源管理的相依性。  

|相依性|詳細資訊|  
|----------------|----------------------|  
|必須先啟用電源管理，才能建立和監視電源計劃。|如需如何啟用和設定電源管理的相關資訊，請參閱[設定 System Center Configuration Manager 的電源管理](../../../../core/clients/manage/power/configuring-power-management.md)。|  
|Reporting Services 點|您必須先設定 Reporting Services 點，才能檢視電源管理報告。 如需詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。|  
