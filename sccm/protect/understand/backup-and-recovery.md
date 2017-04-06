---
title: "备份和恢复 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中出现故障或数据丢失时如何备份和恢复站点。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: ea6668ee7ee6b209b659426a0dc2c0be605ceaf1
ms.lasthandoff: 03/27/2017

---

# <a name="backup-and-recovery"></a>备份和恢复

*适用范围：System Center Configuration Manager (Current Branch)*

准备备份和恢复方法，以避免数据丢失。 对于 Configuration Manager 站点，备份和恢复方法可有助于更快地恢复站点和层次结构，并保持最小程度的数据丢失。 本主题中的内容可以帮助备份站点，并在出现故障或数据丢失时恢复站点。  



- [备份 Configuration Manager 站点](#BKMK_SiteBackup)   

  - [备份维护任务](#BKMK_BackupMaintenanceTask)   

  - [使用 Data Protection Manager 来备份站点数据库](#BKMK_DPMBackup)   

  -  [将备份快照存档](#BKMK_ArchivingBackupSnapshot)   

  -  [使用 AfterBackup.bat 文件](#BKMK_UsingAfterBackup)   

  -  [补充备份任务](#BKMK_SupplementalBackup)   

-  [恢复 Configuration Manager 站点](#BKMK_RecoverSite)   

  -   [确定恢复选项](#BKMK_DetermineRecoveryOptions)   

         -   [站点服务器恢复选项](#BKMK_SiteServerRecoveryOptions)   

         -   [站点数据库恢复选项](#BKMK_SiteDatabaseRecoveryOption)   

         -   [SQL Server 更改跟踪保持期](#bkmk_SQLretention)   

         -   [继续重新初始化站点或全局数据](#bkmk_reinit)   

         -   [站点数据库恢复方案](#BKMK_SiteDBRecoveryScenarios)  

  -   [无人参与的站点恢复脚本文件密钥](#BKMK_UnattendedSiteRecoveryKeys)  

  -   [恢复后任务](#BKMK_PostRecovery)  

  -   [恢复辅助站点](#BKMK_RecoverSecondarySite)  

-   [SMS 编写器服务](#BKMK_SMSWriterService)  

> [!NOTE]  
>  如果使用 SQL Server AlwaysOn 可用性组托管站点数据库，请根据 [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)（通过 SQL Server AlwaysOn 实现适用于 System Center Configuration Manager 的高可用性站点数据库）主题中的[使用 SQL Server AlwaysOn 可用性组时备份和恢复的更改](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#bkmk_BnR)部分所述的内容修改备份和恢复计划。  

##  <a name="BKMK_SiteBackup"></a> 备份 Configuration Manager 站点  
 Configuration Manager 包含一个执行以下操作的备份维护任务：  

-   按计划运行  

-   备份站点数据库  

-   备份特定注册表项  

-   备份特定文件夹和文件  

-   备份 **CD.Latest** 文件夹（请参阅 [System Center Configuration Manager 的 CD.Latest 文件夹](../../core/servers/manage/the-cd.latest-folder.md)）  

 计划至少每 5 天运行一次默认站点备份任务。 这是因为 Configuration Manager 使用为期 5 天的 [SQL Server 更改跟踪保持期](#bkmk_SQLretention)。  

 若要简化备份过程，可以创建 **AfterBackup.bat** 文件以在备份维护任务成功运行后自动执行备份后操作。 AfterBackup.bat 文件通常用于将备份快照存档到安全位置。 也可以使用 AfterBackup.bat 文件将文件复制到备份文件夹并启动其他补充备份任务。

使用下列部分来帮助创建 Configuration Manager 备份策略。  

> [!NOTE]  
>  Configuration Manager 可以从 Configuration Manager 备份维护任务或从使用另一个进程创建的站点数据库备份来恢复站点数据库。 例如，可以通过作为 Microsoft SQL Server 维护计划一部分创建的备份来还原站点数据库。 可以从使用 System Center 2012 Data Protection Manager (DPM) 创建的备份还原站点数据库。 有关详细信息，请参阅 [使用 Data Protection Manager 备份站点数据库](#BKMK_DPMBackup)。  

###  <a name="BKMK_BackupMaintenanceTask"></a> 备份维护任务  
 可以通过计划预定义的备份站点服务器维护任务来自动完成 Configuration Manager 站点的备份。 你可以备份管理中心站点和主站点，但不支持备份辅助站点或站点系统服务器。 当 Configuration Manager 备份服务运行时，它将按照备份控制文件 (**&lt;ConfigMgrInstallationFolder\>\Inboxes\Smsbkup.box\Smsbkup.ctl**) 中定义的指令进行操作。 你可以修改备份控制文件来更改备份服务的行为。 站点备份状态信息将写入 **Smsbkup.log** 文件。 将在备份站点服务器维护任务属性内指定的目标文件夹中创建此文件。  


##### <a name="to-enable-the-site-backup-maintenance-task"></a>启用站点备份维护任务  

1.  在 Configuration Manager 控制台中，依次打开“管理” > “站点配置”  

     \>“站点”。  

2.  选择要在其中启用站点备份维护任务的站点。  

3.  在“主页”选项卡上的“设置”组中，选择“站点维护任务”。  

4.  选择“备份站点服务器”  >  “编辑”。  

5.  选择“启用此任务” > “设置路径”以指定备份目标。 有下列选项：  

    > [!IMPORTANT]  
    >  为了帮助防止篡改备份文件，请将文件存储在安全的位置。 最安全的备份路径是本地驱动器，因此你可以在文件夹上设置 NTFS 文件系统权限。 Configuration Manager 不会对备份路径中存储的备份数据进行加密。  

    -   **站点服务器上用于站点数据和数据库的本地驱动器**：指定将站点和站点数据库的备份文件存储在站点服务器本地磁盘驱动器上的指定路径中。 你必须在备份任务运行之前创建本地文件夹。 站点服务器上的本地系统帐户必须具有站点服务器备份的本地文件夹的 **“写入”** NTFS 文件系统权限。 运行 SQL Server 的计算机上的本地系统帐户必须具有站点数据库备份文件夹的 **“写入”** NTFS 权限。  

    -   “站点数据和数据库的网络路径（UNC 名称）”；指定将站点和站点数据库的备份文件存储在指定 UNC 路径中。 你必须在备份任务运行之前创建共享。 站点服务器的计算机帐户以及 SQL Server 的计算机帐户（如果 SQL Server 安装在另一台计算机上）必须具有共享网络文件夹的 **“写入”** NTFS 和共享权限。  

    -   **站点服务器和 SQL Server 上的本地驱动器**：指定将站点的备份文件存储在站点服务器本地驱动器上的指定路径中，并将站点数据库的备份文件存储在站点数据库服务器本地驱动器上的指定路径中。 你必须在备份任务运行之前创建本地文件夹。 站点服务器的计算机帐户必须具有你在站点服务器上创建的文件夹的 **“写入”** NTFS 权限。 SQL Server 的计算机帐户必须具有你在站点数据库服务器上创建的文件夹的 **“写入”** NTFS 权限。 只有在站点服务器未安装站点数据库时，此选项才可用。  

    > [!NOTE]  
    >    - 只有在你指定备份目标的 UNC 路径时，用于浏览到备份目标的选项才可用。

    > - 用于备份目标的文件夹名称或共享名称不支持使用 Unicode 字符。  


6.  为站点备份任务配置计划。 作为最佳方案，请考虑活动工作时间外的备份计划。 如果有层次结构，请考虑使用一周至少运行两次的计划，以确保在出现站点故障时保留最大量的数据。  

    如果在为备份配置的同一站点服务器上运行 Configuration Manager 控制台，则备份站点服务器维护任务将为计划使用本地时间。 如果 Configuration Manager 控制台从为备份配置的站点的远程计算机中运行，则备份站点服务器维护任务为计划使用 UTC。  

7.  选择在站点备份任务失败时是否创建警报，单击“确定”，然后单击“确定”。 如果选择，则 Configuration Manager 将为备份失败创建关键警报，可以在“监视”工作区的“警报”节点中查看该警报。  

 接下来，验证备份站点服务器维护任务是否正在运行，以确保正在创建备份。  

##### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>验证备份站点服务器维护任务是否正在运行  

-   通过查看下列任何信息来验证站点备份维护任务是否正在运行：  

    -   检查该任务创建的备份目标文件夹中的文件上的时间戳。 验证是否已使用与上次计划运行该任务的时间匹配的时间更新了该时间戳。  

    -   在“监视”  工作区的“组件状态”  节点中，查看 SMS_SITE_BACKUP 的状态消息。 如果站点备份成功完成，你将看到消息 ID 5035，指示站点备份已成功完成，且未出现任何错误。  

    -   如果将备份站点服务器维护任务配置为在备份失败的情况下创建警报，你可以检查“监视”  工作区中的“警报”  节点来了解备份失败情况。  

    -   在 &lt;*ConfigMgrInstallationFolder*>\Logs 中，查看 Smsbkup.log 以了解警告和错误。 站点备份成功完成后，你将看到 `Backup completed` ，时间戳和消息 ID 为 `STATMSG: ID=5035`。  

    > [!TIP]  
    >  如果备份维护任务失败，你可以通过停止并重启 SMS_SITE_BACKUP 服务来重启备份任务。  

###  <a name="BKMK_DPMBackup"></a> 使用 Data Protection Manager 来备份站点数据库  
 你可以使用 System Center 2012 Data Protection Manager (DPM) 来备份站点数据库。 你可以在 DPM 中为站点数据库计算机创建一个新保护组。 在创建新保护组向导的“选择组成员”  页上，从数据源列表中选择 SMS 编写器服务，然后选择站点数据库作为适当的成员。 有关使用 DPM 来备份站点数据库的详细信息，请参阅 TechNet 上的 [Data Protection Manager Documentation Library（Data Protection Manager 文档库）](http://go.microsoft.com/fwlink/?LinkId=272772) 。  

> [!IMPORTANT]  
>  Configuration Manager 不支持对使用命名实例的 SQL Server 群集进行 DPM 备份，但支持对使用默认 SQL Server 实例的 SQL Server 群集进行 DPM 备份。  

 还原站点数据库之后，请按照安装程序中的步骤进行操作以恢复站点。 选择“使用已手动恢复的站点数据库”恢复选项以使用通过 Data Protection Manager 恢复的站点数据库。  

###  <a name="BKMK_ArchivingBackupSnapshot"></a> 将备份快照存档  
 备份站点服务器维护任务第一次运行时将创建一个备份快照，你可以使用该快照在出现故障时恢复站点服务器。 当备份任务在后续周期中再次运行时，它将创建新备份快照，该快照将覆盖以前的快照。 因此，站点只有一个备份快照，并且你无法检索以前的备份快照。  

 作为最佳方案，请保留备份快照的多个存档，原因如下：  

-   备份媒体经常会出现故障、位置不正确或仅包含部分备份。 从较旧的备份恢复出现故障的独立主站点比在没有任何备份的情况下进行恢复要好。 对于层次结构中的站点服务器，备份必须位于 SQL Server 更改跟踪保持期内，或者不需要备份。  

-   对于若干备份周期，可能检测不到站点中的损坏。 可能必须使用获取自站点损坏之前的备份快照。 这适用于独立主站点以及层次结构中备份处于 SQL Server 更改跟踪保持期内的站点。  

-   举例来说，如果备份站点服务器维护任务失败，站点将可能根本没有任何备份快照。 由于备份任务会在其开始备份当前数据之前删除以前的备份快照，因此将不具备有效的备份快照。  

###  <a name="BKMK_UsingAfterBackup"></a> 使用 AfterBackup.bat 文件  
 成功备份站点之后，备份站点服务器任务会自动尝试运行一个名为 AfterBackup.bat 的文件。 必须在 &lt;*ConfigMgrInstallationFolder*>\Inboxes\Smsbkup 中手动创建 AfterBackup.bat 文件。 如果 AfterBackup.bat 文件存在并存储在正确的文件夹中，则该文件将在备份任务完成后自动运行。 AfterBackup.bat 文件使你能够在每个备份操作结束时将备份快照存档，并自动执行不属于备份站点服务器维护任务一部分的其他备份后任务。 AfterBackup.bat 文件将存档和备份操作结合，从而确保将每个新备份快照存档。 如果 AfterBackup.bat 文件不存在，备份任务将跳过该文件，不会对备份操作产生影响。 要验证站点备份任务是否成功运行了 AfterBackup.bat 文件，请查看“监视”  工作区的“组件状态”  节点，并查看 SMS_SITE_BACKUP 的状态消息。 如果任务成功启动了 AfterBackup.bat 命令文件，你将看到消息 ID 5040。  

> [!TIP]  
>  要创建 AfterBackup.bat 文件以将站点服务器备份文件存档，必须在该批处理文件中使用复制命令工具，例如 Robocopy。 例如，你可以创建 AfterBackup.bat 文件，并在第一行上添加下列类似内容： `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`。 有关 Robocopy 的详细信息，请参阅 [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408) 命令行参考网页。  

 尽管 AfterBackup.bat 的预期用途是将备份快照存档，但你可以创建 AfterBackup.bat 文件以在每个备份操作结束时执行其他任务。  

###  <a name="BKMK_SupplementalBackup"></a> 补充备份任务  
 备份站点服务器维护任务提供站点服务器文件和站点数据库的备份快照，但会存在一些你在创建备份策略时必须考虑的其他未备份项目。 使用下列部分来帮助完成 Configuration Manager 备份策略。  

#### <a name="back-up-custom-reporting-services-reports"></a>备份自定义 Reporting Services 报表  
 如果修改了预定义或已创建自定义 Reporting Services 报表，则为报表服务器数据库文件创建备份是备份策略的一个重要部分。 报表服务器备份必须包括报表和模型的源文件、加密密钥、自定义程序集或扩展、配置文件、自定义报表中使用的自定义 SQL Server 视图、自定义存储过程等的备份。  

> [!IMPORTANT]  
>  将 Configuration Manager 升级到较新版本时，预定义的报表可能被新报表覆盖。 如果修改预定义报表，请备份该报表，然后在 Reporting Services 中将其还原。  

 有关在 Reporting Services 中备份自定义报表的详细信息，请参阅 SQL Server 2014 联机丛书中的 [Reporting Services 安装的备份和还原操作](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) 。  

#### <a name="backup-content-files"></a>备份内容文件  
 Configuration Manager 中的内容库是存储软件更新、应用程序、操作系统部署等的所有内容文件的位置。 内容库位于站点服务器和每个分发点上。 “备份站点服务器”维护任务不包含内容库或包源文件的备份。 在站点服务器失败时，有关内容库文件的信息会被还原到站点数据库，但你必须还原站点服务器上的内容库和包源文件。  

-   “内容库”：必须还原内容库，然后才能将内容重新分发到分发点。 当开始执行内容重分发时，Configuration Manager 会将文件从站点服务器上的内容库复制到分发点。 站点服务器的内容库位于 SCCMContentLib 文件夹中，该文件夹通常位于安装站点时可用磁盘空间最多的驱动器上。  

-   “包源文件”：必须还原包源文件，然后才能更新分发点上的内容。 当开始进行内容更新时，Configuration Manager 会将新文件或修改的文件从包源复制到内容库，后者依次将这些文件复制到关联的分发点。 你可以在 SQL Server 中运行以下查询来查找所有包和应用程序的包源位置： `SELECT * FROM v_Package`。 你可以通过查看包 ID 的前三个字符来确定包源站点。 例如，如果包 ID 为 CEN00001，则源站点的站点代码为 CEN。 在还原包源文件时，必须将它们还原到发生故障之前所在的同一位置。  

 验证是否在站点服务器的文件系统备份中包括了内容库和包源位置。  

#### <a name="back-up-custom-software-updates"></a>备份自定义软件更新  
 System Center Updates Publisher 2011 是一种独立工具，通过该工具可将自定义软件更新发布到 Windows Server Update Services (WSUS)、将软件更新同步到 Configuration Manager、评估软件更新符合性，并将自定义软件更新部署到客户端。 Updates Publisher 为其软件更新存储库使用本地数据库。 使用 Updates Publisher 管理自定义软件更新时，请确定是否必须在备份计划中包括 Updates Publisher 数据库。 有关 Updates Publisher 的详细信息，请参阅 System Center TechCenter 库中的 [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) 。  

 使用下列过程来备份 Updates Publisher 数据库。  

###### <a name="to-back-up-the-updates-publisher-2011-database"></a>备份 Updates Publisher 2011 数据库  

1.  在运行 Updates Publisher 的计算机上，浏览到 %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\ 中的 Updates Publisher 数据库文件 (Scupdb.sdf)。 每个运行 Updates Publisher 的用户有不同的数据库文件。  

2.  将数据库文件复制到备份目标。 例如，如果备份目标为 E:\ConfigMgr_Backup，则可将 Updates Publisher 数据库文件复制到 E:\ConfigMgr_Backup\SCUP2011。  

    > [!TIP]  
    >  如果计算机上有多个数据库文件，请考虑将文件存储在子文件夹中，该子文件夹指示与数据库文件关联的用户配置文件。 例如，你可能在 E:\ConfigMgr_Backup\SCUP2011\User1 中有一个数据库文件，并在 E:\ConfigMgr_Backup\SCUP2011\User2 中有另一个数据库文件。  

### <a name="user-state-migration-data"></a>用户状态迁移数据  
 在希望保留当前操作系统的用户状态的操作系统部署方案中，可以使用 Configuration Manager 任务序列来捕获和还原用户状态数据。 状态迁移点的属性中列出了存储用户状态数据的文件夹。 在站点服务器备份维护任务中，不会备份此用户状态迁移数据。 作为备份计划的一部分，你必须手动备份指定用于存储用户状态迁移数据的文件夹。   

#### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>确定用于存储用户状态迁移数据的文件夹  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”工作区中，展开“站点配置”，并选择“服务器和站点系统角色”。  

3.  选择承载状态迁移角色的站点系统，然后在“站点系统角色”中选择“状态迁移点”。  


4.  在“站点角色”  选项卡上的“属性”  组中，单击“属性” 。  
5.  “常规”  选项卡上的“文件夹详细信息”  部分中列出了存储用户状态迁移数据的文件夹。  

## <a name="recover-a-configuration-manager-site"></a>恢复 Configuration Manager 站点
 每当 Configuration Manager 站点出现故障或者站点数据库中发生数据丢失时，都需要 Configuration Manager 站点恢复。 修复和重新同步数据是站点恢复的核心任务，并且是防止操作中断所必需的。  

> [!IMPORTANT]  
>  当恢复站点的数据库时：  

>  -   必须使用相同版本的 SQL Server。 例如，不支持还原在 SQL Server 2012 到 SQL Server 2014 上运行的数据库。 同样，也不支持还原在 SQL Server 2014 标准版和 SQL Server 2014 企业版上运行的站点数据库。  
> -   不能将 SQL Server 设置为 **单用户模式**。  
> -   确保 .MDF 和 .LDF 文件有效。 恢复站点时，不对正在还原的文件的状态进行检查。  


 通过从 CD.Latest 文件夹运行 Configuration Manager 安装向导可启动站点恢复。  还可以配置无人参与的安装脚本，然后使用安装程序命令 **/script** 选项从同一 CD.Latest 文件夹运行安装程序。 恢复选项因是否具有 Configuration Manager 站点数据库的备份而异。 有关详细信息，请参阅 [System Center Configuration Manager 的 CD.Latest 文件夹](../../core/servers/manage/the-cd.latest-folder.md)。  

> [!IMPORTANT]  
>  如果从站点服务器上的“开始”菜单中运行 Configuration Manager 安装程序，则“恢复站点”选项不可用。  

>  如果在进行备份之前，从 Configuration Manager 控制台内安装任何更新，则无法通过从安装媒体或从 Configuration Manager 安装路径中使用安装程序来成功重装该站点。  

> [!NOTE]  
>  还原为数据库副本配置的站点数据库之后，你必须重新配置每个数据库副本（从而重新创建发布和订阅），然后才能使用数据库副本。  

###  <a name="BKMK_DetermineRecoveryOptions"></a> 确定恢复选项  
 必须为 Configuration Manager 主站点服务器和管理中心站点恢复考虑两个主要方面；即站点服务器和站点数据库。 使用下列部分来帮助你确定必须为恢复方案选择的选项。  

> [!NOTE]  

####  <a name="BKMK_SiteServerRecoveryOptions"></a> 站点服务器恢复选项  
 必须从 Configuration Manager 安装文件夹之外创建的 CD.Latest 文件夹副本中启动安装程序。 然后选择“恢复站点”  选项。 在运行安装程序时，你可以为出现故障的站点服务器使用下列恢复选项：  

-   “使用现有备份恢复站点服务器”：如果具有在站点出现故障之前作为“备份站点服务器”维护任务的一部分在站点服务器上创建的 Configuration Manager 站点服务器的备份，请使用此选项。 将重新安装站点，并基于备份的站点配置站点设置。  

-   “重新安装站点服务器”：在没有站点服务器的备份时使用此选项。 将重新安装站点服务器，并且你必须指定站点设置，就像在初始安装过程中指定这些设置一样。 你必须使用在第一次安装出现故障的站点时所使用的相同站点代码和站点数据库名称才能成功恢复站点。  

> [!NOTE]  
>  如果安装程序检测到服务器上的现有 Configuration Manager 站点，可以启动站点恢复，但适用于站点服务器的恢复选项有限。 例如，如果在现有站点服务器上运行安装程序，则在选择恢复时，你可以恢复站点数据库服务器，但用于恢复站点服务器的选项则处于禁用状态。  

####  <a name="BKMK_SiteDatabaseRecoveryOption"></a> 站点数据库恢复选项  
 在运行安装程序时，你可以为站点数据库使用下列恢复选项：  

-   “使用备份集恢复站点数据库”：如果具有在站点数据库出现故障之前，作为站点上所运行“备份站点服务器”维护任务的一部分创建的 Configuration Manager 站点数据库的备份，请使用此选项。 如果你具有层次结构，则会从主站点的管理中心站点或管理中心站点的引用主站点中检索在上次站点数据库备份之后对站点数据库所做的更改。 当你恢复独立主站点的站点数据库时，将会丢失上次备份之后所做的站点更改。  

     如果为层次结构中的站点恢复站点数据库，则管理中心站点与主站点的恢复行为不同，并且当上次备份在 SQL Server 更改跟踪保持期之内或之外时，恢复行为也不同。 有关详细信息，请参阅本主题中的 [站点数据库恢复方案](#BKMK_SiteDBRecoveryScenarios) 部分。  

    > [!NOTE]  
    >  如果选择使用备份集还原站点数据库，但站点数据库已经存在，则恢复将失败。  

-   “为此站点创建新数据库”：在没有 Configuration Manager 站点数据库的备份时使用此选项。 如果你具有层次结构，系统会创建一个新站点数据库，并使用主站点的管理中心站点或管理中心站点的引用主站点中的复制数据恢复数据。 当你恢复独立主站点或没有主站点的管理中心站点时，此选项不可用。  

-   “使用已手动恢复的站点数据库”：当已经恢复 Configuration Manager 站点数据库但必须完成恢复过程时，使用此选项。 Configuration Manager 可以从 Configuration Manager 备份维护任务或从使用 DPM 或另一个进程执行的站点数据库备份中恢复站点数据库。 在 Configuration Manager 之外使用某种方法还原站点数据库之后，必须运行安装程序并选择此选项以完成站点数据库恢复。 如果你具有层次结构，则会从主站点的管理中心站点或管理中心站点的引用主站点中检索在上次站点数据库备份之后对站点数据库所做的更改。 当你恢复独立主站点的站点数据库时，将会丢失上次备份之后所做的站点更改。  

    > [!NOTE]  
    >  如果使用 DPM 备份站点数据库，请使用 DPM 过程将站点数据库还原到指定位置，然后继续在 Configuration Manager 中进行还原过程。 有关 DPM 的详细信息，请参阅 TechNet 上的 [Data Protection Manager Documentation Library（Data Protection Manager 文档库）](http://go.microsoft.com/fwlink/?LinkId=272772) 。  

-   “跳过数据库恢复”：当 Configuration Manager 站点数据库服务器上未发生数据丢失时使用此选项。 仅当站点数据库所在的计算机不同于你正在恢复的站点服务器时，此选项才有效。  

####  <a name="bkmk_SQLretention"></a> SQL Server 更改跟踪保持期  
 系统为 SQL Server 中的站点数据库启用了更改跟踪。 利用更改跟踪，Configuration Manager 可以查询有关在上一个时刻之后对数据库表所做的更改的信息。 保持期指定更改跟踪信息将保留多长时间。 默认情况下，站点数据库被配置为具有 5 天保持期。 恢复站点数据库时，恢复过程在备份处于保持期内或保持期外这两种情况下会以不同方式继续进行。 例如，你的站点数据库服务器出现故障，并且上次备份是在 7 天之前，则它在保持期之外。

 有关 SQL Server 更改跟踪内部机制的详细信息，请参阅以下 SQL Server 团队博客：[Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1)（更改跟踪清除 - 第 1 部分）和 [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2)（更改跟踪清除 - 第 2 部分）。



####  <a name="bkmk_reinit"></a> 继续重新初始化站点或全局数据  
 重新初始化站点或全局数据的过程将站点数据库中的现有数据替换为另一个站点数据库中的数据。 例如，当站点 ABC 重新初始化站点 XYZ 中的数据时，会进行以下步骤：  

-   将数据从站点 XYZ 复制到站点 ABC。  

-   从站点 ABC 上的站点数据库中删除站点 XYZ 的现有数据。  

-   将站点 XYZ 中的已复制数据插入到站点 ABC 的站点数据库中。  

##### <a name="example-scenario-1"></a>示例方案 1  
 **主站点重新初始化管理中心站点中的全局数据**：恢复过程删除主站点数据库中主站点的现有全局数据，并将数据替换为从管理中心站点中复制的全局数据。  

##### <a name="example-scenario-2"></a>示例方案 2  
 **管理中心站点重新初始化主站点中的站点数据**：恢复过程删除管理中心站点数据库中该主站点的现有站点数据，并将数据替换为从主站点中复制的站点数据。 其他主站点的站点数据不受影响。  

####  <a name="BKMK_SiteDBRecoveryScenarios"></a> 站点数据库恢复方案  
 从备份中还原站点数据库之后，Configuration Manager 会尝试还原上次数据库备份之后在站点和全局数据中所做的更改。 下面描述了从备份中还原站点数据库之后 Configuration Manager 启动的操作。  

 **恢复的站点是管理中心站点：**  

-   **更改跟踪保持期内的数据库备份**  

    -   **全局数据：** 从所有主站点中复制备份之后，全局数据中所做的更改。  

    -   **站点数据：** 从所有主站点中复制备份之后，站点数据中所做的更改。  

-   **更改跟踪保持期之前的数据库备份**  

    -   **全局数据：** 如果指定引用主站点，则管理中心站点会重新初始化引用主站点中的全局数据。 然后，所有其他主站点会重新初始化管理中心站点中的全局数据。 如果未指定引用站点，则所有主站点会重新初始化管理中心站点中的全局数据（从备份中还原的数据）。  

    -   **站点数据：** 管理中心站点重新初始化每个主站点中的站点数据。  

 **恢复的站点是主站点：**  

-   **更改跟踪保持期内的数据库备份**  

    -   **全局数据：** 从管理中心站点中复制备份之后，全局数据中所做的更改。  

    -   **站点数据：** 管理中心站点重新初始化主站点中的站点数据。 备份之后的更改将会丢失，但将信息发送到主站点的客户端会重新生成大部分数据。  

-   **更改跟踪保持期之前的数据库备份**  

    -   **全局数据：** 主站点重新初始化管理中心站点中的全局数据。  

    -   **站点数据：** 管理中心站点重新初始化主站点中的站点数据。 备份之后的更改将会丢失，但将信息发送到主站点的客户端会重新生成大部分数据。  

### <a name="site-recovery-procedures"></a>站点恢复过程  
 使用以下过程之一来帮助恢复站点服务器和站点数据库。  

##### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>在安装向导中启动站点恢复  

1.  将 CD.Latest 文件夹复制到 Configuration Manager 安装文件夹之外的位置。 （请参阅 [System Center Configuration Manager 的 CD.Latest 文件夹](../../core/servers/manage/the-cd.latest-folder.md)）  

     从 CD.Latest 文件夹的副本中，运行 Configuration Manager 安装向导。  

2.  在“入门”  页上，选择“恢复站点” ，然后单击“下一步” 。  

3.  使用适合你的站点恢复的选项完成向导。  

    > [!IMPORTANT]  
    >  在恢复过程中，安装程序会标识 SQL Server 所使用的 SQL Server Service Broker (SSB) 端口。 请勿在恢复过程中更改此端口设置，否则在恢复完成之后数据复制将不会正常工作。  

    > [!NOTE]  
    >  可以在安装向导中指定要用于 Configuration Manager 安装的原始路径或新路径。  

##### <a name="to-start-an-unattended-site-recovery"></a>启动无人参与的站点恢复  

1.  针对站点恢复所需要的选项准备无人参与安装脚本。  

2.  使用命令 **/script** 选项运行 Configuration Manager 安装程序。 例如，你将安装程序初始化文件命名为 ConfigMgrUnattend.ini 并且将其保存在运行安装程序的计算机上的 C:\Temp 目录中，那么命令将如下所示： **Setup /script C:\temp\ConfigMgrUnattend.ini**。  

> [!NOTE]  
>  恢复管理中心站点后，可能无法建立某些来自子站点的站点数据的副本。 这可能包括硬件清单、软件清单和状态消息。  
>   
>  如果发生这种情况，必须重新初始化 **ConfigMgrDRSSiteQueue** 才能进行数据库复制。  为此，请在管理中心站点上的 Configuration Manager 站点数据库上使用 **SQL Server Manager** 运行以下查询：  
>   
>  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**  
>   
>  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**  

###  <a name="BKMK_UnattendedSiteRecoveryKeys"></a> 无人参与的站点恢复脚本文件密钥  
 要对 Configuration Manager 管理中心站点或主站点执行无人参与恢复，可以创建一个无人参与安装脚本并将安装程序与 /script 命令选项一起使用。 此脚本提供的信息的类型与安装向导提示输入的信息的类型相同，不同的是没有默认设置。 必须为适用于你要使用的恢复类型的安装密钥指定所有值。  

 通过将初始化文件与 /script 安装程序命令行选项配合使用，可以以无人参与方式运行 Configuration Manager 安装程序。 Configuration Manager 管理中心站点与主站点恢复支持无人参与安装。 要使用 /script 安装程序命令行选项，你必须创建一个初始化文件并在 /script 安装程序命令行选项后面指定初始化文件名。 只要文件的名称具有 .ini 文件扩展名，文件的名称并不重要。 如果从命令行引用安装程序初始化文件，则必须提供文件的完整路径。 例如，安装程序初始化文件的名称为 setup.ini，并且此文件存储在 C:\setup 文件夹中，则命令行应为：  

 **setup /script c:\setup\setup.ini**。  

> [!IMPORTANT]  
>  你必须具有管理员权限才能运行安装程序。 使用无人参与脚本运行安装程序时，请使用“以管理员身份运行” 在管理员上下文中启动命令提示符。  

 脚本包含部分名称、项名称和值。 所需部分项名称因你正在为其编写脚本的恢复类型而异。 部分内项的顺序和文件中部分的顺序并不重要。 项不区分大小写。 当你为项提供值时，项名称后面必须跟一个等号 (=) 以及该项的值。  

 使用下列部分来帮助你为无人参与的站点恢复创建脚本。 表格列出了可用的安装程序脚本项、其对应的值、是否需要它们、它们用于哪种安装类型以及项的简要描述。  

#### <a name="recover-a-central-administration-site-unattended"></a>在无人参与的情况下恢复管理中心站点  
 使用下列信息，配置无人参与的安装程序脚本文件以恢复管理中心站点。  

 **标识**  

-   **项名称：** Action  

    -   **是否必需：** 是  

    -   **值：** RecoverCCAR  

    -   **详细信息：** 恢复管理中心站点  

-   **密钥名称：**CDLatest  

    -   **必备：**是（仅在使用 CD.Latest 文件夹中的介质时）。    

    -   **值：**1。1 以外的任何值均视为不使用 CD.Latest。

    -   **详细信息：**从 CD.Latest 文件夹中的介质运行安装程序时，你的脚本必须包含该密钥和值，以安装主站点或管理中心站点，或恢复主站点或管理中心站点。 该值将告知安装程序当前使用介质形式 CD.Latest。  

**RecoveryOptions**  

-   **项名称：** ServerRecoveryOptions  

    -   **是否必需：** 是  

    -   **值：** 1、2 或 4  

         1 = 恢复站点服务器和 SQL Server。  

         2 = 仅恢复站点服务器。  

         4 = 仅恢复 SQL Server。  

    -   **详细信息：** 指定安装程序是恢复站点服务器、SQL Server 还是两者都恢复。 设置 ServerRecoveryOptions 设置的以下值时需要关联的项：  

        -   **值 = 1** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

             如果为 **DatabaseRecoveryOptions** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。  

        -   **值 = 2** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

        -   **值 = 4** 如果为 **BackupLocation** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。  

-   **项名称：** DatabaseRecoveryOptions  

    -   **是否必需：** 可能  

    -   **值：** 10、20、40、80  

         10 = 从备份中还原站点数据库。  

         20 = 使用已通过另一种方法手动恢复的站点数据库。  

         40 = 为站点创建新数据库。 没有可用的站点数据库备份时，请使用此选项。 通过其他站点中的复制来恢复全局数据和站点数据。  

         80 = 跳过数据库恢复。  

    -   **详细信息：** 指定安装程序将如何恢复 SQL Server 中的站点数据库。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **4**时，需要此项。  

-   **项名称：** ReferenceSite  

    -   **是否必需：** 可能  

    -   **值：**&lt;ReferenceSiteFQDN\>  

    -   **详细信息：** 指定在数据库备份早于更改跟踪保持期或者在没有备份的情况下恢复站点时，管理中心站点用于恢复全局数据的引用主站点。  

         如果未指定引用站点，并且备份早于更改跟踪保持期，则会使用管理中心站点中的还原数据重新初始化所有主站点。  

         如果未指定引用站点，并且备份在更改跟踪保持期中，则从主站点中仅复制备份以后的更改。 如果不同的主站点中具有冲突的更改，则管理中心站点使用它收到的第一个更改。  

         当 **DatabaseRecoveryOptions** 设置的值为 **40**时，需要此项。  

-   **项名称：** SiteServerBackupLocation  

    -   **是否必需：** 否  

    -   **值：**&lt;PathToSiteServerBackupSet\>  

    -   **详细信息：** 指定站点服务器备份集的路径。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **2**时，此项是可选的。 为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

-   **项名称：** BackupLocation  

    -   **是否必需：** 可能  

    -   &lt;PathToSiteDatabaseBackupSet\>  

    -   **详细信息：** 指定站点数据库备份集的路径。 如果为 **ServerRecoveryOptions** 项配置了值 **1** 或 **4** ，并为 **DatabaseRecoveryOptions** 项配置了值 **10** ，则需要 **BackupLocation** 项。  

**选项**  

-   **项名称：** ProductID  

    -   **是否必需：** 是  

    -   **值：**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         评估版  

    -   **详细信息：**Configuration Manager 安装产品密钥，包括短划线。 输入 **Eval** 可以安装 Configuration Manager 的评估版。  

-   **项名称：** SiteCode  

    -   **是否必需：** 是  

    -   **值：**&lt;Site code\>  

    -   **详细信息：** 三个字母数字字符，用于唯一标识层次结构中的站点。 你必须指定在发生故障之前站点使用的站点代码。  

-   **项名称：** SiteName  

    -   **是否必需：** 是  

    -   **值：** SiteName  

    -   **详细信息：** 此站点的描述。  

-   **项名称：** SMSInstallDir  

    -   **是否必需：** 是  

    -   &lt;*ConfigMgrInstallationPath*>  

    -   **详细信息：**指定 Configuration Manager 程序文件的安装文件夹。  

        > [!NOTE]  
        >  可以指定要用于 Configuration Manager 安装的原始路径或新路径。  

-   **项名称：** SDKServer  

    -   **是否必需：** 是  

    -   **值：**&lt;SMS 提供程序的 FQDN>  

    -   **详细信息：** 指定将托管 SMS 提供程序的服务器的 FQDN。 你必须指定在发生故障之前承载 SMS 提供程序的服务器。  

         你可以在初始安装后为站点配置其他 SMS 提供程序。  

-   **项名称：** PrerequisiteComp  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 下载  

         1 = 已下载  

    -   **详细信息：** 指定安装程序必备文件是否已下载。 例如，如果使用值 0，则安装程序将下载文件。  

-   **项名称：** PrerequisitePath  

    -   **是否必需：** 是  

    -   **值：**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **详细信息：** 指定安装程序必备文件的路径。 根据 **PrerequisiteComp** 值，安装程序将使用此路径来存储已下载文件或查找以前下载的文件。  

-   **项名称：** AdminConsole  

    -   **是否必需：** 可能  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否安装 Configuration Manager 控制台。 除非 **ServerRecoveryOptions** 设置的值为 **4**，否则此项为必需。  

-   **项名称：** JoinCEIP  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **详细信息：** 指定是否加入客户体验改善计划。  

**SQLConfigOptions**  

-   **项名称：** SQLServerName  

    -   **是否必需：** 是  

    -   **值：***&lt;SQLServerName\>*  

    -   **详细信息：**运行将托管站点数据库的 SQL Server 的服务器名称或群集实例名称。 你必须指定在发生故障之前承载站点数据库的同一服务器。  

-   **项名称：** DatabaseName  

    -   **是否必需：** 是  

    -   **值：**  

         *&lt;SiteDatabaseName\>*  

         对话框内的“操作”  

         *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*  

    -   **详细信息：**要创建或用于安装管理中心站点数据库的 SQL Server 数据库的名称。 你必须指定在发生故障之前使用的同一数据库名称。  

        > [!IMPORTANT]  
        >  如果未使用默认实例，你必须指定实例名称和站点数据库名称。  

-   **项名称：** SQLSSBPort  

    -   **是否必需：** 否  

    -   **值：**&lt;*SSBPortNumber*>  

    -   **详细信息：** 指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 通常，SSB 配置为使用 TCP 端口 4022，但也支持其他端口。 你必须指定在发生故障之前使用的相同 SSB 端口。  

#### <a name="recover-a-primary-site-unattended"></a>在无人参与的情况下恢复主站点  
 使用下列信息，配置无人参与的安装程序脚本文件以恢复管理中心站点。  

 **标识**  

-   **项名称：** Action  

    -   **是否必需：** 是  

    -   **值：** RecoverPrimarySite  

    -   **详细信息：** 恢复主站点  

-   **密钥名称：**CDLatest  

    -   **必备：**是（仅在使用 CD.Latest 文件夹中的介质时）。    

    -   **值：**1。1 以外的任何值均视为不使用 CD.Latest。

    -   **详细信息：**从 CD.Latest 文件夹中的介质运行安装程序时，你的脚本必须包含该密钥和值，以安装主站点或管理中心站点，或恢复主站点或管理中心站点。 该值将告知安装程序当前使用介质形式 CD.Latest。

**RecoveryOptions**  

-   **项名称：** ServerRecoveryOptions  

    -   **是否必需：** 是  

    -   **值：** 1、2 或 4  

         1 = 恢复站点服务器和 SQL Server。  

         2 = 仅恢复站点服务器。  

         4 = 仅恢复 SQL Server。  

    -   **详细信息：** 指定安装程序是恢复站点服务器、SQL Server 还是两者都恢复。 设置 ServerRecoveryOptions 设置的以下值时需要关联的项：  

        -   **值 = 1** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

             如果为 **DatabaseRecoveryOptions** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。  

        -   **值 = 2** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

        -   **值 = 4** 如果为 **BackupLocation** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。  

-   **项名称：** DatabaseRecoveryOptions  

    -   **是否必需：** 可能  

    -   **值：** 10、20、40、80  

         10 = 从备份中还原站点数据库。  

         20 = 使用已通过另一种方法手动恢复的站点数据库。  

         40 = 为站点创建新数据库。 没有可用的站点数据库备份时，请使用此选项。 通过其他站点中的复制来恢复全局数据和站点数据。  

         80 = 跳过数据库恢复。  

    -   **详细信息：** 指定安装程序将如何恢复 SQL Server 中的站点数据库。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **4**时，需要此项。  

-   **项名称：** SiteServerBackupLocation  

    -   **是否必需：** 否  

    -   **值：**&lt;PathToSiteServerBackupSet\>  

    -   **详细信息：** 指定站点服务器备份集的路径。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **2**时，此项是可选的。 为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

-   **项名称：** BackupLocation  

    -   **是否必需：** 可能  

    -   &lt;PathToSiteDatabaseBackupSet\>  

    -   **详细信息：** 指定站点数据库备份集的路径。 如果为 **ServerRecoveryOptions** 项配置了值 **1** 或 **4** ，并为 **DatabaseRecoveryOptions** 项配置了值 **10** ，则需要 **BackupLocation** 项。  

**选项**  

-   **项名称：** ProductID  

    -   **是否必需：** 是  

    -   **值：**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         评估版  

    -   **详细信息：**Configuration Manager 安装产品密钥，包括短划线。 输入 **Eval** 可以安装 Configuration Manager 的评估版。  

-   **项名称：** SiteCode  

    -   **是否必需：** 是  

    -   **值：**&lt;Site code\>  

    -   **详细信息：** 三个字母数字字符，用于唯一标识层次结构中的站点。 你必须指定在发生故障之前站点使用的站点代码。  

-   **项名称：** SiteName  

    -   **是否必需：** 是  

    -   **值：** SiteName  

    -   **详细信息：** 此站点的描述。  

-   **项名称：** SMSInstallDir  

    -   **是否必需：** 是  

    -   &lt;*ConfigMgrInstallationPath*>  

    -   **详细信息：**指定 Configuration Manager 程序文件的安装文件夹。  

        > [!NOTE]  
        >  可以指定要用于 Configuration Manager 安装的原始路径或新路径。  

-   **项名称：** SDKServer  

    -   **是否必需：** 是  

    -   **值：**&lt;SMS 提供程序的 FQDN>  

    -   **详细信息：** 指定将托管 SMS 提供程序的服务器的 FQDN。 你必须指定在发生故障之前承载 SMS 提供程序的服务器。  

         你可以在初始安装后为站点配置其他 SMS 提供程序。  

-   **项名称：** PrerequisiteComp  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 下载  

         1 = 已下载  

    -   **详细信息：** 指定安装程序必备文件是否已下载。 例如，如果使用值 0，则安装程序将下载文件。  

-   **项名称：** PrerequisitePath  

    -   **是否必需：** 是  

    -   **值：**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **详细信息：** 指定安装程序必备文件的路径。 根据 **PrerequisiteComp** 值，安装程序将使用此路径来存储已下载文件或查找以前下载的文件。  

-   **项名称：** AdminConsole  

    -   **是否必需：** 可能  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否安装 Configuration Manager 控制台。 除非 **ServerRecoveryOptions** 设置的值为 **4**，否则此项为必需。  

-   **项名称：** JoinCEIP  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **详细信息：** 指定是否加入客户体验改善计划。  

**SQLConfigOptions**  

-   **项名称：** SQLServerName  

    -   **是否必需：** 是  

    -   **值：***&lt;SQLServerName\>*  

    -   **详细信息：**运行将托管站点数据库的 SQL Server 的服务器名称或群集实例名称。 你必须指定在发生故障之前承载站点数据库的同一服务器。  

-   **项名称：** DatabaseName  

    -   **是否必需：** 是  

    -   **值：**  

         *&lt;SiteDatabaseName\>*  

         对话框内的“操作”  

         *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*  

    -   **详细信息：**要创建或用于安装管理中心站点数据库的 SQL Server 数据库的名称。 你必须指定在发生故障之前使用的同一数据库名称。  

        > [!IMPORTANT]  
        >  如果未使用默认实例，你必须指定实例名称和站点数据库名称。  

-   **项名称：** SQLSSBPort  

    -   **是否必需：** 否  

    -   **值：**&lt;*SSBPortNumber*>  

    -   **详细信息：** 指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 通常，SSB 配置为使用 TCP 端口 4022，但也支持其他端口。 你必须指定在发生故障之前使用的相同 SSB 端口。  

**层次结构扩展选项**  

-   **项名称：** CCARSiteServer  

    -   **是否必需：** 可能  

    -   **值：** &lt;SiteCodeForCentralAdministrationSite>  

    -   **详细信息：**指定主站点加入 Configuration Manager 层次结构时将要附加到的管理中心站点。 如果在发生故障之前主站点已附加到管理中心站点，则此设置为必需。 你必须指定在发生故障之前用于管理中心站点的站点代码。  

-   **项名称：** CASRetryInterval  

    -   **是否必需：** 否  

    -   **值：**&lt;Interval>  

    -   **详细信息：** 指定连接失败后尝试连接到管理中心站点的重试间隔（以分钟为单位）。 例如，如果连接到管理中心站点失败，则主站点将等待你为 CASRetryInterval 指定的分钟数，然后重新尝试连接。  

-   **项名称：** WaitForCASTimeout  

    -   **是否必需：** 否  

    -   **值：** &lt;Timeout>  

    -   **详细信息：** 指定主站点连接到管理中心站点的最大超时值（以分钟为单位）。 例如，主站点未能连接到管理中心站点，则在达到 WaitForCASTimeout 期间之前，主站点将基于 CASRetryInterval 重新尝试连接到管理中心站点。 你可以指定 0 到 100 的值。  

###  <a name="BKMK_PostRecovery"></a> 恢复后任务  
 恢复站点之后，有一些你必须在站点恢复完成之前考虑的恢复后任务。 使用下列部分来帮助你完成站点恢复过程。  

#### <a name="re-enter-user-account-passwords"></a>重新输入用户帐户密码  
 在站点服务器恢复之后，必须重新输入为站点指定的用户帐户的密码，因为这些密码在站点恢复过程中已重置。 在站点恢复完成后，这些帐户列在安装向导的“已完成”  页上，并保存到恢复的站点服务器上的 C:\ConfigMgrPostRecoveryActions.html。  

###### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>在站点恢复后重新输入用户帐户密码  

1.  打开 Configuration Manager 控制台并连接到恢复的站点。  

2.  在 Configuration Manager 控制台中，单击“管理” 。  

3.  在“管理”  工作区中，展开“安全” ，然后单击“帐户” 。  

4.  对于你必须重新输入密码的每个帐户，请执行下列操作：  

    1.  从站点恢复后确定的帐户的列表中选择帐户。 你可以在恢复的站点服务器上的 C:\ConfigMgrPostRecoveryActions.html 中找到此列表。  

    2.  在“主页”  选项卡上的“属性”  组中，单击“属性”  以打开帐户属性。  

    3.  在“常规”  选项卡上，单击“设置” ，然后为帐户重新输入密码。  

    4.  单击“验证” ，为所选用户帐户选择适当的数据源，然后单击“测试连接”  以验证该用户帐户是否可连接到数据源。  

    5.  单击“确定”  保存密码更改，然后单击“确定” 。  

#### <a name="re-enter-sideloading-keys"></a>重新输入旁加载密钥  
 在站点服务器恢复之后，必须重新输入为站点指定的 Windows 旁加载密钥，因为这些密钥在站点恢复过程中已重置。 重新输入旁加载密钥后，将在 Configuration Manager 控制台中重置 Windows 旁加载密钥的“已使用激活数”列中的计数。 例如，假设在站点失败之前，针对设备已经使用的密钥数将“激活总数”计数设置为“100”，将“已使用激活数”设置为“90”。 在站点恢复之后，“激活总数”  列仍显示“100” ，但“已使用激活数”  列错误地显示“0” 。 然而，在 10 个新设备使用旁加载密钥之后，将没有剩余的旁加载密钥，下一个设备将无法应用旁加载密钥。  

#### <a name="recreate-the-microsoft-intune-subscription"></a>重新创建 Microsoft Intune 订阅  
 如果在重新制作站点服务器计算机的映像后恢复 Configuration Manager 站点服务器，将不会还原 Microsoft Intune 订阅。 恢复站点后必须重新连接订阅。  不要创建新的 APN 要求，而改为上传当前有效的 .pem 文件，此文件在上一次配置或续订 iOS 管理时上传。 有关详细信息，请参阅 [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription)。  

#### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>为使用 IIS 的站点系统角色配置 SSL  
 当你恢复运行 IIS 并且在发生故障之前针对 HTTPS 进行了配置的站点系统时，你必须重新配置 IIS 以使用 Web 服务器证书。  

#### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>在恢复的站点服务器中重新安装修补程序  
 站点恢复之后，你必须重新安装之前应用于站点服务器的任何修补程序。 在站点恢复后，以前安装的修补程序的列表列在安装向导的“已完成”  页上，并保存到恢复的站点服务器上的 **C:\ConfigMgrPostRecoveryActions.html** 。  

#### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>在运行 Reporting Services 的计算机上恢复自定义报表  
 如果创建了自定义 Reporting Services 报表，并且 Reporting Services 失败，则可以在备份了报表服务器时恢复报表。 有关在 Reporting Services 中还原自定义报表的详细信息，请参阅 SQL Server 2008 联机丛书中的 [Reporting Services 安装的备份和还原操作](http://go.microsoft.com/fwlink/p/?LinkId=228724) 。  

#### <a name="recover-content-files"></a>恢复内容文件  
 站点数据库包含有关内容文件在站点服务器上的存储位置的信息，但在备份和恢复过程中不会备份或还原内容文件。 要完全恢复内容文件，你必须将内容库和包源文件还原到原始位置。 有很多用于恢复内容文件的方法，但最简单的方法是从站点服务器的文件系统备份中还原文件。  

 如果没有包源文件的文件系统备份，你必须按照最初创建包时的方式手动复制或下载这些文件。 你可以在 SQL Server 中运行以下查询来查找所有包和应用程序的包源位置： `SELECT * FROM v_Package`。 你可以通过查看包 ID 的前三个字符来确定包源站点。 例如，如果包 ID 为 CEN00001，则源站点的站点代码为 CEN。 在还原包源文件时，必须将它们还原到发生故障之前所在的同一位置。  

 如果没有包含内容库的文件系统备份，则有下列还原选项：  

-   **导入预安排内容文件**：如果有 Configuration Manager 层次结构，可以创建包含另一个位置中的所有包和应用程序的预安排内容文件，然后导入该预安排内容文件以在站点服务器上恢复内容库。  

-   **更新内容**：当你为包或应用程序部署类型启动更新内容操作时，会将内容从包源复制到内容库。 原始位置中必须有包源文件，此操作才能成功完成。 你必须对每个包和应用程序执行此操作。  

#### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>在运行 Updates Publisher 的计算机上恢复自定义软件更新  
 如果在备份计划中包括了 Updates Publisher 数据库文件，可以在运行 Updates Publisher 的计算机发生故障时恢复数据库。 有关 Updates Publisher 的详细信息，请参阅 System Center TechCenter 库中的 [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) 。  

 使用下列过程来还原 Updates Publisher 数据库。  

###### <a name="to-restore-the-updates-publisher-2011-database"></a>还原 Updates Publisher 2011 数据库  

1.  在恢复的计算机上重新安装 Updates Publisher。  

2.  将数据库文件 (Scupdb.sdf) 从备份目标复制到运行 Updates Publisher 的计算机上的 %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ 中。  

3.  如果有多个用户在计算机上运行 Updates Publisher，则必须将每个数据库文件复制到相应的用户配置文件位置。  

#### <a name="user-state-migration-data"></a>用户状态迁移数据  
 作为状态迁移点站点系统属性的一部分，要指定存储用户状态迁移数据的文件夹。 在恢复带有此类文件夹（存储了用户状态迁移数据）的服务器之后，必须手动将该服务器上的用户状态迁移数据还原到在失败前存储此数据的相同文件夹中。  

#### <a name="regenerate-the-certificates-for-distribution-points"></a>重新生成分发点的证书  
 还原站点后，distmgr.log 可能包含一个或多个分发点的以下条目： **无法解密证书 PFX 数据**。 此条目表示站点无法解密分发点证书数据。 为了解决这一问题，你必须重新生成或重新导入受影响分发点的证书。 此过程可使用 [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) PowerShell cmdlet 完成。  

#### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>更新用于基于云的分发点的证书  
 Configuration Manager 需要使用管理证书来执行从站点服务器到基于云的分发点的通信。 在站点恢复之后，必须为基于云的分发点更新证书。  

####  <a name="BKMK_RecoverSecondarySite"></a> 恢复辅助站点  
 Configuration Manager 不支持在辅助站点上进行数据库备份，但支持通过重新安装辅助站点进行恢复。 在 Configuration Manager 辅助站点失败时，必须恢复辅助站点。 可以在 Configuration Manager 控制台的“站点”节点中使用“恢复辅助站点”操作来恢复辅助站点。 与恢复管理中心站点或主站点不同的是，恢复辅助站点不使用备份文件，而是在失败的辅助站点计算机上重新安装辅助站点文件。 然后，使用父主站点中的数据重新初始化辅助站点数据。 在恢复过程中，Configuration Manager 会验证辅助站点计算机上是否存在内容库，以及合适的内容是否可用。 如果辅助站点包含合适的内容，则它将使用现有的内容库。 否则，若要恢复已恢复辅助站点的内容库，则需将内容重新分发或预留到该已恢复站点。 如果拥有不在辅助站点上的分发点，则无需在恢复辅助站点的过程中重新安装分发点。 在恢复辅助站点之后，站点会自动与分发点同步。  

 可以在 Configuration Manager 控制台的“站点”节点中使用“显示安装状态”操作来验证辅助站点恢复的状态。  

> [!IMPORTANT]  
>  必须使用在配置上与失败的计算机相同（例如使用其 FQDN）的计算机才能成功恢复辅助站点。 计算机还必须满足辅助站点的所有先决条件，而且具有适当的安全权限配置。 此外，还要使用失败的站点所用的相同安装路径。  

> [!IMPORTANT]  
>  在恢复辅助站点的过程中，如果计算机上未安装 SQL Server Express，则 Configuration Manager 并不会安装它。 因此，在恢复辅助站点之前，必须手动安装 SQL Server Express 或 SQL Server。 必须使用在失败前用于辅助站点数据库的同一个 SQL Server 版本和同一个 SQL Server 实例。  

##  <a name="BKMK_SMSWriterService"></a> SMS 编写器服务  
 SMS 编写器是一项服务，该服务在备份过程中与卷影复制服务 (VSS) 交互。 SMS 编写器服务必须正在运行，Configuration Manager 站点备份才能成功完成。  

### <a name="purpose"></a>目的  
 SMS 编写器向 VSS 服务注册，并绑定到其接口和事件。 当 VSS 广播事件时，或者，如果它将特定通知发送到 SMS 编写器，SMS 编写器将响应通知并执行适当的操作。 SMS 编写器可读取位于 &lt;*ConfigMgr Installation Path*>\inboxes\smsbkup.box 中的备份控制文件 (smsbkup.ctl)，并确定要备份的文件和数据。 SMS 编写器根据此信息以及 SMS 注册表项和子项中的特定数据生成由不同部分组成的元数据。 当请求元数据时，它将元数据发送到 VSS。 然后，VSS 将元数据发送到请求应用程序，即 Configuration Manager 备份管理器。 备份管理器选择备份的数据并通过 VSS 将此数据发送到 SMS 编写器。 SMS 编写器执行适当的步骤来为备份做好准备。 稍后，当 VSS 准备获取快照时，它将发送事件，SMS 编写器停止所有 Configuration Manager 服务，并确保在创建快照时 Configuration Manager 活动已冻结。 完成快照后，SMS 编写器重启服务和活动。  

 将自动安装 SMS 编写器服务。 当 VSS 应用程序请求备份或还原时，该服务必须正在运行。  

### <a name="writer-id"></a>编写器 ID  
 SMS 编写器的编写器 ID 为：03ba67dd-dc6d-4729-a038-251f7018463b。  

### <a name="permissions"></a>权限  
 SMS 编写器服务必须采用本地系统帐户运行。  

### <a name="volume-shadow-copy-service"></a>卷影复制服务  
 VSS 是一组 COM API，它实现一个框架，以允许在系统上的应用程序继续写入卷时执行所有卷备份。 VSS 提供一个一致的接口，在用于更新磁盘上的数据的用户应用程序（SMS 编写器服务）和用于备份应用程序的用户应用程序（备份管理器服务）之间实现协作。 有关 VSS 的详细信息，请参阅 Windows Server TechCenter 中的 [Volume Shadow Copy Service（卷影复制服务）](http://go.microsoft.com/fwlink/p/?LinkId=241968) 主题。  

