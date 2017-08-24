---
title: "监视 Endpoint Protection 状态 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 层次结构中监视 Endpoint Protection。"
ms.custom: na
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
caps.latest.revision: "8"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: b5771f4faebc06076bdbf84727848c881fc1dfb4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-monitor-endpoint-protection-status"></a>如何监视 Endpoint Protection 状态

*适用范围：System Center Configuration Manager (Current Branch)*

可以使用“监视”工作区中的“安全性”下的“Endpoint Protection 状态”节点，“资产和符合性”工作区中的“Endpoint Protection”节点以及使用报表，在 Microsoft System Center Configuration Manager 层次结构中监视 Endpoint Protection。  

##  <a name="BKMK_1"></a>如何使用“Endpoint Protection 状态”节点监视 Endpoint Protection  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”工作区中，展开“安全性”，然后单击“Endpoint Protection 状态”。  

3.  在 **集合** 列表中，选择想要查看状态信息的集合。  

    > [!IMPORTANT]  
    >  集合是在以下情况下可供选择：  
    >   
    >  -   当你在“<集合名称\>属性”对话框的“警报”选项卡上选择“在 Endpoint Protection 仪表板中查看此集合”时。  
    > -   当你部署 Endpoint Protection 反恶意软件策略应用到集合。  
    > -   如果先启用然后部署 Endpoint Protection 到集合的客户端设置。  

4.  查看中显示的信息 **安全状态** 和 **操作状态** 部分。 您可以单击以创建临时集合中的任何状态链接 **设备** 中的节点 **资产和符合性** 工作区。 此临时集合包含具有所选状态的计算机。  

    > [!IMPORTANT]  
    >  “Endpoint Protection 状态”节点中显示的信息基于上次从 Configuration Manager 数据库汇总的数据，可能不是最新的。 如果想要检索最新数据，则在“主页”选项卡上，单击“运行摘要”，或单击“计划摘要”以调整摘要间隔。  

##  <a name="BKMK_2"></a>如何在“资产和符合性”工作区中监视 Endpoint Protection  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在 **资产和符合性** 工作区中，执行以下操作之一：  

    -   单击 **设备**。 在 **设备** 列表，选择一台计算机，然后单击 **恶意软件详细信息** 选项卡。  

    -   单击 **设备集合**。 在 **设备集合** 列表中，选择包含您想要监视的计算机的集合，然后在 **主页** 选项卡上，在 **集合** 组中，单击 **显示成员**。  

3.  在 <集合名称\> 列表中，选择一台计算机，然后单击“恶意软件详细信息”选项卡。  

##  <a name="BKMK_3"></a>如何使用报表监视 Endpoint Protection  
 使用以下报表可帮助查看有关层次结构中的 Endpoint Protection 的信息。 你还可以使用这些报表来帮助针对任何 Endpoint Protection 问题进行故障排除。 有关如何在 Configuration Manager 中配置报表的详细信息，请参阅 [System Center Configuration Manager 中的报表](../../core/servers/manage/reporting.md)和 [System Center Configuration Manager 中的日志文件](../../core/plan-design/hierarchy/log-files.md)。 Endpoint Protection 报表处于 Endpoint Protection 文件夹中。  

|报告名称|描述|  
|-----------------|-----------------|  
|**反恶意软件活动报告**|显示指定集合的反恶意软件活动的概述。|  
|**受感染的计算机**|显示在其检测到指定的威胁的计算机的列表。|  
|**通过威胁的前几名用户**|显示具有最多的检测到的威胁的用户列表。|  
|**用户威胁列表**|显示已找到指定的用户帐户的威胁的列表。|  

## <a name="malware-alert-levels"></a>恶意软件警报级别  
 使用下表来标识可能会显示在报表中或显示在 Configuration Manager 控制台中的不同 Endpoint Protection 警报级别。  

|警报级别|描述|  
|-----------------|-----------------|  
|**已失败**|Endpoint Protection 未能修正恶意软件。 检查有关错误的详细信息日志。<br /><br /> **注意：**有关 Configuration Manager 和 Endpoint Protection 日志文件的列表，请参阅 [System Center Configuration Manager 中的日志文件](../../core/plan-design/hierarchy/log-files.md)主题中的“Endpoint Protection”部分。|  
|**已删除**|Endpoint Protection 已成功删除了恶意软件。|  
|**已隔离**|Endpoint Protection 已将恶意软件移动到一个安全位置，并已阻止其运行，直到你将其删除或允许其运行。|  
|**已清理**|恶意软件已清理受感染的文件中。|  
|**允许**|管理用户选择允许包含要运行的恶意软件的软件。|  
|**不执行任何操作**|Endpoint Protection 对恶意软件不执行任何操作。 如果重新启动计算机后检测到恶意软件和不能再检测到恶意软件 ； 这可能会发生例如，如果映射的网络驱动器上检测到的恶意软件是不重新连接时在计算机重新启动。|  
|**已阻止**|Endpoint Protection 已阻止恶意软件运行。 这可能是如果发现计算机上的进程是包含恶意软件。|
