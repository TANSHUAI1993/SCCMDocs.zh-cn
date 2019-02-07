---
title: 条件性访问
titleSuffix: Configuration Manager
description: 了解如何在 System Center Configuration Manager 中使用条件访问来帮助保护电子邮件和其他服务。
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 37688e1bf992e6b48f3d871f09b7b357453cfc3f
ms.sourcegitcommit: 33e066aceaf321add1031df00e552e942c8351a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2019
ms.locfileid: "55764338"
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理对服务的访问

适用范围：System Center Configuration Manager (Current Branch)

使用条件访问指定条件，从而帮助确保设备上通过 Microsoft Intune 注册的电子邮件和其他服务的安全。  

> [!Important]  
> 混合 MDM 包括本地条件性访问[已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。 有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<!--Intune feature 2683117-->  
> 
> 如果在使用 Configuration Manager 客户端管理的设备上使用条件性访问，以确保它们仍然受到保护，首次启用条件性访问在 Intune 中的为这些设备在迁移之前。 启用共同管理配置管理器中，将符合性策略工作负载移动到 Intune，然后完成从 Intune 混合版迁移到 Intune 独立版。 有关详细信息，请参阅[条件访问的共同管理](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access)。 


 有关使用 Configuration Manager 客户端管理的设备上的条件访问信息，请参阅[管理对由 System Center Configuration Manager 管理的电脑的 O365 服务的访问](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)。  


 条件性访问的典型流可能如下所示：  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 使用条件性访问管理对以下服务的访问：  

- Microsoft Exchange 内部部署  

- Microsoft Exchange Online  

- Exchange Online Dedicated  

- SharePoint Online  

- Skype for Business Online

- Dynamics CRM Online

  若要实现条件性访问，可以在 Configuration Manager 中配置两个策略类型：  

- “符合性策略” 是可选策略，你可以将其部署到用户集合并对设置进行评估，例如：  

  - 密码  

  - 加密  

  - 设备是否已越狱或取得 root 权限  

  - 设备上的电子邮件是由 Configuration Manager 策略还是由 Microsoft Intune 策略管理  

    如果不向设备部署任何符合性策略，则设备会为所有适用的条件访问策略报告符合性。

- 条件访问策略适用于特定服务。 这些策略定义规则，例如定义哪些 Azure Active Directory 安全用户组或 Configuration Manager 用户集合是策略目标或被策略排除。  

   可从 Configuration Manager 控制台配置本地 Exchange 条件访问策略。 但配置 Exchange Online 或 SharePoint Online 策略时，将打开 Microsoft Intune 控制台以配置策略。  

   与其他 Microsoft Intune 或 Configuration Manager 策略不同，你无需部署条件访问策略。 相反，你只需配置这些策略一次，它们将应用于所有目标用户。  

  如果设备不满足配置条件，用户会在指导下完成设备注册并修复设备符合性问题。  

在你开始使用条件性访问之前，请确保已经满足正确的要求：  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Exchange Online 的要求（使用共享多租户环境）
条件访问 Exchange Online 支持运行以下操作系统的设备：
- Windows 8.1 及更高版本（若已注册到 Intune）
- Windows 7.0 或 Windows 8.1（若已加入域）
- Windows Phone 8.1 及更高版本
- iOS 7.1 及更高版本
- Android 4.0 及更高版本、Samsung KNOX 标准版 4.0 及更高版本

  **此外**：
- 设备必须加入工作区，工作区将设备注册到 Azure Active Directory Device Registration 服务 (AAD DRS)。<br />     
- 已加入域的 PC 必须通过组策略或 MSI 自动注册到 Azure Active Directory。

  本文中的“电脑的条件访问”描述了启用电脑的条件访问的所有要求。<br />     
  AAD DRS 针对 Microsoft Intune 和 Office 365 客户自动激活。 已经部署了 ADFS 设备注册服务的用户不会在他们本地的 Active Directory 上看到已注册的设备。
- 使用包括 Exchange Online 的 Office 365 订阅（例如 E3）。 用户必须获得 Exchange online 许可。
- 可以选择使用“Exchange Server 连接器”，并将 Configuration Manager 连接到 Microsoft Exchange Online。 此连接器有助于通过 Configuration Manager 控制台监视设备信息。 有关详细信息，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。
  使用符合性策略或条件访问策略无需此连接器。 运行关于条件访问影响的报表需要此连接器。

## <a name="requirements-for-exchange-online-dedicated"></a>Exchange Online Dedicated 的要求
Exchange Online Dedicated 的条件性访问支持运行以下操作系统的设备：
- Windows 8 及更高版本（若已注册到 Intune）
- Windows 7.0 或 Windows 8.1（若已加入域）

  已加入域的 PC 的条件性访问仅针对新 Exchange Online 专用环境中的租户。
- Windows Phone 8 及更高版本
- 使用 Exchange ActiveSync (EAS) 电子邮件客户端的任何 iOS 设备
- Android 4 及更高版本。
- 对于旧 Exchange Online Dedicated 环境中的租户：    

  使用“Exchange Server 连接器”，将 Configuration Manager 连接到 Microsoft Exchange 内部部署。 该连接器使你可以管理移动设备并启用条件访问。 有关详细信息，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。
- 对于新 Exchange Online Dedicated 环境中的租户：     
  可以选择使用“Exchange Server 连接器”，将 Configuration Manager 连接到 Microsoft Exchange Online 并帮助管理设备信息。 有关详细信息，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。 使用符合性策略或条件访问策略无需此连接器。 运行关于条件访问影响的报表需要此连接器。  

## <a name="requirements-for-exchange-on-premises"></a>Exchange 内部部署的要求
Exchange 内部部署支持的条件访问：
-   Windows 8 及更高版本（若已注册到 Intune）
-   Windows Phone 8 及更高版本
-   iOS 上的本机电子邮件应用
-   Android 4 或更高版本上的本机电子邮件应用
-   不支持 Microsoft Outlook 应用（Android 和 iOS）

**此外**：

- Exchange 版本必须是 Exchange 2010 或更高版本
- 支持 Exchange Server 客户端访问服务器 (CAS) 阵列

> [!TIP]
> 如果你的 Exchange 环境在 CAS 服务器配置中，则必须将本地 Exchange 连接器配置为指向一个 CAS 服务器。
> - 使用“Exchange Server 连接器”，将 Configuration Manager 连接到 Microsoft Exchange 内部部署。 该连接器使你可以管理移动设备并启用条件访问。 有关详细信息，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。
>   - 请确保使用最新版本的本地 Exchange 连接器。 通过 Configuration Manager 控制台来配置本地 Exchange 连接器。 有关详细的演练，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。
>   - 仅在 Configuration Manager 主站点上配置连接器

- 可以使用基于证书的身份验证或用户凭据条目来配置 Exchange ActiveSync


## <a name="requirements-for-skype-for-business-online"></a>Skype for Business Online 的要求
条件访问 Skype Online 支持运行以下操作系统的设备：
 -   iOS 7.1 及更高版本
 -   Android 4.0 及更高版本
 -   Samsung KNOX 标准版 4.0 或更高版本

为 Skype for Business Online 启用[新式验证](https://aka.ms/SkypeModernAuth)。 

你的所有用户必须使用 Skype for Business Online。 如果部署中同时具有 Skype for Business Online 和本地 Skype for Business，则条件访问策略不会应用于本地用户。

## <a name="requirements-for-sharepoint-online"></a>SharePoint Online 的要求
条件访问至 SharePoint Online 支持运行以下操作系统的设备：
- Windows 8.1 及更高版本（若已注册到 Intune）
- Windows 7.0 或 Windows 8.1（若已加入域）
- Windows Phone 8.1 及更高版本
- iOS 7.1 及更高版本
- Android 4.0 及更高版本、Samsung KNOX 标准版 4.0 及更高版本

  **此外**：
- 设备必须加入工作区，工作区将设备注册到 Azure Active Directory Device Registration 服务 (AAD DRS)。

  已加入域的 PC 必须通过组策略或 MSI 自动注册到 Azure Active Directory。 本文中的“电脑的条件访问”描述了启用电脑的条件访问的所有要求。

  AAD DRS 针对 Microsoft Intune 和 Office 365 客户自动激活。 已经部署了 ADFS 设备注册服务的用户不会在他们本地的 Active Directory 上看到已注册的设备。
- SharePoint Online 订阅是必需的，并且用户必须获得 SharePoint Online 许可。

  ### <a name="conditional-access-for-pcs"></a>PC 的条件性访问

  可以为运行 Office 桌面应用程序的电脑配置条件访问，并访问 Exchange Online 或 SharePoint Online。 电脑必须满足以下要求：
- 电脑必须运行 Windows 7.0 或 Windows 8.1
- 电脑必须是已加入域的或符合的

  为了符合规范，电脑必须在 Microsoft Intune 中注册且符合相应策略。

  对于加入域的电脑，必须将它设置为 [自动向 Azure Active Directory 注册设备](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/) 。
- [Office 365 新式验证必须已启用](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)，且具有所有最新的 Office 更新。<br />     新式验证将基于 Active Directory 身份验证库 (ADAL) 的登录引入到 Office 2013 Windows 客户端中，并实现诸如“多重身份验证”和“基于证书的身份验证”等更佳的安全性。
- 安装 ADFS 声明规则以阻止非新式验证协议。  

## <a name="next-steps"></a>后续步骤  
 阅读以下主题，了解如何为你要求的方案配置合规性策略和条件性访问策略：  

-   [在 System Center Configuration Manager 中管理设备合规性策略](../../protect/deploy-use/device-compliance-policies.md)  

-   [在 System Center Configuration Manager 中管理对电子邮件的访问](../../protect/deploy-use/manage-email-access.md)  

-   [在 System Center Configuration Manager 中管理 SharePoint Online 访问](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [管理 Skype for Business Online 访问权限](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>另请参阅  

 [System Center Configuration Manager 中的符合性设置入门](../../compliance/get-started/get-started-with-compliance-settings.md)
