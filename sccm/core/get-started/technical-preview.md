---
title: 技术预览版
titleSuffix: Configuration Manager
description: 了解可测试 Configuration Manager 中的新功能和新特性的技术预览分支。
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6e4475e5db6562fc95d3fafc7c88805b2df53075
ms.sourcegitcommit: d1df13fc95a1f1540177c294555d9be26161b9cb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974141"
---
# <a name="technical-preview-for-configuration-manager"></a>Configuration Manager 的技术预览版

适用范围：  System Center Configuration Manager（技术预览版）

本文提供了有关 Configuration Manager 的每月技术预览分支的详细信息。 技术预览版介绍 Microsoft 正在开发的新功能。 它介绍 Configuration Manager 当前分支中尚未包含的新功能。 这些功能可能最终会包含在当前分支的更新中。 在我们最终发布这些功能前，我们希望你试用这些功能并向我们提供反馈。  

由于此版本是技术预览版，因此详细信息和功能可能有所更改。  

此信息适用于 Configuration Manager 技术预览分支的所有版本。 本文列出了每个新功能以及该功能首次出现所在的技术预览版。 例如，版本 1901 为 2019 年 (19) 的 1 月 (01)  。 单独的文章专用于详细介绍每个预览版的单独功能。  

有关 Configuration Manager 的当前版本  中新增功能的信息，请参阅 [Configuration Manager 增量版本中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)。

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
    > 更新可用于预览版本时，仍从 Configuration Manager 控制台的“更新与维护服务”  节点查找并安装它们。 有关控制台中升级过程的视频，请观看 youtube.com 上的[安装 Configuration Manager 更新包](https://www.youtube.com/embed/KBd_EGFbUT8)。  

- 它仅支持独立主站点。 不支持管理中心站点、多个主站点或辅助站点。  

Configuration Manager 的技术预览分支支持以下产品和技术：

- 它仅支持 SQL Server  的以下版本：  

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

### <a name="technical-preview-version-1905"></a>技术预览版 1905

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

- [改进了对 WSUS 维护的控制](/sccm/core/get-started/2019/technical-preview-1905#improved-control-over-wsus-maintenance) <!--4110109-->
- [对 Configuration Manager 控制台的改进](/sccm/core/get-started/2019/technical-preview-1905#bkmk_console) <!--4616810-->
- [配置软件更新的默认最长运行时间](/sccm/core/get-started/2019/technical-preview-1905#bkmk_timeout) <!--3734426-->
- [Windows Defender 应用程序防护文件信任标准](/sccm/core/get-started/2019/technical-preview-1905#bkmk_wdag) <!--3555858-->
- [应用程序组](/sccm/core/get-started/2019/technical-preview-1905#bkmk_app-group) <!--3555907-->
- [作为应用模型部署类型的任务序列](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdt) <!--3555953-->
- [BitLocker 管理](/sccm/core/get-started/2019/technical-preview-1905#bkmk_bitlocker) <!--3601034-->
- [任务序列调试器](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdebug) <!--3612274-->
- [客户端数据源仪表板中的传递优化](/sccm/core/get-started/2019/technical-preview-1905#bkmk_do) <!--3555759-->
- [对社区中心的改进](/sccm/core/get-started/2019/technical-preview-1905#bkmk_hub) <!--4224401-->
- [在设备列表中查看 SMBIOS GUID](/sccm/core/get-started/2019/technical-preview-1905#bkmk_smbios) <!--4526580-->
- [OneTrace 日志查看器](/sccm/core/get-started/2019/technical-preview-1905#bkmk_onetrace) <!--3555962-->
- [软件中心基础结构改进](/sccm/core/get-started/2019/technical-preview-1905#bkmk_swctr) <!--3555950-->
- [对软件中心选项卡自定义项的改进](/sccm/core/get-started/2019/technical-preview-1905#improvements-to-software-center-tab-customizations) <!--4063773-->
- [对应用审批的改进](/sccm/core/get-started/2019/technical-preview-1905#bkmk_approve) <!--4224910-->
- [重试安装预先批准的应用程序](/sccm/core/get-started/2019/technical-preview-1905#bkmk_retry) <!--4336307-->
- [为设备安装应用程序](/sccm/core/get-started/2019/technical-preview-1905#bkmk_device-app) <!--4402180-->
- [更频繁的重启倒计时通知](/sccm/core/get-started/2019/technical-preview-1905#bkmk_restart) <!--3976435-->
- [将集合成员身份结果同步到 Azure Active Directory 组](/sccm/core/get-started/2019/technical-preview-1905#bkmk_aadcollsync) <!--3607475-->
- [配置客户端缓存最短保持期](/sccm/core/get-started/2019/technical-preview-1905#bkmk_cache) <!--4485509-->
- [对 OS 部署的改进](/sccm/core/get-started/2019/technical-preview-1905#bkmk_osd) <!--4512937,4224642-->
- [添加 SQL AlwaysOn 节点](/sccm/core/get-started/2019/technical-preview-1905#bkmk_sqlao) <!--3127336-->

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
 | Office 365 专业增强版升级就绪情况仪表板 <!--4021125--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_o365) | ![未添加](media/Red_X.gif) |
 | 配置功能更新的动态更新 <!--4062619--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#configure-dynamic-update-during-feature-updates) | ![未添加](media/Red_X.gif) |
 | 社区中心和 GitHub <!--3555935,3555936--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) | ![未添加](media/Red_X.gif) |
 | CMPivot 独立应用 <!--3555890--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_cmpivot) | ![未添加](media/Red_X.gif) |
 | 软件中心基础结构的改进 <!--3555950--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_swctr) | ![未添加](media/Red_X.gif) |
 | 改进了对 WSUS 维护的控制 <!--4110109--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#improved-control-over-wsus-maintenance) | ![未添加](media/Red_X.gif) |
 | 预缓存驱动程序包和 OS 映像 <!--4224642--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_precache) | ![未添加](media/Red_X.gif) |
 | 对 OS 部署的改进 <!--2839943,4447680--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_osd) | ![未添加](media/Red_X.gif) |
 | 云服务成本估算器 <!--3555774--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) | ![未添加](media/Red_X.gif) |
 | 将分发点用作传递优化的本地缓存服务器 <!--3555764--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_doinc) | ![未添加](media/Red_X.gif) |
 | 回收锁定以编辑任务序列 <!--3699337--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_sedo) | ![未添加](media/Red_X.gif) |
 | 钻取必需更新 <!--4224414--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_req-updates) | ![未添加](media/Red_X.gif) |
 | 对任务序列媒体创建的改进 <!--4090666--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_tsmedia) | ![未添加](media/Red_X.gif) |
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


## <a name="features-in-previous-technical-previews"></a>旧版技术预览版中的功能

以下是旧版 Configuration Manager 技术预览分支发布的功能。 这些功能在更高版本中保持可用，但在当前分支中不可用。

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| 功能        | 技术预览版 |  
|----------------|---------------------------|
| 从社区中心下载报表<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
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
