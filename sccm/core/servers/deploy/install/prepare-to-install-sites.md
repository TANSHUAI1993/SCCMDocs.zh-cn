---
title: "安装站点的准备工作 | Microsoft Docs"
description: "如果计划安装多个 Configuration Manager 站点，请阅读此信息，帮助节省时间并防止出现错误。"
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 829f2d44a9b8d203a5b753ebb6d8f759b1a05111
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>准备安装 System Center Configuration Manager 站点

*适用范围：System Center Configuration Manager (Current Branch)*

若要准备成功部署一个或多个 System Center Configuration Manager 站点，请熟悉本文中有关步骤的详细信息。 这些步骤可以节省安装多个站点的时间，并有助于防止漏掉步骤从而导致需要重新安装一个或多个站点。

> [!TIP]
> 管理 System Center Configuration Manager 站点和层次结构基础结构时，术语“升级”“更新”和“安装”用于描述三种不同概念。 若要了解每个术语的使用方法，请参阅[有关升级、更新和安装](/sccm/core/understand/upgrade-update-install)。

## <a name="bkmk_options"></a>安装不同类型站点的选项
安装新的 Configuration Manager 站点时，可使用的源文件版本取决于层次结构中已有站点的版本（若有）。 可用的安装方法取决于要安装的站点类型。  

安装站点前，请确保已对层次结构进行了规划，并且了解想要安装的站点类型。 有关详细信息，请参阅[设计站点层次结构](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)。


### <a name="first-site"></a>第一个站点
层次结构中安装的第一个站点必须是独立主站点或管理中心站点。

**安装介质**：若要将管理中心站点或独立主站点安装为新层次结构中的第一个站点，必须使用 Configuration Manager 的[基线版本](../../../../core/servers/manage/updates.md#bkmk_Baselines)。 安装新层次结构的第一个站点时，请勿使用任何站点的 [CD.Latest 文件夹](../../../../core/servers/manage/the-cd.latest-folder.md)中更新的源文件。

**安装方法**：可使用 [Configuration Manager 安装向导](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)安装任一站点类型，或可将脚本配置为与[脚本化命令行安装](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)配合使用。


### <a name="additional-sites"></a>其他站点
在初始站点安装完成后，可随时添加更多站点。 可使用以下选项添加站点（不得超过[支持的限制](../../../../core/plan-design/configs/size-and-scale-numbers.md)）：

|你拥有的站点|可安装的其他站点类型|
|---|---|
|管理中心站点|子级主站点|
|子级主站点|辅助站点|
|独立主站点|辅助站点（可扩展将独立主站点转换为子级主站点的主站点）|

**安装介质**：若要安装管理中心站点以扩展独立主站点，或在现有层次结构中安装新的子主站点，必须使用与一个或多个现有站点的版本匹配的安装介质（内附源文件）。

> [!IMPORTANT]
> 如果已安装控制台内部更新（更改了以前安装的站点版本），请勿使用原始安装媒体。 此情况下，请改用已更新站点的 [CD.Latest 文件夹](../../../../core/servers/manage/the-cd.latest-folder.md)中的源文件。 Configuration Manager 要求所用的源文件必须与新站点要连接到的现有站点版本相匹配。

必须从 Configuration Manager 控制台安装辅助站点。 由此，始终使用父主站点的源文件安装辅助站点。

**安装方法**：附加站点的安装方法取决于要安装的站点类型。
-   **添加管理中心站点**：可使用 Configuration Manager 安装向导或脚本化命令行，将新的管理中心站点作为父站点安装到现有的独立主站点中。 有关详细信息，请参阅[扩展独立主站点](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)。
-   **添加子主站点**：可使用 Configuration Manager 安装向导或命令行安装在管理中心站点下添加子主站点。
-   **添加辅助站点**：使用 Configuration Manager 控制台将辅助站点安装为主站点下的子站点。 不可使用其他方法添加辅助站点。

## <a name="bkmk_tasks"></a>开始安装前要完成的常见任务
-   **了解用于部署的层次结构拓扑**    
有关详细信息，请参阅[设计 System Center Configuration Manager 的站点层次结构](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)。  

-   **准备和配置单个服务器以满足与 Configuration Manager 搭配使用的先决条件和受支持的配置**         
有关详细信息，请参阅[站点和站点系统先决条件](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

-   **安装和配置 SQL Server 以托管站点数据库**     
有关详细信息，请参阅[对 System Center Configuration Manager 的 SQL Server 版本的支持](../../../../core/plan-design/configs/support-for-sql-server-versions.md)。  

-   **准备网络环境以支持 Configuration Manager**      
有关详细信息，请参阅[配置防火墙、端口和域以准备 Configuration Manager](../../../../core/plan-design/network/configure-firewalls-ports-domains.md)。  

- **如果要使用公钥基础结构 (PKI)，请准备基础结构和证书**      
有关详细信息，请参阅 [Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)。

-   **在要用作站点服务器或站点系统服务器的计算机上安装最新的安全更新，并在需要时重启它们**

## <a name="bkmk_sitecodes"></a>关于站点名称和站点代码
站点代码和站点名称用于标识和管理 Configuration Manager 层次结构中的站点。 在 Configuration Manager 控制台中，站点代码和名称以 &lt;*站点代码*\> - &lt;*站点名称*\> 的格式显示。 在层次结构中使用的每个站点代码必须是唯一的。 如果已扩展了 Configuration Manager 的 Active Directory 架构，且站点正在发布数据，则在 Active Directory 林中使用的站点代码必须唯一，即使这些代码在不同的 Configuration Manager 层次结构中使用或已在早期安装的 Configuration Manager 中使用过。 在部署层次结构之前，请务必仔细规划站点代码和名称。

### <a name="specify-a-site-code-and-site-name"></a>指定站点代码和站点名称
运行 Configuration Manager 安装程序时，系统将提示为管理中心站点以及每个主站点和辅助站点安装输入站点代码及站点名称。 站点代码必须唯一地标识层次结构中的每个站点。 由于文件夹名称中使用了站点代码，因此，请勿将以下名称用于站点代码，其中包括为 Configuration Manager 和 Windows 保留的名称：
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> Configuration Manager 安装程序不会验证站点代码是否已弃用。

若要在运行 Configuration Manager 安装程序时输入站点代码，必须输入 3 个字母数字字符。 站点代码中只允许使用任意组合的 *A* 到 *Z* 的字母和 *0* 到 *9* 的数字。 字母或数字的序列对站点之间的通信没有影响。 例如，不一定要将主站点和辅助站点分别命名为 *ABC* 和 *DEF*。

站点名称是站点的友好名称标识符。 仅可在站点名称中使用字符 *A* 到 *Z*、*a* 到 *z*、*0* 到 *9* 和连字符 (*-*)。

> [!IMPORTANT]
> 安装站点后，不可更改站点代码或站点名称。

### <a name="reuse-a-site-code"></a>重复使用站点代码
在 Configuration Manager 层次结构中，管理中心站点或主站点的站点代码只能使用一次，即使在卸载了原始站点和站点代码后也是如此。 如果重复使用站点代码，则可能会在层次结构中遇到对象 ID 冲突。 如果 Configuration Manager 层次结构或 Active Directory 林中不再使用某个辅助站点，则可重复使用该辅助站点的站点代码。

## <a name="limits-and-restrictions-for-installed-sites"></a>已安装站点的限制和局限性
安装站点前，请务必了解适用于站点和站点层次结构的以下限制：
-   运行安装程序后，除非卸载该站点，然后再使用新值重新安装，否则无法更改下列站点属性：  
  -   程序文件安装目录  
  -   站点代码  
  -   站点说明  
-   当你的层次结构中包括管理中心站点时：  
  -   Configuration Manager 不支持将子主站点移出层次结构，以创建独立主站点或将其附加到不同的层次结构。 而首先需要卸载子主站点，然后重新将它安装为新的独立主站点或其他层次结构的管理中心站点的子站点。  


## <a name="bkmk_optionalsteps"></a>运行安装程序前的可选步骤
**手动运行[安装程序下载程序](../../../../core/servers/deploy/install/setup-downloader.md)**

若要为 Configuration Manager 下载更新后的安装文件，可运行安装程序下载程序。 若要运行安装程序的计算机未连接到 Internet，或者需要安装多个站点服务器，请考虑使用安装程序下载程序下载安装程序所需的更新。 下面是其他信息：
-  安装程序默认连接到 Internet，以下载更新的安装程序文件。
-  这些文件默认存储在 Redist 文件夹中。
-  可将安装程序定向到网络上以前存储这些文件的副本的位置。

**手动运行[先决条件检查程序](../../../../core/servers/deploy/install/prerequisite-checker.md)**

若要确定并修复问题，然后再运行安装程序来安装站点并在一台服务器上安装站点系统角色，可运行先决条件检查程序。 先决条件检查程序有助于确保计算机满足托管站点或站点系统角色的要求。 下面是其他信息：
 -  安装程序默认运行先决条件检查程序。
 -  如果存在任何错误，安装程序将停止，直到问题解决。

**确定可选端口**

可确定供站点系统和客户端使用的可选端口。 下面是其他信息：
 -  站点系统和客户端默认使用预定义的端口进行通信。
 -  安装过程中，可以配置备用端口。

 有关详细信息，请参阅 [System Center Configuration Manager 中使用的端口](../../../../core/plan-design/hierarchy/ports.md)。
