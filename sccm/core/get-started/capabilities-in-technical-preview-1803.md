---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1803 版中提供的新功能。
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 672257141c0672a76b89ee9d78184d2a4230280f
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898352"
---
# <a name="capabilities-in-technical-preview-1803-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1803 中的功能

适用范围：System Center Configuration Manager (Technical Preview)

本文介绍 Configuration Manager Technical Preview 1803 版中提供的功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 

安装此更新之前，请查看 [Technical Preview](/sccm/core/get-started/technical-preview) 一文。 该文章将帮助你熟悉使用 Technical Preview 的常规要求和限制，如何在版本之间进行更新以及如何提供相关的反馈。     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**以下是此版本可以试用的新功能。**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>请求分发点支持将云分发点作为源  
<!--1321554--> 许多客户在远程办公室或分支机构使用[请求分发点](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)，这些分发点通过 WAN 从源分发点下载内容。 如果远程办公室与 Internet 建立了更好的连接，或者为了减少 WAN 链路负载，现在可以在 Microsoft Azure 中使用[云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)作为源。 现在，当你在分发点属性的“请求分发点”选项卡上添加源时，站点中的所有云分发点都会列为可用的分发点。 两个站点系统角色的行为都保持不变。 

### <a name="prerequisites"></a>先决条件
- 请求分发点需要访问 Internet 才能与 Microsoft Azure 通信。
- 必须内容将分发到源云分发点。

> [!Note]  
> 此功能确实会对你的 Azure 数据存储和网络出口订阅收取费用。 有关详细信息，请参阅[使用基于云的分发的成本](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#BKMK_CloudDPCost)。



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>客户端对等缓存中的部分下载支持可降低 WAN 利用率
<!--1357346--> 客户端对等缓存源现可以将内容分成多个部分。 这些部分最大限度地减少了网络传输，从而降低了 WAN 利用率。 管理点提供更详细的内容部分跟踪。 它试图消除每个边界组多次下载相同内容的行为。 

### <a name="example-scenario"></a>示例方案
Contoso 有一个单独的主站点，该站点包含两个边界组：总部 (HQ) 和分支机构。 边界组之间有 30 分钟的回退关系。 该站点的管理点和分发点都位于 HQ 边界中。 分支机构所在地没有本地分发点。 分支机构的四个客户端中有两个配置为对等缓存源。 

![示例方案中所述网络配置的示意图](media/1357346-peer-cache-source-parts.png)

1. 将分支机构中的所有四个客户端作为内容部署的目标。 仅将内容分发到了分发点。
2. Client3 和 Client4 没有用于部署的本地源。 管理点指示客户端等待 30 分钟后再回退到远程边界组。
3. Client1 (PCS1) 是第一个向管理点刷新策略的对等缓存源。 由于此客户端已启用为对等缓存源，因此管理点指示它立即开始从分发点下载 A 部分。  
4. 当 Client2 (PCS2) 与管理点联系时，由于 A 部分已在下载，但尚未完成，因此管理点指示它立即开始从分发点下载 B 部分。
5. PCS1 下载完 A 部分，并立即通知管理点。 由于 B 部分已在下载，但尚未完成，因此管理点指示它开始从分发点下载 C 部分。
6. PCS2 下载完 B 部分，并立即通知管理点。 管理点指示它开始从分发点下载 D 部分。 
7. PCS1 下载完 C 部分，并立即通知管理点。 管理点告知它远程分发点没有更多可用部分。 管理点指示它从本地对等源 PCS2 下载 B 部分。
8. 此过程一直持续到这两个客户端对等缓存源拥有彼此的所有部分。 在指示对等缓存源从本地对等源下载部分之前，管理点会优先考虑远程分发点中的部分。 
9. Client3 是 30 分钟回退期到期后第一个刷新策略的客户端。 现在，它与管理点进行核对，后者告知它有新的本地源。 它从其中一个客户端对等缓存源下载全部内容，而不是通过 WAN 从分发点下载全部内容。 客户端优先考虑本地对等源。 

> [!Note]  
> 如果客户端对等缓存源的数量超出内容部分的数量，则管理点会指示其他对等缓存源像正常客户端一样等待回退。 


### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。

1. 按常规设置[边界组](/sccm/core/servers/deploy/configure/boundary-groups)和[对等缓存源](/sccm/core/plan-design/hierarchy/client-peer-cache)。
2. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”。 单击功能区中的“层次结构设置”。 
3. 在“常规”选项卡上，启用“配置客户端对等缓存源以将内容分成多个部分”选项。 
4. 创建必需的内容部署。  

   > [!Note]  
   > 此功能仅适用于客户端在后台下载内容的情况（例如进行必需的部署）。 按需下载（例如用户在软件中心安装可用部署时）的行为与往常一样。  

1. 若要了解它们如何处理多部分内容的下载，请检查客户端对等缓存源上的 **ContentTransferManager.log** 和管理点上的 **MP_Location.log**。  
 



## <a name="maintenance-windows-in-software-center"></a>软件中心的维护时段
<!--1358131--> 软件中心现在显示下一个计划性维护时段。 在“安装状态”选项卡上，将视图从“全部”切换为“即将进行”。 它显示时间范围和计划部署列表。 如果没有将来的维护时段，则该列表为空。 

![软件中心的“安装状态”选项卡上显示即将进行的部署的列表](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>软件中心用于网页的自定义选项卡
<!--1358132--> 现在可以在软件中心创建自定义选项卡来打开网页。 此功能可让你以一致、可靠的方式向最终用户展示内容。 以下列表包含几个示例：
- 联系 IT 部门：有关如何联系组织 IT 部门的信息
- IT 支持中心：IT 自助操作，如搜索知识库或开启支持票证。
- 最终用户文档：面向组织中的用户的文章，涉及各种 IT 主题，例如使用应用程序或升级到 Windows 10。


### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。

1. 在 Configuration Manager 控制台的“管理”工作区的“客户端设置”节点中，打开“默认客户端设置”策略。
2. 选择“软件中心”组。
3. 对于“软件中心设置”，单击“自定义”。
4. 切换到“选项卡”选项卡。
5. 启用“为软件中心指定自定义选项卡”选项。
    1. 在“选项卡名称”文本字段中输入名称。 该名称是软件中心向用户展示的名称。
    2. 在“内容 URL”文本字段中输入有效的 URL。 此 URL 是用户单击此选项卡时软件中心显示的内容。

> [!Tip]  
> 软件中心使用 Internet Explorer 组件来呈现网页。

## <a name="enable-third-party-software-update-support-on-clients"></a>对客户端启用第三方软件更新支持

现在可以为 Configuration Manager 客户端配置第三方软件更新。 当你为 SUP 组件属性“启用第三方软件更新”时，SUP 将下载 WSUS 用于第三方更新的签名证书。 <!--1357605-->

选择客户端设置中的“启用第三方软件更新”后，它会执行以下操作： 
- 在客户端上，它会设置“允许 Intranet Microsoft 更新服务位置的签名更新”策略 
- 将签名证书安装到客户端上受信任的发布者库。 

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。

1. 在 Configuration Manager 层次结构中最顶层的站点上，转到“管理”节点，依次展开“站点配置”和“站点”。
2. 右键单击最顶层的站点服务器，依次选择“配置站点组件”和“软件更新点”。
3. 单击“第三方更新”选项卡，选中“启用第三方软件更新”。
4. 打开“客户端设置”，转到“软件更新”的设置。
5. 确保“启用第三方软件更新”设置为“是”。

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>支持从监视视图中复制/粘贴资产详细信息
作为 [User Voice 反馈](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det)的结果，你现在可以在部署和分发状态监视视图的资产详细信息窗格中启用复制/粘贴功能。  <!--1357552-->

## <a name="scap-extensions"></a>SCAP 扩展
SCAP 扩展的预发行版本位于 Cd.latest 文件夹中的 SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi 下。 SCAP 扩展的此预发行版本可以安装在当前支持的任何 Configuration Manager Current Branch 和 LTSB 1606 版本上。 有关详细信息，请参阅[关于安全内容自动化协议 (SCAP) 扩展](/sccm/compliance/plan-design/scap/about-scap)。



## <a name="next-steps"></a>后续步骤
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。    
