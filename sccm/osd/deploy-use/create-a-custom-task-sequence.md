---
title: "创建自定义任务序列 | Microsoft Docs"
description: "在 System Center Configuration Manager 中编辑自定义任务序列以将步骤添加到任务序列。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 03c844084c72fc52806123d9f4c11a410a3ec775
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-custom-task-sequence-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建自定义任务序列

*适用范围：System Center Configuration Manager (Current Branch)*

当在 System Center Configuration Manager 中创建自定义任务序列时，它不包含任何任务序列步骤。 创建任务序列后，必须对其进行编辑，并添加所需的任务序列步骤。  

##  <a name="BKMK_CustomTS"></a> 创建自定义任务序列  
 使用下列过程来创建自定义任务序列。  

#### <a name="to-create-a-custom-task-sequence"></a>创建自定义任务序列  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“任务序列” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建任务序列”  以启动创建任务序列向导。  

4.  在“创建新的任务序列”  页面上，选择“创建新的自定义任务序列” 。  

5.  在“任务序列信息”  页上，指定任务序列的名称、任务序列的描述以及供任务序列使用的可选启动映像，然后完成向导。  

 完成“创建任务序列向导”之后，Configuration Manager 会将自定义任务序列添加到“任务序列”节点。 你现在可以编辑此任务序列以向其中添加任务序列步骤。  

 有关可用的任务序列步骤列表，请参阅[任务序列步骤](../understand/task-sequence-steps.md)。  

 有关如何编辑任务序列的信息，请参阅[编辑任务序列](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence)。  

 通常使用任务序列来自动执行操作系统部署的任务，但你可以创建自定义任务序列来自动执行各种任务。 有关详细信息，请参阅[创建用于非操作系统部署的任务序列](create-a-task-sequence-for-non-operating-system-deployments.md)。  

 ## <a name="next-steps"></a>后续步骤
 [部署任务序列](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
