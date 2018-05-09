---
title: 针对任务序列创建分阶段部署
titleSuffix: Configuration Manager
description: 针对任务序列创建分阶段部署
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2bda41cfd01e5ef90771350e650f68a27c3af6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="create-phased-deployments-for-a-task-sequence-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 针对任务序列创建分阶段部署

*适用范围：System Center Configuration Manager (Current Branch)*

分阶段部署可在多个集合中自动协调有序地推出任务序列。 创建分阶段部署时，既可以使用默认的两个阶段，也可以手动配置多个阶段。 任务序列的分阶段部署不支持 PXE 或介质安装。 

>[!NOTE]
> 分阶段部署是 Configuration Manager 1802 中引入的预发行功能。 <!--1356837-->

## <a name="security-scope-and-log-file-information"></a>安全作用域和日志文件信息

**安全作用域**：</br>
任何没有“全部”安全作用域的人员都无法查看由分阶段部署创建的部署。

**日志文件**： </br>
SMS_PhasedDeployment.log

## <a name="create-a-default-two-phased-deployment-for-a-task-sequence"></a>针对任务序列创建默认的两阶段部署

按照以下说明创建分阶段部署。 

1. 在“软件库”工作区中，展开“操作系统”，并选择“任务序列”。

2. 右键单击现有任务序列并选择“创建分阶段部署”。 

3. 在“常规”选项卡上，为分阶段部署提供名称、说明（可选），并选择“自动创建默认的二阶段部署”。 

4. 填充“第一个集合”和“第二个集合”字段。 选择“下一步”。

5. 在“设置”选项卡上，为每个计划设置选择一个选项，然后在完成后选择“下一步”。 
    - **第一阶段的成功标准。** 
        - **部署成功百分比**：指定成功完成部署的设备所占的百分比作为阶段成功标准。 
    - **在第一阶段成功后开始第二阶段部署的条件**（选择一个）：
        - **在某个延迟时间段(以天为单位)后自动开始此阶段**：选择在第一阶段成功后开始第二阶段之前等待的天数。 
        - **手动开始第二阶段部署**：在第一阶段成功后不自动开始第二阶段。 要求手动开始第二阶段。 
    - **确定目标设备后立即安装软件**（选择一个）：
        - **尽快**：确定目标设备后立即设置设备上的安装截止时间。
        - **截止时间(相对于确定目标设备的时间)**：将安装截止时间设置为确定目标设备后的特定天数。 

6. 在“阶段”选项卡上，单击第一阶段，然后单击“编辑”。  指定“用户体验”，例如，“用户通知”和“Windows Embedded 设备的写入筛选器处理”。 单击“应用” 。

7. 在“分发点”选项卡上指定该阶段的“分发点”设置。依次单击“应用”、“确定”。        

8. 在“阶段”选项卡上，编辑第二阶段的“用户体验”和“分发点”。 依次单击“应用”、“确定”。

9. 在“摘要”选项卡上确认你的选择，然后单击“下一步”继续运行向导。

>[!WARNING]
>分阶段部署不会通知你任务序列部署是否具有[高风险](/sccm/protect/understand/settings-to-manage-high-risk-deployments.md)。 


## <a name="suspend-and-resume-phases-or-move-to-the-next-phase"></a>暂停和恢复阶段或进入下一阶段
有时，你可能需要手动暂停分阶段部署、恢复暂停的分阶段部署或进入下一阶段。 

### <a name="move-to-the-next-phase"></a>进入下一阶段
如果选择“手动开始第二阶段部署”设置，你需要开始第二阶段。 按照以下说明进入第二阶段： 

1. 在 Configuration Manager 控制台中，选择“软件库”，展开“操作系统”，然后单击“任务序列”。
2. 突出显示任务序列。
3. 单击控制台底部附近的“分阶段部署”选项卡。 
4. 右键单击分阶段部署并选择“进入下一阶段”。
![暂停、恢复或进入下一阶段](media/Suspend-phased-deployment.PNG)

### <a name="suspend-or-resume-a-phased-deployment"></a>暂停或恢复分阶段部署
1. 在 Configuration Manager 控制台中，选择“软件库”，展开“操作系统”，然后单击“任务序列”。
2. 突出显示任务序列，然后单击控制台底部附近的“分阶段部署”选项卡。 
3. 选择分阶段部署，单击功能区中的“暂停”或“恢复”。

## <a name="next-steps"></a>后续步骤
[创建自定义任务序列](create-a-custom-task-sequence.md) </br>
[创建用于非操作系统部署的任务序列](create-a-task-sequence-for-non-operating-system-deployments.md)。 








