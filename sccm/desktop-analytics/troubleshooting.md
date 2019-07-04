---
title: 桌面分析的疑难解答
titleSuffix: Configuration Manager
description: 若要帮助你解决使用 Desktop 分析问题的技术详细信息。
ms.date: 06/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 246ee2c314df3d942d40d16ac9953580fed32803
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551246"
---
# <a name="troubleshoot-desktop-analytics"></a>桌面分析的疑难解答

使用本文中详细信息以帮助您使用与 Configuration Manager 集成的 Desktop 分析进行问题故障排除。



## <a name="confirm-prerequisites"></a>确认系统必备组件

许多常见的问题被由于缺少的必备组件。 首先请确认以下配置：

- [先决条件](/sccm/desktop-analytics/overview#prerequisites)  

- [Windows 组件更新](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [如何启用数据共享](/sccm/desktop-analytics/enable-data-sharing)，其中涵盖以下主题：  

    - 客户端需要连接 Internet 的终结点  

    - 代理服务器身份验证  

    - 诊断数据级别  



## <a name="monitor-connection-health"></a>监视器连接运行状况

使用**连接运行状况**仪表板在 Configuration Manager 中向下钻取到类别的设备运行状况。 在 Configuration Manager 控制台中，转到**软件库**工作区中，展开**Desktop 分析服务**节点，然后选择**连接运行状况**仪表板。  

有关详细信息，请参阅[监视连接运行状况](/sccm/desktop-analytics/monitor-connection-health)。


## <a name="log-files"></a>日志文件

有关详细信息，请参阅[Desktop 分析的日志文件](/sccm/core/plan-design/hierarchy/log-files#desktop-analytics)

### <a name="enable-verbose-logging"></a>启用详细日志记录

1. 对服务连接点，请转到以下注册表项： `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. 设置**LoggingLevel**值设为 `0`  


## <a name="bkmk_AzureADApps"></a> Azure AD 应用程序

桌面 Analytics 添加到你的 Azure AD 的以下应用程序：

- **配置管理器微服务**:将 Configuration Manager 连接与桌面的分析。 此应用具有没有访问要求。  

- **MALogAnalyticsReader**:检索 OMS 组和 Log Analytics 中创建的设备。 有关详细信息，请参阅[MALogAnalyticsReader 应用程序角色](#bkmk_MALogAnalyticsReader)。  

如果需要在完成安装后将这些应用程序，请转到**连接服务**窗格。 选择**配置用户和应用访问**，将应用和设置。  

- **Azure AD 应用程序为 Configuration Manager**。 如果你需要设置或安装完成后对连接问题进行故障排除，请参阅[创建和导入应用程序为 Configuration Manager](#create-and-import-app-for-configuration-manager)。 此应用需要**CM 集合数据写入**并**读取 CM 集合数据**上**配置管理器服务**API。  


### <a name="create-and-import-app-for-configuration-manager"></a>创建并应用导入 Configuration Manager

完成后[初始载入](/sccm/desktop-analytics/set-up#initial-onboarding)上桌面分析门户中，使用以下步骤来手动创建和导入应用程序为 Configuration Manager 如果无法从配置 Azure 服务创建此 Azure AD 应用向导。

#### <a name="create-app-in-azure-ad"></a>在 Azure AD 中创建应用

1. 打开[Azure 门户](http://portal.azure.com)具有的用户身份*全局管理员*权限，请转到**Azure Active Directory**，然后选择**应用注册**。 然后选择**新的注册**。  

2. 在中**创建**面板中，配置以下设置：  

    - **名称**： 唯一名称标识的应用，例如： `Desktop-Analytics-Connection`  

    - **支持的帐户类型**:**此组织目录中只 (Contoso) 的帐户**

    - **重定向 URI （可选）** :**Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    选择**注册**。  

3. 选择的应用，请注意**应用程序 （客户端） ID**并**目录 （租户） ID**。 值是用于配置 Configuration Manager 连接的 Guid。  

4. 在中**管理**菜单中，选择**证书和机密**。 选择**新的客户端机密**。 输入**描述**，指定过期持续时间，并选择**添加**。 复制**值**的密钥，用于进行配置的配置管理器连接。

    > [!Important]  
    > 这是唯一的机会来复制密钥值。 如果您不立即将其复制，需要创建另一个密钥。  
    >
    > 将密钥值保存在安全的位置。  

5. 在中**管理**菜单中，选择**API 权限**。  

    1. 上**API 的权限**面板中，选择**添加权限**。  

    2. 在中**请求 API 的权限**面板中，切换到**我的组织使用的 Api**。  

    3. 搜索并选择**配置管理器微服务**API。  

    4. 选择**应用程序权限**组。 展开**CmCollectionData**，并选择这两个以下权限：**CM 集合数据写入**并**读取 CM 集合数据**。  

    5. 选择**添加权限**。  

6. 上**API 的权限**面板中，选择**授予管理员同意...** .选择**是**。  


#### <a name="import-app-in-configuration-manager"></a>导入应用程序在配置管理器

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点    。 选择**配置 Azure 服务**功能区中。  

2. 上**Azure 服务**页上的 Azure 服务向导配置以下设置：  

    - 指定 Configuration Manager 中的对象名称  。  

    - 指定可选说明以帮助标识服务  。  

    - 选择**Desktop 分析**从可用服务列表。  
  
   选择“下一步”  。  

3. 上**应用程序**页上，选择相应**Azure 环境**。 然后选择**导入**为 web 应用。 配置中的以下设置**导入应用**窗口：  

    - **Azure AD 租户名称**:此名称是它如何命名已在配置管理器  

    - **Azure AD 租户 ID**:**Directory ID**从 Azure AD 复制  

    - **客户端 ID**：**应用程序 ID**复制从 Azure AD 应用  

    - **机密密钥**:键**值**复制从 Azure AD 应用  

    - **密钥到期日期**：密钥的同一个到期日期  

    - **应用 ID URI**：此设置应自动填充以下值： `https://cmmicrosvc.manage.microsoft.com/`  
  
   选择**验证**，然后选择**确定**以关闭导入应用窗口中。 选择**下一步**Azure 服务向导的应用页上。  

若要继续在向导的其余部分**诊断数据**页上，请参阅[连接到服务](/sccm/desktop-analytics/connect-configmgr#bkmk_connect)。

#### <a name="troubleshoot-app-in-configuration-manager"></a>在 Configuration Manager 中应用进行故障排除

如果遇到问题，创建或导入应用程序，第一次检查**SMSAdminUI.log**特定错误的。 然后检查以下配置：

- 已成功注册了该租户与 Desktop 分析服务。 有关详细信息，请参阅[如何设置桌面 Analytics](/sccm/desktop-analytics/set-up)。

- 所有必需的终结点都可访问。 有关详细信息，请参阅[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)。

- 请确保登录的用户具有正确权限。 有关详细信息，请参阅[先决条件](/sccm/desktop-analytics/overview#prerequisites)。

- 请确保，用户可以登录到 Azure 一般情况下。 此操作确定是否有任何常规的 Azure AD 身份验证问题。

- 检查的状态消息**SMS_SERVICE_CONNECTOR**组件有关*Desktop 分析辅助*。


### <a name="bkmk_MALogAnalyticsReader"></a> MALogAnalyticsReader 应用程序角色

如果设置了桌面分析时，将代表你的组织同意。 此许可是将 MALogAnalyticsReader 应用程序分配工作区的 Log Analytics 读者角色。 此应用程序角色是桌面分析所需。

如果在安装过程中没有此过程的问题，请使用以下过程来手动添加此权限：

1. 转到[Azure 门户](http://portal.azure.com)，然后选择**的所有资源**。 选择类型的工作区**Log Analytics**。  

2. 在工作区菜单中，选择**访问控制 (IAM)** ，然后选择**添加**。  

3. 在中**添加权限**面板中，配置以下设置：  

    - **角色**:**读取器**  

    - **分配其访问权限**:**Azure AD 用户、 组或应用程序**  

    - **选择**:**MALogAnalyticsReader**  

4. 选择“保存”  。

门户会显示一个通知它添加的角色分配的。


## <a name="data-latency"></a>数据滞后时间

<!-- 3846531 -->
当首次设置 Desktop 分析时，Configuration Manager 和桌面 Analytics 门户中的报表可能不会显示完整的数据立即。 可能需要有关发生的以下步骤 2-3 天：

- 活动设备将诊断数据发送到 Desktop 分析服务
- 该服务处理数据
- 该服务将与 Configuration Manager 站点同步

在同步时从 Configuration Manager 层次结构到 Desktop 分析的设备集合，它可能需要 10 分钟才会出现在桌面分析门户这些集合。 同样，当在桌面 Analytics 中创建部署计划，它可能需要 10 分钟才会出现在 Configuration Manager 层次结构的部署计划关联的新集合。 主站点创建集合，并与 Desktop 分析的管理中心站点同步。

在 Desktop 分析门户中，有两种类型的数据：**管理员数据**并**诊断数据**:

- **管理员数据**指的是对工作区配置进行任何更改。 例如，当你更改的资产**升级决策**或**重要性**，您要更改管理员数据。 这些更改通常具有组合的效果，因为它们可以更改安装的设备与资产相关的就绪状态。

- **诊断数据**指的是从客户端设备上传到 Microsoft 的系统元数据。 此数据为桌面分析提供支持。 它包括诸如设备清单属性和安全性和功能更新状态。

默认情况下，门户会自动提供的桌面分析中的所有数据都刷新每日。 此刷新进行了更改的诊断数据和对配置 （管理员数据） 进行任何更改。 它应会显示在通过 08:00 AM UTC Desktop 分析门户中每一天。

当你更改管理员数据时，可以在工作区中触发管理员数据按需刷新。 从桌面 Analytics 门户中的任何页上，打开数据货币浮出控件：

![在 Desktop 分析门户中的数据货币浮出控件选项卡的屏幕截图](media/data-currency-flyout.png)

然后选择**将更改应用**:

![展开的数据在桌面分析门户中的货币浮出控件的屏幕截图](media/data-currency-flyout-expand.png)

此过程通常需要 15-60 分钟。 时间取决于你的工作区的大小和需要流程对更改的范围。 当请求按需数据刷新时，它不会对诊断数据产生的任何更改。  有关详细信息，请参阅[Desktop 分析常见问题](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。

如果未看到上述时间范围内已更新的更改，等待另一个 24 小时后下, 一次每日刷新。 如果您看到的更长的延迟，请检查服务运行状况仪表板。 如果该服务报告为正常运行，请联系 Microsoft 支持部门。<!-- 3896921 -->
