---
title: "特性和功能 | Microsoft Docs"
description: "了解 System Center Configuration Manager 的主要管理功能。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
caps.latest.revision: "18"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4691f43dccdf73936107f4635321897b9779bead
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>System Center Configuration Manager 的特性和功能

*适用范围：System Center Configuration Manager (Current Branch)*

以下是 System Center Configuration Manager 的主要管理功能。 每项功能都有自己的先决条件，用户希望使用的功能可能会影响 Configuration Manager 层次结构的设计和实现。 例如，你希望将软件部署到层次结构中的设备，则必须安装分发点站点系统角色。  

 有关如何规划和安装 Configuration Manager 以在环境中支持这些管理功能的详细信息，请参阅[为 System Center Configuration Manager 做准备](../../../core/plan-design/get-ready.md)。  

 **应用程序管理**  

 提供一组工具和资源，这些工具和资源可帮助你创建、管理、部署和监视一系列你管理的不同设备的应用程序。 此外，Configuration Manager 提供了一些工具，这些工具有助于保护用户应用中的公司数据。 请参阅[应用程序管理简介](/sccm/apps/understand/introduction-to-application-management)。

 **公司资源访问**  

 提供了一组工具和资源，使你能够向机构中的用户授予对远程位置中的数据和应用程序的访问权限。 这些工具包括 Wi-Fi 配置文件、VPN 配置文件、证书配置文件和对 Exchange 和 SharePoint Online 的条件访问权限。 请参阅[使用 System Center Configuration Manager 保护数据和站点基础结构](../../../protect/understand/protect-data-and-site-infrastructure.md)和[在 System Center Configuration Manager 中管理对服务的访问权限](../../../protect/deploy-use/manage-access-to-services.md)。  

 **符合性设置**  

 提供一组工具和资源，这些工具和资源可帮助你在企业中评估、跟踪和修正客户端设备的配置符合性。 此外，你还可以使用符合性设置来配置你管理的设备上的一系列功能和安全设置。 请参阅[使用 System Center Configuration Manager 确保设备的合规性](../../../compliance/understand/ensure-device-compliance.md)。  

 **Endpoint Protection**  

 提供针对企业中的计算机的安全性、反恶意软件和 Windows 防火墙管理。 请参阅 [System Center Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

 **清单**  

 提供一组工具以帮助确定和监视资产：  

-   **硬件清单**：收集有关企业中的设备硬件的详细信息。 请参阅 [System Center Configuration Manager 中的硬件清单简介](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md)。  

-   **软件清单**：收集和报告有关存储在组织中客户端计算机上的文件的信息。 请参阅 [System Center Configuration Manager 中的软件清单简介](../../../core/clients/manage/inventory/introduction-to-software-inventory.md)。  

-   **资产智能**：提供工具以收集清单数据，并监视企业中的软件许可证使用情况。 请参阅 [System Center Configuration Manager 中的资产智能简介](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)。  

**使用 Microsoft Intune 进行移动设备管理**  

 Configuration Manager 可用于通过 Internet 使用 Microsoft Intune 服务来管理 iOS、Android（包括 Samsung KNOX 标准版）、Windows Phone 和 Windows 设备。

 尽管你使用 Intune 服务，但管理任务也可通过使用服务连接点站点系统角色（可通过 Configuration Manager 控制台获得）完成。 请参阅[使用 System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)。  

 **本地移动设备管理**  

 使用本地 Configuration Manager 基础结构和内置于设备平台的管理功能（而不是依靠单独安装的 Configuration Manager 客户端）注册、管理电脑和移动设备。 当前支持管理 Windows 10 企业版和 Windows 10 移动版设备。 请参阅[在 System Center Configuration Manager 中使用本地基础结构管理移动设备](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

 **操作系统部署**  

 提供工具以创建操作系统映像。 随后可使用这些映像通过 PXE 启动或可启动媒体（例如 CD 集、DVD 或 USB 闪存驱动器）将操作系统部署到计算机。 请注意，这适用于 Configuration Manager 管理的计算机，以及不受管理的计算机。 请参阅 [System Center Configuration Manager 中的操作系统部署简介](../../../osd/understand/introduction-to-operating-system-deployment.md)。  

 **电源管理**  

 提供一组工具和资源，你可以使用这些工具和资源来管理和监视企业中的客户端计算机的功耗。 请参阅 [System Center Configuration Manager 中的电源管理简介](../../../core/clients/manage/power/introduction-to-power-management.md)。  

 **查询**  

 提供工具以检索有关层次结构中的资源的信息，以及有关清单数据和状态消息的信息。 可以使用此信息为软件部署及配置设置报告或定义设备或用户的集合。 请参阅 [System Center Configuration Manager 中的查询简介](../../../core/servers/manage/introduction-to-queries.md)。  

 **远程连接配置文件**  

 提供了一组工具和资源，帮助你为组织中的设备创建、部署和监视远程连接设置。 通过部署这些设置，你可以最大程度地减少用户连接到公司网络上他们的计算机所需的工作。 请参阅[在 System Center Configuration Manager 中使用远程连接配置文件](/sccm/compliance/deploy-use/create-remote-connection-profiles)。  

 **用户数据和配置文件配置项目**  

 Configuration Manager 中的用户数据和配置文件配置项目可为层次结构中的用户管理运行 Windows 8 和更高版本的计算机上的文件夹重定向、脱机文件和漫游配置文件。 请参阅[使用 System Center Configuration Manager 中的用户数据和配置文件配置项目](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)。  

 **远程控制**  

 提供工具以通过远程方式从 Configuration Manager 控制台中管理客户端计算机。 请参阅 [System Center Configuration Manager 中的远程控制简介](../../../core/clients/manage/remote-control/introduction-to-remote-control.md)。  

 **报表**  

 提供一组工具和资源，这些工具和资源帮助你从 Configuration Manager 控制台中使用 SQL Server Reporting Services 的高级报表功能。 请参阅 [System Center Configuration Manager 中的报告简介](../../../core/servers/manage/introduction-to-reporting.md)。  

 **软件计数**  

 提供工具以监视和收集 Configuration Manager 客户端中的软件使用情况数据。 请参阅[在 System Center Configuration Manager 中使用软件计数监视应用使用情况](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

 **软件更新**  

 提供一组工具和资源，这些工具和资源可帮助你在企业中管理、部署和监视软件更新。 请参阅 [System Center Configuration Manager 中的软件更新简介](/sccm/sum/understand/software-updates-introduction)。  
