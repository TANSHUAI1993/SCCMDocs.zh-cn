---
title: "为工厂中的 OEM 或本地 depot 创建映像 | Microsoft Docs"
description: "将操作系统部署到未完全预配的计算机时，可使用预留媒体部署减少网络流量。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
caps.latest.revision: "8"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 07aba04fb1b845e389a5f75b115d536136c1569c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 为工厂中的 OEM 或本地 depot 创建映像

*适用范围：System Center Configuration Manager (Current Branch)*

通过 System Center Configuration Manager 中的预留媒体部署，可将操作系统部署到未完全预配的计算机。 预留媒体是 Windows 映像格式 (WIM) 文件，可以由制造商 (OEM) 安装在裸机计算机上，也可以安装在未连接到 Configuration Manager 环境的企业暂存中心。 之后在 Configuration Manager 环境中，使用媒体提供的启动映像启动计算机，会在预留媒体上运行哈希检查以确保其有效性，然后计算机将连接到站点管理点以执行完成下载过程可用的任务序列。


此部署方法可以减少网络流量，因为启动映像和操作系统映像包已在目标计算机上。 你可以指定要包含在预留媒体中的应用程序、包和驱动程序包。 在计算机上安装操作系统后，首先检查应用程序、包或驱动程序包的本地任务序列缓存，如果找不到内容或内容已被修改，则从在预留媒体中配置的分发点下载内容，然后进行安装。  

 可在以下操作系统部署方案中使用预留媒体：  

-   [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)  

-   [替换现有计算机和传输设置](replace-an-existing-computer-and-transfer-settings.md)  

 完成其中一个操作系统部署方案中的步骤，然后使用以下部分来准备并创建预留媒体。  

## <a name="configure-deployment-settings"></a>配置部署设置  
 当你使用预留媒体来启动操作系统部署过程时，必须配置该部署才能使操作系统对媒体可用。 可以在“部署软件向导”的“部署设置”  页面或部署属性的“部署设置”  选项卡上配置这一选项。  对于“可用于以下项目”  设置，请配置下述内容之一：  

-   **Configuration Manager 客户端、媒体和 PXE**  

-   **仅媒体和 PXE**  

-   **仅媒体和 PXE（隐藏）**  

## <a name="create-the-prestaged-media"></a>创建预留媒体  
 创建要发送到的 OEM 或本地 depot 的预留媒体文件。 有关详细信息，请参阅 [Create prestaged media with System Center Configuration Manager](create-prestaged-media.md)。  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>将预留媒体文件发送到 OEM 或本地 depot  
 将该媒体发送到 OEM 或本地 depot 以预留计算机。 预留媒体文件应用于计算机上已格式化的硬盘。  

## <a name="start-the-computer-to-install-the-operating-system"></a>启动计算机以安装操作系统  
 预留媒体文件应用于计算机。 第一次启动计算机时，将启动操作系统安装过程。  
