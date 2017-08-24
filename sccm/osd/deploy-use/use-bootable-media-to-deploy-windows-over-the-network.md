---
title: "使用可启动媒体通过网络部署 Windows | Microsoft Docs"
description: "使用 System Center Configuration Manager 中的可启动媒体在启动目标计算机时部署操作系统。"
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: "5"
author: mattbriggs
ms.author: mattbriggs
manager: angrobe
ms.openlocfilehash: 9b20e5e2a66d92038033e816e6fc701581c48a7f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>使用可启动媒体与 System Center Configuration Manager 一起通过网络部署 Windows

*适用范围：System Center Configuration Manager (Current Branch)*

可以在使用可启动媒体部署启动目标计算机时部署操作系统。 媒体包含指向任务序列的指针、操作系统映像和来自网络的其他所需内容。 当目标计算机启动时，计算机会检索到指针所引用的项。 使用没有内容的可启动媒体可以更新目标，无需在媒体中进行替换。

通过在以下操作系统部署方案中使用多播，可以通过网络部署操作系统：

-   [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)  

-   [替换现有计算机和传输设置](replace-an-existing-computer-and-transfer-settings.md)  

完成其中一个操作系统部署方案中的步骤，然后运行以下部分来使用可启动媒体部署操作系统。  

## <a name="configure-deployment-settings"></a>配置部署设置  
当你使用可启动媒体来启动操作系统部署过程时，配置该部署才能使操作系统对媒体可用。 可以在“部署软件向导”的“部署设置”页或部署属性的“部署设置”选项卡上设置这一选项。 对于“可用于以下项目”  设置，请配置下述内容之一：

-   Configuration Manager 客户端、媒体和 PXE

-   仅媒体和 PXE

-   仅媒体和 PXE（隐藏）

## <a name="create-the-bootable-media"></a>创建可启动媒体
你可以指定可启动媒体是 U 盘还是 CD/DVD 设备。 启动媒体的计算机必须支持选为可启动驱动器的选项。 有关详细信息，请参阅[创建可启动媒体](create-bootable-media.md)。  

##  <a name="BKMK_Deploy"></a> 从可启动媒体安装操作系统  
在计算机的可启动驱动器中插入可启动媒体，然后再启动它以安装操作系统。
