---
title: "站点的先决条件 | Microsoft Docs"
description: "了解安装不同类型的 System Center Configuration Manager 站点所需的先决条件。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d46a8b66ace45d25da9d86f2e91b19ae1d6875ab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>安装 System Center Configuration Manager 站点的先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

在开始站点安装之前，最好先了解安装不同类型的 System Center Configuration Manager 站点的先决条件。

## <a name="primary-sites-and-the-central-administration-site"></a>主站点和管理中心站点
以下先决条件适用于将管理中心站点安装为层次结构的第一个站点、安装独立主站点或子主站点。 如果在层次结构扩展期间安装管理中心站点，请参阅本主题中的[扩展独立主站点](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)。

###  <a name="bkmk_PrereqPri"></a>安装主站点或管理中心站点的先决条件  

-   安装站点的用户帐户必须具有以下权限：  

    -   站点服务器计算机上的**管理员**权限  
    -   各计算机上将托管**站点数据库**或站点的 **SMS 提供程序**实例的**管理员**  
    -   托管站点数据库的 SQL Server 实例上的 **Sysadmin**  

        > [!IMPORTANT]  
        >  安装完成后，运行安装程序的用户帐户和站点服务器计算机帐户都必须保留 SQL Server 的 sysadmin 权限。 不要从这些帐户中删除 sysadmin 权限。  

-   如果安装的是主站点，则需要下列附加权限：  
    -  要安装初始管理点和分发点的其他计算机上的**管理员**权限（若不在站点服务器上）  

-   如果在管理中心站点下安装新的子级主站点，需要下列附加权限：  

    -   托管管理中心站点的计算机上的**管理员**权限  

    -   Configuration Manager 中基于角色的管理权限，这些权限相当于**基础结构管理员**或**完全权限管理员**的安全角色  

-   必须使用正确的安装介质（源文件），并从该位置运行安装程序。 若要了解用于安装不同站点类型的适当源文件，请参阅[安装站点的准备工作](../../../../core/servers/deploy/install/prepare-to-install-sites.md)主题中的[不同类型站点的安装选项](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options)。

-   站点服务器计算机必须可通过以下某种方式访问更新的 Microsoft 安装程序文件：
    -  开始安装前，可通过[安装程序下载程序](../../../../core/servers/deploy/install/setup-downloader.md)在本地网络上下载这些文件并存储其副本。
    -  如果这些文件的本地副本不可用，站点服务器必须具有 Internet 访问权限，以便可在安装过程中从 Microsoft 下载这些文件。

- 在扩展安装了服务连接点站点系统角色的独立主站点之前，必须卸载服务连接点。 层次结构中仅允许存在此角色的一个实例，并且只允许在层次结构的顶层站点使用。 你将有机会在管理中心站点的安装过程中重新安装角色。
- 站点服务器和站点数据库计算机必须满足所有先决条件配置。 在启动安装程序之前，可[手动运行必备组件检查程序](../../../../core/servers/deploy/install/prerequisite-checker.md)以识别并修复问题。  


### <a name="bkmk_expand"></a> 扩展独立主站点的先决条件
在你将独立主站点扩展到带管理中心站点的层次结构之前，独立主站点必须满足下列先决条件：

-   **必须使用与独立主站点版本匹配的 CD.Latest 文件夹（其中包含源文件）中的介质来安装新的管理中心站点安装**

 要确保版本匹配，请使用独立主站点上 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)中找到的源文件。

 若要详细了解用于安装不同站点的适当源文件，请参阅[安装站点的准备工作](../../../../core/servers/deploy/install/prepare-to-install-sites.md)主题中的[不同类型站点的安装选项](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options)。


-   **无法将独立主站点配置为从另一 Configuration Manager 层次结构迁移数据**  

     必须停止从其他 Configuration Manager 层次结构活动迁移到独立主站点，并删除迁移的所有配置。 这包括尚未完成的迁移作业、数据收集以及活动源层次结构的配置。  

     这是必须的，因为迁移操作由层次结构的顶层站点执行，并且在扩展独立主站点时，迁移配置不会传输到管理中心站点。  

     扩展独立主站点后，如果在主站点上重新配置迁移，管理中心站点将执行与迁移相关的操作。 若要深入了解如何配置迁移，请参阅[配置源层次结构和源站点以迁移到 System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)。  

-   **要托管新管理中心站点的计算机的计算机帐户必须隶属于独立主站点上的“管理员”用户组**  

     若要成功扩展独立主站点，新管理中心站点的计算机帐户必须具有独立主站点的“管理员”权限。 仅在站点扩展期间需要。 站点扩展完成后，可从主站点的用户组中删除该帐户。  

-   **运行安装程序以安装新管理中心站点的用户帐户必须在独立主站点上具有基于角色的管理权限**  

     若要在站点扩展期间安装管理中心站点，必须在独立主站点的基于角色的管理中，将运行安装程序以安装管理中心站点的用户帐户定义为“完全权限管理员”或“基础结构管理员”。  

-   **必须先从独立主站点中卸载下列站点系统角色才能扩展站点：**  

    -   资产智能同步点  
    -   Endpoint Protection 点  
    -   服务连接点  

   仅在层次结构的顶层站点中才会支持这些站点系统角色。 因此，必须先卸载这些站点系统角色才能扩展独立主站点。 在扩展站点后，你可以在管理中心站点重新安装这些站点系统角色。  

    所有其他站点系统角色仍然可以安装在主站点中。  

-   **在独立主站点和要安装管理中心站点的计算机之间，SQL Server Service Broker (SSB) 的端口必须打开：**  

     若要在管理中心站点和主站点之间成功复制数据，Configuration Manager 需要在两个站点之间打开端口以供 SSB 使用。 在安装管理中心站点并扩展独立主站点时，先决条件检查不会验证为 SSB 指定的端口是否在主站点上打开。  

**配置 Azure 服务后的已知问题：**  
将以下任一 Azure 服务与 Configuration Manager 配合使用，并计划扩展站点时，扩展站点后必须删除指向该服务的连接并重新创建连接。

服务：  
-       [Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)   (OMS)
-       [升级就绪情况](/sccm/core/clients/manage/upgrade/upgrade-analytics)
-       [适用于企业的 Windows 应用商店](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)

请执行以下步骤，解决此问题：
 1.    在 Configuration Manager 控制台中，从 Azure 服务节点删除 Azure 服务。
 2.    在 Azure 门户中，从 Azure Active Directory 租户节点删除与该服务关联的租户。  这还会删除与该服务关联的 Azure AD Web 应用。  
 3.   重新配置与 Azure 服务的连接，用于 Configuration Manager。


## <a name="bkmk_secondary"></a>辅助站点
以下是安装辅助站点的先决条件：
-   在 Configuration Manager 控制台中配置辅助站点安装的管理员必须具有基于角色的管理权限，且这些权限相当于“基础结构管理员”或“完全权限管理员”的安全角色。  
-   父级主站点的计算机帐户必须是辅助站点服务器计算机上的**管理员**。  
-   当辅助站点使用以前安装的 SQL Server 实例承载辅助站点数据库时：  

    -   父级主站点的 **计算机帐户** 必须具有对辅助站点服务器计算机上 SQL Server 实例的 **sysadmin** 权限。  

    -   辅助站点服务器计算机的 **本地系统** 帐户必须具有对辅助站点服务器计算机上 SQL Server 实例的 **sysadmin** 权限。  

        > [!IMPORTANT]  
        >  安装完成后，两个帐户都必须保留 SQL Server 的 sysadmin 权限。 不要从这些帐户中删除 sysadmin 权限。  

-   辅助站点服务器计算机必须满足所有必备配置，其中包括 SQL Server 及管理点和分发点的默认站点系统角色。  
