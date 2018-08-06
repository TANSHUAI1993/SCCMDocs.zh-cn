---
title: Technical Preview 1806.2
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1806.2 版中提供的新功能。
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5183b30d9184f7119d1423b5773da2b692026ab7
ms.sourcegitcommit: 64b343906afdd442189559119eea8e933642cbf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342808"
---
# <a name="capabilities-in-technical-preview-18062-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1806.2 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了 Configuration Manager Technical Preview 1806.2 版中提供的功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 

安装此更新之前，请查看 [Technical Preview](/sccm/core/get-started/technical-preview) 一文。 该文章将帮助你熟悉使用 Technical Preview 的常规要求和限制，如何在版本之间进行更新以及如何提供相关的反馈。     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->

## <a name="known-issues-in-this-technical-preview"></a>此 Technical Preview 中的已知问题

### <a name="ki_sqlncli"></a>客户端不会自动更新
<!--518760-->更新到版本 1806.2 时，站点也会更新 SQL Native Client，这可能导致站点服务器等待重启。 此延迟会导致某些文件不更新，从而影响客户端自动升级。

#### <a name="workarounds"></a>工作区
通过在将 Configuration Manager 更新到版本 1806.2 之前手动升级 SQL Native Client 避免此问题。 有关详细信息，请参阅 [SQL Server 2012 Native Client 最新服务更新](https://www.microsoft.com/download/details.aspx?id=50402)。

如果你已更新站点，则客户端将不自动升级和推送。 你需要更新客户端以完全测试最新的功能。 使用以下过程手动更新 Technical Preview 客户端：  

1. 在站点服务器上的 Configuration Manager 安装目录的“CMUClient”文件夹中查找客户端源文件。 例如 `C:\Program Files\Configuration Manager\CMUClient`  

2. 将整个 CMUClient 文件夹复制到客户端设备。 例如 `C:\Temp\CMUClient`  

    此位置可以是可从客户端访问的网络共享。  

3. 在提升了权限的命令提示符下运行以下命令行：`C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

如果要在 Technical Preview 1806.2 版站点中安装新的客户端，请使用同一过程。 

> [!Important]  
> 在此场景中，请勿使用 `/MP` 命令行参数。 此参数优先于 `/source`，并会导致 ccmsetup 从管理点或分发点下载客户端内容。
> 
> 升级现有客户端时，可以使用命令行属性（如 SMSSITECODE 或 CCMLOGLEVEL），但不是必须使用。 


### <a name="ki_version"></a>版本 1806.2 在“关于 Configuration Manager”中显示版本 1806
<!--518148-->在升级到 Technical Preview 1806.2 版后，如果从控制台左上角打开“关于 Configuration Manager”窗口，它将仍显示“版本 1806”。 

#### <a name="workaround"></a>解决方法
使用“站点版本”属性确定 1806 和 1806.2 之间的区别：

| 站点版本  | 版本
|---------|---------|
| 5.0.8672.1000 | 1806 |
| 5.0.8685.1000 | 1806.2 |
 


</br>

**以下是此版本可以试用的新功能。**  


## <a name="bkmk_pod"></a>分阶段部署改进

此版本包括对[分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)的以下改进：
- [分阶段部署状态](#bkmk_pod-monitor)
- [应用程序的分阶段部署](#bkmk_pod-app)
- [分阶段部署期间逐渐推出](#bkmk_pod-throttle)


### <a name="bkmk_pod-monitor"></a>分阶段部署状态
<!--1358577-->现在分阶段部署具有本地监视体验。 从“监视”工作区中的“部署”节点，选择分阶段部署，然后单击功能区中的“分阶段部署状态”。

![显示两个阶段的状态的分阶段部署状态仪表板](media/1358577-phased-deployment-status.png)

此仪表板显示部署的每个阶段的以下信息：  

- **总设备数**：此阶段针对多少台设备。  

- **状态**：此阶段的当前状态。 每个阶段可以为以下状态之一：  

    - **已创建部署**：分阶段部署为此阶段创建了软件到集合的部署。 使用此软件主动针对客户端。  

    - **等待中**：之前的阶段尚未达到让部署继续到此阶段的成功标准。  

    - **已挂起**：管理员已挂起部署。  

- **进度**：客户端的用颜色标明的部署状态。 例如：成功、进行中、错误、不符合要求以及未知。 


#### <a name="known-issue"></a>已知问题
分阶段部署状态仪表板可能会为同一阶段显示多行。<!--518510-->


### <a name="bkmk_pod-app"></a>应用程序的分阶段部署
<!--1358147-->为应用程序创建分阶段部署。 通过分阶段部署，可以根据可自定义条件和组进行协调安排，有序推出软件。

在 Configuration Manager 控制台中，转到“软件库”，展开“应用程序管理”，然后选择“应用程序”。 选择一个应用程序，然后单击功能区中的“创建分阶段部署”。 

应用程序分阶段部署的行为与任务序列的行为相同。 有关详细信息，请参阅[为任务序列创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)。

#### <a name="prerequisite"></a>先决条件
创建分阶段部署之前，将应用程序的内容分发到分发点。<!--518293-->

#### <a name="known-issue"></a>已知问题
你无法手动为应用程序创建阶段。 向导会自动为应用程序部署创建两个阶段。


### <a name="bkmk_pod-throttle"></a>分阶段部署期间逐渐推出
<!--1358578-->在分阶段部署期间，每个阶段的推出可以逐步进行。 此行为有助于缓解部署问题的风险，降低网络上因向客户端分发内容而导致的负载。 根据每个阶段的配置，此站点可以逐步使软件可用。 相对于使软件可用的时间，一个阶段中的每个客户端都有一个截止时间。 对于一个阶段中的所有客户端，可用时间和截止时间之间的时间窗都是相同的。 

创建分阶段部署和手动配置阶段时，在“添加阶段向导”的“阶段设置”页面上，或在“创建分阶段部署”向导的“设置”页面上，配置“在这段时间(以天计)逐步使软件可用”选项。 此设置的默认值为“0”，因此默认情况下，部署不受限制。

> [!Note]  
> 此选项目前仅适用于任务序列的分阶段部署。  



## <a name="bkmk_msix"></a>支持新的 Windows 应用包格式
<!--1357427-->Configuration Manager 现在支持部署新的 Windows 10 应用包 (.msix) 和应用程序包 (.msixbundle) 格式。 最新的 [Windows Insider Preview](https://insider.windows.com/) 内部版本当前支持这些格式。

有关 MSIX 的概述，请参阅 [MSIX 详解](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/)。

有关如何创建新的 MSIX 应用，请参阅 [Insider 内部版本 17682 中引入的 MSIX 支持](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376)。

### <a name="prerequisites"></a>先决条件
- 至少运行 Windows Insider Preview 内部版本 17682 的 Windows 10 客户端
- Windows 应用包（采用 MSIX 格式）

### <a name="try-it-out"></a>试试看！
尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，[创建一个应用程序](/sccm/apps/deploy-use/create-applications)。 
2. 将应用程序安装文件类型选择为 Windows 应用包（\*.appx、\*.appxbundle、\*.msix、\*.msixbundle）。
3. [将应用程序部署](/sccm/apps/deploy-use/deploy-applications)到运行最新 Windows Insider Preview 内部版本的客户端。



## <a name="bkmk_client-push"></a>客户端推送安全性改进
<!--1358204-->使用[客户端推送](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation)方法安装 Configuration Manager 客户端时，站点服务器创建到客户端的远程连接以开始安装。 从此版本开始，站点可以通过不允许在建立连接之前回退到 NTLM 来要求 Kerberos 相互身份验证。 此增强有助于保护服务器与客户端之间的通信。 

根据你的安全策略，你的环境可能偏好或要求 Kerberos，而不是较旧的 NTLM 身份验证。 有关这些身份验证协议的安全注意事项的详细信息，请参阅[用于限制 NTLM 的 Windows 安全策略设置](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations)。


### <a name="prerequisite"></a>先决条件

要使用此功能，客户端必须位于信任的 Active Directory 林中。 Windows 中的 Kerberos 依赖 Active Directory 进行相互身份验证。 


### <a name="try-it-out"></a>试试看！

尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

升级站点时，仍然存在现有行为。 打开客户端推送安装属性后，该站点会自动启用 Kerberos 检查。 如有必要，可以允许连接回退以使用较不安全的 NTLM 连接，但通常不建议这样操作。 

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”。 选择目标站点。 在功能区中，单击“客户端安装设置”，然后选择“客户端推送安装”。  

2. 站点现已为客户端推送启用 Kerberos 检查。 单击“确定”关闭窗口。  

3. 如果对你的环境来说是必要的，请在“客户端推送安装属性”窗口中的“常规”选项卡上，查看“允许连接回退到 NTLM”选项。 默认情况下禁用此选项。 



## <a name="bkmk_insights"></a>针对主动维护的管理见解
<!--1352184,et al-->在此版本中，还有其他管理见解，用于突出显示潜在的配置问题。 在新的“主动维护”组中查看以下规则：  

- **未使用的配置项**：这些配置项不属于配置基线，并且存在已超过 30 天。  

- **未使用的启动映像**：未引用这些启动映像以用于 PXE 启动或任务序列。  

- **未被分配站点系统的边界组**：这些边界组未被分配站点系统，只能用于站点分配。  

- **不包含任何成员的边界组**：如果这些边界组没有任何成员，则不适用于站点分配或内容查找。  

- **未向客户端提供内容的分发点**：这些分发点在过去 30 天内未向客户端提供内容。 此数据基于来自其客户端的下载历史记录报告。  

- **找到的过期更新**：这些过期更新不适用于部署。   



## <a name="bkmk_comgmt"></a>转移共同管理的设备的移动应用工作负荷
<!--1357892-->使用 Microsoft Intune 管理移动应用，同时继续使用 Configuration Manager 部署 Windows 桌面应用程序。 要转移现代应用工作负荷，请转到共同管理属性页。 将滚动条从 Configuration Manager 移动到“试点”或“全部”。 

转移此工作负荷之后，任何从 Intune 部署的可用应用在公司门户中也变得可用。 从 Configuration Manager 部署的应用在软件中心可用。 

有关详细信息，请参阅下列文章：  

- [适用于 Windows 10 设备的共同管理](/sccm/core/clients/manage/co-management-overview)  

- [什么是 Microsoft Intune 应用管理？](https://docs.microsoft.com/intune/app-management)  



## <a name="bkmk_bgoptions"></a>对等下载适用的边界组选项
<!--1356193-->边界组现在包含其他设置，可以让你更好地控制环境中的内容分发。 此版本添加了以下选项：  

- **在此边界组中允许对等下载**：默认情况下启用此设置。 管理点向客户端提供包含对等源的内容位置的列表。 <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    有两个应考虑禁用此选项的常见场景：  

    - 如果你拥有的边界组包括来自地理上分散的位置（例如 VPN）的边界， 两个客户端可能位于同一边界组中，因为它们都通过 VPN 连接，但位于不适合对等共享内容的极其不同的位置。  

    - 如果将单个较大的而且不引用任何分发点的边界组用于站点分配。  

- **在对等下载期间，仅使用同一子网内的对等项**：此设置取决于上面那个选项。 如果启用此选项，管理点将仅包含与客户端在同一子网中的内容位置列表对等源。

    启用此选项的常见场景：

    - 内容分发的边界组设计包含一个与其他较小边界组重叠的大型边界组。 使用此新设置，管理点向客户端提供的内容源列表仅包含来自同一子网的对等源。

    - 你拥有的单个大型边界组适用于所有远程办公室位置。 启用此选项，客户端仅在远程办公室位置的子网内共享内容，而不是冒险在位置之间共享内容。


### <a name="known-issue"></a>已知问题
如果对等源客户端具有多个 IP 地址（IPv4 和/或 IPv6），则对等缓存不起作用。 如果对等源具有多个 IP 地址，则新选项“对等下载期间，仅使用同一子网内的对等项”不起作用。<!--518661-->   



## <a name="bkmk_3pupdate"></a>自定义目录支持第三方软件更新
<!--1358714-->根据 [UserVoice 反馈](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)，此版本在以前版本的基础上进一步更替对第三方软件更新的支持。 [Technical Preview 版本 1806](/sccm/core/get-started/capabilities-in-technical-preview-1806#bkmk-3pupdate) 提供对合作伙伴目录的支持，这些目录是软件供应商提供的注册目录。 你提供的未向 Microsoft 注册的目录称为“自定义目录”。 在 Configuration Manager 控制台中添加自定义目录。  


### <a name="prerequisites"></a>先决条件 

- 安装[第三方软件更新](/sccm/core/get-started/capabilities-in-technical-preview-1806#bkmk-3pupdate)。 完成阶段 1：启用和设置功能。   

- 包含数字签名的软件更新的数字签名的自定义目录。  

- 管理员要求具有以下权限：  

    - 站点：创建、修改  


### <a name="try-it-out"></a>试试看！

尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“软件更新”，然后选择“第三方软件更新目录”节点。 单击功能区中的“添加自定义目录”。  

2. 在“常规”页面上，指定以下详细信息：  

    - **下载 URL**：自定义目录的有效的 HTTPS 地址。  

    - **发行商**：发布目录的组织的名称。  

    - **名称**：要在 Configuration Manager 控制台中显示的目录的名称。  

    - **描述**：目录描述。  

    - **支持 URL**（可选）：用于获取目录相关帮助的网站的有效 HTTPS 地址。  

    - **支持联系人**（可选）：用于获取目录相关帮助的联系人信息。  

3. 完成向导。 向导在取消订阅的状态下添加新目录。  

4. 使用现有的“订阅目录”操作订阅自定义目录。 有关详细信息，请参阅[阶段 2：订阅第三方目录并同步更新](/sccm/core/get-started/capabilities-in-technical-preview-1806#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates)。  

> [!Note]  
> 无法添加下载 URL 相同的目录，并且无法编辑目录属性。 如果为自定义目录指定了错误的属性，请先删除此目录，再重新添加。  


#### <a name="unsubscribe-from-a-catalog"></a>取消订阅目录
要取消订阅目录，请在列表中选择所需的目录，然后单击功能区中的“取消订阅目录”。 如果你取消订阅目录，将发生以下操作和行为： 
- 网站停止同步新的更新 
- 站点阻止目录签名和更新内容的关联证书。 
- 不会删除现有更新，但可能无法发布或部署它们。

#### <a name="delete-a-custom-catalog"></a>删除自定义目录
从控制台的同一节点中删除自定义目录。 选择处于“取消订阅”状态的自定义目录，然后单击“删除自定义目录”。 如果你已订阅目录，请先取消订阅，再将其删除。 无法删除合作伙伴目录。 删除自定义目录会将其从目录列表中删除。 此操作不会影响任何已发布到软件更新点的软件更新。


### <a name="known-issue"></a>已知问题
自定义目录的删除操作呈灰显状态，因此不能从控制台中删除自定义目录。 要解决此问题，请使用站点服务器上的 wbemtest 工具。 使用名称或下载 URL 查询要删除的实例，例如：`select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`。 在查询结果窗口中，选择对象，然后单击“删除”。<!--518676-->  



## <a name="bkmk_cloud"></a>云管理功能改进

此版本包括以下改进：  

- 以下功能现在均支持使用 Azure 美国政府云：<!--511980-->  

    - 通过 [Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)载入云管理站点  

    - [使用 Azure 资源管理器部署云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager)  

    - [使用 Azure 资源管理器部署云分发点](/sccm/core/get-started/capabilities-in-technical-preview-1805#cloud-distribution-point-support-for-azure-resource-manager)  

- 客户使用 Windows AutoPilot 预配连接到本地网络上的加入 Azure Active Directory 的设备上的 Windows 10。 要在这些设备上安装或升级 Configuration Manager 客户端，现在不再需要被配置为“允许客户端匿名连接”的云分发点或本地分发点。 相反，启用站点选项“将 Configuration Manager 生成的证书用于 HTTP 站点系统”，这允许加入云域的客户端与启用本地 HTTP 的分发点进行通信。 有关详细信息，请参阅[已改进安全客户端通信](https://docs.microsoft.com/en-us/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications)。<!--515854-->  



## <a name="bkmk_report"></a>新的软件更新符合性报告
<!--1357775-->查看软件更新符合性报告传统上包含最近未联系站点的客户端中的数据。 你可以通过新的报告按“正常运行”客户端筛选特定软件更新组的符合性结果。 此报告显示你环境中的活动客户端的更真实的符合性状态。 
 
要查看报告，请转到“监视”工作区，依次展开“报告”“报告”“软件更新 - 符合性”，然后选择“符合性 9 - 整体运行状况和符合性”。 指定“更新组”、“集合名称”以及“客户端运行状况”状态。

报告包括以下几个部分：
- **正常客户端与总客户端**：此条形图比较了在指定时间段内与站点通信的“正常”客户端的数量和指定集合中的客户端总数。
- **符合性概述**：此饼图显示了指定集合中活动客户端上的特定软件更新组的总体符合性状态。
- **前 5 个不符合（按文章 ID）**：此条形图显示了特定组中在指定集合中的活动客户端上不符合的前五个软件更新。
- 报告底部是具有更多详细信息的表，其中列出了指定组中的软件更新。



## <a name="next-steps"></a>后续步骤
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。    
