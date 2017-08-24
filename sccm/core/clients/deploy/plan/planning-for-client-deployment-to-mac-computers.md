---
title: "规划 Mac 计算机的客户端部署 | Microsoft Docs"
description: "在 System Center Configuration Manager 中规划 Mac 计算机的客户端部署。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 75bddb41d4d1cf209fa7595c52b5a6aa831ba3dd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-client-deployment-to-mac-computers-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中规划 Mac 计算机的客户端部署

*适用范围：System Center Configuration Manager (Current Branch)*

可以在运行 Mac OS X 操作系统并使用以下管理功能的 Mac 计算机上安装 Configuration Manager 客户端：  

-   **硬件清单**  

     可使用 Configuration Manager 硬件清单收集关于 Mac 计算机上的硬件和所安装的应用程序的信息。 然后可以在 Configuration Manager 控制台内的资源浏览器中查看此信息，并且可以使用此信息创建集合、查询和报表。 有关详细信息，请参阅[如何使用资源浏览器查看 System Center Configuration Manager 中的硬件清单](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)。  

     Configuration Manager 从 Mac 计算机中收集下列硬件信息：  

    -   处理器  

    -   计算机系统  

    -   磁盘驱动器  

    -   磁盘分区  

    -   网络适配器  

    -   操作系统  

    -   服务  

    -   过程  

    -   已安装的软件  

    -   计算机系统产品  

    -   USB 控制器  

    -   USB 设备  

    -   CDROM 驱动器  

    -   视频控制器  

    -   桌面监视器  

    -   便携式电池  

    -   物理内存  

    -   打印机  

    > [!IMPORTANT]  
    >  在硬件清点过程中，你无法扩展从 Mac 计算机收集的硬件信息。  

-   **符合性设置**  

     可以使用 Configuration Manager 符合性设置查看 Mac OS X 首选项 (.plist) 设置的符合性以及修正这些设置。 例如，你可以在 Safari Web 浏览器中强制主页设置，或者确保启用 Apple 防火墙。 也可以使用外壳脚本在 MAC OS X 中监视和修正设置。  

-   **应用程序管理**  

     Configuration Manager 可以将软件部署到 Mac 计算机。 你可以将以下软件格式部署到 Mac 计算机：  

    -   Apple 磁盘映像 (.DMG)  

    -   元包文件 (.MPKG)  

    -   Mac OS X 安装程序包 (.PKG)  

    -   Mac OS X 应用程序 (.APP)  

 在 Mac 计算机上安装 Configuration Manager 客户端时，无法使用基于 Windows 的计算机上 Configuration Manager 客户端支持的以下管理功能：  

-   客户端请求安装  

-   操作系统部署  

-   软件更新  

    > [!NOTE]  
    >  可以使用 Configuration Manager 应用程序管理将所需的 Mac OS X 软件更新部署到 Mac 计算机。 此外，可以使用符合性设置来确保计算机具有任何所需的软件更新。  

-   维护时段  

-   远程控制  

-   电源管理  

-   客户端状态客户端检查和修正  

 有关如何安装和配置 Configuration Manager Mac 客户端的详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 Mac](../../../../core/clients/deploy/deploy-clients-to-macs.md)。
