---
title: "备份站点 | Microsoft 文档"
description: "在 System Center Configuration Manager 中出现故障或数据丢失之前备份站点。"
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: "22"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7deb00d4b67eabf3238907b337a9d0367c3d99cc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="back-up-a-configuration-manager-site"></a>备份 Configuration Manager 站点

*适用范围：System Center Configuration Manager (Current Branch)*

准备备份和恢复方法，以避免数据丢失。 对于 Configuration Manager 站点，备份和恢复方法可有助于更快地恢复站点和层次结构，并最大程度降低数据丢失的风险。  

本主题中介绍的内容可帮助你备份站点。 要恢复站点，请参阅 [Configuration Manager 的恢复](/sccm/protect/understand/recover-sites)。  

## <a name="considerations-before-creating-a-backup"></a>创建备份之前的注意事项  
-   如果你使用 SQL Server AlwaysOn 可用性组来承载站点数据库：按照[准备使用 SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup) 中的说明修改你的备份和恢复计划。

-   Configuration Manager 可以从 Configuration Manager 备份维护任务或从使用另一个进程创建的站点数据库备份来恢复站点数据库。   

    例如，可以通过作为 Microsoft SQL Server 维护计划一部分创建的备份来还原站点数据库。 你还可以使用通过使用 Data Protection Manager 创建的备份来备份站点数据库 (DPM)。

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>使用 Data Protection Manager 来备份站点数据库
你可以使用 System Center 2012 Data Protection Manager (DPM) 来备份站点数据库。

你可以在 DPM 中为站点数据库计算机创建一个新保护组。 在创建新保护组向导的“选择组成员”页上，从数据源列表中选择 SMS 编写器服务，然后选择站点数据库作为适当的成员。 有关使用 DPM 来备份站点数据库的详细信息，请参阅 TechNet 上的 [Data Protection Manager Documentation Library（Data Protection Manager 文档库）](http://go.microsoft.com/fwlink/?LinkId=272772)。  

> [!IMPORTANT]  
>  Configuration Manager 不支持对使用命名实例的 SQL Server 群集进行 DPM 备份，但支持对使用默认 SQL Server 实例的 SQL Server 群集进行 DPM 备份。  

 还原站点数据库之后，请按照安装程序中的步骤进行操作以恢复站点。 选择“使用已手动恢复的站点数据库”恢复选项以使用通过 Data Protection Manager 恢复的站点数据库。  

## <a name="backup-maintenance-task"></a>备份维护任务
可以通过计划预定义的备份站点服务器维护任务来自动完成 Configuration Manager 站点的备份。 此任务包括：

-   按计划运行
-   备份站点数据库
-   备份特定注册表项
-   备份特定文件夹和文件
-   备份 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)   

计划至少每 5 天运行一次默认站点备份任务。 这是因为 Configuration Manager 使用为期 5 天的 SQL Server 更改跟踪保持期。  （请参阅“恢复站点”主题中的 [SQL Server 更改跟踪保持期](/sccm/protect/understand/recover-sites#bkmk_SQLretention)。）

若要简化备份过程，可以创建 **AfterBackup.bat** 文件以在备份维护任务成功运行后自动执行备份后操作。 AfterBackup.bat 文件通常用于将备份快照存档到安全位置。 也可以使用 AfterBackup.bat 文件将文件复制到备份文件夹并启动其他补充备份任务。  

你可以备份管理中心站点和主站点，但不支持备份辅助站点或站点系统服务器。

当 Configuration Manager 备份服务运行时，它将按照备份控制文件 (**&lt;ConfigMgrInstallationFolder\>\Inboxes\Smsbkup.box\Smsbkup.ctl**) 中定义的指令进行操作。 你可以修改备份控制文件来更改备份服务的行为。  

站点备份状态信息将写入 **Smsbkup.log** 文件。 将在备份站点服务器维护任务属性内指定的目标文件夹中创建此文件。  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>启用站点备份维护任务  

1.  在 Configuration Manager 控制台中，依次打开“管理” > “站点配置” > “站点”。  

2.  选择要在其中启用站点备份维护任务的站点。  

3.  在“主页”选项卡上的“设置”组中，选择“站点维护任务”。  

4.  选择“备份站点服务器”  >  “编辑”。  

5.  选择“启用此任务” > “设置路径”以指定备份目标。 有下列选项：  

    > [!IMPORTANT]  
    >  为了帮助防止篡改备份文件，请将文件存储在安全的位置。 最安全的备份路径是本地驱动器，因此你可以在文件夹上设置 NTFS 文件系统权限。 Configuration Manager 不会对备份路径中存储的备份数据进行加密。  

    -   站点服务器上用于站点数据和数据库的本地驱动器：指定将站点和站点数据库的备份文件存储在站点服务器本地磁盘驱动器上的指定路径中。 你必须在备份任务运行之前创建本地文件夹。 站点服务器上的本地系统帐户必须具有站点服务器备份的本地文件夹的**“写入”**NTFS 文件系统权限。 运行 SQL Server 的计算机上的本地系统帐户必须具有站点数据库备份文件夹的**“写入”**NTFS 权限。  

    -   站点数据和数据库的网络路径（UNC 名称）：指定将站点和站点数据库的备份文件存储在指定 UNC 路径中。 你必须在备份任务运行之前创建共享。 站点服务器的计算机帐户以及 SQL Server 的计算机帐户（如果 SQL Server 安装在另一台计算机上）必须具有共享网络文件夹的“写入”NTFS 和共享权限。  

    -   **站点服务器和 SQL Server 上的本地驱动器**：指定将站点的备份文件存储在站点服务器本地驱动器上的指定路径中，并将站点数据库的备份文件存储在站点数据库服务器本地驱动器上的指定路径中。 你必须在备份任务运行之前创建本地文件夹。 站点服务器的计算机帐户必须具有你在站点服务器上创建的文件夹的“写入”NTFS 权限。 SQL Server 的计算机帐户必须具有你在站点数据库服务器上创建的文件夹的“写入”NTFS 权限。 只有在站点服务器未安装站点数据库时，此选项才可用。  

    > [!NOTE]  
    >   只有在你指定备份目标的 UNC 路径时，用于浏览到备份目标的选项才可用。

    > 用于备份目标的文件夹名称或共享名称不支持使用 Unicode 字符。  

6.  为站点备份任务配置计划。 作为最佳方案，请考虑活动工作时间外的备份计划。 如果有层次结构，请考虑使用一周至少运行两次的计划，以确保在出现站点故障时保留最大量的数据。  

    如果在为备份配置的同一站点服务器上运行 Configuration Manager 控制台，则备份站点服务器维护任务将为计划使用本地时间。 如果 Configuration Manager 控制台从为备份配置的站点的远程计算机中运行，则备份站点服务器维护任务为计划使用 UTC。  

7.  选择在站点备份任务失败时是否创建警报，单击“确定”，然后单击“确定”。 如果选择，则 Configuration Manager 将为备份失败创建关键警报，可以在“监视”工作区的“警报”节点中查看该警报。  

 接下来，验证备份站点服务器维护任务是否正在运行，以确保正在创建备份。  

#### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>验证备份站点服务器维护任务是否正在运行  
通过查看下列任何信息来验证站点备份维护任务是否正在运行：  

-   检查该任务创建的备份目标文件夹中的文件上的时间戳。 验证是否已使用与上次计划运行该任务的时间匹配的时间更新了该时间戳。  

-   在“监视”工作区的“组件状态”节点中，查看 SMS_SITE_BACKUP 的状态消息。 如果站点备份成功完成，你将看到消息 ID 5035，指示站点备份已成功完成，且未出现任何错误。  

-   如果将备份站点服务器维护任务配置为在备份失败的情况下创建警报，你可以检查“监视”工作区中的“警报”节点来了解备份失败情况。  

-   在 &lt;*ConfigMgrInstallationFolder*>\Logs 中，查看 Smsbkup.log 以了解警告和错误。 站点备份成功完成后，你将看到`Backup completed`，时间戳和消息 ID 为 `STATMSG: ID=5035`。  

    > [!TIP]  
    >  如果备份维护任务失败，你可以通过停止并重启 SMS_SITE_BACKUP 服务来重启备份任务。  

## <a name="archive-the-backup-snapshot"></a>存档备份快照  
备份站点服务器维护任务第一次运行时将创建一个备份快照，你可以使用该快照在出现故障时恢复站点服务器。 当备份任务在后续周期中再次运行时，它将创建新备份快照，该快照将覆盖以前的快照。 因此，站点只有一个备份快照，并且你无法检索以前的备份快照。  

作为最佳方案，请保留备份快照的多个存档，原因如下：  

-   备份媒体经常会出现故障、位置不正确或仅包含部分备份。 从较旧的备份恢复出现故障的独立主站点比在没有任何备份的情况下进行恢复要好。 对于层次结构中的站点服务器，备份必须位于 SQL Server 更改跟踪保持期内，或者不需要备份。  

-   对于若干备份周期，可能检测不到站点中的损坏。 可能必须使用获取自站点损坏之前的备份快照。 这适用于独立主站点以及层次结构中备份处于 SQL Server 更改跟踪保持期内的站点。  

-   举例来说，如果备份站点服务器维护任务失败，站点将可能根本没有任何备份快照。 由于备份任务会在其开始备份当前数据之前删除以前的备份快照，因此将不具备有效的备份快照。  

## <a name="using-the-afterbackupbat-file"></a>使用 AfterBackup.bat 文件  
成功备份站点之后，备份站点服务器任务会自动尝试运行一个名为 AfterBackup.bat 的文件。 必须在 &lt;*ConfigMgrInstallationFolder*>\Inboxes\Smsbkup 中手动创建 AfterBackup.bat 文件。 如果 AfterBackup.bat 文件存在并存储在正确的文件夹中，则该文件将在备份任务完成后自动运行。

AfterBackup.bat 文件使你能够在每个备份操作结束时将备份快照存档，并自动执行不属于备份站点服务器维护任务一部分的其他备份后任务。 AfterBackup.bat 文件将存档和备份操作结合，从而确保将每个新备份快照存档。

如果 AfterBackup.bat 文件不存在，备份任务将跳过该文件，不会对备份操作产生影响。 要验证站点备份任务是否成功运行了 AfterBackup.bat 文件，请查看“监视”工作区的“组件状态”节点，并查看 SMS_SITE_BACKUP 的状态消息。 如果任务成功启动了 AfterBackup.bat 命令文件，你将看到消息 ID 5040。  

> [!TIP]  
>  要创建 AfterBackup.bat 文件以将站点服务器备份文件存档，必须在该批处理文件中使用复制命令工具，例如 [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408)。 例如，你可以创建 AfterBackup.bat 文件，并在第一行上添加以下类似内容：`Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

 尽管 AfterBackup.bat 的预期用途是将备份快照存档，但你可以创建 AfterBackup.bat 文件以在每个备份操作结束时执行其他任务。  

##  <a name="supplemental-backup-tasks"></a>补充备份任务  
备份站点服务器维护任务提供站点服务器文件和站点数据库的备份快照，但会存在一些你在创建备份策略时必须考虑的其他未备份项目。 使用下列部分来帮助完成 Configuration Manager 备份策略。  

### <a name="back-up-custom-reporting-services-reports"></a>备份自定义 Reporting Services 报表  
如果修改了预定义或已创建自定义 Reporting Services 报表，则为报表服务器数据库文件创建备份是备份策略的一个重要部分。 报表服务器备份必须包括报表和模型的源文件、加密密钥、自定义程序集或扩展、配置文件、自定义报表中使用的自定义 SQL Server 视图、自定义存储过程等的备份。  

> [!IMPORTANT]  
>  将 Configuration Manager 升级到较新版本时，预定义的报表可能被新报表覆盖。 如果修改预定义报表，请备份该报表，然后在 Reporting Services 中将其还原。  

 有关在 Reporting Services 中备份自定义报表的详细信息，请参阅 SQL Server 2014 联机丛书中的 [Reporting Services 安装的备份和还原操作](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) 。  

### <a name="back-up-content-files"></a>备份内容文件  
Configuration Manager 中的内容库是存储软件更新、应用程序、操作系统部署等的所有内容文件的位置。 内容库位于站点服务器和每个分发点上。 “备份站点服务器”维护任务不包含内容库或包源文件的备份。 在站点服务器失败时，有关内容库文件的信息会被还原到站点数据库，但你必须还原站点服务器上的内容库和包源文件。  

-   内容库：必须还原内容库，然后才能将内容重新分发到分发点。 当开始执行内容重分发时，Configuration Manager 会将文件从站点服务器上的内容库复制到分发点。 站点服务器的内容库位于 SCCMContentLib 文件夹中，该文件夹通常位于安装站点时可用磁盘空间最多的驱动器上。  

-   包源文件：必须还原包源文件，然后才能更新分发点上的内容。 当开始进行内容更新时，Configuration Manager 会将新文件或修改的文件从包源复制到内容库，后者依次将这些文件复制到关联的分发点。 你可以在 SQL Server 中运行以下查询来查找所有包和应用程序的包源位置：`SELECT * FROM v_Package`。 你可以通过查看包 ID 的前三个字符来确定包源站点。 例如，如果包 ID 为 CEN00001，则源站点的站点代码为 CEN。 在还原包源文件时，必须将它们还原到发生故障之前所在的同一位置。  

 验证是否在站点服务器的文件系统备份中包括了内容库和包源位置。  

### <a name="back-up-custom-software-updates"></a>备份自定义软件更新  
 System Center Updates Publisher 2011 是一种独立工具，通过该工具可将自定义软件更新发布到 Windows Server Update Services (WSUS)、将软件更新同步到 Configuration Manager、评估软件更新符合性，并将自定义软件更新部署到客户端。 Updates Publisher 为其软件更新存储库使用本地数据库。 使用 Updates Publisher 管理自定义软件更新时，请确定是否应在备份计划中包括 Updates Publisher 数据库。 有关 Updates Publisher 的详细信息，请参阅 System Center TechCenter 库中的 [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) 。  

 使用下列过程来备份 Updates Publisher 数据库。  

#### <a name="to-back-up-the-updates-publisher-2011-database"></a>备份 Updates Publisher 2011 数据库  

1.  在运行 Updates Publisher 的计算机上，浏览到 %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\ 中的 Updates Publisher 数据库文件 (Scupdb.sdf)。 每个运行 Updates Publisher 的用户有不同的数据库文件。  

2.  将数据库文件复制到备份目标。 例如，如果备份目标为 E:\ConfigMgr_Backup，则可将 Updates Publisher 数据库文件复制到 E:\ConfigMgr_Backup\SCUP2011。  

    > [!TIP]  
    >  如果计算机上有多个数据库文件，请考虑将文件存储在子文件夹中，该子文件夹指示与数据库文件关联的用户配置文件。 例如，你可能在 E:\ConfigMgr_Backup\SCUP2011\User1 中有一个数据库文件，并在 E:\ConfigMgr_Backup\SCUP2011\User2 中有另一个数据库文件。  

## <a name="user-state-migration-data"></a>用户状态迁移数据  
在希望保留当前操作系统的用户状态的操作系统部署方案中，可以使用 Configuration Manager 任务序列来捕获和还原用户状态数据。 状态迁移点的属性中列出了存储用户状态数据的文件夹。 在站点服务器备份维护任务中，不会备份此用户状态迁移数据。 作为备份计划的一部分，你必须手动备份指定用于存储用户状态迁移数据的文件夹。   

### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>确定用于存储用户状态迁移数据的文件夹  

1.  在 Configuration Manager 控制台中，单击“管理”。  

2.  在“管理”工作区中，展开“站点配置”，并选择“服务器和站点系统角色”。  

3.  选择承载状态迁移角色的站点系统，然后在“站点系统角色”中选择“状态迁移点”。  


4.  在“站点角色”选项卡上的“属性”组中，单击“属性”。  
5.  “常规”选项卡上的“文件夹详细信息”部分中列出了存储用户状态迁移数据的文件夹。  



## <a name="about-the-sms-writer-service"></a>关于 SMS 编写器服务  
SMS 编写器是一项服务，该服务在备份过程中与卷影复制服务 (VSS) 交互。 SMS 编写器服务必须正在运行，Configuration Manager 站点备份才能成功完成。  

### <a name="purpose"></a>目的  
SMS 编写器向 VSS 服务注册，并绑定到其接口和事件。 当 VSS 广播事件时，或者，如果它将特定通知发送到 SMS 编写器，SMS 编写器将响应通知并执行适当的操作。 SMS 编写器可读取位于 &lt;*ConfigMgr Installation Path*>\inboxes\smsbkup.box 中的备份控制文件 (smsbkup.ctl)，并确定要备份的文件和数据。 SMS 编写器根据此信息以及 SMS 注册表项和子项中的特定数据生成由不同部分组成的元数据。 当请求元数据时，它将元数据发送到 VSS。 然后，VSS 将元数据发送到请求应用程序，即 Configuration Manager 备份管理器。 备份管理器选择备份的数据并通过 VSS 将此数据发送到 SMS 编写器。 SMS 编写器执行适当的步骤来为备份做好准备。 稍后，当 VSS 准备获取快照时，它将发送事件，SMS 编写器停止所有 Configuration Manager 服务，并确保在创建快照时 Configuration Manager 活动已冻结。 完成快照后，SMS 编写器重启服务和活动。  

将自动安装 SMS 编写器服务。 当 VSS 应用程序请求备份或还原时，该服务必须正在运行。  

### <a name="writer-id"></a>编写器 ID  
SMS 编写器的编写器 ID 为：03ba67dd-dc6d-4729-a038-251f7018463b。  

### <a name="permissions"></a>权限  
SMS 编写器服务必须采用本地系统帐户运行。  

### <a name="volume-shadow-copy-service"></a>卷影复制服务  
VSS 是一组 COM API，它实现一个框架，以允许在系统上的应用程序继续写入卷时执行所有卷备份。 VSS 提供一个一致的接口，在用于更新磁盘上的数据的用户应用程序（SMS 编写器服务）和用于备份应用程序的用户应用程序（备份管理器服务）之间实现协作。 有关详细信息，请参阅 Windows Server TechCenter 中的[卷影复制服务](http://go.microsoft.com/fwlink/p/?LinkId=241968)主题。  

## <a name="next-steps"></a>后续步骤
创建备份后，使用该备份练习[站点恢复](/sccm/protect/understand/recover-sites)。 这可以帮助你在需要基于备份执行恢复操作之前熟悉恢复过程，并有助于确认备份是否可成功实现其预期目的。  
