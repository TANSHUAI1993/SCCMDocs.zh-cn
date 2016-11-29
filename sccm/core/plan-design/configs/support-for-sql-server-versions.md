---
title: "SQL Server 支持 | System Center Configuration Manager"
description: "获取托管 System Center Configuration Manager 站点数据库的 SQL Server 版本和配置要求。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b17720021f797d404a89933939427696dfafd7dc


---
# <a name="support-for-sql-server-versions-for-system-center-configuration-manager"></a>对 System Center Configuration Manager 的 SQL Server 版本的支持

*适用范围：System Center Configuration Manager (Current Branch)*

每个 System Center Configuration Manager 站点都需要受支持的 SQL Server 版本和配置来托管站点数据库。  

##  <a name="a-namebkmkinstancesa-sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server 实例和位置  
 **管理中心站点和主站点：**  

站点数据库必须使用 SQL Server 的完整安装。  

 SQL Server 的位置可以是：  

-   站点服务器计算机  
-   远离站点服务器的计算机  

支持以下实例：  

-   SQL Server 的默认或命名的实例  
-   多个实例配置  
-   SQL Server 群集 - 请参阅[使用 SQL Server 群集承载站点数据库](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)
-   SQL Server AlwaysOn 可用性组 - 此选项需要 Configuration Manager 1602 版或更高版本。 有关详细信息，请参阅[通过 SQL Server AlwaysOn 实现适用于 System Center Configuration Manager 的高可用性站点数据库](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)  

> [!NOTE]  
>  不支持网络负载平衡 (NLB) 群集配置中的 SQL Server 群集。 此外，不支持 SQL Server 数据库镜像技术和对等复制。 SQL Server 标准事务复制仅支持将对象复制到配置为使用 [数据库副本](https://technet.microsoft.com/library/mt608546.aspx)的管理点。  


 **辅助站点：**  

 站点数据库可以使用 SQL Server 完整安装的默认实例，或 SQL Server Express  

 SQL Server 必须位于站点服务器计算机上  

##  <a name="a-namebkmksqlversionsa-supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> 支持的 SQL Server 版本  
 在具有多个站点的层次结构中，不同站点可以使用不同版本的 SQL Server 来托管站点数据库，只要你使用 Configuration Manager 支持的 SQL Server 版本。  

 System Center Configuration Manager 1511 及更高版本支持以下版本的 SQL Server。  

> [!IMPORTANT]  
>  为管理中心站点上的数据库使用 SQL Server Standard 会限制层次结构可支持的客户端总数。 请参阅[调整大小和扩展数量](../../../core/plan-design/configs/size-and-scale-numbers.md)。

### <a name="sql-server-2016---standard-enterprise"></a>SQL Server 2016 - 标准版、企业版  

支持与 1606 版配合使用。   
可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：  

-   管理中心站点  
-   主站点  
-   辅助站点  


### <a name="sql-server-2014-sp2---standard-enterprise"></a>SQL Server 2014 SP2 – 标准版、企业版  

支持与 1511 版及更高版本配合使用。  
可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：  

-   管理中心站点  
-   主站点  
-   辅助站点  



### <a name="sql-server-2014-sp1---standard-enterprise"></a>SQL Server 2014 SP1 - 标准版、企业版  

支持与 1511 版及更高版本配合使用。  
 可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：  

-   管理中心站点  
-   主站点  
-   辅助站点  


### <a name="sql-server-2012-sp3---standard-enterprise"></a>SQL Server 2012 SP3 - 标准版、企业版  

支持与 1511 版及更高版本配合使用。  
 可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：  

-   管理中心站点  
-   主站点  
-   辅助站点  


### <a name="sql-server-2012-sp2---standard-enterprise"></a>SQL Server 2012 SP2 - 标准版、企业版  

支持与 1511 版及更高版本配合使用。  
 可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：  

-   管理中心站点  
-   主站点  
-   辅助站点  


### <a name="sql-server-2008-r2-sp3---standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3 – 标准版、企业版、数据中心版  

支持与 1511 版及更高版本配合使用。    
可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：  

-   管理中心站点  
-   主站点  
-   辅助站点  

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
支持与 1606 版配合使用。  
可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：
-   辅助站点

### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2  
支持与 1511 版及更高版本配合使用。  
可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：  

-   辅助站点  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1  
 支持与 1511 版及更高版本配合使用。   
 可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：  

-   辅助站点  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
支持与 1511 版及更高版本配合使用。   
可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：  

-   辅助站点  

### <a name="sql-server-2012-express-sp2"></a>SQL Server 2012 Express SP2  
 支持与 1511 版及更高版本配合使用。  
 可将此版本的 SQL Server 与以下产品的非最低累计更新版本一起使用：  

-   辅助站点  

##  <a name="a-namebkmksqlconfiga-required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> SQL Server 所需的配置  
 用于站点数据库（包括 SQL Server Express）的 SQL Server 的所有安装都需要以下内容。 当 Configuration Manager 将 SQL Server Express 作为辅助站点安装的一部分进行安装时，将为你自动设置这些配置。  

 **SQL Server 体系结构版本：**  
 Configuration Manager 需要 64 位版本的 SQL Server 以托管站点数据库。  

 **数据库排序规则：**  
 在每个站点上，用于站点和站点数据库的 SQL Server 实例必须使用以下排序规则： **SQL_Latin1_General_CP1_CI_AS**。  

 Configuration Manager 支持对此排序规则的两种例外情况，以满足在 GB18030 中定义的标准，以便在中国使用。 有关详细信息，请参阅 [System Center Configuration Manager 的国际支持](../../../core/plan-design/hierarchy/international-support.md)。  

 **SQL Server 功能：**  
 仅“数据库引擎服务”  功能是每个站点服务器所必需的。  

 Configuration Manager 数据库复制不需要“SQL Server 复制”功能。 但是，如果要使用 [System Center Configuration Manager 管理点的数据库副本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)，则需要进行此 SQL Server 配置。  

 **Windows 身份验证：**  
 Configuration Manager 需要“Windows 身份验证”来验证与数据库的连接。  

 **SQL Server 实例：**  
 必须为每个站点使用专用的 SQL Server 实例。 可以为 **命名实例** 或 **默认实例**。  

 **SQL Server 内存：**  
 通过使用 SQL Server Management Studio 和设置“服务器内存选项”下的“最小服务器内存”设置来保留 SQL Server 的内存。 有关如何设置固定的内存量的详细信息，请参阅 [如何：设置固定的内存量 (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759)。  

-   **与站点服务器安装在同一台计算机上数据库服务器：** - 将 SQL Server 的内存限制为可用可寻址系统内存的 50% 到 80%。  

-   **专用的数据库服务器（远离站点服务器）：** -  将用于 SQL Server 的内存限制为可用可寻址的系统内存的 80% 到 90%。  

-   **使用中的每个 SQL Server 实例的缓冲池的内存预留：**  

    -   管理中心站点：至少 8 千兆字节 (GB)  
    -   主站点：至少 8 千兆字节 (GB)  
    -   辅助站点：至少 4 千兆字节 (GB)  

 **SQL 嵌套触发器：**  

 必须启用[SQL 嵌套触发器](http://go.microsoft.com/fwlink/?LinkId=528802) 。  

 **SQL Server CLR 集成**  

  站点数据库要求启用 SQL Server 公共语言运行时 (CLR)。 这在 Configuration Manager 安装时会自动启用。 有关 CLR 的详细信息，请参阅 [SQL Server CLR 集成简介](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx)  

##  <a name="a-namebkmkoptionala-optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> SQL Server 可选配置  
 以下配置对使用完整 SQL Server 安装的每个数据库是可选的。  

 **SQL Server 服务：**  
 你可以将 SQL Server 服务配置为使用以下账户运行：  

-   **域本地用户** 帐户：  

    -   这是最佳做法，并且可能会要求你手动注册该帐户的服务主体名称 (SPN)。  

-   运行 SQL Server 的计算机的**本地系统** 帐户：  

    -   使用本地系统帐户简化配置过程。  
    -   使用本地系统帐户时，Configuration Manager 将自动注册 SQL Server 服务的 SPN。  
    -   请注意，为 SQL Server 服务使用本地系统帐户不是 SQL Server 最佳做法。  

当 SQL Server 不使用该计算机的本地系统帐户运行 SQL Server 服务时，必须配置帐户的服务主体名称 (SPN)，该帐户在 Active Directory 域服务中运行 SQL Server 服务。 （当使用系统帐户时，将为你自动注册 SPN）。

有关站点数据库的 SPN 的信息，请参阅  [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) 主题中的 [Manage the SPN for the site database server](../../../core/servers/manage/modify-your-infrastructure.md) 。  

有关如何更改 SQL 服务使用的帐户的信息，请参阅 [如何：更改 SQL Server 的服务启动帐户 (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkId=237661)。  

**SQL Server Reporting Services：**  
需要安装使你可以运行报表的 Reporting Services 点。  

**SQL Server 端口：**  
对于与 SQL Server 数据库引擎的通信和站点间复制，可以使用默认的 SQL Server 端口配置，也可以指定自定义端口：  

-   **站点间通信** 使用 SQL Server Service Broker，它默认使用端口 TCP 4022。  
-   SQL Server 数据库引擎与各种 Configuration Manager 站点系统角色之间的“站点内通信”默认使用端口 TCP 1433。 下列站点系统角色直接与 SQL Server 数据库进行通信：  

    -   管理点  
    -   SMS 提供程序计算机  
    -   Reporting Services 点  
    -   站点服务器  

在 SQL Server 托管多个站点中的数据库时，每个数据库都必须使用独立的 SQL Server 实例，而且每个实例必须被配置为使用一组唯一的端口。  

> [!WARNING]  
>  Configuration Manager 不支持动态端口。 由于 SQL Server 命名实例默认情况下使用动态端口来连接到数据库引擎，因此，在使用命名实例时，必须手动配置要用于站点内通信的静态端口。  

如果在运行 SQL Server 的计算机上启用防火墙，请确保将防火墙配置为不阻止你的部署使用的端口，以及位于与 SQL Server 通信的计算机之间的网络上任何位置处的端口。  

有关演示如何将 SQL Server 配置为使用指定的端口的示例，请参阅 SQL Server TechNet 库中的 [如何：将服务器配置为侦听特定的 TCP 端口 (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) 。  



<!--HONumber=Nov16_HO1-->


