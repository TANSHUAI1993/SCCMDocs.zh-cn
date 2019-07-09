---
title: 软件清单
titleSuffix: Configuration Manager
description: 获取 System Center Configuration Manager 中的软件清单简介。
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0ca25d64f3dd0e86ddbd89e2d86ae13da170891
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550734"
---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的软件清单简介

适用范围：  System Center Configuration Manager (Current Branch)

使用软件清单在客户端设备上收集文件相关信息。 软件清单还可从客户端设备收集文件并将其存储在站点服务器上。 如果选中客户端设置中的“在客户端上启用软件清单”  设置，便会收集软件清单。 此外，还可以在客户端设置中安排此操作。  

在你启用软件清单且客户端运行软件清单周期后，客户端便会将信息发送到客户端站点中的管理点。 随后，管理点将清单信息转发到 Configuration Manager 站点服务器，后者会将信息存储在站点数据库中。

 可通过以下几种方法来查看软件清单数据：  

- [创建查询](../../../../core/servers/manage/create-queries.md)，该查询将返回具有特定文件的设备。   

- 创建[基于查询的集合](../../../../core/clients/manage/collections/introduction-to-collections.md)，此集合包括具有特定文件的设备。   

- [运行报表](../../../../core/servers/manage/reporting.md)，此报表提供有关设备上文件的详细信息。

- 使用[资源浏览器](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)查看已列出清单并从客户端设备收集的文件的详细信息。   

 在客户端设备上运行软件清单时，返回的第一个报表是完整清单。 后续报告只包含增量清单信息。 站点服务器按接收顺序对增量信息进行处理。 如果缺少客户端的增量信息，站点服务器会拒绝其他增量信息，并指示客户端运行完整清单周期。  

 Configuration Manager 可以发现双引导计算机，但只从在清单周期运行时处于活动状态的操作系统返回清单信息。  

**移动设备：** 若要了解如何收集移动设备上已安装应用的清单，请参阅[向 Microsoft Intune 注册的移动设备的软件清单](../../../../mdm/deploy-use/software-inventory-mobile-devices.md)。
