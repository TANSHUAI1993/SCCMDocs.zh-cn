---
title: "Technical Preview 版本"
titleSuffix: Configuration Manager
description: "了解可让你试用 System Center Configuration Manager 中的新功能和新特性的 Technical Preview 版本。"
ms.custom: na
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 975bd66bb86efb133ccd7017295e8108558f633d
ms.sourcegitcommit: db9978135d7a6455d83dbe4a5175af2bdeaeafd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview

*适用范围：System Center Configuration Manager (Technical Preview)*

**欢迎使用 System Center Configuration Manager Technical Preview**。 本文提供了有关不断完善的预览版的详细信息，该版本包括我们正在开发的功能。 每个版本的 Technical Preview 都会引入尚未包含在 Configuration Manager 的 Current Branch 中的新功能。 这些功能最终可能会包含在当前分支版本的更新中，但在确定和添加功能之前，我们希望你有机会试用它们并向我们提供反馈。  

 由于此版本是技术预览版，因此详细信息和功能可能有所更改。  

 本文包含适用于所有版本的 Technical Preview 的信息。 它还列出了每个新功能及其首次出现的 Technical Preview 版本，例如版本 1801 表示 2018 年 1 月。 这些功能将专门在各预览版的单独主题中详细介绍。  

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
>  当你将更新安装到技术预览版时，即可将预览安装更新到此新的技术预览版。    技术预览版安装绝不会升级到当前的分支安装，也不会从当前分支版本获取更新。  

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

### <a name="technical-preview-version-1801"></a>Technical Preview 版本 1801
- [创建分阶段部署](capabilities-in-technical-preview-1801.md#create-phased-deployments)<!-- 1357405 --> 
- [共同管理报告](capabilities-in-technical-preview-1801.md#co-management-reporting)<!-- 1356648 --> 
- [自动部署规则评估计划改进](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule)<!-- 1357133 --> 
- [重新分配分发点](capabilities-in-technical-preview-1801.md#reassign-distribution-point)<!-- 1306937 --> 
- [硬件清单改进](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory)<!-- 1357389 --> 
- [软件中心的客户端设置改进](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center)<!-- 1355146 --> 
- [新的 Windows Defender 应用程序防护设置](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard)<!-- 1356256 --> 
- [运行脚本的改进](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts)<!-- 1236459 --> 




## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>最新受支持的 Technical Preview 中提供的功能
以下是旧版 Configuration Manager Technical Preview 提供且依然受支持的功能。 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |功能 |Technical Preview 版本 |Current Branch 版本|  
 |----------------|---------------------|--------------------|
 |不自动升级被取代的应用程序<!-- 1351266 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications)  |![未添加](media/Red_X.gif)    | 
 |安装软件中心中的多个应用程序<!-- 1357126 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center)  |![未添加](media/Red_X.gif)    |
 |Configuration Manager 客户端安装中的更改<!-- 1356195 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install)  |![未添加](media/Red_X.gif)    | 
 |对 Surface 设备仪表板的更改<!-- 1355788 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard)  |![未添加](media/Red_X.gif)    | 
 |对 Office 365 客户端管理仪表板的改进<!-- 1357281 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard)  |![未添加](media/Red_X.gif)    | 
 |对 Configuration Manager 控制台的改进<!-- 1357280,1357282 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console)  |![未添加](media/Red_X.gif)    | 
 |对操作系统部署的改进<!-- SMS 500897 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment)  |![未添加](media/Red_X.gif)    | 
 |运行任务序列步骤 <!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |[版本 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence)    |
 |允许在安装应用程序时进行用户交互<!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![未添加](media/Red_X.gif)    |
 |Windows Analytics 设备运行状况的 Windows 10 遥测 <!--1356148 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health) |[版本 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#reporting)    |
 |对软件中心图标的改进 <!-- 1356194 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#software-center-no-longer-distorts-icons-larger-than-250x250) |[版本 1710](/sccm/apps/plan-design/plan-for-and-configure-application-management#supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center)    |
 |检查软件中心中共同托管的设备的符合性<!-- 1356374 -->|[Tech Preview 1710](capabilities-in-technical-preview-1710.md#check-compliance-from-software-center-for-co-managed-devices)|[版本 1710](/sccm/core/clients/manage/co-management-overview)    |
 |对 CNG 证书的有限支持<!-- 1356191 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limited-support-for-cng-certificates)|[版本 1710](/sccm/core/plan-design/network/cng-certificates-overview)    |
 |对攻击防护的支持 <!--1355468 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#support-for-exploit-guard) |[版本 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)    |
 |对挂起的计算机重启的改进性说明   <!-- 1356283  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[版本 1710](/sccm/core/clients/manage/manage-clients)    |
 |设备防护策略更改   <!-- 1355092  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[版本 1710](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)    |
 |配置和部署 Windows Defender 应用程序防护策略   <!-- 1351960  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[版本 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)    |
 |针对从 Configuration Manager 部署 PowerShell 脚本的改进<!-- 1236459 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#improvements-for-deploying-powershell-scripts-from-configuration-manager) | [版本 1710](/sccm/apps/deploy-use/create-deploy-scripts)
 

## <a name="capabilities-delivered-in-previous-technical-previews"></a>以前的技术预览版中提供的功能
以下是旧版 Configuration Manager Technical Preview 提供的特定功能。 这些功能在更高版本中保持可用，但在 Current Branch 版本中还不可用。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |功能 |Technical Preview 版本 |  
 |----------------|---------------------|
 |Configuration Manager 控制台中改进了 VPN 配置文件体验<!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |
 |管理见解<!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|
 |Surface 设备仪表板 <!-- 1355788 --> |[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|
 |站点服务器角色的高可用性 <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |PXE 网络启动对 IPv6 的支持 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |用于条件访问的符合性策略的“设备运行状况证明”评估 <!-- 1235616 -->|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|
 |使用 Azure Active Directory<!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Windows Update for Business 更新的符合性评估 <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |OData 终结点数据访问 <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |对资产智能的改进<!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |最终用户可从公司门户安装应用 <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>另请参阅  
[System Center Configuration Manager 中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [System Center Configuration Manager 简介](../../core/understand/introduction.md)
