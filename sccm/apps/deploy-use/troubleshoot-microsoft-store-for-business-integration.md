---
title: MSfB 集成故障排除
titleSuffix: Configuration Manager
description: 提供建议和解决方法，以解决 Microsoft Store 业务集成的一些最常见问题。
ms.date: 08/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5c77e743e34cd731dec5803e0e5c1a23064f62e
ms.sourcegitcommit: b28a97e22a9a56c5ce3367c750ea2bb4d50449c3
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70243752"
---
# <a name="troubleshoot-the-microsoft-store-for-business-integration-with-configuration-manager"></a>排查 Microsoft Store 与 Configuration Manager 进行业务集成

本文提供了一些重要的故障排除提示和修补程序，以解决你可能遇到的一些与 Configuration Manager Microsoft Store for Business （MSfB）集成的常见问题。

若要详细了解如何将 Microsoft Store 用于业务 Configuration Manager，请参阅使用[Configuration Manager 管理 Microsoft Store For business 中的应用](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)。

## <a name="monitor"></a>监视器

### <a name="component-status"></a>组件状态

在 Configuration Manager 控制台中，转到“监视”工作区，展开“系统状态”，然后选择“组件状态”节点    。 监视以下组件的状态：

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>同步状态

在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“适用于企业的 Microsoft Store”节点    。 选中 "**上次同步状态**" 列。

### <a name="view-synchronized-apps"></a>查看同步的应用

在 Configuration Manager 控制台中，转到“软件库”工作区中，展开“应用程序管理”，然后选择“应用商店应用的许可证信息”节点    。


## <a name="log-files"></a>日志文件

### <a name="msfbsyncworkerlog"></a>MSfBSyncWorker

此日志文件位于服务连接点上的 "Configuration Manager 安装`\Logs`目录" 下。 它记录有关与云服务通信的信息。 此信息包括元数据、图标、包和许可证文件检索。

若要更改日志级别，请在`LoggingLevel` `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION`注册表项`0`中将值更改为。 有关详细信息，请参阅[配置日志记录选项](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-site)。

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION

此日志文件位于服务连接点上的 "Configuration Manager 安装`\Logs`目录" 下。 如果 MSfBSyncWorker 服务未启动，或者重复启动和停止，请查看此日志文件中的条目。

> [!NOTE]
> 此日志文件与其他功能共享。

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker

此日志文件位于层次结构中顶层站点的站点服务器上。 它位于 Configuration Manager `\Logs`安装目录下。 它记录有关以下过程的信息：

- 将 BusinessAppProcessWorker 组件同步的元数据信息插入到数据库中
- 处理文件`\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER

此日志文件位于层次结构中顶层站点的站点服务器上。 它位于 Configuration Manager `\Logs`安装目录下。 如果 BusinessAppProcessWorker 服务未启动，或者重复启动和停止，请查看此日志文件中的条目。



## <a name="last-sync-failed"></a>上次同步失败

当上次同步状态为 "*失败*" 时，请首先查看以下[日志文件](#log-files)来确定症状：

- MSfBSyncWorker
- SMS_CLOUDCONNECTION

然后，查看以下部分中的常见问题：

- [授权错误](#bkmk_fail-symptom1)
- [密钥无效](#bkmk_fail-symptom2)
- [获取应用程序令牌时出错](#bkmk_fail-symptom3)
- [内容位置不存在](#bkmk_fail-symptom4)
- [发出 http 请求调用 "GET" 方法时出错](#bkmk_fail-symptom5)
- [无法将更多字节写入缓冲区](#bkmk_fail-symptom6)

### <a name="bkmk_fail-symptom1"></a> 授权错误

#### <a name="cause"></a>原因

如果配置的 Azure Active Directory （Azure AD）应用程序无权管理此租户的 Microsoft Store for Business，则会出现此问题。

#### <a name="workaround"></a>解决方法

1. 打开 "[业务门户 Microsoft Store](https://www.microsoft.com/business-store)，并以管理员身份登录。
1. 请参阅 "**设置**"，然后选择 "**管理工具**"。
1. 如果未列出该应用程序，请选择 "**添加管理工具**"。 然后按名称搜索，并选择与 Configuration Manager 中的相同 ClientID 关联的 Azure AD 应用程序。
1. 如果状态不是 "**活动**"，请选择 "**操作**" 部分中的 "**激活**"。
1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“适用于企业的 Microsoft Store”节点    。 与应用商店同步，或等待下一个同步间隔发生。

> [!Tip]
> 若要在 Configuration Manager 中查找 ClientID：
>
> 1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure Active Directory 租户”节点    。
> 1. 选择用于业务集成的 Microsoft Store 租户。
> 1. 在结果窗格中，找到匹配的应用程序，然后查看 "**客户端 ID** " 列。

### <a name="bkmk_fail-symptom2"></a>密钥无效

#### <a name="cause"></a>原因

如果 Microsoft Store for Business 配置的 Azure AD 应用上的密钥已过期，则可能出现此问题。

#### <a name="resolution"></a>解决方法

续订 Azure AD 应用程序的密钥。 有关详细信息，请参阅[续订密钥](/sccm/core/servers/deploy/configure/azure-services-wizard#bkmk_renew)。

### <a name="bkmk_fail-symptom3"></a>获取应用程序令牌时出错

#### <a name="cause"></a>原因

如果已连接的应用在 Azure AD 中不再存在，则会出现此问题。

#### <a name="resolution"></a>解决方法

删除并重新创建与企业 Microsoft Store 的连接。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“适用于企业的 Microsoft Store”节点    。
1. 选择现有连接。
1. 在功能区中选择 "**删除**"。

然后重新创建连接。 有关详细信息，请参阅下列文章：

- [配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)
- [设置适用于企业的 Microsoft Store 同步](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#bkmk_setup)

### <a name="bkmk_fail-symptom4"></a>内容位置不存在

#### <a name="cause"></a>原因

设置业务连接 Microsoft Store 时，请指定用于存储已同步内容的网络共享。 如果此共享不存在或权限不正确，则可能出现此问题。

若要查看配置的位置：

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“适用于企业的 Microsoft Store”节点    。

1. 选择帐户并打开其**属性**。

1. 切换到 " **配置** " 选项卡。" **位置** " 设置显示用于存储从企业 Microsoft Store 下载的应用程序内容的网络路径。

#### <a name="workaround"></a>解决方法

1. 如果它尚不存在，请创建共享。

1. 检查文件夹的 NTFS 权限以及网络共享上的权限。 授予服务连接点的计算机帐户的**读取**和**写入**权限。

如果要重新配置位置，请删除并重新创建与新内容位置的连接。

### <a name="bkmk_fail-symptom5"></a>发出 http 请求调用 "GET" 方法时出错

#### <a name="cause"></a>原因

如果从应用商店中的应用程序的同步所用的时间太长，则表明内容 URL 已过期。

#### <a name="workaround"></a>解决方法

重试同步过程

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“适用于企业的 Microsoft Store”节点    。
1. 选择连接。 在功能区中，选择 "**从 Business Microsoft Store 同步**"。

每次都应该继续。 可能需要多次重试，具体取决于以下因素：

- 脱机应用程序的数量
- 包的大小
- 网络速度

尝试每次后，你应该会看到错误更少。 如果错误数不减少，则会出现另一个问题。

### <a name="bkmk_fail-symptom6"></a>无法将更多字节写入缓冲区

#### <a name="cause"></a>原因

如果应用程序的包大于 500 MB，则会出现此问题。 Configuration Manager 仅支持自动同步包小于 500 MB 的脱机应用程序。

#### <a name="workaround"></a>解决方法

你无法自动同步这些应用，但你可以下载内容并手动创建应用程序：

1. 从**MSfBSynWorker**中的以下行获取发生故障的应用程序 ID：

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. 请中转到[Microsoft Store For Business portal](https://www.microsoft.com/business-store)，并以存储管理员身份登录。 查找此应用程序的页面。

    > [!Tip]
    > 页面的 URL 类似于：`https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. 如果尚未选中，请选择 "**脱机**"。 然后选择 "**管理**"。

    1. 对于所有受支持的平台，请在应用程序内容共享上创建一个单独的文件夹。

    1. 将包下载到包文件夹中。

    1. 将编码的许可证文件作为`.bin`文件下载到包文件夹中。

    1. 将所有必需的框架下载到包文件夹中。

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”节点    。

1. [创建应用程序](/sccm/apps/deploy-use/create-applications)，手动指定应用程序信息。

    1. 为之前下载的每个受支持平台创建部署类型。

    1. 类型：Windows 应用包 (\*.appx, \*.appxbundle) 

    1. 为实际应用包指定 appx/.appxbundle，而不是所需的依赖项包。

在最后的 "**导入信息**" 页上确认以下详细信息：

- **许可证文件：** `.bin`指定文件。 脱机应用需要此许可证文件。
- **Windows 应用程序依赖关系：** 验证是否为此包下载了所有必需的依赖项。


## <a name="sync-doesnt-run"></a>同步不运行

本部分介绍以下同步问题：

- 手动启动同步过程，但它不会运行
- 网站不会每天自动同步

首先查看以下[日志文件](#log-files)，以确定症状：

- BusinessAppProcessWorker
- SMS_BUSINESS_APP_PROCESS_MANAGER
- MSfBSyncWorker
- SMS_CLOUDCONNECTION

然后，查看以下部分中的常见问题：

- [手动同步未启动](#bkmk_sync-symptom1)
- [自动每日同步不会运行，并在 SMS_BUSINESS_APP_PROCESS_MANAGER 中 "关闭 # 辅助角色" 错误](#bkmk_sync-symptom2)

### <a name="bkmk_sync-symptom1"></a>手动同步未启动

#### <a name="cause"></a>原因

如果在上一次同步后的同步时间小于10分钟，则可能出现此问题。你不能比每10分钟更频繁地同步。

#### <a name="resolution"></a>解决方法

等待至少10分钟，然后再开始另一次同步。

### <a name="bkmk_sync-symptom2"></a>自动每日同步不会运行，并在 SMS_BUSINESS_APP_PROCESS_MANAGER 中 "关闭 # 辅助角色" 错误

#### <a name="cause"></a>原因

如果 SMS_BUSINESS_APP_PROCESS_MANAGER 组件停止了 MSfBSyncWorker 线程，则会出现此问题。 错误可以指定`2`或`4`工作线程。

#### <a name="workaround"></a>解决方法

重新启动**SMS_EXECUTIVE**服务。

如果无法重新启动该主服务，请将这两个组件与 MSfB worker 一起停止，并同时启动这两个组件：

1. 在运行服务连接点的服务器上打开 Windows 注册表

1. 转到 `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. 将请求的操作设置为**停止**。

    1. 刷新以确认当前状态 = "**已停止**"。

1. 转到 `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. 将请求的操作设置为**停止**。

    1. 刷新以确认当前状态 = "**已停止**"。

1. 在**SMS_CLOUDCONNECTION**中，将 "请求的操作" 设置为 "**启动**"。

1. 在**SMS_BUSINESS_APP_PROCESS_MANAGER**中，将 "请求的操作" 设置为 "**启动**"。


## <a name="language-related-issues"></a>与语言相关的问题

本部分包括以下常见问题：

- [未应用语言选择更改](#bkmk_lang-symptom1)
- [并非所有所选语言都适用于所有许可证信息](#bkmk_lang-symptom2)

### <a name="bkmk_lang-symptom1"></a>未应用语言选择更改

#### <a name="cause"></a>原因

如果缓存语言选择，则可能出现此问题，并且在属性值更改后并不清除。

#### <a name="workaround"></a>解决方法

若要解决此问题，请重新启动**SMS_Executive**服务。

### <a name="bkmk_lang-symptom2"></a>并非所有所选语言都适用于所有许可证信息

#### <a name="cause"></a>原因

如果业务应用程序的许可证信息 Microsoft Store 不包含指定语言的本地化数据，则可能出现此问题。

#### <a name="workaround"></a>解决方法

对于创建的应用程序，手动添加缺少的任何语言。


## <a name="offline-applications"></a>脱机应用程序

本部分包括以下常见问题：

- [由于无法验证内容，因此无法创建脱机应用程序](#bkmk_off-symptom1)
- [无法安装通过脱机许可证信息创建的应用程序](#bkmk_off-symptom2)

### <a name="bkmk_off-symptom1"></a>由于无法验证内容，因此无法创建脱机应用程序

#### <a name="cause"></a>原因

如果脱机应用程序的同步内容损坏或修改，则可能出现此问题。

#### <a name="workaround"></a>解决方法

启动新的同步。同步完成后，应验证并下载任何错误的内容文件。

### <a name="bkmk_off-symptom2"></a>无法安装通过脱机许可证信息创建的应用程序

#### <a name="cause"></a>原因

如果将应用程序部署到运行早于版本1511的 Windows 10 版本的客户端，则会发生此问题。 仅在 Windows 10 版本1511及更高版本上支持从适用于企业的 Microsoft Store 脱机许可的应用。

#### <a name="resolution"></a>解决方法

安装最新版的 Windows 10。


## <a name="next-steps"></a>后续步骤

若要查找更多帮助，请参阅[查找有关使用 Configuration Manager 的帮助](/sccm/core/understand/find-help)。

<!-- these videos are old...1604/1605, is there still benefit in linking to them?
- Here are also some videos to learn more about it:

  - [How to set up the required prerequisites in AAD and the Microsoft Store for Business portal](https://www.youtube.com/watch?v=fC1AQY42flQ)
  - [Choose languages to sync and create apps from app metadata for each Microsoft Store for Business, and how to create apps from app metadata](https://www.youtube.com/watch?v=VJs-475rfaI)
 -->