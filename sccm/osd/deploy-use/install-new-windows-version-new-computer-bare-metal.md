---
title: "在新计算机上安装 Windows - Configuration Manager | Microsoft Docs"
description: "通过 PXE、OEM 或独立介质在新计算机（裸机）上使用 Configuration Manager 安装操作系统。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
caps.latest.revision: "8"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 584dad7d8b05a2da9f7a66b73028ae99ff1a594f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 在新计算机（裸机）上安装新版本的 Windows

*适用范围：System Center Configuration Manager (Current Branch)*

本主题提供了在 System Center Configuration Manager 中在新计算机上安装操作系统的常规步骤。 对于此方案，可以从许多不同的部署方法中选择，如 PXE、OEM、或独立媒体。 如果不确定这是否是正确的操作系统部署方案，请参阅[部署企业版操作系统的方案](scenarios-to-deploy-enterprise-operating-systems.md)。  

采用以下部分内容，使用新版本的 Windows 来刷新现有计算机。  

##  <a name="BKMK_Plan"></a> 计划  

-   **规划和实现基础结构要求**  

     在你可以部署操作系统前，有几个必须实施到位的基础结构要求，例如 Windows ADK、Windows 部署服务 (WDS) 以及支持的硬盘配置等。有关详细信息，请参阅[操作系统部署的基础架构要求](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)。

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

##  <a name="BKMK_Deploy"></a> 部署  

-   使用下列部署方法之一部署操作系统：  

    -   [使用 PXE 通过网络部署 Windows](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [使用多播通过网络部署 Windows](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [为工厂中的 OEM 或本地 depot 创建映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [使用独立媒体部署 Windows，而不使用网络](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [使用可启动媒体通过网络部署 Windows](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>监视器  

-   **监视任务序列部署**  

     若要监视用于安装操作系统的任务序列部署，请参阅[监视操作系统部署](monitor-operating-system-deployments.md)。  
