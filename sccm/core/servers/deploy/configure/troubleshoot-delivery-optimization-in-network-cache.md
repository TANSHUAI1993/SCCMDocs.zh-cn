---
title: DOINC 故障排除
titleSuffix: Configuration Manager
description: 关于传递优化网络内缓存的技术详细信息，可帮助解决问题。
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2dd946cd35db19622a79436b55a95f2274fa9e47
ms.sourcegitcommit: cdf2827fb3f44d7522a9b533c115f910aa9c382a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70910749"
---
# <a name="troubleshoot-delivery-optimization-in-network-cache-in-configuration-manager"></a>Configuration Manager 中的传递优化网络内缓存故障排除

本文提供有关 Configuration Manager 中的传递优化网络内缓存 (DOINC) 的技术详细信息。 这些信息有助于解决环境中可能存在的问题。 有关其工作原理及用法的详细信息，请参阅 [Configuration Manager 中的传递优化网络内缓存](/sccm/core/plan-design/hierarchy/delivery-optimization-in-network-cache)。

## <a name="verify"></a>验证

如果已正确安装传递优化缓存服务器，并已正确配置客户端，则它们会从安装在分发点上的缓存服务器下载，而不是从 Internet 下载。

验证[客户端](#bkmk_verify-client)或[服务器](#bkmk_verify-server)上的此行为。

### <a name="bkmk_verify-client"></a> 在客户端上验证

1. 在运行 Windows 10 1809 版本或更高版本的客户端上，下载云托管的内容。 有关 DOINC 支持的内容类型的详细信息，请参阅[验证 DOINC](/sccm/core/plan-design/hierarchy/delivery-optimization-in-network-cache#verify)。

2. 请打开 PowerShell 并运行以下命令：`Get-DeliveryOptimizationStatus`

例如：

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

请注意，`BytesFromCacheServer` 属性不为零。

如果客户端配置不正确，或缓存服务器未正确安装，则传递优化客户端将回退到初始云源。 然后 BytesFromCacheServer 属性将为零。

### <a name="bkmk_verify-server"></a> 在服务器上验证

首先，验证是否正确配置了注册表属性：`HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache`。 例如，驱动器缓存位置是 `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294`，其中 `PrimaryDrivesInput` 可为多个驱动器，例如 `C,D,E`。

接下来，使用以下方法，通过必需标头来模拟针对服务器的客户端下载请求。

1. 以管理员身份打开 64 位 PowerShell 窗口。
2. 运行以下命令，并针对 `<DoincServer>` 替换服务器的名称或 IP 地址：

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

输出类似于以下示例：

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

以下属性表示成功：

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>日志文件

- ARR 安装日志：`%temp%\arr_setup.log`

- DO 缓存服务器安装日志：分发点上为 `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log`，站点服务器上为 `DistMgr.log`

- IIS 运行日志：默认为 `%SystemDrive%\inetpub\logs\LogFiles`

- DO 缓存服务器运行日志：`C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > 除此之外，此日志可帮助识别 Microsoft 云的连接问题。

## <a name="setup-error-codes"></a>设置错误代码

Configuration Manager 在分发点上安装 DOINC 组件时，下表列出了可能出现的错误代码：

| 错误代码 | 错误说明 |
|------------|-------------------|
| 0x00000000 | 成功 |
| 0x00000BC2 | 成功，需要重启 |
| 0x00000643 | 一般安装故障 |
| 0x00D00001 | 只有安装 Internet Information Services (IIS) 后才能运行 DOINC 安装程序 |
| 0x00D00002 | 只有服务器上存在“默认网站”时才能运行 DOINC 安装程序 |
| 0x00D00003 | 如果已安装应用程序请求路由 (ARR)，则无法安装 DOINC |
| 0x00D00004 | 只有 Install.ps1 脚本安装了应用程序请求路由 (ARR) 后，才能运行 DOINC 安装程序 |
| 0x00D00005 | DOINC 安装程序需要以管理员身份运行的 PowerShell 会话 |
| 0x00D00006 | DOINC 安装程序只能从 64 位 PowerShell 环境运行 |
| 0x00D00007 | DOINC 安装程序只能在 Windows Server 上运行 |
| 0x00D00008 | 失败：指定的缓存驱动器数必须与指定的缓存驱动器大小百分比的数量匹配 |
| 0x00D00009 | 失败：必须提供有效的缓存节点 ID |
| 0x00D0000A | 失败：必须提供有效的缓存驱动器集 |
| 0x00D0000B | 失败：必须提供有效的缓存驱动器大小百分比集 |
| 0x00D0000C | 失败：必须提供有效的缓存驱动器大小百分比集或缓存驱动器大小（以 GB 为单位） |
| 0x00D0000D | 失败：无法同时提供有效的缓存驱动器大小百分比集和缓存驱动器大小（以 GB 为单位） |
| 0x00D0000E | 失败：指定的缓存驱动器数必须与指定的缓存驱动器大小（以 GB 为单位）的数量匹配 |
| 0x00D0000F | 失败：无法将 applicationhost.config 文件从 $AppHostConfig 备份到 $AppHostConfigDestinationName |
| 0x00D00010 | 失败：无法将默认网站 web.config 文件从 $WebsiteConfigFilePath 备份到 $WebConfigDestinationName |
| 0x00D00011 | 失败：SetupARRWebFarm.ps1 中发生了异常 |
| 0x00D00012 | 失败：SetupARRWebFarmRewriteRules.ps1 中发生了异常 |
| 0x00D00013 | 失败：SetupARRWebFarmProperties.ps1 中发生了异常 |
| 0x00D00014 | 失败：SetupAllowableServerVariables.ps1 中发生了异常 |
| 0x00D00015 | 失败：SetupFirewallRules.ps1 中发生了异常 |
| 0x00D00016 | 失败：SetupAppPoolProperties.ps1 中发生了异常 |
| 0x00D00017 | 失败：SetupARROutboundRules.ps1 中发生了异常 |
| 0x00D00018 | 失败：SetupARRDiskCache.ps1 中发生了异常 |
| 0x00D00019 | 失败：SetupARRProperties.ps1 中发生了异常 |
| 0x00D0001A | 失败：SetupARRHealthProbes.ps1 中发生了异常 |
| 0x00D0001B | 失败：VerifyIISSItesStarted.ps1 中发生了异常 |
| 0x00D0001C | 失败：SetDrivesToHealthy.ps1 中发生了异常 |
| 0x00D0001D | 失败：VerifyCacheNodeSetup.ps1 中发生了异常 |
| 0x00D0001E | 如果默认网站不在端口 80 上，则无法安装 DOINC |
| 0x00D0001F | 失败：缓存驱动器分配百分比不能超过 100 |
| 0x00D00020 | 失败：缓存驱动器分配（以 GB 为单位）不能超过驱动器的可用空间 |
| 0x00D00021 | 失败：缓存驱动器分配百分比必须大于 0 |
| 0x00D00022 | 失败：缓存驱动器分配（以 GB 为单位）必须大于 0 |
| 0x00D00023 | 失败：RegisterScheduledTask_CacheNodeKeepAlive 中发生了异常 |
| 0x00D00024 | 失败：RegisterScheduledTask_Maintenance 中发生了异常 |
| 0x00D00025 | 失败：为 HTTPS 场 $FarmName 设置重写规则时出现异常 |
| 0x00D00026 | 失败：为 HTTP 场 $FarmName 设置重写规则时出现异常 |
| 0x00D00027 | 无法安装 DOINC，因为从属软件“应用程序请求路由 (ARR)”安装失败。 请参阅位于 %temp%\arr_setup.log 的日志文件 |

## <a name="iis-configurations"></a>IIS 配置

DO 缓存服务器安装对分发点上的 IIS 配置进行了多次修改。

### <a name="application-request-routing"></a>应用程序请求路由

DO 缓存服务器安装并配置了 IIS [应用程序请求路由 (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing)。 为避免潜在的冲突，分发点无法让该组件完成安装。

### <a name="allowed-server-variables"></a>允许的服务器变量

安装 DO 缓存服务器后，默认网站具有以下本地服务器变量  ：

- HTTP_HOST
- QUERY_STRING
- X-CCC
- X-CID
- X-DOINC-OUTBOUND

### <a name="rewrite-rules"></a>重写规则

DO 缓存服务器添加以下重写规则：

#### <a name="inbound-rewrite-rules"></a>入站重写规则

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>出站重写规则

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>管理服务器资源

根据组织的更新要求，每个 DO 缓存服务器所需的磁盘空间可能会有所不同。 100 GB 的空间应该足以缓存以下内容：

- 功能更新
- 两到三个月的质量和 Office 更新
- Microsoft Intune 应用和 Windows 收件箱应用

DO 缓存服务器不应消耗太多系统内存或处理器时间。 安装 DO 缓存服务器后，如果发现了重要的进程或内存资源消耗，请分析 IIS 和 ARR 日志文件。

如果 IIS 和 ARR 日志文件在服务器上占用的空间过多，则可以使用几种方法来管理日志文件。 有关详细信息，请参阅 [Managing IIS Log File Storage](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview)（管理 IIS 日志文件存储）。

## <a name="see-also"></a>另请参阅

[Configuration Manager 中的传递优化网络内缓存](/sccm/core/plan-design/hierarchy/delivery-optimization-in-network-cache)
