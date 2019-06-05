---
title: 如何启用 TLS 1.2
titleSuffix: Configuration Manager
description: 有关如何为 Microsoft Configuration Manager 启用 TLS 1.2 的信息。
ms.date: 05/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3641c3a9adce23f24a80135d996da03e12e78907
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355604"
---
# <a name="how-to-enable-tls-12-for-configuration-manager"></a>如何为 Configuration Manager 启用 TLS 1.2

适用范围：  System Center Configuration Manager (Current Branch)

本文介绍如何为 Configuration Manager 启用 TLS 1.2，包括各个组件。 本文还描述了常用功能的更新要求，以及一些常见问题的故障排除。

Configuration Manager 依赖于许多不同的组件来实现安全通信。 用于给定连接的协议取决于所有必需组件的功能。 如果一个组件过期，则通信可能使用较旧的、安全性较差的协议。

要正确启用 Configuration Manager 来支持 TLS 1.2，必须为所有必需的组件启用 TLS 1.2。 所需的组件取决于你所使用的环境和 Configuration Manager 功能。


## <a name="to-enable-tls-12"></a>启用 TLS 1.2

要启用 TLS 1.2，必须首先启用 TLS 1.2 作为运行 Configuration Manager 或与之交互的每台计算机的安全提供程序。 然后，为 Configuration Manager 赖以进行安全通信的组件启用 TLS 1.2。

### <a name="enable-the-tls-12-protocol-as-a-security-provider"></a>启用 TLS 1.2 协议作为安全提供程序

验证“\SecurityProviders\SCHANNEL\Protocols”注册表子项设置，如 [.NET Framework 中的传输层安全性 (TLS) 最佳做法](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry?)所示。

> [!NOTE]
> 默认情况下启用 TLS 1.2。 因此，不需要更改这些项便可以启用它。 在遵循本文指南的其余部分并通过只启用 TLS 1.2 验证了环境的运作情况之后，可以根据协议进行更改来禁用 TLS 1.0 和 TLS 1.1。

### <a name="enable-tls-12-for-dependent-components"></a>为从属组件启用 TLS 1.2
若要为 Configuration Manager 赖以进行安全通信的从属组件启用 TLS 1.2，必须：

- [更新 .NET Framework 以支持 TLS 1.2](#update-net-framework-to-support-tls-12)
- [更新 SQL Server 和客户端组件](#update-sql-server-and-client-components)
- [更新 Windows 8.0、Windows Server 2012 R2 及更早版本上的 Windows 和 WinHTTP](#update-windows-and-winhttp)
- [更新 Windows Server Update Services (WSUS)](#update-windows-server-update-services)

#### <a name="update-net-framework-to-support-tls-12"></a>更新 .NET Framework 以支持 TLS 1.2
若要更新 .NET Framework 以支持 TLS 1.2，请首先确定你的 .NET 版本号。 有关帮助，请参阅[如何确定安装了 Microsoft .NET Framework 的哪些版本以及服务包级别](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso)。

.NET Framework 的早期版本可能需要更新或更改注册表来启用强加密。 使用以下准则：

- NET Framework 4.6.2 支持 TLS 1.1 和 TLS 1.2。  不需要进行其他更改。
- [必须更新](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies) NET Framework 4.6 和更低版本以支持 TLS 1.1 和 TLS 1.2。

如果在 Windows 8.1、Windows RT 8.1 或 Windows Server 2012 上使用 .NET Framework 4.5.1 或 4.5.2，也可从[下载中心](https://www.microsoft.com/download/details.aspx?id=42883)获取相关更新和详细信息。
-  .NET Framework 必须配置为支持强加密。 将 `SchUseStrongCrypto` 注册表设置设置为 `DWORD:00000001`。 这将禁用 RC4 流密码，并需要重新启动。 若要了解有关此设置的详细信息，请参阅 [Microsoft 安全公告 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358)。

对于在 32 位系统上运行的 32 位应用程序或在 64 位系统上运行的 64 位应用程序，请更新以下子项值：

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
对于在 64 位系统上运行的 32 位应用程序，请更新以下子项值：

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\.NETFramework\\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
#### <a name="update-sql-server-and-client-components"></a>更新 SQL Server 和客户端组件

Microsoft SQL Server 2016 支持 TLS 1.1 和 TLS 1.2。
早期版本和依赖库可能需要更新。 有关详细信息，请参阅 [KB 3135244：支持 Microsoft SQL Server 的 TLS 1.2](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)。

> [!NOTE]
> KB 3135244 还介绍了 SQL Server 客户端组件的要求。 更新在环境中使用的每个组件。

#### <a name="update-windows-and-winhttp"></a>更新 Windows 和 WinHTTP

Windows 10、Windows 8.1、Windows Server 2016 和 Windows Server 2012 R2 支持通过现成的 WinHTTP 进行客户端服务器通信的 TLS 1.2。

Windows 8.0、Windows Server 2012 和更早版本的 Windows 默认情况下不启用通过 HTTPS 进行客户端服务器通信的 TLS 1.1 或 1.2。 对于这些较早版本的 Windows，应安装 [Update 3140245](https://support.microsoft.com/help/3140245)，以便在 Windows 的 WinHTTP 中启用 TLS 1.1 和 TLS 1.2 作为默认安全协议，并设置以下注册表值。

> [!IMPORTANT]
> 在启用 TLS 1.2 之前  ，必须先在所有下层客户端上运行此操作，否则可能会无意中孤立它们。

验证 `DefaultSecureProtocols` 注册表设置为 `0xAA0`，如下所示：

```
HKEY_LOCAL_MACHINE\SOFTWARE\
   \Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```
> [!NOTE]
> 此更改需要重新启动。

#### <a name="update-windows-server-update-services"></a>更新 Windows Server Update Services

要在 Windows Server 2012 和 Windows Server 2012 R2 上支持客户端服务器在 WSUS 中进行通信的 TLS 1.2，必须在 WSUS 服务器上应用以下更新：
- 对于运行 Windows Server 2012 的 WSUS 服务器，应用 [update 4022721](https://support.microsoft.com/help/4022721) 或更高版本的更新。
- 对于运行 Windows Server 2012 R2 的 WSUS 服务器，应用 [update 4022720](https://support.microsoft.com/help/4022720) 或更高版本的更新。

## <a name="tasks-required-for-configuration-manager-features-and-scenarios"></a>Configuration Manager 功能和场景所需的任务
本部分介绍特定 Configuration Manager 功能和场景的依赖项。 要确定后续步骤，请找到适用于你的环境的项，然后使用前面在[为从属组件启用 TLS 1.2](#enable-tls-12-for-dependent-components) 中提供的步骤验证依赖项。

|功能或方案|更新任务|
|--- |--- |
|站点服务器（中央站点服务器、主站点服务器或辅助站点服务器）|[更新 .NET Framework](#update-net-framework-to-support-tls-12)，并验证强加密设置。|
|SMS 提供程序|根据每个 SMS 提供程序的需要[更新 SQL Server 及其客户端组件](#update-sql-server-and-client-components)。|
|站点系统角色|[更新 .NET Framework](#update-net-framework-to-support-tls-12)，并验证强加密设置。 [更新 SQL Server 及其客户端组件](#update-sql-server-and-client-components)。|
|服务连接点应用程序目录|[更新 .NET Framework](#update-net-framework-to-support-tls-12)，并验证强加密设置。|
|SRS 报表点|在站点服务器和 SRS 服务器上[更新 .NET Framework](#update-net-framework-to-support-tls-12)。 根据需要重新启动 SMS_Executive 服务。|
|Configuration Manager 控制台|[更新 .NET Framework](#update-net-framework-to-support-tls-12)，并验证强加密设置。|
|SCCM 客户端与 HTTPS 站点系统角色|[更新 Windows 以支持通过使用 WinHTTP 进行客户端服务器通信的 TLS 1.2](#update-windows-and-winhttp)。|
|软件中心|[更新 .NET Framework](#update-net-framework-to-support-tls-12)，并验证强加密设置。|
|软件更新点|[更新 WSUS](#update-windows-server-update-services)。|
|管理点|更新到最新的 SQL Server 本机客户端，使 Configuration Manager 能够与启用了 TLS 1.2 的最新 SQL Server 组件进行通信。 请参阅[支持 Microsoft SQL Server 的 TLS 1.2](https://support.microsoft.com/help/3135244) 中的“客户端组件下载”表。|

## <a name="known-issues"></a>已知问题

本部分为启用 TLS 1.2 支持时出现的常见问题提供建议。

### <a name="fips-security-policy-enabled"></a>已启用 FIPS 安全策略

如果为客户端或服务器启用了 FIPS 安全策略设置，即使使用注册表禁用了协议，安全通道 (Schannel) 协商也会导致使用 TLS 1.0。

若要进行研究，请启用安全通道事件日志记录，然后在系统日志中检查 Schannel 事件。 有关相关信息，请参阅[如何限制 Schannel.dll 中某些加密算法和协议的使用](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc)。

### <a name="sql-server-communication-failure"></a>SQL Server 通信失败

如果 SQL Server 通信失败并返回 SslSecurityError  错误，请确认以下信息：
- .NET Framework 已更新且在每台计算机上均启用了强加密。
- SQL Server 在主机服务器上更新。
- SQL 客户端组件在站点服务器、SMS 提供程序、站点角色服务器以及与 SQL Server 通信的所有其他系统上进行更新。

### <a name="configuration-manager-client-communication-failures"></a>Configuration Manager 客户端通信失败

如果 Configuration Manager 客户端不与站点角色终结点（比如分布点、管理点和状态迁移点）通信，则验证 Windows 是否已更新为支持 TLS 1.2，以便客户端服务器使用 WinHTTP 进行通信。

### <a name="srs-reporting-point-fails-and-returns-an-expected-error"></a>SRS 报表点失败并返回预期错误

如果 SRS 报表点没有配置报表，请检查 SRSRP.log  是否存在以下错误条目：

`The underlying connection was closed:`
`An expected error occurred on a receive.`

若要解决此问题，请执行下列步骤：

1. 验证 .NET Framework 已更新，并且在所有相关计算机上都启用了强加密。
1. 在安装任何更新之后，验证 SMS_Executive 服务已重新启动。

### <a name="application-catalog-doesnt-initialize"></a>应用程序目录未初始化

如果应用程序目录未初始化，请检查 ServicePortalWebSite.svclog  文件是否存在以下错误条目：

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

若要解决此问题，请执行下列步骤：
1. 验证 .NET Framework 已更新，并且在所有相关计算机上都启用了强加密。
1. 在应用程序目录服务器的 C:\Windows\System32\InetSrv 文件夹中，通过运行以下脚本创建 W2SP.exe.config  文件： 

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

   > [!NOTE]
   > 当为应用程序目录角色使用 HTTP 消息安全性时，WCF 将被硬编码为只使用 SSL 3.0 和 TLS 1.0。 这可以防止使用 TLS 1.2。
1. 如果有任何更改，请重新启动计算机。


### <a name="software-center-or-browser-doesnt-communicate-with-application-catalog"></a>软件中心或浏览器不与应用程序目录通信

若要解决应用程序目录与软件中心或浏览器之间的通信故障，请验证以下条件：

- .NET Framework 已更新且在每台计算机上均启用了强加密。
- 浏览器被配置为支持 TLS 1。 在 Windows 10 之前，默认情况下禁用此选项。
- 更改完成后，所有计算机都会重新启动。

   > [!NOTE]
   > 为了让软件中心与强制实施 TLS 1.2 的服务器协同工作，以便为用户提供可用的应用程序，建议删除应用程序目录角色，并让软件中心与管理点通信。 有关详细信息，请参阅[删除应用程序目录](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat)。

### <a name="service-connection-point-upload-failures"></a>服务连接点上传失败

如果服务连接点没有将数据上传到 SCCMConnectedService，请验证 .NET Framework已更新，并且在每台计算机上都启用了强加密。 更改完成后，请记住重新启动计算机。

### <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Configuration Manager 控制台显示 Intune 载入对话框

如果控制台尝试连接到 Intune 门户时出现了 Intune 载入对话框，请验证 .NET Framework 已更新，并在每台计算机上启用了强加密。  更改完成后，请记住重新启动计算机。

### <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Configuration Manager 控制台显示登录到 Azure 失败

尝试创建 Azure AD 应用程序时，如果在选择“登录”  后 Azure Services 载入对话框立即失败，请验证 .NET Framework 已更新并启用了强加密。 要使这些更改生效，需要重新启动。

## <a name="see-also"></a>另请参阅

[加密控制技术参考](cryptographic-controls-technical-reference.md)
