---
title: "管理 SharePoint Online 访问 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager SharePoint Online 条件访问策略管理对 OneDrive 的访问。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
caps.latest.revision: 11
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 58a82b29743cb37a5d358f020cf11b91d6f6f42e
ms.contentlocale: zh-cn
ms.lasthandoff: 03/06/2017


---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理 SharePoint Online 访问

*适用范围：System Center Configuration Manager (Current Branch)*


使用 System Center Configuration Manager **SharePoint Online** 条件访问策略，根据指定条件，管理对位于 SharePoint Online 上的 OneDrive for Business 文件的访问。
你可以从所列平台的以下应用中控制对 SharePoint Online 的访问：  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive（Android 和 iOS）  

-   Microsoft Word（Android 和 iOS）  

-   Microsoft Excel（Android 和 iOS）  

-   Microsoft PowerPoint（Android 和 iOS）  

-   Microsoft OneNote（Android 和 iOS）

Office 桌面应用程序可以访问运行以下系统的电脑上的 SharePoint Online：  

-   已启用 [新式身份验证](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) 的 Office 桌面 2013及更高版本。  

-   Windows 7.0 或 Windows 8.1  

> [!NOTE]  
>  电脑应已加入域或符合 Intune 中设置的策略。  



 当目标用户尝试在其设备上使用支持的应用（如 OneDrive）连接到文件时，会进行以下评估：  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 若要连接到所需文件，运行 OneDrive 的设备必须：  

-   已向 Microsoft Intune 注册或是已加入域的电脑。  

-   在 Azure Active Directory 中注册设备（向 Intune 注册设备时会自动发生此情况）。  

     对于加入域的 PC，必须将它设置为向 Azure Active Directory [自动注册](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) 。  

-   符合任何已部署的 Configuration Manager 合规性策略  

 基于指定的条件，设备状态存储在可授予或阻止对文件的访问权限的 Azure Active Directory 中。  

 如果不满足条件，则用户将在登录时看到以下消息的其中一条：  

-   如果设备未向 Intune 注册，或未在 Azure Active Directory 中注册，则会显示一条消息，说明如何安装公司门户应用并进行注册。  

-   如果设备不合规，则显示一条消息，将用户定向到 Intune Web 门户，用户可在该门户中找到有关问题及其解决方式的信息。  

- 对于移动设备：

  当使用 **iOS** 和 **Android** 设备的浏览器访问时，可以阻止对 SharePoint Online 的访问。  只允许在合规设备上使用受支持的浏览器进行访问：
* Safari (iOS)
* Chrome (Android)
* Managed Browser（iOS 和 Android）

  将阻止不受支持的浏览器。
-   对于 PC：  


    -   如果策略设置为要求加入域，而 PC 未加入域，则会显示一条与 IT 管理员联系的消息。  

    -   如果策略设置要求加入域或合规，而 PC 不符合任一要求，则会显示一条消息，其中包含有关如何安装公司门户应用和注册的说明。  

 你可以从以下应用阻止对 SharePoint Online 的访问：  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive（Android 和 iOS）  

-   Microsoft Word（Android 和 iOS）  

-   Microsoft Excel（Android 和 iOS）  

-   Microsoft PowerPoint（Android 和 iOS）  

-   Microsoft OneNote（Android 和 iOS）  

## <a name="configure-conditional-access-for-sharepoint-online"></a>为 SharePoint Online 配置条件访问  

### <a name="step-1-configure-active-directory-security-groups"></a>步骤 1：配置 Active Directory 安全组  
 在开始之前，针对条件访问策略配置 Azure Active Directory 安全组。 你可以在 **“Office 365 管理中心”**，或 **“Intune 帐户门户”**中配置这些组。 这些组包含将作为目标的用户，或从策略中免除的用户。 如果将某个用户设定为策略的目标，则其使用的每个设备必须合规才能访问资源。  

 你可以在 SharePoint Online 策略中指定两种组类型：  

-   **目标组** - 包含将应用策略的用户组  

-   **免除组** - 包含从策略中免除的用户组（可选）  

 如果用户位于两个组中，则会将其从策略中免除。  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>步骤 2：配置和部署合规性策略  
 确保你创建合规性策略并将其部署到设定为 SharePoint Online 策略的目标的所有设备。  

> [!NOTE]  
>  将合规性策略部署到 Intune 组或 Configuration Manager 集合，而条件访问策略以 Azure Active Directory 安全组为目标。  

 有关如何配置合规性策略的详细信息，请参阅[管理 System Center Configuration Manager 中的设备合规性策略](../../protect/deploy-use/device-compliance-policies.md)。  

> [!IMPORTANT]  
>  如果你尚未部署合规性策略，但是启用了 SharePoint Online 策略，则允许所有目标设备进行访问。  

 准备就绪后，继续 **步骤 3**。  

###  <a name="BKMK_OneDrive"></a>步骤 3：配置 SharePoint Online 策略  


 接下来，配置策略以要求只有托管及合规设备才能访问 SharePoint Online。 此策略会存储在 Azure Active Directory 中。

 >[!NOTE]
 >此外，还可在 Azure AD 管理控制台中创建条件访问策略。 除多重身份验证之类的其他条件访问策略之外，Azure AD 管理控制台还允许创建 Intune 设备条件访问策略（在 Azure AD 中称为基于设备的条件访问策略）。 还可为第三方企业应用（如 Azure AD 支持的 Salesforce 和 Box）设置条件访问策略。 有关详细信息，请参阅[如何设置基于 Azure Active Directory 设备的条件访问策略，用于控制对 Azure Active Directory 连接的应用程序的访问](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/)。  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  选择“启用 SharePoint Online 的条件访问策略” 。  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  在使用新式验证的 Outlook 和应用的“应用程序访问”下，可以选择将访问仅限为对每个平台合规的设备。  

    > [!TIP]  
    >  “新式验证” 允许基于 Active Directory 身份验证库 (ADAL) 登录到 Office 客户端。  
    >   
    >  -   基于 ADAL 的身份验证使 Office 客户端能够实现基于浏览器的身份验证（也称为被动身份验证）。  为了进行身份验证，用户将被导向登录网页。  
    > -   这种全新的登录方法实现了新的方案，如基于“设备符合性”  以及“多重身份验证”  执行情况的条件访问。  
    >   
    >  有关新式身份验证工作原理的更多详细信息，请参阅本 [文章](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) 。  

     Windows 电脑必须加入域，或是向 Intune 注册并合规。 可以设置以下要求：  

    -   **设备必须已加入域或必须是合规的。** 这意味着电脑必须已加入域或符合在 Intune 中设置的策略。 如果电脑不满足任一要求，则系统会提示用户向 Intune 注册设备。  

    -   **设备必须已加入域。** 这意味着 PC 必须加入域才能访问 Exchange Online。 如果 PC 未加入域，则系统会阻止对电子邮件的访问，并且提示用户与 IT 管理员联系。  

    -   **设备必须是合规的。** 这意味着电脑必须在 Intune 中注册并合规。 如果 PC 未注册，则会显示一条消息，其中包含有关如何注册的说明。  

4.  在 SharePoint Online 和 OneDrive for Business 的“浏览器访问权限”中，你可以选择只允许通过受支持的浏览器访问 Exchange Online：Safari (iOS) 和 Chrome (Android)。 将阻止来自其他浏览器的访问。  你为 OneDrive 应用程序访问选择的平台限制在此处同样适用。

    在 **Android** 设备上，用户必须启用浏览器访问。  若要执行此操作，最终用户必须在注册的设备上启用“启用浏览器访问”选项，如下所示：
    1.  启动“公司门户应用”。
    2.  从三个点 (…) 或硬件菜单按钮转到“设置”页。
    3.  按“启用浏览器访问”按钮。
    4.  在 Chrome 浏览器中注销 Office 365 并重新启动 Chrome。

    在 **iOS 和 Android** 平台上，为了识别用于访问服务的设备，Azure Active Directory 将向该设备颁发一个传输层安全性 (TLS) 证书。  该设备在显示证书时会出现提示，让最终用户选择证书，如以下屏幕截图所示。 最终用户必须选择此证书后，才能继续使用该浏览器。

     **Android**

     ![ipad 上证书提示的屏幕截图](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Outlook Web Access (OWA)**

      ![Android 设备上证书提示的屏幕截图](media/mdm-browser-ca-android-cert-prompt.png)

4.  在“主页”  选项卡的“链接”  组，单击“在 Intune 控制台中配置条件性访问策略” 。 你可能需要提供用于连接 Configuration Manager 和 Intune 的帐户的用户名和密码。  

     随即将打开 Intune 管理控制台。  

5.  在 [Microsoft Intune 管理控制台](https://manage.microsoft.com)中，单击“策略” > “条件访问” > “SharePoint Online 策略”。  

6.  选择 **如果该设备不符合要求，阻止应用访问 SharePoint Online**。  

7.  在“目标组” 下，单击“修改”  以选择将应用策略的 Azure Active Directory 安全组。  

8.  在“免除组” 下，可以选择“修改”  以选择从此策略中免除的 Azure Active Directory 安全组。  

9. 完成后，请单击“保存” 。  

 不需要部署条件访问策略，它将立即生效。  

 请参阅[使用 Microsoft Intune 管理 SharePoint Online 访问](https://technet.microsoft.com/library/dn705844.aspx)，了解有关如何监视 Intune 控制台中的策略的信息。  

### <a name="see-also"></a>另请参阅  

 [在 System Center Configuration Manager 中管理对服务的访问](../../protect/deploy-use/manage-access-to-services.md)

