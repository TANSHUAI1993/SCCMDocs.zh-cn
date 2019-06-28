---
title: 更新和服务
titleSuffix: Configuration Manager
description: 了解称为“更新与服务”的控制台内服务方法，该方法可轻松找到并安装建议的更新。
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bb875529224655fb56aeea5636bf92c7ddaf8b2c
ms.sourcegitcommit: 9d186b8b9ff652d5ea8a5d352f3f793f11db66f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2019
ms.locfileid: "66822064"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Configuration Manager 的更新和服务

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager 使用称为“更新和服务”的控制台中服务方法  。 通过此控制台中方法，可轻松找到并安装 Configuration Manager 基础结构的建议更新。 控制台内服务由带外更新（如修补程序）补充。 带外更新适用于需要解决其环境特定问题的客户。  

> [!TIP]  
> “升级”、“更新”和“安装”这三个术语在 Configuration Manager 中用于描述三个独立概念    。 若要详细了解每个术语的使用方法，请参阅[关于升级、更新和安装](/sccm/core/understand/upgrade-update-install)。  


##  <a name="bkmk_Baselines"></a> 基准和更新版本  

在新的层次结构中安装新站点时，请使用最新的基准版本。

- 也可使用基准版本从 System Center 2012 Configuration Manager 升级。  

- 升级到 Configuration Manager Current Branch 之后，请勿使用基准版本以保持最新状态。 而是仅使用[控制台中更新](/sccm/core/servers/manage/install-in-console-updates)来更新到最新版本。  

- 我们会定期发布其他基准版本。 使用最新基准版本安装新的层次结构时，应避免安装过期或不受支持的 Configuration Manager 版本，然后再次升级基础结构以使其保持最新状态。  

安装基准版本之后，其他版本的 Configuration Manager 都可用作控制台中更新。 控制台中更新可将你的基础结构更新为最新版本的 Configuration Manager。  

- 请安装控制台中更新来更新顶层站点的版本。  

- 子主站点会自动安装管理中心站点安装的更新。 通过在主站点使用维护时段来控制此时间。  

- 手动在控制台中将辅助站点更新到新的更新版本。  

安装更新时，更新会将该版本的安装文件存储在站点服务器上名为 CD.Latest 的文件夹中  。 有关这些文件的详细信息，请参阅 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)。  

- 在站点恢复期间，使用 CD.Latest 文件夹中的文件。 另外，层次结构不再运行基准版本时，请使用这些文件来安装其他站点。  

- 不能使用 CD.Latest 中的安装文件来安装新层次结构的首个站点，或从 System Center 2012 Configuration Manager 升级站点。  

### <a name="version-details"></a>版本详细信息

Configuration Manager 的某些更新可用作现有基础结构的控制台中更新版本，以及新的基准版本。  

#### <a name="supported-versions"></a>支持的版本

以下受支持版本的 Configuration Manager 目前可用作基准和/或更新：  

| 版本 | 可用日期 | [支持结束日期](/sccm/core/servers/manage/current-branch-versions-supported) | Baseline | 控制台内更新 |  
|-------------|-----------|------------|--------------|------------------------|  
| [1902](/sccm/core/plan-design/changes/whats-new-in-version-1902)<br /><br /> 5.00.8790.1000 | 2019 年 3 月 27 日 | 2020 年 9 月 27 日 | 是<sup>[注释 1](#bkmk_note1)</sup> | 是 |
| [1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)<br /><br /> 5.00.8740.1000 | 2018 年 11 月 27 日 | 2020 年 5 月 27 日 | 否 | 是 |
| [1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)<br /><br /> 5.00.8692.1000 | 2018 年 7 月 31 日 | 2020 年 1 月 31 日 | 否 | 是 |
| [1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)<br /><br /> 5.00.8634.1000 | 2018 年 3 月 22 日 | 2019 年 9 月 22 日 | 是<sup>[注释 1](#bkmk_note1)</sup> | 是 |
| [1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)<br /><br /> 5.00.8577.1000 | 2017 年 11 月 20 日 | 2019 年 5 月 20 日 | 否 | 是 |

<a name="bkmk_note1"></a>

> [!Note]  
> <sup>备注 1：</sup>  在[批量许可服务中心](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC)，基线介质在以下版本中提供：
>
> - System Center Config Mgr (Current Branch)
> - System Center 2016 Datacenter
> - System Center 2016 Standard  
>
> 例如，在 VLSC 中搜索 `System Center Config Mgr (current branch)`。 在文件列表中找到基线介质，然后下载对应的版本。  

#### <a name="historical-versions"></a>历史版本

下表列出了不受支持的 Configuration Manager Current Branch 的历史版本：

| 版本 | 可用日期 | 支持结束日期 | Baseline | 控制台内更新 |  
|-------------|-----------|------------|--------------|------------------------|  
| 1706 <br /><br /> 5.00.8540.1000 | 2017 年 7 月 31 日 | 2018 年 7 月 31 日 | 否 | 是 |
| 1702 <br /><br /> 5.00.8498.1000 | 2017 年 3 月 27 日 | 2018 年 3 月 27 日 | 是 | 是 |
| 1610 <br /><br /> 5.00.8458.1000 | 2016 年 11 月 18 日 | 2017 年 11 月 18 日 | 否 | 是 |
| 1606 <br /><br /> 5.00.8412.1000 | 2016 年 7 月 22 日 | 2017 年 7 月 22 日 | 否 | 是 |
| 1606 和 1606 修补程序汇总 (KB3186654) <br><br>5.00.8412.1307 | 2016 年 10 月 12 日 | 2017 年 10 月 12 日 | 是 | 否 |
| 1602<br /><br /> 5.00.8355.1000 | 2016 年 3 月 11 日 | 2017 年 3 月 11 日 | 否 | 是 |
| 1511 <br /><br /> 5.00.8325.1000 | 2015 年 12 月 8 日 | 2016 年 12 月 8 日 | 是 | 否 |  

#### <a name="how-to-check-the-version"></a>如何检查版本

若要查看 Configuration Manager 站点的版本，请转到控制台左上角的“关于 System Center Configuration Manager”  。 对话框会显示站点和控制台版本。  

> [!Note]  
> 从 1802 版开始，控制台版本现在与站点版本略有不同。 控制台的次要版本现在对应于 Configuration Manager 发行版。 例如，在 Configuration Manager 1802 版中，初始站点版本为 5.0.8634.1000，初始控制台版本为 5.**1802**.1082.1700。 内部版本号 (1082) 和修订版本号 (1700) 可能会随 1802 发行版的未来修补程序而变化。


## <a name="bkmk_inconsole"></a> 控制台中更新和服务  

使用 Configuration Manager Current Branch 的生产就绪型安装时，可通过“更新和维护服务”渠道获得大部分更新  。 此方法可标识、下载并提供适用于当前基础结构版本和配置的更新。 它仅包含 Microsoft 为所有客户推荐的更新。

这些更新包括：  

- 新版本，如版本 1806、1810 或 1902。  

- 包括当前版本新功能的更新。

- 修补程序，适用于你的 Configuration Manager 版本，所有客户都应安装。

    > [!Note]  
    > 从 1902 版本开始，控制台内修补程序现具有取代关系。 有关详细信息，请参阅[控制台内修补程序的取代](#bkmk_supersede)。

控制台中更新可提供更强的稳定性并解决常见的问题。 它们可替代早期产品版本的更新类型，如服务包、累积更新、适用于所有客户的修补程序以及 Microsoft Intune 的扩展。

这些控制台中更新可应用于以下一种或多种系统：  

- 主站点和管理中心站点服务器  

- 站点系统角色和站点系统服务器  

- SMS 提供程序的实例  

- Configuration Manager 控制台  

- Configuration Manager 客户端  

Configuration Manager 可为你发现新的更新。 使用 Microsoft 云服务同步 Configuration Manager 服务连接点时，注意以下行为：  

- 当服务连接点处于联机模式时，站点每天都会与 Microsoft 同步。 它会自动确定适用于基础结构的新更新。 要下载更新和可再发行的文件，承载服务连接点站点系统角色的计算机需使用“系统”上下文访问以下 Internet 位置：go.microsoft.com 和 download.microsoft.com  。 有关服务连接点使用的其他位置的详细信息，请参阅 [Internet 访问要求](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)。  

- 当服务连接点处于脱机模式时，请使用服务连接工具手动与 Microsoft 云同步。 有关详细信息，请参阅[使用服务连接工具](/sccm/core/servers/manage/use-the-service-connection-tool)。  

- 凭借控制台中更新，无需再单独查找和安装单个更新、服务包和新功能。  

- 仅安装选择的控制台中更新。 安装某些更新时，可以选择启用或使用个别功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。  

安装控制台中更新时会出现以下过程：  

- 它将自动运行先决条件检查。 也可以先手动运行此检查，然后再开始安装。  

- 它安装在环境中的顶级站点上。 此站点是管理中心站点（如果有）。 在层次结构中，更新会在主站点上自动安装。 可以通过使用[站点服务器的服务时段](/sccm/core/servers/manage/service-windows)控制允许每个主站点服务器更新的时间。  

- 站点服务器更新后，会自动更新受影响的所有站点系统角色。 这些角色包括 SMS 提供程序的实例。 站点安装更新后，Configuration Manager 控制台还会提示控制台用户更新控制台。  

- 如果更新包括 Configuration Manager 客户端，还会提供在预生产中测试更新或立即将更新应用到所有客户端的选项。  

- 更新主站点后，辅助站点不会自动更新。 而是必须手动启动辅助站点更新。  

> [!NOTE]  
> Configuration Manager Current Branch、Long-Term Servicing Branch 和 Technical Preview Branch 是不同的版本。 适用于一个分支的更新无法作为其他分支的控制台中更新。 有关可用分支的详细信息，请参阅[我应使用 Configuration Manager 的哪一个分支？](/sccm/core/understand/which-branch-should-i-use)

### <a name="bkmk_supersede"></a> 控制台内修补程序的取代

<!-- 3229613 -->
从 1902 版本开始，控制台内修补程序现具有取代关系。 Microsoft 发布新的 Configuration Manager 修补程序时，控制台不会显示任何由这个新的修补程序取代的修补程序。 这一新行为可帮助你更好地确定要安装哪些修补程序。

### <a name="supersedence-example"></a>取代示例

有三个修补程序可用：Hotfix-A、Hotfix-B 和 Hotfix-C。 Hotfix-B 取代 Hotfix-A，Hotfix-C 取代 Hotfix-B。

|Hotfix-A|Hotfix-B|Hotfix-C|控制台内视图|
|--------|--------|--------|---------------|
|未安装|未安装|未安装|显示全部的三个修补程序|
|已安装|已安装|未安装|Hotfix-B 显示为已安装<br/>Hotfix-C 显示为已准备好安装|
|未安装|未安装|已安装|Hotfix-C 显示为已安装|


## <a name="bkmk_outofband"></a> 带外修补程序  

在处理特定问题方面，某些修补程序会有一定限制。 其他修补程序适用于所有客户，但无法使用控制台中方法进行安装。 这些修补程序在带外提供，Microsoft 云服务不会发现。  

通常情况下，如果正在寻求修复或解决 Configuration Manager 部署问题的方法，可通过 Microsoft 客户支持服务、Microsoft 支持知识库文章或 [Configuration Manager 团队博客](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog)了解带外修补程序。

请使用以下两种方法中的一种方法来手动安装这些修补程序：  

#### <a name="update-registration-tool"></a>更新注册工具

此工具用于将修补程序手动导入 Configuration Manager 控制台。 然后按照安装自动发现的控制台中更新的方法来安装更新。  

此方法适用于采用以下文件名结构的修补程序：  
    `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

有关详细信息，请参阅[使用更新注册工具导入修补程序](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)。  

#### <a name="hotfix-installer"></a>修补程序安装程序

使用此工具可手动安装无法使用控制台内方法安装的修补程序。  

此方法适用于采用以下文件名结构的修补程序：  
    `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

有关详细信息，请参阅[使用修补程序安装程序安装更新](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates)。  


## <a name="next-steps"></a>后续步骤

以下文章可帮助了解如何为 Configuration Manager 查找和安装不同更新类型：  

- [安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates)  

- [使用服务连接工具](/sccm/core/servers/manage/use-the-service-connection-tool)  

- [使用更新注册工具导入修补程序](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

- [使用修补程序安装程序安装更新](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates)  

有关技术预览分支的详细信息，请参阅[技术预览](/sccm/core/get-started/technical-preview)。
