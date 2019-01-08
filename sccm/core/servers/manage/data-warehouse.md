---
title: 数据仓库
titleSuffix: Configuration Manager
description: Configuration Manager 的数据仓库服务点和数据库
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c04ee9a62b6c629060f79df2f4b104fe78ca794
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418979"
---
#  <a name="the-data-warehouse-service-point-for-configuration-manager"></a>Configuration Manager 的数据仓库服务点

适用范围：System Center Configuration Manager (Current Branch)

<!--1277922--> 使用数据仓库服务点存储和报告关于 Configuration Manager 部署的长期历史数据。

> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  


数据仓库最多支持 2 TB 数据，且具有跟踪更改的时间戳。 数据仓库通过自动将 Configuration Manager 站点数据库中的数据同步到数据仓库数据库来存储数据。 然后，可从 Reporting Services 点访问此信息。 同步到数据仓库数据库的数据将保留三年。 内置任务会定期删除超过三年的数据。

同步的数据包括以下全局数据和站点数据组中的对象：
- 基础结构运行状况
- 安全
- 合规性
- 恶意软件   
- 软件部署
- 清单详细信息（但不会同步清单历史记录）

安装站点系统角色时，将安装和配置数据仓库数据库。 还会安装多个报表，以便你可轻松就此数据进行搜索和报告。

从版本 1810 开始，可将更多表从站点数据库同步到数据仓库。 通过此更改，可根据业务需求创建更多报告。<!--1358870--> 



## <a name="prerequisites"></a>先决条件

- 只有在层次结构的顶层站点中才会支持数据仓库站点系统角色。 例如，管理中心站点或独立主站点。  

- 安装站点系统角色的计算机要求具有 .NET Framework 4.5.2 或更高版本。  

- 在数据仓库数据库上向 **Reporting Services 点帐户**授予 **db_datareader** 权限。  

- 要与数据仓库数据库同步数据，Configuration Manager 将使用站点系统角色的计算机帐户。 此帐户要求具有以下权限：  

    - 对托管数据仓库数据库的计算机具有**管理员**权限。  

    - 对数据仓库数据库具有 DB_Creator 权限。  

    - 对顶层站点的数据库具有 DB_owner 或带 execute 的 DB_reader 权限。  

- 数据仓库数据库需要使用 SQL Server 2012 或更高版本。 版本可以是 Standard、Enterprise 或 Datacenter。 数据仓库的 SQL Server 版本不需要与站点数据库服务器相同。<!--SCCMDocs issue 662-->  

- 仓库数据库支持以下 SQL Server 配置：  

    - 默认或命名的实例  

    - SQL Server Always On 可用性组  

    - SQL Server 故障转移群集  

- 如果使用[分布式视图](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews)，则必须在托管管理中心站点的数据库的同一服务器上安装数据仓库服务点。  

有关 SQL Server 许可的详细信息，请参阅[产品和许可常见问题解答](/sccm/core/understand/product-and-licensing-faq)。 <!-- sms500967 -->

将数据仓库数据库的大小设置为与站点数据库相同。 虽然数据仓库最初较小，但它会随着时间的推移而增长。 <!--SCCMDocs issue 756-->



## <a name="install"></a>安装

在顶层站点的任何站点系统上，每个层次结构都支持此角色的单个实例。 相对于站点系统角色而言，托管仓库数据库的 SQL Server 可以是本地的，也可以是远程的。 数据仓库适用于安装在同一站点的 Reporting Services 点。 不需要在同一台服务器上安装两个站点系统角色。   

若要安装该角色，请使用“添加站点系统角色向导”或“创建站点系统服务器向导”。 有关详细信息，请参阅[安装站点系统角色](/sccm/core/servers/deploy/configure/install-site-system-roles)。 在向导的“系统角色选择”页上，选择“数据仓库服务点”角色。 

安装角色时，Configuration Manager 在指定的 SQL Server 实例上创建数据仓库数据库。 如果指定现有数据库的名称，Configuration Manager 将不会创建新数据库。 而会使用你指定的数据库。 此过程与[将数据仓库数据库移动到新 SQL Server](#move-the-data-warehouse-database) 时的过程相同。


### <a name="configure-properties"></a>配置属性

#### <a name="general-page"></a>“常规”页

- **SQL Server 完全限定的域名**：指定托管数据仓库服务点和数据库的服务器的完全限定的域名 (FQDN)。  

- **SQL Server 实例名称(如果适用)**：如果不使用 SQL Server 的默认实例，则指定该命名实例。  

- **数据库名称**：指定数据仓库数据库的名称。 Configuration Manager 使用此名称创建数据仓库数据库。 如果指定 SQL Server 实例上已存在的数据库名称，则 Configuration Manager 会使用该数据库。  

- **用于连接的 SQL Server 端口**：指定托管数据仓库数据库的 SQL Server 使用的 TCP/IP 端口号。 数据仓库同步服务使用此端口连接到数据仓库数据库。 默认情况下，它使用 SQL Server 端口 1433 进行通信。  

- **数据仓库服务点帐户**：从版本 1802 开始，设置 SQL Server Reporting Services 连接到数据仓库数据库时使用的用户名。  


#### <a name="synchronization-schedule-page"></a>同步计划页
适用于版本 1806 及更早版本

- **开始时间**：指定想要数据仓库开始同步的时间。  

- **定期模式**

    - **每天**：指定每天运行同步。  

    - **每周**：指定每周的某一天和每周重复进行同步。


#### <a name="synchronization-settings-page"></a>同步设置页
适用于 1810 和更高版本

- **数据同步自定义设置**：选择“选择表”选项。 在“数据库表”窗口中，选择要与数据仓库数据库同步的表名。 使用筛选器按名称搜索，或选择下拉列表以选择特定组。 完成后选择“确定”进行保存。  

    > [!Note]  
    > 无法删除该角色默认选择的表。  

- **开始时间**：指定想要数据仓库开始同步的时间。  

- **定期模式**

    - **每天**：指定每天运行同步。  

    - **每周**：指定每周的某一天和每周重复进行同步。



## <a name="reporting"></a>报表

安装数据仓库服务点后，可以在站点的 Reporting Services 点上获得多个报告。 如果在安装 Reporting Services 点之前先安装数据仓库服务点，当稍后安装 Reporting Services 点时，将自动添加这些报表。

> [!WARNING]  
> 从版本 1802 开始，数据仓库点支持备用凭据。<!--507334--> 如果从先前版本的 Configuration Manager 升级，则需指定 SQL Server Reporting Services 用于连接到数据仓库数据库的凭据。 在添加凭据之前，数据仓库报告不会打开。 
> 
> 要指定一个帐户，请在角色属性中为数据仓库服务点帐户设置用户名。 有关详细信息，请参阅[配置属性](#configure-properties)。 

数据仓库站点系统角色包括数据仓库类别下的以下报告：  

- **应用程序部署 -历史记录**：查看有关特定应用程序和计算机的应用程序部署的详细信息。  

- **Endpoint Protection 和软件更新符合性 - 历史记录**：查看缺少软件更新的计算机。  

- **常规硬件清单 - 历史记录**：查看特定计算机的所有硬件清单。  

- **常规软件清单 - 历史记录**：查看特定计算机的所有软件清单。  

- **基础结构运行状况概述 - 历史记录**：显示 Configuration Manager 基础结构运行状况概述。  

- **检测到的恶意软件列表 - 历史记录**：  查看组织中检测到的恶意软件。  

- **软件分发摘要 - 历史记录**：特定播发和计算机的软件分发摘要。  



## <a name="site-expansion"></a>站点扩展

先卸载数据仓库服务点角色，然后才能安装管理中心站点来扩展现有的独立主站点。 安装管理中心站点之后，可以随后在管理中心站点上安装站点系统角色。  

与移动数据仓库数据库不同，此更改会导致之前在主站点上同步的历史数据丢失。 不支持从主站点备份数据库，然后在管理中心站点上进行还原。



## <a name="move-the-database"></a>移动数据库

使用以下步骤将数据仓库数据库移到新的 SQL Server：  

1. 使用 SQL Server Management Studio 备份数据仓库数据库。 然后，将该数据库还原到托管数据仓库的新计算机上的 SQL Server。  

    > [!NOTE]  
    > 将数据库还原到新服务器后，请确保新数据仓库数据库与原始数据仓库数据库上的数据库访问权限相同。  

2. 使用 Configuration Manager 控制台从当前服务器删除数据仓库服务点角色。  

3. 重新安装数据仓库服务点。 指定托管已还原数据仓库数据库的新 SQL Server 和实例的名称。  

4. 安装站点系统角色后，迁移即完成。  



## <a name="troubleshooting"></a>故障排除 

### <a name="log-files"></a>日志文件 

使用以下日志，调查数据仓库服务点安装或数据同步方面的问题：

- DWSSMSI.log 和 DWSSSetup.log：使用这些日志调查安装数据仓库服务点时的错误。  

- **Microsoft.ConfigMgrDataWarehouse.log**：使用此日志调查站点数据库和数据仓库数据库之间的数据同步。  


### <a name="set-up-failure"></a>设置失败 

当数据仓库服务点角色是你在远程服务器上安装的第一个角色时，数据仓库的安装将失败。  

#### <a name="workaround"></a>解决方法 
请确保安装数据仓库服务点的计算机上已托管了至少一个其他角色。  


### <a name="synchronization-failed-to-populate-schema-objects"></a>同步无法填充架构对象 

同步失败，同时 Microsoft.ConfigMgrDataWarehouse.log 中出现以下消息：`failed to populate schema objects`

#### <a name="workaround"></a>解决方法 
请确保站点系统角色的计算机帐户是数据仓库数据库上的 db_owner。


### <a name="reports-fail-to-open"></a>报表打开失败

当数据仓库数据库和 Reporting Servive 点位于不同的站点系统时，数据仓库报表将无法打开。  

#### <a name="workaround"></a>解决方法
在数据仓库数据库上向 **Reporting Services 点帐户**授予 **db_datareader** 权限。


### <a name="error-opening-reports"></a>打开报表时出错

打开数据仓库报表打开时，会返回以下错误：

```
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

#### <a name="workaround"></a>解决方法 
使用以下步骤配置证书：

1. 在托管数据仓库数据库的计算机上：  

    1. 打开 IIS，选择“服务器证书”，然后右键单击“创建自签名证书”。 然后将证书名称的“友好名称”指定为数据仓库 SQL Server 标识证书。 将证书存储选为“个人”。  

    2. 打开“SQL Server 配置管理器” 。 在“SQL Server 网络置配”下，右键单击选择“MSSQLSERVER 协议”下的“属性”。 在“证书”选项卡上，选择“数据仓库 SQL Server 标识证书”作为证书，然后保存所做更改。  

    3. 在“SQL Server 配置管理器”中，在“SQL Server 服务”下，重启“SQL Server 服务”和“Reporting Service”服务。  

    4. 打开 Microsoft 管理控制台 (MMC)，然后添加“证书”管理单元。 选择本地计算机的“计算机帐户”。 展开“个人”文件夹，然后选择“证书”。 将“数据仓库 SQL Server 标识证书”导出为 DER 编码的二进制 X.509 (.CER) 文件。  

2. 在托管 SQL Server Reporting Services 的计算机上，打开 MMC，然后添加证书的管理单元。 选择“计算机帐户”。 在**受信任的根证书颁发机构**文件夹下，导入**数据仓库 SQL Server 标识证书**。  



## <a name="data-flow"></a>数据流   

![显示数据仓库站点组件之间的逻辑数据流的图示](./media/datawarehouse.png)

#### <a name="data-storage-and-synchronization"></a>数据存储和同步

| 步骤   | 详细信息  |
|--------|----------|  
| **1**  | 站点服务器传输和存储站点数据库中的数据。 |  
| **2**  | 根据其计划和配置，数据仓库服务点可从站点数据库获取数据。 |  
| **3**  | 数据仓库服务点可传输和存储数据仓库数据库中已同步数据的副本。 |  


#### <a name="reporting"></a>报表

| 步骤   | 详细信息  |
|--------|----------|  
| **A**  | 通过使用内置报表，用户可提出数据请求。 该请求将通过 SQL Server Reporting Services 传递到 Reporting Services 点。 |  
| **B**  | 大多数报表针对当前信息，然后对站点数据库运行这些请求。 |  
| **C**  | 报表通过使用“类别”为“数据仓库”的其中一个报表请求历史数据时，则会对数据仓库数据库运行该请求。 |  
