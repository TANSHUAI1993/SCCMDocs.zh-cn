---
title: 桌面分析常见问题解答
titleSuffix: Configuration Manager
description: 有关桌面分析的常见问题。
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 884626cd46659917734fa309fa6e84fbdd517ae2
ms.sourcegitcommit: b28a97e22a9a56c5ce3367c750ea2bb4d50449c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70243649"
---
# <a name="desktop-analytics-faq"></a>桌面分析常见问题解答

> [!Note]  
> 此信息与预览版服务相关，该服务可能会在商业发布之前进行大量修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

## <a name="prerequisites"></a>先决条件

### <a name="can-i-use-desktop-analytics-with-intune-managed-devices"></a>能否将桌面分析用于 Intune 托管的设备？ 

大多数可以从桌面分析工作流获益的客户使用 Configuration Manager 来部署 Windows。 我们知道，Intune 客户喜欢分析数据的其他见解，并且我们正在努力与他们分享见解。

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>它已超过72小时，门户仍在处理数据，接下来要做什么？ 

首次设置桌面分析时，Configuration Manager 和 Desktop Analytics 门户中的报表可能不会立即显示完整的数据。 服务处理数据可能需要2-3 天。 如果已超过72小时，并且门户仍在处理数据，请执行以下步骤：

- 若要确认已正确配置活动设备，请使用 "[连接运行状况" 仪表板](/sccm/desktop-analytics/monitor-connection-health)。 此仪表板不会实时更新。
- 确保设备将诊断数据发送到桌面分析服务。 有关详细信息，请参阅[启用数据共享](/sccm/desktop-analytics/enable-data-sharing)。
- 预配 Azure AD 上的[Azure AD 应用程序](/sccm/desktop-analytics/troubleshooting#bkmk_AzureADApps)。
- 在过去7天内检查与组织关联的设备。 在[桌面分析门户](https://aka.ms/desktopanalytics)中，请参阅 "**连接服务**" 窗格。 选择 "**注册设备**" 并**查看最近的数据**

如果设备配置正确，并且仍未看到工作区中的数据，请[联系 Microsoft 支持](https://support.microsoft.com/hub/4343728/support-for-business)部门。

## <a name="windows-upgrade"></a>Windows 升级

### <a name="can-i-upgrade-windows-and-change-architecture"></a>能否升级 Windows 和更改体系结构？

桌面分析旨在最大程度地支持就地升级。 就地升级不支持从32位到64位体系结构的迁移。 如果需要在此方案中迁移计算机，请使用刷新方案。 在这种情况下，桌面分析见解仍有价值，但你可以忽略特定于升级的指南。

有关详细信息，请参阅[使用新版本的 Windows 刷新现有的计算机](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)。

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>升级 Windows 时，是否可以从 BIOS 更改为 UEFI？

是。 有关详细信息，请参阅[在就地升级过程中从 BIOS 转换为 UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)。

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>能否将桌面分析用于 Windows 10 LTSC？

尽管可以使用桌面分析来帮助将设备从 Windows 10 长期服务通道（LTSC）更新到 Windows 10 半年频道，但桌面分析不支持 Windows 10 LTSC 更新。 此 Windows 10 通道并非适用于广泛使用，并且不会收到功能更新，因此不是桌面分析支持的目标。 有关详细信息，请参阅[Windows 即服务概述](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)。

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>是否可以减少在桌面分析门户中刷新数据所需的时间？

桌面分析门户中有两种类型的数据：管理员数据和诊断数据。 若要按需刷新管理员数据，请打开 "数据货币" 弹出窗口，并选择 "**应用更改**"。 此操作会立即触发工作区中任何挂起的管理员更改的一次性刷新。 更改将在15-60 分钟内传播并公开发布。 计时取决于工作区的大小和挂起的更改的范围。 可在24小时内请求最多六次的按需数据刷新。

所有数据会每天自动更新一次，即使你未请求按需数据刷新也是如此。 无法触发诊断数据的按需刷新。 有关桌面分析中不同类型的数据的详细信息，请参阅[数据延迟](/sccm/desktop-analytics/troubleshooting#data-latency)。

## <a name="privacy"></a>隐私

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>能否在没有直接客户端与 Microsoft 数据管理服务的连接的情况下使用桌面分析？

不可以，整个服务由 Windows 诊断数据提供支持，这要求设备具有这种直接连接性。

### <a name="can-i-choose-the-data-center-location"></a>能否选择数据中心位置？

对于 Azure Log Analytics：是，当设置桌面分析并创建 Log Analytics 工作区时。

对于 Microsoft 数据管理服务和分析 Azure 存储：不是，这两个服务托管在美国中。

### <a name="where-is-my-organizations-data-stored"></a>我的组织的数据存储在何处？

来自您的计算机的 Windows 诊断数据被加密、发送到，并在位于美国的 Microsoft 托管的安全数据中心进行处理。 接下来，我们将通过 Azure 门户中的桌面分析解决方案为你提供与桌面分析相关的数据的分析。 所有 Azure 区域都支持桌面分析。 选择国际 Azure 区域不会阻止在美国的 Microsoft 安全数据中心发送和处理诊断数据。

## <a name="existing-windows-analytics-customers"></a>现有 Windows Analytics 客户

### <a name="can-i-migrate-inputs-from-windows-analytics"></a>能否从 Windows Analytics 迁移输入？

是，当你在[初始载入](/sccm/desktop-analytics/set-up#initial-onboarding)期间将现有 Windows Analytics 工作区作为桌面分析工作区进行设置时。 如果创建一个新的工作区，或选择一个不是 Windows Analytics 工作区的工作区，则桌面分析不会迁移你的输入。

#### <a name="migration-scope"></a>迁移范围

| 输入类型 | 将迁移？ |
|------------|---------------|
| 重要性 | 是 |
| 应用所有者 | 是 |
| 升级决策 | 否 |
| 测试计划 | 否 |
| 测试结果 | 否 |

#### <a name="importance-mapping"></a>重要性映射

| Windows Analytics | 桌面分析 |
|-------------------| ------------------|
| 低安装计数 | （不适用） <br> 注意:桌面分析运行其自己的试探法来确定低安装计数 |
| 未查看 | 未查看 |
| 查看正在进行 | 未查看 |
| 关键任务 | 关键 |
| 业务关键 | 关键 |
| 重要提示 | 重要提示 |
| 最大努力 | 重要提示 |
| 忽略 | 不重要 |

### <a name="can-i-migrate-from-multiple-windows-analytics-workspaces"></a>能否从多个 Windows Analytics 工作区迁移？

不可以，只能选择一个要从中迁移输入的 Windows Analytics 工作区。 如果你拥有多个 Windows Analytics 工作区，请选择最适合你的组织的工作区。

### <a name="ive-chosen-to-migrate-where-can-i-find-the-inputs-on-desktop-analytics"></a>我选择了迁移，在哪里可以找到桌面分析上的输入？

注册设备后，若要在桌面 Analytics 门户中查看已迁移的输入，请参阅**管理 > 资产 > 应用**。

### <a name="when-can-i-see-my-migrated-inputs"></a>何时可以看到已迁移的输入？

迁移过程是事务性的。 你将看到所有已迁移的输入没有损坏，或者根本没有迁移的输入。 如果在24小时内未看到迁移的输入，请联系 Microsoft 支持部门。 查看已迁移的输入时开始标记应用。 如果已标记一些应用，桌面分析会保留这些输入，以防与 Windows Analytics 中的输入发生冲突。

### <a name="im-not-ready-yet-can-i-migrate-after-the-initial-onboarding"></a>我还没有准备好，我是否可以在初次加入后迁移？

不需要，此时需要决定在[初始载入](/sccm/desktop-analytics/set-up#initial-onboarding)期间进行迁移。

## <a name="other"></a>其他

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a>我能否将桌面分析用于我的 Office 365 ProPlus 升级？

不能，桌面分析侧重于 Windows。 Microsoft 开发的桌面分析与许多客户紧密协作。 通过预览计划，客户的反馈涉及到桌面分析如何提高其自信地管理 Windows 部署的能力。 他们还告诉我们，他们希望[office 365 ProPlus 的准备工作](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness)与 Configuration Manager 和 Intune 中的 office 管理工具更紧密地集成。 Microsoft 将继续在这些领域进行投资，同时重点介绍桌面分析中的 Windows 方案。

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>如何提供有关桌面分析的反馈？

若要共享有关桌面分析的反馈，请选择门户顶部的 "**发送笑脸**" 图标。 在提交时包含屏幕截图，帮助 Microsoft 更好地了解你的反馈。 你还可以提交产品建议并在[UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805)上投票赞成其他观点。

> [!Note]
> 永远不要通过发送笑脸或 UserVoice 来共享隐私信息。 此类私人信息包括你的租户 Id 或商业 Id。Microsoft 不通过 "发送笑脸" 或 "UserVoice" 通道提供支持。 若要获取桌面分析工作区帮助，请在导航菜单中选择 "**帮助和支持**" 链接以打开支持票证。
