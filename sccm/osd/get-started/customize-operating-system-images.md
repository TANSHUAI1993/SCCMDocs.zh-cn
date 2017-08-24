---
title: "自定义操作系统映像 - Configuration Manager | Microsoft Docs"
description: "使用捕获和生成任务序列、手动配置或这两者的组合来自定义操作系统映像。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 485cb3ca4988f983c1ec71b6c8daf136571bf0ea
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="customize-operating-system-images-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 自定义操作系统映像

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的操作系统映像是 WIM 文件，并且表示在计算机上成功安装和配置操作系统所需的参考文件和文件夹的压缩集合。 自定义操作系统映像是通过一台引用计算机构建和捕获的。在该计算机上，你配置了所有必需的操作系统文件、支持文件、软件更新、工具和其他软件应用。 由你决定将引用计算机手动配置到何种程度。 你可以通过使用构建和捕获任务序列完全自动完成配置引用计算机的过程，可以手动配置引用计算机的某些方面然后使用任务序列自动完成其余配置，或者可以在不使用任务序列的情况下手动配置引用计算机。 使用以下部分自定义操作系统。

##  <a name="BKMK_PrepareReferenceComputer"></a>准备引用计算机  
 在你使用从引用计算机捕获操作系统映像之前，有一些事项需要注意。  

###  <a name="BKMK_RefComputerDecide"></a>在自动或手动配置之间作出决定  
 下面概述了引用计算机的自动和手动配置的优点和缺点。  

#### <a name="automated-configuration"></a>自动配置  
 **优点**  

-   配置可完全无人参与，因而不需要管理员或用户存在。  

-   你可以重用任务序列来信心十足地重复配置其他引用计算机。  

-   你可以修改任务序列来适用引用计算机中的差异，而不必重新创建整个任务序列。  

 **缺点**  

-   创建任务序列的初始操作可能要花费很长时间来创建和测试。  

-   如果引用计算机要求发生很大变化，则可能要花费很长时间来重建和重新测试任务序列。  

#### <a name="manual-configuration"></a>手动配置  
 **优点**  

-   你不必创建任务序列或花时间来对任务序列进行测试和故障诊断。  

-   你可以直接从 CD 中安装，而不必将所有软件包（包括 Windows 本身）放在 Configuration Manager 包中。  

 **缺点**  

-   引用计算机配置的准确性取决于配置计算机的管理员或用户。  

-   你仍然必须验证和测试已正确配置的引用计算机。  

-   你无法重用配置方法。  

-   需要有人员主动参与整个过程。  

###  <a name="BKMK_RefComputerConsiderations"></a>引用计算机的注意事项  
 下面列出了在配置引用计算机时要考虑的基本项目。  

-   **要部署的操作系统**  

     必须使用你打算部署到目标计算机的操作系统安装引用计算机。 有关可以部署的操作系统的详细信息，请参阅[操作系统部署的基础结构要求](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

-   **适当的 Service Pack**  

     必须使用你打算部署到目标计算机的操作系统安装引用计算机。  

-   **适当的软件更新**  

     安装要包括在从引用计算机中捕获的操作系统映像中的所有软件应用程序。 你也可以在将捕获的操作系统映像部署到目标计算机时安装软件应用程序。  

-   **工作组成员身份**  

     必须将引用计算机配置为工作组的成员。  

-   **Sysprep**  

     系统准备 (Sysprep) 工具是你可随其他部署工具一起使用以将 Windows 操作系统安装到新硬件上的一种技术。 Sysprep 通过将计算机配置为在计算机重启时创建新的计算机安全标识符 (SID) 来准备计算机以进行磁盘映像或交付给客户。 此外，Sysprep 还会清理不得复制到目标计算机的特定于用户和计算机的设置及数据。  

     你可以通过运行下列命令来对引用计算机手动执行 Sysprep 操作：  

     `Sysprep /quiet /generalize /reboot`  

     /generalize 选项指示 Sysprep 从 Windows 安装中删除特定于系统的数据。 特定于系统的信息包括事件日志、唯一安全 ID (SID) 和其他唯一性信息。 删除唯一系统信息后，计算机将重启。  

     你可以使用“准备 Windows 以便捕获” [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) 任务序列步骤或捕获媒体来自动完成 Sysprep。  

    > [!IMPORTANT]  
    >  “准备 Windows 以便捕获” [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) 任务序列步骤会在 Sysprep 运行之前尝试将引用计算机上的本地管理员密码重置为空白值。 如果启用了本地安全策略“密码必须满足复杂性要求”  ，则此任务序列步骤将无法重置管理员密码。 在这种情况下，请在运行任务序列之前禁用此策略。  

     有关 Sysprep 的详细信息，请参阅 [System Preparation (Sysprep) Technical Reference（系统准备 (Sysprep) 概述技术参考）](http://go.microsoft.com/fwlink/?LinkId=280286)。  

-   **迁移安装方案所需的适当工具和脚本**  

     迁移安装方案所需的适当工具和脚本  

-   **适当桌面自定义，如墙纸、品牌和默认用户配置文件**  

     你可以使用要在从引用计算机中捕获操作系统映像时包括的桌面自定义属性来配置引用计算机。 桌面属性包括墙纸、组织外观方案和标准默认用户配置文件。  

##  <a name="BKMK_ManuallyBuildReference"></a>手动构建引用计算机  
 使用以下过程来手动构建引用计算机。  

> [!NOTE]  
>  当手动构建引用计算机时，你可以通过使用捕获媒体来捕获操作系统映像。 有关详细信息，请参阅[创建捕获媒体](../deploy-use/create-capture-media.md)。  

#### <a name="to-manually-build-the-reference-computer"></a>若要手动构建引用计算机  

1.  确定要用作引用计算机的计算机。  

2.  配置具有适当操作系统以及创建要部署的操作系统映像所需的任何其他软件的引用计算机。  

    > [!WARNING]  
    >  至少要安装适当的操作系统和服务包、支持驱动程序、以及必需的软件更新。  

3.  将引用计算机配置为工作组的成员。  

4.  重置引用计算机上的本地管理员密码以使密码值为空白。  

5.  通过使用以下命令来运行 Sysprep：  **sysprep /quiet /generalize /reboot**。 /generalize 选项指示 Sysprep 从 Windows 安装中删除特定于系统的数据。 特定于系统的信息包括事件日志、唯一安全 ID (SID) 和其他唯一性信息。 删除唯一系统信息后，计算机将重启。  

 引用计算机准备就绪之后，使用任务序列从引用计算机捕获操作系统映像。  有关详细步骤，请参阅 [从现有引用计算机中捕获操作系统映像](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer)。  

##  <a name="BKMK_UseTSToBuildReference"></a>使用任务序列构建引用计算机  
 你可以通过使用任务序列自动执行创建引用计算机的过程以部署操作系统、驱动程序、应用程序等。  使用以下步骤构建引用计算机，然后从引用计算机捕获操作系统映像。  

-   使用任务序列构建和捕获引用计算机中的操作系统映像。  有关详细步骤，请参阅 [使用任务序列来构建和捕获引用计算机](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS)。  
