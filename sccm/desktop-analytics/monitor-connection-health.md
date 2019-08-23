---
title: 监视器连接运行状况
titleSuffix: Configuration Manager
description: 有关如何在 Configuration Manager 中监视桌面分析的连接运行状况和设备状态的详细信息。
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17a58992c01f59080edd74051329b82a0f760938
ms.sourcegitcommit: e0d303d87c737811c2d3c40d01cd3d260a5c7bde
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69974796"
---
# <a name="monitor-connection-health"></a>监视器连接运行状况

使用 Configuration Manager 中的 "**连接运行状况**" 仪表板, 按设备运行状况向下钻取类别。 在 Configuration Manager 控制台中, 打开 "**软件库**" 工作区, 展开 " **Desktop Analytics 服务**" 节点, 然后选择 "**连接运行状况**" 仪表板。  

![Configuration Manager 连接运行状况仪表板的屏幕截图](media/connection-health-dashboard.png)

首次设置桌面分析时, 这些图表可能不会显示完整的数据。 活动设备需要2-3 天才能将诊断数据发送到桌面分析服务、用于处理数据的服务, 然后与 Configuration Manager 网站同步。<!-- 4098037 -->


## <a name="connection-details"></a>连接详细信息

此磁贴显示有关从 Configuration Manager 到桌面分析的连接的下列基本信息:

- **租户名称**:" **Azure 服务**" 节点中的桌面分析连接的名称

- **目标集合**：将 Configuration Manager 连接到桌面分析时指定的*目标集合*。 此集合包括 Configuration Manager 配置商业 ID 和诊断数据设置的所有设备。 它是 Configuration Manager 连接到桌面分析服务的完整设备集。

- **目标设备**:目标集合中的所有设备减去以下类型的设备:

    - 已解除授权
    - 弃用
    - 非活动
    - 无
    - 运行长期服务通道 (LTSC) 的 Windows 10 版本的设备
    - 运行 Windows Server 的设备

    有关这些设备状态的详细信息, 请参阅[关于客户端状态](/sccm/core/clients/manage/monitor-clients#bkmk_about)。

    > [!Note]  
    > Configuration Manager 上传到桌面分析目标集合中的所有设备减去已停止和过时的客户端。

- **适用于 DA 的设备**:目标为不符合桌面分析的设备的设备数。 例如, 运行 Windows Server 或 Windows 10 长期服务通道 (LTSC) 的目标集合中的设备。


## <a name="last-sync-details"></a>上次同步的详细信息

此磁贴显示 Configuration Manager 与桌面分析云服务同步以及它所同步的设备的数量。

- **同步的设备**:Configuration Manager 发送到桌面分析的唯一设备数。 该服务将这些设备包括在当前可见的快照中。

- **上次服务同步**:与桌面分析门户中**最后一次更新**的时间相同。

- **下一个服务同步**:当你预计桌面分析中的下一个每日快照。

> [!Note]  
> 第一次将设备注册到桌面分析时, 可能需要几天时间才能上传和处理数据。 在此期间, "**最后一个同步详细信息**" 磁贴可能会显示为空白。 此外, 当你请求按需快照时, 此磁贴中的任何值都不会自动更新。 有关详细信息, 请参阅[数据延迟](/sccm/desktop-analytics/troubleshooting#data-latency)。

如果认为某些设备不显示在桌面分析中, 请确保设备受桌面分析支持。 有关详细信息，请参阅[先决条件](/sccm/desktop-analytics/overview#prerequisites)。


## <a name="connection-health"></a>连接运行状况

**连接运行状况**图表显示处于以下运行状况状态的设备数:  

- 已[正确注册](#properly-enrolled):设备在桌面分析中显示为具有完整清单
- [无法注册](#unable-to-enroll):出现阻止设备注册的阻止性问题
- [配置警报](#configuration-alert):设备不会出现在桌面分析中, 或显示为不完整的清单。 Configuration Manager 还识别到设备注册问题。
- 正在[等待注册](#awaiting-enrollment):Configuration Manager 配置设备, 但它还不会出现在桌面分析中
- [状态挂起](#status-pending):Configuration Manager 仍在配置此设备, 或者设备上没有足够的数据来确定其状态
- [缺少数据](#missing-data):Configuration Manager 配置设备, 但桌面分析只包含部分数据

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

此图表中的设备总数应该与 "连接详细信息" 磁贴中**符合 DA**值的设备的数量相同。

在图表中选择要向下钻取到处于该状态的设备的列表。 有关详细信息, 请参阅[设备列表](#device-list)。

在图例中选择要从图表中删除或添加的类别名称。 此操作有助于放大图表, 以便查看较小段的相对大小。

### <a name="properly-enrolled"></a>已正确注册

设备具有以下属性:

- Configuration Manager 1902 或更高版本的客户端版本  
- 没有配置错误  
- 桌面分析在过去28天内接收到此设备的完整诊断数据  
- 桌面分析提供设备配置和已安装应用的完整清单  

### <a name="unable-to-enroll"></a>无法注册

Configuration Manager 检测到一个或多个阻止设备注册的阻止问题。 有关详细信息, 请参阅中的[桌面分析设备属性列表 Configuration Manager](#bkmk_config-issues)。  

例如, Configuration Manager 客户端的版本不低于 1902 (5.0.8790)。 将客户端更新到最新版本。 请考虑为 Configuration Manager 站点启用自动客户端升级。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade)。  

### <a name="configuration-alert"></a>配置警报

设备不会出现在桌面分析中, 或显示为不完整的清单。 Configuration Manager 还识别到设备注册问题。 有关详细信息, 请参阅中的[桌面分析设备属性列表 Configuration Manager](#bkmk_config-issues)。

例如, 设备没有与服务的连接。 有关详细信息, 请参阅[Windows 诊断终结点连接](#windows-diagnostic-endpoint-connectivity)。

### <a name="awaiting-enrollment"></a>正在等待注册

桌面分析没有此设备的诊断数据。 此问题可能是因为最近将设备添加到目标集合, 并且尚未发送数据。 它也可能表示设备未与服务正常通信, 最新的诊断数据超过28天。

请确保设备可以与服务进行通信。 有关详细信息, 请参阅[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)。  

### <a name="status-pending"></a>状态已挂起

Configuration Manager 仍在配置此设备, 或者设备上没有足够的数据来确定其状态。

### <a name="missing-data"></a>缺少数据

Configuration Manager 已成功配置设备, 但桌面分析无法创建兼容性评估。 它没有为设备配置 (人口普查) 或已安装的应用 (库存) 提供完整的数据集。

当设备重试时, 通常会自动修复此问题。 如果此问题仍然存在, 请确保设备能够与服务进行通信。 有关详细信息, 请参阅[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)。  


## <a name="device-list"></a>设备列表

若要按状态查看特定的设备列表, 请从 "**连接运行状况**" 仪表板开始。 选择**连接运行状况**磁贴的其中一个段, 并向下钻取到处于此状态的设备的列表。 默认情况下, 此自定义设备视图显示以下桌面分析列:

- 商业 ID 配置
- 最低兼容性更新
- Windows 诊断数据选择加入
- Windows 商业数据选择加入
- Windows 诊断终结点连接

> [!Note]  
> 忽略**Office 诊断终结点连接**列。 它保留供将来的功能之用。

这些列与设备进行桌面分析的主要[先决条件](/sccm/desktop-analytics/overview#prerequisites)相对应。

![正确注册的设备列表的屏幕截图](media/sccm-device-list-properly-enrolled.png)

选择一个设备, 查看详细信息窗格中可用属性的完整列表。 你还可以将任何这些属性作为列添加到设备列表中。


## <a name="bkmk_config-issues"></a>设备属性

以下桌面分析设备属性可作为 Configuration Manager 设备列表中的列:

- [人员配置](#appraiser-configuration)  
- [最低兼容性更新](#minimum-compatibility-update)  
- [人员版本](#appraiser-version)  
- [上次成功的人员完全运行](#last-successful-full-run-of-appraiser)  
- [人员数据收集](#appraiser-data-collection)  
- [上次成功的人口普查完全运行](#last-successful-full-run-of-census)  
- [人口普查数据收集](#census-data-collection)  
- [Windows 诊断终结点连接](#windows-diagnostic-endpoint-connectivity)  
- [查看最终用户诊断数据](#check-end-user-diagnostic-data)  
- [检查用户代理](#check-user-proxy)  
- [商业 ID 配置](#commercial-id-configuration)  
- [Windows 商业数据选择加入](#windows-commercial-data-opt-in)  
- [检查诊断数据中的设备名称](#check-device-name-in-diagnostic-data)  
- [DiagTrack 服务配置](#diagtrack-service-configuration)  
- [DiagTrack 版本](#diagtrack-version)  
- [SQM ID 检索](#sqm-id-retrieval)  
- [唯一的设备标识符检索](#unique-device-identifier-retrieval)  
- [Windows 诊断数据选择加入](#windows-diagnostic-data-opt-in)  

> [!Note]  
> 忽略**office 诊断终结点连接**和**office 诊断数据选择**的属性。 它们是为将来的功能而保留的。

"连接运行状况" 仪表板的 "**最常见注册阻止程序" 和 "配置警报**" 磁贴显示设备最常报告为问题的属性。

### <a name="appraiser-configuration"></a>人员配置

<!--20,21-->
人员是对应于[兼容性更新](/sccm/desktop-analytics/enroll-devices#update-devices)的 Windows 组件。 它会评估设备上的应用和驱动程序, 以与最新版本的 Windows 兼容。 

如果此检查成功, 则已在设备上正确配置人员组件。

否则, 可能会显示以下错误之一:

- 无法配置设备应用兼容性数据收集 (SetRequestAllAppraiserVersions)。 检查日志中是否有异常详细信息  

- 无法配置设备应用兼容性数据收集 (SetRequestAllAppraiserVersions)。 检查日志中是否有异常详细信息  

- 无法将 RequestAllAppraiserVersions 写入注册表项`HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`。 检查权限  

检查此注册表项的权限。 请确保本地系统帐户可以访问此密钥, 以便 Configuration Manager 客户端进行设置。  

有关详细信息, 请查看客户端上的 M365AHandler。  

### <a name="minimum-compatibility-update"></a>最低兼容性更新

<!--18,19,32-->
兼容性更新 (人员) 未在设备上安装或过期。 它比桌面分析的最低要求10.0.17763。

安装最新的兼容性更新。 有关详细信息, 请参阅[兼容性更新](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)。

### <a name="appraiser-version"></a>人员版本

此属性显示设备上的人员组件的当前版本。 它显示上`%windir%\System32\appraiser.dll`的文件版本, 不包含小数点。 例如, 文件版本10.0.17763 显示为10017763。

### <a name="last-successful-full-run-of-appraiser"></a>上次成功的人员完全运行

此属性显示设备上一次成功运行人员的日期和时间。

### <a name="appraiser-data-collection"></a>人员数据收集

<!--Appraiser run status-->
<!--22,33-->
此属性显示运行人员组件的 Windows 的最新结果。

如果不成功, 它可能会显示以下错误之一:

- 无法收集应用兼容性数据 (RunAppraiser)。 查看日志以了解详细信息  

- 应用兼容性数据收集 (CompatTelRunner) 以错误代码结束  

有关详细信息, 请查看客户端上的 M365AHandler。

检查以下文件: `%windir%\System32\CompatTelRunner.exe`。 如果它不存在, 请重新安装所需的[兼容性更新](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)。 请确保没有其他系统组件正在删除此文件, 如组策略或反恶意软件服务。

如果客户端上的 M365AHandler 文件包含以下错误之一:
```
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

若要帮助修正这些错误, 请在受影响的客户端上从提升的 Windows PowerShell 控制台运行以下命令:

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

### <a name="last-successful-full-run-of-census"></a>上次成功的人口普查完全运行

此属性显示设备上次成功运行人口普查的日期和时间。

### <a name="census-data-collection"></a>人口普查数据收集

<!-- Census run status -->
<!--51,52-->
人口普查是对设备进行清点的 Windows 组件。 此清单数据用于了解设备及其配置。

此属性显示运行人口普查组件的 Windows 的最新结果。

如果不成功, 它可能会显示以下错误之一:

- 无法收集有关设备及其配置 (RunCensus) 的数据。 检查日志中是否有异常详细信息  

- 找不到设备和配置数据收集工具 (devicecensus)  

有关详细信息, 请查看客户端上的 M365AHandler。

检查以下文件: `%windir%\System32\DeviceCensus.exe`。 如果它不存在, 请重新安装所需的[兼容性更新](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)。 请确保没有其他系统组件正在删除此文件, 如组策略或反恶意软件服务。

### <a name="windows-diagnostic-endpoint-connectivity"></a>Windows 诊断终结点连接

<!--12,15-->
如果此检查成功, 则设备可以连接到连接的用户体验和遥测终结点 (Vortex)。

否则, 它可能会显示以下错误之一:  

- 无法连接到连接的用户体验和遥测终结点 (Vortex)。 检查网络/代理设置  

- 无法检查与连接的用户体验和遥测终结点 (CheckVortexConnectivity) 的连接。 检查日志中是否有异常详细信息  

设备基于 OS 版本验证是否已通过 GET 请求连接到以下终结点:

| 操作系统版本 | 终结点 |
|------------|----------|
| Windows 10 版本1803或更高版本, 具有最新累积更新 | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10 版本1803或更高版本, 无需2018-09 或更高版本的累积更新 | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10 版本1709或更早版本 | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 或 Windows 8。1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

请确保设备可以与服务进行通信。 此检查将验证某些 (但不是全部) 所需的终结点。 有关详细信息, 请参阅[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)。  

有关详细信息, 请查看客户端上的 M365AHandler。  

### <a name="check-end-user-diagnostic-data"></a>查看最终用户诊断数据

<!--1004-->
如果此检查不成功, 则用户在设备上选择了更低的 Windows 诊断数据。 它也可能由冲突的组策略对象引起。 有关详细信息, 请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。

根据你的业务需求, 可以通过组策略禁用用户选择。 使用设置**配置遥测选项设置用户界面**。 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management)。

### <a name="check-user-proxy"></a>检查用户代理

<!--30,35-->
默认情况下, 为 Windows 7 启用了 DisableEnterpriseAuthProxy 设置。 对于 Windows 8.1 计算机, Configuration Manager 将 DisableEnterpriseAuthProxy 设置设置为 0 (未禁用)。

此属性可能会显示以下错误:

- 已启用身份验证代理。 将 DisableEnterpriseAuthProxy 设置为 0 in`HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- 无法检查身份验证代理状态。 检查日志中是否有异常详细信息

有关详细信息, 请查看客户端上的 M365AHandler。  

检查此注册表项的权限。 请确保本地系统帐户可以访问此密钥, 以便 Configuration Manager 客户端进行设置。 它也可能由冲突的组策略对象引起。 有关详细信息, 请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。  

### <a name="commercial-id-configuration"></a>商业 ID 配置

<!--9, 11, 53-->
Microsoft 使用唯一的商业 ID 将设备中的信息映射到桌面分析工作区。 将 Configuration Manager 与桌面分析集成时, 它会自动查询该 ID 的服务。 Configuration Manager 应自动将此 ID 应用到你面向桌面分析设置的客户端。

如果此检查成功, 则使用商业 ID 正确配置设备。

否则, 它可能会显示以下错误之一:

- 无法将 CommercialId 写入注册表项`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`。 检查权限  

- 无法在注册表项`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`中更新 CommercialId。 检查日志中是否有异常详细信息  

- 提供正确的 CommercialId 值`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

有关详细信息, 请查看客户端上的 M365AHandler。  

检查此注册表项的权限。 请确保本地系统帐户可以访问此密钥, 以便 Configuration Manager 客户端进行设置。 它也可能由冲突的组策略对象引起。 有关详细信息, 请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。  

设备有不同的 ID。 此注册表项由组策略使用。 其优先级高于 Configuration Manager 提供的 ID。  

<a name="bkmk_ViewCommercialID"></a>若要在桌面 Analytics 门户中查看商业 ID, 请使用以下过程:

1. 中转到桌面分析门户, 并在 "全局设置" 组中选择 "**连接的服务**"。  

2. 在 "**连接的服务**" 窗格中, 默认情况下会选择 "**注册设备**" 窗格。 在 "注册设备" 窗格中, "信息" 部分显示你的商业 ID 键。  

![桌面分析门户中商业 ID 的屏幕截图](media/commercial-id.png)

> [!Important]  
> 仅当你无法使用当前**ID 键**时, 才获取它。 如果重新生成商业 ID, 请[用新 ID 重新注册设备](/sccm/desktop-analytics/enroll-devices#device-enrollment)。此过程可能会导致在转换过程中丢失诊断数据。  

### <a name="windows-commercial-data-opt-in"></a>Windows 商业数据选择加入

<!--64-->
此属性特定于运行 Windows 7 或 Windows 8.1 的设备。 它除了 CommercialDataOptIn 值外, 还运行与[Windows 诊断数据选择加入](#windows-diagnostic-data-opt-in)相同的测试。

### <a name="check-device-name-in-diagnostic-data"></a>检查诊断数据中的设备名称

<!--56,58-->
如果此检查成功, 则设备已正确配置为共享设备名称。

否则, 它可能会显示以下错误之一:

- 无法检查是否要将设备名称作为 Windows 诊断数据的一部分发送给 Microsoft。 检查日志中是否有异常详细信息  

- 无法将 AllowDeviceNameInTelemetry 写入注册表项`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`。 检查权限  

有关详细信息, 请查看客户端上的 M365AHandler。  

检查此注册表项的权限。 请确保本地系统帐户可以访问此密钥, 以便 Configuration Manager 客户端进行设置。 它也可能由冲突的组策略对象引起。 有关详细信息, 请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。  

请确保其他策略机制 (如组策略) 未禁用此设置。

### <a name="diagtrack-service-configuration"></a>DiagTrack 服务配置

<!--44,45,50-->
如果此检查成功, 则已在设备上正确配置 DiagTrack 组件。 桌面分析所需的最低版本为 10010586 (10.0.10586)。

否则, 可能会显示以下错误之一:

- 已连接的用户体验和遥测 (diagtrack) 组件已过时。 检查要求  

- 找不到连接的用户体验和遥测 (diagtrack) 组件。 检查要求  

- 启用并启动已连接的用户体验和遥测服务, 将数据发送给 Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

安装最新更新。 有关详细信息, 请参阅[设备更新](/sccm/desktop-analytics/enroll-devices#update-devices)。

请确保设备上的**连接的用户体验和遥测**服务正在运行。

### <a name="diagtrack-version"></a>DiagTrack 版本

此属性显示设备上连接的用户体验和遥测组件的当前版本。 它显示上`%windir%\System32\diagtrack.dll`的文件版本, 不包含小数点。 例如, 文件版本10.0.10586 显示为10010586。

### <a name="sqm-id-retrieval"></a>SQM ID 检索

<!--38-->
此属性主要用于 Windows 7 设备。 以后的操作系统版本可能会将其用作设备的备用标识符。

如果不成功, 可能显示以下错误:

- 无法检索旧设备遥测标识符 (SQM ID)

有关详细信息, 请查看客户端上的 M365AHandler。  

请确保您的环境中没有重复的 Id。 例如, 如果使用未通用化的 OS 映像部署设备。

### <a name="unique-device-identifier-retrieval"></a>唯一的设备标识符检索

<!--54-->
桌面分析将 Microsoft 帐户服务用于更可靠的设备标识。

请确保未禁用**Microsoft 帐户登录助手**服务。 启动类型应为**手动 (触发器启动)** 。

若要禁用最终用户 Microsoft 帐户访问权限, 请使用策略设置, 而不是阻止此终结点。 有关详细信息, 请参阅[企业中的 Microsoft 帐户](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)。

### <a name="windows-diagnostic-data-opt-in"></a>Windows 诊断数据选择加入

<!--8,40,55,62-->
此属性检查 Windows 是否已正确配置为允许诊断数据。 它将检查以下注册表项中的 AllowTelemetry 值:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

检查对这些注册表项的权限。 请确保本地系统帐户可以访问这些密钥, 以便 Configuration Manager 客户端进行设置。 它也可能由冲突的组策略对象引起。 有关详细信息, 请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。  

有关详细信息, 请查看客户端上的 M365AHandler。  



## <a name="see-also"></a>另请参阅

[桌面分析疑难解答](/sccm/desktop-analytics/troubleshooting)
