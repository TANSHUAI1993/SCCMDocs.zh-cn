---
title: "远程控制先决条件 | Microsoft Docs"
description: "获取在 System Center Configuration Manager 中远程控制的先决条件。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: a99a18bcb5c981a56e5b38eb631cfabbad8c44d7
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/14/2017
---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中远程控制的先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的远程控制具有外部依赖关系和产品中的依赖关系。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系  

|依赖关系|更多信息|  
|----------------|----------------------|  
|计算机视屏卡驱动程序|为获得最优的远程控制性能，请确保客户端计算机上已安装了最新的视屏驱动程序。|  

 运行 Windows Embedded、Windows Embedded for Point of Service (POS) 以及 Windows Fundamentals for Legacy PC 的设备不支持远程控制查看器，但它们却支持远程控制客户端。  

 Configuration Manager 远程控制不能用于远程管理运行 Systems Management Server 2003 或 Configuration Manager 2007 的客户端计算机。  

> [!NOTE]  
>  不需要 Windows 服务作为远程控制的外部依赖关系。  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>支持远程控制查看器的操作系统  
在 Configuration Manager 控制台支持的所有操作系统上，支持使用远程控制查看器。 有关信息，请参阅 [System Center Configuration Manager 控制台支持的配置](../../../../core/plan-design/configs/supported-operating-systems-consoles.md)。   

## <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  

|依赖关系|更多信息|  
|----------------|----------------------|  
|必须为客户端启用远程控制|默认情况下，安装 Configuration Manager时，不启用远程控制。 有关如何启用和配置远程控制的信息，请参阅[在 System Center Configuration Manager 中配置远程控制](../../../../core/clients/manage/remote-control/configuring-remote-control.md)。|  
|Reporting Services 点|在远程控制的报表前，必须先安装 Reporting Services 点站点系统角色。 有关详细信息，请参阅 [System Center Configuration Manager 中的报表](../../../../core/servers/manage/reporting.md)。|  
|管理远程控制的安全权限|若要访问集合资源并从 Configuration Manager 控制台启动远程控制会话，需要拥有“集合”对象的“读取”、“读取资源”和“远程控制”权限。<br /><br /> “远程工具操作人员”安全角色包括这些在 Configuration Manager 中管理远程控制所需要的权限。<br /><br /> 有关详细信息，请参阅[为 System Center Configuration Manager 配置基于角色的管理](../../../../core/servers/deploy/configure/configure-role-based-administration.md)。<br /><br /> 此外，还必须将获准的查看器添加到“远程工具”客户端设置中的“获准的远程控制和远程协助查看器”列表中，它们才有权使用远程控制。
