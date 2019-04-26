---
title: 管理 SharePoint Online 访问
titleSuffix: Configuration Manager
description: 了解如何使用 System Center Configuration Manager SharePoint Online 条件访问策略管理对 OneDrive 的访问。
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 69a160a3c7833f196d50185e551f619d68dc0925
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62255550"
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理 SharePoint Online 访问

适用范围：System Center Configuration Manager (Current Branch)


SharePoint Online 的 Configuration Manager 条件访问策略可管理对 OneDrive for Business 文件（存储在 SharePoint Online 上）的访问。 根据所指定的条件进行访问。
你可以从所列平台的以下应用中控制对 SharePoint Online 的访问：  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive（Android 和 iOS）  

-   Microsoft Word（Android 和 iOS）  

-   Microsoft Excel（Android 和 iOS）  

-   Microsoft PowerPoint（Android 和 iOS）  

-   Microsoft OneNote（Android 和 iOS）

Office 桌面应用程序可以访问运行以下系统的电脑上的 SharePoint Online：  

-   已启用 [新式身份验证](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) 的 Office 桌面 2013及更高版本。  

-   Windows 7.0 或 Windows 8.1  

> [!NOTE]  
>  电脑应已加入域或符合 Intune 中设置的策略。  



 当目标用户尝试在其设备上使用支持的应用（如 OneDrive）连接到文件时，进行以下评估：  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 若要连接到所需文件，运行 OneDrive 的设备必须：  

- 已向 Microsoft Intune 注册或是已加入域的电脑。  

- 在 Azure Active Directory (Azure AD) 中注册设备。 向 Intune 注册设备时进行此项注册。  

   对于加入域的电脑，必须将其设置为向 Azure AD [自动注册](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)。  

- 符合任何已部署的 Configuration Manager 合规性策略  

  Azure AD 保存设备状态。 它根据指定的条件授权访问或阻止访问文件。  

  如果不满足条件，用户在登录时将看到下述某条消息：  

- 如果未向 Intune 注册或未在 Azure AD 中注册设备，会显示一条消息，说明如何安装公司门户应用并进行注册。  

- 如果设备不符合条件，会显示一条消息将用户转到 Intune Web 门户。 可在此处找到问题的详细信息和纠正方法。  

- 对于移动设备：

  使用 iOS 和 Android 设备的浏览器访问时，可限制对 SharePoint Online 的访问。 仅允许通过合规设备上受支持的浏览器进行访问：  
  - Safari (iOS)
  - Chrome (Android)
  - Managed Browser（iOS 和 Android）  

    阻止不受支持的浏览器的访问。  

- 对于 PC：  


  -   如果策略设置为需要加入域，而电脑未加入域，将显示“请与 IT 管理员联系”消息。  

  -   如果策略设置为要求加入域或必须符合，而电脑不满足某项要求，将显示一条消息，其中说明了如何安装公司门户应用和进行注册。  

你可以从以下应用阻止对 SharePoint Online 的访问：  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive（Android 和 iOS）  

-   Microsoft Word（Android 和 iOS）  

-   Microsoft Excel（Android 和 iOS）  

-   Microsoft PowerPoint（Android 和 iOS）  

-   Microsoft OneNote（Android 和 iOS）  



## <a name="configure-conditional-access-for-sharepoint-online"></a>为 SharePoint Online 配置条件访问  

### <a name="step-1-configure-active-directory-security-groups"></a>步骤 1：配置 Active Directory 安全组  
 在开始之前，请针对条件访问策略配置 Azure AD 安全组。 你可以配置这些组中的**Microsoft 365 管理中心**，或**Intune 帐户门户**。 这些组包含要作为目标或者要从策略中免除的用户。 如果将某用户设定为策略的目标，则其使用的每台设备必须符合条件才能访问资源。  

 你可以在 SharePoint Online 策略中指定两种组类型：  

- **目标组**:包含该策略应用用户的组  

- **免除组**:包含是从 （可选） 策略中免除的用户的组  

  如果某用户存在于这两个组，则将其从策略中免除。  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>步骤 2:配置和部署合规性策略  
 创建符合性策略，并将其部署到设为 SharePoint Online 策略目标的所有设备。  

> [!NOTE]   
>  将符合性策略部署到 Intune 组或 Configuration Manager 集合，而条件访问策略以 Azure AD 安全组为目标。  

 有关如何配置合规性策略的详细信息，请参阅[管理 System Center Configuration Manager 中的设备合规性策略](../../protect/deploy-use/device-compliance-policies.md)。  

> [!IMPORTANT]  
>  如果尚未部署符合性策略，但之后启用了 SharePoint Online 策略，则用户可访问所有目标设备。  

   

###  <a name="BKMK_OneDrive"></a>步骤 3：配置 SharePoint Online 策略  

 接下来，配置策略以要求只有托管及合规设备才能访问 SharePoint Online。 此策略存储在 Azure AD 中。

 >[!NOTE]
 >此外，还可在 Azure AD 管理控制台中创建条件访问策略。 可通过 Azure AD 管理控制台创建 Intune 设备条件访问策略。 Azure AD 将这些策略称为基于设备的条件访问策略。 还可创建其他条件访问策略，例如多重身份验证。 可在门户中为 Azure AD 支持的第三方企业应用（如 Salesforce 和 Box）设置条件访问策略。 有关详细信息，请参阅[如何将基于 Azure AD 设备的条件访问策略设置为控制到 Azure AD 连接的应用程序的访问](/azure/active-directory/active-directory-conditional-access-policy-connected-applications)。  

1. 在 Configuration Manager 控制台中，单击“资产和符合性”。  

2. 选择“启用 SharePoint Online 的条件访问策略”。  

    ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3. 在使用新式验证的 Outlook 和应用的“应用程序访问”下，可以选择将访问仅限为对每个平台合规的设备。  

   > [!TIP]
   >  通过“新式验证”，用户可基于 Active Directory 身份验证库 (ADAL) 登录到 Office 客户端。  
   > 
   > - Office 客户端可通过基于 ADAL 的身份验证参与基于浏览器的身份验证（也称为被动身份验证）。 为了进行身份验证，用户将被导向登录网页。  
   >   -   这种全新的登录方法带来了新的应用情景，例如根据设备符合性以及是否执行多重身份验证进行条件访问。  
   > 
   >   有关详细信息，请参阅[适用于 Office 2013 和 Office 2016 客户端应用的新式验证工作原理](https://support.office.com/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517)。  

    Windows 电脑必须加入域，或是向 Intune 注册并合规。 可以设置以下要求：  

   -   **设备必须已加入域或符合**:Pc 必须已加入域或符合在 Intune 中设置的策略。 如果电脑不满足任一要求，系统会提示用户向 Intune 注册设备。  

   -   **设备必须已加入域**:Pc 必须加入域才能访问 Exchange Online。 如果电脑未加入域，系统会阻止对电子邮件的访问，且提示用户与 IT 管理员联系。  

   -   **设备必须合规**:电脑必须注册 Intune 且符合。 如果电脑未注册，系统会显示一条消息，其中包含注册方式的相关说明。  

4. 下**浏览器访问**SharePoint Online 和 OneDrive for Business，你可以选择允许访问 Exchange Online 仅通过支持的浏览器：Safari (iOS) 和 Chrome (Android)。 阻止来自其他浏览器的访问。 你为 OneDrive 应用程序访问选择的平台限制在此处同样适用。

   在 Android 设备上，用户必须在注册的设备上打开“启用浏览器访问”选项，如下所示：
   1.  启动“公司门户应用”。
   2.  从三个点 (…) 或硬件菜单按钮转到“设置”页。
   3.  按“启用浏览器访问”按钮。
   4.  在 Chrome 浏览器中注销 Office 365 并重新启动 Chrome。

   在 iOS 和 Android 平台上，Azure AD 向设备颁发 TLS 证书，用于识别访问服务时所用的设备。 设备显示证书时会出现提示，向最终用户选择的证书，如以下屏幕截图中所示：最终用户必须选择此证书，然后它们可以继续使用浏览器。

    **iOS**

    ![iPad 上的证书提示屏幕截图](media/mdm-browser-ca-ios-cert-prompt_v2.png)

    **Outlook Web Access (OWA)**

     ![Android 设备上证书提示的屏幕截图](media/mdm-browser-ca-android-cert-prompt.png)

5. 在“主页”  选项卡的“链接”  组，单击“在 Intune 控制台中配置条件性访问策略” 。 你可能需要提供用于连接 Configuration Manager 和 Intune 的帐户的用户名和密码。  

    随即将打开 Intune 管理控制台。  

6. 在 [Microsoft Intune 管理控制台](https://manage.microsoft.com)中，单击“策略” > “条件访问” > “SharePoint Online 策略”。  

7. 选择 **如果该设备不符合要求，阻止应用访问 SharePoint Online**。  

8. 在“目标组”下单击“修改”，选择要应用策略的 Azure AD 安全组。  

9. 在“免除组”下单击“修改”，选择要从此策略中免除的 Azure AD 安全组。  

10. 完成后，请单击“保存” 。  

    条件访问策略将立即生效，无需进行部署。  

    请参阅[使用 Microsoft Intune 管理 SharePoint Online 访问](/intune-classic/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)，了解有关如何监视 Intune 控制台中的策略的信息。  

### <a name="see-also"></a>另请参阅  

 [在 System Center Configuration Manager 中管理对服务的访问](../../protect/deploy-use/manage-access-to-services.md)
