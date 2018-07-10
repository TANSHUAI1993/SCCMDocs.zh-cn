---
title: Technical Preview 版本
titleSuffix: Configuration Manager
description: 了解可测试 Configuration Manager 中的新功能和新特性的 Technical Preview 版本。
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1fd848c3e0ed663e0731eb86d39c930db3af7819
ms.sourcegitcommit: d1bf26bcf0d78b37ac7598fab36eb58ca69b1dc5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37066277"
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview

*适用范围：System Center Configuration Manager (Technical Preview)*

**欢迎使用 System Center Configuration Manager Technical Preview**。 本文提供了有关不断完善的预览版的详细信息，该版本包括我们正在开发的功能。 每个版本的 Technical Preview 都会引入尚未包含在 Configuration Manager 的 Current Branch 中的新功能。 这些功能最终可能会包含在当前分支版本的更新中，但在确定和添加功能之前，我们希望你有机会试用它们并向我们提供反馈。  

 由于此版本是技术预览版，因此详细信息和功能可能有所更改。  

 本文包含适用于所有版本的 Technical Preview 的信息。 它还列出了每个新功能及其首次出现的 Technical Preview 版本，例如版本 1806 表示 2018 年 6 月。 这些功能将专门在各预览版的单独主题中详细介绍。  

 有关 Configuration Manager 的 Current Branch 中新增功能的信息，请参阅 [System Center Configuration Manager 中的新增功能](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)。



##  <a name="bkmk_reqs"></a> Technical Preview 的要求和限制  

> [!IMPORTANT]     
>  Technical Preview 仅授权用于实验室环境。 Microsoft 可能无法提供支持服务，预览软件中某些功能可能不可用。 此外，相对于面向市场提供的软件，预览版软件可能采用简化的或不同的安全性、隐私性、可访问性、可用性和可靠性标准。  

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

此 Configuration Manager 分支支持以下产品和技术。 不过，将它们囊括在这一内容中并不表示对超出相应产品的单独支持生命周期的产品或版本延长支持。 不支持将超出其支持生命周期的产品与 Configuration Manager 一起使用。 有关 Microsoft 支持生命周期的详细信息，请访问 [Microsoft 支持生命周期](https://go.microsoft.com/fwlink/p/?LinkId=208270) 网站。  

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
-  **Technical Preview 1806** - Configuration Manager Technical Preview 1806 可同时用作控制台内更新和新的基线版本。 [从 TechNet 评估中心](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)下载基线版本。


##  <a name="BKMK_TPFeedback"></a> 提供反馈  
 欢迎提供有关技术预览版功能的反馈。 有关详细信息，请参阅[产品反馈](../understand/find-help.md#product-feedback)。

如果你对于想要看到的新功能有任何想法，也请让我们知道。 若要提交新的想法，并为他人提交的想法投票，请 [访问我们的用户之声页面](https://configurationmanager.uservoice.com)。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a>最新技术预览版中提供的功能  
以下是最新 Configuration Manager Technical Preview 版本中提供的功能。 某个旧版 Technical Preview 中可用的功能在其后的版本中仍然可用。 同样，已添加到 Configuration Manager Current Branch 的功能在 Technical Preview 版本中仍然可用。 请单击查看每个预览版本的内容，了解有关特定功能的详细信息。  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-18062"></a>Technical Preview 版本 1806.2
- [分阶段部署的改进](capabilities-in-technical-preview-1806-2.md#bkmk_pod) <!--1358577,1358147,1358578-->
- [支持新的 Windows 应用包格式](capabilities-in-technical-preview-1806-2.md#bkmk_msix) <!--1357427-->
- [客户端推送安全性改进](capabilities-in-technical-preview-1806-2.md#bkmk_client-push) <!--1358204-->
- [针对主动维护的管理见解](capabilities-in-technical-preview-1806-2.md#bkmk_insights) <!--1352184,et al-->
- [转移共同管理的设备的移动应用工作负荷](capabilities-in-technical-preview-1806-2.md#bkmk_comgmt) <!--1357892-->
- [对等下载适用的边界组选项](capabilities-in-technical-preview-1806-2.md#bkmk_bgoptions) <!--1356193-->
- [自定义目录支持第三方软件更新](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate) <!--1358714-->
- [云管理功能改进](capabilities-in-technical-preview-1806-2.md#bkmk_cloud) <!--511980,515854-->
- [新的软件更新符合性报告](capabilities-in-technical-preview-1806-2.md#bkmk_report) <!--1357775-->



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>最新受支持的 Technical Preview 中提供的功能
以下是旧版 Configuration Manager Technical Preview 提供且依然受支持的功能。 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |功能 |Technical Preview 版本 |Current Branch 版本|  
 |----------------|---------------------|--------------------|
 | 第三方软件更新<!--1352101--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)  | ![未添加](media/Red_X.gif) |  
 | 为 Microsoft Edge 配置 Windows Defender SmartScreen 设置<!--1353701--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge)  | ![未添加](media/Red_X.gif) |  
 | 通过 Microsoft Intune 为共同管理的设备同步 MDM 策略<!--1357377--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device)  | ![未添加](media/Red_X.gif) |  
 | 使用共同管理将 Office 365 工作负荷转移到 Intune<!--1357841--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#transition-office-365-workload-to-intune-using-co-management)  | ![未添加](media/Red_X.gif) |  
 | 包转换管理器<!--1357861--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#package-conversion-manager)  | ![未添加](media/Red_X.gif) |  
 | 部署无内容的软件更新<!--1357933--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content)  | ![未添加](media/Red_X.gif) |  
 | Office 自定义工具与 Office 365 安装程序集成<!--1358149--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#office-customization-tool-integration-with-the-office-365-installer)  | ![未添加](media/Red_X.gif) |  
 | 云管理网关的改进<!--1358215,1358651,503899--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway)   | ![未添加](media/Red_X.gif) |  
 | 安全客户端通信的改进<!--1358278,1358279--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-secure-client-communications)  | ![未添加](media/Red_X.gif) |  
 | 软件中心基础结构的改进<!--1358309--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#software-center-infrastructure-improvements)  | ![未添加](media/Red_X.gif) |  
 | 为设备上的所有用户预配 Windows 应用包<!--1358310--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#provision-windows-app-packages-for-all-users-on-a-device)  | ![未添加](media/Red_X.gif) |  
 | Surface 仪表板的改进<!--1358654--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-the-surface-dashboard)  | ![未添加](media/Red_X.gif) |  
 | 硬件清单默认单位修订<!--514442--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#hardware-inventory-default-unit-revision)  | ![未添加](media/Red_X.gif) |  
 | 使用手动配置的任务序列阶段创建分阶段部署 <!--1358148--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | ![未添加](media/Red_X.gif) |  
 | 对 Azure 资源管理器的云分发点支持 <!--1322209--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | ![未添加](media/Red_X.gif) |  
 | 根据管理见解执行操作 <!--1357930--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | ![未添加](media/Red_X.gif) |  
 | 使用共同管理将设备配置工作负荷转移到 Intune <!--1357903--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | ![未添加](media/Red_X.gif) |  
 | 启用分发点以使用网络拥塞控制 <!--1358112--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | ![未添加](media/Red_X.gif) |  
 | 云管理仪表板 <!--1358461--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | ![未添加](media/Red_X.gif) |  
 | CMPivot <!--1358456--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | ![未添加](media/Red_X.gif) |  
 | 已改进安全客户端通信 <!--1356889,1358228,1358460--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | ![未添加](media/Red_X.gif) |  
 | 启用第三方软件更新支持的改进 <!--1357605--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | ![未添加](media/Red_X.gif) |  
 | 对 Windows 10 就地升级任务序列的改进 <!--1358500--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | ![未添加](media/Red_X.gif) |  
 | 与客户端一起安装的 CMTrace <!--1357971--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | ![未添加](media/Red_X.gif) |  
 | 对 Configuration Manager 控制台的改进 <!--1358202--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | ![未添加](media/Red_X.gif) |  
 | 对控制台反馈的改进 <!--1357542--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | ![未添加](media/Red_X.gif) |  
 | 对已启用 PXE 的分发点的改进 <!--1357580--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | ![未添加](media/Red_X.gif) |  
 | 对大整数值硬件清单的改进 <!--1357880--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | ![未添加](media/Red_X.gif) |  
 | WSUS 维护改进 <!--1357898--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | ![未添加](media/Red_X.gif) |  
 | 对 CNG 证书支持的改进 <!--1357314--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | ![未添加](media/Red_X.gif) |  
| 配置用于站点服务器的远程内容库 <!--1357525--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)  | ![未添加](media/Red_X.gif) | 
 | 从 Configuration Manager 控制台提交反馈 <!--1357542--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#bkmk_feedback)  | ![未添加](media/Red_X.gif) | 
 | 支持中心 <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | ![未添加](media/Red_X.gif) | 
 | Configuration Manager 工具包 <!--1357145--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit)  | ![未添加](media/Red_X.gif) | 
 | 在批准撤消时卸载应用程序 <!--1357891--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation)  | ![未添加](media/Red_X.gif) | 
 | 从发现中排除 Active Directory 容器 <!--1358143--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery)  | ![未添加](media/Red_X.gif) | 
 | 指定应用程序目录网站链接在软件中心的可见性 <!--1358214--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center)  | ![未添加](media/Red_X.gif) | 
 | 按软件更新体系结构筛选自动部署规则 <!--1322266--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture)  | ![未添加](media/Red_X.gif) | 
 | 对操作系统部署的改进 <!--1358330,1358493--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) | ![未添加](media/Red_X.gif) | 
 | 请求分发点支持将云分发点作为源 <!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![未添加](media/Red_X.gif) | 
 | 客户端对等缓存中的部分下载支持可降低 WAN 利用率 <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![未添加](media/Red_X.gif) | 
 | 软件中心的维护时段 <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![未添加](media/Red_X.gif) | 
 | 软件中心用于网页的自定义选项卡 <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![未添加](media/Red_X.gif) | 
 | 对客户端启用第三方软件更新支持 <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![未添加](media/Red_X.gif) | 
 | 支持从监视视图中复制/粘贴资产详细信息 <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![未添加](media/Red_X.gif) | 
 | SCAP 扩展 <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![未添加](media/Red_X.gif) | 
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>以前的技术预览版中提供的功能
以下是旧版 Configuration Manager Technical Preview 提供的特定功能。 这些功能在更高版本中保持可用，但在 Current Branch 版本中还不可用。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |功能 |Technical Preview 版本 |  
 |----------------|---------------------|
 | 对已启用 PXE 的分发点的改进 <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | 
 | 产品生命周期仪表板 <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | 
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

