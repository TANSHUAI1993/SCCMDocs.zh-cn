---
title: "站点恢复 | Microsoft Docs"
description: "了解如何恢复 System Center Configuration Manager 站点。"
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 49eea15ea2888f8f93c33eb771c09147ba21529e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="recover-a-configuration-manager-site"></a>恢复 Configuration Manager 站点

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 站点出现故障或者站点数据库中发生数据丢失后，请运行 Configuration Manager 站点恢复。 修复和重新同步数据是站点恢复的核心任务，并且是防止操作中断所必需的。

此主题中的各节可帮助你恢复 Configuration Manager 站点。 要创建备份，请参阅 [Configuration Manager 备份](/sccm/protect/understand/backup-and-recovery)。

## <a name="considerations-before-recovering-a-site"></a>恢复站点前的注意事项
**必须使用相同版本的 SQL Server：**例如，不支持将 SQL Server 2014 上运行的数据库还原到 SQL Server 2016。 同样，也不支持还原在 SQL Server 2016 标准版和 SQL Server 2016 企业版上运行的站点数据库。
-   不能将 SQL Server 设置为 **单用户模式**。
-   确保 .MDF 和 .LDF 文件有效。 恢复站点时，不会对正在还原的文件的状态进行检查。

**如果使用 SQL Server AlwaysOn 可用性组来托管站点数据库：**按照[准备使用 SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery) 中所述修改恢复计划。

**使用数据库副本时：**还原为数据库副本配置的站点数据库之后，必须重新配置每个数据库副本（从而重新创建发布和订阅），然后才能使用数据库副本。

## <a name="determine-your-recovery-options"></a>确定恢复选项
为 Configuration Manager 主站点服务器和管理中心站点恢复考虑两个主要方面；即站点服务器和站点数据库。
以下部分可帮助你选择用于恢复方案的最佳选项。

> [!NOTE]   
> 如果安装程序检测到服务器上的现有 Configuration Manager 站点，可以启动站点恢复，但适用于站点服务器的恢复选项有限。 例如，如果在现有站点服务器上运行安装程序，则在选择恢复时，你可以恢复站点数据库服务器，但用于恢复站点服务器的选项则处于禁用状态。

### <a name="site-server-recovery-options"></a>站点服务器恢复选项
从 Configuration Manager 安装文件夹之外创建的 CD.Latest 文件夹副本中启动安装程序。
-   如果从站点服务器上的“开始”菜单中运行 Configuration Manager 安装程序，则“恢复站点”选项不可用。
-   如果在进行备份之前，从 Configuration Manager 控制台内安装了任何更新，则无法通过从安装媒体或从 Configuration Manager 安装路径中使用安装程序来成功重装该站点。

然后选择“恢复站点”选项。 可以为出现故障的站点服务器使用下列恢复选项：

-   **使用现有备份恢复站点服务器**：如果具有在站点出现故障之前作为“备份站点服务器”维护任务的一部分在站点服务器上创建的 Configuration Manager 站点服务器的备份，请使用此选项。 将重新安装站点，并基于备份的站点配置站点设置。
-   **重新安装站点服务器**：在没有站点服务器的备份时使用此选项。 将重新安装站点服务器，并且你必须指定站点设置，就像在初始安装过程中指定这些设置一样。
  -   必须使用在第一次安装出现故障的站点时所使用的相同站点代码和站点数据库名称。
  -   可以在运行新操作系统的新计算机上重新安装站点。
  -   计算机必须使用与原始站点服务器相同的名称和 FQDN。   

### <a name="site-database-recovery-options"></a>站点数据库恢复选项
在运行安装程序时，你可以为站点数据库使用下列恢复选项：
-   **使用备份集恢复站点数据库：**如果具有在站点数据库出现故障之前，作为站点上所运行“备份站点服务器”维护任务的一部分创建的 Configuration Manager 站点数据库的备份，请使用此选项。 如果你具有层次结构，则会从主站点的管理中心站点或管理中心站点的引用主站点中检索在上次站点数据库备份之后对站点数据库所做的更改。 当你恢复独立主站点的站点数据库时，将会丢失上次备份之后所做的站点更改。

   如果为层次结构中的站点恢复站点数据库，则管理中心站点与主站点的恢复行为不同，并且当上次备份在 SQL Server 更改跟踪保持期之内或之外时，恢复行为也不同。 有关详细信息，请参阅本主题中的 [站点数据库恢复方案](##site-database-recovery-scenarios) 部分。
  > [!NOTE]   
  > 如果选择使用备份集还原站点数据库，但站点数据库已经存在，则恢复将失败。  

-   **为此站点创建新数据库：**在没有 Configuration Manager 站点数据库的备份时使用此选项。 如果你具有层次结构，系统会创建一个新站点数据库，并使用主站点的管理中心站点或管理中心站点的引用主站点中的复制数据恢复数据。 当你恢复独立主站点或没有主站点的管理中心站点时，此选项不可用。

-   **使用已手动恢复的站点数据库：**当已经恢复 Configuration Manager 站点数据库但必须完成恢复过程时，使用此选项。
    -   Configuration Manager 可以从 Configuration Manager 备份维护任务或从使用 DPM 或另一个进程执行的站点数据库备份中恢复站点数据库。 在 Configuration Manager 之外使用某种方法还原站点数据库之后，必须运行安装程序并选择此选项以完成站点数据库恢复。

    > [!NOTE]   
    > 如果使用 DPM 备份站点数据库，请使用 DPM 过程将站点数据库还原到指定位置，然后继续在 Configuration Manager 中进行还原过程。 有关 DPM 的详细信息，请参阅 TechNet 上的 [Data Protection Manager Documentation Library（Data Protection Manager 文档库）]() 。    

    -   如果你具有层次结构，则会从主站点的管理中心站点或管理中心站点的引用主站点中检索在上次站点数据库备份之后对站点数据库所做的更改。 当你恢复独立主站点的站点数据库时，将会丢失上次备份之后所做的站点更改。     


-   **跳过数据库恢复：**当 Configuration Manager 站点数据库服务器上未发生数据丢失时使用此选项。 仅当站点数据库所在的计算机不同于你正在恢复的站点服务器时，此选项才有效。

### <a name="sql-server-change-tracking-retention-period"></a>SQL Server 更改跟踪保持期
系统为 SQL Server 中的站点数据库启用了更改跟踪。 利用更改跟踪，Configuration Manager 可以查询有关在上一个时刻之后对数据库表所做的更改的信息。 保持期指定更改跟踪信息将保留多长时间。 默认情况下，站点数据库被配置为具有 5 天保持期。 恢复站点数据库时，恢复过程在备份处于保持期内或保持期外这两种情况下会以不同方式继续进行。 例如，你的站点数据库服务器出现故障，并且上次备份是在 7 天之前，则它在保持期之外。

有关 SQL Server 更改跟踪内部机制的详细信息，请参阅以下 SQL Server 团队博客：[Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/)（更改跟踪清除 - 第 1 部分）和 [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2)（更改跟踪清除 - 第 2 部分）。

### <a name="reinitialization-of-site-or-global-data"></a>重新初始化站点或全局数据
重新初始化站点或全局数据的过程将站点数据库中的现有数据替换为另一个站点数据库中的数据。 例如，当站点 ABC 重新初始化站点 XYZ 中的数据时，会进行以下步骤：
-   将数据从站点 XYZ 复制到站点 ABC。
-   从站点 ABC 上的站点数据库中删除站点 XYZ 的现有数据。
-   将站点 XYZ 中的已复制数据插入到站点 ABC 的站点数据库中。

#### <a name="example-scenario-1"></a>示例方案 1
**主站点重新初始化管理中心站点中的全局数据：**恢复过程删除主站点数据库中主站点的现有全局数据，并将数据替换为从管理中心站点中复制的全局数据。

#### <a name="example-scenario-2"></a>示例方案 2
**管理中心站点重新初始化主站点中的站点数据：**恢复过程删除管理中心站点数据库中该主站点的现有站点数据，并将数据替换为从主站点中复制的站点数据。 其他主站点的站点数据不受影响。

### <a name="site-database-recovery-scenarios"></a>站点数据库恢复方案
从备份中还原站点数据库之后，Configuration Manager 会尝试还原上次数据库备份之后在站点和全局数据中所做的更改。 下面描述了从备份中还原站点数据库之后 Configuration Manager 启动的操作。

**恢复的站点是管理中心站点：**
-   **更改跟踪保持期内的数据库备份**
    -   **全局数据：** 从所有主站点中复制备份之后，全局数据中所做的更改。
    -   **站点数据：** 从所有主站点中复制备份之后，站点数据中所做的更改。


-   **更改跟踪保持期之前的数据库备份**
    -   全局数据：如果指定引用主站点，则管理中心站点会重新初始化引用主站点中的全局数据。 然后，所有其他主站点会重新初始化管理中心站点中的全局数据。 如果未指定引用站点，则所有主站点会重新初始化管理中心站点中的全局数据（从备份中还原的数据）。
    -   **站点数据：** 管理中心站点重新初始化每个主站点中的站点数据。


**恢复的站点是主站点：**
-   **更改跟踪保持期内的数据库备份**
    -   **全局数据：** 从管理中心站点中复制备份之后，全局数据中所做的更改。
    -   **站点数据：** 管理中心站点重新初始化主站点中的站点数据。 备份之后的更改将会丢失，但将信息发送到主站点的客户端会重新生成大部分数据。


-   **更改跟踪保持期之前的数据库备份**
    -   **全局数据：** 主站点重新初始化管理中心站点中的全局数据。
    -   **站点数据：** 管理中心站点重新初始化主站点中的站点数据。 备份之后的更改将会丢失，但将信息发送到主站点的客户端会重新生成大部分数据。

## <a name="site-recovery-procedures"></a>站点恢复过程
使用以下过程之一来帮助恢复站点服务器和站点数据库。

### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>在安装向导中启动站点恢复
1.  将 [CD.Latest](/sccm/core/servers/manage/the-cd.latest-folde) 文件夹复制到 Configuration Manager 安装文件夹之外的位置。
从 CD.Latest 文件夹的副本中，运行 Configuration Manager 安装向导。

2.  在“入门”  页上，选择“恢复站点” ，然后单击“下一步” 。

3.  使用适合你的站点恢复的选项完成向导。

  -   在恢复过程中，安装程序会标识 SQL Server 所使用的 SQL Server Service Broker (SSB) 端口。 请勿在恢复过程中更改此端口设置，否则在恢复完成之后数据复制将不会正常工作。

  -   可以在安装向导中指定要用于 Configuration Manager 安装的原始路径或新路径。

### <a name="to-start-an-unattended-site-recovery"></a>启动无人参与的站点恢复
  1.    针对站点恢复所需要的选项准备无人参与安装脚本。  请参阅[无人参与的站点恢复脚本文件密钥](/sccm/protect/understand/unattended-site-recovery-script-file-keys)。

  2.    使用命令 **/script** 选项运行 Configuration Manager 安装程序。 例如，你将安装程序初始化文件命名为 ConfigMgrUnattend.ini 并且将其保存在运行安装程序的计算机上的 C:\Temp 目录中，那么命令将如下所示： **Setup /script C:\temp\ConfigMgrUnattend.ini**。

  > [!NOTE]   
  >  恢复管理中心站点后，可能无法建立某些来自子站点的站点数据的副本。 这可能包括硬件清单、软件清单和状态消息。
  >
  >  如果发生这种情况，必须重新初始化 **ConfigMgrDRSSiteQueue** 才能进行数据库复制。  为此，请在管理中心站点上的 Configuration Manager 站点数据库上使用 **SQL Server Manager** 运行以下查询：
  >
  >  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**
  >
  >  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**


## <a name="post-recovery-tasks"></a>恢复后任务
恢复站点之后，有一些你必须在站点恢复完成之前考虑的恢复后任务。 使用下列部分来帮助你完成站点恢复过程。

### <a name="re-enter-user-account-passwords"></a>重新输入用户帐户密码
在站点服务器恢复之后，必须重新输入为站点指定的用户帐户的密码，因为这些密码在站点恢复过程中已重置。 在站点恢复完成后，这些帐户列在安装向导的“已完成”  页上，并保存到恢复的站点服务器上的 C:\ConfigMgrPostRecoveryActions.html。

#### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>在站点恢复后重新输入用户帐户密码

1.  打开 Configuration Manager 控制台并连接到恢复的站点。

2.  在 Configuration Manager 控制台中，单击“管理” 。

3.  在“管理”  工作区中，展开“安全” ，然后单击“帐户” 。

4.  对于你重新输入密码的每个帐户，请执行下列操作：

    1.  从站点恢复后确定的帐户的列表中选择帐户。 你可以在恢复的站点服务器上的 C:\ConfigMgrPostRecoveryActions.html 中找到此列表。

    2.  在“主页”  选项卡上的“属性”  组中，单击“属性”  以打开帐户属性。

    3.  在“常规”  选项卡上，单击“设置” ，然后为帐户重新输入密码。

    4.  单击“验证” ，为所选用户帐户选择适当的数据源，然后单击“测试连接”  以验证该用户帐户是否可连接到数据源。

    5.  单击“确定”  保存密码更改，然后单击“确定” 。

### <a name="re-enter-sideloading-keys"></a>重新输入旁加载密钥
在站点服务器恢复之后，必须重新输入为站点指定的 Windows 旁加载密钥，因为这些密钥在站点恢复过程中已重置。 重新输入旁加载密钥后，将在 Configuration Manager 控制台中重置 Windows 旁加载密钥的“已使用激活数”列中的计数。 例如，假设在站点失败之前，针对设备已经使用的密钥数将“激活总数”计数设置为“100”，将“已使用激活数”设置为“90”。 在站点恢复之后，“激活总数”  列仍显示“100” ，但“已使用激活数”  列错误地显示“0” 。 然而，在 10 个新设备使用旁加载密钥之后，将没有剩余的旁加载密钥，下一个设备将无法应用旁加载密钥。

### <a name="recreate-the-microsoft-intune-subscription"></a>重新创建 Microsoft Intune 订阅
 如果在重新制作站点服务器计算机的映像后恢复 Configuration Manager 站点服务器，将不会还原 Microsoft Intune 订阅。 恢复站点后必须重新连接订阅。  不要创建新的 APN 要求，而改为上传当前有效的 .pem 文件，此文件在上一次配置或续订 iOS 管理时上传。 有关详细信息，请参阅 [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription)。

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>为使用 IIS 的站点系统角色配置 SSL
当你恢复运行 IIS 并且在发生故障之前针对 HTTPS 进行了配置的站点系统时，你必须重新配置 IIS 以使用 Web 服务器证书。

### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>在恢复的站点服务器中重新安装修补程序
站点恢复之后，你必须重新安装之前应用于站点服务器的任何修补程序。 站点恢复后在安装向导的“已完成”页上查看以前安装的修补程序列表。 此列表还保存到恢复的站点服务器上的 C:\ConfigMgrPostRecoveryActions.html。

### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>在运行 Reporting Services 的计算机上恢复自定义报表
如果创建了自定义 Reporting Services 报表，并且 Reporting Services 失败，则可以在备份了报表服务器时恢复报表。 有关在 Reporting Services 中还原自定义报表的详细信息，请参阅 SQL Server 2008 联机丛书中的 [Reporting Services 安装的备份和还原操作](http://go.microsoft.com/fwlink/p/?LinkId=228724) 。

### <a name="recover-content-files"></a>恢复内容文件
 站点数据库包含有关内容文件在站点服务器上的存储位置的信息，但在备份和恢复过程中不会备份或还原内容文件。 要完全恢复内容文件，你必须将内容库和包源文件还原到原始位置。 有很多用于恢复内容文件的方法，但最简单的方法是从站点服务器的文件系统备份中还原文件。

 如果没有包源文件的文件系统备份，必须按照最初创建包时的方式手动复制或下载这些文件。 你可以在 SQL Server 中运行以下查询来查找所有包和应用程序的包源位置： `SELECT * FROM v_Package`。 你可以通过查看包 ID 的前三个字符来确定包源站点。 例如，如果包 ID 为 CEN00001，则源站点的站点代码为 CEN。 在还原包源文件时，必须将它们还原到发生故障之前所在的同一位置。

 如果没有包含内容库的文件系统备份，则有下列还原选项：

-   **导入预安排内容文件**：如果有 Configuration Manager 层次结构，可以创建包含另一个位置中的所有包和应用程序的预安排内容文件，然后导入该预安排内容文件以在站点服务器上恢复内容库。

-   **更新内容**：当你为包或应用程序部署类型启动更新内容操作时，会将内容从包源复制到内容库。 原始位置中必须有包源文件，此操作才能成功完成。 你必须对每个包和应用程序执行此操作。

### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>在运行 Updates Publisher 的计算机上恢复自定义软件更新
如果在备份计划中包括了 Updates Publisher 数据库文件，可以在运行 Updates Publisher 的计算机发生故障时恢复数据库。 有关 Updates Publisher 的详细信息，请参阅 System Center TechCenter 库中的 [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) 。

使用下列过程来还原 Updates Publisher 数据库。

#### <a name="to-restore-the-updates-publisher-2011-database"></a>还原 Updates Publisher 2011 数据库
1.  在恢复的计算机上重新安装 Updates Publisher。

2.  将数据库文件 (Scupdb.sdf) 从备份目标复制到运行 Updates Publisher 的计算机上的 %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ 中。

3.  如果有多个用户在计算机上运行 Updates Publisher，则必须将每个数据库文件复制到相应的用户配置文件位置。

### <a name="user-state-migration-data"></a>用户状态迁移数据
作为状态迁移点站点系统属性的一部分，要指定存储用户状态迁移数据的文件夹。 在恢复带有此类文件夹（存储了用户状态迁移数据）的服务器之后，必须手动将该服务器上的用户状态迁移数据还原到在失败前存储此数据的相同文件夹中。

### <a name="regenerate-the-certificates-for-distribution-points"></a>重新生成分发点的证书
还原站点后，distmgr.log 可能包含一个或多个分发点的以下条目： **无法解密证书 PFX 数据**。 此条目表示站点无法解密分发点证书数据。 为了解决这一问题，必须重新生成或重新导入受影响分发点的证书。 此过程可使用 [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) PowerShell cmdlet 完成。

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>更新用于基于云的分发点的证书
 Configuration Manager 需要使用管理证书来执行从站点服务器到基于云的分发点的通信。 在站点恢复之后，必须为基于云的分发点更新证书。

## <a name="recover-a-secondary-site"></a>恢复辅助站点
 Configuration Manager 不支持在辅助站点上进行数据库备份，但支持通过重新安装辅助站点进行恢复。 在 Configuration Manager 辅助站点失败时，必须恢复辅助站点。

### <a name="requirements-for-reinstalling-a-secondary-site"></a>重新安装辅助站点的要求
-   计算机必须满足辅助站点的所有先决条件，而且具有适当的安全权限配置。
-   必须使用失败的站点所用的相同安装路径。
-   必须使用在配置上与失败的计算机相同（例如使用其 FQDN）的计算机才能成功恢复辅助站点。
-   计算机必须具有与出现故障的站点相同的 SQL Server 配置。
  -   在恢复辅助站点的过程中，如果计算机上尚未安装 SQL Server Express，则 Configuration Manager 并不会安装它。
  -   必须使用在失败前用于辅助站点数据库的同一个 SQL Server 版本和同一个 SQL Server 实例。

### <a name="to-recover-a-secondary-site"></a>恢复辅助站点：
若要恢复辅助站点，请在 Configuration Manager 控制台的“站点”节点中使用“恢复辅助站点”操作。 与恢复管理中心站点或主站点不同的是，恢复辅助站点不使用备份文件，而是在失败的辅助站点计算机上重新安装辅助站点文件。 站点重新安装后，使用父主站点中的数据重新初始化辅助站点数据。

在恢复过程中，Configuration Manager 会验证辅助站点计算机上是否存在内容库，以及合适的内容是否可用。 如果辅助站点包含合适的内容，则它将使用现有的内容库。 否则，若要恢复已恢复辅助站点的内容库，则需将内容重新分发或预留到该已恢复站点。

如果拥有不在辅助站点上的分发点，则无需在恢复辅助站点的过程中重新安装分发点。 在恢复辅助站点之后，站点会自动与分发点同步。

可以在 Configuration Manager 控制台的“站点”节点中使用“显示安装状态”操作来验证辅助站点恢复的状态。
