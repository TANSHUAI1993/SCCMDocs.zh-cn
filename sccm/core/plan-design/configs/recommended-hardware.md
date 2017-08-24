---
title: "推荐的硬件 | Microsoft Docs"
description: "获取硬件建议，有助于在基本部署以上扩展 System Center Configuration Manager 环境。"
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
caps.latest.revision: "26"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8dac6df60b07461d6410d305723b3f03fb09fa16
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="recommended-hardware-for-system-center-configuration-manager"></a>用于 System Center Configuration Manager 的推荐硬件

*适用范围：System Center Configuration Manager (Current Branch)*

以下建议是一些指南，可以帮助扩展 System Center Configuration Manager 环境，支持比非常基本的站点、站点系统和客户端部署更高级的部署。 这些指南并未打算将所有可能的站点和层次结构配置都包括在内。  

 请使用以下各部分中的这些信息作为指南来帮助你做好硬件规划，使默认的硬件配置能满足使用 Configuration Manager 可用功能的客户端和站点在处理负载方面的要求。  


##  <a name="bkmk_ScaleSieSystems"></a>站点系统  
 本部分提供用于 Configuration Manager 站点系统的推荐硬件配置，以实现具有以下效果的部署：支持最大数目的客户端，以及使用大部分或全部 Configuration Manager 功能。 支持小于最大数量的客户端且不使用所有可用功能的部署可能需要更少的计算机资源。 通常，限制整个系统的性能的关键因素包括下列因素（按顺序列出）：  

1.  磁盘 I/O 性能  

2.  可用内存  

3.  CPU  

为了获得最佳性能，请将 RAID 10 配置用于所有数据驱动器以及 1 Gbps 以太网。  

###  <a name="bkmk_ScaleSiteServer"></a>站点服务器  

|独立主站点|CPU（核心数）|内存(GB)|SQL Server 的内存分配 (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|数据库站点角色在同一服务器上的独立主站点服务器<sup>1</sup>|16|96|80|  
|具有远程站点数据库的独立主站点服务器|8|16|-|  
|独立主站点的远程数据库服务器|16|72|90|  
|数据库站点角色在同一服务器上的管理中心站点服务器<sup>1</sup>|20|128|80|  
|具有远程站点数据库的管理中心站点服务器|8|16|-|  
|管理中心站点的远程数据库服务器|16|96|90|  
|数据库站点角色在同一服务器上的子主站点|16|96|80|  
|具有远程站点数据库的子主站点服务器|8|16|-|  
|子主站点的远程数据库服务器|16|72|90|  
|辅助站点服务器|8|16|-|  

 <sup>1</sup>在同一台计算机上安装站点服务器和 SQL Server 时，部署对站点和客户端支持[调整大小和缩放数量](/sccm/core/plan-design/configs/size-and-scale-numbers)的最大值。 但是，此配置可以限制 [System Center Configuration Manager 的高可用性选项](/sccm/protect/understand/high-availability-options)，像使用 SQL Server 群集那样。 此外，由于支持 SQL Server 和 Configuration Manager 站点服务器所需的 I/O 要求较高，因此在同一台计算机上运行二者时，如果部署较大，最好考虑将配置用于远程 SQL Server 计算机。  

###  <a name="bkmk_RemoteSiteSystem"></a>远程站点系统服务器  
 以下指南适用于具有单一站点系统角色的计算机。 当在同一台计算机上安装多个站点系统角色时，请计划实施调整。  

|站点系统角色|CPU（核心数）|内存(GB)|硬盘空间 (GB)|  
|----------------------|---------------|---------------|--------------------|  
|管理点|4|8|50|  
|分发点|2|8|根据操作系统需要，存储所部署的内容|  
|应用程序目录（Web 服务和网站在站点系统计算机上）|4|16|50|  
|软件更新点<sup>1</sup>|8|16|根据操作系统需要，存储所部署的更新|  
|所有其他站点系统角色|4|8|50|  

 <sup>1</sup>托管软件更新点的计算机对 IIS 应用程序池需要使用以下配置：  

-   将 **WsusPool 队列长度** 增加到 **2000**。  

-   将 **WsusPool 专用内存限制** 增加 4 倍，或设置为 **0**（无限制）。  

###  <a name="bkmk_DiskSpace"></a>站点系统的磁盘空间  
 磁盘分配和配置会影响 Configuration Manager 的性能。 由于每个 Configuration Manager 环境都不同，因此，所实现的值可能会不同于下列指南的值。  

 为了获得最佳性能，请将每个对象都放在单独、专用的 RAID 卷上。 对于所有数据卷（Configuration Manager 及其数据库文件），请使用 RAID 10 以获得最佳性能。  

|数据用途|最小磁盘空间|25,000 个客户端|50,000 个客户端|100,000 个客户端|150,000 个客户端|700,000 个客户端（管理中心站点）|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|操作系统|请参阅操作系统指南。|请参阅操作系统指南。|请参阅操作系统指南。|请参阅操作系统指南。|请参阅操作系统指南。|请参阅操作系统指南。|  
|Configuration Manager 应用程序和日志文件|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|站点数据库 .mdf 文件|每 25,000 个客户端 75 GB|75 GB|150 GB|300 GB|500 GB|2 TB|  
|站点数据库 .ldf 文件|每 25,000 个客户端 25 GB|25 GB|50 GB|100 GB|150 GB|100 GB|  
|临时数据库文件（.mdf 和 .ldf）|按需而定|按需而定|按需而定|按需而定|按需而定|按需而定|  
|内容（分发点共享）|按需而定<sup>1</sup>|按需而定<sup>1</sup>|按需而定<sup>1</sup>|按需而定<sup>1</sup>|按需而定<sup>1</sup>|按需而定<sup>1</sup>|  

 <sup>1</sup>磁盘空间指导未包括位于站点服务器或分发点上内容库中的内容所需的空间。 有关规划内容库的信息，请参阅[内容库](../../../core/plan-design/hierarchy/the-content-library.md)。  

 在规划磁盘空间要求时，除了考虑上述指南之外，另请考虑下列指南：  

-   每个客户端都需要大约 5 MB 的空间。  

-   规划主站点的临时数据库大小时，其组合大小应为站点数据库 .mdf 文件大小的 25% 到 30%。 实际大小可能会小得多或大得多，具体取决于站点服务器的性能，以及短期和长期的传入数据量。  

    > [!NOTE]  
    >  站点有 50,000 个或更多客户端时，请计划使用 4 个或更多临时数据库 .mdf 文件。  

-   管理中心站点的临时数据库大小通常比主站点的此大小要小得多。  

-   辅助站点数据库的大小有下列限制：  

    -   SQL Server 2012 Express：10 GB  

    -   SQL Server 2014 Express：10 GB  

##  <a name="bkmk_ScaleClient"></a>客户端  
 本部分提供使用 Configuration Manager 客户端软件管理计算机的推荐硬件配置。  

### <a name="client-for-windows-computers"></a>Windows 计算机的客户端  
 以下是使用 Configuration Manager 管理基于 Windows 的计算机的最低要求，包括嵌入的操作系统：  

-   **处理器和内存：**请参阅计算机操作系统的处理器和 RAM 要求。  

-   **磁盘空间：**500 MB 可用磁盘空间，含 5 GB 建议用于 Configuration Manager 客户端缓存。 如果使用自定义设置安装 Configuration Manager 客户端，则需要较少的磁盘空间：  

    -   使用 CCMSetup 命令行属性/skipprereq 避免安装客户端不需要的文件。 例如，如果客户端不使用应用程序目录，则运行 **CCMSetup.exe /skipprereq:silverlight.exe**。  

    -   使用 Client.msi 属性 SMSCACHESIZE 设置小于默认为 5120 MB 的缓存文件。 最小大小为 1 MB。 例如， **CCMSetup.exe SMSCachesize=2** 创建大小为 2 MB 的缓存。  

    有关这些客户端安装设置的详细信息，请参阅[关于 System Center Configuration Manager 的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

    > [!TIP]  
    >  使用最小磁盘空间安装客户端适用于 Windows Embedded 设备，此设备的磁盘大小通常比标准 Windows 计算机的磁盘大小要小。  



 以下是 Configuration Manager 中可选功能的其他最低硬件要求。  

-   **操作系统部署：**384 MB RAM  

-   **软件中心：**500 MHz 处理器  

-   **远程控制：**Pentium 4 Hyper-Threaded 3 GHz（单核）或类似的 CPU，包含至少 1 GB RAM 以获得最佳体验  

### <a name="client-for-linux-and-unix"></a>适用于 Linux 和 UNIX 的客户端  
 以下是对使用 Configuration Manager 管理的 Linux 和 UNIX 服务器的最低要求。  

|要求|详细信息|  
|-----------------|-------------|  
|处理器和内存|请参阅计算机操作系统的处理器和 RAM 要求。|  
|硬盘空间|500 MB 可用磁盘空间，含 5 GB 建议用于 Configuration Manager 客户端缓存。|  
|网络连接|Configuration Manager 客户端计算机必须具有到 Configuration Manager 站点系统的网络连接才能启用管理。|  

##  <a name="bkmk_ScaleConsole"></a> Configuration Manager 控制台  
 下表中的要求适用于运行 Configuration Manager 控制台的每台计算机。  

 **最低硬件配置：**  

-   Intel i3 或相当的 CPU  

-   2 GB RAM  

-   2 GB 磁盘空间  

|DPI 设置|最小分辨率|  
|-----------------|------------------------|  
|96/100%|1024 x 768|  
|120/125%|1280 x 960|  
|144/150%|1600 x 1200|  
|196/200%|2500 x 1600|  

 **支持 PowerShell：**  

 在运行 Configuration Manager 控制台的计算机上安装针对 PowerShell 的支持时，可以在该计算机上运行 PowerShell cmdlet 以管理 Configuration Manager。

 - 支持 PowerShell 3.0 或更高版本

除 PowerShell 以外，还支持 Management Framework (WMF) 版本 3.0 或更高版本。   


##  <a name="bkmk_ScaleLab"></a>实验室部署  
 对 Configuration Manager 的实验室和测试部署使用下列建议的最低硬件配置。 这些建议适用于所有站点类型，并可用于最多 100 个客户端：  

|角色|CPU（核心数）|内存(GB)|硬盘空间 (GB)|  
|----------|---------------|-------------------|-----------------------|  
|站点和数据库服务器|2 - 4|7 - 12|100|  
|站点系统服务器|1 - 4|2 - 4|50|  
|客户端|1 - 2|1 - 3|30|  
