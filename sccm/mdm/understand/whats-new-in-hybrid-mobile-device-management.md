---
title: "Configuration Manager 的混合 MDM 中的新增功能 | Microsoft Docs"
description: "了解 Configuration Manager 和 Intune 的混合部署可用的新移动设备管理功能。"
ms.custom: na
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: ae008c91a7387ba76f2bfac13f8feb489a0cc558
ms.openlocfilehash: 0af5ae68353fcf1db846e2e27f3391fe87dcfc42
ms.contentlocale: zh-cn
ms.lasthandoff: 05/17/2017

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理中的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*

本文提供有关 System Center Configuration Manager 和 Microsoft Intune 的混合部署的可用的新移动设备管理 (MDM) 功能的详细信息。  

##  <a name="compatibility-with-configuration-manager-versions"></a>与 Configuration Manager 版本的兼容性  

 本文的每个部分都列出了混合功能，共 3 个不同类别。 请使用以下指南，确定每个类别中的功能与不同版本的 Configuration Manager 的兼容性：  

|功能类别|描述|
|-|-|
|**Microsoft Intune 中的新增功能** | 一般情况下，此类别列出的所有功能应适用于所有 Configuration Manager 版本（包括 System Center 2012 R2 Configuration Manager 版本），因为这些功能仅需要 Intune 服务，不需要 Configuration Manager 中的其他功能。|
|**Configuration Manager Technical Preview 中的新增功能**| 此类别下列出的所有功能仅适用于指定的 Technical Preview 版本。 若要试用这些功能，必须安装功能说明中指定的 Technical Preview 版本。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)。|
|**Configuration Manager (Current Branch) 中的新增功能**| 此类别下列出的所有功能仅适用于指定的 Configuration Manager (Current Branch) 版本，例如版本 1511 或 1602。 如果要为混合部署使用较旧版本的 Configuration Manager，则必须升级到功能说明中指定的 Configuration Manager (Current Branch) 版本。 有关详细信息，请参阅[升级到 System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。|

## <a name="april-2017"></a>2017 年 4 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **适用于 Managed Browser 的 MyApps**

  现在 Microsoft MyApps 改进了 Managed Browser 内部的支持。 不作为管理目标的 Managed Browser 用户将直接转至 MyApps 服务，这些用户可以在其中访问管理员预配的 SaaS 应用。 作为 Intune 管理目标的用户将可以继续从内置 Managed Browser 书签访问 MyApps。

- **Managed Browser 和公司门户的新图标**

  Managed Browser 将获得该应用的 Android 和 iOS 版的更新图标。 新图标将包含更新的 Intune 徽章，使其与企业移动性 + 安全性 (EM+S) 中的其他应用更为一致。 可以在 [Intune 应用 UI 页中的新增功能](/intune/whats-new/whats-new-in-intune-app-ui.md)中查看 Managed Browser 的新图标。

  公司门户还将获得该应用的 Android、iOS 和 Windows 版的更新图标，以改进与 EM+S 中的其他应用的一致性。 这些图标将于四月至五月底逐步在平台上发布。

- **Android 公司门户中的登录进度指示器**

  用户启动或重启应用时，Android 公司门户应用的更新程序将显示登录进度指示器。 允许用户访问应用前，指示器将经历以下新状态：开始是“正在连接...”，然后是“正在登录...”，接下来是“正在查看安全要求...”。 可以在 [Intune 应用 UI 页中的新增功能](/intune/whats-new/whats-new-in-intune-app-ui.md)中查看适用于 Android 的公司门户应用的新屏幕。

- **阻止应用访问 SharePoint Online**

  现在可以创建基于应用的条件访问策略来阻止未向其实施应用保护策略的应用访问 [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online)。 在基于应用的条件访问方案中，可以指定想要让其具备使用 Azure 门户访问 SharePoint Online 的权限的应用。

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Configuration Manager Technical Preview 1704 中的新变化

- **使用应用配置策略配置 Android 应用**

  当用户在 Android for Work 设备上运行应用时，可以在 System Center Configuration Manager (Configuration Manager) 中使用应用配置策略分发预配置的设置。 Android 应用配置策略仅适用于运行 Android for Work 的设备，并可应用于 Play for Work 商店中获批的应用。 若要了解如何试用此功能，请参阅[使用应用配置策略配置 Android 应用](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies)。

## <a name="march-2017"></a>2017 年 3 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **Android 适用的公司门户应用的最新用户体验**

  Android 适用的公司门户应用的用户界面具有更新式的外观。 值得注意的更新有：

  - 颜色：“公司门户”选项卡的颜色与 IT 定义的品牌颜色相同。
  - 应用：在“应用”选项卡中，更新了“特色应用”和“所有应用”按钮。
  - 搜索：在“应用”选项卡中，“搜索”按钮是浮动的操作按钮。
  - 导航应用：“所有应用”视图以选项卡形式呈现出“特色”、“所有”和“分类”视图，便于导航。
  - 支持：更新了“我的设备”和“联系 IT”选项卡，以改善可读性。

  有关这些更改的详细信息，请参阅 [Intune 最终用户应用的 UI 更新](/intune/whats-new/whats-new-in-intune-app-ui)。

- **Windows 10 公司门户的签名脚本**

  如果需要下载和旁加载 Windows 10 公司门户应用，现在可以使用脚本为你的组织简化应用签名过程。  若要下载该脚本及其使用说明，请参阅 TechNet 库中的 [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript)（Windows 10 公司门户适用的 Microsoft Intune 签名脚本）。 有关此公告的详细信息，请参阅 Intune 支持团队博客上的 [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/)（更新 Windows 10 公司门户应用）。

- **改进了对中国的 Android 用户的支持**

  由于中国地区没有 Google Play 商店，Android 设备必须从中国的应用商店获取应用。 公司门户通过重定向中国的 Android 用户，从本地应用商店下载公司门户和 Outlook 应用来支持此工作流。 启用条件性访问策略后，将同时改善有关移动设备管理和移动应用程序管理的用户体验。 以下中文应用商店可以提供 Android 适用的公司门户和 Outlook 应用：

  - [百度](https://go.microsoft.com/fwlink/?linkid=836946)
  - [小米](https://go.microsoft.com/fwlink/?linkid=836947)
  - [腾讯](https://go.microsoft.com/fwlink/?linkid=836949)
  - [华为](https://go.microsoft.com/fwlink/?linkid=836948)
  - [豌豆荚](https://go.microsoft.com/fwlink/?linkid=836950)

- **请确保公司门户应用处于最新状态**

  2016 年 12 月，我们发布了更新，当一组用户在注册 iOS、Android、Windows 8.1+ 或 Windows Phone 8.1+ 设备时，该更新将执行多重身份验证 (MFA)。 如果没有 Android (v5.0.3419.0+) 和 iOS (v2.1.17+) 适用的某些基准版本的公司门户应用，此功能将无法运行。

  Intune 的管理功能在不断改进，并且很多改进对所有支持平台上的公司门户应用的更新进行了协调。 因此，建议保留安装在设备上的最新版本的公司门户应用，以便利用 Intune 中的改进功能并获得最佳的用户体验。

  >[!Tip]
  > 让用户将其设备设置为从相应的应用商店中自动更新应用。 如果通过网络共享提供 Android 公司门户应用，则可从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=49140)下载最新版本。

- **Microsoft Teams 现已在 iOS 和 Android 上启用了 MAM**

  iOS 和 Android 适用的 Microsoft Teams 应用现已启用了 Intune 移动应用管理 (MAM) 功能，因此你可帮助团队跨设备自由工作，同时确保每个环节的对话和公司数据均受保护。 有关详细信息，请参阅企业移动性和安全性博客中的 [Microsoft Teams 公告](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/)。

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Configuration Manager Technical Preview 1703 中的新增功能

- **对 Apple Volume Purchase Program 方案的额外支持**

   从 Technical Preview 1703 开始，现可支持以下 Volume Purchase Program (VPP) 方案：

   - 设备许可 - 对于支持设备许可且部署到设备集合的应用，每个设备仅需要一个许可证。  以前，设备上每位用户都需要一个许可证。 有关详细信息，请参阅[将批量采购的 iOS 应用部署到设备集合](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections)。
   - 将多个 VPP 令牌用于单个混合租户，且同时将两个令牌均用于管理 VPP 应用。
   - 使用 VPP 教育令牌，且可区分企业和教育令牌。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

以下功能以前可在 Configuration Manager Technical Preview 版本中使用，现在可在 Intune 和 Configuration Manager (Current Branch) 1702 版本的混合部署中使用。

- [Android for Work 支持](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [针对不符合应用的符合性设置](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [PFX 证书创建和分发以及 S/MIME 支持](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [混合 MDM 的创建向导中，Android 和 iOS 版本不再作为目标](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Configuration Manager (Current Branch) 1702 版本中还包括以下其他混合功能：

- **对 Apple Volume Purchase Program (VPP) 改进的支持**

  - 你现在可以将已授权的应用部署到设备以及用户。 根据应用对设备授权的支持能力，合适的许可证将在部署时按以下方式声明：

    | Configuration Manager 版本 | 应用是否支持设备授权？ | 部署集合类型 | 已声明的许可证 |
    |-|-|-|-|
    |早于 1702|是|用户|用户许可证|
    |早于 1702|否|用户|用户许可证|
    |早于 1702|是|设备|用户许可证|
    |早于 1702|否|设备|用户许可证|
    |1702 及更高版本|是|用户|用户许可证|
    |1702 及更高版本|否|用户|用户许可证|
    |1702 及更高版本|是|设备|设备许可证|
    |1702 及更高版本|否|设备|用户许可证|

  - 此外，你现在可以部署并跟踪你从 iOS Volume Purchase Program 教育版购买的应用。

  - 你现在可以将多个 Apple 批量采购程序令牌与 Configuration Manager 相关联。

  有关批量购买的 iOS 应用的详细信息，请参阅[管理批量购买的 iOS 应用](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)。

- **对适用于企业的 Windows 应用商店中的业务线应用程序的支持**

  现在可以同步来自适用于企业的 Windows 应用商店的自定义业务线应用程序。

- **新移动威胁防御监视工具**

    现在你可以采用新的方法通过移动威胁防御服务提供程序来监视合规性状态。

    有关详细信息，请参阅[如何监视移动威胁防御合规性](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance)。

## <a name="february-2017"></a>2017 年 2 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **公司门户网站现代化**

  公司门户网站支持面向没有托管设备的用户的应用。 该网站使用新的对比色配色方案、动态插图和“汉堡菜单”（其中包含支持人员详细联系信息和现有托管设备的信息），这与其他 Microsoft 产品和服务保持一致。 对登录页面进行了重新组织，以突出用户可用的应用，并且会循环播放精选应用和最近更新的应用。 可在[“UI更新”](/intune/whats-new/whats-new-in-intune-app-ui)页面上找到前后对照的图片。

- **适用于 Windows 设备的新 MDM 服务器地址**

  用于注册 Windows 和 Windows Phone 设备的 MDM 服务器地址已从 manage.microsoft.com 更改为 enrollment.manage.microsoft.com。 注册 Windows 或/和 Windows Phone 设备时如果出现提示，请通知用户使用 enrollment.manage.microsoft.com 作为 MDM 服务器地址。 对于 DNS 中将 EnterpriseEnrollment.contoso.com 重定向到 manage.microsoft.com 的 CNAME，此更新还需要将其替换为 DNS 中将 EnterpriseEnrollment.contoso.com 重定向到 EnterpriseEnrollment-s.manage.microsoft.com 的 CNAME。 有关此更改的其他信息，请访问 http://aka.ms/intuneenrollsvrchange。

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Configuration Manager Technical Preview 1702 中的新增功能

- **Android for Work 支持**

  在使用 Configuration Manager Technical Preview 1702 的混合 MDM 环境中，现可使用 Android for Work 管理 Android 设备。 受支持的 Android 设备现可注册为 Android for Work 设备，从而在相关设备上创建工作配置文件，其中可在该设备上部署 Play for Work 批准的应用。 还可为这些设备配置和部署配置项、符合性策略和资源访问配置文件。 有关详细信息，请参阅 [Android for Work 支持](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support)。

- **针对不符合应用的符合性设置**

  现可在符合性策略中创建面向 Android 和 iOS 应用的不符合应用规则。 如果设备安装了指定应用程序，则根据部署的条件性访问策略，它们将被标记为“不符合”且不可再访问公司资源。 有关详细信息，请参阅[条件性访问设备符合性策略改进](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements)。

- **PFX 证书创建和分发以及 S/MIME 支持**

  现可在混合环境中为用户创建和部署 PFX 证书。 随后，这些证书可用于用户已注册的设备的 S/MIME 电子邮件加密和解密。 有关详细信息，请参阅[创建支持 S MIME 的 PFX 证书](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support)。

- **对其他 iOS 配置设置的支持**
   
    你现在有 42 个其他 iOS 设置，可配置为配置项的一部分。 已为受监督的 iOS 设备添加大部分设置（总共 35 个设置）。 有关详细信息，请参阅 [iOS 设备的新符合性设置](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices)。

## <a name="january-2017"></a>2017 年 1 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **Android 7.1.1 支持**

  Intune 现在完全支持并可管理 Android 7.1.1。

- **解决了以下问题：iOS 设备处于非活动状态，或管理控制台无法与其通信**

  如果用户设备与 Intune 失去联系，可向用户提供新的故障排除步骤，帮助其重新获得访问公司资源的权限。 请参阅[设备处于非活动状态，或管理控制台无法与其通信](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them)。

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Configuration Manager Technical Preview 1701 中的新增功能

- **混合 MDM 的创建向导中，Android 和 iOS 版本不再作为目标**

  从用于混合移动设备管理 (MDM) 的 Technical Preview 1701 开始，创建用于 Intune 托管设备的新策略和配置文件时，不再需要将特定版本的 Android 和 iOS 作为目标。 得益于此更改，混合部署可为新的 Android 和 iOS 版本更快地提供支持，无需新的 Configuration Manager 版本或扩展。 有关详细信息，请参阅 [Android 和 iOS 版本不再作为创建向导中的目标](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)。


## <a name="december-2016"></a>2016 年 12 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **注册移动到 Azure 门户时的多重身份验证**

  以前，你会转到 Intune 控制台或 Configuration Manager 控制台，以设置 MFA 用于 Intune 注册。 通过此更新的功能，现可使用 Intune 凭据登录 [Microsoft Azure 门户] (https://manage.windowsazure.com)，并通过 Azure AD 配置 MFA 设置。 若要了解详细信息，请参阅 [Microsoft Intune 的多重身份验证] (https://aka.ms/mfa_ad)。

- **Android 版公司门户应用现已在中国推出**

  Android 版公司门户应用现已在中国推出。 由于中国地区没有 Google Play 商店，Android 设备必须从中国的应用市场获取应用。 可从以下商店下载 Android 版公司门户应用：

  -    [百度](https://go.microsoft.com/fwlink/?linkid=836946)
  -    [华为](https://go.microsoft.com/fwlink/?linkid=836948)
  -    [腾讯](https://go.microsoft.com/fwlink/?linkid=836949)
  -    [豌豆荚](https://go.microsoft.com/fwlink/?linkid=836950)
  -    [小米](https://go.microsoft.com/fwlink/?linkid=836947)

  Android 版公司门户应用使用 Google Play Services 与 Microsoft Intune 服务进行通信。 由于 Google Play Services 尚未在中国推出，因此执行以下任何任务最长可能需要 8 个小时才能完成。

  | Configuration Manager 管理控制台 | Android 适用的 Intune 公司门户应用 | Intune 公司门户网站 |
  |----|----|----|        
  | 停用/擦除（删除所有数据）    | 删除远程设备 | 删除设备（本地和远程） |
  | 停用/擦除（删除公司数据）    | 重置设备 | 重置设备|
  | 新的或更新的应用部署 | 安装可用的业务线应用 | 设备密码重置|
  | 远程锁定    | | |
  | 密码重置 | | |        


## <a name="november-2016"></a>2016 年 11 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **适用于 Windows 10 设备的新 Microsoft Intune 公司门户**

  Microsoft 发布了一个新的[适用于 Windows 10 设备的公司门户应用](https://www.microsoft.com/store/apps/9wzdncrfj3pz)。 此应用利用了新 Windows 10 通用格式，可跨所有 Windows 10 设备（PC 和移动设备等）提供相同的更新用户体验，同时仍启用以前公司门户应用提供的所有相同功能。

  新应用可在 Windows 10 设备上利用平台功能，例如单一登录 (SSO) 和基于证书的身份验证。 此应用将作为对现有 Windows 8.1 公司门户和 Windows Phone 8.1 公司门户（安装自 Windows 应用商店）的升级而提供。 有关详细信息，请转到 [Intune 支持团队博客](http://aka.ms/intunecp_universalapp)。

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


## <a name="notices"></a>通知

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 和 System Center 2012 R2 Configuration Manager (RTM)：对混合移动设备管理的支持将于 2017 年 4 月 10 日终止

2017 年 1 月 11 日

对 System Center 2012 Configuration Manager SP1 和 System Center 2012 R2 Configuration Manager RTM 的支持已于 2016 年 7 月 12 日终止。 随后，对与混合 MDM 的 Microsoft Intune 服务关联的这些版本的支持将于 2017 年 4 月 10 日终止。 在此之后，混合 MDM 将停止运行这些版本。 托管设备实质上将成为非托管设备，因为 Intune 连接器将无法再连接到 Intune 服务。 在升级发生前，Configuration Manager 数据（如策略和应用程序）将不会向上流入 Intune，托管设备数据将不会向下流入 Configuration Manager。

如果运行 Configuration Manager 2012 SP1 或 R2 RTM 的混合部署，建议在 2017 年 4 月 10 日前升级到 Configuration Manager (Current Branch) 或 Configuration Manager 2012（R2 SP1 或 SP2）的最新支持 Service Pack，以避免服务中断。

其他资源：
-    [升级到 System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-    [计划升级到 System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-    [计划升级到 System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>已弃用的 Windows Phone 8 公司门户上传
2016 年 10 月 25 日

已从 Configuration Manager 控制台中删除上传已签名的公司门户应用这一功能，因为即将禁用对 Windows 8、Windows Phone 8 和 Windows RT 的 Intune 支持，并且对 Windows Phone 8 公司门户的支持也将在 11 月结束。  将继续支持已注册的 Windows 8、Windows Phone 8 和 Windows RT 设备，但不再支持使用这些平台注册其他设备。


### <a name="see-also"></a>另请参阅

- [以前的混合 MDM 功能](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager 中的 MDM 的新增功能](https://technet.microsoft.com/library/mt445560.aspx)

