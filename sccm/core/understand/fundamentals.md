---
title: "System Center Configuration Manager 基础知识 | Microsoft Docs"
description: "了解 System Center Configuration Manager 的基础概念。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc4cdb35-f0b4-42b5-9cec-6431a8c30793
caps.latest.revision: 11
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: b808e9089aabe3895892ecf3caf1610478361172

---
# <a name="fundamentals-of-system-center-configuration-manager"></a>System Center Configuration Manager 基础知识

*适用范围：System Center Configuration Manager (Current Branch)*

如果不熟悉 System Center Configuration Manager，请在运行安装程序安装第一个站点之前，阅读基础主题以了解有关 Configuration Manager 的基本概念。 如果已熟悉 Configuration Manager，则可以立即着手，并且建议从 [System Center Configuration Manager 中的新增功能](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)开始。  

 有关支持的操作系统和支持的环境的信息、硬件要求以及容量信息，请参阅 [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)。  

 当部署 Configuration Manager 时，部署一个或多个站点：  

-   **部署多个站点时**，站点将形成子级到父级的关系，这些关系统称为层次结构。 层次结构能够让你集中管理大量站点和设备。  数据和信息沿层次结构向下流动到达你管理的设备。 设备信息、配置任务和请求的结果沿层次结构向上流动。  

-   **部署单个站点时** ，该站点也称为层次结构。  

 一些配置任务和设置将适用于层次结构中的所有站点，而其他一些则适用于个别站点。  


**以下主题可解释 System Center Configuration Manager的基本概念：**  

-   [System Center Configuration Manager 的站点和层次结构基础知识](../../core/understand/fundamentals-of-sites-and-hierarchies.md)  

-   [使用 System Center Configuration Manager 管理设备的基础知识](../../core/understand/fundamentals-of-managing-devices.md)  

-   [System Center Configuration Manager 的客户端管理任务基础](../../core/understand/fundamentals-of-client-management-tasks.md)  

-   [System Center Configuration Manager 安全性的基础知识](../../core/understand/fundamentals-of-security.md)  



<!--HONumber=Dec16_HO3-->


