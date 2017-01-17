---
title: "大小和扩展 | Microsoft Docs"
description: "确定需要用来支持 System Center Configuration Manager 环境中设备的站点系统角色和站点的数量。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 453d934d693d58e98cf800988dff702400daaf95

---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>System Center Configuration Manager 的大小和扩展数量

*适用范围：System Center Configuration Manager (Current Branch)*



每个 System Center Configuration Manager 部署存在可支持的站点、站点系统角色和设备的最大数量。 这些数量因层次结构（使用的站点的类型和数量）和部署的站点系统角色而异。  下列主题中的信息可帮助确定用于支持环境中需管理的设备的站点系统角色和站点的数量。

将本主题中的信息和以下文章中的信息一起使用：
-   [推荐硬件](../../../core/plan-design/configs/recommended-hardware.md)
-   [站点系统服务器支持的操作系统](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [客户端和设备支持的操作系统](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [站点和站点系统先决条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)

本文中的这些支持数量基于为 Configuration Manager 使用推荐的硬件。 如果未使用推荐的硬件，站点系统的性能会下降并且可能无法满足规定的支持级别。

##  <a name="a-namebkmksitesystemscalea-site-types"></a><a name="bkmk_SiteSystemScale"></a>站点类型  
 **管理中心站点：**  

-   一个管理中心站点最多可支持 25 个子主站点。  

**主站点：**  

-   每个主站点最多支持 250 个辅助站点。  

-   每个主站点的辅助站点数基于持续连接和可靠的广域网 (WAN) 连接。 对于具有少于 500 个客户端的位置，请考虑使用分发点而不是辅助站点。  

 有关主站点可支持的客户端数和设备数的信息，请参阅本主题中的[站点和层次结构的客户端数量](#bkmk_clientnumbers)。  

**辅助站点：**  

-   辅助站点不支持子站点。  

-   一个管理中心站点最多可支持 25 个子主站点。  

**应用程序目录网站点：**  

-   你可以在主站点安装“应用程序目录”网站点的多个实例。  

    > [!TIP]  
    >  最佳做法是，当“应用程序目录”网站点和“应用程序目录”Web 服务点为位于 Intranet 上的客户端提供服务时，将它们一起安装在相同的站点系统上。  

    -   为改进性能，计划每个实例最多支持 50,000 个客户端。  

    -   此站点系统角色的每个实例支持层次结构所支持的最大客户端数。  

## <a name="a-namebkmkrolesa-site-system-roles"></a><a name="bkmk_roles"></a> Site system roles    

**应用程序目录 web 服务点：**  

-   你可以在主站点安装“应用程序目录”Web 服务点的多个实例。  

    > [!TIP]  
    >  最佳做法是，当“应用程序目录”网站点和“应用程序目录”Web 服务点为位于 Intranet 上的客户端提供服务时，将它们一起安装在相同的站点系统上。  

    -   为改进性能，计划每个实例最多支持 50,000 个客户端。  

    -   此站点系统角色的每个实例支持层次结构所支持的最大客户端数。  

**分发点：**  

-   每个站点的分发点：  

    -   每个主站点和辅助站点最多支持 250 个分发点。  

    -   每个主站点和辅助站点最多支持 2000 个被配置为请求分发点的其他分发点。 **例如**，当其中的 2000 个分发点被配置为请求分发点时，一个单一主站点可支持 2250 个分发点。  

    -   每个分发点最多支持来自 4,000 台客户端的连接。  

    -   请求分发点从源分发点访问内容时，它的作用类似于客户端。  

-   每个主站点最多支持合并总计 5,000 个分发点。 该总数包括主站点中的所有分发点和隶属于主站点的子辅助站点的所有分发点。  

-   每个分发点最多支持合并总计 10,000 个包和应用程序。  

> [!WARNING]  
>  一个分发点可以支持的客户端实际数取决于网络速度和分发点计算机的硬件配置。  
>   
>  一个源分发点可以支持的请求分发点数同样取决于网络速度和源分发点计算机的硬件配置，但还会受已部署的内容量的影响。 这是因为与客户端不同的是，客户端通常在不同的时间通过部署窗口访问内容，而所有请求分发点在同一时间请求内容，并可以请求所有可用内容而不仅仅是适用于它们的内容，客户端将仅请求适用于它们的内容。 当太多处理负载放置在源分发点上时，这会导致将内容分发到你的环境中的预期分发点出现意外延迟。  


**回退状态点：**  

-   每个回退状态点最多可支持 100,000 个客户端。  

**管理点：**  

-   每个主站点最多支持 15 个管理点。  

    > [!TIP]  
    >  请勿在从主站点服务器或站点数据库服务器通过慢速链接的服务器上安装管理点。  

-   每个辅助站点支持一个单一管理点，该管理点必须安装在辅助站点服务器上。  

 有关管理点可支持的客户端数和设备数的信息，请参阅本主题中的[管理点](#bkmk_mp)一节。  

**软件更新点：**  

-   安装在站点服务器上的软件更新点最多可支持 25,000 个客户端。  

-   当远程计算机满足 WSUS 支持此数量客户端的要求时，远离站点服务器的软件更新点最多可支持 150,000 个客户端。  

-   默认情况下，Configuration Manager 不支持将软件更新点配置为 NLB 群集。 但是，可以使用 Configuration Manager SDK 在 NLB 群集上配置最多 4 个软件更新点。  

##  <a name="a-namebkmkclientnumbersa-client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a>站点和层次结构的客户端数量  
 使用以下信息来确定站点中或层次结构中可以支持多少客户端和哪些客户端类型。  

###  <a name="a-namebkmkcasa-hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a>具有管理中心站点的层次结构  
管理中心站点最多可支持包括对下列三组列出的设备数量总数：  

-   700,000 台台式机（运行 Windows、Linux 和 UNIX 的计算机）  

-   运行 Mac 和 Windows CE 7.0 的 25,000 台设备  

-   下列情况之一，具体取决于你的部署支持移动设备管理的方式：  

    -   使用本地 MDM 管理的 100,000 台设备  

    -   300,000 台基于云的设备  

 例如，在集成 Microsoft Intune 时，层次结构中可以支持 700,000 台台式机、最多 25,000 个 Mac 和 Windows CE 7.0 客户端和最多 300,000 台基于云的设备，总共 1,025,000 台设备。  如果你支持通过本地 MDM 管理的设备，那么层次结构支持的设备总数为 825,000 台设备。  

> [!IMPORTANT]  
>  在管理中心站点使用标准版 SQL Server 的层次结构中，层次结构最多可支持 50,000 台台式机和设备。 在独立主站点上使用的 SQL Server 版本不限制该站点容量，以便其支持最大的规定客户端数量。  


###  <a name="a-namebkmkchipria-child-primary-site"></a><a name="bkmk_chipri"></a>子主站点  
包含管理中心站点的层次结构中的每个子主站点支持：  

-   总共 150,000 台客户端和设备，不局限于特定组或类型，只要不超过层次结构所支持的数量  

例如，一个支持 25,000 台（因为这是一个层次结构的上限数量）运行 Mac 和 Windows CE 7.0 的计算机的主站点，则还可支持 125,000 个台式计算机，这就使支持的设备总数达到支持的子主站点上限数量 - 150,000。

###  <a name="a-namebkmkpria-stand-alone-primary-site"></a><a name="bkmk_pri"></a>独立主站点  
独立主站点支持下列数量的设备：  

-   总数不超过 175,000 的客户端和设备  

    -   150,000 台台式机（运行 Windows、Linux 和 UNIX 的计算机）  

    -   运行 Mac 和 Windows CE 7.0 的 25,000 台设备  

    -   下列情况之一，具体取决于你的部署支持移动设备管理的方式：  

        -   使用本地 MDM 管理的 50,000 台设备  

        -   150,000 台基于云的设备  

例如，支持 150,000 台台式机和 10,000 个 Mac 或 Windows CE 7.0 客户端的独立主站点仅可额外支持 15,000 台设备。 这些设备可以是基于云的，也可以是使用本地 MDM 管理的。  

###  <a name="a-namebkmkseca-secondary-sites"></a><a name="bkmk_sec"></a>辅助站点  
辅助站点支持：  

-   15,000 台台式机（运行 Windows、Linux 和 UNIX 的计算机）  

###  <a name="a-namebkmkmpa-management-points"></a><a name="bkmk_mp"></a>管理点  
每个管理可以支持以下数目的设备：  

-   总数不超过 25,000 的客户端和设备  

    -   25,000 台台式机（运行 Windows、Linux 和 UNIX 的计算机）  

    -   下列之一（不能两种都包含）：  

        -   10,000 台使用本地 MDM 管理的设备  

        -   10,000 台运行 Mac 和 Windows CE 7.0 的设备  



<!--HONumber=Dec16_HO3-->


