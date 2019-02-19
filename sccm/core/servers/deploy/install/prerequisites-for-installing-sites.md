---
title: 站点的先决条件
titleSuffix: Configuration Manager
description: 了解安装不同类型的 Configuration Manager 站点所需的先决条件。
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a56739eee4d116014f89b3a7e7835e3e87a62ac
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124582"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>安装 Configuration Manager 站点的先决条件

适用范围：System Center Configuration Manager (Current Branch)

在开始站点安装之前，先了解安装不同类型的 Configuration Manager 站点的先决条件。



## <a name="primary-sites-and-the-central-administration-site"></a>主站点和管理中心站点

以下先决条件适用于安装以下类型之一：
- 管理中心站点作为层次结构的第一个站点
- 独立主站点
- 子主站点

如果在层次结构扩展期间安装管理中心站点，请参阅[扩展独立主站点](#bkmk_expand)。


###  <a name="bkmk_PrereqPri"></a>安装主站点或管理中心站点的先决条件  

- 安装站点的用户帐户必须具有以下权限：  

    - 下列服务器上的管理员权限：  
        - 站点服务器  
        - 托管站点数据库的每个服务器  
        - 站点的每个 SMS 提供程序实例  

    - 托管站点数据库的 SQL Server 实例上的 **Sysadmin**  

        > [!IMPORTANT]  
        >  Configuration Manager 安装完成后，运行安装程序的用户帐户和站点服务器计算机帐户都必须保留 SQL Server 的 sysadmin 权限。 请勿从这些帐户中删除 sysadmin 权限。  

- 如果安装的是主站点，则需要下列附加权限：  

    - 安装初始管理点和分发点的其他服务器上的管理员权限（若不在站点服务器上）  

- 如果在管理中心站点下安装新的子级主站点，需要下列附加权限：  

    - 托管管理中心站点的服务器上的管理员权限  

    - Configuration Manager 中基于角色的管理权限，这些权限相当于**基础结构管理员**或**完全权限管理员**的安全角色  

- 使用正确的安装源文件，并从该位置运行安装程序。 若要了解用于安装不同站点类型的适当源文件，请参阅[不同类型站点的安装选项](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options)。  

- 站点服务器必须可通过以下某种方式访问更新的 Microsoft 安装程序文件：  

    - 开始安装前，可在本地网络上下载这些文件并存储其副本。 有关详细信息，请参阅[安装程序下载程序](/sccm/core/servers/deploy/install/setup-downloader)。  

    - 如果这些文件的本地副本不可用，则站点服务器必须具有 Internet 访问权限。 它在安装过程中从 Microsoft 下载这些文件。  

- 站点服务器和站点数据库服务器必须满足所有先决条件配置。 在启动 Configuration Manager 安装程序之前，可[手动运行必备组件检查程序](/sccm/core/servers/deploy/install/prerequisite-checker)以识别并修复问题。  


### <a name="bkmk_expand"></a> 扩展独立主站点的先决条件

在你将独立主站点扩展到带管理中心站点的层次结构之前，独立主站点必须满足下列先决条件：

#### <a name="source-file-version-matches-site-version"></a>源文件版本与站点版本匹配
使用 CD.Latest 文件夹中的介质安装与独立主站点的版本匹配的新管理中心站点。 要确保版本匹配，请使用在独立主站点上的 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)中找到的源文件。 

若要深入了解用于安装不同站点的适当源文件，请参阅[不同类型站点的安装选项](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options)。  

#### <a name="stop-active-migration-from-another-hierarchy"></a>停止从另一个层次结构进行活动迁移
无法将独立主站点配置为从另一 Configuration Manager 层次结构迁移数据。 停止从其他 Configuration Manager 层次结构活动迁移到独立主站点，并删除迁移的所有配置。 这些配置包括： 
- 尚未完成的迁移作业  
- 数据收集  
- 活动源层次结构的配置  

此配置是必需的，因为 Configuration Manager 从层次结构的顶层站点迁移数据。 扩展独立主站点时，迁移配置不会传输到管理中心站点。  

扩展独立主站点后，如果在主站点上重新配置迁移，管理中心站点将执行迁移操作。 

若要深入了解如何配置迁移，请参阅[配置源层次结构和迁移源站点](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration)。  

#### <a name="computer-account-as-administrator"></a>管理员身份的计算机帐户
承载新管理中心站点的服务器的计算机帐户必须是独立主站点服务器上“管理员”组的成员。 

若要成功扩展独立主站点，新管理中心站点的计算机帐户必须具有独立主站点的“管理员”权限。 仅在站点扩展期间需要。 站点扩展完成后，可从主站点的用户组中删除该帐户。  

#### <a name="installation-account-permissions"></a>安装帐户权限
运行 Configuration Manager 安装程序以安装新管理中心站点的用户帐户必须在独立主站点上具有基于角色的管理权限。

若要在站点扩展期间安装管理中心站点，必须在独立主站点的基于角色的管理中，将运行安装程序以安装管理中心站点的用户帐户定义为“完全权限管理员”或“基础结构管理员”。  

#### <a name="top-level-site-roles"></a>顶层站点角色
必须先从独立主站点中卸载下列站点系统角色才能扩展站点：

- 资产智能同步点  
- Endpoint Protection 点  
- 服务连接点  

Configuration Manager 仅在层次结构的顶层站点上支持这些角色。 必须先卸载这些站点系统角色才能扩展独立主站点。 在扩展站点后，在管理中心站点重新安装这些站点系统角色。  

所有其他站点系统角色仍然可以安装在主站点中。  

#### <a name="open-the-sql-server-service-broker-port"></a>打开 SQL Server Service Broker 端口
在独立主站点和管理中心站点的服务器之间，SQL Server Service Broker (SSB) 的网络端口必须打开。  

若要在管理中心站点和主站点之间成功复制数据，Configuration Manager 需要在两个站点之间打开端口以供 SSB 使用。 在安装管理中心站点和扩展独立主站点时，先决条件检查不会验证你为 SSB 指定的端口是否在主站点上打开。  

#### <a name="known-issues-with-azure-services"></a>Azure 服务的已知问题
将以下任一 Azure 服务与 Configuration Manager 配合使用，扩展站点后，删除指向该服务的连接并重新创建连接。

- [Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  
- [升级就绪情况](/sccm/core/clients/manage/upgrade/upgrade-readiness)  
- [适用于企业的 Microsoft Store](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

请执行以下步骤，解决此问题：
 1. 在 Configuration Manager 控制台中，从“Azure 服务”节点删除 Azure 服务。  

 2. 在 Azure 门户中，从“Azure Active Directory 租户”节点删除与该服务关联的租户。 此操作还会删除与该服务关联的 Azure AD Web 应用。  

 3. 重新配置与 Azure 服务的连接，用于 Configuration Manager。  



## <a name="bkmk_secondary"></a>辅助站点

以下是安装辅助站点的先决条件：

- 在 Configuration Manager 控制台中配置辅助站点安装的管理员必须具有基于角色的管理权限，且这些权限相当于“基础结构管理员”或“完全权限管理员”的安全角色。  

- 父级主站点的计算机帐户必须是辅助站点服务器上的管理员。  

- 当辅助站点使用以前安装的 SQL Server 实例承载辅助站点数据库时：  

    - 父级主站点的计算机帐户必须具有对辅助站点服务器上 SQL Server 实例的 sysadmin 权限。  

    - 辅助站点服务器计算机的本地系统帐户必须具有对辅助站点服务器上 SQL Server 实例的 sysadmin 权限。  

        > [!IMPORTANT]  
        >  Configuration Manager 安装完成后，两个帐户都必须保留 SQL Server 的 sysadmin 权限。 请勿从这些帐户中删除 sysadmin 权限。  

- 辅助站点服务器必须满足所有先决条件配置。 这些配置包括 SQL Server 以及管理点和分发点的默认站点系统角色。  
