---
title: Technical Preview 1612 中的功能
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager Technical Preview（版本 1612）中的可用功能。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a72f7979c38a0a8782aa41fef66b7aa00af9bc0f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342233"
---
# <a name="capabilities-in-technical-preview-1612-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1612 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*



本文介绍了 System Center Configuration Manager Technical Preview（版本 1612）中的可用功能。 你可以安装此版本，以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。    


**以下是此版本可以试用的新功能。**  

## <a name="the-data-warehouse-service-point"></a>数据仓库服务点
从 Technical Preview 1612 开始，通过数据仓库服务点，可存储和报告关于 Configuration Manager 部署的长期历史数据。 通过从 Configuration Manager 站点数据库自动同步到数据仓库数据库可实现这点。 然后，可从 Reporting Services 点访问此信息。

默认情况下，安装新的站点系统角色时，可以使用 Configuration Manager 在指定的 SQL Server 实例上创建数据仓库数据库。 数据仓库最多支持 2 TB 数据，且具有跟踪更改的时间戳。  默认情况下，从站点数据库同步的数据包括全局数据、站点数据、Global_Proxy、云数据和数据库视图中的数据组。 还可修改要同步的内容以包括其他表，或从默认的复制组中排除特定表。
要同步的默认数据包括以下内容的相关信息：
- 基础结构运行状况
- 安全
- 合规性
- 恶意软件   
- 软件部署
- 清单详细信息（但不会同步清单历史记录）

除安装和配置数据仓库数据库外，还安装了多个新报表，以方便用户搜索和报告此数据。

### <a name="data-warehouse-dataflow"></a>数据仓库数据流   
![Datawarehouse_flow](./media/datawarehouse.png)

| 步骤         | 详细信息  |
|:------:|-----------|  
| **1**  |  站点服务器传输和存储站点数据库中的数据。  |  
| **2** |   根据其计划和配置，数据仓库服务点可从站点数据库获取数据。  |  
| **3** |  数据仓库服务点可传输和储存数据仓库数据库中的一份已同步数据的副本。 |  
| **A** |  通过使用内置报表，可提出数据请求，该请求将通过 SQL Server Reporting Services 传递到 Reporting Services 点。 |  
| **B** |   大多数报表针对当前信息，然后对站点数据库运行这些请求。 |  
| **C** | 报表通过使用类别为**数据仓库**的其中一个报表请求历史数据时，则会对数据仓库数据库运行该请求。   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>数据仓库服务点和数据库的必备组件
- 层次结构必须安装 Reporting Services 点站点系统角色。
- 安装站点系统角色的计算机要求具有 .NET Framework 4.5.2 或更高版本。
- 安装站点系统角色的计算机帐户必须对要托管数据仓库数据库的计算机具有本地管理员权限。
- 用于安装站点系统角色的管理帐户必须是要托管数据仓库数据库的 SQL Server 实例上的 DBO。  
-  支持的数据库需满足以下要求：
  - 使用 SQL Server 2012 或更高版本、Enterprise Edition 或 Datacenter Edition。
  - 位于默认或命名的实例上
  - 位于 SQL Server 群集上。 尽管此配置应可正常工作，但尚未经过测试，因此支持人员正尽其最大努力。
  - 与站点数据库或 Reporting Services 点数据库共存时。 但是，我们建议在单独的服务器上进行安装。  
- 用作 *Reporting Services 点帐户*的帐户必须具有对数据仓库数据库的 **db_datareader** 权限。  
- SQL Server AlwaysOn 可用性组上不支持该数据库。

### <a name="install-the-data-warehouse"></a>安装数据仓库
通过使用“添加站点系统角色向导”或“创建站点系统服务器向导”，在管理中心站点或主站点上安装数据仓库站点系统角色。 有关详细信息，请参阅[安装站点系统角色](/sccm/core/servers/deploy/configure/install-site-system-roles)。 层次结构支持此角色的多个实例，但是每个站点仅支持一个实例。  

安装角色时，Configuration Manager 在指定的 SQL Server 实例上创建数据仓库数据库。 如果指定现有数据库的名称（类似[将数据仓库数据库迁移到新的 SQL Server ](#move-the-data-warehouse-database)时采取的操作），Configuration Manager 不会创建新的数据库，而是使用指定的数据库。

#### <a name="configurations-used-during-installation"></a>安装期间使用的配置
使用以下信息完成站点系统角色的安装：

“系统角色选择”页面：  
必须先安装 Reporting Services 点，然后向导才能显示选择和安装数据仓库服务点的选项。

**常规**页面：以下常规信息为必需信息：
- **Configuration Manager 数据库设置：**   
  - **服务器名称** - 指定承载站点数据库的服务器的 FQDN。 如果不使用 SQL Server 的默认实例，则必须采用如下格式在 FQDN 后指定实例：***&lt;Sqlserver_FQDN>\&lt;Instance_name>***
  - **数据库名称** - 指定站点数据库的名称。
  - **验证** - 单击“验证”可确保已成功连接站点数据库。
</br></br>
- **数据仓库数据库设置：**
  - **服务器名称** - 指定承载数据仓库服务点和数据库的服务器的 FQDN。 如果不使用 SQL Server 的默认实例，则必须采用如下格式在 FQDN 后指定实例：***&lt;Sqlserver_FQDN>\&lt;Instance_name>***
  - **数据库名称** - 指定数据仓库数据库的 FQDN。  Configuration Manager 将使用此名称创建数据库。 如果指定 SQL server 实例上已存在的数据库名称，则 Configuration Manager 将使用该数据库。
  - **验证** - 单击“验证”可确保已成功连接站点数据库。

“同步设置”页面：   
- **数据设置：**
  - **要同步的复制组** – 选择要同步的数据组。 有关各种类型数据组的信息，请参阅[数据库复制](/sccm/core/servers/manage/data-transfers-between-sites#a-namebkmkdbrepa-database-replication)和[站点间数据传输](/sccm/core/servers/manage/data-transfers-between-sites)中的**分布式视图**。
  - **包含同步的表** – 指定要同步的每个附加表的名称。 使用逗号分隔多个表。 除选择的复制组外，还会从站点数据库同步这些表。
  - **排除同步的表** - 从同步的复制组中指定各个表的名称。 从中排除所指定的表。 使用逗号分隔多个表。
- **同步设置：**
  - **同步时间间隔（分钟）** - 以分钟为单位指定一个值。 到时间间隔后，会开始新的同步。 支持范围为 60 到 1440 分钟（24 小时）。
  - **计划** - 指定同步进行的天数。

**报表点访问**：   
安装数据仓库角色后，请确保用作 *Reporting Services 点帐户*的帐户具有对数据仓库数据库的 **db_datareader** 权限。

#### <a name="troubleshoot-installation-and-data-synchronization"></a>安装和数据同步故障排除
使用以下日志，调查数据仓库服务点安装或数据同步方面的问题：
- **DWSSMSI.log** 和 **DWSSSetup.log** - 使用这些日志调查安装数据仓库服务点时的错误。
-   **Microsoft.ConfigMgrDataWarehouse.log** – 使用此日志调查站点数据库和数据仓库数据库之间的数据同步。

### <a name="reporting"></a>报表
安装数据仓库站点系统角色之后，可在 Reporting Services 点上找到以下报告，其类别为**数据仓库**：

|报告                   | 详细信息                                  |
|-------------------------|------------------------------------------|
| **应用程序部署报表** | 查看有关特定应用程序和计算机的应用程序部署的详细信息。|
| **Endpoint Protection 和软件更新合规性报表**   | 查看缺少软件更新的计算机。|
| **常规硬件清单报表**  | 查看特定计算机的所有硬件清单。|
| **常规软件清单报表**  | 查看特定计算机的所有软件清单。|
| **基础结构运行状况概述**  |显示 Configuration Manager 基础结构运行状况概述。|
| **检测到的恶意软件列表**  |查看组织中检测到的恶意软件。|
| 软件分发摘要报表 | 特定播发和计算机的软件分发摘要。|

### <a name="move-the-data-warehouse-database"></a>迁移数据仓库数据库
使用以下步骤将数据仓库数据库移到新的 SQL Server：

  1. 查看当前数据库配置并记录配置详细信息，包括内容如下：  
   - 同步的数据组
   - 在同步中包含或排除的表       

   将数据库还原到新的服务器并重新安装站点系统角色后，用户将重新配置这些数据组和表。  

  2. 使用 SQL Server Management Studio 备份数据仓库数据库，然后再次将该数据库还原到要托管此数据仓库的新计算机上的 SQL Server。

  将数据库还原到新服务器后，请确保新数据仓库数据库与原始数据仓库数据库上的数据库访问权限相同。

  3. 使用 Configuration Manager 控制台从当前服务器删除数据仓库服务点站点系统角色。

  4. 安装新的数据仓库服务点并指定托管已还原数据仓库数据库的新 SQL Server 和实例的名称。

  5. 安装站点系统角色后，迁移即完成。

可以查看以下 Configuration Manager 日志，确认是否已成功重新安装站点系统角色：  
- **DWSSMSI.log** 和 **DWSSSetup.log** - 使用这些日志调查安装数据仓库服务点时的错误。
-   **Microsoft.ConfigMgrDataWarehouse.log** – 使用此日志调查站点数据库和数据仓库数据库之间的数据同步。


## <a name="content-library-cleanup-tool"></a>内容库清理工具
从 Technical Preview 1612 开始，用户可以使用新的命令行工具 (**ContentLibraryCleanup.exe**) 从分发点删除不再与任何包或应用程序关联的内容（即孤立内容）。 此工具称为内容库清理工具。

此工具仅对其运行时用户指定的分发点上的内容有效，并不会从站点服务器上的内容库中删除内容。

安装 Technical Preview 1612 后，可以在 Technical Preview 站点服务器中的 \*%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* 文件夹中找到 **ContentLibraryCleanup.exe**。

随附此 Technical Preview 发布的工具旨在替换随附以往 Configuration Manager 产品发布的旧版类似工具。 尽管此工具版本将在 2017 年 3 月 1 日后停用，但新的版本将随附以后的 Technical Preview 发布，直到此工具作为 Current Branch 的一部分或生产就绪型带外版本进行发布。

### <a name="requirements"></a>要求  
 - 此工具可在承载分发点的计算机上直接运行，或者从其他服务器远程运行。 该工具一次只能对一个分发点运行。
 - 运行该工具的用户帐户必须具有基于角色的直接管理权限，该权限相当于 Configuration Manager 层次结构中的完全权限管理员。  当向用户帐户授予具有完全权限管理员权限的 Windows 安全组成员权限时，该工具不能运行。

### <a name="modes-of-operation"></a>操作模式
该工具可按以下两种模式运行：
  1.    **假设模式**：   
      当未指定 **/delete** 开关时，该工具会以假设模式运行，并且标识将从分发点删除但不实际删除任何数据的内容。

      - 该工具以此模式运行时，有关要删除内容的信息会自动写入工具日志文件。 不提示用户确认每个可能的删除操作。
      - 默认情况下，日志文件写入运行工具的计算机上的用户临时文件夹，但用户可使用 /log 开关将日志文件重定向到其他位置。  
      </br>

    使用 /delete 开关运行该工具前，建议以此模式运行该工具，并查看生成的日志文件。  

  2. **删除模式**：使用 **/delete** 开关运行工具时，工具将以删除模式运行。

     - 以此模式运行工具时，可从分发点的内容库删除指定分发点上的孤立内容。
     -  删除每个文件之前，系统将提示用户确认是否要删除文件。  若要删除，请选择“是”；若不删除，请选择“否”；或者选择“删除所有”，跳过后续提示并删除所有孤立内容。  
     </br>

     我们建议在假设模式下运行该工具，并查看生成的日志文件，然后再使用 /delete 开关运行该工具。  

内容库清理工具在其中任一模式下运行时，会自动创建带名称的日志，该日志包括运行采用的模式、分发点名称、日期和操作时间等内容。 工具结束时，日志文件会自动打开。 默认情况下，该日志会写入运行工具所在计算机上的用户**临时**文件夹，但用户可使用命令行开关将日志文件重定向到其他位置，如网络共享。   


### <a name="run-the-tool"></a>运行该工具
要运行该工具，请执行以下操作：
1. 使用管理命令提示符打开包含 **ContentLibraryCleanup.exe** 的文件夹。  
2. 接下来，输入包含所需命令行开关和可选开关的命令行。

**已知问题** 运行该工具时，当任何程序包或部署失败或正在进行时，可能会返回以下错误：
-  *System.InvalidOperationException：由于程序包 <packageID> 未完全安装，因此无法清理此内容库。*

**解决方法：** 无。 当内容正在进行处理或部署失败时，该工具无法可靠地识别孤立的文件。 因此，该工具将不允许你清理内容，直到该问题解决。



### <a name="command-line-switches"></a>命令行开关  
可以按任何顺序使用以下命令行开关。   

|开关|详细信息|
|---------|-------|
|**/delete**  |**可选** </br> 要从分发点删除内容时使用此开关。 删除内容之前，系统会进行提示。 </br></br> 如果不使用此开关，该工具将记录有关要删除的内容的结果，但不会从分发点删除任何内容。 </br></br> 示例：***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**可选** </br> 在阻止所有提示（如删除内容时的提示）的安静模式下运行该工具，并且不会自动打开该日志文件。 </br></br> 示例：***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;distribution point FQDN>**  | **必需** </br> 指定要清理的分发点的完全限定域名 (FQDN)。 </br></br> 示例：***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;primary site FQDN>**       | **可选** - 从主站点上的分发点清除内容时。</br>**必需** - 从辅助站点上的分发点清除内容时。 </br></br> 当分发点位于辅助站点上时，指定分发点所属的主站点的 FQDN，或父级主站点的 FQDN。 </br></br> 示例：***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;primary site code>**  | **可选** - 从主站点上的分发点清除内容时。</br>**必需** - 从辅助站点上的分发点清除内容时。 </br></br> 当分发点位于辅助站点上时，指定分发点所属的主站点的站点代码，或父级主站点的站点代码。</br></br> 示例：***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**可选** </br> 指定放置日志文件的目录。 此目录可以是本地驱动器，或者位于网络共享上。</br></br> 如果不使用此开关，日志文件会自动放在用户临时文件夹中。</br></br> 本地驱动器示例：***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>网络共享示例：***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;share>\&lt;folder>***|


## <a name="improvements-for-in-console-search"></a>控制台中搜索功能的改进
根据 User Voice 反馈，我们对控制台中搜索功能作出以下改进：
 - **对象路径：**  
  现在，很多对象都支持名为**对象路径**的新列。  当用户搜索并将此列包括在显示结果中时，可以查看每个对象的路径。 例如，如果在应用程序节点搜索应用，并且同时要搜索子节点，结果窗格中的对象路径列将向用户显示每个返回对象的路径。   

- **保留搜索文本：**  
  在搜索文本框中输入文本，然后在搜索子节点和搜索当前节点之间切换时，已键入的文本会保留，并且仍然可用于新搜索而无需重新键入。

- **保留搜索子节点的决策：**  
 现在，更改使用的节点时，会保留对搜索当前节点或所有子节点所选择的选项。   这一新特点意味着在控制台执行操作时无需不断重置决策。  默认情况下，打开控制台选项时，将仅搜索当前节点。

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>如果指定的程序正在运行，则阻止安装应用程序。
现在，用户可在部署类型属性配置一列可执行文件（扩展名为 .exe），如果该文件正在运行，则将阻止安装应用程序。 尝试安装后，用户将看到对话框，要求其关闭阻止安装的进程。

### <a name="try-it-out"></a>试试看
配置一列可执行文件
1.  在任何部署类型的属性页上，选择“安装程序处理”选项卡。
2.  单击“添加”，向列表添加一个额外的可执行文件（例如，**Edge.exe**）
3.  单击“确定”以关闭部署类型属性对话框。

现在，向用户或设备部署此应用程序，但其中一个添加的可执行文件正在运行时，最终用户会看到“软件中心”对话框，告知用户由于某个应用程序正在运行而导致安装失败。

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>新的 Windows Hello 企业版最终用户通知

新的 Windows 10 通知告知最终用户必须采取额外操作才能完成 Windows Hello 企业版安装（例如，设置 PIN）。

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Configuration Manager 中适用于企业的 Windows 应用商店支持

现在可在适用于企业的 Windows 应用商店中以“可用”为部署目的，将联机许可应用部署到运行 Configuration Manager 客户端的电脑。
有关更多详细信息，请参阅[使用 System Center Configuration Manager 管理来自适用于企业的 Windows 应用商店的应用](https://docs.microsoft.com/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)。

此功能支持当前仅适用于运行 Windows 10 RS2 预览版的电脑。

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>任务序列失败时返回上一页
现在，运行任务序列出现故障时，可以返回到上一页面。 在此版本之前，出现故障时必须重启任务序列。 例如，可在以下应用场景中使用“上一页”按钮：

- 当计算机在 Windows PE 中启动时，任务序列可用之前可能会先显示任务序列启动对话框。 在此应用场景中单击“下一步”时，会显示任务序列的最后一页，同时显示一条消息告知无可用的任务序列。 现在，可单击“上一页”以再次搜索可用任务序列。 在出现可用任务序列之前，可重复此过程。
- 运行任务序列但分发点上尚无可用从属内容包时，任务序列会失败。 现在，用户可以分发缺失的内容（如果尚未分发），或等待分发点上出现可用内容，然后单击“上一页”使任务序列再次搜索内容。

## <a name="express-installation-files-support-for-windows-10-updates"></a>Windows 10 更新的快速安装文件支持
我们在 Configuration Manager 中添加了对 Windows 10 更新的快速安装文件支持。 如果使用支持版本的 Windows 10，现在可通过 Configuration Manager 设置只下载当前月份 Windows 10 累计更新和上一月份更新之间的增量文件。 当前，在 Configuration Manager Current Branch 中，每个月都会下载完整的 Windows 10 累积更新（包括先前月份的所有更新）。 使用快速安装文件，所需下载文件更小，在客户端上安装更快速。

> [!IMPORTANT]
> 尽管 Configuration Manager 中支持快速安装文件的设置已可用，但仅 Windows 10 版本 1607 支持此功能，该版本具有 2017 年 1 月 10 日（星期二修补日）发布的更新中随附的 Windows 更新代理更新。 若要深入了解这些更新，请参阅[支持文章 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693)。 2017 年 2 月 14 日发布下一组更新时，用户可充分利用快速安装文件。 不包含此更新的 Windows 10 版本 1607 和之前版本不支持快速安装文件。


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>在服务器上启用 Windows 10 更新的快速安装文件下载
若要开始同步 Windows 10 快速安装文件的元数据，则必须在软件更新点属性中将其启用。
1.  在 Configuration Manager 控制台中，导航到“管理” > “站点配置” > “站点”。
2.  选择管理中心站点或独立主站点。
3.  在“主页”  选项卡上的“设置”  组中，单击“配置站点组件” ，再单击“软件更新点” 。 在“更新文件”选项卡上，选择“下载所有 Windows 10 已审核更新和快速安装文件的完整文件”。

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>启用客户端对下载并安装快速安装文件的支持
若要在客户端上启用快速安装文件支持，则必须在客户端设置的软件更新分区中启用客户端上的快速安装文件。 这将创建新的 HTTP 侦听器，该侦听器会侦听在指定的端口下载快速安装文件的请求。 在客户端上部署客户端设置启用此功能后，会尝试下载当前月份的 Windows 10 累计更新和上一月份的更新之间的增量文件（客户端必须运行支持快速安装文件的 Windows 10 版本）。
1.  在“软件更新点组件”属性中启用快速安装文件支持（上一过程）。
2.  在 Configuration Manager 控制台中，导航到“管理” > “客户端设置”。
3.  选择相应的客户端设置，然后在“主页”选项卡上，单击“属性”。
4.  选择“软件更新”页，将“在客户端上启用快速更新安装”设置配置为“是”，并将“下载快速更新内容所用端口”设置配置为客户端上 HTTP 侦听器所使用的端口。


## <a name="odata-endpoint-data-access"></a>OData 终结点数据访问

 Configuration Manager 现提供 RESTful OData 终结点，以便访问 Configuration Manager 数据。 此终结点与 Odata 版本 4 兼容，使诸如 Excel 和 Power BI 等工具可轻松地通过单个终结点访问 Configuration Manager 数据。 Technical Preview 1612 仅支持对 Configuration Manager 中对象的读取访问。  

[Configuration Manager WMI 提供程序](/sccm/develop/reference/configuration-manager-reference)中当前可用的数据现在也可通过新的 OData RESTful 终结点进行访问。 通过 OData 终结点公开的实体集，能够循环访问与使用 WMI 提供程序查询的相同数据。

### <a name="try-it-out"></a>试试看

必须对站点启用 OData 终结点，然后才可使用该终结点。

1.  转到“管理” > “站点配置” > “站点”。
2.  选择主站点，然后单击“属性”。
3.  在主站点属性页的“常规”选项卡上，单击“对此站点上所有提供程序启用 REST 终结点”，然后单击“确定”。

在个人偏好的 OData 查询查看器中，请尝试类似于以下示例的查询，以在 Configuration Manager 中返回各种对象：

| 目的 | OData 查询 |
|---|---|
| 获取所有集合 | `http://localhost/CMRestProvider/Collection` |
| 获取集合 | `http://localhost/CMRestProvider/Collection('SMS00001')`
| 获取集合中的前 100 个设备 | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| 获取集合中具有资源 ID 的设备 | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| 获取集合中设备的操作系统 | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| 获取集合中的用户 | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> 此表中所示的示例查询使用 localhost 作为 URL 中的主机名称，并且可在运行 SMS 提供程序的计算机上使用。 如果要在另一台计算机运行查询，请将 localhost 替换为已安装 SMS 提供程序的服务器的 FQDN。

## <a name="azure-active-directory-onboarding"></a>Azure Active Directory 载入

Azure Active Directory (AD) 载入会创建一个其他云服务使用的 Configuration Manager 和 Azure Active Directory 之间的连接。 当前可将此用于创建云管理网关所需的连接。

以 Azure 管理员执行此任务，因为这需要 Azure 管理员凭据。

#### <a name="to-create-the-connection"></a>创建连接：

2. 在“管理”工作区中，选择“云服务” > “Azure Active Directory” > “添加 Azure Active Directory”。
2. 选择“登录”，创建与 Azure AD 的连接。

#### <a name="configuration-manager-client-requirements"></a>Configuration Manager 客户端要求

在云管理网关中启用用户策略创建具有几点要求。

- 必须完成 Azure AD 载入流程，且客户端开始必须连接到公司网络，以便获取连接信息。
- 客户端必须都已加入域（已在 Active Directory 中注册）和已加入云域（已在 Azure AD 中注册）。
- 必须运行 [Active Directory 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#active-directory-user-discovery#active-directory-user-discovery)。
- 必须修改 Configuration Manager 客户端，以允许用户策略请求通过 Internet，并将更改部署到客户端。 尽管尚未完成用户策略所需的配置更改，但由于此客户端更改发生在客户端设备上，因此可以通过云管理网关部署更改。
- 管理点必须配置为使用 HTTPS，以保护网络中的令牌，并且必须已安装 .Net 4.5。

进行这些配置更改后，便可创建用户策略并将客户端移动到 Internet 以测试策略。 通过云管理网关的用户策略请求将使用基于 Azure AD 令牌的身份验证进行身份验证。

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>更改为配置多重身份验证以进行设备注册

现在，可为在 Azure 门户中进行设备注册设置多重身份验证 (MFA)，Configuration Manager 控制台中已删除 MFA 选项。 有关设置注册 MFA 的详细信息，请参阅 [Microsoft Intune 主题](https://docs.microsoft.com/en-us/intune/deploy-use/multi-factor-authentication-azure-active-directory)。
