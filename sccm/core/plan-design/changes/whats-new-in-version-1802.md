---
title: 新的 1802 版
titleSuffix: Configuration Manager
description: 获取有关 Configuration Manager 1802 版中引入的更改和新功能的详细信息。
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4582d1105f2465c37e001570227112bfca3bad1c
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="whats-new-in-version-1802-of-system-center-configuration-manager"></a>System Center Configuration Manager 1802 版的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager Current Branch 的 1802 更新作为控制台中更新提供。 将此更新应用于运行 1702、1706 或 1710 版的站点。 <!-- baseline only statement: -->安装新站点时，也可将其用作基准版本。

> [!TIP]  
> 若要安装新站点，必须使用 Configuration Manager 的基准版本。  
>
>  了解详细信息：    
>   - [安装新站点](/sccm/core/servers/deploy/install/installing-sites)  
>   - [在站点上安装更新](/sccm/core/servers/manage/updates)  
>   - [基准和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

以下各节提供有关 Configuration Manager 1802 版中的更改和新功能的详细信息。  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>站点基础结构

### <a name="reassign-distribution-point"></a>重新分配分发点
<!-- 1306937 -->
许多客户都有大型的 Configuration Manager 基础结构，并且正在减少主站点或辅助站点来简化其环境。 他们仍需要在分支机构位置保留分发点，以向托管客户提供内容。 这些分发点通常包含多个 TB 或更多的内容。 将此内容分发到这些远程服务器所需的时间和网络带宽成本高昂。 此功能允许向其他主站点重新分配分发点，而无需重新分发内容。 此操作可更新站点系统分配，同时在服务器上保留所有内容。 有关详细信息，请参阅[重新分配分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign)。

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>配置 Windows 传递优化以使用 Configuration Manager 边界组
<!-- 1324696 -->
使用 Configuration Manager 边界组来定义和控制跨公司网络和到远程办公室的内容分发。 [Windows 传递优化](/windows/deployment/update/waas-delivery-optimization)是一种基于云的对等技术，用于在 Windows 10 设备之间共享内容。 从此版本开始，配置传递优化以在对等方之间共享内容时使用边界组。 新的客户端设置将边界组标识符用作客户端上的传递优化组标识符。 当客户端与传递优化云服务进行通信时，它使用此标识符来查找具有所需内容的对等方。 有关详细信息，请参阅[内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization)。

### <a name="support-for-windows-10-arm64-devices"></a>Windows 10 ARM64 设备支持
<!-- 1353704 -->
从此版本开始，Windows 10 ARM64 设备将支持 Configuration Manager 客户端。 现有客户端管理功能应适用于这些新设备。 例如，硬件和软件清单、软件更新和应用程序管理。 当前不支持操作系统部署。 

### <a name="improved-support-for-cng-certificates"></a>改进了对 CNG 证书的支持
<!-- 1357314 -->
Configuration Manager（当前分支）版本 1710 支持[下一代加密技术 (CNG) 证书](/sccm/core/plan-design/network/cng-certificates-overview)。 版本 1710 在多种方案中对客户端证书提供有限支持。 

从此版本开始，CNG 证书将用于以下已启用 HTTPS 的服务器角色：
- 管理点
- 分发点
- 软件更新点
- 状态迁移点  


### <a name="boundary-group-fallback-for-management-points"></a>管理点的边界组回退
<!-- 1324594 -->
可在[边界组](/sccm/core/servers/deploy/configure/boundary-groups)之间配置管理点的回退关系。 此行为可以更好地控制客户端使用的管理点。 有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups#management-points)。


### <a name="cloud-distribution-point-site-affinity"></a>云分发点站点相关性
<!--503719-->
如果客户的层次机构具有多个站点且在地理上各处分散，则此功能可以使用云分发点帮助客户。 以前，当基于 Internet 的客户端搜索内容时，客户端收到的云分发点列表没有顺序。 此行为可能导致基于 Internet 的客户端从地理上相距遥远的云分发点接收内容。 从这种距离较远的服务器下载内容的速度通常会比较近的服务器慢。
 
在具有云分发点站点相关性的前提下，基于 Internet 的客户端会收到排好顺序的列表。 此列表会根据客户端的分配站点优先排列云分发点。 此行为让管理员可以保留他们从站点资源下载内容的设计意图。
 

## <a name="management-insights"></a>管理见解
<!-- 1353967 -->
System Center Configuration Manager 中的管理见解提供有关环境当前状态的信息。 该信息基于对站点数据库中数据的分析。 见解有助于更好地了解环境，并根据见解执行操作。 有关详细信息，请参阅[管理见解](/sccm/core/servers/manage/management-insights)

Configuration Manager 1802 中提供以下见解：
- 应用程序
    - 不具有部署的应用程序
- 云服务：<!--1356412-->
    - 评估共同管理准备情况 
    - 使设备加入混合 Azure Active Directory
    - 更新标识和访问基础结构
    -  将客户端升级到 Windows 10 1709 版或更高版本 
- 集合：
    - 空集合
- 简化管理：<!--1355148-->
    - 过时的客户端版本  
- 软件中心： 
    - 将用户定向到软件中心，而不是应用程序目录  
    - 使用新版软件中心 
- Windows 10：<!--1357421-->
    - 配置 Windows 遥测和商业 ID 键 
    - 将 Configuration Manager 连接至 Upgrade Readiness 
   
<!-- ## Migration  -->



## <a name="client-management"></a>客户端管理

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>云管理网关支持 Azure 资源管理器
<!-- 1324735 -->
在创建[云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG) 实例时，向导现提供选项来创建“Azure 资源管理器部署”。 [Azure 资源管理器](/azure/azure-resource-manager/resource-group-overview)是一个现代平台，用于以单个实体（称为[资源组](/azure/azure-resource-manager/resource-group-overview#resource-groups)）的方式来管理所有解决方案资源。 如果在 Azure 资源管理器中部署 CMG，站点将使用 Azure Active Directory (Azure AD) 进行身份验证并创建必要的云资源。 此现代化部署不需要经典 Azure 管理证书。 有关详细信息，请参阅 [CMG 拓扑设计](/sccm/core/clients/manage/plan-cloud-management-gateway#azure-resource-manager)。

> [!IMPORTANT]
> 此功能不提供对 Azure 云服务提供商 (CSP) 的支持。 Azure 资源管理器中的 CMG 部署将继续使用 CSP 不支持的经典云服务。 有关详细信息，请参阅 [Azure CSP 中可用的 Azure 服务](/azure/cloud-solution-provider/overview/azure-csp-available-services)。  

### <a name="improvements-to-cloud-management-gateway"></a>云管理网关的改进  

- 从此版本开始，“云管理网关”不再是预发行功能。  

- 功能文档已经过修订和增强。 有关详细信息，请参阅下列文章：
    - [规划云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
    - [云管理网关的大小和扩展数量](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
    - [云管理网关的安全和隐私](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
    - [有关云管理网关的常见问题解答](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
    - [云管理网关的证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
    - [设置云管理网关](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>配置硬件清单以收集超过 255 个字符的字符串
<!-- 1357389 -->
可以针对硬件清单属性将字符串长度配置为超过 255 个字符。 此更改仅适用于新添加的类和不为键的硬件清单属性。 有关详细信息，请参阅文章[扩展硬件清单](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255)。 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Linux 和 Unix 客户端支持的弃用公告
 <!--510139-->
Microsoft 计划从现在起大约一年后弃用 System Center Configuration Manager 中的 Linux 和 UNIX 客户端支持，因此，2019 年初的 SCCM 1902 发布中将不会包括这些客户端。  2018 年底的 Configuration Manager 1810 版将是包含 Linux 和 UNIX 客户端的最后一个版本，Configuration Manager 1810 的整个生命周期都将支持这些客户端。  Configuration Manager 1810 后，客户应考虑使用 Microsoft Operations Management Suite 管理 Linux 服务器。  OMS 具有广泛的 Linux 支持（包括面向 Linux 的端到端补丁管理），在大多数情况下优于 Configuration Manager 的功能。

### <a name="surface-device-dashboard"></a>Surface 设备仪表板
<!--1355788-->
Surface 设备仪表板提供有关在环境中找到的 Surface 设备的信息。 在控制台中，转到“监视” > “Surface 设备”。 可以查看以下项：
- Surface 百分比
- Surface 型号百分比
- 前五个固件版本

有关详细信息，请参阅文章 [Surface 仪表板](/sccm/core/clients/manage/surface-device-dashboard)。

### <a name="change-in-the-configuration-manager-client-install"></a>Configuration Manager 客户端安装中的更改
<!--1356195-->|
从此版本开始，客户端设备上不会自动安装 Silverlight。 有关详细信息，请参阅[将客户端部署到 Windows 计算机的先决条件](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.#BKMK_ExternalDependencies)

## <a name="co-management"></a>共同管理

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>使用共同管理将 Endpoint Protection 工作负荷转移到 Intune
<!-- 1357365 -->
 启用共同管理后，Endpoint Protection 工作负荷可以转换到 Intune。 若要转移 Endpoint Protection 工作负荷，请转到共同管理属性页，并将滚动条从 Configuration Manager 移动到“试点”或“所有”。 有关工作负荷的详细信息，请参阅[工作负荷能够转换到 Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)。 有关共同管理的详细信息，请参阅 [Windows 10 设备共同管理](/sccm/core/clients/manage/co-management-overview)。
 
### <a name="co-management-dashboard-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的共同管理仪表板
<!--1356648-->
从此版本开始，可以查看包含共同管理相关信息的仪表板。 此仪表板可帮助你查看环境中共同管理的计算机。 图形有助于标识可能需要注意的设备。 有关详细信息，请参阅文章[共同管理仪表板](\sccm\core\clients\manage\client-management-dashboard)。 


## <a name="compliance-settings"></a>符合性设置

### <a name="microsoft-edge-browser-policies"></a>Microsoft Edge 浏览器策略
<!-- 1357310 -->
在 Windows 10 客户端上使用 [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) Web 浏览器的客户，可创建 Configuration Manager 符合性设置策略，以配置多个 Microsoft Edge 设置。 有关详细信息，请参阅[创建 Microsoft Edge 浏览器配置文件](/sccm/compliance/deploy-use/browser-profiles)。 



## <a name="application-management"></a>应用程序管理

### <a name="allow-user-interaction-when-installing-an-application"></a>允许在安装应用程序时进行用户交互
<!-- 1356976 -->
允许最终用户在任务序列运行期间与应用程序安装进行交互。 例如，运行安装过程会提示最终用户各种选项。 某些应用程序安装程序无法关闭用户提示或安装过程需要仅用户知道的特定配置值。 此功能可用于处理这些安装方案。 有关详细信息，请参阅[指定部署类型的用户体验选项](/sccm/apps/deploy-use/create-applications#specify-user-experience-options-for-the-deployment-type)。

### <a name="do-not-automatically-upgrade-superseded-applications"></a>不自动升级被取代的应用程序
<!-- 1351266 -->
将应用程序部署配置为不自动升级任何被取代的版本。 现在创建部署时，在“部署软件向导”的“部署设置”页中，对于可用的或必需的安装目的，可启用或禁用“自动升级此应用程序的任何被取代版本”选项。 有关详细信息，请参阅[指定部署设置](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings)。

### <a name="approve-application-requests-for-users-per-device"></a>审批每台设备的用户的应用程序请求
<!-- 1357015 -->
从此版本开始，当用户请求需要审批的应用程序时，特定设备名称现为请求的一部分。 如果管理员批准请求，则用户只能在该设备上安装应用程序。 用户必须提交另一个请求才能在另一台设备上安装应用程序。 有关详细信息，请参阅[指定部署设置](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings)。

 > [!Note]  
 > 这是一个可选功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。  


### <a name="run-scripts-improvements"></a>运行脚本的改进 
<!-- 1236459 -->
 从此版本开始，“运行脚本”不再是预发行功能。 脚本输出现在使用 JSON 格式返回。 有关详细信息，请参阅[从 Configuration Manager 控制台创建并运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)。


## <a name="operating-system-deployment"></a>操作系统部署

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>通过云管理网关执行的 Windows 10 就地升级任务序列
<!-- 1357149 -->
Windows 10 [就地升级任务序列](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)现在支持部署到通过[云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway)托管的基于 Internet 的客户端。 此功能可让远程用户更轻松地升级到 Windows 10，而无需连接公司网络。 有关详细信息，请参阅 [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg)。

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>对 Windows 10 就地升级任务序列的改进
<!-- 1357425 -->
Windows 10 就地升级的默认任务序列模板现在包括在升级过程前后要添加的带建议操作的其他组。 这些操作在许多将设备成功升级到 Windows 10 的客户之间是通用的。 有关详细信息，请参阅[创建用于升级 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-to-prepare-for-upgrade)。

### <a name="improvements-to-operating-system-deployment"></a>对操作系统部署的改进
此版本包括对操作系统部署的以下改进：
 - 在 Windows PE 中，启动 cmtrace.exe 时不再提示选择是否将此程序设置为日志文件的默认查看器。 <!-- SMS 500897 -->
 - 将启动映像添加到[下载包内容](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent)任务序列步骤。
 - 对[运行任务序列](/sccm/osd/understand/task-sequence-steps#child-task-sequence)步骤的改进：<!-- 1261338 -->   
     - 支持所有来自软件中心、PXE和媒体的操作系统部署方案。
     - 在对象删除期间改进控制台操作，例如复制、导入、导出和警告。
     - 支持[创建预留内容文件](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent)向导。
     - 与部署验证集成。 有关详细信息，请参阅[高风险任务序列部署](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)。 
     - 运行任务序列步骤现在可以在多级别任务序列中使用，而不仅仅适用于单个父子关系。 多级别关系会增加复杂性，请谨慎使用。 仍会检查这些关系的循环引用。
    
### <a name="deployment-templates-for-task-sequences"></a>任务序列的部署模板
<!-- 1357391 -->
[任务序列的部署向导](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)现在可以创建部署模板。 部署模板可以保存并应用到现有或新任务序列以创建部署。 

### <a name="phased-deployments-for-task-sequences"></a>任务序列的分阶段部署
<!--1356837-->
 分阶段部署是一项[预发行功能](/sccm/core/servers/manage/pre-release-features)。 分阶段部署可在多个集合中自动协调有序地推出任务序列。 [创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)时，既可以使用默认的两个阶段，也可以手动配置多个阶段。 任务序列的分阶段部署不支持 PXE 或介质安装。




## <a name="software-center"></a>软件中心

### <a name="install-multiple-applications-in-software-center"></a>安装软件中心中的多个应用程序
<!-- 1357126 -->
如果最终用户或桌面技术人员需要在设备上安装多个应用程序，软件中心现在支持安装多个选定的应用程序。 通过此行为，用户无需等待安装完成即可开始下一个安装，从而提高工作效率。 有关详细信息，请参阅新软件中心用户指南中的[安装多个应用程序](/sccm/core/understand/software-center#install-multiple-applications)。

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>在已加入 Azure AD 的设备上，使用软件中心来浏览和安装用户可用的应用程序
<!-- 1322613 -->
如果将应用程序以可用的方式部署到用户，则他们现在可以通过 Azure Active Directory (Azure AD) 设备上的软件中心浏览和安装应用程序。 有关详细信息，请参阅[在加入 Azure AD 的设备上部署用户可用的应用程序](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)。

### <a name="hide-installed-applications-in-software-center"></a>在软件中心隐藏安装的应用程序
<!--1357592-->
安装的应用程序现在可以在软件中心隐藏。 在客户端设置下启用此选项后，已安装的应用程序将不再显示在“应用程序”选项卡中。 安装或升级到 Configuration Manager 1802 时，此选项会设置为默认选项。  仍可以在安装状态选项卡下查看已安装的应用程序。[在软件中心隐藏安装的应用程序](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled)提供其他详细信息。   

### <a name="hide-unapproved-applications-in-software-center"></a>在软件中心隐藏未批准的应用程序
 <!--1355146-->
启用此客户端设置选项后，软件中心将隐藏需要批准的用户可用应用程序。  [在软件中心隐藏未批准的应用程序](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved)提供其他详细信息。  

### <a name="software-center-shows-user-additional-compliance-information"></a>软件中心显示用户的其他符合性信息
<!-- 1235616 -->
 现在，将设备运行状况证明状态用作对公司资源进行条件性访问的符合性策略规则时，软件中心会向用户显示不符合的设备运行状况证明设置。


 ## <a name="software-updates"></a>软件更新 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>将自动部署规则评估安排为偏移一个基准日。 
<!--1357133-->
可以安排自动部署规则评估，使其偏移一个基准日。 也就是说，如果周二补丁日对你而言实际上是星期三，则可以将评估计划设置为该月的第二个周二偏移一天。 有关详细信息，请参阅[自动部署软件更新](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule)。 



## <a name="reporting"></a>报表

### <a name="report-for-default-browser-counts"></a>默认浏览器计数报表
<!-- 1357830 -->
现在提供了一个新报表来显示将特定 Web 浏览器作为 Windows 默认浏览器的客户端计数。 请参阅“软件 - 公司和产品”报表组中的“默认浏览器计数”报表。 有关详细信息，请参阅[报表列表](/sccm/core/servers/manage/list-of-reports#software---companies-and-products)。

### <a name="report-on-windows-autopilot-device-information"></a>关于 Windows AutoPilot 设备信息的报表
<!-- 1351442 -->
Windows AutoPilot 是以现代方式载入和配置新 Windows 10 设备的一种解决方案。 有关详细信息，请参阅 [Windows AutoPilot 概述](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot)。 向 Windows AutoPilot 注册现有设备的一种方法是，将设备信息上传到 Microsoft Store 商业版和教育版。 此信息包括设备序列号、Windows 产品标识符和硬件标识符。 使用 Configuration Manager 通过“硬件 - 常规”报表节点中的新报表“Windows AutoPilot 设备信息”收集和报告此设备信息。 有关详细信息，请参阅准备进行公共管理中的[新 Windows 10 设备](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices)。

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>特定集合的 Windows 10 维护服务详细信息报表
<!--1357653-->
“特定集合的 Windows 10 维护服务详细信息”报表显示与特定集合的 Windows 10 维护服务相关的常规信息。 此报表显示 Windows 10 设备的资源 ID、NetBIOS 名称、OS 名称、OS 版本名称、内部版本、OS 分支和服务状态。 有关详细信息，请参阅[报表列表](/sccm/core/servers/manage/list-of-reports#operating-system)



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>保护设备

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>对 Configuration Manager 的 Windows Defender 攻击防护策略的改进
<!-- 1356220 -->
在 Configuration Manager 中，为 [Windows Defender 攻击防护](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard)添加了有关[攻击面减少](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#BKMK_ASR)和[受控文件夹访问权限](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#BKMK_CFA)组件的其他策略设置。

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Windows Defender 应用程序防护的新主机交互设置
<!-- 1356256 -->
Windows 10 1709 版和更高版本的设备中包含面向 [Windows Defender 应用程序防护](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS)的两种新主机交互设置： 
- 可向网站授予主机虚拟图形处理器的访问权限。 
- 容器内已下载的文件可保存在主机上。 




## <a name="configuration-manager-console"></a>Configuration Manager 控制台

### <a name="improvements-to-the-configuration-manager-console"></a>对 Configuration Manager 控制台的改进 
此版本包含对 Configuration Manager 控制台的以下改进。
- 默认情况下，现在“资产和符合性”、“设备”下的设备列表显示主要用户。 此列仅在“设备”节点中显示。 上次登录的用户还可以作为可选列添加。<!-- 1357280 --> 为站点启用[用户和设备相关性](/sccm/core/clients/deploy/about-client-settings#user-and-device-affinity)客户端设置，将主要用户与设备相关联。
- 如果一个集合是另一个集合的成员且已重命名，新名称将根据成员资格规则更新。<!--1357282--> 
- 在 DPI 缩放比例不同的多个监视器中对客户的使用远程控制时，鼠标光标现可在监视器之间进行正确映射。 <!--433170-->
- 选中图形部分时，[Office 365 客户端管理仪表板](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)会显示相关设备的列表。 <!--1357281 --> 



## <a name="next-steps"></a>后续步骤
准备好安装此版本时，请参阅 [Configuration Manager 的更新](/sccm/core/servers/manage/updates)。
