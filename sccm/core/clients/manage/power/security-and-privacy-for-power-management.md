---
title: "電源管理的安全性和隱私權 | Microsoft Docs"
description: "取得 System Center Configuration Manager 中電源管理的安全性和隱私權資訊。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 94d5418c364c318dba92dc9f9066f54d1130aa34
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 的電源管理安全性與隱私權

*適用於：System Center Configuration Manager (最新分支)*

本主題包含 System Center Configuration Manager 中電源管理的安全性和隱私權資訊。  

## <a name="security-best-practices-for-power-management"></a>電源管理的安全性最佳做法  
 電源管理沒有任何安全性相關的最佳做法。  

## <a name="privacy-information-for-power-management"></a>電源管理的隱私權資訊  
 電源管理會使用 Windows 內建的功能監視電源使用量，並在營業和非營業時間將電源設定套用到電腦。 Configuration Manager 會從電腦收集電源使用量資訊，包含使用者何時使用電腦的相關資料。 雖然 Configuration Manager 監視集合的電源使用量不是每一部電腦的使用量，但是集合可以只包含一部電腦。 電源管理預設不啟用，而且必須由系統管理員設定。  

 電源使用量資訊存放在 Configuration Manager 資料庫中，且不會傳送給 Microsoft。 詳細資訊會在資料庫中保留 31 天，摘要資訊會保留 13 個月。 您可以設定刪除間隔。  

 在您設定電源管理之前，請先考慮隱私權需求。  
