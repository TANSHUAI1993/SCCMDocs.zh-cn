---
title: "混合 MDM 的新增功能 | Microsoft Intune | System Center Configuration Manager"
description: "了解 System Center Configuration Manager 和 Intune 的混合部署可用的新移动设备管理功能。"
ms.custom: na
ms.date: 10/25/2016
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
ms.sourcegitcommit: f13b38fcc4e7c55f05dbf6a7d8f516643939ba92
ms.openlocfilehash: 3525fba1b75196bddebc89e49f40cbfd3c75d9d0

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理中的新增功能

*适用范围：System Center Configuration Manager (Current Branch)*

本文提供有关 System Center Configuration Manager 和 Microsoft Intune 的混合部署的可用的新移动设备管理 (MDM) 功能的详细信息。  

##  <a name="compatibility-with-configuration-manager-versions"></a>与 Configuration Manager 版本的兼容性  

 本文的每个部分都列出了混合功能，共 3 个不同类别。 请使用以下指南，确定每个类别中的功能与不同版本的 Configuration Manager 的兼容性：  

|功能类别|
|-|  
|**Microsoft Intune 新增功能** - 一般情况下，此类别列出的所有功能应适用于所有 Configuration Manager 版本（包括 System Center 2012 R2 Configuration Manager 版本），因为这些功能仅需要 Intune 服务，不需要 Configuration Manager 中的其他功能。<br /><br /> **Configuration Manager Technical Preview 中的新增功能** - 此类别下列出的所有功能仅适用于指定的 Technical Preview 版本。 若要试用这些功能，必须安装功能说明中指定的 Technical Preview 版本。 有关详细信息，请参阅 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)。<br /><br /> **Configuration Manager (Current Branch) 中的新增功能** - 此类别下列出的所有功能仅适用于指定的 Configuration Manager (Current Branch) 版本，例如版本 1511 或 1602。 如果要为混合部署使用较旧版本的 Configuration Manager，则必须升级到功能说明中指定的 Configuration Manager (Current Branch) 版本。 有关详细信息，请参阅[升级到 System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。|  

## <a name="new-hybrid-features-in-october-2016"></a>2016 年 10 月版本中的新增混合功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2016 年 10 月推出的以下 Intune 功能适用于混合部署。

- **移动应用程序管理的条件性访问**

  可以限制对 Exchange Online 的访问，以便仅访问支持 Intune 移动应用程序管理策略的应用，如 Outlook。 [这一新增功能](/intune/deploy-use/allow-policy-managed-apps-access-to-o365)可与 Intune 移动应用管理 (MAM) 策略完美结合使用，用户可以阻止对未使用 Intune MAM 策略配置的内置邮件客户端或其他应用的访问。 这可确保你的用户使用通过 Intune MAM 进行保护的应用访问组织的数据。 可通过 Azure 门户使用 Intune 移动应用管理。 查找“设置”边栏选项卡中的条件性访问部分。

-   **Intune App Wrapping Tool for Android**

  通过使用 Intune App Wrapping Tool，应用将可以使用 Intune 移动应用程序管理 (MAM) 策略。

- **Android Samsung KNOX 与 Intune 的兼容性**

  Intune 不能将 Samsung Galaxy Ace 手机的某些型号作为 Samsung KNOX 设备进行管理。 向 Intune 注册这些设备时，Intune 会将它们作为标准 Android 设备进行管理。

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

## <a name="new-hybrid-features-in-september-2016"></a>2016 年 9 月版本中的新增混合功能

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

  如果有针对所有 iOS 平台的配置文件或配置项目，也会将它们推送到 iOS 10。 我们还发布了对 Configuration Manager 1606 版的更新，允许用户将配置文件和配置项目用于 iOS 平台，包括 iOS 10。 可在 Configuration Manager 管理控制台中，转到“管理”>“概述”>“云服务”>“更新与服务”来安装此更新。 有关更新的详细信息，请访问 [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616)。

## <a name="new-hybrid-features-in-august-2016"></a>2016 年 8 月版本中的新增混合功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2016 年 8 月推出的以下 Intune 功能适用于混合部署。

- **Android 7 的公司门户应用支持**

  Android 版 Intune 公司门户应用为即将推出的移动设备的 Android 7.0 操作系统提供“零日”支持。

- **Google 将删除 Android 7.0 设备中的远程密码重置功能**

  Google 即将删除 IT 管理员和最终用户远程重置 Android 7.0 设备密码的功能。 以前，IT 管理员可以远程重置用户的密码，最终用户也可以从其公司门户网站重置密码。

- **Samsung KNOX 设备允许和阻止的应用策略**

  现在可以配置适用于 Samsung KNOX 设备的自定义策略，可通过此策略创建以下内容之一：

  - 禁止在设备上运行的应用列表。 即使已安装，在阻止列表中定义的应用也不能在设备上激活。
  - 允许设备用户从 Google Play 商店安装的应用列表。 不能从该应用商店安装任何其他应用。

  只有运行 Samsung KNOX 的设备才可以使用这些设置。 有关详细信息，请参阅[使用自定义策略允许和阻止 Samsung KNOX 设备的应用](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps)。

- **从公司门户到 Microsoft 的反馈链接**

   公司门户网站使最终用户能够点击页面底部的新“反馈”链接，向 Microsoft 发送有关网站体验的反馈。 收集到的匿名反馈将有助于 Microsoft 改进用户的公司门户网站体验。

- **最低 iOS Managed Browser 版本（已更新到 8.0）**

  用于 iOS 的 Microsoft Intune Managed Browser 应用已更新为支持运行 iOS 8.0 或更高版本的设备。 虽然 iOS 7.1 设备仍可使用现有的 Managed Browser 应用，但鼓励你的用户更新到 iOS 8.0 或更高版本，以访问并充分利用新的 Managed Browser 功能。

### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview 中的新增功能

2016 年 8 月版本的 Configuration Manager Technical Preview 中没有新增的混合功能。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (Current Branch) 中的新增功能

2016 年 8 月版本的 Configuration Manager (Current Branch) 中没有新增的混合功能。

## <a name="new-hybrid-features-in-july-2016"></a>2016 年 7 月版本中的新增混合功能

### <a name="new-in-microsoft-intune"></a>Microsoft Intune 中的新增功能

2016 年 7 月推出的以下 Intune 功能适用于混合部署。

- **用于 Intune 应用的 Xamarin SDK 已可用**

  Intune App SDK Xamarin 组件使用户能在使用 Xamarin 生成的移动 iOS 和 Android 应用中启用 Intune 移动应用管理功能。 可在 [Xamarin 应用商店](https://components.xamarin.com/view/Microsoft.Intune.MAM)或 [Microsoft Intune Github 页面](https://github.com/msintuneappsdk)中找到该组件。

- **改进了注册 Windows 设备时的最终用户体验**

  使用条件性访问时，Windows 8.1、Windows 10 桌面版和 Windows 10 移动版的注册步骤已在公司门户网站中阐明。 用户现在可以看到单独的“设备注册”和“工作区加入”步骤，如果他们遇到了“工作区加入(WPJ)”失败，便可更轻易地看到设备的状态并完成此过程。 这些步骤还有望简化 IT 管理员的故障排除过程。 以前，当最终用户尝试注册并成功完成 WPJ 以外的所有步骤时，已注册的设备将不会出现在设备列表中供用户识别，导致用户困惑。

 - **Windows 10 设备中现已提供完全擦除功能**

    可以擦除注册为移动设备的 Windows 10 电脑和笔记本，目的是将设备重置为出厂设置。 有关详细信息，请参阅[如何使用远程擦除保护设备](/sccm/mdm/deploy-use/wipe-lock-reset)。

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

* 从 Configuration Manager 控制台查找、管理和分发用于 Windows 10 设备的适用于企业的 Windows 应用商店应用 ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   适用于 Android 设备的 SmartLock 设置 ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   Windows 10 设备的应用触发的 VPN ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   远程设备操作的新体验 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   适用于企业的 Windows 应用商店应用 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   批量采购应用的一般改进 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Windows 信息保护 (WIP) ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   预声明具有 IMEI 或 iOS 序列号的企业自有设备 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   自动将设备分类到集合 ([1606](whats-new-hybrid-archive.md#new-in-1606-technical-preview))

有关新功能的信息，请参阅指定的 Technical Preview 版本的文档。

## <a name="notices"></a>通知

- **2016 年 10 月 25 日：已弃用的 Windows Phone 8 公司门户上传**

  已从 Configuration Manager 控制台中删除上传已签名的公司门户应用这一功能，因为即将禁用对 Windows 8、Windows Phone 8 和 Windows RT 的 Intune 支持，并且对 Windows Phone 8 公司门户的支持也将在 11 月结束。  将继续支持已注册的 Windows 8、Windows Phone 8 和 Windows RT 设备，但不再支持使用这些平台注册其他设备。


### <a name="see-also"></a>另请参阅

- [以前的混合 MDM 功能](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager 中的 MDM 的新增功能](https://technet.microsoft.com/library/mt445560.aspx)



<!--HONumber=Nov16_HO1-->


