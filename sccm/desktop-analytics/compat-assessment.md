---
title: 兼容性评估
titleSuffix: Configuration Manager
description: 了解有关桌面分析中的 Windows 应用和驱动程序的兼容性评估。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6181f0e1a502d701ca7337641013a18b03251f9
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536002"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>桌面分析中的兼容性评估

> [!Note]  
> 此信息与预览版服务相关, 该服务可能会在商业发布之前进行大量修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

Windows Analytics 中的升级评估是通用的, 例如:需要注意或已修复。 它不提供有关如何对应用程序或驱动程序的问题或升级见解进行排序的任何可视指示器。 桌面分析将此功能替换为**兼容性风险**。 桌面分析只显示针对升级前方案的部署视图中应用的评估。 它基于从当前部署计划中包含的计算机获得的见解对应用进行分类。

桌面分析使用以下兼容性评估类别:

- **低**：该服务未找到任何信号来使此应用程序面临 Windows 升级的风险。 可能会按原样处理目标操作系统。  

- **中**:分析表明, 应用程序可能具有受损的功能, 但可能会发生修正。  

- **高**:在升级过程中或升级之后, 应用程序几乎会出现故障。 可能需要进行修正。  

- **未知**：未评估应用。 没有其他见解, 如*MS 已知问题*或*Windows 就绪*。  

在部署计划中的应用程序或驱动程序资产列表中, 你将在 "**兼容性风险**" 列中看到每个资产的此值。


## <a name="app-risk-assessment"></a>应用风险评估

![应用风险评估源示意图](media/app-risk-assessment-sources.png)

桌面分析使用多个源来生成应用程序的评估分级:

- [Microsoft 已知问题](#microsoft-known-issues)
- [Windows 目录就绪](#ready-for-windows)
- [高级见解](#advanced-insights)

可以在 "桌面分析" 中找到应用的每个源的评估。 在部署计划中的应用资产列表中, 选择单个应用以打开其 "属性" 浮出控件窗格。 你将看到整体建议和评估级别。 "**兼容性风险因素**" 部分显示了这些评估的详细信息。


## <a name="microsoft-known-issues"></a>Microsoft 已知问题

桌面分析查看 Microsoft 应用程序兼容性数据库中的任何已知问题。 它使用此数据库来确定适用于 Microsoft 或其他发布者的公开可用应用程序的任何现有兼容性块。 此检查仅适用于所选部署计划的目标操作系统。

你将在 "应用程序属性" 窗格中看到以下问题作为**MS 已知问题**:

### <a name="application-is-removed-during-upgrade"></a>升级过程中删除了应用程序

Windows 检测到的兼容性问题。 应用程序不会迁移到新的操作系统版本。 若要继续升级, 无需执行任何操作。

### <a name="blocking-upgrade"></a>阻止升级

Windows 检测到阻止问题, 因此在升级期间无法删除应用程序。 它可能不适用于新的操作系统版本。 升级之前, 请删除该应用程序。 在新的操作系统版本上重新安装并测试。

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>阻止升级, 但在升级后可以重新安装

应用程序与新的操作系统版本兼容, 但不会迁移。 请在升级 Windows 之前删除该应用程序。 请在新的操作系统版本上重新安装它。

### <a name="blocking-upgrade-update-application-to-newest-version"></a>阻止升级, 将应用程序更新到最新版本

现有的应用程序版本与新的操作系统版本不兼容, 因此不会迁移。 提供应用程序的兼容版本。 升级之前, 请更新应用程序。

### <a name="disk-encryption-blocking-upgrade"></a>磁盘加密阻止升级

应用程序的加密功能会阻止升级。 在升级 Windows 之前禁用加密功能, 并在升级后启用它。

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>不适用于新操作系统, 但不会阻止升级

应用程序与新的操作系统版本不兼容, 但不会阻止升级。 若要继续升级, 无需执行任何操作。 在新的操作系统版本上安装应用程序的兼容版本。

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>不适用于新操作系统, 将阻止升级

应用程序与新的操作系统版本不兼容, 将阻止升级。 请在升级前删除该应用程序。 可以使用应用程序的兼容版本。

### <a name="evaluate-application-on-new-os"></a>评估新操作系统上的应用程序

Windows 将迁移应用程序, 但它检测到可能影响应用程序在新操作系统版本上的性能的问题。 若要继续升级, 无需执行任何操作。 在新的操作系统版本上测试应用程序。

### <a name="may-block-upgrade-test-application"></a>可能会阻止升级、测试应用程序

Windows 检测到可能会干扰升级, 但需要进一步调查的问题。 在升级过程中测试应用程序的行为。 如果它阻止升级, 请在升级前将其删除。 然后重新安装它, 并测试新的操作系统版本。

### <a name="multiple"></a>多个

多个问题会影响应用程序。 选择 "**查询**" 以查看 Windows 检测到的问题的详细信息。

### <a name="reinstall-application-after-upgrading"></a>升级后重新安装应用程序

应用程序与新的操作系统版本兼容, 但在升级 Windows 后需要重新安装它。 升级过程将删除该应用程序。 若要继续升级, 无需执行任何操作。 在新的操作系统版本上重新安装应用程序。


## <a name="ready-for-windows"></a>适用于 Windows

"[适用于 Windows](https://www.readyforwindows.com)应用程序目录" 与下列数据源关联:

- 来自其他报告相同应用的客户的诊断数据
- 来自 Microsoft 的其他检查, 例如设备上的兼容性块

可能的类别包括:

- **严格采用**:至少100000商用 Windows 10 设备已安装此应用。  

- **采用**:至少10000商用 Windows 10 设备已安装此应用。  

- **数据不足**:商业 Windows 10 设备太少共享此应用程序的信息, 因此无法对其采用进行分类。

- **联系开发人员**:此版本的应用程序可能存在兼容性问题。 Microsoft 建议联系软件提供商以了解详细信息。 有关详细信息, 请参阅[Windows 就绪](https://www.readyforwindows.com/)。  

- **未知**：此应用程序的此版本无法使用 Windows 信息。 可以在适用于[Windows](https://www.readyforwindows.com/)的应用程序的其他版本中使用此信息。  

### <a name="support-statement"></a>支持语句

如果软件提供程序在 Windows 10 上支持此应用程序的一个或多个版本, 则会在应用程序的 "属性" 窗格中看到此语句。 在 "兼容性风险因素" 部分中, 查看**支持声明**。



## <a name="advanced-insights"></a>高级见解

桌面分析还可以使用以下其他见解来检测问题:

### <a name="adopted-version-available"></a>采用的可用版本

此应用的另一个版本已由其他客户使用。 此信号使用适用于 Windows 的数据。 如果当前版本存在任何升级拦截程序, 请考虑改为部署替代版本。

### <a name="driver-dependency"></a>驱动程序依赖关系

该应用程序依赖于驱动程序。 桌面分析建议应用程序进行试验性测试, 以发现任何退化。 如果有任何问题, 请与发布者联系以请求符合 Windows 10 的版本。

### <a name="additional-insights"></a>其他见解

<!-- 4021225 -->
将 Configuration Manager 站点和客户端更新到版本1906时, 客户端还会报告这些其他见解:

> [!Important]  
> 若要利用 Configuration Manager 的新功能，更新站点后，还请将客户端更新到最新版本。 如果客户端版本也是最新的, 则此方案不起作用。

#### <a name="16-bit-apps"></a>16位应用

从应用程序中删除所有16位组件, 并将替换为32位或64位的等效组件。 有关详细信息, 请[参阅 windows Vista 和 windows Server 2008 开发人员情景:应用程序兼容](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\))性指南。

另一种方法是启用 NT 虚拟 DOS 机 (NTVDM) 以支持 Windows 10。

#### <a name="requires-admin-privileges"></a>需要管理员权限

应用要求用户具有设备的管理访问权限。 为需要管理员权限的应用程序使用应用程序清单。 有关详细信息, 请参阅[创建和嵌入应用程序清单](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\))。

桌面分析建议应用程序进行试验性测试, 以发现任何退化。

#### <a name="java-dependency"></a>Java 依赖项

许多 Java 应用程序依赖于单独安装的 Java Runtime Environment (JRE)。 尽管较旧的 JRE 版本可能会继续在 Windows 10 上运行, 但 Oracle 仅支持最新的 JRE 版本。 使用不受支持的旧 JRE 可能会产生安全漏洞。 检查应用程序是否在最新的 JRE 版本上运行。

#### <a name="not-dpi-aware"></a>不能识别 DPI

应用可能会显示 Windows 10 上的高级屏幕分辨率出现问题。 使用应用程序清单以避免出现高 DPI 分辨率问题。 有关详细信息, 请参阅[应用程序清单](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests)。

桌面分析建议应用程序进行试验性测试, 以发现任何退化。

#### <a name="silverlight-framework"></a>Silverlight 框架

Microsoft 建议非基于浏览器的应用不使用 Silverlight。 Silverlight 5 的支持结束日期为10月2021。

大多数当前 web 浏览器不支持 Silverlight。

| 浏览者 | 支持 |
|---------|---------|
| Google Chrome | 支持结束:2015年9月 |
| Firefox | 支持结束:2017 年 3 月 |
| Microsoft Edge | 无可用插件 |

桌面分析建议应用程序进行试验性测试, 以发现任何退化。

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1。1

Windows 10 不支持 .NET Framework 版本1.0。 版本1.1 在 Windows 10 上不兼容。 如果应用来自第三方发布者, 请与供应商联系, 请求符合 Windows 10 的版本。 否则, 请 redevelop 该应用程序使用受支持的 .NET 版本。

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3。0

Windows 10 上支持 .NET 2.0 和3.5 框架。 可能需要启用 Windows 功能。 有关详细信息, 请参阅[在 Windows 10 上安装 .NET Framework 3.5](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10)。

#### <a name="ui-access"></a>UI 访问

具有 UI 访问权限的应用程序可以绕过用户界面控制级别来驱动桌面上的更高权限窗口的输入。 仅对用户界面辅助技术应用程序使用此设置。

如果你未在应用中使用辅助功能, 请在应用程序清单中将 "UI 访问标志" 设置为 "false"。 有关详细信息, 请参阅[创建和嵌入应用程序清单](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\))。

桌面分析建议应用程序进行试验性测试, 以发现任何退化。


## <a name="driver-risk-assessment"></a>驱动程序风险评估

桌面分析还按可用性列出并分组不迁移到操作系统版本的任何驱动程序。

可以在 "桌面分析" 中找到有关驱动程序的评估。 在部署计划中的驱动程序资产列表中, 选择单个驱动程序以打开其 "属性" 浮出控件窗格。 你将看到整体建议和评估级别。 "**兼容性风险因素**" 部分显示了这些评估的详细信息。

| 驱动程序可用性 | 是否需要执行操作？ | 含义 | 指导 |
|---------------------|------------------|---------------|----------|
| 可用内置 | 否, 仅用于识别 | 当前安装的应用程序或驱动程序版本不会迁移到新的操作系统版本。 与新的操作系统版本一起安装了兼容的版本。 | 若要继续升级, 无需执行任何操作。 |
| 从 Windows 更新导入 | 是 | 当前安装的驱动程序版本不会迁移到新的操作系统版本。 Windows 更新提供兼容的版本。 | 如果计算机自动接收来自 Windows 更新的更新, 则无需执行任何操作。 否则, 请在升级 Windows 后从 Windows 更新导入新的驱动程序。 |
| 可用内置和 Windows 更新 | 是 | 当前安装的驱动程序版本不会迁移到新的操作系统版本。 尽管升级过程中安装了新的驱动程序, 但 Windows 更新提供了较新版本。 | 如果计算机自动接收来自 Windows 更新的更新, 则无需执行任何操作。 否则, 请在升级 Windows 后从 Windows 更新导入新的驱动程序。 |
| 与供应商核实 | 是 | 驱动程序不会迁移到新的操作系统版本, 桌面分析无法找到兼容的版本。 | 对于解决方案, 请咨询制造驱动程序的独立硬件供应商 (IHV), 或提供设备的原始设备制造商 (OEM)。 |


## <a name="see-also"></a>另请参阅

适用于 Windows 10 的 FastTrack 中心权益提供对**桌面应用程序**的访问。 此优势是一项新服务, 旨在解决 Windows 10 和 Office 365 ProPlus 应用程序兼容性问题。 有关详细信息, 请参阅[桌面应用确保](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure)。
