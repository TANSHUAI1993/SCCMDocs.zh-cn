---
title: "支持的配置 | System Center Configuration Manager"
description: "标识重要配置和要求，以便可以规划、部署和维护功能性 System Center Configuration Manager 部署。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 170bd941bd123b998dd5d6235359aee97adc06bd


---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>System Center Configuration Manager 支持的配置

*适用范围：System Center Configuration Manager (Current Branch)*

作为本地解决方案，System Center Configuration Manager 会使用服务器、客户端、网络配置和其他产品（如 Microsoft Intune、SQL Server 和 Azure）。

对于标识重要配置和要求或限制，以便可以规划、部署和维护功能性 Configuration Manager 部署，本主题及后续主题中的信息至关重要。  此信息特定于 Configuration Manager 站点、层次结构和托管设备的基础结构。 当 Configuration Manager 特性或功能需要更具体的配置时，该信息会包含在功能特定文档中，可补充这些更常规的受支持配置详细信息。  

 以下各主题中详细列出的产品和技术通过 Configuration Manager 进行支持。 但是，它们包括在此内容中并不表示对任何超出该产品个体支持生命周期的产品的扩展支持。 不支持将超出其支持生命周期的产品与 Configuration Manager 一起使用。 有关 Microsoft 支持生命周期的详细信息，请访问 [Microsoft 支持生命周期](http://go.microsoft.com/fwlink/p/?LinkId=208270) 网站。  

> [!NOTE]  
>  有关 Microsoft 支持生命周期策略的信息，请转到 Microsoft 支持生命周期支持策略常见问题网站：[Microsoft 支持生命周期策略常见问题](http://go.microsoft.com/fwlink/p/?LinkId=31976)。  

 此外，System Center Configuration Manager 不支持以下主题中未列出的产品和产品版本，除非它们已在[企业移动性和安全性博客](https://blogs.technet.microsoft.com/enterprisemobility/)上公布。  此博客上的内容有时会早于本文档正文的更新。


-  [大小和扩展数量](../../../core/plan-design/configs/size-and-scale-numbers.md)  
有关 Configuration Manager 的不同层次结构设计中支持的站点、每个站点的站点系统角色以及客户端或设备数的详细信息。

-  [站点和站点系统先决条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Windows 服务器支持不同站点类型和站点系统角色所需的配置。

-  [站点系统服务器支持的操作系统](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
了解可以用作站点服务器或站点系统服务器的操作系统。

-  [客户端和设备支持的操作系统](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
了解可以使用 Configuration Manager 进行管理的操作系统，包括 Windows、Linux 和 UNIX、Mac、嵌入式操作系统以及移动设备。

-  [控制台支持的操作系统](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
了解可以承载 Configuration Manager 控制台以便为管理部署提供访问点的操作系统。  

-  [支持 SQL Server 版本](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
列出可以承载站点数据库和报表数据库的 SQL Server 版本，以及必需配置和可以选择使用的可选配置。

-  [高可用性选项](../../../protect/understand/high-availability-options.md)  
了解设计环境以帮助为 Configuration Manager 部署维护高可用服务级别时可以实现的选项。

-  [推荐硬件](../../../core/plan-design/configs/recommended-hardware.md)  
可以帮助确定适合于承载 Configuration Manager 站点和关键服务的硬件和配置的指导。

-  [对 Active Directory 域的支持](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
了解 Configuration Manager 需要和支持的受支持 Active Directory 域配置。

-  [对 Windows 功能和网络的支持](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Configuration Manager 支持多种 Windows 技术，如 BranchCache 和重复数据删除。 了解支持的技术以及它们用于 Configuration Manager 时的限制。

-  [对虚拟化环境的支持](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
用于帮助使用支持的虚拟机技术的信息。



<!--HONumber=Nov16_HO1-->


