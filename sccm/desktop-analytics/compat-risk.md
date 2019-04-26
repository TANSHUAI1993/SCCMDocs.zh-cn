---
title: Windows 应用兼容性风险
titleSuffix: Configuration Manager
description: 了解有关桌面 Analytics 中的 Windows 应用程序的兼容性风险。
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bf2114ac77a75fedc18c38a8d373b9c0a1ada591
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62206571"
---
# <a name="compatibility-risk-for-windows-apps-in-desktop-analytics"></a>用于 Windows 桌面 Analytics 中的应用程序兼容性风险

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

Windows Analytics 中的升级评估了泛型类型，例如：需要注意或修补程序可用。 它不提供有关如何确定问题的应用程序的优先级或升级 insights 任何可视的指示器。 桌面分析将使用此功能替换**兼容性风险**。 桌面分析仅在升级前方案部署视图中显示应用的应用风险评估。 它将基于当前的部署计划中包含的计算机从 Microsoft 获取的见解的应用。

桌面分析使用以下的兼容性风险类别：

- **低**：找到该服务没有信号以 Windows 为此应用程序置于危险升级。 很可能会继续作为目标 OS 上运行的是。  

- **中等**:分析用于指示应用程序可能会有障碍的功能，但是修正是可能的可能。  

- **高**:应用程序是几乎可以肯定期间或之后升级失败。 它可能需要修复。  

- **未知**：应用程序不被评估应用程序运行状况分析器。 如有任何其他见解*MS 已知问题*或*准备用于 Windows*。  



## <a name="risk-assessment-engine"></a>风险评估引擎

有多个来源的应用程序运行状况分析器用于生成风险评级。

![应用程序运行状况分析器风险评估引擎领域的关系图](media/aha-risk-assessment-engine.png)


### <a name="ms-known-issues"></a>MS 的已知问题

应用程序运行状况分析器来看待 Microsoft 应用程序兼容性数据库的任何已知问题。 它使用此数据库来确定任何现有的兼容性块的公开可用的应用程序从 Microsoft 或其他发布服务器。 此检查仅适用于您选择的部署计划将目标操作系统。


### <a name="ready-for-windows"></a>准备好进行 Windows

[准备用于 Windows](https://www.readyforwindows.com)应用目录相关联的设备上报告与来自 Microsoft 的其他检查，如兼容性块的相同应用其他客户的诊断数据。 

可能的类别包括：

- **数据不足**意味着太少商业的 Windows 10 设备共享此应用程序，以便 Microsoft 对其采用率进行分类的信息。

- **采用**意味着至少 10,000 个商用 Windows 10 设备上安装了应用程序。  

- **高度采用**意味着至少 10 万商业的 Windows 10 设备上安装了应用程序。  

- **请联系开发人员**意味着可能与此解决方案中，兼容性问题，因此 Microsoft 建议联系软件提供商以了解详细信息。  

### <a name="app-health-analyzer-signals-for-compatibility-assessment"></a>应用程序运行状况分析器信号兼容性评估

使用的应用程序运行状况分析器工具包来收集有关应用程序兼容性的其他信号。 有关详细信息，请参阅[应用程序运行状况分析器](/sccm/desktop-analytics/app-health-analyzer)。

以下信号是当前可用：

#### <a name="adopted-version-available"></a>采用的可用版本

还有其他客户高度采用此应用程序的另一个版本。 此信号从准备好的 Windows 中使用的数据。 如果有任何与当前版本的升级阻塞程序，请考虑改为部署的替代版本。

#### <a name="16-bit"></a>16 位

删除所有的 16 位组件从应用程序，并使用 32 位或 64 位等效信息替换。 有关详细信息，请参阅[Windows Vista 和 Windows Server 2008 开发人员故事：应用程序兼容性指南](https://msdn.microsoft.com/library/aa480152.aspx)。

另一个选项是为支持 Windows 10 上启用 NT 虚拟 DOS 计算机 (NTVDM)。

#### <a name="requires-admin-privileges"></a>需要管理员权限

应用程序要求用户具有管理访问权限的设备。 使用这些应用需要管理员权限的应用程序清单。 有关详细信息，请参阅[创建和应用程序清单嵌入](https://msdn.microsoft.com/library/bb756929.aspx)。
<!--Is this a better, more current link? https://docs.microsoft.com/windows/desktop/sbscs/application-manifests-->

桌面的分析建议适用于试验测试的应用。 它应正常的试验，但您会发现任何回归。

#### <a name="java-dependency"></a>Java 依赖项

很多 Java 应用程序依赖于上单独安装 Java Runtime Environment (JRE)。 当较旧的 JRE 版本可继续在 Windows 10 上工作时，Oracle 将仅支持最新的 JRE 版本。 使用较早的不支持的 JRE 可能会产生安全漏洞。 检查你的应用程序在最新的 JRE 版本上运行。

#### <a name="not-dpi-aware"></a>非 DPI 感知

Windows 10 上，应用程序可能具有高级的屏幕分辨率的显示问题。 使用应用程序清单以避免与高 DPI 分辨率的任何问题。 有关详细信息，请参阅[应用程序清单](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests)。

桌面的分析建议适用于试验测试的应用。 它应正常的试验，但您会发现任何回归。

#### <a name="visual-basic-version-6-vb6"></a>Visual Basic 版本 6 (VB6)

桌面的分析建议适用于试验测试的应用。 VB6 应用程序通常是兼容的。 如果应用在试点期间 regresses 由于任何其他依赖项或小组件，则应更新应用到 Visual Basic.NET

#### <a name="os-version-dependency"></a>OS 版本依赖关系

请考虑重新开发应用程序以使用版本帮助程序 API 或清单到目标 Windows 10 应用程序。

桌面的分析建议适用于试验测试的应用。 它应正常的试验，但您会发现任何回归。

#### <a name="silverlight-framework"></a>Silverlight framework

Microsoft 建议非基于浏览器的应用不使用 Silverlight。 Silverlight 5 的支持结束日期是年 10 月 2021年。

最新的 web 浏览器不支持 Silverlight。

| 浏览器 | 支持 |
|---------|---------|
| Google Chrome | 终止支持时间：2015 年 9 月 |
| Firefox | 终止支持时间：2017 年 3 月 |
| Microsoft Edge | 没有可用的插件 |

桌面的分析建议适用于试验测试的应用。 它应正常的试验，但您会发现任何回归。

#### <a name="net-framework-1011"></a>.NET framework 1.0/1.1

在 Windows 10 上不支持.NET framework 1.0 版。 版本 1.1 中不允许在 Windows 10 上。 如果应用是从第三方发布者，请联系供应商联系以请求与 Windows 10 兼容的版本。 否则，重新开发应用程序以使用受支持的.NET 版本。

#### <a name="net-framework-2030"></a>.NET framework 2.0/3.0

在 Windows 10 上支持.NET 2.0 和 3.5 框架。 您可能需要启用 Windows 功能。 有关详细信息，请参阅[在 Windows 10 上安装.NET Framework 3.5](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10)。

#### <a name="ui-access"></a>UI 访问

使用 UI 访问应用程序可以绕过用户界面控制级别，以将输入到高特权的 windows 桌面上。 仅为用户界面辅助技术应用程序中使用此设置。

如果您不使用辅助功能应用程序中，为 false 的应用程序清单中设置 UI 访问标志。 有关详细信息，请参阅[创建和应用程序清单嵌入](https://msdn.microsoft.com/library/bb756929.aspx)。

#### <a name="driver-dependency"></a>驱动程序依赖关系

该应用是依赖于驱动程序。 桌面的分析建议适用于试验测试的应用。 它应正常的试验，但您会发现任何回归。 如果有任何疑问，请联系发布者请求与 Windows 10 兼容的版本。



## <a name="app-confidence-simulation-for-a-sample-population"></a>应用样本总体的置信度模拟

下图是从示例案例研究。 此数据会突出显示应用程序运行状况分析器使用 Desktop 分析应用程序验证到采用数据驱动方法的使用。 这种方法可以帮助减少时间和精力在 Windows 10 升级过程中测试您的应用程序。

此数据显示 60 899 应用程序，包括业务线应用与设备的置信度度量值。

![之前和之后显示应用置信度的图表](media/aha-app-confidence-simulation.png)


## <a name="see-also"></a>另请参阅

FastTrack 中心权益适用于 Windows 10 的连接可以访问**桌面应用程序确保**。 这一优势是设计用于 Windows 10 和 Office 365 专业增强版应用程序兼容性的解决问题的新服务。 有关详细信息，请参阅[桌面应用程序确保](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure)。
