---
title: 已弃用的功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 不再支持的功能。
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96a9c497f7b8dbcd831fd42de646e836fc91ef29
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496347"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Configuration Manager 中已删除和已弃用的功能

适用范围：System Center Configuration Manager (Current Branch)

本文列出了已弃用或已从 Configuration Manager 支持中删除的功能。 已弃用的功能将在未来的更新中删除。 未来的这些更改可能会影响 Configuration Manager 的使用。  

此信息会随未来的发布进行更改。 其中可能不会包含每个弃用的 Configuration Manager 功能。



## <a name="deprecated-features"></a>已弃用的功能  

|功能|首次宣布弃用|支持&nbsp;删除|  
|-----------|---|--------------|  
|共享 Azure 内容的实现已更改。 使用启用了内容的云管理网关。 将来无法创建传统的云分发点。|2019 年 2 月|2019 年 11 月 1 日后发布的首版|
|适用于云管理网关和云分发点的 Azure 经典服务部署。 有关详细信息，请参阅 [CMG 规划](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager)。|2018 年 11 月|在 2019 年 7 月 1 日之后发布的第一个版本| 
|适用于 Mac 和 Linux 的 System Center Endpoint Protection<br>有关详细信息，请参阅[“不再提供支持”博客文章](https://go.microsoft.com/fwlink/?linkid=870182)。|2018 年 10 月|2018 年 12 月 31 日|
|本地条件访问<br>有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。|2019 年 1 月 30 日|2019 年 9 月 1 日|
|混合移动设备管理 (MDM)<br>有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<br><br>自 1902 Intune 服务版本起，预计在 2019 年 2 月底，新客户便无法新建混合连接。<!--Intune feature 2683117-->|2018 年 8 月 14 日|2019 年 9 月 1 日|
|Configuration Manager 中的 Windows Hello 企业版设置<br>有关详细信息，请参阅 [Windows Hello 企业版设置](/sccm/protect/deploy-use/windows-hello-for-business-settings)。|2017 年 12 月|2019 年 11 月 1 日后发布的首版|
|应用程序目录网站点的 Silverlight 用户体验不再受支持。 用户应使用新的软件中心。 注意：应用目录网站点和 Web 服务点角色仍受支持。 在某些情况下，新的软件中心会与应用程序目录网站点进行通信。 有关详细信息，请参阅[配置软件中心](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)。<!--1358309-->|2017 年 8 月 11日| 版本 1806|
|以前版本的软件中心。<br><br>有关新软件中心的详细信息，请参阅[规划和配置应用程序管理](/sccm/apps/plan-design/plan-for-and-configure-application-management##bkmk_userex)。|2016 年 12 月 13 日|版本 1802|
|利用 Configuration Manager 管理虚拟硬盘 (VHD)。 <br><br>此次弃用包括删除使用任务序列创建新 VHD 或管理 VHD 的选项，以及删除 Configuration Manager 控制台的虚拟硬盘节点。 <br><br>不会删除现有 VHD，但无法从 Configuration Manager 控制台中对其进行访问。  |2017 年 1 月 6 日 |版本 1710|
|任务序列： <br /> - 将磁盘转换为动态磁盘 <br /> - 安装部署工具 |2016 年 11 月 18 日|版本 1710|
|System Center Configuration Manager 升级评估工具。 <br><br>升级评估工具依赖于 System Center Configuration Manager 和应用程序兼容性工具包 (ACT) 6.x。 ACT 的最终版本随附在 Windows 10 v1511 ADK 中。 由于不再对 ACT 进行任何更新，因此会停止对升级评估工具的支持。 <br><br>升级评估工具将由[升级准备](/sccm/core/clients/manage/upgrade/upgrade-analytics)功能取代。 弃用通知已于 2016 年 9 月 12 日添加到 [UAT 的下载页面](https://www.microsoft.com/download/details.aspx?id=37145)。 | 2016 年 9 月 12 日  | 2017 年 7 月 11 日 |
|带有网络负载均衡 (NLB) 群集的软件更新点 | 2016 年 2 月 27 日 | 版本 1702 | 
|任务序列： <br /> - OSDPreserveDriveLetter  <br /><br /> 现在，在操作系统部署期间，默认情况下，Windows 安装程序会确定要使用的最佳驱动器号（通常为 C:）。 如果想要指定使用另一个驱动器，可以在“应用操作系统”任务序列步骤中更改位置。 转到“选择要应用此操作系统的位置”设置。 选择“特定逻辑驱动器号”并选择想要使用的驱动器。 |2016 年 6 月 20 日 |版本 1606 |
|网络访问保护 (NAP)- 在 System Center 2012 Configuration Manager 中找到|2015 年 10 月|版本 1511|  
|带外管理- 在 System Center 2012 Configuration Manager 中找到|2015 年 10 月 16 日|版本 1511|



## <a name="features-removed-in-version-1511"></a>版本 1511 中删除的功能
以下部分包含版本 1511 中删除的功能的其他详细信息：

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
 - [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)
 - [对 Configuration Manager Current Branch 版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)。
