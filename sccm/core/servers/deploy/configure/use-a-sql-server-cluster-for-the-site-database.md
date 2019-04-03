---
title: SQL Server 群集
titleSuffix: Configuration Manager
description: 使用 SQL Server 群集托管 Configuration Manager 站点数据库
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d07005c63f0d69d57d24eac163b67c34529658cf
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2019
ms.locfileid: "58477545"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>将 SQL Server 群集用于站点数据库

适用范围：System Center Configuration Manager (Current Branch)

可以使用 SQL Server 故障转移群集托管 Configuration Manager 站点数据库。 群集提供故障转移支持，并提高站点数据库的可靠性。 但是，它不提供额外的处理或负载均衡优势。 此外，SQL Server 故障转移群集还使用共享的存储，并引入了单点故障。 由于站点服务器在连接到站点数据库之前必须查找 SQL Server 群集的活动节点，因此可能出现性能下降。  

> [!IMPORTANT]  
> SQL Server 群集是否设置成功依赖于 SQL Server 文档库中提供的文档和过程。  


安装 Configuration Manager 之前，准备 SQL Server 群集以支持 Configuration Manager。 有关详细信息，请参阅[准备群集 SQL Server 实例](#bkmk_prepare)。

Configuration Manager 安装过程中，会在 Microsoft Windows Server 群集的每个物理计算机节点上安装 Windows 卷影复制服务编写器。 此服务支持“备份站点服务器”维护任务。  

安装站点后，Configuration Manager 每小时检查一次群集节点的更改。 Configuration Manager 自动管理发现的影响其组件安装的任何更改。 例如，节点故障转移或将新节点添加到 SQL Server 群集。  



## <a name="supported-options"></a>支持的选项

用作站点数据库的 SQL Server 故障转移群集支持以下选项：

- 单个实例群集  

- 多个实例配置  

- 多个活动节点  

- 命名或默认实例  



## <a name="prerequisites"></a>先决条件

请注意以下先决条件：  

- 站点数据库必须远离站点服务器。 群集不能包括站点系统服务器。  

    > [!Note]  
    > 从版本 1810 开始，Configuration Manager 设置进程不再阻止在具有适用于故障转移群集的 Windows 角色的计算机上安装站点服务器角色。 以前你无法在站点服务器上共置站点数据库。 进行此更改后，你可以通过在被动模式下使用 SQL 群集和站点服务器创建具有更少服务器的高可用站点。 有关详细信息，请参阅[高可用性选项](/sccm/core/servers/deploy/configure/high-availability-options)。 <!--3607761, fka 1359132-->  

- 将站点服务器的计算机帐户添加到群集中每个服务器的本地“管理员”组。  

- 若要支持 Kerberos 身份验证，请启用 TCP/IP 网络通信协议，使每个 SQL Server 群集节点进行网络连接。 不需要命名管道协议，但可以将其用于排除 Kerberos 身份验证问题。 在“SQL Server 网络配置”的“SQL Server 配置管理器”中配置网络协议设置。  

- 如果使用公钥基础结构 (PKI)，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。 在将 SQL Server 群集用于站点数据库时，需要满足特定证书要求。  



## <a name="limitations"></a>限制

请考虑以下限制：  


### <a name="installation-and-configuration"></a>安装和配置

- 辅助站点不能使用 SQL Server 群集。  

- 指定 SQL Server 群集后，用于指定站点数据库的非默认文件位置的选项不可用。  


### <a name="sms-provider"></a>SMS 提供程序

不能在 SQL Server 群集上安装 SMS 提供程序的实例。 在作为群集 SQL Server 节点运行的计算机上也不受支持。  


### <a name="data-replication-options"></a>数据复制选项

如果使用“分布式视图”，则无法使用 SQL Server 群集来托管站点数据库。  


### <a name="backup-and-recovery"></a>备份和恢复

对于使用命名实例的 SQL Server 群集，Configuration Manager 不支持 Data Protection Manager (DPM) 备份。 它支持使用默认 SQL Server 实例的 SQL Server 群集上的 DPM 备份。  



## <a name="bkmk_prepare"></a>准备群集 SQL Server 实例  

下面是在准备站点数据库时要完成的主要任务：

- 创建虚拟 SQL Server 群集以在现有 Windows Server 群集环境上承载站点数据库。 有关安装和设置 SQL Server 群集的具体步骤，请参阅特定于 SQL Server 版本的文档。 有关详细信息，请参阅[创建新的 SQL Server 故障转移群集](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017)。  

- 在 SQL Server 群集的每台计算机上，在不希望 Configuration Manager 在其上安装站点组件的各驱动器的根文件夹中放置一个文件。 命名文件 `NO_SMS_ON_DRIVE.SMS`。 默认情况下，Configuration Manager 将在各物理节点上安装某些组件以支持备份等操作。  

- 将站点服务器的计算机帐户添加到每台 Windows Server 群集节点计算机的本地“管理员”组。  

- 在虚拟 SQL Server 实例中，将 sysadmin SQL Server 角色分配给运行 Configuration Manager 安装程序的用户帐户。  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>若要安装使用群集 SQL Server 的新站点  

若要安装使用群集站点数据库的站点，请按照安装站点的通常过程运行 Configuration Manager 安装程序，但执行以下例外操作：  

- 在“数据库信息”  页上，指定要承载站点数据库的虚拟 SQL Server 群集实例的名称。 虚拟实例将替换运行 SQL Server 的计算机的名称。  

    > [!IMPORTANT]  
    > 当输入虚拟 SQL Server 群集实例的名称时，请勿输入 Windows Server 群集创建的虚拟 Windows Server 名称。 如果使用虚拟 Windows Server 名称，则在活动 Windows Server 群集节点的本地硬盘驱动器上安装站点数据库。 这会在该节点故障时阻止成功进行故障转移。  
