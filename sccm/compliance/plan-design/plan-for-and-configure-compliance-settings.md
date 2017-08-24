---
title: "规划和配置符合性设置 | Microsoft Docs"
description: "了解在 System Center Configuration Manager 中使用符合性设置的先决条件和配置任务。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d26ac3de58d2f0ef447725e63fc2d8adda6ea06c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-and-configure-compliance-settings-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中规划和配置符合性设置

*适用范围：System Center Configuration Manager (Current Branch)*

在开始使用 System Center Configuration Manager 符合性设置之前，需要了解几个先决条件，并且需要执行一些配置任务。  

## <a name="prerequisites-for-compliance-settings"></a>符合性设置的先决条件  

|先决条件|更多信息|  
|------------------|----------------------|  
|必须启用 Windows Configuration Manager 客户端并配置符合性评估。|请参阅下文|  
|如果你想要运行报表，就必须为站点配置报告。|[System Center Configuration Manager 中的报表](../../core/servers/manage/reporting.md)|  
|所需的安全权限。|“符合性设置管理员”安全角色包括管理符合性设置、用户数据和配置文件配置项目和远程连接配置文件必需的权限。<br /><br /> [配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>启用并配置符合性设置（仅适用于 Windows 电脑）  

此过程为符合性设置配置默认客户端设置并应用于你的层次结构中的所有计算机。 如果希望这些设置仅应用于某些计算机，请创建一个自定义设备客户端设置，并将其分配给包含要使用符合性设置的计算机的集合。 有关如何创建自定义设备设置的详细信息，请参阅[如何配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

> [!TIP]  
>  其他设备类型不需要任何特定的配置以评估符合性设置。  

1.  在 Configuration Manager 控制台中，单击“管理” > “客户端设置” > “默认设置”。  
2.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  
3.  在“默认设置”  对话框中，单击“符合性设置” 。  
4.  为符合性设置配置下列客户端设置：
    - **在客户端上启用符合性评估** - 如果要在客户端设备上评估符合性，则设置为“True”。
    - **计划符合性评估** - 如果要修改客户端设备上的默认符合性评估计划，请单击“计划”。
    - **启用用户数据和配置文件** - 如果要向 Windows 计算机创建并部署用户数据和配置文件配置项目，则启用此选项。 有关详细信息，请参阅[创建用户数据和配置文件配置项目](/sccm/compliance/deploy-use/create-remote-connection-profiles)。
5. 单击“确定”  来关闭“默认设置”  对话框。  

当客户端计算机下一次下载客户端策略时，将使用这些设置进行配置。  
