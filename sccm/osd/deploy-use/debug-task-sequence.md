---
title: 调试任务序列
titleSuffix: Configuration Manager
description: 使用任务序列调试工具对任务序列进行故障排除。
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00c05b7023f90783fbdd741a354cfd6382f632ad
ms.sourcegitcommit: f7e4ff38d4b4afb49e3bccafa28514be406a9d7b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69549561"
---
# <a name="debug-a-task-sequence"></a>调试任务序列

<!--3612274-->

从1906版开始, 任务序列调试器是一种新的疑难解答工具。 在调试模式下将任务序列部署到小集合。 这样便可通过可控方式单步执行任务序列，以帮助进行故障排除和调查。 调试器当前与任务序列引擎运行在同一设备上, 它不是远程调试器。

> [!Note]  
> 在此版本的 Configuration Manager 中, 任务序列调试器是预发行功能。 若要启用此功能，请参阅[预发行功能](/sccm/core/servers/manage/pre-release-features)。  


## <a name="prerequisites"></a>先决条件

- 更新目标设备上的 Configuration Manager 客户端

- 以本地**管理员**组中的用户身份登录到目标设备。 调试器只为管理员运行。

- 更新与任务序列关联的启动映像，以确保其具有最新的客户端版本


## <a name="start-the-tool"></a>启动工具

1. 在 Configuration Manager 工作区中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”    。

1. 选择任务序列。 在功能区的部署组中，选择“调试”  。

    > [!Tip]  
    > 或者，在部署任务序列的集合或计算机对象上将变量“TSDebugMode”设置为 `TRUE`  。 具有此变量集的任何设备会将部署的任何任务序列置于调试模式。

1. 创建调试部署。 部署设置与常规任务序列部署相同。 有关详细信息，请参阅 [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence#process)。

    > [!Note]  
    > 您只能为调试部署选择一个小集合。 它仅显示具有10个或更少成员的设备集合。


## <a name="use-the-tool"></a>使用工具

任务序列在设备上运行时，“任务序列调试器”窗口将打开，类似于以下屏幕截图：

![任务序列调试器的屏幕截图](media/3612274-tsdebug.png)

调试器包含以下控件：

- **步骤**：从“当前”位置，仅运行任务序列中的下一步  。  

    > [!Note]  
    > 当任务序列处于调试模式时, 如果某个步骤返回致命错误, 则任务序列不会正常运行。 此行为使你可以选择在进行外部更改后重试步骤。

- **运行**：从“当前”位置，正常运行任务序列到结束或下一个“中断”点（如果步骤失败）   。 使用此操作之前, 请确保使用**设置中断**操作设置任何断点。

- **设置当前**：在调试器中选择一个步骤，然后选择“设置当前”  。 此操作将“当前”指针移动到该步骤  。 此操作允许跳过步骤或向后移动。  

    > [!Warning]  
    > 当你更改序列中的当前位置时，调试器不会考虑步骤的类型。 一些步骤可能会设置条件评估所需的任务序列变量, 如后面的步骤所述。 如果运行顺序颠倒，某些步骤可能会失败或对设备造成重大损坏。 使用此选项需要自担风险。  

- **设置中断**：在调试器中选择一个步骤，然后选择“设置中断”  。 此操作将在调试器中添加“中断”点  。 “运行”任务序列时，它会在“中断”处停止   。  

    - 使用 "**运行**" 操作之前, 请设置断点。

    - 计算机重启后, 中断点不会保存, 如 "[重新启动计算机](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer)" 步骤。 例如, 如果从软件中心为映像任务序列启动调试器, 请不要在 Windows PE 阶段中设置中断。 当计算机重新启动到 Windows PE 时, 调试器将暂停任务序列, 以便可以设置中断。

- **清除所有**中断点: 删除所有断点。

- **日志文件**: 用[CMTrace](/sccm/core/support/cmtrace)打开当前任务序列日志文件**smsts.log**。 当任务序列引擎 "正在等待调试程序" 时, 可以看到日志条目。

- **Cmd 提示符**: 在 Windows PE 中, 打开命令提示符。

- **取消**: 关闭调试器, 并使任务序列失败。

- **Quit**: 分离并关闭调试器, 但任务序列继续正常运行。

"**任务序列变量**" 窗口显示任务序列环境中所有变量的当前值。 有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables)。 如果将 "[设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)" 步骤用于选项 "**不显示此值**", 则调试器不会显示变量值。 不能在调试器中编辑变量值。

> [!Note]
> 某些任务序列变量仅供内部使用, 而不是在参考文档中列出。

任务序列调试器会在[重新启动计算机](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer)步骤之后继续运行, 但您需要重新创建断点。 尽管任务序列可能不需要它, 但由于调试器需要用户交互, 因此你需要登录到 Windows 以继续。 如果在一小时后未登录就可以继续调试, 则任务序列将失败。

它还使用[运行任务序列](/sccm/osd/understand/task-sequence-steps#child-task-sequence)步骤逐步执行子任务序列。 "调试器" 窗口显示子任务序列以及主任务序列的步骤。


## <a name="known-issues"></a>已知问题

如果通过多个部署以普通部署和调试部署为目标, 则任务序列调试器可能无法启动。


## <a name="see-also"></a>另请参阅

- [关于任务序列步骤](/sccm/osd/understand/task-sequence-steps)
- [任务序列变量](/sccm/osd/understand/task-sequence-variables)
- [如何使用任务序列变量](/sccm/osd/understand/using-task-sequence-variables)
- [部署任务序列](/sccm/osd/deploy-use/deploy-a-task-sequence)
