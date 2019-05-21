---
title: 创建分阶段部署
titleSuffix: Configuration Manager
description: 使用分阶段部署自动将软件推出到多个集合。
ms.date: 04/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 028d515efa2e685becec0790b0a7d7b64445e9cc
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65494745"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>使用 Configuration Manager 创建分阶段部署

*适用范围：System Center Configuration Manager (Current Branch)*

分阶段部署可在多个集合中自动协调有序地推出软件。 例如，将软件部署到试点集合，然后根据成功条件自动继续推出。 创建分阶段部署时，既可以使用默认的两个阶段，也可以手动配置多个阶段。 

针对以下对象创建分阶段部署：
- **任务序列**  
    - 任务序列的分阶段部署不支持 PXE 或介质安装   
- **应用程序**（从版本 1806 开始） <!--1358147-->  
- **软件更新**（从版本 1810 开始） <!--1358146-->  
    - 不能将自动部署规则与分阶段部署配合使用

> [!Tip]  
> 分阶段部署功能作为[预发行功能](/sccm/core/servers/manage/pre-release-features)在版本 1802 中首次引入。 从版本 1806 开始，此功能不再属于预发行功能。<!--1356837-->  



## <a name="prerequisites"></a>先决条件

#### <a name="security-scope"></a>安全作用域
任何没有“全部”安全作用域的管理用户都无法查看由分阶段部署创建的部署。 有关详细信息，请参阅 [安全作用域](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope)。

#### <a name="distribute-content"></a>分发内容
在创建分阶段部署前，请将关联内容分发到分发点。<!--518293-->  

- **应用程序**：在控制台中选择目标应用程序，并使用功能区中的“分发内容”操作。 有关详细信息，请参阅[部署和管理内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content)。   

- **任务序列**：在创建任务序列前，必须创建引用对象，如 OS 升级包。 在创建部署前分发这些对象。 使用每个对象上的“分发内容”操作，或使用任务序列。 若要查看所有引用内容的状态，请选择任务序列，然后切换到细节窗格中的“引用”选项卡。 有关详细信息，请参阅[准备进行 OS 部署](/sccm/osd/get-started/prepare-for-operating-system-deployment)中的特定对象类型。   

- **软件更新**：创建部署包并分发。 使用“下载软件更新向导”。 有关详细信息，请参阅[下载软件更新](/sccm/sum/deploy-use/download-software-updates)。  



## <a name="bkmk_settings"></a>阶段设置

这些设置是分阶段部署特有的。 在创建或编辑阶段时配置这些设置，控制分阶段部署过程的计划和行为。 


#### <a name="criteria-for-success-of-the-first-phase"></a>第一阶段成功的标准  

- **部署成功百分比**：指定要确保第一阶段成功，需成功完成部署的设备所占百分。 默认情况下，此值为 95%。 换而言之，针对此部署，当 95% 的设备的符合性状态都为“成功”时，站点认为第一阶段成功。 然后，该站点将继续进入第二阶段，并创建下一个集合的软件部署。  
- **成功部署的设备数**：已在 Configuration Manager 版本 1902 中添加。 指定要确保第一阶段成功，需成功完成部署的设备数。 当集合的大小可变并且你在前进到下一阶段前已有一定数量的设备成功部署时，此选项很有用。 <!--3555946-->


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>在第一阶段成功后开始第二阶段部署的条件  

- **在某个延迟时间段(以天为单位)后自动开始此阶段**：选择在第一阶段成功后开始第二阶段之前等待的天数。 默认情况下，此值为一天。  

- **手动开始第二阶段部署**：在第一阶段成功后，站点不会自动开始第二阶段。 此选项需手动启动第二阶段。 有关详细信息，请参阅[进入下一阶段](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move)。  

    > [!Note]  
    > 此选项不可用于应用程序的分阶段部署。  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>在此时间段内(以天为单位)逐渐提供此软件
<!--1358578-->
从版本 1806 开始，可配置此设置，以便在每个阶段逐步推出软件。 此行为有助于缓解部署问题的风险，降低网络上因向客户端分发内容而导致的负载。 此站点根据每个阶段的配置，逐步提供软件。 相对于使软件可用的时间，一个阶段中的每个客户端都有一个截止时间。 对于一个阶段中的所有客户端，可用时间和截止时间之间的时间窗都是相同的。 此设置的默认值为零，因此默认情况下，部署不受限制。 请勿设置大于 30 的值。<!--SCCMDocs-pr issue 2767--> 

![成功设置的分阶段部署条件](media/phased-deployment-criteria-for-success.png)

#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>配置与软件可用时间相关的截止时间行为  

- **需要尽快安装**：将设备上的安装截止时间设置为在确定目标设备后立即安装。  

- **需要在这段时间后进行安装**：将安装截止时间设置为在确定目标设备后的特定天数内安装。 默认情况下，此值为七天。   


<!--### Examples
Include a timeline diagram
-->



## <a name="bkmk_auto"></a>自动创建默认的二阶段部署

1. 在 Configuration Manager 控制台中启动“创建分阶段部署”向导。 此操作因要部署的软件类型而有所不同：  

    - **应用程序**（仅在版本 1806 或更高版本中）：转到“软件库”，展开“应用程序管理”，然后选择“应用程序”。 选择现有应用程序，然后选择功能区中的“创建分阶段部署”。  

    - **软件更新**（仅在版本 1810 或更高版本中）：转到“软件库”，展开“软件更新”并选择“所有软件更新”。 选择一个或多个更新，然后选择功能区中的“创建分阶段部署”。  

        此操作可用于以下节点的软件更新：  
        - 软件更新  
            - **所有软件更新**  
            - **软件更新组**   
        - Windows 10 服务、所有 Windows 10 更新  
        - Office 365 客户端管理、Office 365 更新  

    - **任务序列**：转到“软件库”工作区中，展开“操作系统”，然后选择“任务序列”。 选择现有任务序列，然后选择功能区中的“创建分阶段部署”。  

2. 在“常规”页上，为分阶段部署提供名称、说明（可选），并选择“自动创建默认的二阶段部署”。  

3. 选择“浏览”，然后为“第一个集合”和“第二个集合”字段选择目标集合。 对于任务序列和软件更新，请从设备集合中进行选择。 对于应用程序，请从用户或设备集合中进行选择。 选择“下一步”。  

    > [!Important]  
    > 如果部署可能存在高风险，“创建分阶段部署”向导不会就此发出通知。 有关详细信息，请参阅[用于管理高风险部署的设置](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments)以及[部署任务序列](/sccm/osd/deploy-use/deploy-a-task-sequence)时的说明。  

4. 在“设置”页上，为每个计划设置选择一个选项。 有关详细信息，请参阅[阶段设置](#bkmk_settings)。 完成后单击“下一步”。  

5. 在“阶段”页上，查看向导为指定集合创建的两个阶段。 选择“下一步”。   

    > [!Note]  
    > 本部分介绍自动创建默认两阶段部署的过程。 向导允许为分阶段部署添加、删除、重新排序、编辑或查看阶段。 有关这些其他操作的详细信息，请参阅[使用手动配置的阶段创建分阶段部署](#bkmk_manual)。  

6. 在“摘要”选项卡上确认选择，然后选择“下一步”完成向导。  



## <a name="bkmk_manual"></a>使用手动配置的阶段创建分阶段部署
<!--1358148--> 

从版本 1806 开始，可使用手动配置的任务序列阶段创建分阶段部署。 可从“创建分阶段部署”向导的“阶段”选项卡添加最多 10 个其他阶段。 

> [!Note]  
> 目前无法手动为应用程序创建阶段。 向导会自动为应用程序部署创建两个阶段。


1. 为任务序列或软件更新启动“创建分阶段部署”向导。  

2. 在“创建分阶段部署”向导的“常规”页上，为分阶段部署提供名称、说明（可选），并选择“手动配置所有阶段”。  

3. 在“创建分阶段部署”向导的“阶段”页中，可进行下列操作：  

    - 筛选部署阶段列表。 为“顺序”、“名称”或“集合”列输入匹配的字符串，不区分大小写。 

    - 添加新阶段：  

        1. 在“添加阶段向导”的“常规”页上，指定该阶段名称，然后浏览到目标“阶段集合”。 此页面上的其他设置与正常部署任务序列或软件更新时的设置相同。  

        2. 在“添加阶段向导”的“阶段设置”页上，配置计划设置，然后在完成后选择“下一步”。 有关详细信息，请参阅[设置](#bkmk_settings)。   

            > [!Note]  
            > 无法在第一阶段中编辑阶段设置：“部署成功百分比”或“成功部署的设备数”（版本 1902 或更高版本）。 此设置仅适用于具有上一阶段的阶段。  

        3. “添加阶段向导”的“用户体验”和“分发点”页面上的设置与正常部署任务序列或软件更新时的设置相同。  

        4. 查看“摘要”页上的设置，然后完成“添加阶段向导”。  

    - **编辑**：此操作将打开选定阶段的“属性”窗口，该窗口中的选项卡与“添加阶段向导”页面上的选项卡相同。  

    - **删除**：此操作将删除选定的阶段。  

       > [!Warning]  
       > 不会出现任何确认信息，并且无法撤消此操作。  

    - “上移”或“下移”：该向导按照添加方式对阶段进行排序。 最近添加的阶段位于列表最后。 若要更改顺序，请选择一个阶段，然后使用这些按钮，在列表中移动该阶段的位置。  

       > [!Important]  
       > 更改顺序后查看阶段设置。 请确保以下设置仍符合对此分阶段部署的要求：  
       > 
       > - 前一阶段成功的标准  
       > - 在上一阶段成功后开始此阶段部署的条件   

5. 选择“下一步”。 查看“摘要”页上的设置，然后完成“创建分阶段部署”向导。  


创建分阶段部署后，打开其属性进行更改：  

- 在现有分阶段部署中添加其他阶段。  

- 如果阶段未处于活动状态，可以对其进行“编辑”、“删除”、“上移”或“下移”。 无法将其移动到活动阶段之前。  

- 活动阶段处于只读状态。 不能对其进行编辑、删除或移动其在列表中的位置。 唯一可用选项是“查看”阶段的属性。  

- 应用程序分阶段部署始终为只读。  



## <a name="next-steps"></a>后续步骤

管理和监视分阶段部署：
- [应用程序](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [软件更新](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [任务序列](/sccm/osd/deploy-use/manage-monitor-phased-deployments)  

