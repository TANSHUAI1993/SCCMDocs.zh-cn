---
title: "存档 | 混合 MDM 的新增功能 | Microsoft Intune | System Center Configuration Manager"
description: "System Center Configuration Manager 和 Intune 的混合部署过去可用的移动设备管理功能的存档"
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: bfc4baefbdddc5125c38272f2087d214151c91d5
ms.openlocfilehash: 4c0910ae365e1fda7b9747b79e13782a6056c0da

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 和 Microsoft Intune 过去的混合功能

*适用范围：System Center Configuration Manager (Current Branch)*

本文提供有关 System Center Configuration Manager 和 Microsoft Intune 的混合部署过去可用的移动设备管理 (MDM) 功能的详细信息。  

##  <a name="compatibility-with-configuration-manager-versions"></a>与 Configuration Manager 版本的兼容性  

 本文的每个部分都列出了混合功能，共 3 个不同类别。 请使用以下指南，确定每个类别中的功能与不同版本的 Configuration Manager 的兼容性：  

|功能类别|
|-|  
|**Microsoft Intune 新增功能** - 一般情况下，此类别列出的所有功能应适用于所有 Configuration Manager 版本（包括 System Center 2012 R2 Configuration Manager 版本），因为这些功能仅需要 Intune 服务，不需要 Configuration Manager 中的其他功能。<br /><br /> **Configuration Manager Technical Preview 中的新增功能** - 此类别下列出的所有功能仅适用于指定的 Technical Preview 版本。 若要试用这些功能，必须安装功能说明中指定的 Technical Preview 版本。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)。<br /><br /> **Configuration Manager (Current Branch) 中的新增功能** - 此类别下列出的所有功能仅适用于指定的 Configuration Manager (Current Branch) 版本，例如版本 1511 或 1602。 如果要为混合部署使用较旧版本的 Configuration Manager，则必须升级到功能说明中指定的 Configuration Manager (Current Branch) 版本。 有关详细信息，请参阅[升级到 System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。|  

## <a name="new-hybrid-features-in-june-2016"></a>2016 年 6 月版本中的新增混合功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能
2016 年 6 月推出的以下 Intune 功能适用于混合部署。

- **Intune 服务运行状况**：Intune 的服务运行状况信息已与其他 Microsoft 服务一起移到了中央位置。 现在可在 Office 365 管理门户中的“服务运行状况”下找到此信息。 有关详细信息，请参阅此[博客文章](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/)。

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

  可以创建设备类别，可将其用于配合使用 Intune 和 Configuration Manager 时自动在设备集合放置中。 然后要求用户在 Intune 中注册设备时选择某个设备类别。 此外，还可以从 Configuration Manager 控制台中更改设备的类别。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1606 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1606.md)中的[自动将设备分类到集合](/sccm/core/get-started/capabilities-in-technical-preview-1606.md#dmp_category)。

  > [!IMPORTANT]
  > 此功能适用于 2016 年 6 月版本的 Microsoft Intune。 试用这些过程前，请确保已更新到此版本。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能
2016 年 6 月版本的 Configuration Manager (Current Branch) 中没有新增的混合功能。

##  <a name="new-hybrid-features-in-may-2016"></a>2016 年 5 月版本中的新增混合功能  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能  
 2016 年 5 月推出的以下 Intune 功能适用于混合部署。

- **MAM SDK：支持 PIN 长度配置**

  与设备 PIN 类似，现在可指定 MAM 应用的 PIN 长度。 这要求最终用户符合所设置的新限制。 同时，对 PIN 屏幕稍微进行了修改，以满足较长输入的需要。 有关详细信息，请参阅[适用于 Android 的 MAM 策略设置](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings)和[适用于 iOS 的 MAM 策略设置](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings)。  

- **适用于 iOS 和 Android 的 Skype for Business**

  现在，[无需注册策略即可针对 Skype for business 使用 MAM](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune)。 在用户登录后，系统将应用 MAM 策略。  

- **可使用 MAM 策略管理的新应用**

  适用于 Android 的 Microsoft Word、Excel 和 PowerPoint 应用现在可与未注册 Intune 的设备上的 MAM 策略相关联。 有关受支持应用的完整列表，请转到 [Microsoft Intune 应用程序合作伙伴](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx)页面上的 Microsoft Intune 移动应用程序库。  

- **Android 公司门户应用：最终用户 Toast 通知**

  最终用户在公司门户中注册设备或从中删除设备时，会显示来自 Android 公司门户应用的 Toast 通知。  

- **公司门户网站：设备标识横幅将为最终用户提供更多信息**

  现在当最终用户使用公司门户网站时，可以更轻松地识别其所选的设备。 如果选择了错误的设备，可以通过点击主页横幅中的“点击此处”链接选择正确设备。  


### <a name="new-in-1605-technical-preview"></a>Technical Preview 1605 中的新增功能  
 2016 年 5 月推出的以下新功能可用于 Intune 和 Configuration Manager Technical Preview 1605 的混合部署。 用户需要使用 Configuration Manager 控制台来配置和管理这些功能。  

- **Windows 10 设备的应用触发的 VPN**

  对于配合使用 Configuration Manager 和 Intune 管理的 Windows 10 设备，可添加一个应用列表，此列表可自动打开通过 Configuration Manager 管理控制台配置的 VPN 连接。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1605 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1605)中的[Windows 10 设备的应用触发的 VPN](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **远程设备操作的新体验**

  已改进从 Configuration Manager 控制台执行远程设备操作的体验。

  现在，常见操作（如“停用/擦除”、“重置密码”、“远程锁定”和“绕过激活锁定”）可在从“资产和合规性”工作区访问的“远程设备操作”菜单中找到

  有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1605 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1605)中的[远程设备操作的新体验](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions)。  

- **适用于企业的 Windows 应用商店应用**

  在[适用于企业的 Windows 应用商店](https://www.microsoft.com/en-us/business-store)中可以为组织查找并采购应用（单个或批量）。 通过将应用商店连接到 Configuration Manager，可从 Configuration Manager 控制台管理批量采购的应用。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1605 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1605)中的[适用于企业的 Windows 应用商店应用](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps)。  

- **批量采购应用的一般改进**

  从适用于企业的 Windows 应用商店和 iOS 应用商店批量采购的应用已合并为同一个视图，即**应用商店应用的许可证信息**。 此外，已改进了创建适用于 iOS 的批量采购的应用的方式。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1605 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1605)中的[批量采购应用的一般改进](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps)。  

- **预声明具有 IMEI 或 iOS 序列号的公司拥有的设备**

  现在，可通过导入公司拥有的设备的国际移动设备识别 (IMEI) 码对此类设备进行识别。 可上传包含设备 IMEI 码的逗号分隔值 (.csv) 文件，或者手动输入设备信息。  还可以导入 iOS 设备的序列号。  有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1605 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1605)中的[预声明具有 IMEI 或 iOS 序列号的公司拥有的设备](../../core/get-started/capabilities-in-technical-preview-1605.md#pre-declare-corporate-owned-devices-with-with-imei-or-ios-serial-number)。  

- **Windows 信息保护 (WIP)**

  可以创建配置项目来部署 Windows 信息保护 (WIP) 策略，包括允许选择受保护的应用、WIP 保护级别以及在网络上查找企业数据的方法。 有关 WIP 的详细信息，请参阅下列主题：  

  -   [使用 Windows 信息保护 (WIP) 保护企业数据](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [使用 System Center Configuration Manager 创建和部署 Windows 信息保护 (WIP) 策略](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能  
 2016 年 5 月版本的 Configuration Manager (Current Branch) 中没有新增的混合功能。  

##  <a name="new-hybrid-features-in-april-2016"></a>2016 年 4 月版本中的新增混合功能  

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


  Configuration Manager Technical Preview 1604 中提供对适用于企业的 Windows 应用商店的支持，以帮助查找和管理应用，并将其分发到所管理的 Windows 10 设备。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1604 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1604)中的[管理从适用于企业的 Windows 应用商店批量采购的应用](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business)。  

- **适用于 Android 设备的 SmartLock 设置**

  一个新设置已添加到“Android 和 Samsung KNOX”配置项目，此设置使用户可以在兼容的 Android 设备上控制 SmartLock 功能。  可以使用此设置防止最终用户配置 SmartLock。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview 1604 中的功能](/sccm/core/get-started/capabilities-in-technical-preview-1604.md)中的[适用于 Android 设备的 SmartLock 设置](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices)。  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能  
 2016 年 4 月版本的 Configuration Manager (Current Branch) 中没有新增的混合功能。  

##  <a name="new-hybrid-features-in-march-2016"></a>2016 年 3 月版本中的新增混合功能  

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

  可以使用第三方移动设备管理 (MDM) 供应商以充分利用 iOS“Open-In”管理。 可在配置文件设置中设置限制，并使用 MDM 软件部署应用。 当用户安装托管应用时，会应用限制。 请阅读 Intune 库中相关的详细信息：[Microsoft Intune 移动应用管理策略和 iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune)。  

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

- **Android Samsung KNOX 设备的展台模式设置**

  展台模式可让你锁定设备以只允许某些功能工作。  从 Configuration Manager (Current Branch) 的版本 1602 开始，现在可指定 Samsung KNOX 设备的展台模式设置。 有关详细信息，请参阅[如何为没有使用 System Center Configuration Manager 客户端管理的 Android 和 Samsung KNOX 设备创建配置项目](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)。  

- **iOS 激活锁定**

  从 Configuration Manager (Current Branch) 的版本 1602 开始，可管理 iOS 激活锁定，这是适用于 iOS 7.1 和更高版本设备的“查找我的 iPhone”应用的功能。 当设备上使用了“查到我的 iPhone”应用时，激活锁定自动启用。  有关详细信息，请参阅[绕过 System Center Configuration Manager 管理 iOS 激活锁定](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock)。  



<!--HONumber=Nov16_HO1-->


