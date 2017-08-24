---
title: "新版本 1702 |Microsoft Docs"
description: "获取有关 System Center Configuration Manager 的 1702 版中引入的更改和新功能的详细信息。"
ms.custom: na
ms.date: 05/02/2017
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a2954b3c6f9a09b7246347e780c4cfc49ba39ca1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>System Center Configuration Manager 版本 1702 中的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager Current Branch 的更新 1702 作为控制台内更新提供，用于运行版本 1602, 1606 或 1610 的以前安装的站点。 安装新部署时，也可将其作为基准版本使用。

> [!TIP]  
> 若要安装新站点，必须使用 Configuration Manager 的基准版本。  
>  了解详细信息：    
>   - [安装新站点](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [在站点上安装更新](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [基准和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

以下各节提供有关 Configuration Manager 版本 1702 中引入的更改和新功能的详细信息。  

## <a name="deprecated-features-and-operating-systems"></a>弃用的功能和操作系统
在其施前，先在[删除和弃用的功能](/sccm/core/plan-design/changes/removed-and-deprecated-features)中了解有关支持更改的相关信息。

版本 1702 删除了对以下产品的支持：
- **SQL Server 2008 R2**，针对站点数据库服务器。 在 2015 年 7 月 10 日[首次公布](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-support-for-sql-server-versions-as-a-site-database)要弃用支持。 在使用版本 1702 以前的 Configuration Manager 的版本时，此版本的 SQL Server 仍受支持。
- **Windows Server 2008 R2**，针对站点系统服务器和大部分站点系统角色。 在 2015 年 7 月 10 日[首先公布](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems)要弃用支持。 在使用版本 1702 以前的 Configuration Manager 的版本时，此版本的 Windows 仍受支持。  
- **Windows Server 2008**，针对站点系统服务器和大部分站点系统角色。 在 2015 年 7 月 10 日[首先公布](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems)要弃用支持。
- **Windows XP Embedded**，作为客户端操作系统。 在 2015 年 7 月 10 日[首先公布](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems)要弃用。 在使用版本 1702 以前的 Configuration Manager 的版本时，此版本的 Windows 仍受支持。




## <a name="site-infrastructure"></a>站点基础结构

### <a name="improvements-for-in-console-search"></a>控制台中搜索功能的改进
以下是对在 Configuration Manager 控制台中使用搜索所进行的改进：
 - **对象路径：**  
  现在，很多对象都支持名为**对象路径**的列。  当用户搜索并将此列包括在显示结果中时，可以查看每个对象的路径。 例如，如果在应用程序节点搜索应用，并且同时要搜索子节点，结果窗格中的*对象路径*列将向用户显示每个返回对象的路径。   

- **保留搜索文本：**  
  在搜索文本框中输入文本，然后在搜索子节点和搜索当前节点之间切换时，已键入的文本会保留，并且仍然可用于新搜索而无需重新输入。

- **保留搜索子节点的决策：**  
 现在，更改使用的节点时，会保留对搜索*当前节点*或*所有子节点*所选择的选项。 这一新特点意味着在控制台执行操作时无需不断重置此决策。 默认情况下，打开控制台选项时，将仅搜索当前节点。


### <a name="send-feedback-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台发送反馈

 可以使用控制台内反馈选项将反馈直接发送到开发团队。

 可在以下位置找到“反馈”选项：
 -  在功能区中每个节点的“主页”选项卡的最左侧。  
    ![功能区](./media/feedback-home.png)

 -  右键单击控制台中的任何对象时。   
     ![右键单击选项](./media/feedback-option.png)   

 选择“反馈”将打开浏览器，并转到 [Configuration Manager UserVoice 反馈网站](https://go.microsoft.com/fwlink/?linkid=617029)。


###  <a name="changes-for-updates-and-servicing"></a>更新和维护服务的更改
以下是对更新和服务的更改：

- **节点位置**   
  安装版本 1702 后，**更新和服务**节点在**管理**下方作为顶级节点显示。 它不再是**云服务**下方的子节点。

- **新的更新状态**  
  在控制台中查看可用更新时，将有两种新状态：  
  - **可供安装** - 这是已下载并准备安装的更新。
  - **准备下载** - 此更新可用，但尚未下载。 可选择下载此更新，但它已被较新的更新所取代。


- **简化更新选项**  
  下次当你的基础架构有资格下载两个或多个更新时，将仅下载最新更新。 例如，如果当前站点版本比最新可用版本低两个或更多版本，将仅自动下载最新版本的更新。  

  可选择下载并安装其他可用更新，即使它们不是最新版本。 如果下载了较旧的版本，你将收到此更新已由较新更新替换的警告。 若要下载可下载的更新，在控制台中选择更新，然后单击“下载”。

- **针对较旧更新的清理功能得到改进**   
  已添加自动清理功能，可从站点服务器上的“EasySetupPayload”文件夹中删除不需要的下载文件。 因为这是在版本 1702 中引入的，所以在安装后续更新后（如更新汇总或未来的更新版本）开始清理工作。  


### <a name="data-warehouse-service-point"></a>数据仓库服务点
 使用数据仓库服务点存储和报告关于 Configuration Manager 部署的长期历史数据。

 数据仓库最多支持 2 TB 数据，且具有跟踪更改的时间戳。 通过从 Configuration Manager 站点数据库自动同步到数据仓库数据库可实现数据存储。 然后，可从 Reporting Services 点访问此信息。

 有关详细信息，请参阅[数据仓库服务点](/sccm/core/servers/manage/data-warehouse)。


### <a name="peer-cache-improvements"></a>对等缓存功能改进
 从版本 1702 开始，当对等缓存源计算机满足以下任一条件时，将会拒绝对内容的请求：  
  -  处于低电量模式。
  -  请求内容时 CPU 负载超过 80%。
  -  磁盘 I/O 的 AvgDiskQueueLength 超过 10。
  -  该计算机没有其他可用连接。   
有关详细信息，请参阅 [Configuration Manager 客户端的对等缓存](/sccm/core/plan-design/hierarchy/client-peer-cache)中的**对等缓存源的有限访问**。   

此外，向你的报表点添加了三个新的报表。 可以使用这些报表了解有关被拒绝的内容请求的详细信息，其中包括边界组、计算机和所涉及的内容。 请参阅对等缓存主题中的[监视](/sccm/core/plan-design/hierarchy/client-peer-cache#monitoring)。

### <a name="content-library-cleanup-tool"></a>内容库清理工具
 使用[内容库清理工具](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool)从分发点删除与应用程序不再关联的内容。


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>将 OMS 连接器与 Azure Government 云结合使用
可以使用 OMS 连接器连接到 Microsoft Azure Government 云中的 OMS Log Analytics。 这要求你在安装 OMS 连接器前修改配置文件，以将连接器与 Government 云结合使用。 有关详细信息，请参阅[将 OMS 连接器与 Azure Government 云结合使用](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig)。

### <a name="software-update-points-are-added-to-boundary-groups"></a>将软件更新点添加到边界组。
从版本 1702 开始，客户端使用边界组查找新的软件更新点，并在其当前软件更新点不再可用时回退并查找新的软件更新点。 可以向不同的边界组添加各个软件更新点，以控制客户端可以找到哪些服务器。 有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)主题中的[软件更新点](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>符合性设置

### <a name="new-compliance-settings-for-ios"></a>iOS 的新符合性设置

我们为 iOS 设备添加了许多新的设置以匹配 Microsoft Intune 中可用的设置。
有关所有可用设置的列表，请参阅[为使用 Intune 管理的 iOS 和 Mac OS X 设备创建配置项](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)。


## <a name="application-management"></a>应用程序管理

### <a name="improved-support-for-windows-store-for-business-apps"></a>提升了对适用于企业的 Windows 应用商店应用的支持

现在，可以使用 Configuration Manager 客户端将联机许可应用从适用于企业的 Windows 应用商店部署到你所管理的 Windows 10 电脑 。
有关详细信息，请参阅[管理来自适用于企业的 Windows 应用商店的应用](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)。

### <a name="check-for-running-executable-files-before-installing-an-application"></a>在安装应用程序之前检查运行的可执行文件

在部署类型的“属性”对话框的“安装行为”选项卡中，现在可以指定一个或多个可执行文件，如果运行此类文件，将阻止安装部署类型。 用户必须先关闭运行中的可执行文件（或者因为部署的特定要求而自动关闭），然后才能安装部署类型。

如果应用程序已部署为“可用”，最终用户尝试安装应用程序时，系统会提示其先关闭指定的任何运行中的可执行文件，然后才能继续安装。

如果应用程序已部署为“必需”，且已选择“自动关闭在‘部署类型属性’对话框中的‘安装行为’选项卡中指定的任何运行中的可执行文件”选项，他们将看到一个对话框，通知他们在应用程序安装截止时间到达时将自动关闭指定的可执行文件。

### <a name="app-management-improvements-for-hybrid-mdm"></a>针对混合 MDM 的应用管理改进

- [将批量采购的 iOS 应用部署到设备集合](#deploy-volume-purchased-ios-apps-to-device-collections)
- [支持 iOS Volume Purchase Program 教育版](#support-for-ios-volume-purchase-program-for-education)
- [支持多个批量采购计划标记](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>操作系统部署

### <a name="expire-stand-alone-media"></a>对独立介质设置到期日期
创建独立介质时，可使用新选项对介质设置可选开始日期和到期日期。 默认情况下，这些设置处于禁用状态。 独立介质运行前，该日期将与计算机上的系统时间进行比较。 如果系统时间早于开始时间或晚于过期时间，则独立介质不会启动。 也可通过使用 New-CMStandaloneMedia PowerShell cmdlet 启用这些选项。 有关详细信息，请参阅[创建独立介质](/sccm/osd/deploy-use/create-stand-alone-media)。

### <a name="package-id-displayed-in-task-sequence-steps"></a>在任务序列步骤中显示包 ID
任何引用包、驱动程序包、操作系统映像、启动映像或操作系统升级包的任务序列步骤现在将显示引用对象的包 ID。 任务序列步骤引用应用程序时，将显示对象 ID。

### <a name="support-for-additional-content-in-stand-alone-media"></a>对独立介质中的其他内容的支持
在独立介质中现在支持其他内容。 可选择将额外的包、驱动程序包和应用程序，以及任务序列中引用的其他内容暂存在介质中。 以前，仅任务序列中引用的内容才暂存在独立介质中。 有关详细信息，请参阅[创建独立介质](/sccm/osd/deploy-use/create-stand-alone-media)。

### <a name="hardware-inventory-collects-uefi-information"></a>硬件清单将收集 UEFI 信息
新的硬件清单类 (**SMS_Firmware**) 和属性 (**UEFI**) 可帮助确定是否以 UEFI 模式启动计算机。 如果以 UEFI 模式启动计算机，则 **UEFI** 属性设为 **TRUE**。 默认情况下，这在硬件清单中处于启用状态。 有关硬件清单的详细信息，请参阅[如何配置硬件清单](/sccm/core/clients/manage/inventory/configure-hardware-inventory)。

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>改进了高效任务序列的软件中心警告消息
此版本对高效部署任务序列的软件中心警告消息进行了以下改进：

- 在任务序列的属性中，现可将任何任务序列（包括非操作系统任务序列）配置为高风险部署。 任何符合特定条件的任务序列都将自动定义为“影响重大”。 有关详细信息，请参阅[管理高风险部署](/sccm/protect/understand/settings-to-manage-high-risk-deployments)。
- 在任务序列的属性中，可以选择针对影响重大的部署，使用默认通知消息或创建自定义通知消息。
- 在任务序列的属性中，可以配置软件中心属性，其中包括设置必要的重启、任务序列的下载大小和预计运行时间。
- 对于就地升级，默认的重大影响部署消息指示你的应用、数据和设置将自动迁移。 以前，任何操作系统安装的默认消息均指示所有应用、数据和设置将丢失，但这样的消息实际上并不适用于就地升级。

有关详细信息，请参阅[配置影响重大的任务序列设置](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>任务序列失败时返回上一页
现在，运行任务序列出现故障时，可以返回到上一页面。 在此版本之前，出现故障时必须重启任务序列。 例如，可在以下应用场景中使用“上一页”按钮：

- 当计算机在 Windows PE 中启动时，任务序列可用之前可能会先显示任务序列启动对话框。 在此应用场景中单击“下一步”时，会显示任务序列的最后一页，同时显示一条消息告知无可用的任务序列。 现在，可单击“上一页”以再次搜索可用任务序列。 在出现可用任务序列之前，可重复此过程。
- 运行任务序列但分发点上尚无可用从属内容包时，任务序列会失败。 现在，用户可以分发缺失的内容（如果尚未分发），或等待分发点上出现可用内容，然后单击“上一页”使任务序列再次搜索内容。

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>为可用部署和任务序列预先缓存内容
从版本 1702 开始，对于可用的部署和任务序列，可以选择使用预先缓存内容。 借助预先缓存内容，用户可选择允许客户端在收到部署后立即下载适用的内容。 因此，当用户在软件中心中单击“安装”时，内容便已就绪，并且安装可以快速启动，因为内容位于本地硬盘上。 有关详细信息，请参阅[配置预先缓存内容](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)。

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>在就地升级过程中从 BIOS 转换到 UEFI
Windows 10 创意者更新引入了一个简单的转换工具，可自动执行对用于启用 UEFI 的硬件的硬盘重新分区的过程，并将该转换工具集成到 Windows 7 到 Windows 10 的就地升级过程中。 将此工具与你的操作系统升级任务序列和将固件从 BIOS 转换到 UEFI 的 OCM 工具组合使用时，可以在 Windows 10 创意者更新的就地升级过程中将你的计算机从 BIOS 转换到 UEFI。 有关详细信息，请参阅[管理 BIOS 转换为 UEFI 所采用的任务序列步骤](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)。

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>对“安装应用程序任务”序列步骤的改进
此版本引入了以下改进：
- 在**安装应用程序**任务序列步骤中，将可安装的应用程序的最大数量增加到 99 个。 以前的最大数量为 9 个应用程序。
- 在任务序列编辑器中向“安装应用程序”任务序列步骤添加应用程序时，现在可以从“选择要安装的应用程序”窗格中选择多个应用程序。

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>对“自动应用驱动程序”任务序列所做的改进
在发出 HTTP 目录请求时，新任务序列变量现在可在“自动应用驱动程序”任务序列步骤中配置超时值。 下面是可用的变量和默认值（以秒为单位）：
   - SMSTSDriverRequestResolveTimeOut  
     默认值：60
   - SMSTSDriverRequestConnectTimeOut  
     默认值：60
   - SMSTSDriverRequestSendTimeOut  
     默认值：60
   - SMSTSDriverRequestReceiveTimeOut  
     默认值：480

### <a name="windows-10-adk-tracked-by-build-version"></a>内部版本所跟踪的 Windows 10 ADK
现在可通过内部版本号跟踪 Windows 10 ADK，确保自定义 Windows 10 启动映像时有更多受支持的体验。 例如，如果站点使用适用于 Windows 10 的 Windows ADK（版本 1607），那么控制台中仅可自定义版本号为 10.0.14393 的启动映像。 若要深入了解如何自定义 WinPE 版本，请参阅[自定义启动映像](/sccm/osd/get-started/customize-boot-images)。

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>默认启动映像源路径无法再进行更改
默认启动映像由 Configuration Manager 托管，并且无法再在 Configuration Manager 控制台中或通过使用 Configuration Manager SDK 更改默认启动映像源路径。 可继续为自定义启动映像配置自定义源路径。

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Configuration Manager 升级到新版本后将重新生成默认启动映像
从此版本开始，如果升级 Windows ADK 版本，然后使用更新和服务安装 Configuration Manager 的最新版本，Configuration Manager 将重新生成默认启动映像。 这包括已更新的 Windows ADK 中的新 Window PE 版本、新版本的 Configuration Manager 客户端、驱动程序、自定义项等。不会修改自定义启动映像。 有关详细信息，请参阅[管理启动映像](/sccm/osd/get-started/manage-boot-images#BKMK_BootImageDefault)。

## <a name="software-updates"></a>软件更新

### <a name="deploy-office-365-apps-to-clients"></a>将 Office 365 应用部署到客户端
从版本 1702 起，可以从 Office 365 客户端管理仪表板启动 Office 365 安装程序，此程序可用于配置 Office 365 安装设置、从 Office 内容传送网络 (CDN) 下载文件，以及将文件部署为 Configuration Manager 中的应用程序。 有关详细信息，请参阅[管理 Office 365 ProPlus 更新](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)。

> [!IMPORTANT]
> 在 Configuration Manager 中使用 Office 365 应用程序向导创建和部署的 Office 365 应用不会由 Configuration Manager 自动管理，除非启用软件更新客户端代理设置“再次启用 Office 365 客户端管理”。 有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings)。

### <a name="manage-express-installation-files-for-windows-10-updates"></a>管理 Windows 10 更新的快速安装文件
从版本 1702 起，Configuration Manager 支持 Windows 10 更新的快速安装文件。 如果使用支持版本的 Windows 10，可通过 Configuration Manager 设置只下载本月的 Windows 10 累积更新和上月更新之间的更改。 在没有快速安装文件的情况下，Configuration Manager 每个月都会下载完整的 Windows 10 累积更新（包括先前月份的所有更新）。 使用快速安装文件，所需下载文件更小，在客户端上安装更快速。 有关详细信息，请参阅[管理 Windows 10 更新的快速安装文件](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)。


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>移动设备管理

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>在混合 MDM 的创建向导中，不再以 Android 和 iOS 版本为目标

从混合移动设备管理 (MDM) 的版本 1702 开始，创建用于 Intune 托管设备的新策略和配置文件时，不再需要将特定版本的 Android 和 iOS 作为目标。 转而选择下述某个设备类型：

- Android
- Samsung KNOX 标准版 4.0 及更高版本
- iPhone
- iPad

此更改会影响以下项的创建向导：

- 配置项目
- 相容性策略
- 证书配置文件
- 电子邮件配置文件
- VPN 配置文件
- Wi-Fi 配置文件

由于此更改，混合部署可为 Android 和 iOS 新版本更快提供支持，无需新的 Configuration Manager 版本或扩展。 Intune 独立版中支持新版本后，用户就可将其移动设备升级到此版本。

为防止从 Configuration Manager 先前版本升级时出现问题，移动操作系统版本仍在这些项的属性页中可用。 如果仍需以特定版本为目标，可创建新项，然后在新创建的项的属性页上指定目标版本。

### <a name="android-for-work-support"></a>Android for Work 支持
从 1702 开始，Microsoft Intune 的混合移动设备管理现在支持 Android for Work 设备注册和管理。 托管的 Android for Work 设备指南：

- [注册 Android for Work 设备](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)
- [批准和部署 Android for Work 应用](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [创建 Android for Work 配置项目](/sccm/mdm/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-for-work-configuration-items)
- [在 Android for Work 设备上执行选择性擦除](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)
- [Android for Work 的电子邮件配置文件](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Android for Work 的合规性策略](/sccm/mdm/deploy-use/create-compliance-policy)


### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>将批量采购的 iOS 应用部署到设备集合

现在可以将已授权的应用程序部署到设备以及用户。 根据应用对设备授权的支持能力，合适的许可证将在部署时按以下方式声明：

|||||
|-|-|-|-|
|Configuration Manager 版本|应用是否支持设备授权？|部署集合类型|已声明的许可证|
|早于 1702|是|用户|用户许可证|
|早于 1702|否|用户|用户许可证|
|早于 1702|是|设备|用户许可证|
|早于 1702|否|设备|用户许可证|
|1702 及更高版本|是|用户|用户许可证|
|1702 及更高版本|否|用户|用户许可证|
|1702 及更高版本|是|设备|设备许可证|
|1702 及更高版本|否|设备|用户许可证|

有关批量购买的 iOS 应用的详细信息，请参阅[管理批量购买的 iOS 应用](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)。

### <a name="support-for-ios-volume-purchase-program-for-education"></a>支持 iOS Volume Purchase Program 教育版

此外，现在可以部署并跟踪你从 iOS Volume Purchase Program 教育版购买的应用。
有关批量购买的 iOS 应用的详细信息，请参阅[管理批量购买的 iOS 应用](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)。

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>支持多个批量采购计划标记

现在可以将多个 Apple 批量采购计划令牌与 Configuration Manager 相关联。
有关批量购买的 iOS 应用的详细信息，请参阅[管理批量购买的 iOS 应用](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)。

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>对适用于企业的 Windows 应用商店中的业务线应用的支持

现在可以同步来自适用于企业的 Windows 应用商店的自定义业务线应用。

### <a name="conditional-access-device-compliance-policy-improvements"></a>条件性访问设备符合性策略改进

当用户使用非符合性应用列表中的应用时，新的设备符合性策略规则可用于帮助阻止对支持条件性访问的公司资源的访问。 当添加新的符合性规则“无法安装的应用”时，可由管理员定义非符合性应用列表。 将应用添加到非符合性列表时，此规则要求管理员输入“应用名称”、“应用 ID”和“应用发布者”（可选）。 此设置仅适用于 iOS 和 Android 设备。

此外，这可帮助组织缓解使用不安全应用导致的数据泄漏，并防止通过某些应用过度使用数据。

- 深入了解[设备符合性策略的工作原理](/sccm/mdm/deploy-use/device-compliance-policies)。
- 深入了解[如何创建设备符合性策略](/sccm/mdm/deploy-use/create-compliance-policy)。

### <a name="new-mobile-threat-defense-monitoring-tools"></a>新移动威胁防御监视工具

从版本 1702 开始，现在可以采用新的方法通过移动威胁防御服务提供程序来监视合规性状态。

- 了解[如何监视移动威胁防御合规性](https://docs.microsoft.com/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance)的详细信息。

## <a name="protect-devices"></a>保护设备

### <a name="detect-outdated-antimalware-client-versions"></a>检测过时的反恶意软件客户端版本
从版本 1702 开始，可以配置警报，以确保 Endpoint Protection 客户端不会过时。 有关详细信息，请参阅[过时的恶意软件客户端警报](/sccm/protect/deploy-use/endpoint-configure-alerts#detect-outdated-antimalware-client-versions)。

### <a name="device-health-attestation-updates"></a>设备运行状况证明更新
适用于本地客户端的设备运行状况证明服务现在可以从管理点进行配置和管理。 有关详细信息，请参阅[运行状况证明](/sccm/core/servers/manage/health-attestation)。

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Windows Hello 企业版的证书配置文件

如果想要在 Windows Hello 企业版密钥容器中存储证书配置文件，而证书配置文件使用智能卡登录 EKU，则必须配置密钥注册的权限，以确保证书验证正确。
有关详细信息，请参阅 [Windows Hello 企业版设置](/sccm/protect/deploy-use/windows-hello-for-business-settings)。

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>新的 Windows Hello 企业版最终用户通知
新的 Windows 10 通知告知最终用户必须采取额外操作才能完成 Windows Hello 企业版安装（例如，设置 PIN）。
