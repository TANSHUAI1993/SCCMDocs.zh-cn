---
title: "Configuration Manager 的混合 MDM 中的新增功能 | Microsoft Docs"
description: "了解 Configuration Manager 和 Intune 的混合部署可用的新移动设备管理功能。"
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: "40"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 93609815ab4d93eddb99b8461dda9f4b4bf8058e
ms.sourcegitcommit: 9a6f8e028fb5eb2e752da70f42a5b548339bd8f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2017
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理中的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*

本文提供有关 System Center Configuration Manager 和 Microsoft Intune 的混合部署的可用的新移动设备管理 (MDM) 功能的详细信息。  

##  <a name="compatibility-with-configuration-manager-versions"></a>与 Configuration Manager 版本的兼容性  

 本文的每个部分都列出了混合功能，并按 3 个不同类别进行分类。 请使用以下指南，确定每个类别中的功能与不同版本的 Configuration Manager 的兼容性：  

|功能类别|描述|
|-|-|
|**Microsoft Intune 中的新增功能** | 一般情况下，此类别列出的所有功能应适用于所有 Configuration Manager 版本（包括 System Center 2012 R2 Configuration Manager 版本），因为这些功能仅需要 Intune 服务，不需要 Configuration Manager 中的其他功能。|
|**Configuration Manager Technical Preview 中的新增功能**| 此类别下列出的所有功能仅适用于指定的 Technical Preview 版本。 若要试用这些功能，必须安装功能说明中指定的 Technical Preview 版本。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)。|
|**Configuration Manager (Current Branch) 中的新增功能**| 此类别下列出的所有功能仅适用于指定的 Configuration Manager (Current Branch) 版本，例如版本 1511 或 1602。 如果要为混合部署使用较旧版本的 Configuration Manager，则必须升级到功能说明中指定的 Configuration Manager (Current Branch) 版本。 有关详细信息，请参阅[升级到 System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。|

## <a name="july-2017"></a>2017 年 7 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **针对 Android 和 Windows Phone 添加了不再支持的通知**

    针对不再支持 Android 和 Windows Phone 版本添加了新通知。 有关详细信息，请参阅[通知](#notices)。



### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

以下功能以前可在 Configuration Manager Technical Preview 版本中使用，现在可在 Intune 和 Configuration Manager (Current Branch) 1706 版本的混合部署中使用。

- [支持 Entrust 证书颁发机构](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [新移动应用程序管理策略设置](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Android for Work 共享配置更新](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [新设备符合性策略规则](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [不使用 Configuration Manager 客户端管理的 Windows 10 设备适用的新配置设置](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [macOS VPN 配置文件的 Cisco (IPSec) 支持](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Android 和 iOS 注册限制](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 

## <a name="june-2017"></a>2017 年 6 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **更改 MDM 机构**

  从 Configuration Manager 1610 版本和 Microsoft Intune 1705 版本开始，可以更改你的 MDM 机构而无需联系 Microsoft 支持部门，也无需取消注册并重新注册现有的托管设备。 有关详细信息，请参阅[更改 MDM 机构]( /sccm/mdm/deploy-use/change-mdm-authority)。

- **Managed Browser 和应用代理集成**

  Intune Managed Browser 现在可以与 Azure AD 应用程序代理服务集成，用户即使在远程工作时也可以访问内部网站。 浏览器的用户只需照常输入网站 URL，Managed Browser 会通过应用程序代理 Web 网关路由请求。 有关详细信息，请参阅[使用 Managed Browser 策略管理 Internet 访问权限](/intune/app-configuration-managed-browser)。

- **Android 公司门户应用现在提供全新的应用保护策略最终用户体验**

  根据客户反馈，我们修改了适用于 Android 的公司门户应用，现在显示“访问公司内容”按钮。 这样一来，如果最终用户只需访问支持应用保护策略（一项 Intune 移动应用管理功能）的应用，便无需完成不必要的注册过程。 在[应用 UI 中的新增功能](/intune/whats-new-app-ui)页上可以看到这些更改。

- **可轻松删除公司门户的新菜单操作**

  根据用户反馈，适用于 Android 的公司门户应用已添加一个新的菜单操作，用于从设备删除公司门户。 此操作可从 Intune 管理中删除设备，这样用户就可以从设备中删除应用。 有关这些更改，可以参阅[应用 UI 中的新增功能](/intune/whats-new-app-ui)页和 [Android 最终用户文档](/intune-user-help/unenroll-your-device-from-intune-android)。

- **对与 Windows 10 创意者更新之间的应用同步的改进**

  Windows 10 公司门户应用现在自动开始为安装了 Windows 10 创意者更新（版本 1703）的设备同步应用安装请求。 这会减少“挂起同步”状态期间出现的应用安装停止问题。 此外，用户还可以在应用中手动启动同步。 在[应用 UI 中的新增功能](/intune/whats-new-app-ui)页上可以看到这些更改。

- **Windows 10 公司门户的全新引导式体验**

  适用于 Windows 10 的公司门户应用为尚未进行标识或注册的设备提供引导式 Intune 演练体验。 新体验提供分步说明，指导用户完成注册到 Azure Active Directory（条件访问功能需要）和 MDM 注册（设备管理功能需要）的过程。 从公司门户主页可以进入引导式体验。 如果用户没有完成注册，仍可以继续使用应用，但可用功能受到限制。

  此更新仅在运行 Windows 10 周年更新（内部版本 1607）或更高版本的设备上可见。 在[应用 UI 中的新增功能](/intune/whats-new-app-ui)页上可以看到这些更改。

- **对适用于 iOS 的公司门户应用中的应用磁贴的改进**

  我们更新了主页上的应用磁贴设计，现在可以反映你为公司门户设置的品牌颜色。 有关详细信息，请参阅[应用 UI 中的新增功能](/intune/whats-new-app-ui)。

- **帐户选取器现在可用于适用于 iOS 的公司门户应用**

  如果用户使用其工作或学校帐户登录到其他 Microsoft 应用，则 iOS 设备用户在登录到公司门户时，可以看到我们的新帐户选取器。 有关详细信息，请参阅[应用 UI 中的新增功能](/intune/whats-new-app-ui)。

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Configuration Manager Technical Preview 1706 中的新增功能

- **新移动应用程序管理策略设置**    

  目前提供以下移动应用程序管理 (MAM) 策略设置：

  - 阻止屏幕捕获(仅限 Android 设备)：指定在使用该应用时，阻止设备的屏幕捕获功能。
  - 禁用联系人同步：阻止应用将数据保存到设备上的本机“联系人”应用。
  - 禁用打印：阻止应用打印工作或学校数据。

  请参阅[使用 Configuration Manager 中的应用保护策略来保护应用](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies)，尝试新的应用保护策略设置。

- **新 Windows 配置项设置**  <!-- 1354715 -->    

  新的 Windows 配置项适用于密码、设备、存储和 Microsoft Edge 设置类别。 有关详细信息，请参阅[新 Windows 配置项设置](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings)。

- **新设备符合性策略规则**    

  对于以前仅适用于 Intune 独立版本的符合性策略，现在可以为其配置新选项。 有关详细信息，请参阅[设备符合性策略改进](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules)。

- **Android 和 iOS 注册限制** <!-- 1290826 -->      

  管理员现在可以指定用户不能在其混合环境中注册个人 Android 或 iOS 设备。 这样一来，可以将注册的设备限制为预先声明的公司自有设备，或仅为注册了“设备注册计划”的 iOS 设备。 有关详细信息，请参阅 [Android 和 iOS 注册限制](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions)。

- **支持 Entrust 证书颁发机构** <!-- 1350740 -->     

  现在，Configuration Manager 可支持 Entrust 证书颁发机构；这使得 PFX 证书可传送到在 Microsoft Intune 中注册的设备。    

  在 Configuration Manager 中添加“证书注册点”角色时，你可以将 Entrust 配置为证书颁发机构。 在添加颁发 PFX 证书的新证书配置文件时，你可以选择 Microsoft 或 Entrust 证书颁发机构。

  已知问题：在 Technical Preview 1706 中，没有为 Microsoft 证书颁发机构颁发 PFX 证书。 这并不会影响导入的 PFX 证书或 SCEP 配置文件。

- **对 macOS VPN 配置文件的 Cisco (IPsec) 支持**  <!-- 1321367 -->    

  你可以使用 Cisco (IPsec) 作为连接类型创建 macOS VPN 配置文件。 有关详细信息，请参阅[创建 VPN 配置文件](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles)。


## <a name="april-2017"></a>2017 年 4 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **适用于 Managed Browser 的 MyApps**

  现在 Microsoft MyApps 改进了 Managed Browser 内部的支持。 不作为管理目标的 Managed Browser 用户将直接转至 MyApps 服务，这些用户可以在其中访问管理员预配的 SaaS 应用。 作为 Intune 管理目标的用户可以继续通过内置的 Managed Browser 书签访问 MyApps。

- **Managed Browser 和公司门户的新图标**

  Managed Browser 将获得该应用的 Android 和 iOS 版的更新图标。 新图标将包含更新的 Intune 徽章，使其与企业移动性 + 安全性 (EM+S) 中的其他应用更为一致。 可以在 [Intune 应用 UI 页中的新增功能](/intune/whats-new/whats-new-in-intune-app-ui.md)中查看 Managed Browser 的新图标。

  公司门户还将获得该应用的 Android、iOS 和 Windows 版的更新图标，以改进与 EM+S 中的其他应用的一致性。 这些图标将于四月至五月底逐步在平台上发布。

- **Android 公司门户中的登录进度指示器**

  将 Android 公司门户应用更新为在用户启动或恢复应用时显示登录进度指示器。 允许用户访问应用前，指示器将经历以下新状态：开始是“正在连接...”，然后是“正在登录...”，接下来是“正在查看安全要求...”。 可以在 [Intune 应用 UI 页中的新增功能](/intune/whats-new/whats-new-in-intune-app-ui.md)中查看适用于 Android 的公司门户应用的新屏幕。

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

  如果需要下载和旁加载 Windows 10 公司门户应用，现在可以使用脚本为你的组织简化应用签名过程。  若要下载该脚本及其使用说明，请参阅 TechNet 库中的 [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript)（Windows 10 公司门户适用的 Microsoft Intune 签名脚本）。 有关此公告的详细信息，请参阅 Intune 支持团队博客上的[更新 Windows 10 公司门户应用](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/)。

- **改进了对中国的 Android 用户的支持**

  由于中国地区没有 Google Play 商店，Android 设备必须从中国的应用商店获取应用。 公司门户通过重定向中国的 Android 用户，以便从本地应用商店下载公司门户和 Outlook 应用，从而支持此工作流。 启用条件访问策略后，这将同时提升有关移动设备管理和移动应用管理的用户体验。 以下中文应用商店可以提供 Android 适用的公司门户和 Outlook 应用：

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

   - 设备授权 - 对于支持设备授权且部署到设备集合的应用，现在每个设备只需一个许可证。  以前，设备上每位用户都需要一个许可证。 有关详细信息，请参阅[将批量采购的 iOS 应用部署到设备集合](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections)。
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

  - 你现在可以将已授权的应用部署到设备以及用户。 部署应用时，将声明相应的许可证（如下所示），具体视应用是否支持设备授权而定：

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

- **适用于企业的 Windows 应用商店支持业务线应用**

  现在，可以从适用于企业的 Windows 应用商店同步自定义业务线应用。

- **新移动威胁防御监视工具**

    现在，可以使用新方法通过移动威胁防御服务提供程序来监视符合性状态。

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

  现可在符合性策略中创建面向 Android 和 iOS 应用的不符合应用规则。 如果设备安装了指定应用，根据部署的条件访问策略，它们被标记为“不符合”，且不可再访问公司资源。 有关详细信息，请参阅[条件性访问设备符合性策略改进](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements)。

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


## <a name="notices"></a>通知

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>平台支持提醒：Windows Phone 8.1 主流支持将于 2017 年 7 月 11 日终止
<!-- 1327781 -->
*2017 年 7 月 11 日*

Windows Phone 8.1 平台的主流支持已终止。 Windows 8.1 PC 支持不会受到影响。

不会对 Intune 服务托管的任何 Windows Phone 8.1 设备产生直接影响，包括混合 MDM 中注册的设备。 注册的设备将继续工作，并且所有策略、配置和应用都将继续按预期方式工作。 请注意，不会针对 Intune 服务中的 Windows Phone 8.1 平台以及 Windows Phone 8.1 公司门户应用进行任何改进。

建议尽早将符合条件的 Windows Phone 8.1 设备升级到 Windows 10 移动版。  

### <a name="end-of-support-for-android-43-and-lower"></a>不再支持 Android 4.3 及更低版本
<!---1171127--->
2017 年 7 月 6 日

托管应用和 Android 公司门户应用将要求使用 Android 4.4 及更高版本，才能访问公司资源。 在 10 月初之前未更新的设备将无法再访问公司门户或这些应用。 截至 12 月，所有注册的设备都将在 12 月内被强制停用，进而将无法再访问公司资源。 如果在未启用 MDM 的情况下使用应用保护策略，应用将无法接收更新，应用体验质量将随着时间的推移而逐渐降低。


### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 和 System Center 2012 R2 Configuration Manager (RTM)：对混合移动设备管理的支持将于 2017 年 4 月 10 日终止
2017 年 1 月 11 日

对 System Center 2012 Configuration Manager SP1 和 System Center 2012 R2 Configuration Manager RTM 的支持已于 2016 年 7 月 12 日终止。 随后，对与混合 MDM 的 Microsoft Intune 服务关联的这些版本的支持将于 2017 年 4 月 10 日终止。 在此之后，混合 MDM 将停止运行这些版本。 托管设备实质上将成为非托管设备，因为 Intune 连接器将无法再连接到 Intune 服务。 在升级发生前，Configuration Manager 数据（如策略和应用程序）将不会向上流入 Intune，托管设备数据将不会向下流入 Configuration Manager。

如果运行 Configuration Manager 2012 SP1 或 R2 RTM 的混合部署，建议在 2017 年 4 月 10 日前升级到 Configuration Manager (Current Branch) 或 Configuration Manager 2012（R2 SP1 或 SP2）的最新支持 Service Pack，以避免服务中断。

其他资源：
-   [升级到 System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [计划升级到 System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [计划升级到 System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>已弃用的 Windows Phone 8 公司门户上传
2016 年 10 月 25 日

已从 Configuration Manager 控制台中删除上传已签名的公司门户应用这一功能，因为即将禁用对 Windows 8、Windows Phone 8 和 Windows RT 的 Intune 支持，并且对 Windows Phone 8 公司门户的支持也将在 11 月结束。  将继续支持已注册的 Windows 8、Windows Phone 8 和 Windows RT 设备，但不再支持使用这些平台注册其他设备。


### <a name="see-also"></a>另请参阅

- [以前的混合 MDM 功能](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager 中的 MDM 的新增功能](https://technet.microsoft.com/library/mt445560.aspx)
