---
title: 客户端对等缓存
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 部署内容时，将客户端对等缓存用于源位置。
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 575a011271026e5b617a334476d3c4e8fa401014
ms.sourcegitcommit: cdf2827fb3f44d7522a9b533c115f910aa9c382a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70902960"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>用于 Configuration Manager 客户端的对等缓存

适用范围：  System Center Configuration Manager (Current Branch)

<!--1101436-->
在将内容部署到远程位置的客户端时，可使用“对等缓存”帮助管理部署。 对等缓存是内置 Configuration Manager 解决方案，使客户端能够直接从本地缓存将内容与其他客户端共享。   

> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  



## <a name="overview"></a>概述

定义：  

- **对等缓存客户端**：从对等项下载内容的任意 Configuration Manager 客户端  

- **对等缓存源**：为对等缓存启用的、与其他客户端共享内容的 Configuration Manager 客户端  

请使用客户端设置将客户端启用为对等缓存源。 无需启用对等缓存客户端。 在将客户端启用为对等缓存源时，管理点既已将其包含在内容位置源列表中。<!--510397--> 要详细了解此过程，请参阅[操作](#operations)。  

对等源必须属于对等缓存客户端的当前边界组。 管理点不会将相邻边界组中的对等缓存源包含在提供给客户端的内容源列表中。 它仅包含相邻边界组中的分发点。 有关当前边界组和相邻边界组的详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/boundary-groups)。<!--SCCMDocs issue 685-->  

Configuration Manager 客户端使用对等缓存将缓存中每种类型的内容提供给其他客户端。 此内容包括 Office 365 文件和快速安装文件。<!--SMS.500850-->  

对等缓存不会取代 Windows BranchCache 或交付优化等其他解决方案的使用。 对等缓存可与其他解决方案结合使用。 这些技术为扩展传统内容部署解决方案提供了更多选项，例如分发点。 对等缓存属于自定义解决方案，独立于 BranchCache。 即使未启用或使用 BranchCache，对等缓存仍能正常运行。  

> [!Note]  
> 自版本 1802 起，Windows BranchCache 始终在部署上启用。 “允许客户端与同一子网上的其他客户端共享内容”设置已删除  。<!--SCCMDocs issue 539--> 如果分发点支持此功能，并在客户端设置中启用，客户端就会使用 BranchCache。 有关详细信息，请参阅[配置 BranchCache](/sccm/core/clients/deploy/about-client-settings#configure-branchcache)。<!--SCCMDocs issue 735-->   



## <a name="operations"></a>操作

要启用对等缓存，请将[客户端设置](#bkmk_settings)部署到集合。 然后，该集合的成员充当同一边界组中其他客户端的对等缓存源。  

- 充当对等内容源的客户端会使用状态消息将可用缓存内容列表提交到其管理点。

   > [!NOTE]
   > 有关适用的对等内容源状态消息的列表，请参阅 [Configuration Manager 中的状态消息](/sccm/core/plan-design/hierarchy/state-messaging-system-center-configuration-manager#7200-state_topictype_super_peer_update_cache_map)，特别是状态消息 ID 为 7200、7201、7202 和 7203 的消息。

- 同一边界组中的另一客户端会向管理点发出内容位置请求。 服务器返回潜在内容源的列表。 此列表包含带有内容且在线的所有对等缓存源。 它还包括分发点及该边界组中的其他内容源位置。 有关详细信息，请参阅[内容源优先级](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority)。  

- 通常，查找内容的客户端会从所提供的列表中选择一个源。 然后，客户端尝试获取该内容。  

从版本 1806 开始，边界组包含其他设置，可以更好地控制环境中的内容分发。 有关详细信息，请参阅[对等下载适用的边界组选项](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions)。<!--1356193-->

> [!NOTE]  
> 如果客户端回退到相邻边界组查找内容，管理点不会将相邻边界组中的对等缓存源添加到潜在内容源位置的列表中。  

请仅选择最适合的客户端作为对等缓存源。 根据底盘类型、磁盘空间和网络连接性等属性评估客户端的适用性。 有关可帮助选择最适合用于对等缓存的客户端的详细信息，请参阅[由 Microsoft 顾问撰写的此博客](https://blogs.technet.microsoft.com/askpfeplat/2018/11/21/configuration-manager-peer-cache-custom-reporting-examples/)。


### <a name="limited-access-to-a-peer-cache-source"></a>限制对对等缓存源的访问  

在对等项请求内容时，如果存在下列情况，则对等缓存源会拒绝其对内容的请求：  

- 低电量模式  

- 处理器负载超过 80%  

- 磁盘 I/O 的 AvgDiskQueueLength 超过 10   

- 没有其他到该计算机的可用连接  

> [!Tip]  
> 在 Configuration Manager SDK 中，使用对等源功能的客户端配置服务器 WMI 类 (SMS_WinPEPeerCacheConfig) 配置这些设置  。  

如果对等缓存源拒绝对内容的请求，对等缓存客户端会继续在其内容源位置列表中搜索内容。   



## <a name="requirements"></a>要求

- 对等缓存支持[客户端和设备支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)中列出的所有受支持的 Windows 版本。 不支持将非 Windows 操作系统作为对等缓存源或对等缓存客户端。  

- 对等缓存源必须是已加入域的 Configuration Manager 客户端。 但是，未加入域的客户端可从已加入域的对等缓存源获取内容。  

- 客户端只能从其当前边界组的对等缓存源中下载内容。  

- 下述列外情况不需要[网络访问帐户](/sccm/core/plan-design/hierarchy/accounts#network-access-account)：  

  - 当启用对等缓存的客户端从软件中心运行任务序列且重启到启动映像时，在站点中配置网络访问帐户。 当设备位于 Windows PE 中时，它使用网络访问帐户从对等缓存源获取内容。  

  - 必要时，对等缓存源会使用网络访问帐户对来自对等项的下载请求进行身份验证。 为此，此帐户只需域用户权限。  

- 使用 1802 及更早版本，对等缓存源的当前边界由客户端的上一次检测信号发现提交内容决定。 出于对等缓存的目的，漫游到其他边界组的客户端可能仍是其以前边界组的成员。 此行为会导致提供给客户端的对等缓存源不在其直接网络位置中。 请不要将漫游客户端启用为对等缓存源。<!--SCCMDocs issue 641-->  

  > [!Important]  
  > 从版本 1806 开始，Configuration Manager 可以更有效地确定对等缓存源是否已漫游到其他位置。 此行为可确保管理点将其作为内容源提供给新位置的客户端，而不是旧位置的客户端。 如果将对等缓存功能与漫游的对等缓存源一起使用，则在将站点更新到版本 1806 之后，还会将所有对等缓存源更新为最新的客户端版本。 在至少将这些对等缓存源更新到版本 1806 后，管理点才会将它们包含在内容位置列表中。<!--SCCMDocs issue 850-->  

- 在尝试下载内容之前，管理点先验证对等缓存源是否处于联机状态。<!--sms.498675--> 此验证通过客户端通知的“快速通道”进行，采用 TCP 端口 10123。<!--511673-->  

> [!Note]  
> 若要利用新的 Configuration Manager 功能，请先将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。  



## <a name="bkmk_settings"></a>对等缓存客户端设置

要详细了解对等缓存客户端设置，请参阅[客户端缓存设置](/sccm/core/clients/deploy/about-client-settings#client-cache-settings)。 

要详细了解如何配置这些设置，请参阅[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。

在使用 Windows 防火墙且启用了对等缓存的客户端上，Configuration Manager 会配置在客户端设置中指定的防火墙端口。



## <a name="bkmk_parts"></a>部分下载支持
<!--1357346-->
自版本 1806 起，客户端对等缓存源可将内容分成多个部分。 这些部分最大限度地减少了网络传输，从而降低了 WAN 利用率。 管理点提供更详细的内容部分跟踪。 它试图消除每个边界组多次下载相同内容的行为。 


### <a name="example-scenario"></a>示例方案

Contoso 有一个单独的主站点，该站点包含两个边界组：总部 (HQ) 和分支机构。 边界组之间有 30 分钟的回退关系。 该站点的管理点和分发点都位于 HQ 边界中。 分支机构所在地没有本地分发点。 分支机构的四个客户端中有两个配置为对等缓存源。 

![示例方案中所述网络配置的示意图](media/1357346-peer-cache-source-parts.png)

1. 将分支机构中的所有四个客户端作为内容部署的目标。 仅将内容分发到了分发点。  

2. Client3 和 Client4 没有用于部署的本地源。 管理点指示客户端等待 30 分钟后再回退到远程边界组。  

3. Client1 (PCS1) 是第一个向管理点刷新策略的对等缓存源。 由于此客户端已启用为对等缓存源，因此管理点指示它立即开始从分发点下载 A 部分。  

4. 当 Client2 (PCS2) 与管理点联系时，由于 A 部分已在下载，但尚未完成，因此管理点指示它立即开始从分发点下载 B 部分。  

5. PCS1 下载完 A 部分，并立即通知管理点。 由于 B 部分已在下载，但尚未完成，因此管理点指示它开始从分发点下载 C 部分。  

6. PCS2 下载完 B 部分，并立即通知管理点。 管理点指示它开始从分发点下载 D 部分。  

7. PCS1 下载完 C 部分，并立即通知管理点。 管理点告知它远程分发点没有更多可用部分。 管理点指示它从本地对等源 PCS2 下载 B 部分。  

8. 此过程一直持续到这两个客户端对等缓存源拥有彼此的所有部分。 在指示对等缓存源从本地对等源下载部分之前，管理点会优先考虑远程分发点中的部分。  

9. Client3 是 30 分钟回退期到期后第一个刷新策略的客户端。 现在，它与管理点进行核对，后者告知它有新的本地源。 它从其中一个客户端对等缓存源下载全部内容，而不是通过 WAN 从分发点下载全部内容。 客户端优先考虑本地对等源。 

> [!Note]  
> 如果客户端对等缓存源的数量超出内容部分的数量，则管理点会指示其他对等缓存源像正常客户端一样等待回退。 


### <a name="configure-partial-download"></a>配置部分下载

1. 按常规设置[边界组](/sccm/core/servers/deploy/configure/boundary-groups)和对等缓存源。  

2. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  。 单击功能区中的“层次结构设置”  。  

3. 在“常规”  选项卡上，启用“配置客户端对等缓存源以将内容分成多个部分”  选项。  

4. 创建必需的内容部署。  

   > [!Note]  
   > 此功能仅适用于客户端在后台下载内容的情况（例如进行必需的部署）。 按需下载（例如用户在软件中心安装可用部署时）的行为与往常一样。  

若要了解它们如何处理多部分内容的下载，请检查客户端对等缓存源上的 **ContentTransferManager.log** 和管理点上的 **MP_Location.log**。  



## <a name="guidance-for-cache-management"></a>缓存管理指南
<!--510645-->
对等缓存依靠 Configuration Manager 客户端缓存进行内容共享。 在环境中管理客户端缓存时，请考虑以下几点：  

- Configuration Manager 客户端缓存和分发点上的内容库不同。 在管理分发到分发点的内容时，Configuration Manager 客户端会自动管理其缓存中的内容。 存在一些设置和方法可帮助控制对等缓存源的缓存中包含哪些内容。 有关详细信息，请参阅[为 Configuration Manager 客户端配置客户端缓存](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache)。  

- 对等缓存源采用常规缓存大小和维护。 有关详细信息，请参阅[配置客户端缓存大小](/sccm/core/clients/deploy/about-client-settings#configure-client-cache-size)。 请考虑较大内容的大小，例如 OS 升级包或 Windows 10 快速更新文件。 请结合对等缓存源上可用的磁盘空间，比较你对此内容的需求。  

- 在对等项下载内容时，对等缓存源客户端会更新缓存中的上次内容引用时间。 客户端将在自动维护其缓存时使用此时间戳，以便先移除较旧的内容。 若是这样，客户端应等待一段时间才能删除对等缓存客户端下载较频繁的内容。  

- 必要时，请在 OS 部署任务序列期间使用 SMSTSPreserveContent 变量，从而保留客户端缓存中的内容  。 有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables#SMSTSPreserveContent)。  

- 必要时，请在创建以下软件时使用“保留客户端缓存中的内容”选项  ：  
  - 应用程序
  - 包
  - OS 映像
  - OS 升级包
  - 启动映像



## <a name="monitoring"></a>监视   

请查看“客户端数据源”仪表板，了解对等缓存的使用情况  。 有关详细信息，请参阅[客户端数据源仪表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。

此外，可通过报表查看对等缓存的使用情况。 在控制台中，转到“监视”工作区，展开“报表”，再选择“报表”节点    。 下面的报表都属于“软件分发内容”类型  ：  

1.  **对等缓存源内容拒绝**：边界组中对等缓存源拒绝内容请求的频率。  

    > [!Note]  
    >  已知问题<!--486652-->：在向下钻取结果（例如 MaxCPULoad 或 MaxDiskIO）时，可能会收到一条错误，表明找不到该报表或详细信息   。 要解决此问题，请使用另外两个直接显示结果的报表。  

2. **按条件的对等缓存源内容拒绝**：显示指定边界组的拒绝详细信息或拒绝类型。 

    > [!Note]  
    >  已知问题<!--486652-->：无法从可用参数中选择，必须手动输入。 输入“边界组名称”和“拒绝类型”的值，如“对等缓存源内容拒绝”报表中所示    。 例如，对于*拒绝类型*，你可以输入 *MaxCPULoad* 或 *MaxDiskIO*。  

3. **对等缓存源内容拒绝详细信息**：显示客户端在被拒绝时所请求的内容。  

    > [!Note]  
    >  已知问题<!--486652-->：无法从可用参数中选择，必须手动输入。 如“对等缓存源内容拒绝”报表中所示，输入“拒绝类型”的值   。 然后输入想要了解其详细信息的内容源的源 ID  。 
    > 
    > 查找内容源的资源 ID：  
    > 
    > 1. 在按条件的对等缓存源内容拒绝报表的结果中查找显示为对等缓存源的计算机名称   。  
    > 
    > 2. 转到“资产和符合性”工作区，选择“设备”节点并搜索该计算机的名称   。 使用资源 ID 列中的值。  

