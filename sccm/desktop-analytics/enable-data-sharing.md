---
title: 启用数据共享
titleSuffix: Configuration Manager
description: 使用桌面分析来共享诊断数据的参考指南。
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91be1fbb03c49b28d689aff974a43ba8434fc194
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72385686"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>启用桌面分析的数据共享

若要将设备注册到桌面分析，需要将诊断数据发送给 Microsoft。 如果你的环境使用代理服务器，请使用此信息来帮助配置代理。


## <a name="diagnostic-data-levels"></a>诊断数据级别

![桌面分析的诊断数据级别示意图](media/diagnostic-data-levels.png)

将 Configuration Manager 与桌面分析集成时，还可以使用它来管理设备上的诊断数据级别。 为获得最佳体验，请使用 Configuration Manager。

桌面分析的基本功能适用于**基本**诊断数据级别。 不启用已更新的设备的使用情况或运行状况数据，无需启用 "**增强（受限）** " 级别。 Microsoft 建议您启用 "**增强（受限）** " 诊断数据级别。 有关详细信息，请参阅 windows [10 增强的诊断数据事件和 Windows Analytics 使用的字段](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)。

> [!Important]   
> Microsoft 对提供用于控制隐私的工具和资源提供了强大的承诺。 因此，Microsoft 不会从位于欧洲国家/地区（EEA 和瑞士）的设备中收集以下数据：
>
> - 来自 Windows 8.1 设备的 Windows 诊断数据
> - 适用于 Windows 7 的应用使用情况数据

有关详细信息，请参阅[桌面分析隐私](/sccm/desktop-analytics/privacy)。

下面的文章也是用于更好地了解 Windows 诊断数据级别的有用资源：

- [Windows 10 和 IT 决策者的 GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [在组织中配置 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> 在 "增强（受限）" 级别，当每个客户端执行初始完全扫描时，它会向 Microsoft 云发送大约 2 MB 的数据。 每日增量不同于 250-400 KB。
>
> 每日增量扫描发生在上午3:00 （设备本地时间）。 有些事件会在一天中的第一天可用时发送。 这些时间不可配置。
>
> 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://aka.ms/enterprisetelemetry)。  



## <a name="endpoints"></a>终结点

若要启用数据共享，请将代理服务器配置为允许以下终结点：

> [!Important]  
> 对于隐私和数据完整性，Windows 会在与诊断数据终结点通信时检查 Microsoft SSL 证书。 无法进行 SSL 拦截和检查。 若要使用桌面分析，请从 SSL 检查中排除这些终结点。<!-- BUG 4647542 -->

| 终结点  | 函数  |
|-----------|-----------|
| `https://aka.ms` | 用于查找服务 |
| `https://v10c.events.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行 Windows 10 版本1703或更高版本的设备使用，其中安装了2018-09 累积更新或更高版本。 |
| `https://v10.events.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行 Windows 10 版本1803或更高版本的设备使用，_无需_安装2018-09 累积更新。 |
| `https://v10.vortex-win.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行 Windows 10 版本1709或更早版本的设备使用。 |
| `https://vortex-win.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行 Windows 7 和 Windows 8.1 的设备使用 |
| `https://settings-win.data.microsoft.com` | 启用兼容性更新，将数据发送到 Microsoft。 |
| `http://adl.windows.com` | 允许兼容性更新从 Microsoft 接收最新的兼容性数据。 |
| `https://watson.telemetry.microsoft.com` | Windows 错误报告（WER）。 需要在 Windows 10 版本1803或更早版本中监视部署运行状况。 |
| `https://umwatsonc.events.data.microsoft.com` | Windows 错误报告（WER）。 Windows 10 版本1809或更高版本中的设备运行状况报告所需的。 |
| `https://ceuswatcab01.blob.core.windows.net`<br> `https://ceuswatcab02.blob.core.windows.net`<br> `https://eaus2watcab01.blob.core.windows.net`<br> `https://eaus2watcab02.blob.core.windows.net`<br> `https://weus2watcab01.blob.core.windows.net`<br> `https://weus2watcab02.blob.core.windows.net` | Windows 错误报告（WER）。 需要在 Windows 10 版本1809或更高版本中监视部署运行状况。 |
| `https://kmwatsonc.events.data.microsoft.com` | 联机崩溃分析。 Windows 10 版本1809或更高版本中的设备运行状况报告所需的。 |
| `https://oca.telemetry.microsoft.com`  | 联机崩溃分析（OCA）。 需要在 Windows 10 版本1803或更早版本中监视部署运行状况。 |
| `https://login.live.com` | 需要为桌面分析提供更可靠的设备标识。 <br> <br>若要禁用最终用户 Microsoft 帐户访问权限，请使用策略设置，而不是阻止此终结点。 有关详细信息，请参阅[企业中的 Microsoft 帐户](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)。 |
| `https://graph.windows.net` | 用于在将层次结构附加到桌面分析（Configuration Manager Server 角色上）时自动检索设置，如 CommercialId。 有关详细信息，请参阅 [为站点系统服务器配置代理
] （/sccm/core/plan-design/network/proxy-server-support # 配置--代理-站点系统服务器）。 |
| `https://*.manage.microsoft.com` | 用于使用桌面分析同步设备集合成员身份、部署计划和设备就绪状态（仅限 Configuration Manager Server 角色上）。 有关详细信息，请参阅 [为站点系统服务器配置代理
] （/sccm/core/plan-design/network/proxy-server-support # 配置--代理-站点系统服务器）。 |


## <a name="proxy-server-authentication"></a>代理服务器身份验证

由于身份验证，请确保代理不会阻止诊断数据。 如果你的组织对出站流量使用代理服务器身份验证，请使用以下一种或多种方法：

- **绕过**（推荐）：将代理服务器配置为不要求对诊断数据终结点的流量进行代理身份验证。 此选项是最全面的解决方案。 它适用于所有版本的 Windows 10。  

- **用户代理身份验证**：将设备配置为使用登录用户的上下文进行代理身份验证。 此方法要求设备运行 Windows 10 1703 版或更高版本。 请确保用户具有访问诊断数据终结点的代理权限。 此选项要求设备具有具有代理权限的控制台用户，因此无法将此方法用于无外设设备。  

- **设备代理身份验证**：

    - 在设备上配置系统级代理服务器。  
    - 将这些设备配置为使用基于设备的出站代理身份验证。  
    - 配置代理服务器以允许计算机帐户访问诊断数据终结点。  
