---
title: "发现设备和用户资源 | Microsoft Docs"
description: "阅读发现过程和发现数据记录的概述。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
caps.latest.revision: "20"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 647826e9d340d3ef97abab0dba51041a3727dedc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="run-discovery-for-system-center-configuration-manager"></a>运行 System Center Configuration Manager 发现

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 中的一种或多种发现方法以查找可以管理的设备和用户资源。 还可以使用发现来识别环境中的网络基础结构。 可使用多种不同的方法来发现不同的内容，并且每种方法都有其自己的配置和限制。  

## <a name="overview-of-discovery"></a>发现概述  
 发现是一个 Configuration Manager 用于了解可管理的事务的过程。 以下是可用的发现方法：  

-   Active Directory 林发现  

-   Active Directory 组发现  

-   Active Directory 系统发现  

-   Active Directory 用户发现  

-   检测信号发现  

-   网络发现  

-   服务器发现  

> [!TIP]  
>  你可以在[有关 System Center Configuration Manager 的发现方法](../../../../core/servers/deploy/configure/about-discovery-methods.md)中了解各个发现方法。  
>   
>  有关选择要使用的方法和层次结构中的站点的帮助，请参阅[选择 System Center Configuration Manager 要使用的发现方法](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)。  

 若要使用大部分的发现方法，必须在站点上启用该方法，并将其设置为搜索特定网络或 Active Directory 位置。 运行时，此方法会查询特定位置以获取有关 Configuration Manager 可管理的设备或用户的信息。 当发现方法成功找到有关资源的信息时，它会将该信息放在称为发现数据记录 (DDR) 的文件中。 主站点或管理中心站点随后将对该文件进行处理。 对 DDR 的处理会在站点数据库中为新发现的资源创建一条新记录，或使用新信息更新现有记录。  

 某些发现方法可能会生成大量的网络流量，并且所产生的 DDR 可能会导致在处理过程中使用大量的 CPU 资源。 因此，请计划仅使用满足目标所需的那些发现方法。 可在开始时仅使用一种或两种发现方法，之后以管制方式启用其他方法以扩展环境中的发现级别。  

 将发现信息添加到站点数据库后，再将其复制到层次结构中的每个站点中，与发现或处理此信息的位置无关。 因此，尽管可为不同站点中的发现方法设置不同的计划和设置，但可能仅会在单个站点中运行特定的发现方法。 这通过重复的发现操作减少网络带宽的使用，并减少在多个站点中对冗余发现数据的处理。  

 可以使用发现数据来创建对管理任务的资源进行逻辑分组的自定义集合和查询。 例如：  

-   推送客户端安装或升级。  

-   将内容部署到用户或设备。  

-   部署客户端设置和相关配置。

##  <a name="BKMK_DDRs"></a>关于发现数据记录  
 DDR 是由发现方法创建的文件。 它们包含可在 Configuration Manager 中管理的资源的信息，如计算机、用户和（某些情况下的）网络基础结构。 将在主站点或管理中心站点上对它们进行处理。 在 DDR 中的资源信息进入数据库后，即会删除该 DDR，并且信息将以全局数据的形式复制到层次结构中的所有站点。  

 处理 DDR 的站点取决于它包含的信息：  

-   数据库中没有的新发现资源的 DDR 在层次结构的顶层站点上进行处理。 顶层站点在数据库中创建一条新的资源记录，并为其分配唯一的标识符。 DDR 通过基于文件的复制进行传输，直至到达顶层站点为止。  

-   以前发现的对象的 DDR 在主站点上进行处理。 如果 DDR 包含有关数据库中已有资源的信息，则子主站点不会将 DDR 传输到管理中心站点。  

-   辅助站点不处理 DDR，并会始终通过基于文件的复制将其传输到它们的父主站点。  

DDR 文件由 .ddr 扩展名标识，大小通常约为 1 KB。  

## <a name="get-started-with-discovery"></a>发现入门：  
 使用 Configuration Manager 控制台设置发现之前，应了解方法间的差异、方法可实现的效果，以及某些方法的局限性。  

以下主题可构成有助于你成功使用发现方法的基础：  

-   [关于 System Center Configuration Manager 的发现方法](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [选择 System Center Configuration Manager 要使用的发现方法](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

在对要使用的方法有所了解之后，可在[配置 System Center Configuration Manager 的发现方法](../../../../core/servers/deploy/configure/configure-discovery-methods.md)中找到每个方法的设置指南。  
