---
title: "操作系统部署简介 | Microsoft Docs"
description: "请在 Configuration Manager 环境中部署操作系统之前，了解一些概念。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2baa6b7dbd66ab41bc9b67e8f43c313be233153c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-operating-system-deployment-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的操作系统部署简介

*适用范围：System Center Configuration Manager (Current Branch)*

可以通过不同方式使用 Configuration Manager 部署操作系统。 通过本节中的信息了解如何部署操作系统和自动执行任务。 

##  <a name="BKMK_OSDeploymentProcess"></a> 操作系统部署过程  
 Configuration Manager 提供可用于部署操作系统的一些方法。 无论使用哪种部署方法，都必须执行一些操作：  

-   标识要开始启动映像或安装操作系统映像（必须部署的）所必需的 Windows 设备驱动程序。  

-   确定想要用来启动目标计算机的启动映像。  

-   使用任务序列捕获将要部署的操作系统的映像。 或者，你可以使用默认的操作系统映像。  

-   将启动映像、操作系统映像包以及任何相关内容分发至分发点。  

-   创建任务序列，该序列带有部署启动映像和操作系统映像的步骤。  

-   将任务序列部署到计算机集合。  

-   监视部署。  

##  <a name="BKMK_OSDScenarios"></a> 操作系统部署方案  
 Configuration Manager 中有许多可供选择的操作系统部署方案，具体取决于你的环境和操作系统的安装目的。  例如，你可以使用新版本的 Windows 对现有计算机进行分区和格式化，或将 Windows 升级到最新版本。 为帮助确定所需的部署方法，请查看[部署企业操作系统的方案](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)。  你可以从以下操作系统部署方案中进行选择：  

-   [将 Windows 升级到最新版本](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [使用新版的 Windows 刷新现有的计算机](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [在新计算机（裸机）上安装新版的 Windows](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [替换现有计算机和传输设置](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_OSDMethods"></a> 用于部署操作系统的方法  
 可以使用一些方法将操作系统部署到 Configuration Manager 客户端计算机。  

-   **PXE 启动部署**：PXE 启动部署允许客户端计算机通过网络请求部署。 在此部署方法中，操作系统映像包和 Windows PE 启动映像会发送到配置为接受 PXE 启动请求的分发点。 有关详细信息，请参阅[使用 PXE 与 System Center Configuration Manager 一起通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

-   **使操作系统在软件中心中可用**：可以部署操作系统，并使其在软件中心中可用。 Configuration Manager 客户端可以从软件中心启动操作系统安装。 有关详细信息，请参阅[替换现有计算机和传输设置](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)。  

-   **多播部署**：多播部署通过将数据并行发送到多个客户端，而不是通过单独连接向每个客户端发送数据副本，从而节省网络带宽。 在此部署方法中，操作系统映像包将发送到分发点。 这反过来会在客户端计算机请求部署时部署映像。 有关详细信息，请参阅[使用多播通过网络部署 Windows](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。  

-   **可启动媒体部署**：可启动媒体部署允许在目标计算机启动时部署操作系统。 在目标计算机启动时，它从网络中检索任务序列、操作系统映像包和任何其他必需的内容。 由于媒体上未包括该内容，因此，你无需重新创建媒体就能更新内容。 有关详细信息，请参阅[创建可启动媒体](../deploy-use/create-bootable-media.md)。  

-   **独立媒体部署**：独立媒体部署允许在下列情况下部署操作系统：  

    -   在通过网络复制操作系统映像包或其他大型包并不实际可行的环境中。  

    -   在无网络连接或具有低带宽网络连接的环境中。  

     有关详细信息，请参阅[创建独立媒体](../deploy-use/create-stand-alone-media.md)。  

-   **预留媒体部署**：预留媒体部署允许将操作系统部署到未完全设置的计算机。 预留媒体是 Windows 映像格式 (WIM) 文件，可以由制造商安装在裸机上，也可以安装在未连接到 Configuration Manager 环境的企业暂存中心。  

     随后在 Configuration Manager 环境中，计算机使用媒体提供的启动映像启动，然后连接到站点管理点以执行完成下载过程的可用任务序列。 此部署方法可以减少网络流量，因为启动映像和操作系统映像包已在目标计算机上。 你可以指定要包含在预留媒体中的应用程序、包和驱动程序包。 有关详细信息，请参阅[创建预留媒体](../deploy-use/create-prestaged-media.md)。  

##  <a name="BKMK_BootImages"></a> 启动映像  
 Configuration Manager 中的启动映像是在操作系统部署过程中使用的 Windows PE (WinPE) 映像。 启动映像用于在 WinPE 中启动计算机，它是用于准备在目标计算机上安装 Windows 的有限组件和服务的最精简操作系统。 Configuration Manager 提供两个启动映像：一个用于支持 x86 平台，另一个用于支持 x64 平台。 这些视为默认启动映像。 创建并添加到 Configuration Manager 的启动映像被视为自定义映像。 更新 Configuration Manager 时，会自动替换默认启动映像。 有关启动映像的详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

##  <a name="BKMK_OSImages"></a> 操作系统映像  
 Configuration Manager 中的操作系统映像以 Windows 映像 (WIM) 文件格式存储，代表在计算机上成功安装和配置操作系统所需的引用文件和文件夹的压缩集合。 对于所有操作系统部署方案，必须选择操作系统映像。 你可以使用默认操作系统映像或从你配置的引用计算机生成操作系统映像。 有关详细信息，请参阅[管理操作系统映像](../get-started/manage-operating-system-images.md)。  

##  <a name="BKMK_OSUpgradePackages"></a> 操作系统升级包  
 操作系统升级包用于升级操作系统，并且是安装程序启动的操作系统部署。 从 DVD 或已安装的 ISO 文件将操作系统升级包导入 Configuration Manager。 有关详细信息，请参阅[管理操作系统升级包](../get-started/manage-operating-system-upgrade-packages.md)。  

##  <a name="BKMK_OSDMedia"></a> 用于部署操作系统的媒体  
 你可以创建若干种可用于部署操作系统的媒体。 这包括捕获用于捕获操作系统映像的媒体，以及捕获用于部署操作系统的独立、预留和可启动媒体。 通过使用媒体，可以在没有网络连接或者使用低带宽连接连接到 Configuration Manager 站点的计算机上部署操作系统。 有关如何使用媒体的详细信息，请参阅[创建任务序列媒体](../deploy-use/create-task-sequence-media.md)。  

##  <a name="BKMK_DeviceDrivers"></a> 设备驱动程序  
 你可以在目标计算机上安装设备驱动程序，而不将它们包含在正在部署的操作系统映像中。 Configuration Manager 提供包含对导入 Configuration Manager 的所有设备驱动程序的引用的驱动程序目录。 此驱动程序目录位于“软件库”  工作区中并且包含以下两个节点：“驱动程序”  和“驱动程序包” 。 “驱动程序”  节点列出了已导入到驱动程序目录的所有驱动程序。 你可以使用此节点发现关于每个导入的驱动程序的详细信息，更改驱动程序所属的驱动程序包或启动映像，启用或禁用驱动程序，以及执行其他操作。 有关详细信息，请参阅[管理驱动程序](../get-started/manage-drivers.md)。  

##  <a name="BKMK_OSDUserState"></a> 保存并还原用户状态  
 部署操作系统时，你可以保存目标计算机中的用户状态，部署操作系统，然后在部署操作系统之后还原用户状态。 此过程通常在 Configuration Manager 客户端计算机上安装操作系统时使用。  

 用户状态信息是使用任务序列捕获和还原的。 捕获用户状态信息后，可以使用下列方法之一存储信息：  

-   你可以通过配置状态迁移点以远程存储用户状态数据。 捕获任务序列将数据发送到状态迁移点。 然后，在部署操作系统之后，还原任务序列检索数据并在目标计算机上还原用户状态。  

-   你可以以本地方式将用户状态数据存储到特定位置。 在此方案中，捕获任务序列将用户数据复制到目标计算机上的特定位置。 然后，在部署操作系统之后，还原任务序列从该位置检索用户数据。  

-   你可以指定可用于将用户数据还原到其原始位置的硬链接。 在此方案中，删除旧操作系统时，用户状态数据会保留在驱动器上。 然后，在部署操作系统之后，还原任务序列使用硬链接将用户状态数据还原到其原始位置。  

 有关详细信息，请参阅[管理用户状态](../get-started/manage-user-state.md)。  

##  <a name="BKMK_UnknownComputer"></a> 部署到未知计算机  
 可以将操作系统部署到不由 Configuration Manager 管理的计算机。 Configuration Manager 数据库中没有这些计算机的记录。 这些计算机称为未知计算机。 未知计算机包括下列各项：  

-   未安装 Configuration Manager 客户端的计算机  

-   未导入到 Configuration Manager 中的计算机  

-   未被 Configuration Manager 发现的计算机  

 有关详细信息，请参阅[准备未知计算机部署](../get-started/prepare-for-unknown-computer-deployments.md)。  

##  <a name="BKMK_UDA"></a> 将用户与计算机关联  
 部署操作系统时，可以将用户与目标计算机关联，以支持用户设备关联操作。 将用户与目标计算机关联时，管理用户稍后可以对与该用户关联的任何计算机执行操作，如将应用程序部署到特定用户的计算机。 但是，在部署操作系统时，你无法将操作系统部署到特定用户的计算机。 有关详细信息，请参阅[将用户与目标计算机相关联](../get-started/associate-users-with-a-destination-computer.md)。  

##  <a name="BKMK_TaskSequences"></a> 使用任务序列自动执行步骤  
 可创建任务序列在 Configuration Manager 环境中执行各种任务。 序列的各个步骤中定义了任务序列的操作。 运行任务序列时，系统在命令行级别执行每个步骤的操作，无需用户干预。 可以针对以下情况使用任务序列：  

-   [创建用于安装操作系统的任务序列](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [创建用于非操作系统部署的任务序列](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [创建用于捕获操作系统的任务序列](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [创建用于捕获和还原用户状态的任务序列](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [创建自定义任务序列](../deploy-use/create-a-custom-task-sequence.md)  
