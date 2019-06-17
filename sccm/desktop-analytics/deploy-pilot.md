---
title: 如何将部署到试运行
titleSuffix: Configuration Manager
description: 用于部署到桌面分析试验组的操作方法指南。
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: e18e2e43e9bb768f81233fb2d2deda0ae05c1961
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67145838"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>如何将部署到试运行时使用 Desktop 分析

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

Desktop 分析的好处之一是帮助标识设备，可提供因素范围最广范围的最小集。 它主要关注对试运行 Windows 升级和更新最重要的因素。 确保来说，试点更大的成功，可将更快、 更有信心地移动到生产环境中广泛部署。  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]


## <a name="identify-devices"></a>标识设备

第一步是标识要包括在试验中的设备。 桌面的分析建议基于所报告的数据，设备和可以包括或替换此列表中的设备。

1. 转到[Desktop 分析门户](https://aka.ms/desktopanalytics)，并在管理组中选择**部署计划**。

1. 选择部署计划。

1. 在部署计划菜单上的准备组中，选择**标识试点**。

你将看到来自显示建议的最佳覆盖范围包括的设备数的桌面分析数据。 此算法主要基于重要和关键应用程序的使用和广泛的硬件配置。

执行以下操作的其他建议的设备列表：

- **将全部添加到试验**:将所有建议的设备添加到试验组
- **将添加到试验**:只能添加单个设备
- **替换为**试验的任何特定设备
- **重新计算**完成后进行更改

此外可以将整个系统决定哪些 Configuration Manager 集合以包含或排除飞行员。 在 Desktop 分析主菜单中，在全局设置组中，选择**全局试点**。

### <a name="example"></a>示例

- Configuration Manager 中为目标配置桌面 Analytics 连接**所有系统**集合。 此操作注册到服务的所有客户端。
- 您还可以配置其他集合与 Desktop 分析进行同步：
    - 所有 Windows 10 客户端
    - 所有 IT 设备
    - 首席执行官 office
- 在中**全局试点**设置，则包含**所有 IT 设备**集合。 排除**首席执行官 office**集合。
- 创建部署计划，并选择**所有 Windows 10 客户端**集合。
- 你**试验包含设备**列表包含下面的设备设置：
    - 全局试验包含列表中的任何设备：**所有 IT 设备**
    - 也是部署计划的目标组的一部分的集合：**所有 Windows 10 客户端**
- 从桌面分析中排除**其他推荐的设备**列表中全局试验的任何设备*排除*列表：**首席执行官 office**
- 只有前两个集合都被视为试点的一部分。 成功升级到这些组和资产后*准备好*，桌面分析中的设备同步**首席执行官 office**到 Configuration Manager 生产集合的集合。


## <a name="address-issues"></a>解决问题

使用 Desktop 分析门户来查看报告的所有问题的可能会阻止你的部署的资产。 然后批准、 拒绝或修改建议的修复方法。 必须将标记的所有项**准备**或**准备 （进行修正）** 试验部署开始之前。

1. 转到[Desktop 分析门户](https://aka.ms/desktopanalytics)，并在管理组中选择**部署计划**。  

2. 选择部署计划。  

3. 在部署计划菜单上的准备组中，选择**准备试点**。  

4. 上**应用**选项卡上，查看需要你的反馈的应用。  

5. 对于每个应用，选择应用名称。 在信息窗格中查看建议，并选择升级决策。 如果愿意**未检查**或**无法**，则桌面分析不会将试验部署包含与此应用的设备。 如果愿意 **（进行修正） 准备**，使用**修正说明**来捕获解决问题所采取的操作，这类似于*重新安装*或*查找制造商的建议的版本*。

6. 重复此评审的其他资产。  


## <a name="create-software"></a>创建的软件

你可以部署 Windows 之前，先软件对象创建 Configuration Manager 中。 有关详细信息，请参阅[Windows 10 就地升级任务序列](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)。


## <a name="deploy-to-pilot-devices"></a>将部署到试运行的设备

Configuration Manager 使用 Desktop 分析中的数据创建试验和生产部署的集合。 为了确保设备处于正常状态的每个部署阶段完成之后，请使用以下过程创建桌面 Analytics 集成的分阶段的部署：

1. 在 Configuration Manager 控制台中，转到**软件库**，展开**Desktop 分析服务**，然后选择**部署计划**节点。  

2. 选择部署计划，并选择**部署计划的详细信息**功能区中。  

3. 选择**创建分阶段部署**功能区中。 此操作将启动创建分阶段部署向导。

    > [!Tip]  
    > 如果你想要创建的经典的任务序列部署的只是试验集合，请选择**部署**中**试验状态**磁贴。 此操作将启动部署软件向导。 有关详细信息，请参阅 [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence)。  

4. 输入部署的名称，然后选择要使用的任务序列。 使用选项来**自动创建默认的两个阶段部署**，然后配置下列集合：  

    - **第一个集合**:找到并选择**试点**此部署计划的集合。 为此集合的标准命名约定是`<deployment plan name> (Pilot)`。

    - **第二个集合**:找到并选择**生产**此部署计划的集合。 为此集合的标准命名约定是`<deployment plan name> (Production)`。

    > [!Note]  
    > 通过桌面 Analytics 集成，Configuration Manager 会自动创建试验和生产部署计划的集合。 它可能需要 10 分钟这些集合可以使用它们之前进行同步。<!-- 3887891 -->
    >
    > 这些集合仅供 Desktop 分析部署计划设备。 不支持对这些集合的手动更改。<!-- 3866460, SCCMDocs-pr 3544 -->  

5. 完成向导以配置分阶段的部署。 有关详细信息，请参阅[创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)。

    > [!Note]  
    > 使用默认设置为**会自动开始此阶段后延迟期 （以天为单位）** 。 若要启动的第二个阶段，必须满足以下条件：
    >
    > 1. 试验设备需要升级，然后发送后修改了诊断数据。
    > 1. 第一阶段达到**部署成功百分比**成功标准。 在分阶段部署配置此设置。
    > 1. 您需要检查并在桌面 Analytics，以将标记为重要和关键资产升级决策*准备*。 有关详细信息，请参阅[查看需要升级决策的资产](/sccm/desktop-analytics/deploy-prod#bkmk_review)。
    > 1. 同步到 Configuration Manager 集合满足任何生产设备的桌面分析*准备*条件。
    >
    > 当配置管理器分阶段部署将自动移动到下一阶段，仅适用于桌面 Analytics 同步生产集合中的设备。

> [!Important]  
> 这些集合继续作为其成员身份的更改进行同步。 例如，如果您确定问题与一个资产并将其标记为**无法**，与该资产的设备不再满足*准备*条件。 这些设备将从生产部署集合中删除。


## <a name="monitor"></a>监视器

### <a name="configuration-manager-console"></a>Configuration Manager 控制台

打开部署计划。 **准备升级决策的总体状态**磁贴提供有关部署计划的状态摘要。 此状态是针对你的试点和生产集合。 设备可以分为以下类别之一：

- **最新**:设备已升级到目标 Windows 版本的此部署计划

- **升级决策完整**:以下状态之一：
    - 值得注意的内容资产的设备**准备好**或**准备进行修正**
    - 设备状态**已阻止**，**替换为设备**或**重新安装设备**

- **未检查**:值得注意的内容的资产的设备**未检查**或**评审正在进行中**

设备状态中的更新**试验状态**并**生产状态**磁贴执行以下操作：

- 兼容性评估进行更改
- 设备升级到 Windows 目标版本
- 部署进度

此外可以使用监视与任何其他任务序列部署相同的配置管理器部署。 有关详细信息，请参阅[监视器 OS 部署](/sccm/osd/deploy-use/monitor-operating-system-deployments)。


### <a name="desktop-analytics-portal"></a>桌面分析门户

使用[Desktop 分析门户](https://aka.ms/desktopanalytics)若要查看任何部署计划的状态。 选择部署计划，然后选择**计划概述**。

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

让一段时间才能收集操作数据的试验运行。 鼓励用户的试运行设备测试应用程序。

在你的试验部署符合您的成功条件时，请转到下一篇文章中部署到生产环境。
> [!div class="nextstepaction"]  
> [部署到生产环境](/sccm/desktop-analytics/deploy-prod)  
