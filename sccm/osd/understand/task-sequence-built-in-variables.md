---
title: 任务序列内置变量
titleSuffix: Configuration Manager
description: 任务序列内置变量提供有关任务序列运行环境的信息，并且这些变量在整个任务序列期间均适用。
ms.date: 04/18/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 02bc6bd4-ca53-4e22-8b80-d8ee5fe72567
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d3ea1b35c5f220155cecafddaf3a2ff1acf5ed53
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351653"
---
# <a name="task-sequence-built-in-variables-in-system-center-configuration-manager"></a>ystem Center Configuration Manager 中的任务序列内置变量

*适用范围：System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager 提供的任务序列内置变量。 内置变量提供有关任务序列的运行环境的信息，并且它们的值可在整个任务序列可用。 通常，在任务序列中运行步骤前初始化内置变量。 例如，内置变量 _SMSTSLogPath 是一个环境变量，指定 Configuration Manager 组件用于写入日志文件的路径。 任何任务序列步骤均可访问此环境变量。 但是，任务序列在每一个步骤之前都会评估某些变量，例如 &#95;SMSTSCurrentActionName。 对于名称以下划线开头的内置变量，值是只读的。  

## <a name="task-sequence-built-in-variable-list"></a>任务序列内置变量列表  
 下面的列表描述了 Configuration Manager 中可用的内置变量：  

|内置变量名称|说明|  
|-----------------------------|-----------------|  
|_OSDDetectedWinDir|在 Windows PE 启动时，任务序列会在计算机的硬盘驱动器上扫描是否以前已安装操作系统。 Windows 文件夹位置存储在此变量中。 你可以将任务序列配置为从环境中检索该值，并将其用于指定相同的 Windows 文件夹位置进行新的操作系统安装。|  
|_OSDDetectedWinDrive|在 Windows PE 启动时，任务序列会在计算机的硬盘驱动器上扫描是否以前已安装操作系统。 安装操作系统的硬盘驱动器位置存储在此变量中。 你可以将任务序列配置为从环境中检索该值，并将其用于指定相同的硬盘驱动器位置以供新的操作系统使用。|  
|_SMSTSAdvertID|存储当前运行的任务序列部署的唯一 ID。 它使用与 Configuration Manager 软件分发部署 ID 相同的格式。 如果任务序列从独立的媒体运行，则此变量未定义。<br /><br /> 例如：<br /><br /> **ABC20001**|  
|_TSAppInstallStatus|任务序列在[安装应用程序](task-sequence-steps.md#BKMK_InstallApplication)步骤中随应用程序的安装状态一起设置 _TSAppInstallStatus 变量。 任务序列使用下列值之一设置该变量：<br /><br /> 1.**未定义**：“安装应用程序”步骤未运行。<br />2.**错误**：在至少一个应用程序由于“安装应用程序”步骤中出错而失败时设置。<br />3.**警告**：在“安装应用程序”步骤中未发生任何错误。 由于不满足要求，一个或多个应用程序或必需的依赖项未安装。<br />4.**成功**：在“安装应用程序”步骤中未检测到任何错误或警告。|  
|_SMSTSBootImageID|如果当前运行的任务序列引用某个启动映像包，此变量会存储启动映像包 ID。 如果任务序列不引用启动映像包，则不会设置此变量。<br /><br /> 例如：<br /><br /> **ABC00001**|  
|_SMSTSBootUEFI|当任务序列检测到计算机处于 UEFI 模式时，它会设置 SMSTSBootUEFI 变量。|  
|_SMSTSClientGUID|存储 Configuration Manager 客户端 GUID 的值。 如果从独立的媒体运行任务序列，则不设置此变量。<br /><br /> 例如：<br /><br /> **0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c**|  
|_SMSTSCurrentActionName|指定当前运行的任务序列步骤的名称。 此变量在任务序列管理器运行每个单独步骤前设置。<br /><br /> 例如：<br /><br /> **运行命令行**|  
|_SMSTSDownloadOnDemand|如果当前的任务序列正在按需下载模式下运行，则此变量为 true。 按需下载模式是指任务序列管理器仅在必须访问内容时本地下载内容。|  
|_SMSTSInWinPE|如果当前的任务序列步骤正在 Windows PE 中运行，则此变量为 true。 测试此任务序列变量以确定当前的操作系统环境。|  
|_SMSTSLastActionRetCode|存储由运行的上一操作返回的返回代码。 此变量可作为决定下一步是否运行的条件。<br /><br /> 例如：<br /><br /> **0**|  
|_SMSTSLastActionSucceeded|如果最后一个步骤成功，此变量为 true。 如果最后一个步骤失败，此变量为 false。 如果由于任务序列被禁用或相关的条件被评估为 false 而导致其跳过最后一个操作，则不会重置此变量。 它仍保留之前操作的值。|  
|_SMSTSLaunchMode|指定以下一种任务序列启动方法：<br /><br /> -   **SMS**：从 Configuration Manager 客户端启动任务序列<br />-   **UFD**：从旧的 USB 媒体启动任务序列<br />-   **UFD+FORMAT**：从较新的 USB 媒体启动任务序列<br />-   **CD**：从 CD 启动任务序列<br />-   **DVD**：从 DVD 启动任务序列<br />-   **PXE**：从 PXE 启动任务序列<br />-   **HD**：从硬盘上的预暂存媒体启动任务序列|  
|_SMSTSLogPath|存储日志目录的完整路径。 可使用此值确定记录操作的位置。 如果没有硬盘驱动器可用，则不设置此值。|  
|_SMSTSMachineName|存储并指定计算机名称。 存储任务序列将用于记录所有状态消息的计算机的名称。 要更改新操作系统中的计算机名称，请使用“OSDComputerName”  变量。<br /><br /> 例如：<br /><br /> **ABC**|  
|_SMSTSMDataPath|指定由 SMSTSLocalDataDrive 变量定义的路径。 当在启动任务序列前定义 SMSTSLocalDataDrive 时，例如设置集合变量，启动任务序列后，Configuration Manager 将定义 _SMSTSMDataPath 变量。|  
|_SMSTSMediaType|指定用于启动安装的媒体类型。 媒体类型示例有启动媒体、完全媒体、PXE 和预暂存媒体。|  
|_SMSTSMP|存储 Configuration Manager 管理点的 URL 或 IP 地址。|  
|_SMSTSMPPort|存储 Configuration Manager 管理点的管理点端口号。<br /><br /> 例如：<br /><br /> **80**|  
|_SMSTSOrgName|存储任务序列在进度对话框中显示的品牌标题名称。<br /><br /> 例如：<br /><br /> **XYZ Organization**|  
|_SMSTSOSUpgradeActionReturnCode|存储 Windows 安装程序返回的用于指示成功或失败的退出代码值。 此变量在[升级操作系统](task-sequence-steps.md#BKMK_UpgradeOS)任务序列步骤过程中进行设置。 此变量可与 /Compat 命令行选项结合使用。<br /><br /> 例如：<br /><br /> 在 /Compat 完成时，可以根据失败或成功退出代码在后续步骤中执行操作。 成功时，可以启动升级。 或者，在环境中设置标记（例如，添加文件或设置注册表项）来收集硬件清单。 该标记可以用于创建准备好进行升级或在升级之前需要执行操作的计算机集合。|  
|_SMSTSPackageID|存储当前运行的任务序列的 ID。 此 ID 使用与 Configuration Manager 软件包 ID 相同的格式。<br /><br /> 例如：<br /><br /> **HJT00001**|  
|_SMSTSPackageName|存储当前运行的任务序列由 Configuration Manager 管理员在创建任务序列时指定的名称。<br /><br /> 例如：<br /><br /> **部署 Windows 10 任务序列**|  
|_SMSTSSetupRollback|指定操作系统安装程序是否执行了回滚操作。 变量值可以为“true”  或“false” 。|  
|_SMSTSRunFromDP|如果当前任务序列正在“从分发点运行”模式下运行（意味着任务序列管理器将从分发点获取所需的包共享），则此值设置为“true”  。|  
|_SMSTSSiteCode|存储 Configuration Manager 站点的站点代码。<br /><br /> 例如：<br /><br /> **ABC**|  
|_SMSTSType|指定当前运行的任务序列的类型。 可以有下列值：<br /><br /> **1** - 表示一般任务序列。<br /><br /> **2** - 表示操作系统部署任务序列。|  
|_SMSTSTimezone|_SMSTSTimezone 变量用以下格式（不含空格）存储时区信息：<br /><br /> Bias, StandardBias, DaylightBias, StandardDate.wYear, wMonth, wDayOfWeek, wDay, wHour, wMinute, wSecond, wMilliseconds, DaylightDate.wYear, wMonth, wDayOfWeek, wDay, wHour, wMinute, wSecond, wMilliseconds, StandardName, DaylightName<br /><br /> 例如：<br /><br /> 对于美国东部和加拿大时间，值是 **300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0, 东部标准时间, 东部白天时间**|  
|_SMSTSUseCRL|指定在使用 HTTPS 与管理点通信时，任务序列是否使用证书吊销列表 (CRL)。|  
|_SMSTSUserStarted|指定任务序列是否由用户启动。 仅当任务序列从软件中心启动时设置此变量。 例如，如果  “_SMSTSLaunchMode”设置为“SMS” 。 变量可以有下列值：<br /><br /> -   **true** - 指示任务序列通过用户从软件中心手动启动。<br />-   **false** - 指示任务序列由 Configuration Manager 计划程序自动启动。|  
|_SMSTSUseSSL|指定任务序列是否使用 SSL 与 Configuration Manager 管理点通信。 如果你的站点在纯模式下运行，则将此值设置为“true” 。|  
|_SMSTSWTG|指定计算机是否作为 Windows To Go 设备运行。|  
|OSDPreserveDriveLetter|此任务序列变量已被弃用。 在操作系统部署期间，默认情况下，Windows 安装程序会确定要使用的最佳驱动器号（通常为 C:）。 <br /><br />上一行为：应用映像时，OSDPreverveDriveLetter 变量确定任务序列是否使用在映像文件 (.WIM) 中捕获的驱动器号。 可以将此变量的值设置为“False”以使用为“应用操作系统”任务序列步骤中的“目标”设置指定的位置。 有关详细信息，请参阅 [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)。|  
|SMSTSAssignmentsDownloadInterval|客户端自上次尝试（未返回策略）下载策略到再次尝试之前所等待的秒数。 默认情况下，客户端将等待 0 秒，然后再重试。<br /><br /> 可以使用媒体或 PXE 中的预启动命令来设置此变量。|  
|SMSTSAssignmentsDownloadRetry|客户端在初次尝试下载策略而未找到策略之后将再次尝试下载该策略的次数。 默认情况下，客户端重新尝试 0 次。<br /><br /> 可以使用媒体或 PXE 中的预启动命令来设置此变量。|  
|SMSTSAssignUsersMode|指定任务序列如何将用户与目标计算机关联。 将该变量设置为以下值之一：<br /><br /> -   **自动**：当任务序列将操作系统部署到目标计算机时，它会在指定的用户和目标计算机之间创建关系。<br />-   **挂起**：任务序列创建指定的用户和目标计算机之间的关系。 管理员必须批准该关系才能对其进行设置。<br />-   **禁用**：当任务序列部署操作系统时，它不会将用户与目标计算机关联。|  
|SMSTSDownloadAbortCode|此变量包含（在 SMSTSDownloadProgram 变量中指定的）外部程序下载程序的中止代码值。 如果程序返回的错误代码等于 SMSTSDownloadAbortCode 变量的值，则内容下载失败，且未尝试其他下载方法。
|SMSTSDownloadProgram|使用此变量为任务序列指定替换内容提供程序，即用于下载内容的下载程序（而非默认的 Configuration Manager 下载程序）。 作为内容下载过程的一部分，任务序列会检查此变量，以了解是否指定了下载程序。 如果已指定，则任务序列会运行指定的程序来执行下载。|  
|SMSTSDownloadRetryCount|Configuration Manager 尝试从分发点下载内容的次数。 默认情况下，客户端重新尝试 2 次。|  
|SMSTSDownloadRetryDelay|Configuration Manager 重新尝试从分发点下载内容前等待的秒数。 默认情况下，客户端将等待 15 秒，然后再重试。|
|SMSTSDriverReceiveTimeOut|到服务器的连接超时之前的秒数。|
|SMSTSErrorDialogTimeout|当任务序列中发生错误时，它将显示对话框并包含相关错误。 任务序列在此变量指定的秒数后自动将其关闭。 默认情况下，该值为 900 秒（15 分钟）。|  
| TSDisableProgressUI | <!-- 1354291 -->从 Configuration Manager 版本 1706 开始，使用此变量控制任务序列何时向最终用户显示进度。 若要在不同时间隐藏或显示进度，请在一个任务序列中多次设置此变量。 若要隐藏任务序列进度，将此变量的值设为 True。 若要显示任务序列进度，将此变量的值设为 False。 | 
| SMSTSDisableStatusRetry | <!--512358--> 在断开连接的应用场景中，任务序列引擎重复尝试将状态消息发送到管理点。 在这种情况下，此行为会导致在任务序列处理过程中的延迟。 从 Configuration Manager 版本 1802 开始，将此变量设置为“True”后，任务序列引擎将不会尝试在第一次消息发送失败之后重新发送状态消息。 该第一次尝试包含多次重试。<br/><br/>重启任务序列时，此变量的值仍然存在。 但任务序列会尝试发送初始状态消息。 该第一次尝试包含多次重试。 如果成功，任务序列会继续发送状态，不会考虑此变量的值。 如果状态发送失败，任务序列将使用此变量的值。<br/><br/>注意：[任务序列状态报告](/sccm/core/servers/manage/list-of-reports#task-sequence---deployment-status)依赖这些状态消息，以显示进度、历史记录和每个步骤的详细信息。 | 
|SMSTSLanguageFolder|使用此变量可更改语言中性启动映像的显示语言。|  
|SMSTSLocalDataDrive|指定运行任务序列时临时文件保存在目标计算机的位置。<br /><br /> 此变量必须在任务序列开始前设置，例如通过设置集合变量。 任务序列启动后，Configuration Manager 定义 _SMSTSMDataPath 变量。|  
|SMSTSMP|使用此变量指定 Configuration Manager 管理点的 URL 或 IP 地址。|  
|SMSTSPeerDownload|使用此变量可使客户端能够使用 Windows PE 对等缓存。<br /><br /> 例如：<br /><br /> SMSTSPeerDownload  = **TRUE** 可启用此功能。|  
|SMSTSPeerRequestPort|Windows PE 对等缓存用于初始广播的自定义网络端口。 客户端设置中配置的默认端口为 8004。|  
|SMSTSPersistContent|使用此变量可临时将内容保存在任务序列缓存中。|  
|SMSTSPostAction|指定任务序列完成后运行的命令。 例如，你可使用此变量指定任务序列将操作系统部署到设备后，在嵌入的设备上启用写筛选器的脚本。|  
|SMSTSPreferredAdvertID|强制任务序列运行目标计算机上的特定目标部署。 可通过媒体或 PXE 的预启动命令对此变量进行设置。 如果设置此变量，则任务序列覆盖任何必需的部署。|  
|SMSTSPreserveContent|此变量用于标志在部署后将保留在 Configuration Manager 客户端缓存中的任务序列内容。 此变量不同于 SMSTSPersistContent，后者仅保留任务序列持续期间的内容。 SMSTSPersistContent 使用任务序列缓存，而 SMSTSPreserveContent 使用 Configuration Manager 客户端缓存。<br /><br /> 例如：<br /><br /> SMSTSPreserveContent = **TRUE** 可启用此功能。|  
|SMSTSRebootDelay|指定在计算机重新启动之前要等待多少秒。 如果此变量为零 0，则任务序列管理器在重启之前不会显示通知对话框。<br /><br /> 示例：<br /><br /> **0**：不显示通知消息<br /><br /> **60**：显示通知消息 1 分钟|  
|SMSTSRebootMessage|指定要在重启通知对话框中显示的消息。 如果未设置此变量，则显示默认消息。<br /><br /> 例如：<br /><br /> **任务序列正在重启此计算机**。|  
|SMSTSRebootRequested|指示当前任务序列步骤完成后，请求重新启动。 如果需要重新启动，则仅将此变量设置为 **true**，任务序列管理器将在此任务序列步骤后重新启动计算机。 如果任务序列步骤需要重启才能完成操作，请设置此变量。 重启计算机后，任务序列继续从下一个任务序列步骤运行。|  
|SMSTSRetryRequested|在完成当前的任务序列步骤后，将请求重试。 如果设置任务序列变量， **SMSTSRebootRequested** 必须设置为 **true**。 重新启动计算机后，任务序列管理器将重新运行相同的任务序列步骤。|  
|SMSTSUDAUsers|通过使用以下格式指定目标计算机的主要用户：<br /><br /> 例如：<br /><br /> **domain\user1、domain\user2、domain\user3**<br /><br /> 使用逗号 (，) 分隔多个用户。 有关详细信息，请参阅[将用户与目标计算机相关联](../get-started/associate-users-with-a-destination-computer.md)。|  
 
