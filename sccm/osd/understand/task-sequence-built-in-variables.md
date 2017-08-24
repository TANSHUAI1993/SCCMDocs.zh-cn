---
title: "任务序列内置变量 | Microsoft Docs"
description: "任务序列内置变量提供有关任务序列运行环境的信息，并且这些变量在整个任务序列期间均适用。"
ms.custom: na
ms.date: 03/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02bc6bd4-ca53-4e22-8b80-d8ee5fe72567
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 32b24b3637dfafe401ea1d9f51b3769aa749f544
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-built-in-variables-in-system-center-configuration-manager"></a>ystem Center Configuration Manager 中的任务序列内置变量

*适用范围：System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager 提供的任务序列内置变量。 内置变量提供有关任务序列的运行环境的信息，并且它们的值可在整个任务序列可用。 通常，在任务序列中运行步骤前初始化内置变量。 例如，内置变量 **_SMSTSLogPath** 是一个环境变量，指定任务序列运行时，Configuration Manager 组件用于写入日志文件的路径；任何任务序列步骤均可以访问此环境变量。 但是，有些变量（如 &#95;SMSTSCurrentActionName）在执行每个步骤前都要进行评估。 内置变量的值通常是只读的。 对于名称以下划线开头的内置变量，值是只读的。  

## <a name="task-sequence-built-in-variable-list"></a>任务序列内置变量列表  
 下面的列表描述了 Configuration Manager 中可用的内置变量：  

|内置变量名称|描述|  
|-----------------------------|-----------------|  
|_OSDDetectedWinDir|从 Configuration Manager 版本 1602 开始，在 Windows PE 启动时，任务序列会在计算机的硬盘驱动器上扫描是否以前已安装操作系统。 Windows 文件夹位置存储在此变量中。 你可以将任务序列配置为从环境中检索该值，并将其用于指定相同的 Windows 文件夹位置进行新的操作系统安装。|  
|_OSDDetectedWinDrive|从 Configuration Manager 版本 1602 开始，在 Windows PE 启动时，任务序列会在计算机的硬盘驱动器上扫描是否以前已安装操作系统。  安装操作系统的硬盘驱动器位置存储在此变量中。 你可以将任务序列配置为从环境中检索该值，并将其用于指定相同的硬盘驱动器位置以供新的操作系统使用。|  
|_SMSTSAdvertID|存储当前运行的任务序列部署的唯一 ID。 它使用与 Configuration Manager 软件分发部署 ID 相同的格式。 如果任务序列从独立的媒体运行，则此变量未定义。<br /><br /> 例如：<br /><br /> **ABC20001**|  
|_TSAppInstallStatus|任务序列在“安装应用程序”任务序列步骤中随应用程序的安装状态一起设置 _TSAppInstallStatus 变量。 任务序列使用下列值之一设置该变量：<br /><br /> 1.**未定义**：在“安装应用程序”任务序列步骤未运行时设置。<br />2.**错误**：在至少一个应用程序由于“安装应用程序”任务序列步骤中出错而失败时设置。<br />3.**警告**：在“安装应用程序”任务序列步骤中未出错但一个或多个应用程序或必需的依赖关系由于不满足要求而未安装时设置。<br />4.**成功**：在“安装应用程序”任务序列步骤中未检测到错误或警告时设置。|  
|_SMSTSBootImageID|如果某个启动映像包与当前运行的任务序列关联，则存储 Configuration Manager 启动映像包 ID。 如果不关联任何 Configuration Manager 启动映像包，则不设置此变量。<br /><br /> 例如：<br /><br /> **ABC00001**|  
|_SMSTSBootUEFI|当任务序列检测到计算机处于 UEFI 模式时，它会设置 SMSTSBootUEFI 变量。|  
|_SMSTSClientGUID|存储 Configuration Manager 客户端 GUID 的值。 如果从独立的媒体运行任务序列，则不设置此变量。<br /><br /> 例如：<br /><br /> **0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c**|  
|_SMSTSCurrentActionName|指定当前运行的任务序列步骤的名称。 此变量在任务序列管理器运行每个单独步骤前设置。<br /><br /> 例如：<br /><br /> **运行命令行**|  
|_SMSTSDownloadOnDemand|如果当前任务序列正在按需下载模式下运行（意味着任务序列管理器仅在必须访问内容时本地下载内容），则设置为“true”  。|  
|_SMSTSInWinPE|如果当前任务序列步骤正在 Windows PE 环境中运行，则此变量设置为“true”  ，否则设置为“false”  。 你可以测试此任务序列变量以确定当前的操作系统环境。|  
|_SMSTSLastActionRetCode|存储由运行的上一操作返回的返回代码。 此变量可作为决定下一步是否运行的条件。<br /><br /> 例如：<br /><br /> **0**|  
|_SMSTSLastActionSucceeded|如果上一操作成功，变量设置为“true”  ，如果上一操作失败，变量设置为“false”  。 如果由于步骤被禁用或关联的条件被评估为“false”而跳过上一操作，则此变量不会重置，这意味着仍保留之前操作的值 。|  
|_SMSTSLaunchMode|指定任务序列启动方法。 任务序列可以有下列值：<br /><br /> -   **SMS** - 指定通过使用 Configuration Manager 客户端启动任务序列。<br />-   **UFD** - 指定通过使用 USB 媒体启动任务序列和在 Windows XP/2003 中创建的 USB 媒体。<br />-   **UFD+FORMAT** - 指定通过使用 USB 媒体启动任务序列和在 Windows Vista 以及更高版本中创建的 USB 媒体。<br />-   **CD** - 指定通过使用 CD 启动任务序列。<br />-   **DVD** - 指定通过使用 DVD 启动任务序列。<br />-   **PXE** - 指定从 PXE 启动任务序列。<br />-   **HD** - 指定从硬盘（仅预暂存媒体）启动任务序列。|  
|_SMSTSLogPath|存储日志目录的完整路径。 可用于确定记录操作的位置。 如果没有硬盘驱动器可用，则不设置此值。|  
|_SMSTSMachineName|存储并指定计算机名称。 存储任务序列将用于记录所有状态消息的计算机的名称。 要更改新操作系统中的计算机名称，请使用“OSDComputerName”  变量。<br /><br /> 例如：<br /><br /> **ABC**|  
|_SMSTSMDataPath|指定由 SMSTSLocalDataDrive 变量定义的路径。 当在启动任务序列前定义 SMSTSLocalDataDrive 时，例如设置集合变量，启动任务序列后，Configuration Manager 将定义 _SMSTSMDataPath 变量。|  
|_SMSTSMediaType|指定用于启动安装的媒体类型。 媒体类型示例有启动媒体、完全媒体、PXE 和预暂存媒体。|  
|_SMSTSMP|存储 Configuration Manager 管理点的 URL 或 IP 地址。|  
|_SMSTSMPPort|存储 Configuration Manager 管理点的管理点端口号。<br /><br /> 例如：<br /><br /> **80**|  
|_SMSTSOrgName|存储在任务序列进度用户界面对话框中显示的品牌标题名称。<br /><br /> 例如：<br /><br /> **XYZ Organization**|  
|_SMSTSOSUpgradeActionReturnCode|存储从安装程序返回的用于指示成功或失败的退出代码值。  此变量在任务序列步骤“操作系统升级”任务序列步骤过程中进行设置。 这可与 /Compat Windows 10 安装程序命令行选项结合使用。<br /><br /> 例如：<br /><br /> 在 /Compat 完成时，可以根据失败或成功退出代码在后续步骤中执行操作。 成功时，可以启动升级。 或者，可以在环境中设置一个标记（例如，添加文件或设置注册表项），该标记随后可以用于创建准备好进行升级或是在升级之前需要执行操作的计算机集合。|  
|_SMSTSPackageID|存储当前运行的任务序列的 ID。 此 ID 使用与 Configuration Manager 软件包 ID 相同的格式。<br /><br /> 例如：<br /><br /> **HJT00001**|  
|_SMSTSPackageName|存储当前运行的任务序列由 Configuration Manager 管理员在创建任务序列时指定的名称。<br /><br /> 例如：<br /><br /> **部署 Windows 10 任务序列**|  
|_SMSTSSetupRollback|指定操作系统安装程序是否执行了回滚操作。 变量值可以为“true”  或“false” 。|  
|_SMSTSRunFromDP|如果当前任务序列正在“从分发点运行”模式下运行（意味着任务序列管理器将从分发点获取所需的包共享），则此值设置为“true”  。|  
|_SMSTSSiteCode|存储 Configuration Manager 站点的站点代码。<br /><br /> 例如：<br /><br /> **ABC**|  
|_SMSTSType|指定当前运行的任务序列的类型。 可以有下列值：<br /><br /> **1** - 表示一般任务序列。<br /><br /> **2** - 表示操作系统部署任务序列。|  
|_SMSTSTimezone|_SMSTSTimezone 变量用以下格式（不含空格）存储时区信息：<br /><br /> Bias, StandardBias, DaylightBias, StandardDate.wYear, wMonth, wDayOfWeek, wDay, wHour, wMinute, wSecond, wMilliseconds, DaylightDate.wYear, wMonth, wDayOfWeek, wDay, wHour, wMinute, wSecond, wMilliseconds, StandardName, DaylightName<br /><br /> 例如：<br /><br /> 对于美国东部和加拿大时间，值是 **300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0, 东部标准时间, 东部白天时间**|  
|_SMSTSUseCRL|指示当任务序列使用安全套接字层 (SSL) 证书与管理点通信时，任务序列是否使用证书吊销列表。|  
|_SMSTSUserStarted|指定任务序列是否由用户启动。 仅当任务序列从软件中心启动时设置此变量。 例如，如果  “_SMSTSLaunchMode”设置为“SMS” 。 变量可以有下列值：<br /><br /> -   **true** - 指示任务序列通过用户从软件中心手动启动。<br />-   **false** - 指示任务序列由 Configuration Manager 计划程序自动启动。|  
|_SMSTSUseSSL|指定任务序列是否使用 SSL 与 Configuration Manager 管理点通信。 如果你的站点在纯模式下运行，则将此值设置为“true” 。|  
|_SMSTSWTG|指定计算机是否作为 Windows To Go 设备运行。|  
|OSDPreserveDriveLetter|从 Configuration Manager 版本 1606 开始，已弃用此任务序列变量。 在操作系统部署期间，默认情况下，Windows 安装程序会确定要使用的最佳驱动器号（通常为 C:）。 <br /><br />在以前的版本中，OSDPreverveDriveLetter 变量决定当将此图像应用到目标计算机时，任务序列是否使用在操作系统映像 WIM 文件中捕获的驱动器号。 你可以将此变量的值设置为“False”  以使用为“应用操作系统”  任务序列步骤中的“目标”  设置指定的位置。 有关详细信息，请参阅 [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)。|  
|OSDSetupAdditionalUpgradeOptions|从 Configuration Manager 版本 1602 开始，此变量可用于指定 Windows 安装程序升级的其他选项。
|SMSTSAssignmentsDownloadInterval|使用此变量可指定客户端自上次尝试（未返回策略）下载策略到再次尝试之前所等待的秒数。 默认情况下，客户端将等待 **0** 秒，然后再重试。<br /><br /> 可以使用媒体或 PXE 中的预启动命令来设置此变量。|  
|SMSTSAssignmentsDownloadRetry|此变量用于指定客户端在初次尝试下载策略而未找到策略之后将再次尝试下载该策略的次数。 默认情况下，客户端将重试 **0** 次。<br /><br /> 可以使用媒体或 PXE 中的预启动命令来设置此变量。|  
|SMSTSAssignUsersMode|指定任务序列如何将用户与目标计算机关联。 将该变量设置为以下值之一。<br /><br /> -   自动：当任务序列将操作系统部署到目标计算机时，它会在指定的用户和目标计算机之间创建关系。<br />-   挂起：任务序列创建指定的用户和目标计算机之间的关系，但在设置关系前需等待来自管理用户的批准。<br />-   禁用：当任务序列部署操作系统时，它不会将用户与目标计算机关联。|  
|SMSTSDownloadAbortCode|此变量包含（在 SMSTSDownloadProgram 变量中指定的）外部程序下载程序的中止代码值。 如果程序返回的错误代码等于 SMSTSDownloadAbortCode 变量的值，则内容下载失败，且未尝试其他下载方法。
|SMSTSDownloadProgram|使用此变量为任务序列指定替换内容提供程序，即用于下载内容的下载程序（而非默认的 Configuration Manager 下载程序）。 作为内容下载过程的一部分，任务序列会检查此变量，以了解是否指定了下载程序。 如果已指定，则任务序列会运行指定的程序来执行下载。|  
|SMSTSDownloadRetryCount|使用此变量来指定 Configuration Manager 尝试从分发点下载内容的次数。 默认情况下，客户端将重试 **2** 次。|  
|SMSTSDownloadRetryDelay|使用此变量来指定 Configuration Manager 重新尝试从分发点下载内容前等待的秒数。 默认情况下，客户端将在重试之前等待 **15** 秒。|  
|SMSTSDriverReceiveTimeOut|使用此变量指定到服务器的连接超时之前的秒数。|
|SMSTSDriverRequestConnectTimeOut|在自动应用驱动程序任务序列步骤期间请求驱动程序目录时，使用此变量指定等待 HTTP 服务器连接的秒数。 如果连接时间超过超时设置，则取消该请求。 默认情况下，超时时间设置为 60 秒。|  
|SMSTSDriverRequestReceiveTimeOut|在自动应用驱动程序任务序列步骤期间，使用此变量指定等待驱动程序目录响应的秒数。 如果连接时间超过超时设置，则取消该请求。 默认情况下，超时时间设置为 480 秒。|
|SMSTSDriverRequestResolveTimeOut|在自动应用驱动程序任务序列步骤期间请求驱动程序目录时，使用此变量指定等待 HTTP 名称解析的秒数。 如果连接时间超过超时设置，则取消该请求。 默认情况下，超时时间设置为 60 秒。|
|SMSTSDriverRequestSendTimeOut|在自动应用驱动程序任务序列步骤期间发送驱动程序目录请求时，使用此变量指定要使用的秒数。 如果该请求用时比超时设置更长，则取消该请求。 默认情况下，超时时间设置为 60 秒。|
|SMSTSErrorDialogTimeout|当任务序列中发生错误时，显示对话框，在此变量指定的秒数后自动关闭。 默认情况下，该对话框将在 **900** 秒（15 分钟）后自动关闭。|  
| TSDisableProgressUI | 使用此变量可以在任务序列的不同部分中隐藏或显示任务序列进度。 | 
|TSErrorOnWarning|使用此变量指定任务序列引擎是否将应用程序安装任务序列步骤检测到的警告视为错误。 由于未满足要求而导致一个或多个应用程序或所需的依赖项未安装时，任务序列将 _TSAppInstallStatus 变量设置为 **Warning** 。 当你将 TSErrorOnWarning 变量设置为 **True** 且 _TSAppInstallStatus 变量设置为 Warning 时，它被视为错误。 值 **False** 是默认行为。| 
|SMSTSLanguageFolder|使用此变量可更改语言中性启动映像的显示语言。|  
|SMSTSLocalDataDrive|指定运行任务序列时临时文件保存在目标计算机的位置。<br /><br /> 此变量必须在任务序列开始前设置，例如通过设置集合变量。 任务序列启动后，Configuration Manager 定义 _SMSTSMDataPath 变量。|  
|SMSTSMP|使用此变量指定 Configuration Manager 管理点的 URL 或 IP 地址。|  
|SMSTSMPListRequestTimeout|使用此变量指定任务序列在利用定位服务检索管理点列表失败后重新尝试安装应用程序或软件更新前等待的毫秒数。 默认情况下，60,000 毫秒（60 秒）后，它重试此步骤，最多三次。 此变量仅适用于安装应用程序和安装软件更新任务序列步骤。|  
|SMSTSMPListRequestTimeoutEnabled|使用此变量启用重复的 MPList 请求，以便在客户端不在 Intranet 上时刷新客户端。 <br />默认情况下，此变量设置为 True。 当客户端位于 Internet 上时，可以将此变量设置为 False 以避免不必要的延迟。 此变量仅适用于安装应用程序和安装软件更新任务序列步骤。|  
|SMSTSPeerDownload|使用此变量可使客户端能够使用 Windows PE 对等缓存。<br /><br /> 例如：<br /><br /> SMSTSPeerDownload  = **TRUE** 可启用此功能。|  
|SMSTSPeerRequestPort|将此变量用于 Windows PE 对等缓存可指定在不使用客户端设置中配置的默认端口 (8004) 时，要用于初始广播的自定义网络端口。|  
|SMSTSPersistContent|使用此变量可临时将内容保存在任务序列缓存中。|  
|SMSTSPostAction|指定任务序列完成后运行的命令。 例如，你可使用此变量指定任务序列将操作系统部署到设备后，在嵌入的设备上启用写筛选器的脚本。|  
|SMSTSPreferredAdvertID|强制运行目标计算机上的特定目标部署。 可通过媒体或 PXE 的预启动命令对其进行设置。 如果设置此变量，则任务序列覆盖任何必需的部署。|  
|SMSTSPreserveContent|此变量用于标志在部署后将保留在 Configuration Manager 客户端缓存中的任务序列内容。 这与使用 SMSTSPersisContent（仅任务序列持续期间保留内容）不同，并且使用任务序列缓存，而非 Configuration Manager 客户端缓存。<br /><br /> 例如：<br /><br /> SMSTSPreserveContent = **TRUE** 可启用此功能。|  
|SMSTSRebootDelay|指定在计算机重新启动之前要等待多少秒。 如果此变量没有设置为 0，则任务序列管理器将在重新启动之前显示通知对话。<br /><br /> 例如：<br /><br /> **0**<br /><br /> **30**|  
|SMSTSRebootMessage|指定需要重新启动时显示在关机对话框中的消息。 如果未设置此变量，则显示默认消息。<br /><br /> 例如：<br /><br /> **此计算机将由任务序列管理器重新启动**。|  
|SMSTSRebootRequested|指示当前任务序列步骤完成后，请求重新启动。 如果需要重新启动，则仅将此变量设置为 **true**，任务序列管理器将在此任务序列步骤后重新启动计算机。 任务序列步骤必须设置此任务序列变量，如果其需要重新启动以完成任务序列步骤。 重新启动计算机后，任务序列将继续从下一个任务序列步骤运行。|  
|SMSTSRetryRequested|在完成当前的任务序列步骤后，将请求重试。 如果设置任务序列变量， **SMSTSRebootRequested** 必须设置为 **true**。 重新启动计算机后，任务序列管理器将重新运行相同的任务序列步骤。|  
|SMSTSSoftwareUpdateScanTimeout| 让你能够在执行[安装软件更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)任务序列步骤期间控制软件更新扫描的超时。 例如，如果有大量要安装的软件更新，你可能会增加默认值。 默认值为 30 分钟。 |
|SMSTSUDAUsers|指定目标计算机的主要用户。 通过使用以下格式指定用户。 使用逗号 (，) 分隔多个用户。<br /><br /> 例如：<br /><br /> **domain\user1、domain\user2、domain\user3**<br /><br /> 有关如何将用户与目标计算机关联的详细信息，请参阅[将用户与目标计算机关联](../get-started/associate-users-with-a-destination-computer.md)。|  
|SMSTSWaitForSecondReboot|从 Configuration Manager 版本 1602 开始，可使用这一可选的任务序列变量在软件更新安装需要两次重启时帮助控制客户端行为。 必须在[安装软件更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)步骤之前设置此变量，以防软件更新安装的第二次重启导致任务序列失败。<br /><br /> 设置 SMSTSWaitForSecondReboot 的值（以秒为单位），指定安装软件更新步骤期间，任务序列在计算机重启时的暂停时长，预留充足的时间，以防还有第二次重启。 <br />例如，将 SMSTSWaitForSecondReboot 设置为 600，即重启后任务序列将暂停 10 分钟，然后运行其他任务序列步骤。 当单个安装软件更新任务序列步骤中需安装数百个软件更新时，这一功能十分有用。|  
