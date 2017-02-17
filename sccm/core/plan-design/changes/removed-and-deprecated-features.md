---
title: "弃用的功能 | Microsoft Docs"
description: "了解有关 System Center Configuration Manager 不再支持的功能、产品和操作系统的信息。"
ms.custom: na
ms.date: 1/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1948e2914fff91f156dd8956c018ff0fabcda2f9
ms.openlocfilehash: 3a1edd1b59676e59d4bfcd4c01a23f7a04f91f4f


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>System Center Configuration Manager 的已删除和已弃用的功能

*适用范围：System Center Configuration Manager (Current Branch)*

本主题介绍 System Center Configuration Manager 不再支持或将在将来更新中删除（弃用）的功能、产品和操作系统。 目的是针对可能会影响使用 Configuration Manager 的将来更改提出早期通知。  

此信息在将来版本中可能有所变化，并且可能不会包括每一个弃用的功能、产品或操作系统。  

## <a name="how-to-use-this-information"></a>如何使用此信息  
将功能或操作系统首次列为已弃用后，未来版本的 Configuration Manager 中将计划不支持将其与 Configuration Manager 配合使用。 提供此信息是为了帮助你计划替代该功能或操作系统的方法。 发布 Configuration Manager 的第一个版本（其中已移除该支持）时，将更新本主题，以指示该特定版本。  

不再支持某功能或操作系统后，使用以前版本的 Configuration Manager（只要仍支持该版本的 Configuration Manager）时仍支持该功能或操作系统。 但使用所指日期和版本后发布的 Configuration Manager 版本时，该版本的 Configuration Manager 不提供支持。

例如：如果计划在 2016 年 9 月后发布的首个更新中不再支持某功能，则 2016 年 10 月发布的更新 1610 中将不再包含对该功能的支持。
-  使用更新 1610，该功能将不再受支持。
-  将更新此主题，以指示已从版本 1610 中移除支持。
但如果继续使用支持该功能的早期版本，如版本 1602 或 1606，则可以继续使用该功能，直到所使用的版本不再提供支持。

有关详情，请参阅：
 - [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)网站。
 - [对 Configuration Manager Current Branch 版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)。

## <a name="deprecated-features"></a>已弃用的功能  

|**功能**|**首次宣布弃用**|**删除的支持**|  
|-|-|-|  
|网络访问保护 (NAP)- 在 System Center 2012 Configuration Manager 中找到|2015 年 10 月|版本 1511|  
|带外管理- 在 System Center 2012 Configuration Manager 中找到|2015 年 10 月 16 日|版本 1511|
|任务序列： <br /> - OSDPreserveDriveLetter  <br /><br /> 现在，在操作系统部署期间，默认情况下，Windows 安装程序会确定要使用的最佳驱动器号（通常为 C:）。 如果想要指定使用另一个驱动器，可以在“应用操作系统”任务序列步骤中更改位置。 转到“选择要应用此操作系统的位置”设置，选择“特定逻辑驱动器号”，然后选择要使用的驱动器。 |2016 年 6 月 20 日 |版本 1606 |
|任务序列： <br /> - 将磁盘转换为动态磁盘 <br /> - 安装部署工具 |2016 年 11 月 18 日|对这些任务序列的支持随 2017 年 6 月 1 日后发布的首个更新结束。|
|软件中心将呈现新式外观。 并且本应仅出现在依赖于 Silverlight 的应用程序目录中的应用（用户可用的应用）现在将出现在“应用程序”选项卡中的软件中心。 应用程序目录仍然可以通过软件中心的“安装状态”选项卡中的链接进行访问。<br><br>在未来几个月，以前版本的软件中心将不再可用。<br><br>你可以通过启用客户端设置“计算机代理” > “使用新的软件中心”来使用新的软件中心。<br><br>有关软件中心的详细信息，请参阅[规划和配置 System Center Configuration Manager 中的应用程序管理](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management)。|2016 年 12 月 13 日|即将公布|
|利用 Configuration Manager 管理虚拟硬盘 (VHD)。 </br></br>这包括去除使用任务序列创建新 VHD 或管理 VHD 的选项，以及去除 Configuration Manager 控制台的虚拟硬盘节点。 </br></br>去除这种支持后，虽然现有 VHD 将不被删除，但再也无法从 Configuration Manager 控制台内访问。  |2017 年 1 月 6 日 |对 VHD 的支持将在 2017 年 6 月 1 日后随首个更新的发布而结束。|


1511 版 System Center Configuration Manager 发布中删除的功能的其他信息如下：

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a>带外管理  
 通过 Configuration Manager，已删除 Configuration Manager 控制台中基于 AMT 的计算机的本机支持。  

-   使用[适用于 Microsoft System Center Configuration Manager 的 Intel SCS 外接程序](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)时，基于 AMT 的计算机保持完全托管。 使用外接程序可以在 Configuration Manager 能够合并这些更改之前使用用于管理 AMT 的最新功能，同时删除引入的限制。  

-   System Center 2012 Configuration Manager 中的带外管理不受此更改的影响。  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a>网络访问保护  
 System Center Configuration Manager 已不再支持网络访问保护。 该功能已在 Windows Server 2012 R2 中弃用并从 Windows 10 中删除。  

 有关网络访问保护备选方案，请参阅 *网络策略和访问服务概述* 的 [已弃用功能](https://technet.microsoft.com/library/hh831683.aspx)部分。  


## <a name="deprecated-operating-systems"></a>已弃用的操作系统
### <a name="server-operating-systems"></a>服务器操作系统  

|**操作系统**|**首次宣布弃用**|**删除的支持** |  
|-|-|-|  
|Windows Server 2008|2015 年 10 月|此支持随 2016 年 12 月 31 日发布的首个更新结束（请参阅注释 1）。|  
|Windows Server 2008 R2|2015 年 10 月|此支持随 2016 年 12 月 31 日发布的首个更新结束（请参阅注释 2）。|  

-   注释 1：支持结束后，站点服务器或大多数站点系统角色将不再支持此操作系统。 但是，分发点站点系统角色（包括请求分发点）仍会继续支持此操作系统，直至正式宣布此支持弃用或此操作系统的扩展支持期过期。  

-   注释 2：支持结束后，站点服务器或大多数站点系统角色将不再支持此操作系统。 但是，状态迁移点和分发点站点系统角色（包括请求分发点、PXE 和多播）仍会继续支持此操作系统，直至正式宣布弃用此支持或此操作系统的扩展支持期过期。 从版本 1602 开始，可以对站点服务器的操作系统进行就地升级，从 Windows Server 2008 R2 升级到 Windows Server 2012 R2。  

     有关站点服务器操作系统就地升级的详细信息，请参阅 [System Center Configuration Manager 中的更改内容](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)中的[就地升级运行 Windows Server 2008 R2 的站点服务器的操作系统](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS)部分。



### <a name="client-operating-systems"></a>客户端操作系统  

 除非另有说明，否则支持每种作为 Configuration Manager 客户端进行支持的操作系统，直至此操作系统的扩展支持结束日期为止。 有关扩展支持结束日期的详细信息，请参阅 [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)。 如果对某个操作系统的 Configuration Manager 支持将在扩展支持结束日期前结束，则此处将列出此操作系统的弃用日期和支持删除日期。  

|**操作系统**|**首次宣布弃用**|**删除的支持**|  
|-|-|-|  
|Windows XP|2015 年 10 月|版本 1511|  
|Windows XP Embedded|2015 年 10 月|此支持随 2016 年 12 月 31 日发布的首个更新结束。|  
|Windows Server 2003|2015 年 10 月|版本 1511|  
|Windows Server 2003 R2|2015 年 10 月|版本 1511|  
|Windows Vista|2015 年 10 月|版本 1511|  
|Mac OS X 10.6 - 10.8|2015 年 10 月|版本 1511|  
|Windows Mobile 6.0 - 6.5|2015 年 10 月|版本 1511|  
|Nokia Symbian Belle|2015 年 10 月|版本 1511|  
|Windows CE 5.0 - 6.0|2015 年 10 月|版本 1511|  


## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>SQL Server 版本作为站点数据库的已弃用支持  

|**SQL Server 版本**|**首次宣布弃用**|**删除的支持**|   
|-|-|-|  
|SQL Server 2008|2015 年 10 月|版本 1511|  
|SQL Server 2008 R2|2015 年 10 月|此支持随 2016 年 12 月 31 日发布的首个更新结束。|  



<!--HONumber=Feb17_HO2-->


