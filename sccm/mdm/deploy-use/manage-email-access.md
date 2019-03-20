---
title: 管理电子邮件访问权限
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 条件访问管理对 Exchange 电子邮件的访问权限。
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ee4ed8f102507b4d62a1ccbfe1cc38240e85df9
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196851"
---
# <a name="manage-email-access-in-configuration-manager"></a>管理 Configuration Manager 中的电子邮件访问

适用范围：System Center Configuration Manager (Current Branch)

使用 Configuration Manager 条件访问来管理对 Exchange 电子邮件基于你指定的条件访问中。  

你可以管理对以下内容的访问权限：  

- Microsoft Exchange 内部部署  

- Microsoft Exchange Online  

- Exchange Online Dedicated  

你可以从以下平台上的内置电子邮件客户端控制对 Exchange Online 和 Exchange 内部部署的访问：  

- Android 4.0 及更高版本、Samsung KNOX 标准版 4.0 及更高版本  

- iOS 9.0 及更高版本  

- Windows Phone 8.1 及更高版本  

- Windows 8.1 和更高版本上的邮件应用程序  

Office 桌面应用程序可以访问运行以下系统的电脑上的 Exchange Online：  

- 已启用 [新式身份验证](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) 的 Office 桌面 2013及更高版本。  

- Windows 7.0 或 Windows 8.1  

> [!NOTE]  
> 电脑应已加入域或符合在 Intune 中设置的策略。  


## <a name="device-requirements"></a>设备要求
如果在用户可以连接到其电子邮件之前配置条件访问，那么他们使用的设备必须：  

- 已向 Intune 注册或是已加入域的电脑。  

- 在 Azure Active Directory 中注册设备（设备在注册 Intune 时会自动发生此情况（仅限 Exchange Online））。 此外，必须已向 Azure Active Directory 注册客户端 Exchange ActiveSync ID（不适用于连接到 Exchange 内部部署的 Windows 和 Windows Phone 设备）。  

    对于加入域的 PC，必须将它设置为自动向 Azure Active Directory 注册。 **的电脑进行条件性访问**主题中[管理对服务的访问](../../protect/deploy-use/manage-access-to-services.md)文章列出了为 Pc 启用条件性访问的要求的完整集。  

- 符合任何部署到该设备的 Configuration Manager 符合性策略  

    如果不满足条件性访问条件，用户将看到以下消息之一，在登录时：  

- 如果设备未向 Intune 注册或未在 Azure Active Directory 中注册，说明如何安装公司门户应用、 注册设备，和 （适用于 Android 和 iOS 设备），激活电子邮件，这将显示一条消息设备的 Exchange ActiveSync ID 与 Azure Active Directory 中的设备记录。  

- 如果设备不合规，将显示一条消息，将定向到 Intune web 门户，用户可以在其中找到有关问题的信息及其修正方式的用户。  

#### <a name="for-mobile-devices"></a>为移动设备

当使用 **iOS** 和 **Android** 设备的浏览器访问时，可以阻止对 Exchange Online 上的 **Outlook Web Access (OWA)** 的访问。 只允许在合规设备上使用受支持的浏览器进行访问：  

- Safari (iOS)  
- Chrome (Android)  
- Managed Browser（iOS 和 Android）  

将阻止不受支持的浏览器。 适用于 iOS 和 Android 的 OWA 应用不受支持。 将通过 ADFS 声明规则对其进行阻止：  

- 安装 ADFS 声明规则以阻止非新式验证协议。 方案 3 中提供了详细的说明[阻止除基于浏览器应用程序的所有访问 Office 365](https://technet.microsoft.com/library/dn592182.aspx)。  

#### <a name="for-pcs"></a>为电脑

- 如果条件访问策略要求是允许“已加入域”  或“合规” ，则会显示一条消息，其中包含有关如何注册设备的说明。 如果电脑不满足任一要求，则系统会要求用户向 Intune 注册设备。  

- 如果条件访问策略要求设置为只允许加入域的 Windows 设备，则会阻止设备并显示一条与 IT 管理员联系的消息。  

在以下平台上，你可以从设备内置 Exchange ActiveSync 电子邮件客户端阻止对 Exchange 电子邮件的访问：  

- Android 4.0 及更高版本、Samsung KNOX 标准版 4.0 及更高版本  

- iOS 9.0 及更高版本  

- Windows Phone 8.1 及更高版本  

- Windows 8.1 及更高版本上的 **“邮件”** 应用程序  

Exchange Online 仅支持适用于 iOS 和 Android 的 Outlook 应用以及 Outlook 桌面 2013 和更高版本。  

运行条件性访问需要 Configuration Manager 和 Exchange 之间的**本地 Exchange Connector**。  

可从 Configuration Manager 控制台为 Exchange 内部部署配置条件访问策略。 为 Exchange Online 配置条件访问策略时，可以在 Configuration Manager 控制台中开始此过程，这将启动 Intune 控制台，可在其中完成该过程。  



## <a name="configure-conditional-access"></a>配置条件访问

### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>步骤 1:评估条件性访问策略的影响  

配置后**内部部署 Exchange 连接器**，可以使用 Configuration Manager**按条件访问状态的设备列表**报告，以确定将阻止的设备在配置条件性访问策略后，请访问 Exchange。 此报表还要求：  

- 订阅 Intune  

- 应配置和部署服务连接点  

在报表参数中，选择想要评估的 Intune 组，并在必要时选择策略将应用到的设备平台。  

有关如何运行报告的详细信息，请参阅 [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting)。  

运行报表后，检查以下四列以确定是否将阻止用户：  

- **管理通道**:设备由 Intune、 Exchange ActiveSync 和 / 或管理。  

- **已向 AAD 注册**:设备注册到 Azure Active Directory （称为工作区加入） 中。  

- **符合**：设备不符合任何已部署的符合性策略。  

- **已激活 EAS**: iOS 和 Android 设备需要具有与 Azure Active Directory 中的设备注册记录相关联的 Exchange ActiveSync ID。 当用户单击隔离电子邮件中的“激活电子邮件”  链接时，将发生这种情况。  

    > [!NOTE]  
    > Windows Phone 设备始终在此列中显示一个值。  

对于属于目标组或集合的设备，将阻止其访问 Exchange，除非列值与下表中列出的值匹配：  

|管理通道|已向 ADD 注册|合规|已激活 EAS|产生的操作|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**由 Microsoft Intune 和 Exchange ActiveSync 管理**|是|是|显示“是” 或“否” |允许电子邮件访问|  
|任何其他值|否|否|不显示任何值|阻止电子邮件访问|  

你可以导出报表的内容，并使用 **“电子邮件地址”** 列来帮助你通知用户他们将被阻止。  


### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>步骤 2:为条件性访问策略配置用户组或集合  

将条件性访问策略的目标设定为不同的用户组或集合，具体取决于策略类型。 这些组包含将作为目标的用户，或从策略中免除的用户。 如果将某个用户设定为策略的目标，则其使用的每个设备必须合规才能访问电子邮件。  

- **对于 Exchange Online 策略**： 为 Azure Active Directory 安全用户组。 你可以配置这些组中的**Microsoft 365 管理中心**，或**Intune 帐户门户**。  

- **对于 Exchange 内部部署策略**： 到 Configuration Manager 用户集合。 你可以在“资产和符合性”  工作区中进行配置。  

你可以在每个策略中指定两种组类型：  

- **目标组**:策略应用到的用户组或集合  

- **免除组**:从 （可选） 策略中免除的用户组或集合  

如果用户位于两个组中，则会将其从策略中免除。  

仅会对条件性访问策略面向的组或集合评估 Exchange 访问权限。  


### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>步骤 3:配置和部署合规性策略  

确保你已创建合规性策略并将其部署到设定为 Exchange 条件访问策略的目标的所有设备。  

有关如何配置符合性策略的详细信息，请参阅[管理设备符合性策略](device-compliance-policies.md)。  

> [!IMPORTANT]  
> 如果你尚未部署合规性策略，但是启用了 Exchange 条件性访问策略，访问将允许所有目标的设备。  


### <a name="step-4-configure-the-conditional-access-policy"></a>步骤 4:配置条件性访问策略  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>对于 Exchange Online（和新 Exchange Online Dedicated 环境中的租户）

> [!NOTE]  
> 此外，还可在 Azure AD 管理控制台中创建条件访问策略。 除多重身份验证之类的其他条件访问策略之外，Azure AD 管理控制台还允许创建 Intune 设备条件访问策略（在 Azure AD 中称为基于设备的条件访问策略）。 还可为第三方企业应用（如 Azure AD 支持的 Salesforce 和 Box）设置条件访问策略。 有关更多详细信息，请参阅[How To:需要使用条件性访问的云应用访问权限的被管理的设备](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)。  

Exchange Online 的条件访问策略使用下面的流来评估是允许还是阻止设备。  

![条件访问流](media/ConditionalAccess8-1.png)  

若要访问电子邮件，设备必须：  

- 注册 Intune  

- Pc 必须已加入域的或在 Intune 中设置的策略中进行注册并符合要求  

- 在 Azure AD 中注册设备。 发生这种情况会自动向 Intune 注册设备时。 对于加入域的电脑，你必须将它设置为[自动注册该设备](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-manual-steps)与 Azure AD。  

- 已激活电子邮件，这会将设备的 Exchange ActiveSync ID 与 Azure Active Directory 中的设备记录相关联（仅适用于 iOS 和 Android 设备）。  

- 符合任何已部署的符合性策略  

根据评估的条件，设备状态存储在可授予或阻止对电子邮件的访问权限的 Azure Active Directory 中。  

如果不满足条件，用户将看到以下消息之一，在登录时：  

- 如果设备未注册，或在 Azure AD 中注册，包含有关如何安装公司门户应用并注册的说明显示一条消息  

- 如果设备不合规，将显示一条消息将用户定向到 Intune 公司门户网站或公司门户应用用户可以在其中找到有关问题的信息及其解决方式。  

- 对于 PC：  

    - 如果策略设置为要求加入域，而电脑未加入域的显示一条消息与 IT 管理员联系。  

    - 如果策略设置为要求加入域或合规，并电脑不满足任一要求，包含有关如何安装公司门户应用并注册的说明显示一条消息。  

消息将在新 Exchange Online Dedicated 环境中 Exchange Online 用户和租户的设备上显示，并且被传送到 Exchange 本地设备和 Exchange Online Dedicated 旧设备的用户电子邮件收件箱。  

> [!NOTE]  
> Configuration Manager 条件访问规则可替代、允许、阻止和隔离在 Exchange Online 管理控制台中定义的规则。  
> 
> 必须在 Intune 控制台中配置条件访问策略。 以下步骤首先通过 Configuration Manager 访问 Intune 控制台。 如果系统提示，请使用用于设置服务连接点，Configuration Manager 和 Intune 之间的相同凭据登录。  

##### <a name="to-enable-the-exchange-online-policy"></a>若要启用 Exchange Online 策略  

1. 在 Configuration Manager 控制台中，选择**资产和符合性**。  

2. 展开**符合性设置**，展开**条件性访问**，然后选择**Exchange Online**。  

3. 上**主页**选项卡上，在**链接**组中，选择**Intune 控制台中配置条件性访问策略**。 可能需要提供用于将 Configuration Manager 与 Intune 服务的任何全局管理员相连接的帐户的用户名和密码。 随即将打开 Intune 管理控制台。  

4. 在 Microsoft Intune 门户中，选择**策略** > **条件性访问** > **Exchange Online 策略**。  

    ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5. 在“Exchange Online 策略”  页面上，选择“启用 Exchange Online 的条件访问策略” 。 如果选中此项，则设备必须合规。 如果未选中此选项不被应用条件性访问。  

    > [!NOTE]  
    > 如果你尚未部署合规性策略，但是启用了 Exchange Online 策略，则所有目标的设备被报告为符合。  
   >   
   >  无论符合性状态如何，策略的所有目标用户都需要向 Intune 注册其设备。  

6. 下**应用程序访问**、 Outlook 和其他使用新式身份验证的应用，你可以选择将访问仅限为对每个平台合规的设备。 Windows 设备必须已加入域或在 Intune 中注册并且符合。  

    > [!TIP]  
    > “新式验证” 允许基于 Active Directory 身份验证库 (ADAL) 登录到 Office 客户端。  
    > 
    > - 基于 ADAL 的身份验证使 Office 客户端能够实现基于浏览器的身份验证（也称为被动身份验证）。 为了进行身份验证，用户将被导向登录网页。  
    > - 这种全新的登录方法实现了新的方案，如基于“设备符合性”  以及“多重身份验证”  执行情况的条件访问。  
    > 
    >  有关详细信息，请参阅[适用于 Office 2013 和 Office 2016 客户端应用的新式验证工作原理](https://docs.microsoft.com/office365/enterprise/modern-auth-for-office-2013-and-2016)。  

    通过将 Exchange Online 与 Configuration Manager 和 Intune 配合使用，不仅可以使用条件访问管理移动设备，而且还可以管理台式计算机。 Pc 必须加入域，或在 Intune 中注册并且合规。 可以设置以下要求：  

    - **设备必须已加入域或必须是合规的。** Pc 必须已加入域或符合策略。 如果电脑不满足任一要求，系统会提示用户注册设备与 Intune。  

    - **设备必须已加入域。** Pc 必须已加入域的访问 Exchange Online。 如果电脑未加入域的阻止访问电子邮件并提示用户与 IT 管理员联系。  

    - **设备必须是合规的。** 电脑必须在 Intune 中注册并且合规。 如果电脑未注册，将显示一条消息包含有关如何注册的说明。  

7. 下**Outlook web access (OWA)**，你可以选择允许访问 Exchange Online 仅通过支持的浏览器：Safari (iOS) 和 Chrome (Android)。 将阻止来自其他浏览器的访问。 你为 Outlook 应用程序访问选择的平台限制在此处同样适用。  

    - 在 **Android** 设备上，用户必须启用浏览器访问。 若要执行此操作，用户必须按如下所示启用已注册的设备上的"启用浏览器访问"选项：  

        1. 启动“公司门户应用”。  

        2. 从三个点 (…) 或硬件菜单按钮转到“设置”页。  

        3. 按“启用浏览器访问”按钮。  

        4. 在 Chrome 浏览器中注销 Office 365 并重新启动 Chrome。  

    - 上**iOS 和 Android**平台，以识别用于访问该服务，Azure AD 的设备将向设备颁发 TLS 证书。 设备显示证书，并提示用户选择的证书，如下面的屏幕截图中所示。 用户必须选择此证书，然后它们可以继续使用浏览器。  

        - **iOS**  

        ![ipad 上证书提示的屏幕截图](media/mdm-browser-ca-ios-cert-prompt_v2.png)  

        - **Outlook Web Access (OWA)**  

        ![Android 设备上证书提示的屏幕截图](media/mdm-browser-ca-android-cert-prompt.png)  

8. 对于**Exchange ActiveSync 邮件应用**，可以选择在设备不合规时阻止电子邮件访问 Exchange Online，并选择在 Intune 无法管理设备时是允许还是阻止访问电子邮件。  

9. 在 **“目标组”** 下，选择策略将应用到的 Active Directory 安全用户组。  

    > [!NOTE]  
    > 目标组中的用户，Intune 策略将替换 Exchange 规则和策略。  
    > 
    > 出现以下情况时，Exchange 将仅强制执行 Exchange 允许、阻止和隔离规则及 Exchange 策略：  
    > 
    > - 用户未获 Intune 授权。  
    > - 用户已获 Intune 授权，但用户不属于条件访问策略针对的任何安全组。  

10. 在 **“免除组”** 下，选择将会从此策略中免除的 Active Directory 安全用户组。 如果用户处于目标和例外组，它们将从策略中免除，并且有权访问其电子邮件。  

11. 完成后，单击“保存” 。  


查看有关此策略的以下说明：  

- 无需部署条件性访问策略;它将立即生效。  

- 用户创建电子邮件帐户后，设备将立即被阻止。  

- 如果被阻止的用户向 Intune 注册设备（或修正不合规性），则将在 2 分钟内解除对电子邮件访问的阻止。  

- 如果用户取消对其设备的注册，电子邮件将会在大约 6 小时后被阻止。  


### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>对于 Exchange 内部部署（和旧 Exchange Online Dedicated 环境中的租户）  
针对 Exchange 内部部署和旧 Exchange Online Dedicated 环境中的租户的条件访问策略使用下面的流来评估是允许还是阻止设备。  

![ConditionalAccess8&#45;2](media/ConditionalAccess8-2.png)  

#### <a name="to-enable-the-exchange-on-premises-policy"></a>若要启用 Exchange 内部部署策略  

1. 在 Configuration Manager 控制台中，选择**资产和符合性**。  

2. 展开**符合性设置**，展开**条件性访问**，然后选择**本地 Exchange**。  

3. 上**主页**选项卡上，在**的本地 Exchange**组中，选择**配置条件性访问策略**。  

4. 上**常规**页**配置条件性访问策略向导**，指定是否要覆盖 Exchange Active Sync 默认规则。 如果要将已注册且合规的设备始终有权访问电子邮件，即使默认规则设置为隔离或阻止访问，请选择此选项。  

    > [!NOTE]  
    > 没有适用于 Android 设备的默认覆盖存在问题。 如果 Exchange 服务器的默认访问规则设置为“阻止”，启用了 Exchange 条件访问策略且设置了默认规则覆盖选项，则即使在目标用户的 Android 设备注册 Intune 且合规后，也可能不会解除阻止该设备。 若要解决此问题，请将 Exchange 默认访问规则设置为“隔离”。 设备不会默认情况下，对 Exchange 的访问和管理员可从隔离的设备列表上的 Exchange 服务器获取报表。  

    如果设置 Exchange 连接器时未以通知电子邮件帐户设置，您会看到一条警告在此页上，并**下一步**按钮处于禁用状态。  必须先在 Exchange Connector 中配置通知电子邮件设置，然后返回“配置条件访问策略向导”完成该过程，才能继续操作。  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

5. 在“目标集合”  页面中，添加一个或多个用户集合。 若要访问 Exchange，则这些集合中的用户必须向 Intune 注册他们的设备，并且这些设备需符合部署的任何符合性策略。  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

6. 在“免除集合”  页面中，添加任何想从条件性访问策略中免除的用户集合。 这些组中的用户，不需要向 Intune 注册其设备并不需要为了访问 Exchange 而符合任何部署的符合性策略。  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

    如果用户同时处于目标列表和免除列表，则会从条件性访问策略中免除。  

7. 在“编辑用户通知”页面上，配置 Intune 向用户发送的说明如何取消阻止他们的设备的电子邮件（包括 Exchange 发送的电子邮件）。  

    你可以编辑默认消息，还可使用 HTML 标记来设置文本的显示格式。 还可以提前向员工发送电子邮件，以便通知他们即将进行的更改，并为他们提供有关注册其设备的说明。  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    > 由于已将包含修正说明的 Intune 通知电子邮件发送到用户的 Exchange 邮箱，因此，如果用户的设备在接收电子邮件消息之前被阻止，则用户可以使用取消阻止的设备或其他方法来访问 Exchange 并查看该消息。  
    > 
    > 为了使 Exchange 发送的通知电子邮件，配置将用于发送通知电子邮件的帐户。 配置 Exchange Server 连接器属性时执行此操作。  
    >   
    > 有关详细信息，请参阅[使用 Configuration Manager 和 Exchange 管理移动设备](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)。  

8. 上**摘要**页上，查看设置，，然后完成向导。  


查看有关此策略的以下说明：  

- 条件访问策略将立即生效，无需进行部署。  

- 用户设置 Exchange ActiveSync 配置文件后，可能需要一到三个小时设备才会被阻止 （如果它不由 Intune 管理）。  

- 如果被阻止的用户然后向 Intune 注册设备 （或修正不合规性），在两分钟内将取消阻止电子邮件访问权限。  

- 如果用户取消-从它可能需要一到三个小时设备才会被阻止的 Intune 注册。  


## <a name="see-also"></a>另请参阅  

[管理对服务的访问](/sccm/protect/deploy-use/manage-access-to-services)
