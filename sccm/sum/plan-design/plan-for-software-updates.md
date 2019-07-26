---
title: 规划软件更新
titleSuffix: Configuration Manager
description: 在 Configuration Manager 生产环境中使用软件更新之前，软件更新点架构规划至关重要。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/19/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce5a80b99149d31282036b33b97b57294ab38663
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340472"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>在 Configuration Manager 中规划软件更新

*适用范围：System Center Configuration Manager (Current Branch)*

在 Configuration Manager 生产环境中使用软件更新之前，请务必完成规划过程。 很好地规划软件更新点基础结构对于成功的软件更新实现十分关键。



## <a name="capacity-planning-recommendations-for-software-updates"></a>软件更新的容量规划建议  

本部分包含以下细分主题：  
- [软件更新点的容量规划](#BKMK_SUMCapacity)
- [软件更新对象的容量规划](#bkmk_sum-capacity-obj)  


使用以下建议作为基线。 此基线可帮助你确定适合于你的组织的软件更新容量计划相关信息。 实际容量要求可能与本文中所列的建议有所不同，具体取决于以下条件： 
- 特定的网络环境
- 用于托管软件更新点站点系统的硬件
- 受管客户端的数量
- 服务器上安装的其他站点系统角色  


###  <a name="BKMK_SUMCapacity"></a> 软件更新点的容量规划  

支持的客户端数量取决于在软件更新点上运行的 Windows Server Update Services (WSUS) 的版本。 还取决于软件更新点站点系统角色是否与另一站点系统角色共存：  

-   当 WSUS 在软件更新点服务器上运行，并且软件更新点与另一站点系统角色共存时，软件更新点可支持多达 25,000 个客户端。  

-   当远程服务器满足 WSUS 要求、WSUS 与 Configuration Manager 配合使用，并且你配置了下述设置时，软件更新点可支持多达 150,000 个客户端：

    IIS 应用程序池：
    - 将 WsusPool 队列长度增加到 2000
    - 将 WsusPool 专用内存限制增加 4 倍，或设置为 0（无限制）。 例如，如果默认限制是 1,843,200 KB，则将其增加到 7,372,800。 有关详细信息，请参阅 [Configuration Manager 支持团队博客文章](https://blogs.technet.microsoft.com/configurationmgr/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/)。  

    要详细了解软件更新点的硬件要求，请参阅[推荐的站点系统硬件](/sccm/core/plan-design/configs/recommended-hardware#bkmk_ScaleSieSystems)。  


### <a name="bkmk_sum-capacity-obj"></a>软件更新对象的容量规划  

使用下列容量信息来规划软件更新对象：  

#### <a name="limit-of-1000-software-updates-in-a-deployment"></a>部署中 1000 个软件更新的限制  
将每个软件更新部署的软件更新数量限制为 1000 个。 创建自动部署规则 (ADR) 时，指定限制软件更新数量的条件。 如果指定的条件返回超过 1000 个软件更新时，ADR 失效。 在 Configuration Manager 控制台中的“自动部署规则”节点上查看 ADR 的状态  。 手动部署软件更新时，选择进行部署的更新不能超过 1000 个。  

配置基线中的软件更新数量也限制为 1000。 有关详细信息，请参阅[创建配置基线](/sccm/compliance/deploy-use/create-configuration-baselines)。



##  <a name="BKMK_SUPInfrastructure"></a> 确定软件更新点基础结构  

本部分包含以下细分主题：    
- [软件更新点列表](#BKMK_SUPList)
- [软件更新点切换](#BKMK_SUPSwitching)
- [将客户端手动切换到新的软件更新点](#BKMK_ManuallySwitchSUPs)
- [不受信任林中的软件更新点](#BKMK_SUP_CrossForest)
- [使用现有的 WSUS 服务器作为顶级站点中的同步源](#BKMK_WSUSSyncSource)
- [辅助站点上的软件更新点](#BKMK_SUPSecSite)  
- [基于 Internet 的客户端规划](#bkmk_internet-clients)  
- [规划软件更新内容](#bkmk_content)  
- [第三方更新计划](#bkmk_thirdparty)  


管理中心站点和所有子主站点必须有一个软件更新点。 规划软件更新点架构时，请确定以下依赖项：
- 在何处安装站点软件更新点  
- 哪些站点需要接受来自基于 Internet 的客户端通信的软件更新点
- 是否需要辅助站点的软件更新点  

> [!IMPORTANT]  
>  要详细了解软件更新所需的内部和外部依赖项，请参阅[软件更新的先决条件](prerequisites-for-software-updates.md)。  

在 Configuration Manager 主站点上添加多个软件更新点以提供容错。 软件更新点的故障转移设计与管理点设计中使用的纯随机化模型不同。 与管理点设计不同，当客户端切换到新的软件更新点时，软件更新点设计中存在客户端和网络性能成本。 当客户端切换到新的 WSUS 服务器来扫描软件更新时，将会使目录大小增加，并产生关联的客户端和网络性能需求。 因此，客户端将保留与其成功扫描的最后一个软件更新点的关联。  

你在主站点上安装的第一个软件更新点是在主站点上添加的所有其他软件更新点的同步源。 添加了软件更新点并开始同步后，从“监视”工作区的“软件更新点同步状态”节点中查看软件更新点和同步源的状态   。  

软件更新点未能配置为站点的同步源时，请手动删除失败的角色。 然后选择新的软件更新点用作同步源。 有关详细信息，请参阅[删除软件更新点站点系统角色](../get-started/remove-a-software-update-point.md)。  


###  <a name="BKMK_SUPList"></a> 软件更新点列表  

Configuration Manager 在下列情况下为客户端提供软件更新点列表：  

- 新的客户端接收启用软件更新的政策  

- 客户端无法联系其分配的软件更新点且需要切换到另一个更新点  

客户端从列表中随机选择一个软件更新点。 优先考虑同一林中的软件更新点。 Configuration Manager 根据客户端的类型向客户端提供不同的列表：  

-   **基于 Intranet 的客户端**：接收可配置为仅允许来自 Intranet 连接的软件更新点列表，或接收允许 Internet 和 Intranet 客户端连接的软件更新点列表。  

-   **基于 Internet 的客户端**：接收配置为仅允许来自 Internett 连接的软件更新点列表，或接收允许 Internet 和 Intranet 客户端连接的软件更新点列表。  


###  <a name="BKMK_SUPSwitching"></a> 软件更新点切换  

> [!NOTE]  
> 客户端使用边界组来查找新的软件更新点。 如果无法再访问其当前软件更新点，则客户端还会使用边界组回退并查找新的更新点。 添加单个软件更新点到不同的边界组，以控制客户端可找到的服务器。 有关详细信息，请参阅[软件更新点](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。  

如果某站点上有多个软件更新点，且其中一个更新点失败或不再可用，则客户端将连接到其他软件更新点。 使用该新服务器时，客户端将继续扫描查找最新的软件更新。 首次向客户端分配软件更新点后，除非无法扫描，否则该客户端将一直分配给该软件更新点。  

软件更新扫描可能会失败，并出现很多不同的重试和非重试错误代码。 如果扫描失败并出现重试错误代码，则客户端将启动重试过程以在软件更新点上扫描软件更新。 导致重试错误代码的高级别情况通常是因为 WSUS 服务器不可用或暂时超负荷。 如果客户端未能扫描到软件更新，则使用以下流程：  

1.  客户端在以下时间扫描软件更新：  
    - 在计划的时间
    - 从客户端的控制面板手动运行时
    - 通过客户端通知操作从 Configuration Manager 控制台中手动运行时
    - 从 Configuration Manager SDK 方法运行时  

2.  如果扫描失败，客户端将等待 30 分钟，然后重新尝试扫描。 它将使用同一个软件更新点。  

3.  客户端每 30 分钟重试一次，至少重试 4 次。 第 4 次失败后，客户端将再等待两分钟，然后移动到列表中的下一个软件更新点。  

4.  客户端使用新的软件更新点重复此过程。 成功扫描后，客户端继续连接到新的软件更新点。  

以下列表提供了在软件更新点重试和切换方案时要考虑的其他信息：  

-   如果客户端与 Intranet 断开连接且无法扫描软件更新，则它不会切换到另一个软件更新点。 这种失败情况是意料之中的，因为客户端无法访问内部网络，也无法访问允许来自 Intranet 连接的软件更新点。 Configuration Manager 客户端确定 Intranet 软件更新点的可用性。  

-   如果在 Internet 上管理客户端，并且配置多个软件更新点以接受来自 Internet 上客户端的通信，则切换过程将遵循先前描述的标准重试过程。  

-   如果扫描过程已启动，但客户端在扫描完成之前关闭，则不会将其视为扫描失败，且不计入 4 次重试操作。  

当 Configuration Manager 收到以下任何 Windows 更新代理错误代码时，客户端将重试连接：  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

要查找错误代码的含义，请将十进制错误代码转换为十六进制，然后在 [Windows Update Agent - Error Codes Wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx)（Windows 更新代理 - 错误代码 Wiki）等网站上搜索十六进制值。例如，十进制错误代码 2149842970 等于十六进制 8024001A，它表示 WU_E_POLICY_NOT_SET，即未设置策略值。  


###  <a name="BKMK_ManuallySwitchSUPs"></a>将客户端手动切换到新的软件更新点

活动软件更新点出现问题时，请将 Configuration Manager 客户端切换到新的软件更新点。 仅当客户端从管理点接收多个软件更新点时，才会发生此更改。

> [!IMPORTANT]    
> 切换设备以使用新的服务器时，设备使用回退来查找该新服务器。 客户端在下一个软件更新扫描周期中切换到新的软件更新点。<!-- SCCMDocs#1537 -->
>
> 在开始此更改之前，请检查边界组配置，确保软件更新点位于正确的边界组中。 有关详细信息，请参阅[软件更新点](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。  
>
> 切换到新的软件更新点会产生额外的网络流量。 流量大小取决于 WSUS 配置设置，例如同步的分类和产品或使用共享 WSUS 数据库。 如果打算切换多个设备，请考虑在维护时段执行此操作。 客户端使用新的软件更新点进行扫描时，这一时间安排可减少对网络的影响。  

#### <a name="process-to-switch-software-update-points"></a>切换软件更新点的流程  
开始在设备集合上进行此更改。 一旦触发，客户端就会在下次扫描时查找另一个软件更新点。  

1.  在 Configuration Manager 控制台中，转到“资产和符合性”  工作区，并选择“设备集合”  节点。  

2.  选择目标集合。 在功能区的“主页”选项卡上的“集合”组中，单击“客户端通知”，然后单击“切换到下一个软件更新点”     。  


###  <a name="BKMK_SUP_CrossForest"></a> 不受信任林中的软件更新点  

在站点上创建一个或多个软件更新点，以支持不受信任的林中的客户端。 要添加另一个林中的软件更新点，请先在该林中安装和配置 WSUS 服务器。 然后启动向导以添加具有软件更新点站点系统角色的 Configuration Manager 站点服务器。 在向导中，配置下列设置以成功连接到不受信任林中的 WSUS：  

-   指定可访问不受信任的林中的 WSUS 服务器的站点系统安装帐户  。  

-   指定要连接到 WSUS 帐户的 WSUS 服务器连接帐户  。  

例如，你在具有两个软件更新点（SUP01 和 SUP02）的林 A 中具有主站点。 对于同一主站点，林 B 中还有两个软件更新点（SUP03 和 SUP04）。切换到下一个软件更新点时，客户端会优先考虑来自同一林的服务器。  


###  <a name="BKMK_WSUSSyncSource"></a>使用现有的 WSUS 服务器作为顶级站点中的同步源  

通常，层次结构中的顶层站点被配置为将软件更新元数据与 Microsoft 更新同步。 当组织安全策略不允许从顶级站点访问 Internet 时，请将顶级站点的同步源配置为使用现有 WSUS 服务器。 此 WSUS 服务器不在 Configuration Manager 层次结构中。 例如，你的 WSUS 服务器位于已连接到 Internet 的网络（外围网络）中，但顶级站点位于未访问 Internet 的内部网络中。 将外围网络中的 WSUS 服务器配置为软件更新元数据的同步源。 在外围网络中配置 WSUS 服务器，使用 Configuration Manager 中所需的相同条件同步软件更新。 否则，顶层站点可能无法对你期待的软件更新进行同步。 安装软件更新点时，请配置 WSUS 服务器连接帐户。 此帐户需要访问外围网络中的 WSUS 服务器。 同时请确认防火墙防允许流量通过相应的端口。 有关详细信息，请参阅[软件更新点用于同步源的端口](/sccm/core/plan-design/hierarchy/ports#BKMK_PortsSUP-WSUS)。  


###  <a name="BKMK_SUPSecSite"></a> 辅助站点上的软件更新点  

软件更新点在辅助站点上是可选的。 仅在辅助站点上安装一个软件更新点。 如果辅助站点上未安装软件更新点，则辅助站点边界内的设备将使用其所分配的主站点上的软件更新点。 通常当辅助站点中的设备与父主站点上的软件更新点之间存在受限网络带宽时，在辅助站点上安装软件更新点。 也可在主站点上的软件更新点接近容量限制时使用此配置。 在辅助站点上成功安装和配置软件更新点后，将为客户端更新站点范围的政策，并且这些客户端开始使用新的软件更新点。  


### <a name="bkmk_internet-clients"></a>基于 Internet 的客户端规划

当需要管理将流量从你的网络漫游到 Internet 的设备时，请针对如何在这些设备上管理软件更新制定相关计划。 Configuration Manager 支持向此方案应用多种技术。 根据需要使用一项或几项技术以满足组织的需求。

#### <a name="cloud-management-gateway"></a>云管理网关
在 Microsoft Azure 中创建云管理网关，并至少启用一个本地软件更新点，以允许来自基于 Internet 的客户端的流量。 当客户端漫游到 Internet 上时，会继续针对软件更新点进行扫描。 所有基于 Internet 的客户端都始终从 Microsoft 更新云服务中获取内容。 

有关详细信息，请参阅[云管理网关计划](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)。  

#### <a name="internet-based-client-management"></a>基于 Internet 的客户端管理
将软件更新点置于面向 Internet 的网络中，并启用该更新点，以允许来自基于 Internet 的客户端的流量。 当客户端漫游到 Internet上时，它们将切换到此软件更新点进行扫描。 所有基于 Internet 的客户端都始终从 Microsoft 更新云服务中获取内容。

要详细了解基于 Internet 的客户端管理的优缺点，请参阅[在 Internet 上管理客户端](/sccm/core/clients/manage/manage-clients-internet)。

#### <a name="windows-update-for-business"></a>Windows Update for Business
借助适用于企业的 Windows 更新，可让 Windows 10 设备始终保持最新质量和功能更新。 这些设备直接连接到 Windows 更新云服务。 Configuration Manager 能够区分使用 WUfB 和 WSUS 来获取软件更新的 Windows 10 计算机。

有关详细信息，请参阅 [与适用于企业的 Windows 更新集成](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)。


### <a name="bkmk_content"></a>规划软件更新内容

客户端需要下载软件更新的内容文件才能安装它们。 Configuration Manager 提供了多种技术来支持此内容的管理和交付。 此外，可配置软件更新部署，从而允许或要求客户端直接从 Microsoft 更新云服务中获取内容。

#### <a name="download-and-distribute-content"></a>下载并分发其内容 
Configuration Manager 中的软件更新管理过程默认使用内置的内容管理功能。 这些功能包括集中式的单实例存储内容库以及分发点站点系统角色的分布式设计。 下载和分发软件更新部署包时将使用这些功能。 

有关详细信息，请参阅[下载软件更新](/sccm/sum/deploy-use/download-software-updates)。

#### <a name="manage-express-installation-files-for-windows-10"></a>管理 Windows 10 的快速安装文件
Configuration Manager 支持使用 Windows 10 更新的快速安装文件。 快速更新文件和支持技术（例如传递优化）可帮助降低将大型内容文件下载到客户端时出现的网络影响。 

有关详细信息，请参阅[优化 Windows 10 更新传递](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)。

#### <a name="clients-download-content-from-the-internet"></a>客户端从 Internet 下载内容
将软件更新部署到客户端时，请配置部署，使客户端从 Microsoft 更新云服务下载内容。 当客户端无法从另一内容源下载内容时，它们仍可以从 Internet 下载内容。 

自 1806 版本起，无需在部署软件更新时创建部署包。 如果你选择“无部署包”  选项，客户端仍可从本地源下载内容（若有），但通常是从 Microsoft 更新服务下载内容。<!--1357933-->

基于 Internet 的客户端始终从 Microsoft 更新云服务中下载内容。 请不要将软件更新部署包分发到云分发点。 使用云分发点存储需要付费，但客户端不会下载这些包。 


### <a name="bkmk_thirdparty"></a>第三方更新计划
Configuration Manager 与 WSUS 集成，后者本身支持 Microsoft 发布的软件更新。 大多数客户使用的其他第三方应用程序也需要更新。 要使第三方应用程序保持最新状态，可考虑以下几种选项。

#### <a name="supersede-applications-to-update"></a>取代应用程序实现更新
使用与 Configuration Manager 中的应用程序管理功能的取代关系来升级或替换现有应用程序。 取代应用程序时，请指定新的部署类型来替换被取代应用程序的部署类型。 还需确定是否要在安装取代应用程序之前升级或卸载被取代的应用程序。

有关详细信息，请参阅 [修改和取代应用程序](/sccm/apps/deploy-use/revise-and-supersede-applications)。

#### <a name="third-party-software-updates"></a>第三方软件更新
自版本 1806 起，可使用 Configuration Manager 控制台中的“第三方软件更新目录”  节点来订阅第三方目录、将更新发布到软件更新点，以及将它们部署到客户端。<!--1352101-->

有关详细信息，请参阅[软件更新](/sccm/sum/deploy-use/third-party-software-updates)。

#### <a name="system-center-updates-publisher"></a>System Center Updates Publisher
System Center Updates Publisher (SCUP) 是一款独立工具，可方便独立软件供应商或业务线应用程序开发人员管理自定义更新。 这些更新包括具有依赖项（例如驱动程序和更新捆绑）的更新。

有关详细信息，请参阅 [System Center Updates Publisher](/sccm/sum/tools/updates-publisher)。



##  <a name="BKMK_SUPInstallation"></a>规划软件更新点安装  

本部分包含以下细分主题：  
- [软件更新点的要求](#BKMK_SUPSystemRequirements)
- [规划 WSUS 安装](#BKMK_PlanningForWSUS)
- [配置防火墙](#BKMK_ConfigureFirewalls)  


本部分介绍了成功规划和准备软件更新点安装的相关步骤。 在 Configuration Manager 中为软件更新点创建站点系统角色之前，需考虑几项要求。 具体要求由 Configuration Manager 架构而定。 配置软件更新点，使其通过使用 HTTPS 进行通信时，请务必查看此部分。 已启用 HTTPS 的服务器需要其他步骤才能正常工作。  

###  <a name="BKMK_SUPSystemRequirements"></a> 软件更新点的要求  

在满足 WSUS 的最低要求且具备 Configuration Manager 站点系统支持的配置的站点系统上安装软件更新点角色。  

-   要详细了解针对 Windows Server WSUS 服务器角色的最低要求，请参阅[查看注意事项和系统要求](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#11-review-considerations-and-system-requirements)。  

-   有关 Configuration Manager 站点系统支持的配置的详细信息，请参阅[站点和站点系统先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。  


###  <a name="BKMK_PlanningForWSUS"></a> 规划 WSUS 安装  

在为软件更新点角色配置的所有站点系统服务器上安装受支持的 WSUS 版本。 如果未在站点服务器上安装软件更新点，则请在站点服务器上安装 WSUS 管理控制台。 站点服务器可通过此组件与软件更新点上运行的 WSUS 通信。  

在 Windows Server 2012 或更高版本上使用 WSUS 时，请配置其他权限，让 Configuration Manager 中的 WSUS Configuration Manager 组件能够连接到 WSUS  。 此组件定期执行运行状况检查。 请选择下述某个选项来配置所选权限：  

-   将“SYSTEM”  帐户添加到“WSUS 管理员”  组  

-   添加“NT AUTHORITY\SYSTEM”帐户作为 WSUS 数据库 (SUSDB) 的用户  。 配置最低限度的 webService 数据库角色成员身份。  
  
要详细了解如何在 Windows Server 上安装 WSUS，请参阅[安装 WSUS 服务器角色](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role)。  

在主站点上安装多个软件更新点时，请为同一 Active Directory 林中的每个软件更新点使用同一 WSUS 数据库。 在客户端切换到新的软件更新点时，共享同一个数据库可提高性能。 有关详细信息，请参阅[为软件更新点使用共享的 WSUS 数据库](/sccm/sum/plan-design/software-updates-best-practices#bkmk_shared-susdb)。  


####  <a name="BKMK_CustomWebSite"></a>配置 WSUS 以使用自定义网站  
在安装 WSUS 时，可以选择使用现有的 IIS 默认网站或创建自定义的 WSUS 网站。 为 WSUS 创建自定义网站，使 IIS 在专用虚拟网站中托管 WSUS 服务。 否则，它将共享由其他 Configuration Manager 站点系统或应用程序使用的同一网站。 在站点服务器上安装软件更新点角色时，尤其需要此配置。 在 Windows Server 2012 或更高版本中运行 WSUS 时，WSUS 默认配置为对 HTTP 使用端口 8530，对 HTTPS 使用端口 8531。 在站点上创建软件更新点时，请指定这些端口设置。  


####  <a name="BKMK_WSUSInfrastructure"></a> 使用现有的 WSUS 基础结构  
安装 Configuration Manager 之前，请选择在环境中处于活动状态的 WSUS 服务器作为软件更新点。 配置软件更新点后，请指定同步设置。 Configuration Manager 连接至在软件更新点服务器运行的 WSUS 服务器并使用相同设置配置 WSUS。 

在将服务器配置为软件更新点之前，请将其产品和分类的配置与 Configuration Manager 设置进行比较。 如果在将现有 WSUS 服务器配置为软件更新点之前同步该服务器，并且产品列表和分类列表不相同，则无论配置的设置如何，它都会同步所有软件更新元数据。 此行为将导致站点数据库中出现意外的软件更新元数据。 

直接在 WSUS 管理控制台中添加产品或分类然后立即启动同步时，你将遇到相同的行为方式。 默认情况下，Configuration Manager 每小时连接到 WSUS 一次并重置在 Configuration Manager 之外修改的任何设置。 与你在同步设置中指定的产品和分类不符的软件更新将设置为“已过期”。 然后，其将从站点数据库中删除。  

将 WSUS 服务器配置为软件更新点之后，即无法再将其用作独立的 WSUS 服务器。 如果需要非 Configuration Manager 托管的单个独立 WSUS 服务器，请在其他服务器上进行配置。  

####  <a name="BKMK_WSUSAsReplica"></a> 将 WSUS 配置为副本服务器  
在主站点服务器上添加软件更新点角色时，无法使用配置为副本的 WSUS 服务器。 将 WSUS 服务器配置为副本后，Configuration Manager 无法配置 WSUS 服务器，且 WSUS 同步失败。 在主站点中安装的第一个软件更新点为默认的软件更新点。 站点中的其他软件更新点被配置为默认软件更新点的副本。  

####  <a name="BKMK_WSUSandSSL"></a> 决定是否将 WSUS 配置为使用 SSL  
使用 SSL 协议帮助保护软件更新点。 WSUS 使用 SSL 向 WSUS 服务器验证客户端计算机和下游 WSUS 服务器的身份。 WSUS 还使用 SSL 来加密软件更新元数据。 选择使用 SSL 保护 WSUS 时，请在安装软件更新点之前准备 WSUS 服务器。 有关详细信息，请参阅在 WSUS 文档中的[在 WSUS 服务器上配置 SSL](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) 一文。 

在安装和配置软件更新点时，请选择“为 WSUS 服务器启用 SSL 通信”选项  。 否则，Configuration Manager 会将 WSUS 配置为不使用 SSL。 在软件更新点上启用 SSL 时，还要在子站点上配置任意软件更新点来使用 SSL。  


###  <a name="BKMK_ConfigureFirewalls"></a> 配置防火墙  

Configuration Manager 管理中心站点上的软件更新点与软件更新点上的 WSUS 进行通信。 WSUS 与同步源通信以同步软件更新元数据。 子站点上的软件更新点与父站点上的软件更新点进行通信。 当主站点中有多个软件更新点时，附加的软件更新点将与默认软件更新点进行通信。 默认角色是站点上安装的第一个软件更新点。  

可能需要配置防火墙，使其允许 WSUS 在以下情况中使用的 HTTP 或 HTTPS 流量： 
- 软件更新点与 Internet 之间
- 软件更新点与其上游同步源之间
- 在附加的软件更新点之间  

至 Microsoft 更新的连接始终配置为针对 HTTP 使用端口 80，针对 HTTPS 使用端口 443。 对于从子站点软件更新点上的 WSUS 到父站点软件更新点上的 WSUS 的连接，请使用自定义端口。 如果安全策略禁止此连接，请使用导出和导入同步方法。 有关详细信息，请参阅本文中的[同步源](#BKMK_SyncSource)部分。 要详细了解 WSUS 使用的端口，请参阅[如何确定 Configuration Manager 中 WSUS 使用的端口设置](../get-started/install-a-software-update-point.md#wsus-settings)。  


#### <a name="restrict-access-to-specific-domains"></a>限制对特定域的访问  

如果组织使用防火墙或代理设备限制与 Internet 的网络通信，你必须允许活动软件更新点访问 Internet 终结点。 WSUS 和自动更新可以与 Microsoft 更新云服务进行通信。

有关详细信息，请参阅 [Internet 访问要求](/sccm/core/plan-design/network/internet-endpoints#bkmk_sum)。


##  <a name="BKMK_SyncSettings"></a> 规划同步设置  

本部分包含以下细分主题：  
- [同步源](#BKMK_SyncSource)
- [同步计划](#BKMK_SyncSchedule)
- [更新分类](#BKMK_UpdateClassifications)
- [产品](#BKMK_UpdateProducts)
- [取代规则](#BKMK_SupersedenceRules)
- [语言](#BKMK_UpdateLanguages)  


Configuration Manager 中的软件更新同步会根据所配置的条件下载软件更新元数据。 层次结构中的顶级站点会同步 Microsoft 更新中的软件更新。 你可以选择将顶层站点上的软件更新点配置为与不在 Configuration Manager 层次结构中的现有 WSUS 服务器同步。 子主站点从管理中心站点上的软件更新点同步软件更新元数据。 安装和配置软件更新点之前，请使用本部分规划同步设置。  


###  <a name="BKMK_SyncSource"></a> 同步源  

软件更新点的同步源设置可指定软件更新点在何处检索到软件更新元数据。 它还指定同步过程是否创建 WSUS 报告事件。  

-   **同步源**：顶级站点的软件更新点默认配置 Microsoft 更新的同步源。 你可以选择将顶层站点与现有的 WSUS 服务器同步。 子主站点上的软件更新点会将同步源配置为管理中心站点中的软件更新点。  

    -  在主站点中安装的第一个软件更新点为默认的软件更新点，并且会与管理中心站点同步。 主站点中的其他软件更新点与主站点中的默认软件更新点同步。  

    - 当软件更新点与 Microsoft 更新或上游更新服务器断开连接时，请配置同步源，使其不与已配置的同步源进行同步。 转而，请将其配置为使用 WSUSUtil 工具的导出和导入功能来同步软件更新  。 有关详细信息，请参阅[从断开连接的软件更新点中同步软件更新](../get-started/synchronize-software-updates-disconnected.md)。  

-   **WSUS 报告事件**：客户端计算机上的 Windows 更新代理可为 WSUS 报告创建事件消息。 Configuration Manager 不使用这些事件。 因此，默认选中“不创建WSUS报告事件”选项  。 如果未创建这些事件，客户端应仅在软件更新评估和符合性扫描期间连接到 WSUS 服务器。 如果在 Configuration Manager 之外进行报告需要这些事件，请修改此设置以创建 WSUS 报告事件。  


###  <a name="BKMK_SyncSchedule"></a> 同步计划  

仅在 Configuration Manager 层次结构中顶级站点的软件更新点上配置同步计划。 配置同步计划后，软件更新点会在你指定的日期和时间与同步源同步。 借助自定义计划，你可同步软件更新来优化环境。 请注意 WSUS 服务器、站点服务器和网络的性能需求。 例如，每周在凌晨 2:00 同步一次。 或者，通过使用 Configuration Manager 控制台中“所有软件更新”或“软件更新组”节点的“同步软件更新”操作，在顶级站点上手动启动同步    。  

> [!TIP]  
>  使用适合你环境的时间来安排软件更新同步进行运行。 一种常见的方案是将同步计划设置为在每月第二个星期二的 Microsoft 常规软件更新发布后不久运行。 这一天通常被称为“周二补丁日”  。 如果使用 Configuration Manager 提供 Endpoint Protection 和 Windows Defender 定义及引擎更新，请考虑将同步计划设置为每天运行一次。  

软件更新点同步成功后，它向子站点发送同步请求。 如果主站点中有其他软件更新点，则向每个软件更新点发送一个同步请求。 此过程在层次结构中的每个站点上重复发生。  


###  <a name="BKMK_UpdateClassifications"></a> 更新分类  

每个软件更新都是利用更新分类定义的，此分类能帮助组织不同的更新类型。 同步过程中，站点会同步指定类别的元数据。 

Configuration Manager 支持同步以下更新类别：  

-   **关键更新**：针对特定问题的广泛发布的更新，解决与安全性无关的关键错误。  

-   **定义更新**：对病毒或其他定义文件的更新。  

-   **功能包**：在产品版本之外分发的新的产品功能，通常包含在下一个完整产品版本中。  

-   **安全更新**：广泛发布的更新，针对产品特定的与安全相关的问题。  

-   **服务包**：一组应用于 OS 或应用程序的累积修补程序。 这些修补程序包含安全更新、关键更新和软件更新等。  

-   **工具**：可帮助完成一项或多项任务的实用程序或功能。  

-   **更新汇总**：一组打包在一起便于部署的累积修复程序。 这些修补程序包含安全更新、关键更新和软件更新等。 更新汇总通常解决特定领域的问题，例如安全性或产品组件问题。  

-   **更新**：针对当前安装的应用程序或文件的更新。  

-   **升级**：新版 Windows 10 的功能更新。  

仅在顶级站点上配置更新分类设置。 未在子站点的软件更新点上配置更新分类设置，理由是软件更新元数据是从顶级站点复制的。 选择更新分类时，请注意，你选择的分类越多，同步软件更新元数据所需的时间越长。  

> [!WARNING]  
>  最佳做法是，在首次同步之前清除所有分类。 初始同步后，请选择所需的分类，然后重新运行同步。  


###  <a name="BKMK_UpdateProducts"></a> 产品  

每个软件更新的元数据都定义了更新适用的一个或多个产品。 产品是 OS 或应用程序的特定版本， 例如 Microsoft Windows 10 产品。 产品系列是指从中派生单个产品的基本 OS 或应用程序。 例如 Microsoft Windows 是一个产品系列，Windows 10 和 Windows Server 2016 是其中的成员。 可选择一个产品系列，也可选择产品系列中的单个产品。  

当软件更新适用于多个产品，且至少选中其中一个产品进行同步时，所有产品都将在 Configuration Manager 控制台中显示，即使未选中某些产品也是如此。 例如，只选择了 Windows Server 2012 产品。 如果软件更新适用于 Windows Server 2012 和 Windows Server 2012 Datacenter Edition，则这两个产品都位于站点数据库中。  

仅在顶级站点上配置产品设置。 子站点的软件更新点上不配置产品设置，原因是已从顶级站点复制软件更新元数据。 选择的产品越多，同步软件更新元数据所需的时间就越长。  

> [!IMPORTANT]  
>  Configuration Manager 存储一个包含产品和产品系列的列表，你可在首次安装软件更新点时从中进行选择。 在完成同步之前，可能无法选择在 Configuration Manager 发布后发布的产品和产品系列。 同步进程会更新可供选择的可用产品和产品系列的列表。 请在首次同步软件更新之前清除所有产品。 初始同步后，请选择所需的产品，然后重新运行同步。  


###  <a name="BKMK_SupersedenceRules"></a> 取代规则  

通常，取代另一个软件更新的软件更新执行下列一项或多项操作：  

-   增强、改进或更新由以前发布的一个或多个更新提供的修补程序。  

-   提升被取代的更新文件包的效率；如果更新已获准安装，则该文件包安装在客户端上。 例如，在被取代的更新中，某些文件可能不再与修补程序或新更新支持的操作系统相关联。 这些文件不包含在更新的取代文件包中。  

-   更新产品的较新版本。 换句话说，它将更新不再适用于产品的较旧版本或配置的版本。 如果进行了修改来扩展语言支持，则更新还可能取代其他更新。 例如，稍后对 Microsoft Office 产品更新进行的修订可能会删除对旧操作系统的支持，但可能会在初始更新版本中添加对新语言的额外支持。  

在软件更新点的属性中，指定被取代的软件更新立即过期。 此设置可防止它们被包含在新的部署中。 它还会标记现有部署，指示它们包含一个或多个过期的软件更新。 或者，请指定被取代的软件更新的有效期。 此操作可让你继续部署这些更新。 

考虑你可能需要部署被取代软件更新的以下情况：  

-   取代的软件更新仅支持较新版本的操作系统。 某些客户端计算机运行早期版本的操作系统。  

-   与所取代的软件更新相比，取代的软件更新在适用性方面受到更多限制。 此行为将导致它不适用于某些客户端。  

-   如果禁止在生产环境中部署取代的软件更新。  

    > [!NOTE]  
    > - 在 Configuration Manager 1806 版之前，当 Configuration Manager 将被取代的软件更新设置为“已过期”时，不会在 WSUS 中将该更新设置为“已拒绝”   。 客户端继续扫描已过期的更新，直到手动或通过自定义脚本拒绝更新。  自 Configuration Manager 1806 版之后，Configuration Manager 还会拒绝 WSUS 中被取代的更新。 有关 WSUS 清除任务的详细信息，请参阅[软件更新维护](/sccm/sum/deploy-use/software-updates-maintenance)。
    > - 从 Configuration Manager 版本1810开始, 你可以将**功能更新**的取代规则行为与**非功能更新**分开指定。

###  <a name="BKMK_UpdateLanguages"></a> 语言  

可使用软件更新点的语言设置配置以下项： 
- 同步软件更新的摘要详细信息（软件更新元数据）时使用的语言  
- 为软件更新下载的软件更新文件语言  

#### <a name="software-update-file"></a>软件更新文件  
在软件更新点的属性中为“软件更新文件”设置配置语言  。 此设置提供在站点下载软件更新时可用的默认语言。 每次下载或部署软件更新时，都请修改默认选择的语言。 在下载过程中，会将配置的语言的软件更新文件下载到部署包源位置（如果有采用所选语言的软件更新文件）。 接下来，它们将被复制到站点服务器上的内容库中。 然后，它们将分发到为包配置的分发点。  

使用环境中最常用的语言配置软件更新文件语言设置。 例如，你站点中的客户端主要对 Windows 或应用程序使用英语或日语。 该站点几乎不使用其他语言。 下载或部署软件更新时，请仅在“软件更新文件”列中选择英语和日语  。 通过此操作，你可使用部署和下载向导的“语言选择”页面上的默认设置  。 此操作还可防止下载不需要的更新文件。 请在 Configuration Manager 层次结构中的每个软件更新点上配置此设置。  

#### <a name="summary-details"></a>摘要详细信息  
在同步过程中，将采用你指定的语言为软件更新更新摘要详细信息（软件更新元数据）。 元数据提供软件更新相关信息，例如：
- 名称
- 说明
- 更新支持的产品
- 更新分类
- 文章 ID
- 下载 URL
- 适用性规则

仅在顶级站点上配置摘要详细信息设置。 子站点的软件更新点上不配置摘要详细信息，理由是软件更新元数据通过使用基于文件的复制从中央管理站点复制。 在选择摘要详细信息语言时，请仅选择环境中需要的语言。 选择的语言越多，同步软件更新元数据所花的时间就越长。 Configuration Manager 在运行 Configuration Manager 控制台的操作系统区域设置中显示软件更新元数据。 如果软件更新的本地化属性在此操作系统的区域设置中不可用，则软件更新信息以英语显示。  

> [!IMPORTANT]  
>  请选择所有必需的摘要详细信息语言。 当顶级站点的软件更新点与同步源进行同步时，所选摘要详细信息语言将确定其检索的软件更新元数据。 如果在同步运行（至少运行一次）后修改摘要详细信息语言，则只针对新的或更新的软件更新检索修改后的摘要详细信息语言的软件更新元数据。 除非对同步源上的软件更新进行了更改，否则已同步的软件更新不会使用已修改语言的新元数据进行更新。  



##  <a name="BKMK_MaintenanceWindow"></a>规划软件更新维护时段  

添加专用于软件更新安装的维护时段。 通过此操作，你可为软件更新配置常规维护时段和其他维护时段。 同时配置常规维护时段和软件更新维护时段时，客户端仅在软件更新维护时段期间安装软件更新。 

从 Configuration Manager 版本1810开始, 你可以更改此行为, 并允许在常规维护时段内安装软件更新。 有关此客户端设置的详细信息, 请参阅[软件更新客户端设置](/sccm/core/clients/deploy/about-client-settings#bkmk_SUMMaint)。

有关维护时段的详细信息，请参阅[如何使用维护时段](../../core/clients/manage/collections/use-maintenance-windows.md)。  


##  <a name="BKMK_RestartOptions"></a> 在软件更新安装之后重启 Windows 10 客户端的选项

使用 Configuration Manager 部署和安装需要重启的软件更新时，客户端会计划挂起的重启并显示重启对话框。

Configuration Manager 软件更新存在挂起的重启时，Windows 10 计算机的 Windows 电源选项中提供“更新并重启”和“更新并关闭”选项   。 使用上述任一选项后，计算机重启后不显示重启对话框。



## <a name="next-steps"></a>后续步骤
规划软件更新之后，请参阅[准备软件更新管理](../get-started/prepare-for-software-updates-management.md)。  

要详细了解如何管理 Windows 即服务，请参阅[ Configuration Manager 即服务和 Windows 即服务的基础知识](/sccm/core/understand/configuration-manager-and-windows-as-service)。
