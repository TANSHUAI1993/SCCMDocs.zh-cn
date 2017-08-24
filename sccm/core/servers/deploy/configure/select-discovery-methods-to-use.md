---
title: "选择 Configuration Manager 的发现方法 | Microsoft Docs"
description: "查看可考虑使用的方法和运行它们的站点。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4b6be888be2ad6c1f5e7c0be33d9830bb870114e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="select-discovery-methods-to-use-for-system-center-configuration-manager"></a>选择 System Center Configuration Manager 要使用的发现方法

*适用范围：System Center Configuration Manager (Current Branch)*

若要成功且有效地使用 System Center Configuration Manager 的发现，必须考虑使用哪些方法以及在哪些站点运行它们。  

 因为发现可能会生成大量的网络流量，并且所产生的发现数据记录 (DDR) 可能会在处理过程中使用大量的 CPU 资源，所以请仅使用满足目标所需的那些发现方法。 可在开始时仅使用一种或两种发现方法，之后以管制方式启用其他方法以扩展环境中的发现级别。 本主题中的信息可以帮助做出明智的决策。  

 有关不同的发现方法的信息，请参阅[关于 System Center Configuration Manager 的发现方法](../../../../core/servers/deploy/configure/about-discovery-methods.md)。  

## <a name="select-methods-to-discover-different-things"></a>选择可发现不同事项的方法  
 若要发现潜在的 Configuration Manager 客户端计算机或用户资源，必须启用合适的发现方法。 可以使用发现方法的不同组合来查找不同的资源，以及发现关于那些资源的附加信息。 使用的发现方法决定了发现的资源类型，以及发现进程中使用的 Configuration Manager 服务和代理。 它们还决定了关于你可以发现的资源的信息类型。  

### <a name="discover-computers"></a>发现计算机   
如果想要发现计算机，可以使用 **Active Directory 系统发现**或**网络发现**。  

 例如，在使用客户端请求安装之前，想要发现能够安装 Configuration Manager 客户端的资源，则可以运行 Active Directory 系统发现。 通过此方法，不仅可以从 Active Directory 域服务发现资源，还可以发现相关基本信息和扩展信息。 此信息或许可用于构建复杂的查询和集合，以用于分配客户端设置或内容部署。

或者，可以运行网络发现并使用其选项来发现（以后使用客户端请求安装所需的）资源的操作系统。 网络发现可提供无法通过其他发现方法获得的网络拓扑信息。 但此方法不提供关于 Active Directory 环境的任何信息。

 还有一个名为**检测信号发现**的方法。 可以仅使用检测信号发现来强制发现用客户端请求安装以外的其他方法安装的客户端。 但是，与其他发现方法不同，检测信号发现无法发现没有活动的 Configuration Manager 客户端的计算机。 它会返回有限的一组信息，以维护现有的数据库记录，而不是作为该记录的基础。 检测信号发现提交的信息可能不足，因此无法构建复杂的查询或集合。  

 如果使用 **Active Directory 组发现**来发现指定组的成员资格，则可能会发现有限的系统或计算机信息。 这不能取代计算机的完整发现，但可以提供基本信息。 此信息不足以进行客户端请求安装。  

### <a name="discover-users"></a>发现用户   
如果想要发现关于用户的信息，可使用 **Active Directory 用户发现**。 与 Active Directory 系统发现相似，此方法从 Active Directory 中发现用户。 它包含 Active Directory 的基本信息和扩展信息。 与计算机信息相似，你可以使用此信息构建复杂的查询和集合。  

### <a name="discover-group-information"></a>发现组信息   
如果想要发现关于组和组成员身份的信息，请使用 **Active Directory 组发现**。 此发现方法创建安全组的资源记录。  

 可以使用此方法搜索特定的 Active Directory 组，从而确定该组以及该组内的任何嵌套组中的成员。 也可以使用此方法在 Active Directory 位置中搜索组，以及以递归方式搜索 Active Directory 域服务内该位置中的每个子容器。  

 此发现方法还搜索通讯组的成员资格。 这可以确定用户和计算机的组关系。  

 发现组时，也可能会发现关于其成员的有限信息。 但是，这并不能取代 Active Directory 系统或用户发现方法。 它通常不足以构建复杂查询和集合或用作客户端请求安装的基础。  

### <a name="discover-infrastructure"></a>发现基础结构   
可以使用 **Active Directory 林发现**和**网络发现**这两种方法来发现网络基础结构。  

 使用 Active Directory 林发现在 Active Directory 林中搜索关于子网和 Active Directory 站点配置的信息。 然后，这些配置会自动作为边界位置输入到 Configuration Manager 中。  

 想要发现网络拓扑时，请使用网络发现。 虽然其他发现方法会返回与 Active Directory 域服务相关的信息，并且可以确定客户端的当前网络位置，但它们不会根据网络的子网和路由器拓扑提供基础结构信息。  

##  <a name="bkmk_shared"></a>发现数据在站点之间共享  
 Configuration Manager 将发现数据添加到数据库后，将会在层次结构中的所有站点之间快速共享该数据。 由于通常情况下，在层次结构中的多个站点上发现相同信息并无好处，因此请考虑设置一个用于在单一站点上运行的每个发现方法的单一实例。 最好不要在不同的站点上运行单一方法的多个实例。  

 不过，将相同的发现方法指派为在多个站点上运行（每个方法有单独的配置和计划）在某些环境下可能也会有用。 例如，使用网络发现时，可能需要指示每个站点发现其本地网络，而不是尝试发现 WAN 中所有网络位置。

如果将相同发现方法的多个实例配置为在不同站点上运行，请仔细规划每个站点的配置。 请避免让两个或者更多站点从网络或 Active Directory 中发现相同的资源。 这可能会使用额外的网络带宽并创建重复的 DDR。

下表确定可在哪些站点上设置不同的发现方法。  

|发现方法|支持的位置|  
|----------------------|-------------------------|  
|Active Directory 林发现|管理中心站点<br /><br /> 主站点|  
|Active Directory 组发现|主站点|  
|Active Directory 系统发现|主站点|  
|Active Directory 用户发现|主站点|  
|检测信号发现<sup>1</sup>|主站点|  
|网络发现|主站点<br /><br /> 辅助站点|  

 <sup>1</sup>辅助站点无法配置检测信号发现，但可从客户端接收检测信号 DDR。  

 当辅助站点运行网络发现或接收检测信号发现 DDR 时，它们会通过基于文件的复制将 DDR 传输到其父主站点。 这是因为只有主站点和管理中心站点才能处理 DDR。 有关如何处理 DDR 的详细信息，请参阅[关于发现数据记录](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs) 。  

## <a name="considerations-for-different-discovery-methods"></a>不同发现方法的注意事项  
 由于每个站点服务器和网络环境有所不同，因此最好限制发现的初始配置。 然后密切监视每个站点服务器，了解其处理生成的发现数据的能力。  

针对系统、用户或组使用 **Active Directory 发现方法**时：  

-   在拥有与域控制器的快速网络连接的站点上运行发现。  

-   考虑 Active Directory 复制拓扑以确保发现可访问最新信息。  

-   考虑发现配置的作用域，并仅限于发现那些必须发现的 Active Directory 位置和组。  

如果使用**网络发现**：  

-   使用受限的初始配置来确定网络拓扑。  

-   确定网络拓扑后，请将网络发现设置为在位于网络区域中心你希望更充分发现的特定站点上运行。  

由于**检测信号发现**不在特定站点上运行，因此在有关在何处运行发现的一般规划中不必考虑它。  

##  <a name="bkmk_best"></a>最佳发现方案  
为了获取发现的最佳结果，建议执行以下操作：

 - **在运行 Active Directory 组发现之前运行 Active Directory 系统发现和 Active Directory 用户发现。**  

 当 Active Directory 组发现将以前未发现的用户或计算机标识为组成员时，它会尝试发现该用户或计算机的基本详细信息。 由于 Active Directory 组发现未针对此类型的发现进行优化，此过程可能会导致它运行缓慢。 此外，Active Directory 组发现只会确定有关它发现的用户和计算机的基本详细信息，而不会创建完整的用户或计算机发现记录。 运行 Active Directory 系统发现和 Active Directory 用户发现时，每个对象类型的其他 Active Directory 属性将可用。 因此，Active Directory 组发现可更高效地运行。  

- **设置 Active Directory 组发现时，请只指定用于 Configuration Manager 的组。**  

 若要帮助控制 Active Directory 组发现的资源使用，请仅指定用于 Configuration Manager 的那些组。 这是因为 Active Directory 组发现会以递归方式搜索它发现的每个组来查找用户、计算机和嵌套组。 搜索每个嵌套组可能会扩展 Active Directory 组发现的作用域，并降低性能。 此外，如果为 Active Directory 组发现设置增量发现，发现方法将监视每个组的更改。 如果该方法必须搜索不必要的组，这会进一步降低性能。  

- **将发现方法设置为具有更长的完整发现间隔和更频繁的增量发现周期。**  

 由于增量发现使用的资源比完整发现周期少，并且可确定 Active Directory 中的新资源或修改的资源，因此可将完整发现周期的频率减少到每周运行一次或更少。 Active Directory 系统发现、Active Directory 用户发现和 Active Directory 组发现的增量发现可确定 Active Directory 对象的几乎所有更改，并可保持准确的资源发现数据。  

- **在其网络位置与 Active Directory 域控制器最接近的主站点上运行 Active Directory 发现方法。**  

 为了提高 Active Directory 发现的性能，最好在拥有与域控制器的快速网络连接的主站点上运行发现。 如果在多个站点上运行同一 Active Directory 发现方法，请对每个发现方法进行设置以避免重叠。 与 Configuration Manager 过去的版本不同，发现数据会在站点中共享。 因此不必在多个站点上发现相同的信息。 有关详细信息，请参阅[发现数据在站点之间共享](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared)。  

- **计划依据发现数据自动创建边界时，请仅在一个站点上运行 Active Directory 林发现。**  

 如果在层次结构中的多个站点上运行 Active Directory 林发现，最好仅启用在单一站点上自动创建边界的选项。 这是因为，Active Directory 林发现在每个站点上运行并创建边界时，Configuration Manager 无法将这些边界合并为单一边界对象。 如果将 Active Directory 林发现配置为在多个站点上自动创建边界，将会导致在 Configuration Manager 控制台中出现重复的边界对象。  
