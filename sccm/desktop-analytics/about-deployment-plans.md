---
title: 桌面分析中的部署计划
titleSuffix: Configuration Manager
description: 了解桌面分析中的部署计划。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a1acd99ca1a4676c4397eee427cdcb8b795cf00
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68956399"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>关于桌面分析中的部署计划

> [!Note]  
> 此信息与预览版服务相关, 该服务可能会在商业发布之前进行大量修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

桌面分析收集并分析组织中的设备、应用程序和驱动程序数据。 根据此分析和你的输入, 你可以使用服务创建适用于 Windows 10 的部署计划。 部署计划具有以下功能:  

- 自动建议在试验中包含哪些设备  

- 确定兼容性问题和建议缓解措施  

- 在更新之前、期间和更新后评估部署的运行状况  

- 跟踪部署进度  

作为部署计划的一部分, 你可以执行以下操作:  

- 定义要部署的 Windows 10 版本  

- 选择要部署到的设备组  

- 为部署创建准备情况规则  

- 定义应用的重要性  

- 根据自动建议选择试点设备  

- 根据桌面分析中的建议确定如何修复应用的问题  

默认情况下, 桌面分析每日刷新部署计划数据。 在部署计划中所做的任何更改 (例如, 将重要性分配给应用或选择要包括在试点中的设备) 最多需要24小时才能完成处理。 若要加快此过程, 请请求按需进行数据刷新。 有关详细信息, 请参阅[桌面分析常见问题解答](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。  

将桌面分析连接到 Configuration Manager 后, 请在部署计划中选择集合。 此集成使你能够根据桌面分析数据将 Windows 部署到集合。



## <a name="readiness-rules"></a>准备情况规则

部署计划中提供了以下准备情况规则:

- 设备是否自动接收来自 Windows 更新的驱动程序。 如果设备接收到 Windows 更新的驱动程序更新, 则在准备情况评估过程中标识的任何驱动程序问题都将自动标记为 "**就绪**"。  

- 适用于你的 Windows 应用的低安装计数阈值。 如果应用安装在比此阈值更高的计算机上, 则部署计划会将应用标记为 "**值得注意**"。 此标记表示你可以决定应用在试验阶段测试的重要性。  


## <a name="plan-assets"></a>计划资产

<!-- 4670224 -->

虽然 "[资产](/sccm/desktop-analytics/about-assets)" 区域还显示了设备和应用, 但特定部署计划下的 "**计划资产**" 区域包含附加信息。

### <a name="devices"></a>设备

请参阅部署计划中每个设备的**Windows 升级决定**。

**替换设备**的 Windows 升级决策可能是由于以下原因之一导致的:

- 它未通过 Windows 10 所需的处理器检查。 有关详细信息, 请参阅[最低硬件要求](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor)。
- 它包含 BIOS 块
- 没有足够的内存
- 系统上的启动关键组件包含被阻止的驱动程序
- 特定品牌和型号无法升级
- 有一个显示类组件, 其中包含具有以下所有属性的驱动程序块:
    - 不替代
    - 新的操作系统版本中不存在驱动程序
    - 它尚未处于 Windows 更新
- 系统上有另一个可用于阻止升级的 "即插即用" 组件
- 存在使用 XP 模拟驱动程序的无线组件
- 具有活动连接的网络组件将丢失其驱动程序。 换句话说, 升级后可能会失去网络连接。

### <a name="apps"></a>应用

在此部署计划中设置此应用程序的**升级决策**和**重要性**。 有关详细信息, 请参阅[如何创建部署计划](/sccm/desktop-analytics/create-deployment-plans)。

在应用的详细信息中, 还可以看到以下信息:建议、兼容性风险因素和 Microsoft 已知问题。 使用此信息可帮助设置**升级决策**。 有关详细信息, 请参阅[兼容性评估](/sccm/desktop-analytics/compat-assessment)。

桌面分析显示为 "*值得注意*" 的应用基于部署计划的准备情况规则的低安装计数阈值。 有关详细信息, 请参阅[准备情况规则](/sccm/desktop-analytics/create-deployment-plans#readiness-rules)。

#### <a name="a-namebkmk_plan-autoapp--automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" />系统和应用商店应用的自动升级决策

<!-- 3587232 -->
确定**重要性**和**升级决策**对于桌面分析工作流中的所有值得注意的应用而言至关重要。 为了帮助减少对这些应用进行注释的工作量, 某些类型的应用会自动标记为*不重要*。 这些应用的部署计划升级决策也标记为 "*就绪*"。 以下应用是兼容的, 并且应在升级 Windows 后继续工作:

- Microsoft 发布的系统应用和组件

- 从 Microsoft Store 管理和更新的应用

> [!Tip]
> 管理全局级别或按部署计划的任何应用的输入。
>
> 1. 在桌面分析门户的 "**管理**" 菜单中, 选择 "**资产**"。 然后选择 "**应用**"。
>
> 2. 使用 "**类型**" 和 "**类别**" 列可以管理这些应用类别:
>
>    - 适用于应用商店应用, 筛选器**类型**为**新式**
>    - 对于系统应用, 筛选**类别**为**后台进程**或**Windows 组件**


### <a name="drivers"></a>驱动程序

请参阅此部署计划中包含的驱动程序列表。 设置**升级决策**, 查看 Microsoft 的建议, 并参阅兼容性风险因素。


## <a name="importance"></a>重要性

作为部署计划的一部分, 请设置应用的*重要性*。 桌面分析在目标设备上检测到这些应用。 此设置可帮助桌面分析确定它在部署的试验阶段中包含的设备。

如果在目标设备的 2% 以下的设备上安装了应用, 则会将其标记为 "**低安装计数**"。 默认值为 2%。 可以在就绪设置中将阈值从 0% 调整到 10%。 桌面分析会自动将这些应用标记为已**准备好升级**。  

对于应用, 请选择 "**关键**"、"**重要**" 或 "**不重要**" 的重要性。 如果将一个标记为关键或重要, 则桌面分析会在试验部署中包括该应用的一些设备。 此服务包括在关键应用程序的试点更多实例中。 如果将某个应用标记为不重要, 桌面分析会自动将其设置为 "**准备升级**"。



## <a name="pilot-devices"></a>试点设备

桌面分析将重要信息与全局试点设置结合起来。 然后, 它将创建一个建议, 用于应对试验部署的设备。 建议的试验部署包括具有不同硬件配置的设备以及所有关键和重要应用程序的一个或多个实例。 如果某个应用被标记为 "严重", 则该服务会在试验中建议使用该应用的更多设备。



## <a name="deployment-plans-in-configuration-manager"></a>Configuration Manager 中的部署计划

创建部署计划后, 使用 Configuration Manager 部署产品。 部署开始后, 桌面分析会根据计划中的设置来监视部署。


## <a name="next-steps"></a>后续步骤

- [了解桌面分析资产](/sccm/desktop-analytics/about-assets): 设备、驱动程序和应用  

- [了解安全性和功能更新](/sccm/desktop-analytics/about-updates)  

- [创建部署计划](/sccm/desktop-analytics/create-deployment-plans)  
