---
title: 共同管理仪表板
titleSuffix: Configuraton Manager
description: 使用仪表板查看有关共同管理的信息。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3d4cbbf78639a135e9e36e3402f9920a6ef71ed
ms.sourcegitcommit: 78d2dce465e3500653b252583a6903a006784c26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2018
ms.locfileid: "46448780"
---
# <a name="co-management-dashboard-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的共同管理仪表板
*适用范围：System Center Configuration Manager (Current Branch)*

从版本 1802 开始，你可以查看包含共同管理相关信息的仪表板。 仪表板可帮助你查看环境中共同托管的计算机。 图表有助于标识可能需要注意的设备。<!--1356648-->

## <a name="open-the-co-management-dashboard"></a>打开共同管理仪表板
若要打开共同管理仪表板，请使用以下步骤： 

1. 打开 Configuration Manager 控制台。 
2. 单击“监视”节点。 
3. 若要加载仪表板，请单击“共同管理”。

## <a name="reviewing-information-in-the-co-management-dashboard"></a>查看共同管理仪表板中的信息

共同管理仪表板针对你的环境显示四个图表。 

- **共同托管的设备**：提供共同托管的设备在你的环境中所占的百分比。

    ![共同托管的设备图表](media\co-management-dashboard\Percent-Co-managed-graph.PNG)

- **客户端 OS 分发**：按版本显示每个 OS 的客户端设备数量。 使用下列分组： </br>
    - Windows 7 和 8.x
    - Windows 10 1709 以下版本
    - Windows 10 1709 及更高版本

         > [!NOTE] 
         > Windows 10 1709 及更高版本是共同管理的先决条件。

     将鼠标悬停在某个图表部分上方将显示所选 OS 分组中的设备所占的百分比。

     ![客户端 OS 分发图表](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)

- **共同管理状态**：设备成功或失败分类细目如下：
    - 成功，已联接混合 Azure AD
    - 成功，已联接 Azure AD
    - 失败：自动注册失败
    
     将鼠标悬停在某个图表部分上方将显示该类别的设备所占的百分比。 

     ![共同管理状态图表](media\co-management-dashboard\Co-management-status-graph.PNG)

     单击某个图表部分将转到该类别的设备列表。
 
     ![注册失败设备列表](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


- **工作负荷转换** - 显示一个条形图，其中包含为了四个可用工作负荷而转换为 Microsoft Intune 的设备数：
    - 符合性策略
    - 资源访问
    - Windows Update for Business
    - Endpoint Protection

     将鼠标悬停在某个图表部分上方将显示为该工作负荷转换的设备数量。 
     ![工作负荷转换条形图](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>后续步骤

有关共同管理的详细信息，请参阅：
 - [适用于 Windows 10 设备的共同管理](/sccm/core/clients/manage/co-management-overview)
 - [准备 Windows 10 设备进行共同管理](/sccm/core/clients/manage/co-management-prepare)

    
