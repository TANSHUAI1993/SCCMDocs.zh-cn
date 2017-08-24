---
title: "System Center Configuration Manager 版本 1602 中的新功能 | Microsoft Docs"
description: "获取有关 System Center Configuration Manager 的 1602 版中引入的更改和新功能的详细信息。"
ms.custom: na
ms.date: 12/30/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 9a548f43625a907173e7b967d26356bd80f1c5d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>System Center Configuration Manager 版本 1602 中的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*


System Center Configuration Manager 的更新 1602 作为控制台内部更新提供，用于以前安装的、运行版本 1511 的站点。 版本 1511 是用于安装新 Configuration Manager 站点的初始基准版本。  


> [!TIP]  
>  了解详细信息：  
>   
>   -   [安装新站点](/sccm/core/servers/deploy/install)（使用基准版本，如 1511）  
>   -   [在站点上安装更新](/sccm/core/servers/manage/updates)（如更新 1602）  

 以下各节提供有关 Configuration Manager 版本 1602 中引入的更改和新功能的详细信息。  

## <a name="site-infrastructure"></a>站点基础结构  

###  <a name="bkmk_UpgradeOS"></a>就地升级运行 Windows Server 2008 R2 的站点服务器的操作系统  
 运行版本 1602 或更高版本的 Configuration Manager 站点支持站点服务器的操作系统从 Windows Server 2008 R2 就地升级到 Windows Server 2012 R2。  

> [!WARNING]  
>  升级到 Windows Server 2012 R2 之前，必须从服务器中卸载 WSUS 3.2。  
>   
>  有关此关键步骤的信息，请参阅 Windows Server 文档中 [Windows Server 更新服务概述](https://technet.microsoft.com/library/hh852345.aspx)中的“新增和更改的功能”部分。  

 若要升级服务器，请使用 Windows Server 2012 R2 升级过程。 升级后不需要运行 Configuration Manager 站点服务器还原。 有关升级过程，请参阅 Windows Server 文档中的 [Windows Server 2012 R2 的升级选项](https://technet.microsoft.com/library/dn303416.aspx)。  

###  <a name="bkmk_AOAG"></a> SQL Server AlwaysOn 可用性组  
 使用 SQL Server AlwaysOn 可用性组，以承载主站点和管理中心站点上的站点数据库作为高可用性和灾难恢复解决方案。  

 有关详细信息，请参阅[通过 SQL Server AlwaysOn 实现适用于 System Center Configuration Manager 的高可用性站点数据库](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。  

## <a name="operating-system-deployment"></a>操作系统部署  

### <a name="windows-10-servicing"></a>Windows 10 维护服务  
 Configuration Manager 1602 版新增了以下 Windows 10 维护服务的改进功能：  

-   为维护服务计划提供了新筛选器选项，可用于筛选“语言”、“必需”和“标题”。 只有满足指定条件的升级项才会添加到关联部署中。  

-   对软件更新同步选择“升级”时，将会显示警告。 此警告将说明：必须首先具有适用于 Windows Server Update Services (WSUS) 4.0 的[修补程序 3095113](https://support.microsoft.com/kb/3095113)，而后同步软件才能成功更新以及 Windows 10 维护服务才能正常工作。 从警告消息中可以转到关联的知识库文章。  

-   可用的 Windows 10 升级现在仅显示在 Configuration Manager 控制台的“Windows 10 维护服务” \ “所有 Windows 10 更新”节点中。 这些更新不再显示在控制台的“软件更新” \ “所有软件更新”节点中。  

-   维护服务计划被视为高风险部署，“选择集合”窗口将仅显示满足在站点属性中配置的部署验证设置的自定义集合。 有关详细信息，请参阅 [Settings to manage high-risk deployments for System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md)。  

-   现在 Windows 10 升级包的用户将收到一条消息，告知他们正在升级操作系统。  

## <a name="application-management"></a>应用程序管理  

### <a name="ios-app-configuration-policies"></a>iOS 应用配置策略  
 使用 Configuration Manager 应用配置策略可提供用户在运行 iOS 应用时可能需要的设置。 例如，应用可能要求用户指定自定义端口号、语言、安全性设置或品牌设置（如公司徽标）。 如果输入的这些设置不正确，可能会加重支持人员的负担并降低新应用的采用率。  

 通过让你在运行应用之前将策略中的这些设置部署给用户，应用配置策略可消除此类问题。 随后这些设置会自动提供，用户无需执行任何操作。 有关详细信息，请参阅[在 System Center Configuration Manager 中使用应用配置策略配置 iOS 应用](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md)。  

### <a name="manage-volume-purchased-ios-apps"></a>Manage volume-purchased iOS apps  
 Configuration Manager 可帮助部署和管理从 Apple Volume-Purchase Program (VPP) 中批量购买的应用。 Configuration Manager 从应用商店中导入许可证信息，然后跟踪用户使用的许可证数量。  

 有关详细信息，请参阅[使用 System Center Configuration Manager 管理批量购买的 iOS 应用](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md)。  

### <a name="automatic-creation-of-office-mobile-apps"></a>自动创建 Office 移动应用  
 从版本 1511 升级到版本 1602 时，Configuration Manager 将自动创建适用于 Android 和 iOS 的以下 Microsoft Office 移动应用：  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote（仅限 iOS）  

-   Microsoft Outlook  

可在 Configuration Manage 控制台的“应用程序”节点中找到这些应用。  

 关于部署应用程序的详细信息，请参阅[如何使用 System Center Configuration Manager 部署应用程序](../../../apps/deploy-use/deploy-applications.md)。  

## <a name="software-updates"></a>软件更新  

### <a name="manage-office-365-client-updates"></a>管理 Office 365 客户端更新  
 System Center Configuration Manager 现在能够通过使用软件更新管理工作流来管理 Office 365 客户端更新。 有关详细信息，请参阅[使用 System Center Configuration Manager 管理 Office 365 ProPlus 更新](/sccm/sum/deploy-use/manage-office-365-proplus-updates)。  

## <a name="compliance-settings"></a>符合性设置  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>运行 Windows 10 Team 的设备的符合性设置  
 新设置已添加到 **Windows 8.1 和 Windows 10** 配置项中。 这些设置有助于控制运行 Windows 10 Team 的设备，如 Surface Hub 设备。  

 有关详细信息，请参阅[如何为没使用 System Center Configuration Manager 客户端管理的 Windows 8.1 和 Windows 10 设备创建配置项目](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)。  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Android Samsung KNOX 标准版设备的展台模式设置  
 展台模式允许锁定设备以便只允许某些功能工作。 例如，可以让设备只运行一个指定的托管应用，也可以禁用设备上的音量按钮。 这些设置可用于设备的演示模型，也可用于专门执行一个功能的设备（如销售点设备）。 在 Configuration Manager 中，现可指定 Samsung KNOX 标准版设备的展台模式设置。  

 有关详细信息，请参阅[如何为未使用 System Center Configuration Manager 客户端管理的 Android 和 Samsung KNOX 标准版设备创建配置项目](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)。  

## <a name="conditional-access"></a>条件性访问  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>对由 System Center Configuration Manager 管理的电脑进行条件访问  
 此版本之前，若要配置电脑的条件访问，则该电脑必须已在 Intune 中注册或为已加入域。 从 1602 更新开始，支持对由 System Center Configuration Manager 管理的电脑进行条件访问。 对于由 System Center Configuration Manager 管理的电脑，可将对 Exchange Online 和 SharePoint Online 的访问限制为仅限符合你设置的合规性策略的设备。  

 有关详细信息，请参阅[管理对由 System Center Configuration Manager 管理的电脑的 O365 服务的访问](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)。  

### <a name="restricting-access-based-on-the-health-of-devices"></a>基于设备的运行状况限制访问  
 现可根据运行状况证明服务所报告的设备的运行状况来限制对电子邮件和 0ffice 365 服务的访问。 此外，设备健康状况报告还包括由 Intune 管理的设备。  

 Configuration Manager 控制台中添加了新的合规性规则，该规则允许根据设备的运行状况状态指定应允许还是阻止访问设备。 有关运行状况证明服务及如何在 Intune 中报告设备的运行状况的详细信息，请参阅 [System Center Configuration Manager 的运行状况证明](../../../core/servers/manage/health-attestation.md)。  

### <a name="new-compliance-policy-rules"></a>新的合规性策略  
 为对更高的安全性要求提供支持，已添加自动更新和要求使用密码解锁设备等新的合规性策略规则。

 有关详细信息，请参阅 [System Center Configuration Manager 中的设备合规性策略](../../../protect/deploy-use/device-compliance-policies.md)。  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>确保已注册且合规的设备始终有权访问 Exchange 内部部署  
 选中以下选项时，允许已在 Intune 中注册且符合合规性策略的设备访问 Exchange 内部部署：**默认规则覆盖 - 始终允许已注册 Intune 且合规的设备访问 Exchange 内部部署**。 Exchange 内部部署的“配置条件访问策略向导”的“常规页面”提供了此规则。

 此规则将覆盖“默认规则”，这意味着，即使将“默认规则”设置为隔离或阻止访问，已注册并符合要求的设备也仍然能够访问内部部署的 Exchange。 当你希望已注册且合规的设备始终可通过内部部署的 Exchange 访问电子邮件时，使用该设置。   

 有关详细的演练，请参阅[在 System Center Configuration Manager 中管理对电子邮件的访问](../../../protect/deploy-use/manage-email-access.md)。  

## <a name="client-management"></a>客户端管理  

### <a name="client-online-status"></a>客户端联机状态  
 提供了用于监视计算机是否处于联机状态的客户端的新状态。 如果计算机连接到其已分配的管理点，则将其视为联机。 为指示计算机处于联机状态，客户端将向管理点发送类似 ping 的消息。 如果管理点在 5 分钟后未收到消息，则将客户端视为处于脱机状态。  

 有关详细信息，请参阅[如何在 System Center Configuration Manager 中监视客户端](../../../core/clients/manage/monitor-clients.md)。  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>从软件中心刷新 PC 计算机和用户策略  
 已将新选项“同步策略”添加到软件中心的“选项” > “计算机维护”页面，该操作可让电脑刷新其 Configuration Manager 计算机和用户策略。  

### <a name="software-center-branding-changes"></a>软件中心品牌更改  
 你可以更改软件中心内显示的颜色、组织名称和图标。 根据以下规则应用这些设置：  

- 如果未安装应用程序目录网站点站点服务器角色，则软件中心将显示“计算机代理”客户端设置中指定的组织名称，称为“软件中心中显示的组织名称”。  

- 如果已安装应用程序目录网站点站点服务器角色，则软件中心将显示在应用程序目录网站点站点服务器角色属性中指定的组织名称和颜色。  

- 如果已配置 Microsoft Intune 订阅并将其连接到 Configuration Manager 环境，则软件中心将显示 Intune 订阅属性中指定的组织名称、颜色和公司徽标。  

### <a name="health-attestation"></a>运行状况证明  
 管理员可以在 Configuration Manager 控制台中查看 Windows 10 设备运行状况证明的状态。 此功能适用于 Configuration Manager 和带 Microsoft Intune 的 Configuration Manager。 设备运行状况证明让管理员能够确保客户端计算机启用以下可信 BIOS、TPM 和启动软件配置：  

-   开机初期启动的反恶意软件  

-   BitLocker  

-   安全启动  

-   代码完整性  

有关详细信息，请参阅 [System Center Configuration Manager 的运行状况证明](../../../core/servers/manage/health-attestation.md)。  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Endpoint Protection 反恶意软件设置的改进  
 在 1602 中，我们在 Windows Defender 的 Endpoint Protection 反恶意软件策略中添加了以下新设置：  

-   实时保护：在下载时和安装前阻止可能不需要的应用程序。  

-   扫描设置：在完全扫描期间扫描映射的网络驱动器。  

-   自动示例文件提交配置：  

     反恶意软件引擎可能会请求将文件示例发送到 Microsoft 供进一步分析。 默认情况下，发送此类示例之前将始终给出提示。 管理员现在可以管理以下设置以配置此行为：  

    -   高级：启动自动示例文件提交以帮助 Microsoft 确定某些检测到的项目是否恶意。  

    -   高级：允许用户修改自动示例文件提交设置。  

    此外，在 Endpoint Protection 反恶意软件政策的“排除设置”部分中，现有“排除文件和文件夹”设置现在允许设备排除。  

有关详细信息，请参阅[如何在 System Center Configuration Manager 中为 Endpoint Protection 创建和部署反恶意软件策略](../../../protect/deploy-use/endpoint-antimalware-policies.md)。  

## <a name="mobile-device-management"></a>移动设备管理  

### <a name="ios-activation-lock"></a>iOS 激活锁定  
 Configuration Manager 可以帮助管理 iOS 激活锁定，这是适用于 iOS 7.1 及更高版本设备的“查找我的 iPhone”应用的功能。 当设备上使用了“查到我的 iPhone”应用时，激活锁定自动启用。 启用后，任何人都必须先输入用户的 Apple ID 和密码，然后才能执行以下操作：  

-   关闭“查找我的 iPhone”。  

-   擦除设备。  

-   重新激活设备。  

Configuration Manager 可以请求运行 iOS 7.1 和更高版本的已监管设备和非监管设备的激活锁定状态。 对于监管设备而言，Configuration Manager 可以检索绕过激活锁定代码并将其直接发布到设备。  

 有关详细信息，请参阅[通过 System Center Configuration Manager 中的绕过激活锁定帮助保护 iOS 设备](/sccm/mdm/deploy-use/manage-ios-activation-lock)。  

### <a name="monitor-terms-and-conditions-deployments"></a>监控条款和条件部署  
 你可以在 Configuration Manager 控制台中监视条款和条件部署。  

 从部署的列表中选择部署的条款和条件。 摘要区域显示以下统计信息：  

-   **合规**：用户已接受最新版本的条款和条件。  

-   **错误**  

-   **不合规**：用户已接受某版本的条款和条件，但未接受最新版本。  

-   **未知**：用户从未接受条款和条件，包括不具有已注册设备的用户。  
