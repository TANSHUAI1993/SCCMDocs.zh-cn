---
title: 新版本 1706
titleSuffix: Configuration Manager
description: 获取有关 System Center Configuration Manager 的 1706 版中引入的更改和新功能的详细信息。
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 050122d6a1b799a30bd2c5a83ab261e92aaafabe
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677206"
---
# <a name="what39s-new-in-version-1706-of-system-center-configuration-manager"></a>System Center Configuration Manager 版本 1706 的新增功能

适用范围：  System Center Configuration Manager (Current Branch)

System Center Configuration Manager Current Branch 的更新 1706 作为控制台内更新提供，用于运行版本 1606、1610 或 1702 的以前安装的站点。

> [!TIP]  
> 若要安装新站点，必须使用 Configuration Manager 的基准版本。  
>  了解详细信息：    
>   - [安装新站点](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [在站点上安装更新](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [基准和更新版本](/sccm/core/servers/manage/updates#bkmk_Baselines)  

以下各节提供有关 Configuration Manager 版本 1706 中引入的更改和新功能的详细信息。  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>站点基础结构

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>对于适用于 Windows 10 和 Office 365 的快速安装文件的客户端对等缓存支持  
<!-- 1352486 -->
从此版本开始，对等缓存支持分发 Windows 10 的内容快速安装文件和 Office 365 的更新文件。 不需要其他配置来支持此更改。

### <a name="updates-for-the-data-warehouse"></a>数据仓库更新
<!-- 1277922 -->
数据仓库不再是预发行功能。 我们还更新了先决条件，加入了对 SQL Server Always On 可用性组和故障转移群集上的数据库的支持。 有关详细信息，请参阅[数据仓库服务点](/sccm/core/servers/manage/data-warehouse)。

### <a name="accessibility-improvements"></a>辅助功能改进
<!-- 1253000 -->
我们添加了对 Configuration Manager 控制台辅助功能的其他改进。 有关详细信息，请参阅[辅助功能](/sccm/core/understand/accessibility-features)。

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性组改进
<!-- 1352094 -->
借助此版本，现在可以在与 Configuration Manager 配合使用的 SQL Server AlwaysOn 可用性组中使用异步提交副本。 这意味着，你可以将其他副本添加到可用性组，用作场外（远程）备份，然后在灾难恢复方案中使用它们。  
  - Configuration Manager 支持使用异步提交副本来恢复同步副本。 请参阅备份和恢复主题中的[站点数据库恢复选项](/sccm/core/servers/manage/recover-sites#site-database-recovery-options)，了解有关如何实现此操作的信息。
  - 此版本不支持故障转移后使用异步提交副本作为站点数据库。
有关详细信息，请参阅[准备使用 Always On 可用性组](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。

### <a name="update-reset-tool"></a>更新重置工具
<!-- 1324589 -->
从版本 1706 开始，Configuration Manager 主站点和管理中心站点包含 Configuration Manager 更新重置工具，即 CMUpdateReset.exe  。 控制台中更新存在下载或复制问题时，可通过当前仍受支持的分支的任意版本使用此工具来修复问题。 有关详细信息，请参阅[更新重置工具](/sccm/core/servers/manage/update-reset-tool)。

### <a name="high-dpi-console-support"></a>高 DPI 控制台支持  
<!-- 1353476 -->
使用此版本，应能修复在高 DPI 设备（如 Surface Book）上进行查看时，Configuration Manager 控制台如何缩放和显示 UI 不同部分的问题。

### <a name="improved-boundary-groups-for-software-update-points"></a>改进了软件更新点的边界组
<!-- 1324591 -->
此版本包括了针对软件更新点如何与边界组配合使用的多项改进。 以下内容总结了新的回退行为：
-   现在，软件更新点的回退使用一个可配置的时间来回退到相邻边界组。
-   独立于回退配置，客户端会尝试访问它使用了 120 分钟的最后一个软件更新点。 在 120 分钟无法访问该服务器后，客户端将检查其池中可用的软件更新点，以便找到一个新的软件更新点。
-   如果在两个小时内无法连接到其原始服务器，则客户端会切换到一个短循环，以联系新的软件更新点。 这意味着，如果客户端无法连接到新的服务器，它就会从自己的可用服务器池中快速选择下一个服务器，并尝试进行连接。

有关详细信息，请参阅 Current Branch 的边界组主题中的[软件更新点](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。

### <a name="azure-ad-integration-with-configuration-manager"></a>Azure AD 与 Configuration Manager 集成
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
在此版本中，我们改进了 Configuration Manager 与 Azure Active Directory (Azure AD) 的集成。  这些改进可简化配置用于 Configuration Manager 的 Azure 服务的方式，并可帮助管理通过 Azure AD 进行身份验证的客户端和用户。

通过改进集成实现了以下功能：  
  -   Azure 服务向导 – 此向导提供了一种可替换单个工作流的常见配置体验，可供设置用于 Configuration Manager 的下列 Azure 服务。
      - 云管理  ：使用 Azure Active Directory (Azure AD) 支持客户端进行身份验证。 还可以配置 Azure AD 用户发现。
      - Log Analytics 连接器  连接到 Azure Log Analytics 并同步集合数据。
      - 升级就绪情况  ：连接到升级就绪情况并查看客户端升级兼容性数据。
      - 适用于企业的 Windows 应用商店  ：连接到适用于企业的 Windows 应用商店的在线商店并为组织获取应用，以通过 Configuration Manager 进行部署。


  可通过使用 [Azure 服务器 Web 应用](/azure/app-service/app-service-authentication-overview)提供订阅和配置详情来完成此操作，否则需要在每次使用 Azure 设置新 Configuration Manager 组件或服务时输入这些详细信息。 有关详细信息，请参阅 [Azure 服务向导](/sccm/core/servers/deploy/configure/azure-services-wizard)。

-   在 Internet 上使用 Azure AD 对客户端进行身份验证以访问 Configuration Manager 站点。 Azure AD 使你不再需要配置和使用客户端身份验证证书。 它需要云管理网关站点系统角色。 有关详细信息，请参阅[使用 Azure AD 从 Internet 安装并分配 Configuration Manager 客户端以进行身份验证](/sccm/core/clients/deploy/deploy-clients-cmg-azure)。

-   在位于 Internet 上的计算机上安装和管理 Configuration Manager 客户端。 它需要使用云管理网关站点系统角色。 有关详细信息，请参阅[使用 Azure AD 从 Internet 安装并分配 Configuration Manager 客户端以进行身份验证](/sccm/core/clients/deploy/deploy-clients-cmg-azure)。

-   配置 Azure AD 用户发现。  使用 Azure 服务向导配置此新发现方法。 此新方法查询 Azure AD 以获取用户数据，然后可以将该数据与传统的发现数据一起使用。  支持完全同步和增量同步。  有关详细信息，请参阅 [Azure AD 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)。

### <a name="peer-cache-improvements"></a>对等缓存功能改进
<!-- 1252345 -->
对等缓存功能不再使用网络访问帐户对来自对等项的下载请求进行身份验证。 客户端仍然需要此帐户时，需要注意这一点。 启动到 WinPE 然后从对等缓存源访问内容的客户端仍然需要此帐户。 有关详细信息，请参阅[对等缓存的要求和注意事项](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements)。


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>符合性设置

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>不使用 Configuration Manager 客户端管理的 Windows 10 设备适用的新配置设置
<!-- 1354715 -->
在此版本中，我们添加了适用于使用 Intune 注册的或由 Configuration Manager 本地管理的 Windows 10 设备的新配置项目设置。 这些设置包括：

- **密码**
  - 设备加密
- **设备**
  - 区域设置修改（仅限桌面设备）
  - 电源和睡眠设置修改
  - 语言设置修改
  - 系统时间修改
  - 设备名称修改
- **应用商店**
  - 自动更新来自应用商店的应用
  - 仅使用专用应用商店
  - 启动来自应用商店的应用
- **Microsoft Edge**
  - 阻止访问 about:flags
  - SmartScreen 提示重写
  - 文件的 SmartScreen 提示重写
  - WebRTC localhost IP 地址
  - 默认搜索引擎
  - OpenSearch XML URL
  - 主页（仅限桌面设备）

有关所有 Windows 10 设置的详细信息，请参阅[如何为没使用 System Center Configuration Manager 客户端管理的 Windows 8.1 和 Windows 10 设备创建配置项目](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)。

### <a name="new-device-compliance-policy-rules"></a>新设备符合性策略规则

* **所需的密码类型**。 指定用户是否必须创建字母数字密码或数字密码。 对于字母数字密码，你还可以指定密码必须包含的字符集的最小个数。 四个字符集为：小写字母、大写字母、符号和数字。

  **在以下设备上受支持：**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
  <br></br>
* **在设备上阻止进行 USB 调试**。 无需配置此设置，因为已在 Android for Work 的设备上禁用 USB 调试。

  **在以下设备上受支持：**
  * Android 4.0+
  * Samsung KNOX 标准版 4.0+
  <br></br>
* **阻止来自未知源的应用**。 要求设备阻止安装来自未知源的应用。 无需配置此设置，因为 Android for Work 设备始终限制来自未知源的安装。

  **在以下设备上受支持：**
  * Android 4.0+
  * Samsung KNOX 标准版 4.0+
  <br></br>
* **要求对应用进行威胁扫描**。 此设置指定在设备上启用的“验证”应用功能。

  **在以下设备上受支持：**
  * Android 4.2 到 4.4
  * Samsung KNOX 标准版 4.0+

请参阅[创建和部署设备符合性策略](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy)，尝试新的设备符合性规则

## <a name="application-management"></a>应用程序管理

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台运行 PowerShell 脚本
<!-- 1236459 -->

在 Configuration Manager 中，你可以使用包和程序将脚本部署到客户端设备。 在此版本中，我们添加了可以让你执行以下操作的新功能：

- 将 PowerShell 脚本导入到 Configuration Manager
- 从 Configuration Manager 控制台编辑脚本（仅针对未签名的脚本）
- 将脚本标记为“已批准”或“已拒绝”，以提高安全性
- 在 Windows 客户端 PC 和本地托管的 Windows PC 的集合上运行脚本。 不过，你不需要部署脚本，它们可以在客户端设备上近乎实时的运行。
- 在 Configuration Manager 控制台中检查脚本返回的结果。

有关详细信息，请参阅[从 Configuration Manager 控制台创建并运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)。

### <a name="new-mobile-application-management-policy-settings"></a>新移动应用程序管理策略设置    
<!--1324760-->
从此版本开始，你可以使用三个新的移动应用程序管理 (MAM) 策略设置：

- **阻止屏幕捕捉（仅限于 Android 设备）：** 指定在使用该应用时，阻止设备的屏幕捕捉功能。

请参阅[使用 Configuration Manager 中的应用保护策略来保护应用](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies)，尝试新的应用保护策略设置。


## <a name="operating-system-deployment"></a>操作系统部署

### <a name="hardware-inventory-collects-secure-boot-information"></a>硬件清单收集安全启动信息
硬件清单现在收集有关是否在客户端启用安全启动的信息。 该信息存储在 **SMS_Firmware** 类（在 1702 版本中引入）中，并在硬件清单中默认启用。 有关硬件清单的详细信息，请参阅[如何配置硬件清单](/sccm/core/clients/manage/inventory/configure-hardware-inventory)。

### <a name="collapsible-task-sequence-groups"></a>可折叠的任务序列组
此版本引入了扩展和折叠任务序列组的功能。 可以展开或折叠单个组，也可一次展开或折叠所有组。

### <a name="reload-boot-images-with-current-windows-pe-version"></a>重载当前的 Windows PE 版本的启动映像
当你在所选启动映像上运行“更新分发点”  时，现在可以选择在启动映像中从 Windows ADK 安装目录重载最新版本的 Windows PE。 有关详细信息，请参阅[使用启动映像更新分发点](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)。

## <a name="software-updates"></a>软件更新

### <a name="improvements-to-express-update-download-time"></a>对快速更新下载时间的改进
在此版本中，我们对快速更新的下载时间进行了重大的改进。 有关详细信息，请参阅[管理 Windows 10 更新的快速安装文件](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)。

### <a name="manage-microsoft-surface-driver-updates"></a>管理 Microsoft Surface 驱动程序更新
<!-- 1098490 -->
你现在可以使用 Configuration Manager 来管理 Microsoft Surface 驱动程序更新。    


#### <a name="prerequisites"></a>先决条件
- 所有软件更新点都必须运行 Windows Server 2016。    
- 这是预发行功能，必须启用它才能使用。 有关详细信息，请参阅[使用更新中的预发行功能](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。

#### <a name="to-manage-surface-driver-updates"></a>管理 Surface 驱动程序更新

1. 为 Microsoft Surface 驱动程序启用同步。 使用[配置分类和产品](/sccm/sum/get-started/configure-classifications-and-products)中的过程，并选中“分类”  选项卡上的“包括 Microsoft Surface 驱动程序和固件更新”  复选框，以启用 Surface 驱动程序。
2. [同步 Microsoft Surface 驱动程序](/sccm/sum/get-started/synchronize-software-updates)。
3. [部署同步的 Microsoft Surface 驱动程序](/sccm/sum/deploy-use/deploy-software-updates)

### <a name="configure-windows-update-for-business-deferral-policies"></a>配置 Windows Update for Business 延迟策略
<!-- 1290890 -->
现在，你可以针对 Windows 10 功能更新或直接由 Windows Update for Business 托管的 Windows 10 设备的质量更新，配置延迟策略。 你可以在“软件库”   > “Windows 10 维护服务”  下方的新“Windows Update for Business 策略”  节点中管理延迟策略。

有关详细信息，请参阅[在 Windows 10 中与适用于企业的 Windows 更新集成](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)。

### <a name="improved-user-notifications-for-office-365-updates"></a>改进了 Office 365 更新的用户通知
已进行了改进，在客户端安装 Office 365 更新时利用 Office 即点即用用户体验。 这包括弹出通知、应用内通知以及倒计时体验。 有关详细信息，请参阅 [Office 365 更新的重启行为和客户端通知](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates)

## <a name="reporting"></a>报表

### <a name="use-windows-analytics-with-configuration-manager"></a>结合使用 Windows Analytics 和 Configuration Manager
<!-- 1318608 -->
Windows Analytics 是一组解决方案，可便于深入了解环境的当前状态。 环境中的设备报告 Windows 遥测数据。 可通过 Azure 门户访问数据。 对于升级就绪情况，可在 Configuration Manager 控制台的监视节点中直接获取此数据。

有关详细信息，请参阅[结合使用 Windows Analytics 和 Configuration Manager](/sccm/core/clients/manage/monitor-windows-analytics)。


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>移动设备管理

### <a name="updates-to-android-for-work-sharing-configuration"></a>Android for Work 共享配置更新
<!-- 1338403 -->
在此版本中，更新了“工作配置文件”  设置组中的“允许工作和个人配置文件间的数据共享”  设置的值。 还添加了自定义设置，用于阻止在工作个个人配置文件之间进行复制粘贴。

有关详细信息，请参阅 [Android for Work 设备的配置项](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)。

### <a name="android-and-ios-enrollment-restrictions"></a>Android 和 iOS 注册限制
<!-- 1290826 -->
使用此版本，现在可以指定用户不能注册个人 Android 或 iOS 设备。 借助新的设备限制设置，可以限制为将 Android 设备注册为预声明设备。 对于 iOS 设备，可以阻止所有设备注册，使用 Apple 设备注册计划、Apple Configurator 或 Intune 设备注册管理器帐户注册的设备除外。
- 有关 Android 注册限制的详细信息，请参阅[设置 Android 设备管理](/sccm/mdm/deploy-use/enroll-hybrid-android)。
- 有关 iOS 注册限制的详细信息，请参阅[配置 iOS 注册限制](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions)。

## <a name="protect-devices"></a>保护设备

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>在 Device Guard 策略中包括对特定文件和文件夹的信任
<!--1324676-->
在此版本中，我们已向 Device Guard 策略管理添加了更多功能。

现在可以选择在 Device Guard 策略中添加对特定文件或文件夹的信任。 此操作可让你：

- 解决托管安装程序行为的问题
- 信任无法使用 Configuration Manager 部署的业务线应用
- 信任包括在操作系统部署映像中的应用

有关详细信息，请参阅[使用 Configuration Manager 进行 Device Guard 管理](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)。
