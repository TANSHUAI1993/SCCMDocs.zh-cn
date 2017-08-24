---
title: "规划软件更新 | Microsoft Docs"
description: "在 System Center Configuration Manager 生产环境中使用软件更新之前，需要规划软件更新点基础结构。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 06/27/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: 8b739a01a6bb5cacf0f7109e2e6fa3b31dd666d3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-software-updates-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中规划软件更新

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 生产环境中使用软件更新之前，需进行规划过程，这点十分重要。 很好地规划软件更新点基础结构对于成功的软件更新实现十分关键。

## <a name="capacity-planning-recommendations-for-software-updates"></a>软件更新的容量规划建议  
 你可以使用下列建议作为基准，可帮助你确定适合于你的组织的软件更新容量规划的信息。 实际容量要求可能会与本主题中列出的建议有所不同，具体取决于以下标准：你的特定网络环境、用于承载软件更新点站点系统的硬件、安装的客户端的数量，以及服务器上安装的站点系统角色。  

###  <a name="BKMK_SUMCapacity"></a> 软件更新点的容量规划  
 受支持客户端的数量取决于在软件更新点上运行的 Windows Server Update Services (WSUS) 版本，并且还取决于软件更新点站点系统角色是否与另一站点系统角色并存：  

-   当 WSUS 运行在软件更新点计算机上并且该软件更新点与另一站点系统角色并存时，软件更新点最多可支持 25,000 个客户端。  

-   在远程计算机满足 WSUS 要求、将 WSUS 与 Configuration Manager 配合使用，并进行以下配置时，软件更新点最多可支持 150,000 个客户端：

    IIS 应用程序池：
    - 将 WsusPool 队列长度增加到 2000
    - 将 WsusPool 专用内存限制增加 4 倍，或设置为 0（无限制）      

    有关软件更新点的硬件要求的详细信息，请参阅[推荐的站点系统硬件](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems)。

-   默认情况下，Configuration Manager 不支持将软件更新点配置为 NLB 群集。 在 Configuration Manager 版本 1702 之前，可以使用 Configuration Manager SDK 在 NLB 群集上配置最多 4 个软件更新点。 但是，从 Configuration Manager 版本 1702 开始，软件更新点不再作为 NLB 群集支持，并且如果检测到此配置，则会阻止升级到 Configuration Manager 版本 1702。

### <a name="capacity-planning-for-software-updates-objects"></a>软件更新对象的容量规划  
 使用下列容量信息来规划软件更新对象。  

-   **部署中 1000 个软件更新的限制**  

     你必须为每个软件更新部署将软件更新数限制为 1000。 在创建自动部署规则时，请指定一个条件，该条件限制返回的软件更新的数量。 如果指定的条件返回超过 1000 个软件更新，自动部署规则将失败。 你可以在 Configuration Manager 控制台的“自动部署规则”节点中查看自动部署规则的状态。 在手动部署软件更新时，请不要选择超过 1000 个更新进行部署。  

     还必须在配置基线中将软件更新数限制为 1000。 有关详细信息，请参阅[创建配置基线](../../compliance/deploy-use/create-configuration-baselines.md)。

##  <a name="BKMK_SUPInfrastructure"></a> 确定软件更新点基础结构  
 管理中心站点和所有子主站点必须有你将在其中部署软件更新的软件更新点。 在规划软件更新点基础结构时，你需要确定下列依赖关系：
 - 在何处安装站点软件更新点
 - 哪些站点需要接受来自基于 Internet 的客户端的通信的软件更新点
 - 是否需要在辅助站点上安装软件更新点。

使用下列部分来确定软件更新点基础结构。  

> [!IMPORTANT]  
>  有关软件更新所需的内部和外部依赖关系的信息，请参阅[软件更新的先决条件](prerequisites-for-software-updates.md)。  

 你可以在 Configuration Manager 主站点上添加多个软件更新点。 在一个站点上使用多个软件更新点的功能提供了容错能力，而无需使用复杂的 NLB。 但是，对于纯粹的负载平衡而言，你通过多个软件更新点实现的故障转移不如 NLB 可靠，然而它却是为容错设计的。 并且，软件更新点的故障转移设计与管理点设计中使用的纯粹随机化模型不同。 与管理点设计中不同，在软件更新点中，存在与切换到新软件更新点关联的客户端和网络性能开销。 当客户端切换到新的 WSUS 服务器来扫描软件更新时，将会使目录大小增加，并产生关联的客户端和网络性能需求。 因此，客户端将保留与它成功扫描的上一个软件更新点的相关性。  

 你在主站点上安装的第一个软件更新点是在主站点上添加的所有其他软件更新点的同步源。 添加了软件更新点并启动了软件更新同步后，你可以从“监视”  工作区的“软件更新点同步状态”  节点中查看软件更新点和同步源的状态。  

 当软件更新点失败，并且该软件更新点配置为站点上其他软件更新点的同步源时，你必须手动删除失败的软件更新点，并选择新的软件更新点以用作同步源。 有关如何删除软件更新点的详细信息，请参阅[删除软件更新点站点系统角色](../get-started/remove-a-software-update-point.md)。  

###  <a name="BKMK_SUPList"></a> 软件更新点列表  
 Configuration Manager 在以下方案中向客户端提供软件更新点列表：在新客户端接收策略以启用软件更新时，或在客户端无法与其软件更新点联系并需要切换到另一个软件更新点时。 客户端将随机从列表中选择一个软件更新点，并将排列位于同一林中的软件更新点的优先级。 Configuration Manager 根据客户端的类型向客户端提供不同的列表。  

-   **基于 Intranet 的客户端**：接收可配置为仅允许来自 Intranet 的连接的软件更新点的列表，或接收允许 Internet 和 Intranet 客户端连接的软件更新点的列表。  

-   “基于 Internet 的客户端”：接收配置为仅允许来自 Internett 的连接的软件更新点的列表，或接收允许 Internet 和 Intranet 客户端连接的软件更新点的列表。  

###  <a name="BKMK_SUPSwitching"></a> 软件更新点切换  
> [!NOTE]
> 从版本 1702 开始，客户端使用边界组查找新的软件更新点，并在其当前软件更新点不再可用时回退并查找新的软件更新点。 可以向不同的边界组添加各个软件更新点，以控制客户端可以找到哪些服务器。 有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)主题中的[软件更新点](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。

如果站点上有多个软件更新点，然后一个软件更新点失败或变得不可用，则客户端将连接到其他软件更新点并继续扫描最新的软件更新。 为客户端第一次分配了软件更新点后，会将该客户端一直分配给该软件更新点，除非它无法在该软件更新点上扫描软件更新。  

软件更新扫描可能会失败，并出现很多不同的重试和非重试错误代码。 如果扫描失败并出现重试错误代码，则客户端将启动重试过程以在软件更新点上扫描软件更新。 导致重试错误代码的高级别情况通常是因为 WSUS 服务器不可用或暂时超负荷。 客户端在无法扫描软件更新时将使用下列过程：  

1.  客户端按其计划的时间扫描软件更新、在其通过客户端上的控制面板启动时进行扫描，或通过使用 SDK 进行扫描。 如果扫描失败，客户端将等待 30 分钟再重试扫描，并使用相同的软件更新点。  

2.  客户端按 30 分钟的间隔至少重试四次。 第四次失败后，客户端将再等待两分钟，然后切换到软件更新点列表中的下一个软件更新点。  

3.  客户端将在新的软件更新点完成相同的过程。 成功扫描之后，客户端将继续连接到新的软件更新点。

 下面的列表提供了可为软件更新点重试和切换方案考虑的其他信息：  

-   如果客户端从公司 Intranet 断开连接并且无法扫描软件更新，它将不会切换到另一个软件更新点。 这种失败情况是意料之中的，因为客户端无法访问公司网络，也无法访问允许来自 Intranet 的连接的软件更新点。 Configuration Manager 客户端确定 Intranet 软件更新点的可用性。  

-   如果启用了基于 Internet 的客户端管理，并且有多个配置为接受来自 Internet 客户端的通信的软件更新点，则切换过程将按照前面的方案中描述的标准重试过程进行。  

-   如果扫描过程已启动，但客户端在扫描完成之前关闭，则不会将其视为扫描失败，并且不会计入四次重试之一。  

当 Configuration Manager 收到以下任何 Windows 更新代理错误代码时，将使客户端重试连接：  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

若要查找错误代码的含义，必须将十进制错误代码转换为十六进制，然后在 [Windows Update Agent - Error Codes Wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx)（Windows Update 代理 - 错误代码 Wiki）等网站搜索该十六进制值。


###  <a name="BKMK_ManuallySwitchSUPs"></a>手动将客户端切换到新的软件更新点
从 Configuration Manager 版本 1606 开始，可以启用使 Configuration Manager 客户端在活动软件更新点出现问题时切换到新软件更新点的选项。 仅当客户端从管理点接收多个软件更新点时，此选项才导致更改。

> [!IMPORTANT]    
> 切换设备以使用新的服务器时，设备使用回退来查找该新服务器。 因此，请检查你的边界组配置，并在确保软件更新点位于正确的边界组后，再开始进行此更改。 有关详细信息，请参阅[软件更新点](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。
>
> 切换到新的软件更新点会产生额外的网络流量。 流量大小取决于你的 WSUS 配置设置（更新分类、产品、软件更新点是否共享 WSUS 数据库等等）。 如果计划切换多个设备，请考虑在维护时段执行此操作，以减少同步到新的软件更新点服务器时对网络的影响。

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>启用切换软件更新点的选项  
在设备集合或一套所选设备上启用此选项。 启用后，客户端将在下次扫描时查找另一个软件更新点。

1.  在 Configuration Manager 控制台中，转到“资产和符合性”>“概览”>“设备集合”。  

2.  在“主页”选项卡上的“集合”组中，单击“客户端通知”，然后单击“切换到下一个软件更新点”。  


###  <a name="BKMK_SUP_CrossForest"></a> 不受信任林中的软件更新点  
 你可以在站点上创建一个或多个软件更新点来支持不受信任林中的客户端。 要添加另一个林中的软件更新点，你必须首先在该林中安装和配置 WSUS 服务器。 然后启动向导以添加具有软件更新点站点系统角色的 Configuration Manager 站点服务器。 在向导中，配置下列设置以成功连接到不受信任林中的 WSUS：  

-   指定可访问林中的 WSUS 服务器的站点系统安装帐户。  

-   指定要用于连接到 WSUS 服务器的 WSUS 服务器连接帐户。  

 例如，你在具有两个软件更新点（SUP01 和 SUP02）的林 A 中具有主站点。 此外，对于此相同的主站点，你在林 B 中具有两个软件更新点（SUP03 和 SUP04）。在此示例中发生切换时，与客户端在相同林中的软件更新点的优先级排在第一位。  

###  <a name="BKMK_WSUSSyncSource"></a> 使用现有的 WSUS 服务器作为顶层站点中的同步源  
 通常，层次结构中的顶层站点被配置为将软件更新元数据与 Microsoft 更新同步。 当公司安全策略不允许从顶层站点访问 Internet 时，你可以将顶层站点的同步源配置为使用不在 Configuration Manager 层次结构中的现有 WSUS 服务器。 例如，你可能在具有 Internet 访问权限的 DMZ 中安装了 WSUS 服务器，但顶层站点没有。 你可以将 DMZ 中的 WSUS 服务器配置为软件更新元数据的同步源。 你必须确保 DMZ 中的 WSUS 服务器对满足 Configuration Manager 层次结构中所需的条件的软件更新进行同步。 否则，顶层站点可能无法对你期待的软件更新进行同步。 安装软件更新点时，请配置能够访问 DMZ 中的 WSUS 服务器的 WSUS 连接帐户，并确认防火墙允许合适的端口流量。 有关详细信息，请查看[软件更新点用于同步源的端口](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS)。  

###  <a name="BKMK_NLBSUPSP1"></a> 配置为使用 NLB 的软件更新点  
 软件更新点切换可能会满足你具有的容错需求。 默认情况下，Configuration Manager 不支持将软件更新点配置为 NLB 群集。 在 Configuration Manager 版本 1702 之前，可以使用 Configuration Manager SDK 在 NLB 群集上配置最多 4 个软件更新点。 但是，从 Configuration Manager 版本 1702 开始，软件更新点不再作为 NLB 群集支持，并且如果检测到此配置，则会阻止升级到 Configuration Manager 版本 1702。 有关 Set-CMSoftwareUpdatePoint PowerShell cmdlet 的详细信息，请参阅 [Set-CMSoftwareUpdatePoint](http://go.microsoft.com/fwlink/?LinkId=276834)。

###  <a name="BKMK_SUPSecSite"></a> 辅助站点上的软件更新点  
 软件更新点在辅助站点上是可选的。 在辅助站点上安装软件更新点时，WSUS 数据库被配置为父主站点上默认软件更新点的副本。 你只能在辅助站点上安装一个软件更新点。 分配给辅助站点的设备被配置为当辅助站点上未安装软件更新点时使用父站点上的软件更新点。 通常，当分配给辅助站点的设备与父主站点上的软件更新点之间存在受限制的网络带宽时，或者当软件更新点接近容量限制时，你将在辅助站点上安装软件更新点。 在辅助站点中成功安装和配置软件更新点之后，会为分配给该站点的客户端计算机更新站点范围的策略，并且这些计算机将开始使用新软件更新点。  

##  <a name="BKMK_SUPInstallation"></a>规划软件更新点安装  
 在 Configuration Manager 中创建软件更新点站点系统角色之前，你必须根据 Configuration Manager 基础结构考虑一些要求。 将软件更新点配置为使用 SSL 进行通信时，查看本部分特别重要，因为你必须执行其他步骤，层次结构中的软件更新点才能正常工作。 本部分提供有关成功规划和准备软件更新点安装所必须执行的步骤的信息。  

###  <a name="BKMK_SUPSystemRequirements"></a> 软件更新点的要求  
 必须在满足 WSUS 的最低要求且达到 Configuration Manager 站点系统的支持配置的站点系统上安装软件更新点站点系统角色。  

-   有关针对 Windows Server 2012 中 WSUS 服务器角色的最低要求的详细信息，请参阅 Windows Server 2012 文档库中的[查看注意事项和系统要求](https://technet.microsoft.com/library/hh852344.aspx#BKMK_1.1)。  

-   有关 Configuration Manager 站点系统支持的配置的详细信息，请参阅[站点和站点系统先决条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

###  <a name="BKMK_PlanningForWSUS"></a> 规划 WSUS 安装  

软件更新要求在为软件更新点站点系统角色配置的所有站点系统服务器上安装 WSUS 的支持版本。 此外，如果你未在站点服务器上安装软件更新点，则必须在站点服务器计算机上安装 WSUS 管理控制台（如果尚未安装该控制台）。 这允许站点服务器与软件更新点上运行的 WSUS 通信。  

 在 Windows Server 2012 上使用 WSUS 时，必须将其他权限配置为允许 Configuration Manager 中的“WSUS Configuration Manager”连接到 WSUS 以执行定期运行状况检查。 选择下列选项之一以配置权限：  

-   将“SYSTEM”  帐户添加到“WSUS 管理员”  组  

-   将“NT AUTHORITY\SYSTEM”  帐户添加为 WSUS 数据库 (SUSDB) 的用户，并配置最低的 webService 数据库角色成员资格  

 有关如何在 Windows Server 2012 上安装 WSUS 的详细信息，请参阅 Windows Server 2012 文档库中的 [Install the WSUS Server Role（安装 WSUS 服务器角色）](http://go.microsoft.com/fwlink/p/?LinkId=272355) 。  

 在主站点上安装多个软件更新点时，请为同一 Active Directory 林中的每个软件更新点使用同一 WSUS 数据库。 如果共享相同的数据库，则可以极大程度地进行缓解，但不完全排除在客户端切换到新软件更新点时可能会遇到的客户端和网络性能影响。 当客户端切换到与旧软件更新点共享数据库的新软件更新点时，仍然会进行增量扫描，但与 WSUS 服务器具有其自己的数据库的情况相比，扫描工作要少得多。  

####  <a name="BKMK_CustomWebSite"></a> 配置 WSUS 以使用自定义网站  
 在安装 WSUS 时，可以选择使用现有的 IIS 默认网站或创建自定义的 WSUS 网站。 为 WSUS 创建自定义网站，以便 IIS 在专用的虚拟网站中承载 WSUS 服务，而不是共享由其他 Configuration Manager 站点系统或其他应用程序使用的同一个网站。 尤其是在站点服务器上安装软件更新点站点系统角色时。 在 Windows Server 2012 或 Windows Server 2016 中运行 WSUS 时，WSUS 被默认配置为针对 HTTP 使用端口 8530，针对 HTTPS 使用端口 8531。 在站点上创建软件更新点时，必须指定这些端口设置。  

####  <a name="BKMK_WSUSInfrastructure"></a> 使用现有的 WSUS 基础结构  
 安装 Configuration Manager 之前，可以选择在环境中处于活动状态的 WSUS 服务器，以用作软件更新点。 配置软件更新点时，必须指定同步设置。 Configuration Manager 连接至在软件更新点服务器运行的 WSUS 服务器并使用相同设置配置 WSUS。 如果 WSUS 服务器以前与未配置为软件更新点同步设置的产品或分类同步，则会对 WSUS 数据库中的所有软件更新元数据同步产品和分类的软件更新元数据，而与软件更新点配置的同步设置无关。 这可能会导致站点数据库中出现意外的软件更新元数据。 直接在 WSUS 管理控制台中添加产品或分类然后立即启动同步时，你将遇到相同的行为方式。 默认情况下，Configuration Manager 每小时会连接到软件更新点上的 WSUS，并重置在 Configuration Manager 外修改的任何设置。 未满足你在同步设置中指定的产品和分类要求的软件更新被设置为过期，然后会从站点数据库中删除。

 将 WSUS 服务器配置为软件更新点时，将无法再将其用作独立 WSUS 服务器。 如果需要不由 Configuration Manager 管理的单独的独立 WSUS 服务器，则必须在其他服务器上配置它。

####  <a name="BKMK_WSUSAsReplica"></a> 将 WSUS 配置为副本服务器  
 在主站点服务器上创建软件更新点站点系统角色时，你无法使用配置为副本的 WSUS 服务器。 将 WSUS 服务器配置为副本时，Configuration Manager 无法配置 WSUS 服务器，WSUS 同步也会失败。 在辅助站点上创建软件更新点时，Configuration Manager 会将 WSUS 配置为在父主站点中软件更新点上运行的 WSUS 的副本服务器。 在主站点中安装的第一个软件更新点为默认的软件更新点。 站点中的其他软件更新点被配置为默认软件更新点的副本。  

####  <a name="BKMK_WSUSandSSL"></a> 决定是否将 WSUS 配置为使用 SSL  
 你可以使用 SSL 协议帮助保护软件更新点上运行的 WSUS。 WSUS 使用 SSL 向 WSUS 服务器验证客户端计算机和下游 WSUS 服务器的身份。 WSUS 还使用 SSL 来加密软件更新元数据。 如果选择使用 SSL 保护 WSUS，则必须在安装软件更新点之前准备 WSUS 服务器。  

 在安装和配置软件更新点时，必须选择“为 WSUS 服务器启用 SSL 通信”  设置。 否则，Configuration Manager 会将 WSUS 配置为不使用 SSL。 为软件更新点上运行的 WSUS 启用 SSL 时，也必须将在任何子站点的软件更新点上运行的 WSUS 配置为使用 SSL。  

###  <a name="BKMK_ConfigureFirewalls"></a> 配置防火墙  
 Configuration Manager 管理中心站点上的软件更新与软件更新点上运行的 WSUS 进行通信，这反过来会与同步源进行通信以同步软件更新元数据。 子站点上的软件更新点与父站点上的软件更新点通信。 如果主站点中有多个软件更新点，则其他软件更新点必须与安装在该站点中的第一个软件更新点（默认的软件更新点）通信。  

 为了接受 WSUS 在以下方案中使用的 HTTP 或 HTTPS 端口，可能需要配置防火墙：当 Configuration Manager 软件更新点与 Internet 之间具有企业防火墙；当你具有软件更新点及其上游同步源；当你具有其他的软件更新点。 至 Microsoft 更新的连接始终配置为针对 HTTP 使用端口 80，针对 HTTPS 使用端口 443。 你可以将自定义端口用于从子站点中软件更新点上运行的 WSUS 至主站点中软件更新点上运行的 WSUS 的连接。 当安全策略不允许连接时，必须使用导出和导入同步方法。 有关详细信息，请参阅本主题中的 [同步源](#BKMK_SyncSource) 部分。 有关 WSUS 使用的端口的详细信息，请参阅[如何确定 System Center Configuration Manager 中 WSUS 使用的端口设置](../get-started/install-a-software-update-point.md#wsus-settings)。  

#### <a name="restrict-access-to-specific-domains"></a>限制对特定域的访问  
 如果组织不允许向活动软件更新点与 Internet 之间的防火墙上的所有地址开放端口和协议，则可以限制访问以下域，以便 WSUS 和自动更新可以与 Microsoft 更新通信：  

-   http://windowsupdate.microsoft.com

-   http://*.windowsupdate.microsoft.com  

-   https://*.windowsupdate.microsoft.com  

-   http://*.update.microsoft.com  

-   https://*.update.microsoft.com  

-   http://*.windowsupdate.com  

-   http://download.windowsupdate.com  

-   http://download.microsoft.com  

-   http://*.download.windowsupdate.com  

-   http://test.stats.update.microsoft.com  

-   http://ntservicepack.microsoft.com  

 在以下情况下，可能需要将下列地址添加到位于两个站点系统中的防火墙中：如果子站点具有软件更新点或如果站点中存在远程活动的基于 Internet 的软件更新点：  

 **子站点上的软件更新点**  

-   http://<*子站点上软件更新点的 FQDN*>  

-   https://<*子站点上软件更新点的 FQDN*>  

-   http://<*父站点上软件更新点的 FQDN*>  

-   https://<*父站点上软件更新点的 FQDN*>  

##  <a name="BKMK_SyncSettings"></a> 规划同步设置  
 Configuration Manager 中的软件更新同步是指根据你配置的条件检索软件更新元数据的过程。 层次结构中的顶层站点、管理中心站点或独立主站点从 Microsoft 更新同步软件更新。 你可以选择将顶层站点上的软件更新点配置为与不在 Configuration Manager 层次结构中的现有 WSUS 服务器同步。 子主站点从管理中心站点上的软件更新点同步软件更新元数据。 安装和配置软件更新点之前，请使用本部分规划同步设置。  

###  <a name="BKMK_SyncSource"></a> 同步源  
 软件更新点的同步源设置指定软件更新点检索软件更新元数据所在的位置，以及是否在同步过程中创建 WSUS 报表事件。  

-   **同步源** ：默认情况下，顶层站点的软件更新点针对 Microsoft 更新配置同步源。 你可以选择将顶层站点与现有的 WSUS 服务器同步。 默认情况下，子主站点上的软件更新点会将同步源配置为管理中心站点中的软件更新点。  

    > [!NOTE]  
    >  在主站点中安装的第一个软件更新点为默认的软件更新点，并且会与管理中心站点同步。 主站点中的其他软件更新点与主站点中的默认软件更新点同步。  

     从 Microsoft 更新或从上游更新服务器中断开软件更新点时，可以将同步源配置为不与配置的同步源同步，而是使用 WSUSUtil 工具的导出和导入功能来同步软件更新。 有关详细信息，请参阅[从断开连接的软件更新点中同步软件更新](../get-started/synchronize-software-updates-disconnected.md)。  

-   **WSUS 报告事件：** 客户端计算机上的 Windows 更新代理可以创建用于 WSUS 报告的事件消息。 但这些事件不会用于 Configuration Manager 中的软件更新，因此，默认情况下选择“不创建 WSUS 报告事件”选项。 如果未创建这些事件，则客户端计算机应该仅在软件更新评估和符合性扫描过程中连接到 WSUS 服务器。 如果在 Configuration Manager 中的软件更新之外进行报告需要这些事件，则将需要修改此设置以创建 WSUS 报告事件。  

###  <a name="BKMK_SyncSchedule"></a> 同步计划  
 你只能在 Configuration Manager 层次结构中顶层站点的软件更新点上配置同步计划。 配置同步计划后，软件更新点会在你指定的日期和时间与同步源同步。 自定义的计划允许你在 WSUS 服务器、站点服务器和网络的需求不高的日期和时间同步软件更新，如每周凌晨 2:00 一次。 或者，你可以使用“所有软件更新”中的“同步软件更新”操作或 Configuration Manager 控制台的“软件更新组”节点启动顶层站点的同步。  

> [!TIP]  
>  使用适合你的环境的时间范围来计划运行软件更新同步。 最常见的一种情况是将软件更新同步计划设置为在每月第二个星期二发布了 Microsoft 定期安全更新（这通常称为周二补丁日）之后立即运行。 另一种常见的情况是将软件更新同步计划设置为每天使用软件更新提供 Endpoint Protection 定义和引擎更新时运行。  

 在软件更新点成功完成同步后，会将同步请求发送给子站点。 如果主站点中有其他软件更新点，则会将同步请求发送给每个软件更新点。 此过程在层次结构中的每个站点上重复发生。  

###  <a name="BKMK_UpdateClassifications"></a> 更新分类  
 每个软件更新都是利用更新分类定义的，此分类能帮助组织不同的更新类型。 同步过程中，将同步指定分类的软件更新元数据。 Configuration Manager 可以将软件更新与下列更新分类一并同步：  

-   **关键更新：** 针对特定的问题指定广泛发布的更新，以解决与安全性无关的关键错误。  

-   **定义更新：** 指定对病毒定义文件或其他定义文件的更新。  

-   **功能包：** 指定新的产品功能，这些功能在产品版本以外分发，而且通常包含在下一个完整的产品版本和功能中。  

-   **安全更新：** 针对特定于产品而且与安全性相关的问题指定广泛发布的更新。  

-   **Service Pack：** 指定一组累积的将应用于应用程序的修补程序。 这些修补程序可以包括安全更新、关键更新、软件更新等。  

-   **工具：** 指定可帮助完成一项或多项任务的实用程序或功能。  

-   **更新汇总：** 指定一组累积的修补程序，它们打包在一起以便于部署。 这些修补程序可以包括安全更新、关键更新、其他更新等。 更新汇总通常解决特定领域的问题，例如安全性或产品组件问题。  

-   **更新：** 指定对已安装的应用程序或文件的更新。  

 仅在顶层站点上配置更新分类设置。 未在子站点上的软件更新点上配置更新分类设置，因为已将软件更新元数据从顶层站点复制到子主站点。 选择更新分类时，请注意，你选择的分类越多，同步软件更新元数据所需的时间越长。  

> [!WARNING]  
>  作为最佳方案，请在首次同步软件更新之前清除所有分类。 初次同步之后，请从软件更新点组件属性中选择分类，然后重新启动同步。  

###  <a name="BKMK_UpdateProducts"></a> 产品  
 每个软件更新的元数据都定义了更新适用于的一个或多个产品。 产品是指特定版本的操作系统或应用程序。 产品示例是 Microsoft Windows Server 2008。 产品家族是指从中派生单个产品的基本操作系统或应用程序。 产品系列的示例是 Microsoft Windows，而 Microsoft Windows Server 2008 是其成员之一。 可以指定产品系列或产品系列中的各个产品。  

 在软件更新适用于多个产品，而且至少选择了一个要同步的产品时，即使没有选择某些产品，所有产品都将出现在 Configuration Manager 控制台中。 例如，Windows Server 2012 是你订阅的唯一操作系统，并且软件更新应用于 Windows Server 2012 和 Windows Server 2012 Datacenter Edition，那么，这两个产品都将位于站点数据库中。  

 只会在顶层站点上配置产品设置， 而不会在子站点的软件更新点上配置产品设置，因为软件更新元数据将从顶层站点复制到子主站点。 在选择产品时，请注意，你选择的产品越多，同步软件更新元数据所花费的时间就越长。  

> [!IMPORTANT]  
>  Configuration Manager 存储产品和产品系列的列表，你在初次安装软件更新点时可以从此列表中进行选择。 如果某些产品和产品系列是在发布 Configuration Manager 之后发布的，那么，在完成软件更新同步（这将更新可供你从中进行选择的可用产品和产品系列的列表）之前，可能无法选择它们。 作为一种最佳方案，请在首次同步软件更新之前清除所有产品。 初始同步后，从软件更新点组件属性中选择产品，然后重新启动同步。  

###  <a name="BKMK_SupersedenceRules"></a>取代规则  
 通常，取代另一个软件更新的软件更新执行下列一项或多项操作：  

-   增强、改进或更新由以前发布的一个或多个更新提供的修补程序。  

-   提高被取代更新文件包的效率，如果更新已获准安装，则该更新文件包将安装在客户端计算机上。 例如，被取代更新可能包含不再与修补程序或新更新支持的操作系统相关的文件，因此这些文件未包括在更新的取代文件包中。  

-   更新产品的较新版本。 换句话说，它将更新不再适用于产品的较旧版本或配置的版本。 如果进行了修改来扩展语言支持，则更新还可能取代其他更新。 例如，稍后对 Microsoft Office 的产品更新进行的修订可能会删除对较旧操作系统的支持，但可能会在初始更新版本中添加对新语言的额外支持。  

 在软件更新点的属性中，你可以指定被取代软件更新立即过期，从而防止将它们包括在新部署中，并标记现有部署以指示它们包含一个或多个过期的软件更新。 或者，你可以指定被取代软件更新过期之前的时间段，从而允许你继续部署这些更新。 考虑你可能需要部署被取代软件更新的以下情况：  

-   如果取代软件更新仅支持较新版本的操作系统，而你的部分客户端计算机运行较早版本的操作系统。  

-   如果取代软件更新与它所取代的软件更新相比适用性限制更多。 这将使其不适合于某些客户端计算机。  

-   如果取代软件更新未获准在生产环境中进行部署。  

    > [!NOTE]  
    > Configuration Manager 将被取代的软件更新设置为“已过期”时，不会在 WSUS 中将该更新设置为“已拒绝”。 但是，WSUS 清除任务运行时，在 Configuration Manager 中设置为“已过期”的更新在 WSUS 服务器中设置为“已拒绝”状态，并且计算机上的 Windows 更新代理不再扫描这些更新。 这意味着客户端将继续扫描已过期的更新，直到清除任务运行。 有关 WSUS 清除任务的信息，请参阅[软件更新维护](/sccm/sum/deploy-use/software-updates-maintenance)。

###  <a name="BKMK_UpdateLanguages"></a> 语言  
 软件更新点的语言设置允许你配置为软件更新同步摘要详细信息（软件更新元数据）的语言，以及将为软件更新下载的软件更新文件语言。  

#### <a name="software-update-file"></a>软件更新文件  
 你为软件更新点属性中的“软件更新文件”  设置配置的语言提供在站点上下载软件更新时可用的默认语言集。 每次下载或部署软件更新时，你可以修改默认选择的语言。 在下载过程中，会将配置的语言的软件更新文件下载到部署包源位置（如果有采用所选语言的软件更新文件）。 然后，会将这些软件更新文件复制到站点服务器上的内容库，再将它们复制到为包配置的分发点。  

 软件更新文件语言设置应配置为包含环境中最常用的语言。 例如，分配给站点的客户端计算机为操作系统或应用程序最常使用英语和日语，并且有站点上使用的极少数其他语言，则在下载或部署软件更新时在“软件更新文件”  列中选择英语和日语，并清除其他语言。 这允许你在部署和下载向导的“语言选择”  页上使用默认设置， 还可防止下载不需要的更新文件。 在 Configuration Manager 层次结构中的每个软件更新点上配置此设置。  

#### <a name="summary-details"></a>摘要详细信息  
 在同步过程中，将采用你指定的语言为软件更新更新摘要详细信息（软件更新元数据）。 元数据提供有关软件更新的信息，例如名称、描述、更新支持的产品、更新分类、文章 ID、下载 URL、适用性规则等。  

 只会在顶层站点上配置摘要详细信息设置， 而不会在子站点上的软件更新点上配置摘要详细信息，因为软件更新元数据将通过使用基于文件的复制从管理中心站点向下复制到这些站点。 在选择摘要详细信息语言时，请仅选择环境中需要的语言。 选择的语言越多，同步软件更新元数据所花的时间就越长。 Configuration Manager 在 Configuration Manager 控制台运行的操作系统的区域设置中显示软件更新元数据。 如果操作系统的区域设置中没有软件更新的本地化属性，则软件更新信息以英语显示。  

> [!IMPORTANT]  
>  请务必选择将在 Configuration Manager 层次结构中需要的所有摘要详细信息语言。 当顶层站点上的软件更新点与同步源同步时，所选摘要详细信息语言确定检索的软件更新元数据。 如果在同步至少运行一次后修改摘要详细信息语言，则针对修改的摘要详细信息语言检索的软件更新元数据仅适用于新的或更新的软件更新。 除非更改了同步源上的软件更新，否则不会使用已修改语言的新元数据更新已同步的软件更新。  

##  <a name="BKMK_MaintenanceWindow"></a> 规划软件更新维护窗口  
 你可以添加专用于软件更新安装的维护时段。 这样，你将能配置一般维护时段以及用于软件更新的其他维护时段。 如果同时配置了一般维护时段和软件更新维护时段，则客户端将仅在软件更新维护时段内安装软件更新。 有关维护时段的详细信息，请参阅[如何使用维护时段](../../core/clients/manage/collections/use-maintenance-windows.md)。  

##  <a name="BKMK_RestartOptions"></a> 在软件更新安装之后重启 Windows 10 客户端的选项
当需要重启的软件更新已使用 Configuration Manager 进行部署并且已安装在一台计算机上时，将计划挂起的重启并显示重启对话框。

从 Configuration Manager 版本 1606 开始，只要 Configuration Manager 软件更新存在挂起的重启，则 Windows 10 计算机上的 Windows 电源选项中将出现“更新并重启”和“更新并关闭”选项。 使用这些选项中的某一个后，计算机重启后将不再显示重启对话框。

在 Configuration Manager 的以前版本中，当 Windows 8 和更高版本的计算机挂起重新启动时，以及当使用 Windows 电源选项（而不是从重新启动对话框）关闭或重新启动计算机时，计算机重新启动后“重新启动”对话框仍然保留并且计算机在配置的截止时间仍将需要重新启动。

## <a name="next-steps"></a>后续步骤
规划软件更新之后，请参阅[准备软件更新管理](../get-started/prepare-for-software-updates-management.md)。
