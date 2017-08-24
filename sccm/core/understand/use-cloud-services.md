---
title: "将云服务与 Configuration Manager 结合使用 | Microsoft Docs"
description: "为 System Center Configuration Manager 预配云资源，补充本地基础结构。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 52f7c63d155d5c34f0f12e13020767dec1867dab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>将云服务用于 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 支持多个基于云的选项。 这些选项能补充本地基础结构，还有助于解决以下业务问题，如：  

-   如何管理 BYOD（通过将 Intune 用于移动设备管理）。  

-   如何向公司防火墙之外的 Intranet 上的独立客户端或资源提供内容资源（通过使用基于云的分发点）。  

-   当物理硬件不可用或未以逻辑方式放置以支持你的需求时，如何扩大基础结构（通过使用 Microsoft Azure 虚拟机）。  

尽管不一定必须在部署 Configuration Manager 之前预配云资源，但是它对于在层次结构设计规划进展太快之前理解这些选项十分有益。 使用云资源可在解决业务问题时节省金钱和时间，而这一点是本地基础结构无法做到的。  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>可与 Configuration Manager 一起使用的基于云的资源  
 由于每个选项具有不同的要求，更深入地调查每个选项可了解唯一的先决条件、限制和根据使用情况产生额外成本的可能性。  

-   有关基于云的分发点的信息，请参阅[安装基于云的分发点](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)。

-   有关 Azure 的详细信息，请参阅 MSDN 库中的 [Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965)。  

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Azure 虚拟机（用于基于云的基础结构）  
 Configuration Manager 支持使用在 Azure 虚拟机中运行的计算机，正如在物理公司网络中进行本地运行一样。 你可在以下方案中使用 Azure 虚拟机：  

-   **方案 1：**可以在虚拟机中运行 Configuration Manager，并使用它管理其他虚拟机上安装的客户端。  

-   **方案 2：**可以在虚拟机中运行 Configuration Manager，并使用它管理不在 Azure 中运行的客户端。  

-   **方案 3：**可以在虚拟机中运行不同的 Configuration Manager 站点系统角色，同时在物理公司网络（具有用于通信的相应网络连接）中运行其他角色。  

如果网络、操作系统和硬件要求适用于在物理公司网络中安装 Configuration Manager，则相同的这些要求也适用于在 Azure 中安装 Configuration Manager。  

Azure 虚拟机的使用需要一个 Azure 订阅。 根据所使用虚拟机的数量及其配置以及基于云的资源的使用计费。  

此外，Configuration Manager 站点和在 Azure 虚拟机中运行的客户端与本地安装遵循相同的许可证要求。  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Azure 服务（用于基于云的分发点）  
 可以使用 Azure 服务托管 Configuration Manager 分发点，该分发点名为调用的基于云的分发点。 可以[将基于云的分发点与 System Center Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)，连同本地分发点和 Azure 虚拟机中部署的分发点一起使用。  

 这与使用在其上部署了站点系统角色的 Azure 虚拟机不同。 基于云的分发点：  

-   在 Azure 中作为一项服务运行，而不是在虚拟机上运行。  

-   自动扩展以适应客户端的内容请求增加。  

-   支持 Internet 和 intranet 上的客户端。  

将 Azure 用于承载分发点，需要一个 Azure 订阅。 根据传入该服务和从该服务传出的数据量计费。  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune（用于移动设备管理）  
 可以将 Microsoft Intune 订阅与 Configuration Manager 集成，实现通过 Intune 服务对设备进行管理。 此集成：  

-   称为混合配置，并扩展 Configuration Manager（或 Intune，具体取决于你的观点），以支持多种设备。  

-   要求 Microsoft Intune 连接器站点系统角色。  

-   要求有一个单独的 Intune 订阅，并且对于将使用 Intune 管理的设备具有足够的许可证。  

尽管 Intune 使用 Azure，但它不要求单独配置 Azure，也不会产生 Intune 订阅成本以外的其他成本。  

### <a name="additional-configuration-manager-capabilities"></a>附加 Configuration Manager 管理功能  
 某些 Configuration Manager 功能可以连接到基于云的服务，如：  

-   Windows Server Update Services (WSUS)。  

-   用于下载 Configuration Manager 更新的 Configuration Manager 服务云。  

这些附加功能不要求用户拥有 Azure 订阅。 不必在云中设置特定的连接、证书或服务。 它们由 Configuration Manager 自动进行管理。 用户需要做的就是确保可应用的站点系统和设备能够访问基于 Internet 的 URL。  

##  <a name="BKMK_CloudSec"></a>基于云的服务的安全性  
 Configuration Manager 使用证书预配和访问 Azure 中的内容，并管理所使用的服务。 Configuration Manager 加密你存储在 Azure 中的数据，但除引入 Azure 提供的那些安全或数据控制之外，不会引入的其他安全或数据控制。  

 有关详细信息，请参阅关于不同的基于云的资源方案的详细信息。 还可以查看 Azure 安全性的以下主题：  

-   [Azure：了解 Azure 中的安全帐户管理](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Azure 安全性概述](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [在云迁移中通过安全性十字路口](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Azure 中的数据安全性（1/2 部分）](http://go.microsoft.com/fwlink/p/?LinkId=262974)  
