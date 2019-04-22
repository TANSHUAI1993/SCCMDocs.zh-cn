---
title: 应用程序运行状况分析器
titleSuffix: Configuration Manager
description: 用于评估应用程序运行状况分析器桌面 Analytics 中使用的兼容性的操作方法指南。
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2af150a4-0c18-4b40-8492-c04c5d154596
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 21b4907667e055c9595b31eedf9da0ad516b5fec
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802251"
---
# <a name="how-to-assess-compatibility-with-app-health-analyzer"></a>如何评估应用程序运行状况分析器与兼容性

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

使用 Desktop 分析的应用程序运行状况分析器工具包来评估桌面应用程序兼容性问题。 它有助于将精力集中验证对于桌面应用程序包括业务线应用。 该工具提供了以及可能的更正操作的风险评级。 它还包括应用程序准备情况报告来帮助您评估 Windows 10 升级的应用程序准备情况。



## <a name="download"></a>下载

下载工具包[Microsoft Download Center](http://download.microsoft.com/download/3/7/D/37D7E378-D805-4822-A712-4EADBF50FC08/AppHealthAnalyzer.zip)<!-- (https://www.microsoft.com/download/details.aspx?id=57276) -->。 始终使用最新版本。

下载是一个 Windows Installer (MSI) 文件。 用户的计算机上安装的应用程序运行状况分析器工具包。 在运行该工具包时，向导将指导您完成创建应用程序准备情况报告的过程。

该工具包包括示例脚本。 如果需要自动执行整个组织中的设备中的准备情况信息的集合，使用 Configuration Manager 部署这些脚本。 有关详细信息，请参阅[自动化](#automation)。



## <a name="how-it-works"></a>其工作原理

该工具将执行在设备已安装的应用程序的静态分析。 它不执行打包应用安装程序的分析。 用户无需以运行该应用程序。 该工具会评估所有已安装的应用程序注册到 Windows 设备上。

应用程序运行状况分析器不需要维护的不主动管理的旧应用程序的安装程序。 它指出了其安装状态中的应用程序兼容性问题。 所有应用的预定义的兼容性规则都评估。 这些信号是常见普遍的问题报告给 Microsoft，当客户升级到 Windows 10。 兼容性 insights 还包括可能的补救措施或修补程序。 如果你有问题的应用，开始使用建议的操作。

> [!Important]  
> 该工具包不支持功能来修复或解决您的应用程序。 如果您创建应用程序准备情况报告，它提供见解和指南，帮助您在升级到 Windows 10 之前修复您的应用程序。  



## <a name="prerequisites"></a>先决条件

之前安装和使用该工具包，请确保设备满足以下要求：  

- Windows 7 Service Pack 1 或更高版本  

- 在设备上具有管理员权限  

- Microsoft.NET Framework 4.5.1 或更高版本  

- 在 Desktop 分析服务，其中包括以下要求中注册：  

    - 最新的更新。 有关详细信息，请参阅[更新设备](/sccm/desktop-analytics/enroll-devices#update-devices)。  

    - 诊断数据级别。 有关详细信息，请参阅[诊断数据级别](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)。  



## <a name="analyze"></a>分析

1. 安装到目标设备的应用程序运行状况分析器。 默认情况下，它安装到以下路径： `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`  

2. 转到 Windows**启动**菜单中，展开**Microsoft 应用程序运行状况分析器**组，然后打开**应用程序运行状况分析器**以管理员身份。 可能需要几分钟时间才能生成报表。  

    > [!Note]  
    > 如果未配置任何所需的诊断数据设置，您将看到一个错误。 请确保正确配置的必备组件的设置。 有关详细信息，请参阅[诊断数据级别](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)。  

3. 应用程序准备情况报告打开后，它将启动评估应用程序。 等待该工具包就可以完成，这可能需要时间取决于在设备上的应用程序的数量。  

![应用程序准备情况报告的应用程序运行状况分析器的屏幕截图](media/app-readiness-report-evaluating.png)

可以最小化窗口并继续执行其他任务时在后台运行，该工具包。


### <a name="app-readiness-report-features"></a>应用程序准备情况报表功能

#### <a name="get-started"></a>入门

此选项卡提供此当前版本中受支持的信号的概述。 它还包括可能的补救措施。

#### <a name="insights"></a>Insights

此选项卡提供了该工具评估的所有应用的视图。 它显示的风险评估和确定兼容性问题的使用的各种信号。

- **信号**菜单：通过使用在左侧菜单的信号筛选这些应用程序  

- **导出 CSV**:导出为逗号分隔值 (CSV) 文件，这些见解  

- **重新扫描应用程序**:如果安装任何新应用程序，请使用此选项以重新运行该工具  

- **故障排除 ID**:如果设备已安装的应用，但请参阅在报表中的任何见解，为提供此 ID 才可支持  

#### <a name="desktop-analytics"></a>桌面分析

此选项卡提供了如何使用应用程序运行状况分析器来为应用提供准备情况的见解，在组织内的概述。



## <a name="automation"></a>自动化

若要深入了解这些应用多个设备，部署应用程序运行状况分析器命令行版本与 Configuration Manager。 将其部署到一小组的代表组织中的设备。 例如，使用 Desktop 分析*试验*集合。 相同[先决条件](#prerequisites)适用于这些设备。

在执行更广泛的部署之前, 先验证成功运行。 请确保在桌面 Analytics 中显示任何数据。

应用程序运行状况分析器 toolkit 包含的示例脚本，run_silent.cmd。 默认情况下，此脚本位于以下路径： `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`。 使用此脚本来自动执行过程与 Configuration Manager。


### <a name="tips"></a>提示

- 升级到目标操作系统之前，将应用程序运行状况分析器部署到你的试点中的所有设备。 若要获取有效的准备情况的见解，它至少运行一次部署计划的试验组。  

- 桌面分析具有内置功能可建议试验组的部署计划。 若要获取完整的覆盖范围对你重要的应用程序的所有试验设备上运行该工具包。  

- 计划要在运行时用户未登录，或不使用该设备时的工具。  

- 配置重复执行的计划。 例如，运行它每隔 30 天。 此计划从你的设备，以帮助他们了解最新功能中获取最新的准备情况见解。  



## <a name="desktop-analytics-integration"></a>桌面 Analytics 集成

从桌面分析下面的屏幕截图显示了 ContosoApp 版本 1.15.25 的详细信息。

- 它具有**中等**风险评估  
- 提供了采用的版本  
- 它具有驱动程序依赖关系  

![显示应用程序兼容性风险因素的 Analytics 桌面](media/aha-desktop-analytics-compat-risk-factors.png)



## <a name="troubleshooting"></a>故障排除

本部分介绍的故障排除步骤和最常见的操作问题，可能会看到与应用程序运行状况分析器。 例如：

- 看不到应用程序运行状况分析器中的欢迎屏幕  

- 在设备上安装的应用，但未看到应用程序准备情况报告中的任何见解  

- 没有任何反应在运行工具  

### <a name="diagnostic-data-settings"></a>诊断数据设置

请仔细检查 Windows 诊断数据设置的配置。 配置管理器应设置这些值时设备加入 Desktop 分析。 作为一种解决方法，可以使用其他方法，例如脚本或组策略。 有关详细信息，请参阅[诊断数据级别](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)。  

### <a name="verbose-mode"></a>详细模式

在详细模式与 run_verbose.cmd 脚本运行该工具。 默认情况下，脚本位于以下路径： `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\run_verbose.cmd`

详细模式生成其他日志，可帮助您解决潜在问题。 它将保存到日志`LogCollection`文件夹中的安装位置。 例如，默认日志集合路径为： `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\LogCollection\`


## <a name="see-also"></a>另请参阅

FastTrack 中心权益适用于 Windows 10 的连接可以访问**桌面应用程序确保**。 这一优势是设计用于 Windows 10 和 Office 365 专业增强版应用程序兼容性的解决问题的新服务。 有关详细信息，请参阅[桌面应用程序确保](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure)。
