---
title: "新版本 1710 |Microsoft Docs"
titleSuffix: Configuration Manager
description: "获取有关 System Center Configuration Manager 的 1710 版中引入的更改和新功能的详细信息。"
ms.custom: na
ms.date: 11/20/2017
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 310343a6dff97b240b319bed59994349cbd9ae7d
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="what39s-new-in-version-1710-of-system-center-configuration-manager"></a>System Center Configuration Manager 版本 1710 的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager Current Branch 的更新 1710 作为控制台内更新提供，用于运行版本 1610、1702 或 1706 的以前安装的站点。

> [!TIP]  
> 若要安装新站点，必须使用 Configuration Manager 的基准版本。  
>  了解详细信息：    
>   - [安装新站点](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [在站点上安装更新](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [基准和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

以下各节提供有关 Configuration Manager 版本 1710 中引入的更改和新功能的详细信息。  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>站点基础结构

### <a name="updates-for-peer-cache-----sms500850---"></a>用于对等缓存的更新<!-- sms500850 -->
从这个版本开始，对等缓存不再属于预发行功能。  此版本中没有引入对等缓存的其他更改。 有关详细信息，请参阅[用于 Configuration Manager 客户端的对等缓存](/sccm/core/plan-design/hierarchy/client-peer-cache)。

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>对 Azure 政府云的云分发点支持<!-- sms491428 -->
现在可以在 Azure 政府云中使用[基于云的分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)。   


<!-- ## Migration  -->


## <a name="client-management"></a>客户端管理

### <a name="co-management-for-windows-10-devices"></a>适用于 Windows 10 设备的共同管理    
<!-- 1350871 -->
从 Windows 10 版本 1607（也称为周年更新）开始，可以将 Windows 10 设备同时联接到本地 Active Directory (AD) 和基于云的 Azure AD（混合 Azure AD）。 共同管理将利用此项改进，并使你能够同时使用 Configuration Manager 和 Intune 来管理 Windows 10 设备。 它是一种解决方案，在传统管理与现代管理之间架起一座桥梁，为你提供利用分阶段的方法实现转换的途径。 有关详细信息，请参阅[适用于 Windows 10 设备的共同管理](/sccm/core/clients/manage/co-management-overview)。

### <a name="restart-computers-form-the-configuration-manager-console-----1356283---"></a>从 Configuration Manager 控制台重启计算机<!-- 1356283 -->
从此版本开始，用户可以使用 Configuration Manager 控制台标识需要重启的客户端设备，然后使用客户端通知操作来重启它们。

请参阅[如何在 System Center Configuration Manager 中管理客户端](/sccm/core/clients/manage/manage-clients#restart-clients)


<!--  ## Compliance settings  -->


## <a name="application-management"></a>应用程序管理
### <a name="improvements-for-run-scripts------1236459---"></a>运行脚本的改进<!-- 1236459 -->
此版本中将多项改进引入**“运行脚本”**功能，可将 PowerShell 脚本部署为在托管设备上运行。 1706 版本首次引入了此功能。

改进包括：
- 采用安全作用域帮助控制使用“运行脚本”的人员
- 实时监视你运行的脚本
- 脚本参数显示在“创建脚本”向导、支持验证中，并标识为强制或可选。

有关使用“运行脚本”的详细信息，请参阅[创建和运行脚本](../../../apps/deploy-use/create-deploy-scripts.md)。

### <a name="new-mobile-application-management-policy-settings"></a>新移动应用程序管理策略设置
<!-- 1324760 -->
以下设置已添加到移动应用程序管理策略设置：
- **禁用联系人同步**：阻止应用将数据保存到设备上的本机“联系人”应用。
- **禁用打印**：阻止应用打印工作或学校数据。

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>软件中心不会再使大于 250 x 250 的图标失真  
<!-- 1356194 -->

在此版本中，软件中心不会再使大于 250 x 250 的图标失真。 软件中心曾使此类图标看起来很模糊。 现在图标的像素大小最大可设置为 512 x 512，并在显示时不会失真。

若要在软件中心添加你的应用图标，请参阅[创建应用程序](/sccm/apps/deploy-use/create-applications)。

## <a name="operating-system-deployment"></a>操作系统部署
 > [!TIP]   
 > <!-- 1354281 -->
 > 从 Windows 10 版本 1709（也称为 Fall Creators Update）开始，Windows Media 包括多个版本。 在配置用于使用操作系统升级包或操作系统映像的任务序列时，请务必选择[支持供 Configuration Manager 使用的版本](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client)。

### <a name="add-child-task-sequences-to-a-task-sequence"></a>将子任务序列添加到任务序列
<!-- 1261338 -->

可以添加一个运行其他任务序列的新任务序列步骤，该步骤在任务序列之间创建父/子关系。 这允许创建更多可重复使用的模块式任务序列。  

若要了解有关子任务序列的详细信息，请参阅[子任务序列](/sccm/osd/understand/task-sequence-steps#child-task-sequence)。

## <a name="software-center-customization"></a>软件中心自定义
<!-- 1351224 -->
可以添加企业品牌元素，并在“软件中心”上指定选项卡的可见性。 可以添加“软件中心”特定公司名称、设置“软件中心”配置颜色主题、设置公司徽标，并设置客户端设备的可见选项卡。

有关详细信息，请参阅[在 System Center Configuration Manager 中规划和配置应用程序管理](/sccm/apps/plan-design/plan-for-and-configure-application-management)。

## <a name="software-updates"></a>软件更新

### <a name="surface-driver-updates-----1098490---"></a>Surface 驱动程序更新<!-- 1098490 -->
从此版本开始，管理 Surface 驱动程序更新不再是预发行功能。  


## <a name="reporting"></a>报表

### <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>限制 Windows 10 增强遥测只发送与 Windows Analytics 设备运行状况相关的数据
<!-- 1356148 -->

现在可以将 Windows 10 遥测数据收集级别设置为“增强(受限)”。 该设置使你能够在环境中获得对设备的可操作见解，而无需设备通过 Windows 10 版本 1709 或更高版本报告“增强”遥测级别的所有数据。

有关详细信息，请参阅 [如何在 System Center Configuration Manager 中配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>移动设备管理

### <a name="windows-10-arm64-device-support"></a>Windows 10 ARM64 设备支持
<!-- 1355000 -->

运行 Windows 10 的 ARM64 设备支持混合移动设备管理 (MDM) 方案（当这些设备可用时）。

这些方案包括：

- [注册设备](../../../mdm/deploy-use/enroll-hybrid-windows.md)
- [执行远程的完全和选择性擦除操作](../../../mdm/deploy-use/wipe-lock-reset-devices.md)
- [通过配置项目和基线管理设置](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [管理符合性策略](../../../mdm/deploy-use/device-compliance-policies.md)
- 通过以下内容管理对公司资源的访问：
   - [证书配置文件](../../../mdm/deploy-use/create-pfx-certificate-profiles.md)
   - [VPN 配置文件](../../../mdm/deploy-use/create-vpn-profiles.md)
   - [Wi-Fi 配置文件](../../../mdm/deploy-use/create-wifi-profiles.md)
   - [电子邮件配置文件](../../../mdm/deploy-use/create-exchange-activesync-profiles.md)
- [配置 Windows Hello 企业版策略](../../../mdm/deploy-use/windows-hello-for-business-settings.md)
- [管理应用程序](../../../mdm/deploy-use/management-tasks-applications.md)

### <a name="improved-vpn-profile-experience-in-configuration-manager-console----1318232---"></a>Configuration Manager 控制台中改进了 VPN 配置文件体验<!-- 1318232 -->

在此版本中，我们更新了 VPN 配置文件向导和属性页，以显示选定平台相应的设置：


- 每个平台均有其自己的工作流，这意味着新的 VPN 配置文件仅包含平台支持的设置。
- 如今，“支持的平台”页在“常规”页后显示。  现在于设置属性值之前选择平台。
- 如果将平台设置为“Android”、“Android for Work”或“Windows Phone 8.1”，则不需要“支持的平台”页，该页也不会显示。
- 基于 Configuration Manager 客户端的工作流已与基于混合移动设备 (MDM) 客户端的 Windows 10 工作流相结合，它们支持相同的设置。
- 每个平台工作流仅包含适用于该工作流的设置。  例如，Android 工作流包含适用于 Android 的设置；Android 工作流中将不再显示适用于 iOS 或 Windows 10 移动版的设置。
- 对于 Windows 8.1 设备，只由 Configuration Manager 客户端管理（不由 Intune 支持）的连接类型进行了明确标记。
- “自动 VPN”页已过时且已删除。

这些更改适用于新的 VPN 配置文件。  

为把兼容性风险降至最低，现有的 VPN 配置文件保持不变。  编辑现有的配置文件时，设置将以创建该配置文件时的形式显示。  

更多详细信息，请参阅[System Center Configuration Manager 中移动设备上的 VPN 配置文件](../../../mdm/deploy-use/create-vpn-profiles.md)。

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>对下一代加密技术 (CNG) 证书的有限支持<!-- 1356191 -->

Configuration Manager 对下一代加密技术 (CNG) 证书提供有限支持。 Configuration Manager 客户端可以通过 CNG 密钥存储提供者 (KSP) 中的私钥使用 PKI 客户端身份验证证书。 通过 KSP 支持，Configuration Manager 客户端可支持基于硬件的私钥，如用于 PKI 客户端身份验证证书的 TPM KSP。

有关详细信息，请参阅 [CNG 证书概述](../network/cng-certificates-overview.md)。

## <a name="protect-devices"></a>保护设备

### <a name="create-and-deploy-exploit-guard-policies"></a>创建和部署攻击防护策略
<!-- 1355468 -->

可以[创建和部署策略](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)以管理 Windows Defender 攻击防护的全部四个组成部分，包括攻击面减少、受控文件夹访问权限、攻击防护和网络保护。

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>创建和部署 Windows Defender 应用程序防护策略
<!-- 1351960 -->

可以使用 Configuration Manager Endpoint Protection [创建和部署 Windows Defender 应用程序防护策略](/sccm/protect/deploy-use/create-deploy-application-guard-policy)。

### <a name="device-guard-policy-changes"></a>设备防护策略更改
<!-- 1355092 -->
下面是三个与设备防护策略相关的更改：

- 设备防护策略已被重命名为 Windows Defender 应用程序控制策略。 因此，举例来说，“创建设备防护策略”向导现命名为“创建 Windows Defender 应用程序控制策略”向导。
- 使用 Windows 版本 1709 Fall Creators Update 的设备无需重启就能应用 Windows Defender 应用程序控制策略。 重新启动仍是默认设置，但你可以[关闭重启](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)。
- 可以[将设备设置为自动运行](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)受 Intelligent Security Graph 信任的软件。





## <a name="next-steps"></a>后续步骤
准备好安装此版本时，请参阅 [Configuration Manager 的更新](/sccm/core/servers/manage/updates)。
