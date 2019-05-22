---
title: 1902 版中的新增功能
titleSuffix: Configuration Manager
description: 获取有关 Configuration Manager Current Branch 版本 1902 中引入的更改和新增功能的详细信息。
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0c88cdc52442463bb3788c80c45d6c074dd900f5
ms.sourcegitcommit: 53f2380ac67025fb4a69fc1651edad15d98e0cdd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65673425"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch 版本 1902 中的新增功能

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager Current Branch 的更新 1902 作为控制台中更新提供。 将此更新应用于运行版本 1802、1806 或 1810 的站点。 <!-- baseline only statement:-->安装新站点时，它也可作为基准版本提供。 本文汇总了 Configuration Manager 版本 1902 中的更改和新增功能。  

始终查看安装此更新的最新清单。 有关详细信息，请参阅[用于安装更新 1902 的清单](/sccm/core/servers/manage/checklist-for-installing-update-1902)。 更新站点后，还可以查看[更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1902#post-update-checklist)。

若要利用 Configuration Manager 的新功能，更新站点后，还请将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

> [!Note]  
> 本文目前列出了此版本中的所有重要功能。 但是，并非所有部分都链接到更新的内容并提供有关新功能的进一步信息。 定期查看此页面以获取更新。 我们使用 [已更新] 标记标注更改。 内容最终确定后，将删除此标注。  

> [!Tip]  
> 若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`



## <a name="bkmk_deprecated"></a>弃用的功能和操作系统

在[已删除和已启用的项](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)中实施支持更改之前，先了解这些更改。

- 共享 Azure 内容的实现已更改。 通过启用“允许 CMG 充当云分发点，并提供 Azure 存储中的内容”的选项，使用启用了内容的云管理网关。 将来无法创建传统的云分发点。

版本 1902 删除了对以下产品的支持：  

- 作为客户端的 Linux 和 UNIX。 已在[版本 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support) 中宣布弃用。 请考虑使用 Microsoft Azure 管理来管理 Linux 服务器。 Azure 解决方案具有广泛的 Linux 支持（包括面向 Linux 的端到端补丁管理），在大多数情况下优于 Configuration Manager 的功能。



## <a name="bkmk_infra"></a>站点基础结构

### <a name="client-health-dashboard"></a>客户端运行状况仪表板
<!--3599209-->
可部署软件更新和其他应用，以帮助保护环境，但这些部署只能到达正常运行的客户端。 运行不正常的 Configuration Manager 客户端会对总体符合性产生不利影响。 根据分母来确定客户端运行状况可能有难度：在管理范围内总共应该有多少设备？ 例如，如果发现 Active Directory 中的所有系统，即便部分记录用于已停用的计算机，但此过程仍会使分母增大。 

现在可在环境中查看具有 Configuration Manager 客户端运行状况信息的仪表板。 查看客户端运行状况、方案运行状况和常见错误。 按多个属性筛选视图，以查看按 OS 和客户端版本列出的所有潜在问题。 

在 Configuration Manager 控制台中，转到“监视”工作区。 展开“客户端状态”，然后选择“客户端运行状况仪表板”节点。 

![客户端运行状况仪表板屏幕截图](media/3599209-client-health-dashboard.png)

<!-- For more information, see [How to monitor clients](/sccm/core/clients/manage/monitor-clients). -->


### <a name="new-management-insight-rules"></a>新管理见解规则
管理见解功能具有以下新规则：

- 包含对管理集合的建议的多个规则。 利用这些见解来简化管理并提高性能。 在“集合”组中查看这些新规则。<!--3555752-->  

- 将客户端更新到“简化管理”组中支持的 Windows 10 版本规则。 此规则报告运行不再受支持的 Windows 10 版本的客户端。 它还包括具有服务即将结束（三个月）的 Windows 10 版本的客户端。<!--3897268-->  

<!-- For more information, see [Management insights](/sccm/core/servers/manage/management-insights). -->


### <a name="improvement-to-enhanced-http"></a>对增强型 HTTP 的改进
<!--3798957-->
现在可为每个主站点或管理中心站点启用增强型 HTTP。 

在管理中心站点的属性上，选择“将 Configuration Manager 生成的证书用于 HTTP 站点系统”选项。 此设置仅适用于管理中心站点中的站点系统角色。 它不是层次结构的全局设置。 

<!-- For more information, see [enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http). -->


### <a name="improvement-to-setup-prerequisites"></a>对安装程序先决条件的改进
安装或更新到版本 1902 时，Configuration Manager 安装程序现在包括以下先决条件检查：

- **正在等待远程 SQL Server 上的系统重启**：此先决条件检查类似于“等待系统重启”规则，但它会检查远程 SQL Server。 有关详细信息，请参阅[先决条件检查列表](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart-on-the-remote-sql-server)。 <!--SCCMDocs-pr issue 3377-->  



## <a name="bkmk_cloud"></a>云附加管理

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>超过阈值时停止云服务
<!--3735092-->
现在，当数据传输总量超过限制时，Configuration Manager 可停止云管理网关 (CMG) 服务。 CMG 始终提供提醒，以便在使用量达到警告或严重级别时触发通知。 此新选项将关闭云服务，以帮助降低由于使用量陡升而意外导致的 Azure 成本。 

在 CMG 上[设置出站流量警告](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#set-up-outbound-traffic-alerts)，然后启用“在服务超过临界阈值时停止该服务”选项。  

<!-- For more information, see [Set up outbound traffic alerts](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#set-up-outbound-traffic-alerts). -->


### <a name="use-azure-resource-manager-for-cloud-services"></a>使用云服务适用的 Azure 资源管理器
<!--3605704-->
从版本 1810 开始，Configuration Manager 已弃用 Azure 的经典服务部署。 该版本是支持创建这些 Azure 部署的最后一个版本。 

现有部署将继续使用。 从此 Current Branch 版本起，Azure 资源管理器是用于云管理网关和云分发点的新实例的唯一部署机制。

<!-- For more information, see [Azure Resource Manager for the cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).   -->


### <a name="add-cloud-management-gateway-to-boundary-groups"></a>将云管理网关添加到边界组
<!--3640932-->
现在可以将云管理网关 (CMG) 与边界组关联。 此配置允许客户端根据边界组关系默认或回退到 CMG 以进行客户端通信。 在分支机构和 VPN 方案中，这一行为特别有用。 可以使客户端流量不使用昂贵且速度缓慢的 WAN 链接，改为使用更快的 Internet 链接以指向 Microsoft Azure。

<!-- For more information, see [Plan for the CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). -->



## <a name="bkmk_real"></a>实时管理

### <a name="run-cmpivot-from-the-central-administration-site"></a>从管理中心站点运行 CMPivot
<!--3610960-->
[已更新] Configuration Manager 现在支持从层次结构中的管理中心站点运行 CMPivot。 主站点仍可处理与客户端的通信。 从管理中心站点运行 CMPivot 时，它将通过高速消息订阅通道与主站点通信。 该通信不依赖于站点之间的标准 SQL 复制。

有关详细信息，请参阅[使用 CMPivot 获得实时数据](/sccm/core/servers/manage/cmpivot#bkmk_cmpivot1902)。


### <a name="edit-or-copy-powershell-scripts"></a>编辑或复制 PowerShell 脚本
<!--3705507-->
现在可以“编辑”或“复制”与运行脚本功能一起使用的现有 PowerShell 脚本。 现在可以直接编辑想要更改的脚本，而无需重新创建脚本。 这两种操作都使用与创建新脚本时所使用的相同向导体验。 编辑或复制脚本时，Configuration Manager 不会保留审批状态。 

<!-- For more information, see [Run Scripts](/sccm/apps/deploy-use/create-deploy-scripts). -->



## <a name="bkmk_content"></a>内容管理

### <a name="distribution-point-maintenance-mode"></a>分发点维护模式 
<!--3555754-->
现在可在维护模式下设置分发点。 如果要安装软件更新，或对服务器进行硬件更改，请启用维护模式。

当分发点处于维护模式下时，其行为如下： 

- 站点不会向该分发点分发任何内容。  

- 管理点不会向客户端返回此分发点的位置。 

- 更新站点时，维护模式下的分发点仍会更新。 

- 分发点属性为只读。 例如，不能更改证书或添加边界组。  

- 任何计划的任务（例如，内容验证）仍按相同的日程安排运行。 

<!-- For more information, see [Maintenance mode](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_maint) -->



## <a name="bkmk_client"></a> 客户端管理

### <a name="client-provisioning-mode-timeout"></a>客户端预配模式超时
<!--3197824-->
当任务序列使客户端处于预配模式时，将设置时间戳。 处于预配模式下的客户端每隔 60 分钟检查一次自该时间戳以后的持续时间。 如果客户端处于预配模式下超过 48 小时，它将自动退出预配模式，并重新启动其进程。 

<!-- For more information, see ... -->

### <a name="view-first-screen-only-during-remote-control"></a>在远程控制期间仅查看第一个屏幕
<!--3231732-->
[已更新] 当连接到具有两个或多个监视器的客户端时，可能很难在 Configuration Manager 远程控制查看器中查看所有监视器。 远程工具操作人员现在可以选择查看“所有屏幕”或仅查看“第一个屏幕”。

有关详细信息，请参阅[如何远程管理 Windows 客户端计算机](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer)。 


### <a name="specify-a-custom-port-for-peer-wakeup"></a>指定一个自定义端口用于对等唤醒
<!--3605925-->
***[已更新]***：现在可以为唤醒代理指定自定义端口号。 在客户端设置中，在“电源管理”组中，配置“唤醒 LAN 端口号(UDP)”的设置。  

有关详细信息，请参阅[如何配置 LAN 唤醒](/sccm/core/clients/deploy/configure-wake-on-lan)。



<!-- ## <a name="bkmk_comgmt"></a> Co-management -->




<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a>应用程序管理

### <a name="improvements-to-application-approvals-via-email"></a>对通过电子邮件进行的应用程序批准的改进
<!--3594063-->
此版本对用于接收应用程序请求的电子邮件通知的功能进行了改进。 用户始终能够从软件中心向请求添加注释。 此注释显示在 Configuration Manager 控制台中的应用程序请求中。 现在此注释也显示在电子邮件中。 在电子邮件中包含此注释有助于审批者做出更好的决定来批准或拒绝请求。

<!-- For more information, see [Email notifications](/sccm/apps/deploy-use/app-approval#bkmk_email-approve). -->


### <a name="improvements-to-package-conversion-manager"></a>对包转换管理器的改进
<!-- SCCMDocs-pr issue #3357 -->
此版本包括对[包转换管理器](/sccm/apps/pcm/package-conversion-manager)的以下改进：
- 默认情况下，计划的包分析每 7 天运行一次
- 用于分析和转换包的 PowerShell cmdlet
- 一般性的 bug 修复与改进



## <a name="bkmk_osd"></a> OS 部署


### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>就地升级任务序列期间的进度状态
<!--3747129-->
现在，在 Windows 10 就地升级任务序列期间，可以看到更为详细的进度栏。 此栏显示 Windows 安装程序的进度，否则在任务序列中为无提示状态。 用户现在可以了解基础进度。 它有助于解决由于缺少进度指示而暂停升级过程的问题。  

![使用 Windows 升级进度的示例任务序列进度](media/3747129-installation-progress.png)

此功能适用于任何受支持的 Windows 10 版本，且仅适用于就地升级任务序列。 


### <a name="improvements-to-task-sequence-media-creation"></a>对任务序列媒体创建的改进

<!--3556027, fka 1359388-->
***[已更新]***：此版本包括几项改进，有助于用户更好地创建和管理任务序列媒体。 有关详细信息，请参阅下列关于特定媒体类型的文章：

- [创建独立媒体](/sccm/osd/deploy-use/create-stand-alone-media)
- [创建预留媒体](/sccm/osd/deploy-use/create-prestaged-media)
- [创建可启动媒体](/sccm/osd/deploy-use/create-bootable-media)
- [创建捕获媒体](/sccm/osd/deploy-use/create-capture-media)

#### <a name="specify-temporary-storage"></a>指定临时存储

创建任务序列媒体时，现在可以自定义站点用作临时存储数据的位置。 此过程可能需要大量临时驱动空间。 此更改可以让你更灵活地选择存储这些临时文件的位置。

在“创建任务序列媒体向导”中，指定“暂存文件夹”的位置。 默认情况下，此位置类似于以下路径：`%UserProfile%\AppData\Local\Temp`。

#### <a name="add-a-label-to-the-media"></a>向媒体添加标签

现在可以向任务序列媒体添加标签。 此标签可帮助你在创建媒体后更好地识别媒体。 在“创建任务序列媒体向导”中，指定“媒体标签”。

#### <a name="include-autoruninf-file-on-media"></a>在媒体上添加 autorun.inf 文件

<!-- 4090666 -->
当你创建任务序列媒体时，Configuration Manager 不会添加 autorun.inf 文件。 反恶意软件通常会阻止此文件。 如果情况需要，仍然可以包括该文件。


### <a name="import-a-single-index-of-an-os-image"></a>导入 OS 映像的单个索引
<!--3719699-->
如果向 Configuration Manager 导入 Windows 映像 (WIM) 文件，现可指定自动导入单个索引，而不是文件中的所有映像索引。 此选项提供以下好处：

- 映像文件更小  
- 脱机维护更快  
- 优化映像维护，因为在脱机维护后可获得更小的映像文件 

导入 OS 映像时，选择“从指定 WIM 文件中提取特定的映像索引”选项。 然后从列表中选择该映像索引。  

<!-- For more information, see [Add an OS image](/sccm/osd/get-started/manage-operating-system-images#BKMK_AddOSImages). -->


### <a name="optimized-image-servicing"></a>经优化的映像维护
<!--3555951-->
向 OS 映像应用软件更新时，具有通过删除任何被取代更新来优化输出的新选项。 脱机维护优化仅适用于具有单个索引的映像。 

创建更新 OS 映像的计划时，选择“更新映像后删除被取代的更新”。 

<!-- For more information, see [Apply software updates to an image](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).  -->


### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>对运行 PowerShell 脚本任务序列步骤的改进

<!--3556028, fka 1359389-->
***[已更新]***：“运行 PowerShell 脚本”任务序列步骤现在包括以下改进：  

- 现在，可以在此步骤中直接输入 Windows PowerShell 代码。 此更改允许你在任务序列期间运行 PowerShell 命令，而无需先使用脚本创建和分发包。

- 选择“输入 PowerShell 脚本”选项时，请选择“编辑脚本”。 新的 PowerShell 脚本窗口提供以下操作：  

    - 直接编辑脚本  

    - 从文件打开现有的脚本  

    - 浏览到 Configuration Manager 中现有的已批准脚本

- 将脚本输出保存到自定义任务序列变量  

- 要在任务序列日志中包含脚本参数，请将任务序列变量 OSDLogPowerShellParameters 设置为“TRUE”。 默认情况下，参数不在日志中。  

- 提供与[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)步骤功能相似的其他改进。 例如，指定备用用户凭据或指定超时值。

> [!Important]  
> 若要利用 Configuration Manager 的此项新功能，更新站点后，还请将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

有关详细信息，请参阅[运行 PowerShell 脚本](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript)。


### <a name="other-improvements-to-os-deployment"></a>对 OS 部署的其他改进

<!--3633146,3641475,3654172,3734270-->
***[已更新]***：此版本包括以下对 OS 部署的改进：

- 任务序列中新增了“查看”默认操作。 <!--3633146-->  

- 任务序列错误对话框窗口现在显示更多信息。 它将显示失败的任务序列步骤的名称。 <!--3641475-->  

- 将 OSDDoNotLogCommand 任务序列变量设为 true 时，现在还可在日志文件中隐藏“运行命令行”步骤中的命令行。 它以前仅屏蔽 smsts.log 中“安装包”步骤中的程序名称。<!--3654172-->  

- 如果不使用 Windows 部署服务对分发点启用 PXE 响应程序，则它现在可能位于与 DHCP 服务相同的服务器上。 <!--3734270-->  <!-- For more information, see ... -->



## <a name="bkmk_userxp"></a>软件中心

### <a name="replace-toast-notifications-with-dialog-window"></a>使用对话框窗口替换 toast 通知

<!--3555947-->
***[已更新]***：有时，用户看不到有关重启或必需部署的 Windows toast 通知。 然后，他们也看不到推迟提醒体验。 当客户端临近截止时间时，此行为可能导致不佳的用户体验。

现在，在部署需要重启或要求进行软件更改时，可以选择使用侵入性更强的对话框窗口。

有关详细信息，请参阅[为软件中心制定计划](/sccm/apps/plan-design/plan-for-software-center#bkmk_impact)


### <a name="configure-user-device-affinity-in-software-center"></a>在软件中心中配置用户设备相关性
<!--3485366-->
借助从版本 1806 开始的[软件中心基础结构改进](/sccm/core/plan-design/changes/whats-new-in-version-1806#software-center-infrastructure-improvements)，大多数方案不再需要应用程序目录站点服务器角色。 某些客户仍依赖应用程序目录来允许用户将其主要设备设置为用户设备相关性。 

现在，用户可以在软件中心中设置其主要设备。 此操作使其成为 Configuration Manager 中设备的主要用户。

<!-- For more information, see [Link users and devices with user device affinity](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity). -->


### <a name="configure-default-views-in-software-center"></a>在软件中心配置默认视图
<!--3612112-->
此版本的 Configuration Manager 进一步迭代自定义软件中心的方式：
 
- 将应用程序的默认布局设置为磁贴或列表  

    - 如果用户更改此配置，则软件中心以后会保留用户的首选项  

- 对所有应用或仅对需要的应用配置默认应用程序筛选器  

    - 软件中心始终使用默认设置。 用户可以更改此筛选器，但软件中心不会保留其首选项。    

在客户端设置的“软件中心”组中指定这些设置。

<!-- For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#software-center). -->



## <a name="bkmk_sum"></a>软件更新

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>在 Windows 10 维护服务中指定功能更新的优先级
<!--3734525-->
[已更新] 调整客户端通过 [Windows 10 维护服务](/sccm/osd/deploy-use/manage-windows-as-a-service)安装功能更新的优先级。 默认情况下，客户端现在安装具有较高处理优先级的功能更新。 

使用客户端设置来配置此选项。 在“软件更新”组中，配置以下设置：为功能更新指定线程优先级。

有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#software-updates)。 



## <a name="bkmk_o365"></a>Office 管理

### <a name="redirect-windows-known-folders-to-onedrive"></a>将 Windows 已知文件夹重定向到 OneDrive
<!--3556021-->
[已更新] 使用 Configuration Manager 将 Windows 已知文件夹移动到 OneDrive for Business。 这些文件夹包括桌面、文档和图片。 若要简化 Windows 10 升级过程，请先将这些设置部署到 Windows 7 客户端，然后部署任务序列。 

有关此 OneDrive for Business 功能的详细信息，请参阅[将 Windows 已知文件夹重定向并移动到 OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders)。

首先，[找到你的 Office 365 租户 ID](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)。 然后部署 OneDrive 同步客户端版本 18.111.0603.0004 或更高版本。 有关详细信息，请参阅[使用 System Center Configuration Manager 部署 OneDrive 应用](https://docs.microsoft.com/onedrive/deploy-on-windows)。  

若要创建和部署 OneDrive for Business 配置文件，在 Configuration Manager 控制台中，转到“资产和符合性”工作区。 展开“符合性设置”，然后选择“OneDrive for Business 配置文件”节点。  

有关详细信息，请参阅 [OneDrive for Business 配置文件](/sccm/compliance/deploy-use/onedrive-profile)一文中的“将 Windows 已知文件夹重定向到 OneDrive”部分。


### <a name="integration-for-office-365-proplus-readiness"></a>Office 365 专业增强版集成的就绪情况
<!--3735402-->
[已更新] 使用 Configuration Manager 识别准备升级到 Office 365 专业增强版的设备，且识别的可信度非常高。 通过该集成可以深入了解环境中所用 Office 加载项和宏的任何潜在兼容性问题。 然后使用 Configuration Manager 将 Office 部署到已就绪的设备。 

现有 Office 365 客户端管理仪表板现在包含新磁贴“Office 365 专业增强版升级就绪情况”。

有关详细信息，请参阅 [Office 365 客户端管理仪表板](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness)


### <a name="additional-languages-for-office-365-updates"></a>Office 365 更新的其他语言
<!--3555955-->
Configuration Manager 现在支持 Office 365 客户端更新支持的所有语言。 现在，更新工作流将“Windows 更新”的 38 种语言与“Office 365 客户端更新”的多种语言分开。 

有关详细信息，请参阅[管理 Office 365 更新](/sccm/sum/deploy-use/manage-office-365-proplus-updates#bkmk_o365_lang)


### <a name="office-products-on-lifecycle-dashboard"></a>生命周期仪表板上的 Office 产品
<!--3556026-->
***[已更新]***：产品生命周期仪表板现包括已安装的 Office 2003 至 Office 2016 版本的信息。 数据在站点运行生命周期摘要任务后（即每隔 24 小时）显示。

有关详细信息，请参阅[使用产品生命周期仪表板](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard)。



<!-- ## <a name="bkmk_inv"></a> Inventory -->



## <a name="bkmk_pod"></a>分阶段部署

### <a name="dedicated-monitoring-for-phased-deployments"></a>分阶段部署专用监视
<!--3555949-->
***[已更新]***：分阶段部署现有自己的专用监视节点。 此节点可以更轻松地标识创建的分阶段部署，然后导航到分阶段部署监视视图。 在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“分阶段部署”节点。 它将显示分阶段部署列表。

有关详细信息，请参阅[分阶段部署监视视图](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_monitor)。 


### <a name="improvement-to-phased-deployment-success-criteria"></a>对分阶段部署成功标准的改进
<!--3555946-->
***[已更新]***：指定分阶段部署中额外的阶段成功标准。 此标准现在也可以是成功部署的设备数，而不仅仅是百分比。 当集合的大小可变并且你在前进到下一阶段前已有一定数量的设备成功部署时，此选项很有用。 

为任务序列、软件更新或应用程序创建分阶段部署。 然后，在向导的“设置”页上，选择以下选项作为第一阶段成功的标准：“成功部署的设备数”。

有关详细信息，请参阅[创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)。



## <a name="bkmk_admin"></a> Configuration Manager 控制台

### <a name="bkmk_console"></a> 对 Configuration Manager 控制台的改进
<!--3594151-->
根据中西部管理峰会 (MMS) Desert 版本 2018 的客户反馈，此版本包含对 Configuration Manager 控制台的以下改进：
- 将应用程序检测方法浏览注册表窗口最大化
- 从应用程序部署转到集合
- 从监视状态中删除内容
- “监视”工作区的“部署”节点中，视图按整数值排序
- 移动警告以获得大量结果

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="configuration-manager-console-notifications"></a>Configuration Manager 控制台通知
<!--3556016, fka 1318035-->
为了更好地了解情况以便采取适当的操作，Configuration Manager 控制台现在会通知以下事件：
- Configuration Manager 本身有可用的更新
- 环境中发生生命周期和维护事件

此通知位于功能区下方控制台窗口顶部的栏。 Configuration Manager 更新可用时，它将替换以前的体验。 这些控制台内通知仍显示关键信息，但不会干扰你在控制台中的工作。 不能消除重要通知。 控制台在标题栏的新通知区域中显示所有通知。 

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="confirmation-of-console-feedback"></a>确认控制台反馈
<!--3556010-->
[已更新] 在 Configuration Manager 控制台中发送[反馈](/sccm/core/understand/find-help#product-feedback)时，现在它将显示一条确认消息。 此消息包含反馈 ID，可将其作为跟踪标识符提供给 Microsoft。

有关详细信息，请参阅[产品反馈](/sccm/core/understand/find-help#bkmk_feedbackid)。


### <a name="view-recently-connected-consoles"></a>查看最近连接的控制台 
<!--3699367-->
[已更新] 现在可以查看 Configuration Manager 控制台的最新连接。 视图包括活动连接以及最近连接的控制台。 在 Configuration Manager 控制台中，转到“管理”工作区，展开“安全性”，然后选择“控制台连接”节点。

有关详细信息，请参阅[使用 Configuration Manager 控制台](/sccm/core/servers/manage/admin-console#bkmk_viewconnected)。


### <a name="in-console-documentation-dashboard"></a>控制台内文档仪表板
<!--3556019, fka 1357546-->
新“社区”工作区中新增了一个“文档”节点。 此节点包含有关 Configuration Manager 文档和支持文章的最新信息。

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="search-device-views-using-mac-address"></a>使用 MAC 地址搜索设备视图
<!--3600878-->
现在可以在 Configuration Manager 控制台的设备视图中搜索 MAC 地址。 此属性在 OS 部署管理员排查基于 PXE 部署的问题时很有用。 查看设备列表时，请向视图添加“MAC 地址”列。 使用搜索字段添加“MAC 地址”搜索条件。 


### <a name="use-net-47-for-improved-console-accessibility"></a>使用 .NET 4.7 以改进控制台的辅助功能
<!-- SCCMDocs-pr issue #3228 -->
若要改进 Configuration Manager 控制台的辅助功能，请在运行控制台的计算机上将 .NET 更新到版本 4.7 或更高版本。 

有关详细信息，请参阅 [Configuration Manager 中的辅助功能](/sccm/core/understand/accessibility-features)。


### <a name="changes-to-console-setup-process"></a>对控制台安装过程的更改

<!-- 3612513 -->
[已更新] 安装 Configuration Manager 控制台时需要新组件。 如果创建用于在其他计算机上安装控制台的程序包，请确保该程序包包含以下文件：

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

安装或更新站点服务器时，它会将这些安装文件和受支持的站点语言包复制到 Tools\ConsoleSetup 子文件夹中。 有关详细信息，请参阅[安装 Configuration Manager 控制台](/sccm/core/servers/deploy/install/install-consoles)。



<!-- ## <a name="bkmk_opmdm"></a> On-premises MDM -->




## <a name="other-updates"></a>其他更新

除了新增功能外，这一版还有其他变化（如缺陷修复）。 有关详细信息，请参阅 [Configuration Manager Current Branch（版本 1902）的更改摘要](https://support.microsoft.com/help/4498910)。

有关 Configuration Manager 的 Windows PowerShell cmdlet 更改的详细信息，请参阅 [PowerShell 版本 1902 发行说明](https://docs.microsoft.com/powershell/sccm/1902-release-notes?view=sccm-ps)。

<!-- 
The following update rollup (4486457) is available in the console starting on 25 January 2019: [Update rollup for Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4486457).


### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |
 
-->



## <a name="next-steps"></a>后续步骤

准备好安装此版本时，请参阅[安装 Configuration Manager 的更新](/sccm/core/servers/manage/updates)和[用于安装更新 1902 的清单](/sccm/core/servers/manage/checklist-for-installing-update-1902)。

> [!TIP]  
> 若要安装新站点，请使用 Configuration Manager 的基准版本。  
>
>  了解详细信息：    
>   - [安装新站点](/sccm/core/servers/deploy/install/installing-sites)  
>   - [基准和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

关于已知的重要问题，请参阅[发行说明](/sccm/core/servers/deploy/install/release-notes)。

更新站点后，还可以查看[更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1902#post-update-checklist)。
