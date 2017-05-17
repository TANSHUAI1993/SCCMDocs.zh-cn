---
title: SQL Server AlwaysOn | Microsoft Docs
ms.custom: na
ms.date: 1/4/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: aaaab003ddd22f18160d4be63cfeab3a7e7f6b03
ms.contentlocale: zh-cn
ms.lasthandoff: 05/17/2017


---
# <a name="sql-server-alwayson-for-a-highly-available-site-database-for-system-center-configuration-manager"></a>通过 SQL Server AlwaysOn 实现适用于 System Center Configuration Manager 的高可用性站点数据库

*适用范围：System Center Configuration Manager (Current Branch)*


 从 System Center Configuration Manager 1602 版开始，可以使用 SQL Server [AlwaysOn 可用性组](https://msdn.microsoft.com/library/hh510230\(v=sql.120\).aspx)承载主站点和管理中心站点上的站点数据库作为高可用性和灾难恢复解决方案。 可在本地或在 Microsoft Azure 中托管可用性组。  

 使用 Microsoft Azure 托管可用性组时，可将 SQL Server AlwaysOn 可用性组用于 Azure 可用性集，从而进一步提升站点数据库的可用性。 有关 Azure 可用性集的详细信息，请参阅 [管理虚拟机的可用性](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/)。  

 Configuration Manager 支持在位于内部或外部负载均衡器后面的 SQL 可用性组上承载站点数据库。 除了在每个副本上配置防火墙例外，还需要为以下端口添加负载均衡规则：
  - SQL over TCP: TCP 1433
  - SQL Server Service Broker: TCP 4022
  - 服务器消息块 (SMB): TCP 445
  - RPC 终结点映射程序: TCP 135


以下是支持可用性组的方案：  

-   可以将站点数据库移到可用性组的默认实例  

-   可以从托管站点数据库的可用性组添加或删除副本成员  

-   可以将站点数据库从可用性组移到独立 SQL Server 的默认实例或命名实例  

> [!Important]  
> 在混合配置中将 Microsoft Intune 与 Configuration Manager 结合使用时，从可用性组来回移动站点数据库将触发数据与云重新同步。 此问题无法避免。 



> [!NOTE]  
>  成功配置和使用可用性组要求你熟悉 SQL Server 和 SQL Server 可用性组的配置。 本主题中 System Center Configuration Manager 的过程依赖于 SQL Server 文档库中找到的其他文档和过程。  

 **将 Configuration Manager 与 AlwaysOn 可用性组配合使用时的已知问题：**  

-   **设置 Configuration Manager 以使用可用性组时，所有副本服务器需要相同的文件路径：**  

    -   运行 Configuration Manager 安装程序以重定向站点以使用可用性组中的数据库时，组中的每个辅助副本服务器的文件路径必须和用来承载当前主副本上站点数据库文件的文件路径相同。 如果辅助副本上不存在相同的路径，则安装程序将无法将可用性组实例添加为站点数据库的新位置。  

         此外，在每个辅助副本服务器上，本地 SQL Server 服务帐户必须具有对此文件夹的“完全控制”权限。  

         仅当使用安装程序指定可用性组中的数据库实例时，次要副本服务器才需要此文件路径。  安装程序完成在可用性组中使用站点数据库的更改后，可以从次要副本服务器删除未使用的路径。  

         例如，考虑以下情况：  

        -   创建使用三个 SQL 服务器的可用性组  

        -   主副本服务器是新安装的 SQL Server 2014。  默认情况下，数据库 .MDF 和 .LDF 文件存储在 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA  

        -   你的两个辅助副本服务器均已从以前版本升级到 SQL Server 2014，并保留用于存储数据库文件的原始文件路径：C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA  

        -   尝试将站点数据库移到该可用性组之前，即使辅助副本不使用以下文件位置，也必须在每个辅助副本服务器上创建以下文件路径：C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA（此为主副本上所使用路径的副本）  

        -   然后向每个辅助副本上的 SQL Server 服务帐户授予对该服务器上新创建文件位置的完全控制访问权限  

        -   现在，便可以成功运行 Configuration Manager 安装程序以引导站点使用可用性组中的站点数据库  

-   **运行安装程序以引导站点数据库使用可用性组时，ConfigMgrSetup.log 中可能会记录类似于以下的错误：**  

    -   错误：SQL Server 错误：[25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]未能更新数据库 "CM_AAA"，因为此数据库为只读。   Configuration Manager 安装程序 1/21/2016 4:54:59 PM  7344 (0x1CB0)  

     安装程序在尝试处理可用性组辅助副本上的数据库角色时记录了这些错误。 可以放心忽略这些错误。
- **承载其他可用性组的 SQL Server：**

  安装版本 1610 之前，当使用可用性组，然后运行 Configuration Manager 安装程序或安装 Configuration Manager 更新时，承载 Configuration Manager 可用性组的 SQL Server 上每个其他可用性组中的每个副本必须进行以下配置：
    - **手动故障转移**
    - **允许任何只读连接**


##  <a name="bkmk_BnR"></a> 当你使用 SQL Server AlwaysOn 可用性组时，备份和恢复的更改  
 **备份：**  

 当站点数据库在某一可用性组中运行时，应继续运行内置“备份站点”服务器维护任务来备份常规 Configuration Manager 设置和文件，但不要计划使用由该备份创建的 .MDF 或 .LDF 文件。 相反，计划通过使用 SQL Server 直接备份站点数据库。  

 此外，由于已将数据库的恢复模式设置为完整备份，因此必须计划监视和维护站点数据库事务日志的大小。  在完整恢复模型下，在进行数据库或事务日志的完整备份后，才对事务进行强化。 完整恢复模式是使用可用性组中站点数据库的要求，在配置与 Configuration Manager 一起使用的组时设置。 有关 SQL Server 备份和还原的详细信息，请参阅 SQL Server 文档中的 [SQL Server 数据库的备份和还原](https://msdn.microsoft.com/library/ms187048\(v=sql.120\).aspx) 。  

 **恢复：**  

 在站点恢复期间，只要可用性组的一个节点仍正常工作，就可以使用“跳过数据库恢复”站点恢复选项（当站点数据库未受影响时使用此选项）。  

 但是，如果可用性组的所有节点都已丢失，则必须重新创建可用性组，才能恢复站点（System Center Configuration Manager 不能重新生成或还原可用性节点。）使用还原且重新配置的备份重新创建组后，即可使用“跳过数据库恢复(当站点数据库未受影响时使用此选项)”站点恢复选项。  

 有关备份和恢复的详细信息，请参阅 [System Center Configuration Manager 的备份和恢复](../../../../protect/understand/backup-and-recovery.md)。  

##  <a name="bkmk_create"></a> 配置与 Configuration Manager 配合使用的可用性组  
 在开始下列过程之前，请熟悉完成此配置所需的 SQL Server 过程，以及配置与 Configuration Manager 配合使用的可用性组的以下详细信息。  

 **与 System Center Configuration Manager 配合使用的 AlwaysOn 可用性组的要求：**  

-  *版本*：可用性组中的每个节点（或副本）必须运行由 System Center Configuration Manager 支持的 SQL Server 版本。 如果 SQL Server 支持，可用性组的不同节点可以运行不同版本的 SQL Server。   

- *版本*：必须使用 SQL Server 企业版。  SQL Server 2016 标准版引入了 Basic 可用性组（Configuration Manager 不支持此组）。


-   此可用性组必须具有一个主副本，并且可以具有最多两个同步辅助副本。  

-  将数据库添加到某一可用性组后，必须将主副本故障转移到辅助副本（使其成为新的主副本），然后对数据库进行以下配置：
    - 启用 Trustworthy：等于 True
    - 启用 Service Broker：等于 True
    - 设置 dbowner：等于 SA

    可以运行以下脚本来配置这些设置，其中 cm_ABC 是站点数据库的名称：  

    >     USE master  
    >     ALTER DATABASE cm_ABC SET NEW_BROKER   
    >     ALTER DATABASE cm_ABC SET ENABLE_BROKER  
    >     ALTER DATABASE cm_ABC SET TRUSTWORTHY ON;  
    >     USE cm_ABC  
    >     EXEC sp_changedbowner 'sa'  
    >     Exec sp_configure 'max text repl size (B)', 2147483647 reconfigure



-   此可用性组必须具有至少一个“可用组侦听器”。  将 Configuration Manager 配置为使用可用性组中的站点数据库时，将使用此侦听器的虚拟名称。 尽管可用性组可以包含多个侦听器，但 Configuration Manager 只能使用其中一个  

-   每个主要和辅助副本必须满足以下条件：  
    - 设置为“允许任何只读连接”
    - 使用“默认实例”
    - 设置为“手动故障转移”  

        > [!TIP]  
        >  System Center Configuration Manager 设置为“自动故障转移”时，支持使用可用性组副本。 但是，当运行安装程序以指定使用可用性组中站点数据库，以及安装 Configuration Manager 的任何更新（不仅是适用于站点数据库的更新）时，必须设置“手动故障转移”。  

  **可用性组的限制**
   - 不支持 Basic 可用性组（随 SQL Server 2016 标准版引入）。 这是因为 Basic 可用性组不支持对次要副本的读取访问，这是与 Configuration Manager 配合使用的要求。 有关详细信息，请参阅 [Basic 可用性组（AlwaysOn 可用性组）](https://msdn.microsoft.com/en-us/library/mt614935.aspx)。

   - 可用性组仅可用于站点数据库，不支持软件更新数据库或报表数据库。   
   - 使用可用性组时，必须将报表点手动配置为使用当前主副本，而非可用性组侦听器。 如果主副本故障转移到另一个副本，则必须将报表点重新配置为使用新的主副本。  
   - 在安装更新（例如版本 1606）之前，请确保将可用性组设置为手动故障转移。 站点更新后，可以将故障转移还原为自动故障转移。



 **配置和使用可用性组所需的权限：**  

-   站点服务器的计算机帐户必须是可用性组成员计算机上“本地管理员”组的成员。  

#### <a name="to-configure-an-availability-group-to-host-a-site-database"></a>将可用性组配置为托管站点数据库  

1.  使用以下命令可停止 Configuration Manager 站点：  
     **Preinst.exe /stopsite**  

     有关使用 Preinst.exe 的详细信息，请参阅 [System Center Configuration Manager 的层次结构维护工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

2.  将站点数据库的备份模型从“简单”更改为“完整”。  

     请参阅 SQL Server 文档中的[查看或更改数据库的恢复模式](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx)。 （可用性组仅支持“完整”）。  

3.  在将托管组的主要副本的服务器上，使用“新建可用性组向导”创建可用性组。 在向导中：  

    -   在“选择数据库”页面上，为你的 Configuration Manager 站点选择数据库  

    -   在“添加副本”页面，配置以下内容：  

        -   **副本：**指定将托管次要副本的服务器  

        -   **侦听器**：指定“侦听器 DNS 名称”作为完整 DNS 名称，如 **&lt;Listener_Server>.fabrikam.com**。 将 Configuration Manager 配置为使用可用性组中的站点数据库时，将使用此名称。

    -   在“选择初始数据同步”页面，选择“完整”。 该向导创建可用性组后，向导将备份主数据库和事务日志，并在托管辅助副本的每个服务器上还原它们。 如果不使用此步骤，则需要将站点数据库的副本还原到托管辅助副本的每个服务器，并将该数据库手动联接到组。  

    有关详细信息，请参阅 SQL Server 文档中的[使用可用性组向导](https://msdn.microsoft.com/library/hh403415\(v=sql.120\).aspx)。  

4.  配置可用性组后，为主要副本上的站点数据库配置“TRUSTWORTHY”属性，然后“启用 CLR 集成”。 有关如何配置这些项目的信息，请参阅 SQL Server 文档中的 [TRUSTWORTHY 数据库属性](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx)和[启用 CLR 集成](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)。  

5.  执行以下操作以配置可用性组中的每个辅助副本：  

    1.  将当前主要副本手动故障转移到辅助副本。 请参阅 SQL Server 文档中的 [执行可用性组的计划手动故障转移](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) 。  

    2.  为新增主要副本上的数据库配置 **TRUSTWORTHY** 属性，然后 **启用 CLR 集成**。  

6.  将所有副本提升为主要副本并配置数据库后，即可将该可用性组与 Configuration Manager 配合使用。  





##  <a name="bkmk_direct"></a> 将站点数据库移至可用性组中  
 可以将以前安装的站点的站点数据库移到可用性组。 必须首先创建可用性组，然后在可用性组中配置用于操作的数据库。  

 若要完成此过程，运行 Configuration Manager 安装程序的用户帐户必须是可用性组成员计算机上“本地管理员”组的成员。  

#### <a name="to-move-a-site-database-to-an-availability-group"></a>将站点数据库移至可用性组中  

1.  从 **&lt;Configuration Manager 站点安装文件夹 \>\BIN\X64\setup.exe** 运行 **Configuration Manager 安装程序**。  

2.  在“入门”  页上，选择“执行站点维护或重置此站点” ，然后单击“下一步” 。  

3.  选择“修改 SQL Server 配置”选项，然后单击“下一步”。  

4.  为站点数据库重新配置以下内容：  

    -   **SQL Server 名称** ：输入在创建可用性组时配置的可用性组侦听器的虚拟名称。 虚拟名称应为完整的 DNS 名称，如 **&lt;endpointServer\>.fabrikam.com**  

    -   **实例：** 此值必须为空，以便为可用性组的可用性组侦听器指定默认实例。  如果当前站点数据库安装在已命名实例上，则将列出且必须清除该已命名实例  

    -   **数据库：** 保留所显示的名称。 这是当前站点数据库的名称。  

5.  为新的数据库位置提供此信息后，使用常规过程和配置完成安装。  

##  <a name="bkmk_change"></a> 添加或删除活动可用性组的成员  
 Configuration Manager 使用可用性组中托管的站点数据库后，可删除副本成员或添加其他副本成员（不超过一个主节点和两个辅助节点）。  

#### <a name="to-add-a-new-replica-member"></a>添加新的副本成员  

1.  将新的服务器作为辅助副本添加到可用性组。 请参阅 SQL Server 文档库中的  [将次要副本添加到可用性组 (SQL Server)](https://msdn.microsoft.com/library/hh213247\(v=sql.120\).aspx)。  

2.  通过运行 **Preinst.exe /stopsite** 停止 Configuration Manager 站点，请参阅 [System Center Configuration Manager 的层次结构维护工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

3.  配置每个辅助副本。 为可用性组中的每个辅助副本执行以下操作：  

    1.  将主要副本手动故障转移到新的辅助副本。 请参阅 SQL Server 文档中的 [执行可用性组的计划手动故障转移](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) 。  

    2.  将新服务器上数据库配置为“Trustworthy”，并启用 CLR 集成。 请参阅 SQL Server 文档中的 [TRUSTWORTHY 数据库属性](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) 和  [启用 CLR 集成](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)。  

4.  通过启动站点组件管理器 (**sitecomp**) 和 **SMS_Executive** 服务重启站点。  

#### <a name="to-remove-a-replica-member-from-the-availability-group"></a>从可用性组删除副本成员  

-   请使用 SQL Server 文档中 [从可用性组删除辅助副本](https://msdn.microsoft.com/library/hh213149\(v=sql.120\).aspx) 中的信息。  

##  <a name="bkmk_remove"></a> 将站点数据库从可用性组移回单个实例 SQL Server  
 不再需要在可用性组中托管站点数据库时，请使用以下过程。  

#### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>将站点数据库从可用性组移回单个实例 SQL Server  

1.  使用以下命令停止 Configuration Manager 站点：  
     **Preinst.exe /stopsite**  有关详细信息，请参阅 [System Center Configuration Manager 的层次结构维护工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

2.  使用 SQL Server 创建主要副本中站点数据库的完整备份。 有关如何完成此步骤的信息，请参阅 SQL Server 文档中的 [创建完整数据库备份](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) 。  

3.  如果托管可用性组主要副本的服务器现将托管站点数据库的单个实例，可跳过此步骤：  

    -   使用 SQL Server 将站点数据库备份还原到将托管站点数据库的服务器。  请参阅 SQL Server 文档库中的[还原数据库备份 (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx)。  

4.  在已还原的站点数据库中，将站点数据库备份模型从“完整”更改为“简单”。  请参阅 SQL Server 文档中的 [查看或更改数据库的恢复模式](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) 。  

5.  从 **&lt;Configuration Manager 站点安装文件夹 \>\BIN\X64\setup.exe** 运行 **Configuration Manager 安装程序**。  

6.  在“入门”  页上，选择“执行站点维护或重置此站点” ，然后单击“下一步” 。  

7.  选择“修改 SQL Server 配置”选项，然后单击“下一步”。  

8.  为站点数据库重新配置以下内容：  

    -   **SQL Server 名称：** 输入现在托管站点数据库的服务器的名称。  

    -   **实例：** 指定托管站点数据库的已命名实例（如果数据库在默认实例上则将其留空）。  

    -   **数据库：** 保留所显示的名称。 这是当前站点数据库的名称。  

9. 为新的数据库位置提供此信息后，使用常规过程和配置完成安装。 安装完成后，站点将重启并开始使用新的数据库位置。  

10. 若要清理原为可用性组成员的服务器，请按照 SQL Server 文档中 [删除可用性组](https://msdn.microsoft.com/library/ff878113\(v=sql.120\).aspx) 中的指导进行操作。

