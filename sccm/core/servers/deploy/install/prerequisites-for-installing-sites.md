---
title: "站点的先决条件 | System Center Configuration Manager"
description: "了解安装不同类型的 System Center Configuration Manager 站点所需的不同先决条件。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bf3b1e4d87a972f530590bf94e38a5ec66c4fc9a

---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>安装 System Center Configuration Manager 站点的先决条件

*适用范围：System Center Configuration Manager (Current Branch)*


以下部分提供有关安装不同类型的 System Center Configuration Manager 站点所需的不同先决条件的详细信息。



## <a name="primary-sites-and-the-central-administration-site"></a>主站点和管理中心站点
以下先决条件适用于将管理中心站点安装为层次结构、独立主站点或子主站点的第一个站点。 如果将管理中心站点作为层次扩展方案的一部分进行安装，请参阅本主题中的[扩展独立主站点](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand
)。

####  <a name="a-namebkmkprereqpria-prerequisites-to-install-a-primary-site-or-central-administration-site"></a><a name="bkmk_PrereqPri"></a> 安装主站点或管理中心站点的先决条件  

-   将安装站点的用户必须具有以下权限：  

    -   站点服务器计算机上的**本地管理员** 权限  

    -   将托管**站点数据库** 或站点的 **本地管理员** 实例的每台计算机上的 **本地管理员**  

    -   托管站点数据库的 SQL Server 实例上的**Sysadmin**  

        > [!IMPORTANT]  
        >  安装完成后，运行安装程序的用户帐户和站点服务器计算机帐户必须保留 SQL Server 的 sysadmin 权限。 不支持从这些帐户中删除 sysadmin 权限。  

-   安装主站点时需要下列附加权限：  
    -  将在其中安装初始管理点和分发点的其他计算机上的**本地管理员** 权限（如果不在站点服务器上）。  

-   在管理中心站点下面安装新的子级主站点时，需要下列附加权限：  

    -   托管管理中心站点的计算机上的**本地管理员** 权限  

    -   Configuration Manager 中基于角色的管理权限，这些权限相当**基础结构管理员**或**完全权限管理员**的安全角色。  

-   必须使用正确的安装媒体（源文件），并从该位置运行安装程序。 有关用于安装不同站点的正确源文件的信息，请参阅[安装站点的准备工作](../../../../core/servers/deploy/install/prepare-to-install-sites.md)主题中的[安装不同类型站点的选项](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options)。

-   站点服务器计算机必须具有对 Microsoft 已更新的安装程序文件的访问权限：
    -  在开始安装之前，可以通过使用[安装程序下载程序](../../../../core/servers/deploy/install/setup-downloader.md)在本地网络上下载并存储这些文件的副本
    -  如果这些文件的本地副本不可用，站点服务器必须具有 Internet 访问权限，以便其可以在安装过程中从 Microsoft 下载这些文件

  - 在扩展已安装“服务连接点”站点系统角色的独立主站点之前，必须卸载“服务连接点”。 层次结构中仅允许存在此角色的一个实例，并且只允许在层次结构的顶层站点使用。 你将有机会在管理中心站点的安装过程中重新安装角色。
  - 站点服务器和站点数据库计算机必须满足所有先决条件配置。 在启动安装程序之前，可以[手动运行先决条件检查程序](../../../../core/servers/deploy/install/prerequisite-checker.md)以识别并修复问题。  


## <a name="a-namebkmkexpanda-expanding-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> 扩展独立主站点
在你将独立主站点扩展到带管理中心站点的层次结构之前，独立主站点必须满足下列先决条件：


-   **必须安装与独立主站点的版本匹配的新管理中心站点安装媒体（源文件）：**  
     为确保版本匹配，请使用在独立主站点上的 [CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) 文件夹中找到的源文件来安装新站点。

     有关用于安装不同站点的正确源文件的详细信息，请参阅[安装站点的准备工作](../../../../core/servers/deploy/install/prepare-to-install-sites.md)主题中的[安装不同类型站点的选项](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options)。


-   **无法将独立主站点配置为从另一 Configuration Manager 层次结构迁移数据：**  

     必须停止从其他 Configuration Manager 层次结构活动迁移到独立主站点，并删除迁移的所有配置。 这包括尚未完成的迁移作业、数据收集和活动源层次结构的配置。  

     这是必须的，因为迁移操作由层次结构的顶层站点执行，并且在扩展独立主站点时，迁移配置不会传输到管理中心站点。  

     在你扩展独立主站点后，如果在主站点上重新配置迁移，则它将是执行与迁移相关操作的管理中心站点。 有关如何配置迁移的详细信息，请参阅[配置源层次结构和源站点以迁移到 System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)。  

-   **承载新管理中心站点的计算机的计算机帐户必须是独立主站点上“管理员”组的成员：**  

     若要成功扩展独立主站点，新管理中心站点的计算机帐户必须是独立主站点的“管理员”  组的成员。 仅在站点扩展过程中才有此要求，在站点扩展完成后，可以将该帐户从主站点上的组中删除。  

-   **在独立主站点上，必须向运行安装程序来安装新管理中心站点的用户帐户授予基于角色的管理权限：**  

     要在站点扩展方案中安装管理中心站点，必须在独立主站点的基于角色的管理中将运行安装程序来安装管理中心站点的用户帐户定义为“完全权限管理员”  或“基础结构管理员” 。  

-   **必须先从独立主站点中卸载下列站点系统角色才能扩展站点：**  

    -   资产智能同步点  

    -   Endpoint Protection 点  

    -   服务连接点  

     仅在层次结构的顶层站点中才会支持这些站点系统角色。 因此，必须先卸载这些站点系统角色才能扩展独立主站点。 在扩展站点后，你可以在管理中心站点重新安装这些站点系统角色。  

    所有其他站点系统角色仍然可以安装在主站点中。  

-   **在独立主站点和将安装管理中心站点的计算机之间，SQL Server Service Broker 的端口必须打开：**  

     若要在管理中心站点和主站点之间成功复制数据，Configuration Manager 需要供 SQL Server Service Broker 使用的端口在两个站点之间打开。 在安装管理中心并扩展独立主站点时，先决条件检查不会确定你为 SQL Server Service Broker 指定的端口在主站点上已打开。  


## <a name="a-namebkmksecondarya-secondary-sites"></a><a name="bkmk_secondary"></a> 辅助站点
以下是安装辅助站点的先决条件：
-   在 Configuration Manager 控制台中配置辅助站点安装的管理用户必须具有相当于**基础结构管理员**或**完全权限管理员**的安全角色的基于角色的管理权限。  

-   父级主站点的计算机帐户必须是辅助站点服务器计算机上的 **本地管理员** 。  

-   当辅助站点使用以前安装的 SQL Server 实例承载辅助站点数据库时：  

    -   父级主站点的 **计算机帐户** 必须具有对辅助站点服务器计算机上 SQL Server 实例的 **sysadmin** 权限。  

    -   辅助站点服务器计算机的 **本地系统** 帐户必须具有对辅助站点服务器计算机上 SQL Server 实例的 **sysadmin** 权限。  

        > [!IMPORTANT]  
        >  安装完成后，两个帐户必须保留 SQL Server 的 sysadmin 权限。 不支持从这些帐户中删除 sysadmin 权限。  

-   辅助站点服务器计算机必须满足所有必备配置，其中包括 SQL Server 及管理点和分发点的默认站点系统角色。  



<!--HONumber=Nov16_HO1-->


