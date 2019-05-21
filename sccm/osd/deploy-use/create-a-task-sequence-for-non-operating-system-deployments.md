---
title: 为非操作系统部署创建任务序列
titleSuffix: Configuration Manager
description: 创建不用于部署 OS 的任务序列，例如分发软件或自动执行任务
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17ba0f146a80928b1eaae6334e6418a5e08b1114
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083063"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>创建非 OS 部署的任务序列

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的任务序列用于自动在环境中执行不同类型的任务。 这些任务经过测试主要设计用于部署操作系统。 Configuration Manager 具有许多其他功能，这些功能应作为用于以下场景的主要技术：

- [应用程序安装](/sccm/apps/understand/introduction-to-application-management)
- [软件更新安装](/sccm/sum/understand/software-updates-introduction)
- [设置配置](/sccm/compliance/understand/ensure-device-compliance)

另外，还可以考虑使用诸如 [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) 和 [Service Management Automation](https://docs.microsoft.com/system-center/sma/) 等其他 Microsoft System Center 自动化技术。  

任务序列的强大功能在于其灵活性以及使用方式。 它们可以配置客户端设置、分发软件、更新驱动程序、编辑用户状态以及执行与 OS 部署无关的其他任务。 你可以创建自定义任务序列以添加任意数量的任务。 Configuration Manager 中支持使用非 OS 部署的自定义任务序列。 但是，如果任务序列导致不必要或不一致的结果，请设法简化操作：

- 使用更简单的步骤
- 将操作划分为多个任务序列
- 采用分阶段方法创建和测试任务序列

支持将以下步骤用于非 OS 部署自定义任务序列：  

- [检查准备情况](/sccm/osd/understand/task-sequence-steps#BKMK_CheckReadiness)  

- [连接到网络文件夹](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  

- [下载包内容](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent)  

- [安装应用程序](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication)  

- [安装包](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)  

- [安装软件更新](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)  

- [重启计算机](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer)  

- [运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

- [运行 PowerShell 脚本](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript)  

- [运行任务序列](/sccm/osd/understand/task-sequence-steps#child-task-sequence)  

- [设置动态变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables)  

- [设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)  
