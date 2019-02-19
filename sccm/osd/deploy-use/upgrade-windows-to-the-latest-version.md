---
title: 升级到 Windows 10
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 将操作系统从 Windows 7 或更高版本升级到 Windows 10。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c118c50eccf7fdb443a54f630d2d5698836d44f2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135494"
---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 将 Windows 升级到最新版本

适用范围：System Center Configuration Manager (Current Branch)

本文介绍在 Configuration Manager 中升级计算机操作系统的步骤。 你可以在不同的部署方法（如独立媒体或软件中心）中进行选择。 “就地升级”方案具有以下特点：  

-   升级当前运行以下系统版本的计算机的操作系统：
    - Windows 7、Windows 8 或 Windows 8.1。 你还可以执行 Windows 10 内部版本的升级。 例如可以将 Windows 10 版本 1607 升级到版本为 1709 的 Windows 10。  
    
    - Windows Server 2012。 还可以执行 Windows Server 2016 内部版本的升级。 有关支持的升级路径的详细信息，请参阅[支持的升级路径](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016)。    

-   保留计算机上的应用程序、设置和用户数据。  

-   没有 Windows ADK 等外部依赖关系。  

-   比传统操作系统部署更快、更具弹性。  


> [!Note]  
> 从 1802 版开始，Windows 10 就地升级任务序列支持部署到通过[云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway)托管的基于 Internet 的客户端。 此功能可让远程用户更轻松地升级到 Windows 10，无需连接 Intranet。 有关详细信息，请参阅[通过 CMG 部署 Windows 10 就地升级](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg)。 <!-- 1357149 -->



##  <a name="BKMK_Plan"></a> 计划  

### <a name="task-sequence-requirements-and-limitations"></a>任务序列要求和限制

查看使用任务序列升级操作系统时的要求和限制，以确保其满足你的需要：  

- 仅添加与操作系统升级的核心任务相关的任务序列步骤。 这些步骤主要包括安装包、应用程序或更新。 还会用到用于运行命令行、PowerShell 或设置动态变量的步骤。  

- 在部署升级任务序列前查看安装在计算机中的驱动程序和应用程序以确保它们与 Windows 10 兼容。  

- 以下任务与就地升级不兼容。 它们需要使用传统的操作系统部署：  

  - 更改计算机域成员身份或更新本地管理员组。  

  - 在计算机上实现基础更改，例如： 
    - 更改磁盘分区
    - 将系统体系结构从 x86 改为 x64
    - 实现 UEFI。 （有关可选操作的更多信息，请参阅[在就地升级过程中从 BIOS 转换到 UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)。）
    - 修改基本操作系统语言  

  - 你有自定义要求，包括使用自定义基本映像、使用第三方磁盘加密或要求 WinPE 脱机操作。  

### <a name="infrastructure-requirements"></a>基础结构要求  

该升级方案的唯一先决条件是具备可用的分发点。 分发操作系统升级包和任务序列中包含的任何其他包。 有关详细信息，请参阅[安装或修改分发点](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)。



##  <a name="BKMK_Configure"></a> 配置  

### <a name="prepare-the-os-upgrade-package"></a>准备 OS 升级包  

  Windows 10 升级包包含在目标计算机上升级操作系统所必需的源文件。 此升级包的版本、体系结构和语言必须与将升级的客户端的相同。 有关详细信息，请参阅[管理操作系统升级包](../get-started/manage-operating-system-upgrade-packages.md)。  


### <a name="create-a-task-sequence-to-upgrade-the-os"></a>创建用于升级操作系统的任务序列  

  使用[创建用于升级操作系统的任务序列](create-a-task-sequence-to-upgrade-an-operating-system.md)中的步骤自动升级操作系统。  

   > [!NOTE]  
   > 通常使用[创建用于升级操作系统的任务序列](create-a-task-sequence-to-upgrade-an-operating-system.md)中的步骤来创建任务序列，将操作系统升级到 Windows 10。 任务序列包括升级操作系统步骤以及用于处理端到端升级过程的其他建议步骤和组。 但是，可以创建自定义任务序列并添加 [升级操作系统](../understand/task-sequence-steps.md#BKMK_UpgradeOS)任务序列步骤以升级操作系统。 这是将操作系统升级到 Windows 10 所需的唯一步骤。 如果选择此方法，还要在升级操作系统步骤后添加[重启计算机](../understand/task-sequence-steps.md#BKMK_RestartComputer)步骤来完成升级。 请务必使用“当前安装的默认操作系统”设置，将计算机重启到已安装的操作系统而不是 Windows PE。  



##  <a name="BKMK_Deploy"></a> 部署  

使用下列部署方法之一部署操作系统：  

  -   [使用软件中心通过网络部署 Windows](use-software-center-to-deploy-windows-over-the-network.md)  

  -   [使用独立媒体部署 Windows，而不使用网络](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

      > [!IMPORTANT]  
      > 使用独立媒体时，必须在任务序列中包括启动映像，以供“任务序列媒体向导”使用。




## <a name="monitor"></a>监视器  

若要监视任务序列部署以升级操作系统，请参阅[监视操作系统部署](monitor-operating-system-deployments.md)。  
