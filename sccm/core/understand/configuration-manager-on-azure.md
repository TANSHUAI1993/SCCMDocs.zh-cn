---
title: "Azure 上的 Configuration Manager | Microsoft Docs"
description: "有关在 Azure 环境中使用 Configuration Manager 的信息。"
ms.custom: na
ms.date: 03/27/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
caps.latest.revision: "2"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 5276ad999fc871496d79e6efff34d5edc6335380
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Azure 上的 Configuration Manager - 常见问题解答
*适用范围：System Center Configuration Manager (Current Branch)*

下列问题和解答可帮助了解何时使用以及如何在 Microsoft Azure 上配置 Configuration Manager。

## <a name="general-questions"></a>一般问题
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>我的公司正在尝试尽可能多地将物理服务器移动到 Microsoft Azure，我能否将 Configuration Manager 服务器移动到 Azure？
当然，支持这种方案。  请参阅[对 System Center Configuration Manager 的虚拟化环境的支持](/sccm/core/plan-design/configs/support-for-virtualization-environments)。

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>很好！ 我的环境需要多个站点。 所有子主站点是应与管理中心站点一起位于 Azure 中还是位于本地？ 辅助站点呢？
在 Azure 中托管，站点到站点通信（基于文件和数据库复制）可受益于邻近带来的便利性。 但是，所有与客户端相关的通信流会离站点服务器和站点系统较远。 如果通过不限流量计划使用快速稳定的网络连接 Azure 和 Intranet，则可以选择在 Azure 中托管所有基础结构。

但是，如果使用按流量计费的数据计划且受可用带宽或成本限制，或连接 Azure 与 Intranet 的网络较慢或不稳定，请考虑将特定站点（及站点系统）放置在本地，然后使用 Configuration Manager 中内置的带宽控件。

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>在 Azure 中设置 Configuration Manager 是否是一个 SaaS 方案（软件即服务）？
否，它是 IaaS（基础结构即服务），因为是在 Azure 虚拟机中托管 Configuration Manager 基础结构服务器。

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>当考虑将 Configuration Manager 基础结构转移到 Azure 时应考虑哪些方面？
问得好，以下是做决定时应考虑的最重要的方面，本主题分别通过不同的部分对各方面进行了探讨：
1.  网络
2.  可用性
3.  性能
4.  成本
5.  用户体验

## <a name="networking"></a>网络
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>有些什么网络要求？应使用 ExpressRoute 还是 Azure VPN 网关？
有关网络的决策是一项非常重要的决策。 网络速度和延迟会影响站点服务器和远程站点系统之间的功能以及任何客户端与站点系统之间的通信。 我们的建议是使用 ExpressRoute。 但不存在会阻止使用 Azure VPN 网关的 Configuration Manager 限制。 应仔细斟酌对此基础结构的需求（性能、修补、软件分发、操作系统部署），然后再做决定。 需要为每个解决方案考虑的事项包括：

 - **ExpressRoute**（推荐）
  - 自然地扩展到数据中心（可联接多个数据中心）
  - Azure 数据中心与基础结构之间的专用连接
  - 不使用公共 Internet
  - 提供可靠性、高速度、更低的延迟和高安全性
  - 高达 10gbps 的速度和不限流量计划选项
 - **VPN 网关**
  - 站点到站点/点到站点 VPN
  - 通信流不经过公共 Internet
  - 使用 Internet 协议安全性 (IPsec) 和 Internet 密钥交换 (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute 有多种不同的选项，如不限流量和按流量计费的选项、不同速度的选项和高级加载项。 应选择哪一种？
选择哪一种取决于要实现的方案和计划分发的数据量。 可控制站点服务器和分发点之间的 Configuration Manager 数据传输，但不能控制站点服务器到站点服务器之间的通信。   如果使用按流量计费的数据计划，则可将特定站点（以及站点系统）放置在本地，并使用 [Configuration Manager 的内置带宽控件](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)来帮助控制使用 Azure 的成本。

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>有什么安装要求（比如 Active Directory 域）？ 是否仍需要将站点服务器加入到 Active Directory 域？
是。 移动到 Azure 后，[支持的配置](/sccm/core/plan-design/configs/supported-configurations)保持不变，包括安装 Configuration Manager 时的 Active Directory 要求。

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>我了解需要将站点服务器加入到 Active Directory 域，但是否可使用 Azure Active Directory？
否，目前不支持 Azure Active Directory。 所有站点服务器仍必须为 [Windows Active Directory 域](/sccm/core/plan-design/configs/support-for-active-directory-domains)的成员。



## <a name="availability"></a>可用性
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>我打算将基础结构转移到 Azure 的原因之一是产品和服务所承诺的高可用性。 是否可利用高可用性选项，例如将用于 Configuration Manager 的 VM 的 Azure VM 可用性集？
可以！ Azure VM 可用性集可用于冗余的站点系统角色，例如分发点或管理点。

还可以将其用于 Configuration Manager 站点服务器。 例如，管理中心站点和主站点可全部位于同一可用性集中，这能帮助确保其不会同时重启。

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>如何让数据库高度可用？ 是否可以使用 Azure SQL 数据库？ 或是否必须在 VM 中使用 Microsoft SQL Server？
需在 VM 中使用 Microsoft SQL Server。 Configuration Manager 目前不支持 Azure SQL Server。 但 AlwaysOn 可用性组等功能可用于 SQL server。 从 Configuration Manager 版本 1602 开始，正式支持和推荐使用 [AlwaysOn 可用性组](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>可否将站点系统角色（如管理点或软件更新点）与 Azure 负载均衡器一起使用？
虽然未就 Configuration Manager 与 Azure 负载均衡器的配合使用进行测试，但如果该功能对该应用程序是透明的，将二者配合使用应不会影响正常操作和运行。


## <a name="performance"></a>性能
### <a name="what-factors-affect-performance-in-this-scenario"></a>此方案中，哪些因素会影响性能？
[Azure VM 大小和类型](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs)、Azure VM 磁盘（建议使用高级存储，尤其是对于 SQL Server）、网络延迟和速度是最重要的几个方面。

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>可否提供有关 Azure 虚拟机的详细信息？应使用何种大小的虚拟机？
一般情况下，计算能力（CPU 和内存）需满足[用于 System Center Configuration Manager 的推荐硬件](/sccm/core/plan-design/configs/recommended-hardware)。 但常规计算机硬件与 Azure VM 之间有些区别，尤其涉及到这些虚拟机使用的磁盘时。  使用的虚拟机的大小取决于环境的规模，这里有一些建议：
- 对于任何大规模的生产部署，建议使用“S”级 Azure VM。 这是因为这些 VM 可利用高级存储磁盘。  非“S”级 VM 使用 Blob 存储，通常不符合可接受的生产体验所需的性能要求。
- 对于较大的规模，应使用多个高级存储磁盘，并在 Windows 磁盘管理控制台中将其进行分区以获得最大 IOPS。  
- 建议在初始站点部署期间使用较好的或多个高级磁盘（如使用 P30 而不是 P20，在带区卷中使用 2 个 P30 而不是 1 个 P30）。 之后，如果站点因额外负荷需要增加 VM 的大小，则可利用较大 VM 提供的额外 CPU 和内存空间。 此外，已配置好的磁盘也可充分利用较大 VM 所允许的额外 IOPS 吞吐量。



下表列出针对各种规模的安装，建议在主站点和管理中心站点处使用的初始磁盘数：

**位于同一位置的站点数据库** - 主站点或管理中心站点的站点数据库位于站点服务器上：

| 桌面客户端    |建议的 VM 大小|建议的磁盘空间|
|--------------------|-------------------|-----------------|
|**最多 25k**       |   DS4_V2          |2xP30（带区）  |
|**25k 到 50k**      |   DS13_V2         |2xP30（带区）  |
|**50k 到 100k**     |   DS14_V2         |3xP30（带区）  |


**远程站点数据库** - 主站点或管理中心站点的站点数据库位于远程服务器上：

| 桌面客户端    |建议的 VM 大小|建议的磁盘空间 |
|--------------------|-------------------|------------------|
|**最多 25k**       | 站点服务器：F4S </br>数据库服务器：DS12_V2 | 站点服务器：1xP30 </br>数据库服务器：2xP30（带区）  |
|**25k 到 50k**      | 站点服务器：F4S </br>数据库服务器：DS13_V2 | 站点服务器：1xP30 </br>数据库服务器：2xP30（带区）   |
|**50k 到 100k**     | 站点服务器：F8S </br>数据库服务器： DS14_V2 | 站点服务器：2xP30（带区）   </br>数据库服务器：3xP30（带区）   |

下面显示了 DS14_V2 上 50k 到 100k 客户端的示例配置，其中 3xP30 磁盘位于带区卷中，Configuration Manager 安装和数据库文件具有单独的逻辑卷：![VM)disks](media/vm_disks.png)  



## <a name="user-experience"></a>用户体验
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>为什么说用户体验是非常重要的一个方面？
所做的有关网络、可用性、性能和放置 Configuration Manager 站点服务器的位置的决策会直接影响用户。 我们认为转移到 Azure 这一操作对用户应是透明的，由此确保其与 Configuration Manager 的日常交互不会发生变化。

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>好的，明白了。 我计划在 Azure 虚拟机上安装单个独立主站点，并且想要确保成本较低。 是否也应将（远程）站点系统（例如，管理点、分发点和软件更新点）放置在 Azure 虚拟机上，还是应将其放置在本地？
除了站点服务器与分发点之间的通信之外，站点中的这些服务器对服务器通信随时都可能发生，并且不使用任何机制来控制网络带宽的使用。 由于无法控制站点系统之间的通信，应考虑与这些通信相关的所有成本。

网络速度和延迟也是需要考虑的重要因素。 较慢或不稳定的网络可能会影响站点服务器和远程站点系统之间的功能以及任何客户端与站点系统之间的通信。 还应考虑使用给定站点系统的托管客户端以及用户主动使用的功能的数量。
一般情况下，可使用常规指导，因为作为起始点，它与 WAN 链接和站点系统相关。 理想情况下，所选择和所接收的 Azure 与 intranet 之间的吞吐量会与通过快速网络良好连接的 WAN 一致。

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>内容分发和内容管理呢？ 标准分发点应位于 Azure 中还是位于本地？应在本地使用 BranchCache 还是拉取分发点？ 或者，是否应以独占方式使用云分发点？
内容管理的方法与站点服务器和站点系统管理非常相似。
- 如果通过不限流量计划使用快速稳定的网络连接 Azure 和 Intranet，则可以选择在 Azure 中托管所有标准分发点。
-  如果使用按流量计费的数据计划且需考虑带宽成本，或者 Azure 与 Intranet 之间的网络连接不快或不稳定，则可以考虑其他方案。 这些方案包括在本地放置标准或拉取分发点以及使用 BranchCache。 也可以选择使用基于云的分发点，但在支持的内容类型上存在一些限制（例如，不支持软件更新包）。

> [!NOTE]
>  如果需要 PXE 支持，则必须使用本地分发点（标准或拉取）来响应启动请求。 [目前不支持在 Azure VM 上运行 WDS](https://technet.microsoft.com/library/hh831764(v=ws.11).aspx)。


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>我了解并能接受基于云的分发点的限制，但不想将管理点置于 DMZ 内，即使这是支持基于 Internet 的客户端所需的。 是否有其他选择？
可以！ 在 Configuration Manager 1610 版本中，我们引入了[云管理网关](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway)作为预发行功能。 （此功能最先出现在 Technical Preview 1606 版本中，用作[云代理服务](/sccm/core/get-started/capabilities-in-technical-preview-1606#a-namecloudproxyacloud-proxy-service-for-managing-clients-on-the-internet)）。

**云管理网关**提供一种简单的方法来管理 Internet 上的 Configuration Manager 客户端。 该服务部署到 Microsoft Azure 且需要 Azure 订阅，它使用名为云管理网关连接点的新角色连接到本地 Configuration Manager 基础结构。 部署并配置好该服务后，客户端便可以访问本地 Configuration Manager 站点系统角色，而不管它们是连接到内部专用网络还是 Internet 上。

接着可以开始在环境中使用云管理网关，并向我们提供反馈以帮助优化该服务。 有关预发行功能的信息，请参阅[使用更新中的预发行功能](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkprereleasea-use-pre-release-features-from-updates)。

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>我还听说，在版本 1610 中引入了另一个名为“对等缓存”的新功能作为预发布功能。 此功能是否与 BranchCache 不同？ 应选择哪一种？
是的，完全不同。 [对等缓存](/sccm/core/plan-design/hierarchy/client-peer-cache)是 100% 本机 Configuration Manager 技术，而 BranchCache 是 Windows 的一个功能。 两者各有各自的用途；BranchCache 使用广播来查找所需的内容，而“对等缓存”则使用 Configuration Manager 常规分发工作流和边界组设置。

可以将任何客户端配置为对等缓存源。 然后，当管理点提供有关内容源位置的客户端信息时，它们会提供分发点和任何包含客户端所需内容的对等缓存源的详细信息。


## <a name="cost"></a>成本
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>好的，请提供一些成本方面的信息。 这对我来说是划算的解决方案吗？
很难说，因为环境存在差异。 最佳办法就是使用 Microsoft Azure 定价计算器为环境估算成本： https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>其他资源
**基础知识：** http://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Azure VM 计算机类型：**
 - Azure 计算机大小：https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
 - VM 定价： http://azure.microsoft.com/pricing/details/virtual-machines/  
 - 存储定价：http://azure.microsoft.com/pricing/details/storage/

**磁盘性能注意事项：**    
 - 高级磁盘简介：http://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
 - 高级磁盘详情：http://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
 - 易于使用的最大存储大小和存储性能目标图表集：https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
 - 其他介绍 + 一些有关高级存储工作原理的超酷 uber-geek 数据： http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**可用性：**
 - Azure IaaS 正常运行时间 SLA：https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
 - 所述的可用性集：https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**连接性：**
 - Express Route 与Azure VPN：http://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
 - Express Route 定价：http://azure.microsoft.com/pricing/details/expressroute/
 - Express Route 详情：http://azure.microsoft.com/documentation/articles/expressroute-introduction/

 
