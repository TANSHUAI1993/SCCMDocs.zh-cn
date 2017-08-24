---
title: "卸载站点 | Microsoft Docs"
description: "卸载 System Center Configuration Manager 站点时，请使用这些详细信息作为指南。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6ad06753dc0e1d0958f7131afbf3ecb75eecb2e3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中卸载站点和层次结构

*适用范围：System Center Configuration Manager (Current Branch)*

如果需要卸载 System Center Configuration Manager 站点，请使用以下详细信息作为指南。  

要取消标记具有多个站点的层次结构，删除的顺序非常重要。 从卸载层次结构底部的站点开始，然后向上移动：  

1.  删除连接到主站点的辅助站点。  
2.  删除主站点。
3.  删除所有主站点之后，即可以卸载管理中心站点。  


##  <a name="BKMK_RemoveSecondarysite"></a> 从层次结构中删除辅助站点  
无法移动辅助站点或将辅助站点重新分配到新的父主站点。 若要从层次结构中删除，必须将辅助站点从其直接父站点中删除。 在 Configuration Manager 控制台中使用删除辅助站点向导来删除辅助站点。 在删除辅助站点时，必须选择要将其删除还是卸载：  

-   **卸载辅助站点**。 使用此选项以删除可从网络中访问的正常运行的辅助站点。 此选项从辅助站点服务器中卸载 Configuration Manager，然后从 Configuration Manager 站点层次结构中删除站点及其资源的所有相关信息。 如果 Configuration Manager 在辅助站点安装过程中安装了 SQL Server Express，则 Configuration Manager 将在卸载辅助站点时卸载 SQL Express。 如果 SQL Server Express 是在安装辅助站点之前安装的，则 Configuration Manager 不会卸载 SQL Server Express。  

-   **删除辅助站点**。 如果满足以下条件之一，则使用此选项：  

    -   辅助站点安装失败  
    -   辅助站点在卸载之后仍然显示在 Configuration Manager 控制台中

    此选项将从 Configuration Manager 层次结构中删除有关站点及其资源的所有信息，但保留安装在辅助站点服务器上的 Configuration Manager。  

    > [!NOTE]  
    >  也可使用层次结构维护工具和 **/DELSITE** 选项来删除辅助站点。 有关详细信息，请参阅 [System Center Configuration Manager 的层次结构维护工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>卸载或删除辅助站点  

1.  验证运行安装程序的管理用户是否具有以下安全权限：  

    -   辅助站点计算机上的管理权限  
    -   主站点（如果为远程）的远程站点数据库服务器上的本地管理员权限  
    -   父主站点上的“基础结构管理员”或“完全权限管理员”安全角色  
    -   辅助站点的站点数据库上的 Sysadmin 权限  

2.  在 Configuration Manager 控制台中，选择“管理”。  
3.  在“管理”工作区中，展开“站点配置”，然后选择“站点”。  
4.  选择要删除的辅助站点服务器。  
5.  在“主页”选项卡上的“站点”组中，选择“删除”。  
6.  在“常规”  页上，选择是卸载还是删除辅助站点，然后单击“下一步” 。  
7.  在“摘要”页上验证设置，然后选择“下一步”。  
8.  在“完成”页上，选择“关闭”退出向导。  

##  <a name="BKMK_UninstallPrimary"></a> 卸载主站点  
可以运行 Configuration Manager 安装程序来卸载没有关联辅助站点的主站点。 在卸载主站点之前，请考虑下列事项：  

-   如果 Configuration Manager 客户端位于站点上配置的边界内，并且主站点是 Configuration Manager 层次结构的一部分，请考虑在卸载主站点之前将边界添加到层次结构中的另一个主站点。  
-   如果主站点服务器不再可用，你必须使用管理中心站点上的层次结构维护工具来从站点数据库中删除主站点。 有关详细信息，请参阅 [System Center Configuration Manager 的层次结构维护工具 (Preinst.exe)](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md)。  

使用下列过程来卸载主站点。  

#### <a name="to-uninstall-a-primary-site"></a>要卸载主站点  

1.  验证运行安装程序的管理用户是否具有以下安全权限：  

    -   管理中心站点服务器上的本地管理员权限  
    -   管理中心站点（如果为远程）的远程站点数据库服务器上的本地管理员权限
    -   管理中心站点的站点数据库的 Sysadmin 权限  
    -   主站点计算机上的本地管理员权限  
    -   主站点（如果为远程）的远程站点数据库服务器上的本地管理员权限  
    -   管理中心站点上与“基础结构管理员”或“完全权限管理员”安全角色关联的用户名  

2.  通过使用以下方法之一在主站点服务器上启动 Configuration Manager 安装程序：  

    -   在“开始”上，选择“Configuration Manager 安装程序”。  
    -   打开 &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64 中的 Setup.exe。  
    -   打开 &lt;*ConfigMgrInstallationPath*>\BIN\X64 中的 Setup.exe。  

3.  在“开始之前”页面上，选择“下一步”。  
4.  在“入门”页上，选择“卸载 Configuration Manager 站点”，然后选择“下一步”。  
5.  在“卸载 Configuration Manager 站点”中，指定是否从主站点服务器中删除站点数据库，以及是否删除 Configuration Manager 控制台。 默认情况下，安装程序会删除这两项。  

    > [!IMPORTANT]  
    >  如果辅助站点附加到主站点，则你必须删除辅助站点，然后才能卸载主站点。  

6.  选择“是”以确认卸载 Configuration Manager 主站点。  

##  <a name="BKMK_UninstallPrimaryDistViews"></a> 卸载配置有分布式视图的主站点  
 针对为指向管理中心站点的复制链接打开了分布式视图的子主站点，在卸载此类子主站点之前，必须在层次结构中关闭分布式视图。 使用以下信息在卸载主站点之前关闭分布式视图。  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>要卸载配置为具有分布式视图的主站点  

1.  在卸载任何主站点之前，必须在管理中心站点和主站点之间的层次结构的每个链接上关闭分布式视图。  
2.  在每个链接上关闭分布式视图之后，请确认主站点中的数据在管理中心站点上完成重新初始化。 若要监视数据的初始化，请在 Configuration Manager 控制台的“监视”工作区中，查看“数据库复制”节点上的链接。  
3.  在数据使用管理中心站点成功重新初始化后，你可以卸载主站点。 若要卸载主站点，请参阅[卸载主站点](#BKMK_UninstallPrimary)。  
4.  成功卸载主站点后，可以在指向主站点的链接上重新配置分布式视图。  

    > [!IMPORTANT]  
    >  如果在卸载主站点后才在每个站点上关闭分布式视图，或者之后才在管理中心站点上成功重新初始化数据，则主站点和管理中心站点之间的数据复制可能会失败。 在这种情况下，必须为站点层次结构中的每个链接关闭分布式视图，然后，在数据使用管理中心站点成功重新初始化后，你可以重新配置分布式视图。  

##  <a name="BKMK_UninstallCAS"></a> 卸载管理中心站点  
 可以运行 Configuration Manager 安装程序卸载没有子主站点的管理中心站点。 使用以下过程来卸载管理中心站点。  

#### <a name="to-uninstall-a-central-administration-site"></a>要卸载管理中心站点  

1.  验证运行安装程序的管理用户是否具有以下安全权限：  

    -   管理中心站点服务器上的本地管理员权限  
    -   管理中心站点的站点数据库服务器上的本地管理员权限（如果站点数据库服务器未安装在站点服务器上） 

2.  通过使用以下方法之一在管理中心站点服务器上启动 Configuration Manager 安装程序：  

    -   在“开始” 上，单击“Configuration Manager 安装程序” 。  
    -   打开 &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64 中的 Setup.exe。  
    -   打开 &lt;*ConfigMgrInstallationPath*>\BIN\X64 中的 Setup.exe。  

3.  在“开始之前”页面上，选择“下一步”。  
4.  在“入门”页上，选择“卸载 Configuration Manager 站点”，然后选择“下一步”。  
5.  在“卸载 Configuration Manager 站点”中，指定是否从管理中心站点服务器中删除站点数据库，以及是否删除 Configuration Manager 控制台。 默认情况下，安装程序会删除这两项。  

    > [!IMPORTANT]  
    >  在主站点连接到管理中心站点时，若要卸载管理中心站点，必须先卸载主站点。  

6.  选择“是”以确认卸载 Configuration Manager 管理中心站点。  
