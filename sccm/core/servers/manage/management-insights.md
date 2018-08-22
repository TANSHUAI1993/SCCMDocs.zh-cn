---
title: 管理见解
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 控制台中提供的管理见解功能。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 92f82ee7247030d19df63e50b0ac4437f250717a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383491"
---
# <a name="management-insights-in-configuration-manager"></a>Configuration Manager 中的管理见解

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的管理见解功能提供了环境当前状态的相关信息。 该信息基于对站点数据库中数据的分析。 见解有助于更好地了解环境，并根据见解执行操作。 此功能在 Configuration Manager 1802 版中发布。 <!--1353967-->



## <a name="review-management-insights"></a>查看管理见解 

若要查看规则，帐户需要站点对象的读取权限。

1. 请打开 Configuration Manager 控制台。  

2. 转到“管理”工作区并单击“管理见解”。  

3. 选择“所有见解”。  

4. 双击要查看的“管理见解组名称”。 或突出显示该见解，然后单击功能区中的“显示见解”。  

以下四个选项卡可供查看： 

- **所有规则**：提供所选管理见解组的完整规则列表。  

- **已完成**：列出无需执行任何操作的规则。  

- **正在进行**：显示已完成部分（但非全部）先决条件的规则。  

- **需要执行操作**：列出需要执行操作的规则。 右键单击并选择“更多详细信息”可检索需要执行操作的特定项目。  

“先决条件”窗格列出了运行规则所需的项目。

#### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>云服务组的所有规则和先决条件
![管理见解 - 云服务组的所有规则和先决条件](./media/Management-insights-all-cloud-rules.png)


选择规则并单击“更多详细信息”，查看规则详细信息。



## <a name="operations"></a>操作

管理见解规则每周重新评估一次适用性。 若要按需重新评估规则，请右键单击该规则并选择“重新评估”。

管理见解规则的日志文件是站点服务器上的 SMS_DataEngine.log。

<!--1357930-->从版本 1806 开始，一些规则允许执行操作。 选择规则，单击“更多详细信息”，然后单击“执行操作”（如果可用）。 

根据规则，此操作会出现以下某一行为：  

- 在控制台中自动导航到可以采取进一步操作的节点。 例如，如果管理见解建议更改客户端设置，执行操作将导航到“客户端设置”节点。 然后通过修改默认或自定义客户端设置对象采取进一步操作。  

- 基于查询导航到筛选的视图。 例如，对空集合规则执行操作只会在集合列表中显示这些集合。 然后采取进一步操作，例如删除集合或修改其成员身份规则。  



## <a name="groups-and-rules"></a>组和规则

规则分为不同的管理见解组。 有关当前可用的组和规则，请参阅以下列表：


### <a name="applications"></a>应用程序

应用程序管理见解。

- **没有部署的应用程序**：列出环境中没有活动部署的应用程序。 此规则有助于查找并删除未使用的应用程序，以简化显示在控制台中的应用程序列表。 有关详细信息，请参阅[部署应用程序](/sccm/apps/deploy-use/deploy-applications)。  


### <a name="cloud-services"></a>Cloud Services

帮助与多种云服务集成，实现设备的现代化管理。 

- **评估共同管理准备情况**：帮助了解启用共同管理所需执行的步骤。 此规则具有先决条件。 有关详细信息，请参阅[共同管理概述](/sccm/core/clients/manage/co-management-overview)。  

- **配置 Azure 服务以与 Configuration Manager 配合使用**：此规则可帮助将 Configuration Manager 安装到 Azure AD，从而使客户端可以使用 Azure AD 对站点进行身份验证。 有关详细信息，请参阅[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)。  

- **使设备加入混合 Azure Active Directory**：加入 Azure AD 的设备允许用户使用其域凭据登录，同时确保设备符合组织的安全性和符合性标准。 有关详细信息，请参阅 [Azure AD 混合标识设计注意事项](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)。  

- **将客户端升级到最新的 Windows 10 版本**：Windows 10 版本 1709 或更高版本对用户的计算体验进行了改进和现代化处理。 有关详细信息，请参阅[有关采用服务型 Windows 的关键文章](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service)。  


### <a name="collections"></a>集合

通过清理和重新配置集合来帮助简化管理的见解。

- **空集合**：列出环境中没有成员的集合。 有关详细信息，请参阅[如何管理集合](/sccm/core/clients/manage/collections/manage-collections)。  


### <a name="proactive-maintenance"></a>主动维护
<!--1352184-->从版本 1806 开始，此组中的规则突出了通过维护 Configuration Manager 对象避免的潜在配置问题。    

- **未被分配站点系统的边界组**：这些边界组未被分配站点系统，只能用于站点分配。 有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)。  

- **不包含任何成员的边界组**：如果这些边界组没有任何成员，则不适用于站点分配或内容查找。 有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)。  

- **未向客户端提供内容的分发点**：这些分发点在过去 30 天内未向客户端提供内容。 此数据基于来自其客户端的下载历史记录报告。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points)。  

- **启用 WSUS 清理**：验证是否已启用在软件更新点组件的属性上运行 WSUS 清理的选项。 此选项有助于提高 WSUS 性能。 有关详细信息，请参阅[软件更新维护](/sccm/sum/deploy-use/software-updates-maintenance)。  

- **未使用的启动映像**：未引用这些启动映像以用于 PXE 启动或任务序列。 有关详细信息，请参阅[管理启动映像](/sccm/osd/get-started/manage-boot-images)。  

- **未使用的配置项**：这些配置项不属于配置基线，并且存在已超过 30 天。 有关详细信息，请参阅[创建配置基线](/sccm/compliance/deploy-use/create-configuration-baselines)。  


### <a name="security"></a>安全
提高基础结构和设备安全性的见解。 

- **不受支持的反恶意软件客户端版本**：10% 以上的客户端所运行的 System Center Endpoint Protection 版本不受支持。 有关详细信息，请参阅 [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection)。  


### <a name="simplified-management"></a>简化管理

有助于简化对环境的日常管理的见解。 

- **非 CB 客户端版本**：列出其版本不是 Current Branch (CB) 内部版本的所有客户端。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients)。  


### <a name="software-center"></a>软件中心

关于管理软件中心的见解。 

- **将用户定向到软件中心而不是应用程序目录**：检查用户是否在过去 14 天内从应用程序目录安装或请求了应用程序。 应用程序目录的主要功能现在包含在软件中心内。 版本 1806 中停止了对应用程序目录网站的支持。 有关详细信息，请参阅[已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features)。  

- **使用新版软件中心**：不再支持以前的软件中心版本。 通过在“计算机代理”组中启用客户端设置“使用新的软件中心”，将客户端设置为使用新的软件中心。 有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#use-new-software-center)。  


### <a name="windows-10"></a>Windows 10

与 Windows 10 的部署和服务相关的见解。 当超过一半的客户端运行 Windows 7、Windows 8 或 Windows 8.1 时，才可以使用 Windows 10 管理见解组。

- **配置 Windows 遥测和商业 ID 键**：若要使用“升级就绪情况”中的数据，请使用商业 ID 键配置设备并启用遥测。 将 Windows 10 设备设置为“增强型(有限)”或更高遥测级别。 有关详细信息，请参阅[将客户端配置为向 Windows Analytics 报告数据](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics)。  

- **将 Configuration Manager 连接至升级就绪情况**：在 Windows 7 不再受支持之前，利用升级就绪情况加快 Windows 10 部署。 有关详细信息，请参阅 [集成升级就绪情况](/sccm/core/clients/manage/upgrade/upgrade-analytics)。   

#### <a name="windows-10-management-insights-rules"></a>Windows 10 管理见解规则
![管理见解 - 适用于 Windows 10 的规则](./media/Windows-10-insights-group.png)
