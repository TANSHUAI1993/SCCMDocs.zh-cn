---
title: 发行说明
titleSuffix: Configuration Manager
description: 了解有关产品中尚未解决或 Microsoft 支持知识库文章中未涵盖的紧急问题。
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 858ba3b39ea2290e1d5ca39d9d804e3f46be3002
ms.sourcegitcommit: ef7800a294e5db5d751921c34f60296c1642fc1f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68712714"
---
# <a name="release-notes-for-configuration-manager"></a>Configuration Manager 发行说明

适用范围：  System Center Configuration Manager (Current Branch)

在 Configuration Manager 中，产品发布说明仅限于紧急问题。 产品中尚未解决这些紧急问题，Microsoft 支持知识库文章中也未对此进行详细介绍。  

特定于功能的文档包含有关影响核心方案的已知问题的信息。  

本文包含 Configuration Manager Current Branch 的发行说明。 有关技术预览分支的信息，请参阅[技术预览](/sccm/core/get-started/technical-preview)  

有关不同版本引入的新功能的信息，请参阅以下文章：

- [版本 1906 中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1906)  
- [版本 1902 中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1902)
- [1810 版中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [1806 版中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1806)  

> [!Tip]  
> 若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`


## <a name="set-up-and-upgrade"></a>设置和升级  

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>服务器 2019 上有关域功能级别的安装程序先决条件警告

<!-- 4904376 -->

*适用于版本 1906*

在具有运行 Windows Server 2019 的域控制器的环境中安装版本 1906 的更新时，域功能级别的先决条件检查将返回以下警告：

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

#### <a name="workaround"></a>解决方法

忽略此警告。

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>站点扩展后，Azure AD 用户发现和集合组同步不起作用

<!-- 4797313 -->
*适用于版本 1906*

配置以下任一功能后：

- Azure Active Directory 用户组发现
- 将集合成员身份结果同步到 Azure Active Directory 组

如果随后将独立主站点扩展为具有管理中心站点的层次结构，则会在 SMS_AZUREAD_DISCOVERY_AGENT.log 中显示以下错误：

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

#### <a name="workaround"></a>解决方法

续订与 Azure AD 中的应用注册相关联的密钥。 有关详细信息，请参阅[续订密钥](/sccm/core/servers/deploy/configure/azure-services-wizard#bkmk_renew)。


### <a name="setup-command-line-option-joinceip-must-be-specified"></a>必须指定安装程序命令行选项 JoinCEIP

<!--510806-->
适用范围：  Configuration Manager 版本 1802

从 Configuration Manager 版本 1802 开始，从产品中删除了客户体验改善计划 (CEIP) 功能。 从命令行或无人参与的脚本中[自动安装](/sccm/core/servers/deploy/install/command-line-options-for-setup)新站点时，安装程序返回指示缺失所需参数的错误。

#### <a name="workaround"></a>解决方法

虽然它对安装进程的结果没有影响，但请在安装程序命令行中包含 JoinCEIP 参数  。

> [!Note]  
> [控制台安装程序](/sccm/core/servers/deploy/install/install-consoles)的 EnableSQM 参数不是必需的。

### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>在被动模式下，站点服务器上的云服务管理器组件停止

<!--VSO 2858826, SCCMDocs issue 772-->
适用范围：  Configuration Manager 版本 1806

如果[服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)与[被动模式下的站点服务器](/sccm/core/servers/deploy/configure/site-server-high-availability)共存，则无法启动[云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)的部署和监视。 云服务管理器组件 (MS_CLOUD_SERVICES_MANAGER) 处于停止状态。

#### <a name="workaround"></a>解决方法

将服务连接点角色移至另一台服务器。


<!-- ## Backup and recovery  -->

<!--## Client deployment and upgrade-->


## <a name="os-deployment"></a>OS 部署

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>提升被动站点服务器之后，默认启动映像包在上一个活动服务器上仍有包源

<!--3453224, SCCMDocs-pr issue 3097-->
适用范围：  Configuration Manager 版本 1810

如果站点服务器处于被动模式（服务器 B），在将其提升为活动模式时，默认启动映像的内容位置将继续引用先前活动的服务器（服务器 A）。 如果服务器 A 出现硬件故障，则无法更新或更改默认启动映像。

#### <a name="workaround"></a>解决方法

无


## <a name="software-updates"></a>软件更新

### <a name="security-roles-are-missing-for-phased-deployments"></a>分阶段部署缺少安全角色

<!--3479337, SCCMDocs-pr issue 3095-->
适用范围：  Configuration Manager 版本 1810、1902

OS Deployment Manager  内置安全角色具有[分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)的权限。 以下角色缺少这些权限：  

- **应用程序管理员**  
- **应用程序部署管理员**  
- **软件更新管理员**  

“应用创建者”角色可能看起来对分阶段部署具有某些权限，但无法创建部署  。

具有这些角色的用户可以启动“创建分阶段部署”向导，并可以查看应用程序或软件更新的分阶段部署。 他们无法完成向导，也无法对现有部署进行任何更改。

#### <a name="workaround"></a>解决方法

创建自定义安全角色。 复制现有安全角色，并在“分阶段部署”对象类上添加以下权限  ：

- 创建  
- 删除  
- 修改  
- 读取  

有关详细信息，请参阅[创建自定义安全角色](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole)。

### <a name="changing-office-365-client-setting-doesnt-apply"></a>更改 Office 365 客户端设置不适用

<!--511551-->
适用范围：  Configuration Manager 版本 1802  

部署[客户端设置](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent)，其中将“启用 Office 365 客户端代理的管理”  配置为 `Yes`。 然后，将该设置更改为 `No` 或 `Not Configured`。 更新目标客户端上的策略后，Office 365 更新仍由 Configuration Manager 管理。

#### <a name="workaround"></a>解决方法

将以下注册表值更改为 `0` 并重启 **Microsoft Office 即点即用服务** (ClickToRunSvc)：

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```

## <a name="desktop-analytics"></a>桌面分析

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>如果将硬件清单用于分布式视图，则无法载入桌面分析

<!-- 4950335 -->
适用范围：*包含更新汇总的 Configuration Manager 版本 1902 和版本 1906*

如果你具有层次结构，并且在任何站点复制链接上启用[分布式视图](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews)的硬件清单  站点数据，则在 Configuration Manager 中配置桌面分析连接后，将在 M365UploadWorker.log 中显示以下错误：

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

#### <a name="workaround"></a>解决方法

在每个站点复制链接上禁用分布式视图的硬件清单站点数据  。


### <a name="console-unexpectedly-closes-when-removing-collections"></a>删除集合时控制台意外关闭

<!-- 4749443 -->
适用范围：*包含更新汇总的 Configuration Manager 版本 1902*

将网站连接到[桌面分析](/sccm/desktop-analytics/connect-configmgr)后，可以选择要与桌面分析同步的特定集合  。 如果删除集合并应用更改，则立即添加新集合会导致未处理的异常。 控制台意外关闭。

#### <a name="workaround"></a>解决方法

删除集合时，选择  “确定”可关闭“属性”窗口。 然后再次打开“属性”窗口，在  “桌面分析连接”选项卡中添加新集合。

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>试点状态图块显示某些设备为“未定义”

<!-- 4547783 -->
适用范围：*包含更新汇总的 Configuration Manager 版本 1902*

使用 Configuration Manager 控制台来监视试点部署状态时，在该部署计划的 Windows 目标版本上处于最新状态的试点设备在试点状态图块中显示为“未定义”  。  

对此部署计划而言，这些未定义的设备具有 OS 目标版本，处于最新状态   。 无需进一步操作。


## <a name="mobile-device-management"></a>移动设备管理  

### <a name="validation-for-ios-app-link-sometimes-fails-on-valid-link"></a>有效链接上的 iOS 应用链接验证有时会失败

适用范围：  Configuration Manager 版本 1810 及更低版本

<!-- LSI 106004348 -->
创建“应用商店中的 iOS 应用包”类型的新应用程序时，验证程序不接受该位置的某些有效 URL   。 具体而言，iOS App Store 不需要 URL 的应用名称部分的值。 例如，以下两个链接都有效并指向同一个应用，但“创建应用程序向导”仅接受第一个链接  ：

- `https://itunes.apple.com/us/app/app-name/id123456789?mt=8`
- `https://itunes.apple.com/us/app//id123456789?mt=8`

#### <a name="workaround"></a>解决方法

在创建一个 URL 中缺少应用名称的 iOS 应用时，请添加任意值，就好像它是 URL 的应用名称一样。 例如：

- `https://itunes.apple.com/us/app/any-string/id123456789?mt=8`

使用此操作可以完成向导。 该应用仍然成功部署到 iOS 设备。 添加到 URL 的字符串在向导的“常规信息”选项卡上显示为“名称”   。 它也是公司门户中应用的标签。




<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->

<!-- ## Endpoint Protection -->
