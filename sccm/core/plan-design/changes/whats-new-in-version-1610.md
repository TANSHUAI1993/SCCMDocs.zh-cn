---
title: "新版本 1610 |Microsoft Docs"
description: "获取有关 System Center Configuration Manager 的 1610 版中引入的更改和新功能的详细信息。"
ms.custom: na
ms.date: 11/23/2016
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
caps.latest.revision: "40"
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 8b80f4d14eafa4cbbfb083178a118bc0e71f4019
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-new-in-version-1610-of-system-center-configuration-manager"></a>System Center Configuration Manager 版本 1610 的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager Current Branch 的更新 1610 作为控制台内更新提供，用于运行版本 1511、1602 或 1606 的以前安装的站点。


> [!TIP]  
> 若要安装新站点，必须使用 Configuration Manager 的基准版本。  
>  了解详细信息：    
>  -   [安装新站点](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [在站点上安装更新](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [基准和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

以下各节提供有关 Configuration Manager 版本 1610 中引入的更改和新功能的详细信息。  


## <a name="in-console-monitoring-of-update-installation-status"></a>在控制台内部监视更新安装状态  
从 1610 版起，当安装更新包并在控制台中监视安装时，会有一个新阶段：**安装后**。 此阶段包括重新启动关键服务和复制监视初始化等任务的状态。 （在站点更新至版本 1610 之前，此阶段在控制台中不可用。）有关更新安装状态的详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)。


## <a name="exclude-clients-from-automatic-upgrade"></a>从自动升级中排除客户端
可以排除通过新版本客户端软件升级 Windows 客户端。 若要执行此操作，请将客户端计算机包括在指定要从升级中排除的集合中。 排除的集合中的客户端会忽略升级客户端软件的请求。  有关详细信息，请参阅[从升级中排除 Windows 客户端](../../clients/manage/upgrade/exclude-clients-windows.md)。


## <a name="improvements-for-boundary-groups"></a>边界组的改进
版本 1610 介绍了对边界组做出的重要更改以及它们如何与分发点配合使用。 这些更改可简化内容基础结构的设计，同时使你更好地控制客户端如何以及何时回退以搜索更多分发点作为内容源位置。 这包括位于本地和基于云的分发点。
这些改进会替代你可能熟悉的概念和行为（如将分发点配置为快速或慢速）。 新模型应更易设置和维护。 这些更改也是未来更改的基础，以后还将改进与边界组相关联的其他站点系统角色。

在升级到版本 1610 期间，升级将转换你的当前边界组配置，以适应新的模型，以便这些更改不会妨碍现有内容分发配置。

有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups)。


## <a name="peer-cache-for-content-distribution-to-clients"></a>用于向客户端进行内容分发的对等缓存
从 1610 版起，客户端**对等缓存**可帮助管理对远程客户端内容的部署。 对等缓存是内置 Configuration Manager 解决方案，供客户端用于直接从本地缓存将内容与其他客户端共享。

将启用对等缓存的客户端设置部署到集合后，该集合的成员可以充当同一边界组中其他客户端的对等内容源。

还可以使用新的“客户端数据源”仪表板，来了解环境中对等缓存内容源的使用。

> [!TIP]  
> 1610 版本中，对等缓存和“客户端数据源”仪表板均为预发行功能。 若要启用这些功能，请参阅[使用更新中的预发行功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。

有关详细信息，请参阅[用于 Configuration Manager 客户端的对等缓存](/sccm/core/plan-design/hierarchy/client-peer-cache)和[客户端数据源仪表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>同时迁移多个共享分发点
现在可以通过该选项**重新分配分发点**以便 Configuration Manager 可同时并行处理最多 50 个共享分发点的重新分配。 在此版本之前，每次只能处理一个分发点的重新分配。 有关详细信息，请参阅[同时迁移多个共享分发点](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time)。

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>用于管理基于 Internet 的客户端的云管理网关

云管理网关提供一种简单的方法来管理 Internet 上的 Configuration Manager 客户端。 云管理网关服务部署到 Microsoft Azure 且需要 Azure 订阅，它使用名为云管理网关连接点的新角色连接到本地 Configuration Manager 基础结构。 服务完全部署并配置好后，客户端可以与本地 Configuration Manager 站点系统角色和基于云的分发点通信，而不管它们是连接到内部专用网络还是 Internet 上。 有关详细信息，及云管理网关与基于 Internet 的客户端管理之间的比较，请参阅[管理 Internet 上的客户端](/sccm/core/clients/manage/manage-clients-internet)。

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Windows 10 版本升级策略的改进
在此版本中，已对此策略类型进行了以下改进：

- 现在，除了已向 Microsoft Intune 注册的 Windows 10 电脑之外，还可以对运行 Configuration Manager 客户端的 Windows 10 电脑使用版本升级策略。
- 可以从 Windows 10 专业版升级到与你的硬件兼容的向导中的任何平台。

## <a name="manage-hardware-identifiers"></a>管理硬件标识符
现在可以提供 Configuration Manager 为实现 PXE 启动和客户端注册而应忽略的硬件 ID 列表。 这可以帮助解决两个常见问题：

1. 许多设备（如 Surface Pro 3）不包含板载以太网端口。 为部署操作系统，通常会使用 USB 到以太网适配器来建立有线连接。 但是，出于成本和一般可用性的考虑，这些适配器通常会共享使用。 由于此适配器的 MAC 地址用于标识设备，因此在每次部署之间若无额外的管理员操作，重用适配器就会出现问题。 现在在 Configuration Manager 版本 1610 中，可排除此适配器的 MAC 地址，以便在此种情况下轻松重用该适配器。
2. 虽然 SMBIOS ID 应是唯一的硬件标识符，但是某些特殊硬件设备自身具有重复 ID。 此问题可能不如上述的 USB 到以太网适配器方案那样常见，但可以通过使用已排除的硬件 ID 列表来解决此问题。

有关详细信息，请参阅[管理重复硬件标识符](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers)。

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>适用于企业的 Windows 应用商店与 Configuration Manager 集成的增强功能
此版本中的更改：
- 以前，你仅可以从适用于企业的 Windows 应用商店部署免费的应用程序。 Configuration Manager 现在还支持部署在线支付许可应用（仅适用于注册了 Intune 的设备）。
- 现在你可启动适用于企业的 Windows 应用商店和 Configuration Manager 之间的即时同步。
- 现在可修改从 Azure Active Directory 获取的客户端密钥。
- 可以删除对应用商店的订阅。

有关详细信息，请参阅[使用 System Center Configuration Manager 管理来自适用于企业的 Windows 应用商店的应用](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)。


## <a name="policy-sync-for-intune-enrolled-devices"></a>已注册 Intune 的设备的策略同步
现在可以从 Configuration Manager 控制台中为已注册 Intune 的设备请求策略同步，而无需在设备本身的公司门户应用中请求同步。 同步请求状态信息可用作设备视图中的新列，称为**远程同步状态**。 每台设备的“属性”对话框的“发现数据”部分也会提供此信息。
有关详细信息，请参阅[从 Configuration Manager 控制台中远程同步已注册 Intune 的设备上的策略](/sccm/mdm/deploy-use/sync-intune-device)。


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>使用符合性设置来配置 Windows Defender 设置
现在可以在 Configuration Manager 控制台中，使用配置项目在注册有 Intune 的 Windows 10 计算机上配置 Windows Defender 客户端设置。
有关详细信息，请参阅[为不使用 System Center Configuration Manager 客户端管理的 Windows 8.1 和 Windows 10 设备创建配置项目](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)中的 **Windows Defender** 部分。



## <a name="general-improvements-to-software-center"></a>对软件中心的一般改进
- 用户现在可以从软件中心以及应用程序目录中请求应用。
- 通过改进，现可帮助用户了解哪些是最新且相关的软件。

## <a name="new-columns-in-device-collection-views"></a>设备集合视图中的新列
现在，可以在设备集合视图中显示 **IMEI** 和**序列号**（针对 iOS 设备）的列。
有关详细信息，请参阅[预声明具有 IMEI 或 iOS 序列号的设备](https://docs.microsoft.com/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)。

## <a name="customizable-branding-for-software-center-dialogs"></a>软件中心自定义品牌对话框
Configuration Manager 版本 1602 中引入了软件中心的自定义品牌。 在版本 1610 中，现已将该品牌功能扩展到所有关联的对话框，以便为软件中心用户提供更一致的体验。

根据以下规则应用软件中心的自定义品牌：

- 如果未安装应用程序目录网站点站点服务器角色，则软件中心将显示“计算机代理”客户端设置 -“软件中心中显示的组织名称” - 中指定的组织名称。 有关说明，请参阅[如何配置客户端设置](../../clients/deploy/configure-client-settings.md)。

- 如果已安装应用程序目录网站点站点服务器角色，则软件中心将显示在应用程序目录网站点站点服务器角色属性中指定的组织名称和颜色。 有关详细信息，请参阅[应用程序目录网站点的配置选项](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#Application-Catalog-website-point)。

- 如果已配置 Microsoft Intune 订阅并将其连接到 Configuration Manager 环境，则软件中心将显示 Intune 订阅属性中指定的组织名称、颜色和公司徽标。 有关详细信息，请参阅 [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription)。


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>所需的应用程序和软件更新部署的强制宽限期
在某些情况下，可能会希望为用户提供更多时间（超出所设置的任何截止时间）来安装所需的应用程序部署或软件更新。 例如，当一台计算机关闭的时间过长和计算机需要安装大量应用程序或更新部署时，可能会需要执行这种操作。 例如，如果最终用户刚从假期返回，则他们可能需要等待很长时间，因为安装的应用程序部署已过期。 为了帮助解决此问题，现在可通过将 Configuration Manager 客户端设置部署到集合来定义强制的宽限期。 

若要配置宽限期，请执行以下操作：
1.      在客户端设置的“计算机代理”页上，将“部署截止时间后强制的宽限期(小时)”这一新属性的值配置为介于 **1** 和 **120** 小时之间。
2.      在新的所需应用程序部署中，或在现有部署属性中，在“计划”页上，选中复选框“根据用户首选项延迟此部署的强制执行”，延迟时间以客户端设置中定义的宽限期为依据。 选中了此复选框并针对其中部署了客户端设置的设备的所有部署都将使用此强制宽限期。

如果配置强制宽限期，并选中该复选框，则当到达应用程序安装截止时间后，将在用户按照宽限期配置的第一个非业务窗口中安装该应用程序。 但是，用户仍可打开软件中心并在任何所需时间安装该应用程序。 一旦过了宽限期，对于未完成的部署，强制将恢复为正常行为。 已将类似的选项添加到软件更新部署向导、自动部署规则向导和属性页中。



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>有关所需软件的对话框的功能改进
当用户收到来自“暂停并提醒我：”设置的所需软件后，可以从下面的下拉值列表中进行选择： 
- **以后**。 指定根据客户端代理设置中配置的通知设置安排通知。
- **固定时间**。 指定在选定时间（比如 30 分钟）之后再次显示通知。

![客户端代理设置中的计算机代理页](media/client-notification-settings.png)

最大暂停时间取决于“客户端代理”设置中配置的通知值。 例如，如果将计算机代理页上的“部署截止时间大于 24 小时，请提醒用户，提醒间隔时间（小时）为”设置配置为 10 小时，且距离截止时间超过 24 小时，则用户将看到一组暂停选项，暂停时间最多不超过 10小时。 随着截止时间的临近，可用的选项会变少，与部署时间轴的每个组件的相关客户端代理设置相一致。

此外，对于高风险部署，如用于部署操作系统的任务序列，用户会更频繁地收到通知。 这不是临时性的任务栏通知，每次通知用户需要维护关键软件后，用户的电脑上会显示类似于以下对话框：

![所需软件对话框](media/client-toast-notification.png)


更多相关信息：
- [用于管理高风险部署的设置](../../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [如何配置客户端设置](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>软件更新仪表板
可使用新的软件更新仪表板查看组织中设备的当前符合性状态，并快速分析数据以确定哪些设备处于风险中。 若要查看仪表板，请导航到“监视” > “概述” > “安全性” > “软件更新仪表板”。

有关详细信息，请参阅[监视软件更新](/sccm/sum/deploy-use/monitor-software-updates)。


## <a name="improvements-to-the-application-request-process"></a>对应用程序请求过程的改进
批准安装应用程序后，可随后在 Configuration Manager 控制台中通过单击“拒绝”选择拒绝该请求。 以前，批准后此按钮为灰显。

执行此操作不会从任何设备卸载应用程序。 但是，它会阻止用户从软件中心安装应用程序的新副本。

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>按自动部署规则中的内容大小进行筛选
现在可以对自动部署规则中软件更新的内容大小进行筛选。 例如，可以将“内容大小 (KB)”筛选器设置为 **< 2048**，以仅下载小于 2 MB 的软件更新。 使用此筛选器可防止自动下载较大的软件更新，以便在带宽受到限制时更好地支持简化的 Windows 低级别维护。 有关详细信息，请参阅：
- [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)（低级别操作系统上的 Configuration Manager 和简化的 Windows 维护服务）
- [自动部署软件更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)

若要配置“内容大小 (KB)”字段，请执行下列操作之一：
- 当创建自动部署规则时，请在“创建自动部署规则”向导中转到“软件更新”页。
- 在现有自动部署规则的属性中，请转到“软件更新”选项卡。

## <a name="office-365-client-management-dashboard"></a>Office 365 客户端管理仪表板
现在可以在 Configuration Manager 控制台中使用 Office 365 客户端管理仪表板。 若要查看该仪表板，请转到“软件库” > “概述” > “Office 365 客户端管理”。

仪表板显示以下内容的图表：

- Office 365 客户端数
- Office 365 客户端版本
- Office 365 客户端语言
- Office 365 客户端通道     

有关详细信息，请参阅[管理 Office 365 ProPlus 更新](/sccm/sum/deploy-use/manage-office-365-proplus-updates)。

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>管理 BIOS 转换为 UEFI 所采用的任务序列步骤
现在可以使用新的变量 TSUEFIDrive 自定义操作系统部署任务的序列，以便“重启计算机”步骤为到 UEFI 的转换在硬盘驱动器上准备 FAT32 分区。 以下过程提供了有关如何创建任务序列步骤以便为 BIOS 到 UEFI 的转换准备硬盘驱动器的示例。 有关详细信息，请参阅[管理 BIOS 转换为 UEFI 所采用的任务序列步骤](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)。

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>任务序列步骤的改进：准备 ConfigMgr 客户端以便捕获  
“准备 ConfigMgr 客户端”一步现在将完全删除 Configuration Manager 客户端，而不是仅删除密钥信息。 任务序列每次部署捕获的操作系统映像时，都将安装新的 Configuration Manager 客户端。 有关详细信息，请参阅[任务序列步骤](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)。



## <a name="intune-compliance-policy-charts"></a>Intune 合规性策略图表
现可通过使用 Configuration Manager 控制台中“监视”工作区下的新图表快速查看设备的总体合规性以及不合规的主要原因。 可以单击图表中的某个分区向下钻取，以查看该类别中的设备列表。 有关详细信息，请参阅[监视合规性策略](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)。


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>集成了 Lookout，以获得保护 iOS 和 Android 设备的混合实现
Microsoft 与 Lookout 的移动威胁防护解决方案集成，通过检测设备上的恶意软件和风险应用等，来保护 iOS 和 Android 移动设备。 Lookout 的解决方案可帮助确定威胁级别，它是可配置的。 可以在 System Center Configuration Manager 中创建合规性策略规则，以根据 Lookout 的风险评估确定设备合规性。 使用条件访问策略，可以根据设备合规性状态允许或阻止对公司资源的访问。 若要了解集成和它的工作原理，请参阅[根据设备、网络和应用程序风险管理访问权限](/sccm/protect/deploy-use/manage-access-based-on-device-network-app-risk)。

系统将提示不合规 iOS 设备的用户进行注册。 将要求这些用户在自己的设备上安装 Lookout for Work 应用、激活应用并修正 Lookout for Work 应用程序中报告的威胁，以获取对公司数据的访问权限。 了解如何[配置和部署 Lookout for Work 应用](/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps)。



## <a name="new-compliance-settings-for-configuration-items"></a>配置项目的新符合性设置
可将配置项目中的许多新设置用于各种设备平台。 这些设置之前存在于 Microsoft Intune 的独立配置中，现在结合使用 Intune 和 Configuration Manager 时可以使用这些设置。
有关详细信息，请参阅[不使用 System Center Configuration Manager 客户端管理的设备配置项目](/sccm/compliance/deploy-use/configuration-items-for-devices-managed-without-the-client)。

### <a name="new-settings-for-android-devices"></a>适用于 Android 设备的新设置
#### <a name="password-settings"></a>密码设置
- **记住密码历史**
- **允许指纹解锁**

#### <a name="security-settings"></a>安全设置
- **需要对存储卡进行加密**
- **允许屏幕捕获**
- **允许提交诊断数据**

#### <a name="browser-settings"></a>浏览器设置
- **允许使用 Web 浏览器**
- **允许自动填充**
- **允许使用弹出窗口阻止程序**
- **允许使用 Cookie**
- **允许使用活动脚本**

#### <a name="app-settings"></a>应用设置
- **允许使用 Google Play 商店**

#### <a name="device-capability-settings"></a>设备功能设置
- **允许使用可移动存储**
- **允许使用 Wi-Fi tethering**
- **允许使用地理位置**
- **允许使用 NFC**
- **允许使用蓝牙**
- **允许语音漫游**
- **允许数据漫游**
- **允许 SMS/MMS 消息传送**
- **允许使用语音助手**
- **允许语音拨号**
- **允许复制和粘贴**

### <a name="new-settings-for-ios-devices"></a>适用于 iOS 设备的新设置
#### <a name="password-settings"></a>密码设置
- **密码中所需的复杂字符数**
- **允许简单密码**
- **需要提供密码之前处于非活动状态的分钟数**
- **记住密码历史**

### <a name="new-settings-for-mac-os-x-devices"></a>适用于 Mac OS X 设备的新设置
#### <a name="password-settings"></a>密码设置
- **密码中所需的复杂字符数**
- **允许简单密码**
- **记住密码历史**
- **屏幕保护程序激活前处于非活动状态的分钟数**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>适用于 Windows 10 桌面和移动版设备的新设置
#### <a name="password-settings"></a>密码设置
- **最小字符集数**
- **记住密码历史**
- **当设备从空闲状态返回时需要密码**

#### <a name="security-settings"></a>安全设置
- **需要对移动设备加密**
- **允许手动取消注册**

#### <a name="device-capability-settings"></a>设备功能设置
- **允许通过移动电话网络使用 VPN**
- **允许在通过移动电话网络漫游时使用 VPN**
- **允许重置手机**
- **允许使用 USB 连接**
- **允许使用 Cortana**
- **允许操作中心通知**

### <a name="new-settings-for-windows-10-team-devices"></a>适用于 Windows 10 协同版设备的新设置
#### <a name="device-settings"></a>设备设置
- **启用 Azure Operational Insights**
- **启用 Miracast 无线投影**
- **选择“欢迎”屏幕上显示的会议信息**
- **锁屏背景图像 URL**

### <a name="new-settings-for-windows-81-devices"></a>适用于 Windows 8.1 设备的新设置
#### <a name="applicability-settings"></a>适用性设置
- **将所有配置应用到 Windows 10**

#### <a name="password-settings"></a>密码设置
- **所需的密码类型**
- **最小字符集数**
- **最短密码长度**
- **擦除设备前允许的重复登录失败次数**
- **屏幕关闭前处于不活动状态的分钟数**
- **密码过期（天数）**
- **记住密码历史**
- **防止重用以前的密码**
- **允许图片密码和 PIN**

#### <a name="browser-settings"></a>浏览器设置
- **允许自动检测 Intranet 网络**

### <a name="new-settings-for-windows-phone-81-devices"></a>适用于 Windows Phone 8.1 设备的新设置
#### <a name="applicability-settings"></a>适用性设置
- **将所有配置应用到 Windows 10**

#### <a name="password-settings"></a>密码设置
- **最小字符集数**
- **允许简单密码**
- **记住密码历史**

#### <a name="device-capability-settings"></a>设备功能设置
- **允许自动连接到免费 Wi-Fi 热点**
