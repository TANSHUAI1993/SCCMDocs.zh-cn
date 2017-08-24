---
title: "虚拟化环境的支持 | Microsoft Docs"
description: "获取在虚拟化环境中安装 System Center Configuration Manager 客户端和站点系统的要求"
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b49bd179da850cee35b2487a353bb1788df03d58
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>对 System Center Configuration Manager 的虚拟化环境的支持

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 支持在受支持的操作系统上安装客户端和站点系统角色，这些受支持的操作系统在本文中列出的虚拟化环境中作为虚拟机运行。 甚至当虚拟机主机（虚拟化环境）不被支持作为客户端或站点服务器时，这种支持仍然存在。  

 例如，如果使用 Microsoft Hyper-V Server 2012 托管运行 Windows Server 2012 的虚拟机，则可在虚拟机 (Windows Server 2012) 上安装客户端或站点系统角色，但不是在主机 (Microsoft Hyper-V Server 2012) 上。  

|虚拟化环境|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|
|Windows Server 2016 <sup>（见注释 1）</sup>|
|Microsoft Hyper-V Server 2016 <sup>（见注释 1）|
-  注释 1：Configuration Manager 不支持[嵌套虚拟化](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new)，这是 Windows Server 2016 的新增功能。


 使用的每台虚拟计算机必须满足或超过将用于物理 Configuration Manager 计算机的相同硬件和软件要求。  

 通过使用服务器虚拟化验证计划和其在线的虚拟化计划支持策略向导，可以验证虚拟化环境是否支持 Configuration Manager。 有关服务器虚拟化验证计划的详细信息，请参阅 [Windows Server 虚拟化验证计划](https://www.windowsservercatalog.com/svvp.aspx)。  

> [!NOTE]  
>  Configuration Manager 不支持在 Mac 计算机上运行的虚拟 PC 或虚拟服务器来宾操作系统。  

Configuration Manager 无法管理虚拟机，除非虚拟机处于联机状态。 不能更新脱机虚拟机映像，也不能使用主计算机上的 Configuration Manager 客户端收集清单。  

未提供虚拟机的特别注意事项。 例如，如果停止并重新启动了虚拟机，但是没有保存应用更新的虚拟机状态，则 Configuration Manager 可能无法确定是否需要将更新重新应用到虚拟机映像。  

##  <a name="bkmk_Azure"></a> Microsoft Azure 虚拟机  
 Configuration Manager 可在 Azure 中的虚拟机上运行，正如在实体公司网络中本地运行一样。 可以在以下方案中将 Configuration Manager 与 Azure 虚拟机配合使用：  

-   **方案 1：**可以在 Azure 虚拟机上运行 Configuration Manager，并使用它管理安装在其他 Azure 虚拟机上的客户端。  

-   **方案 2：**可以在 Azure 虚拟机上运行 Configuration Manager，并使用它管理不在 Azure 上运行的客户端。  

-   **方案 3：**可以在 Azure 虚拟机上运行不同的 Configuration Manager 站点系统角色，同时在物理公司网络（具有用于通信的相应网络连接）中运行其他角色。  

如果网络 System Center Configuration Manager 要求以及支持的配置和硬件要求适用于在物理公司网络中安装本地 Configuration Manager，则这些要求也适用于在 Azure 虚拟机中进行安装。  

有关详细信息，请参阅 [Azure 上的 Configuration Manager - 常见问题解答](/sccm/core/understand/configuration-manager-on-azure)。

> [!IMPORTANT]  
>  Configuration Manager 站点和在 Azure 虚拟机中运行的客户端与本地安装遵循相同的许可证要求。  
