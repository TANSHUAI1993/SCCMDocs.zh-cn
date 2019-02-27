---
title: 设计站点层次结构
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 的可用拓扑和管理选项，以便规划站点层次结构。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74b8f7b099e906856300f5cc76b807daf894e060
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120072"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>为 Configuration Manager 设计站点层次结构

适用范围：System Center Configuration Manager (Current Branch)

在安装新的 Configuration Manager 层次结构的第一个站点之前，最好先了解：  

- Configuration Manager 的可用拓扑  

- 可用站点的类型及其彼此之间的关系  

- 每个站点类型提供的管理范围  

- 可减少需安装的站点数的内容管理选项  

然后规划一个拓扑，该拓扑能够高效地为当前业务需求提供服务，并且之后可进行扩展以管理未来的增长。  

在规划时，请考虑将其他站点添加到层次结构或独立站点的限制：  

- 在管理中心站点下安装新的主站点，这取决于层次结构[支持的主站点数](/sccm/core/plan-design/configs/size-and-scale-numbers)。  

- [扩展独立主站点以安装新的管理中心站点](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand)，以便随后安装其他主站点。  

- 在主站点下安装新的辅助站点，这取决于[主站点的支持限制](/sccm/core/plan-design/configs/size-and-scale-numbers)和整体层次结构。  

- 不能将先前安装的站点添加到现有的层次结构来合并两个独立站点。 Configuration Manager 仅支持将新站点安装到现有的站点层次结构。  


> [!NOTE]  
> 在计划安装新的 Configuration Manager 时，请熟悉[发行说明](/sccm/core/servers/deploy/install/release-notes)，其中详细说明了活动版本中的当前问题。 此发行说明适用于 Configuration Manager 的所有分支。 使用[技术预览版分支](/sccm/core/get-started/technical-preview)时，请在各个技术预览版的文档中查找特定于该分支的问题。  



##  <a name="bkmk_topology"></a>层次结构拓扑  

层次结构拓扑的范围：  

- 最简单：一个独立主站点  

- 最复杂：一组连接的主站点和辅助站点，在层次结构的顶层站点上具有管理中心站点  

在层次结构中使用的站点类型和计数的关键驱动因素通常是你必须支持的设备的类型和数量。   

### <a name="standalone-primary-site"></a>独立主站点

如果独立主站点可以支持所有设备和用户的管理，则使用该站点。 有关详细信息，请参阅[调整大小和扩展数量](/sccm/core/plan-design/configs/size-and-scale-numbers)。 如果公司的各个地理位置可由单一主站点提供服务，那么也可使用该拓扑。 若要帮助管理网络流量，可以在边界组中使用多个管理点，并使用精心规划的内容基础结构。 有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)和[内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)。  

此拓扑提供以下优点：  

- 简化管理开销  

- 简化可用资源和服务的客户端站点分配和发现  

- 消除站点之间的数据库复制可能引起的延迟  

- 用于将独立主站点扩展为包含管理中心站点的更大层次结构的选项。 此选项使你随后能够安装新的主站点来扩展部署的规模。  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>带有一个或多个子主站点的管理中心站点 

当需要多个主站点支持所有设备和用户的管理时，可使用此拓扑。 当需要使用多于一个主站点时需要。 

此拓扑提供以下优点：  

- 最多支持 25 个主站点，这样能够扩展层次结构的规模。    

- 始终使用管理中心站点（除非重新安装站点）。 此选项是永久性的。 不能分离子主站点而将其变为独立主站点。  



##  <a name="BKMK_ChooseCAS"></a>确定何时使用管理中心站点  

使用管理中心站点配置层次结构范围设置，以及监视层次结构中的所有站点和对象。 此站点类型不直接管理客户端。 它可协调站点到站点的数据复制，其中包括整个层次结构中站点和客户端的配置。  

以下信息可帮助你决定何时安装管理中心站点：  

- 管理中心站点是层次结构中的顶层站点。  

- 在配置具有多个主站点的层次结构时，请安装管理中心站点。  

     - 如果立即需要两个或更多主站点，请先安装管理中心站点。  

     - 如果已有主站点并想随后安装管理中心站点，请[扩展独立主站点](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand)，以安装管理中心站点。  

- 管理中心站点仅支持使用主站点作为子站点。  

- 无法为管理中心站点分配客户端。  

- 管理中心站点不支持直接支持客户端的站点系统角色（例如管理点和分发点）。  

- 通过连接到管理中心站点的 Configuration Manager 控制台管理层次结构中的所有客户端并执行所有站点管理任务。 这些任务包括在子主站点或辅助站点安装管理点或其他站点系统角色。  

- 使用管理中心站点时，只能在该站点中看到层次结构中所有站点的站点数据。 此数据包括诸如清单数据和状态消息等信息。  

- 从管理中心站点配置整个层次结构中的发现操作。 从管理中心站点将发现方法指派为在各个主站点上运行。  

- 通过将不同的安全角色、安全作用域和集合分配给不同的管理用户，来管理整个层次结构中的安全性。 这些配置在层次结构中的每个站点上适用。  

- 配置复制以控制层次结构中站点之间的通信。 计划站点数据的数据库复制，以及管理用于站点之间基于文件的数据传输的带宽。  



##  <a name="BKMK_ChoosePriimary"></a>确定何时使用主站点  

使用主站点来管理客户端。 在管理中心站点下面安装主站点作为子站点，或作为新层次结构的第一个站点。 作为层次结构第一个站点的主站点将创建独立主站点。 子主站点和独立主站点均支持辅助站点。  

出于以下原因而考虑添加其他主站点：  

- 要增加设备的数目，使用单一层次结构进行管理。  

- 满足组织的管理要求。 例如，你可以在远程位置安装主站点来管理低带宽网络上的部署内容传输。  

     - 在将数据传输到分发点时，可考虑改用网络带宽限制选项。 借助此内容管理功能，便不再需要安装其他站点。  


以下信息可帮助你决定何时安装主站点：  

- 主站点可以是独立主站点或较大层次结构中的子主站点。 如果主站点是包含管理中心站点的层次结构的成员，则站点将使用数据库复制在站点之间复制数据。 除非需要支持的客户端和设备数大于单一主站点支持的数目，否则，请考虑安装独立主站点。 安装独立主站点后，如果将来需要，可以将其扩展到可向新管理中心站点报告以纵向扩展部署。  

- 主站点仅支持使用管理中心站点作为父站点。  

- 主站点仅支持使用辅助站点作为子站点，并且支持多个辅助站点。  

- 主站点负责处理为其分配的客户端中的所有客户端数据。  

- 主站点使用数据库复制与其管理中心站点直接通信。 安装新站点时会自动配置此行为。  



##  <a name="BKMK_ChooseSecondary"></a>确定何时使用辅助站点  

使用辅助站点管理跨低带宽网络的部署内容和客户端数据传输。  

你可从管理中心站点或辅助站点的直接父主站点管理辅助站点。 辅助站点连接到主站点。 若要将它们移至不同的父站点，必须先卸载它们，然后在新的主站点下将它们作为子站点重新安装。

但是，你可以在两个对等辅助站点之间进行内容路由，以便于管理部署内容的基于文件的复制。 为将客户端数据传输到主站点，辅助站点将使用基于文件的复制。 辅助站点还使用数据库复制与其父主站点进行通信。  

如果满足下列任何条件，请考虑安装辅助站点：  

- 你不需要用于管理用户的本地连接点。  

- 你需要管理指向层次结构中较低级别站点的部署内容传输。  

- 你需要管理发送到层次结构中较高级别站点的客户端信息。  

如果不希望安装辅助站点，并具有位于远程位置的客户端，请考虑使用以下选项：  

- 使用诸如 Windows BranchCache 之类的对等技术  

- 为带宽控制和计划启用分发点   

无论是否具有辅助站点都可使用这些内容管理选项。 它们有助于缩减 Configuration Manager 基础结构的大小。 有关 Configuration Manager 中内容管理选项的详细信息，请参阅[确定何时使用内容管理选项](#BKMK_ChooseSecondaryorDP)。  


以下信息帮助你决定何时安装辅助站点：  

- 如果 SQL Server 的本地实例不可用，则在站点安装过程中，辅助站点服务器会自动安装 SQL Server Express。  

- 从 Configuration Manager 控制台启动辅助站点安装，而不是直接在计算机上运行安装程序。  

- 辅助站点使用站点数据库中信息的子集。 此行为减少了 SQL 在父主站点和辅助站点之间复制的数据量。  

- 辅助站点支持将基于文件的内容路由至具有公用父主站点的其他辅助站点。  

- 辅助站点安装自动在辅助站点服务器上安装管理点和分发点站点系统角色。  



##  <a name="BKMK_ChooseSecondaryorDP"></a>确定何时使用内容管理选项  

如果你具有设在远程网络位置的客户端，请考虑使用一个或多个内容管理选项而非一个主站点或辅助站点。 以下选项通常无需安装站点：  

- Windows 10 传递优化  

- Configuration Manager 对等缓存  

- Windows BranchCache  

- 为带宽控制配置分发点  

- 将内容手动复制到分发点（预留内容）  


如果满足下列任何条件，请考虑部署分发点（而非安装另一站点）：  

- 网络带宽足以使远程位置的客户端计算机与主站点上的管理点进行通信。 客户端与管理点通信，以下载客户端策略、发送清单、报告状态和发现信息。  

- 后台智能传输服务 (BITS) 提供的带宽控制不足以满足你的网络要求。  

有关 Configuration Manager 中内容管理选项的详细信息，请参阅[内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)。  



##  <a name="bkmk_beyond"></a>除层次结构拓扑之外  

除了初始层次结构拓扑外，还需考虑以下问题：  

- 哪些站点系统角色从层次结构中的不同站点提供服务或功能？  

- 如何在基础结构中管理层次结构范围的配置和功能？  


以下常见注意事项会在单独的文章中进行介绍。 这些信息很重要，因为它们可影响层次结构设计或受层次结构设计影响：  

- 当你准备[管理计算机和设备](/sccm/core/clients/manage/manage-clients)时，请考虑设备是在本地、在云中还是包括用户拥有的设备 (BYOD)。 此外，请考虑如何管理支持多个管理选项的设备。 例如，通过 Configuration Manager 或通过与 Microsoft Intune 进行集成来管理 Windows 10 设备。 有关详细信息，请参阅[选择设备管理解决方案](/sccm/core/plan-design/choose-a-device-management-solution)。  

- 了解可用的网络基础结构可能会如何影响远程位置之间的数据流。 有关详细信息，请参阅[准备网络环境](/sccm/core/plan-design/network/configure-firewalls-ports-domains)。 同时考虑用户和设备的地理位置，以及它们是通过本地网络还是 Internet 访问你的基础结构。  

- 规划内容基础结构，以便将部署的内容高效分发到所管理的设备。 该内容可能是应用程序、软件更新或操作系统。 有关详细信息，请参阅[管理内容和内容基础结构](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)。  

- 确定计划使用的 [Configuration Manager 特性和功能](/sccm/core/plan-design/changes/features-and-capabilities)。 不同的功能需要不同的站点系统角色或 Windows 基础结构。 在多站点层次结构中，确定它们的部署位置，以便最有效地使用网络和服务器资源。  

- 考虑数据和设备的安全性，包括对公钥基础结构 (PKI) 的使用。 有关详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  


查看下列文章以了解站点特定配置：  

- [规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)  

- [规划站点数据库](/sccm/core/plan-design/hierarchy/plan-for-the-site-database)  

- [规划站点系统服务器和站点系统角色](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles)  

- [规划安全性](/sccm/core/plan-design/security/plan-for-security)  

- 当在站点内部署内容时，则为[Managing network bandwidth](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) 。  


考虑跨站点和层次结构的配置  

- 站点和层次结构的[高可用性选项](/sccm/protect/understand/high-availability-options)

- [扩展 Active Directory 架构](/sccm/core/plan-design/network/extend-the-active-directory-schema)并配置站点以[发布站点数据](/sccm/core/servers/deploy/configure/publish-site-data)  

- [站点间数据传输](/sccm/core/servers/manage/data-transfers-between-sites)  

- [基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)  

- [在 Internet 上管理客户端](/sccm/core/clients/manage/manage-clients-internet)  

