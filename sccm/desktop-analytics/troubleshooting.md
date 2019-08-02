---
title: 疑难解答桌面分析
titleSuffix: Configuration Manager
description: 有助于解决桌面分析问题的技术详细信息。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ecb1657903fd3d1dfe43f2ad46258b4643c2f55
ms.sourcegitcommit: ef7800a294e5db5d751921c34f60296c1642fc1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68712609"
---
# <a name="troubleshoot-desktop-analytics"></a>疑难解答桌面分析

使用本文中的详细信息来帮助解决与 Configuration Manager 集成的桌面分析问题。



## <a name="confirm-prerequisites"></a>确认先决条件

许多常见问题是由于缺少必备组件引起的。 首先确认以下配置:

- [先决条件](/sccm/desktop-analytics/overview#prerequisites)  

- [Windows 组件更新](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [如何启用数据共享](/sccm/desktop-analytics/enable-data-sharing), 其中包括以下主题:  

    - 客户端需要连接到的 Internet 终结点  

    - 代理服务器身份验证  

    - 诊断数据级别  



## <a name="monitor-connection-health"></a>监视器连接运行状况

使用 Configuration Manager 中的 "**连接运行状况**" 仪表板, 按设备运行状况向下钻取类别。 在 Configuration Manager 控制台中, 打开 "**软件库**" 工作区, 展开 " **Desktop Analytics 服务**" 节点, 然后选择 "**连接运行状况**" 仪表板。  

有关详细信息, 请参阅[监视连接运行状况](/sccm/desktop-analytics/monitor-connection-health)。


## <a name="log-files"></a>日志文件

有关详细信息, 请参阅[用于桌面分析的日志文件](/sccm/core/plan-design/hierarchy/log-files#desktop-analytics)

从 Configuration Manager 版本1906开始, 使用 Configuration Manager 安装目录中的**DesktopAnalyticsLogsCollector**工具来帮助解决桌面分析问题。 它运行一些基本的故障排除步骤, 并将相关日志收集到一个工作目录中。 有关详细信息, 请参阅[日志收集器](/sccm/desktop-analytics/log-collector)。

### <a name="enable-verbose-logging"></a>启用详细日志记录

1. 在服务连接点上, 请执行以下注册表项:`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. 将**logginglevel.information**值设置为`0`  


## <a name="bkmk_AzureADApps"></a>Azure AD 应用程序

桌面分析将以下应用程序添加到 Azure AD:

- **Configuration Manager 微服务**:通过桌面分析连接 Configuration Manager。 此应用没有访问要求。  

- **MALogAnalyticsReader**:检索在 Log Analytics 中创建的 OMS 组和设备。 有关详细信息, 请参阅[MALogAnalyticsReader 应用程序角色](#bkmk_MALogAnalyticsReader)。  

如果需要在完成安装后设置这些应用, 请在 "连接的服务" 窗格中转到 "**连接的服务**" 窗格。 选择 "**配置用户和应用访问**", 并预配应用。  

- **Configuration Manager Azure AD 应用**。 如果需要在完成设置后对连接问题进行预配或故障排除, 请参阅[创建并导入用于 Configuration Manager 的应用](#create-and-import-app-for-configuration-manager)。 此应用需要在**Configuration Manager 服务**API 上**写入 cm 收集数据**和**读取 cm 集合数据**。  


### <a name="create-and-import-app-for-configuration-manager"></a>为 Configuration Manager 创建并导入应用

如果无法从 "配置 Azure 服务向导" 创建用于 Configuration Manager 的 Azure AD 应用程序, 或者如果想要重复使用现有应用程序, 则需要手动创建并导入它。 完成桌面分析门户上的[初始载入](/sccm/desktop-analytics/set-up#initial-onboarding)后, 请执行以下步骤:

#### <a name="create-app-in-azure-ad"></a>在 Azure AD 中创建应用

1. 以具有*全局管理员*权限的用户身份打开[Azure 门户](https://portal.azure.com) **Azure Active Directory**, 并选择 "**应用注册**"。 然后选择 "**新建注册**"。  

2. 在 "**创建**" 面板中, 配置以下设置:  

    - **名称**: 标识应用的唯一名称, 例如:`Desktop-Analytics-Connection`  

    - **支持的帐户类型**:**仅限此组织目录中的帐户 (Contoso)**

    - **重定向 URI (可选)** :**Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    选择 "**注册**"。  

3. 选择应用, 记下**应用程序 (客户端) id**和**目录 (租户) id**。 这些值是用于配置 Configuration Manager 连接的 Guid。  

4. 在 "**管理**" 菜单中, 选择 "**证书 & 机密**"。 选择 "**新建客户端密码**"。 输入 "**说明**", 指定过期持续时间, 然后选择 "**添加**"。 复制用于配置 Configuration Manager 连接的密钥**值**。

    > [!Important]  
    > 这是复制密钥值的唯一机会。 如果现在不复制, 则需要创建另一个密钥。  
    >
    > 将密钥值保存在安全的位置。  

5. 在 "**管理**" 菜单中, 选择 " **API 权限**"。  

    1. 在 " **API 权限**" 面板中, 选择 "**添加权限**"。  

    2. 在 "**请求 API 权限**" 面板中, 切换到 **"我的组织使用的 api**"。  

    3. 搜索并选择**Configuration Manager 微服务**API。  

    4. 选择 "**应用程序权限**" 组。 展开 " **CmCollectionData**", 并选择以下两个权限:**写入 Cm 集合数据**并**读取 cm 集合数据**。  

    5. 选择 "**添加权限**"。  

6. 在 " **API 权限**" 面板中, 选择 "**授予管理员许可 ...** "。选择 **"是"** 。  


#### <a name="import-app-in-configuration-manager"></a>导入应用 Configuration Manager

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点。 在功能区中选择 "**配置 Azure 服务**"。  

2. 在 Azure 服务向导的 " **Azure 服务**" 页上, 配置以下设置:  

    - 指定 Configuration Manager 中的对象名称。  

    - 指定可选说明以帮助标识服务。  

    - 从可用服务列表中选择 "**桌面分析**"。  
  
   选择“下一步”。  

3. 在 "**应用**" 页上, 选择相应的**Azure 环境**。 然后选择 "**导入**web 应用"。 在 "**导入应用**" 窗口中配置以下设置:  

    - **Azure AD 租户名称**:此名称是它在中的命名方式 Configuration Manager  

    - **Azure AD 租户 ID**:从 Azure AD 复制的**目录 ID**  

    - **客户端 ID**：从 Azure AD 应用复制的**应用程序 ID**  

    - 密钥:从 Azure AD应用复制的键值  

    - **密钥到期日期**：密钥的到期日期  

    - **应用 ID URI**：此设置应自动填充以下值:`https://cmmicrosvc.manage.microsoft.com/`  
  
   选择 "**验证**", 然后选择 **"确定"** 以关闭 "导入应用" 窗口。 在 Azure 服务向导的 "应用" 页上选择 "**下一步**"。  

若要继续在 "**诊断数据**" 页上执行向导的其余部分, 请参阅[连接到服务](/sccm/desktop-analytics/connect-configmgr#bkmk_connect)。

#### <a name="troubleshoot-app-in-configuration-manager"></a>Configuration Manager 中的应用疑难解答

如果在创建或导入应用时遇到问题, 请首先检查**smsadminui.log**中是否有特定的错误。 然后检查以下配置:

- 已成功将租户注册到桌面分析服务。 有关详细信息, 请参阅[如何设置桌面分析](/sccm/desktop-analytics/set-up)。

- 所有必需的终结点都是可访问的。 有关详细信息, 请参阅[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)。

- 请确保登录的用户具有正确的权限。 有关详细信息，请参阅[先决条件](/sccm/desktop-analytics/overview#prerequisites)。

- 请确保用户可以一般登录到 Azure。 此操作确定是否存在一般的 Azure AD 身份验证问题。

- 检查有关*桌面分析工作线程*的**SMS_SERVICE_CONNECTOR**组件的状态消息。


### <a name="bkmk_MALogAnalyticsReader"></a>MALogAnalyticsReader 应用程序角色

设置桌面分析时, 表示你的组织同意。 此同意是为 MALogAnalyticsReader 应用程序分配工作区 Log Analytics 读取者角色。 桌面分析需要此应用程序角色。

如果在安装过程中此过程出现问题, 请使用以下过程手动添加此权限:

1. 中转到[Azure 门户](https://portal.azure.com), 并选择 "**所有资源**"。 选择 " **Log Analytics**" 类型的工作区。  

2. 在工作区菜单中, 选择 "**访问控制 (IAM)** ", 然后选择 "**添加**"。  

3. 在 "**添加权限**" 面板中, 配置以下设置:  

    - **角色**:**读取器**  

    - **将访问权限分配给**:**Azure AD 用户、组或应用程序**  

    - **选择**:**MALogAnalyticsReader**  

4. 选择**保存**。

门户会显示一条通知, 指出它添加了角色分配。


## <a name="data-latency"></a>数据延迟

<!-- 3846531 -->
首次设置桌面分析、注册新的客户端或配置新的部署计划时, Configuration Manager 和桌面分析门户中的报表可能不会立即显示完整的数据。 可能需要2-3 天才能执行以下步骤:

- 活动设备将诊断数据发送到桌面分析服务
- 该服务处理数据
- 服务与 Configuration Manager 站点同步

将 Configuration Manager 层次结构中的设备集合同步到桌面分析时, 这些集合可能需要一小时才能出现在桌面分析门户中。 同样, 在桌面分析中创建部署计划时, 与部署计划关联的新集合可能需要一小时才能出现在 Configuration Manager 层次结构中。 主站点创建集合, 管理中心站点与桌面分析同步。 评估和更新集合成员身份 Configuration Manager 可能需要长达24小时。 若要加快此过程, 请手动更新集合成员身份。<!-- 4984639 -->

> [!Note]
> 若要手动收集更新以反映所做的更改, SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker 组件首先需要同步。 运行此进程最多可能需要一小时。 有关详细信息, 请参阅**M365ADeploymentPlanWorker**。

在桌面分析门户中, 有两种类型的数据:**管理员数据**和**诊断数据**:

- **管理员数据**是指对工作区配置所做的任何更改。 例如, 当你更改资产的**升级决策**或**重要性**时, 将更改管理员数据。 这些更改通常具有复合效果, 因为它们可以更改设备的就绪状态, 其中包含已安装的相关资产。

- **诊断数据**是指从客户端设备上传到 Microsoft 的系统元数据。 此数据支持桌面分析。 它包括诸如设备清单之类的属性, 以及安全和功能更新状态。

默认情况下, 将每天自动刷新桌面分析门户中的所有数据。 此刷新包括诊断数据中的更改, 以及对配置所做的任何更改 (管理员数据)。 在您的桌面分析门户中, 它每天应显示 08:00 AM UTC。

更改管理员数据时, 可以触发工作区中管理员数据的按需刷新。 从桌面分析门户的任意页面, 打开 "数据货币" 飞出:

![桌面分析门户中 "数据货币飞出" 选项卡的屏幕截图](media/data-currency-flyout.png)

然后选择 "**应用更改**":

![桌面分析门户中的扩展数据货币飞出屏幕截图](media/data-currency-flyout-expand.png)

此过程通常在15-60 分钟内发生。 计时取决于工作区的大小以及需要处理的更改的范围。 请求按需刷新数据时, 不会更改诊断数据。  有关详细信息, 请参阅[桌面分析常见问题解答](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。

如果在上面指示的时间范围内未看到更新的更新, 请等待24小时后再执行下一次刷新。 如果发现延迟时间较长, 请检查服务运行状况仪表板。 如果服务报告为正常, 请联系 Microsoft 支持部门。<!-- 3896921 -->
