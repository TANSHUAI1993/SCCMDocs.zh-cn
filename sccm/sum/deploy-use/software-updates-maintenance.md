---
title: "軟體更新維護 | Microsoft Docs"
description: "若要在 Configuration Manager 中維護更新，您可以排程 WSUS 清理工作，也可以手動進行執行。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
ms.openlocfilehash: 1590c623f7bc2f42a8617f110de5321212732a03
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="software-updates-maintenance"></a>軟體更新維護

*適用於：System Center Configuration Manager (最新分支)*

您可以從 Configuration Manager 主控台排程和執行 WSUS 清理工作，也可以從 [軟體更新點元件內容] 手動執行 WSUS 清理工作。 當您選取執行 WSUS 清理工作時，它會在下一次軟體更新同步處理時執行。 到期的軟體更新在 WSUS 伺服器上會設為拒絕狀態，而電腦上的 Windows Update 代理程式將不再掃描這些軟體更新。 WSUS 清理工作預設會每 30 天執行一次。  

#### <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>進行排程及執行 WSUS 清理工作  

1.  在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [概觀] > [站台設定] > [站台]。  

2.  按一下 [設定]  群組中的 [設定站台元件]  ，然後按一下 [軟體更新點]  開啟軟體更新點元件屬性。  

3.  按一下 [取代規則]  索引標籤，選取 [執行 WSUS 清理精靈] ，然後按一下 [確定] 。
