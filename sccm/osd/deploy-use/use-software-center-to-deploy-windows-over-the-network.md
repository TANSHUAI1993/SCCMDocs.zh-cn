---
title: "使用软件中心通过网络部署 Windows | Microsoft Docs"
description: "可将操作系统部署到软件中心，使用新版 Windows 刷新现有计算机或将 Windows 升级到最新版本。"
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: "5"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 8988409c68b7f69439ed03872c316b2139d25616
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>使用软件中心与 System Center Configuration Manager 一起通过网络部署 Windows

*适用范围：System Center Configuration Manager (Current Branch)*

你可以使在 System Center Configuration Manager 中安装操作系统的任务序列在软件中心可用。 可以使用以下操作系统部署方案将操作系统部署到软件中心：

-   [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [将 Windows 升级到最新版本](upgrade-windows-to-the-latest-version.md)

完成其中一个操作系统部署方案中的步骤。 然后使用以下部分来准备在 Software Center 中可用的部署。

## <a name="configure-deployment-settings"></a>配置部署设置  
要使操作系统部署在软件中心中可用，请配置该部署。 可以在部署软件向导的“部署设置”页或部署属性的“部署设置”选项卡中配置部署。 对于“可用于以下项目”  设置，请配置“仅 Configuration Manager 客户端”  或“Configuration Manager 客户端、媒体和 PXE” 。 系统部署操作系统后，操作系统显示在目标集合成员的软件中心中。

##  <a name="BKMK_Deploy"></a> 将任务序列部署到计算机  
将操作系统部署到目标集合。 有关详细信息，请参阅 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。 在为软件中心部署操作系统时，可以配置部署属性为必需还是可用。

-   **必需部署**：必需部署将使操作系统在软件中心可用，但会按配置的分配计划自动启动。

-   **可用部署**：操作系统将在软件中心内可用，且用户可根据需要进行安装。
