---
title: "混合 MDM 中的新增功能"
titleSuffix: Configuration Manager
description: "了解 Configuration Manager 和 Intune 的混合部署可用的新移动设备管理功能。"
ms.custom: na
ms.date: 03/01/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3b48c5296caecd66b5abb6d40578af2009ef0f11
ms.sourcegitcommit: 6e4fca19083b5dbdcd841012f6e1051bb7c00eb8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2018
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Configuration Manager 和 Microsoft Intune 的混合移动设备管理中的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*

本文提供有关 System Center Configuration Manager 和 Microsoft Intune 的混合部署的可用的新移动设备管理 (MDM) 功能的详细信息。     

> [!Note]    
> Azure 上的 Intune 是 Microsoft 建议的 MDM 解决方案。     
> - 若有详细了解 Intune 独立版中的新增功能和更新，请参阅 [Intune 中的新增功能](https://docs.microsoft.com/intune/whats-new)。    
> - 有关如何迁移到 Intune 独立版的详细信息，请参阅[将混合 MDM 用户和设备迁移到 Intune 独立版](https://docs.microsoft.com/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)。
> - 有关 Intune 和混合 MDM 的 UI 更新的详细信息，请参阅 [Intune 最终用户应用的 UI 更新](https://docs.microsoft.com/intune/whats-new-app-ui)。 

##  <a name="compatibility-with-configuration-manager-versions"></a>与 Configuration Manager 版本的兼容性  
本文的每个部分都列出了混合功能，并按 3 个不同类别进行分类。 请使用以下指南，确定每个类别中的功能与不同版本的 Configuration Manager 的兼容性：  

|功能类别|说明|
|-|-|
|**Microsoft Intune 中的新增功能** | 一般情况下，此类别下列出的所有功能都应适用于所有 Configuration Manager 版本。 这包括 System Center 2012 R2 Configuration Manager 版本，因为这些功能仅需要 Intune 服务，不需要 Configuration Manager 中的其他功能。|
|**Configuration Manager Technical Preview 中的新增功能**| 此类别下列出的所有功能仅适用于指定的 Technical Preview 版本。 若要试用这些功能，必须安装功能说明中指定的 Technical Preview 版本。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)。|
|**Configuration Manager (Current Branch) 中的新增功能**| 此类别下列出的所有功能仅适用于指定的 Configuration Manager (Current Branch) 版本，例如版本 1511 或 1602。 如果要为混合部署使用较旧版本的 Configuration Manager，则必须升级到功能说明中指定的 Configuration Manager (Current Branch) 版本。 有关详细信息，请参阅[升级到 System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。|



## <a name="february-2018"></a>2018 年 2 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **macOS 公司门户支持使用设备注册管理器的注册**  
    用户现在可以在通过 macOS 公司门户注册时使用设备注册管理器。
    <!-- 1352411 -->


## <a name="january-2018"></a>2018 年 1 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **批准适用于 Android for Work 的公司门户应用**  
  如果你的组织使用 Android for Work，请手动批准适用于 Android 的公司门户应用。 然后，它继续从托管的 Google Play 商店接收自动更新。
  <!--1797090 -->  

- **适用于 Intune 的条件访问策略仅可从 Azure 门户获取**   
  从此版本开始，必须配置和管理 [Azure 门户](https://portal.azure.com)中的条件访问策略（“Azure Active Directory” > “条件访问”）。 为方便起见，也可以通过 Azure 门户中的“Intune” > “条件访问”，从 Intune 访问此边栏选项卡。
  <!-- 1737088 1634311 --> 

- **对符合性电子邮件的更新**    
  发送电子邮件以报告不符合设备时，会包括不符合设备的详细信息。 
  <!--1637547 -->

- **Android 设备“解析”操作的新功能**    
  适用于 Android 的公司门户应用正在扩展其更新设备设置的“解析”操作，以解决[设备加密问题](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android)。
  <!--1583480-->

- **适用于 Windows 10 的公司门户应用中提供远程锁定**    
  最终用户现在可以从适用于 Windows 10 的公司门户应用远程锁定他们的设备。 不会为他们当前使用的本地设备显示此操作。
  <!--676506-->

- **为适用于 Windows 10 的公司门户应用符合性问题提供了更轻松的解决方案**   
  使用 Windows 设备的最终用户可以点击公司门户应用中不符合的原因。 在可能的情况下，此操作将用户直接带到设置应用中的正确位置来解决此问题。
  <!--676546-->    



## <a name="december-2017"></a>2017 年 12 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **Android 企业版现在支持可用的应用程序部署**    
  除了“必选”以外，现在还可以将 Android 企业版（也就是之前的 Android for Work）应用部署为“可用”。 有关详细信息，请参阅[使用 System Center Configuration Manager 创建 Android 应用程序](/sccm/mdm/deploy-use/creating-android-applications)。



## <a name="november-2017"></a>2017 年 11 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **允许来自托管应用的文本协议**  
  由 Intune App SDK 管理的应用可发送短信。
  <!-- 1414050  -->   

- **提供了适用于 macOS 的公司门户应用**   
  macOS 上的 Intune 公司门户具有更新的体验。 该体验已进行了优化，对于用户已注册的所有设备它均可以清楚地显示用户所需的所有信息和符合性通知。 此外，将 Intune 公司门户部署到设备后，适用于 macOS 的 Microsoft 自动更新将为其提供更新。 通过从 macOS 设备登录到 Intune 公司门户网站来下载适用于 macOS 的新 Intune 公司门户。
  <!--1541700-->   

- **Microsoft Planner 现已加入已批准应用的移动应用管理 (MAM) 列表**    
  适用于 iOS 和 Android 的 Microsoft Planner 应用现在属于移动应用管理 (MAM) 的已批准应用。 通过 Azure 门户中的“Intune 应用保护”边栏选项卡将该应用配置到所有租户。 有关详细信息，请参阅 [MAM 已批准应用列表](https://www.microsoft.com/cloud-platform/microsoft-intune-apps)。
  <!-- 1248473 -->    

- **访问 iOS 的托管应用日志**    
  安装了 Managed Browser 的最终用户现在可查看所有 Microsoft 已发布应用的管理状态，并可针对托管 iOS 应用的疑难问题发送日志。
  <!-- 1469920 -->    

  若要了解如何在运行于 iOS 设备上的 Managed Browser 中启用疑难解答模式，请参阅[如何在 iOS 上使用 Managed Browser 访问托管应用日志](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios)。

- **对适用于 iOS 的公司门户 2.9.0 版中设备安装工作流的改进**    
  我们改进了适用于 iOS 的公司门户应用中的设备安装工作流。 语言更贴近用户，并尽可能地将屏幕合并。 我们还通过在整个安装文本中使用贵公司的名称，使语言更具有针对性。 可在[应用 UI 中的新增功能](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017)页上查看此更新的工作流。

- **适用于 Android 的公司门户应用的反馈提示**    
  适用于 Android 的公司门户应用现在请求最终用户反馈。 此反馈将直接发送给 Microsoft，并且最终用户将有机会在公开的 Google Play 商店中评价该应用。 反馈不是必填项，可轻松消除此提示，以便用户可以继续使用此应用。 
  <!--1165249-->    

- **告知最终用户可以看到 Windows 10 设备的哪些设备信息**    
  在适用于 Windows 10 的公司门户应用上，我们还在“设备详细信息”屏幕中添加了“所有权类型”。 此信息允许用户直接从 Intune 最终用户文档中找到隐私的相关详情。用户还可以在“关于”屏幕上找到此类信息。
  <!--1337920-->    

- **可用于 Android 设备的新“解析”操作**    
  适用于 Android 的公司门户应用“更新设备设置”页面上引入了“解析”操作。 选择此选项可使最终用户直接进入导致其设备为不符合设备的设置。 适用于 Android 的公司门户应用程序当前支持将此操作用于[设备密码](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android)、[设备加密](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android)、[USB 调试](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android)和[未知源](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android)设置。 
  <!--1583480-->    


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

- **针对非符合性的操作**    
  现在可配置一系列以时间排序的应用于不符合设备的操作。 例如，可通过电子邮件通知不符合设备的最终用户，或将这些设备标记为不符合。 有关详细信息，请参阅[设置针对非符合性的操作](/sccm/mdm/deploy-use/actions-for-noncompliance)。
  <!--1321366 -->

- **新移动应用程序管理策略设置**     
  以下设置已添加到移动应用程序管理策略设置：
  - **禁用联系人同步**：阻止应用将数据保存到设备上的本机“联系人”应用。
  - **禁用打印**：阻止应用打印工作或学校数据。
  <!-- 1324760 -->    

  请参阅[使用 Configuration Manager 中的应用保护策略来保护应用](/sccm/mdm/deploy-use/protect-apps-using-mam-policies)，尝试新的应用保护策略设置。

- **Windows 10 ARM64 设备支持**     
  运行 Windows 10 的 ARM64 设备支持混合移动设备管理 (MDM) 方案（当这些设备可用时）。 有关详细信息，请参阅 [Windows 10 ARM64 设备支持](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support)。
  <!-- 1355000 -->    

- **改进了 Configuration Manager 控制台中的 VPN 配置文件体验**     
  在此版本中，我们更新了 VPN 配置文件向导和属性页，以显示选定平台相应的设置。 此功能以前在 Configuration Manager Technical Preview 1709 中提供。 现在可用于 Intune 和 Configuration Manager (Current Branch) 版本 1710 的混合部署。 有关详细信息，请参阅[改进了 Configuration Manager 控制台中的 VPN 配置文件体验](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console)。
  <!-- 1318232 -->


### <a name="new-in-configuration-manger-technical-preview-1711"></a>Configuration Manager Technical Preview 1711 中的新增功能

- **Windows 10 的新符合性策略选项**   
  现在可以为 Windows 10 设备配置新的符合性策略选项。 新的设置包括防火墙、用户帐户控制、Windows Defender 防病毒和操作系统内部版本版本控制的策略。 有关详细信息，请参阅[适用于 Windows 10 的新符合性策略选项](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10)。



## <a name="october-2017"></a>2017 年 10 月

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Configuration Manager Technical Preview 1709 中的新增功能

- **改进了 Configuration Manager 控制台中的 VPN 配置文件体验**      
  VPN 配置文件设置现根据平台进行筛选。 在创建新的 VPN 配置文件时，每个受支持的平台都将包含仅适用于该平台的设置。 不会影响现有的 VPN 配置文件。 可以在[此处](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console)阅读有关此更改的详细信息。
  <!-- 1313282 -->


### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能  

- **帮助用户使用适用于 Android 的公司门户应用**     
  适用于 Android 的公司门户应用已为最终用户添加说明，帮助他们了解并尽量自行解决新的用例。
    - 如果最终用户已达到他们可添加的最大设备数，他们将被引导至 [Azure Active Directory 门户](https://account.activedirectory.windowsazure.com/r/#/profile)以移除设备。
    - 为最终用户提供要遵守的步骤以帮助他们[修复 Samsung Knox 设备上的激活错误](https://go.microsoft.com/fwlink/?linkid=859718)或者[关闭节能模式](https://docs.microsoft.com/intune-user-help/power-saving-mode-android)。 如果这些解决方案都不能解决他们的问题，我们将提供如何[将日志提交到 Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android) 的说明。
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Android 公司门户中的设备安装进度指示器**    
  适用于 Android 的公司门户应用在用户注册设备时显示设备安装进度指示器。 指示器显示新状态，从“安装设备...”开始，然后“注册设备...”，接下来“完成注册设备...”，最后“完成安装设备...”。  
  <!--1565657-->    

- **适用于 iOS 的公司门户上基于证书的身份验证支持**    
  我们在适用于 IOS 的公司门户应用中添加了对基于证书的身份验证 (CBA) 的支持。 具有 CBA 的用户输入其用户名，然后点击“使用证书登录”链接。 CBA 已支持用于 Android 和 Windows 的公司门户应用。 你可以在[登录到公司门户应用](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal)页上了解详细信息。
  <!--1029830-->   

- **对公司门户中设备安装工作流的改进**     
  我们改进了适用于 Android 的公司门户应用中的设备安装工作流。 语言更贴近贵公司的用语习惯，在可能的情况下我们还对屏幕进行了合并。 在[应用 UI 中的新增功能](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017)页上可以看到这些改进。
  <!--1490692-->     

- **关于在 Android 设备上访问联系人的请求的改进指导**     
  适用于 Android 的公司门户应用通常需要最终用户接受“联系人”权限。 如果最终用户拒绝此访问权限，他们会看到一个应用内通知，提醒他们授予其条件访问权限。 
  <!--1484985-->     

- **适用于 Android 的安全启动修正**     
  使用 Android 设备的最终用户可以点击公司门户应用中不符合的原因。 在可能的情况下，此操作将用户直接带到设置应用中的正确位置来解决此问题。 
  <!--1490712-->    

- **向最终用户额外发送有关 Android Oreo 公司门户应用的推送通知**    
  最终用户可以看到其他通知，其中指明了 Android Oreo 公司门户应用何时执行后台任务，如从 Intune 服务检索策略。 通知进一步提高了透明度，可方便最终用户了解公司门户应用何时在其设备上执行管理任务。 此改进是 Android Oreo 公司门户应用的整体[公司门户 UI 优化](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune)中的一部分。 
  <!--1475932 -->     

- **使用工作配置文件时适用于 Android 公司门户应用的新行为**     
  当你使用工作配置文件注册 Android for Work 设备时，它是工作配置文件中在设备上执行管理任务的公司门户应用。 

  除非你在个人配置文件中使用启用了 MAM 的应用，否则适用于 Android 的公司门户应用将不再提供任何服务。 若要改进工作配置文件体验，Intune 将在工作配置文件成功注册后自动隐藏个人版公司门户应用。

  通过浏览 [Play Store 中的公司门户](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)并点击“启用”，可以随时在个人配置文件中启用适用于 Android 的公司门户应用。
  <!--1485783-->    

- **适用于 Windows 8.1 和 Windows Phone 8.1 的公司门户将移至维护模式**    
  在公告中添加了一个通知：适用于 Windows 8.1 和 Windows Phone 8.1 的公司门户应用将移至维护模式。 有关详细信息，请参阅[通知](#notices)。  
  <!--1428681-->    

- **块不受支持的 Samsung Knox 设备注册**   
  公司门户应用仅尝试注册受支持的 Samsung Knox 设备。 若要避免阻止 MDM 注册的 KNOX 激活错误，只有在[由 Samsung 发布的设备列表](https://www.samsungknox.com/knox-supported-devices/knox-workspace)中显示设备时才会尝试进行设备注册。 Samsung 设备可以有支持 KNOX 的型号，而其他设备则没有。 在采购和部署之前，需与设备经销商验证 Knox 的兼容性。 可以在 [Android 和 Samsung KNOX Standard 策略设置](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices)中找到经验证的设备的完整列表。
  <!-- 1490695 -->     

- **不再支持 Android 4.3 及更低版本**     
  添加了 Android 4.3 及更低版本不再受支持的通知。 有关详细信息，请参阅[通知](#notices)。
  <!--1171126, 1326920 -->     

- **告知最终用户可以在注册设备上看到哪些设备信息**     
  在所有公司门户应用上，我们在“设备详细信息”屏幕中添加了“所有权类型”。 此信息允许用户直接从[公司可以看到哪些信息？](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune)一文中找到隐私的相关详情。 此改进将在不久的将来在所有公司门户应用中推出。 我们在 [9 月](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017)宣布了适用于 iOS 的此功能。 
  <!--1165314-->     



## <a name="september-2017"></a>2017 年 9 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能     

- **向 Windows 10 版公司门户应用中添加了刷新操作**    
    通过 Windows 10 版公司门户应用，用户可以通过下拉刷新或在桌面上按 F5 来刷新应用中的数据。
    <!-- 1132468 -->     

- **告知最终用户可以看到哪些 iOS 设备信息**   
    在 iOS 公司门户应用上，我们还在“设备详细信息”屏幕中添加了“所有权类型”。 此信息允许用户直接从 Intune 最终用户文档中找到隐私的相关详情。用户还可以在“关于”屏幕上找到此类信息。 
    <!--739894-->    

- **Android 公司门户应用的表述更易于理解**   
    Android 公司门户应用的注册流程进行了简化，新增了文本，更易于最终用户进行注册。 如果你有自定义的注册文档，请对其进行更新以反映新屏幕。 有关示例图像，可以访问 [Intune 最终用户应用的 UI 更新](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017)页。
    <!---1396349-->    

- **将 Windows 10 公司门户应用添加到 Windows 信息保护允许策略**    
    Windows 10 公司门户应用已更新为支持 Windows 信息保护 (WIP)。 可以将应用添加到 WIP 允许策略。 此更改生效后，无需再将应用添加到“豁免”列表。 

    仅可将单个 WIP 配置项目传递到设备。 如果将两个 WIP 配置项目传递到同一设备，所有 WIP 策略都将失效。
    <!-- 677129 -->    

- **添加了 iOS 8.0 不再受支持的通知**    
    添加了 iOS 8.0 不再受支持的通知。 有关详细信息，请参阅[通知](#notices)。



## <a name="august-2017"></a>2017 年 8 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能     

- **为 Android 公司门户用户和应用保护策略用户提供了新登录体验**    
  最终用户现在可以使用 Android 公司门户应用浏览应用、管理设备和查看 IT 联系人信息，而无需注册其 Android 设备。 此外，如果最终用户已使用受 Intune 应用保护策略保护的应用并启动了 Android 公司门户，则最终用户将不会再收到注册设备的提示。
  <!-- 621669 -->



## <a name="july-2017"></a>2017 年 7 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

- **针对 Android 和 Windows Phone 添加了不再支持的通知**    
    针对不再支持的 Android 和 Windows Phone 版本添加了新通知。 有关详细信息，请参阅[通知](#notices)。


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

以下功能以前在 Configuration Manager Technical Preview 版本中提供。 这些功能现在可用于 Intune 和 Configuration Manager (Current Branch) 版本 1706 的混合部署。

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
  从 Configuration Manager 1610 版本开始，可以更改 MDM 机构而无需联系 Microsoft 支持部门。 也无需取消注册并重新注册现有的托管设备。 有关详细信息，请参阅[更改 MDM 机构](/sccm/mdm/deploy-use/change-mdm-authority)。

- **Managed Browser 和应用代理集成**    
  Intune Managed Browser 现在可以与 Azure AD 应用程序代理服务集成，用户即使在远程工作时也可以访问内部网站。 浏览器的用户照常输入网站 URL，Managed Browser 会通过应用程序代理 Web 网关路由请求。 有关详细信息，请参阅[使用 Managed Browser 策略管理 Internet 访问权限](https://docs.microsoft.com/intune/app-configuration-managed-browser)。

- **Android 公司门户应用现在提供全新的应用保护策略最终用户体验**  
  根据客户反馈，我们修改了适用于 Android 的公司门户应用，现在显示“访问公司内容”按钮。 其目的在于，使最终用户在仅需要访问支持应用保护策略（Intune 移动应用程序管理的一项功能）的应用时，无需完成不必要的注册过程。 在[应用 UI 中的新增功能](https://docs.microsoft.com/intune/whats-new-app-ui)页上可以看到这些更改。

- **可轻松删除公司门户的新菜单操作**  
  根据用户反馈，适用于 Android 的公司门户应用已添加一个新的菜单操作，用于从设备删除公司门户。 此操作可从 Intune 管理中删除设备，这样用户就可以从设备中删除应用。 有关这些更改，可以参阅[应用 UI 中的新增功能](https://docs.microsoft.com/intune/whats-new-app-ui)页和 [Android 最终用户文档](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android)。

- **对与 Windows 10 创意者更新之间的应用同步的改进**  
  Windows 10 公司门户应用现在自动开始为安装了 Windows 10 创意者更新（版本 1703）的设备同步应用安装请求。 此行为会减少“挂起同步”状态期间出现的应用安装停止问题。 此外，用户还可以在应用中手动启动同步。 在[应用 UI 中的新增功能](https://docs.microsoft.com/intune/whats-new-app-ui)页上可以看到这些更改。

- **Windows 10 公司门户的全新引导式体验**  
  适用于 Windows 10 的公司门户应用为尚未进行标识或注册的设备提供引导式 Intune 演练体验。 新体验提供分步说明，可指导用户完成注册到 Azure Active Directory（条件访问功能需要）和 MDM 注册（设备管理功能需要）的过程。 从公司门户主页可以进入引导式体验。 如果用户没有完成注册，可以继续使用该应用，但可用功能会受到限制。

  此更新仅在运行 Windows 10 周年更新（内部版本 1607）或更高版本的设备上可见。 在[应用 UI 中的新增功能](https://docs.microsoft.com/intune/whats-new-app-ui)页上可以看到这些更改。

- **对适用于 iOS 的公司门户应用中的应用磁贴的改进**  
  我们更新了主页上的应用磁贴设计，现在可以反映你为公司门户设置的品牌颜色。 有关详细信息，请参阅[应用 UI 中的新增功能](https://docs.microsoft.com/intune/whats-new-app-ui)。

- **帐户选取器现在可用于适用于 iOS 的公司门户应用**  
  如果 iOS 设备用户使用其工作或学校帐户登录到其他 Microsoft 应用，则他们在登录到公司门户时，可以看到我们的新帐户选取器。 有关详细信息，请参阅[应用 UI 中的新增功能](https://docs.microsoft.com/intune/whats-new-app-ui)。

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Configuration Manager Technical Preview 1706 中的新增功能

- **新 Windows 配置项设置**      
  新的 Windows 配置项适用于密码、设备、存储和 Microsoft Edge 设置类别。 有关详细信息，请参阅[新 Windows 配置项设置](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings)。
  <!-- 1354715 -->

- **新设备符合性策略规则**   
  对于以前仅适用于 Intune 独立版本的符合性策略，现在可以为其配置新选项。 有关详细信息，请参阅[设备符合性策略改进](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules)。

- **Android 和 iOS 注册限制**       
  管理员现在可以指定用户不能在其混合环境中注册个人 Android 或 iOS 设备。 此操作允许你将注册的设备限制为预先声明的公司自有设备，或仅注册了“设备注册计划”的 iOS 设备。 有关详细信息，请参阅 [Android 和 iOS 注册限制](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions)。
  <!-- 1290826 -->

- **支持 Entrust 证书颁发机构**      
  Configuration Manager 现在支持 Entrust 证书颁发机构。 此支持可将 PFX 证书传递到注册到 Microsoft Intune 的设备。    
  <!-- 1350740 -->

  在 Configuration Manager 中添加“证书注册点”角色时，你可以将 Entrust 配置为证书颁发机构。 在添加颁发 PFX 证书的新证书配置文件时，你可以选择 Microsoft 或 Entrust 证书颁发机构。

  **已知问题**：在 Technical Preview 1706 中，没有为 Microsoft 证书颁发机构颁发 PFX 证书。 此问题不会影响导入的 PFX 证书或 SCEP 配置文件。

- **Cisco (IPsec) 支持 macOS VPN 配置文件**      
  你可以使用 Cisco (IPsec) 作为连接类型创建 macOS VPN 配置文件。 有关详细信息，请参阅[创建 VPN 配置文件](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles)。
  <!-- 1321367 -->


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

  - 颜色：“公司门户”选项卡的颜色与 IT 定义的品牌颜色相同。
  - 应用：在“应用”选项卡中，更新了“特色应用”和“所有应用”按钮。
  - 搜索：在“应用”选项卡中，“搜索”按钮是浮动的操作按钮。
  - 导航应用：“所有应用”视图以选项卡形式呈现出“特色”、“所有”和“分类”视图，便于导航。
  - 支持：更新了“我的设备”和“联系 IT”选项卡，以改善可读性。

  有关这些更改的详细信息，请参阅 [Intune 最终用户应用的 UI 更新](https://docs.microsoft.com/intune/whats-new-app-ui)。

- **Windows 10 公司门户的签名脚本**  
  如果需要下载和旁加载 Windows 10 公司门户应用，现在可以使用脚本为你的组织简化应用签名过程。 若要下载该脚本及其使用说明，请参阅 TechNet 库中的 [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript)（Windows 10 公司门户适用的 Microsoft Intune 签名脚本）。 有关此公告的详细信息，请参阅 Intune 支持团队博客上的[更新 Windows 10 公司门户应用](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/)。

- **改进了对中国的 Android 用户的支持**  
  由于中国地区没有 Google Play 商店，Android 设备必须从中国的应用商店获取应用。 公司门户支持此工作流。 它可重定向中国的 Android 用户，以便从本地应用商店下载公司门户和 Outlook 应用。 启用条件访问策略后，此行为将同时提升有关移动设备管理和移动应用程序管理的用户体验。 以下中文应用商店可以提供 Android 适用的公司门户和 Outlook 应用：

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

- **对适用于企业的 Microsoft Store 中的业务线应用的支持**  
  现在可以同步来自适用于企业的 Microsoft Store 的自定义业务线应用。

- **新移动威胁防御监视工具**  
    现在，可以使用新方法通过移动威胁防御服务提供程序来监视符合性状态。

    有关详细信息，请参阅[如何监视移动威胁防御合规性](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance)。



## <a name="notices"></a>通知

### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>适用于 Windows 8.1 和 Windows Phone 8.1 的公司门户将移至维护模式 
<!--1428681-->
*2017 年 10 月 6日*   
 
从 2017 年 10 月开始，适用于 Windows 8.1 和 Windows Phone 8.1 的公司门户应用移至维护模式。 此模式意味着应用和现有方案（如注册和符合性）继续支持这些平台。 这些应用继续通过现有发布通道下载，如 Microsoft Store。 

一旦处于维护模式，这些应用仅接收重要的安全更新。 将不会对这些应用发布任何其他更新或功能。 对于新功能，我们建议将设备更新到 Windows 10 或 Windows 10 移动版。 

### <a name="end-of-support-for-ios-80"></a>iOS 8.0 不再受支持 
<!---1164477--->
托管应用和 iOS 公司门户应用要求必须使用 iOS 9.0 及更高版本，才能访问公司资源。 9 月前未更新的设备无法再访问公司门户或这些应用。 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>平台支持提醒：Windows Phone 8.1 主流支持将于 2017 年 7 月 11 日终止
<!-- 1327781 -->
*2017 年 7 月 11 日*

Windows Phone 8.1 平台的主流支持已终止。 Windows 8.1 PC 支持不会受到影响。

不会对 Intune 服务托管的任何 Windows Phone 8.1 设备产生直接影响，包括混合 MDM 中注册的设备。 注册的设备继续正常工作。 所有策略、配置和应用继续按预期方式工作。 请注意，不会针对 Intune 服务中的 Windows Phone 8.1 平台以及 Windows Phone 8.1 公司门户应用进行任何改进。

建议尽早将符合条件的 Windows Phone 8.1 设备升级到 Windows 10 移动版。  

### <a name="end-of-support-for-android-43-and-lower"></a>不再支持 Android 4.3 及更低版本
<!---1171127--->
*2017 年 7 月 6 日*

托管应用和 Android 公司门户应用要求必须使用 Android 4.4 及更高版本，才能访问公司资源。 在 10 月初之前未更新的设备无法再访问公司门户或这些应用。 截至 12 月，所有注册的设备都在 12 月内被强制停用，因此将无法再访问公司资源。 如果在未启用 MDM 的情况下使用应用保护策略，应用将无法接收更新，应用体验质量将随着时间的推移而逐渐降低。



## <a name="see-also"></a>另请参阅

- [以前的混合 MDM 功能和注意事项](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager 中的 MDM 的新增功能](https://technet.microsoft.com/library/mt445560.aspx)
