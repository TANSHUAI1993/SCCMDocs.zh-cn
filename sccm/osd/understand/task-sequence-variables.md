---
title: 任务序列变量引用
titleSuffix: Configuration Manager
description: 了解用于控制和自定义 Configuration Manager 任务序列的变量。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cde62242fc4db99d762d670037aad22bd25d6c00
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456730"
---
# <a name="task-sequence-variables-in-configuration-manager"></a>Configuration Manager 中的任务序列变量

*适用范围：System Center Configuration Manager (Current Branch)*

本文是按字母顺序对所有可用变量的引用。 使用浏览器的查找功能（通常使用 CTRL + F）查找特定变量。 如果变量特定于特定步骤，会对此进行说明。 有关[任务序列步骤](/sccm/osd/understand/task-sequence-steps)的文章包括特定于每个步骤的变量列表。 

有关详细信息，请参阅[使用任务序列变量](/sccm/osd/understand/using-task-sequence-variables)。



## <a name="bkmk_tsvar"></a> 任务序列变量引用


### <a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

 在 Windows PE 启动时，任务序列会在计算机的硬盘驱动器上扫描是否以前已安装操作系统。 Windows 文件夹位置存储在此变量中。 你可以将任务序列配置为从环境中检索该值，并将其用于指定相同的 Windows 文件夹位置进行新的操作系统安装。


### <a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

 在 Windows PE 启动时，任务序列会在计算机的硬盘驱动器上扫描是否以前已安装操作系统。 安装操作系统的硬盘驱动器位置存储在此变量中。 你可以将任务序列配置为从环境中检索该值，并将其用于指定相同的硬盘驱动器位置以供新的操作系统使用。


### <a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

 适用于[捕获用户状态](task-sequence-steps.md#BKMK_CaptureUserState)步骤。

 (input)

 指定包含 USMT 文件的 Configuration Manager 包的包 ID。 此变量是必需的。


### <a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

 适用于[还原用户状态](task-sequence-steps.md#BKMK_RestoreUserState)步骤。

 (input)

 指定包含 USMT 文件的 Configuration Manager 包的包 ID。 此变量是必需的。


### <a name="SMSTSAdvertID"></a> _SMSTSAdvertID

 存储当前运行的任务序列部署的唯一 ID。 它使用与 Configuration Manager 软件分发部署 ID 相同的格式。 如果任务序列从独立的媒体运行，则此变量未定义。

 #### <a name="example"></a>示例
 `ABC20001`


### <a name="SMSTSAssetTag"></a> _SMSTSAssetTag

 适用于[设置动态变量](task-sequence-steps.md#BKMK_SetDynamicVariables)步骤。

 指定计算机的资产标记。


### <a name="SMSTSBootImageID"></a> _SMSTSBootImageID

 如果当前运行的任务序列引用某个启动映像包，此变量会存储启动映像包 ID。 如果任务序列不引用启动映像包，则不会设置此变量。

 #### <a name="example"></a>示例
 `ABC00001`  


### <a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

 当任务序列检测到计算机处于 UEFI 模式时，它会设置此变量。


### <a name="SMSTSClientGUID"></a> _SMSTSClientGUID

 存储 Configuration Manager 客户端 GUID 的值。 如果任务序列从独立的媒体运行，则此变量未设置。

 #### <a name="example"></a>示例
 `0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`


### <a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

 指定当前运行的任务序列步骤的名称。 此变量在任务序列管理器运行每个单独步骤前设置。

 #### <a name="example"></a>示例
 `run command line`


### <a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

 适用于[设置动态变量](task-sequence-steps.md#BKMK_SetDynamicVariables)步骤。

 指定计算机使用的默认网关。


### <a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

 如果当前的任务序列正在按需下载模式下运行，则此变量为 `true`。 按需下载模式是指任务序列管理器仅在必须访问内容时本地下载内容。


### <a name="SMSTSInWinPE"></a> _SMSTSInWinPE

 如果当前的任务序列步骤正在 Windows PE 中运行，则此变量为 `true`。 测试此任务序列变量以确定当前的操作系统环境。


### <a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

 适用于[设置动态变量](task-sequence-steps.md#BKMK_SetDynamicVariables)步骤。

 指定计算机使用的 IP 地址。


### <a name="SMSTSLastActionName"></a> _SMSTSLastActionName
 从版本 1810 开始  

 存储运行的最后一个操作的名称。 此变量与 _SMSTSLastActionRetCode 相关。 任务序列将这些值记录到 smsts.log 文件中。 对任务序列进行故障排除时，此变量十分有用。 当步骤失败时，自定义脚本可以包含步骤名称和返回代码。


### <a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

 存储源自所运行的上一操作的返回代码。 此变量可作为决定下一步是否运行的条件。

 #### <a name="example"></a>示例
 `0`


### <a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

 - 如果最后一个步骤成功，此变量为 `true`。  

 - 如果最后一个步骤失败，此变量为 `false`。  

 - 如果由于该步骤被禁用或相关的条件被评估为 false 而导致任务序列跳过最后一个操作，则不会重置此变量。 它仍保留之前操作的值。  

 
### <a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

 通过以下方法之一指定启动的任务序列：  

 - SMS：Configuration Manager 客户端，例如当用户从软件中心启动它
 - UFD：传统 USB 媒体
 - UFD+FORMAT：较新的 USB 媒体
 - CD：可启动的 CD
 - DVD：可启动的 DVD
 - PXE：使用 PXE 的网络启动
 - HD：硬盘上的预留媒体


### <a name="SMSTSLogPath"></a> _SMSTSLogPath

 存储日志目录的完整路径。 使用此值确定任务序列步骤记录其操作的位置。 如果没有硬盘驱动器可用，则不设置此值。


### <a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

 适用于[设置动态变量](task-sequence-steps.md#BKMK_SetDynamicVariables)步骤。

 指定计算机使用的 MAC 地址。


### <a name="SMSTSMachineName"></a> _SMSTSMachineName

 存储并指定计算机名称。 存储任务序列将用于记录所有状态消息的计算机的名称。 要更改新操作系统中的计算机名称，请使用 [OSDComputerName](#OSDComputerName) 变量。


### <a name="SMSTSMake"></a> _SMSTSMake

 适用于[设置动态变量](task-sequence-steps.md#BKMK_SetDynamicVariables)步骤。

 指定计算机的品牌。


### <a name="SMSTSMDataPath"></a> _SMSTSMDataPath

 指定由 [SMSTSLocalDataDrive](#SMSTSLocalDataDrive) 变量定义的路径。 当在启动任务序列前定义 SMSTSLocalDataDrive 时，例如设置集合变量，启动任务序列后，Configuration Manager 将定义 _SMSTSMDataPath 变量。


### <a name="SMSTSMediaType"></a> _SMSTSMediaType

 指定用于启动安装的媒体类型。 媒体类型示例有启动媒体、完全媒体、PXE 和预暂存媒体。


### <a name="SMSTSModel"></a> _SMSTSModel

 适用于[设置动态变量](task-sequence-steps.md#BKMK_SetDynamicVariables)步骤。

 指定计算机的型号。


### <a name="SMSTSMP"></a> _SMSTSMP

 存储 Configuration Manager 管理点的 URL 或 IP 地址。


### <a name="SMSTSMPPort"></a> _SMSTSMPPort

 存储 Configuration Manager 管理点的端口号。


### <a name="SMSTSOrgName"></a> _SMSTSOrgName

 存储任务序列在进度对话框中显示的品牌标题名称。


### <a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

 适用于[升级操作系统](task-sequence-steps.md#BKMK_UpgradeOS)步骤。

 存储 Windows 安装程序返回的用于指示成功或失败的退出代码值。 此变量可与 `/Compat` 命令行选项结合使用。

 #### <a name="example"></a>示例
 在仅限兼容性扫描完成时，可以根据失败或成功退出代码在后续步骤中执行操作。 成功时，可以启动升级。 或者在环境中设置一个标记来收集硬件清单。 例如，添加文件或设置注册表项。 该标记可以用于创建准备好进行升级或在升级之前需要执行操作的计算机集合。


### <a name="SMSTSPackageID"></a> _SMSTSPackageID

 存储当前运行的任务序列的 ID。 此 ID 使用与 Configuration Manager 包 ID 相同的格式。 

 #### <a name="example"></a>示例
 `HJT00001`


### <a name="SMSTSPackageName"></a> _SMSTSPackageName

 存储当前运行的任务序列的名称。 创建任务序列时，由 Configuration Manager 管理员指定此名称。

 #### <a name="example"></a>示例
 `Deploy Windows 10 task sequence`


### <a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

 如果当前任务序列在从分发点运行模式下运行，设置为 `true`。 此模式意味着任务序列管理器将从分发点获取所需的包共享。


### <a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

 适用于[设置动态变量](task-sequence-steps.md#BKMK_SetDynamicVariables)步骤。

 指定计算机的序列号。


### <a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

 指定 Windows 安装程序是否在就地升级期间执行回滚操作。 变量值可以是 `true` 或 `false`。


### <a name="SMSTSSiteCode"></a> _SMSTSSiteCode

 存储 Configuration Manager 站点的站点代码。

 #### <a name="example"></a>示例
 `ABC`


### <a name="SMSTSTimezone"></a> _SMSTSTimezone

 此变量用以下格式存储时区信息： 

 ```
 Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName
 ```

 #### <a name="example"></a>示例
 对于时区东部时间（美国和加拿大）： 

 ```
 300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time
 ```


### <a name="SMSTSType"></a> _SMSTSType

 指定当前运行的任务序列的类型。 可以具有以下一个值：  

 - 1：一般任务序列
 - 2：OS 部署任务序列


### <a name="SMSTSUseCRL"></a> _SMSTSUseCRL

 此变量指定在使用 HTTPS 与管理点通信时，任务序列是否使用证书吊销列表 (CRL)。


### <a name="SMSTSUserStarted"></a> _SMSTSUserStarted

 指定用户是否启动了任务序列。 仅当任务序列从软件中心启动时设置此变量。 例如，如果 [_SMSTSLaunchMode](#SMSTSLaunchMode) 设置为 `SMS`。 

 此变量可以有下列值：  

 - `true`：指示任务序列通过用户从软件中心手动启动。  

 - `false`：指示任务序列由 Configuration Manager 计划程序自动启动。


### <a name="SMSTSUseSSL"></a> _SMSTSUseSSL

 指定任务序列是否使用 SSL 与 Configuration Manager 管理点通信。 如果为 HTTPS 配置站点系统，将值设置为 `true`。


### <a name="SMSTSUUID"></a> _SMSTSUUID

 适用于[设置动态变量](task-sequence-steps.md#BKMK_SetDynamicVariables)步骤。

 指定计算机的 UUID。


### <a name="SMSTSWTG"></a> _SMSTSWTG

 指定计算机是否作为 Windows To Go 设备运行。


### <a name="TSAppInstallStatus"></a> _TSAppInstallStatus

 任务序列在[安装应用程序](task-sequence-steps.md#BKMK_InstallApplication)步骤中随应用程序的安装状态一起设置此变量。 它设置为下列值之一：  

 - 未定义：“安装应用程序”步骤未运行。  

 - **错误**：在至少一个应用程序由于“安装应用程序”步骤中出错而失败时设置。  

 - 警告：在“安装应用程序”步骤中未发生任何错误。 由于不满足要求，一个或多个应用程序或必需的依赖项未安装。  

 - **成功**：在“安装应用程序”步骤中未检测到任何错误或警告。  


### <a name="OSDAdapter"></a> OSDAdapter

 适用于[应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步骤。

 (input)

 此任务序列变量是一个数组变量。 数组中的每个元素都代表计算机上单个网络适配器的设置。 通过将数组变量名称与基于零的网络适配器下标及属性名称组合，访问每个适配器的设置。

 如果应用网络设置步骤配置多个网络适配器，则使用变量名称中的下标 1定义第二个网络适配器的属性。 例如：OSDAdapter1EnableDHCP、OSDAdapter1IPAddressList 和 OSDAdapter1DNSDomain。

 以下变量名称可用于为将由此步骤配置的第一个网络适配器定义属性：

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP
 此设置是必需的。 可能的值包括 `True` 或 `False`。 例如：

 `true`：设置为“true”将为适配器启用动态主机配置协议 (DHCP)

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList
 以逗号分隔的适配器 IP 地址列表。 除非“EnableDHCP”设置为 `false`，否则将忽略此属性。 此设置是必需的。

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask
 以逗号分隔的子网掩码列表。 除非“EnableDHCP”设置为 `false`，否则将忽略此属性。 此设置是必需的。

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways
 以逗号分隔的 IP 网关地址列表。 除非“EnableDHCP”设置为 `false`，否则将忽略此属性。 此设置是必需的。

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain
 适配器的域名系统 (DNS) 域。

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList
 以逗号分隔的适配器 DNS 服务器列表。 此设置是必需的。

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration
 设置为 `true` 将在 DNS 中为适配器注册 IP 地址。

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration
 设置为 `true` 将根据计算机的完整 DNS 名称在 DNS 中为适配器注册 IP 地址。

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering
 设置为 `true` 将在适配器上启用 IP 协议筛选。

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList
 以逗号分隔的协议列表，这些协议被允许在 IP 的上层运行。 如果“EnableIPProtocolFiltering”设置为 `false`，将忽略此属性。

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering
 设置为 `true` 将为适配器启用 TCP 端口筛选。

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList
 以逗号分隔的端口列表，这些端口将被授予对 TCP 的访问权限。 如果“EnableTCPFiltering”设置为 `false`，将忽略此属性。

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions
 TCP/IP 上层的 NetBIOS 选项。 可能的值如下：  

 - `0`：使用 DHCP 服务器中的 NetBIOS 设置  
 - `1`：启用 TCP/IP 上层的 NetBIOS  
 - `2`：禁用 TCP/IP 上层的 NetBIOS  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS
 设置为 `true` 以使用 WINS 进行名称解析。

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList
 以逗号分隔的 WINS 服务器 IP 地址列表。 除非“EnableWINS”设置为 `true`，否则将忽略此属性。

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress
 MAC 地址，用于匹配物理网络适配器的设置。

#### <a name="osdadapter0name"></a>OSDAdapter0Name
 显示在网络连接控制面板程序中的网络连接的名称。 该名称的长度介于 0 到 255 个字符之间。

#### <a name="osdadapter0index"></a>OSDAdapter0Index
 设置数组中网络适配器设置的下标。

#### <a name="example"></a>示例
 - OSDAdapterCount = `1`  
 - OSDAdapter0EnableDHCP = `FALSE`  
 - OSDAdapter0IPAddressList = `192.168.0.40`  
 - OSDAdapter0SubnetMask = `255.255.255.0`  
 - OSDAdapter0Gateways = `192.168.0.1`  
 - OSDAdapter0DNSSuffix = `contoso.com`  


### <a name="OSDAdapterCount"></a> OSDAdapterCount

 适用于[应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步骤。

 (input)

 指定目标计算机上安装的网络适配器的数目。 在设置 OSDAdapterCount 值时，还需为每个适配器的所有配置选项设置值。 

 例如，如果为首个适配器设置 OSDAdapter0TCPIPNetbiosOptions 值，那么也必须设置该适配器的所有值。

 如果未指定此值，任务序列将忽略所有 OSDAdapter 值。


### <a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

 适用于[应用驱动程序包](task-sequence-steps.md#BKMK_ApplyDriverPackage)步骤。

 (input)

 指定要从驱动程序包中进行安装的大容量存储驱动程序的内容 ID。 如果没有指定此变量，则不安装大容量存储驱动程序。


### <a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

 适用于[应用驱动程序包](task-sequence-steps.md#BKMK_ApplyDriverPackage)步骤。

 (input)

 指定无论是否安装大容量存储设备驱动程序，此变量都必须为 scsi。

 如果设置了 [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID)，则需要此变量。


### <a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

 适用于[应用驱动程序包](task-sequence-steps.md#BKMK_ApplyDriverPackage)步骤。

 (input)

 指定要安装的大容量存储设备驱动程序的启动关键 ID。 此 ID 列在设备驱动程序 txtsetup.oem 文件的 scsi 部分中。

 如果设置了 [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID)，则需要此变量。

### <a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

 适用于[应用驱动程序包](task-sequence-steps.md#BKMK_ApplyDriverPackage)步骤。

 (input)

 指定要安装的大容量存储驱动程序的 INF 文件。

 如果设置了 [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID)，则需要此变量。


### <a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

 适用于[自动应用驱动程序](task-sequence-steps.md#BKMK_AutoApplyDrivers)步骤。

 (input)

 如果驱动程序目录中有多个设备驱动程序与硬件设备兼容，此变量确定步骤的操作。 

 #### <a name="valid-values"></a>有效值
 - `true`（默认值）：仅安装最适合的设备驱动程序  

 - `false`：安装所有兼容的设备驱动程序并且 Windows 会选择使用最适合的驱动程序  


### <a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

 适用于[自动应用驱动程序](task-sequence-steps.md#BKMK_AutoApplyDrivers)步骤。

 (input)

 驱动程序目录类别唯一 ID 的以逗号分隔的列表。 “自动应用驱动程序”步骤只考虑至少一个指定类别中的驱动程序。 此值是可选的，默认情况下不设置。 可以通过枚举站点上的 SMS_CategoryInstance 对象列表来获取可用的类别 ID。


### <a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

 适用于[启用 BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker) 步骤。

 (input)

 “启用 BitLocker”步骤使用指定的值作为恢复密码，而不是生成随机恢复密码。 此值必须是有效的数字 BitLocker 恢复密码。


### <a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

 适用于[启用 BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker) 步骤。

 (input)

 “启用 BitLocker”步骤使用受信任的平台模块 (TPM) 作为启动密钥，而不是为密钥管理选项“仅 USB 上的启动密钥”生成随机启动密钥。 此值必须是一个有效的 256 位 Base-64 编码的 BitLocker 启动密钥。


### <a name="OSDCaptureAccount"></a> OSDCaptureAccount

 适用于[捕获 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步骤。

 (input)

 指定在网络共享 ([OSDCaptureDestination](#OSDCaptureDestination)) 上有权限存储所捕获映像的 Windows 帐户名称。 此外指定 [OSDCaptureAccountPassword](#OSDCaptureAccountPassword)。

 有关此捕获 OS 映像帐户的详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#capture-operating-system-image-account)。


### <a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

 适用于[捕获 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步骤。

 (input)

 指定用于将捕获映像存储到网络共享 ([OSDCaptureDestination](#OSDCaptureDestination)) 的 Windows 帐户 ([OSDCaptureAccount](#OSDCaptureAccount)) 的密码。


### <a name="OSDCaptureDestination"></a> OSDCaptureDestination

 适用于[捕获 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步骤。

 (input)

 指定任务序列在其中保存捕获的 OS 映像的位置。 目录名称的最大长度为 255 个字符。 如果网络共享要求进行身份验证，请指定 [OSDCaptureAccount](#OSDCaptureAccount) 和 [OSDCaptureAccountPassword](#OSDCaptureAccountPassword) 变量。


### <a name="OSDComputerName-input"></a> OSDComputerName (input)

 适用于[应用 Windows 设置](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步骤。

 指定目标计算机的名称。

 #### <a name="example"></a>示例
 `%_SMSTSMachineName%`（默认值）


### <a name="OSDComputerName-output"></a> OSDComputerName (output)

 适用于[捕获 Windows 设置](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步骤。

 设置为计算机的 NetBIOS 名称。 仅当 [OSDMigrateComputerName](#OSDMigrateComputerName) 变量设置为 `true` 时设置该值。


### <a name="OSDConfigFileName"></a> OSDConfigFileName

 适用于[应用 OS 映像](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)步骤。

 (input)

 指定与操作系统部署映像包关联的操作系统部署答案文件的文件名。  


### <a name="OSDDataImageIndex"></a> OSDDataImageIndex

 适用于[应用数据映像](task-sequence-steps.md#BKMK_ApplyDataImage)步骤。

 (input)

 指定应用于目标计算机的映像的索引值。


### <a name="OSDDiskIndex"></a> OSDDiskIndex

 适用于[格式化磁盘并分区](task-sequence-steps.md#BKMK_FormatandPartitionDisk)步骤。

 (input)

 指定要分区的物理磁盘编号。


### <a name="OSDDNSDomain"></a> OSDDNSDomain

 适用于[应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步骤。

 (input)

 指定目标计算机使用的主 DNS 服务器。


### <a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

 适用于[应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步骤。

 (input)

 指定目标计算机的 DNS 搜索顺序。


### <a name="OSDDomainName"></a> OSDDomainName

 适用于[应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步骤。

 (input)

 指定目标计算机加入的 Active Directory 域的名称。 指定的值必须是有效的 Active Directory 域服务的域名。


### <a name="OSDDomainOUName"></a> OSDDomainOUName

 适用于[应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步骤。

 (input)

 指定目标计算机加入的组织单位 (OU) 的 RFC 1779 格式名称。 如果指定了值，该值必须包含完整路径。

 #### <a name="example"></a>示例
 `LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`


### <a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand
 <!--1358493--> 从版本 1806 开始  
 适用于[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)步骤。

 (input)

 若要禁止显示或记录潜在的敏感数据，请将此变量设置为 `TRUE`。 在[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)任务序列步骤过程中，此变量将程序名称隐藏在 smsts.log 中。   


### <a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

 适用于[应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步骤。

 (input)

 指定是否启用 TCP/IP 筛选。

 #### <a name="valid-values"></a>有效值
 - `true`  
 - `false`（默认值）  


### <a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

 适用于[格式化磁盘并分区](task-sequence-steps.md#BKMK_FormatandPartitionDisk)步骤。

 (input)

 指定是否在 GPT 硬盘上创建 EFI 分区。 基于 EFI 的计算机使用此分区作为启动磁盘。

 #### <a name="valid-values"></a>有效值
 - `true`  
 - `false`（默认值）


### <a name="OSDImageCreator"></a> OSDImageCreator

 适用于[捕获 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步骤。

 (input)

 创建映像的用户的名称（可选）。 此名称存储在 WIM 文件中。 此用户名称的最大长度为 255 个字符。


### <a name="OSDImageDescription"></a> OSDImageDescription

 适用于[捕获 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步骤。

 (input)

 用户定义的、捕获的 OS 映像的可选描述。 此描述存储在 WIM 文件中。 此描述的最大长度为 255 个字符。


### <a name="OSDImageIndex"></a> OSDImageIndex

 适用于[应用 OS 映像](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)步骤。

 (input)

 指定应用于目标计算机上的 WIM 文件的映像索引值。


### <a name="OSDImageVersion"></a> OSDImageVersion

 适用于[捕获 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步骤。

 (input)

 向捕获的 OS 映像分配的用户定义的版本号（可选）。 该版本号存储在 WIM 文件中。 此值可以为字母数字字符的任意组合（最大长度为 32 个字符）。


### <a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions
<!--516679/2840016--> 从版本 1806 开始  
 适用于[应用驱动程序包](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage)步骤。

 (input)

 指定在应用驱动程序包时添加到 DISM 命令行的其他选项。 任务序列不验证命令行选项。 

 要使用此变量，在“应用驱动程序包”步骤上，启用设置“使用递归选项通过运行 DISM 来安装驱动程序包”。 

 有关详细信息，请参阅 [Windows 10 DISM 命令行选项](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options)。


### <a name="OSDJoinAccount"></a> OSDJoinAccount

 适用于以下步骤：  
 - [应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)   
 - [加入域或工作组](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  


 (input)

 指定用于将目标计算机添加到域的域用户帐户。 此变量是加入域时必需的变量。

 有关任务序列域加入帐户的详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account)。


### <a name="OSDJoinDomainName"></a> OSDJoinDomainName

 适用于[加入域或工作组](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)步骤。

 (input)

 指定目标计算机加入的 Active Directory 域的名称。 域名长度必须介于 1 到 255 个字符之间。


### <a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

 适用于[加入域或工作组](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)步骤。

 (input)

 指定目标计算机加入的组织单位 (OU) 的 RFC 1779 格式名称。 如果指定了值，该值必须包含完整路径。 OU 名称的长度必须介于 0 到 32,767 个字符之间。 如果 [OSDJoinType](#OSDJoinType) 变量设置为 `1`（加入工作组），则不设置此值。

 #### <a name="example"></a>示例
 `LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

  
### <a name="OSDJoinPassword"></a> OSDJoinPassword

 适用于以下步骤：  
 - [应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
 - [加入域或工作组](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  


 (input)

 指定目标计算机加入 Active Directory 域时使用的 [OSDJoinAccount](#OSDJoinAccount) 密码。 如果任务序列环境不包括此变量，Windows 安装程序会尝试使用空密码。 如果变量 [OSDJoinType](#OSDJoinType) 设置为 `0`（加入域），则此值为必需。


### <a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

 适用于[加入域或工作组](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)步骤。

 (input)

 指定在目标计算机加入域或工作组后是否跳过重新启动。

 #### <a name="valid-values"></a>有效值
 - `true`  
 - `false`  


### <a name="OSDJoinType"></a> OSDJoinType

 适用于[加入域或工作组](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)步骤。

 (input)

 指定目标计算机是否加入 Windows 域或工作组。 

 #### <a name="valid-values"></a>有效值
 - `0`：将目标计算机加入到 Windows 域中  
 - `1`：将目标计算机加入到工作组中  


### <a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

 适用于[加入域或工作组](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)步骤。

 (input)

 指定目标计算机加入的工作组的名称。 工作组的名称长度必须介于 1 到 32 个字符之间。


### <a name="OSDKeepActivation"></a> OSDKeepActivation

 适用于[准备 Windows 以便捕获](task-sequence-steps.md#BKMK_PrepareWindowsforCapture)步骤。

 (input)

 指定 sysprep 是否重置产品激活标志。

 #### <a name="valid-values"></a>有效值
 - `true`
 - `false`（默认值）


### <a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

 适用于[应用 Windows 设置](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步骤。

 (input)

 指定本地管理员帐户密码。 如果启用选项“随机生成本地管理员密码并在所有支持的平台上禁用帐户”，则该步骤将忽略此变量。 指定的值字符数必须介于 1 和 255 之间。


### <a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

 适用于[捕获网络设置](task-sequence-steps.md#BKMK_CaptureNetworkSettings)步骤。

 (input)

 指定任务序列是否捕获网络适配器信息。 此信息包括 TCP/IP、DNS 和 WINS 的配置设置。

 #### <a name="valid-values"></a>有效值
 - `true`（默认值）
 - `false`


### <a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

 适用于[捕获用户状态](task-sequence-steps.md#BKMK_CaptureUserState)步骤。

 (input)

 指定任务序列用于捕获用户状态的其他用户状态迁移工具 (USMT) 命令行选项。 此步骤在任务序列编辑器中不公开这些设置。 将这些选项指定为一个字符串，任务序列将该字符串追加到为 ScanState 自动生成的 USMT 命令行。

 在运行任务序列之前，使用此任务序列变量指定的 USMT 选项未通过精确度验证。

 有关可用选项的详细信息，请参阅 [ScanState 语法](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax)。


### <a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

 适用于[还原用户状态](task-sequence-steps.md#BKMK_RestoreUserState)步骤。

 (input)

 指定任务序列在还原用户状态时使用的其他用户状态迁移工具 (USMT) 命令行选项。 将其他选项指定为一个字符串，任务序列将该字符串追加到为 LoadState 自动生成的 USMT 命令行。 

 在运行任务序列之前，使用此任务序列变量指定的 USMT 选项未通过精确度验证。

 有关可用选项的详细信息，请参阅 [LoadState 语法](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax)。


### <a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

 适用于[捕获 Windows 设置](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步骤。

 (input)

 指定是否迁移计算机名称。

 #### <a name="valid-values"></a>有效值
 - `true`（默认值）。 将 [OSDComputerName (output)](#OSDComputerName-output) 变量设置为计算机的 NetBIOS 名称。  
 - `false`   


### <a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

 适用于[捕获用户状态](task-sequence-steps.md#BKMK_CaptureUserState)步骤。

 (input)

 指定用于控制对用户配置文件的捕获的配置文件。 仅当 [OSDMigrateMode](#OSDMigrateMode) 设置为 `Advanced` 时，才使用此变量。 设置此逗号分隔的列表值，以执行自定义的用户配置文件迁移。

 #### <a name="example"></a>示例
 `miguser.xml,migsys.xml,migapps.xml`  


### <a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

 适用于[捕获用户状态](task-sequence-steps.md#BKMK_CaptureUserState)步骤。

 (input)

 如果 USMT 无法捕获某些文件，此变量允许继续进行用户状态捕获。 

 #### <a name="valid-values"></a>有效值
 - `true`（默认值）  
 - `false`   


### <a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

 适用于[还原用户状态](task-sequence-steps.md#BKMK_RestoreUserState)步骤。

 (input)

 继续执行过程，即使 USMT 无法还原某些文件。

 #### <a name="valid-values"></a>有效值
 - `true`（默认值）  
 - `false`  


### <a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

 适用于以下步骤：  
 - [捕获用户状态](task-sequence-steps.md#BKMK_CaptureUserState)  
 - [还原用户状态](task-sequence-steps.md#BKMK_RestoreUserState)  


 (input)

 启用 USMT 的详细日志记录。 该步骤需要此值。

 #### <a name="valid-values"></a>有效值
 - `true`  
 - `false`（默认值）  


### <a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

 适用于[还原用户状态](task-sequence-steps.md#BKMK_RestoreUserState)步骤。

 (input)

 指定是否还原本地计算机帐户。

 #### <a name="valid-values"></a>有效值
 - `true`  
 - `false`（默认值）  


### <a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

 适用于[还原用户状态](task-sequence-steps.md#BKMK_RestoreUserState)步骤。

 (input)

 如果 [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) 变量为 `true`，此变量必须包含分配给所有已迁移的本地帐户的密码。 USMT 将相同的密码分配给所有已迁移的本地帐户。 将此密码视为临时密码，稍后使用其他方法进行更改。


### <a name="OSDMigrateMode"></a> OSDMigrateMode

 适用于[捕获用户状态](task-sequence-steps.md#BKMK_CaptureUserState)步骤。

 (input)

 允许自定义 USMT 捕获的文件。 

 #### <a name="valid-values"></a>有效值
 - `Simple`：任务序列只会使用标准 USMT 配置文件  

 - `Advanced`：任务序列变量 [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) 会指定 USMT 使用的配置文件  


### <a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

 适用于[捕获网络设置](task-sequence-steps.md#BKMK_CaptureNetworkSettings)步骤。

 (input)

 指定任务序列是否迁移工作组或域成员身份信息。

 #### <a name="valid-values"></a>有效值
 - `true`（默认值）
 - `false`


### <a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

 适用于[捕获 Windows 设置](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步骤。

 (input)

 指定该步骤是否迁移用户和组织信息。

 #### <a name="valid-values"></a>有效值
 - `true`（默认值）。 将 [OSDRegisteredOrgName (output)](#OSDRegisteredOrgName-output) 变量设置为计算机的注册组织名称。  
 - `false`   


### <a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

 适用于[捕获用户状态](task-sequence-steps.md#BKMK_CaptureUserState)步骤。

 (input)

 指定是否捕获加密文件。

 #### <a name="valid-values"></a>有效值
 - `true`  
 - `false`（默认值）  


### <a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

 适用于[捕获 Windows 设置](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步骤。

 (input)

 指定是否迁移计算机名称时区。

 #### <a name="valid-values"></a>有效值
 - `true`（默认值）。 将变量 [OSDTimeZone (output)](#OSDTimeZone-output) 设置为计算机的时区。  
 - `false`   


### <a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

 适用于[应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步骤。

 (input)

 指定目标计算机是否加入 Active Directory 域或工作组。

 #### <a name="value-values"></a>“值”的值
 - `0`：加入 Active Directory 域  
 - `1`：加入工作组


### <a name="OSDPartitions"></a> OSDPartitions

 适用于[格式化磁盘并分区](task-sequence-steps.md#BKMK_FormatandPartitionDisk)步骤。

 (input)

 此任务序列变量是分区设置的一个数组变量。 数组中的每个元素都代表硬盘上单个分区的设置。 通过将数组变量名称与基于零的磁盘分区号及属性名称组合，可以访问为每个分区定义的设置。

以下变量名称可用于为此步骤在硬盘上创建的第一个分区定义属性：

 #### <a name="osdpartitions0type"></a>OSDPartitions0Type
 指定分区类型。 此属性为必需。 有效值为 `Primary`、`Extended`、`Logical` 和 `Hidden`。

 #### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem
 指定格式化分区时使用的文件系统类型。 此属性为可选。 如果不指定文件系统，此步骤不会格式化分区。 有效值为 `FAT32` 和 `NTFS`。

 #### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable
 指定分区是否可引导。 此属性为必需。 如果 MBR 磁盘的该值设置为 `TRUE`，则此步骤将该分区标记为活动分区。

 #### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat
 指定使用的格式类型。 此属性为必需。 如果此值设置为 `TRUE`，此步骤执行快速格式化。 否则，该步骤执行完全格式化。

 #### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName
 指定格式化时分配给该卷的名称。 此属性为可选。

 #### <a name="osdpartitions0size"></a>OSDPartitions0Size
 指定分区的大小。 此属性为可选。 如果未指定此属性，将使用所有剩余可用空间来创建分区。 单位由 **OSDPartitions0SizeUnits** 变量指定。

 #### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits
 该步骤使用这些单位来解释 OSDPartitions0Size 变量。 此属性为可选。 有效值为 `MB`（默认值）、`GB` 和 `Percent`。

 #### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable
 此步骤创建分区后，分区始终使用 Windows PE 中的下一可用驱动器号。 使用此可选属性指定另一个任务序列变量的名称。 该步骤使用此变量保存新的驱动器号，供将来参考。

 如果使用此任务序列步骤定义多个分区，可使用变量名称中的下标 1 来定义第二个分区的属性。 例如：OSDPartitions1Type、OSDPartitions1FileSystem、OSDPartitions1Bootable、OSDPartitions1QuickFormat 和 OSDPartitions1VolumeName。


### <a name="OSDPartitionStyle"></a> OSDPartitionStyle

 适用于[格式化磁盘并分区](task-sequence-steps.md#BKMK_FormatandPartitionDisk)步骤。

 (input)

 指定对磁盘进行分区时使用的分区类型。 

 #### <a name="valid-values"></a>有效值
 - `GPT`：使用 GUID 分区表形式
 - `MBR`：使用主启动记录分区形式


### <a name="OSDProductKey"></a> OSDProductKey

 适用于[应用 Windows 设置](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步骤。

 (input)

 指定 Windows 产品密钥。 指定的值字符数必须介于 1 和 255 之间。


### <a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

 适用于[应用 Windows 设置](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步骤。

 (input)

 指定在新操作系统中为本地管理员帐户随机生成的密码。 

 #### <a name="valid-values"></a>有效值
 - `true`（默认值）：Windows 安装程序将在目标计算机上禁用本地管理员帐户  

 - `false`：Windows 安装程序将在目标计算机上启用本地管理员帐户，并将帐户密码设置为值 [OSDLocalAdminPassword](#OSDLocalAdminPassword)  


### <a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (input)

 适用于[应用 Windows 设置](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步骤。

 指定新操作系统中的默认注册组织名称。 指定的值字符数必须介于 1 和 255 之间。


### <a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (output)

 适用于[捕获 Windows 设置](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步骤。

 设置为计算机的注册组织名称。 仅当 [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) 变量被设置为 `true` 时，才设置该值。


### <a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

 适用于[应用 Windows 设置](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步骤。

 (input)

 指定新操作系统中的默认注册用户名。 指定的值字符数必须介于 1 和 255 之间。


### <a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

 适用于[应用 Windows 设置](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步骤。

 (input)

 指定允许的最大连接数。 指定的连接数必须介于 5 和 9999 之间。


### <a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

 适用于[应用 Windows 设置](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步骤。

 (input)

 指定使用的 Windows Server 许可证模式。

 #### <a name="valid-values"></a>有效值
 - `PerSeat`
 - `PerServer`


### <a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

 适用于[升级操作系统](task-sequence-steps.md#BKMK_UpgradeOS)步骤。

 (input)

 指定在 Windows 10 升级过程中添加到 Windows 安装程序的其他命令行选项。 任务序列不验证命令行选项。 

 有关详细信息，请参阅 [Windows 安装程序命令行选项](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)。


### <a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

 适用于[请求状态存储](task-sequence-steps.md#BKMK_RequestStateStore)步骤。

 (input)

 当计算机帐户无法连接到状态迁移点时，此变量指定任务序列步骤是否应回退到使用网络访问帐户 (NAA)。 

 有关网络访问帐户的详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#network-access-account)。

 #### <a name="valid-values"></a>有效值
 - `true`  
 - `false`（默认值）  


### <a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

 适用于[请求状态存储](task-sequence-steps.md#BKMK_RequestStateStore)步骤。

 (input)

 指定在步骤失败前，任务列表步骤尝试查找状态迁移点的次数。 指定的计数必须介于 0 和 600 之间。


### <a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

 适用于[请求状态存储](task-sequence-steps.md#BKMK_RequestStateStore)步骤。

 (input)

 指定任务序列步骤在重新尝试之间等待的秒数。 秒数最多可为 30 个字符。


### <a name="OSDStateStorePath"></a> OSDStateStorePath

 适用于以下步骤：  
 - [捕获用户状态](task-sequence-steps.md#BKMK_CaptureUserState)  
 - [发布状态存储](task-sequence-steps.md#BKMK_ReleaseStateStore)  
 - [请求状态存储](task-sequence-steps.md#BKMK_RequestStateStore)  
 - [还原用户状态](task-sequence-steps.md#BKMK_RestoreUserState)  


 (input)

 任务序列保存或还原用户状态的文件夹的网络共享或本地路径名称。 无默认值。


### <a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

 适用于[应用 OS 映像](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)步骤。

 (output)

 指定在应用映像后包含操作系统文件的分区的驱动器号。


### <a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (input)

 适用于[捕获 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步骤。

 指定引用计算机上已安装操作系统的 Windows 目录的路径。 任务序列将验证它是由 Configuration Manager 捕获的受支持的操作系统。


### <a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (output)

 适用于[准备 Windows 以便捕获](task-sequence-steps.md#BKMK_PrepareWindowsforCapture)步骤。

 指定引用计算机上已安装操作系统的 Windows 目录的路径。 任务序列将验证它是由 Configuration Manager 捕获的受支持的操作系统。


### <a name="OSDTimeZone-input"></a> OSDTimeZone (input)

 适用于[应用 Windows 设置](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步骤。

 指定在新操作系统中使用的默认时区设置。


### <a name="OSDTimeZone-output"></a> OSDTimeZone (output)

 适用于[捕获 Windows 设置](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步骤。

 设置为计算机的时区。 仅当 [OSDMigrateTimeZone](#OSDMigrateTimeZone) 变量设置为 `true` 时，才设置该值。


### <a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

 适用于[应用数据映像](task-sequence-steps.md#BKMK_ApplyDataImage)步骤。

 (input)

 指定是否删除位于目标分区上的文件。

 #### <a name="valid-values"></a>有效值
 - `true`（默认值）
 - `false`


### <a name="OSDWorkgroupName"></a> OSDWorkgroupName

 适用于[应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步骤。

 (input)

 指定目标计算机加入的工作组的名称。

 指定此变量或 [OSDDomainName](#OSDDomainName) 变量。 工作组名称最多可使用 32 个字符。 


### <a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

 适用于[安装 Windows 和 ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) 步骤。

 (input)

 指定在安装 Configuration Manager 客户端时任务序列所使用的客户端安装属性。

 有关详细信息，请参阅[关于客户端安装参数和属性](/sccm/core/clients/deploy/about-client-installation-properties)。


### <a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

 适用于[连接到网络文件夹](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)步骤。

 (input)

 指定用于连接到 [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath) 中的网络共享的用户帐户。 使用 [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword) 值指定帐户密码。

 有关任务序列网络文件夹连接帐户的详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-network-folder-connection-account)。


### <a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

 适用于[连接到网络文件夹](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)步骤。

 (input)

 指定要连接的网络驱动器号。 此值是可选的。 如果不指定此值，则网络连接不会映射到某个驱动器号。 如果指定此值，该值必须在 D 到 Z 范围内。不能使用 X，它是在 Windows PE 阶段由 Windows PE 使用的驱动器号。

 #### <a name="examples"></a>示例
 - `D:`  
 - `E:`  


### <a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

 适用于[连接到网络文件夹](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)步骤。

 (input)

 指定用于连接到 [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath) 中的网络共享的 [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) 密码。 


### <a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

 适用于[连接到网络文件夹](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)步骤。

 (input)

 指定连接的网络路径。 如果需要将此路径映射到驱动器号，使用 [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter) 值。

 #### <a name="example"></a>示例
 `\\server\share`


### <a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

 适用于[安装软件更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)步骤。

 (input)

 指定是否安装所有更新或仅安装必备更新。

 #### <a name="valid-values"></a>有效值
 - `All`  
 - `Mandatory`  


### <a name="SMSRebootMessage"></a> SMSRebootMessage

 适用于[重新启动计算机](task-sequence-steps.md#BKMK_RestartComputer)步骤。

 (input)

 指定重新启动计算机之前要向用户显示的消息。 如果未设置此变量，则显示默认消息文本。 指定的消息不能超过 512 个字符。

 #### <a name="example"></a>示例
 `Save your work before the computer restarts.`  


### <a name="SMSRebootTimeout"></a> SMSRebootTimeout

 适用于[重新启动计算机](task-sequence-steps.md#BKMK_RestartComputer)步骤。

 (input)

 指定计算机重新启动之前向用户显示警告的秒数。 

 #### <a name="examples"></a>示例
 - `0`（默认值）：不显示重新启动消息  
 - `60`：显示一分钟的警告  


### <a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

 客户端自上次尝试（未返回策略）下载策略到再次尝试之前所等待的秒数。 默认情况下，客户端将等待 0 秒，然后再重试。 

 可以使用媒体或 PXE 中的预启动命令来设置此变量。


### <a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

 客户端在初次尝试下载策略而未找到策略之后再次进行下载尝试的次数。 默认情况下，客户端重新尝试 0 次。

 可以使用媒体或 PXE 中的预启动命令来设置此变量。


### <a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

 指定任务序列如何将用户与目标计算机关联。 将该变量设置为以下值之一：  

 - 自动：当任务序列将操作系统部署到目标计算机时，它会在指定的用户和目标计算机之间创建关系。  

 - 挂起：任务序列创建指定的用户和目标计算机之间的关系。 管理员必须批准该关系才能对其进行设置。  

 - 禁用：当任务序列部署操作系统时，它不会将用户与目标计算机关联。


### <a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry
 <!--512358--> 在断开连接的应用场景中，任务序列引擎重复尝试将状态消息发送到管理点。 在这种情况下，此行为会导致在任务序列处理过程中的延迟。 

 从版本 1802 开始，将此变量设置为 `true` 后，任务序列引擎将不会尝试在第一次消息发送失败之后重新发送状态消息。 该第一次尝试包含多次重试。

 重启任务序列时，此变量的值仍然存在。 但任务序列会尝试发送初始状态消息。 该第一次尝试包含多次重试。 如果成功，任务序列会继续发送状态，不会考虑此变量的值。 如果状态发送失败，任务序列将使用此变量的值。

 > [!NOTE]  
 > [任务序列状态报告](/sccm/core/servers/manage/list-of-reports#task-sequence---deployment-status)依赖这些状态消息，以显示进度、历史记录和每个步骤的详细信息。


### <a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

 适用于[运行命令行](task-sequence-steps.md#BKMK_RunCommandLine)步骤。

 (input)

 默认在 64 位操作系统上，任务序列使用 WOW64 文件系统重定向程序在命令行查找并运行程序。 此行为允许使用命令查找 32 位版本的操作系统程序和 DLL。 将此变量设置为 `true` 可禁用 WOW64 文件系统重定向程序。 此命令查找本机 64 位版本的操作系统程序和 DLL。 在 32 位操作系统上运行时，此变量没有任何作用。


### <a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

 此变量包含外部程序下载程序的中止代码值。 此程序在 [SMSTSDownloadProgram](#SMSTSDownloadProgram) 变量中指定。 如果程序返回的错误代码等于 SMSTSDownloadAbortCode 变量的值，则内容下载失败，且未尝试其他下载方法。


### <a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

 使用此变量来指定替换内容提供程序 (ACP)。 ACP 是用于下载内容的下载程序。 任务序列使用 ACP，而不是默认的 Configuration Manager 下载程序。 作为内容下载过程的一部分，任务序列会检查此变量。 如果已指定，则任务序列会运行程序来下载内容。


### <a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

 Configuration Manager 尝试从分发点下载内容的次数。 默认情况下，客户端重新尝试 2 次。


### <a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

 Configuration Manager 重新尝试从分发点下载内容前等待的秒数。 默认情况下，客户端将等待 15 秒，然后再重试。


### <a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

 适用于[自动应用驱动程序](task-sequence-steps.md#BKMK_AutoApplyDrivers)步骤。

 请求驱动程序目录时，此变量用于指定任务序列等待 HTTP 服务器连接的秒数。 如果连接时间超过超时设定值，任务序列会取消该请求。 默认情况下，超时时间设置为 60 秒。


### <a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

 适用于[自动应用驱动程序](task-sequence-steps.md#BKMK_AutoApplyDrivers)步骤。

 请求驱动程序目录时，此变量用于指定任务序列等待响应的秒数。 如果连接时间超过超时设定值，任务序列会取消该请求。 默认情况下，超时时间设置为 480 秒。


### <a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

 适用于[自动应用驱动程序](task-sequence-steps.md#BKMK_AutoApplyDrivers)步骤。

 请求驱动程序目录时，此变量用于指定任务序列等待 HTTP 名称解析的秒数。 如果连接时间超过超时设定值，任务序列会取消该请求。 默认情况下，超时时间设置为 60 秒。


### <a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

 适用于[自动应用驱动程序](task-sequence-steps.md#BKMK_AutoApplyDrivers)步骤。

 请求驱动程序目录时，此变量用于指定任务序列等待发送请求的秒数。 如果请求时间超过超时设定值，任务序列会取消该请求。 默认情况下，超时时间设置为 60 秒。


### <a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

 当任务序列中发生错误时，它将显示对话框并包含相关错误。 任务序列在此变量指定的秒数后自动将其关闭。 默认情况下，该值为 900 秒（15 分钟）。


### <a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

 使用此变量可更改语言中性启动映像的显示语言。


### <a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

 指定运行任务序列时在目标计算机上保存临时文件的位置。

 在任务序列开始前设置此变量，例如通过设置集合变量。 任务序列启动后，Configuration Manager 定义 [_SMSTSMDataPath](#SMSTSMDataPath) 变量。


### <a name="SMSTSMP"></a> SMSTSMP

 使用此变量指定 Configuration Manager 管理点的 URL 或 IP 地址。


### <a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

 适用于以下步骤：  
 - [安装应用程序](task-sequence-steps.md#BKMK_InstallApplication)  
 - [安装软件更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  


 (input) 

 使用此变量启用重复的 MPList 请求，以便在客户端不在 Intranet 上时刷新客户端。 默认情况下，此变量设置为 `True`。 

 当客户端位于 Internet 上时，将此变量设置为 `False` 以避免不必要的延迟。 


### <a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

 适用于以下步骤：  
 - [安装应用程序](task-sequence-steps.md#BKMK_InstallApplication)  
 - [安装软件更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  


 (input) 

 此变量指定任务序列在利用定位服务检索管理点列表 (MPList) 失败后重新尝试此步骤之前等待的毫秒数。 默认情况下，任务序列在重新尝试之前会等待 `60000` 毫秒（60 秒）。 最多重试三次。


### <a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

 使用此变量可使客户端能够使用 Windows PE 对等缓存。 将此变量设置为 `true` 可启用此功能。


### <a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

 Windows PE 对等缓存用于初始广播的自定义网络端口。 客户端设置中配置的默认端口为 8004。


### <a name="SMSTSPersistContent"></a> SMSTSPersistContent

 使用此变量可临时将内容保存在任务序列缓存中。 此变量不同于 [SMSTSPreserveContent](#SMSTSPreserveContent)，它会在任务序列完成后将内容保存在 Configuration Manager 客户端缓存中。 SMSTSPersistContent 使用任务序列缓存，而 SMSTSPreserveContent 使用 Configuration Manager 客户端缓存。 


### <a name="SMSTSPostAction"></a> SMSTSPostAction

 指定任务序列完成后运行的命令。 例如，指定任务序列将操作系统部署到设备后，在嵌入的设备上启用写入筛选器的脚本。


### <a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

 强制任务序列运行目标计算机上的特定目标部署。 可通过媒体或 PXE 的预启动命令对此变量进行设置。 如果设置此变量，则任务序列覆盖任何必需的部署。


### <a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

 此变量用于标志在部署后将保留在 Configuration Manager 客户端缓存中的任务序列内容。 此变量不同于 [SMSTSPersistContent](#SMSTSPersistContent)，后者仅保留任务序列持续期间的内容。 SMSTSPersistContent 使用任务序列缓存，而 SMSTSPreserveContent 使用 Configuration Manager 客户端缓存。 将 SMSTSPreserveContent 设置为 `true` 可启用此功能。


### <a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

 指定在计算机重新启动之前要等待多少秒。 如果此变量为零 0，则任务序列管理器在重启之前不会显示通知对话框。

 #### <a name="example"></a>示例
 - `0`：不显示通知消息  

 - `60`：显示通知消息 1 分钟  


### <a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

 指定要在重启通知对话框中显示的消息。 如果未设置此变量，则显示默认消息。

 #### <a name="example"></a>示例
 `The task sequence is restarting this computer`


### <a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

 指示当前任务序列步骤完成后，请求重新启动。 如果需要重新启动，则将此变量设置为 `true`，任务序列管理器将在此任务序列步骤后重新启动计算机。 如果任务序列步骤需要重启才能完成操作，请设置此变量。 重启计算机后，任务序列继续从下一个任务序列步骤运行。


### <a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

 在完成当前的任务序列步骤后，将请求重试。 如果设置任务序列变量，还需将 [SMSTSRebootRequested](#SMSTSRebootRequested) 变量设置为 `true`。 重新启动计算机后，任务序列管理器将返回运行相同的任务序列步骤。


### <a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

 适用于[运行命令行](task-sequence-steps.md#BKMK_RunCommandLine)步骤。

 (input)

 指定运行命令行所依据的帐户。 此值为用户名或域\用户名形式的字符串。 使用 [SMSTSRunCommandLinePassword](#SMSTSRunCommandLinePassword) 变量指定帐户密码。

 有关任务序列运行方式帐户的详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account)。


### <a name="SMSTSRunCommandLinePassword"></a> SMSTSRunCommandLinePassword

 适用于[运行命令行](task-sequence-steps.md#BKMK_RunCommandLine)步骤。

 (input)

 为 [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName) 变量所指定的帐户指定密码。


### <a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

 适用于[安装软件更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)步骤。

 (input)

 控制此步骤中软件更新扫描的超时。 例如，如果预计在扫描期间有大量更新，则增加该值。 默认值为 `1800` 秒（30 分钟）。 变量值以秒为单位。


### <a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

 通过使用以下格式指定目标计算机的主要用户：`<DomainName>\<UserName>`。 使用逗号 (`,`) 分隔多个用户。 有关详细信息，请参阅[将用户与目标计算机相关联](/sccm/osd/get-started/associate-users-with-a-destination-computer)。

 #### <a name="example"></a>示例
 `contoso\jqpublic, contoso\megb, contoso\janedoh`


### <a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

 适用于[安装软件更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)步骤。

 (input)

 可使用这一可选的任务序列变量在软件更新安装需要两次重启时控制客户端行为。 在此步骤之前设置此变量，以防软件更新安装的第二次重启导致任务序列失败。

 设置 SMSTSWaitForSecondReboot 值（以秒为单位），指定在此步骤中，任务序列在计算机重启时的暂停的秒数。 预留充足的时间，以防还有第二次重启。 

例如，如果将 SMSTSWaitForSecondReboot 设置为 `600`，重启后任务序列将暂停 10 分钟，然后再运行其他步骤。 当单个安装软件更新任务序列步骤中需安装数百个软件更新时，这一变量十分有用。


### <a name="TSDisableProgressUI"></a> TSDisableProgressUI
 <!-- 1354291 --> 使用此变量控制任务序列何时向最终用户显示进度。 若要在不同时间隐藏或显示进度，请在一个任务序列中多次设置此变量。  

 - `true`：隐藏任务序列进度  

 - `false`：显示任务序列进度  


### <a name="TSErrorOnWarning"></a> TSErrorOnWarning 

 适用于[安装应用程序](task-sequence-steps.md#BKMK_InstallApplication)步骤。

 (input) 

 指定任务序列引擎是否在此步骤中将检测到的警告视为错误。 由于未满足要求而导致一个或多个应用程序或所需的依赖项未安装时，任务序列会将 [_TSAppInstallStatus](#TSAppInstallStatus) 变量设置为 `Warning`。 将此变量设置为 `True` 时，如果任务序列将 _TSAppInstallStatus 设置为 `Warning`，结果会出错。 值 `False` 是默认行为。


### <a name="WorkingDirectory"></a> WorkingDirectory

 适用于[运行命令行](task-sequence-steps.md#BKMK_RunCommandLine)步骤。

 (input)

 指定命令行操作的开始目录。 指定的目录名称不能超过 255 个字符。

 #### <a name="examples"></a>示例
 - `C:\`  
 - `%SystemRoot%`  



## <a name="deprecated-variables"></a>不推荐使用的变量

不推荐使用以下变量：

- OSDAllowUnsignedDriver：部署 Windows Vista 和更高版本的操作系统时不使用此变量
- OSDBuildStorageDriverList：仅适用于 Windows XP 和 Windows Server 2003
- OSDDiskpartBiosCompatibilityMode：部署 Windows XP 或 Windows Server 2003 时才需要此变量
- OSDInstallEditionIndex：Windows Vista 之后的版本不需要此变量
- OSDPreserveDriveLetter：有关详细信息，请参阅 [OSDPreserveDriveLetter](#OSDPreserveDriveLetter)

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

 > [!Important]
 > 此任务序列变量已被弃用。 
 >
 > 在操作系统部署期间，默认情况下，Windows 安装程序会确定要使用的最佳驱动器号（通常为 C:）。 

 上一行为：应用映像时，OSDPreverveDriveLetter 变量确定任务序列是否使用在映像文件 (WIM) 中捕获的驱动器号。 可以将此变量的值设置为 `false` 以使用为“应用操作系统”任务序列步骤中的“目标”设置指定的位置。 有关详细信息，请参阅[应用 OS 映像](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)。



## <a name="see-also"></a>另请参阅

- [任务序列步骤](/sccm/osd/understand/task-sequence-steps)
- [现有任务序列变量](/sccm/osd/understand/using-task-sequence-variables)
- [自动执行任务的规划注意事项](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
