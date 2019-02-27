---
title: 备份站点
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中出现故障或数据丢失之前备份站点。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e876e34929479654240ff220c3cad91043da0f83
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123131"
---
# <a name="back-up-a-configuration-manager-site"></a>备份 Configuration Manager 站点

适用范围：System Center Configuration Manager (Current Branch)

准备备份和恢复方法，以避免数据丢失。 对于 Configuration Manager 站点，备份和恢复方法可有助于更快地恢复站点和层次结构，并最大程度降低数据丢失的风险。  

本文中介绍的内容可帮助备份站点。 要恢复站点，请参阅 [Configuration Manager 的恢复](/sccm/core/servers/manage/recover-sites)。  



## <a name="considerations-before-creating-a-backup"></a>创建备份之前的注意事项  

-   如果使用 SQL Server Always On 可用性组托管站点数据库：修改备份和恢复计划，如[准备使用 SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup) 中所述。  

-   Configuration Manager 可以从 Configuration Manager 备份任务恢复站点数据库。 它还可以使用通过其他进程创建的站点数据库的备份。   

     例如，可以从作为 Microsoft SQL Server 维护计划一部分创建的备份还原站点数据库。 还可以使用通过使用 Data Protection Manager 创建的备份来备份站点数据库。  

-   从版本 1806 开始，安装处于被动模式的额外站点服务器。 被动模式下的站点服务器是对主动模式下的现有站点服务器的补充。 在需要时可立即使用被动模式下的站点服务器。 有关详细信息，请参阅[站点服务器高可用性](/sccm/core/servers/deploy/configure/site-server-high-availability)。 虽然此角色并不能消除规划和实施备份和恢复操作的需要，但它可以显著减少在必要时恢复站点的工作量。  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>使用 Data Protection Manager 来备份站点数据库
可以使用 System Center Data Protection Manager (DPM) 备份 Configuration Manager 站点数据库。

在 DPM 中为站点数据库计算机创建一个新保护组。 在创建新保护组向导的“选择组成员”页上，从数据源列表中选择 SMS 编写器服务。 然后选择站点数据库作为适当的成员。 有关使用 DPM 的详细信息，请参阅 [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) 文档库。  

> [!IMPORTANT]  
>  对于使用命名实例的 SQL Server 群集，Configuration Manager 不支持 DPM 备份。 它支持使用默认 SQL Server 实例的 SQL Server 群集上的 DPM 备份。  

还原站点数据库之后，请按照安装程序中的步骤进行操作以恢复站点。 要使用通过 Data Protection Manager 备份的站点数据库，请选择“使用已手动恢复的站点数据库”恢复选项。  



## <a name="backup-maintenance-task"></a>备份维护任务
可以通过计划预定义的备份站点服务器维护任务来自动完成 Configuration Manager 站点的备份。 此任务具有以下功能：

-   按计划运行
-   备份站点数据库
-   备份特定注册表项
-   备份特定文件夹和文件
-   备份 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)   

计划至少每 5 天运行一次默认站点备份任务。 此计划是因为 Configuration Manager 使用为期 5 天的 SQL Server 更改跟踪保持期。 有关详细信息，请参阅 [SQL Server 更改跟踪保留期](/sccm/protect/understand/recover-sites#bkmk_SQLretention)。

要简化备份过程，可以创建 AfterBackup.bat 文件。 备份任务成功完成后，此脚本会自动运行备份后操作。 使用 AfterBackup.bat 文件将备份快照存档到安全位置。 也可以使用 AfterBackup.bat 文件将文件复制到备份文件夹，或启动其他备份任务。  

可以备份管理中心站点和主站点。 辅助站点或站点系统服务器没有备份任务。

当 Configuration Manager 备份服务运行时，它会按照备份控制文件中定义的指令进行操作：`<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`。 你可以修改备份控制文件来更改备份服务的行为。  

站点备份状态信息将写入 **Smsbkup.log** 文件。 将在备份站点服务器维护任务属性内指定的目标文件夹中创建此文件。  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>启用站点备份维护任务  
1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。  

2.  选择要在其中启用站点备份维护任务的站点。  

3.  单击功能区中的“站点维护任务”。  

4.  选择“备份站点服务器”任务，然后单击“编辑”。  

5.  选择“启用此任务”选项。 单击“设置路径”以指定备份目标。 有下列选项：  

    > [!IMPORTANT]  
    >  为了帮助防止篡改备份文件，请将文件存储在安全的位置。 最安全的备份路径是本地驱动器，因此可以在文件夹上设置 NTFS 文件权限。 Configuration Manager 不会对备份路径中存储的备份数据进行加密。  

    -   **站点服务器上用于站点数据和数据库的本地驱动器**：指定任务将站点和站点数据库的备份文件存储在站点服务器本地磁盘驱动器上的指定路径中。 在备份任务运行之前创建本地文件夹。 站点服务器上的本地系统帐户必须具有站点服务器备份的本地文件夹的“写入”NTFS 文件权限。 运行 SQL Server 的计算机上的本地系统帐户必须具有站点数据库备份文件夹的“写入”NTFS 权限。  

    -   **站点数据和数据库的网络路径(UNC 名称)**：指定任务将站点和站点数据库的备份文件存储在指定的网络路径中。 在备份任务运行之前创建共享。 站点服务器的计算机帐户必须具有对共享网络文件夹的“写入”NTFS 和共享权限。 如果 SQL Server 安装在另一台计算机上，则 SQL Server 的计算机帐户必须具有相同的权限。  

    -   **站点服务器和 SQL Server 上的本地驱动器**：指定任务将站点的备份文件存储在站点服务器的本地驱动器上的指定路径中。 该任务将站点数据库的备份文件存储在站点数据库服务器的本地驱动器上的指定路径中。 在备份任务运行之前创建本地文件夹。 站点服务器的计算机帐户必须具有你在站点服务器上创建的文件夹的“写入”NTFS 权限。 SQL Server 的计算机帐户必须具有你在站点数据库服务器上创建的文件夹的“写入”NTFS 权限。 只有在站点服务器未安装站点数据库时，此选项才可用。  

    > [!NOTE]  
    >   只有在指定了备份目标的网络路径时，用于浏览到备份目标的选项才可用。  
    >  
    > 用于备份目标的文件夹名称或共享名称不支持使用 Unicode 字符。  

6.  为站点备份任务配置计划。 请考虑活动工作时间外的备份计划。 如果具有层次结构，请考虑每周至少运行两次的计划。 如果站点失败，则此计划可确保最大程度的数据保留。  

    如果在为备份配置的同一站点服务器上运行 Configuration Manager 控制台，则备份任务将为计划使用本地时间。 从另一台计算机运行 Configuration Manager 控制台时，备份任务为计划使用协调世界时 (UTC)。  

7.  选择在站点备份任务失败时是否创建警报。 选择后，Configuration Manager 会为备份失败创建严重警报。 可以在“监视”工作区的“警报”节点中查看这些警报。  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>验证备份站点服务器维护任务是否正在运行  

-   检查该任务创建的备份目标文件夹中的文件上的时间戳。 验证时间戳是否更新为上次计划运行任务的时间。  

-   转到“监视”工作区的“组件状态”节点。 查看 SMS_SITE_BACKUP 的状态消息。 站点备份成功完成后，会看到消息 ID 5035。 此消息表示站点备份已完成且没有任何错误。  

-   将备份任务配置为在失败时创建警报后，请在“监视”工作区的“警报”节点中查找备份失败警报。  

-   在站点服务器上打开 Windows 资源管理器并浏览到 `<ConfigMgrInstallationFolder>\Logs`。 查看“Smsbkup.log”以了解警告和错误。 站点备份成功完成后，日志会显示消息 ID 为 `STATMSG: ID=5035` 的 `Backup completed`。  

    > [!TIP]  
    >  如果备份维护任务失败，则可以通过停止并重启 SMS_SITE_BACKUP Windows 服务来重启备份任务。  



## <a name="archive-the-backup-snapshot"></a>存档备份快照  
备份任务会在第一次运行时创建备份快照。 如果站点服务器失败，可以使用此快照来恢复它。 当备份任务按计划再次运行时，它会创建新的备份快照，该快照将覆盖以前的快照。 因此，站点只有一个备份快照，并且你无法检索以前的备份快照。  

请保留备份快照的多个存档，原因如下：  

-   备份媒体经常会出现故障、位置不正确或仅包含部分备份。 从较旧的备份恢复出现故障的独立主站点比在没有任何备份的情况下进行恢复要好。 对于层次结构中的站点服务器，备份必须处于 SQL Server 更改跟踪保持期内，否则不需要备份。  

-   对于若干备份周期，可能检测不到站点中的损坏。 可能必须使用获取自站点损坏之前的备份快照。 此原因适用于独立主站点以及层次结构中备份处于 SQL Server 更改跟踪保持期内的站点。  

-   该站点可能根本没有备份快照。 例如，如果备份站点服务器维护任务失败。 由于备份任务会在其开始备份当前数据之前删除以前的备份快照，因此将不存在有效的备份快照。  



## <a name="using-the-afterbackupbat-file"></a>使用 AfterBackup.bat 文件  
成功备份站点后，备份任务会自动尝试运行名为 AfterBackup.bat 的脚本。 在 `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box` 中的站点服务器上手动创建 AfterBackup.bat 文件。 如果 AfterBackup.bat 文件存在于正确的文件夹中，则该文件会在备份任务完成后自动运行。

AfterBackup.bat 文件可以让你在每个备份操作结束时存档备份快照。 它可以自动执行不属于备份站点服务器维护任务的其他备份后任务。 AfterBackup.bat 文件将存档和备份操作结合，从而确保将每个新备份快照存档。

如果不存在 AfterBackup.bat 文件，则备份任务会跳过该文件，并且不会对备份操作产生影响。 要验证备份任务是否成功运行了此脚本，请转到“监视”工作区的“组件状态”节点，并查看 SMS_SITE_BACKUP 的状态消息。 如果任务成功启动了 AfterBackup.bat 命令文件，则将看到消息 ID 5040。  

> [!TIP]  
>  要使用 AfterBackup.bat 存档站点服务器备份文件，必须在批处理文件中使用复制命令工具。 其中一个此类工具是 Windows Server 中的 [Robocopy ](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy)。 例如，使用以下命令创建 AfterBackup.bat 文件：`Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

尽管 AfterBackup.bat 的预期用途是将备份快照存档，但你可以创建 AfterBackup.bat 文件以在每个备份操作结束时运行其他任务。  



##  <a name="supplemental-backup-tasks"></a>补充备份任务  
备份站点服务器维护任务会为站点服务器文件和站点数据库提供备份快照。 在创建备份策略时，必须考虑其他未备份的项目。 使用这些部分来帮助完成 Configuration Manager 备份策略。  

### <a name="back-up-custom-reports"></a>备份自定义报表   
如果在 SQL Server Reporting Services 中修改预定义或创建的自定义报表，请为报表服务器数据库文件创建备份。 报表服务器备份必须包含以下组件：
- 报表和模型的源文件
- 加密密钥
- 自定义程序集或扩展
- 配置文件
- 自定义报表中使用的自定义 SQL Server 视图
- 自定义存储过程  

> [!IMPORTANT]  
>  将 Configuration Manager 升级到较新版本时，预定义的报表可能被新报表覆盖。 如果修改预定义报表，请确保备份该报表，然后在 Reporting Services 中将其还原。  

有关在 Reporting Services 中备份自定义报表的详细信息，请参阅 [Reporting Services 的备份和还原操作](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services)。  

### <a name="back-up-content-files"></a>备份内容文件  
Configuration Manager 中的内容库是存储所有软件部署的所有内容文件的位置。 内容库位于站点服务器和每个分发点上。 备份站点服务器维护任务不备份内容库或包源文件。 当站点服务器失败时，有关内容库的信息会被还原到站点数据库，但必须还原内容库和包源文件。  

-   必须还原内容库，然后才能将内容重新分发到分发点。 当开始执行内容重分发时，Configuration Manager 会将文件从站点服务器的内容库复制到分发点。 有关详细信息，请参阅[内容库](/sccm/core/plan-design/hierarchy/the-content-library)。  

-   必须还原包源文件，然后才能更新分发点上的内容。 当开始进行内容更新时，Configuration Manager 会将新文件或修改的文件从包源复制到内容库。 然后，它会将文件复制到关联的分发点。 针对站点数据库运行以下 SQL Server 查询，以查找所有包和应用程序的包源位置：`SELECT * FROM v_Package`。 你可以通过查看包 ID 的前三个字符来确定包源站点。 例如，如果包 ID 为 CEN00001，则源站点的站点代码为 CEN。 在还原包源文件时，必须将它们还原到发生故障之前所在的同一位置。  

验证是否在站点服务器的文件系统备份中包含了内容库和包源文件。  

### <a name="back-up-custom-software-updates"></a>备份自定义软件更新  
System Center Updates Publisher 是可以管理自定义软件更新的独立工具。 Updates Publisher 为其软件更新存储库使用本地数据库。 使用 Updates Publisher 管理自定义软件更新时，请确定是否应在备份计划中包括 Updates Publisher 数据库。 有关详细信息，请参阅 [System Center Updates Publisher](/sccm/sum/tools/updates-publisher)。  

使用下列过程来备份 Updates Publisher 数据库。  

#### <a name="back-up-the-updates-publisher-database"></a>备份 Updates Publisher 数据库  

1.  在运行 Updates Publisher 的计算机上，浏览到 `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` 中的 Updates Publisher 数据库文件 Scupdb.sdf。 每个运行 Updates Publisher 的用户都有不同的数据库文件。  

2.  将数据库文件复制到备份目标。 例如，如果备份目标为 `E:\ConfigMgr_Backup`，则可以将 Updates Publisher 数据库文件复制到 `E:\ConfigMgr_Backup\SCUP`。  

    > [!TIP]  
    >  如果计算机上有多个数据库文件，请考虑将文件存储在子文件夹中，该子文件夹指示与数据库文件关联的用户配置文件。 例如，可以在 `E:\ConfigMgr_Backup\SCUP\User1` 中拥有一个数据库文件，在 `E:\ConfigMgr_Backup\SCUP\User2` 中拥有另一个数据库文件。  



## <a name="user-state-migration-data"></a>用户状态迁移数据  
可以使用 Configuration Manager 任务序列捕获和还原 OS 部署方案中的用户状态数据。 状态迁移点的属性列出存储用户状态数据的文件夹。 此数据不作为站点服务器备份维护任务的一部分进行备份。 作为备份计划的一部分，你必须手动备份指定用于存储用户状态迁移数据的文件夹。   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>确定用于存储用户状态迁移数据的文件夹  

1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“服务器和站点系统角色”节点。  

2.  选择托管状态迁移角色的站点系统。 然后在“站点系统角色”窗格中选择“状态迁移点”。  

3.  单击功能区中的“属性”。  

4.  “常规”选项卡上的“文件夹详细信息”部分中列出了存储用户状态迁移数据的文件夹。  



## <a name="about-the-sms-writer-service"></a>关于 SMS 编写器服务  
SMS 编写器是一项在备份过程中与 Windows 卷影复制服务 (VSS) 进行交互的服务。 SMS 编写器服务必须正在运行，Configuration Manager 站点备份才能成功完成。  

### <a name="process"></a>过程  
1. SMS 编写器向 VSS 服务注册，并绑定到其接口和事件。 
2. 当 VSS 广播事件时，或者，如果它将特定通知发送到 SMS 编写器，SMS 编写器将响应通知并执行适当的操作。 
3. SMS 编写器会读取位于 `<ConfigMgrInstallationPath>\inboxes\smsbkup.box` 中的备份控制文件 smsbkup.ctl，并确定要备份的文件和数据。 
4. SMS 编写器会构建由各种组件组成的元数据，这些组件包括 SMS 注册表项和子项中的特定数据。 
    a. 当请求元数据时，它会将元数据发送到 VSS。 
    b. 然后，VSS 会将元数据发送到发出请求的应用程序，即 Configuration Manager 备份管理器。 
5. 备份管理器选择要备份的数据并通过 VSS 将此数据发送到 SMS 编写器。 
6. SMS 编写器执行适当的步骤来为备份做好准备。 
7. 之后，当 VSS 准备获取快照时：a. 它发送一个事件 b. SMS 编写器停止所有 Configuration Manager 服务 c. 它确保在创建快照时已冻结 Configuration Manager 活动。 
8. 完成快照后，SMS 编写器重启服务和活动。

将自动安装 SMS 编写器服务。 当 VSS 应用程序请求备份或还原时，该服务必须正在运行。  

### <a name="writer-id"></a>编写器 ID  
SMS 编写器的编写器 ID 为：03ba67dd-dc6d-4729-a038-251f7018463b。  

### <a name="permissions"></a>权限  
SMS 编写器服务必须采用本地系统帐户运行。  

### <a name="volume-shadow-copy-service"></a>卷影复制服务  
VSS 是一组 COM API，它实现一个框架，以允许在系统上的应用程序继续写入卷时执行所有卷备份。 VSS 提供一个一致的接口，在用于更新磁盘上的数据的用户应用程序（SMS 编写器服务）和用于备份应用程序的用户应用程序（备份管理器服务）之间实现协作。 有关详细信息，请参阅[卷影复制服务](https://go.microsoft.com/fwlink/p/?LinkId=241968)。  



## <a name="next-steps"></a>后续步骤
创建备份后，使用该备份练习[站点恢复](/sccm/protect/understand/recover-sites)。 此练习可以帮助你在需要依赖它之前熟悉恢复过程。 它还可以帮助确认备份是否成功用于其预期用途。  
