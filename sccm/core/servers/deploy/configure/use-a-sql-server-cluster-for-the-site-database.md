---
title: "SQL Server 群集 | Microsoft Docs"
description: "使用 SQL Server 群集托管 System Center Configuration Manager 站点数据库。 包括受支持选项的相关信息。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e5a001ee018e240396498d134c5e75e325eae275


---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>对 System Center Configuration Manager 站点数据库使用 SQL Server 群集。

*适用范围：System Center Configuration Manager (Current Branch)*


 可以使用 SQL Server 群集托管 System Center Configuration Manager 站点数据库。 站点数据库是 Server 群集支持的唯一站点系统角色。  

> [!NOTE]  
>  成功的配置和 SQL Server 群集要求你适应配置 SQL Server 群集，并且依赖于 SQL Server 文档库中提供的文档和过程。  

 使用群集可以提供故障转移支持，并提高站点数据库的可靠性。 但是，使用群集的站点数据库并不提供额外的处理或负载平衡优点。 事实上，由于站点服务器必须查找 SQL Server 群集的活动节点之后才会连接到站点数据库，因此可能出现性能下降。  

 安装 Configuration Manager 之前，必须准备 SQL Server 群集以支持 Configuration Manager。 （请参阅本节后面的先决条件）。  

 在 Configuration Manager 安装过程中，在 Microsoft Windows Server 群集的每个物理计算机节点上安装卷影复制服务 (VSS) 编写器，支持“备份站点服务器”维护任务。  

 安装站点后，Configuration Manager 每小时检查群集节点的更改并自动管理发现的影响 Configuration Manager 组件安装的任何更改（如节点故障转移或向 SQL Server 群集添加新节点）。  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>使用 SQL Server 故障转移群集的支持选项

-   单个实例群集  

-   多个实例配置  

-   多个活动节点  

-   命名或默认实例都受支持  

**先决条件：**  

-   站点数据库必须远离站点服务器。 （群集不能包括站点系统服务器。）  

-   必须将站点服务器的计算机帐户添加到群集中每台 Server 的“本地管理员”组。  

-   若要支持 Kerberos 身份验证，必须启用 **TCP/IP** 网络通信协议，以便每个 SQL Server 群集节点进行网络连接。 不需要**命名管道** ，但可以将其用于排除 Kerberos 身份验证问题。 在“SQL Server 网络配置”  下的“SQL Server 配置管理器” 中配置网络协议设置。  

-   如果使用 PKI，有关对站点服务器使用 SQL Server 时的特定证书要求，请参阅 &lt;Configuration Manager 的 PKI 证书要求>。  

**要考虑的限制：**  

-   **安装和配置：**  

    -   辅助站点不能使用 SQL Server 群集。  

    -   当你指定 SQL Server 群集时，用于指定站点数据库的非默认文件位置的选项不可用。  

-   **SMS 提供程序：**  

    -   不支持在 SQL Server 群集或作为群集 SQL Server 节点运行的计算机上安装 SMS 提供程序的实例。  

-   **数据复制选项：**  

    -   如果将使用“分布式视图” ，则不能使用 SQL Server 群集承载站点数据库。  

-   **备份和恢复：**  

    -   Configuration Manager 不支持对使用命名实例的 SQL Server 群集进行 DPM 备份，但支持对使用默认 SQL Server 实例的 SQL Server 群集进行 DPM 备份。  

## <a name="to-prepare-a-clustered-sql-server-instance-for-the-site-database"></a>若要为站点数据库准备群集 SQL Server 实例  

-   创建虚拟 SQL Server 群集以在现有 Windows Server 群集环境上承载站点数据库。 有关安装和配置 SQL Server 群集的具体步骤，请参阅特定于 SQL Server 版本的文档。 例如，你在使用 SQL Server 2008 R2，请参阅  [安装 SQL Server 2008 R2 故障转移群集](http://go.microsoft.com/fwlink/p/?LinkId=240231)。 如果你在使用 SQL Server 2014，请参阅 [SQL Server 故障转移群集安装](https://technet.microsoft.com/library/hh231721\(v=sql.120\).aspx)。  

-   在 SQL Server 群集中的每台计算机上，可以在不希望 Configuration Manager 在其上安装站点组件的各驱动器的根文件夹中放置名为 **NO_SMS_ON_DRIVE.SMS** 的文件。 默认情况下，Configuration Manager 将在每个物理节点上安装某些组件以支持诸如备份等操作。  

-   将站点服务器的计算机帐户添加到每台 Windows Server 群集节点计算机的“本地管理员”  组。  

-   在虚拟 SQL Server 实例中，将 **sysadmin** SQL Server 角色分配给将运行 Configuration Manager 安装程序的用户帐户。  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>若要安装使用群集 SQL Server 的新站点  
 若要安装使用群集站点数据库的站点，则按照安装站点的通常过程并执行以下变更来运行 Configuration Manager 安装程序：  

-   在“数据库信息”  页上，指定要承载站点数据库的虚拟 SQL Server 群集实例的名称。  虚拟实例将替换运行 SQL Server 的计算机的名称。  

    > [!IMPORTANT]  
    >  当输入虚拟 SQL Server 群集实例的名称时，请勿输入 Windows Server 群集创建的虚拟 Windows Server 名称。 如果使用虚拟 Windows Server 名称，则站点数据库在活动 Windows Server 群集节点的本地硬盘驱动器上安装。 这会在该节点故障时阻止成功进行故障转移。  



<!--HONumber=Dec16_HO3-->


