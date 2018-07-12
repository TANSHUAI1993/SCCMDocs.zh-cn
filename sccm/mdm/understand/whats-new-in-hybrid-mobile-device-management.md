---
title: 混合 MDM 中的新增功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 和 Intune 的混合部署可用的新移动设备管理功能。
ms.date: 07/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d527d2fc4fdc52e132b6f603d9b83851e1693f3
ms.sourcegitcommit: c9d0a4c24ce90825cb2d05e4fe37c5b41fa48a50
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2018
ms.locfileid: "37923535"
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



## <a name="july-2018"></a>2018 年 7 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

#### <a name="updates-to-out-of-compliance-messages-in-company-portal-app"></a>更新公司门户应用中的不合规消息 
<!--1832222--> 我们正在修改当设备不合规时向使用该设备的用户显示的消息。 消息原义未变，只是用更为友好的语言和更少的技术术语进行更新。 此外，我们还将刷新文档和修正步骤的链接，以使其保持最新。  

以下更新前后的文本是你将看到的对消息所做改进的一个示例：  

- 更新前：此设备未在 IT 管理员要求的指定时段内连接 Intune 服务。若要解决此问题，请打开设备上的公司门户应用，并单击“检查合规性”按钮。  

- 更新后：你的设备已有一段时间未签入组织。要重新建立连接，请打开设备上的公司门户应用，然后点击设备的“检查设置”。  

#### <a name="select-device-categories-by-using-the-access-work-or-school-settings"></a>使用“访问工作单位或学校”设置选择设备类别 
<!--1058963--> 如果你已启用[设备组映射](https://docs.microsoft.com/intune/device-group-mapping)，Windows 10 用户在通过“设置” > “帐户” > “访问工作单位或学校”中的“连接”按钮进行注册后，系统现在将提示他们选择设备类别。  



## <a name="june-2018"></a>2018 年 6 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

#### <a name="access-to-macos-company-portal-pre-release-build"></a>访问 macOS 公司门户预发布版本 
<!--1734766--> 使用 Microsoft 自动更新，通过加入预览体验计划注册以提早接收内部版本。 通过注册，可使你在更新的公司门户对最终用户可用前使用它。

#### <a name="intune-app-protection-policies-and-microsoft-edge"></a>Intune 应用保护策略和 Microsoft Edge 
<!--1818968,1818969--> 面向移动设备（iOS 和 Android）的 Microsoft Edge 浏览器现支持 Microsoft Intune 应用保护策略。 在 Microsoft Edge 应用程序中使用公司的 Azure Active Directory 帐户进行登录的 iOS 和 Android 设备用户受到 Intune 保护。 在 iOS 设备上，“需要使用托管浏览器获取 Web 内容”的策略允许用户在托管的 Microsoft Edge 中打开链接。



## <a name="may-2018"></a>2018 年 5 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

#### <a name="requesting-help-in-the-company-portal-for-windows-10"></a>在适用于 Windows 10 的公司门户中请求帮助 
<!--1874137--> 当用户启动工作流以获取相关问题的帮助时，适用于 Windows 10 的公司门户现在将直接向 Microsoft 发送应用日志。 此行为有助于更轻松地进行故障排除并解决向 Microsoft 提出的问题。  


### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

#### <a name="android-for-work-and-lookout-onboarding-moved-to-intune-on-azure"></a>Android for Work 和 Lookout 载入已移至 Azure 上的 Intune
<!--2355022,2357366--> 借助最新的 Intune 更新，可访问 Azure 门户中的 Intune，在混合移动设备管理租户上启用并管理 Android for Work 集成和 Lookout 移动威胁防御集成。 在此更新之前，只能在 Intune Classic (Silverlight) 门户中配置这些内容。
 
注意：Lookout 是混合环境中唯一支持的移动威胁防御 (MTD) 提供程序。 如果之前已与任何其他 MTD 提供程序集成，它仍会在 Azure 门户的 Intune 中显示。 如果删除它的连接器，则不能再重新添加它。
 
这些更改不影响现有功能。 继续使用 Configuration Manager 控制台管理相关应用、报告和策略。
 
有关详细信息，请参阅下列文章：
- [设置 Android 混合设备管理](/sccm/mdm/deploy-use/enroll-hybrid-android)
- [根据设备、网络和应用程序风险管理对公司资源的访问权限](/sccm/mdm/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)


#### <a name="support-for-new-versions-of-cisco-anyconnect-client-for-ios"></a>对适用于 iOS 的 Cisco AnyConnect 客户端新版本的支持
<!--1357393--> 你可以启用对适用于 iOS 4.0.7 或更高版本的 Cisco AnyConnect 的支持。 如果启用，现有 Cisco AnyConnect VPN 配置文件会标记为“Cisco 旧式 AnyConnect”，然后继续按照以前的方式工作。 “Cisco AnyConnect”选项适用于可与 iOS 4.0.7 或更高版本的 Cisco AnyConnect 配合使用的新 VPN 配置文件。

  > [!Tip]  
  > 适用于 iOS 的 Cisco AnyConnect 4.0.07x 和更高版本作为[预发行功能](/sccm/core/servers/manage/pre-release-features)首次被引入版本 1802。 从[更新 4163547](https://support.microsoft.com/help/4163547) 开始到版本 1802，此功能不再属于预发行功能。  

> [!Note]  
> 继续使用适用于 macOS VPN 配置文件的“Cisco 旧式 AnyConnect”选项。 



## <a name="april-2018"></a>2018 年 4 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10"></a>Intune 适用于面向 Windows 10 的公司门户中的 Fluent Design System 
<!--1195010--> 适用于 Windows 10 的 Intune 公司门户应用已更新 [Fluent Design System 的导航窗格视图](/windows/uwp/design/basics/navigation-basics)。 在应用程序旁边，会看到一个包含所有顶级页面的静态垂直列表。 单击任意链接可快速查看并在页面之间进行切换。 我们正不断努力在 Intune 中打造更具适应性、引人入胜且熟悉的体验，在此期间，你会看到多个更新，此更新正是第一个。 要查看更新的外观，请转到[应用 UI 中的新增功能](/intune/whats-new-app-ui)。

#### <a name="improved-device-tiles-in-the-windows-10-company-portal"></a>改进了 Windows 10 公司门户中的设备磁贴
<!--2213364--> 更新后的磁贴更易于视力较差的用户使用，还可使屏幕阅读工具提供更好的性能。


#### <a name="test-the-company-portal-for-macos-on-virtual-machines"></a>在虚拟机上测试适用于 macOS 的公司门户
<!--2216679--> 我们已发布可帮助 IT 管理员在 Parallels Desktop 和 VMware Fusion 虚拟机上测试适用于 macOS 的公司门户应用的指南。 有关详细信息，请参阅[注册用于测试的虚拟 macOS 计算机](/intune/macos-enroll#enroll-virtual-macos-machines-for-testing)。


#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos"></a>在适用于 macOS 的公司门户应用中发送诊断报告
<!--2216677--> 适用于 macOS 设备的公司门户应用已更新，改进了用户报告 Intune 相关错误的方式。 员工可从公司门户应用中：

- 将诊断报告直接上传给 Microsoft 开发人员团队。
- 通过电子邮件将事件 ID 发送给公司的 IT 支持团队。


#### <a name="updated-help-experience-on-company-portal-app-for-android"></a>Android 公司门户应用中更新的帮助体验 
<!--1631531--> 我们更新了适用于 Android 的公司门户应用中的帮助体验，以符合 Android 平台的最佳做法。 现在，当用户在应用中遇到问题时，他们可以点击“菜单” > “帮助”并执行以下操作：
- 将诊断日志上传到 Microsoft。
- 将描述问题和事件 ID 的电子邮件发送给公司支持人员。


#### <a name="update-where-to-configure-your-app-protection-policies"></a>更新配置应用保护策略的位置 
<!--2144597--> 在 Microsoft Intune 服务的 Azure 门户中，我们将从“Intune 应用保护服务”边栏选项卡暂时重定向到“移动应用”边栏选项卡。 请注意，Intune 中“应用配置”下的“移动应用”边栏选项卡已包括所有应用保护策略。 直接转到 Intune 即可，无需转到“Intune 应用保护”。 在 2018 年 4 月，我们将停止重定向并将完全删除“Intune 应用保护服务”边栏选项卡，以便在 Intune 中只存在应用保护策略的一个位置。 

**这会对我产生哪些影响？** 此更改将同时影响 Intune 独立版客户和混合版（带 Configuration Manager 的 Intune）客户。 此集成将有助于简化云管理。

**我需要如何准备应对此项变化？** 请将 Intune 标记为收藏（而不是“Intune 应用保护服务”边栏选项卡），并确保熟悉 Intune 的“移动应用”边栏选项卡中的应用保护策略工作流。 我们将重定向一小段时间，然后删除“应用保护”边栏选项卡。 请记住，所有应用保护策略都已转到 Intune，可修改任何条件访问策略。 有关修改条件访问策略的详细信息，请参阅 [Azure Active Directory 中的条件访问](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)。 有关其他信息，请参阅[应用保护策略是什么？](/intune/app-protection-policy) 




#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>iOS 版公司门户应用的用户体验更新 
<!--1412866--> 我们已向 iOS 版公司门户应用发布用户体验主要更新。 此更新具有经过完全重新设计的视觉效果，包括现代化的外观。 我们保留了应用的功能，但提高了其可用性和可访问性。  

你还会看到：
- 对 iPhone X 的支持。
- 应用启动速度和加载响应速度更快，可节省用户时间。
- 可为用户提供最新状态信息的附加进度条。
- 改进了用户上传日志的方式，因此可在出现问题时更轻松地报告该问题。  

要查看更新的外观，请转到[应用 UI 中的新增功能](/intune/whats-new-app-ui)。



## <a name="march-2018"></a>2018 年 3 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

#### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>Windows 公司门户的“发送反馈”选项可能失效
<!--2070166--> Windows 公司门户应用上有一个“发送反馈”选项，用户可用它向 Microsoft 发送应用反馈。 自 2018 年 4 月 30 日起，只有 Windows 10 版本 1607 及更高版本上运行的 Windows 10 公司门户应用才能继续使用此选项。   

**这会对我产生哪些影响？**

如果尚未为最终用户安装 Windows 公司门户应用，请忽略此消息。

如果任一最终用户具备公司门户应用，请注意，自 4 月 30 日期，以下情形中的应用不可再使用“发送反馈”按钮：  

 - Windows 10 版本 1507 和版本 1511 上的 Windows 10 公司门户应用  

 - Windows Phone 8.1 公司门户应用  

对于受影响的设备，“发送反馈”选项会失效，且重试后仍不能成功运行。 若要将上述平台的体验反馈发送给 Microsoft，可使用下述备用反馈通道。

**我需要如何准备应对此项变化？**

请告知最终用户出现此项变化，并在必要时更新用户指南。 

让在 Windows Phone 8.1、Windows 10 版本 1507 和 Windows 10 版本 1511 上使用公司门户的最终用户了解有两个备用反馈通道可用。 最终用户可：  

- 使用 Windows 10 上的反馈中心应用  
- 发送电子邮件至 WinCPfeedback@microsoft.com  

要求使用 Windows 10 版本 1607 或更高版本的最终用户将 Windows 公司门户更新到 Microsoft Store 中的最新版。



#### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview"></a>Azure Active Directory 网站可能需要 Intune Managed Browser 应用，且支持 Managed Browser（公共预览版）的单一登录
<!-- 710595 --> 利用 Azure Active Directory (Azure AD)，现可在移动设备上将网站访问限制为仅可访问 Intune Managed Browser 应用。 在 Managed Browser 中，网站数据可保持安全并且独立于最终用户的个人数据。 此外，Managed Browser 支持受 Azure AD 保护的站点的单一登录功能。 通过登录 Managed Browser，或在设备上搭配使用 Managed Browser 和 Intune 管理的其他应用，用户无需输入凭据，Managed Browser 即可访问受 Azure AD 保护的公司站点。 此功能适用于 Outlook Web Access (OWA) 和 SharePoint Online 等站点，以及通过 Azure 应用代理访问的其他公司站点（如 Intranet 资源）。



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


## <a name="notices"></a>通知

### <a name="plan-for-change-intune-moving-to-support-ios-10-and-later-in-september-2018"></a>更改计划：Intune 将于 2018 年 9 月升级为支持 iOS 10 和更高版本 
<!--2454656-->

Apple 预期于 2018 年 9 月发布 iOS 12。 在发布后不久，我们即将 Intune 注册、公司门户和托管浏览器升级为支持 iOS 10 和更高版本。

#### <a name="how-does-this-affect-me"></a>这会对我产生哪些影响？

Office 365 移动应用在 iOS 10 和更高版本上均受支持，因此，你可能已升级了你的操作系统或设备。 如果情况如此，此次更改对你不会有影响。

但是，如果你使用的是下列任一设备，或者想要注册下列任一设备，请注意，这些设备仅支持 iOS 9 和更早版本。 若要继续访问 Intune 公司门户，必须在 9 月前将这些设备升级为支持 iOS 10 或更高版本的设备： 

- iPhone 4S
- iPod Touch 
- iPad 2
- iPad（第 3 代）
- iPad Mini（第 1 代）

从 7 月开始，使用 iOS 9 和公司门户的已注册 MDM 的设备将收到升级其操作系统或设备的提示。 如果你使用应用保护策略，也可以设置“需要最低 iOS 操作系统(仅限警告)”访问设置。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要如何准备应对此项变化？

查看组织中受影响的设备或用户。 在 Azure 门户中的 Intune 中，转到“设备” > “所有设备”，并按“操作系统”进行筛选。  单击“列”以显示操作系统版本等详细信息。 要求你的用户在 9 月前将其设备升级到受支持的操作系统版本。


### <a name="plan-for-change-intune-moving-to-tls-12"></a>更改计划：Intune 升级到 TLS 1.2

从 2018 年 10 月 31 日起，Intune 将支持传输层安全性 (TLS) 协议版本 1.2，以提供一流的加密，确保我们的服务在默认情况下更为安全，并与 Microsoft Office 365 等其他 Microsoft 服务一致。 Office 将在 MC128929 中对此次更改进行说明。

#### <a name="how-does-this-affect-me"></a>这会对我产生哪些影响？

自 2018 年 10 月 31 日起，Intune 将不再支持 TLS 协议版本 1.0 或 1.1。 所有客户端 - 服务器和浏览器 - 服务器组合都应使用 TLS 版本 1.2，以确保能够正常连接到 Intune。 请注意，此次更改将影响不再受 Intune 支持但仍通过 Intune 接收策略的最终用户设备，此类设备无法使用 TLS 版本 1.2。 这包括运行 Android 4.3 和更早版本的设备。 有关受影响的设备和浏览器的列表，请参阅以下其他信息。

在 2018 年 10 月 31 日后，如果你遇到有关使用旧 TLS 版本的问题，作为解决方案的一部分，你将需要更新到 TLS 1.2 或支持 TLS 1.2 的设备。

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要如何准备应对此项变化？

我们建议在可能的情况下，主动删除环境中的 TLS 1.0 和 1.1 依赖项，并在操作系统级别禁用 TLS 1.0 和 1.1。 立即计划迁移到 TLS 1.2。 查看以下支持博客文章，了解现在不受 Intune 支持但仍可能接收策略的设备列表，这些设备将无法使用 TLS 版本 1.2 进行通信。 你可能需要通知这些最终用户，他们将无法访问公司资源。

有关详细信息，请参阅[将 Intune 升级到 TLS 1.2 以进行加密](https://blogs.technet.microsoft.com/intunesupport/2018/06/05/intune-moving-to-tls-1-2-for-encryption/)。


### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>适用于 Windows 8.1 和 Windows Phone 8.1 的公司门户将移至维护模式 
<!--1428681-->
*2017 年 10 月 6 日*   
 
从 2017 年 10 月开始，适用于 Windows 8.1 和 Windows Phone 8.1 的公司门户应用移至维护模式。 此模式意味着应用和现有方案（如注册和符合性）继续支持这些平台。 这些应用继续通过现有发布通道下载，如 Microsoft Store。 

一旦处于维护模式，这些应用仅接收重要的安全更新。 将不会对这些应用发布任何其他更新或功能。 对于新功能，我们建议将设备更新到 Windows 10 或 Windows 10 移动版。 

### <a name="end-of-support-for-ios-80"></a>iOS 8.0 不再受支持 
<!---1164477---> 托管应用和 iOS 公司门户应用要求必须使用 iOS 9.0 及更高版本，才能访问公司资源。 9 月前未更新的设备无法再访问公司门户或这些应用。 

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
