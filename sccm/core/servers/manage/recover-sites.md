---
title: 站点恢复
titleSuffix: Configuration Manager
description: 了解如何恢复 Configuration Manager 站点。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c8a55ec24a70e6059bb638d1d7ddfc7651574055
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134361"
---
#  <a name="recover-a-configuration-manager-site"></a>恢复 Configuration Manager 站点

适用范围：*System Center Configuration Manager (Current Branch)*

站点出现故障或者站点数据库中发生数据丢失后，请运行 Configuration Manager 站点恢复。 修复和重新同步数据是站点恢复的核心任务，并且是防止操作中断所必需的。

本文中的各节可帮助恢复 Configuration Manager 站点。 要创建备份，请参阅 [Configuration Manager 备份](/sccm/core/servers/manage/backup-and-recovery)。



## <a name="considerations-before-recovering-a-site"></a>恢复站点前的注意事项

> [!Important]  
> 此信息仅适用于站点恢复方案。 在升级本地基础结构且未主动恢复故障站点时，请查看以下文章中的信息：
> - [升级本地基础结构](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> - [修改基础结构](/sccm/core/servers/manage/modify-your-infrastructure)


#### <a name="use-the-same-version-and-edition-of-sql-server"></a>使用相同版本的 SQL Server   
例如，不支持将数据库从 SQL Server 2014 还原到 SQL Server 2016。 同样，不支持将 SQL Server 2016 站点数据库从标准版还原到企业版。
- 不能将 SQL Server 设置为“单用户模式”。
- 确保 .MDF 和 .LDF 文件有效。 恢复站点时，不会检查文件的状态。  

#### <a name="sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性组   
如果使用 SQL Server Always On 可用性组来托管站点数据库，请按照[准备使用 SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery) 中所述修改恢复计划。

#### <a name="database-replicas"></a>数据库副本  
在还原为数据库副本配置的站点数据库后，请重新配置每个副本。 在使用数据库副本之前，请重新创建发布和订阅。



## <a name="determine-your-recovery-options"></a>确定恢复选项

为 Configuration Manager 主站点服务器和管理中心站点恢复考虑两个主要方面：站点服务器和站点数据库。
以下部分可帮助你选择用于恢复方案的最佳选项。

> [!NOTE]   
> 如果 Configuration Manager 安装程序检测到服务器上的现有站点，可以启动站点恢复，但适用于站点服务器的恢复选项有限。 例如，如果在现有站点服务器上运行安装程序，则在选择恢复时，你可以恢复站点数据库服务器，但用于恢复站点服务器的选项则处于禁用状态。


### <a name="site-server-recovery-options"></a>站点服务器恢复选项

从 Configuration Manager 安装文件夹之外创建的 CD.Latest 文件夹副本中启动 Configuration Manager 安装程序。  

-   如果从站点服务器上的“开始” 菜单中运行安装程序，则“恢复站点”选项不可用。  

-   如果在进行备份之前从 Configuration Manager 控制台中安装了任何更新，则无法使用以下位置中的安装程序重新安装站点： 
    - 安装介质
    - Configuration Manager 安装路径 

然后选择“恢复站点”选项。 可以为出现故障的站点服务器使用下列恢复选项：  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>使用现有备份恢复站点服务器
如果在站点发生故障之前便拥有站点服务器的 Configuration Manager 备份，请使用此选项。 该站点创建此备份作为备份站点服务器维护任务的一部分。 站点会重新安装，并且站点设置会根据备份的站点进行配置。  

#### <a name="reinstall-the-site-server"></a>重新安装站点服务器
如果没有站点服务器的备份，则使用此选项。 站点服务器会重新安装，并且必须像初始安装期间一样指定站点设置。  

-   使用首次安装失败站点时所使用的同一站点代码和站点数据库名称。  

-   可以在运行新 OS 版本的新计算机上重新安装站点。  

-   服务器必须使用原始站点服务器的相同主机名和完全限定的域名 (FQDN)。   


### <a name="site-database-recovery-options"></a>站点数据库恢复选项

在运行 Configuration Manager 安装程序时，可以为站点数据库使用下列恢复选项：  

#### <a name="recover-the-site-database-using-a-backup-set"></a>使用备份集恢复站点数据库
如果在数据库发生故障之前便拥有站点数据库的 Configuration Manager 备份，请使用此选项。 该站点创建此备份作为备份站点服务器维护任务的一部分。 在层次结构中，还原主站点时，恢复过程会从管理中心站点检索上次备份后对站点数据库所做的任何更改。 还原管理中心站点时，恢复过程会从引用主站点检索这些更改。 恢复独立主站点的站点数据库时，将会丢失上次备份之后所做的站点更改。  

在层次结构中恢复站点的站点数据库时，管理中心站点和主站点的恢复行为有所不同。 上次备份在 SQL Server 更改跟踪保持期之内或之外时的行为也会不同。 有关详细信息，请参阅本文中的[站点数据库恢复方案](#site-database-recovery-scenarios)部分。  

> [!NOTE]   
> 如果选择使用备份集还原站点数据库，但站点数据库已经存在，则恢复将失败。   

#### <a name="create-a-new-database-for-this-site"></a>为此站点创建新数据库
如果没有站点数据库的备份，则使用此选项。 在层次结构中，恢复过程会创建新的站点数据库。 还原子级主站点时，它通过从管理中心站点进行复制来恢复数据。 还原管理中心站点时，它会从引用主站点复制数据。 在恢复独立主站点或没有主站点的管理中心站点时，此选项不可用。  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>使用已手动恢复的站点数据库
已经恢复 Configuration Manager 站点数据库但需要完成恢复过程时，请使用此选项。  

- Configuration Manager 可以从以下任何进程恢复站点数据库：  

  - Configuration Manager 备份维护任务  
  - 使用 Data Protection Manager (DPM) 进行站点数据库备份  
  - 另一备份过程   

    在 Configuration Manager 之外使用某种方法还原站点数据库之后，运行安装程序并选择此选项以完成站点数据库恢复。  

    > [!NOTE]   
    > 如果使用 DPM 备份站点数据库，请使用 DPM 过程将站点数据库还原到指定位置，然后继续在 Configuration Manager 中进行还原过程。 有关 DPM 的详细信息，请参阅 [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) 文档库。    

- 在层次结构中，还原主站点数据库时，恢复过程会从管理中心站点检索上次备份后对站点数据库所做的任何更改。 还原管理中心站点时，恢复过程会从引用主站点检索这些更改。 恢复独立主站点的站点数据库时，将会丢失上次备份之后所做的站点更改。   

#### <a name="skip-database-recovery"></a>跳过数据库恢复
当 Configuration Manager 站点数据库服务器上未发生数据丢失时使用此选项。 仅当站点数据库与正在恢复的站点服务器位于不同计算机上时，此选项才有效。  


### <a name="sql-server-change-tracking-retention-period"></a>SQL Server 更改跟踪保持期

Configuration Manager 为 SQL Server 中的站点数据库启用更改跟踪。 利用更改跟踪，Configuration Manager 可以查询有关在上一个时间点之后对数据库表所做的更改的信息。 保持期指定更改跟踪信息将保留多长时间。 默认情况下，站点数据库被配置为具有 5 天保持期。 恢复站点数据库时，恢复过程在备份处于保持期内或保持期外这两种情况下会以不同方式继续进行。 例如，如果 SQL 服务器出现故障，并且上次备份是在 7 天之前，则它不在保持期范围内。

有关 SQL Server 更改跟踪内部机制的详细信息，请参阅以下 SQL Server 团队的博客文章：[Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/)（更改跟踪清除 - 第 1 部分）和 [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2)（更改跟踪清除 - 第 2 部分）。


### <a name="reinitialization-of-site-or-global-data"></a>重新初始化站点或全局数据

重新初始化站点或全局数据的过程将站点数据库中的现有数据替换为另一个站点数据库中的数据。 例如，当站点 ABC 重新初始化站点 XYZ 中的数据时，会进行以下步骤：
- 将数据从站点 XYZ 复制到站点 ABC。
- 从站点 ABC 上的站点数据库中删除站点 XYZ 的现有数据。
- 将站点 XYZ 中的已复制数据插入到站点 ABC 的站点数据库中。

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-central-administration-site"></a>示例方案 1：主站点重新初始化管理中心站点中的全局数据  
恢复过程删除主站点数据库中主站点的现有全局数据，并将数据替换为从管理中心站点中复制的全局数据。

#### <a name="example-scenario-2-the-central-administration-site-reinitializes-the-site-data-from-a-primary-site"></a>示例方案 2：管理中心站点重新初始化主站点中的站点数据 
恢复过程会删除管理中心站点数据库中该主站点的现有站点数据。 它将数据替换为从主站点中复制的站点数据。 其他主站点的站点数据不受影响。


### <a name="site-database-recovery-scenarios"></a>站点数据库恢复方案

从备份中还原站点数据库之后，Configuration Manager 会尝试还原上次数据库备份之后在站点和全局数据中所做的更改。 从备份中还原站点数据库之后，Configuration Manager 会启动以下操作：  

#### <a name="recovered-site-is-a-central-administration-site"></a>恢复的站点是管理中心站点
- 更改跟踪保持期内的数据库备份  

     - **全局数据**：系统从所有主站点中复制备份之后在全局数据中所做的更改。  

     - **站点数据**：系统从所有主站点中复制备份之后在站点数据中所做的更改。  

- 更改跟踪保持期之前的数据库备份  

     - **全局数据**：如果指定了引用主站点，则管理中心站点会重新初始化引用主站点中的全局数据。 然后，所有其他主站点会重新初始化管理中心站点中的全局数据。 如果未指定引用站点，则所有主站点都会从管理中心站点重新初始化全局数据。 此数据是从备份还原的数据。  

     - **站点数据**：管理中心站点重新初始化每个主站点中的站点数据。  

#### <a name="recovered-site-is-a-primary-site"></a>恢复的站点是主站点
- 更改跟踪保持期内的数据库备份  

     - **全局数据**：系统从管理中心站点中复制备份之后在全局数据中所做的更改。  

     - **站点数据**：管理中心站点重新初始化主站点中的站点数据。 备份后所做的更改会丢失。 客户端在向主站点发送信息时会重新生成大部分数据。  

- 更改跟踪保持期之前的数据库备份  
     - **全局数据**：主站点重新初始化管理中心站点中的全局数据。  

     - **站点数据**：管理中心站点重新初始化主站点中的站点数据。 备份后所做的更改会丢失。 客户端在向主站点发送信息时会重新生成大部分数据。  



## <a name="site-recovery-procedures"></a>站点恢复过程

使用以下过程之一来帮助恢复站点服务器和站点数据库：


### <a name="start-a-site-recovery-in-the-setup-wizard"></a>在安装向导中启动站点恢复

1.  将 [CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) 文件夹复制到 Configuration Manager 安装文件夹之外的位置。 从 CD.Latest 文件夹的副本中，运行 Configuration Manager 安装向导。  

2.  在“入门”  页上，选择“恢复站点” ，然后单击“下一步” 。  

3.  使用适合你的站点恢复的选项完成向导。  

     - 在恢复过程中，安装程序会标识 SQL Server 所使用的 SQL Server Service Broker (SSB) 端口。 请勿在恢复过程中更改此端口设置，否则在恢复完成之后数据复制将不会正常工作。  

     - 可以在安装向导中指定要用于 Configuration Manager 安装的原始路径或新路径。  


### <a name="start-an-unattended-site-recovery"></a>启动无人参与的站点恢复

1. 针对站点恢复所需要的选项准备无人参与安装脚本。 有关详细信息，请参阅[无人参与的站点恢复](/sccm/core/servers/manage/unattended-recovery)。  

2. 使用 `/script` 命令行选项运行 Configuration Manager 安装程序。 例如，创建一个安装程序初始化文件 ConfigMgrUnattend.ini。 将其保存在运行安装程序的计算机的 `C:\Temp` 目录中。 请使用以下命令：  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  


> [!NOTE]   
>  恢复管理中心站点后，可能无法建立某些来自子站点的站点数据的副本。 此数据可能包括硬件清单、软件清单和状态消息。
>
>  如果发生此问题，则重新初始化 ConfigMgrDRSSiteQueue 以进行数据库复制。 针对管理中心站点的站点数据库，使用 SQL 服务器管理器运行以下查询：
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```



## <a name="post-recovery-tasks"></a>恢复后任务

恢复站点之后，需要在完成站点恢复之前考虑几个恢复后任务。 使用下列部分来帮助你完成站点恢复过程。


### <a name="reenter-user-account-passwords"></a>重新输入用户帐户密码

执行站点服务器恢复后，重新输入站点中任何用户帐户的密码。 这些密码在站点恢复期间重置。 站点恢复完成后，帐户将在安装向导的已“完成”页面上列出。 该列表还会保存到已恢复的站点服务器上的 `C:\ConfigMgrPostRecoveryActions.html` 中。

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>在站点恢复后重新输入用户帐户密码
1. 打开 Configuration Manager 控制台并连接到恢复的站点。  

2. 转到“管理”工作区，展开“安全”，然后单击“帐户”。  

3. 对于每个帐户，请执行以下步骤以重新输入密码：  

     1. 从站点恢复后确定的列表中选择帐户。  

     2. 单击功能区中的“属性”。  

     3. 在“常规”选项卡上，单击“设置”，然后重新输入帐户密码。  

     4. 单击“验证”，为所选用户帐户选择适当的数据源，然后单击“测试连接”。 此步骤测试用户帐户是否可以连接到数据源，并验证凭据。  

     5. 单击“确定”保存密码更改，然后单击“确定”关闭帐户属性页面。  


### <a name="reenter-sideloading-keys"></a>重新输入旁加载密钥

执行站点服务器恢复后，重新输入为站点指定的 Windows 旁加载密钥。 这些密钥会在站点恢复期间重置。 重新输入旁加载密钥后，站点会重置 Windows 旁加载密钥的“已使用激活数”列中的计数。 

例如，在站点发生故障之前，“激活总数”显示为“100”。 设备已使用的密钥数或“已使用激活数”为“90”。 在站点恢复之后，“激活总数”列仍显示“100”，但“已使用激活数”列错误地显示“0”。 在 10 个新设备使用旁加载密钥之后，不会再有更多的旁加载密钥且第 11 个设备将无法应用旁加载密钥。


### <a name="recreate-the-microsoft-intune-subscription"></a>重新创建 Microsoft Intune 订阅

如果在站点服务器重置映像后恢复 Configuration Manager 站点服务器，将不会还原 Microsoft Intune 订阅。 恢复站点后重新连接订阅。 不要创建新的 APN 请求。 而是上传当前有效的 PEM 文件。 使用上次配置或续订 iOS 管理时上传的相同文件。 有关详细信息，请参阅 [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription)。


### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>为使用 IIS 的站点系统角色配置 SSL

当恢复运行 IIS 的站点系统并且已对 HTTPS 进行了配置时，请重新配置 IIS 以使用 Web 服务器证书。


### <a name="reinstall-hotfixes"></a>重新安装修补程序 

站点恢复之后，你必须重新安装之前应用于站点服务器的任何修补程序。 站点恢复后，在安装向导的“已完成”页上查看以前安装的修补程序列表。 该列表还会保存到已恢复的站点服务器上的 `C:\ConfigMgrPostRecoveryActions.html` 中。


### <a name="recover-custom-reports"></a>恢复自定义报表 

某些客户在 SQL Server Reporting Services 中创建自定义报表。 当此组件发生故障时，需从报表服务器的备份中恢复报表。 有关在 Reporting Services 中还原自定义报表的详细信息，请参阅 [Reporting Services 的备份和还原操作](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services)。


### <a name="recover-content-files"></a>恢复内容文件

站点数据库会跟踪站点服务器存储内容文件的位置。 内容文件本身不会作为备份和恢复过程的一部分进行备份或还原。 要完全恢复内容文件，需要将内容库和包源文件还原到原始位置。 有多种方法可以恢复内容文件。 最简单的方法是从站点服务器的文件系统备份还原文件。

如果没有包源文件的文件系统备份，请手动复制或下载它们。 此过程与最初创建包时的过程类似。 在 SQL Server 中运行以下查询来查找所有包和应用程序的包源位置：`SELECT * FROM v_Package`。 通过查看包 ID 的前三个字符来确定包源站点。 例如，如果包 ID 为 CEN00001，则源站点的站点代码为 CEN。 在还原包源文件时，必须将它们还原到发生故障之前所在的同一位置。

如果没有包含内容库的文件系统备份，则可以使用以下还原选项：  

- **导入预留内容文件**：在 Configuration Manager 层次结构中，可以从另一个位置创建含所有包和应用程序的预留内容文件。 然后导入预留内容文件以恢复站点服务器上的内容库。  

- **更新内容**：Configuration Manager 会将内容从包源复制到内容库。 原始位置中必须有包源文件，此操作才能成功完成。 对每个包和应用程序执行此操作。


### <a name="recover-custom-software-updates"></a>恢复自定义软件更新

在备份计划中已包含 System Center Updates Publisher 数据库文件时，如果 Updates Publisher 计算机出现故障，可以恢复数据库。 有关 Updates Publisher 的详细信息，请参阅 [System Center Updates Publisher](/sccm/sum/tools/updates-publisher)。

#### <a name="restore-the-updates-publisher-database"></a>还原 Updates Publisher 数据库
1. 在恢复的计算机上重新安装 Updates Publisher。  

2. 将数据库文件 Scupdb.sdf 从备份目标复制到运行 Updates Publisher 的计算机上的 `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` 中。  

3. 如果有多个用户在计算机上运行 Updates Publisher，则将每个数据库文件复制到相应的用户配置文件位置。  


### <a name="user-state-migration-data"></a>用户状态迁移数据

作为状态迁移点属性的一部分，指定存储用户状态数据的文件夹。 恢复状态迁移点后，手动还原服务器上的用户状态数据。 将其还原到故障前存储该数据的同一文件夹。


### <a name="regenerate-the-certificates-for-distribution-points"></a>重新生成分发点的证书

还原站点后，distmgr.log 可能会列出一个或多个分发点的以下条目：`Failed to decrypt cert PFX data`。 此条目表示站点无法解密分发点证书数据。 要解决此问题，需重新生成或重新导入受影响分发点的证书。 使用 [Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) PowerShell cmdlet。


### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>更新用于基于云的分发点的证书

Configuration Manager 需要 Azure 管理证书才能使站点服务器与基于云的分发点进行通信。 在站点恢复后，更新基于云的分发点的证书。



## <a name="recover-a-secondary-site"></a>恢复辅助站点

Configuration Manager 不支持在辅助站点上进行数据库备份，但支持通过重新安装辅助站点进行恢复。 在 Configuration Manager 辅助站点失败时，必须恢复辅助站点。


### <a name="requirements"></a>要求

- 服务器必须满足辅助站点的所有先决条件，而且具有适当的安全权限配置。  

- 使用故障站点所用的相同安装路径。  

- 使用具有与故障服务器相同配置的服务器。 此配置包括其完全限定的域名 (FQDN)。  

- 服务器必须具有与故障站点相同的 SQL Server 配置。  

     - 在恢复辅助站点的过程中，如果计算机上尚未安装 SQL Server Express，则 Configuration Manager 不会安装它。  

     - 使用在故障前用于辅助站点数据库的同一个 SQL Server 版本和同一个 SQL Server 实例。  


### <a name="procedure"></a>过程

在 Configuration Manager 控制台的“站点”节点中使用“恢复辅助站点”操作。 与其他类型的站点不同，辅助站点的恢复不使用备份文件。 此过程会在故障服务器上重新安装辅助站点文件。 站点重新安装后，辅助站点数据会从父级主站点重新初始化。

在恢复过程中，Configuration Manager 会验证辅助站点服务器上是否存在内容库。 它还会检查是否有可用的合适内容。 如果辅助站点包含合适的内容，则它会使用现有的内容库。 否则，要恢复辅助站点的内容库，需要将内容重新分发或预留到服务器。

如果拥有不在辅助站点上的分发点，则无需在恢复辅助站点的过程中重新安装分发点。 在恢复辅助站点之后，站点会自动与分发点同步。

可以在 Configuration Manager 控制台的“站点”节点中使用“显示安装状态”操作来验证辅助站点恢复的状态。
