---
title: 管理和监视分阶段部署
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中管理和监视软件的分阶段部署。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5ebf89e46b33649f12ea5770d6e771e811a66094
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125725"
---
# <a name="manage-and-monitor-phased-deployments"></a>管理和监视分阶段部署

本文介绍如何管理和监视分阶段部署。 管理任务包括手动开始下一阶段、暂停或恢复某一阶段。 

首先，需要创建分阶段部署： 
- [应用程序](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [软件更新](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [任务序列](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  



## <a name="bkmk_move"></a> 进入下一阶段

选择“手动开始部署的第二阶段”设置时，站点不会根据成功标准自动开始下一阶段。 需要将分阶段部署移动到下一阶段。  

1. 启动此操作的方法因部署软件的类型而有所不同：  

    - **应用程序**（仅在版本 1806 或更高版本中）：转到“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”。   

    - **软件更新**（仅在版本 1810 或更高版本中）：转到“软件库”工作区，再选择以下节点之一：    
        - 软件更新  
            - **所有软件更新**  
            - **软件更新组**   
        - Windows 10 服务、所有 Windows 10 更新  
        - Office 365 客户端管理、Office 365 更新  

    - **任务序列**：转到“软件库”工作区，展开“操作系统”，选择“任务序列”。   

2. 选择具有分阶段部署的软件。  

3. 在详细信息窗格中，切换到“分阶段部署”选项卡。  

4. 选择分阶段部署，并单击功能区中的“进入下一阶段”。  

    ![右键单击显示分阶段部署上的操作的菜单](media/Suspend-phased-deployment.PNG)



## <a name="bkmk_suspend"></a> 暂停或恢复阶段 

可手动暂停或恢复分阶段部署。 例如，针对任务序列创建分阶段部署。 监视试点组的阶段时，注意到大量的失败数。 暂停分阶段部署可阻止其他设备再运行任务序列。 解决问题后，恢复分阶段部署以继续推出。 

1. 启动此操作的方法因部署软件的类型而有所不同：  

    - **应用程序**（仅在版本 1806 或更高版本中）：转到“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”。   

    - **软件更新**（仅在版本 1810 或更高版本中）：转到“软件库”工作区，再选择以下节点之一：    
        - 软件更新  
            - **所有软件更新**  
            - **软件更新组**   
        - Windows 10 服务、所有 Windows 10 更新  
        - Office 365 客户端管理、Office 365 更新  

    - **任务序列**：转到“软件库”工作区，展开“操作系统”，选择“任务序列”。 选择一个现有任务序列，然后单击功能区中的“创建分阶段部署”。  

2. 选择具有分阶段部署的软件。  

3. 在详细信息窗格中，切换到“分阶段部署”选项卡。  

4. 选择分阶段部署，并单击功能区中的“暂停”或“恢复”。  

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="bkmk_monitor"></a> 监视
<!--1358577-->

从版本 1806 开始，分阶段部署具有本地监视体验。 从“监视”工作区中的“部署”节点，选择分阶段部署，然后单击功能区中的“分阶段部署状态”。

![显示两个阶段的状态的分阶段部署状态仪表板](media/1358577-phased-deployment-status.png)

此仪表板显示部署的每个阶段的以下信息：  

- **设备总数**：此阶段针对多少台设备。  

- **状态**：此阶段的当前状态。 每个阶段可以为以下状态之一：  

    - **已创建部署**：分阶段部署为此阶段创建了软件到集合的部署。 使用此软件主动针对客户端。  

    - **等待中**：之前的阶段尚未达到让部署继续到此阶段的成功标准。  

    - **已挂起**：管理员已挂起部署。  

- **进度**：客户端中用颜色标明的部署状态。 例如：成功、进行中、错误、不符合要求以及未知。 

#### <a name="success-criteria-tile"></a>成功标准磁贴

使用“选择阶段”下拉列表更改“成功标准”磁贴的显示。 此磁贴将阶段目标与部署的当前符合性进行比较。 在默认设置下，阶段目标是 95%。 此值意味着部署需要达到 95% 的符合性才能进入下一阶段。 

在此示例中，阶段目标是 65%，当前符合性是 66.7%。 分阶段部署自动进入到第二阶段，因为第一阶段满足成功标准。  

![来自分阶段部署状态的示例成功标准磁贴](media/pod-status-success-criteria-tile.png)

阶段目标与下一阶段的阶段设置上的部署成功百分比相同。 为让分阶段部署开始下一阶段，该第二阶段会定义第一阶段的成功标准。 查看此设置： 

1. 转到软件上的分阶段部署对象，并打开分阶段部署属性。  

2. 切换到“阶段”选项卡。选择“第 2 阶段”，然后单击“查看”。  

3. 在阶段属性窗口中，切换到“阶段设置”选项卡。  

4. 查看“上一阶段的成功标准”组中“部署成功百分比”的值。  

例如，以下属性用于与上面显示的成功标准磁贴相同的阶段，其中标准为 65％：  
![阶段属性上的阶段设置选项卡](media/phase-properties-phase-settings.png)

