---
title: 共同管理仪表板
titleSuffix: Configuration Manager
description: 使用共同管理仪表板查看有关共同管理的设备的信息。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5e20985ac8fc39f2384cee5d202e19fc69e2b348
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414678"
---
# <a name="co-management-dashboard-in-configuration-manager"></a>Configuration Manager 中的共同管理仪表板

适用范围：System Center Configuration Manager (Current Branch)

从版本 1802 开始，可查看含共同管理相关信息的仪表板。 此仪表板可帮助你查看环境中共同管理的计算机。 图表有助于标识可能需要注意的设备。<!--1356648-->

在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“共同管理”节点。

自版本 1810 开始，通过在共同管理仪表板中增加了更多详细信息，共同管理仪表板的功能得到了增强。 <!--1358980-->



## <a name="dashboard-tiles"></a>仪表板磁贴 

共同管理仪表板根据站点版本显示不同的磁贴。 


### <a name="co-managed-devices"></a>共同管理的设备

适用于 1802 和 1806 两个版本

显示整个环境中共同管理的设备所占的百分比。
 ![“共同管理的设备”磁贴](media/co-management-dashboard/Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>客户端 OS 分发

适用于所有版本 

按版本显示每个 OS 的客户端设备数量。 使用以下分组：  
- Windows 7 和 8.x  
- Windows 10 1709 以下版本  
- Windows 10 1709 及更高版本  

    > [!Tip]  
    > Windows 10 1709 及更高版本是共同管理的先决条件。  

将鼠标悬停在图表的某个部分上方可显示该 OS 组中设备所占的百分比。
 ![“客户端 OS 分发”磁贴](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>共同管理状态（圆环图）

适用于 1802 和 1806 两个版本

显示以下类别中设备成功或失败的细目：
- 成功，已联接混合 Azure AD  
- 成功，已联接 Azure AD  
- 失败：自动注册失败  

将鼠标悬停在图表的某个部分上可显示该类别中设备所占的百分比。 
 ![共同管理状态（圆环图）磁贴](media/co-management-dashboard/Co-management-status-graph.PNG)

选择图中某个部分可查看该类别的设备列表。
 ![注册失败设备列表](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>共同管理状态（漏斗图）

适用于 1810 和更高版本

漏斗图，显示注册过程中具有以下状态的设备的数量：  
- 符合条件的设备  
- 已计划  
- 已启动注册  
- 已注册  

![共同管理状态（漏斗图）磁贴](media/co-management-dashboard/1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>共同管理注册状态

适用于 1810 和更高版本

显示以下类别中设备状态的细目：
- 成功，已联接混合 Azure AD  
- 成功，已联接 Azure AD  
- 正在注册，已联接混合 Azure AD  
- 失败，已联接混合 Azure AD  
- 失败，已联接 Azure AD  
- 挂起用户登录  

在该磁贴中选择一种状态，即可深入查看相关状态的设备列表。  

![共同管理注册状态磁贴](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="enrollment-errors"></a>注册错误

适用于 1810 和更高版本

显示设备注册错误计数的表。  


### <a name="workload-transition"></a>工作负荷转换

适用于所有版本

显示一个条形图，其中包含为可用工作负荷而转换为 Microsoft Intune 的设备数量。 （工作负荷列表因 Configuration Manager 的版本而异。 有关详细信息，请参阅[能够转换到 Intune 的工作负荷](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune)。）

将鼠标悬停在图表某个部分上方可显示为该工作负荷转换的设备的数量。 
 ![工作负荷转换条形图](media/co-management-dashboard/Workload-Transition.PNG)


## <a name="next-steps"></a>后续步骤

有关共同管理的详细信息，请参阅：
 - [适用于 Windows 10 设备的共同管理](/sccm/core/clients/manage/co-management-overview)
 - [准备 Windows 10 设备进行共同管理](/sccm/core/clients/manage/co-management-prepare)

    
