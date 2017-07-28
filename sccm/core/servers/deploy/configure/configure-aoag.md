---
title: "配置可用性组 | Microsoft 文档"
description: "通过 SCCM 设置和管理 SQL Server AlwaysOn 可用性组。"
ms.custom: na
ms.date: 5/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 138834b6cc64332202256961ad1d2f5ab6d176db
ms.contentlocale: zh-cn
ms.lasthandoff: 06/01/2017


---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>为 Configuration Manager 配置 SQL Server AlwaysOn 可用性组

*适用范围：System Center Configuration Manager (Current Branch)*

使用本主题提供的信息配置和管理与 Configuration Manager 配合使用的可用性组。

开始之前：  
-   熟悉[准备将 SQL Server AlwaysOn 可用性组与 Configuration Manager 配合使用](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)中的信息。
-   熟悉 SQL Server 文档，其中包括使用可用性组和完成以下方案所需的相关过程。

> [!TIP]  
>  单击本主题中的 SQL Server 链接可转到 SQL Server 2016 相关内容。 如果你未使用该版本的 SQL Server，请参阅所用版本的相关文档。

## <a name="create-and-configure-an-availability-group"></a>创建和配置可用性组
使用以下过程创建可用性组，然后将站点数据库的副本移动到该可用性组。

若要完成此过程，所用的帐户必须是：
-   每个可用性组成员计算机上的本地管理员组成员。
-   托管站点数据库的每个 SQL Server 实例上的 Sysadmin。

### <a name="to-create-and-configure-an-availability-group-for-configuration-manager"></a>为 Configuration Manager 创建和配置可用性组  
1.    使用以下命令可停止 Configuration Manager 站点：Preinst.exe /stopsite 有关使用 PreInst.exe 的详细信息，请参阅[层次结构维护工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)。

2.    将站点数据库的备份模型从“简单”更改为“完整”。
请参阅 SQL Server 文档中的[查看或更改数据库的恢复模式](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server)。 （可用性组仅支持“完整”）。

3.    使用 SQL Server 创建站点数据库的完整备份，然后执行以下操作，具体要取决于承载站点数据库的服务器是否将成为新可用性组的副本成员：
    -   将成为可用性组的成员：  
        如果将此服务器用作可用性组的初始主副本成员，则不需要将站点数据库副本还原到这个或组中的另一个服务器。 数据库在主副本上已就位，SQL Server 会在后续步骤中将数据库复制到辅助副本。  

      -     不是可用性组的成员：  
    必须将站点数据库的副本还原到将承载组的主副本的服务器。

    有关如何完成此步骤的信息，请参阅 SQL Server 文档中的[创建完整数据库备份](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)和[使用 SSMS 还原数据库备份](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。

4.    在将托管组的初始主要副本的服务器上，使用 [新建可用性组向导](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) 创建可用性组。 在向导中：
      -    在“选择数据库”页面上，为你的 Configuration Manager 站点选择数据库。  

      -    在“添加副本”页面，配置以下内容：
          -    副本：指定将托管辅助副本的服务器。

          -    侦听器：指定“侦听器 DNS 名称”作为完整 DNS 名称，如 **&lt;Listener_Server>.fabrikam.com**。 将 Configuration Manager 配置为使用可用性组中的站点数据库时，将使用此名称。

      -    在“选择初始数据同步”页面，选择“完整”。 在向导创建可用性组后，向导将备份主数据库和事务日志，然后在托管辅助副本的每个服务器上还原它们。 （如果不使用此步骤，则需要将站点数据库的副本还原到托管辅助副本的每个服务器，并将该数据库手动联接到组。）   

5.    检查每个副本上的配置：   
  1.    确保站点服务器的计算机帐户是每个可用性组成员计算机上“本地管理员”组的成员。  

  2.  从先决条件中运行[验证脚本](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites)，以确认正确配置了每个副本上的站点数据库。

  3.    如果有必要在辅助副本上设置配置，则必须将主要副本手动故障转移到辅助副本，然后再继续，因为你只能配置主副本的数据库。 有关详细信息，请参阅 SQL Server 文档中的[执行可用性组的计划手动故障转移](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server)。

6.    所有副本都满足要求后，可用性组即可与 Configuration Manager 一起使用。

## <a name="configure-a-site-to-use-the-database-in-the-availability-group"></a>将站点配置为使用可用性组中的数据库
[创建和配置可用性组](#create-and-configure-an-availability-group) 之后，使用 Configuration Manager 站点维护，将站点配置为使用由可用性组托管的数据库。

不支持使用它在可用性组中的数据库安装新站点。 例如，如果你使用基线 1702 媒体，则必须安装使用单个 SQL Server 实例的站点。 安装站点后，即可将站点数据库移到可用性组中。

若要完成此过程，用于运行 Configuration Manager 安装程序的帐户必须是：
-   每个可用性组成员计算机上的本地管理员组成员。
-   托管站点数据库的每个 SQL Server 实例上的 **Sysadmin**。

> [!IMPORTANT]
> 在混合配置中将 Microsoft Intune 与 Configuration Manager 结合使用时，从可用性组来回移动站点数据库将会触发数据与云重新同步。 此问题无法避免。

### <a name="to-configure-a-site-to-use-the-availability-group"></a>将站点配置为使用可用性组
1.    从 **&lt;*Configuration Manager 站点安装文件夹*>\BIN\X64\setup.exe** 中运行“Configuration Manager 安装程序”。

2.    在“入门”页上，选择“执行站点维护或重置此站点”，然后单击“下一步”。

3.    选择“修改 SQL Server 配置”选项，然后单击“下一步”。

4.    为站点数据库重新配置以下内容：
    -   SQL Server 名称：输入你在创建可用性组时配置的可用性组 listener 的虚拟名称。 虚拟名称应为完整的 DNS 名称，如 **&lt;*endpointServer*>.fabrikam.com**。  

    -   实例：此值必须为空，以便为可用性组的 listener 指定默认实例。 如果当前站点数据库安装在已命名实例上，则将列出且必须清除该已命名实例。

    -   **数据库：**保留所显示的名称。 这是当前站点数据库的名称。

5.    为新的数据库位置提供此信息后，使用常规过程和配置完成安装。



## <a name="add-and-remove-replica-members"></a>添加和删除副本成员  
当站点数据库在可用性组中托管时，请使用以下过程添加或删除副本成员。 Configuration Manager 支持一个主节点和最多两个辅助节点。

若要完成以下过程，你使用的帐户必须是：
-   每个可用性组成员计算机上的本地管理员组成员。
-   托管或将托管站点数据库的每个 SQL Server 上的 Sysadmin。


### <a name="to-add-a-new-replica-member"></a>添加新的副本成员
1.    将新的服务器作为辅助副本添加到可用性组。 请参阅 SQL Server 文档库中的[将辅助副本添加到可用性组 (SQL Server)](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)。

2.    通过运行 **Preinst.exe /stopsite** 停止 Configuration Manager 站点。 请参阅[层次结构维护工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)。

3.    使用 SQL Server 创建主要副本中站点数据库的备份，然后将该备份还原到新的辅助副本服务器。 请参阅 SQL Server 文档中的[创建完整数据库备份](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)和[使用 SSMS 还原数据库备份](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。

4.    配置每个辅助副本。 为可用性组中的每个辅助副本执行以下操作：

    1.    确保站点服务器的计算机帐户是每个可用性组成员计算机上“本地管理员”组的成员。

    2.    从先决条件中运行[验证脚本](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites)，以确认正确配置了每个副本上的站点数据库。

    3.    如有必要配置新副本，将主要副本手动故障转移到新的辅助副本，然后执行所需的设置。 请参阅 SQL Server 文档中的[执行可用性组的计划手动故障转移](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server)。

5.    通过启动站点组件管理器 (**sitecomp**) 和 **SMS_Executive** 服务重启站点。

### <a name="to-remove-a-replica-member"></a>删除副本成员
对于此过程，请使用 SQL Server 文档中[从可用性组删除辅助副本](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server)部分的信息。

## <a name="stop-using-an-availability-group"></a>停止使用可用性组
不再需要在可用性组中托管站点数据库时，请使用以下过程。 这涉及到将站点数据库移回 SQL Server 的单个实例。

若要完成此过程，所用的帐户必须是：
-   每个可用性组成员计算机上的本地管理员组成员
-   托管站点数据库的每个 SQL Server 实例上的 **Sysadmin**。

> [!IMPORTANT]  
> 在混合配置中将 Microsoft Intune 与 Configuration Manager 结合使用时，从可用性组来回移动站点数据库将会触发数据与云重新同步。 此问题无法避免。

### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>将站点数据库从可用性组移回单个实例 SQL Server
1.    使用以下命令可停止 Configuration Manager 站点：Preinst.exe /stopsite 有关详细信息，请参阅[层次结构维护工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)。

2.    使用 SQL Server 创建主要副本中站点数据库的完整备份。 有关如何完成此步骤的信息，请参阅 SQL Server 文档中的 [创建完整数据库备份](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) 。

3.    如果可用性组主要副本所在的服务器将托管站点数据库的单个实例，则可跳过此步骤：  

    -   使用 SQL Server 将站点数据库备份还原到将托管站点数据库的服务器。 请参阅 SQL Server 文档中的[使用 SSMS 还原数据库备份](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。   <br />  <br />

4.    在将承载站点数据库（主副本或在其中还原站点数据库的服务器）的服务器上，将站点数据库的备份模型从“完整”更改为”简单”。 请参阅 SQL Server 文档中的[查看或更改数据库的恢复模式](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server)。  

5.    从 **&lt;*Configuration Manager 站点安装文件夹*\BIN\X64\setup.exe** 运行 **Configuration Manager 安装程序**。

6.    在“入门”页上，选择“执行站点维护或重置此站点”，然后单击“下一步”。  

7.    选择“修改 SQL Server 配置”选项，然后单击“下一步”。  

8.    为站点数据库重新配置以下内容：
    -   **SQL Server 名称：**输入现在托管站点数据库的服务器的名称。

    -   **实例：**指定托管站点数据库的已命名实例（如果数据库在默认实例上则将其留空）。

    -   **数据库：**保留所显示的名称。 这是当前站点数据库的名称。    

9.    为新的数据库位置提供此信息后，使用常规过程和配置完成安装。 安装完成后，站点将重启并开始使用新的数据库位置。    

10.    若要清理原为可用性组成员的服务器，请按照 SQL Server 文档中[删除可用性组](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server)中的指导进行操作。

