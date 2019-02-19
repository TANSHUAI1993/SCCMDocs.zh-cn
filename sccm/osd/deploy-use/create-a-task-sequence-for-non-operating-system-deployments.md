---
title: 为非操作系统部署创建任务序列
titleSuffix: Configuration Manager
description: 创建与部署操作系统不相关的任务序列，如软件分发、更新驱动程序和编辑用户状态等。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c8ef75ea9b0948a932c1b146d0f4fe7051017759
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140307"
---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建用于非操作系统部署的任务序列

适用范围：System Center Configuration Manager (Current Branch)

System Center Configuration Manager 中的任务序列用于自动在环境中执行各种任务。 这些任务经过测试主要设计用于部署操作系统。  Configuration Manager具有许多其他功能，这些功能应是用于以下这些方案的主要技术：[应用程序安装](../../apps/understand/introduction-to-application-management.md)[软件更新安装](../../sum/understand/software-updates-introduction.md)、[设置配置](../../compliance/understand/ensure-device-compliance.md)或自定义自动化。 此外，你也可以考虑诸如 [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) 和 [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) 等其他 Microsoft System Center 自动化技术。  

任务序列的强大功能在于其灵活性以及如何使用它们配置客户端设置、分发软件、更新驱动程序、编辑用户状态并执行独立于操作系统部署的其他任务。 你可以创建自定义任务序列以添加任意数量的任务。 Configuration Manager 中支持使用非操作系统部署的自定义任务序列。 但是，如果任务序列导致不需要或不一致的结果，请设法简化操作。 通过使用简化的步骤、在多个任务序列之间划分操作，或通过采用阶段方法创建和测试任务序列，可完成此操作。

 支持将以下步骤用于非操作系统部署自定义任务序列：  

-   [检查准备情况](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [连接到网络文件夹](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [下载包内容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [安装应用程序](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [安装包](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [安装软件更新](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [重启计算机](../understand/task-sequence-steps.md#BKMK_RestartComputer)   

-   [运行命令行](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [运行 PowerShell 脚本](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [设置动态变量](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [设置任务序列变量](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>后续步骤 
[部署任务序列](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
