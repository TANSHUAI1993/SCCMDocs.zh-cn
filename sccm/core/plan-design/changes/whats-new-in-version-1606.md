---
title: "版本 1606 中的新增功能"
titleSuffix: Configuraton Manager
description: "获取有关 System Center Configuration Manager 的 1606 版中引入的更改和新功能的详细信息。"
ms.custom: na
ms.date: 12/30/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
caps.latest.revision: "40"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 346a1c7199a2d9dbb2cb174502adbb8d03a39f86
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2017
---
# <a name="what39s-new-in-version-1606-of-system-center-configuration-manager"></a>System Center Configuration Manager 1606 版中的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 的更新 1606 作为控制台内部更新提供，用于以前安装的、运行版本 1511 或 1602 的站点。 版本 1511 是用于安装新 Configuration Manager 站点的初始基准版本。
> [!TIP]  
>  了解详细信息：  
>   
>  -   [安装新站点](/sccm/core/servers/deploy/install)（使用基准版本，如 1511）  
>  -   [在站点上安装更新](/sccm/core/servers/manage/updates)（如更新 1602 或 1606）  

 以下各节提供有关 Configuration Manager 版本 1606 中引入的更改和新功能的详细信息。  



## <a name="updatesandservicing"></a>更新和维护服务

### <a name="changes-for-the-updates-and-servicing-node"></a>更新和维护服务节点的更改
Configuration Manager 控制台中的更新和维护服务节点更改如下：
> [!NOTE]
> 安装版本 1606 后，这些更改才可用。

- **节点名称更改：**

    在“监视”工作区中，已将“站点服务状态”节点重命名为“更新和服务状态”。
- **更多安装状态详细信息：**

    查看站点的更新安装状态时，控制台现在会显示以下操作的单独详细信息：
    - **下载**（这仅适用于安装服务连接点站点系统角色所在的顶层站点。）
    - **复制**
    - **先决条件检查**
    - **安装**

  此外，现提供了每个步骤的更详细信息，包括可查看详细信息的日志文件。  
-   **用于重试先决条件失败的新选项：**

    在“管理”和“监视”这两个工作区中，“更新和维护服务”节点都在功能区上包含了一个名为“忽略先决条件警告”的新按钮。

    如果安装更新时不使用“忽略先决条件警告”选项（位于更新向导中），更新安装会因出现警告而中止，之后可从功能区选择“忽略先决条件警告”。 这可触发更新的自动继续安装。  



- **更清楚的更新视图：**

    在“更新和维护服务”节点中，现在仅能看到最近安装的更新以及任何可供安装的新更新。 若要查看以前安装的更新，请单击显示在功能区中的新“历史记录”按钮。  

-   **重命名的预生产选项：**

    在“更新和维护服务”节点中，“客户端选项”按钮现称为“提升预生产客户端”。


###  <a name="pre-release-features"></a>预发行功能
从 1606 开始，必须同意使用 System Center Configuration Manager 中的预发行功能，然后才可以选择并启用它们。 有关详细信息，请参阅[使用更新中的预发行功能](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)。

### <a name="new-distribution-point-update-behavior"></a>新分发点更新行为
更新 1606 引入的更改可在安装将来更新时改进分发点的可用性。

安装更新 1606 后，下一次在需要自动重新安装标准和请求分发点站点系统角色的站点安装更新时，所有分发点将不再脱机以同时进行更新。 而站点服务器使用站点的内容分发设置，在任意给定时间将更新分发到分发点的子集。 结果只有某些分发点脱机以安装更新。 这允许尚未开始更新或已完成更新的分发点保持联机状态，并能够向客户端提供内容。



## <a name="accessibility"></a>辅助功能
若要在工作区的不同节点之间导航，现可输入节点名称的第一个字母。 每次按键都会将光标移动到以该字母开头的下一节点。 对于拥有屏幕阅读器的用户，阅读器会读出该节点的名称。 有关辅助功能选项的详细信息，请参阅 [System Center Configuration Manager 中的辅助功能](../../../core/understand/accessibility-features.md)。

## <a name="administration"></a>管理
Configuration Manager 控制台中的管理更改如下：
### <a name="oms-connector"></a>OMS 连接器

现在，可以将 Configuration Manager 作为集合从 System Center Configuration Manager 连接到 [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/en-us/documentation/articles/operations-management-suite-overview/)。 这使得 Configuration Manager 部署中的数据（例如集合）在 OMS 中可见。 有关详细信息，请参阅此处的[将数据从 Configuration Manager 同步到 Microsoft Operations Management Suite](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md)。

OMS 连接器是一种预发行功能。 若要启用此功能，请参阅[使用更新中的预发行功能](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)。

### <a name="support-for-cache-size-in-client-settings"></a>在客户端设置中支持缓存大小

现在，可以使用 Configuration Manager 控制台中的“客户端设置”在客户端计算机上配置缓存文件夹的大小。 以前，只能在安装或重新安装客户端软件时设置客户端缓存大小。 现在，可以将缓存大小指定为客户端设置（默认或自定义），然后将这些设置应用于客户端上的下一个策略更新，无需重新安装客户端。 有关详细信息，请参阅 [Configure the Client Cache for Configuration Manager Clients](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache)。

## <a name="on-premises-mobile-device-management"></a>本地移动设备管理

### <a name="support-for-multiple-device-management-points"></a>支持多个设备管理点

本地移动设备管理 (MDM) 现支持 Windows 10 周年更新中的一个新功能，该功能会自动将已注册设备配置为具有多个可供使用的设备管理点。 此功能允许设备在其正常使用的设备管理点不可用时回退到另一个设备管理点。 此功能仅适用于安装了 Windows 10 周年更新的电脑和设备。


## <a name="application-management"></a>应用程序管理

### <a name="manage-apps-from-the-windows-store-for-business"></a>管理来自适用于企业的 Windows 应用商店的应用

在[适用于企业的 Windows 应用商店](https://www.microsoft.com/business-store)中可以为组织查找并采购 Windows 应用（单个或批量）。 通过将应用商店连接到 Configuration Manager，可以同步已使用 Configuration Manager 购买的应用列表，在 Configuration Manager 控制台中查看这些应用，并像部署任何其他应用一样部署它们。

有关详细信息，请参阅[使用 System Center Configuration Manager 管理来自适用于企业的 Windows 应用商店的应用](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)。

### <a name="manage-ios-volume-purchased-apps"></a>管理 iOS 批量购买的应用

已改进管理批量购买的 iOS 应用以及使用 Configuration Manager 部署这些应用的工作流。

有关详细信息，请参阅[使用 System Center Configuration Manager 管理批量购买的 iOS 应用](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md)。

### <a name="software-center-user-interface"></a>软件中心用户界面

软件中心用户界面已简化，可实现更轻松的发现。
*  “安装状态”和“已安装的软件”选项卡已合并为一个“安装状态”选项卡。
*  “更新”、“操作系统”和“应用程序”已分为 3 个单独的选项卡。
* 现在可以一次选择多个更新进行安装，或者可以通过单击“全部安装”一次性安装所有更新。

### <a name="content-status-links"></a>内容状态链接
在应用程序或包的属性上，现有一个链接可以转到该对象的状态。

## <a name="software-updates"></a>软件更新

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>用于管理 Office 365 客户端代理的客户端设置
现在可以使用 Configuration Manager 客户端设置来管理 Office 365 客户端代理。 对此进行设置并部署 Office 365 更新后，Configuration Manager 客户端代理与 Office 365 客户端代理协作，从分发点下载并安装 Office 365 更新。

有关详细信息，请参阅[使用 Configuration Manager 管理 Office 365 ProPlus 更新](../../../sum/deploy-use/manage-office-365-proplus-updates.md)。

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>手动将客户端切换到新的软件更新点
现可启用供 Configuration Manager 客户端在活动软件更新点出现问题时切换到新软件更新点的选项。 启用后，客户端将在下次扫描时查找另一个软件更新点。

有关详细信息，请参阅[在 Configuration Manager 中规划软件更新](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs)。

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>在软件更新安装之后重启 Windows 10 客户端的选项
需要重启的软件更新已使用 Configuration Manager 进行部署并已安装在计算机上时，将计划挂起的重启。 还会显示重启对话框。 从 Configuration Manager 版本 1606 开始，只要 Configuration Manager 软件更新存在挂起的重启，就可使用“更新并重启”和“更新并关闭”选项。 Windows 10 计算机的 Windows 电源选项中提供这些选项。 使用这些选项中的某一个后，计算机重启后将不再显示重启对话框。

有关详细信息，请参阅[在 System Center Configuration Manager 中规划软件更新](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions)。

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>客户端安装软件更新并重启后，立即运行软件更新符合性扫描
现可在客户端安装软件更新并重启后，立即运行符合性扫描。 若要为部署进行此设置，请在部署软件更新向导的“用户体验”页上，选择“如果此部署中的任何更新需要重启系统，则在重启之后运行更新部署评估周期”。 这可使客户端检查在客户端重启之后变为适用状态的其他软件更新，然后在相同维护时段期间安装它们（并成为符合状态）。 有关详细信息，请参阅[自动部署软件更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)或[手动部署软件更新](/sccm/sum/deploy-use/manually-deploy-software-updates)。

## <a name="operating-system-deployment"></a>操作系统部署

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>任务序列步骤的改进：安装软件更新
使用“根据缓存的扫描结果评估软件更新”这一新设置可选择对软件更新进行完整扫描，而不是使用缓存的扫描结果。 有关详细信息，请参阅 [System Center Configuration 中的任务序列步骤](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)。

此外，还可使用新任务序列变量 **SMSTSSoftwareUpdateScanTimeout**。 通过此变量，可在安装软件更新任务序列步骤期间控制软件更新扫描的超时时间。 默认值为 30 分钟。 有关详细信息，请参阅 [System Center Configuration Manager 中的任务序列内置变量](../../../osd/understand/task-sequence-built-in-variables.md)。

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>已弃用 OSDPreserveDriveLetter 任务序列变量
已弃用 OSDPreserveDriveLetter 任务序列变量。 从 Configuration Manager 版本 1606 开始，默认情况下，Windows 安装程序会在操作系统部署期间确定要使用的最佳驱动器号（通常为 C:）。

有关详细信息，请参阅 [System Center Configuration Manager 中的任务序列内置变量](../../../osd/understand/task-sequence-built-in-variables.md)。

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>为已启用 PXE 的分发点自定义 RamDisk TFTP 窗口大小
现可以为已启用 PXE 的分发点自定义 RamDisk 窗口大小。 如果自定义了网络，则可能因窗口太大而出现超时错误，从而导致启动映像下载失败。 通过自定义 RamDisk 日常文件传输协议 (TFTP) 窗口大小，可在使用 PXE 时优化 TFTP 流量，以满足特定网络要求。

有关详细信息，请参阅[通过 System Center Configuration Manager 为操作系统部署准备站点系统角色](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)。

## <a name="compliance-settings"></a>符合性设置

### <a name="smart-lock-setting-for-android-devices"></a>适用于 Android 设备的 Smart Lock 设置
已将“允许 Smart Lock 和其他信任代理”这一新设置添加到 Android 和 Samsung KNOX Standard 配置项目。

此设置允许控制兼容的 Android 设备上的 Smart Lock 功能。 如果设备处于可信位置，则使用此手机功能（有时称为“信任代理”）可禁用或绕过设备锁屏界面密码。 例如，可信位置可能是它连接到特定蓝牙设备时，或者靠近 NFC 标签时。 可以使用此设置防止用户配置 Smart Lock。

有关详细信息，请参阅[如何为未使用 System Center Configuration Manager 客户端管理的 Android 和 Samsung KNOX 标准版设备创建配置项目](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)。

## <a name="device-configuration-and-protection"></a>设备配置和保护

### <a name="product-name-changes"></a>产品名称更改

* Microsoft Passport for Work 现被称为 **Windows Hello 企业版**。
* 企业数据保护现被称为 **Windows 信息保护**。

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Windows Hello 企业版 (Passport for Work) 的部署

现可将 Windows Hello 企业版策略部署到 Configuration Manager 客户端管理的、已加入域的 Windows 10 设备。

已更新 Configuration Manager 控制台，以便反映这些更改。

### <a name="ios-activation-lock"></a>iOS 激活锁定
Configuration Manager 可以帮助管理 iOS 激活锁定，这是适用于 iOS 7.1 及更高版本设备的“查找我的 iPhone”应用的功能。 启用激活锁定后，任何人都必须先输入用户的 Apple ID 和密码，然后才能执行以下操作：
* 关闭“查找我的 iPhone”。
* 擦除设备。
* 重新激活设备。

Configuration Manager 可以以下两种方法帮助你管理激活锁定：

- 在受到监督的设备上启用激活锁定。
- 在受到监督的设备上绕过激活锁定。

有关详细信息，请参阅[使用 System Center Configuration Manager 管理 iOS 激活锁](../../../mdm/deploy-use/manage-ios-activation-lock.md)。


### <a name="windows-defender-advanced-threat-protection"></a>Windows Defender 高级威胁防护

Endpoint Protection 可以帮助管理和监视 Windows Defender 高级威胁防护 (ATP)。 Windows Defender ATP 是一种新服务，可帮助企业检测、调查其网络上的高级攻击并做出响应。 Configuration Manager 策略可帮助载入和监视运行 Windows 10 版本 1607（内部版本 14328）或更高版本的托管计算机。

有关详细信息，请参阅[Windows Defender 高级威胁防护](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md)。

### <a name="device-categories"></a>设备类别
可创建设备类别，可将其用于配合使用 Configuration Manager 和 Microsoft Intune 时自动在设备集合中放置设备。 然后要求用户在 Intune 中注册设备时选择某个设备类别。 此外，还可从 Configuration Manager 控制台中更改设备类别。

有关详细信息，请参阅[如何使用 System Center Configuration Manager 自动将设备分类到集合](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md)。

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>预声明具有 IMEI 或 iOS 序列号的设备

可通过导入公司拥有设备的国际移动设备识别 (IMEI) 码或 iOS 序列号对此类设备进行识别。 可上传包含设备 IMEI 码的逗号分隔值 (.csv) 文件，或者手动输入设备信息。 导入的信息将用于设置在设备列表中作为“公司”注册的设备的所有权。 访问该服务的每位用户仍需要 Intune 许可证。

有关详细信息，请参阅[预声明具有 IMEI 或 iOS 序列号的设备](../../../mdm/deploy-use/predeclare-devices-with-hardware-id.md)。

### <a name="on-premises-health-attestation-service-communication"></a>本地运行状况证明服务通信

现在，可以仅使用本地基础结构对 Windows 10 电脑启用运行状况证明服务监视，使没有 Internet 访问权限的计算机可以报告设备运行状况证明 (DHA)。

有关详细信息，请参阅 [System Center Configuration Manager 的运行状况证明](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers)。  

## <a name="remote-control"></a>远程控制
在远程控制会话中从共享剪贴板传输内容前，允许用户选择接受或拒绝文件传输。 用户在每个会话中只需授予一次权限，而查看者无法授予自己继续文件传输的权限。 可在“管理”工作区中找到此新设置。 转到“客户端设置”，然后在“默认设置”中打开“远程工具”窗格。
