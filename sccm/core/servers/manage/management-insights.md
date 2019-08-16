---
title: 管理见解
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 控制台中提供的管理见解功能。
ms.date: 08/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed1c182aabcfbd9ec974a380c379304d7eef63e9
ms.sourcegitcommit: 9c29ee22d3af5ab2bf8d51262c11d5a756dc55c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68913758"
---
# <a name="management-insights-in-configuration-manager"></a>Configuration Manager 中的管理见解

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager 中的管理见解功能提供了环境当前状态的相关信息。 该信息基于对站点数据库中数据的分析。 见解有助于更好地了解环境，并根据见解执行操作。 此功能在 Configuration Manager 1802 版中发布。 <!--1353967-->


## <a name="review-management-insights"></a>查看管理见解

若要查看规则，帐户需要站点对象的读取权限   。

1. 请打开 Configuration Manager 控制台。  

2. 转到“管理”工作区，展开“管理见解”，然后选择“所有见解”    。  

    > [!Note]  
    > 从版本 1810 开始，当选择“管理见解”节点时，它会显示为[管理见解仪表板](#bkmk_insights)  。  

3. 打开要查看的管理见解组名称。 在功能区中选择“显示见解”  。  

以下四个选项卡可供查看：

- **所有规则**：提供选定管理见解组的完整规则列表。  

- **已完成**：列出无需执行任何操作的规则。  

- **正在进行**：显示已完成部分（但非全部）先决条件的规则。  

- **需要执行操作**：列出需要执行操作的规则。 选择“更多详细信息”，检索需要执行操作的特定项目  。  

“先决条件”窗格列出了运行规则所需的项目  。

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>云服务组的所有规则和先决条件

![管理见解 - 云服务组的所有规则和先决条件](./media/Management-insights-all-cloud-rules.png)

选择规则并选择“更多详细信息”，查看规则详细信息  。


## <a name="operations"></a>操作

管理见解规则每周重新评估一次适用性。 若要按需重新评估规则，请右键单击该规则并选择“重新评估”  。

管理见解规则的日志文件是站点服务器上的 SMS_DataEngine.log  。

<!--1357930-->
自版本 1806 起，一些规则允许你执行操作。 选择规则，选择“更多详细信息”，然后选择“执行操作”（如果可用）   。

根据规则，此操作会出现以下某一行为：  

- 在控制台中自动导航到可以采取进一步操作的节点。 例如，如果管理见解建议更改客户端设置，执行操作将导航到“客户端设置”节点。 然后通过修改默认或自定义客户端设置对象采取进一步操作。  

- 基于查询导航到筛选的视图。 例如，对空集合规则执行操作只会在集合列表中显示这些集合。 然后采取进一步操作，例如删除集合或修改其成员身份规则。  


## <a name="bkmk_insights"></a> 管理见解仪表板

<!--1357979-->

从版本 1810 开始，“管理见解”节点包括一个图形仪表板  。 此仪表板可概要显示规则状态，让你能够更轻松地显示进度。

使用仪表板顶部的以下筛选器可以细化视图：

- 显示已完成的工作
- 可选
- 建议
- 严重

该仪表板具有以下磁贴：  

- **管理见解索引**：跟踪管理见解规则的总体进度。 该索引为加权平均值。 关键规则最为重要。 此索引为可选规则提供的加权最低。  

- **管理见解组**：显示每个组中的规则百分比，支持筛选器。 选择一个组以深入查看此组中的特定规则。  

- **管理见解优先级**：按优先级显示规则百分比，支持筛选器。  

- **所有见解**：一个包括优先级和状态的见解表。 使用表顶部的“筛选器”字段匹配任何可用列中的字符串  。 仪表板按以下顺序对表进行排序：

    - 状态：需要执行操作、已完成、未知  
    - 优先级：重要、建议、可选  
    - 上次更改时间：较早的日期排在前面  

![管理见解仪表板的屏幕截图](media/1357979-management-insights-dashboard.png)


## <a name="groups-and-rules"></a>组和规则

规则分为以下管理见解组：

- [应用程序](#applications)  
- [云服务](#cloud-services)  
- [集合](#collections)  
- [主动维护](#proactive-maintenance)  
- [安全](#security)  
- [简化管理](#simplified-management)  
- [软件中心](#software-center)  
- [Windows 10](#windows-10)  

### <a name="applications"></a>应用程序

应用程序管理见解。

- **不具有部署的应用程序**：列出环境中没有活动部署的应用。 此规则有助于查找并删除未使用的应用程序，以简化显示在控制台中的应用程序列表。 有关详细信息，请参阅[部署应用程序](/sccm/apps/deploy-use/deploy-applications)。  

### <a name="cloud-services"></a>云服务

帮助与多种云服务集成，实现设备的现代化管理。

- **评估共同管理准备情况**：有助于了解启用共同管理所需执行的步骤。 此规则具有先决条件。 有关详细信息，请参阅[共同管理概述](/sccm/comanage/overview)。  

- **配置 Azure 服务以用于 Configuration Manager**：此规则有助于将 Configuration Manager 载入 Azure AD，以便客户端能够使用 Azure AD 向站点进行身份验证。 有关详细信息，请参阅[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)。  

- **将设备启用为加入混合 Azure Active Directory**：使用加入 Azure AD 的设备，用户可使用自己的域凭据登录，同时确保设备符合组织的安全性和符合性标准。 有关详细信息，请参阅 [Azure AD 混合标识设计注意事项](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)。  

- **将客户端升级到最新版 Windows 10**：Windows 10 版本 1709 或更高版本改进和新式化用户计算体验。 有关详细信息，请参阅[有关采用服务型 Windows 的关键文章](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service)。  

### <a name="collections"></a>集合

通过清理和重新配置集合来帮助简化管理的见解。

- **空集合**：列出环境中没有成员的集合。 有关详细信息，请参阅[如何管理集合](/sccm/core/clients/manage/collections/manage-collections)。  

从 1902 版开始，包含对管理集合的新规则和建议。<!--3555752--> 利用这些见解来简化管理并提高性能：

- **不包含查询规则和直接成员的集合**：若要简化层次结构中的集合列表，请将其删除。  

- **重新评估开始时间相同的集合**：这些集合与其他集合的重新评估时间相同。 修改重新评估时间，使它们不冲突。  

- **查询时间超过 2 秒的集合**：查看此集合的查询规则。 请考虑修改或删除该集合。

- 以下规则包括可能导致站点上的不必要负载的配置。 查看这些集合，然后将其删除，或禁用规则评估：  

    - **没有查询规则且已启用增量更新的集合**  

    - **没有查询规则且已启用计划或增量评估的集合**  

    - **没有查询规则且选定计划完整评估的集合**  


### <a name="proactive-maintenance"></a>主动维护

<!--1352184-->
自版本 1806 起，此组中的规则突出显示潜在的配置问题，以通过定期维护 Configuration Manager 对象避免这些问题。

- **未分配有站点系统的边界组**：未分配有站点系统的边界组只能用于站点分配。 有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)。  

- **没有成员的边界组**：没有任何成员的边界组不适用于站点分配或内容查找。 有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)。  

- **未向客户端提供内容的分发点**：在过去 30 天内，分发点未向客户端提供内容。 此数据基于来自其客户端的下载历史记录报告。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points)。  

- **启用 WSUS 清理**：验证是否已启用对软件更新点组件的属性运行 WSUS 清理的选项。 此选项有助于提高 WSUS 性能。 有关详细信息，请参阅[软件更新维护](/sccm/sum/deploy-use/software-updates-maintenance)。  

- **未用启动映像**：未引用启动映像来用于 PXE 启动或任务序列。 有关详细信息，请参阅[管理启动映像](/sccm/osd/get-started/manage-boot-images)。  

- **未用配置项目**：配置项目不属于配置基线，且已存在超过 30 天。 有关详细信息，请参阅[创建配置基线](/sccm/compliance/deploy-use/create-configuration-baselines)。  

- **将对等缓存源升级到最新版 Configuration Manager 客户端**：确定用作对等缓存源，但尚未从先前的 1806 客户端版本升级的客户端。 先前的 1806 客户端不能用作运行版本 1806 或更高版本的客户端的对等缓存源。 选择“采取措施”  打开显示客户端列表的设备视图。<!--1358008-->  

### <a name="security"></a>安全

提高基础结构和设备安全性的见解。

- **已启用 NTLM 回退**：<!--4572953--> 从版本 1906 开始，此规则检测是否为站点启用了安全级别较低的 NTLM 身份验证回退方法。 当使用客户端推送方法安装 Configuration Manager 客户端时，站点可以要求进行 Kerberos 相互身份验证。 此增强有助于保护服务器与客户端之间的通信。 有关详细信息，请参阅[如何使用客户端请求安装客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)。

- **不受支持的反恶意软件客户端版本**：超过 10% 的客户端运行的 System Center Endpoint Protection 版本不受支持。 有关详细信息，请参阅 [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection)。  

### <a name="simplified-management"></a>简化管理

有助于简化对环境的日常管理的见解。

- **将站点连接到用于 Configuration Manager 更新的 Microsoft 云**：此规则可确保 Configuration Manager 服务连接点在过去七天内已连接到 Microsoft 云。 此连接用于下载定期更新内容。 查看 DMPDownloader.log 和 hman.log。 有关详细信息，请参阅 [Internet 访问要求](/sccm/core/plan-design/network/internet-endpoints#bkmk_scp-updates)。

- **非 CB 客户端版本**：列出版本不是 Current Branch (CB) 内部版本的所有客户端。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients)。  

- **将客户端更新到支持的 Windows 10 版本**：从 1902 版开始，此规则报告运行不再受支持的 Windows 10 版本的客户端。 它还包括具有服务即将结束（三个月）的 Windows 10 版本的客户端。<!--3897268-->  


### <a name="software-center"></a>软件中心

关于管理软件中心的见解。

- **将用户定向到软件中心，而不是应用目录**：检查用户是否在过去 14 天内从应用目录安装或请求获取应用。 应用程序目录的主要功能现在包含在软件中心内。 应用程序目录已遭弃用。 有关详细信息，请参阅[已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features)。  

- **使用新版软件中心**：不再支持以前版本的软件中心。 通过在“计算机代理”组中启用客户端设置“使用新的软件中心”，将客户端设置为使用新的软件中心   。 有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#use-new-software-center)。  

### <a name="software-updates"></a>软件更新

- **客户端设置未配置为允许客户端下载增量内容**：在环境中同步的某些软件更新包括增量内容。 启用客户端设置“在有可用内容时，允许客户端下载增量内容”  。 如果不启用此设置，则在部署这些更新，客户端将不必要地下载超出要求的内容。 有关详细信息，请参阅[客户端设置 - 软件更新](/sccm/core/clients/deploy/about-client-settings#software-updates)。

- **启用“Windows 10 版本 1903 及更高版本”的软件更新产品类别**：Windows 10 版本 1903 及更高版本有一个新的软件更新产品类别。 如果同步 Windows 10 更新且装有 Windows 10 版本 1903 或更高版本的客户端，请在软件更新点组件属性中选择“Windows 10 版本 1903 及更高版本”  产品类别。 有关详细信息，请参阅[配置要同步的分类和产品](/sccm/sum/get-started/configure-classifications-and-products)。

### <a name="windows-10"></a>Windows 10

与 Windows 10 的部署和服务相关的见解。 当超过一半的客户端运行 Windows 7、Windows 8 或 Windows 8.1 时，才可以使用 Windows 10 管理见解组。

- **配置 Windows 遥测和商业 ID 键**：若要使用“升级就绪情况”中的数据，请使用商业 ID 键配置设备并启用诊断数据收集。 将 Windows 10 设备设置为“增强型(有限)”或更高级别  。 有关详细信息，请参阅[将客户端配置为向 Windows Analytics 报告数据](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics)。  

- **将 Configuration Manager 连接到“升级就绪情况”** ：在 Windows 7 支持结束前，将“升级就绪情况”用于 Windows 10 部署。 有关详细信息，请参阅 [集成升级就绪情况](/sccm/core/clients/manage/upgrade/upgrade-analytics)。  

#### <a name="windows-10-management-insights-rules"></a>Windows 10 管理见解规则

![管理见解 - 适用于 Windows 10 的规则](./media/Windows-10-insights-group.png)
