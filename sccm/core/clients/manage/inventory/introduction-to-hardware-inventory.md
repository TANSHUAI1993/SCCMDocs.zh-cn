---
title: "硬件清单 - Configuration Manager | Microsoft Docs"
description: "获取 System Center Configuration Manager 中的硬件清单简介。"
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: c64f0b42bff25e8e91cf9101d6fbb538634eab15
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的硬件清单简介

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 中的硬件清单可收集有关组织中的客户端设备硬件配置的信息。 要收集硬件清单，必须在客户端设置中启用“针对客户端启用硬件清单”  设置。  

 启用硬件清单并且由客户端运行硬件清单周期之后，客户端会将该信息发送到客户端站点中的管理点。 随后，管理点将清单信息转发到 Configuration Manager 站点服务器，将清单信息存储在站点数据库中。 硬件清单会根据你在客户端设置中指定的计划在客户端上运行。  

 可使用多种方法来查看 Configuration Manager 收集的硬件清单数据。 这些存储包括以下各项：  

-   [创建返回基于特定硬件配置的设备的查询](../../../../core/servers/manage/queries-technical-reference.md)。  

-   [创建基于特定硬件配置的基于查询的集合](../../../../core/clients/manage/collections/introduction-to-collections.md)。 基于查询的集合成员身份会按计划自动更新。 可以将集合用于多个任务（包括软件部署）。 。  

-   [运行显示有关组织中硬件配置的特定详细信息的报表](../../../../core/servers/manage/reporting.md)。   

-   [使用资源浏览器](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)查看有关从客户端设备收集的硬件清单的详细信息。   

 当硬件清单在客户端设备上运行时，客户端返回的第一批清单数据始终是完整清单。 后续清单信息仅包含增量清单信息。 站点服务器按收到增量清单信息的顺序对它进行处理。 如果缺少客户端的增量信息，则站点服务器会拒绝其他增量信息，并指示客户端运行完整清单周期。  

 Configuration Manager 为双引导计算机提供有限支持。 Configuration Manager 可以发现双引导计算机，但只从在清单周期运行时处于活动状态的操作系统返回清单信息。  

> [!NOTE]  
>  有关如何使用运行 Linux 和 UNIX 的客户端硬件清单的信息，请参阅 [System Center Configuration Manager 中 Linux 和 UNIX 的硬件清单](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)。  

## <a name="extending-configuration-manager-hardware-inventory"></a>扩展 Configuration Manager 硬件清单  
 除了 Configuration Manager 中的内置硬件清单，还可以使用以下方法之一来扩展硬件清单以收集其他信息：  

- 可以从 Configuration Manager 控制台为硬件清单启用、禁用、添加和删除清单类。|  
- 使用 NOIDMIF 文件可收集有关无法由 Configuration Manager 列出清单的客户端设备的信息。 例如，您可能想要收集设备资产编号的信息仅作为在设备上的标签存在。 NOIDMIF 清单是自动与收集从客户端设备相关联。  
- 使用 IDMIF 文件收集不与 Configuration Manager 客户端关联的资产的相关信息，例如，投影仪、复印机和网络打印机。  

 有关使用这些方法扩展 Configuration Manager 硬件清单的详细信息，请参阅[如何在 System Center Configuration Manager 中配置硬件清单](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)。  
