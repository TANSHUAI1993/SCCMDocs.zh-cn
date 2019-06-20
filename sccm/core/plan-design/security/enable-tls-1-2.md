---
title: 如何启用 TLS 1.2
titleSuffix: Configuration Manager
description: 有关如何为 Configuration Manager 启用 TLS 1.2 的信息。
ms.date: 06/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3d97ee2e68f9f4606ad46c8566467fad459ffa9
ms.sourcegitcommit: 725e1bf7d3250c2b7b7be9da01135517428be7a1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822072"
---
# <a name="how-to-enable-tls-12"></a>如何启用 TLS 1.2

适用范围：System Center Configuration Manager (Current Branch)

本文介绍如何为 Configuration Manager 启用 TLS 1.2，包括各个组件。 本文还描述了常用功能的更新要求，以及一些常见问题的故障排除。

Configuration Manager 依赖于许多不同的组件来实现安全通信。 用于给定连接的协议取决于所有必需组件的功能。 如果一个组件过期，则通信可能使用较旧的、安全性较差的协议。

要正确启用 Configuration Manager 来支持 TLS 1.2，首先要为所有必需的组件启用 TLS 1.2。 所需的组件取决于环境和所用的 Configuration Manager 功能。

使用客户端启动此进程（尤其是 Windows 早期版本）。 在 Configuration Manager 服务器上启用 TLS 1.2 前，先确保所有客户端支持 TLS 1.2。 否则，客户端将无法与服务器通信，从而可能会被孤立。


## <a name="tasks-for-features-and-scenarios"></a>功能和方案的任务

若要为 Configuration Manager 赖以进行安全通信的组件启用 TLS 1.2，必须完成下列操作：

- [启用 TLS 1.2 协议作为安全提供程序](#enable-tls-12-protocol-as-a-security-provider)
- [更新 .NET Framework 以支持 TLS 1.2](#update-net-framework-to-support-tls-12)
- [更新 SQL Server 和客户端组件](#update-sql-server-and-client-components)
- [更新 Windows 8.0、Windows Server 2012 R2 及更早版本上的 Windows 和 WinHTTP](#update-windows-and-winhttp)
- [更新 Windows Server Update Services (WSUS)](#update-windows-server-update-services-wsus)

本部分介绍特定 Configuration Manager 功能和场景的依赖项。 请找到适用于你所在环境的项目，以确定后续步骤。

|功能或方案|更新任务|
|--- |--- |
|站点服务器（中央站点服务器、主站点服务器或辅助站点服务器）| - [更新 .NET Framework](#update-net-framework-to-support-tls-12)<br/> - 验证强加密设置|
|站点数据库服务器|[更新 SQL Server 及其客户端组件](#update-sql-server-and-client-components)|
|辅助站点服务器|[更新 SQL Server 及其客户端组件](#update-sql-server-and-client-components) 至 SQL Express 兼容版本|
|站点系统角色| - [更新 .NET Framework](#update-net-framework-to-support-tls-12)，并验证强加密设置 <br/> - 在需要 SQL Server 的角色上[更新 SQL Server 及其客户端组件](#update-sql-server-and-client-components)包括 [SQL Server Native Client](#sql-server-native-client)|
|Reporting Services 点|- 在站点服务器、SQL Reporting Services 服务器及使用此控制台的任意计算机上[更新 .NET Framework](#update-net-framework-to-support-tls-12)<br/> - 根据需要重新启动 SMS_Executive 服务|
|软件更新点|[更新 WSUS](#update-windows-server-update-services-wsus)|
|Configuration Manager 控制台| - [更新 .NET Framework](#update-net-framework-to-support-tls-12)<br/> - 验证强加密设置|
|Configuration Manager 客户端与 HTTPS 站点系统角色|[更新 Windows 以支持通过使用 WinHTTP 进行客户端服务器通信的 TLS 1.2](#update-windows-and-winhttp)|
|软件中心| - [更新 .NET Framework](#update-net-framework-to-support-tls-12)<br/> - 验证强加密设置|
|Windows 7 客户端| 在任何服务器组件上启用 TLS 1.2 前，请先[更新 Windows 以支持通过使用 WinHTTP 进行客户端服务器通信的 TLS 1.2](#update-windows-and-winhttp)。 若先在服务器组件上启用了 TLS 1.2，可能会孤立客户端的早期版本。|


## <a name="enable-tls-12-protocol-as-a-security-provider"></a>启用 TLS 1.2 协议作为安全提供程序

验证 `\SecurityProviders\SCHANNEL\Protocols` 注册表子项设置，如 [.NET Framework 中的传输层安全性 (TLS) 最佳做法](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)所示。

> [!NOTE]
> 默认情况下启用 TLS 1.2。 因此，不需要更改这些项便可以启用它。 在遵循本文指南的其余部分并通过只启用 TLS 1.2 验证了环境的运作情况之后，可以根据协议进行更改来禁用 TLS 1.0 和 TLS 1.1。


## <a name="update-net-framework-to-support-tls-12"></a>更新 .NET Framework 以支持 TLS 1.2

### <a name="determine-net-version"></a>确定 .NET 版本

首先确定 .NET 版本号。 有关详细信息，请参阅[如何确定安装了 Microsoft .NET Framework 的哪些版本以及服务包级别](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso)。

### <a name="install-net-updates"></a>安装 .NET 更新

某些 .NET Framework 版本可能需要更新来启用强加密。 使用以下准则：

- NET Framework 4.6.2 及更高版本支持 TLS 1.1 和 TLS 1.2。 确认注册表设置，但无需额外更改。

- 更新 NET Framework 4.6 和更低版本以支持 TLS 1.1 和 TLS 1.2。 有关详细信息，请参阅 [.NET Framework 版本和依赖关系](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)。

- 如果在 Windows 8.1 或 Windows Server 2012 上使用 .NET Framework 4.5.1 或 4.5.2，也可从[下载中心](https://www.microsoft.com/download/details.aspx?id=42883)获取相关更新和详细信息。

### <a name="configure-for-strong-cryptography"></a>配置强加密

将 .NET Framework 配置为支持强加密。 将 `SchUseStrongCrypto` 注册表设置设置为 `DWORD:00000001`。 此值将禁用 RC4 流密码，并需要重新启动。 若要了解有关此设置的详细信息，请参阅 [Microsoft 安全公告 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358)。

请务必在跨网络与启用了 TLS 1.2 的系统通信的所有计算机上设置以下注册表项。 例如，Configuration Manager 客户端，或站点服务器未安装的任何远程站点系统角色。

对于在 32 位系统上运行的 32 位应用程序或在 64 位系统上运行的 64 位应用程序，请更新以下子项值：

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

对于在 64 位系统上运行的 32 位应用程序，请更新以下子项值：

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> `SchUseStrongCrypto` 设置允许 .NET 使用 TLS 1.1 和 TLS 1.2。 `SystemDefaultTlsVersions` 设置允许 .NET 使用操作系统配置。 有关详细信息，请参阅 [.NET Framework 中的传输层安全性 (TLS) 最佳做法](https://docs.microsoft.com/dotnet/framework/network-programming/tls)。


## <a name="update-sql-server-and-client-components"></a>更新 SQL Server 和客户端组件

Microsoft SQL Server 2016 及更高版本支持 TLS 1.1 和 TLS 1.2。 早期版本和依赖库可能需要更新。 有关详细信息，请参阅 [KB 3135244：支持 Microsoft SQL Server 的 TLS 1.2](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)。

辅助站点服务器需要至少使用包含服务包 2 (13.2.50.26) 的 SQL Server 2016 Express，或更高版本。

### <a name="sql-server-native-client"></a>SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) 还介绍了 SQL Server 客户端组件的要求。

此外，还要务必将 SQL Server Native Client 至少更新到 SQL 2012 SP4 (11.*.7001.0) 版本。 从版本 1810 起，此要求属于[先决条件检查（警告）](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-server-native-client)。

Configuration Manager 对以下站点系统角色使用 SQL Server Native Client：

- 站点数据库服务器
- 站点服务器：管理中心站点、主站点或辅助站点
- 管理点
- 设备管理点
- 状态迁移点
- SMS 提供程序
- 软件更新点
- 启用多播的分发点
- 资产智能更新服务点
- Reporting Services 点
- 应用程序目录 Web 服务
- 注册点
- Endpoint Protection 点
- 服务连接点
- 证书注册点
- 数据仓库服务点


## <a name="update-windows-and-winhttp"></a>更新 Windows 和 WinHTTP

Windows 8.1、Windows Server 2012 R2、Windows 10、Windows Server 2016 及 Windows 更高版本以本机方式支持通过 WinHTTP 进行客户端服务器通信的 TLS 1.2。

Windows 早期版本（如 Windows 7 或 Windows Server 2012）默认情况下不启用通过 HTTPS 进行客户端服务器通信的 TLS 1.1 或 1.2。 对于这些较早版本的 Windows，请安装 [Update 3140245](https://support.microsoft.com/help/3140245)，以便为 Windows 的 WinHTTP 启用 TLS 1.1 和 TLS 1.2 作为默认安全协议。 然后设置以下注册表值：

> [!IMPORTANT]
> 先在所有客户端上启用这些设置，然后再在 Configuration Manager 服务器上启用 TLS 1.2。 否则，可能会在无意中孤立它们。

验证 `DefaultSecureProtocols` 注册表设置的值，例如：

```Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

若更改了此值，请重启计算机。

> [!Note]  
> 上面的示例显示了 WinHTTP `DefaultSecureProtocols` 设置的 `0xAA0` 的值。 [KB 3140245：更新以启用 TLS 1.1 和 TLS 1.2 并将其作为 Windows WinHTTP 的默认安全协议](https://support.microsoft.com/help/3140245)列出了各个协议的十六进制值。 默认情况下，Windows 中的此值是为 WinHTTP 启用 SSL 3.0 和 TLS 1.0 的 `0x0A0`。 上面的示例保留了这些默认值，并且还为 WinHTTP 启用了 TLS 1.1 和 TLS 1.2。 此配置将确保更改不会中断可能仍然依赖 SSL 3.0 或 TLS 1.0 的任何其他应用程序。 可以使用 `0xA00` 的值来仅启用 TLS 1.1 和 TLS 1.2。 Configuration Manager 支持 Windows 与两个设备协商的最安全的协议。
>
> 若要完全禁用 SSL 3.0 和 TLS 1.0，请使用 Windows 中的 SChannel 禁用协议设置。 有关详细信息，请参阅[如何限制 Schannel.dll 中某些加密算法和协议的使用](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc)。


## <a name="update-windows-server-update-services-wsus"></a>更新 Windows Server Update Services (WSUS)

要在 Windows Server 2012 和 Windows Server 2012 R2 上支持客户端服务器在 WSUS 中进行通信的 TLS 1.2，请在 WSUS 服务器上安装以下更新：

- 对于运行 Windows Server 2012 的 WSUS 服务器，安装[更新 4022721](https://support.microsoft.com/help/4022721) 或更高版本的更新。
- 对于运行 Windows Server 2012 R2 的 WSUS 服务器，安装[更新 4022720](https://support.microsoft.com/help/4022720) 或更高版本的更新。


## <a name="known-issues"></a>已知问题

本部分为启用 TLS 1.2 支持时出现的常见问题提供建议。

### <a name="unsupported-platforms"></a>不受支持的平台

以下客户端平台受 Configuration Manager 的支持，但不受 TLS 1.2 环境的支持：

- Windows Server 2008
- Windows CE
- Apple OS X
- 使用本地 MDM 托管的 Windows 10 设备

### <a name="reports-dont-show-in-the-console"></a>控制台未显示报表

若 Configuration Manager 控制台未显示报表，请务必更新运行该控制台的计算机。 需要[更新 .NET Framework](#update-net-framework-to-support-tls-12)，并启用强加密。

### <a name="fips-security-policy-enabled"></a>已启用 FIPS 安全策略

若为客户端或服务器启用了 FIPS 安全策略设置，安全通道 (Schannel) 协商可能会导致它们使用 TLS 1.0。 即使在注册表中禁用此协议，也会发生此行为。

若要进行研究，请启用安全通道事件日志记录，然后在系统日志中检查 Schannel 事件。 有关详细信息，请参阅[如何限制 Schannel.dll 中某些加密算法和协议的使用](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc)。

### <a name="sql-server-communication-failure"></a>SQL Server 通信失败

如果 SQL Server 通信失败并返回 SslSecurityError 错误，请确认以下设置：

- [更新 .NET Framework](#update-net-framework-to-support-tls-12)，并在各个计算机上启用强加密
- 在主机服务器上[更新 SQL Server](#update-sql-server-and-client-components)
- 在与 SQL 通信的所有系统上[更新 SQL 客户端组件](#update-sql-server-and-client-components)。 例如，站点服务器、SMS 提供程序和站点角色服务器。

### <a name="configuration-manager-client-communication-failures"></a>Configuration Manager 客户端通信失败

若 Configuration Manager 客户端无法与站点角色通信，请验证是否已[更新 Windows](#update-windows-and-winhttp) 以支持使用 WinHTTP 进行客户端服务器通信的 TLS 1.2。 常见的站点角色包括分发点、管理点和状态迁移点。

### <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Reporting Services 点失败并返回预期错误

如果 Reporting Services 点没有配置报表，请检查 SRSRP.log 是否存在以下错误条目：

`The underlying connection was closed:`
`An expected error occurred on a receive.`

若要解决此问题，请执行下列步骤：

1. [更新 .NET Framework](#update-net-framework-to-support-tls-12)，并在所有相关计算机上启用强加密。

1. 在安装任意更新后，重新启动 SMS_Executive 服务。

### <a name="application-catalog-doesnt-initialize"></a>应用程序目录未初始化

> [!Important]  
> 应用程序目录已遭弃用。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。

如果应用程序目录未初始化，请检查 ServicePortalWebSite.svclog 文件是否存在以下错误条目：

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

若要解决此问题，请执行下列步骤：

1. [更新 .NET Framework](#update-net-framework-to-support-tls-12)，并在所有相关计算机上启用强加密。

1. 在应用程序目录服务器的 `%WinDir%\System32\InetSrv` 文件夹中，使用以下内容创建 W2SP.exe.config 文件：

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > 如果应用程序是使用 .NET Framework 4.6.3 生成的，则这是要创建的默认文件。

1. 为应用程序目录角色使用 HTTPS 传输安全性。

    > [!Important]
    > 当为应用程序目录角色使用 HTTP 消息安全性时，WCF 将被硬编码为只使用 SSL 3.0 和 TLS 1.0。 这可以防止使用 TLS 1.2。

1. 如果有任何更改，请重新启动计算机。

### <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>软件中心或浏览器不与应用程序目录通信

> [!Important]  
> 应用程序目录已遭弃用。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。

若要让软件中心使用启用了 TLS 1.2 的站点中的用户可用的应用，最好的方法是删除应用程序目录角色。 然后让软件中心直接与管理点通信。 有关详细信息，请参阅[删除应用程序目录](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat)。

如需解决应用程序目录与软件中心之间的通信故障，请验证以下条件：

- [更新 .NET Framework](#update-net-framework-to-support-tls-12)，并在各个计算机上启用强加密。

- 执行更改后，重新启动所有受影响的计算机。

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

### <a name="service-connection-point-upload-failures"></a>服务连接点上传失败

如果服务连接点没有将数据上传到 SCCMConnectedService，请[更新 .NET Framework](#update-net-framework-to-support-tls-12)，并在每台计算机上都启用强加密。 更改完成后，请务必重新启动计算机。

### <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Configuration Manager 控制台显示 Intune 载入对话框

如果控制台尝试连接到 Intune 门户时出现了 Intune 载入对话框，请[更新 .NET Framework](#update-net-framework-to-support-tls-12)，并在每台计算机上启用强加密。 更改完成后，请务必重新启动计算机。

### <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Configuration Manager 控制台显示登录到 Azure 失败

尝试在 Azure Active Directory (Azure AD) 中创建应用程序时，如果在选择“登录”后 Azure Services 载入对话框立即失败，请[更新 .NET Framework](#update-net-framework-to-support-tls-12)，并启用强加密。 更改完成后，请务必重新启动计算机。

### <a name="configuration-manager-cloud-services-and-tls-12"></a>Configuration Manager 云服务和 TLS 1.2

自版本 1802 起，云管理网关和云分发点使用的 Azure 虚拟机支持 TLS 1.2。 版本 1802 或更高版本支持的客户端自动使用 TLS 1.2。

SMSAdminui.log 可能包含如下所示的错误：

```
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

在系统事件日志中，SChannel EventID 36874 可能记录了下面的描述：`An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->


## <a name="see-also"></a>另请参阅

- [.NET Framework 中的传输层安全性 (TLS) 最佳做法](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)

- [KB 3135244：支持 Microsoft SQL Server 的 TLS 1.2](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

- [加密控制技术参考](cryptographic-controls-technical-reference.md)
