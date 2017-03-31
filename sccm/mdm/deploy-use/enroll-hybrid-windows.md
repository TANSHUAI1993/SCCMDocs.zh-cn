---
title: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 Windows 混合设备管理 | Microsoft Docs"
description: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 Windows 设备管理。"
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 4189fe34efc2ae134150a89791dc10bbab1b9d02
ms.lasthandoff: 03/17/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>设置 Windows 混合使用 System Center Configuration Manager 和 Microsoft Intune 的设备管理

*适用范围：System Center Configuration Manager (Current Branch)*

本主题介绍 IT 管理员如何能通过 Configuration Manager 和 Microsoft Intune 使用户可以管理 Windows 电脑和移动设备。 有两种可用的注册方法：
-  用户将其帐户与设备连接时自动注册 Azure Active Directory (AD)
- 通过安装和登录公司门户应用进行注册

## <a name="choose-how-to-enroll-windows-devices"></a>选择注册 Windows 设备的方式

两个因素决定注册 Windows 设备的方式：
- **是否使用 Azure Active Directory Premium？** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) 随附企业移动性 + 安全性和其他许可计划。
- **将注册什么版本的 Windows？** <br>可通过添加工作或学校帐户自动注册 Windows 10 设备。 早期版本必须使用公司门户应用进行注册。

||**Azure AD Premium**|**其他 AD**|
|----------|---------------|---------------|  
|**Windows 10**|[自动注册](#automatic-enrollment) |[公司门户注册](#company-portal-enrollment)|
|**早期 Windows 版本**|[公司门户注册](#company-portal-enrollment)|[公司门户注册](#company-portal-enrollment)|

## <a name="automatic-enrollment"></a>自动注册

通过添加工作或学校帐户并同意接受管理，自动注册可让用户注册公司拥有的或个人的 Windows 10 设备。 在后台，用户设备将注册并与 Azure Active Directory 连接。 注册后，可以通过 Intune 管理设备。 托管设备仍可使用公司门户来执行任务，但无需安装它以使设备成为已注册状态。

**先决条件**
- Azure Active Directory Premium 订阅（[试用订阅](http://go.microsoft.com/fwlink/?LinkID=816845)）
- Microsoft Intune 订阅

### <a name="configure-automatic-enrollment"></a>配置自动注册

1. 登录 [Azure 门户](https://manage.windowsazure.com)，导航到左窗格中的“Active Directory”节点，然后选择目录。
2. 选择“配置”选项卡并滚动到名为“设备”的部分。
3. 为“用户可以加入工作区的设备”选择“全部”。
4. 选择你想要按每个用户授权的设备的最大数目。

默认情况下，不会为该服务启用双重身份验证。 但是，在注册设备时，建议启用双重身份验证。 在为该服务请求双重身份验证之前，必须在 Azure Active Directory 中配置一个双重身份验证提供程序并为你的用户帐户配置多重身份验证。 请参阅[Azure 多重身份验证服务器入门](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud)。

## <a name="company-portal-enrollment"></a>公司门户注册
最终用户或[设备注册管理器](enroll-devices-with-device-enrollment-manager.md)可通过安装公司门户，然后使用工作凭据登录以注册 Windows 设备。 为了简化最终用户的注册，你应该当向 DNS 注册添加 CNAME。

### <a name="enable-windows-device-management"></a>启用 Windows 设备管理
若要针对电脑或移动设备启用 Windows 设备管理，请按照以下步骤进行操作：

1.  在为任何平台设置注册前，必须先完成[设置混合 MDM](setup-hybrid-mdm.md) 中的先决条件和过程。  
2.  在 Configuration Manager 控制台中的“管理”工作区中，转到“概述” > “云服务” > “Microsoft Intune 订阅”。  
3.  在功能区中，单击“配置平台”，然后选择 Windows 平台：
    - 对于 Windows 电脑和笔记本电脑，请选择“Windows”，然后执行以下步骤：
      1. 在“常规”选项卡上，单击“启用 Windows 注册”复选框。
      2. 如果使用证书进行代码签名并部署公司门户应用，请浏览到“代码签名证书”。 设备用户还可以从 Windows 应用商店安装公司门户应用，或者你可以在没有代码签名的情况下部署来自适用于企业的 Windows 应用商店中的应用。
      3. 你还可以配置 [Windows Hello 企业版设置](windows-hello-for-business-settings.md)。
    - 对于 Windows 手机和平板电脑，请选择“Windows Phone”，然后执行以下步骤：
      1. 在“常规”选项卡上，单击“Windows Phone 8.1 和 Windows 10 移动版”复选框。 不再支持 Windows Phone 8.0。
      2. 如果你的组织需要旁加载公司应用，你可以上传所需的令牌或文件。 有关旁加载应用的详细信息，请参阅[创建 Windows 应用](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications)。
        - **应用程序注册令牌**
        - **.pfx 文件**
        - **无**：如果使用 Symantec 证书，则可以指定“在 Symantec 证书到期前显示警报”。
4. 单击“确定”  关闭对话框。  若要使用公司门户简化注册过程，你应该为创建 DNS 别名以进行设备注册。 然后可以告知用户如何注册其设备。

### <a name="create-dns-alias-for-device-enrollment"></a>创建 DNS 别名以进行设备注册  
DNS 别名（CNAME 记录类型）使用户能更轻松地通过连接到服务注册其设备，而无需用户输入服务器地址。 若要创建 DNS 别名（CNAME 记录类型），必须在公司的 DNS 记录中配置 CNAME，将发送给公司域名中的 URL 的请求重定向到 Microsoft 的云服务服务器。  例如，贵公司的域为 contoso.com，则应在 DNS 中创建将 EnterpriseEnrollment.contoso.com 重定向到 EnterpriseEnrollment-s.manage.microsoft.com 的 CNAME。  

 虽然可选择性创建 CNAME DNS 条目，但 CNAME 记录可简化用户的注册。 如果找不到注册 CNAME 记录，系统会提示用户手动输入 MDM 服务器名称 enrollment.manage.microsoft.com。

|类型|主机名|指向|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 小时|

如果具有多个 UPN 后缀，你需要为每个域名创建一个 CNAME，并将每个 CNAME 指向 EnterpriseEnrollment-s.manage.microsoft.com。 例如，如果 Contoso 的用户使用 name@contoso.com，但也使用 name@us.contoso.com 和 name@eu.constoso.com 作为其电子邮件/UPN，则 Contoso DNS 管理员需要创建以下 CNAME。

|类型|主机名|指向|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 小时|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 小时|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 小时|

## <a name="tell-users-how-to-enroll-devices"></a>告知用户如何注册设备  

 设置完成后，需要让用户知道如何注册其设备。 有关指南，请参阅[需要使用户了解的有关设备注册的内容](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 可以将用户定向到[在 Intune 中注册 Windows 设备](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows)。 此信息适用于 Microsoft Intune 和 Configuration Manager 托管的移动设备。

> [!div class="button"]
[< 上一步](create-service-connection-point.md)  [下一步 >](set-up-additional-management.md)

