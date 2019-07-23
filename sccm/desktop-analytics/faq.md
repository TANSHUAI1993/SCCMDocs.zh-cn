---
title: 桌面分析常见问题解答
titleSuffix: Configuration Manager
description: 有关桌面分析的常见问题。
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 58230d373d7269c95937a108c021e7c73cdbf07a
ms.sourcegitcommit: 315fbb9c44773b3b1796ae398568cb61bd07092e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2019
ms.locfileid: "68374444"
---
# <a name="desktop-analytics-faq"></a>桌面分析常见问题解答

> [!Note]  
> 此信息与预览版服务相关, 该服务可能会在商业发布之前进行大量修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

## <a name="prerequisites"></a>先决条件 

### <a name="can-i-use-desktop-analytics-with-intune-managed-devices"></a>能否将桌面分析用于 Intune 托管的设备？ 

大多数可以从桌面分析工作流获益的客户使用 Configuration Manager 来部署 Windows。 我们知道, Intune 客户喜欢分析数据的其他见解, 并且我们正在努力与他们分享见解。

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>它已超过72小时, 门户仍在处理数据, 接下来要做什么？ 

首次设置桌面分析时, Configuration Manager 和 Desktop Analytics 门户中的报表可能不会立即显示完整的数据。 服务处理数据可能需要2-3 天。 如果已超过72小时, 并且门户仍在处理数据, 请执行以下步骤:

- 若要确认已正确配置活动设备, 请使用 "[连接运行状况" 仪表板](/sccm/desktop-analytics/monitor-connection-health)。 此仪表板不会实时更新。
- 确保设备将诊断数据发送到桌面分析服务。 有关详细信息, 请参阅[启用数据共享](/sccm/desktop-analytics/enable-data-sharing)。
- 预配 Azure AD 上的[Azure AD 应用程序](/sccm/desktop-analytics/troubleshooting#bkmk_AzureADApps)。
- 在过去7天内检查与组织关联的设备。 在[桌面分析门户](https://aka.ms/desktopanalytics)中, 请参阅 "**连接服务**" 窗格。 选择 "**注册设备**" 并**查看最近的数据**

如果设备配置正确, 并且仍未看到工作区中的数据, 请[联系 Microsoft 支持](https://support.microsoft.com/hub/4343728/support-for-business)部门。


## <a name="windows-upgrade"></a>Windows 升级

### <a name="can-i-upgrade-windows-and-change-architecture"></a>能否升级 Windows 和更改体系结构？

桌面分析旨在最大程度地支持就地升级。 就地升级不支持从32位到64位体系结构的迁移。 如果需要在此方案中迁移计算机, 请使用刷新方案。 在这种情况下, 桌面分析见解仍有价值, 但你可以忽略特定于升级的指南。

有关详细信息，请参阅[使用新版本的 Windows 刷新现有的计算机](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)。

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>升级 Windows 时, 是否可以从 BIOS 更改为 UEFI？

是。 有关详细信息, 请参阅[在就地升级过程中从 BIOS 转换为 UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)。

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>能否将桌面分析用于 Windows 10 LTSC？

尽管可以使用桌面分析来帮助将设备从 Windows 10 长期服务通道 (LTSC) 更新到 Windows 10 半年频道, 但桌面分析不支持 Windows 10 LTSC 更新。 此 Windows 10 通道并非适用于广泛使用, 并且不会收到功能更新, 因此不是桌面分析支持的目标。 有关详细信息, 请参阅[Windows 即服务概述](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)。

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>是否可以减少在桌面分析门户中刷新数据所需的时间？

桌面分析门户中有两种类型的数据:管理员数据和诊断数据。 若要按需刷新管理员数据, 请打开 "数据货币" 弹出窗口, 并选择 "**应用更改**"。 此操作会立即触发工作区中任何挂起的管理员更改的一次性刷新。 更改将在15-60 分钟内传播并公开发布。 计时取决于工作区的大小和挂起的更改的范围。 可在24小时内请求最多六次的按需数据刷新。 

所有数据会每天自动更新一次, 即使你未请求按需数据刷新也是如此。 无法触发诊断数据的按需刷新。 有关桌面分析中不同类型的数据的详细信息, 请参阅[数据延迟](/sccm/desktop-analytics/troubleshooting#data-latency)。

## <a name="privacy"></a>隐私

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>能否在没有直接客户端与 Microsoft 数据管理服务的连接的情况下使用桌面分析？

不可以, 整个服务由 Windows 诊断数据提供支持, 这要求设备具有这种直接连接性。

### <a name="can-i-choose-the-data-center-location"></a>能否选择数据中心位置？

对于 Azure Log Analytics:是, 当设置桌面分析并创建 Log Analytics 工作区时。

对于 Microsoft 数据管理服务和分析 Azure 存储:不是, 这两个服务托管在美国中。

### <a name="where-is-my-organizations-data-stored"></a>我的组织的数据存储在何处？

来自您的计算机的 Windows 诊断数据被加密、发送到, 并在位于美国的 Microsoft 托管的安全数据中心进行处理。 接下来, 我们将通过 Azure 门户中的桌面分析解决方案为你提供与桌面分析相关的数据的分析。 所有 Azure 区域都支持桌面分析。 选择国际 Azure 区域不会阻止在美国的 Microsoft 安全数据中心发送和处理诊断数据。

## <a name="other"></a>其他

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a>我能否将桌面分析用于我的 Office 365 ProPlus 升级？

不能, 桌面分析侧重于 Windows。 Microsoft 开发了与众多客户紧密协作的桌面分析。 通过预览计划, 客户的反馈涉及到桌面分析如何提高其自信地管理 Windows 部署的能力。 他们还告诉我们, 他们希望[office 365 ProPlus 的准备工作](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness)与 Configuration Manager 和 Intune 中的 office 管理工具更紧密地集成。 Microsoft 将继续在这些领域进行投资, 同时重点介绍桌面分析中的 Windows 方案。
