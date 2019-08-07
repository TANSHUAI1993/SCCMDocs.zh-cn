---
title: 规划软件中心
titleSuffix: Configuration Manager
description: 确定你希望为用户配置软件中心和打造软件中心品牌并实现与 Configuration Manager 交互的方式。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2384fb0584fde331cf8667822c81de51eb60cbf0
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68534963"
---
# <a name="plan-for-software-center"></a>规划软件中心

*适用范围：System Center Configuration Manager (Current Branch)*

用户从软件中心更改设置、浏览和安装应用程序。 在 Windows 设备上安装 Configuration Manager 客户端时，它还会自动安装软件中心。

有关软件中心其他功能的详细信息，请参阅[软件中心用户指南](/sccm/core/understand/software-center)。  

## <a name="bkmk_userex"></a> 配置软件中心  

将 Configuration Manager 站点和客户端更新到版本1906或更高版本, 以从最新的改进中受益。

查看下列对软件中心的改进：

> [!Important]  
> 对软件中心和管理点的这些迭代改进将停用应用程序目录角色。
>
> - 从当前分支版本 1806 开始，不支持 Silverlight 用户体验。
> - 从1906版开始, 更新后的客户端自动将管理点用于用户可用的应用程序部署。 还不能安装新的应用程序目录角色。
> - 在 2019 年 10 月 31 日之后的第一个当前分支版本中，应用程序目录角色不再受支持。  

### <a name="starting-in-version-1802"></a>自版本 1802 开始

- 在“计算机代理”  组中默认启用客户端设置“使用新的软件中心”  。 不再支持以前版本的软件中心。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。  

- 用户可以浏览用户可用的应用程序并在加入 Azure Active Directory (Azure AD) 的设备上安装。 有关详细信息，请参阅[在加入 Azure AD 的设备上部署用户可用的应用程序](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)。  

### <a name="starting-in-version-1806"></a>自版本 1806 开始

- 在软件中心的“安装状态”  选项卡上指定应用程序目录网站链接的可见性。 有关详细信息，请参阅[软件中心](/sccm/core/clients/deploy/about-client-settings#software-center)客户端设置。  

- 不再需要应用程序目录角色，即可在软件中心显示用户可用的应用程序。 此项更改有助于减少向用户交付应用程序所需的服务器基础结构。 软件中心现在依靠管理点来获取此信息，通过将更大的环境分配给[边界组](/sccm/core/servers/deploy/configure/boundary-groups#management-points)来帮助它们更好地扩展。<!--1358309-->  

    > [!Note]  
    > 如果当前正在使用应用程序目录，并将 Configuration Manager 更新到版本 1806，它将继续工作。 不再需要  应用程序目录站点和 Web 服务点角色，但依然受支持  。 应用程序目录网站点  的 Silverlight 用户体验  不再受支持。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。
    >
    > 开始计划日后从基础结构中删除应用程序目录角色。 充分利用软件中心改进以使用管理点，并简化 Configuration Manager 环境。  

### <a name="starting-in-version-1902"></a>从版本 1902 开始

- 配置用户设备相关性。 有关详细信息，请参阅[将用户和设备与用户设备相关性进行链接](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)。

### <a name="starting-in-version-1906"></a>从版本 1906 开始

- 软件中心现在可以与面向用户公开发布的应用的管理点通信。 它不再使用应用程序目录。 借助此变化，可以更轻松地从站点中删除应用程序目录。

- 过去，软件中心选择可用服务器列表中的第一个管理点。 自此版本起，它与客户端使用同一个管理点。 借助此变化，软件中心可以与客户端使用分配的主站点中的同一个管理点。

- 管理点具有软件中心端点以支持这些新功能。 它现在每五分钟检查一次这些终结点的运行状况。 管理点通过 SMS_MP_CONTROL_MANAGER 站点组件的状态消息报告问题。

- 不能将新的应用程序目录角色添加到站点。 现有角色将继续工作。 只有现有的客户端将应用程序目录用于用户可用的部署。 更新的客户端自动将管理点用于所有部署。

- 最多可以向软件中心添加5个自定义选项卡。 有关详细信息，请参阅[软件中心客户端设置](/sccm/core/clients/deploy/about-client-settings#software-center)。 <!--4063773-->

### <a name="summary-of-infrastructure-requirements-per-version"></a>每个版本的基础结构要求摘要

使用下表来帮助了解软件中心的要求，具体取决于特定版本的 Configuration Manager：

| 设备类型 | 站点版本 | 基础结构 |
|-----------------|--------------|----------------|
| 加入了 Azure AD 的设备<br>（或者“已加入域的云”） | 1802 或 1806 | 所有应用程序部署的管理点 |
| Internet 上[已加入混合 Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) 的设备 | 1802 或 1806 | 云管理网关和所有应用程序部署的管理点 |
| 本地 Active Directory 加入域的设备 | 1802 | 软件中心中用户可用的应用所需的应用程序目录 |
| 本地 Active Directory 加入域的设备 | 1806 | 所有应用程序部署的管理点 |

> [!Important]  
> 若要利用新的 Configuration Manager 功能，请先将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。


## <a name="bkmk_impact"></a> 使用对话框窗口替换 toast 通知

<!--3555947-->
有时用户看不到有关重启或必需的部署的 Windows toast 通知。 然后，他们也看不到推迟提醒体验。 当客户端临近截止时间时，此行为可能导致不佳的用户体验。

从版本 1902 开始，在[要求进行软件更改](#software-changes-are-required)或部署[需要重新启动](#restart-required)时，可以选择使用侵入性更强的对话框窗口。

### <a name="software-changes-are-required"></a>需要更改软件

如果要在将来的截止时间内根据需要[部署应用程序](/sccm/apps/deploy-use/deploy-applications)，请在“部署软件向导”的“用户体验”  页上选择以下用户通知选项：

- **在软件中心中显示并显示所有通知**
- **需要更改软件时，向用户显示一个对话框窗口而不是 toast 通知**

配置此部署设置将更改此方案的用户体验。

在以下 toast 通知中：

![需要软件更改的 Toast 通知](media/3555947-required-toast.png)  

对于以下对话框窗口：

![需要更改软件的对话框窗口](media/3555947-required-dialog.png)


### <a name="restart-required"></a>需要重启

在客户端设置的[计算机重启](/sccm/core/clients/deploy/about-client-settings#computer-restart)组中，启用以下选项：**当部署要求重启时，向用户显示一个对话框窗口而不是 toast 通知**。  

配置此客户端设置可更改需要重新启动以下类型的所有必需部署的用户体验：

- [应用程序](/sccm/apps/deploy-use/deploy-applications)
- [任务序列](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)
- [软件更新](/sccm/sum/deploy-use/deploy-software-updates)

在以下 toast 通知中：

![需要重启的 Toast 通知](media/3555947-restart-toast.png)  

对于以下对话框窗口：

![重启计算机的对话框窗口](media/3555947-restart-dialog.png)


## <a name="branding-software-center"></a>打造软件中心品牌

更改软件中心的外观，以满足组织构建品牌的要求。 此配置可帮助用户信任软件中心。

### <a name="configure-software-center-branding"></a>配置软件中心品牌

<!-- 1351224 -->
通过添加组织的品牌元素并指定选项卡的可见性来自定义软件中心的外观。

有关详细信息，请参阅下列文章：

- 客户端设置的[软件中心](/sccm/core/clients/deploy/about-client-settings#software-center)组  
- [如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)  

### <a name="branding-priorities"></a>品牌优先级

Configuration Manager 根据以下属性应用自定义软件中心品牌：  

1. 软件中心  客户端设置。 有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#software-center)。  

2. “计算机代理”  组中的“组织名称”  客户端设置。 有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#computer-agent)。  

#### <a name="application-catalog-branding-priorities"></a>应用程序目录品牌优先级

> [!Important]
> 当前分支版本1806不支持应用程序目录的 Silverlight 用户体验。 从1906版开始, 更新后的客户端自动将管理点用于用户可用的应用程序部署。 还不能安装新的应用程序目录角色。 在 2019 年 10 月 31 日之后的第一个当前分支版本中，应用程序目录角色不再受支持。  

如果你使用的是应用程序目录, 则商标遵循以下优先级:  

1. 软件中心  客户端设置。 有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#software-center)。  

2. 如果将 Microsoft Intune 订阅连接到 Configuration Manager，则软件中心将显示 Intune 订阅属性中指定的组织名称  、颜色  和公司徽标  。 有关详细信息，请参阅 [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription)。  

    > [!Important]
    > 混合移动设备管理是[已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。

3. 在应用程序目录网站点属性中指定的组织名称  和颜色  。 有关详细信息，请参阅[应用程序目录网站点的配置选项](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website)。  

4. “计算机代理”  组中的“组织名称”  客户端设置。 有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#computer-agent)。  


## <a name="see-also"></a>另请参阅

- [软件中心用户指导](/sccm/core/understand/software-center)
- [规划和配置应用程序管理](/sccm/apps/plan-design/plan-for-and-configure-application-management)
