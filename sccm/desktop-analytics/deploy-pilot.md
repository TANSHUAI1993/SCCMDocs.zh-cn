---
title: 如何将部署到试运行
titleSuffix: Configuration Manager
description: 用于部署到桌面分析试验组的操作方法指南。
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4aa078f5a8306cb30ea83d45b93b18971be7764f
ms.sourcegitcommit: 5ee9487c891c37916294bd34a10d04e398f111f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59069375"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>如何将部署到试运行时使用 Desktop 分析

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

Desktop 分析的好处之一是帮助标识设备，可提供因素范围最广范围的最小集。 它主要关注对试运行 Windows 和 Office 的升级和更新最重要的因素。 确保来说，试点更大的成功，可将更快、 更有信心地移动到生产环境中广泛部署。  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]



## <a name="address-issues"></a>解决问题

使用 Desktop 分析门户来查看报告的所有问题的可能会阻止你的部署的资产。 然后批准、 拒绝或修改建议的修复方法。 必须将标记的所有项**准备**或**准备 （进行修正）** 试验部署开始之前。

1. 转到桌面分析门户中，并选择**部署计划**管理组中。  

2. 选择其名称以打开部署计划。  

3. 选择**准备试点**部署计划菜单上的准备组中。  

4. 上**应用**选项卡上，查看需要你的反馈的应用。  

5. 对于每个应用，选择应用名称。 在信息窗格中查看建议，并选择升级决策。 如果愿意**未检查**或**无法**，则桌面分析不会将试验部署包含与此应用的设备。 如果愿意 **（进行修正） 准备**，使用**修正说明**来捕获解决问题所采取的操作，这类似于*重新安装*或*查找制造商的建议的版本*。

6. 重复此评审的其他资产。  



## <a name="create-software"></a>创建的软件

你可以部署 Windows 或 Office 之前，先软件对象创建 Configuration Manager 中。

- [Office 365 专业增强版应用程序](https://docs.microsoft.com/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)  

- [Windows 10 就地升级任务序列](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)



## <a name="deploy-to-pilot-devices"></a>将部署到试运行的设备

Configuration Manager 使用 Desktop 分析中的数据创建试验部署的集合。 不需要部署使用的是传统的部署的应用程序或任务序列。 使用以下过程创建桌面 Analytics 集成的部署：

1. 在 Configuration Manager 控制台中，转到**软件库**，展开**Desktop 分析服务**，然后选择**部署计划**节点。  

2. 选择部署计划，并选择**部署计划的详细信息**功能区中。  

3. 在中**试验状态**磁贴中，从下拉列表中选择下列对象类型之一：  

    - **应用程序**适用于 Office 365 专业增强版  

    - **任务序列**适用于 Windows 10  
  
   选择**部署**。 此操作将启动部署软件向导对所选的对象类型。

    > [!Note]  
    > 通过桌面 Analytics 集成，Configuration Manager 自动创建的试验部署计划的集合。 它可能需要 10 分钟的时间为此集合可以使用它之前进行同步。<!-- 3887891 -->
    >
    > 此集合被保留的桌面分析部署计划设备。 不支持对此集合的手动更改。<!-- 3866460, SCCMDocs-pr 3544 -->  

有关详细信息，请参阅下列文章：  

- [部署应用程序](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy)  

- [部署任务序列](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)  

如果你的部署计划适用于 Windows 10 和 Office 365，请重复此过程以创建第二个部署。 例如，如果第一个部署是为任务序列，创建的第二个部署的应用程序。



## <a name="monitor"></a>监视器

### <a name="configuration-manager-console"></a>Configuration Manager 控制台

使用配置管理器部署相同监视任何其他应用程序和任务序列部署。 有关详细信息，请参阅下列文章：  

- [从 Configuration Manager 控制台监视应用程序](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

- [监视 OS 部署](/sccm/osd/deploy-use/monitor-operating-system-deployments)  


### <a name="desktop-analytics-portal"></a>桌面分析门户

使用 Desktop 分析门户中查看任何部署计划的状态。 选择部署计划，然后选择**计划概述**。

![在桌面 Analytics 中的部署计划概述的屏幕截图](media/deployment-plan-overview.png)

选择**试点**磁贴。 它概述了试验部署的当前状态。 此磁贴还显示编号的设备未启动，在进行、 已完成，或返回问题的数据。

报告错误或其他问题的任何设备还会在右侧的试运行详细信息区域中列出。 若要报告的问题的详细信息，请选择**评审**。 此操作将视图更改为**部署状态**页

**部署状态**页列出了以下类别中的设备：

- 未启动
- 正在进行
- 已完成
- 需要注意的设备
- 需要注意的问题

**需要注意**类别以不同方式显示相同的信息，但已排序。

在任一视图，以获取有关检测到的问题的更多详细信息中选择特定的列表。

随着您解决部署问题，在仪表板将继续显示设备的进度。 它将更新从移动设备**需要关注**到**Completed**。



## <a name="next-steps"></a>后续步骤

让一段时间来收集操作数据的试验运行。 鼓励用户的试运行设备测试应用程序、 加载项和宏。

在你的试验部署符合您的成功条件时，请转到下一篇文章中部署到生产环境。
> [!div class="nextstepaction"]  
> [部署到生产环境](/sccm/desktop-analytics/deploy-prod)  
