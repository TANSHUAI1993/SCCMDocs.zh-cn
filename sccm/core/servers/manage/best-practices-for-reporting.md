---
title: "報告最佳做法 | Microsoft Docs"
description: "閱讀有關使用 System Center Configuration Manager 之報告功能的一些實用秘訣。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 759258999f3eaa810803a6a7f856f00fe7771a9e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager 的報告最佳做法

適用於：System Center Configuration Manager (最新分支)

請針對 System Center Configuration Manager 中的報告使用下列最佳做法：  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>若要獲得最佳效能，請在遠端站台系統伺服器上安裝 Reporting Services 點  
 雖然您可以選擇在站台伺服器或遠端站台系統上安裝 Reporting Services 點，但是只有當您在遠端站台系統伺服器上安裝 Reporting Services 點時，才能提升效能。  

## <a name="optimize-sql-server-reporting-services-queries"></a>最佳化 SQL Server Reporting Services 查詢  
 通常，報告延遲都是因為執行查詢及擷取結果的時間過長所致。 如果您使用的是 Microsoft SQL Server，則可以使用如 Query Analyzer 和 Profiler 等工具協助您最佳化查詢。  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>將報告訂閱處理排定在非標準上班時間時執行  
 盡可能將報告訂閱處理排定在非一般標準上班時間執行，將 Configuration Manager 站台資料庫伺服器上的 CPU 處理時間降至最低。 此作法也可提高非預期報告要求的可用性。  

## <a name="next-steps"></a>後續步驟
[設定報告](configuring-reporting.md)
