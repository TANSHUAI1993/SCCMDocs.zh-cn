---
title: "稽核遠端控制使用方式 | Microsoft Docs"
description: "稽核 System Center Configuration Manager 的遠端控制使用方式。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c975e69-0cc0-4afd-b7fb-b7182162a933
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 4259ecfca48ccdffa83247e9ab5a65b3f006c5d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-audit-remote-control-usage-in-system-center-configuration-manager"></a>如何稽核 System Center Configuration Manager 的遠端控制使用方式

適用於：System Center Configuration Manager (最新分支)

您可以使用 System Center Configuration Manager 報告檢視遠端控制的稽核資訊。  

 如需如何在 Configuration Manager 設定報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../../../core/servers/manage/reporting.md)。  

 下列兩種報告有 **狀態訊息 - 稽核**類別：  

-   **遠端控制 - 由特定使用者遠端控制的所有電腦** - 顯示特定使用者起始的遠端控制活動摘要。  

-   **遠端控制 - 所有遠端控制資訊** - 顯示關於用戶端電腦遠端控制的狀態訊息摘要。  

### <a name="to-run-the-report-remote-control---all-computers-remote-controlled-by-a-specific-user"></a>執行 [遠端控制 - 由特定使用者遠端控制的所有電腦] 報告  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [報告] ，然後按一下 [報告] 。  

3.  按一下 [報告]  節點的 [類別]  欄排序報告，以便更容易找到 [狀態訊息 - 稽核] 類別中的報告。  

4.  選取 [遠端控制 - 由特定使用者遠端控制的所有電腦] 報告，然後在 [首頁]  索引標籤的 [報告群組] 中按一下 [執行] 。  

5.  在 [遠端控制 - 由特定使用者遠端控制的所有電腦]  的 [使用者名稱] 清單中，指定要報告其稽核資訊的使用者，然後按一下 [檢視報告] 。  

6.  當您完成報告資料檢視後，請關閉報告視窗。  

### <a name="to-run-the-report-remote-control---all-remote-control-information"></a>執行 [遠端控制 - 所有遠端控制資訊] 報告  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中，展開 [報告] ，然後按一下 [報告] 。  

3.  按一下 [報告]  節點的 [類別]  欄排序報告，以便更容易找到 [狀態訊息 - 稽核] 類別中的報告。  

4.  選取 [遠端控制-所有遠端控制資訊] 報告，然後在 [首頁]  索引標籤的 [報告群組] 中，按一下 [執行]  開啟 [遠端控制 - 所有遠端控制資訊]  視窗。  

5.  當您完成報告資料檢視後，請關閉報告視窗。  
