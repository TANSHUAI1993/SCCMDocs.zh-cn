---
title: "将 Windows 升级到最新版本 | Microsoft Docs"
description: "了解如何使用 Configuration Manager 将操作系统从 Windows 7 或更高版本升级到 Windows 10。"
ms.custom: na
ms.date: 02/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: "13"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 026d61113a918e43ac4395ef092b1931f33f16d3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 将 Windows 升级到最新版本

*适用范围：System Center Configuration Manager (Current Branch)*

本主题提供了在 System Center Configuration Manager 中将目标计算机的操作系统从 Windows 7 或更高版本升级到 Windows 10，或从 Windows Server 2012 升级到 Windows Server 2016 的步骤。 你可以在不同的部署方法（如独立媒体或软件中心）中进行选择。 就地升级方案：  

-   升级当前运行以下系统版本的计算机的操作系统：
    - Windows 7、Windows 8 或 Windows 8.1。 你还可以执行 Windows 10 内部版本的升级。 例如，你可以将 Windows 10 RTM 升级到版本为 1511 的 Windows 10。  
    - Windows Server 2012。 还可以执行 Windows Server 2016 内部版本的升级。 有关支持的升级路径的详细信息，请参阅[支持的升级路径](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016)。    

-   保留计算机上的应用程序、设置和用户数据。  

-   没有 Windows ADK 等外部依赖关系。  

-   比传统操作系统部署更快、更具弹性。  

 根据以下部分，使用任务序列通过网络部署操作系统。  

##  <a name="BKMK_Plan"></a> 计划  

-   **查看用于升级操作系统的任务序列的限制。**  

     查看使用任务序列升级操作系统时的要求和限制以确保其满足你的需要：  

    -   在安装映像后，应仅添加与部署操作系统和配置计算机核心任务相关的任务序列步骤。 这包括安装包、应用程序或更新的步骤，以及运行命令行、PowerShell 或设置动态变量的步骤。  

    -   在部署升级任务序列前查看安装在计算机中的驱动程序和应用程序以确保它们与 Windows 10 兼容。  

    -   以下任务与就地升级不兼容，需要使用传统操作系统部署：  

        -   更改计算机域成员身份或更新本地管理员。  

        -   在计算机上实现基础更改，包括磁盘分区、将 x86 体系结构更改为 x64 体系结构、实现 UEFI 或修改操作系统基本语言。  

        -   拥有自定义要求（包括使用自定义基本映像、使用第三方<sup></sup> 磁盘加密），或要求 WinPE 脱机操作。  

-   **规划和实现基础结构要求**  

     此升级方案的唯一先决条件是具有可用于操作系统升级包和任务序列中包含的其他任何包的分发点。 有关详细信息，请参阅[安装或修改分发点](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)。

##  <a name="BKMK_Configure"></a> 配置  

1.  **准备操作系统升级包**  

     Windows 10 升级包包含在目标计算机上升级操作系统所必需的源文件。 此升级包的版本、体系结构和语言必须与将升级的客户端的相同。  有关详细信息，请参阅[管理操作系统升级包](../get-started/manage-operating-system-upgrade-packages.md)。  

2.  **创建用于升级操作系统的任务序列**  

     使用[创建用于升级操作系统的任务序列](create-a-task-sequence-to-upgrade-an-operating-system.md)中的步骤自动升级操作系统。  

    > [!IMPORTANT]
    > 使用独立媒体时，必须在任务序列中包括启动映像，以供“任务序列媒体向导”使用。

    > [!NOTE]  
    > 通常，将使用[创建用于升级操作系统的任务序列](create-a-task-sequence-to-upgrade-an-operating-system.md)中的步骤来创建任务序列，将操作系统升级到 Windows 10。 任务序列包括升级操作系统步骤以及用于处理端到端升级过程的其他建议步骤和组。 但是，可以创建自定义任务序列并添加 [升级操作系统](../understand/task-sequence-steps.md#BKMK_UpgradeOS)任务序列步骤以升级操作系统。 这是将操作系统升级到 Windows 10 所需的唯一步骤。 如果选择此方法，还要在升级操作系统步骤后添加[重启计算机](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)步骤来完成升级。 请务必使用“当前安装的默认操作系统”设置，将计算机重启到已安装的操作系统而不是 Windows PE。  

##  <a name="BKMK_Deploy"></a> 部署  

-   使用下列部署方法之一部署操作系统：  

    -   [使用软件中心通过网络部署 Windows](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [使用独立媒体部署 Windows，而不使用网络](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## <a name="monitor"></a>监视器  

-   **监视任务序列部署**  

     若要监视任务序列部署以升级操作系统，请参阅[监视操作系统部署](monitor-operating-system-deployments.md)。  
