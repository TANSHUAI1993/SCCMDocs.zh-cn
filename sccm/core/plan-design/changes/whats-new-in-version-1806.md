---
title: 1806 版中的新增功能
titleSuffix: Configuration Manager
description: 获取有关 Configuration Manager Current Branch 1806 版中引入的更改和新功能的详细信息。
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ad5034ca7475009f2dcd4b50df96d22b2f9428fa
ms.sourcegitcommit: 2d38de4846ea47a03cc884cbd3df27db48f64a6a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70110118"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Configuration Manager Current Branch 1806 版中的新增功能

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager Current Branch 的 1806 更新作为控制台中更新提供。 将此更新应用于运行 1706、1710 或 1802 版的站点。 <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

始终查看安装此更新的最新清单。 有关详细信息，请参阅 [1806 的安装更新清单](/sccm/core/servers/manage/checklist-for-installing-update-1806)。 更新站点后，还可以查看[更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1806#post-update-checklist)。

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

以下各节提供有关 Configuration Manager Current Branch 1806 版中的更改和新功能的详细信息。  



## <a name="deprecated-features-and-operating-systems"></a>弃用的功能和操作系统

在[已删除和已启用的项](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)中实施支持更改之前，先了解这些更改。

截至 2018 年 8 月 14 日，混合移动设备管理功能已弃用。 有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>站点基础结构

### <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager 总是提供设备数据的大型集中式存储，客户可将其用于报告目的。 该站点通常每周都会收集这些数据。 CMPivot 是一种新的控制台中实用工具，现提供对环境中设备实时状态的访问。 它立即对目标集合中的所有连接设备运行查询，并返回结果。 然后你可以在工具中对此数据进行筛选和分组。 通过提供来自联机客户端的实时数据，可以更快地回答业务问题、解决问题并对安全事件作出响应。 

有关详细信息，请参阅 [CMPivot](/sccm/core/servers/manage/cmpivot)。  


### <a name="site-server-high-availability"></a>站点服务器高可用性
<!--1128774-->
独立主站点服务器角色的高可用性是一项基于 Configuration Manager 的解决方案，用于安装被动模式下的其他站点服务器。 被动模式下的站点服务器是对主动模式下的现有站点服务器的补充。 在需要时可立即使用被动模式下的站点服务器。 

有关详细信息，请参阅下列文章： 
- [站点服务器高可用性](/sccm/core/servers/deploy/configure/site-server-high-availability) 
- [流程图 - 设置被动模式下的站点服务器](/sccm/core/servers/deploy/configure/passive-site-server-flowchart)
- [流程图 - 升级站点服务器（已规划）](/sccm/core/servers/deploy/configure/promote-site-server-flowchart)
- [流程图 - 升级站点服务器（未规划）](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart)


### <a name="improvements-to-management-insights"></a>管理见解的改进
此版本包括对管理见解的以下改进：  

- 某些管理见解现在可以选择执行一个操作。 此操作要么转到控制台中的关联节点，要么显示经过筛选的基于查询的视图。<!--1357930-->  

- 新的主动维护组已推出，其中包含六条新规则，有助于突出显示潜在的配置问题，以通过定期维护避免这些问题。<!--1352184-->  

有关详细信息，请参阅[管理见解](/sccm/core/servers/manage/management-insights)。


### <a name="configuration-manager-tools"></a>Configuration Manager 工具
<!--1357145-->
服务器现在随附 Configuration Manager 服务器和客户端工具。 可在站点服务器的 `CD.Latest\SMSSETUP\Tools` 文件夹中找到它们。 无需进行其他安装。 

有关详细信息，请参阅 [Configuration Manager 工具](/sccm/core/support/tools)。


### <a name="exclude-active-directory-containers-from-discovery"></a>从发现中排除 Active Directory 容器
<!--1358143-->
若要减少发现的对象数，请从 Active Directory 系统发现中排除特定容器。 

有关详细信息，请参阅[配置 Active Directory 系统发现](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adsd)。



## <a name="content-management"></a>内容管理

### <a name="configure-a-remote-content-library-for-the-site-server"></a>配置用于站点服务器的远程内容库
<!--1357525-->
若要配置站点服务器高可用性，或若要释放管理中心站点或主站点服务器上的硬盘空间，请将内容库重定位到另一个存储位置。 将内容库移至站点服务器上的另一个驱动器、单独服务器或者存储区域网络 (SAN) 中的容错磁盘。 

有关详细信息，请参阅下列文章： 
- [内容库](/sccm/core/plan-design/hierarchy/the-content-library)
- [流程图 - 管理内容库](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>对 Azure 资源管理器的云分发点支持
<!--1322209-->
在你创建云分发点时，向导现在提供用于创建“Azure 资源管理器部署”  的选项。 Azure 资源管理器是一个现代平台，用于以单个实体（称为资源组）的方式来管理所有解决方案资源。 如果在 Azure 资源管理器中部署云分发点，站点将使用 Azure Active Directory 进行身份验证并创建必要的云资源。 此现代化部署不需要经典 Azure 管理证书。 

云分发点的功能文档也进行了修订和补充。 有关详细信息，请参阅下列文章：
- [使用云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)   
- [安装云分发点](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>请求分发点支持将云分发点作为源  
<!--1321554-->
许多客户在远程或分支机构使用拉取分发点，这些分发点跨 WAN 从源分发点下载内容。 如果远程办公室与 Internet 建立了更好的连接，或者为了减少 WAN 链路负载，现在可以在 Microsoft Azure 中使用云分发点作为源。 现在，当你在分发点属性的“请求分发点”  选项卡上添加源时，站点中的所有云分发点都会列为可用的分发点。 两个站点系统角色的行为都保持不变。 

有关详细信息，请参阅[使用请求分发点](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)。


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>启用分发点以使用网络拥塞控制
<!--1358112-->
Windows 低额外延迟后台传输 (LEDBAT) 是 Windows Server 的一项功能，可帮助管理后台网络传输。 对于在受支持版本的 Windows Server 上运行的分发点，请启用一个选项以帮助调整网络流量。 客户端仅在允许的情况下使用网络带宽。 

有关详细信息，请参阅 [Windows LEDBAT](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#windows-ledbat)。


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>客户端对等缓存中的部分下载支持可降低 WAN 利用率
<!--1357346-->
客户端对等缓存源现在可以将内容分成多个部分。 这些部分最大限度地减少了网络传输，从而降低了 WAN 利用率。 管理点提供更详细的内容部分跟踪。 它试图消除每个边界组多次下载相同内容的行为。 

有关详情，请参阅[部分下载支持](/sccm/core/plan-design/hierarchy/client-peer-cache#bkmk_parts)。 


### <a name="boundary-group-options-for-peer-downloads"></a>对等下载适用的边界组选项
<!--1356193-->
边界组现在包含附加设置，可让你更好地控制环境中的内容分发。 此版本添加了以下选项：  

- **允许在此边界组中进行对等下载**：管理点向客户端提供包含对等源的内容位置的列表。 此设置还会影响交付优化组 ID 的使用。  

- **对等下载期间，只能使用同一子网内的对等设备**：管理点仅包含与客户端位于同一子网中的内容位置列表对等源。  

有关详细信息，请参阅[对等下载适用的边界组选项](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions)。


### <a name="improvement-to-peer-cache-source-location-status"></a>改进对等缓存源位置状态
<!--SCCMDocs issue 850-->
Configuration Manager 能更高效地确定对等缓存源是否已漫游到其他位置。 此行为可确保管理点将其作为内容源提供给新位置的客户端，而不是旧位置的客户端。 如果将对等缓存功能与漫游的对等缓存源一起使用，则在将站点更新到版本 1806 之后，还会将所有对等缓存源更新为最新的客户端版本。 在至少将这些对等缓存源更新到版本 1806 后，管理点才会将它们包含在内容位置列表中。

有关详细信息，请参阅[对等缓存的要求](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements)。



<!-- ## Migration  -->



## <a name="client-management"></a>客户端管理

### <a name="improvement-to-client-push-security"></a>客户端推送安全性改进
<!--1358204-->
当你使用客户端推送方法来安装 Configuration Manager 客户端时，站点现在要求进行 Kerberos 相互身份验证。 此增强有助于保护服务器与客户端之间的通信。 

有关详细信息，请参阅[如何使用客户端请求安装客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)。


### <a name="bkmk_ehttp"></a> 增强的 HTTP 站点系统
<!--1356889,1358228-->
建议对于所有 Configuration Manager 通信路径使用 HTTPS 通信，但由于管理 PKI 证书的开销，对一些客户来说可能是一个挑战。

此版本包括对客户端与站点系统之间的通信方式的改进。 在站点属性上，选择“客户端计算机通信”选项卡中的“HTTPS 或 HTTP”选项，然后启用新选项以“将 Configuration Manager 生成的证书用于 HTTP 站点系统”    。 此功能是[预发布功能](/sccm/core/servers/manage/pre-release-features)。

有关详细信息，请参阅[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)。


### <a name="azure-ad-device-identity"></a>Azure AD 设备标识 
<!--1358460-->
如果[已加入 Azure AD 的设备](/azure/active-directory/devices/concept-azure-ad-join)或[混合 Azure AD 设备](/azure/active-directory/devices/concept-azure-ad-join-hybrid)没有 Azure AD 用户登录，设备可以与其分配的站点进行安全通信。 基于云的设备标识现只需使用 CMG 和管理点进行身份验证。  

有关详细信息，请参阅[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)。


### <a name="cmtrace-installed-with-client"></a>与客户端一起安装的 CMTrace
<!--1357971-->
CMTrace 日志查看工具现自动与 Configuration Manager 客户端一起安装。 它被添加到客户端安装目录，默认情况下为 `%WinDir%\ccm\cmtrace.exe`。 

有关详细信息，请参阅 [CMTrace](/sccm/core/support/cmtrace)。


### <a name="cloud-management-dashboard"></a>云管理仪表板
<!--1358461-->
新的云管理仪表板提供了云管理网关 (CMG) 使用情况的集中式视图。 通过 Azure AD 载入网站时，它还显示有关云用户和设备的数据。   

此功能还包括用于实时验证的 CMG 连接分析器  ，为疑难解答提供帮助。 控制台中的实用工具检查该服务的当前状态，以及通过 CMG 连接点通往任何允许 CMG 流量的管理点的通信通道。 

有关详细信息，请参阅 [Monitor CMG](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway) 文章的以下部分：  
- [云管理仪表板](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#cloud-management-dashboard)  
- [连接分析器](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#connection-analyzer)  


### <a name="improvements-to-cloud-management-gateway"></a>云管理网关的改进

1806 版包含对云管理网关 (CMG) 的以下改进：

#### <a name="simplified-client-bootstrap-command-line"></a>简化了客户端启动命令行
<!--1358215-->
当你通过 CMG 在 Internet 上安装 Configuration Manager 客户端时，命令行现在需要的属性更少。 在准备共同管理时，此次改进减少了 Microsoft Intune 中使用的命令行的大小。 

有关详细信息，请参阅[如何准备基于 Internet 的设备以进行共同管理](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client)。

#### <a name="download-content-from-a-cmg"></a>从 CMG 下载内容
<!--1358651-->
以前，必须将云分发点和 CMG 作为单独的角色进行部署。 CMG 现在还可以向客户提供内容。 此功能减少了所需的证书和 Azure VM 的成本。 

有关详细信息，请参阅[修改 CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg)。

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Azure AD 不需要受信任的根证书
<!--503899-->
当创建 CMG 时，不再需要在设置页上提供[受信任的根证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_cmgroot)。 使用 Azure Active Directory (Azure AD) 进行客户端身份验证时不需要此证书，但往往在向导中需要。 如果使用 PKI 客户端身份验证证书，则仍须向 CMG 添加受信任的根证书。



## <a name="co-management"></a>共同管理

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>通过 Microsoft Intune 为共同托管设备同步 MDM 策略
<!--1357377-->
当你切换共同管理工作负荷时，共同管理设备自动从 Microsoft Intune 同步 MDM 策略。 当从 Configuration Manager 控制台的客户端通知中启动“下载计算机策略”操作时也会进行此同步  。 

有关详细信息，请参阅[如何将 Configuration Manager 工作负载切换为 Intune](/sccm/comanage/how-to-switch-workloads)。


### <a name="transition-new-workloads-to-intune-using-co-management"></a>使用共同管理将新的工作负荷转移到 Intune
现在可以在启用共同管理后，将以下工作负荷从 Configuration Manager 转移到 Intune：  

- **设备配置**<!--1357903-->：借助此工作负载，可以使用 Intune 来部署 MDM 策略，同时继续使用 Configuration Manager 来部署应用。  

- **Office 365**<!--1357841-->：设备不会从 Configuration Manager 安装 Office 365 部署。  

- **移动应用**<!--1357892-->：所有从 Intune 部署的应用在公司门户中都可用。 从 Configuration Manager 部署的应用在软件中心可用。 此功能是[预发布功能](/sccm/core/servers/manage/pre-release-features)。  

要转移工作负荷，请转到共同管理属性页并将工作负荷滚动条从 Configuration Manager 移到“试点”或“全部”   。 

有关详细信息，请参阅 [Windows 10 设备共同管理](/sccm/comanage/overview)。


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>支持将多个层次结构合并到一个 Intune 租户
<!--1357944-->
一些客户有多个 Configuration Manager 层次结构，并希望将来合并到一个 Azure Active Directory 和 Microsoft Intune 租户中。 共同管理现支持将多个 Configuration Manager 环境连接到同一个 Intune 租户。

有关详细信息，请参阅[共同管理先决条件](/sccm/comanage/overview#prerequisites)。
 


## <a name="compliance-settings"></a>符合性设置

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>为 Microsoft Edge 配置 Windows Defender SmartScreen 设置
<!--1353701-->
Microsoft Edge 浏览器符合性设置策略添加了以下三个 Windows Defender SmartScreen 设置： 
- 允许 SmartScreen
- 用户可以替代站点的 SmartScreen 提示
- 用户可以替代文件的 SmartScreen 提示

有关详细信息，请参阅[配置 Microsoft Edge 设置](/sccm/compliance/deploy-use/browser-profiles)。


### <a name="scap-extensions"></a>SCAP 扩展
<!--1357552-->
将安全内容自动化协议 (SCAP) 内容转换为符合性设置基准，并使用控制台扩展来生成 SCAP 报告。 此功能还包含一个新仪表板，可用于直观显示客户端符合性和 XCCDF 规则符合性。 

有关详细信息，请参阅[关于 SCAP 扩展](/sccm/compliance/plan-design/scap/about-scap)。



## <a name="application-management"></a>应用程序管理

### <a name="phased-deployment-of-applications"></a>应用程序的分阶段部署
<!--1358147-->
创建应用程序的分阶段部署。 通过分阶段部署，可以根据可自定义条件和组进行协调安排，有序推出软件。 例如，将应用程序部署到试点集合，然后根据成功条件自动继续推出。 

有关详细信息，请参阅下列文章：  

- [创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [管理和监视分阶段部署](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>为设备上的所有用户预配 Windows 应用包
<!--1358310-->
为设备上的所有用户预配包含 Windows 应用包的应用程序。 此方案的一个常见示例是将来自适用于企业和适用于教育的 Microsoft Store 的应用（如 Minecraft: Education Edition）预配到学校学生使用的所有设备。 以前，Configuration Manager 仅支持按用户安装这些应用程序。 登录到新的设备后，学生不得不等会儿时间来访问应用。 现在，将应用预配到所有用户的设备时，他们的工作更快更高效。 

有关详细信息，请参阅[创建 Windows 应用程序](/sccm/apps/get-started/creating-windows-applications#bkmk_provision)。


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Office 自定义工具与 Office 365 安装程序集成
<!--1358149-->
现在 Office 自定义工具在 Configuration Manager 控制台中于 Office 365 安装程序集成。 为 Office 365 创建部署时，可动态配置最新的 Office 可管理性设置。 Microsoft 在发布 Office 365 的新版本时更新 Office 自定义工具。 通过此集成，当 Office 365 中的新可管理性设置可用时，你便可以立即使用。 

有关详细信息，请参阅[部署 Office 365 应用](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)。


### <a name="support-for-new-windows-app-package-formats"></a>支持新的 Windows 应用包格式
<!--1357427-->
Configuration Manager 现在支持部署新的 Windows 10 应用包 (.msix) 和应用程序包 (.msixbundle) 格式。 

有关详细信息，请参阅[创建 Windows 应用程序](/sccm/apps/get-started/creating-windows-applications#bkmk_msix)。


### <a name="uninstall-application-on-approval-revocation"></a>在批准撤消时卸载应用程序
<!--1357891-->
当你撤消应用程序的批准时，行为已更改。 现在当你拒绝应用程序的请求时，客户端将从用户的设备卸载应用程序。 此行为需要启用[可选功能](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_options)“审批每台设备的用户的应用程序请求”  。 

有关详细信息，请参阅[部署应用程序](/sccm/apps/deploy-use/deploy-applications#bkmk_approval)。


### <a name="package-conversion-manager"></a>包转换管理器 
<!--1357861-->
包转换管理器现在是一款集成工具，可便于将旧包转换为 Configuration Manager Current Branch 应用程序。 然后，可以使用应用程序的功能，如依赖关系、要求规则和用户设备相关性。

有关详细信息，请参阅[包转换管理器](/sccm/apps/pcm/package-conversion-manager)。



## <a name="os-deployment"></a>OS 部署

### <a name="improvements-to-phased-deployments"></a>分阶段部署改进

此版本包括对分阶段部署的以下改进：  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>使用手动配置的阶段创建分阶段部署
<!--1358148-->
对于任务序列，现可在创建分阶段部署时手动配置阶段。 可从“创建分阶段部署”向导的“阶段”选项卡添加最多 10 个其他阶段  。 你仍然可以自动创建默认的两阶段部署。 

有段详细信息，请参阅[使用手动配置的阶段创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_manual)。

#### <a name="phased-deployment-status"></a>分阶段部署状态
<!--1358577-->
分阶段部署现在提供本地监视体验。 从“监视”  工作区中的“部署”  节点，选择分阶段部署，然后单击功能区中的“分阶段部署状态”  。 

有关详细信息，请参阅[管理和监视分阶段部署](/sccm/osd/deploy-use/manage-monitor-phased-deployments)。  

#### <a name="gradual-rollout-during-phased-deployments"></a>分阶段部署期间逐渐推出
<!--1358578-->
在分阶段部署期间，每个阶段的推出可以逐步进行。 此行为有助于缓解部署问题的风险，降低网络上因向客户端分发内容而导致的负载。 根据每个阶段的配置，此站点可以逐步使软件可用。 相对于使软件可用的时间，一个阶段中的每个客户端都有一个截止时间。 对于一个阶段中的所有客户端，可用时间和截止时间之间的时间窗都是相同的。 

有关详细信息，请参阅[阶段设置](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_settings)。  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>对 Windows 10 就地升级任务序列的改进
<!--1358500-->
Windows 10 就地升级的默认任务序列模板现在包括在升级过程失败的情况下要添加的带建议操作的另一个新组。 这些操作有助于进行故障排除。 其中一个工具是 Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag)。 它是一个独立的诊断工具，可获取有关 Windows 10 升级失败原因的详细信息。 

有关详细信息，请参阅[创建用于升级 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-on-failure)。


### <a name="improvements-to-pxe-enabled-distribution-points"></a>对已启用 PXE 的分发点的改进
<!--1357580-->
在分发点属性的“PXE”  选项卡上，选中“在没有 Windows 部署服务的情况下启用 PXE 响应者”  。 此选项在分发点上启用 PXE 响应方，而不需要 Windows 部署服务 (WDS)。 由于 WDS 不是必需的，因此已启用 PXE 的分发点可以是客户端或服务器 OS，包括 Windows Server Core。 这个新的 PXE 响应方服务支持 IPv6，还增强了远程办公室中已启用 PXE 的分发点的灵活性。 

有关详细信息，请参阅[在分发点上启用 PXE](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。


### <a name="network-access-account-not-required-for-some-scenarios"></a>某些方案不需要网络访问帐户
<!--1358278,1358279-->
[增强型 HTTP 站点系统](#bkmk_ehttp)功能还会删除网络访问帐户上的一些依赖项。 当启用“将 Configuration Manager 生成的证书用于 HTTP 站点系统”的新选项时，以下方案不需用网络访问帐户从分发点下载内容  ：  

- 从启动媒体或 PXE 运行的任务序列
- 从软件中心运行的任务序列  

这些任务序列可以用于操作系统部署或者是自定义的。 它还支持工作组计算机。

有关详细信息，请参阅[任务序列和网络访问帐户](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSNetworkAccessAccount)。


### <a name="other-improvements-to-os-deployment"></a>对 OS 部署的其他改进

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>屏蔽任务序列变量中存储的敏感数据
 <!--1358330-->
 在**设置任务序列变量**步骤中，选择新选项“不显示此值”  。 

 有关详细信息，请参阅[设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)。 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>在执行任务序列的“运行命令步骤”期间屏蔽程序名称
 <!--1358493-->
 若要防止显示或记录潜在的敏感数据，请配置任务序列变量 OSDDoNotLogCommand  。  

 有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables#OSDDoNotLogCommand)。 

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>安装驱动程序时 DISM 参数的任务序列变量
 <!--516679/2840016-->
 若要为 DISM 指定其他命令行参数，请使用新的任务序列变量 OSDInstallDriversAdditionalOptions  。 

 有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables#OSDInstallDriversAdditionalOptions)。 

#### <a name="option-to-use-full-disk-encryption"></a>“使用全磁盘加密”选项
 <!--SCCMDocs-pr issue 2671-->
 “启用 BitLocker”  和“预配 BitLocker”  步骤现在都包含“使用完整磁盘加密”  选项。 默认情况下，这些步骤会加密驱动器上的已用空间。 建议使用此默认行为，因为它更加快速高效。 

 有关详细信息，请参阅[启用 BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_EnableBitLocker) 和[预配 BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_PreProvisionBitLocker)。 

#### <a name="client-provisioning-mode-isnt-enabled-with-windows-10-upgrade-compatibility-scan"></a>未对 Windows 10 升级兼容性扫描启用客户端预配模式
 <!--SCCMDocs-pr issue 2812-->
 现在，如果你启用“在不启动升级的情况下执行 Windows 安装程序兼容性扫描”  选项，“升级操作系统”  任务序列步骤不会将 Configuration Manager 客户端置于预配模式下。

 有关详细信息，请参阅[升级操作系统](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)

#### <a name="revised-documentation-for-task-sequence-variables"></a>任务序列变量的修订文档
现在，提供了两篇新文章用于了解任务序列变量：  

- [如何使用任务序列变量](/sccm/osd/understand/using-task-sequence-variables)是一篇新文章，介绍不同类型的变量、设置变量的方法，以及如何访问变量。  

- [任务序列变量](/sccm/osd/understand/task-sequence-variables)是对所有可用任务序列变量的引用。 本文将结合之前的文章，以将内置变量与操作变量相分离。 



## <a name="software-center"></a>软件中心

> [!Important]  
> 若要利用新的 Configuration Manager 功能，请先将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。


### <a name="software-center-infrastructure-improvements"></a>软件中心基础结构的改进
<!--1358309-->
不再需要应用程序目录角色，即可在软件中心显示用户可用的应用程序。 此项更改有助于减少向用户交付应用程序所需的服务器基础结构。 软件中心现在依靠管理点来获取此信息，通过将更大的环境分配给[边界组](/sccm/core/servers/deploy/configure/boundary-groups#management-points)来帮助它们更好地扩展。

有关详细信息，请参阅[配置软件中心](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)  

> [!Note]  
> 1806 中不再需要应用程序目录站点和 Web 服务点角色，但该角色依然受支持   。 
> 
> 应用程序目录网站点的 Silverlight 用户体验不再受支持  。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>指定应用程序目录网站链接在软件中心的可见性
<!--1358214-->
使用客户端设置来控制“打开应用程序目录网站”  链接是否显示在软件中心的“安装状态”  节点中。  

有关详细信息，请参阅[软件中心客户端设置](/sccm/core/clients/deploy/about-client-settings#software-center)。

> [!Note]  
> 应用程序目录网站点的 Silverlight 用户体验不再受支持  。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。  


### <a name="custom-tab-for-webpage-in-software-center"></a>软件中心用于网页的自定义选项卡
<!--1358132-->
使用客户端设置在软件中心内创建用于打开网页的自定义选项卡。 此功能可让你以一致、可靠的方式向最终用户展示内容。 以下列表包含几个示例：  

- 联系 IT 部门：有关如何联系组织 IT 部门的信息  

- IT 支持中心：IT 自助操作，如搜索知识库或开启支持票证。  

- 最终用户文档：面向组织中的用户的文章，涉及各种 IT 主题，例如使用应用程序或升级到 Windows 10。  

有关详细信息，请参阅[软件中心客户端设置](/sccm/core/clients/deploy/about-client-settings#software-center)和[软件中心用户指南](/sccm/core/understand/software-center)。


### <a name="maintenance-windows-in-software-center"></a>软件中心的维护时段
<!--1358131-->
软件中心现在显示下一个计划性维护时段。 在“安装状态”选项卡上，将视图从“全部”切换为“即将进行”。 它显示时间范围和计划部署列表。 如果没有将来的维护时段，则该列表为空。 

有关详细信息，请参阅[如何使用维护时段](/sccm/core/clients/manage/collections/use-maintenance-windows)和[软件中心用户指南](/sccm/core/understand/software-center)。



## <a name="software-updates"></a>软件更新

### <a name="third-party-software-updates"></a>第三方软件更新
<!--1357605, 1352101, 1358714-->
通过第三方软件更新，可以在 Configuration Manager 控制台中订阅合作伙伴目录，并将更新发布到 WSUS。 然后可以使用现有的软件更新管理进程来部署这些更新。 

有关详细信息，请参阅[启用第三方更新](/sccm/sum/deploy-use/third-party-software-updates)。


### <a name="deploy-software-updates-without-content"></a>部署无内容的软件更新
<!--1357933-->
将软件更新部署到设备，而无需先下载并将内容分发到分发点。 当处理非常大的更新内容时，或者当始终希望客户端从 Microsoft 更新云服务中获取内容时，此功能很有用。 在此方案中的客户端还可以从已具有所需内容的对等节点下载内容。 Configuration Manager 客户端继续管理内容下载，因此可以利用 Configuration Manager 对等缓存功能或其他技术，如交付优化。 此功能支持受 Configuration Manager 软件更新管理（包括 Windows 和 Office 更新）支持的任何更新类型。 

有关详细信息，请参阅[手动部署软件更新](/sccm/sum/deploy-use/manually-deploy-software-updates)或[自动部署软件更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)时的“无部署包”选项  。


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>通过软件更新体系结构更新自动部署规则
 <!--1322266-->
现在可以筛选自动部署规则 (ADR)，以排除 Itanium 和 ARM64 等体系结构。 在“创建自动部署规则向导”的软件更新页面上，现可使用“体系结构”属性筛选器   。 

有关详细信息，请参阅[自动部署软件更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)。


### <a name="improved-wsus-maintenance"></a>改进了 WSUS 维护 
<!--1357898-->
WSUS 清理向导现在根据对软件更新点组件属性定义的取代规则来拒绝已到期的更新。 

有关详细信息，请参阅[软件更新维护](/sccm/sum/deploy-use/software-updates-maintenance)。



## <a name="reporting"></a>报表

### <a name="new-software-updates-compliance-report"></a>新的软件更新符合性报告
<!--1357775-->
软件更新符合性报告传统上包含最近未联系站点的客户端中的数据。 你可以通过“符合性 9 - 总体运行状况和符合性”这一新报告按“正常运行”客户端筛选特定软件更新组的符合性结果  。 此报告显示你环境中的活动客户端的更真实的符合性状态。 

有关详细信息，请参阅[软件更新报告](/sccm/sum/deploy-use/monitor-software-updates#BKMK_SUReports)。



## <a name="inventory"></a>清单

### <a name="bkmk_bigint"></a> 对大整数值硬件清单的改进
<!--1357880-->
硬件清单之前的限制为，整数不超过 4,294,967,296 (2^32)。 对于诸如以字节为单位的硬盘大小之类的属性，可以达到此限制。 管理点不会处理超过此限制的整数值，因此数据库中不会存储任何值。 现在，此版本中的限制增加到了 18,446,744,073,709,551,616 (2^64)。 

有关详细信息，请参阅[使用大整数值](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory#bkmk_bigint)。


### <a name="hardware-inventory-default-unit-revision"></a>硬件清单默认单位修订
<!--514442-->
在 [Configuration Manager 版本 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure) 中，许多报表视图中使用的默认单元从兆字节 (MB) 更改为千兆字节 (GB)。 由于[硬件清单的大整数值改进](#bkmk_bigint)，并且根据客户反馈，此默认单位现在又是 MB。



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Configuration Manager 控制台

### <a name="product-lifecycle-dashboard"></a>产品生命周期仪表板
<!--1319632-->
产品生命周期仪表板显示，安装在 Configuration Manager 托管设备上的 Microsoft 产品的 Microsoft 生命周期策略状态。 它还提供有关环境中 Microsoft 产品的信息、可支持性状态以及支持结束日期。 使用仪表板了解对每个产品的支持的可用性。 这些信息有助于规划在到达当前支持结束日期之前，何时更新使用的 Microsoft 产品。   

有关详细信息，请参阅[产品生命周期仪表板](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard)。


### <a name="copy-asset-details-from-monitoring-views"></a>支持从监视视图中复制资产详细信息
<!--1357856-->
“监视”  工作区的以下区域现支持复制文本：  

- 在“部署”节点中，选择部署，然后单击“查看状态”   。 在“部署状态”视图的“资产详细信息”窗格中，选择一个或多个设备  。  

- 展开“分发状态”节点，然后选择“内容状态”   。 选择一个软件，然后单击“查看状态”  。 在“内容状态”视图的“资产详细信息”窗格中，选择一个或多个分发点  。 

右键单击资产，并选择“复制”  。 此操作将选定的资产复制为包含完整详细信息的逗号分隔列表。 键盘快捷方式 CTRL + C 也适用于这些视图   。 

有关详细信息，请参阅 [1806 版中的控制台改进](/sccm/core/servers/manage/admin-console#copy-details-in-monitoring-views)。


### <a name="improvements-to-the-surface-dashboard"></a>Surface 仪表板的改进
<!--1358654-->
此版本包括对 Surface 仪表板的以下改进：  

- 选中特定图表部分时，Surface 仪表板现在会显示相关设备列表：  

   - 单击“Surface 设备所占百分比”磁贴将打开 Surface 设备列表  。  

   - 单击“前五个固件版本”磁贴中的栏，将打开带有特定固件版本的 Surface 设备列表  。  

- 当从 Surface 仪表板查看这些设备列表时，可以右键单击设备以执行常见操作。  

有关详细信息，请参阅 [Surface仪表板](/sccm/core/clients/manage/surface-device-dashboard)。


### <a name="view-the-currently-signed-on-user-for-a-device"></a>查看设备的当前已登录用户
<!--1358202-->
现在，“资产和符合性”  工作区的“设备”  节点默认显示“当前已登录用户”  列。 它还会显示任何特定于集合的设备列表。 此值与[客户端状态](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus)同步保持最新。 当用户注销时，客户端会清除此值。 如果没有用户登录，则值为空。 

有关详细信息，请参阅 [1806 版中的控制台改进](/sccm/core/servers/manage/admin-console#view-users-for-a-device)。


### <a name="submit-feedback-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台提交反馈  
<!--1357542-->

发送笑脸！ 现在可以就你的体验直接告知 Configuration Manager 团队。 从 Configuration Manager 控制台发送反馈很简单。 我们希望听到你的所有反馈：表扬、问题和建议。 在 Configuration Manager 控制台中，单击功能区上方右上角的笑脸按钮。 该反馈将直接提交给 Configuration Manager 的 Microsoft 产品团队。 虽然仍然支持使用 Windows 10 反馈中心，但最好使用控制台内部的反馈机制。  

有关详细信息，请参阅 [1806 版中的控制台改进](/sccm/core/servers/manage/admin-console#send-feedback)和[产品反馈](/sccm/core/understand/find-help#BKMK_1806Feedback)。



## <a name="other-updates"></a>其他更新

除了新增功能外，这一版还有其他变化（如缺陷修复）。 有关详细信息，请参阅 [Configuration Manager Current Branch（版本 1806）的更改摘要](https://support.microsoft.com/help/4459701)。

若要详细了解用于 Configuration Manager 的 Windows PowerShell cmdlet 的更改，请参阅 [PowerShell 1806 发行说明](https://docs.microsoft.com/powershell/sccm/1806_release_notes?view=sccm-ps)。

以下更新汇总 (4462978) 于 2018 年 10 月 24 日起在控制台中提供：[Configuration Manager Current Branch（版本 1806）更新汇总](https://support.microsoft.com/help/4462978)。


### <a name="hotfixes"></a>修补程序

以下附加修补程序可用于解决特定问题：

| ID | 标题 | 日期 | 控制台内部 |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | System Center Configuration Manager（版本 1806）更新，第一波 | 2018 年 8 月 31 日 | 是 |
| [4465865](https://support.microsoft.com/help/4465865) | 如果 WSUS 断开连接，则不会在 Configuration Manager 环境中下载软件更新<br><br>更新汇总 (4462978) 中也包括此更新 | 2018 年 10 月 1 日 | 是 |
| [4471892](https://support.microsoft.com/help/4471892) | PXE 响应程序不适用于 Configuration Manager 1806 中的子集 | 2018 年 11 月 23 日 | 否 |
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune 连接器证书在 Configuration Manager 中未续订 | 2019 年 1 月 18 日 | 是 |


## <a name="next-steps"></a>后续步骤

准备好安装此版本时，请参阅[安装 Configuration Manager 的更新](/sccm/core/servers/manage/updates)和 [1806 安装更新清单](/sccm/core/servers/manage/checklist-for-installing-update-1806)。

> [!TIP]  
> 若要安装新站点，请使用 Configuration Manager 的基准版本。  
>
> 了解详细信息：    
> - [安装新站点](/sccm/core/servers/deploy/install/installing-sites)  
> - [基准和更新版本](/sccm/core/servers/manage/updates#bkmk_Baselines)

关于已知的重要问题，请参阅[发行说明](/sccm/core/servers/deploy/install/release-notes)。

更新站点后，还可以查看[更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1806#post-update-checklist)。
