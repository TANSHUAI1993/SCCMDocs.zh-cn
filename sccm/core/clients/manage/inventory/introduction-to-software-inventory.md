---
title: "软件清单 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中的软件清单简介。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 969f2d28649853ddc95860fe72597d6d2c9a94e9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的软件清单简介

*适用范围：System Center Configuration Manager (Current Branch)*

使用软件清单在客户端设备上收集文件相关信息。 软件清单还可从客户端设备收集文件并将其存储在站点服务器上。 在客户端设置中选择“在客户端上启用软件清单”设置可收集软件清单，还可在其中安排操作。  

启用软件清单且客户端运行了一个软件清单周期后，客户端会将信息发送到客户端站点中的管理点。 随后，管理点将清单信息转发到 Configuration Manager 站点服务器，后者会将信息存储在站点数据库中。   

 可通过以下方法查看软件清单数据：  

-   [创建查询](../../../../core/servers/manage/queries-technical-reference.md)，该查询将返回具有特定文件的设备。   

-   创建[基于查询的集合](../../../../core/clients/manage/collections/introduction-to-collections.md)，此集合包括具有特定文件的设备。   

-   [运行报表](../../../../core/servers/manage/reporting.md)，此报表提供有关设备上文件的详细信息。

-   使用[资源浏览器](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)查看已列出清单并从客户端设备收集的文件的详细信息。   

 在客户端设备上运行软件清单时，返回的第一个报表是完整清单。 后续报表只包含增量清单信息。 站点服务器按接收顺序对增量信息进行处理。 如果缺少客户端的增量信息，则站点服务器会拒绝其他增量信息，并指示客户端运行完整清单。  

 Configuration Manager 可以发现双引导计算机，但只从在清单运行时处于活动状态的操作系统返回清单信息。  

**移动设备：**有关在移动设备上收集安装的应用清单，请参阅[使用 Microsoft Intune 注册的移动设备的软件清单](../../../../mdm/deploy-use/software-inventory-mobile-devices.md)。
