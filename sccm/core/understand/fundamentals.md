---
title: 基础
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager 的基础概念。
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cc4cdb35-f0b4-42b5-9cec-6431a8c30793
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bd134857f53157e4ea81d46ff1a36693d7366ca
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="fundamentals-of-system-center-configuration-manager"></a>System Center Configuration Manager 基础知识

*适用范围：System Center Configuration Manager (Current Branch)*

如果不熟悉 System Center Configuration Manager，请在运行安装程序安装第一个站点之前，阅读基础主题以了解有关 Configuration Manager 的基本概念。 如果熟悉 Configuration Manager，则可以直接运行安装程序。 我们建议首先阅读 [System Center Configuration Manager 中的新增功能](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)。  

 有关支持的操作系统和支持的环境的信息、硬件要求以及容量信息，请参阅 [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)。  

 当部署 Configuration Manager 时，部署一个或多个站点：  

-   **部署多个站点时**，站点将形成子级到父级的关系，这些关系统称为层次结构。 使用层次结构集中管理大量站点和设备。  数据和信息沿层次结构向下流动以到达你管理的设备。 设备信息、配置任务和请求的结果沿层次结构向上流动。  

-   **部署单个站点时**，该站点也称为层次结构。  

 一些配置任务和设置将适用于层次结构中的所有站点，而其他一些则适用于个别站点。  

## <a name="fundamental-concepts-for-system-center-configuration-manager"></a>System Center Configuration Manager 的基本概念
查看以下主题，了解 System Center Configuration Manager 的基本概念：  

-   [System Center Configuration Manager 的站点和层次结构基础知识](../../core/understand/fundamentals-of-sites-and-hierarchies.md)  

-   [使用 System Center Configuration Manager 管理设备的基础知识](../../core/understand/fundamentals-of-managing-devices.md)  

-   [System Center Configuration Manager 的客户端管理任务基础](../../core/understand/fundamentals-of-client-management-tasks.md)  

-   [System Center Configuration Manager 安全性的基础知识](../../core/understand/fundamentals-of-security.md)  
