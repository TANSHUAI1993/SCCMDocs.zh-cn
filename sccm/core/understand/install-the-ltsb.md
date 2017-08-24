---
title: "安装使用 1606 基线介质的站点 | Microsoft Docs"
description: "安装或升级到 System Center Configuration Manager 的 LTSB。"
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 39653604ba5fd8e1fe9dd4d42889221d983f9bec
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media-for-system-center-configuration-manager"></a>使用 1606 版基线介质安装或升级 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch) 和 (Long-Term Servicing Branch)*

运行 Configuration Manager 的版本 1606 基线媒体中的安装程序时，可以安装 System Center Configuration Manager 的 Long-Term Servicing Branch 或 Current branch 网站。

此基线介质以 DVD 形式提供，包含在 Microsoft System Center 2016 或 System Center Configuration Manager（Current Branch 和 Long-Term Servicing Branch 1606）版本中。 若要了解有关基线介质的信息，请参阅[基线和更新版本](/sccm/core/servers/manage/updates#baseline-and-udpate-versions)。


如果使用 1606 版基线介质，安装（或升级到）的站点为：
- Current Branch 站点，等效于先使用 1511 版基线介质安装，然后再更新为 1606 版和 1606 修补程序汇总 (KB3186654) 的站点。
-   LTSB 站点，等效于运行 1606 版和 1606 修补程序汇总 (KB3186654) 的 Current Branch 站点。 基线介质已包括修补程序汇总。  但是，LTSB 不支持 Current Branch 中可用的所有功能，如 [System Center Configuration Manager 的 Long-Term Servicing Branch 简介](introduction-to-the-ltsb.md)中所述。

如果不熟悉 System Center Configuration Manager 的不同分支，请参阅[应使用 Configuration Manager 的哪一个分支](which-branch-should-i-use.md)。




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>1606 基线介质中安装程序的更改
1606 基线介质引入了对 Configuration Manager 的安装程序的以下更改。

### <a name="branch-and-edition"></a>分支和版本
运行安装程序时，将出现一个许可页面，可以在该页面选择要安装的 Configuration Manager 分支。 可以选择 Current Branch 或 LTSB 作为许可安装，或选择 Current Branch 的评估版作为非许可安装。

有关详细信息，请参阅 [System Center Configuration Manager 的许可和分支](learn-more-editions.md)。

### <a name="software-assurance-expiration"></a>软件保障到期日期
安装过程中，可以选择输入“软件保障到期日期”值。 这是一个可选值，可指定用于提醒。

> [!NOTE]
> Microsoft 不会验证输入的到期日期，且不会将此日期用作许可证验证。  相反，可以使用该日期作为到期日期提醒。 这很有用，因为 Configuration Manager 定期检查在线提供的新软件更新，而软件保障许可证应为最新状态，以便有资格使用这些额外的更新。    

- 从 System Center Configuration Manager 1606 版基线介质运行安装程序时，可以在安装向导的“产品密钥”页指定日期值。
- 还可以通过在 Configuration Manager 控制台中选择“层次结构设置属性” > “许可”来指定此日期。

有关详细信息，请参阅 [System Center Configuration Manager 的许可和分支](learn-more-editions.md)中的“软件保障协议”。


### <a name="additional-pre-upgrade-configurations"></a>其他升级前的配置
开始将 System Center 2012 Configuration Manager 升级到 LTSB 之前，作为升级前清单的一部分，必须执行以下附加步骤。  
卸载 LTSB 不支持的站点系统角色：
- 资产智能同步点
- Microsoft Intune 连接器
- 基于云的分发点

有关详细信息，请参阅[升级到 System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)。


### <a name="new-scripted-installation-options"></a>新的脚本化安装选项
1606 版基线介质支持新的、无人参与的脚本文件密钥，该密钥用于新的顶层站点的脚本化安装。 此功能适用于安装新的独立主站点，或添加作为站点扩展方案一部分的管理中心站点。

使用无人参与的脚本安装许可的分支时，必须向脚本的“选项”部分添加以下部分、密钥名称和值。 不需要使用这些值来编写 Current Branch 评估版的安装的脚本：  

 **SABranchOptions**
-   **密钥名称：SAActive**
  - 值：0 或 1。  
  - 详细信息：0 表示安装 Current Branch 的未经许可的评估版，1 表示安装许可的版本。   

- **CurrentBranch**
  - 值：0 或 1。  
  - 详细信息：0 表示安装 Long-Term Servicing Branch，1 表示安装 Current Branch。  

例如，若要安装许可的 Current Branch.版本，请使用：

  **密钥名称：SABranchOptions**
   -    **SAActive = 1**
   -  **= 1**


> [!IMPORTANT]  
> **SABranchOptions** 只适用于从基线介质运行安装程序。 它不适用于从站点（之前使用 1606 版基线介质安装的站点）CD.Latest 文件夹运行安装程序。
>
> **SABranchOptions** 不适用于 System Center 2012 Configuration Manager 脚本化升级，始终出现在 Current Branch 中。

有关详细信息，请参阅[使用命令行安装 System Center Configuration Manager 站点](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites)。


## <a name="install-a-new-site"></a>安装新站点
使用 1606 基线介质安装任一分支的新站点时，请使用[安装 System Center Configuration Manager 站点](/sccm/core/servers/deploy/install/installing-sites)主题中的站点规划、准备和安装过程，并考虑以下安装注意事项：

- 在安装期间，必须选择想要安装的 Configuration Manager 分支，这样才能为软件保障协议指定详细信息。
- 同一层次结构中的所有网站必须运行同一分支。 不支持在不同的站点具有混合使用 LTSB 和 Current Branch 的层次结构。
-   新的脚本化安装。 有关详细信息，请参阅本文章前文中的“新的脚本化安装选项”。

## <a name="expand-a-stand-alone-primary-site"></a>扩展独立主站点
可以扩展运行 LTSB 的独立主站点。  此过程与安装 Current Branch 站点的过程并无二致，但需注意一点：

- 安装新管理中心站点时，必须使用用于安装 LTSB 站点的原始源介质中的安装程序。 不支持从此方案的 CD.Latest 文件夹运行安装程序。

有关扩展站点的详细信息，请参阅[使用安装向导来安装站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)中的“扩展独立主站点”。

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>从 System Center 2012 Configuration Manager 升级
若要从 System Center 2012 Configuration Manager 升级，请使用[升级到 System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) 主题中介绍的站点规划、准备和过程，但需要注意以下更改：

**升级到 Current Branch：**
- 在安装期间，必须选择 Current Branch，这样才能为软件保障协议指定详细信息。
-   新的脚本化安装。 有关详细信息，请参阅本文章前文中的“新的脚本化安装选项”。

**升级到 LTSB：**  
- 升级前清单中要遵循的附加步骤。
- 在安装期间，必须选择 LTSB，这样才能为软件保障协议指定详细信息。
- 只能升级可运行 System Center 2012 Configuration Manager Service Pack 2 或 System Center 2012 R2 Configuration Manager Service Pack 1 的站点。

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>1606 版基线介质的就地升级路径
可以使用 1606 版基线介质将以下版本升级到 System Center Configuration Manager 的许可版本：
- System Center 2012 Configuration Manager Service Pack 2。
- System Center 2012 R2 Co。nfiguration Manager Service Pack 1。

此介质还可用于将 Current Branch 的未经许可评估版升级到完全许可版本。

此介质不支持的升级：
- System Center 2012 Configuration Manager 的其他版本。
- Configuration Manager 2007 或早期版本。
- System Center Configuration Manager 的候选发布版安装。

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>关于 CD.Latest 文件夹和 LTSB
Configuration Manager 在站点服务器上的 CD.Latest 文件夹中创建介质，以下是使用该介质的限制。 这些限制适用于运行 LTSB 的站点：

CD.Latest 文件夹中的介质受以下内容支持：
- 站点恢复。
- 站点维护。
- 安装其他子级主站点。

CD.Latest 文件夹中的介质不受以下内容支持：  
- 安装管理中心站点作为站点扩展方案的一部分。

有关详细信息，请参阅 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)。

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>LTSB 的备份、恢复和站点维护
若要在运行 LTSB 的站点上进行备份、恢复或运行站点维护，请使用 [System Center Configuration Manager 的备份和恢复](/sccm/protect/understand/backup-and-recovery)中的指南和步骤。  

使用 LTSB 站点备份 CD.Latest 文件夹中的 Configuration Manager 安装程序。
