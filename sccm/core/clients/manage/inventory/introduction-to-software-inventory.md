---
title: "软件清单 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中的软件清单简介。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a468ce93e9536fe3f6bf0fc191ff9764dd1c3343
ms.openlocfilehash: 401ba6e37d740310d49ab9e96112ce576d7130e4


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的软件清单简介

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 中的软件清单，收集有关组织中的客户端设备所含文件的信息。 而且，软件清单可从客户端设备收集文件并将其存储在站点服务器上。 在客户端设置中启用“在客户端上启用软件清单”  设置时会收集软件清单。  

 启用软件清单并且客户端运行了一个软件清单周期后，客户端会将清单信息发送到客户端站点中的管理点。 随后，管理点将清单信息转发到 Configuration Manager 站点服务器，将清单信息存储在站点数据库中。 根据在客户端设置中指定的计划，会在客户端上运行软件清单。  

 可以使用多种方法来查看 Configuration Manager 收集的软件清单数据。 这些存储包括以下各项：  

-   创建基于你指定的文件返回设备的查询（这些文件可在设备上找到）。 有关详细信息，请参阅 [System Center Configuration Manager 的查询技术参考](../../../../core/servers/manage/queries-technical-reference.md)。  

-   创建基于你指定的文件的基于查询的集合（这些文件可在设备上找到）。 基于查询的集合成员身份会按计划自动更新。 可以使用多个任务的集合，如软件部署。 有关详细信息，请参阅 [System Center Configuration Manager 中的集合简介](../../../../core/clients/manage/collections/introduction-to-collections.md)。  

-   运行报表，该报表可显示贵组织中设备上的文件的特定详细信息。 有关详细信息，请参阅 [System Center Configuration Manager 中的报表](../../../../core/servers/manage/reporting.md)。  

-   使用资源浏览器查看已列出清单并从客户端设备收集的文件的详细信息。 有关详细信息，请参阅[如何使用资源浏览器查看 System Center Configuration Manager 中的软件清单](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)。  

 在客户端设备上运行软件清单时，返回的第一个清单报表始终是完整清单。 后续清单报表只包含增量清单信息。 站点服务器按收到增量清单信息的顺序对它进行处理。 如果缺少客户端的增量清单信息，则站点服务器会拒绝其他增量清单信息，并指示客户端运行完整清单周期。  

 Configuration Manager 为双引导计算机提供有限支持。 Configuration Manager 可以发现双引导计算机，但只从在清单运行时处于活动状态的操作系统返回清单信息。  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Microsoft Intune 注册的移动设备的软件清单  
 可以针对移动设备上安装的应用收集清单。 是否将应用加入清单将取决于设备归公司所有还是归个人所有。 对于个人设备，仅将通过 Microsoft Intune 管理的应用加入清单。  

> [!NOTE]  
>  会将移动设备上安装的应用的清单作为 Configuration Manager 中硬件清单过程的一部分进行收集。 有关详细信息，请参阅[如何配置通过 Microsoft Intune 和 System Center Configuration Manager 注册的移动设备的硬件清单](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md)。  

 下表列出了哪些应用为个人拥有设备的清单，哪些为公司拥有设备的清单。  

|平台|个人拥有设备|公司拥有设备|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10（不带 Configuration Manager 客户端）|仅托管应用|仅托管应用| 
|Windows 8.1（不带 Configuration Manager 客户端）|仅托管应用|仅托管应用|  
|Windows Phone 8|仅托管应用|仅托管应用|  
|Windows RT|仅托管应用|仅托管应用|  
|iOS|仅托管应用|设备上安装的所有应用|  
|Android|仅托管应用|设备上安装的所有应用|  



<!--HONumber=Dec16_HO3-->


