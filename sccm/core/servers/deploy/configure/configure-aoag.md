---
title: 配置可用性组
titleSuffix: Configuration Manager
description: 设置和管理与 Configuration Manager 配合使用的 SQL Server Always On 可用性组
ms.date: 7/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4cc514e37554b8238124255584f59647446baf44
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536542"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>为 Configuration Manager 配置 SQL Server AlwaysOn 可用性组

适用范围：  System Center Configuration Manager (Current Branch)

使用本文提供的信息配置和管理与 Configuration Manager 配合使用的可用性组。

开始之前：  

- 熟悉[准备将 SQL Server AlwaysOn 可用性组与 Configuration Manager 配合使用](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)中的信息。
- 熟悉包括使用可用性组和相关过程的 SQL Server 文档。 需要这些信息来完成以下方案。


## <a name="bkmk_create"></a> 创建和配置可用性组

使用以下过程创建可用性组，然后将站点数据库的副本移动到该可用性组。

1. 使用以下命令可停止 Configuration Manager 站点：

    `preinst.exe /stopsite`

    有关详细信息，请参阅[层次结构维护工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)。

2. 将站点数据库的备份模型从“简单”  更改为“完整”  ：

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    可用性组仅支持“完整”备份模型。 有关详细信息，请参阅[查看或更改数据库的恢复模式](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server)。

3. 使用 SQL Server 创建站点数据库的完整备份。 选择下列选项之一：

    - **将成为可用性组的成员**：如果将此服务器用作可用性组的初始主要副本成员，则不需要将站点数据库副本还原到这个或组中的另一个服务器。 数据库已在主要副本上就位。 SQL Server 在下一步中将数据库复制到次要副本。  

    - **不是可用性组的成员**：将站点数据库的副本还原到将托管组的主要副本的服务器。

    有关详细信息，请参阅 SQL Server 文档中的以下文章：

    - [创建完整数据库备份](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [使用 SSMS 还原数据库备份](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > 如果计划从可用性组移动到现有副本上的独立组，请先从可用性组中删除数据库。

4. 在将托管组的初始主要副本的服务器上，使用[新建可用性组向导](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio)创建可用性组。 在向导中：

    - 在“选择数据库”  页上，为你的 Configuration Manager 站点选择数据库。  

    - 在“添加副本”  页面，配置以下内容：

        - **副本：** 指定将托管次要副本的服务器。

        - **侦听程序：** 将“侦听程序 DNS 名称”  指定为完整的 DNS 名称，例如 `<listener_server>.fabrikam.com`。 将 Configuration Manager 配置为使用可用性组中的数据库时，将使用此名称。

    - 在“选择初始数据同步”  页面，选择“完整”  。 该向导创建可用性组后，向导将备份主数据库和事务日志。 然后在托管次要副本的每个服务器上还原它们。

        > [!Note]  
        > 如果不使用此步骤，请将站点数据库的副本还原到将托管次要副本的每个服务器。 然后将该数据库手动加入组。

5. 检查每个副本上的配置：

    1. 确保站点服务器的计算机帐户是每个可用性组成员计算机上的本地管理员  组的成员。  

    2. 运行[验证脚本](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites)，以确认正确配置了每个副本上的站点数据库。

    3. 如果有必要在次要副本上设置配置，则先将主要副本手动故障转移到次要副本，然后再继续。 只能配置主要副本的数据库。 有关详细信息，请参阅 SQL Server 文档中的[执行可用性组的计划手动故障转移](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server)。

6. 所有副本都满足要求后，可用性组即可与 Configuration Manager 一起使用。


## <a name="bkmk_configure"></a> 配置站点以使用可用性组

[创建和配置可用性组](#bkmk_create)之后，使用 Configuration Manager 站点维护，将站点配置为使用由可用性组托管的数据库。

不支持使用它在可用性组中的数据库安装新站点。 例如，如果你使用基线媒体，则安装使用单个 SQL Server 实例的站点。 安装站点后，即可将站点数据库移到可用性组中。

1. 从 Configuration Manager 站点安装文件夹 `\BIN\X64\setup.exe` 运行 Configuration Manager 安装程序  。

2. 在“入门”  页上，选择“执行站点维护或重置此站点”  ，然后选择“下一步”  。

3. 选择“修改 SQL Server 配置”  ，然后选择“下一步”  。

4. 为站点数据库重新配置以下设置：

    - **SQL Server 名称**：输入可用性组侦听程序  的虚拟名称。 在创建可用性组时配置了侦听程序。 虚拟名称应为完整的 DNS 名称，如 `<Listener_Server>.fabrikam.com`。  

    - **实例：** 若要为可用性组的侦听程序指定默认实例，此值必须为空  。 如果当前站点数据库在命名实例上运行，则会清除当前命名实例。

    - **数据库：** 保留所显示的名称。 这是当前站点数据库的名称。

5. 为新的数据库位置提供此信息后，使用常规过程和配置完成安装。


## <a name="bkmk_sync"></a> 同步副本成员  

当站点数据库在可用性组中托管时，请使用以下过程添加或删除同步的副本成员。 有关支持的类型和副本数的详细信息，请参阅[可用性组配置](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#availability-group-configurations)。

### <a name="bkmk_sync-add"></a> 添加新的同步副本成员

<!--3127336-->
从版本 1906 开始，运行 Configuration Manager 安装程序以添加新的同步副本成员。

1. 使用[层次结构维护工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)停止站点：`preinst.exe /stopsite`

1. 使用 SQL Server 程序修改可用性组：

    1. 从主要副本[创建站点数据库的备份](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)。

    1. [将该备份还原](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)到新的次要副本服务器。

    1. 在 SQL Management Studio 中监视状态。 等待可用性组完全恢复正常运行。

1. 运行 Configuration Manager 安装程序，然后选择修改站点的选项。

1. 将可用性组侦听程序名称指定为数据库名称。 如果侦听程序使用非标准网络端口，也请指定该端口。 此操作会使安装程序确保每个节点都已正确配置。 它还会启动数据库恢复过程。

Configuration Manager 安装程序使用 SQL 数据库移动操作，并确保节点已正确配置。

有关如何在版本 1902 或更早版本中手动执行此过程的详细信息，请参阅 [ConfigMgr 1702：将新节点（次要副本）添加到现有 SQL AO AG](https://blogs.technet.microsoft.com/umairkhan/2017/07/17/configmgr-1702-adding-a-new-node-secondary-replica-to-an-existing-sql-ao-ag/)。

### <a name="remove-a-replica-member"></a>删除副本成员

从版本 1906 开始，可以使用 Configuration Manager 安装程序删除副本成员。 使用同一过程[添加新的同步副本成员](#bkmk_sync-add)。

有关如何在版本 1902 或更早版本中手动执行此过程的详细信息，请参阅[从可用性组中删除次要副本](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server)。  


## <a name="bkmk_async"></a> 异步副本

可以使用与 Configuration Manager 配合使用的可用性组中的异步副本。 无需运行配置同步副本所需的配置脚本，因为站点数据库不支持异步副本。

### <a name="configure-an-asynchronous-commit-replica"></a>配置异步提交副本

有关详细信息，请参阅[将次要副本添加到可用性组](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)。

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>使用异步副本恢复站点

使用异步副本恢复站点数据库。

1. 停止活动的主站点，以防止对站点数据库的额外写入。 要停止站点，请使用[层次结构维护工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)：`preinst.exe /stopsite`

1. 停止站点后，使用异步副本替代[手动恢复的数据库](/sccm/core/servers/manage/recover-sites#use-a-site-database-that-has-been-manually-recovered)。


## <a name="bkmk_stop"></a> 停止使用可用性组

不再需要在可用性组中托管站点数据库时，请使用以下过程。 通过此过程，你会将站点数据库移回 SQL Server 的单个实例。

1. 使用以下命令停止 Configuration Manager 站点：`preinst.exe /stopsite`。 有关详细信息，请参阅[层次结构维护工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)。

2. 使用 SQL Server 创建主要副本中站点数据库的完整备份。 有关详细信息，请参阅[创建完整数据库备份](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)。

3. 使用 SQL Server 将站点数据库备份还原到将托管站点数据库的服务器。 有关详细信息，请参阅[使用 SSMS 还原数据库备份](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。

    > [!Note]  
    > 如果可用性组的主要副本服务器将托管站点数据库的单个实例，则跳过此步骤。

4. 在将托管站点数据库的服务器上，将站点数据库备份模型从“完整”  更改为“简单”  。 有关详细信息，请参阅[查看或更改数据库的恢复模式](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server)。

5. 从 Configuration Manager 站点安装文件夹 `\BIN\X64\setup.exe` 运行 Configuration Manager 安装程序  。

6. 在“入门”  页上，选择“执行站点维护或重置此站点”  ，然后选择“下一步”  。  

7. 选择“修改 SQL Server 配置”  ，然后选择“下一步”  。  

8. 为站点数据库重新配置以下设置：

    - **SQL Server 名称：** 输入现在托管站点数据库的服务器的名称。

    - **实例：** 指定托管站点数据库的命名实例。 如果数据库位于默认实例上，则将此字段留空。

    - **数据库：** 保留所显示的名称。 这是当前站点数据库的名称。

9. 为新的数据库位置提供此信息后，使用常规过程和配置完成安装。 安装完成后，站点将重启并开始使用新的数据库位置。

10. 若要清理原为可用性组成员的服务器，请按照[删除可用性组](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server)中的指导进行操作。
