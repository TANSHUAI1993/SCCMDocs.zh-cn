---
title: "审核远程控制使用 | Microsoft Docs"
description: "审核 System Center Configuration Manager 中的远程控制使用。"
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
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-audit-remote-control-usage-in-system-center-configuration-manager"></a>如何审核 System Center Configuration Manager 中的远程控制使用

*适用范围：System Center Configuration Manager (Current Branch)*

可以使用 System Center Configuration Manager 报表来查看远程控制的审核信息。  

 有关如何在 Configuration Manager 中配置报表的详细信息，请参阅 [System Center Configuration Manager 中的报表](../../../../core/servers/manage/reporting.md)。  

 以下两个报表在“状态消息 - 审核” 类别下列出：  

-   **远程控制 – 特定用户远程控制的所有计算机** – 显示特定用户启动的远程控制活动的摘要。  

-   **远程控制 – 所有远程控制信息** – 显示关于客户端计算机远程控制的状态消息的摘要。  

### <a name="to-run-the-report-remote-control---all-computers-remote-controlled-by-a-specific-user"></a>运行报表“远程控制 - 特定用户远程控制的所有计算机”  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”  工作区中，展开“报表” ，然后单击“报表” 。  

3.  在“报表”  节点中，单击“类别”  列以对报表进行排序，以便可以更轻松地在“状态消息 - 审核” 类别中找到报表。  

4.  选择“远程控制 - 由特定用户远程控制的所有计算机” 报表，然后在“主页”  选项卡的“报表组” 中单击“运行” 。  

5.  在“远程控制 - 由特定用户远程控制的所有计算机”  中的“用户名” 列表中，指定想要为其报告审核信息的用户，然后单击“查看报告” 。  

6.  在报表中查看完数据后，关闭报表窗口。  

### <a name="to-run-the-report-remote-control---all-remote-control-information"></a>运行报表“远程控制 - 所有远程控制信息”  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”  工作区中，展开“报表” ，然后单击“报表” 。  

3.  在“报表”  节点中，单击“类别”  列以对报表进行排序，以便可以更轻松地在“状态消息 - 审核” 类别中找到报表。  

4.  选择“远程控制 - 所有远程控制信息” 报表，然后在“主页”  选项卡的“报表组” 中单击“运行”  以打开“远程控制 - 所有远程控制信息”  窗口。  

5.  在报表中查看完数据后，关闭报表窗口。  
