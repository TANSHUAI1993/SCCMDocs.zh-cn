---
title: "软件清单 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中的软件清单简介。"
ms.custom: na
ms.date: 12/26/2016
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
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: c9956dd4ef94a1b109d761e44e42f512c42eb8d2


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

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Microsoft Intune 注册的移动设备的软件清单  
 可针对移动设备上安装的应用收集清单。 是否将应用加入清单将取决于设备归公司所有还是归个人所有。 对于个人设备，仅将通过 Microsoft Intune 管理的应用加入清单。  

> [!NOTE]  
>  会将移动设备上安装的应用的清单作为[硬件清单](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md)过程的一部分进行收集。  

 下方列出了适用于个人拥有设备或公司拥有设备的应用清单。  

|平台|个人拥有设备|公司拥有设备|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10（不带 Configuration Manager 客户端）|仅托管应用|仅托管应用| 
|Windows 8.1（不带 Configuration Manager 客户端）|仅托管应用|仅托管应用|  
|Windows Phone 8|仅托管应用|仅托管应用|  
|Windows RT|仅托管应用|仅托管应用|  
|iOS|仅托管应用|设备上安装的所有应用|  
|Android|仅托管应用|设备上安装的所有应用|  





<!--HONumber=Dec16_HO5-->


