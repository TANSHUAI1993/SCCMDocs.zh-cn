---
title: Technical Preview 版本
titleSuffix: Configuration Manager
description: 了解可测试 Configuration Manager 中的新功能和新特性的技术预览分支。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec9c4cdf54e6ffc55cc2983152f56492e5b1b354
ms.sourcegitcommit: af4f8bd8dffe6fb05f51322ea9e94d335a2cc0c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39360709"
---
# <a name="technical-preview-for-configuration-manager"></a>Configuration Manager 的技术预览版

*适用范围：System Center Configuration Manager (Technical Preview)*

本文提供了有关 Configuration Manager 的每月技术预览分支的详细信息。 技术预览版介绍 Microsoft 正在开发的新功能。 它介绍 Configuration Manager 当前分支中尚未包含的新功能。 这些功能可能最终会包含在当前分支的更新中。 在我们最终发布这些功能前，我们希望你试用这些功能并向我们提供反馈。  

由于此版本是技术预览版，因此详细信息和功能可能有所更改。  

此信息适用于 Configuration Manager 技术预览分支的所有版本。 本文列出了每个新功能以及该功能首次出现所在的技术预览版。 例如，版本 1806 为 2018 年 (18) 的 6 月 (06)。 单独的文章专用于详细介绍每个预览版的单独功能。  

有关 Configuration Manager 的当前版本 中新增功能的信息，请参阅 [Configuration Manager 增量版本中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)。



##  <a name="bkmk_reqs"></a>要求和限制  

> [!IMPORTANT]     
>  Technical Preview 仅授权用于实验室环境。 Microsoft 可能无法提供支持服务，预览软件中某些功能可能不可用。 此外，相对于面向市场提供的软件，预览版软件可能采用简化的或不同的安全性、隐私性、可访问性、可用性和可靠性标准。  

 有关大多数产品的先决条件，请使用[支持的配置](/sccm/core/plan-design/configs/supported-configurations)中的信息。 以下是适用于技术预览分支的例外情况：  

-   每次安装在活动状态 90 天后变为非活动状态。  

-   英语是唯一受支持的语言。  

-   它仅支持以下安装命令行参数：  
    -   `/silent`  
    -   `/testdbupgrade`    

-   服务连接点安装为联机模式。 它不支持脱机模式。  

-   每个特定版本的 Technical Preview 的单独文章中包括其他限制或要求（如果适用）。

-   以下功能在技术预览分支中不受支持：  

    - [迁移](/sccm/core/migration/migrate-data-between-hierarchies)到此预览分支或从此预览分支迁移。  

    - [升级](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)到此预览分支。  

    - cd.latest 文件夹中的[站点恢复](/sccm/core/servers/manage/recover-sites)。  <!--507106-->

-   不支持从此预览分支更新到当前分支。  

    > [!Note]  
    > 更新可用于预览版本时，仍从 Configuration Manager 控制台的“更新与维护服务”节点查找并安装它们。 有关控制台中升级过程的视频，请观看 youtube.com 上的[安装 Configuration Manager 更新包](https://www.youtube.com/embed/KBd_EGFbUT8)。  

-   它仅支持独立主站点。 不支持管理中心站点、多个主站点或辅助站点。  

Configuration Manager 的技术预览分支支持以下产品和技术： 

-   它仅支持 SQL Server 的以下版本：  

    -   从 Configuration Manager 版本 1710 开始的 SQL Server 2017（含累积更新 2 及更高版本）
    -   SQL Server 2016（不带 Service Pack）及更高版本
    -   SQL Server 2014（含 Service Pack 1）及更高版本
    -   SQL Server 2012（含 Service Pack 3）或更高版本  


-   站点最多支持 10 个客户端，这些客户端必须运行 Windows 的以下版本之一：  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

> [!Note]  
> 在此内容中包含这些产品并不意味着支持超出其支持生命周期以外的版本。 Configuration Manager 不支持超出其支持生命周期以外的产品。 有关详细信息，请参阅 [Microsoft 生命周期策略](https://go.microsoft.com/fwlink/p/?LinkId=208270)。  



##  <a name="bkmk_install"></a>安装和更新  

供实验室使用的 Configuration Manager 技术预览分支与供生产使用的 Configuration Manager 当前分支有所不同。  

首先安装技术预览分支的基线版本。 安装基线版本之后，使用控制台内部更新来升级此内部版本，以便使用最新预览版使你的安装程序保持最新。 通常，每个月都会提供新版本的技术预览版。

Microsoft 将支持每个技术预览版，直到三个连续的版本可用为止。 例如，当版本 1708 发布后，版本 1704 将不再受支持。 版本 1705、1706 和 1707 仍将受支持。 当某个基线版本不受支持后，它仍支持安装新的技术预览版站点（假设你立即更新到支持的版本）。 较旧的基线版本将继续受支持，直到有新的可用的基线版本为止。 从基线版本更新到最新可用版本，然后重复更新过程，直到安装最新技术预览版为止。

> [!TIP]  
>  向 Technical Preview 安装更新后，即可将 Preview 安装更新到这个新的 Technical Preview 版本。 技术预览版安装永远不会有升级到当前分支安装的选项。 它也永远不会接收来自当前分支版本的更新。 
> 
> 技术预览分支和当前分支版本在一年中有几次使用相同的版本号。 例如，有一个技术预览版 1802 和一个当前分支版本 1802。 

   
### <a name="active-baseline-versions"></a>活动基线版本
   
在基线版本发布后的 1 年内安装此基线版本。 在安装新的技术预览版站点时，如果当前有多个可用的基线版本，则使用最新的基线版本。

-  技术预览版 1806：Configuration Manager 技术预览版 1806 可同时用作控制台内更新和新的基线版本。 [从 TechNet 评估中心](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)下载基线版本。



##  <a name="BKMK_TPFeedback"></a> 提供反馈  

欢迎提供有关技术预览版新功能的反馈。 有关详细信息，请参阅[产品反馈](/sccm/core/understand/find-help#product-feedback)。

如果你对于想要看到的新功能有任何想法，也请让我们知道。 若要提交新的想法，并为他人提交的想法投票，请[访问我们的 UserVoice 页面](https://configurationmanager.uservoice.com)。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> 最新版本中的功能  

以下是最新 Configuration Manager 技术预览版中提供的功能： 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1807"></a>技术预览版 1807

- [社区中心](capabilities-in-technical-preview-1807.md#bkmk_hub) <!--1357766-->
- [指定用于为脱机 OS 映像提供服务的驱动器](capabilities-in-technical-preview-1807.md#bkmk_osd) <!--1358924-->
- [来自 Intune 的共同管理的设备同步活动](capabilities-in-technical-preview-1807.md#bkmk_comgmt) <!--1358565-->
- [修复应用程序](capabilities-in-technical-preview-1807.md#bkmk_app-repair) <!--1357866-->
- [通过电子邮件批准应用程序请求](capabilities-in-technical-preview-1807.md#bkmk_email-approve) <!--1321550-->
- [对脚本输出的改进](capabilities-in-technical-preview-1807.md#bkmk_script) <!--1236459-->
- [对第三方软件更新的改进](capabilities-in-technical-preview-1807.md#bkmk_3pupdate) <!--1358714-->

> [!Note]  
> 某个旧版技术预览中可用的功能在其后的版本中仍然可用。 同样，已添加到 Configuration Manager 当前分支的功能在技术预览分支中仍然可用。   



## <a name="features-in-recent-supported-technical-previews"></a>最新受支持的技术预览版中的功能

以下是旧版 Configuration Manager 技术预览分支发布且依然受支持的功能： 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |功能 |技术预览版 |当前分支版|  
 |----------------|---------------------|--------------------|
 | 分阶段部署改进 <!--1358577,1358147,1358578--> | [技术预览版 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_pod)  | ![未添加](media/Red_X.gif) |  
 | 支持新的 Windows 应用包格式 <!--1357427--> | [技术预览版 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_msix)  | ![未添加](media/Red_X.gif) |  
 | 客户端推送安全性改进 <!--1358204--> | [技术预览版 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_client-push)  | ![未添加](media/Red_X.gif) |  
 | 针对主动维护的管理见解 <!--1352184,et al--> | [技术预览版 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_insights)  | ![未添加](media/Red_X.gif) |  
 | 转移共同管理的设备的移动应用工作负载 <!--1357892--> | [技术预览版 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_comgmt)  | ![未添加](media/Red_X.gif) |  
 | 对等下载适用的边界组选项 <!--1356193--> | [技术预览版 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_bgoptions)  | ![未添加](media/Red_X.gif) |  
 | 自定义目录的第三方软件更新支持 <!--1358714--> | [技术预览版 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate)  | ![未添加](media/Red_X.gif) |  
 | 云管理功能改进 <!--511980,515854--> | [技术预览版 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_cloud)  | ![未添加](media/Red_X.gif) |  
 | 新的软件更新符合性报告 <!--1357775--> | [技术预览版 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_report)  | ![未添加](media/Red_X.gif) |  
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
 
  

## <a name="features-in-previous-technical-previews"></a>旧版技术预览版中的功能

以下是旧版 Configuration Manager 技术预览分支发布的功能。 这些功能在更高版本中保持可用，但在当前分支中不可用。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |功能 |技术预览版 |  
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
  
- [在实验室中评估 Configuration Manager](/sccm/core/get-started/evaluate-with-lab-environment)
- [Configuration Manager 增量版本中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Configuration Manager 简介](/sccm/core/understand/introduction)

> [!Tip]  
> 若要详细了解需要同意才能启用的当前分支功能，请参阅[预发布功能](/sccm/core/servers/manage/pre-release-features)。  
> 
> 若要详细了解必须先启用的当前分支功能，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。  
