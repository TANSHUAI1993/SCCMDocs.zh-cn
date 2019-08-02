---
title: 如何部署到试点
titleSuffix: Configuration Manager
description: 部署到桌面分析试验组的操作指南。
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa7566779fe346ddecfd546dc89dc8618fb39953
ms.sourcegitcommit: ef7800a294e5db5d751921c34f60296c1642fc1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68712652"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>如何通过桌面分析部署到试点

> [!Note]  
> 此信息与预览版服务相关, 该服务可能会在商业发布之前进行大量修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

桌面分析的优点之一是帮助识别提供最广泛的因素的最小设备集。 它侧重于对 Windows 升级和更新的试验最为重要的因素。 确保试验更成功, 使你能够更快、更自信地在生产环境中进行广泛的部署。  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]


## <a name="identify-devices"></a>标识设备

第一步是确定要包括在试点中的设备。 桌面分析根据报告的数据推荐设备, 并可包括或替换此列表中的设备。

1. 请中转到[桌面分析门户](https://aka.ms/desktopanalytics), 并在 "管理" 组中选择 "**部署计划**"。

1. 选择部署计划。

1. 在 "部署计划" 菜单的 "准备" 组中, 选择 "**标识试点**"。

你将看到桌面分析中的数据, 其中显示了建议包含的设备数以获得最佳覆盖范围。 此算法主要基于重要和关键应用的使用, 以及各种硬件配置。

对于 "推荐的其他设备" 列表, 请执行以下操作:

- **全部添加到试点**:将所有推荐的设备添加到试点组
- **添加到试验**:仅添加单个设备
- 将所有特定设备**替换**为试验
- 进行更改后**重新计算**

你还可以对要在其中包含或排除的 Configuration Manager 集合进行系统范围的决策。 在主桌面分析菜单的 "全局设置" 组中, 选择 "**全局试点**"。

### <a name="example"></a>示例

- 在 Configuration Manager 中配置桌面分析连接, 以面向 "**所有系统**" 集合。 此操作可将所有客户端注册到服务。
- 还可将其他集合配置为与桌面分析同步:
    - 所有 Windows 10 客户端
    - 所有 IT 设备
    - CEO 办公
- 在**全局试点**设置中, 包括 "**所有 IT 设备**" 集合。 你排除**CEO 办公**托收。
- 创建一个部署计划, 并选择 "**所有 Windows 10 客户端**集合" 作为**目标组**。
- "**试点设备包含**" 列表包含**目标组**中的设备子集:所有同时位于全局试验*包含*列表中的**Windows 10 客户端**:**所有 IT 设备**  
- "**其他建议的设备**" 列表包含**目标组**中的一组设备, 这些设备可为重要资产提供最大的覆盖范围和冗余。  桌面分析从此列表中排除全局试验*排除*列表中的任何设备:**CEO 办公**


## <a name="address-issues"></a>解决问题

使用桌面分析门户查看可能会阻止你的部署的资产的任何已报告问题。 然后批准、拒绝或修改建议的修补程序。 在试验部署开始之前, 所有项都必须标记为 "**就绪**" 或 "**就绪" (带有修正)** 。

1. 请中转到[桌面分析门户](https://aka.ms/desktopanalytics), 并在 "管理" 组中选择 "**部署计划**"。  

2. 选择部署计划。  

3. 在 "部署计划" 菜单的 "准备" 组中, 选择 "**准备试点**"。  

4. 在 "**应用**" 选项卡上, 查看需要你的输入的应用。  

5. 对于每个应用, 请选择 "应用名称"。 在信息窗格中, 查看 "建议", 然后选择 "升级决策"。 如果选择了 "**未查看**" 或 "**无法**查看", 则桌面分析不会在试验部署中包含具有此应用的设备。 如果选择 "**就绪" (带修正)** , 请使用**更正说明**来捕获解决问题所需采取的措施, 如*重新安装*或*查找制造商建议的版本*。

6. 对其他资产重复此评审。  


## <a name="create-software"></a>创建软件

在部署 Windows 之前, 请先在 Configuration Manager 中创建软件对象。 有关详细信息, 请参阅[Windows 10 就地升级任务序列](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)。


## <a name="deploy-to-pilot-devices"></a>部署到试验设备

Configuration Manager 使用桌面分析中的数据来创建试点和生产部署的集合。 若要确保设备在每个部署阶段后正常运行, 请使用以下过程创建桌面分析集成的分阶段部署:

1. 在 Configuration Manager 控制台中, 请参阅 "**软件" 库**, 展开 "**桌面分析服务**", 然后选择 "**部署计划**" 节点。  

2. 选择部署计划, 然后在功能区中选择 "**部署计划详细信息**"。  

3. 在功能区中选择 "**创建分阶段部署**"。 此操作将启动 "创建分阶段部署向导"。

    > [!Tip]  
    > 如果要为试验集合创建经典任务序列部署, 请在 "**试点状态**" 磁贴中选择 "**部署**"。 此操作将启动 "部署软件向导"。 有关详细信息，请参阅 [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence)。  

4. 输入部署的名称, 并选择要使用的任务序列。 使用选项**自动创建默认的二阶段部署**, 然后配置以下集合:  

    - **第一个集合**:查找并选择此部署计划的**试验**集合。 此集合的标准命名约定是`<deployment plan name> (Pilot)`。

    - **第二个集合**:查找并选择此部署计划的**生产**集合。 此集合的标准命名约定是`<deployment plan name> (Production)`。

    > [!Note]  
    > 通过桌面分析集成, Configuration Manager 会自动创建部署计划的试点和生产集合。 在使用它们之前, 这些集合可能需要一些时间才能同步。 有关详细信息, 请参阅[故障排除-数据延迟](/sccm/desktop-analytics/troubleshooting#data-latency)。<!-- 4984639 -->
    >
    > 这些集合保留用于桌面分析部署计划设备。 不支持手动更改这些集合。<!-- 3866460, SCCMDocs-pr 3544 -->  

5. 完成向导以配置分阶段部署。 有关详细信息，请参阅[创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)。

    > [!Note]  
    > 使用默认设置,**在延迟期 (以天为单位) 后自动开始此阶段**。 必须满足以下条件才能开始第二阶段:
    >
    > 1. 第一阶段达到成功**部署的成功百分比**条件。 在分阶段部署上配置此设置。
    > 1. 需要在桌面分析中查看并做出升级决策, 以将重要的关键资产标记为 "*就绪*"。 有关详细信息, 请参阅[查看需要升级决策的资产](/sccm/desktop-analytics/deploy-prod#bkmk_review)。
    > 1. 桌面分析同步到 Configuration Manager 集合任何满足*就绪*条件的生产设备。

> [!Important]  
> 这些集合将继续同步, 因为其成员身份更改。 例如, 如果你发现资产问题并将其标记为 "**无法**识别", 则具有该资产的设备将不再满足 "*就绪*" 条件。 将从生产部署集合中删除这些设备。


## <a name="monitor"></a>监视器

### <a name="configuration-manager-console"></a>Configuration Manager 控制台

打开部署计划。 **准备升级决策-"总体状态**" 磁贴提供了部署计划状态的摘要。 此状态适用于试点和生产集合。 设备可以属于以下类别之一:

- **最**新:设备已升级到此部署计划的目标 Windows 版本

- **升级决策完成**:以下状态之一:
    - 具有已**准备就绪**或已**准备好修正的**资产的设备
    - 设备状态为 "已**阻止**"、"[**替换设备**](/sccm/desktop-analytics/about-deployment-plans#plan-assets)" 或 "**重新安装设备**"

- **未评审**:**未查看**或**正在查看**的具有值得注意的资产的设备

设备状态会在 "**试点状态**" 和 "**生产状态**" 磁贴中更新, 并具有以下操作:

- 对兼容性评估进行更改
- 设备升级到目标版本的 Windows
- 部署进度

你还可以使用与任何其他任务序列部署相同的 Configuration Manager 部署监视。 有关详细信息, 请参阅[监视操作系统部署](/sccm/osd/deploy-use/monitor-operating-system-deployments)。


### <a name="desktop-analytics-portal"></a>桌面分析门户

使用[桌面分析门户](https://aka.ms/desktopanalytics)查看任何部署计划的状态。 选择部署计划, 然后选择 "**计划概述**"。

![桌面分析中的部署计划概述的屏幕截图](media/deployment-plan-overview.png)

选择 "**试点**" 磁贴。 它汇总了试点部署的当前状态。 此磁贴还显示未开始、正在进行、已完成或返回问题的设备的数量数据。

报告错误或其他问题的任何设备也会在右侧的 "试点详细信息" 区域中列出。 若要获取所报告问题的详细信息, 请选择 "**查看**"。 此操作会将视图更改为 "**部署状态**" 页

"**部署状态**" 页列出了以下类别的设备:

- 未启动
- 正在进行
- 已完成
- 需要注意-设备
- 需要注意的问题

"**需要注意**" 类别显示相同的信息, 但以不同的方式进行排序。

在任一视图中选择特定列表以获取有关检测到的问题的更多详细信息。

解决这些部署问题时, 仪表板将继续显示设备的进度。 当设备从**需要注意**到**完成**时, 会进行更新。


## <a name="next-steps"></a>后续步骤

让试验运行一段时间, 收集操作数据。 鼓励试验设备的用户测试应用程序。

当试点部署满足你的成功条件时, 请参阅下一篇文章, 部署到生产环境。
> [!div class="nextstepaction"]  
> [部署到生产环境](/sccm/desktop-analytics/deploy-prod)  
