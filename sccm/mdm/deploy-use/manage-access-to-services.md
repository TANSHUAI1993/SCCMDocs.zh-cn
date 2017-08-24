---
title: "条件访问 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用条件访问来帮助保护电子邮件和其他服务。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: "26"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: d6933a331bb229f7e378e8f0bfa511f6b0553ae9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理对服务的访问

*适用范围：System Center Configuration Manager (Current Branch)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的条件访问
使用“条件访问”，根据指定的条件帮助确保设备上通过 Microsoft Intune 注册的电子邮件和其他服务的安全。  

 有关**使用 System Center Configuration Manager 管理并进行合规性评估的电脑上的条件访问**的信息，请参阅 [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)（管理由 System Center Configuration Manager 管理的电脑的 O365 服务的访问权限）。  


 条件性访问的典型流可能如下所示：  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 使用条件性访问管理对以下服务的访问：  

-   Microsoft Exchange 内部部署  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated  

-   SharePoint Online  

-   Skype for Business Online

-   Dynamics CRM Online

 若要实现条件性访问，可以在 Configuration Manager 中配置两个策略类型：  

-   “符合性策略” 是可选策略，你可以将其部署到用户集合并对设置进行评估，例如：  

    -   密码  

    -   加密  

    -   设备是否已越狱或取得 root 权限  

    -   设备上的电子邮件是由 Configuration Manager 策略还是由 Intune 策略管理  

     **如果未向设备部署合规性策略，则任何适用的条件性访问策略都会将该设备视为合规**。  

-   “条件性访问策略”针对特定服务而配置，并定义相应规则，如哪些 Azure Active Directory 安全用户组或 Configuration Manager 用户集合将被设为目标或豁免。  

     可从 Configuration Manager 控制台配置本地 Exchange 条件性访问策略。 但是，当配置 Exchange Online 或 SharePoint Online 策略时，将打开 Intune 管理控制台用于配置策略。  

     与其他 Intune 或 Configuration Manager 策略不同，不用部署条件性访问策略。 相反，你只需配置这些策略一次，它们将应用于所有目标用户。  

 当设备不满足你配置的条件时，将指导用户完成注册设备并修复阻止设备合规的问题的流程。  

在开始使用条件性访问**之前**，请确保已经满足正确的**要求**：  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Exchange Online 的要求（使用共享多租户环境）
条件访问 Exchange Online 支持运行以下操作系统的设备：
-   Windows 8.1 及更高版本（若已注册到 Intune）
-   Windows 7.0 或 Windows 8.1（若已加入域）
-   Windows Phone 8.1 及更高版本
-   iOS 7.1 及更高版本
-   Android 4.0 及更高版本、Samsung KNOX 标准版 4.0 及更高版本

 **此外**：
-   设备必须加入工作区，工作区将设备注册到 Azure Active Directory Device Registration 服务 (AAD DRS)。<br />     
- 已加入域的 PC 必须通过组策略或 MSI 自动注册到 Azure Active Directory。

  本主题中的“PC 的条件性访问”  描述了启用 PC 的条件性访问的所有要求。<br />     
  AAD DRS 将对 Intune 和 Office 365 客户自动激活。 已经部署了 ADFS 设备注册服务的用户将不会在他们本地的 Active Directory 上看到已注册的设备。
-   你必须使用包含 Exchange Online（例如 E3）的 Office 365 订阅，并且用户必须获得 Exchange Online 许可。
-   **Exchange Server 连接器** 是可选的，其可将 Configuration Manager 连接到 Microsoft Exchange Online 并且有助于通过 Configuration Manager 控制台监视设备信息（请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)）。
你不需要使用连接器来使用合规性策略或条件性访问策略，但要求你运行帮助评估条件性访问影响的报告。

## <a name="requirements-for-exchange-online-dedicated"></a>Exchange Online Dedicated 的要求
Exchange Online Dedicated 的条件性访问支持运行以下操作系统的设备：
-   Windows 8 及更高版本（若已注册到 Intune）
-   Windows 7.0 或 Windows 8.1（若已加入域）

  已加入域的 PC 的条件性访问仅针对新 Exchange Online 专用环境中的租户。
-   Windows Phone 8 及更高版本
-   使用 Exchange ActiveSync (EAS) 电子邮件客户端的任何 iOS 设备
-   Android 4 及更高版本。
-   对于**旧 Exchange Online Dedicated 环境**中的租户：    

  必须使用“Exchange Server 连接器”，它会将 Configuration Manager 连接到 Microsoft Exchange 内部部署）。 由此你可以管理移动设备并启用条件访问（请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)）。
-   对于**新 Exchange Online Dedicated 环境**中的租户：     
  可选的“Exchange Server 连接器”会将 Configuration Manager 连接到 Microsoft Exchange Online 并且帮助管理设备信息（请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)）。 你不需要使用连接器来使用合规性策略或条件性访问策略，但要求你运行帮助评估条件性访问影响的报告。  

## <a name="requirements-for-exchange-on-premises"></a>Exchange 内部部署的要求
Exchange 内部部署支持的条件性访问：
-   Windows 8 及更高版本（若已注册到 Intune）
-   Windows Phone 8 及更高版本
-   iOS 上的本机电子邮件应用
-   Android 4 或更高版本上的本机电子邮件应用
-   不支持 Microsoft Outlook 应用（Android 和 iOS）。

**此外**：

-  Exchange 版本必须是 Exchange 2010 或更高版本。 支持 Exchange Server 客户端访问服务器 (CAS) 阵列。

> [!TIP]
> 如果你的 Exchange 环境在 CAS 服务器配置中，则必须将本地 Exchange 连接器配置为指向一个 CAS 服务器。
- 必须使用“Exchange Server 连接器”，它会将 Configuration Manager 连接到 Microsoft Exchange 内部部署。 由此你可以管理移动设备并启用条件访问（请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)）。
  - 请确保使用最新版本的 **内部部署 Exchange 连接器**。 应通过 Configuration Manager 控制台来配置本地 Exchange 连接器。 有关详细的演练，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。
  - 连接器仅可在 System Center Configuration Manager 主站点上进行配置。</li><li>此连接器支持 Exchange CAS 环境。 <br />        在配置连接器时，必须对其进行设置，以便与一个 Exchange CAS 服务器通信。

- 可以基于身份验证或用户凭据条目使用证书来配置 Exchange ActiveSync


## <a name="requirements-for-skype-for-business-online"></a>Skype for Business Online 的要求
条件访问至 SharePoint Online 支持运行以下操作系统的设备：
 -   iOS 7.1 及更高版本
 -   Android 4.0 及更高版本
 -   Samsung KNOX 标准版 4.0 或更高版本

**此外**，必须为 Skype for Business Online 启用新式验证。 填充该 [连接窗体](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) 以在新式验证程序中注册。

所有最终用户都必须使用 Skype for Business Online。 如果你的部署同时具有 Skype for Business Online 和本地 Skype for Business，则条件访问策略不会应用于处于本地部署中的最终用户。

## <a name="requirements-for-sharepoint-online"></a>SharePoint Online 的要求
条件访问至 SharePoint Online 支持运行以下操作系统的设备：
 -   Windows 8.1 及更高版本（若已注册到 Intune）
 -   Windows 7.0 或 Windows 8.1（若已加入域）
 -   Windows Phone 8.1 及更高版本
 -   iOS 7.1 及更高版本
 -   Android 4.0 及更高版本、Samsung KNOX 标准版 4.0 及更高版本

 **此外**：
 -   设备必须加入工作区，工作区将设备注册到 Azure Active Directory Device Registration 服务 (AAD DRS)。

 已加入域的 PC 必须通过组策略或 MSI 自动注册到 Azure Active Directory。 本主题中的“PC 的条件性访问”  描述了启用 PC 的条件性访问的所有要求。

 AAD DRS 将对 Intune 和 Office 365 客户自动激活。 已经部署了 ADFS 设备注册服务的用户将不会在他们本地的 Active Directory 上看到已注册的设备。
 -   SharePoint Online 订阅是必需的，并且用户必须获得 SharePoint Online 许可。

 ### <a name="conditional-access-for-pcs"></a>PC 的条件性访问

 你可以设置 PC 的条件性访问以访问满足以下要求的 PC 的“Exchange Online”  和“SharePoint Online”  ，其中该 PC 运行 Office 桌面应用程序：
 -   电脑必须运行 Windows 7.0 或 Windows 8.1。
 -   PC 必须已加入域或必须合规。

 为了符合规范，PC 必须在 Intune 中进行注册且符合相应策略。

 对于加入域的电脑，必须将它设置为 [自动向 Azure Active Directory 注册设备](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) 。
 -   [Office 365 新式验证必须已启用](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)，且具有所有最新的 Office 更新。<br />     新式验证将基于 Active Directory 身份验证库 (ADAL) 的登录引入到 Office 2013 Windows 客户端中，并实现诸如“多重身份验证” 和“基于证书的身份验证” 等更佳的安全性。
 -   安装 ADFS 声明规则以阻止非新式验证协议。  

## <a name="next-steps"></a>后续步骤  
 阅读以下主题，了解如何为你要求的方案配置合规性策略和条件性访问策略：  

-   [在 System Center Configuration Manager 中管理设备合规性策略](../../protect/deploy-use/device-compliance-policies.md)  

-   [在 System Center Configuration Manager 中管理对电子邮件的访问](../../protect/deploy-use/manage-email-access.md)  

-   [在 System Center Configuration Manager 中管理 SharePoint Online 访问](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [管理 Skype for Business Online 访问权限](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>另请参阅  

 [System Center Configuration Manager 中的符合性设置入门](../../compliance/get-started/get-started-with-compliance-settings.md)
