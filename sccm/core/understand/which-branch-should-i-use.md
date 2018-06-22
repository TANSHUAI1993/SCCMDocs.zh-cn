---
title: 应该使用哪一个分支
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager 可用分支之间的差异。
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 258d8ac160e9ee31189f8771fd6109d1bb17f714
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341332"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>应该使用 Configuration Manager 的哪一个分支？

*适用范围：System Center Configuration Manager（Current Branch、Long-Term Servicing Branch 和 Technical Preview）*


System Center Configuration Manager 的三个可用分支：Current Branch、Long-Term Servicing Branch 和 Technical Preview Branch。 使用本主题帮助选择适合的分支。

> [!TIP]  
> 层次结构中的所有站点必须运行相同的分支。 不支持在各个网站运行不同分支的层次结构。


## <a name="current-branch"></a>Current Branch
此分支已获许在生产环境中使用。 使用此分支获取最新特性和功能。 如果有以下许可证之一，则可以使用此分支：  
- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- 等效订阅权限  

有关软件保障和许可选项的详细信息，请参阅 [System Center Configuration Manager 的许可和分支](learn-more-editions.md)以及 [Configuration Manager 分支和许可的常见问题解答](/sccm/core/understand/product-and-licensing-faq)。

Current Branch 一年更新几次，更新时提供新的功能。 每个更新版本在其发布后一年内受支持。 请在 1 年期限到期之前或到期日当天更新到 Current Branch 的较新版本。 较新版本的更新以控制台内更新的形式提供。

若要将 Current Branch 作为新站点进行安装，请使用[基线介质](/sccm/core/servers/manage/updates#baseline-and-update-versions)。 也可使用基线介质从 System Center 2012 Configuration Manager Service Pack 2 或 System Center 2012 R2 Configuration Manager Service Pack 1 升级。 对此介质的访问权取决于组织对 System Center Configuration Manager 的许可方式。 

还可使用基线介质安装充当 Current Branch 评估版的新站点。 评估版不需要许可证。 评估版可使用 180 天。 它支持升级到 Current Branch 的许可版。 如果想仅安装评估版，可通过 [TechNet 评估中心](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection)获取。

>  [!NOTE]  
> 使用基线介质安装新的 Configuration Manager 层次结构的站点。 如果以前安装了基准版本，请使用控制台中更新将站点更新到新版本。  
>  
> 使用控制台内部更新更新后的站点与使用基线介质安装新站点的效果一样。
>
> 有关详细信息，请参阅 [ System Center Configuration Manager 的更新](/sccm/core/servers/manage/updates)。  


### <a name="features-of-the-current-branch"></a>Current Branch 的功能
- 接收[控制台中更新](/sccm/core/servers/manage/install-in-console-updates)，使新功能可用。
- 接收控制台中更新，为现有功能提供安全和质量修补程序。
- 必要时支持带外更新。 有关详细信息，请参阅[使用更新注册工具](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)或[使用修补程序安装程序](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates)。
- 与 Microsoft Intune 和其他基于云的服务集成。
- 支持与其他 Configuration Manager 安装之间的[数据迁移](/sccm/core/migration/migrate-data-between-hierarchies)。
- 支持从以前版本的 Configuration Manager 升级。
- 支持安装评估版本，以后可以升级到完全许可的安装。

Current Branch 的初始版本是版本 1511。 后续更新包括版本 1602 和 1606 等。 各版本的有效期为 1 年，Microsoft 建议在最新版本发布后立即更新。 较旧版本最多可使用一年，之后需要更新到较新版本，也可跳过更新，直接安装最新的可用版本。 由于每个版本是累积更新，因此如果跳过更新并安装最新版本，仍可获取以前版本的所有功能和改进。

有关详细信息，请参阅[对 Current Branch 版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)。


### <a name="update-options"></a>更新选项
- 通过可用的软件保障，可以安装 Current Branch 版本的控制台中更新。  
- 无法将 Current Branch 转换为 Technical Preview Branch。 Technical Preview Branch 是单独安装，不需要许可证。
- 无法将 Current Branch 转换为 Long Term Servicing Branch (LTSB)。 必须卸载 Current Branch，然后将 LTSB 作为新安装进行安装。



##  <a name="long-term-servicing-branch"></a>Long Term Servicing Branch 
此分支已获许在生产中使用，面向正在使用 Current Branch 且允许其 Configuration Manager 软件保障 (SA) 或等效订阅权限在 2016 年 10 月 1 日后过期的 Configuration Manager 客户。 有关软件保障和许可选项的详细信息，请参阅 [System Center Configuration Manager 的许可和分支](learn-more-editions.md)以及 [Configuration Manager 分支和许可的常见问题解答](/sccm/core/understand/product-and-licensing-faq)。

LTSB 基于版本 1606。 该分支不会收到提供新功能或更新现有功能的控制台中更新。 但是，提供了关键安全修补程序。 要安装 LTSB，必须使用随附在 System Center 2016 中的版本 1606 [基线介质](/sccm/core/servers/manage/updates#baseline-and-update-versions)。 更高的基准版本不支持安装 LTSB。

若要将 LTSB 安装为新站点或通过升级受支持的 Configuration Manager 2012 站点来安装 LTSB，可以使用随附在 System Center 2016 中的版本 1606 [基线介质](/sccm/core/servers/manage/updates#baseline-and-update-versions)。 可使用基线介质安装运行 Current Branch 版本 1606 的新站点或运行 Long-Term Servicing Branch 的新站点。

> [!TIP]  
> 若要了解 System Center 2016，请参阅 [System Center 2016 文档](https://docs.microsoft.com/system-center/index)。 本文档还说明如何获取 System Center 2016（需要 Microsoft 许可证协议或类似权限）。  
>  
> 若要在批量许可服务中心 (VLSC) 查找 System Center Configuration Manager 版本 1606，请转到 [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) 的“下载和密钥”选项卡，搜索“`System Center 2016`”，然后选择“System Center 2016 Datacenter”或“System Center 2016 Standard”。  
>  
> 也可从 [TechNet 评估中心](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview)获取 System Center 2016 评估版。  


### <a name="features-of-the-ltsb"></a>LTSB 的功能
-   接收提供关键安全修补程序的控制台中更新。
- SA 协议或 Configuration Manager 的等效权限过期后，提供安装选项。
- 如果当前具有 SA 协议或 Configuration Manager 等效权限，支持升级（转换）到 Current Branch。


### <a name="limitations"></a>限制  
LTSB 以 Current Branch 版本 1606 为基础，具有以下限制：
- 正式发布（2016 年 10 月）后，支持 LTSB 的 10 年关键安全更新，此后，对此分支的支持将过期。 有关支持生命周期的详细信息，请参阅 [Microsoft 生命周期策略](https://support.microsoft.com/lifecycle)。
- 支持有限数量的服务器和客户端操作系统以及相关技术（如 SQL Server 版本）。 有关此分支支持功能的详细信息，请参阅 [Long Term Servicing Branch 支持的配置](supported-configurations-for-ltsb.md)。
- 不接收新功能更新
- 不支持以下功能： 
   - 添加 Microsoft Intune 订阅将阻止使用：
     -  混合 MDM 配置中的 Intune
     - 本地 MDM
   -    Windows 10 维护服务仪表板、维护服务计划或 Windows 10 半年频道
   - Windows 10 LTSB 和 Windows Server 的未来版本
   -    资产智能
   -    基于云的分发点
   -    作为 Exchange Connector 的 Exchange Online
   -    任何预发行功能


### <a name="update-options"></a>更新选项
- 可以将 LTSB 安装转换为 Current Branch 安装。 对 LTSB 的支持过期前或过期后，支持转换为 Current Branch。

  若要转换，必须具有与 Microsoft 签署的可用的软件保障协议。 有关详细信息，请参阅以下链接：
  - [将 Long-Term Servicing Branch 升级到 Current Branch](convert-to-current-branch.md)
  - [System Center Configuration Manager 的许可和分支](learn-more-editions.md)
  - [基准和更新版本](/sccm/core/servers/manage/updates#baseline-and-update-versions) 
- 无法将 LTSB 转换为 Technical Preview Branch。 Technical Preview Branch 是单独安装，不需要许可证。
-   不可将 Current Branch 的评估版升级到 LTSB 安装。



## <a name="technical-preview-branch"></a>Technical Preview Branch
Technical Preview Branch 适用于实验室环境。 了解并试用正在为 Configuration Manager 开发的最新功能。 它不支持在生产环境中使用，并且不需要软件保障许可证协议。

若要安装运行 Technical Preview Branch 的新站点，请使用最新 [Technical Preview Branch 的基线介质](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview)。 安装 Technical Preview Branch 后，每月提供作为控制台中更新的新版本。


### <a name="features-of-the-technical-preview-branch"></a>Technical Preview Branch 的功能
-  基于 Current Branch 的最新基准版本
-  接收控制台中更新，该更新将安装更新到最新版 Technical Preview Branch
-  内附正在开发且 Microsoft 希望你提供反馈的新功能
-  接收仅适用于 Technical Preview Branch 的更新


### <a name="limitations"></a>限制
-  [有限支持](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview)，仅包括单个主站点和最多 10 个客户端。  
-  不能升级到 Current Branch 或 LTSB。
-  不支持以下行为：
   - 使用迁移将数据导入或导出到另一个 Configuration Manager 安装
   - 从以前版本的 Configuration Manager 升级
   - 安装评估版

先引入 Technical Preview Branch 中的功能通常会在之后的更新中添加到 Current Branch。 每个新的 Technical Preview Branch 版本都包含以前的 Technical Preview Branch 版本的功能，即使这些功能已添加到 Current Branch，也是如此。

有关详细信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。


### <a name="update-options"></a>更新选项
-   对于新的 Technical Preview Branch 版本，可以安装任何控制台中更新。
-   无法将 Technical Preview Branch 转换为 Current Branch 或 LTSB。



## <a name="identify-your-version-and-branch"></a>识别版本和分支

### <a name="version"></a>版本   
若要查看站点的版本，请转到控制台左上角的“关于 System Center Configuration Manager”。 对话框会显示站点版本。 有关站点版本的列表，请参阅[基准和更新版本](/sccm/core/servers/manage/updates#bkmk_Baselines)。

### <a name="branch"></a>分支
若要确认站点分支，请转到控制台中的“管理” > “站点配置” > “站点”，并打开“层次结构设置”。 如果有转换为 Current Branch 的选项，而且选项处于活动状态，则该站点运行 LTSB 版本。 如果站点运行 Current Branch，此选项将灰显。

有关 Configuration Manager 不同版本的详细信息，请参阅[基准和更新版本](/sccm/core/servers/manage/updates#bkmk_Baselines)。
