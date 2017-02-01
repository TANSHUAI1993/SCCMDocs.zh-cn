---
title: "设置混合 MDM | Microsoft Docs"
description: "使用 Configuration Manager 和 Intune 设置混合设备注册。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0a6cb36aad455b38db628f26b97e1b4c00adc741
ms.openlocfilehash: 12ef5c1faf5fe5780ddb7c12cfe6d533e9785f6d

---

# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 设置混合移动设备管理 (MDM)

*适用范围：System Center Configuration Manager (Current Branch)*


必须先向 Intune 注册 iOS、Windows 和 Android 设备，然后才能使用 Configuration Manager 管理它们。 按照以下步骤可使用 Intune，通过 Configuration Manager 设置混合设备注册。 通过完成以下步骤，你会为用户启用“自带设备办公”(BYOD) 注册。 这些步骤也是[注册公司拥有的设备](enroll-company-owned-devices.md)的先决条件。

 |步骤|详细信息|  
 |-----------|-------------|  
 |**步骤 1：**[创建 MDM 集合](#step-1-create-an-mdm-collection)|创建 Configuration Manager 用户集合，其中的用户的设备可以进行注册|  
 |**步骤 2：**[域名要求](#step-2-domain-name-requirements)|确认组织的域名服务 (DNS) 和 Active Directory 用户管理满足 MDM 要求|
 |**步骤 3：**[配置 Intune 订阅](#step-3-configure-intune-subscription)|Intune 服务使你可以通过 Internet 管理设备。|  
 |**步骤 4：**[添加条款和条件](#step-4-add-terms-and-conditions)| 创建用户必须同意才能使用公司门户应用的条款和条件|
 |**步骤 5：**[创建服务连接点](#step-5-create-service-connection-point)|服务连接点将设置和软件部署信息发送到 Configuration Manager，并从移动设备中检索状态和清单消息。 |  
 |**步骤 6：**[启用平台注册](#step-6-enable-platform-enrollment)|针对 [iOS](#ios-and-mac-enrollment-setup) 和 [Windows](#windows-enrollment-setup) 设备的 MDM 注册需要执行附加步骤，以便在服务与设备之间进行通信。 Android 不需要附加配置。|  
 |**步骤 7：**[设置附加管理](#step-7-set-up-additional-management)|（可选）为已注册的设备设置配置项目和条件访问|
 |**步骤 8：**[验证 MDM 配置](#step-8-verify-mdm-configuration)|查看日志文件，以确认服务连接点已成功创建并且用户帐户在进行同步。|
 |**步骤 9：**[注册设备](#step-9-enroll-devices)|告知用户如何注册其设备，或开始注册公司拥有的设备以满足组织需求|

需要 Intune 而不使用 Configuration Manager？
> [!div class="button"]
[查看 Intune 文档 >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)

## <a name="step-1-create-an-mdm-collection"></a>步骤 1：创建 MDM 集合
需要 Configuration Manager 用户集合以指定可以向管理中注册设备的用户。 由于 Intune 许可证由用户进行分配，所以只能使用用户集合（而非设备集合）。

> [!NOTE]
> 若要向 Intune 注册设备，无需在 Office 365 门户或 Azure Active Directory 门户中向用户分配许可证。 只需在与 Intune 订阅（在一个[后续步骤](#step-3-configure-intune-subscription)中）关联的集合中包括用户即可。

为进行测试，可以设置**直接规则**并添加可以注册设备的特定用户。 在 Configuration Manager 控制台中，选择“资产和符合性” > “用户集合”，单击“主页”选项卡 >“创建”组，然后单击“创建用户集合”。 若要实现更广泛的分发，应使用**查询规则**定义用户。 有关集合的详细信息，请参阅[如何创建集合](https://technet.microsoft.com/library/mt629371.aspx)。

![为 MDM 创建用户集合](../media/mdm-create-user-collection.png)

## <a name="step-2-domain-name-requirements"></a>步骤 2：域名要求

如有必要，请执行以下步骤以满足 Configuration Manager 外部的任何依赖关系：

1. 每个用户必须分配有 Intune 许可证才能注册设备。 若要将 Intune 许可证关联到用户，每个用户必须具有可公开解析的用户主体名称 (UPN)（例如，johndoe@contoso.com)）或是在 Azure Active Directory 中配置的备用登录 ID。 配置备用登录 ID 使用户可以使用电子邮件地址登录，即使其 UPN 是 NetBIOS 格式（例如 CONTOSO\johndoe）。

  - 如果公司使用公开解析的 UPN（例如 johndoe@contoso.com),），则无需进一步配置。
  - 如果公司使用不可解析的 UPN（例如 CONTOSO\johndoe），则你必须[在 Azure Active Directory 中配置备用 ID](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync)。

2.  部署并配置 Active Directory 联合身份验证服务 (AD FS)。 （可选）

     在设置单一登录时，用户可以使用其公司凭据登录，以访问 Intune 中的服务。

     有关详细信息，请参阅下列主题：
    -   [为单一登录做准备](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [规划和部署 AD FS 2.0 以用于单一登录](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  部署并配置目录同步。

     目录同步可让你利用同步的用户帐户来填充 Intune。 同步的用户帐户和安全组被添加到 Intune 中。 未能启用目录同步是在使用 Microsoft Intune 设置 Configuration Manager MDM 时，设备无法注册的一个常见原因。

     有关详细信息，请参阅 Active Directory 文档库中的 [目录集成](http://go.microsoft.com/fwlink/?LinkID=271120) 。

4.  可选但不建议：如果没有使用 Active Directory 联合身份验证服务，则重置用户的 Microsoft Online 密码。

     如果没有使用 AD FS，则必须为每个用户设置 Microsoft Online 密码。

## <a name="step-3-configure-intune-subscription"></a>步骤 3：配置 Intune 订阅
 Intune 订阅使你可以通过 Internet 管理设备。 这包括指定可以注册设备的用户集合以及定义向用户显示的信息。 Intune 订阅执行以下任务：

-   检索服务连接点连接到 Intune 服务所需的证书
-   定义使用户能够注册移动设备的用户集合。
-   定义和配置要支持的移动平台。

> [!IMPORTANT]
>  在 Configuration Manager 中为Microsoft Intune 创建订阅会将你站点的服务连接点置于“联机模式”下。 请参阅[关于 System Center Configuration Manager 中的服务连接点](../../core/servers/deploy/configure/about-the-service-connection-point.md)。

### <a name="to-create-the-microsoft-intune-subscription"></a>创建 Microsoft Intune 订阅

1.  如果尚未注册，请在 [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216) 处注册 Microsoft Intune 帐户。  创建 Intune 帐户之后，无需将任何用户添加到 Intune 帐户或执行其他设置配置。

2.  在 Configuration Manager 控制台中，单击“管理” 。

3.  在“管理”  工作区中，展开“云服务” ，并单击“Microsoft Intune 订阅” 。 在“主页”  选项卡上，单击“添加 Microsoft Intune 订阅” 。

![创建 Intune 订阅](../media/mdm-set-intune.png)

4.  在“创建 Microsoft Intune 订阅向导”的“介绍”  页上，查看文本并单击“下一步” 。

5.  在“订阅”  页上，单击“登录”  并使用你的工作或学校帐户登录。 在“设置移动设备管理机构” 对话框中，选中相应复选框，以便只能通过 Configuration Manager 控制台使用 Configuration Manager 来管理移动设备。 要继续进行订阅，你必须选择此选项。

    > [!IMPORTANT]
    >  选择 Configuration Manager 作为管理机构后，将来你无法将管理机构更改为 Microsoft Intune。

6.  单击隐私链接以查看它们，然后单击“下一步” 。

7.  在“常规”  页上，指定以下选项，然后单击“下一步” 。

  -   **集合**：指定一个用户集合，其中包含将注册其移动设备的用户。

      > [!NOTE]
      >  如果从集合中删除某个用户，则将继续管理该用户的设备最多 24 小时，直至从用户数据库中删除用户记录为止。

  -   **公司名称**：指定你的公司名称。

  -   “指向公司隐私文档的 URL”：如果将公司隐私信息发布到可从 Internet 中访问的链接，请提供该链接以便用户可从公司门户中访问它，例如 http://www.contoso.com/CP_privacy.html。 隐私信息可阐明用户与你的公司分享了什么信息。

  -   **公司门户的配色方案**：（可选）更改公司门户的默认颜色（蓝色）。

  -   **Configuration Manager 站点代码**：指定主站点的站点代码以管理移动设备。

    > [!NOTE]
    >  更改站点代码仅影响新注册，不影响现有注册设备。

8.  在“公司联系人信息”页上，指定在公司门户应用中的“联系 IT”下向用户显示的公司联系人信息。 提供公司的联系人信息，然后单击“下一步”。

9. 在“公司徽标”页上，可以选择是否要在公司门户中显示徽标，然后单击“下一步”。

10. 完成向导。

## <a name="step-4-add-terms-and-conditions"></a>步骤 4：添加条款和条件
 移动设备的 Intune 管理配置完成后，就可以创建“条款和条件” 。 使用条款和条件向用户说明他们注册设备时会发生的情况。 在注册设备之前，用户必须接受相应的条款和条件。 在 Configuration Manager 控制台中，转到“资产和符合性” > “概述” > “符合性设置” > “条款和条件”，然后单击“创建条款和条件”。 请参阅 [System Center Configuration Manager 中的条款和条件](terms-and-conditions.md)。

##  <a name="step-5-create-service-connection-point"></a>步骤 5：创建服务连接点
创建了订阅后，你可以随后安装服务连接点站点系统角色，该角色使你能够连接到 Intune 服务。 此站点系统角色会将设置和应用程序推送到 Intune 服务。

 服务连接点将设置和软件部署信息发送到 Configuration Manager，并从移动设备中检索状态和清单消息。 Configuration Manager 服务充当与移动设备通信的网关并存储设置。

> [!NOTE]
>  服务连接点系统角色只能安装在管理中心站点或独立主站点上。 服务连接点必须具有 Internet 访问权限。


### <a name="configure-the-service-connection-point-role"></a>配置服务连接点角色

1.  在 Configuration Manager 控制台中，单击“管理” 。

2.  在“管理”工作区中，展开“站点”，然后单击“服务器和站点系统角色”。

3.  使用关联的步骤将“服务连接点”  角色添加到新的或现有的站点系统服务器：

    -   新站点系统服务器：在“主页”  选项卡上的“创建”  组中，单击“创建站点系统服务器”  以启动创建站点系统服务器向导。

    -   现有站点系统服务器：单击你要在其上安装服务连接点角色的服务器。 然后，在“主页”  选项卡上的“服务器”  组中，单击“添加站点系统角色”  以启动添加站点系统角色向导。

4.  在“系统角色选择”  页面上，选择“服务连接点” ，然后单击“下一步” 。

![创建服务连接点](../media/mdm-service-connection-point.png)

5.  完成向导。

### <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>服务连接点如何通过 Microsoft Intune 服务进行身份验证？
 服务连接点通过与基于云的 Intune 服务建立连接扩展了 Configuration Manager，从而可通过 Internet 管理移动设备。 服务连接点按照以下方式通过 Intune 服务进行身份验证：

1.  在 Configuration Manager 控制台中创建 Intune 订阅时，通过连接到 Azure Active Directory 对 Configuration Manager 管理员进行身份验证，Azure Active Directory 将重定向到相应的 ADFS 服务器，提示输入用户名和密码。 然后，Intune 向租户颁发证书。

2.  步骤 1 中的证书安装在服务连接点站点角色上，用于对与 Microsoft Intune 服务的所有进一步通信进行身份验证和授权。

## <a name="step-6-enable-platform-enrollment"></a>步骤 6：启用平台注册
  不同设备平台需要附加配置以启用设备注册：
  - [iOS 和 Mac 注册设置](#ios-and-mac-enrollment-setup)：获取 Apple MDM 推送证书
  - [Windows 注册设置](#windows-enrollment-setup)：配置 DNS 并为 Windows 电脑、Windows 10 移动版和 Windows Phone 设备启用注册
  - Android：Android 设备无需附加步骤即可启用注册

启用 MDM 管理后，便可以指定每个用户可注册的设备数量，每个用户最多可注册 15 个设备。

### <a name="ios-and-mac-enrollment-setup"></a>iOS 和 Mac 注册设置
  以下步骤通过将 Apple MDM 推送证书上传到 Intune 服务来启用 Apple 设备的管理。

  1.  **下载证书签名请求** – 证书签名请求文件 (.csr) 要求请求 Apple 的 APNs 证书。  

      1.  在 Configuration Manager 控制台中的“管理”工作区中，转到“云服务”> “Microsoft Intune 订阅”。  

      2.  在“主页”  选项卡上，单击“创建 APNs 证书请求” 。 “请求 Apple Push Notification 服务证书签名请求”  对话框随即打开。  

      3.  “浏览” 到要保存新的证书签名请求 (.csr) 文件的路径。 本地保存证书签名请求 (.csr) 文件。  

      4.  单击“下载” 。 下载新 Microsoft Intune .csr 文件，并由 Configuration Manager 保存。 .Csr 文件用于从 Apple 推送证书门户请求信任关系证书。  

  2.  **请求 Apple 的 APNs 证书** – Apple Push Notification 服务 (APNs) 证书用于在管理服务、Intune 和注册的 iOS 移动设备之间建立信任关系。  

      1.  在浏览器中，转到 [Apple Push Certificates 门户](http://go.microsoft.com/fwlink/?LinkId=269844) 并使用贵公司 Apple ID 登录。 若要续订 APN 证书，必须在将来使用此 Apple ID。  

      2.  使用证书签名请求 (.csr) 文件完成向导。 下载 APNs 证书并在本地保存 .pem 文件。 此 APNs 证书 (.pem) 文件用于在 Apple 推送通知服务器和 Intune 的移动设备管理机构之间建立信任关系。  

  3.  **启用注册并上载 APNs 证书** – 若要启用 iOS 注册，请上载 APNs 证书。  

      1.  在“管理”工作区中的 Configuration Manager 控制台中，转到“云服务” > “Microsoft Intune 订阅”。  

      2.  在“主页”选项卡上的“订阅”组中，单击“配置平台” > “iOS”。  

          > [!NOTE]  
          >  在 Configuration Manager 控制台中启用 iOS 注册之前，请不要上载 Apple Push Notification 服务 (APN) 证书。  

      3.  在“Microsoft Intune 订阅属性”  对话框中，选择“iOS”  选项卡并单击选择“启用 iOS 注册”  复选框。  

      4.  单击“浏览” 并转到“从 Apple 下载的 APNs 证书(.cer)文件”。 Configuration Manager 会显示 APNs 证书信息。 单击“确定”  ，将 APNs 证书保存到 Intune。    


有关 [iOS 和 Mac 注册](enroll-hybrid-ios-mac.md)的其他信息。

### <a name="windows-enrollment-setup"></a>Windows 注册设置  
可以结合 Intune 使用 Configuration Manager 来管理台式机、笔记本电脑和其他将 Windows 作为移动设备运行的设备。 还可以通过在设备上添加公司或学校帐户，将 Windows 10 设备配置为[在加入 Azure Active Directory 时自动注册](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/enroll-hybrid-windows#azure-active-directory-enrollment)。

通过在设备注册期间自动填充服务器名称，DNS 别名（CNAME 记录类型）可让用户更轻松地注册其设备。 随后可以为 Windows 电脑移动设备启用注册。  

1. 在 Configuration Manager 控制台中的“管理”工作区中，转到“云服务” > “Microsoft Intune 订阅”，然后执行以下操作：  
  - **Windows 电脑：**在“主页”选项卡上，单击“配置平台”，然后单击“Windows”。 在“常规”  选项卡上，选择“启用 Windows 注册” 。  
  - **Windows 10 移动版和 Windows Phone：**在“主页”选项卡上，单击“配置平台”，然后单击“Windows Phone”。  在“常规”选项卡上，选择“Windows Phone 8.1 和 Windows 10 移动版”。

2.  还可配置 Configuration Manager 来简化使用公司门户应用进行注册的过程。
（可选）在公司的 DNS 记录中创建 DNS 别名（CNAME 记录类型），它将发送给公司域名中的 URL 的请求重定向到 Microsoft 的云服务服务器。  例如，贵公司的域为 contoso.com，则应在 DNS 中创建将 EnterpriseEnrollment.contoso.com 重定向到 EnterpriseEnrollment-s.manage.microsoft.com 的 CNAME。  

|类型|主机名|指向|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  

有关其他信息，请参阅 [Windows 注册](enroll-hybrid-windows.md)。

### <a name="android-enrollment-setup"></a>Android 注册设置
可以将 Configuration Manager 与 Intune 结合使用来管理运行 Android 的手机和平板电脑。
1.  在“管理”工作区中的 Configuration Manager 控制台中，转到“云服务” > “Microsoft Intune 订阅”。  

2.  在“主页”选项卡上的“订阅”组中，单击“配置平台” > “Android”。  

3.  在“Microsoft Intune 订阅属性”  对话框中，选择“Android”  选项卡并单击选择“启用 Android 注册”  复选框。

有关其他信息，请参阅 [Android](enroll-hybrid-android.md)。

## <a name="step-7-set-up-additional-management"></a>步骤 7：设置附加管理
（可选）注册设备之前，可以设置附加管理。 可以注册设备之后创建并部署这些管理解决方案，不过许多组织更希望在将设备纳入管理时部署它们。

通过**配置项目**可以基于设备平台在注册的设备上管理设置（如要求 PIN 或要求加密）：
- [Windows 10 和 Windows 8.1 设备](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)
- [Windows Phone 设备](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client)
- [iOS 和 Mac 设备](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)
- [Android 和 Samsung KNOX Standard 设备](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)

**应用程序**可以部署到托管设备：
- [iOS 应用程序](/sccm/apps/get-started/creating-ios-applications)
- [Mac 应用程序](/sccm/apps/get-started/creating-mac-computer-applications)
- [Windows 电脑应用程序](/sccm/apps/get-started/creating-windows-applications)
- [Windows Phone 应用程序](/sccm/apps/get-started/creating-windows-phone-applications)
- [Android 应用程序](/sccm/apps/get-started/creating-android-applications)

通过**条件访问**可以管理对公司资源的访问，包括：  
- [电子邮件访问](/sccm/protect/deploy-use/manage-email-access)
- [SharePoint 访问](/sccm/protect/deploy-use/manage-sharepoint-online-access)
- [Skype for Business 访问](/sccm/protect/deploy-use/manage-skype-for-business-online-access)
- [Dynamic CRM Online](/sccm/protect/deploy-use/manage-dynamics-crm-online-access)

## <a name="step-8-verify-mdm-configuration"></a>步骤 8：验证 MDM 配置

 可以通过检查以下日志文件来验证某些设备管理组件：

-   检查 Cloudusersync.log 以验证用户帐户是否已成功同步。

-   检查 Sitecomp.log 以验证是否已成功创建服务连接点。

## <a name="step-9-enroll-devices"></a>步骤 9：注册设备
混合设置现已完成。 可以在 Configuration Manager 中通过多种方式注册设备：
- 用户拥有的 (BYOD) 设备：[告知用户如何注册其设备](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) - 注册指南对于 Intune 和混合托管设备是相同的
- 公司拥有的 (COD) 设备：[注册公司拥有的设备](enroll-company-owned-devices.md)提供有关用于注册公司拥有的设备的不同平台特定方法的指导。

## <a name="managing-intune-subscriptions-associated-with-configuration-manager"></a>管理与 Configuration Manager 关联的 Intune 订阅

如果将 Microsoft Intune（试用订阅或付费订阅）添加到 Configuration Manager，随后需要切换到不同的 Intune 订阅，则必须先从 Configuration Manager 控制台中同时删除 **Microsoft Intune 订阅**和**服务连接点**，然后才能添加新订阅。

### <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>如何从 Configuration Manager 中删除 Intune 订阅

> [!IMPORTANT]
>  删除订阅将删除所有内容，包括用户注册、策略和为由 Intune 订阅管理的设备所配置的应用部署。

1.  在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “Microsoft Intune 订阅”。

2.  右键单击列出的“Microsoft Intune 订阅”，然后单击“删除”。

3.   在向导中，依次单击“从 Configuration Manager 中删除 Microsoft Intune 订阅”、“下一步”，然后再次单击“下一步”以删除订阅。


### <a name="how-to-remove-the-service-connection-point-role"></a>如何删除服务连接点角色

1.  转到“管理” > “概述” > “站点配置” > “服务器和站点系统角色”。

2.  选择承载“服务连接点”角色的服务器。

3.  在“站点系统角色”列表中，选择“服务连接点”，然后在功能区中单击“删除角色”。 确认要删除角色。 服务连接点会删除。

现在可以创建新服务连接点、将新 Intune 订阅添加到 Configuration Manager 以及将 Configuration Manager 设置为 MDM 机构。

### <a name="how-to-change-mdm-authority-to-intune"></a>如何将 MDM 机构更改为 Intune

从 1610 版开始，可以将 Intune MDM 机构从 Configuration Manager 切换为 Intune。 即将发布此功能的相关信息。



<!--HONumber=Dec16_HO3-->


