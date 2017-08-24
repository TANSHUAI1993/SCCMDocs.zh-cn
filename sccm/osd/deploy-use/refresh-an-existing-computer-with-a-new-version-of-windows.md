---
title: "使用新版 Windows 刷新现有计算机 | Microsoft Docs"
description: "可以使用 Configuration Manager 中的几种办法来分区和格式化（擦除）现有计算机和在计算机上安装新操作系统。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
caps.latest.revision: "7"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: b247cbb68ed63a8eb99715a248686d68a28c53e2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows-using-system-center-configuration-manager"></a>通过 System Center Configuration Manager，使用新版本的 Windows 刷新现有的计算机

*适用范围：System Center Configuration Manager (Current Branch)*

本主题提供 System Center Configuration Manager 中用于分区和格式化（擦除）现有计算机和在计算机上安装新操作系统的一般步骤。 对于此方案，可以在许多不同的部署方法中进行选择，如 PXE、可启动媒体或软件中心。 你还可以选择用以存储设置的状态迁移点，然后在安装后将这些设置还原到新的操作系统。 如果不确定这是否是正确的操作系统部署方案，请参阅[部署企业版操作系统的方案](scenarios-to-deploy-enterprise-operating-systems.md)。  

 采用以下部分内容，使用新版本的 Windows 来刷新现有计算机。  

##  <a name="BKMK_Plan"></a> 计划  

-   **规划和实现基础结构要求**  

     在你可以部署操作系统前，有几个必须实施到位的基础结构要求，例如 Windows ADK、用户状态迁移工具 (USMT)、Windows 部署服务 (WDS) 以及支持的硬盘配置等。有关详细信息，请参阅[操作系统部署的基础架构要求](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

-   **安装状态迁移点（仅在传输设置时需要）**  

     当你要从现有计算机捕获设置并将设置还原到新的操作系统时，必须安装状态迁移点。 有关详细信息，请参阅[状态迁移点](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)。  

##  <a name="BKMK_Configure"></a> 配置  

1.  **准备启动映像**  

     启动映像将启动 Windows PE 环境（具有有限组件和服务的最小操作系统）中的计算机，然后在该计算机上安装完整的 Windows 操作系统。   在部署操作系统时，必须选择要使用的启动映像并将其分发到分发点。 使用以下方法来准备启动映像：  

    -   若要了解有关启动映像的详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

    -   有关如何自定义启动映像的详细信息，请参阅[自定义启动映像](../get-started/customize-boot-images.md)。  

    -   将启动映像分发到分发点 有关详细信息，请参阅[分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)。  

2.  **准备操作系统映像**  

     操作系统映像包含在目标计算机上安装操作系统所必需的文件。 使用以下方法来准备操作系统映像：  

    -   若要了解有关如何创建操作系统映像的详细信息，请参阅[管理操作系统映像](../get-started/manage-operating-system-images.md)。  

    -   将操作系统映像分发到分发点。 有关详细信息，请参阅[分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)。  

3.  **创建任务序列以通过网络部署操作系统**  

     使用任务序列以通过网络自动安装操作系统 使用[创建用于安装操作系统的任务序列](create-a-task-sequence-to-install-an-operating-system.md)中的步骤来创建部署操作系统的任务序列。 可能会有有关任务序列的其他注意事项，具体取决于你所选择的部署方法。  

    > [!NOTE]  
    >  在此方案中，任务序列对计算机上的硬盘进行格式化和分区。 若要捕获用户设置，必须使用状态迁移点，并在“创建任务序列”向导的“状态迁移”  页面上选择“在状态迁移点上保存用户设置和文件”  。 如果在本地保存用户设置和文件，它们会在硬盘格式化时丢失并且 Configuration Manager 将无法还原设置。 有关详细信息，请参阅[管理用户状态](../get-started/manage-user-state.md)。  

##  <a name="BKMK_Deploy"></a> 部署  

-   使用下列部署方法之一部署操作系统：  

    -   [使用 PXE 通过网络部署 Windows](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [使用多播通过网络部署 Windows](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [为工厂中的 OEM 或本地 depot 创建映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [使用独立媒体部署 Windows，而不使用网络](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [使用可启动媒体通过网络部署 Windows](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [使用软件中心通过网络部署 Windows](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>监视器  

-   **监视任务序列部署**  

     若要监视用于安装操作系统的任务序列部署，请参阅[监视操作系统部署](monitor-operating-system-deployments.md)。  
