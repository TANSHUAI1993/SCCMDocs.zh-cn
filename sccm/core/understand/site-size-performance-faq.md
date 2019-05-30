---
title: 站点规模和性能常见问题解答
titleSuffix: Configuration Manager
description: 有关站点规模和性能的常见 System Center Configuration Manager 问题的解答。
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 8157ee2212e18d4938beabd40f16e66a319d0b8c
ms.sourcegitcommit: cab3dba5ebfe90f28cedee03c1840c9a395160cc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65849291"
---
# <a name="system-center-configuration-manager-site-sizing-and-performance-faq"></a>System Center Configuration Manager 站点规模和性能常见问题解答

适用范围：  System Center Configuration Manager (Current Branch)

本文档提供有关 Configuration Manager 站点规模指南和性能的常见问题解答。

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>计算机和磁盘配置常见问题解答和示例

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>应该如何设置站点服务器和 SQL Server 上的磁盘格式？

将 Configuration Manager 收件箱和 SQL 文件在至少两个不同卷上分开。 通过这种分离，可以为其执行的不同类型的 I/O 优化群集分配大小。 

对于托管站点服务器收件箱的卷，请使用具有 4K 或 8K 分配单元的 NTFS。 即使是小文件，ReFS 也会写入 64k。 Configuration Manager 有许多小文件，因此 ReFS 会产生不必要的磁盘开销。

对于包含 SQL 数据库文件的磁盘，请使用具有 64K 分配单元的 NTFS 或 ReFS 格式。

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>我应该如何以及在何处布置我的 SQL 数据库文件？

新式固态硬盘 (SSD) 阵列和 Azure 高级存储只需很少的磁盘即可在单个卷上提供高 IOPS。 通常向阵列中添加更多硬盘是为了增加存储，而不是增加吞吐量。 如果使用基于主轴的物理磁盘，可能需要比单个卷上生成的 IOPS 更多的 IOPS。 应该为 .mdf 文件分配 60% 的总推荐 IOPS 和磁盘空间，为 .ldf 文件分配 20%，为日志和数据临时文件分配 20%   。 .ldf 和临时文件都可以驻留在单个卷上，占所分配的 IOPS 的 40% (20% + 20%)  。

默认情况下，SQL 会创建一个临时数据文件。 应该创建更多文件，以避免 SQL 锁定和等待对单个文件的访问。 社区对要创建的临时数据文件的最佳数量意见不一，从 4 个到 8 个不等。 测试显示 4 到 8 之间没有什么差别，所以可以创建 4 个大小相同的临时数据文件  。 tempdb 数据文件应该占整个数据库大小的 20-25%。

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>对于磁盘设置还有其他建议吗？

如果可配置，请将 RAID 控制器内存设置为写入操作分配 70%，读取操作分配 30%。 通常，站点数据库使用 RAID 10 阵列配置。 对于 I/O 要求较低的小规模站点，或者使用快速 SSD 的情况，也可以使用 RAID 1。 对于较大的磁盘阵列，请配置备用磁盘以自动替换故障磁盘。

**示例：带物理磁盘的物理计算机** 

对于具有 100,000 个客户端的并置站点服务器和 SQL Server，其[大小调整准则](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)是站点服务器收件箱 IOPS 为 1200，SQL Server 文件的 IOPS 为 5000  。

生成的磁盘配置可能如下所示：

| 驱动器<sup>1</sup> | RAID | 格式 | 卷内容 | 所需的最小 IOPS| 大约提供的 IOPS<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS 8k     | ConfigMgr 收件箱    |     1700            | 1751             |
| 12x15k         | 10        | 64k ReFS    | SQL .mdf             | 60%*5000 = 3000     | 3476             |
| 8x15k          | 10        | 64k ReFS    | SQL .ldf，临时文件 | 40%*5000 = 2000     | 2322             |

1. 不包括建议的备用磁盘。 
2. 此值来自[示例磁盘配置](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)。 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>我在 Windows Server 上使用 Hyper-V。 如何为 Configuration Manager VM 配置磁盘以获得最佳性能？

如果硬件资源（CPU 核心和直通存储）100% 专用于虚拟机 (VM)，则 Hyper-V 可提供与物理服务器类似的性能。 使用固定大小的“.vhd”或“.vhdx”磁盘文件会导致最低 1-5% 的 I/O 性能影响   。 使用动态扩展的“.vhd”或“.vhdx”磁盘文件会对 Configuration Manager 工作负载造成高达 25% 的 I/O 性能影响   。 如果需要动态扩展磁盘，请通过向阵列添加额外的 25% IOPS 性能来进行补偿。

在 VM 中运行 Configuration Manager 站点服务器或 SQL 时，请将 Hyper-V 主机 OS 驱动器与 VM OS 和数据驱动器隔离。

有关优化 VM 的详细信息，请参阅[对 Hyper-V 服务器进行性能优化](/windows-server/administration/performance-tuning/role/hyper-v-server/)。

**示例：基于 Hyper-V VM 的站点服务器** 

对于具有 150,000 个客户端的并置站点服务器和 SQL Server，其[大小调整准则](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)是站点服务器收件箱 IOPS 为 1800，SQL Server 文件的 IOPS 为 7400  。

生成的磁盘配置可能如下所示：

| 驱动器<sup>1</sup> | RAID | 格式<sup>2</sup> | 卷内容 | 所需的最小 IOPS| 大约提供的 IOPS<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | HYPER-V 主机 OS           | -                    | -                |
| 2x10k          | 1         | -              | (VM) 站点服务器 OS       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS 8k        | (VM) ConfigMgr 收件箱    | 1800                 | 7539             |
| 4xSSD SAS      | 10        | 64k ReFS       | (VM) 主机 SQL（所有文件） | 7400                 | 14346            |

1. 不包括建议的备用磁盘。 
2. 固定大小、直通 .vhdx，用于专用于底层卷的 VM 驱动器  。 
3. 此值来自[示例磁盘配置](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)。 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>对于 Microsoft Azure 中的 Configuration Manager 环境有什么建议？

首先，阅读 [Azure 上的 Configuration Manager 常见问题解答](configuration-manager-on-azure.md)。

利用基于高级存储的磁盘的 Azure 基础结构即服务 (IaaS) VM 可具有较高的 IOPS。 在这些 VM 上，请配置其他磁盘以满足预期的磁盘空间需求，而不是满足额外的 IOPS 需求。

Azure 存储本质上是冗余的，并且不需要多个磁盘来提供可用性。 可以在磁盘管理器或存储空间中对磁盘进行条带化，以提供额外的空间和性能。

要详细了解如何在 Azure IaaS VM 中最大程度提高高级存储性能并运行 SQL Server，请参阅：

- [优化应用程序性能](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [磁盘指南](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**示例：基于 Azure 的站点服务器** 

对于具有 50,000 个客户端的并置站点服务器和 SQL Server，其[大小调整准则](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)是站点服务器收件箱为 8 核、32 GB 和 1200 IOPS，SQL Server 文件为 2800 IOPS  。

生成的 Azure 计算机可能为 DS13v2（8 核，56 GB），具有以下磁盘配置：

| 驱动器 | 格式 | 包含 | 所需的最小 IOPS| 大约提供的 IOPS<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;标准&gt;： | -             | 站点服务器 OS     | -                    | -                |
| 1xP20 (512 GB)    | NTFS 8k       | ConfigMgr 收件箱  | 1200                 | 2334             |
| 1xP30 (1024 GB)   | 64k ReFS      | SQL（所有文件<sup>2</sup>） | 2800                 | 3112             |

1. 此值来自[示例磁盘配置](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)。
2. [Azure 指南](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)允许将 TempDB 放在基于 SSD 的本地 D: 驱动器上，前提是它不会超出可用空间，并且允许额外的磁盘 I/O 分发  。

**示例：基于 Azure 的站点服务器（用于即时性能提升）** 

Azure 磁盘吞吐量受 VM 大小的限制。 前面的 Azure 示例中的配置可能会限制将来的扩展或其他性能。 如果在初始部署 Azure VM 期间添加其他磁盘，则可以增加 Azure VM 大小，以使用最少的前期投资实现未来处理能力的提升。 与后期需要执行较复杂的迁移相比，提前计划根据需求变化增加站点性能要容易的多。

更改前面 Azure 示例中的磁盘，看看 IOPS 的变化情况。

**DS13v2** 

| 驱动器<sup>1</sup> | 格式 | 包含 | 所需的最小 IOPS| 大约提供的 IOPS<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;标准&gt;： | -             | 站点服务器 OS     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | ConfigMgr 收件箱  | 1200                 | 3984             |
| 2xP30 (2048 GB)   | 64k ReFS      | SQL（所有文件<sup>3</sup>） | 2800                 | 3984             |

1. 磁盘使用存储空间进行条带化。
2. 此值来自[示例磁盘配置](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)。 VM 大小限制性能。
3. [Azure 指南](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)允许将 TempDB 放在基于 SSD 的本地 D: 驱动器上，前提是它不会超出可用空间，并且允许额外的磁盘 I/O 分发  。

如果将来需要更高的性能，可将 VM 大小增加到 DS14v2，这将使 CPU 和内存加倍。 该 VM 大小所支持的额外磁盘带宽也将立即增加先前配置磁盘上的可用磁盘 IOPS。

**DS14v2**

| 驱动器<sup>1</sup> | RAID | 格式 | 包含 | 所需的最小 IOPS| 大约提供的 IOPS<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;标准&gt;： | -             | 站点服务器 OS     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | ConfigMgr 收件箱  | 1200                 | 4639             |
| 2xP30 (2048 GB)   | 64k ReFS      | SQL（所有文件<sup>3</sup>） | 2800                 | 6182             |

1. 磁盘使用存储空间进行条带化。
2. 此值来自[示例磁盘配置](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)。 VM 大小限制性能。
3. [Azure 指南](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)允许将 TempDB 放在基于 SSD 的本地 D: 驱动器上，前提是它不会超出可用空间，并且允许额外的磁盘 I/O 分发  。

## <a name="other-common-sql-server-related-performance-questions"></a>其他常见的与 SQL Server 相关的性能问题 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>是使用与站点服务器并置的 SQL 运行更好，还是在远程服务器上运行更好？

假设单个服务器的大小合适，或者两个服务器之间的网络连接足够，则这两种方式都可以提供充足的性能。

远程 SQL 需要使用额外服务器，从而产生前期和运营费用，但这对于大多数大型客户而言是常见的。 此配置的好处包括：

- 增加了站点可用性选项，例如 SQL Always On
- 可以在站点处理开销较低的情况下运行繁重报告
- 简化某些情况下的灾难恢复
- 安全管理更轻松
- SQL 管理的角色分离，例如使用单独的 DBA 团队

并置 SQL 需要使用单个服务器，这对于大多数小规模客户而言是常见的。 此配置的好处包括：

- 降低计算机、许可证和维护成本
- 站点中的故障点较少
- 更好地控制计划停机时间

### <a name="how-much-ram-should-i-allocate-for-sql"></a>应该为 SQL 分配多少 RAM？

默认情况下，SQL 使用服务器上的所有可用内存，可能会使操作系统和计算机上的其他进程无法使用内存。 为避免潜在的性能问题，请务必为 SQL 明确分配内存。 在与 SQL Server 共置的站点服务器上，确保操作系统具有足够的 RAM 用于文件缓存和其他操作。 请确保剩余足够的 RAM 可供 SMSExec 和其他 Configuration Manager 进程使用。 在远程服务器上运行 SQL 时，可以将大部分内存分配给 SQL，但不是全部内存  。 查看[大小调整准则](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)以获取初步指导。 

SQL Server 内存分配应该四舍五入到整数 GB。 此外，随着 RAM 大量增加，可以让 SQL 所占百分比更高。 例如，当 256 GB 或更多 RAM 可用时，可以将 SQL 配置为最高 95%，因为这仍然可以为操作系统保留足够的内存。 监视页面文件是确保操作系统和任何 Configuration Manager 进程有足够内存的好方法。

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>现在内核很便宜。 我是否应该将一些内核添加到我的 SQL Server 中？

如果 SQL Server 上有超过 16 个物理内核，并且没有足够的 RAM，那么可能会出现内存争用问题。 当每个内核至少有 3-4 GB 的 RAM 可用于 SQL 时，Configuration Manager 工作负载的性能会更好。 向 SQL Server 添加内核时，请务必按比例增加 RAM。

### <a name="will-sql-always-on-impact-my-performance"></a>SQL Always On 会影响我的性能吗？

通常，当 SQL 副本服务器之间有足够的网络连接时，SQL Always On 对系统性能的影响可以忽略不计。 在繁忙的 SQL Always On 环境中，.ldf 数据库日志文件的数量会快速增加  。 但是，数据库备份成功后会自动释放日志文件空间。 为 Configuration Manager 数据库添加 SQL 作业以执行备份，例如每 24 小时备份一次，每 6 小时执行一次 .ldf 备份  。 有关 SQL Always On 和 Configuration Manager 的详细信息（包括有关 SQL 备份策略的详细信息），请参阅[适用于高可用性站点数据库的 SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。

### <a name="should-i-enable-sql-compression-on-my-database"></a>应该在数据库上启用 SQL 压缩吗？

不建议 Configuration Manager 数据库使用 SQL 压缩。 虽然在 Configuration Manager 数据库上启用压缩不会出现任何功能问题，但测试结果没有显示出较大的大小节省，与此相比，还可能对系统产生相当大的性能影响。

### <a name="should-i-enable-sql-encryption-on-my-database"></a>应该在数据库上启用 SQL 加密吗？

Configuration Manager 数据库中的任何机密都已安全存储，但添加 SQL 加密可以增加另一层安全性。 在数据库上启用加密不会出现任何功能问题，但性能降低可能高达 25%，具体取决于你选择加密的表和你正在使用的 SQL 版本。 因此，请谨慎加密，尤其是在大型环境中。 另请记住更新备份和恢复计划，以确保可以成功恢复加密数据。

### <a name="what-version-of-sql-should-i-run"></a>应该运行什么版本的 SQL？

有关受支持的 SQL 版本，请参阅[对 SQL Server 版本的支持](../plan-design/configs/support-for-sql-server-versions.md)。 从性能的角度来看，所有受支持的 SQL 版本都满足所需的性能标准。 然而，在 Configuration Manager 工作负载的某些方面，SQL 2012 和 SQL 2016 或更新版本的性能往往优于 SQL 2014。 此外，在 SQL 2012 兼容级别 (110) 上运行 SQL 2014 通常可以提高性能。 在安装时，SQL 2012 和 SQL 2014 上运行的 Configuration Manager 数据库被设置为兼容级别 110。 SQL 2016 或更高版本被设置为 SQL 版本的默认兼容级别，例如 SQL 2016 为 130。 在安装下一个主要 Configuration Manager 当前分支版本之前，就地升级 SQL 不会更新兼容级别。 

如果发现 SQL 2016 或更高版本上的某些 SQL 查询异常超时或运行缓慢（例如在管理员控制台中使用 RBAC 时），请尝试将 Configuration Manager 数据库上的 SQL 兼容级别更改为 110。 完全支持在 SQL 2014 和更新版本的 SQL 上以 SQL 兼容级别 110 运行。 有关详细信息，请参阅 [SQL 查询超时或控制台上某些 Configuration Manager 数据库查询速度慢](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d)。

从 2018 年 1 月开始，由于存在各种已知的性能相关问题或其他潜在问题，应该避免使用以下 SQL 版本  ：

- SQL 2012 SP3 CU1 到 CU5
- SQL 2014 SP1 CU6 到 SP2 CU2
- SQL 2016 RTM 到 CU3，SP1 CU3 到 CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>我应该执行任何其他 SQL 索引任务吗？

是的，每周更新一次索引，每天更新一次统计数据，以提高 SQL 性能。 Configuration Manager 和 SQL 社区提供的第三方脚本和其他信息可以帮助优化这些任务。

在大型站点中，某些 SQL 表（例如 CI\_CurrentComplianceStatusDetails、HinvChangeLog）可能很大，具体取决于你的使用模式。 可能需要逐一减少或改变对其的维护方法。

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>我应该在什么时候在辅助站点上使用完整的 SQL Server 而不是 SQL Express？

SQL Express 对辅助站点没有任何重大的性能影响，它对于大多数客户来说已经够用了。 它还易于部署和管理，并且是适用于几乎所有客户（无论大小）的推荐配置。

有一种情况可能需要完整的 SQL Server 安装。 如果环境中有大量的分发点和包或源，则可能超过 SQL Express 的 10 GB 大小限制。 如果包数量与分发点数量的乘积超过 4,000,000（例如包含 2,000 个内容片段的 2,000 个 DP），请考虑在辅助站点上使用完整的 SQL Server。 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>应该更改数据库中的 MaxDOP 设置吗？

在大多数情况下，将设置保留为 0（使用所有可用的处理器）是实现整体处理性能的最佳选择。

许多 Configuration Manager 管理员都遵循 [SQL Server 中“最大并行度”配置选项的建议和指南](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi)中的指导。 对于大多数新式大型硬件，根据此指导，建议的最大设置为 8。 但是，如果与处理器数量相比，运行的小型查询较多，则将其设置为更高的数量可能会有所帮助。 如果有更多内核可用，则对于较大站点而言，将最大值设置为 8 并不一定是最佳设置。 

对于具有超过 8 个内核的 SQL Server，首先设置为 0，之后仅当出现性能问题或过度锁定时才进行更改。 如果在设置为 0 的情况下出现性能问题而需要更改 MaxDOP，那么可以从一个至少大于或等于用于该站点 SQL Server 大小调整的最小推荐内核数量的新值开始设置。 如果低于这个值，则几乎总是会对性能产生负面影响。 例如，用于 100,000 个客户端站点的远程 SQL Server 至少需要 12 个内核。 如果 SQL Server 有 16 个内核，请先使用值 12 测试 MaxDOP 设置。

## <a name="other-common-performance-related-questions"></a>其他与性能相关的常见问题

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>应该为防病毒软件排除站点服务器（或其他角色）上的哪些文件夹？

在任何系统上禁用防病毒保护时必须谨慎操作。 在高容量的安全环境中，我们建议禁用“主动监视”以获得最佳性能  。

有关推荐的防病毒排除项的详细信息，请参阅[针对 Configuration Manager 2012 和 Current Branch 站点服务器、站点系统和客户端的推荐防病毒排除项](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu)。

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>当 WSUS 与 Configuration Manager 配合使用时，可以如何提高 WSUS 的性能？

更改一些关键的 IIS 设置（例如 WsusPool 队列长度和 WsusPool 专用内存限制）可以提高 WSUS 性能，即使在较小的安装上也是如此。 有关详细信息，请参阅[推荐的硬件](../plan-design/configs/recommended-hardware.md)。

此外，请确保已为运行 WSUS 的操作系统安装了最新的更新：

- Windows Server 2012：2017 年 10 月或之后发布的任何非“仅安全性”累积更新。 ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2：2017 年 8 月或之后发布的任何非“仅安全性”累积更新。 ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Window Server 2016：2017 年 8 月或之后发布的任何非“仅安全性”累积更新。 ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>应该在 WSUS 服务器上运行哪种类型的维护？

请参阅 [Microsoft WSUS 和 Configuration Manager SUP 维护的完整指南](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint)。

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>我想为我的网站设置基本的性能监视。 我应该注意什么？

传统的服务器性能监视对于常规 Configuration Manager 非常有效。 还可以利用 Configuration Manager、SQL Server 和 Windows Server 的各种 System Center Operations Manager 管理包来监视服务器的基本运行状况。 还可以直接监视 Configuration Manager 提供的 Windows 性能监视器 (PerfMon) 计数器。 监视各个收件箱中的积压工作 (backlog)，以获取潜在站点性能问题或积压工作 (backlog) 的早期警告信号。

## <a name="see-also"></a>另请参阅

- [网站大小调整和性能指南](../plan-design/configs/site-size-performance-guidelines.md)
- [Azure 上的 Configuration Manager 常见问题解答](configuration-manager-on-azure.md)
