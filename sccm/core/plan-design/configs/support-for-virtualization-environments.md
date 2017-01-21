---
title: "虚拟化环境的支持 | Microsoft Docs"
description: "获取在虚拟化环境中安装 System Center Configuration Manager 客户端和站点系统的要求"
ms.custom: na
ms.date: 11/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 13df135828e383e666bfc11051011207245a774c
ms.openlocfilehash: 1c00324d2e7cc9a082ba837b29879e3a778d0c54


---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>对 System Center Configuration Manager 的虚拟化环境的支持

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 支持在受支持的操作系统上安装客户端和站点系统角色，该操作系统在以下虚拟化环境中作为虚拟机运行。 甚至当虚拟机主机（虚拟化环境）不被支持作为客户端或站点服务器时，这种支持仍然存在。  

 **例如**，如果你使用 Microsoft Hyper-V Server 2012 托管运行 Windows Server 2012 的虚拟机，则你可以在虚拟机 (Windows Server 2012) 上安装客户端或站点系统角色，但不是在主机 (Microsoft Hyper-V Server 2012) 上。  

|虚拟化环境|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|  

 使用的每台虚拟计算机必须满足或超过将用于物理 Configuration Manager 计算机的相同硬件和软件配置。  

 通过使用服务器虚拟化验证计划和其在线的虚拟化计划支持策略向导，可以验证虚拟化环境是否支持 Configuration Manager。 有关服务器虚拟化验证计划的详细信息，请参阅 [Windows Server 虚拟化验证计划](https://www.windowsservercatalog.com/svvp.aspx)。  

> [!NOTE]  
>  Configuration Manager 不支持在 Mac 上运行的虚拟 PC 或虚拟服务器来宾操作系统。  

Configuration Manager 无法管理虚拟机，除非虚拟机处于联机状态。 不能更新脱机虚拟机映像，也不能使用主计算机上的 Configuration Manager 客户端收集清单。  

未提供虚拟机的特别注意事项。 例如，如果停止并重新启动了虚拟机，但是没有保存应用更新的虚拟机状态，则 Configuration Manager 可能无法确定是否需要将更新重新应用到虚拟机映像。  

##  <a name="a-namebkmkazurea-microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Microsoft Azure 虚拟机  
 支持在 Microsoft Azure 虚拟机中运行 Configuration Manager，正如在物理公司网络中运行内部部署一样。 可以在以下方案中将 Configuration Manager 与 Microsoft Azure 虚拟机配合使用：  

-   **方案 1：**可以在 Microsoft Azure 虚拟机中运行 Configuration Manager，并使用它管理安装在其他 Microsoft Azure 虚拟机上的客户端。  

-   **方案 2：**可以在 Microsoft Azure 虚拟机中运行 Configuration Manager，并使用它管理未在 Microsoft Azure 中运行的客户端。  

-   **方案 3：**可以在 Microsoft Azure 虚拟机中运行不同的 Configuration Manager 站点系统角色，同时在物理公司网络（具有用于通信的相应网络连接）中运行其他角色。  

如果网络 System Center Configuration Manager 要求以及支持的配置和硬件要求适用于在物理公司网络中安装 Configuration Manager 内部部署，则这些要求也适用于在 Microsoft Azure 中进行安装。  

有关详细信息，请参阅 [Azure 上的 Configuration Manager - 常见问题解答](/sccm/core/understand/configuration-manager-on-azure)。

> [!IMPORTANT]  
>  Configuration Manager 站点和在 Azure 虚拟机中运行的客户端与安装内部部署遵循相同的许可证要求。  



<!--HONumber=Dec16_HO3-->


