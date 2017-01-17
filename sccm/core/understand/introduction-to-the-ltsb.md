---
title: "Long-Term Servicing Branch 简介 | Microsoft Docs"
description: "了解 System Center Configuration Manager 的 Long-Term Servicing Branch。"
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: c681068768eda992b570a10b5f1b25c6ff1e1e79


---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager 的 Long-Term Servicing Branch 简介

*适用范围：System Center Configuration Manager (Long-Term Servicing Branch)*

请使用本主题，了解 Configuration Manager 的 Long-Term Servicing Branch (LTSB) 以及此分支的文档。


LTSB 是 Configuration Manager 的基于 Current Branch 1606 版的不同分支。 与 Current Branch 相比，LTSB 的[功能缩减](#features-that-are-not-available-in-the-ltsb-of-configuration-manager)。 它适用于[允许其软件保障 (SA) 或等效订阅权限失效](/sccm/core/understand/learn-more-editions#software-assurance-and-the-ltsb)的客户。

**许可概述：**   
自 2016 年 10 月 1 日起，具有 System Center Configuration Manager 许可证上可用的软件保障 (SA) 或同等订阅权限的客户，有权使用 System Center Configuration Manager 的 2016 年 10 月发行的版本 1606。 自 2016 年 10 月 1 日起（含），对 System Center Configuration Manager 具有权限的客户在安装时将会发现两个已许可的选项：Current Branch 和 Long-Term Servicing Branch (LTSB)。

**许可指定：**  
[可在此处](http://go.microsoft.com/fwlink/?LinkId=800052)找到通过 Microsoft 批量许可计划购买的产品的完整条款和条件。

对 System Center Configuration Manager 具有永久权限或者允许 SA 或订阅在 10 月 1 日之后失效的客户，可以在失效时安装当前的 System Center Configuration Manager LTSB 版本。
- 有关 System Center Configuration Manager 的软件保障和许可证要求的信息，请参阅 [System Center Configuration Manager 许可和分支](learn-more-editions.md)。
-   有关不同分支之间差异的信息，请参阅[我应使用 Configuration Manager 的哪一个分支](which-branch-should-i-use.md)。

若要安装新站点或从受支持的 System Center 2012 Configuration Manager 站点升级到 LTSB，可以使用版本 1606 基线介质。 DVD 上提供此基线介质，此基线介质是 Microsoft System Center 2016 的一部分或来自 System Center Configuration Manager（Current Branch 和 Long-Term Servicing Branch 1606）版本。 可安装 LTSB 的基线介质也可用于安装 Configuration Manager 的 Current Branch 版本 1606。 若要了解有关基线介质的信息，请参阅[基线和更新版本](/sccm/core/servers/manage/updates#baseline-and-update-versions)。

有关如何安装 LTSB 站点的信息，请参阅 [Long-Term Servicing Branch 的安装和升级](install-the-ltsb.md)。 有关如何获取 System Center 2016 的信息，请参阅 [System Center 2016 文档](https:\technet.microsoft.com\system-center-docs\System-Center-2016)。

> [!IMPORTANT]
> 层次结构中的所有站点必须运行相同的分支。 不支持在不同的站点具有混合使用 LTSB 和 Current Branch 的层次结构。
>
> 同样，使用恢复时，必须将站点或站点数据库恢复到其原始的分支。 无法将 Current Branch 站点数据库恢复到 LTSB 安装，反之亦然。


## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Configuration Manager 的 LTSB 不提供的功能
与 Current Branch 相比，LTSB 具有以下支持限制：

- 不接收新功能的更新。
- 不支持添加 Microsoft Intune 订阅，即阻止使用：
  - 混合 MDM 配置中的 Intune
  - 本地 MDM
-   不支持使用 Windows 10 服务仪表板和服务计划，并且不支持 Windows 10 Current Branch (CB) 和 Current Branch for Business (CBB)
- 不支持 Windows 10 LTSB 和 Windows Server 的未来版本
-   不支持资产智能
-   不支持基于云的分发点
-   不支持作为 Exchange 连接器的 Exchange Online
-   不支持任何预发行版本功能


虽然 LTSB 不支持这些功能，但一些功能依然会显示在 Configuration Manager 控制台中，但不能选择或使用这些功能。

此外，Current Branch 支持的新添加的操作系统将不受 LTSB 支持。

## <a name="documentation-for-the-ltsb"></a>LTSB 文档
由于 LTSB 基于版本 1606 Current Branch，所以用于 LTSB 的文档是[适用于 Current Branch 的联机文档](https://docs.microsoft.com/sccm/)，其中包含特定于 LTSB 的警告和限制，如以下主题所述：  

-   [Long-Term Servicing Branch 简介](introduction-to-the-ltsb.md) -（本主题）

-   [我应使用 Configuration Manager 的哪一个分支](which-branch-should-i-use.md) – 通过有关 System Center Configuration Manager 的不同分支的信息，确定需要安装的最佳分支。

-   [安装 Long-Term Servicing Branch](install-the-ltsb.md) - 如何安装新的 LTSB 站点，或将 System Center 2012 Configuration Manager 站点升级到 LTSB。

-   [将 Long-Term Servicing Branch 升级到 Current Branch](convert-to-current-branch.md) – 如何将 LTSB 安装转换为 Current Branch 安装。

-   [System Center Configuration Manager 的许可和分支](learn-more-editions.md) – 有关 System Center Configuration Manager 的软件保障和相关许可证要求的信息。
-   [Long-Term Servicing Branch 的支持配置](supported-configurations-for-ltsb.md) - 可配合 LTSB 使用的操作系统和相关产品（如 SQL Server）的版本和要求。


为帮助区分特定的文档适用于哪个分支，请使用以下指南：  
-   带“适用于：Current Branch”标题的主题适用于 Current Branch 和 Long-Term Servicing Branch（但主题中的某些部分可能仅适用于 Current Branch 的较新版本）。

-   为区分不适用于 LTSB 的主题部分，对于 Current Branch 版本 1606 后引入的功能和更改，使用“从版本 1610 开始”字样标明。 由于这些功能和更改是 Current Branch 1606 版后引入的，因此 LTSB 中不提供。

### <a name="similarities-between-the-current-branch-and-the-ltsb"></a>Current Branch 和 LTSB 之间的相似之处
由于 LTSB 基于 Current Branch 1606 版（某些例外情况除外，如 Intune 集成和与云相关的功能），规划、部署、配置和管理两个分支的大多数任务是相同的。

例如，LTSB 和 Current Branch 支持相同的站点数、站点类型、客户端以及一般基础结构。 因此，可以使用站点中的指南以及适用于 Current Branch 的层次结构规划和设计主题。 同样，对于这两个分支都支持的功能（如软件更新或操作系统部署），可以使用 Current Branch 文档中相关部分的指南（其中警告对于 Current Branch 1606 版之后引入的更改无访问权）。


## <a name="how-to-identify-your-branch-and-version"></a>如何识别分支和版本
查看 Configuration Manager 站点的版本信息时，也可确认分支。

若要查看站点的版本，在控制台中转至控制台左上角的“关于 System Center Configuration Manager”，“站点版本”显示为“5.0.8412.1000”。

若要确认站点分支（是 LTSB 还是 Current Branch），在控制台中转至“管理” > “站点配置” > “站点”，并打开“层次结构设置”。  如果有转换为 Current Branch 的选项，而且选项处于活动状态，该站点运行 LTSB 版本。 如果站点运行 Current Branch，此选项将灰显。

有关 Configuration Manager 的不同版本的信息，请参阅 [Configuration Manager 更新](/sccm/core/servers/manage/updates)主题中的“基线和更新版本”。

## <a name="exceptions-for-using-the-ltsb"></a>使用 LTSB 的异常
### <a name="updates-and-servicing-of-the-ltsb"></a>LTSB 的更新和服务
LTSB 中仅提供作为控制台中更新的关键安全更新。

但是，控制台中显示后续 Current Branch 版本的定期更新信息。 由于不会向 LTSB 提供这些更新，因此不能下载和安装这些更新。

若要支持关键安全修补程序的控制台中更新，LTSB 站点要求使用[服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。 可以在脱机或联机模式下配置此站点系统角色，这与在 Current Branch 中相同。 与 Current Branch 相同，LTSB 会收集并提交遥测和使用情况数据。

LTSB 支持使用修补程序安装程序和更新注册工具，这与 Current Branch 相同。

有关更新和服务的常规信息，请参阅 [Configuration Manager 的更新](/sccm/core/servers/manage/updates)。

### <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>站点扩展和 CD.Latest 文件夹的更改
如果运行 LTSB 且要通过安装新的管理中心站点扩展独立主站点，必须使用 1606 版基线介质中的安装程序和源文件。  （对于 Current Branch，运行 CD.Latest 文件夹中的安装程序并使用此文件夹中的源文件。）

虽然不从 CD.Latest 文件夹运行安装文件用于站点扩展，但仍将 CD.Latest 文件夹用于站点恢复，并且当第一个 LTSB 是管理中心站点时，仍安装新的子主站点。

有关站点扩展的详细信息，请参阅[使用安装向导来安装站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site)中的[扩展独立主站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)。
有关 CD.Latest 文件夹的详细信息，请参阅 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)。



<!--HONumber=Dec16_HO3-->


