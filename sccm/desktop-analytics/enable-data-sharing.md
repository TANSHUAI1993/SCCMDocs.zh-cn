---
title: 启用数据共享
titleSuffix: Configuration Manager
description: 用于共享桌面分析诊断数据的参考指南。
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5ba70b39330fd21077f5b7997e8aa92a1c57f42
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561999"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>共享桌面分析数据

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

若要注册到 Desktop 分析的设备，他们需要向 Microsoft 发送诊断数据。 如果您的环境使用代理服务器，使用此信息来帮助配置代理。


## <a name="diagnostic-data-levels"></a>诊断数据级别

![桌面 Analytics 的诊断数据级别的关系图](media/diagnostic-data-levels.png)

当 Configuration Manager 将使用 Desktop 分析时，你还使用它来管理设备上的诊断数据级别。 为获得最佳体验，使用配置管理器。

在 Desktop 分析的基本功能工作**基本**诊断数据级别。 不会为更新的设备获取使用情况或运行状况数据，而不启用**增强 （受限）** 级别。 Microsoft 建议您启用**增强 （受限）** 诊断数据级别。 有关详细信息，请参阅[Windows 10 增强的诊断数据的事件和使用的 Windows Analytics 字段](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields))。

> [!Important]   
> Microsoft 已为您提供工具和资源，让你控制您的隐私的有力承诺。 因此，Microsoft 不会从位于欧洲国家/地区 （EEA 和瑞士） 设备收集以下数据：
>
> - 从 Windows 8.1 设备的 Windows 诊断数据
> - 适用于 Windows 7 的应用使用情况数据

有关详细信息，请参阅[Desktop 分析隐私](/sccm/desktop-analytics/privacy)。

以下文章也是有用的资源，对更好地了解 Windows 诊断数据级别：

- [Windows 10 和 IT 决策制定者 GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [在你的组织中配置 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> 在增强 （受限） 级别中，当每个客户端执行初始的完全扫描，它将发送大约 2 MB 的数据到 Microsoft 云。 每日增量各不相同，每日 250 400 KB 之间。
>
> 每日增量扫描发生在 3:00 AM （设备本地时间）。 某些事件会在一天中的第一个可用时间。 这些时间不是可配置的。
>
> 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://aka.ms/enterprisetelemetry)。  



## <a name="endpoints"></a>终结点

若要启用的数据共享，请配置代理服务器以允许以下终结点：

> [!Important]  
> 有关隐私和数据完整性，Windows 将检查 Microsoft SSL 证书与诊断数据终结点进行通信时。 SSL 截获和检查不可能实现。 若要使用 Desktop 分析，请从 SSL 检查中排除这些终结点。<!-- BUG 4647542 -->

| 终结点  | 函数  |
|-----------|-----------|
| `https://aka.ms` | 用于定位服务 |
| `https://v10c.events.data.microsoft.com` | 连接的用户体验和诊断组件终结点。 使用运行 Windows 10 的设备，版本 1703年或更高版本，与 2018年-09 累积更新或更高版本安装。 |
| `https://v10.events.data.microsoft.com` | 连接的用户体验和诊断组件终结点。 设备运行 Windows 10，版本 1803 版，或更高版本，使用_而无需_2018年 09 累积更新的安装。 |
| `https://v10.vortex-win.data.microsoft.com` | 连接的用户体验和诊断组件终结点。 由运行 Windows 10 版本 1709年或更早版本的设备。 |
| `https://vortex-win.data.microsoft.com` | 连接的用户体验和诊断组件终结点。 由运行 Windows 7 和 Windows 8.1 的设备 |
| `https://settings-win.data.microsoft.com` | 启用兼容性更新，以将数据发送给 Microsoft。 |
| `http://adl.windows.com` | 允许在兼容性更新，以接收来自 Microsoft 的最新的兼容性数据。 |
| `https://watson.telemetry.microsoft.com` | Windows 错误报告 (WER)。 需要用来监视部署于 Windows 10，版本 1803年或更早版本的运行状况。 |
| `https://umwatsonc.events.data.microsoft.com` | Windows 错误报告 (WER)。 所需的 Windows 10，1809年或更高版本中的设备运行状况报告。 |
| `https://ceuswatcab01.blob.core.windows.net`<br> `https://ceuswatcab02.blob.core.windows.net`<br> `https://eaus2watcab01.blob.core.windows.net`<br> `https://eaus2watcab02.blob.core.windows.net`<br> `https://weus2watcab01.blob.core.windows.net`<br> `https://weus2watcab02.blob.core.windows.net` | Windows 错误报告 (WER)。 需要用来监视部署在 Windows 10 中，1809年或更高版本的运行状况。 |
| `https://kmwatsonc.events.data.microsoft.com` | 在线崩溃分析。 所需的 Windows 10，1809年或更高版本中的设备运行状况报告。 |
| `https://oca.telemetry.microsoft.com`  | 在线崩溃分析 (OCA)。 需要用来监视部署于 Windows 10，版本 1803年或更早版本的运行状况。 |
| `https://login.live.com` | 所需的桌面 Analytics 提供更可靠的设备标识。 <br> <br>若要禁用最终用户的 Microsoft 帐户访问，而不是阻塞此终结点使用策略设置。 有关详细信息，请参阅[企业中的 Microsoft 帐户](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)。 |
| `https://graph.windows.net` | 用于自动检索设置，例如 CommercialId 附加到 Desktop 分析 （在 Configuration Manager 服务器角色） 的层次结构时。 |
| `https://fef.msua06.manage.microsoft.com` | 用于同步设备集合成员身份、 部署计划和使用 Desktop 分析 （在 Configuration Manager 服务器角色） 的设备就绪状态。 |


## <a name="proxy-server-authentication"></a>代理服务器身份验证

请确保代理不会由于身份验证而阻止的诊断数据。 如果你的组织使用代理服务器身份验证的出站流量，使用一个或多个以下方法：

- **绕过**（推荐）：配置代理服务器，以不要求与诊断数据的终结点的流量进行代理身份验证。 此选项是最全面的解决方案。 它适用于所有版本的 Windows 10。  

- **用户代理身份验证**:设备配置为使用代理身份验证登录的用户上下文。 此方法要求运行 Windows 10 版本 1703年或更高版本的设备。 请确保用户具有访问诊断数据终结点的代理权限。 此选项要求的设备具有控制台具有代理权限的用户，因此不能与无外设设备使用此方法。  

- **设备代理身份验证**:

    - 在设备上配置系统级代理服务器。  
    - 这些设备配置为使用基于设备的出站代理身份验证。  
    - 配置代理服务器，以允许访问诊断数据终结点的计算机帐户。  
