---
title: 技术预览版
titleSuffix: Configuration Manager
description: 了解可测试 Configuration Manager 中的新功能和新特性的技术预览分支。
ms.date: 04/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2909de734954d9519c04bc02012c3bfe17c9b81f
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802506"
---
# <a name="technical-preview-for-configuration-manager"></a>Configuration Manager 的技术预览版

适用范围：System Center Configuration Manager（技术预览版）

本文提供了有关 Configuration Manager 的每月技术预览分支的详细信息。 技术预览版介绍 Microsoft 正在开发的新功能。 它介绍 Configuration Manager 当前分支中尚未包含的新功能。 这些功能可能最终会包含在当前分支的更新中。 在我们最终发布这些功能前，我们希望你试用这些功能并向我们提供反馈。  

由于此版本是技术预览版，因此详细信息和功能可能有所更改。  

此信息适用于 Configuration Manager 技术预览分支的所有版本。 本文列出了每个新功能以及该功能首次出现所在的技术预览版。 例如，版本 1901 为 2019 年 (19) 的 1 月 (01)。 单独的文章专用于详细介绍每个预览版的单独功能。  

有关 Configuration Manager 的当前版本 中新增功能的信息，请参阅 [Configuration Manager 增量版本中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)。

> [!Tip]  
> 若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_reqs"></a>要求和限制  

> [!IMPORTANT]  
> 技术预览版仅授权用于实验室环境。 Microsoft 可能无法提供支持服务，预览软件中某些功能可能不可用。 此外，相对于面向市场提供的软件，预览版软件可能采用简化的或不同的安全性、隐私性、可访问性、可用性和可靠性标准。  

有关大多数产品的先决条件，请使用[支持的配置](/sccm/core/plan-design/configs/supported-configurations)中的信息。 以下是适用于技术预览分支的例外情况：  

- 每次安装在活动状态 90 天后变为非活动状态。  

- 英语是唯一受支持的语言。  

- 它仅支持以下安装命令行参数：  

    - `/silent`  
    - `/testdbupgrade`  

- 服务连接点安装为联机模式。 它不支持脱机模式。  

- 每个特定版本的 Technical Preview 的单独文章中包括其他限制或要求（如果适用）。

- 以下功能在技术预览分支中不受支持：  

    - [迁移](/sccm/core/migration/migrate-data-between-hierarchies)到此预览分支或从此预览分支迁移。  

    - [升级](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)到此预览分支。  

    - cd.latest 文件夹中的[站点恢复](/sccm/core/servers/manage/recover-sites)。  <!--507106-->

- 不支持从此预览分支更新到当前分支。  

    > [!Note]  
    > 更新可用于预览版本时，仍从 Configuration Manager 控制台的“更新与维护服务”节点查找并安装它们。 有关控制台中升级过程的视频，请观看 youtube.com 上的[安装 Configuration Manager 更新包](https://www.youtube.com/embed/KBd_EGFbUT8)。  

- 它仅支持独立主站点。 不支持管理中心站点、多个主站点或辅助站点。  

Configuration Manager 的技术预览分支支持以下产品和技术：

- 它仅支持 SQL Server 的以下版本：  

    - SQL Server 2017（带累积更新 2 或更高版本）
    - SQL Server 2016（不带服务包或更高版本）
    - SQL Server 2014（含服务包 1 或更高版本）
    - SQL Server 2012（含服务包 3 或更高版本）  

- 站点最多支持 10 个客户端，这些客户端必须运行 Windows 的以下版本之一：  

    - Windows 10  
    - Windows 8.1  
    - Windows 7  

> [!Note]  
> 在此内容中包含这些产品并不意味着支持超出其支持生命周期以外的版本。 Configuration Manager 不支持超出其支持生命周期以外的产品。 有关详细信息，请参阅 [Microsoft 生命周期策略](https://go.microsoft.com/fwlink/p/?LinkId=208270)。  

## <a name="bkmk_install"></a>安装和更新  

供实验室使用的 Configuration Manager 技术预览分支与供生产使用的 Configuration Manager 当前分支有所不同。  

首先安装技术预览分支的基线版本。 安装基线版本之后，使用控制台内部更新来升级此内部版本，以便使用最新预览版使你的安装程序保持最新。 通常，每个月都会提供新版本的技术预览版。

Microsoft 将支持每个技术预览版，直到三个连续的版本可用为止。 例如，当版本 1708 发布后，版本 1704 将不再受支持。 版本 1705、1706 和 1707 仍将受支持。 当某个基线版本不受支持后，它仍支持安装新的技术预览版站点（假设你立即更新到支持的版本）。 较旧的基线版本将继续受支持，直到有新的可用的基线版本为止。 从基线版本更新到最新可用版本，然后重复更新过程，直到安装最新技术预览版为止。

> [!TIP]  
> 向 Technical Preview 安装更新后，即可将 Preview 安装更新到这个新的 Technical Preview 版本。 技术预览版安装永远不会有升级到当前分支安装的选项。 它也永远不会接收来自当前分支版本的更新。
>
> 技术预览分支和当前分支版本在一年中有几次使用相同的版本号。 例如，有一个技术预览版 1802 和一个当前分支版本 1802。

### <a name="active-baseline-versions"></a>活动基线版本

在基线版本发布后的 1 年内安装此基线版本。 在安装新的技术预览版站点时，如果当前有多个可用的基线版本，则使用最新的基线版本。

- **技术预览版 1902.2**：Configuration Manager 技术预览版 1902.2 可同时用作控制台内更新和新的基线版本。 从 [TechNet 评估中心](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)下载基线版本。

## <a name="BKMK_TPFeedback"></a> 提供反馈  

欢迎提供有关技术预览版新功能的反馈。 有关详细信息，请参阅[产品反馈](/sccm/core/understand/find-help#product-feedback)。

如果你对于想要看到的新功能有任何想法，也请让我们知道。 若要提交新的想法，并为他人提交的想法投票，请[访问我们的 UserVoice 页面](https://configurationmanager.uservoice.com)。  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->

## <a name="bkmk_tpCaps"></a> 最新版本中的功能  

以下是最新 Configuration Manager 技术预览版中提供的功能：

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1903"></a>技术预览版 1903

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

- [云服务成本估算器](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) <!--3555774-->  

- [将分发点用作传递优化的本地缓存服务器](/sccm/core/get-started/2019/technical-preview-1903#bkmk_doinc) <!--3555764-->  

- [回收锁定以编辑任务序列](/sccm/core/get-started/2019/technical-preview-1903#bkmk_sedo) <!--3699337-->  

- [深入查看所需更新](/sccm/core/get-started/2019/technical-preview-1903#bkmk_req-updates) <!--4224414-->  

- [对任务序列媒体创建的改进](/sccm/core/get-started/2019/technical-preview-1903#bkmk_tsmedia) <!--4090666-->  

> [!Note]  
> 某个旧版技术预览中可用的功能在其后的版本中仍然可用。 同样，已添加到 Configuration Manager 当前分支的功能在技术预览分支中仍然可用。  

## <a name="features-in-recent-supported-technical-previews"></a>最新受支持的技术预览版中的功能

以下是旧版 Configuration Manager 技术预览分支发布且依然受支持的功能：

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 | 功能 | 技术预览版 | 当前分支版 |  
 |---------|---------------------------|------------------------|
 | Office 365 更新的其他语言 <!--3555955--> | [技术预览版 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_o365lang) | 版本 1902 |
 | Office 365 专业增强版与分析集成的就绪情况 <!--3735402--> | [技术预览版 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_o365) | 版本 1902 |
 | 对分阶段部署成功标准的改进 <!--3555946--> | [技术预览版 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_pod) | 版本 1902 |
 | 对增强型 HTTP 的改进 <!--3798957--> | [技术预览版 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_ehttp) | 版本 1902 |
 | 使用对话框窗口替换 toast 通知 <!--3555947--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_impact) | 版本 1902 |
 | 就地升级任务序列期间的进度状态 <!--3747129--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_ipu) | 版本 1902 |
 | 将 Windows 已知文件夹重定向到 OneDrive <!--3556021--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_odfb) | 版本 1902 |
 | 在远程控制期间仅查看第一个屏幕 <!--3231732--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_rcmulti) | 版本 1902 |
 | 编辑或复制 PowerShell 脚本 <!--3705507--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_psedit) | 版本 1902 |
 | 将云管理网关添加到边界组 <!--3640932--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_cmgbg) | 版本 1902 |
 | 在软件中心配置默认视图 <!--3612112--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_swctr) | 版本 1902 |
 | 对客户端运行状况仪表板所做的改进 <!--3599209--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_health) | 版本 1902 |
 | 客户端运行状况仪表板 <!--3599209--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_health) | 版本 1902 |
 | 在 Windows 10 维护服务中指定功能更新的优先级 <!--3734525--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_neo) | 版本 1902 |
 | 分阶段部署专用监视 <!--3555949--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_pod) | 版本 1902 |
 | 从管理中心站点运行 CMPivot <!--3610960--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmpivot) | 版本 1902 |
 | 对运行 PowerShell 脚本任务序列步骤的改进 <!--3556028--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_posh) | 版本 1902 |
 | 生命周期仪表板上的 Office 产品 <!--3556026--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_lifecycle) | 版本 1902 |
 | 集合的管理见解规则 <!--3555752--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_micoll) | 版本 1902 |
 | 使用 MAC 地址搜索设备视图 <!--3600878--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_mac) | 版本 1902 |
 | 分发点维护模式 <!--3555754--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_dpmaint) | 版本 1902 |
 | 经优化的映像维护 <!--3555951--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_resetbase) | 版本 1902 |
 | 导入 OS 映像的单个索引 <!--3719699--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_index) | 版本 1902 |
 | 使用云服务适用的 Azure 资源管理器 <!--3605704--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_arm) | 版本 1902 |
 | 确认控制台反馈 <!--3556010--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_feedback) | 版本 1902 |
 | 在 Azure 中创建 Configuration Manager 技术预览实验室 <!--3556017--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_azurevm) | 不适用 |
 | 指定一个自定义端口用于对等唤醒 <!--3605925--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_sleep) | 版本 1902 |
 | 查看最近连接的控制台 <!--3699367--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_console) | 版本 1902 |
 | 超过阈值时停止云服务 <!--3735092--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmg) | 版本 1902 |
 | 客户端预配模式超时 <!--3197824--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osdprov) | 版本 1902 |
 | 对 OS 部署的改进 <!--3633146,3641475,3654172,3734270--> | [技术预览 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osd) | 版本 1902 |
 | 对运行 PowerShell 脚本任务序列步骤的改进 <!--3556028 fka 1359389--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_posh) | 版本 1902 |
 | 对通过电子邮件进行的应用程序批准的改进 <!--3594063--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_email) | 版本 1902 |
 | 在软件中心中配置用户设备相关性 <!--3485366--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_uda) | 版本 1902 |
 | 对 Configuration Manager 控制台的改进 <!--3594151--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_console) | 版本 1902 |
 | 从社区中心下载报表<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) | ![未添加](media/Red_X.gif) |

## <a name="features-in-previous-technical-previews"></a>旧版技术预览版中的功能

以下是旧版 Configuration Manager 技术预览分支发布的功能。 这些功能在更高版本中保持可用，但在当前分支中不可用。

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| 功能        | 技术预览版 |  
|----------------|---------------------------|
| 社区中心 <!--3556020, fka 1357766--> | [技术预览版 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| 基于客户端的 PXE 响应者服务 <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE 网络启动对 IPv6 的支持 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| 使用 Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| 对资产智能的改进 <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| 最终用户可从公司门户安装应用 <!--3601249, fka 1037233--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |

## <a name="see-also"></a>另请参阅  

有关详细信息，请参阅下列文章：  

- [在实验室中评估 Configuration Manager](/sccm/core/get-started/evaluate-with-lab-environment)
- [Configuration Manager 增量版本中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Configuration Manager 简介](/sccm/core/understand/introduction)

> [!Tip]  
> 若要详细了解需要同意才能启用的当前分支功能，请参阅[预发布功能](/sccm/core/servers/manage/pre-release-features)。  
>
> 若要详细了解必须先启用的当前分支功能，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。  
