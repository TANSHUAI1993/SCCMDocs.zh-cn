---
title: "混合 MDM 的新增功能 | Microsoft Docs"
description: "了解 System Center Configuration Manager 和 Intune 的混合部署可用的新移动设备管理功能。"
ms.custom: na
ms.date: 02/14/2017
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
translationtype: Human Translation
ms.sourcegitcommit: 7972aa2c39f5b86e69087b1ed5a1c3b50ba69940
ms.openlocfilehash: f74bd019b5403f3f5702795279759270261ce4db

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

## <a name="new-hybrid-features-in-february-2017"></a>2017 年 2 月版本中的新增混合功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2017 年 2 月推出的以下 Intune 功能适用于混合部署：

- **公司门户网站现代化**

  公司门户网站支持面向没有托管设备的用户的应用。 该网站使用新的对比色配色方案、动态插图和“汉堡菜单”（其中包含支持人员详细联系信息和现有托管设备的信息），这与其他 Microsoft 产品和服务保持一致。 对登录页面进行了重新组织，以突出用户可用的应用，并且会循环播放精选应用和最近更新的应用。 可在“UI更新”[](/intune/whats-new/whats-new-in-intune-app-ui)页面上找到前后对照的图片。

- **适用于 Windows 设备的新 MDM 服务器地址**

  用于注册 Windows 和 Windows Phone 设备的 MDM 服务器地址已从 manage.microsoft.com 更改为 enrollment.manage.microsoft.com。 注册 Windows 或/和 Windows Phone 设备时如果出现提示，请通知用户使用 enrollment.manage.microsoft.com 作为 MDM 服务器地址。 对于 DNS 中将 EnterpriseEnrollment.contoso.com 重定向到 manage.microsoft.com 的 CNAME，此更新还需要将其替换为 DNS 中将 EnterpriseEnrollment.contoso.com 重定向到 EnterpriseEnrollment-s.manage.microsoft.com 的 CNAME。 有关此更改的其他信息，请访问 http://aka.ms/intuneenrollsvrchange。 

## <a name="new-hybrid-features-in-january-2017"></a>2017 年 1 月版本中的新增混合功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2017 年 1 月推出的以下 Intune 功能适用于混合部署：

- **Android 7.1.1 支持**

  Intune 现在完全支持并可管理 Android 7.1.1。

- **解决了以下问题：iOS 设备处于非活动状态，或管理控制台无法与其通信**

  如果用户设备与 Intune 失去联系，可向用户提供新的故障排除步骤，帮助其重新获得访问公司资源的权限。 请参阅[设备处于非活动状态，或管理控制台无法与其通信](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them)。

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Configuration Manager Technical Preview 1701 中的新增功能

- **混合 MDM 的创建向导中，Android 和 iOS 版本不再作为目标**

  从用于混合移动设备管理 (MDM) 的 Technical Preview 1701 开始，创建用于 Intune 托管设备的新策略和配置文件时，不再需要将特定版本的 Android 和 iOS 作为目标。 得益于此更改，混合部署可为新的 Android 和 iOS 版本更快地提供支持，无需新的 Configuration Manager 版本或扩展。 有关详细信息，请参阅 [Android 和 iOS 版本不再作为创建向导中的目标](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)。


## <a name="new-hybrid-features-in-december-2016"></a>2016 年 12 月版本中的新增混合功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2016 年 12 月推出的以下 Intune 功能适用于混合部署：

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


## <a name="new-hybrid-features-in-november-2016"></a>2016 年 11 月版本中的新增混合功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2016 年 11 月推出的以下 Intune 功能适用于混合部署：

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


## <a name="see-also"></a>另请参阅

- [以前的混合 MDM 功能](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager 中的 MDM 的新增功能](https://technet.microsoft.com/library/mt445560.aspx)



<!--HONumber=Feb17_HO2-->


