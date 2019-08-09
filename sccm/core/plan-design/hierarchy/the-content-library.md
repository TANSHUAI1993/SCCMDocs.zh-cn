---
title: 内容库
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 用于减少已分发内容总大小的内容库。
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb4efaf8fb424ee4f6af221ad5316d8fd03f8aa0
ms.sourcegitcommit: ef7800a294e5db5d751921c34f60296c1642fc1f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68712580"
---
# <a name="the-content-library-in-configuration-manager"></a>Configuration Manager 中的内容库

适用范围：  System Center Configuration Manager (Current Branch)

内容库是 Configuration Manager 中内容的单实例存储。 站点用它减少分发内容组合正文的总体大小。 内容库存储软件部署的所有内容文件，例如：软件更新、应用程序和操作系统部署。  

- 站点在每个站点服务器和每个分发点上自动创建并维护内容库的副本。  

- 在 Configuration Manager 将内容文件添加到站点服务器或将文件复制到分发点之前，它会验证每个内容文件是否已在内容库中。  

- 如果内容文件可用，则 Configuration Manager 不会复制该文件。 而是将现有内容文件与应用程序或包相关联。  

在分发点服务器上配置以下选项：

- 希望在其上创建内容库的一个或多个磁盘驱动器。  

- 使用的每个驱动器的优先级。  

Configuration Manager 将内容文件复制到优先级最高的驱动器中，直到该驱动器的可用空间小于所指定的最小可用空间。  

- 在分发点安装过程中，你可以配置驱动器设置。  

- 安装完成后，无法在分发点属性中配置驱动器设置。  

有关如何为分发点配置驱动器设置的详细信息，请参阅[管理内容和内容基础结构](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)。  

> [!IMPORTANT]
> 若要在安装后将内容库移到分发点上的另一位置，请使用 Configuration Manager 工具中的内容库传输工具  。 有关详细信息，请参阅[内容库传输工具](/sccm/core/support/content-library-transfer)。  


## <a name="about-the-content-library-on-the-central-administration-site"></a>关于管理中心站点上的内容库

默认情况下，安装站点时，Configuration Manager 会在管理中心站点上创建内容库。 该内容库放置在具有最多可用磁盘空间的站点服务器驱动器上。 因为无法在管理中心站点上安装分发点，所以无法设置内容库要使用的驱动器的优先级。 类似于其他站点服务器和分发点上的内容库，当包含内容库的驱动器可用磁盘空间不足时，内容库会自动跨越到下一个可用的驱动器。  

Configuration Manager 会在以下情况下使用管理中心站点上的内容库：  

- 在管理中心站点上创建内容  

- 迁移另一个 Configuration Manager 站点中的内容，并将管理中心站点指定为管理该内容的站点  

> [!NOTE]  
> 在主站点创建内容，然后将其分发给其他主站点或其他主站点下面的辅助站点，管理中心站点将该内容临时存储在管理中心站点上的计划员收件箱中，但未将该内容添加到其内容库中。  

使用以下选项管理位于管理中心站点上的内容库：  

- 若要防止在特定驱动器上安装内容库，请创建名为 no_sms_on_drive.sms 的空文件  。 在创建内容库之前将其复制到驱动器的根目录下。  

- 创建内容库之后，请使用 Configuration Manager 工具中的内容库传输工具来管理内容库的位置  。 有关详细信息，请参阅[内容库传输工具](/sccm/core/support/content-library-transfer)。  

> [!Note]  
> 云分发点不使用单实例存储。 该站点在将包发送到 Azure 之前对其进行加密，每个包都有一个唯一的加密密钥。 即使两个文件完全相同，加密版本也不一样。  


## <a name="bkmk_remote"></a>配置用于站点服务器的远程内容库

<!--1357525-->
从 1806 版开始，若要配置[站点服务器高可用性](/sccm/core/servers/deploy/configure/site-server-high-availability)或释放管理中心或主站点服务器上的硬盘空间，请将内容库重定位到另一个存储位置。 将内容库移至站点服务器上的另一个驱动器、单独服务器或者存储区域网络 (SAN) 中的容错磁盘。 建议移至 SAN，因为它具有高可用性，并提供弹性存储，即存储可随时间推移而增长或收缩，以满足不断变化的内容需求。 有关详细信息，请参阅[高可用性选项](/sccm/protect/understand/high-availability-options)。

远程内容库是[站点服务器高可用性](/sccm/core/servers/deploy/configure/site-server-high-availability)的先决条件。

> [!Note]  
> 此操作仅在站点服务器上移动内容库。 它不会影响分发点上的内容库的位置。 

> [!Tip]  
> 此外还需计划管理内容库外部的包源内容。 Configuration Manager 中的每个软件对象都在网络共享上具有包源。 请考虑将所有源集中到单个共享，但请确保此位置冗余且高度可用。
>
> 如果将内容库移动到与包源相同的存储卷，则无法标记此卷用于重复数据删除。 虽然内容库支持重复数据删除，但包源卷不支持。 有关详细信息，请参阅[重复数据删除](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmmk_datadedup)。<!--SCCMDOcs issue #831-->  

### <a name="prerequisites"></a>先决条件  

- 站点服务器计算机帐户需要将内容库移至其中的网络路径的“完全控制”权限  。 此权限适用于共享和文件系统。 远程系统上不安装任何组件。

- 站点服务器无法获得分发点角色。 分发点也使用内容库，并且此角色不支持远程内容库。 移动内容库后，无法将分发点角色添加到站点服务器。  

> [!Important]  
> 不要在多个站点之间重复使用共享网络位置。 例如，不要对管理中心站点和子主站点使用相同的路径。 此配置可能导致内容库损坏并需要重新生成。<!--SCCMDocs-pr issue 2764-->  

### <a name="process-to-manage-the-content-library"></a>管理内容库的过程

1. 在网络共享中创建一个文件夹作为内容库的目标。 例如，`\\server\share\folder`。  

    > [!Warning]  
    > 请勿重复使用包含内容的现有文件夹。 例如，不要使用与包源相同的文件夹。 在复制内容库之前，Configuration Manager 会从指定的位置删除任何现有内容。  

2. 在 Configuration Manager 控制台中，切换到“管理”  工作区。 展开“站点配置”，选择“站点”节点，然后选择站点   。 在详细信息窗格底部的“摘要”  选项卡上，注意“内容库”  的新列。  

3. 选择功能区上的“管理内容库”  。  

4. 在“管理内容库”窗口中，“当前位置”字段将显示本地驱动器和路径  。 在“新位置”中输入有效网络路径  。 此路径是站点将内容库移至其中的位置。 它必须包含已存在于共享上的文件夹名称，例如，`\\server\share\folder`。 选择“确定”  。  

5. 请注意细节窗格“摘要”选项卡上“内容库”列中的“状态”值  。 它会更新以显示站点在移动内容库方面的进度。  

   - 处于“正在进行”状态时，“移动进度(%)”值将显示完成百分比   。  

        > [!Note]  
        > 如果有大型内容库，可能会在一段时间内看到控制台中的进度为 `0%`。 例如，使用 1 TB 库时，在显示 `1%` 之前，它必须复制 10 GB 的数据。 查看 distmgr.log  ，它显示了复制的文件数和字节数。 从 1810 版开始，日志文件还会显示估计的剩余时间。

   - 如果存在错误状态，状态将显示错误。 常见错误包括“访问被拒绝”或“磁盘已满”   。  

   - 完成时，显示“完成”  。  

     有关详细信息，请参阅 **distmgr.log**。 有关详细信息，请参阅[站点服务器和站点系统服务器日志](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog)。  

有关此过程的详细信息，请参阅[流程图 - 管理内容库](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart)。

实际上，站点将内容库文件复制到远程位置  。 此过程不会删除站点服务器上原始位置的内容库文件。 若要释放空间，管理员必须手动删除这些原始文件。

如果原始内容库跨两个驱动器，该库将在新目标中合并为单个文件夹。

从版本 1810 开始，在复制过程中，Despooler  和分发管理器  组件不会处理新包。 此操作可确保该内容在移动时不会添加到库中。 无论如何，在系统维护期间安排此更改。

如果需要将内容库移回站点服务器，请重复此过程，但在“新位置”中输入本地驱动器和路径  。 它必须包含已存在于驱动器上的文件夹名称，例如，`D:\SCCMContentLib`。 如果原始内容仍存在，该过程会快速将配置移动到站点服务器的本地位置。

> [!Tip]  
> 若要将内容移动到站点服务器上的另一个驱动器，请使用“内容库传输”  工具。 有关详细信息，请参阅[内容库传输工具](/sccm/core/support/content-library-transfer)。  


## <a name="inside-the-content-library"></a>在内容库内

> [!Warning]  
> 以下部分仅供参考。 请勿更改、添加或删除内容库中的任何文件或文件夹。 执行此操作可能会损坏包、内容或整个内容库。 如果怀疑存在任何缺失、损坏或无效数据，请使用 Configuration Manager 控制台中的验证功能来检测此类问题。 然后重新分发受影响的内容，从而解决问题。

默认情况下，内容库存储在驱动器根目录上名为 SCCMContentLib 的文件夹中  。 默认情况下，此文件夹共享为 SCCMContentLib$  。 文件夹和共享具有受限权限，以防止意外损坏。 应从 Configuration Manager 控制台进行所有更改。 此文件夹中具有以下对象：  

- 包库（PkgLib 文件夹）  ：有关分发点上存在哪些包的信息。  

- 数据库（DataLib 文件夹）  ：有关包的原始结构的信息。  

- 文件库（FileLib 文件夹）  ：包中的原始文件。 通常情况下，此文件夹占用大部分存储。  

![Configuration Manager 内容库关系图概述](media/content-library-overview.png)

> [!Tip]  
> 使用 Configuration Manager 工具中的“内容库资源管理器”工具浏览内容库的内容  。 此工具不能用于修改内容。 借助它，用户可了解现有内容，并能进行验证和重新分发。 有关详细信息，请参阅[内容库资源管理器](/sccm/core/support/content-library-explorer)。  

### <a name="package-library"></a>包库

包库文件夹 PkgLib 中针对分发到分发点的每个包具有一个文件  。 文件名称是包 ID，例如，`ABC00001.INI`。 此文件的 `[Packages]` 部分为内容 ID 列表，这些 ID 由部分包内容及版本等其他信息组成。 例如，ABC00001 是版本 1 的旧版包   。 其在此文件中的内容 ID 是 `ABC00001.1`。

### <a name="data-library"></a>数据库

数据库文件夹 DataLib 针对每个包中的每项内容具有一个文件和一个文件夹  。 例如，此文件和文件夹分别名为 `ABC00001.1.INI` 和 `ABC00001.1`。 该文件包含用于验证的信息。 该文件夹从原始包重新创建文件夹结构。

数据库中的文件将被具有包中原始文件名称的 INI 文件替换。 例如，`MyFile.exe.INI`。 这些文件包含有关原始文件的信息，例如大小、修改时间和哈希。 使用哈希的前四个字符在文件库找到原始文件。 例如，MyFile.exe.INI 中的哈希为 DEF98765，前四个字符为 DEF9   。

### <a name="file-library"></a>文件库

如果内容库跨多个驱动器，则包文件可能位于其中任一驱动器上的文件库文件夹 FileLib 中  。

使用在数据库中找到的哈希的前四个字符查找特定文件。 文件库文件夹内有多个文件夹，每个文件夹都有一个四个字符的名称。 查找与哈希中前四个字符匹配的文件夹。 找到此文件夹后，可发现其中包含一组或多组三个文件。 这些文件共享相同的名称，但其中一个具有扩展名 INI，一个具有扩展名 SIG，另一个没有文件扩展名。 原始文件是没有扩展名的文件，其名称与数据库中的哈希一致。

例如，文件夹 DEF9 包括 `DEF98765.INI`、`DEF98765.SIG` 和 `DEF98765`  。 `DEF98765` 是原始 `MyFile.exe`。 INI 文件包括共享相同文件的“用户”或内容 ID 列表。 除非删除了所有这些内容，否则该站点不会删除文件。

### <a name="drive-spanning"></a>跨驱动器

内容库可跨多个驱动器。 在创建分发点时选择这些驱动器。 默认情况下，Configuration Manager 会在跨越内容库时自动选择驱动器。

选择驱动器时，需选择主驱动器和辅助驱动器。 站点将所有元数据存储在主驱动器上。 只将文件库跨越到辅助驱动器。 辅助驱动器的文件夹共享名称包括驱动器号。 例如，如果 D: 和 E: 是内容库的辅助驱动器，则共享名为 SCCMContentLibD$ 和 SCCMContentLibE$   。

如果选择“自动”选项，Configuration Manager 将选择具有最多可用空间的驱动器作为其主驱动器  。 它在此驱动器上存储所有元数据。 该站点只将文件库跨越到辅助驱动器。

在配置期间指定保留空间量。 最佳可用磁盘仅剩余此保留空间量后，Configuration Manager 将尝试使用辅助磁盘。 每次选择使用新驱动器时，都会选择具有最多可用空间的驱动器。

无法指定分发点使用除特定一组驱动器之外的所有驱动器。 在驱动器的根目录上创建一个名为 `NO_SMS_ON_DRIVE.SMS` 的空文件可防止此行为。 在 Configuration Manager 选择要使用的驱动器之前创建此文件。 如果 Configuration Manager 在驱动器的根目录上检测到此文件，那么它不会将该驱动器用于内容库。


## <a name="troubleshooting"></a>故障排除

以下提示可帮助解决内容库问题：  

- 查看站点服务器上的日志（distmgr.log 和 PkgXferMgr.log）和分发点上的日志 (smsdpprov.log)，获取指向故障的任何指示    。  

- 使用[内容库资源管理器](/sccm/core/support/content-library-explorer)工具。  

- 检查其他进程（如防病毒软件）锁定的文件。 所有驱动器上的内容库均不执行自动防病毒扫描，也不包含在每个驱动器上的临时分段目录 SMS_DP$ 中  。  

- 若要查看是否存在任何哈希不匹配的情况，请从 Configuration Manager 控制台进行包验证。  

- 最后，也可选择重新分发内容。 此操作应能解决大多数问题。  
