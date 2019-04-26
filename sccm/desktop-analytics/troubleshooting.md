---
title: 故障排除桌面分析
titleSuffix: Configuration Manager
description: 若要帮助你解决使用 Desktop 分析问题的技术详细信息。
ms.date: 04/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0da26f1ea2b7f7c0c49377cb934e451d56889b7
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62261478"
---
# <a name="troubleshooting-desktop-analytics"></a>故障排除桌面分析

使用本文中详细信息以帮助您使用与 Configuration Manager 集成的 Desktop 分析进行问题故障排除。



## <a name="confirm-prerequisites"></a>确认系统必备组件

许多常见的问题被由于缺少的必备组件。 首先请确认以下配置：

- [先决条件](/sccm/desktop-analytics/overview#prerequisites)  

- [Windows 组件更新](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [如何启用数据共享](/sccm/desktop-analytics/enable-data-sharing)，其中涵盖以下主题：  

    - 客户端需要连接 Internet 的终结点  

    - 代理服务器身份验证  

    - 诊断数据级别  



## <a name="monitor-connection-health"></a>监视连接运行状况

使用**连接运行状况**仪表板在 Configuration Manager 中向下钻取到类别的设备运行状况。 在 Configuration Manager 控制台中，转到**软件库**工作区中，展开**Desktop 分析服务**节点，然后选择**连接运行状况**仪表板。  

![配置管理器连接运行状况仪表板的屏幕截图](media/connection-health-dashboard.png)

当首次设置 Desktop 分析时，这些图表可能不会显示完整的数据。 可能需要 2-3 天的活动设备将诊断数据发送到 Desktop 分析服务，该服务处理数据，并与 Configuration Manager 站点同步时间。<!-- 4098037 -->

如果您认为某些设备不显示在桌面 Analytics 中，先检查所占的百分比**连接的设备**。 如果该值小于 100%，请确保由桌面分析支持的设备。 有关详细信息，请参阅[先决条件](/sccm/desktop-analytics/overview#prerequisites)。


### <a name="connection-health-states"></a>连接运行状况状态

接下来回顾**连接运行状况**图表。 它在以下的运行状况类别中显示设备的数：  

- [正确注册](#properly-enrolled)  
- [配置问题](#configuration-issues)  
- [未安装客户端](#client-not-installed)  
- [等待注册](#waiting-for-enrollment)  
- [缺少的必备组件](#missing-prerequisites)  
- [缺少数据](#missing-data)  

选择要删除或将其添加从图表的类别名称。 此操作有助于来放大图表，以便您可以看到较小的段的相对大小。

#### <a name="properly-enrolled"></a>正确注册

设备具有以下属性：

- Configuration Manager 1810 或更高版本的客户端版本  
- 没有配置错误  
- 桌面分析过去 28 天内此设备收到完整的诊断数据  
- 桌面分析具有一个完整的清单的设备的配置和安装的应用  

#### <a name="configuration-issues"></a>配置问题

Configuration Manager 检测到与桌面分析所需的配置的一个或多个问题。 有关详细信息，请参阅的列表[Desktop 分析 Configuration Manager 中的设备属性](#bkmk_config-issues)。  

#### <a name="client-not-installed"></a>未安装客户端

将设备作为目标以桌面分析，但不是 Configuration Manager 客户端。

Configuration Manager 客户端需要配置和管理设备的桌面分析。 有关详细信息，请参阅[客户端安装方法](/sccm/core/clients/deploy/plan/client-installation-methods)。  

#### <a name="waiting-for-enrollment"></a>等待注册

桌面分析没有此设备的诊断数据。 此问题可能会因为设备最近添加到目标集合，以及尚未尚未发送数据。 这还意味着设备不是正确与服务进行通信和最新的诊断数据是超过 28 天。

请确保设备能够与服务进行通信。 有关详细信息，请参阅[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)。  

#### <a name="missing-prerequisites"></a>缺少的必备组件

Configuration Manager 客户端不是至少版本 1810 (5.0.8740)。

更新到最新版本的客户端。 请考虑启用 Configuration Manager 站点的客户端自动升级。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade)。  

#### <a name="missing-data"></a>缺少数据

桌面分析不能创建兼容性评估。 它不包含用于设备的配置 （人口普查） 的完整数据集，或者已安装的应用 （库存）。

当设备重试时，通常是自动修复此问题。 如果仍存在，请确保设备能够与服务通信。 有关详细信息，请参阅[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)。  


### <a name="device-list"></a>设备列表

若要查看按状态的设备的特定列表，请使用启动**连接运行状况**仪表板。 选择其中一个的段**连接运行状况**磁贴，然后深化到此类别中的设备的列表。 默认情况下，此自定义设备视图显示桌面分析以下列：

- 商业 ID 配置
- 最小兼容性更新
- Windows 诊断数据参加
- Windows 商业数据参加
- Windows 诊断终结点连接
- Office 诊断终结点连接

这些列对应于键[先决条件](/sccm/desktop-analytics/overview#prerequisites)以将设备与 Desktop Analytics 进行通信。

![屏幕截图的正确注册的设备列表](media/sccm-device-list-properly-enrolled.png)

选择要查看详细信息窗格中的可用属性的完整列表的设备。 您还可以添加这些属性的任何列作为到设备列表。


### <a name="bkmk_config-issues"></a> 桌面分析设备属性在配置管理器

设备列表中提供了以下各列：

- [评估程序配置](#appraiser-configuration)  
- [最小兼容性更新](#minimum-compatibility-update)  
- [评估程序版本](#appraiser-version)  
- [上次成功完全评估程序运行](#last-successful-full-run-of-appraiser)  
- [估价师数据收集](#appraiser-data-collection)  
- [最后一次成功的完整运行的人口普查](#last-successful-full-run-of-census)  
- [人口普查数据收集](#census-data-collection)  
- [Windows 诊断终结点连接](#windows-diagnostic-endpoint-connectivity)  
- [检查最终用户诊断数据](#check-end-user-diagnostic-data)  
- [检查用户代理](#check-user-proxy)  
- [商业 ID 配置](#commercial-id-configuration)  
- [Windows 商业数据参加](#windows-commercial-data-opt-in)  
- [检查诊断数据中的设备名称](#check-device-name-in-diagnostic-data)  
- [DiagTrack 服务配置](#diagtrack-service-configuration)  
- [DiagTrack 版本](#diagtrack-version)  
- [SQM ID 检索](#sqm-id-retrieval)  
- [唯一的设备标识符检索](#unique-device-identifier-retrieval)  
- [Windows 诊断数据参加](#windows-diagnostic-data-opt-in)  
- [Office 诊断终结点连接](#office-diagnostic-endpoint-connectivity)  
- [Office 诊断数据选择项](#office-diagnostic-data-opt-in)

#### <a name="appraiser-configuration"></a>评估程序配置

<!--20,21-->
评估程序是 Windows 组件，它对应于[兼容性更新](/sccm/desktop-analytics/enroll-devices#update-devices)。 它将评估应用程序和适用于 Windows 的最新版本的兼容性的设备上的驱动程序。 

如果此检查成功，然后评估程序组件在设备上正确配置。

否则，它可能显示下列错误之一：

- 不能配置设备应用程序兼容性数据集合 (SetRequestAllAppraiserVersions)。 检查日志中的异常详细信息  

- 不能配置设备应用程序兼容性数据集合 (SetRequestAllAppraiserVersions)。 检查日志中的异常详细信息  

- 无法写入注册表项 RequestAllAppraiserVersions `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`。 检查权限  

检查此注册表项的权限。 请确保本地系统帐户可以访问此密钥，以便 Configuration Manager 客户端设置。  

有关详细信息，在客户端上查看 M365AHandler.log。  

#### <a name="minimum-compatibility-update"></a>最小兼容性更新

<!--18,19,32-->
兼容性更新 (appraiser.dll) 不是已安装或在设备上已过期。 它是早于 Desktop 分析，10.0.17763 的最低要求。

安装最新的兼容性更新。 有关详细信息，请参阅[兼容性更新](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)。

#### <a name="appraiser-version"></a>评估程序版本

此属性显示在设备上评估程序组件的当前版本。 它在显示的文件版本`%windir%\System32\appraiser.dll`，没有小数点。 例如，文件版本 10.0.17763 显示为 10017763。

#### <a name="last-successful-full-run-of-appraiser"></a>上次成功完全评估程序运行

此属性显示的日期和时间，设备上次成功运行评估程序。

#### <a name="appraiser-data-collection"></a>估价师数据收集

<!--Appraiser run status-->
<!--22,33-->
此属性显示 Windows 的最新结果运行评估程序组件。

如果不成功，它可能会显示以下错误之一：

- 不能收集应用程序兼容性数据 (RunAppraiser)。 检查日志了解详细信息  

- 应用程序兼容性数据集合 (CompatTelRunner.exe) 结束，错误代码  

有关详细信息，在客户端上查看 M365AHandler.log。

检查是否有以下文件： `%windir%\System32\CompatTelRunner.exe`。 如果不存在，重新安装所需[兼容性更新](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)。 请确保没有其他系统组件删除该文件，例如组策略或反恶意软件服务。

如果客户端上的 M365Handler.log 文件包含以下错误之一： `RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005`  

为了帮助修正这些错误，请在受影响的客户端上从提升的 Windows PowerShell 控制台运行以下命令：

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

#### <a name="last-successful-full-run-of-census"></a>最后一次成功的完整运行的人口普查

此属性显示的日期和时间，设备上次成功运行人口普查。

#### <a name="census-data-collection"></a>人口普查数据收集

<!-- Census run status -->
<!--51,52-->
人口普查是列出清单的设备的 Windows 组件。 使用此清单数据以了解设备和其配置。

此属性显示 Windows 的最新结果运行人口普查组件。

如果不成功，它可能会显示以下错误之一：

- 不能收集有关设备和其配置 (RunCensus) 数据。 检查日志中的异常详细信息  

- 设备和配置数据收集工具 (devicecensus.exe) 找不到  

有关详细信息，在客户端上查看 M365AHandler.log。

检查是否有以下文件： `%windir%\System32\DeviceCensus.exe`。 如果不存在，重新安装所需[兼容性更新](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)。 请确保没有其他系统组件删除该文件，例如组策略或反恶意软件服务。

#### <a name="windows-diagnostic-endpoint-connectivity"></a>Windows 诊断终结点连接

<!--12,15-->
如果此检查成功，则可以连接到的连接的用户体验与遥测终结点 （顶点） 设备。

否则，它可能会显示以下错误之一：  

- 无法连接到连接的用户体验与遥测端点 （顶点）。 检查你的网络/代理设置  

- 不能检查连接到连接的用户体验与遥测终结点 (CheckVortexConnectivity)。 检查日志中的异常详细信息  

设备会验证连接到以下终结点的 GET 请求根据 OS 版本：

| 操作系统版本 | 终结点 |
|------------|----------|
| Windows 10，版本 1803 版或更高版本且最新的累积更新 | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10，版本 1803 版或更高版本，而无需 2018年 09 或更高版本累积更新 | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10 版本 1709 或更早版本 | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 或 Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

请确保设备能够与服务进行通信。 此检查验证某些但并非全部所需的终结点。 有关详细信息，请参阅[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)。  

有关详细信息，在客户端上查看 M365AHandler.log。  

#### <a name="check-end-user-diagnostic-data"></a>检查最终用户诊断数据

<!--1004-->
如果此检查不成功，用户选择了较低设备上的 Windows 诊断数据。 它还可能引起冲突的组策略对象。 有关详细信息，请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。

根据你的业务需求，可以禁用通过组策略的用户选择。 使用设置为**配置遥测参加设置用户界面**。 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management)。

#### <a name="check-user-proxy"></a>检查用户代理

<!--30,35-->
默认情况下，DisableEnterpriseAuthProxy 设置启用适用于 Windows 7。 对于 Windows 8.1 的计算机，Configuration Manager 将 DisableEnterpriseAuthProxy 设置设为 0 （不禁用）。

此属性可能会显示以下错误：

- 当启用了身份验证代理。 DisableEnterpriseAuthProxy 中设置为 0 `HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- 不能检查身份验证代理状态。 检查日志中的异常详细信息

有关详细信息，在客户端上查看 M365AHandler.log。  

检查此注册表项的权限。 请确保本地系统帐户可以访问此密钥，以便 Configuration Manager 客户端设置。 它还可能引起冲突的组策略对象。 有关详细信息，请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。  

#### <a name="commercial-id-configuration"></a>商业 ID 配置

<!--9, 11, 53-->
Microsoft 使用的唯一商业 ID 映射到 Desktop 分析工作区设备中的信息。 当 Configuration Manager 将使用 Desktop 分析时，它会自动查询的服务的此 id。 配置管理器自动应用于客户端向其目标 Desktop 分析设置此 ID。

如果此检查成功，然后该设备已正确配置了一个商业 id。

否则，它可能会显示以下错误之一：

- 无法写入注册表项 CommercialId `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`。 检查权限  

- 无法更新注册表项中的 CommercialId `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`。 检查日志中的异常详细信息  

- 提供在正确的 CommercialId 值 `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

有关详细信息，在客户端上查看 M365AHandler.log。  

检查此注册表项的权限。 请确保本地系统帐户可以访问此密钥，以便 Configuration Manager 客户端设置。 它还可能引起冲突的组策略对象。 有关详细信息，请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。  

没有为设备不同的 ID。 组策略使用此注册表项。 它将优先于配置管理器提供的 ID。  

若要查看桌面 Analytics 门户中的商用 ID，请使用以下过程：

1. 转到桌面分析门户中，并选择**连接服务**全局设置组中。  

2. 在中**连接的服务**窗格中，**注册设备**窗格中选择默认情况下。 在注册设备窗格中，信息部分显示商业 ID 键。  

![在 Desktop 分析门户中的商业 ID 的屏幕截图](media/commercial-id.png)

> [!Important]  
> 仅**获取新 ID 密钥**时不能使用当前的一个。 如果你重新生成商用 ID，部署到设备的新 ID。 此过程可能会导致在转换期间丢失的诊断数据。  

#### <a name="windows-commercial-data-opt-in"></a>Windows 商业数据参加

<!--64-->
此属性是特定于运行 Windows 7 或 Windows 8.1 的设备。 运行类似的测试，作为[Windows 诊断数据参加](#windows-diagnostic-data-opt-in)，但对于 CommercialDataOptIn 值。

#### <a name="check-device-name-in-diagnostic-data"></a>检查诊断数据中的设备名称

<!--56,58-->
如果此检查成功，然后该设备已正确配置共享设备的名称。

否则，它可能会显示以下错误之一：

- 无法检查的设备名称以作为 Windows 诊断数据的一部分发送给 Microsoft。 检查日志中的异常详细信息  

- 无法写入注册表项 AllowDeviceNameInTelemetry `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`。 检查权限  

有关详细信息，在客户端上查看 M365AHandler.log。  

检查此注册表项的权限。 请确保本地系统帐户可以访问此密钥，以便 Configuration Manager 客户端设置。 它还可能引起冲突的组策略对象。 有关详细信息，请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。  

请确保另一个策略机制，如组策略未禁用此设置。

#### <a name="diagtrack-service-configuration"></a>DiagTrack 服务配置

<!--44,45,50-->
如果此检查成功，然后 DiagTrack 组件在设备上正确配置。 Desktop 分析所需的最低版本是 10010586 (10.0.10586)。

否则，它可能显示下列错误之一：

- 连接的用户体验和遥测 (diagtrack.dll) 组件已过时。 检查要求  

- 找不到连接的用户体验和遥测 (diagtrack.dll) 组件。 检查要求  

- 启用并启动连接用户体验和遥测服务，以将数据发送给 Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

安装最新的更新。 有关详细信息，请参阅[设备更新](/sccm/desktop-analytics/enroll-devices#update-devices)。

请确保**连接用户体验和遥测**在设备上的服务正在运行。

#### <a name="diagtrack-version"></a>DiagTrack 版本

此属性显示在设备上的互连用户体验与遥测组件的当前版本。 它在显示的文件版本`%windir%\System32\diagtrack.dll`，没有小数点。 例如，文件版本 10.0.10586 显示为 10010586。

#### <a name="sqm-id-retrieval"></a>SQM ID 检索

<!--38-->
此属性是主要适用于 Windows 7 设备。 它可能会用作由更高版本的操作系统版本回退标识符的设备。

如果不成功，它可能会显示以下错误：

- 无法检索旧的设备遥测标识符 (SQM ID)

有关详细信息，在客户端上查看 M365AHandler.log。  

请确保你的环境中没有重复的 Id。 例如，如果设备已不通用化的 OS 映像部署。

#### <a name="unique-device-identifier-retrieval"></a>唯一的设备标识符检索

<!--54-->
桌面分析使用 Microsoft 帐户服务的更可靠的设备标识。

请确保**Microsoft 帐户登录助手**服务未被禁用。 启动类型应为**手动 （触发器启动）**。

若要禁用最终用户的 Microsoft 帐户访问，而不是阻塞此终结点使用策略设置。 有关详细信息，请参阅[企业中的 Microsoft 帐户](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)。

#### <a name="windows-diagnostic-data-opt-in"></a>Windows 诊断数据参加

<!--8,40,55,62-->
此属性检查已正确配置 Windows 以允许诊断数据。 它会检查以下注册表项中的 AllowTelemetry 值：

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

检查这些注册表项的权限。 请确保本地系统帐户可以访问 Configuration Manager 客户端设置这些密钥。 它还可能引起冲突的组策略对象。 有关详细信息，请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。  

有关详细信息，在客户端上查看 M365AHandler.log。  

#### <a name="office-diagnostic-endpoint-connectivity"></a>Office 诊断终结点连接

<!-- 1001,1002,1003 -->

如果此检查成功，则可以连接到 Office 诊断终结点。

否则，它可能会显示以下错误之一：

- 无法连接到 Office 诊断终结点 (Aria)。 检查你的网络/代理设置  

- 无法连接到 Office 诊断终结点 (Nexusrules)。 检查你的网络/代理设置  

- 无法连接到 Office 诊断终结点 (Nexus)。 检查你的网络/代理设置  

请确保设备能够与服务进行通信。 有关详细信息，请参阅[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)。  

#### <a name="office-diagnostic-data-opt-in"></a>Office 诊断数据选择项

<!-- SCCMDocs-pr 3570 -->
从 Configuration Manager 版本 1902年，对将 Office 服务和诊断数据发送到 Microsoft 更改了行为。 此属性检查 Office 策略设置已正确配置。 这些设置控制最小所需的数据，以帮助保持 Office 安全、 最新状态，并按预期方式运行在设备上安装。

有关详细信息，请参阅[隐私概述可以控制对 Office 365 专业增强版](https://docs.microsoft.com/DeployOffice/privacy/overview-privacy-controls)。 使用本文详细介绍隐私控制诊断数据收集并向 Microsoft 发送有关 Office 客户端软件在 Windows 上你的组织中的计算机。

此检查的 Configuration Manager 版本 1810年客户端不会成功。 更新到最新版本的客户端。 请考虑启用 Configuration Manager 站点的客户端自动升级。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade)。



## <a name="log-files"></a>日志文件

使用以下日志文件来帮助解决与桌面 Analytics 与 Configuration Manager 集成的问题。


### <a name="service-connection-point"></a>服务连接点

以下日志文件位于以下目录中的服务连接点： `C:\Program Files\Configuration Manager\Logs\M365A`:

| 日志 | 描述 |
|---------|---------|
| **M365ADeploymentPlanWorker.log** | 有关从桌面分析部署计划同步的信息的云服务到本地 Configuration Manager |
| **M365ADeviceHealthWorker.log** | 有关设备运行状况的信息将从 Configuration Manager 上传到 Microsoft 云 |
| **M365AUploadWorker.log** | 有关集合和设备的信息将从 Configuration Manager 上传到 Microsoft 云 |
| **SmsAdminUI.log** | 有关 Configuration Manager 控制台活动，例如，配置 Azure 云服务的信息  |


### <a name="configuration-manager-client"></a>Configuration Manager 客户端

以下日志文件位于以下目录中的 Configuration Manager 客户端： `C:\Windows\CCM\logs`:

| 日志 | 描述 |
|---------|---------|
| **M365AHandler.log** | 有关桌面分析设置策略的信息 |


### <a name="enable-verbose-logging"></a>启用详细日志记录

1. 对服务连接点，请转到以下注册表项： `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. 设置**LogLevel**值设为 `0`  
3. （可选）在站点数据库上运行以下 SQL 命令：  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. 重新启动**SMS_EXECUTIVE**服务在站点服务器上



## <a name="bkmk_AzureADApps"></a> Azure AD 应用程序

桌面 Analytics 添加到你的 Azure AD 的以下应用程序：

- **配置管理器微服务**:将 Configuration Manager 连接与桌面的分析。 此应用具有没有访问要求。  

- **Office 365 客户端管理**:从 Log Analytics 工作区中检索数据。 此应用需要写入到 Log Analytics 的访问权限。  

- **MALogAnalyticsReader**:检索 OMS 组和 Log Analytics 中创建的设备。 有关详细信息，请参阅[MALogAnalyticsReader 应用程序角色](#bkmk_MALogAnalyticsReader)。  

如果需要将这些应用程序提供了完成设置后，请转到**连接服务**窗格。 选择**配置用户和应用访问**，将应用和设置。  

- **Azure AD 应用程序为 Configuration Manager**。 如果您需要预配或向上完成设置后对连接问题进行故障排除，请参阅[创建应用的 Configuration Manager](/sccm/desktop-analytics/set-up#create-app-for-configuration-manager)。 此应用需要**CM 集合数据写入**并**读取 CM 集合数据**上**配置管理器服务**API。  

### <a name="bkmk_MALogAnalyticsReader"></a> MALogAnalyticsReader 应用程序角色

如果设置了桌面分析时，你代表你的组织接受一个许可。 此许可是将 MALogAnalyticsReader 应用程序分配工作区的 Log Analytics 读者角色。 此应用程序角色是桌面分析所需。

如果存在此过程的问题在设置过程已启动，使用以下过程来手动添加此权限：

1. 转到[Azure 门户](http://portal.azure.com)，然后选择**的所有资源**。 选择类型的工作区**Log Analytics**。  

2. 在工作区菜单中，选择**访问控制 (IAM)**，然后选择**添加**。  

3. 在中**添加权限**面板中，配置以下设置：  

    - **角色**:**Log Analytics 读者**  

    - **分配其访问权限**:**Azure AD 用户、 组或应用程序**  

    - **选择**:**MALogAnalyticsReader**  

4. 选择“保存”。

门户会显示一个通知它添加的角色分配的。


## <a name="data-latency"></a>数据滞后时间

<!-- 3846531 -->
每日刷新桌面 Analytics 门户中的数据。 此刷新包括收集诊断数据从设备更改和对配置进行任何更改。 例如，当你更改的资产**升级决策**，它可能会导致更改到设备的就绪状态与安装该资产。

- **管理员更改**九个小时内通常由桌面 Analytics 服务处理。 例如，如果在下午 11:00 UTC 进行更改，在门户应反映这些更改之前 08:00 AM UTC 下一天。

- **设备更改**检测到通过在 UTC 午夜本地时间中的通常包含在每日刷新。 通常是延迟的额外 23 小时与处理相比管理更改的设备更改相关联。

如果未看到更改这些时间框架内更新，等待下一个每日刷新的另一个 24 小时。 如果您看到的更长的延迟，请检查服务运行状况仪表板。 如果该服务报告为正常运行，请联系 Microsoft 支持部门。

当首次设置 Desktop 分析时，Configuration Manager 和桌面 Analytics 门户中的图表可能不会显示完整的数据。 可能需要 2-3 天的活动设备将诊断数据发送到 Desktop 分析服务，该服务处理数据，并与 Configuration Manager 站点同步时间。

在 Configuration Manager 层次结构中，可能需要 10 分钟后，新的集合来显示的部署计划。 主站点创建集合，并与 Desktop 分析的管理中心站点同步。<!-- 3896921 -->
