---
title: "层次结构维护工具 | Microsoft Docs"
description: "了解层次结构维护工具的作用，以及使用它的原因。 包含命令行选项引用。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: f3ddeaadfb1418aeeaacdca47768600c86b59083
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-system-center-configuration-manager"></a>System Center Configuration Manager 的层次结构维护工具 (Preinst.exe)

*适用范围：System Center Configuration Manager (Current Branch)*

层次结构管理器服务正在运行时，层次结构维护工具 (Preinst.exe) 会将命令传递给 System Center Configuration Manager 层次结构管理器。 在安装 Configuration Manager 站点时，会自动安装层次结构维护工具。 Preinst.exe 位于站点服务器上的 \\&lt;*SiteServerName*>\SMS_&lt;*SiteCode*\bin\X64\00000409 共享文件夹中。  

 在下列情况下，可以使用层次结构维护工具：  

-   当要求安全密钥交换时，在一些情况下，你必须在站点之间手动执行初始公钥交换。 有关详情，请参阅本主题中的 [在站点之间手动交换公钥](#BKMK_ManuallyExchangeKeys) 。  

-   删除针对不再可用的目标站点的活动作业。  

-   在无法使用安装程序卸载站点时，可从 Configuration Manager 控制台中删除站点服务器。 例如，如果在未首先运行安装程序来卸载某 Configuration Manager 站点的情况下将其物理删除，那么，该站点的信息仍在父站点的数据库中存在，而且父站点继续尝试与该子站点进行通信。 若要解决此问题，必须运行层次结构维护工具，并手动从父站点的数据库中删除该子站点。  

-   在不必逐项停止服务的情况下停止站点上的所有 Configuration Manager 服务。  

-   恢复站点时，可以使用 CHILDKEYS 选项将公钥从多个子站点分发到恢复站点。  

若要运行层次结构维护工具，当前用户必须具有本地计算机的管理权限。 此外，用户还必须明确获得“站点 - 管理”安全权限；用户通过成为具有该权限的组的成员来继承此权限并不足够。  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>层次结构维护工具的命令行选项  
在使用层次结构维护工具时，必须在管理中心站点、主站点或辅助站点服务器上以本地方式运行它。  

运行层次结构维护工具时，必须使用下列语法：preinst.exe /&lt;option\>。 以下是命令行选项。  

 **/DELJOB &lt;*SiteCode*>** - 在站点上使用此选项可以删除从当前站点发出到指定目标站点的所有作业或命令。  

 **/DELSITE &lt;*ChildSiteCodeToRemove*>** - 在父站点上使用此选项可从父站点的站点数据库中删除子站点的数据。 通常，在从站点服务器计算机中卸载站点之前，如果解除该计算机的授权，则使用此选项。  

> [!NOTE]  
>  /DELSITE 选项不会在  参数指定的计算机上卸载站点。 此选项仅从 Configuration Manager 站点数据库中删除站点信息。  

**/DUMP &lt;*SiteCode*>** - 在本地站点服务器上使用此选项可将站点控制映像写入到安装该站点的驱动器的根文件夹中。 可以将特定的站点控制映像写入到该文件夹，也可以写入层次结构中的所有站点控制文件。  

-   /DUMP &lt;*SiteCode*> 仅写入指定站点的站点控制映像。  

-   /DUMP 写入所有站点的站点控制文件。  

映像是站点控制文件的二进制表示形式，它存储在 Configuration Manager 站点数据库中。 转储站点控制文件映像是基本映像加上挂起增量映像的总和。  

使用层次结构维护工具转储站点控制文件映像后，该文件名的格式将为 sitectrl_&lt;*SiteCode*>.ct0。  

**/STOPSITE** - 在本地站点服务器上使用此选项可启动部分重置该站点的 Configuration Manager 站点组件管理器服务的关闭周期。 在运行此关闭周期时，站点服务器及其远程站点系统上的某些 Configuration Manager 服务将停止。 这些服务被标记为重新安装。 由于此关闭周期，在重新安装这些服务后，某些密码将自动更改。  

> [!NOTE]  
>  如果要查看站点组件管理器的关闭、重新安装和密码更改的记录，请在使用此命令行选项之前启用此组件的日志记录。  

在启动关闭周期之后，它将自动继续进行，并跳过所有无响应的组件或计算机。 但是，如果站点组件管理器服务在关闭周期期间无法访问远程站点系统，则在重新启动站点组件管理器服务时，将重新安装在远程站点系统上安装的组件。 在重新启动站点组件管理器服务时，它将反复尝试重新安装标记为重新安装的所有服务，直到重新安装成功为止。  

您可以使用服务管理器重新启动站点组件管理器服务。 重新启动之后，所有受影响的服务都将被卸载、重新安装和重新启动。 在使用 /STOPSITE 选项启动关闭周期之后，将无法避免重新启动站点组件管理器服务之后执行的重新安装周期。  

**/KEYFORPARENT** - 在站点上使用此选项可将站点的公钥分发到父站点。  

/KEYFORPARENT 选项可将站点的公钥放置在程序文件驱动器的根目录下的 &lt;*SiteCode*>.CT4 文件中。 运行带有此选项的 preinst.exe 后，请将 &lt;*SiteCode*>.CT4 文件手动复制到父站点的 …\Inboxes\hman.box 文件夹（而非 hman.box\pubkey）中。  

**/KEYFORCHILD** - 在站点上使用此选项可将站点的公钥分发到子站点。  

/KEYFORCHILD 选项会将站点的公钥放置在程序文件驱动器的根目录下的 &lt;*SiteCode*>.CT5 文件中。 在运行带有此选项的 preinst.exe 后，请将 &lt;*SiteCode*>.CT5 文件手动复制到子站点的 …\Inboxes\hman.box 文件夹（而非 hman.box\pubkey）中。  

**/CHILDKEYS** - 可在正恢复的站点的子站点上使用此选项。 使用此选项可以将公钥从多个子站点分发到恢复站点。  

/CHILDKEYS 选项会将运行此选项的站点的密钥及其所有子站点的公钥都放入 &lt;*SiteCode*>.CT6 文件中。  

在运行带有此选项的 preinst.exe 后，请将 &lt;*SiteCode*>.CT6 文件手动复制到恢复站点的 …\Inboxes\hman.box 文件夹（而非 hman.box\pubkey）中。  

**/PARENTKEYS** - 可在正恢复的站点的父站点上使用此选项。 使用此选项可以将公钥从所有父站点分发到恢复站点。  

/PARENTKEYS 选项会将运行此选项的站点的密钥及其上每个父站点的密钥都放入 &lt;SiteCode\>.CT7 文件中。  

在运行带有此选项的 preinst.exe 后，请将 &lt;*SiteCode*>.CT7 文件手动复制到恢复站点的 …\Inboxes\hman.box 文件夹（而非 hman.box\pubkey）中。  

##  <a name="BKMK_ManuallyExchangeKeys"></a>在站点之间手动交换公钥  
默认情况下，将为 Configuration Manager 站点启用“要求安全密钥交换”选项。 当要求安全密钥交换时，在下列两种情况下，你必须在站点之间手动执行初始密钥交换：  

-   如果尚未为 Configuration Manager 扩展 Active Directory 架构  

-   Configuration Manager 站点没有将站点数据发布到 Active Directory  

可以使用层次结构维护工具导出每个站点的公钥。 将它们导出之后，你必须在站点之间手动地交换这些密钥。  

> [!NOTE]  
>  手动交换公钥之后，你可以在父站点服务器上查看 **hman.log** 日志文件（它记录了站点配置的更改和面向 Active Directory 域服务的站点信息发布），以确保主站点已处理新的公钥。  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>将子站点公钥手动传输到父站点  

1.  登录到子站点，打开命令提示符，然后导航到 **Preinst.exe**的位置。  

2.  键入下列命令以导出子站点的公钥：**Preinst /keyforparent**  

3.  /keyforparent 选项会将子站点的公钥放置在系统驱动器根目录下的 **&lt;site code\>.CT4** 文件中。  

4.  将 **&lt;site code\>.CT4** 文件移动到父站点的 **&lt;install directory\>\inboxes\hman.box** 文件夹中。  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>将父站点公钥手动传输到子站点  

1.  登录到父站点，打开命令提示符，然后导航到 **Preinst.exe**的位置。  

2.  键入下列命令以导出父站点的公钥：**Preinst /keyforchild**。  

3.  /keyforchild 选项会将父站点的公钥放置在系统驱动器根目录下的 **&lt;site code\>.CT5** 文件中。  

4.  将 **&lt;site code\>.CT5** 文件移动到子站点上的 **&lt;install directory\>\inboxes\hman.box** 目录中。  
