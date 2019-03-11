---
title: 准备进行 OS 部署
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中准备操作系统部署
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e303a7363e0641210cc7c6e436546d864fe0571
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838712"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>在 Configuration Manager 中准备 OS 部署

适用范围：System Center Configuration Manager (Current Branch)

必须在 Configuration Manager 中完成几件事情，才能部署操作系统。 请阅读以下文章以便准备 OS 部署：  

-   [管理启动映像](manage-boot-images.md)  

-   [管理 OS 映像](manage-operating-system-images.md)  

-   [管理 OS 升级包](manage-operating-system-upgrade-packages.md)  

-   [管理驱动程序](manage-drivers.md)  

-   [管理用户状态](manage-user-state.md)  

-   [准备未知计算机部署](prepare-for-unknown-computer-deployments.md)  

-   [将用户与目标计算机相关联](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>OS 映像大小  

OS 映像大小较大。 例如，Windows 7 的映像大小为 3 GB 或更大。 映像的大小和你向其中同时部署 OS 的计算机的数量会影响网络性能和可用带宽。 请务必测试网络性能。 测试影响可以更好地衡量映像部署可能产生的影响，以及完成部署所需的时间。 影响网络性能的 Configuration Manager 活动包括将映像分发到分发点、将映像从一个站点分发到另一个站点，以及将映像下载到客户端。  

还要确保在托管 OS 映像的分发点上规划足够的磁盘存储空间。  

有关详细信息，请参阅[分发点的其他规划注意事项](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_AdditionalPlanning)。


### <a name="client-cache-size"></a>客户端缓存大小  

Configuration Manager 客户端在下载内容时会自动使用后台智能传输服务 (BITS)（如果该服务可用）。 在部署用于安装 OS 的任务序列时，可以针对部署设置选项，以便 Configuration Manager 客户端在任务序列运行之前将完整映像下载到本地缓存。  

如果 Configuration Manager 客户端必须下载 OS 映像，但缓存中没有足够的空间，那么客户端可以清理其缓存中的空间。 它会检查缓存中的其他包，确定删除任何最旧的包是否可以释放足够的磁盘空间以容纳映像。 如果删除包无法释放足够的空间，则客户端不会下载映像，并且部署失败。 如果缓存中有配置为保留在缓存中的大型包，则会发生这种行为。 如果删除包可在缓存中释放足够的空间，则客户端将删除这些包，然后将映像下载到缓存中。  

Configuration Manager 客户端上的默认缓存大小对于大多数 OS 映像部署而言可能不够大。 如果计划将完整映像下载到客户端缓存，可以在目标计算机上调整客户端缓存大小以适应所部署的映像的大小。  

有关详细信息，请参阅[配置客户端缓存](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache)。  


