---
title: 技术预览版
titleSuffix: Configuration Manager
description: 了解可测试 Configuration Manager 中的新功能和新特性的技术预览分支。
ms.date: 10/16/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f19e998e803bdaeed2b72dac84ae866930ad0003
ms.sourcegitcommit: 73dbd2146bd581a1b668b22b84b7cda68a487d05
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2018
ms.locfileid: "49390626"
---
# <a name="technical-preview-for-configuration-manager"></a>Configuration Manager 的技术预览版

*适用于： System Center Configuration Manager （技术预览版）*

本文提供了有关 Configuration Manager 的每月技术预览分支的详细信息。 技术预览版介绍 Microsoft 正在开发的新功能。 它介绍 Configuration Manager 当前分支中尚未包含的新功能。 这些功能可能最终会包含在当前分支的更新中。 在我们最终发布这些功能前，我们希望你试用这些功能并向我们提供反馈。  

由于此版本是技术预览版，因此详细信息和功能可能有所更改。  

此信息适用于 Configuration Manager 技术预览分支的所有版本。 本文列出了每个新功能以及该功能首次出现所在的技术预览版。 例如，版本 1809 为 2018 年 (18) 的 9 月 (09)。 单独的文章专用于详细介绍每个预览版的单独功能。  

有关 Configuration Manager 的当前版本 中新增功能的信息，请参阅 [Configuration Manager 增量版本中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)。



##  <a name="bkmk_reqs"></a>要求和限制  

> [!IMPORTANT]     
>  技术预览版仅授权用于实验室环境。 Microsoft 可能无法提供支持服务，预览软件中某些功能可能不可用。 此外，相对于面向市场提供的软件，预览版软件可能采用简化的或不同的安全性、隐私性、可访问性、可用性和可靠性标准。  

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

-  技术预览版 1810.2：Configuration Manager 技术预览版 1810.2 可同时用作控制台内更新和新的基线版本。 从 [TechNet 评估中心](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)下载基线版本。



##  <a name="BKMK_TPFeedback"></a> 提供反馈  

欢迎提供有关技术预览版新功能的反馈。 有关详细信息，请参阅[产品反馈](/sccm/core/understand/find-help#product-feedback)。

如果你对于想要看到的新功能有任何想法，也请让我们知道。 若要提交新的想法，并为他人提交的想法投票，请[访问我们的 UserVoice 页面](https://configurationmanager.uservoice.com)。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> 最新版本中的功能  

以下是最新 Configuration Manager 技术预览版中提供的功能： 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-18102"></a>技术预览版 1810.2

<!--capabilities-in-technical-preview-1810-2.md#bkmk_anchor-->

- [对集合评估的改进](capabilities-in-technical-preview-1810-2.md#bkmk_colleval) <!--1358981-->
- [Configuration Manager 管理员身份验证](capabilities-in-technical-preview-1810-2.md#bkmk_auth) <!--1357013-->
- [对等缓存源客户端版本的管理见解规则](capabilities-in-technical-preview-1810-2.md#bkmk_insights) <!--1358008-->
- [对基于 Internet 的客户端设置的改进](capabilities-in-technical-preview-1810-2.md#bkmk_cmg) <!--1359181-->
- [将应用程序转换为 MSIX](capabilities-in-technical-preview-1810-2.md#bkmk_msix) <!--1359029-->
- [更改了用于唤醒设备的客户端通知操作](capabilities-in-technical-preview-1810-2.md#bkmk_wakeup) <!--1317364-->


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
 | 客户端安装改进<!--1358840--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_ccmsetup) | ![未添加](media/Red_X.gif) | 
 | 共同托管设备所需的应用符合性策略<!--1358196--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_app-compliance) | ![未添加](media/Red_X.gif) | 
 | 对共同管理仪表板的改进<!--1358980--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_comgmt-report) | ![未添加](media/Red_X.gif) | 
 | 新的边界组选项<!--1358749--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_bgoptions) | ![未添加](media/Red_X.gif) | 
 | Windows 群集节点上的站点系统<!--1359132--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_cluster) | ![未添加](media/Red_X.gif) | 
 | CMPivot 的改进 <!--1359068--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_cmpivot) | ![未添加](media/Red_X.gif) | 
 | 脚本的改进<!--1358239--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_scripts) | ![未添加](media/Red_X.gif) | 
 | 用于唤醒设备的新客户端通知操作<!--1317364--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_wakeup) | ![未添加](media/Red_X.gif) | 
 | 对边界组的任务序列支持<!--1359025--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_bgr-osd) | ![未添加](media/Red_X.gif) | 
 | 管理见解仪表板<!--1357979--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_insights) | ![未添加](media/Red_X.gif) | 
 | 控制台内文档仪表板<!--1357546--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) | ![未添加](media/Red_X.gif) | 
 | 对驱动程序维护的改进<!--1358270--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_drivers) | ![未添加](media/Red_X.gif) | 
 | 针对现有设备的 Windows Autopilot 的任务序列支持<!--1358333--> | [技术预览版 1810](capabilities-in-technical-preview-1810.md#bkmk_autopilot) | ![未添加](media/Red_X.gif) | 
 | CMPivot 的改进 <!--1359068--> | [技术预览版 1809](capabilities-in-technical-preview-1809.md#bkmk_cmpivot) | ![未添加](media/Red_X.gif) | 
 | 生命周期仪表板的改进 <!--1358702--> | [技术预览版 1809](capabilities-in-technical-preview-1809.md#bkmk_lifecycle) | ![未添加](media/Red_X.gif) | 
 | 数据仓库的改进 <!--1358870--> | [技术预览版 1809](capabilities-in-technical-preview-1809.md#bkmk_dataw) | ![未添加](media/Red_X.gif) | 
 | 软件更新的维护时段的改进 <!--vso2839307--> | [技术预览版 1809](capabilities-in-technical-preview-1809.md#bkmk_sum-mw) | ![未添加](media/Red_X.gif) | 
 | 软件更新的分阶段部署 <!--1358146--> | [技术预览版 1808](capabilities-in-technical-preview-1808.md#bkmk_pod) | ![未添加](media/Red_X.gif) | 
 | 修复应用程序的改进 <!--1357866--> | [技术预览版 1808](capabilities-in-technical-preview-1808.md#bkmk_repair) | ![未添加](media/Red_X.gif) | 



## <a name="features-in-previous-technical-previews"></a>旧版技术预览版中的功能

以下是旧版 Configuration Manager 技术预览分支发布的功能。 这些功能在更高版本中保持可用，但在当前分支中不可用。 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

|功能 |Technical Preview 版本 |  
|----------------|---------------------|
| 社区中心 <!--1357766--> | [技术预览版 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | 
| 指定用于为脱机 OS 映像提供服务的驱动器 <!--1358924--> | [技术预览版 1807](capabilities-in-technical-preview-1807.md#bkmk_osd) | 
| 来自 Intune 的共同管理的设备同步活动 <!--1358565--> | [技术预览版 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | 
| 修复应用程序 <!--1357866--> | [技术预览版 1807](capabilities-in-technical-preview-1807.md#bkmk_app-repair) | 
| 通过电子邮件批准应用程序请求 <!--1321550--> | [技术预览版 1807](capabilities-in-technical-preview-1807.md#bkmk_email-approve) | 
| 对脚本输出的改进 <!--1236459--> | [技术预览版 1807](capabilities-in-technical-preview-1807.md#bkmk_script) | 
| 对第三方软件更新的改进 <!--1358714--> | [技术预览版 1807](capabilities-in-technical-preview-1807.md#bkmk_3pupdate) |
|支持中心 <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | 
|基于客户端的 PXE 响应者服务 <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
|PXE 网络启动对 IPv6 的支持 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
|使用 Azure Active Directory<!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
|Windows Update for Business 更新的符合性评估 <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
|OData 终结点数据访问 <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
|对资产智能的改进<!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
|最终用户可从公司门户安装应用 <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>另请参阅  

有关详细信息，请参阅下列文章：  

- [在实验室中评估 Configuration Manager](/sccm/core/get-started/evaluate-with-lab-environment)
- [Configuration Manager 增量版本中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Configuration Manager 简介](/sccm/core/understand/introduction)

> [!Tip]  
> 若要详细了解需要同意才能启用的当前分支功能，请参阅[预发布功能](/sccm/core/servers/manage/pre-release-features)。  
> 
> 若要详细了解必须先启用的当前分支功能，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。  
