---
title: System Center Configuration Manager Technical Preview | Microsoft Docs
description: "了解可让你试用 System Center Configuration Manager 中的新功能和新特性的 Technical Preview 版本。"
ms.custom: na
ms.date: 4/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f809c9327db9f298168674add2d09820fdecd1b8
ms.openlocfilehash: 3a7370fedee417588d219dc7bff46205faf42929
ms.contentlocale: zh-cn
ms.lasthandoff: 05/17/2017


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview

*适用范围：System Center Configuration Manager (Technical Preview)*

**欢迎使用 System Center Configuration Manager Technical Preview**。 本主题提供了有关不断完善的预览版的详细信息，该版本包括我们正在开发的功能。 每个版本的 Technical Preview 都会引入尚未包含在 System Center Configuration Manager 的 Current Branch 中的新功能。 这些功能最终可能会包含在当前分支版本的更新中，但在确定和添加功能之前，我们希望你有机会试用它们并向我们提供反馈。  

 由于这是技术预览版，因此详细信息和功能可能有所更改。  

 本主题包含适用于所有的技术预览版本的信息，并且列出了每个新功能及功能首次在其中出现的技术预览版本，例如，版本 1701 表示 2017 年 1 月。 这些功能的详细信息将专门在各预览版本的单独主题中详细介绍。  

 有关 Configuration Manager 的 Current Branch 中新增功能的信息，请参阅 [System Center Configuration Manager 中的新增功能](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)。



##  <a name="bkmk_reqs"></a> Technical Preview 的要求和限制  

> [!IMPORTANT]     
>  Technical Preview 仅授权用于实验室环境。  Microsoft 可能无法提供支持服务，预览软件中某些功能可能不可用。 此外，相对于面向市场提供的软件，预览版软件可能采用简化的或不同的安全性、隐私性、可访问性、可用性和可靠性标准。  

 有关大多数产品先决条件，请使用 [System Center Configuration Manager 支持的配置](../../core/plan-design/configs/supported-configurations.md)中的信息。 以下是适用于技术预览版本的例外情况：  

-   每次安装在保持活动状态 90 天后变为非活动状态。  

-   英语是唯一受支持的语言。


-   仅支持以下安装标志（开关）：  

    -   **/Silent**  
    -   **/testdbupgrade**    


-   默认情况下，在使用技术预览时，服务连接点设置为联机模式，且不支持更改为脱机模式。

-   Technical Preview 的每个特定版本的详细信息中会随附其他限制或要求（如果适用）  

-   不支持迁移到此预览版或从此预览版进行迁移。  

-   不支持升级到此预览版。  

-   不支持从此预览版升级到生产版本（当前分支）。 但是，更新可用于预览版本时，可以从 Configuration Manager 控制台的“更新和与维护服务”节点查找并安装它们。 有关控制台中升级过程的视频，请观看 youtube.com 上的 [Installing ConfigMgr Update Packages（安装 ConfigMgr 更新包）](https://www.youtube.com/embed/KBd_EGFbUT8) 。  
-   仅支持独立主站点。 不支持管理中心站点、多个主站点或辅助站点。  

此 Configuration Manager 分支支持以下产品和技术。 不过，将它们囊括在这一内容中并不表示对超出相应产品的单独支持生命周期的产品或版本延长支持。 不支持将超出其支持生命周期的产品与 Configuration Manager 一起使用。 有关 Microsoft 支持生命周期的详细信息，请访问 [Microsoft 支持生命周期](http://go.microsoft.com/fwlink/p/?LinkId=208270) 网站。  

-   仅支持以下 SQL Server 版本：  

    -   SQL Server 2016（不带 Service Pack）及更高版本
    -   SQL Server 2014（含 Service Pack 1）及更高版本
    -   SQL Server 2012（含 Service Pack 3）或更高版本


-   站点最多支持 10 个客户端，这些客户端必须在以下操作系统之一上运行：  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> 安装并更新技术预览版  
 System Center Configuration Manager Technical Preview 与 System Center Configuration Manager 的当前版本是不同的。  

 若要使用技术预览版，必须先安装技术预览版内部版本的 **基线版本** 。 安装基线版本之后，可使用 **控制台内部更新** 来升级此内部版本，以便使用最新预览版使你的安装程序保持最新。     通常，每个月都会提供新版本的 Technical Preview。

每个预览版的支持时间在发布三个后续版本后结束。 也就是说，发布 1702 版时，将不再支持 1610 版，但是仍支持 1611、1612 和 1701 版。 如果基线版本不再受支持（如 1610 版），仍然支持安装新的 Technical Preview 站点（直到新基线版本可用），只要之后将该安装产品更新为受支持的版本即可。 更新时，如果控制台中未显示可用的最新版本，请更新到提供的最新版本，然后重复此过程直至可安装 Technical Preview 的最新版本。

> [!TIP]  
>  当你将更新安装到技术预览版时，即可将预览安装更新到此新的技术预览版。    技术预览版安装绝不会升级到当前的分支安装，也不会从当前分支版本获取更新。  

**Technical Preview 的活动基线版本：**  
可以在基线版本发布后的 1 年内安装此基线版本。 但是，在安装新的技术预览站点时，我们建议使用可用的最新基线版本。
-  **Technical Preview 1703** - Configuration Manager Technical Preview 1703 可作为 Configuration Manager Technical Preview 的控制台中更新，以及作为 TechNet 评估中心网站中提供的新基线版本。

-  **Technical Preview 1610** - Configuration Manager Technical Preview 1610 可同时用作 Configuration Manager Technical Preview 的控制台内更新和基线版本。 如果具有用于安装 1610 的媒体，建议下载版本 1703 并改为安装该版本。




##  <a name="BKMK_TPFeedback"></a> 提供反馈  
 我们希望收到有关技术预览版的反馈。 若要提交关于每个预览版中的功能的反馈，请使用指向我们的反馈表的链接，该反馈表位于 Microsoft Connect 站点上的 [Configuration Manager 反馈计划](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) 页中。  

 此外，如果你对于想要看到的新功能有任何想法，也请让我们知道。 若要提交新的想法，并为他人提交的想法投票，请 [访问我们的用户之声页面](http://configurationmanager.uservoice.com)。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> 技术预览版中提供的功能  
 以下是每个 Configuration Manager Technical Preview 提供的功能。  从某一技术预览版开始提供的功能，在其后的版本中将保持可用。 同样，已添加到 System Center Configuration Manager 发行版本 (Current Branch) 的功能在后续的 Technical Preview 中将保持可用。  请单击查看每个预览版本的内容，了解有关特定功能的详细信息。  

 |功能 |Technical Preview 版本 |Current Branch 版本|  
|----------------|---------------------|--------------------|
 |使用应用配置策略配置 Android 应用  |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![未添加](media/Red_X.gif)|
 |硬件清单收集安全启动信息 |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|![未添加](media/Red_X.gif)|
 |将子任务序列添加到任务序列|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![未添加](media/Red_X.gif)|
 |重载当前的 Windows PE 版本的启动映像 |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|![未添加](media/Red_X.gif)|
 |对操作系统部署的改进|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![未添加](media/Red_X.gif)|
 |将批量采购的 iOS 应用部署到设备集合|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[版本 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |指向软件中心中应用程序的直接链接|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|![未添加](media/Red_X.gif)
 |Configuration Manager Windows 客户端计算机的 PFX 证书|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|![未添加](media/Red_X.gif)|
 |配置 Azure 服务向导|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|![未添加](media/Red_X.gif)|
 |在操作系统升级任务序列中从 BIOS 转换为 UEFI| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[版本 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |可折叠的任务序列组| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |![未添加](media/Red_X.gif)|
 |用于配置 Windows Analytics for Upgrade Readiness 的客户端设置 | [Tech Preview 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |![未添加](media/Red_X.gif)|
 |iOS 设备的新符合性设置|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[版本 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |创建具有 S/MIME 支持的 PFX 证书|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[版本 1702](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |在安装应用程序之前检查运行的可执行文件|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[版本 1702](/sccm/apps/deploy-use/deploy-applications)|
 |从 Configuration Manager 控制台发送反馈 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |更新和维护服务的更改  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |对等缓存功能改进  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[版本 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |使用 Azure Active Directory  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![未添加](media/Red_X.gif)|
 |条件性访问设备符合性策略改进 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[版本 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |反恶意软件客户端版本警报 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[版本 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Windows Update for Business 更新的符合性评估 | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![未添加](media/Red_X.gif)|
 |针对影响重大的任务序列，改进软件中心设置和消息通知|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[版本 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Android for Work 支持| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[版本 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |软件更新点的边界组改进 | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[版本 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |硬件清单将收集 UEFI 信息 | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[版本 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |对操作系统部署的改进| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |使用基于云的分发点托管软件更新| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|![未添加](media/Red_X.gif) |
 |通过管理点验证设备运行状况证明数据| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [版本 1702](/sccm/core/servers/manage/health-attestation) |
 |适用于 Microsoft Azure 政府云的 OMS 连接器 |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[版本 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |在创建向导中，不再以 Android 和 iOS 版本为目标 |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |![未添加](media/Red_X.gif) |
 |OData 终结点数据访问 |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![未添加](media/Red_X.gif)|
 |数据仓库服务点 |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[版本 1702](/sccm/core/servers/manage/data-warehouse)|
 |内容库清理工具 |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[版本 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |控制台中搜索功能的改进 |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |如果指定的程序正在运行，则阻止安装应用程序|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[版本 1702](/sccm/apps/deploy-use/deploy-applications)|
 |新的 Windows Hello 企业版最终用户通知|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![未添加](media/Red_X.gif)|
 |Configuration Manager 中适用于企业的 Windows 应用商店支持|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![未添加](media/Red_X.gif)|
 |任务序列失败时返回上一页|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[版本 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Windows 10 更新的快速安装文件支持|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[版本 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Azure Active Directory 载入|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|![未添加](media/Red_X.gif)|
 |更改为配置多重身份验证以进行设备注册|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![未添加](media/Red_X.gif)|
 |部署和任务序列的预先缓存内容 |[Tech Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[版本 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Windows Defender 配置设置|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[版本 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |从管理员控制台请求策略同步|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[版本 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |“所有公司拥有的设备”节点的附加安全角色支持|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[版本 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Windows 10 VPN 配置文件的条件访问|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[版本 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |按自动部署规则中的内容大小进行筛选|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[版本 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |改进了“所需软件”对话框功能|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[版本 1610](/sccm/apps/deploy-use/deploy-applications)|
 |拒绝以前批准的应用程序请求|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[版本 1610](/sccm/apps/deploy-use/deploy-applications)|
 |从自动升级中排除客户端|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[版本 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Endpoint Protection 的改进|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[版本 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |增加了“注册的设备”的数量|[Tech Preview 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[版本 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |其他 Apple DEP 设置|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[版本 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |适用于企业的 Windows 应用商店与 Configuration Manager 集成的增强功能|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[版本 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |配置项目的新符合性设置|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[版本 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |与 Upgrade Analytics 的集成|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[版本 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Windows 10 VPN 混合配置文件的本机连接类型|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![未添加](media/Red_X.gif)|
 |边界组的改进|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[版本 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Office 365 客户端管理仪表板|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[版本 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |将 Office 365 应用部署到客户端|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[版本 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |对于 BIOS 到 UEFI 转换的改进|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[版本 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Intune 合规性图表|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[版本 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |准备 ConfigMgr 客户端以便捕获任务序列步骤的改进|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[版本 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |对软件中心的改进|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[版本 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |对资产智能的改进|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![未添加](media/Red_X.gif)|
 |远程控制键盘转换|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![未添加](media/Red_X.gif)|
 |Windows 10 版本升级策略的改进|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[版本 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |软件中心可自定义的品牌的对话框|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|![未添加](media/Red_X.gif)|  
 |本地移动设备管理的多个设备管理点|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[版本 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |自动将设备分类到集合|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[版本 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |所需的应用程序和软件更新部署的强制宽限期|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[版本 1610](/sccm/apps/deploy-use/deploy-applications)|
 |通过 Device Guard 将 Configuration Manager 用作托管的安装程序|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![未添加](media/Red_X.gif)|
 |云管理网关（原来的云代理服务）|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [版本 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |在 Configuration Manager 中管理 Office 365 客户端代理|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[版本 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |已弃用 OSDPreserveDriveLetter 任务序列变量|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[版本 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |更新和维护节点的更改|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[版本 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |Windows 10 设备的每应用 VPN|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[版本 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |安装软件更新任务序列的改进|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[版本 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |准备 ConfigMgr 客户端以便捕获任务序列步骤的改进 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[版本 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |所需的应用程序部署的宽限期 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![未添加](media/Red_X.gif)|  
 |远程设备操作的新体验 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[版本 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |适用于企业的 Windows 应用商店应用 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[版本 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |批量采购应用的一般改进|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[版本 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |企业数据保护 (EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[版本 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |最终用户可从公司门户安装应用 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![未添加](media/Red_X.gif)|  
 |软件中心中的更新和操作系统的新选项卡|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[版本 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |为服务器组提供服务 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[版本 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |支持 Windows Defender 高级威胁防护服务 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[版本 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |在软件更新安装之后重启 Windows 10 客户端的新选项|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[版本 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |本地设备运行状况证明 |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[版本 1606](/sccm/core/servers/manage/health-attestation)|  
 |预声明具有 IMEI 或 iOS 序列号的公司拥有的设备|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[版本 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |管理从适用于企业的 Windows 应用商店批量采购的应用| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[版本 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |对 Microsoft Passport for Work 管理的改进|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[版本 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |供客户端切换到新软件更新点的选项|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[版本 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |用于管理客户端缓存设置和客户端对等缓存的客户端设置 |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|客户端设置：[版本 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>对等缓存：[版本 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |支持将 Passport for Work 作为 KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[版本 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |本地设备运行状况证明|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[版本 1606](/sccm/core/servers/manage/health-attestation)|  
 |适用于 Android 设备的 SmartLock 设置|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[版本 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 <!--  TP 1603 Aged out of support and all features in Current Branch Builds:
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->
 当 Current Branch 的最低支持版本提供 technical preview 版本的所有功能时，将从此表删除该预览版本的详细信息。


## <a name="see-also"></a>另请参阅  
[System Center Configuration Manager 中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [System Center Configuration Manager 简介](../../core/understand/introduction.md)

