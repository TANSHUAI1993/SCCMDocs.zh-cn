---
title: 兼容性评估
titleSuffix: Configuration Manager
description: 了解有关适用于 Windows 应用和桌面分析中的驱动程序兼容性评估。
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bef2c11732177dfb842f0961dc2d5d5a69edd55e
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67148094"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>在桌面 Analytics 中的兼容性评估

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

Windows Analytics 中的升级评估了泛型类型，例如：需要注意或修补程序可用。 它不提供有关如何确定应用程序或驱动程序问题的优先级或升级 insights 任何可视的指示器。 桌面分析将使用此功能替换**兼容性风险**。 桌面分析仅在升级前方案部署视图中显示应用程序的评估。 它将基于当前的部署计划中包含的计算机从 Microsoft 获取的见解的应用。

桌面分析使用以下的兼容性评估类别：

- **低**：找到该服务没有信号以 Windows 为此应用程序置于危险升级。 很可能会继续作为目标 OS 上运行的是。  

- **中等**:分析用于指示应用程序可能会有障碍的功能，但是修正是可能的可能。  

- **高**:应用程序是几乎可以肯定期间或之后升级失败。 它可能需要修复。  

- **未知**：不被评估应用程序。 如有任何其他见解*MS 已知问题*或*准备用于 Windows*。  

在部署计划中的应用程序或驱动程序资产的列表中，将看到此值以在每个资产**兼容性风险**列。


## <a name="app-risk-assessment"></a>应用程序的风险评估

有多个桌面分析使用来生成应用程序的评估分级的来源：

- [Microsoft 的已知问题](#microsoft-known-issues)
- [准备好进行 Windows 目录](#ready-for-windows)
- [高级的见解](#advanced-insights)

可以在桌面 Analytics 中查找该应用上的每个源的评估。 在部署计划中的应用程序资产的列表中，选择单个应用以打开其属性的飞出式窗格。 你将看到一个整体的建议和评估级别。 **兼容性风险因素**部分显示了这些评估的详细信息。


## <a name="microsoft-known-issues"></a>Microsoft 的已知问题

桌面分析关注的任何已知问题的 Microsoft 应用程序兼容性数据库了。 它使用此数据库来确定任何现有的兼容性块的公开可用的应用程序从 Microsoft 或其他发布服务器。 此检查仅适用于您选择的部署计划将目标操作系统。

可以看到以下问题上作为应用属性窗格**已知问题的 MS**:

### <a name="application-is-removed-during-upgrade"></a>在升级过程中删除应用程序

Windows 检测到的兼容性问题。 应用程序不会迁移到新的 OS 版本。 为了继续升级，需要执行任何操作不。

### <a name="blocking-upgrade"></a>阻止升级

Windows 检测到阻塞问题，并且无法删除在升级过程中应用程序。 它不可能在新的 OS 版本上运行。 在升级之前，删除应用程序。 重新安装并测试新的操作系统版本上。

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>阻止升级，但可以在升级后重新安装

应用程序与新的 OS 版本兼容，但不会迁移。 删除然后再升级 Windows 应用程序。 新的操作系统版本上重新安装它。

### <a name="blocking-upgrade-update-application-to-newest-version"></a>阻止升级，更新到最新版本的应用程序

现有版本的应用程序与新的 OS 版本不兼容，不会迁移。 可在应用程序的兼容版本。 更新前升级应用程序。

### <a name="disk-encryption-blocking-upgrade"></a>磁盘加密阻止升级

应用程序的加密功能阻止升级。 在升级 Windows 升级后启用之前禁用加密功能。

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>并不适用于新的操作系统，但不会阻止升级

应用程序与新的 OS 版本不兼容，但不会阻止升级。 为了继续升级，需要执行任何操作不。 新的操作系统版本上安装兼容版本的应用程序。

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>并不适用于新的操作系统，且将阻止升级

应用程序与新的 OS 版本不兼容，将阻止升级。 删除然后再升级应用程序。 兼容版本的应用程序可能可用。

### <a name="evaluate-application-on-new-os"></a>评估新 OS 上的应用程序

Windows 将迁移应用程序，但它检测到可能会影响新的操作系统版本上的应用程序的性能问题。 为了继续升级，需要执行任何操作不。 测试新的 OS 版本上的应用程序。

### <a name="may-block-upgrade-test-application"></a>可能会阻止升级、 测试应用程序

Windows 检测到的问题可能会妨碍升级，但需要进一步调查。 在升级过程中测试应用程序的行为。 如果它阻止了升级，则在升级之前删除它。 然后重新安装它，并在新的 OS 版本上进行测试。

### <a name="multiple"></a>多个

多个问题会影响应用程序。 选择**查询**若要查看有关通过 Windows 检测到的问题的详细信息。

### <a name="reinstall-application-after-upgrading"></a>重新安装应用程序升级后

应用程序与新的 OS 版本兼容，但需要重新安装它后升级 Windows。 升级过程中删除应用程序。 为了继续升级，需要执行任何操作不。 新的 OS 版本上重新安装该应用程序。


## <a name="ready-for-windows"></a>准备好进行 Windows

[准备用于 Windows](https://www.readyforwindows.com)应用程序目录将以下数据源相关联：

- 与其他客户报告的相同应用的诊断数据
- 从 Microsoft 的其他检查等设备上的兼容性块

可能的类别包括：

- **高度采用**:至少 10 万商业的 Windows 10 设备已安装此应用。  

- **采用**:至少 10,000 个商用 Windows 10 设备已安装此应用。  

- **数据不足**:太少商业的 Windows 10 设备共享此应用程序，以便 Microsoft 对其采用率进行分类的信息。

- **请联系开发人员**:可能有与此版本的应用程序兼容性问题。 Microsoft 建议联系软件提供商以了解详细信息。 有关详细信息，请参阅[准备用于 Windows](https://www.readyforwindows.com/)。  

- **未知**：没有可用于此版本的此应用程序准备的 Windows 信息。 可用于在应用程序的其他版本可能信息[准备用于 Windows](https://www.readyforwindows.com/)。  

### <a name="support-statement"></a>支持声明

如果软件提供商在 Windows 10 上支持此应用程序的一个或多个版本，您将看到在应用属性窗格上的此语句。 在兼容性风险因素部分，了解**支持语句**。



## <a name="advanced-insights"></a>高级的见解

桌面分析还可以检测的问题，使用以下的其他见解：

### <a name="adopted-version-available"></a>采用的可用版本

还有其他客户高度采用此应用程序的另一个版本。 此信号从准备好的 Windows 中使用的数据。 如果有任何与当前版本的升级阻塞程序，请考虑改为部署的替代版本。

### <a name="driver-dependency"></a>驱动程序依赖关系

该应用是依赖于驱动程序。 桌面的分析建议适用于试验测试的应用。 它应正常的试验，但您会发现任何回归。 如果有任何疑问，请联系发布者请求与 Windows 10 兼容的版本。



## <a name="driver-risk-assessment"></a>驱动程序的风险评估

桌面分析还列出了，并且不会迁移到 OS 版本的任何驱动程序的可用性组。

在桌面 Analytics 中，可以在驱动程序查找评估。 在部署计划中的驱动程序资产的列表中，选择各个驱动程序以打开其属性的飞出式窗格。 你将看到一个整体的建议和评估级别。 **兼容性风险因素**部分显示了这些评估的详细信息。

| 驱动程序可用性 | 所需的操作？ | 这意味着 | 指南 |
|---------------------|------------------|---------------|----------|
| 内置 | 否，仅识别 | 当前安装的应用程序或驱动程序版本不会迁移到新的 OS 版本。 使用新的 OS 版本安装兼容版本。 | 为了继续升级，需要执行任何操作不。 |
| 从 Windows 更新导入 | 是 | 当前安装的驱动程序版本不会迁移到新的 OS 版本。 可从 Windows 更新的兼容版本。 | 如果计算机自动从 Windows Update 接收更新，不不需要任何操作。 否则，从导入新的驱动程序 Windows 更新后升级 Windows。 |
| 随机可用的和从 Windows 更新 | 是 | 当前安装的驱动程序版本不会迁移到新的 OS 版本。 虽然新的驱动程序安装在升级过程中，但较新版本是可从 Windows 更新。 | 如果计算机自动从 Windows Update 接收更新，不不需要任何操作。 否则，从导入新的驱动程序 Windows 更新后升级 Windows。 |
| 请与供应商 | 是 | 该驱动程序不会迁移到新的 OS 版本和桌面分析找不到兼容的版本。 | 对于解决方案，请与独立硬件供应商 (IHV) 人员制造驱动程序或原始设备制造商 (OEM) 提供该设备。 |


## <a name="see-also"></a>另请参阅

FastTrack 中心权益适用于 Windows 10 的连接可以访问**桌面应用程序确保**。 这一优势是设计用于 Windows 10 和 Office 365 专业增强版应用程序兼容性的解决问题的新服务。 有关详细信息，请参阅[桌面应用程序确保](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure)。
