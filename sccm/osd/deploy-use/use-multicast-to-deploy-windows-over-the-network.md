---
title: "使用多播通过网络部署 Windows | Microsoft Docs"
description: "在 System Center Configuration Manager 环境中使用多播，以便多台计算机可同时下载操作系统映像。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
caps.latest.revision: "13"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 55266696aa7340fddda3a57ff90e20222ff665a5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>使用多播与 System Center Configuration Manager 一起通过网络部署 Windows

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 环境中，多个客户端可能会同时下载同一个操作系统映像，而多播是一种可以在此环境中使用的网络优化方法。 在使用多播时，多台计算机同时下载操作系统映像，这是因为分发点多播此映像，而不是通过单独的连接将此数据的副本发送给每个客户端。  

 通过在以下操作系统部署方案中使用多播，你可以通过网络部署操作系统：  

-   [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)  

 完成其中一个操作系统部署方案中的步骤，然后使用以下部分来支持多播。  

##  <a name="BKMK_Configure"></a> 配置分发点以支持多播  
 若要在部署操作系统时使用多播，必须将分发点配置为支持多播。 有关详细信息，请参阅[配置分发点以支持多播](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)。  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>为多播部署准备操作系统映像  
 若要将操作系统映像包配置为支持多播，请参阅[为多播部署准备操作系统映像](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast)。  

##  <a name="BKMK_Deploy"></a> 部署任务序列  
 将操作系统部署到目标集合。 有关详细信息，请参阅 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。  
