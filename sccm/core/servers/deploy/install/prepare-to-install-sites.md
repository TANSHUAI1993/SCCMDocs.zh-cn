---
title: "准备安装站点 | System Center Configuration Manager"
description: "请阅读这些详细信息，以节省安装多个站点的时间并防止出现错误。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6f240f1da4561c05bee974b78f43bfcdba591df6

---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>准备安装 System Center Configuration Manager 站点

*适用范围：System Center Configuration Manager (Current Branch)*

若要准备成功部署一个或多个 System Center Configuration Manager 站点，请熟悉本文中有关步骤的详细信息。 这些步骤可以节省安装多个站点的时间，并有助于防止漏掉步骤从而导致需要重新安装一个或多个站点。
 > [!TIP]
 >  以下方案类似于安装 System Center Configuration Manager current branch 站点，但仍存在区别：
 > -  **升级**：安装 System Center Configuration Manager 以从 System Center 2012 Configuration Manager **升级**，请参阅[升级到 System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)
 > -  **更新**：使用控制台中更新将新的**更新版本**安装到现有的 System Center Configuration Manager 站点，请参阅 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)
 > -  **迁移**：若要将**数据**从其他 Configuration Manager 层次结构迁移到当前的 Configuration Manager 层次结构，请参阅[计划迁移到 System Center Configuration Manager](../../../../core/migration/planning-for-migration.md)



## <a name="a-namebkmkoptionsa-options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a>安装不同类型站点的选项
安装新的 Configuration Manager 时，可以使用的源文件版本取决于层次结构中的已有站点（如果有）的版本，而可用的安装方法取决于想要安装的站点类型。  

安装站点前，请确保已对层次结构进行了规划，并且了解想要安装的站点类型。 有关详细信息，请参阅[设计站点层次结构](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)。


### <a name="first-site"></a>第一个站点
要为层次结构安装的第一个站点必须是独立主站点或管理中心站点。

**安装媒体**：若要将管理中心站点或独立主站点安装为新层次结构中的第一个站点，则必须[使用基线版本](../../../../core/servers/manage/updates.md#bkmk_Baselines)的 Configuration Manager。 请勿使用任何站点的 [CD.Latest 文件夹](../../../../core/servers/manage/the-cd.latest-folder.md)中已更新的源文件来安装新层次结构的第一个站点。

**安装方法**：使用 [Configuration Manager 安装向导](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)安装任一站点类型，或可以将脚本配置为与[脚本化命令行安装](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)配合使用。


### <a name="additional-sites"></a>其他站点
在初始站点安装完成后，可以随时添加其他站点。 可使用以下选项添加其他的站点（最多可添加以达到[支持的限制](../../../../core/plan-design/configs/size-and-scale-numbers.md)）：

你拥有的站点          |可以安装的其他站点  
---------                   |---------
管理中心站点 |   安装子级主站点            
子级主站点          |   安装辅助站点        
独立主站点    |   安装辅助站点<br />扩展将独立主站点转换为子级主站点的主站点

**安装媒体**：若要安装管理中心站点以便展开独立主站点，或在现有层次结构中安装新的子主站点，必须使用与现有站点或站点版本匹配的安装媒体（源文件）。
> [!IMPORTANT]
> 如果已安装控制台中的更新（已更改以前安装的站点版本），请使用已更新站点的 [CD.Latest 文件夹](../../../../core/servers/manage/the-cd.latest-folder.md)中的源文件，不要使用原始安装媒体。  Configuration Manager 要求使用与新站点将连接到的现有站点版本相匹配的源文件。


必须从 Configuration Manager 控制台内安装辅助站点，因此请始终从父主站点中使用源文件进行安装。

**安装方法**：安装其他站点的方法取决于想要安装的站点类型。
-   **添加管理中心站点**：  
可以使用 Configuration Manager 安装向导或脚本化命令行将新的管理中心站点作为父站点安装到现有的独立主站点。  有关详细信息，请参阅[扩展独立主站点](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)。
-   **添加子主站点**：  
可以使用 Configuration Manager 安装向导或命令行安装在管理中心站点下添加子主站点。
-   **添加辅助站点**：   
使用 Configuration Manager 控制台将辅助站点安装为主站点下的子站点。 辅助站点不支持其他方法。



## <a name="a-namebkmktasksa-common-tasks-to-complete-before-starting-an-install"></a><a name="bkmk_tasks"></a>开始安装前要完成的常见任务
-   了解用于部署的层次结构拓扑    
     （请参阅[设计 System Center Configuration Manager 的站点层次结构](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)）  

-   准备和配置单个服务器以满足先决条件以及使用 Configuration Manager 受支持的配置（请参阅 [Site and site system prerequisites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md)（站点和站点系统先决条件））  

-   安装和配置 SQL Server 以托管主站点数据库（请参阅    
    [对 System Center Configuration Manager 的 SQL Server 版本的支持](../../../../core/plan-design/configs/support-for-sql-server-versions.md)）  

-   准备网络环境以支持 Configuration Manager（请参阅 [Configure firewalls, ports, and domains to prepare for Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains)（配置防火墙、端口和域以准备 Configuration Manager））  

-   如果使用 PKI，请准备基础结构和证书（请参阅 [Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)

-   在要用作站点服务器或站点系统服务器的计算机上安装最新的安全更新，并且在需要时重启它们。



## <a name="a-namebkmksitecodesa-about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a>关于站点名称和站点代码
站点代码和站点名称用于标识和管理 Configuration Manager 层次结构中的站点。 在 Configuration Manager 控制台中，站点代码和名称以 &lt;site code\> - &lt;site name\> 的格式显示。 在层次结构中使用的每个站点代码必须是唯一的。 如果已为 Configuration Manager 扩展了 Active Directory 架构，并且站点正在发布数据，则在 Active Directory 林中使用的站点代码必须是唯一的，即使这些代码在不同的 Configuration Manager 层次结构中使用或已在以前安装的 Configuration Manager 中使用过。 在部署层次结构之前，请务必仔细规划站点代码和名称。

### <a name="specify-a-site-code-and-site-name"></a>指定站点代码和名称
在 Configuration Manager 的安装过程中，系统会提示为管理中心站点以及每个主站点和辅助站点安装输入站点代码及站点名称。 站点代码必须唯一地标识层次结构中的每个站点。 由于文件夹名称中使用了站点代码，因此，请勿将以下名称用于站点代码，其中包括 Configuration Manager 保留的名称和 Windows 保留的名称：
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> Configuration Manager 安装程序不会验证所指定的站点代码是否已不再使用。



若要在 Configuration Manager 的安装过程中输入站点代码，则必须输入三个字母数字字符。 在指定站点代码时，仅接受从 A 到 Z 的字母、从 0 到 9 的数字或者两者的组合。 字母或数字的序列对站点之间的通信没有影响。 例如，不一定要将主站点和辅助站点分别命名为 ABC 和 DEF。

站点名称是站点的友好名称标识符。 在站点名称中，请仅使用标准字符，也即 A 到 Z、a 到 z、0 到 9 和连字符 (-)。
> [!IMPORTANT]
> 不支持在安装后更改站点代码或站点名称。

### <a name="reuse-a-site-code"></a>重复使用站点代码
在 Configuration Manager 层次结构中，管理中心站点或主站点的站点代码只能使用一次，即使在已卸载原始站点和站点代码后也是如此。 如果重复使用站点代码，则在层次结构中会出现对象 ID 冲突的风险。 如果在 Configuration Manager 层次结构中或在 Active Directory 林中不再使用某个辅助站点，则可以重复使用辅助站点的站点代码。


## <a name="limits-and-restrictions-for-installed-sites"></a>已安装站点的限制和局限性
在安装站点前，请了解适用于站点和层次结构的以下限制：
-   安装完成后，除非卸载该站点，然后再使用新值重新安装，否则将无法更改下列站点属性：  
    -   程序文件安装目录  
    -   站点代码  
    -   站点说明  
-   当你的层次结构中包括管理中心站点时：  
    -   Configuration Manager 不支持将子主站点移出层次结构，以创建独立主站点或将其附加到不同的层次结构。 相反，首先需要卸载子主站点，然后重新将它安装为新的独立主站点或不同层次结构的管理中心站点的子主站点。  


## <a name="a-namebkmkoptionalstepsa-optional-steps-to-run-before-starting-setup"></a><a name="bkmk_optionalsteps"></a>开始安装前要运行的可选步骤
**可以手动运行[安装程序下载程序](../../../../core/servers/deploy/install/setup-downloader.md)**为 Configuration Manager 下载已更新的安装文件。

要运行安装程序的计算机未连接到 Internet 时，或者需要安装多个站点服务器时，请考虑使用安装程序下载程序更新安装程序下载安装程序文件所需的更新：

-  默认情况下，安装程序将连接到 Internet 以下载更新的安装程序文件
-  默认情况下，这些文件存储在名为 Redist 文件夹中
-  可以将安装程序定向到网络上以前存储这些文件的副本的位置


**可以手动运行[先决条件检查程序](../../../../core/servers/deploy/install/prerequisite-checker.md)**在运行安装程序之前识别并修复问题。 启动安装程序安装站点前，在服务器上安装站点系统角色之前，可以运行先决条件检查程序以确保计算机满足托管站点或站点系统角色的要求。
 -  默认情况下，安装程序将运行先决条件检查程序。
 -  如果存在任何错误，安装程序将暂停，直到问题解决为止。


**确定可选端口** ，以用于站点系统和客户端。
 -  默认情况下，站点系统和客户端使用预定义的端口进行通信。
 -  安装过程中，可以配置备用端口。
 -  有关详细信息，请参阅 [System Center Configuration Manager 中使用的端口](../../../../core/plan-design/hierarchy/ports.md)



<!--HONumber=Nov16_HO1-->


