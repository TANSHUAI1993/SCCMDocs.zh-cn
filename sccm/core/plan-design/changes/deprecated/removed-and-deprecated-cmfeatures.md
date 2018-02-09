---
title: "Configuration Manager 功能中已弃用的项"
titleSuffix: Configuration Manager
description: "了解 System Center Configuration Manager 不再支持的功能。"
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: d49e0f839106af652f7b49227b6c4f8c957347d9
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>System Center Configuration Manager 的已删除和已弃用的功能

*适用范围：System Center Configuration Manager (Current Branch)*

本文介绍 System Center Configuration Manager 的支持中删除的功能或者在未来更新中删除（弃用）的功能。 本文预告了可能会影响 Configuration Manager 的使用的未来变更。  

此信息会随着未来版本变动，并且可能不会包括每一个弃用的 Configuration Manager 功能。

## <a name="deprecated-features"></a>已弃用的功能  

|**功能**|**首次宣布弃用**|**删除的支持**|  
|-|-|-|  
|随着版本 1511 软件中心新体验的提供，之前仅在应用程序目录（用户可用应用程序）中显示的应用程序，现在显示在软件中心内。 </br></br>由于软件中心现在提供应用程序目录这一主要功能，因此在接下来的几个月中将不再提供基于 Web 的应用程序目录体验。|2017 年 8 月 11日| 对应用程序目录网站用户体验的支持终于 2018 年 6 月 1 日后发布的首个更新|
|软件中心具有富有现代感的全新外观。 在未来几个月，以前版本的软件中心将不再可用。<br><br>你可以通过启用客户端设置“计算机代理” > “使用新的软件中心”来使用新的软件中心。<br><br>有关软件中心的详细信息，请参阅[规划和配置 System Center Configuration Manager 中的应用程序管理](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management)。|2016 年 12 月 13 日|以前版本的软件中心支持在 2018 年 1 月 1 日后发布的第一个更新后结束。|
|利用 Configuration Manager 管理虚拟硬盘 (VHD)。 </br></br>这包括去除使用任务序列创建新 VHD 或管理 VHD 的选项，以及去除 Configuration Manager 控制台的虚拟硬盘节点。 </br></br>去除这种支持后，虽然现有 VHD 将不被删除，但再也无法从 Configuration Manager 控制台内访问。  |2017 年 1 月 6 日 |版本 1710|
|任务序列： <br /> - 将磁盘转换为动态磁盘 <br /> - 安装部署工具 |2016 年 11 月 18 日|版本 1710|
|System Center Configuration Manager 升级评估工具。 </br></br>升级评估工具依赖于 System Center Configuration Manager 和应用程序兼容性工具包 (ACT) 6.x。 ACT 的最终版本随附在 Windows 10 v1511 ADK 中。 由于不再对 ACT 进行任何更新，因此将停止对升级评估工具的支持。 </br></br>升级评估工具将由[升级准备](/sccm/core/clients/manage/upgrade/upgrade-analytics)功能取代。 弃用通知已于 2016 年 9 月 12 日添加到 [UAT 的下载页面](https://www.microsoft.com/download/details.aspx?id=37145)。 | 2016 年 9 月 12 日  | 2017 年 7 月 11 日 |
|任务序列： <br /> - OSDPreserveDriveLetter  <br /><br /> 现在，在操作系统部署期间，默认情况下，Windows 安装程序会确定要使用的最佳驱动器号（通常为 C:）。 如果想要指定使用另一个驱动器，可以在“应用操作系统”任务序列步骤中更改位置。 转到“选择要应用此操作系统的位置”设置。 选择“特定逻辑驱动器号”并选择想要使用的驱动器。 |2016 年 6 月 20 日 |版本 1606 |
|网络访问保护 (NAP)- 在 System Center 2012 Configuration Manager 中找到|2015 年 10 月|版本 1511|  
|带外管理- 在 System Center 2012 Configuration Manager 中找到|2015 年 10 月 16 日|版本 1511|



<br></br>
1511 版 System Center Configuration Manager 发布中删除的功能的其他信息如下：

###  <a name="bkmk_amt"></a>带外管理  
 通过 Configuration Manager，已删除 Configuration Manager 控制台中基于 AMT 的计算机的本机支持。  

-   使用[适用于 Microsoft System Center Configuration Manager 的 Intel SCS 外接程序](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)时，基于 AMT 的计算机保持完全托管。 使用外接程序可以在 Configuration Manager 能够合并这些更改之前使用用于管理 AMT 的最新功能，同时删除引入的限制。  

-   System Center 2012 Configuration Manager 中的带外管理不受此更改的影响。  

###  <a name="bkmk_nap"></a>网络访问保护  
 System Center Configuration Manager 已不再支持网络访问保护。 该功能已在 Windows Server 2012 R2 中弃用并从 Windows 10 中删除。  

 有关网络访问保护备选方案，请参阅 *网络策略和访问服务概述* 的 [已弃用功能](https://technet.microsoft.com/library/hh831683.aspx)部分。

## <a name="more-information"></a>更多信息
有关详情，请参阅：
 - [已删除和已弃用的项](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)网站。
 - [对 Configuration Manager Current Branch 版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)。
