---
title: Technical Preview 版本
titleSuffix: Configuration Manager
description: 了解可测试 Configuration Manager 中的新功能和新特性的 Technical Preview 版本。
ms.date: 04/25/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79a535bd9ee7f597e551c2d4f84c39c84ecf262f
ms.sourcegitcommit: d67c6246bb6027cd5501e772b0521f9272407c28
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview

*适用范围：System Center Configuration Manager (Technical Preview)*

**欢迎使用 System Center Configuration Manager Technical Preview**。 本文提供了有关不断完善的预览版的详细信息，该版本包括我们正在开发的功能。 每个版本的 Technical Preview 都会引入尚未包含在 Configuration Manager 的 Current Branch 中的新功能。 这些功能最终可能会包含在当前分支版本的更新中，但在确定和添加功能之前，我们希望你有机会试用它们并向我们提供反馈。  

 由于此版本是技术预览版，因此详细信息和功能可能有所更改。  

 本文包含适用于所有版本的 Technical Preview 的信息。 它还列出了每个新功能及其首次出现的 Technical Preview 版本，例如版本 1804 表示 2018 年 4 月。 这些功能将专门在各预览版的单独主题中详细介绍。  

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


-   默认情况下，如果使用 Technical Preview，则服务连接点安装为联机模式。 它不支持更改为脱机模式。

-   每个特定版本的 Technical Preview 的单独文章中包括其他限制或要求（如果适用）。

-   不支持迁移到此预览版或从此预览版进行迁移。  

-   不支持升级到此预览版。 

-   不支持从 cd.latest 文件夹进行站点恢复。  <!--507106-->

-   不支持从此预览版升级到生产版本（当前分支）。 但是，更新可用于预览版本时，可以从 Configuration Manager 控制台的“更新和与维护服务”节点查找并安装它们。 有关控制台中升级过程的视频，请观看 youtube.com 上的 [Installing ConfigMgr Update Packages（安装 ConfigMgr 更新包）](https://www.youtube.com/embed/KBd_EGFbUT8) 。  
-   仅支持独立主站点。 不支持管理中心站点、多个主站点或辅助站点。  

此 Configuration Manager 分支支持以下产品和技术。 不过，将它们囊括在这一内容中并不表示对超出相应产品的单独支持生命周期的产品或版本延长支持。 不支持将超出其支持生命周期的产品与 Configuration Manager 一起使用。 有关 Microsoft 支持生命周期的详细信息，请访问 [Microsoft 支持生命周期](http://go.microsoft.com/fwlink/p/?LinkId=208270) 网站。  

-   仅支持以下 SQL Server 版本：  

    -   从 Configuration Manager 版本 1710 开始的 SQL Server 2017（含累积更新 2 及更高版本）
    -   SQL Server 2016（不带 Service Pack）及更高版本
    -   SQL Server 2014（含 Service Pack 1）及更高版本
    -   SQL Server 2012（含 Service Pack 3）或更高版本


-   站点最多支持 10 个客户端，这些客户端必须运行 Windows 的以下版本之一：  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

##  <a name="bkmk_install"></a> 安装并更新技术预览版  
 System Center Configuration Manager Technical Preview 与 System Center Configuration Manager 的当前版本是不同的。  

 若要使用 Technical Preview，必须先安装 Technical Preview 内部版本的“基线版本”。 安装基线版本之后，可使用控制台内部更新来升级此内部版本，以便使用最新预览版使你的安装程序保持最新。 通常，每个月都会提供新版本的 Technical Preview。

每个预览版的支持时间在发布三个后续版本后结束。 也就是说，发布 1708 版时，将不再支持 1704 版，但是仍支持 1705、1706 和 1707 版。 如果基线版本不再受支持，仍然支持安装新的 Technical Preview 站点（直到新基线版本可用），只要之后将该安装产品更新为受支持的版本即可。 更新到最新可用版本，然后重复此流程直到可以安装 Technical Preview 最新版为止。

> [!TIP]  
>  向 Technical Preview 安装更新后，即可将 Preview 安装更新到这个新的 Technical Preview 版本。 Technical Preview 安装绝不会升级到 Current Branch 安装，也不会从 Current Branch 版本获取更新。  

**Technical Preview 的活动基线版本：**
   
可以在基线版本发布后的 1 年内安装此基线版本。 但是，在安装新的技术预览站点时，我们建议使用可用的最新基线版本。
-  **Technical Preview 1711** - Configuration Manager Technical Preview 1711 可同时用作控制台内更新和新的基线版本。 [从 TechNet 评估中心](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)下载基线版本。


##  <a name="BKMK_TPFeedback"></a> 提供反馈  
 欢迎提供有关技术预览版功能的反馈。 有关详细信息，请参阅[产品反馈](../understand/find-help.md#product-feedback)。

如果你对于想要看到的新功能有任何想法，也请让我们知道。 若要提交新的想法，并为他人提交的想法投票，请 [访问我们的用户之声页面](http://configurationmanager.uservoice.com)。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a>最新技术预览版中提供的功能  
以下是最新 Configuration Manager Technical Preview 版本中提供的功能。  某个旧版 Technical Preview 中可用的功能在其后的版本中仍然可用。 同样，已添加到 Configuration Manager Current Branch 的功能在 Technical Preview 版本中仍然可用。  请单击查看每个预览版本的内容，了解有关特定功能的详细信息。  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1804"></a>Technical Preview 1804 版
- [配置用于站点服务器的远程内容库](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server) <!--1357525--> 
- [从 Configuration Manager 控制台提交反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback) <!--1357542--> 
- [支持中心](capabilities-in-technical-preview-1804.md#support-center) <!--1357489--> 
- [Configuration Manager 工具包](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit) <!--1357145--> 
- [在批准撤消时卸载应用程序](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation) <!--1357891--> 
- [从发现中排除 Active Directory 容器](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery) <!--1358143--> 
- [指定应用程序目录网站链接在软件中心的可见性](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center) <!--1358214--> 
- [按软件更新体系结构筛选自动部署规则](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture) <!--1322266--> 
- [对 OS 部署的改进](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) <!--1358330,1358493--> 
- [对 Configuration Manager 控制台的改进](capabilities-in-technical-preview-1804.md#improvements-to-the-configuration-manager-console) <!--510252--> 



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>最新受支持的 Technical Preview 中提供的功能
以下是旧版 Configuration Manager Technical Preview 提供且依然受支持的功能。 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |功能 |Technical Preview 版本 |Current Branch 版本|  
 |----------------|---------------------|--------------------|
 | 请求分发点支持将云分发点作为源 <!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![未添加](media/Red_X.gif) | 
 | 客户端对等缓存中的部分下载支持可降低 WAN 利用率 <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![未添加](media/Red_X.gif) | 
 | 软件中心的维护时段 <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![未添加](media/Red_X.gif) | 
 | 软件中心用于网页的自定义选项卡 <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![未添加](media/Red_X.gif) | 
 | 对客户端启用第三方软件更新支持 <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![未添加](media/Red_X.gif) | 
 | 支持从监视视图中复制/粘贴资产详细信息 <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![未添加](media/Red_X.gif) | 
 | SCAP 扩展 <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![未添加](media/Red_X.gif) | 
 | 使用共同管理将 Endpoint Protection 工作负荷转移到 Intune <!-- 1357365 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) | [版本 1802](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune) |  
 | 配置 Windows 传递优化以使用 Configuration Manager 边界组 <!-- 1324696 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) | [版本 1802](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization) |  
 | 通过云管理网关执行的 Windows 10 就地升级任务序列 <!-- 1357149 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) | [版本 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg) |  
 | 对 Windows 10 就地升级任务序列的改进 <!-- 1357425 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) | [版本 1802](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) |  
 | 对已启用 PXE 的分发点的改进 <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | ![未添加](media/Red_X.gif) | 
 | 任务序列的部署模板 <!-- 1357391 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) | [版本 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) |  
 | 产品生命周期仪表板 <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | ![未添加](media/Red_X.gif) | 
 | 报表改进 <!--1357653 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-reporting) | [版本 1802](/sccm/core/servers/manage/list-of-reports#operating-system) |  
 | 对软件中心的改进 <!--1357592 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-software-center) | [版本 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) |  
 | 管理点的边界组回退 <!-- 1324594 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) | [版本 1802](/sccm/core/servers/deploy/configure/boundary-groups#management-points) |  
 | 改进了对 CNG 证书的支持 <!-- 1357314 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) | [版本 1802](/sccm/core/plan-design/network/cng-certificates-overview) |  
 | 云管理网关支持 Azure 资源管理器 <!-- 1324735 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) | [版本 1802](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager) |  
 | 审批每台设备的用户的应用程序请求 <!-- 1357015 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) | [版本 1802](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) |  
 | 在已加入 Azure AD 的设备上，使用软件中心来浏览和安装用户可用的应用程序 <!-- 1322613 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) | [版本 1802](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices) |  
 | 关于 Windows AutoPilot 设备信息的报表 <!-- 1351442 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) | [版本 1802](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) |  
 | 对适用于 Windows Defender 攻击防护的 Configuration Manager 策略的改进 <!-- 1356220 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) | [版本 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |  
 | Microsoft Edge 浏览器策略 <!-- 1357310 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) | [版本 1802](/sccm/compliance/deploy-use/browser-profiles) | 
 | 默认浏览器计数报表 <!-- 1357830 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) | [版本 1802](/sccm/core/servers/manage/list-of-reports#software---companies-and-products) | 
 | Windows 10 ARM64 设备支持 <!-- 1353704 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) | [版本 1802](/sccm/core/plan-design/configs/support-for-windows-10) |  
 | 创建分阶段部署 <!-- 1356837 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#create-phased-deployments) | [版本 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) |
 | 共同管理报告 <!-- 1356648 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#co-management-reporting) | [版本 1802](\sccm\core\clients\manage\client-management-dashboard) |
 | 自动部署规则评估计划改进 <!-- 1357133 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule) | [版本 1802](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule) |
 | 重新分配分发点 <!-- 1306937 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#reassign-distribution-point) | [版本 1802](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign) |
 | 硬件清单改进 <!-- 1357389 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory) | [版本 1802](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255) |
 | 软件中心的客户端设置改进 <!-- 1355146 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center) | [版本 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved) |
 | 新的 Windows Defender 应用程序防护设置 <!-- 1356256 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard) | [版本 1802](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS) |
 | 运行脚本的改进 <!-- 1236459 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts) | [版本 1802](/sccm/apps/deploy-use/create-deploy-scripts) |
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>以前的技术预览版中提供的功能
以下是旧版 Configuration Manager Technical Preview 提供的特定功能。 这些功能在更高版本中保持可用，但在 Current Branch 版本中还不可用。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |功能 |Technical Preview 版本 |  
 |----------------|---------------------|
 | 基于客户端的 PXE 响应者服务 <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
 |站点服务器角色的高可用性 <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |PXE 网络启动对 IPv6 的支持 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |使用 Azure Active Directory<!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Windows Update for Business 更新的符合性评估 <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |OData 终结点数据访问 <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |对资产智能的改进<!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |最终用户可从公司门户安装应用 <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>另请参阅  
[System Center Configuration Manager 中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [System Center Configuration Manager 简介](../../core/understand/introduction.md)

> [!Tip]  
> 若要详细了解需要同意才能启用的当前分支功能，请参阅[预发布功能](/sccm/core/servers/manage/pre-release-features)。  
> 若要详细了解必须先启用的当前分支功能，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。  

