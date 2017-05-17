---
title: "数据仓库 | Microsoft Docs"
description: "System Center Configuration Manager 的数据仓库服务点和数据库"
ms.custom: na
ms.date: 3/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 3c2a07f560e0aa3d2beb7cc50e71c98ac45c27e1
ms.openlocfilehash: 9239f6e749c368835e8594ca2d07378d8555b99e
ms.contentlocale: zh-cn
ms.lasthandoff: 05/17/2017


---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>System Center Configuration Manager 的数据仓库服务点
*适用范围：System Center Configuration Manager (Current Branch)*

从 1702 版开始，可以使用数据仓库服务点存储和报告关于 Configuration Manager 部署的长期历史数据。

> [!TIP]  
> 如 1702 版所述，数据仓库服务点属于预发行功能。 若要启用此功能，请参阅[使用预发行功能](/sccm/core/servers/manage/pre-release-features)。

数据仓库最多支持 2 TB 数据，且具有跟踪更改的时间戳。 通过从 Configuration Manager 站点数据库自动同步到数据仓库数据库可实现数据存储。 然后，可从 Reporting Services 点访问此信息。


同步的数据包括以下全局数据和站点数据组中的对象：
- 基础结构运行状况
- 安全
- 合规性
- 恶意软件   
- 软件部署
- 清单详细信息（但不会同步清单历史记录）

安装站点系统角色时，将安装和配置数据仓库数据库。 还会安装多个报表，以便你可轻松就此数据进行搜索和报告。



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>数据仓库服务点的先决条件
- 安装站点系统角色的计算机要求具有 .NET Framework 4.5.2 或更高版本。
- 安装站点系统角色的计算机的计算机帐户用于将数据与数据仓库数据库同步。 此帐户要求具有以下权限：  
  - 在将托管数据仓库数据库的计算机上是**管理员**。
  - 对数据仓库数据库具有 **DB_owner** 权限。
-    SQL Server 2012 或更高版本的默认或命名的实例上支持数据仓库数据库。 版本必须为企业版或数据中心版。
  - SQL Server AlwaysOn 可用性组：不支持此配置。
  - SQL Server 群集：不支持 SQL Server 故障转移群集。 这是因为数据仓库数据库尚未在 SQL Server 故障转移群集上进行深入测试。
  - 当数据仓库数据库是站点服务器数据库的远程数据库时，必须具有单独的 SQL Server（用于托管数据库）许可证。

> [!IMPORTANT]  
> 当运行数据仓库服务点或托管数据仓库数据库的计算机运行以下任一语言时，不支持数据仓库：
> - JPN – 日语
> - KOR – 朝鲜语
> - CHS - 简体中文
> - CHT – 繁体中文 此问题将在后续版本中解决。


## <a name="install-the-data-warehouse"></a>安装数据仓库
可将此站点系统角色仅安装在层次结构的顶层站点（管理中心站点或独立主站点）。

每个层次结构都支持单个此角色的实例，并且可位于该顶层站点的任何站点系统上。 相对于站点系统角色而言，托管仓库数据库的 SQL Server 可以是本地的，也可以是远程的。 尽管数据仓库与在同一站点中安装的 Reporting Services 点兼容，但不需要将这两个站点系统角色安装在同一台服务器上。   

若要安装该角色，请使用“添加站点系统角色向导”或“创建站点系统服务器向导”。 有关详细信息，请参阅[安装站点系统角色](/sccm/core/servers/deploy/configure/install-site-system-roles)。  

安装角色时，Configuration Manager 在指定的 SQL Server 实例上创建数据仓库数据库。 如果指定现有数据库的名称（类似[将数据仓库数据库迁移到新的 SQL Server ](#move-the-data-warehouse-database)时采取的操作），Configuration Manager 不会创建新的数据库，而是使用指定的数据库。

### <a name="configurations-used-during-installation"></a>安装期间使用的配置
“系统角色选择”页面：  

“常规”页：
-     **Configuration Manager 数据仓库数据库连接设置**：
 - **SQL Server 完全限定的域名**：  
 指定托管数据仓库服务点和数据库的服务器的完全限定的域名 (FQDN)。
 - **SQL Server 实例名称(如果适用)**：   
 如果不使用 SQL Server 的默认实例，必须指定该实例。
 - **数据库名称**：   
 指定数据仓库数据库的名称。  Configuration Manager 将使用此名称创建数据仓库数据库。 如果指定 SQL server 实例上已存在的数据库名称，则 Configuration Manager 将使用该数据库。
 - **用于连接的 SQL Server 端口**：   
 指定为托管数据仓库数据库的 SQL Server 配置的 TCP/IP 端口号。 数据仓库同步服务使用此端口连接到数据仓库数据库。  

“同步计划”页：   
- **同步计划**：
 - **开始时间**：  
 指定想要数据仓库开始同步的时间。
 - **定期模式**：
    - **每天**：指定每天运行同步。
    - **每周**：指定每周的某一天和每周重复进行同步。

## <a name="reporting"></a>报表
安装数据仓库服务点后，同一站点上安装的 Reporting Services 点上将提供多个报表。 如果在安装 Reporting Services 点之前先安装数据仓库服务点，当稍后安装 Reporting Services 点时，将自动添加这些报表。

数据仓库站点系统角色包括下列报表，并且其类别为**数据仓库**：
 - **应用程序部署 -历史记录**：   
 查看有关特定应用程序和计算机的应用程序部署的详细信息。
 - **Endpoint Protection 和软件更新符合性 - 历史记录**：查看缺少软件更新的计算机。  
 - **常规硬件清单 - 历史记录**：      
 查看特定计算机的所有硬件清单。
 - **常规软件清单 - 历史记录**：      
 查看特定计算机的所有软件清单。
 - **基础结构运行状况概述 - 历史记录**：     
 显示 Configuration Manager 基础结构运行状况概述
 - **检测到的恶意软件列表 - 历史记录**：     
 查看组织中检测到的恶意软件。
 - **软件分发摘要 - 历史记录**：     
 特定播发和计算机的软件分发摘要。


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>将现有的独立主站点扩展到层次结构中
必须先卸载数据仓库服务点角色，然后才能安装管理中心站点来扩展现有的独立主站点。 安装管理中心站点之后，可以随后在管理中心站点上安装站点系统角色。  

与移动数据仓库数据库不同，此更改会导致之前在主站点上同步的历史数据丢失。 不支持从主站点备份数据库，然后在管理中心站点上进行还原。




## <a name="move-the-data-warehouse-database"></a>迁移数据仓库数据库
使用以下步骤将数据仓库数据库移到新的 SQL Server：

1.    使用 SQL Server Management Studio 备份数据仓库数据库，然后将该数据库还原到要托管此数据仓库的新计算机上的 SQL Server。   
> [!NOTE]     
> 将数据库还原到新服务器后，请确保新数据仓库数据库与原始数据仓库数据库上的数据库访问权限相同。  

2.    使用 Configuration Manager 控制台从当前服务器删除数据仓库服务点站点系统角色。
3.    重新安装数据仓库服务点并指定托管已还原数据仓库数据库的新 SQL Server 和实例的名称。
4.    安装站点系统角色后，迁移即完成。

## <a name="troubleshooting-data-warehouse-issues"></a>解决数据仓库问题
**日志文件**：  
使用以下日志，调查数据仓库服务点安装或数据同步方面的问题：
 - *DWSSMSI.log* 和 *DWSSSetup.log* - 使用这些日志调查安装数据仓库服务点时的错误。
 - *Microsoft.ConfigMgrDataWarehouse.log* – 使用此日志调查站点数据库和数据仓库数据库之间的数据同步。

**设置失败**  
 当数据仓库为在某计算机上安装的第一个站点系统角色时，在远程站点系统服务器上安装数据仓库服务点将失败。  
  - **解决方案**：   
    请确保要安装数据仓库服务点的计算机上托管至少一个其他站点系统角色。  


**已知同步问题**：   
同步失败，同时 *Microsoft.ConfigMgrDataWarehouse.log* 中出现以下消息：**“填充架构对象失败”**  
 - **解决方案**：  
    请确保托管站点系统角色的计算机的计算机帐户是数据仓库数据库上的 **db_owner**。

当数据仓库数据库和 Reporting Servive 点位于不同的站点系统时，数据仓库报表将无法打开。  

 - **解决方案**：  
    在数据仓库数据库上向 **Reporting Services 点帐户**授予 **db_datareader** 权限。

打开数据仓库报表打开时，会返回以下错误：

*报表处理期间出错。(rsProcessingAborted)无法创建与数据源 “AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_” 的连接。(rsErrorOpeningConnection)已成功创建与服务器的连接，但随后在预登录握手期间出错。(提供程序: SSL 提供程序，错误: 0 - 证书链由不受信任的颁发机构颁发。)*

- **解决方案**：使用以下步骤配置证书：

  1. 在托管数据仓库数据库的计算机上：

    1. 打开 IIS，单击“服务器证书”，右键单击“创建自签名证书”，然后指定证书名称的“友好名称”为**数据仓库 SQL Server 标识证书**。 将证书存储选为“个人”。
    2. 打开“SQL Server 配置管理器”，在“SQL Server 网络置配”下右键单击选择“MSSQLSERVER 协议”下的“属性”。 然后，在“证书”选项卡上，选择“数据仓库 SQL Server 标识证书”作为证书，然后保存所做更改。  
    3. 打开“SQL Server 配置管理器”，在“SQL Server 服务”下，重启“SQL Server 服务” 和“报告服务”。
    4.    打开 Microsoft 管理控制台 (MMC)，然后添加**证书**的管理单元，选择以管理本地计算机的**计算机帐户**的证书。 然后，在 MMC 中，展开“个人”文件夹 >“证书”，然后将“数据仓库 SQL Server 标识证书”导出为 **DER 编码的二进制 X.509 (.CER)** 文件。    
  2.    在托管 SQL Server Reporting Services 的计算机上，打开 MMC，然后添加**证书**的管理单元，然后选择以管理**计算机帐户**的证书。 在**受信任的根证书颁发机构**文件夹下，导入**数据仓库 SQL Server 标识证书**。


## <a name="data-warehouse-dataflow"></a>数据仓库数据流   
![Datawarehouse_flow](./media/datawarehouse.png)

**数据存储和同步**

| 步骤   | 详细信息  |
|:------:|-----------|  
| **1**  |     站点服务器传输和存储站点数据库中的数据。  |  
| **2**  |      根据其计划和配置，数据仓库服务点可从站点数据库获取数据。  |  
| **3**  |  数据仓库服务点可传输和存储数据仓库数据库中已同步数据的副本。 |  
**报表**

| 步骤   | 详细信息  |
|:------:|-----------|  
| **A**  |  通过使用内置报表，用户可提出数据请求。 该请求将通过 SQL Server Reporting Services 传递到 Reporting Services 点。 |  
| **B**  |      大多数报表针对当前信息，然后对站点数据库运行这些请求。 |  
| **C**  | 报表通过使用类别为**数据仓库**的其中一个报表请求历史数据时，则会对数据仓库数据库运行该请求。   |  

