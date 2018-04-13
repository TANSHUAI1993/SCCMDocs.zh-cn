---
title: 为 OSD 准备站点系统角色
titleSuffix: Configuration Manager
description: 在部署操作系统之前配置站点系统角色
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: 11
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1675f6ed3070972354ea4a14a65339c299ee01f
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="prepare-site-system-roles-for-operating-system-deployments-with-system-center-configuration-manager"></a>在 System Center Configuration Manager 中准备操作系统部署的站点系统角色

*适用范围：System Center Configuration Manager (Current Branch)*

若要在 Configuration Manager 中部署操作系统，首先必须准备以下站点系统角色，这些角色要求具有特定配置并考虑特定注意事项。



##  <a name="BKMK_DistributionPoints"></a> 分发点  
 分发点站点系统角色承载客户端要下载的源文件。 此内容适用于应用程序、软件更新、OS 映像、启动映像和驱动程序包。 你可以通过使用带宽、限制和计划选项来控制内容分发。  

 有足够的分发点支持计算机中的操作系统部署非常重要。 将这些分发点放置在层次结构中的规划也同样重要。 有关详细信息，请参阅[管理内容和内容基础结构](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。 本文涵盖一些特定于 OS 部署的分发点的其他规划注意事项。  


###  <a name="BKMK_AdditionalPlanning"></a> 分发点的其他规划注意事项  
 以下为分发点要考虑的其他规划事项：  

-   **如何避免不需要的 OS 部署?**  

     Configuration Manager 不会将站点服务器与集合中的其他目标计算机进行区分。 如果将所需的任务序列部署到包含站点服务器的集合，则站点服务器会以该集合中的任何其他计算机运行任务序列的方式来运行任务序列。 确保 OS 部署使用包含预期客户端的集合。  

     管理高风险任务序列部署的行为。 高风险部署在客户端上自动安装且可能产生意外结果。 例如，一个用途为“必需”且部署 OS 的任务序列。 若要降低不需要的高风险部署的风险，请配置部署验证设置。 有关详细信息，请参阅[用于管理高风险部署的设置](../../protect/understand/settings-to-manage-high-risk-deployments.md)。  

-   **一次有多少台计算机可以接收来自单个分发点的 OS 映像？**  

     若要估计所需的分发点数量，请考虑以下变量：  
       - 分发点的处理速度
       - 分发点的磁盘速度
       - 网络上的可用带宽
       - 映像包的大小   
  
    例如，在 100 MB/秒的以太网上，如果不考虑任何其他服务器资源因素，则一小时内可以处理 4 千兆字节 (GB) 映像包的计算机的最大数量是 11 台。  

    `100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

    如果必须在特定的时间段内将 OS 部署到特定数量的计算机，请将映像分发到适当数量的分发点。  

-   **能否将 OS 部署到某个分发点？**  

     可以将 OS 部署到某个分发点，但必须从其他分发点接收 OS 映像。  


###  <a name="BKMK_PXEDistributionPoint"></a> 配置分发点以接受 PXE 请求  
 要将操作系统部署到发出 PXE 启动请求的 Configuration Manager 客户端，必须配置一个或多个分发点以接受 PXE 请求。 配置分发点后，此分发点会响应 PXE 启动请求，并确定要执行的适当部署操作。 有关详细信息，请参阅[安装或修改分发点](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#pxe)。  


###  <a name="BKMK_RamDiskTFTP"></a> 在启用 PXE 的分发点上自定义 RamDisk TFTP 块大小和窗口大小  
可以为启用 PXE 的分发点自定义 RamDisk TFTP 块大小和窗口大小。 如果已自定义网络，较大的块或窗口可能会导致启动映像下载由于超时错误而失败。 通过 RamDisk TFTP 块大小和窗口大小自定义，可以在使用 PXE 时优化 TFTP 流量，以满足特定网络要求。 若要确定最高效的设置，请在环境中测试自定义设置。  

-   **TFTP 块大小**：块大小是指服务器发送到正在下载文件的客户端的数据包大小。 较大的块大小使服务器可以发送较少的数据包，因此服务器与客户端之间的往返延迟较少。 但是，较大的块会导致产生零碎的数据包，而大多数 PXE 客户端实现不支持这一点。  

-   **TFTP 窗口大小**：对于发送的每个数据块，TFTP 需要确认 (ACK) 数据包。 服务器在收到上一个块的 ACK 数据包之前，不会发送序列中的下一个块。 通过 TFTP 窗口化可定义填满窗口所需的数据块数量。 服务器在窗口填满之前会背靠背地发送数据块，随后客户端会发送 ACK 数据包。 如果增加此窗口大小，它会减少客户端与服务器之间的往返延迟数，并缩短下载启动映像所需的总体时间。  
  


#### <a name="modify-the-ramdisk-tftp-window-size"></a>修改 RamDisk TFTP 窗口大小  
若要自定义 RamDisk TFTP 窗口大小，请在启用 PXE 的分发点上添加以下注册表项：  

  - **位置**：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  - **名称**：RamDiskTFTPWindowSize  
  - **类型**：REG_DWORD  
  - **值**：&lt;自定义窗口大小>  </br>
     默认值为 **1**（一个数据块填满窗口）  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>修改 RamDisk TFTP 块大小  
若要自定义 RamDisk TFTP 窗口大小，请在启用 PXE 的分发点上添加以下注册表项：  

  - **位置**：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  - **名称**：RamDiskTFTPBlockSize  
  - **类型**：REG_DWORD  
  - **值**：&lt;自定义块大小>  </br>
     默认值为 **4096**。  


###  <a name="BKMK_DPMulticast"></a> 配置分发点以支持多播  
 多播是一种网络优化方法。 当多个客户端可能同时下载相同的 OS 映像时，你可以在分发点上使用多播。 使用多播时，多台计算机可以同时下载 OS 映像，因为该映像由分发点多播。 如果不使用多播，分发点会通过单独的连接向每个客户端发送一份数据副本。 有关详细信息，请参阅[使用多播通过网络部署 Windows](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。  

 在部署 OS 之前，请将分发点配置为支持多播。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast)。


##  <a name="BKMK_StateMigrationPoints"></a> 状态迁移点  
 状态迁移点在一台计算机上存储 USMT 捕获的用户状态数据，然后在另一台计算机上还原这些数据。 但是，当你在同一台计算机上捕获 OS 部署（例如在目标计算机上刷新 Windows 的部署）的用户设置时，可以选择是通过硬链接将数据存储在同一台计算机上还是使用状态迁移点。 对于某些计算机部署，当你创建状态存储时，Configuration Manager 会自动在状态存储和目标计算机之间创建关联。 在规划状态迁移点时，请考虑以下因素：    

### <a name="user-state-size"></a>用户状态大小  
 用户状态大小直接影响到状态迁移点上的磁盘存储和迁移期间的网络性能。 请考虑用户状态大小和要迁移的计算机数量， 以及要从计算机迁移哪些设置。 例如，如果“我的文档”文件夹已备份到服务器，那么，你可能无需在映像部署过程中迁移它。 避免不必要的迁移可以减小用户状态的总大小，并且减轻它本来对网络性能和状态迁移点上的磁盘存储造成的影响。  

### <a name="user-state-migration-tool"></a>用户状态迁移工具  
 若要在部署操作系统的过程中捕获和还原用户状态，必须使用指向 USMT 源文件的用户状态迁移工具 (USMT) 包。 Configuration Manager 将在 Configuration Manager 控制台的“软件库” > “应用程序管理” > “包”中自动创建此包。 Configuration Manager 使用 USMT 10 从一个 OS 捕获用户状态，然后将其还原到另一个 OS。 适用于 Windows 10 的 Windows 评估和部署工具包 (Windows ADK) 包含 USMT 10。

 有关 USMT 10 的不同迁移方案的说明，请参阅 Windows 文档中的[常见迁移方案](/windows/deployment/usmt/usmt-common-migration-scenarios)。  

### <a name="retention-policy"></a>保留策略  
 在配置状态迁移点时，可指定它存储的用户状态数据的保留时间。 此数据在状态迁移点上的保留时间取决于两个因素：  

-   所存储的数据对磁盘存储的影响。  

-   将数据保留一段时间以防重新迁移数据这一潜在要求。
  
  
状态迁移分两个阶段进行：捕获数据和还原数据。 在捕获数据时，收集用户状态数据并将其保存到状态迁移点。 在还原数据时，从状态迁移点检索用户状态数据，然后将其写入目标计算机。之后，“发布状态存储”  任务序列步骤发布所存储的数据。 在发布数据时，保留计时器启动。 如果选择与立即删除迁移的数据有关的选项，则在发布用户状态数据后会立即将其删除。 如果选择与将数据保留一段时间有关的选项，则在发布状态数据之后，经过这段时间就会删除数据。 将保留期设置得越长，可能需要的磁盘空间就越多。  

### <a name="select-drive-to-store-user-state-migration-data"></a>选择要用于储存用户状态迁移数据的驱动器  
 在配置状态迁移点时，必须在服务器上指定用于存储用户状态迁移数据的驱动器。 从固定的驱动器列表中选择驱动器。 但是，一些驱动器可能代表不可写入的驱动器，例如 CD 驱动器或非网络共享的驱动器。 一些驱动器号可能无法映射到计算机上的任何驱动器。 在配置状态迁移点时，请指定一个可写入的共享驱动器。  

### <a name="configure-a-state-migration-point"></a>配置状态迁移点  
 你可以使用下列方法来配置状态迁移点以存储用户状态数据：  

-   使用“创建站点系统服务器向导”  为状态迁移点创建一个新站点系统服务器。  

-   使用“添加站点系统角色向导”  将状态迁移点添加到现有服务器。  

 在使用这些向导时，系统会提示你提供状态迁移点的下列信息：  

-   用于存储用户状态数据的文件夹。  

-   可在状态迁移点上存储数据的客户端的最大数量。  

-   供状态迁移点存储用户状态数据的最小可用空间。  

-   角色的删除策略。 指定在计算机上还原用户状态数据之后立即删除该数据，或在计算机上还原用户数据后特定天数之后再删除该数据。  

-   状态迁移点是否仅响应还原用户状态数据的请求。 如果启用此选项，你将无法使用状态迁移点来存储用户状态数据。  

 有关安装站点系统角色的步骤，请参阅[添加站点系统角色](../../core/servers/deploy/configure/add-site-system-roles.md)。  
