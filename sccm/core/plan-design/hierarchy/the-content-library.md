---
title: "内容库 | Microsoft Docs"
description: "了解 System Center Configuration Manager 用于减少已分发内容总大小的内容库的信息。"
ms.custom: na
ms.date: 2/14/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fa9f431c00476d71b2b08f92f914d76636d1a27
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="the-content-library-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的内容库

*适用范围：System Center Configuration Manager (Current Branch)*

内容库是内容的单实例存储，System Center Configuration Manager 使用它来减少分发的内容的组合正文的总体大小。 内容库存储软件更新、应用程序、操作系统部署等的所有内容文件。

 - 会在每个**站点服务器**和每个**分发点**上自动创建并维护内容库的副本。

 - 在 Configuration Manager 将内容文件下载到站点服务器或将文件复制到分发点之前，Configuration Manager 会验证每个内容文件是否已在内容库中。
 - 如果有内容文件，则 Configuration Manager 不会复制该文件，而是会将现有内容文件与应用程序或包关联。

在安装分发点的计算机上，你可以配置下列内容：

- 希望在其上创建内容库的一个或多个磁盘驱动器。
- 使用的每个驱动器的优先级。

Configuration Manager 复制内容文件时，会将文件复制到优先级最高的驱动器中，直到该驱动器的可用空间小于指定的最小可用空间。
- 在分发点安装过程中，你可以配置驱动器设置。
- 安装完成后，无法在分发点属性中配置驱动器设置。


有关如何为分发点配置驱动器设置的详细信息，请参阅[为 System Center Configuration Manager 管理内容和内容基础结构](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  


>  [!IMPORTANT]  
>  若要在安装后将内容库移到分发点上的另一位置，请使用 System Center 2012 R2 Configuration Manager 工具包中的**内容库传输工具**。 可以从 [Microsoft Download Center（Microsoft 下载中心）](http://go.microsoft.com/fwlink/?LinkId=279566)下载此工具包。  

## <a name="about-the-content-library-on-the-central-administration-site"></a>关于管理中心站点上的内容库  
 默认情况下，安装站点时，Configuration Manager 会在管理中心站点上创建内容库。 该内容库放置在具有最多可用磁盘空间的站点服务器驱动器上。 因为无法在管理中心站点上安装分发点，所以无法确定内容库要使用的驱动器的优先级。 类似于其他站点服务器和分发点上的内容库，当包含内容库的驱动器可用磁盘空间不足时，内容库会自动跨越到下一个可用的驱动器。  

 Configuration Manager 会在以下情况下使用管理中心站点上的内容库：  

-   在管理中心站点上创建内容时。  

-   迁移另一个 Configuration Manager 站点中的内容，并将管理中心站点指定为将管理该内容的站点时。  

> [!NOTE]  
>  在主站点创建内容，然后将其分发给其他主站点或其他主站点下面的辅助站点，管理中心站点将该内容临时存储在管理中心站点上的计划员收件箱中，但未将该内容添加到其内容库中。  

 使用以下选项管理位于管理中心站点上的内容库：  

-   若要防止在特定驱动器上安装内容库，请在创建内容库前先创建一个名为 **no_sms_on_drive.sms** 的空文件，然后将该文件复制到驱动器的根文件夹。  

-   创建内容库之后，请使用 System Center 2012 R2 Configuration Manager 工具套件中的**内容库传输工具**来管理内容库的位置。 可以从 [Microsoft Download Center（Microsoft 下载中心）](http://go.microsoft.com/fwlink/?LinkId=279566)下载此工具包。  
