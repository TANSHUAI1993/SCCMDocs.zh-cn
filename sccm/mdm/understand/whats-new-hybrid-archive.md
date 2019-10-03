---
title: 归档混合 MDM 的新增功能
titleSuffix: Configuration Manager
description: System Center Configuration Manager 和 Intune 的混合部署过去可用的移动设备管理功能的存档
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 006580a7ae4965ab4662ae02bee13ed9796697f8
ms.sourcegitcommit: b9cc8e723c5d8c3be44edad24ad29d75c0cdd2b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2019
ms.locfileid: "71826264"
---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 和 Microsoft Intune 过去的混合功能

适用范围：System Center Configuration Manager (Current Branch)

本文提供有关 System Center Configuration Manager 和 Microsoft Intune 的混合部署过去可用的移动设备管理 (MDM) 功能的详细信息。  

##  <a name="compatibility-with-configuration-manager-versions"></a>与 Configuration Manager 版本的兼容性  

 本文的每个部分都列出了混合功能，共 3 个不同类别。 请使用以下指南，确定每个类别中的功能与不同版本的 Configuration Manager 的兼容性：  

|功能类别|
|-|  
|**Microsoft Intune 新增功能** - 一般情况下，此类别列出的所有功能应适用于所有 Configuration Manager 版本（包括 System Center 2012 R2 Configuration Manager 版本），因为这些功能仅需要 Intune 服务，不需要 Configuration Manager 中的其他功能。<br /><br /> **Configuration Manager Technical Preview 中的新增功能** - 此类别下列出的所有功能仅适用于指定的 Technical Preview 版本。 若要试用这些功能，必须安装功能说明中指定的 Technical Preview 版本。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)。<br /><br /> **Configuration Manager (Current Branch) 中的新增功能** - 此类别下列出的所有功能仅适用于指定的 Configuration Manager (Current Branch) 版本，例如版本 1511 或 1602。 如果要为混合部署使用较旧版本的 Configuration Manager，则必须升级到功能说明中指定的 Configuration Manager (Current Branch) 版本。 有关详细信息，请参阅[升级到 System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。|  



## <a name="april-2017"></a>2017 年 4 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **适用于 Managed Browser 的 MyApps**  
  现在 Microsoft MyApps 改进了 Managed Browser 内部的支持。 不作为管理目标的 Managed Browser 用户将直接转至 MyApps 服务，这些用户可以在其中访问管理员预配的 SaaS 应用。 作为 Intune 管理目标的用户可以继续通过内置的 Managed Browser 书签访问 MyApps。

- **Managed Browser 和公司门户的新图标**  
  Managed Browser 将获得该应用的 Android 和 iOS 版的更新图标。 新图标将包含更新的 Intune 徽章，使其与企业移动性 + 安全性 (EM+S) 中的其他应用更为一致。 可以在 [Intune 应用 UI 页中的新增功能](https://docs.microsoft.com/intune/whats-new-app-ui)中查看 Managed Browser 的新图标。

  公司门户还将获得该应用的 Android、iOS 和 Windows 版的更新图标，以改进与 EM+S 中的其他应用的一致性。 这些图标于四月至五月底逐步在平台上发布。

- **Android 公司门户中的登录进度指示器**  
  用户启动或重启应用时，Android 公司门户应用的更新程序将显示登录进度指示器。 允许用户访问应用前，指示器将经历以下新状态：开始是“正在连接...”，然后是“正在登录...”，接下来是“正在查看安全要求...”。 可以在 [Intune 应用 UI 页中的新增功能](https://docs.microsoft.com/intune/whats-new-app-ui)中查看适用于 Android 的公司门户应用的新屏幕。

- **阻止应用访问 SharePoint Online**  
  现在可以创建基于应用的条件访问策略来阻止未向其实施应用保护策略的应用访问 [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online)。 在基于应用的条件访问方案中，可以指定想要让其具备使用 Azure 门户访问 SharePoint Online 的权限的应用。

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Configuration Manager Technical Preview 1704 中的新变化

- **使用应用配置策略配置 Android 应用**  
  当用户在 Android for Work 设备上运行应用时，可以在 Configuration Manager 中使用应用配置策略分发预配置的设置。 Android 应用配置政策仅适用于运行 Android for Work 的设备。 这些策略适用于已从 Play for Work 应用商店批准的应用。 有关详细信息，请参阅[使用应用配置策略配置 Android 应用](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies)。



## <a name="march-2017"></a>2017 年 3 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **Android 适用的公司门户应用的最新用户体验**  
  Android 适用的公司门户应用的用户界面具有更新式的外观。 值得注意的更新有：

  - 颜色公司门户选项卡标题在 IT 定义的品牌中为彩色。
  - 应用在 "**应用**" 选项卡中，更新了 "**特色应用**" 和 "**所有应用**" 按钮。
  - 寻找在 "**应用**" 选项卡中，"**搜索**" 按钮是一个浮动操作按钮。
  - 导航应用："**所有应用**" 视图显示了一个选项卡式视图，其中显示了**特色**、**全部**和**类别**，便于导航。
  - 支持 **"我的设备**和**联系人**" 选项卡将更新以提高可读性。

  有关这些更改的详细信息，请参阅 [Intune 最终用户应用的 UI 更新](https://docs.microsoft.com/intune/whats-new-app-ui)。

- **Windows 10 公司门户的签名脚本**  
  如果需要下载和旁加载 Windows 10 公司门户应用，现在可以使用脚本为你的组织简化应用签名过程。 若要下载该脚本及其使用说明，请参阅 TechNet 库中的 [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript)（Windows 10 公司门户适用的 Microsoft Intune 签名脚本）。 有关此公告的详细信息，请参阅 Intune 支持团队博客上的[更新 Windows 10 公司门户应用](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/)。

- **改进了对中国的 Android 用户的支持**  
  由于中国地区没有 Google Play 商店，Android 设备必须从中国市场获取应用。 公司门户支持此工作流。 它可重定向中国的 Android 用户，以便从本地应用商店下载公司门户和 Outlook 应用。 启用条件访问策略后，此行为将同时提升有关移动设备管理和移动应用程序管理的用户体验。 以下中文应用商店可以提供 Android 适用的公司门户和 Outlook 应用：

  - [百度](https://go.microsoft.com/fwlink/?linkid=836946)
  - [小米](https://go.microsoft.com/fwlink/?linkid=836947)
  - [腾讯](https://go.microsoft.com/fwlink/?linkid=836949)
  - [华为](https://go.microsoft.com/fwlink/?linkid=836948)
  - [豌豆荚](https://go.microsoft.com/fwlink/?linkid=836950)

- **请确保公司门户应用处于最新状态**  
  2016 年 12 月，我们发布了更新，当一组用户在注册 iOS、Android、Windows 8.1+ 或 Windows Phone 8.1+ 设备时，该更新将执行多重身份验证 (MFA)。 如果没有 Android (v5.0.3419.0+) 和 iOS (v2.1.17+) 适用的某些基准版本的公司门户应用，此功能将无法运行。

  Intune 的管理功能在不断改进。 很多改进对所有受支持平台上的公司门户应用的更新进行了协调。 我们建议你将最新版本的公司门户应用安装在设备上。 这种做法可利用 Intune 的改进来获得最佳用户体验。

  >[!Tip]
  > 让用户将其设备设置为从相应的应用商店中自动更新应用。 如果通过网络共享提供 Android 公司门户应用，则可从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=49140)下载最新版本。

- **Microsoft Teams 现已在 iOS 和 Android 上启用了 MAM**  
  适用于 iOS 和 Android 的 Microsoft Teams 应用现已启用 Intunes 移动应用管理 (MAM) 功能。 使你的团队能够跨设备自由地工作，同时确保对话和公司数据得到保护。 有关详细信息，请参阅企业移动性和安全性博客中的 [Microsoft Teams 公告](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/)。

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Configuration Manager Technical Preview 1703 中的新增功能

- **对 Apple Volume Purchase Program 方案的额外支持**  
   从 Technical Preview 1703 开始，现可支持以下 Volume Purchase Program (VPP) 方案：

   - 设备授权 - 对于支持设备授权且部署到设备集合的应用，现在每个设备只需一个许可证。 以前，设备上每位用户都需要一个许可证。 有关详细信息，请参阅[将批量采购的 iOS 应用部署到设备集合](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections)。
   - 将多个 VPP 令牌用于单个混合租户，且同时将两个令牌均用于管理 VPP 应用。
   - 使用 VPP 教育令牌，且可区分企业和教育令牌。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

以下功能以前在 Configuration Manager Technical Preview 版本中提供。 这些功能现在可用于 Intune 和 Configuration Manager (Current Branch) 版本 1702 的混合部署。

- [Android for Work 支持](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [针对不符合应用的符合性设置](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [PFX 证书创建和分发以及 S/MIME 支持](/sccm/core/plan-design/changes/whats-new-in-version-1702#mobile-device-management)
- [混合 MDM 的创建向导中，Android 和 iOS 版本不再作为目标](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Configuration Manager (Current Branch) 1702 版本中还包括以下其他混合功能：

- **对 Apple Volume Purchase Program (VPP) 改进的支持**  
  - 你现在可以将已授权的应用部署到设备以及用户。 部署应用时，将声明相应的许可证（如下所示），具体视应用是否支持设备授权而定：

    | Configuration Manager 版本 | 应用是否支持设备授权？ | 部署集合类型 | 已声明的许可证 |
    |-|-|-|-|
    |早于 1702|是|“用户”|用户许可证|
    |早于 1702|否|“用户”|用户许可证|
    |早于 1702|是|设备|用户许可证|
    |早于 1702|否|设备|用户许可证|
    |1702 及更高版本|是|“用户”|用户许可证|
    |1702 及更高版本|否|“用户”|用户许可证|
    |1702 及更高版本|是|设备|设备许可证|
    |1702 及更高版本|否|设备|用户许可证|

  - 此外，你现在可以部署并跟踪你从 iOS Volume Purchase Program 教育版购买的应用。

  - 你现在可以将多个 Apple 批量采购程序令牌与 Configuration Manager 相关联。

  有关批量购买的 iOS 应用的详细信息，请参阅[管理批量购买的 iOS 应用](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)。

- **对适用于企业的 Microsoft Store 中的业务线应用的支持**  
  现在可以同步来自适用于企业的 Microsoft Store 的自定义业务线应用。

- **新移动威胁防御监视工具**  
    现在，可以使用新方法通过移动威胁防御服务提供程序来监视符合性状态。

    有关详细信息，请参阅[如何监视移动威胁防御合规性](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance)。





## <a name="february-2017"></a>2017 年 2 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **公司门户网站现代化**

  公司门户网站支持面向没有托管设备的用户的应用。 该网站使用新的对比色配色方案、动态插图和“汉堡菜单”（其中包含支持人员详细联系信息和现有托管设备的信息），这与其他 Microsoft 产品和服务保持一致。 对登录页面进行了重新组织，以突出用户可用的应用，并且会循环播放精选应用和最近更新的应用。 可在[“UI更新”](https://docs.microsoft.com/intune/whats-new-app-ui)页面上找到前后对照的图片。

- **适用于 Windows 设备的新 MDM 服务器地址**

  用于注册 Windows 和 Windows Phone 设备的 MDM 服务器地址已从 manage.microsoft.com 更改为 enrollment.manage.microsoft.com。 注册 Windows 或/和 Windows Phone 设备时如果出现提示，请通知用户使用 enrollment.manage.microsoft.com 作为 MDM 服务器地址。 对于 DNS 中将 EnterpriseEnrollment.contoso.com 重定向到 manage.microsoft.com 的 CNAME，此更新还需要将其替换为 DNS 中将 EnterpriseEnrollment.contoso.com 重定向到 EnterpriseEnrollment-s.manage.microsoft.com 的 CNAME。 有关此更改的其他信息，请访问 https://aka.ms/intuneenrollsvrchange 。

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Configuration Manager Technical Preview 1702 中的新增功能

- **Android for Work 支持**

  在使用 Configuration Manager Technical Preview 1702 的混合 MDM 环境中，现可使用 Android for Work 管理 Android 设备。 受支持的 Android 设备现可注册为 Android for Work 设备，从而在相关设备上创建工作配置文件，其中可在该设备上部署 Play for Work 批准的应用。 还可为这些设备配置和部署配置项、符合性策略和资源访问配置文件。 有关详细信息，请参阅 [Android for Work 支持](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support)。

- **针对不符合应用的符合性设置**

  现可在符合性策略中创建面向 Android 和 iOS 应用的不符合应用规则。 如果设备安装了指定应用程序，根据部署的条件访问策略，它们将被标记为“不符合”，且不可再访问公司资源。 有关详细信息，请参阅[条件性访问设备符合性策略改进](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements)。

- **PFX 证书创建和分发以及 S/MIME 支持**

  现可在混合环境中为用户创建和部署 PFX 证书。 随后，这些证书可用于用户已注册的设备的 S/MIME 电子邮件加密和解密。 有关详细信息，请参阅[创建支持 S MIME 的 PFX 证书](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support)。

- **对其他 iOS 配置设置的支持**
   
    你现在有 42 个其他 iOS 设置，可配置为配置项的一部分。 已为受监督的 iOS 设备添加大部分设置（总共 35 个设置）。 有关详细信息，请参阅 [iOS 设备的新符合性设置](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices)。



## <a name="january-2017"></a>2017 年 1 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **Android 7.1.1 支持**

  Intune 现在完全支持并可管理 Android 7.1.1。

- **解决了以下问题：iOS 设备处于非活动状态，或管理控制台无法与其通信**

  如果用户设备与 Intune 失去联系，可向用户提供新的故障排除步骤，帮助其重新获得访问公司资源的权限。 请参阅[设备处于非活动状态，或管理控制台无法与其通信](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cant-communicate-with-them)。

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Configuration Manager Technical Preview 1701 中的新增功能

- **混合 MDM 的创建向导中，Android 和 iOS 版本不再作为目标**

  从用于混合移动设备管理 (MDM) 的 Technical Preview 1701 开始，创建用于 Intune 托管设备的新策略和配置文件时，不再需要将特定版本的 Android 和 iOS 作为目标。 得益于此更改，混合部署可为新的 Android 和 iOS 版本更快地提供支持，无需新的 Configuration Manager 版本或扩展。 有关详细信息，请参阅 [Android 和 iOS 版本不再作为创建向导中的目标](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)。



## <a name="december-2016"></a>2016 年 12 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **注册移动到 Azure 门户时的多重身份验证**

  以前，你会转到 Intune 控制台或 Configuration Manager 控制台，以设置 MFA 用于 Intune 注册。 通过此更新的功能，你现在可以使用 Intune 凭据登录到[Microsoft Azure 门户](https://manage.windowsazure.com)，并通过 AZURE AD 配置 MFA 设置。 若要了解详细信息，请参阅 [Microsoft Intune 的多重身份验证](https://aka.ms/mfa_ad)。

- **Android 版公司门户应用现已在中国推出**

  Android 版公司门户应用现已在中国推出。 由于中国地区没有 Google Play 商店，Android 设备必须从中国的应用市场获取应用。 可从以下商店下载 Android 版公司门户应用：

  - [百度](https://go.microsoft.com/fwlink/?linkid=836946)
  - [华为](https://go.microsoft.com/fwlink/?linkid=836948)
  - [腾讯](https://go.microsoft.com/fwlink/?linkid=836949)
  - [豌豆荚](https://go.microsoft.com/fwlink/?linkid=836950)
  - [小米](https://go.microsoft.com/fwlink/?linkid=836947)

  Android 版公司门户应用使用 Google Play Services 与 Microsoft Intune 服务进行通信。 由于 Google Play Services 尚未在中国推出，因此执行以下任何任务最长可能需要 8 个小时才能完成。

  | Configuration Manager 管理控制台 | Android 适用的 Intune 公司门户应用 | Intune 公司门户网站 |
  |----|----|----|
  | 停用/擦除（删除所有数据）| 删除远程设备 | 删除设备（本地和远程） |
  | 停用/擦除（删除公司数据）| 重置设备 | 重置设备|
  | 新的或更新的应用部署 | 安装可用的业务线应用 | 设备密码重置|
  | 远程锁定| | |
  | 密码重置 | | |


## <a name="november-2016"></a>2016 年 11 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **适用于 Windows 10 设备的新 Microsoft Intune 公司门户**

  Microsoft 发布了一个新的[适用于 Windows 10 设备的公司门户应用](https://www.microsoft.com/store/apps/9wzdncrfj3pz)。 此应用利用了新 Windows 10 通用格式，可跨所有 Windows 10 设备（PC 和移动设备等）提供相同的更新用户体验，同时仍启用以前公司门户应用提供的所有相同功能。

  新应用可在 Windows 10 设备上利用平台功能，例如单一登录 (SSO) 和基于证书的身份验证。 此应用将作为对现有 Windows 8.1 公司门户和 Windows Phone 8.1 公司门户（安装自 Windows 应用商店）的升级而提供。 有关详细信息，请转到 [Intune 支持团队博客](https://aka.ms/intunecp_universalapp)。

  新公司门户应用还会显示在 Configuration Manager 控制台中标记为**可用**的适用于企业的 Windows 应用商店应用程序。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

以下功能以前可在 Configuration Manager Technical Preview 版本中使用，现在可在 Intune 和 Configuration Manager (Current Branch) 1610 版本的混合部署中使用。

* [配置项目的其他设置和改进的体验](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [DEP 配置文件的其他设置](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [适用于企业的 Windows 应用商店中的付费应用](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Windows 10 VPN 配置文件的本机连接类型](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Intune 合规性图表](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [从控制台请求策略同步](/sccm/mdm/deploy-use/sync-intune-device)
* [Windows Defender 配置设置](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

Configuration Manager (Current Branch) 1610 版本中还包括以下其他混合功能：

- **增加了注册设备数**

  用户现在最多可注册 15 台设备。 以前该限制为每个用户 5 台设备。


- **其他安全支持**

  除了完全权限管理员之外，以下内置安全角色现在对所有企业拥有的设备节点中的项具有完全访问权限，包括预声明设备、iOS 注册配置文件，以及 Windows 注册配置文件：

    - 资产管理员
    - 公司资源访问管理器

  对 Configuration Manager 控制台中这些区域的只读访问权限仍授予给只读分析员角色。

- **从 Windows 信息保护应用自动触发 VPN 访问**

  可以将 Windows 信息保护主域添加到 Windows 10 VPN 配置文件（使所有关联的应用在设备上运行时自动触发 VPN 连接）。 只在选择本机连接类型时，此选项才可用。

- **Windows 10 VPN 配置文件的条件访问**

    现在可要求在 Azure Active Directory 中注册的 Windows 10 设备符合要求，以通过在 Configuration Manager 控制台中创建的 Windows 10 VPN 配置文件具有 VPN 访问权限。 这可通过 VPN 配置文件向导中“身份验证方法”页上新的“对此 VPN 连接启用条件性访问”复选框，和 Windows 10 VPN 配置文件的 VPN 配置文件属性来实现。 只在选择本机连接类型时，此选项才可用。

    如果对配置文件启用条件性访问，还可以对单一登录身份验证指定一个单独的证书。

## <a name="october-2016"></a>2016 年 10 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2016 年 10 月推出的以下 Intune 功能适用于混合部署。

- **移动应用程序管理的条件性访问**

  可以限制对 Exchange Online 的访问，以便仅访问支持 Intune 移动应用程序管理策略的应用，如 Outlook。 [这一新增功能](/intune/deploy-use/allow-policy-managed-apps-access-to-o365)可与 Intune 移动应用管理 (MAM) 策略完美结合使用，用户可以阻止对未使用 Intune MAM 策略配置的内置邮件客户端或其他应用的访问。 这可确保你的用户使用通过 Intune MAM 进行保护的应用访问组织的数据。 可通过 Azure 门户使用 Intune 移动应用管理。 查找“设置”边栏选项卡中的条件性访问部分。

- **Intune App Wrapping Tool for Android**

  通过使用 Intune App Wrapping Tool，应用将可以使用 Intune 移动应用程序管理 (MAM) 策略。

- **Android Samsung KNOX 标准版与 Intune 的兼容性**

  Intune 不能将 Samsung Galaxy Ace 手机的某些型号作为 Samsung KNOX 标准版设备进行管理。 向 Intune 注册这些设备时，Intune 会将它们作为标准 Android 设备进行管理。

  受影响的型号包括：

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  你和最终用户不需要采取进一步的操作。 有关详细信息，请访问 Samsung KNOX 网站。

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Configuration Manager Technical Preview 1610 中的新增功能

Configuration Manager Technical Preview 1610 的 2016 年 10 月版本中引入了以下新增的混合功能。

- **从管理员控制台请求策略同步**

  可以从 Configuration Manager 控制台中的已注册移动设备上请求策略同步，而无需在设备本身的公司门户应用中请求同步。 这是一个新操作，在“远程设备操作”菜单中名为“发送同步请求”，此操作会在选中“设备”节点中的移动设备时显示在功能区中。

- **Windows Defender 配置设置**

  现在可以在 Configuration Manager 控制台中，使用配置项目在注册有 Intune 的 Windows 10 计算机上配置 Windows Defender 客户端设置。 配置项目中有一个新设置组，名为 **Windows Defender**。 请注意，此设置组只在 Windows 10 1511 版及更高版本中受支持。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

2016 年 8 月版本的 Configuration Manager (Current Branch) 中没有新增的混合功能。

## <a name="september-2016"></a>2016 年 9 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2016 年 9 月推出的以下 Intune 功能适用于混合部署。

- **Android 公司门户中添加的“通知”**

  Android 公司门户主页上添加了一个新的“通知”图标。 点击此图标可访问“通知”页面，其中会显示在公司门户应用中需要引起注意的最终用户的所有项目，如设备不合规、注册更新和注册激活。 iOS 公司门户应用中已提供此“通知”体验。 有了新的“通知”页面，意味着只要设备已注册，用户就不会在每次启动或继续使用公司门户时看到公司访问设置。 如果创建了自己的最终用户指南，可能需要更新文档才能反映此更改。 在[此处](https://aka.ms/androidcpupdate)查找更新的屏幕截图。

- **iOS 公司门户应用的支持中的更改**

  iOS 的 Microsoft Intune 公司门户应用的所有用户现在都需要使用最新版本。 新用户只能下载最新版本，当前用户需要更新到最新版本。 最新版本需要 iOS 8.0 或更高版本，因此运行较旧 iOS 版本的设备不能使用公司门户或注册，直到将设备更新到 iOS 8.0 或更高版本，然后再将公司门户应用更新到最新版本。 运行 iOS 8.0 以下版本的已注册设备将继续由 Intune 管理控制台进行管理并在其中列出。

- **已添加到 Windows Phone 8.1 公司门户应用的“反馈”按钮**

  Windows Phone 8.1 公司门户应用使最终用户能利用新的“发送反馈”按钮发送关于应用的反馈。 用户可以点击公司门户应用屏幕右下角的 ... 菜单找到此按钮，然后点击“发送反馈”。 收集的匿名反馈将有助于 Microsoft 改进用户的公司门户应用体验。

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Configuration Manager Technical Preview 1609 中的新增功能

Configuration Manager Technical Preview 1609 的 2016 年 9 月版本中引入了以下新增的混合功能。

- **配置项目设置的其他设置和改进的体验**

  Android、iOS 和 Windows 中已添加了新设置，并且只有适用于你在“支持的平台”页选择的平台的设置才会在向导中显示。 有关详细信息，请参阅 [TP 1609 中配置项目的新符合性设置](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items)。

- **DEP 配置文件的其他设置**

  已将 TouchID、ApplePay 和缩放功能作为可配置设置添加到 iOS 设备的 DEP 配置文件中。

- **适用于企业的 Windows 应用商店中的付费应用**

  现在可将付费和免费应用程序均添加到适用于企业的 Windows 应用商店，并将它们部署给组织中的用户。 有关详细信息，请参阅 [TP 1609 中适用于企业的 Windows 应用商店的增强功能](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager)。

- **Windows 10 VPN 配置文件的本机连接类型**

  现在可在 Configuration Manager 控制台中为 MDM 创建具有 Microsoft Automatic、IKEv2 和 PPTP 连接类型的 Windows 10 VPN 配置文件，而无需使用 OMA-URI。

- **Intune 合规性图表**

  可使用监视工作区下的新图表快速查看整体的设备合规性情况和不合规的主要原因。 有关详细信息，请参阅 [TP 1609 中的 Intune 合规性图表](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts)。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

2016 年 9 月推出的以下新功能适用于 Microsoft Intune 和 Configuration Manager 1606 版 (Current Branch) 的混合部署。

- **iOS 10 支持**

  如果有针对所有 iOS 平台的配置文件或配置项目，也会将它们推送到 iOS 10。 我们还发布了对 Configuration Manager 1606 版的更新，允许用户将配置文件和配置项目用于 iOS 平台，包括 iOS 10。 可在 Configuration Manager 管理控制台中，转到“管理”>“概述”>“云服务”>“更新与服务”来安装此更新。 可以在 [https://support.microsoft.com/kb/3192616](https://support.microsoft.com/kb/3192616) 找到有关此更新的详细信息。

## <a name="august-2016"></a>2016 年 8 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2016 年 8 月推出的以下 Intune 功能适用于混合部署。

- **Android 7 的公司门户应用支持**

  Android 版 Intune 公司门户应用为即将推出的移动设备的 Android 7.0 操作系统提供“零日”支持。

- **Google 将删除 Android 7.0 设备中的远程密码重置功能**

  Google 即将删除 IT 管理员和最终用户远程重置 Android 7.0 设备密码的功能。 以前，IT 管理员可以远程重置用户的密码，最终用户也可以从其公司门户网站重置密码。

- **Samsung KNOX 标准版设备允许和阻止的应用策略**

  现可以配置适用于 Samsung KNOX 标准版设备的自定义策略，可通过此策略创建以下内容之一：

  - 禁止在设备上运行的应用列表。 即使已安装，在阻止列表中定义的应用也不能在设备上激活。
  - 允许设备用户从 Google Play 商店安装的应用列表。 不能从该应用商店安装任何其他应用。

  只有运行 Samsung KNOX 标准版的设备才可以使用这些设置。 有关详细信息，请参阅[使用自定义策略允许和阻止 Samsung KNOX 标准版设备适用的应用](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps)。

- **从公司门户到 Microsoft 的反馈链接**

   公司门户网站使最终用户能够点击页面底部的新“反馈”链接，向 Microsoft 发送有关网站体验的反馈。 收集到的匿名反馈将有助于 Microsoft 改进用户的公司门户网站体验。

- **最低 iOS Managed Browser 版本（已更新到 8.0）**

  用于 iOS 的 Microsoft Intune Managed Browser 应用已更新为支持运行 iOS 8.0 或更高版本的设备。 虽然 iOS 7.1 设备仍可使用现有的 Managed Browser 应用，但鼓励你的用户更新到 iOS 8.0 或更高版本，以访问并充分利用新的 Managed Browser 功能。

### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview 中的新增功能

2016 年 8 月版本的 Configuration Manager Technical Preview 中没有新增的混合功能。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

2016 年 8 月版本的 Configuration Manager (Current Branch) 中没有新增的混合功能。

## <a name="july-2016"></a>2016 年 7 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2016 年 7 月推出的以下 Intune 功能适用于混合部署。

- **用于 Intune 应用的 Xamarin SDK 已可用**

  Intune App SDK Xamarin 组件使用户能在使用 Xamarin 生成的移动 iOS 和 Android 应用中启用 Intune 移动应用管理功能。 可在 [Xamarin 应用商店](https://components.xamarin.com/view/Microsoft.Intune.MAM)或 [Microsoft Intune Github 页面](https://github.com/msintuneappsdk)中找到该组件。

- **改进了注册 Windows 设备时的最终用户体验**

  使用条件性访问时，Windows 8.1、Windows 10 桌面版和 Windows 10 移动版的注册步骤已在公司门户网站中阐明。 用户现在可以看到单独的“设备注册”和“工作区加入”步骤，如果他们遇到了“工作区加入(WPJ)”失败，便可更轻易地看到设备的状态并完成此过程。 这些步骤还有望简化 IT 管理员的故障排除过程。 以前，当最终用户尝试注册并成功完成 WPJ 以外的所有步骤时，已注册的设备将不会出现在设备列表中供用户识别，导致用户困惑。

  - **Windows 10 设备中现已提供完全擦除功能**

    可以擦除注册为移动设备的 Windows 10 电脑和笔记本，目的是将设备重置为出厂设置。 有关详细信息，请参阅[如何使用远程擦除保护设备](/sccm/mdm/deploy-use/wipe-lock-reset-devices)。

- **对 iOS 公司门户应用中的设备注册管理器帐户所做的更改**

  为了提高性能和可扩展性，Intune 不再在 iOS 公司门户应用的“我的设备”窗格中显示所有设备注册管理器 (DEM) 设备。 只会显示运行该应用的本地设备，并且要求设备已通过公司门户应用注册。

  DEM 用户可以在本地设备上执行操作，但只能从 Intune 管理控制台对其他注册设备执行远程管理。 此外，Intune 即将弃用 DEM 帐户，而改用 Apple 设备注册计划或 Apple Configurator 工具。 这两种注册方法均支持共享 iOS 设备的无用户注册。

  仅在共享设备无法使用无用户注册时才使用 DEM 帐户。 有关详细信息，请参阅[使用 Microsoft Intune 中的设备注册管理器注册企业自有设备](../deploy-use/enroll-devices-with-device-enrollment-manager.md)。

- **Android 公司门户应用的更改**

  如果 Android 最终用户看到错误消息，指示用户设备缺少所需的证书，则用户可以点击“如何解决此问题”按钮获取安装所缺证书的步骤。 如果用户完成了这些步骤，但看到了其他的“缺少证书”错误消息，系统会要求用户联系其 IT 管理员，并会提供此链接，其中包含 IT 管理员用于解决证书问题的步骤。

- **限制向已注册的 Android 设备安装端加载应用**

  Android 设备不能再通过公司门户网站安装应用程序，除非已使用适用于 Android 的 Intune 公司门户应用在 Intune 中注册该设备。


### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview 中的新增功能

2016 年 7 月版本的 Configuration Manager Technical Preview 中没有新增的混合功能。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

以下功能以前可在 Configuration Manager Technical Preview 版本中使用，现在可在 Intune 和 Configuration Manager (Current Branch) 1606 版本的混合部署中使用。

* 从 Configuration Manager 控制台查找、管理和分发用于 Windows 10 设备的适用于企业的 Windows 应用商店应用 ([1604](#new-in-1604-technical-preview))
* 适用于 Android 设备的 SmartLock 设置 ([1604](#new-in-1604-technical-preview))
* Windows 10 设备的应用触发的 VPN ([1605](#new-in-1605-technical-preview))
* 远程设备操作的新体验 ([1605](#new-in-1605-technical-preview))
* 适用于企业的 Windows 应用商店应用 ([1605](#new-in-1605-technical-preview))
* 批量采购应用的一般改进 ([1605](#new-in-1605-technical-preview))
* Windows 信息保护 (WIP) ([1605](#new-in-1605-technical-preview))
* 预声明具有 IMEI 或 iOS 序列号的企业自有设备 ([1605](#new-in-1605-technical-preview))
* 自动将设备分类到集合 ([1606](#new-in-1606-technical-preview))

有关新功能的信息，请参阅指定的 Technical Preview 版本的文档。

## <a name="june-2016"></a>2016 年 6 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能
2016 年 6 月推出的以下 Intune 功能适用于混合部署。

- **Intune 服务运行状况**：Intune 的服务运行状况信息已与其他 Microsoft 服务一起移到了中央位置。 你现在可以在 "服务运行状况" 下的 "Microsoft 365 管理中心" 中找到此信息。 有关详细信息，请参阅此[博客文章](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/)。

- **增强的 Windows 10 企业数据策略配置体验**

  Intune 现已改进了配置 Windows 10 信息保护策略的体验。 改进的内容包括以更好的方式创建应用规则，指定网络边界定义以及其他 Windows 信息保护设置。 若要了解详细信息，请参阅[使用 Microsoft Intune 创建 Windows 信息保护 (WIP) 策略](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune)。

- **Intune 的 Cisco ISE 网络访问控制策略**

  同时使用 Cisco 标识服务引擎 (ISE) 2.1 和 Microsoft Intune 的客户可在 ISE 中设置网络访问控制策略。如果使用此策略，在可以访问需要使用 WiFi 或 VPN 连接到网络的设备之前，这些设备则必须满足以下条件：

  - 必须由 Intune 管理
  - 必须符合任何已部署的 Intune 合规性策略

  系统将提示不合规设备的最终用户先进行注册并修正任何合规性问题，才能获得访问权限。

- **浏览器的条件性访问**

  可以为 Exchange Online 和 SharePoint Online 设置条件性访问策略，使用户仅能够从受管理且合规的 iOS 和 Android 设备上受支持的 Web 浏览器中访问它们。 系统将提示尝试使用 iOS 和 Android 设备登录 Outlook Web Access (OWA) 和 SharePoint 站点的最终用户先向 Intune 注册其设备并修正任何不合规的问题，才能完成登录。 有关详细信息，请参阅

  * [使用 Intune 限制对 Exchange Online 和新版 Exchange Online Dedicated 的电子邮件访问](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [使用 Microsoft Intune 限制对 SharePoint Online 的访问](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online 支持条件性访问**

  可以为 Dynamics CRM Online 设置条件性访问策略，使用户仅能够通过受管理且合规的 iOS 和 Android 设备访问它。 系统将提示尝试在 iOS 和 Android 设备上登录 Dynamics CRM 移动应用的最终用户先注册 Intune 并修正任何不合规的问题，才能完成登录。 有关详细信息，请参阅[使用 Microsoft Intune 限制对 Dynamics CRM Online 的电子邮件访问](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune)。

- **Android 公司门户应用的更新**

  Intune 现在拥有将影响 Android 公司门户用户的以下新策略：   

  策略  |对用户的影响  
  ---------|---------
  要求设备不允许安装来自未知源的应用 (Android 4.0+)     |  使用 Android 4.0 或更高版本的最终用户将看到“必须禁用来自未知源的安装”的消息。 用户需要在设备上转到“设置”>“安全”，然后关闭“未知源”。 用户可使用合规性消息中的链接获取有关此消息以及要求他们关闭此设置的原因的详细信息。
  要求设备不允许安装来自未知源的应用 (Android 4.0+)  |    使用 Android 4.0 或更高版本的最终用户将看到“扫描设备的安全威胁”的消息。 用户需要在设备上转到“设置”>“Google”>“安全”，然后打开“扫描设备的安全威胁”。 用户可使用合规性消息中的链接获取有关此消息以及要求他们打开此设置的原因的详细信息。     
  要求禁用 USB 调试 (Android 4.2+)  | 使用 Android 4.2 或更高版本的最终用户将看到“必须禁用 USB 调试”的消息。 用户需要在设备上转到“设置”>“开发人员选项”，然后关闭“USB 调试”。 用户可使用合规性消息中的链接获取有关此消息以及要求他们关闭此设置的原因的详细信息。
  最低 Android 安全修补程序级别 (Android 6.0+)  | 使用 Android 6.0 或更高版本设备的最终用户将看到“此设备不满足最低 Android 安全修补程序级别”的消息。 用户需要安装所需的安全修补程序。 用户可使用合规性消息中的链接获取有关如何安装所需的安全修补程序以及如何查看当前安装的安全修补程序的信息。

- **iOS 公司门户应用的更新**

  * 现在当最终用户安装业务线应用时，能感受改进的应用安装体验。 如果应用安装费时较长，用户可以手动同步设备以强制同步过程继续进行。 若要查看最终用户说明，请参阅“手动同步 iOS 设备”。
  * 适用于 iOS 的 Microsoft Intune 公司门户应用已更新，可支持 iOS 8.0 和更高版本。 此更新意味着仅当设备正在运行 iOS 8.0 或更高版本时，最终用户才可安装公司门户应用并在 Intune 中注册新设备。 如果用户已注册运行不受支持的 iOS 版本的设备，则这些用户可以继续使用其设备上的公司门户应用。


### <a name="new-in-1606-technical-preview"></a>Technical Preview 1606 中的新增功能
2016 年 6 月推出的以下新功能可用于 Intune 和 Configuration Manager Technical Preview 1606 的混合部署。

- **自动将设备分类到集合**

  可以创建设备类别，可将其用于配合使用 Intune 和 Configuration Manager 时自动在设备集合放置中。 然后要求用户在 Intune 中注册设备时选择某个设备类别。 此外，还可以从 Configuration Manager 控制台中更改设备的类别。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1606 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1606)中的[自动将设备分类到集合](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category)。

  > [!IMPORTANT]
  > 此功能适用于 2016 年 6 月版本的 Microsoft Intune。 试用这些过程前，请确保已更新到此版本。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能
2016 年 6 月版本的 Configuration Manager (Current Branch) 中没有新增的混合功能。

##  <a name="may-2016"></a>2016 年 5 月  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能  
 2016 年 5 月推出的以下 Intune 功能适用于混合部署。

- @NO__T 0MAM SDK：支持 PIN 长度配置 @ no__t-0

  与设备 PIN 类似，现在可指定 MAM 应用的 PIN 长度。 这要求最终用户符合所设置的新限制。 同时，对 PIN 屏幕稍微进行了修改，以满足较长输入的需要。 有关详细信息，请参阅[适用于 Android 的 MAM 策略设置](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings)和[适用于 iOS 的 MAM 策略设置](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings)。  

- **适用于 iOS 和 Android 的 Skype for Business**

  现在，[无需注册策略即可针对 Skype for business 使用 MAM](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune)。 在用户登录后，系统将应用 MAM 策略。  

- **可使用 MAM 策略管理的新应用**

  适用于 Android 的 Microsoft Word、Excel 和 PowerPoint 应用现在可与未注册 Intune 的设备上的 MAM 策略相关联。 有关受支持应用的完整列表，请转到 [Microsoft Intune 应用程序合作伙伴](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx)页面上的 Microsoft Intune 移动应用程序库。  

- @no__t 0Android 公司门户应用：最终用户 toast 通知 @ no__t-0

  最终用户在公司门户中注册设备或从中删除设备时，会显示来自 Android 公司门户应用的 Toast 通知。  

- @no__t 0Company 门户网站：设备标识横幅将向最终用户提供详细信息 @ no__t-0

  现在当最终用户使用公司门户网站时，可以更轻松地识别其所选的设备。 如果选择了错误的设备，可以通过点击主页横幅中的“点击此处”链接选择正确设备。  


### <a name="new-in-1605-technical-preview"></a>Technical Preview 1605 中的新增功能  
 2016 年 5 月推出的以下新功能可用于 Intune 和 Configuration Manager Technical Preview 1605 的混合部署。 用户需要使用 Configuration Manager 控制台来配置和管理这些功能。  

- **Windows 10 设备的应用触发的 VPN**

  对于配合使用 Configuration Manager 和 Intune 管理的 Windows 10 设备，可添加一个应用列表，此列表可自动打开通过 Configuration Manager 管理控制台配置的 VPN 连接。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1605 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1605)中的[Windows 10 设备的应用触发的 VPN](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **远程设备操作的新体验**

  已改进从 Configuration Manager 控制台执行远程设备操作的体验。

  现在，常见操作（如“停用/擦除”、“重置密码”、“远程锁定”和“绕过激活锁定”）可在从“资产和合规性”工作区访问的“远程设备操作”菜单中找到

  有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1605 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1605)中的[远程设备操作的新体验](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_Remote)。  

- **适用于企业的 Windows 应用商店应用**

  在[适用于企业的 Windows 应用商店](https://www.microsoft.com/business-store)中可以为组织查找并采购应用（单个或批量）。 通过将应用商店连接到 Configuration Manager，可从 Configuration Manager 控制台管理批量采购的应用。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1605 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1605)中的[适用于企业的 Windows 应用商店应用](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_WSFB)。  

- **批量采购应用的一般改进**

  从适用于企业的 Windows 应用商店和 iOS 应用商店批量采购的应用已合并为同一个视图，即**应用商店应用的许可证信息**。 此外，已改进了创建适用于 iOS 的批量采购的应用的方式。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1605 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1605)中的[批量采购应用的一般改进](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_VPP2)。  

- **预声明具有 IMEI 或 iOS 序列号的公司拥有的设备**

  现在，可通过导入公司拥有的设备的国际移动设备识别 (IMEI) 码对此类设备进行识别。 可上传包含设备 IMEI 码的逗号分隔值 (.csv) 文件，或者手动输入设备信息。  还可以导入 iOS 设备的序列号。  有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1605 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1605)中的[预声明具有 IMEI 或 iOS 序列号的公司拥有的设备](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI)。  

- **Windows 信息保护 (WIP)**

  可以创建配置项目来部署 Windows 信息保护 (WIP) 策略，包括允许选择受保护的应用、WIP 保护级别以及在网络上查找企业数据的方法。 有关 WIP 的详细信息，请参阅下列主题：  

  -   [使用 Windows 信息保护 (WIP) 保护企业数据](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [使用 System Center Configuration Manager 创建和部署 Windows 信息保护 (WIP) 策略](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能  
 2016 年 5 月版本的 Configuration Manager (Current Branch) 中没有新增的混合功能。  

##  <a name="april-2016"></a>2016 年 4 月  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能  
 2016 年 4 月推出的以下 Intune 功能适用于混合部署。  

- **MAM 用户合规性**

  现在可以在 Azure Active Directory (AAD) 租户中查看所有用户的应用程序管理策略的状态。  有关详细信息，请参阅 Intune 库中的[使用 Microsoft Intune 监视移动应用管理策略](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)。  

- **防止 Outlook 联系人进行同步的 MAM 控件 (Android)**

  现在提供了一个可防止应用程序将联系人同步到 Android 设备上的本机通讯簿的新设置。 此新设置最初由 Android 设备上的 Outlook 应用程序支持。 有关详细信息，请参阅 Intune 库中的[使用 Microsoft Intune 创建和部署移动应用管理策略](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)。  

- **公司门户网站的改进**

  现在当 Windows 10 移动版和 Windows Phone 8.1 用户安装业务线应用时，将显示以下的新状态，这些状态可为他们提供有关安装状态的详细信息：  

  -   **正在等待设备同步** – 用户已点击了“安装”，现在设备将尝试与 Intune 基础结构进行同步。 必须进行同步才能完成安装。 “正在等待设备同步”消息也是一个链接，用户可点击此链接查看在同步过程耗时较长或停止的情况下如何将设备与 Intune 手动同步的相关说明。  

  -   **正在下载** – 正在处理用户的下载请求，并且设备正在下载和安装应用。  

- **Android 公司门户应用的改进**

  未在 Intune 中注册设备以及未安装正确证书的用户将无法登录 Android 公司门户应用，并且将看到“由于设备缺少所需证书，因此无法登陆”的消息。 该消息包含“如何解决此问题”的链接，用户可点击此链接查看安装证书的相关说明。 若要查看最终用户解决此问题需要遵循的步骤，请参阅 Intune 库中的[设备缺少所需证书](/intune/enduser/using-your-android-device-with-intune)。  

- **iOS 公司门户应用的改进**

  添加了对使用“下拉以刷新”操作刷新主屏幕上的内容的支持，这些内容包括列出的应用、列出的设备和 IT 联系人信息。 “下拉以刷新”操作不会检查合规性或策略信息，可通过选择当前设备的磁贴并点击“同步”按钮以检查这些信息。  

- **Windows 10 移动版和 Windows Phone 8.1 公司门户应用的改进**

  现在当最终用户安装业务线应用时，能感受改进的应用安装体验。 如果应用安装费时较长，用户可以手动同步设备以强制同步过程继续进行。 若要查看最终用户说明，请参阅 Intune 库中的[手动同步设备以加快应用安装速度](/intune/enduser/using-your-windows-device-with-intune)。  

###  <a name="new-in-1604-technical-preview"></a>Technical Preview 1604 中的新增功能
 2016 年 4 月推出的以下新功能可用于 Intune 和 Configuration Manager Technical Preview 1604 的混合部署。 用户需要使用 Configuration Manager 控制台来配置和管理这些功能。  

- **从 Configuration Manager 控制台查找、管理和分发用于 Windows 10 设备的适用于企业的 Windows 应用商店应用**


  Configuration Manager Technical Preview 1604 中提供对适用于企业的 Windows 应用商店的支持，以帮助查找和管理应用，并将其分发到所管理的 Windows 10 设备。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1604 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1604)中的[管理从适用于企业的 Windows 应用商店批量采购的应用](/sccm/core/get-started/capabilities-in-technical-preview-1604#BKMK_WindowsVPP)。  

- **适用于 Android 设备的 SmartLock 设置**

  已向“Android 和 Samsung KNOX 标准版”配置项目添加了一个新设置，通过此设置可在兼容的 Android 设备上控制 SmartLock 功能。  可以使用此设置防止最终用户配置 SmartLock。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1604 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1604)中的[适用于 Android 设备的 SmartLock 设置](/sccm/core/get-started/capabilities-in-technical-preview-1604#BKMK_Smart)。  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能  
 2016 年 4 月版本的 Configuration Manager (Current Branch) 中没有新增的混合功能。  

##  <a name="march-2016"></a>2016 年 3 月  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能  
 2016 年 3 月推出的以下 Intune 功能适用于混合部署。  

- **防止 Outlook 联系人进行同步的 MAM 控件 (iOS)**

  现在提供了一个可防止应用程序将联系人同步到 iOS 设备上的本机通讯簿的新设置。 此新设置由 iOS 设备上的 Outlook 应用程序支持。 有关此设置和其他设置的详细信息，请参阅 Intune 库中的[创建和部署 MAM 策略](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)。  

- **Skype for Business Online 支持条件性访问**

  可以为 Skype for Business Online 设置条件性访问策略，使用户仅能够通过受管理且合规的 iOS 和 Android 设备访问它。  有关详细信息，请参阅 Intune 库中[管理 Skype for Business Online 的访问权限](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune)。  

- **对 iOS 9.3 的支持**

  3 月 21 日星期一，Apple 宣布推出 iOS 9.3。 如果用户将设备升级到 iOS 9.3，当前用于管理 iOS 设备的所有现有 Intune 功能将继续无缝地工作。  

- **公司门户网站直接提供 Windows 应用包**

  Windows 8、Windows 8.1 和 Windows RT 电脑的用户现在可直接从公司门户网站安装 Windows 应用包（扩展名为 .appx）。 而以前则必须进行部署，或者用户必须在其设备上先安装公司门户应用才能安装应用。  

- **用户可以从公司门户网站远程锁定设备**

  新的“远程锁定”选项已添加到公司门户网站，此选项使用户可在设备丢失或被盗的情况下从门户远程锁定其设备。  

- **充分利用 iOS“Open-in”管理对在第三方 MDM 解决方案中注册的设备进行管理**

  可以使用第三方移动设备管理 (MDM) 供应商以充分利用 iOS“Open-In”管理。 可在配置文件设置中设置限制，并使用 MDM 软件部署应用。 当用户安装托管应用时，会应用限制。 阅读详细信息：[Microsoft Intune 移动应用管理策略和 iOS](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune)在 Intune 库中打开。  

- **支持 MAM 的 Microsoft 应用**

  适用于 Intune 移动应用程序管理策略的 Microsoft 应用列表已更新，其中包括最新的应用（仅针对已注册了 Intune 的设备）。  

- **将适用于 Microsoft Intune 的 Adobe Reader 部署到企业中由 Intune 管理的 iOS 设备**

  现在，可使用 Intune 移动应用程序管理策略在注册设备上管理适用于 iOS 的 Adobe Reader 应用。  

- Android 支持 Rights Management 共享应用

  IT 管理员可部署移动应用程序管理策略，使最终用户能够更安全地查看图像、AV 和 PDF 文件，无论 IT 是否使用 Intune 管理设备都是如此。  

- **Android 和 iOS 公司门户应用的改进**

  -   用户启动由移动应用程序管理 (MAM) 管理的应用时，他们将看到此应用由公司管理的通知消息。 用户现在可点击“了解详细信息”链接以了解有关“受管理应用”含义的详细信息。 还可点击“不再显示”，使以后启动应用时不再显示此消息。  

  -   已添加新屏幕以在注册过程中为用户提供指导，并提供有关用户应注册的原因，以及 IT 管理员在他们已注册的设备上可以查看和无法查看的内容的详细信息。  

  -   现在，在公司门户应用中会显示注册错误消息。  

### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview 中的新增功能  
 2016 年 3 月版本的 Configuration Manager Technical Preview 中没有新增的混合功能。  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能  
 2016 年 3 月推出的以下新功能可用于 Intune 和 Configuration Manager (Current Branch) 版本 1602 的混合部署。 用户需要使用 Configuration Manager 控制台来配置和管理这些功能。  

- **iOS 应用配置策略**

  在 Configuration Manager (Current Branch) 的版本 1602 中，可使用应用配置策略以提供用户在运行 iOS 应用时可能需要的设置。 有关详细信息，请参阅[在 System Center Configuration Manager 中使用应用配置策略配置 iOS 应用](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies)。  

- **管理批量采购的 iOS 应用**

  在 Configuration Manager (Current Branch) 的版本 1602 中，可通过从应用商店 导入许可证信息并跟踪已用的许可证数量，帮助部署和管理通过 Apple Volume-Purchase Program (VPP) 批量采购的应用。 有关详细信息，请参阅[使用 System Center Configuration Manager 管理批量购买的 iOS 应用](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps)。  

- **自动创建 Office 移动应用**

  从 Configuration Manager (Current Branch) 的版本 1602 开始，在从版本 1511 进行升级时，会创建以下适用于 Android 和 iOS 的 Microsoft Office 移动应用：  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote（仅限 iOS）  
  -   Microsoft Outlook  

  可在 Configuration Manage 控制台的“应用程序”节点中找到这些应用。 关于部署应用程序的详细信息，请参阅[如何使用 System Center Configuration Manager 部署应用程序](../../apps/deploy-use/deploy-applications.md)。  

- **Android Samsung KNOX 标准版设备的展台模式设置**

  展台模式可让你锁定设备以只允许某些功能工作。  从 1602 版 Configuration Manager (Current Branch) 起，可为 Samsung KNOX 标准版设备指定展台模式设置。 有关详细信息，请参阅[如何为未使用 System Center Configuration Manager 客户端管理的 Android 和 Samsung KNOX 标准版设备创建配置项目](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)。  

- **iOS 激活锁定**

  从 Configuration Manager (Current Branch) 的版本 1602 开始，可管理 iOS 激活锁定，这是适用于 iOS 7.1 和更高版本设备的“查找我的 iPhone”应用的功能。 当设备上使用了“查到我的 iPhone”应用时，激活锁定自动启用。  有关详细信息，请参阅[绕过 System Center Configuration Manager 管理 iOS 激活锁定](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock)。  



## <a name="notices"></a>通知

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 配置 SP1 和 System Center 2012 R2 Configuration Manager （RTM）：支持混合移动设备管理，截止到2017年4月10日
2017 年 1 月 11 日

对 System Center 2012 Configuration Manager SP1 和 System Center 2012 R2 Configuration Manager RTM 的支持已于 2016 年 7 月 12 日终止。 随后，对与混合 MDM 的 Microsoft Intune 服务关联的这些版本的支持将于 2017 年 4 月 10 日终止。 在此之后，混合 MDM 将停止运行这些版本。 托管设备实质上将成为非托管设备，因为 Intune 连接器将无法再连接到 Intune 服务。 在升级发生前，Configuration Manager 数据（如策略和应用程序）将不会向上流入 Intune，托管设备数据将不会向下流入 Configuration Manager。

如果运行 Configuration Manager 2012 SP1 或 R2 RTM 的混合部署，建议在 2017 年 4 月 10 日前升级到 Configuration Manager (Current Branch) 或 Configuration Manager 2012（R2 SP1 或 SP2）的最新支持 Service Pack，以避免服务中断。

其他资源：
- [升级到 System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [计划升级到 System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
- [计划升级到 System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>已弃用的 Windows Phone 8 公司门户上传
2016 年 10 月 25 日

已从 Configuration Manager 控制台中删除上传已签名的公司门户应用这一功能，因为即将禁用对 Windows 8、Windows Phone 8 和 Windows RT 的 Intune 支持，并且对 Windows Phone 8 公司门户的支持也将在 11 月结束。  将继续支持已注册的 Windows 8、Windows Phone 8 和 Windows RT 设备，但不再支持使用这些平台注册其他设备。
