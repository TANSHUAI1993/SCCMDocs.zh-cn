---
title: "软件更新维护 | Microsoft Docs"
description: "若要在 Configuration Manager 中维护更新，可以计划 WSUS 清理任务，也可以手动运行它。"
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
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="software-updates-maintenance"></a>软件更新维护

*适用范围：System Center Configuration Manager (Current Branch)*

你可以从 Configuration Manager 控制台计划和运行 WSUS 清理任务，也可以从“软件更新点组件”属性中手动运行 WSUS 清理任务。 当你选择运行 WSUS 清理任务时，它将在下一次软件更新同步时运行。 过期的软件更新将设置为在 WSUS 服务器上被拒绝的状态，计算机上的 Windows 更新代理将不再扫描这些软件更新。 默认情况下，WSUS 清理任务作业每 30 天运行一次。  

#### <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>计划和运行 WSUS 清理作业  

1.  在 Configuration Manager 控制台中，导航到“管理” > “概述” > “站点配置” > “站点”。  

2.  单击“设置”  组中的  “配置站点组件”，然后单击“软件更新点”  以打开软件更新点组件属性。  

3.  单击“取代规则”  选项卡，选择“运行 WSUS 清理向导” ，然后单击“确定” 。
