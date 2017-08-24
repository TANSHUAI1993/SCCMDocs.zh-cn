---
title: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 Windows 混合设备管理 | Microsoft Docs"
description: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 Windows 设备管理。"
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 47348baeac26bfa2ad5016622fe4dbcb9f572483
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>设置 Windows 混合使用 System Center Configuration Manager 和 Microsoft Intune 的设备管理

*适用范围：System Center Configuration Manager (Current Branch)*

本主题介绍 IT 管理员如何能通过 Configuration Manager 和 Microsoft Intune 使用户可以管理 Windows 电脑和移动设备。

## <a name="enable-windows-device-management"></a>启用 Windows 设备管理
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

## <a name="choose-how-to-enroll-windows-devices"></a>选择注册 Windows 设备的方式

向用户分配 Intune 许可证后，无需其他步骤即可注册 Windows 设备，但是可以使用户的注册过程更为简单。

两个因素决定了简化 Windows 设备注册的方式：
- **是否使用 Azure Active Directory Premium？** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) 随附企业移动性 + 安全性和其他许可计划。
- **将注册什么版本的 Windows？** <br>可通过添加工作或学校帐户自动注册 Windows 10 设备。 早期版本必须使用公司门户应用进行注册。

||**Azure AD Premium**|**其他 AD**|
|----------|---------------|---------------|  
|**Windows 10**|[自动注册](#enable-windows-10-automatic-enrollment) |[用户注册](#enable-windows-enrollment-without-azure-ad-premium)|
|**早期 Windows 版本**|[用户注册](#enable-windows-enrollment-without-azure-ad-premium)|[用户注册](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>启用 Windows 10 自动注册

通过添加工作或学校帐户并同意接受管理，自动注册可让用户在 Intune 中注册公司拥有的电脑或个人 Windows 10 电脑和 Windows 10 移动设备。 就是这么简单。 在后台注册用户设备并加入 Azure Active Directory。 注册后，通过 Intune 管理设备。

**先决条件**
- Azure Active Directory Premium 订阅（[试用订阅](http://go.microsoft.com/fwlink/?LinkID=816845)）
- Microsoft Intune 订阅


### <a name="configure-automatic-mdm-enrollment"></a>配置自动进行 MDM 注册

1. 登录到 [Azure 管理门户](https://portal.azure.com) (https://manage.windowsazure.com) 中，然后选择“Azure Active Directory”。

  ![Azure 门户的屏幕截图](../media/auto-enroll-azure-main.png)

2. 选择“移动性 (MDM 和 MAM)”。

  ![Azure 门户的屏幕截图](../media/auto-enroll-mdm.png)

3. 选择“Microsoft Intune”。

  ![Azure 门户的屏幕截图](../media/auto-enroll-intune.png)

4. 配置“MDM 用户范围”。 指定应由 Microsoft Intune 管理的用户设备。 这些用户的 Windows 10 设备将自动注册，以使用 Microsoft Intune 进行管理。

    - **无**
    - **部分**
    - **所有**

   ![Azure 门户的屏幕截图](../media/auto-enroll-scope.png)

5. 对下列 URL 使用默认值：
    - **MDM 使用条款 URL**
    - **MDM 发现 URL**
    - **MDM 符合性 URL**

6. 选择“保存”。


默认情况下，不会为该服务启用双重身份验证。 但是，在注册设备时，建议启用双重身份验证。 在为该服务请求双重身份验证之前，必须在 Azure Active Directory 中配置一个双重身份验证提供程序并为你的用户帐户配置多重身份验证。 请参阅[Azure 多重身份验证服务器入门](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud)。

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>在不使用 Azure AD Premium 的情况下启用 Windows 注册
可以让用户在不使用 Azure AD Premium 自动注册的情况下注册其设备。 分配许可证后，用户可以在将其工作帐户添加到其个人拥有的设备或将其公司拥有的设备加入你的 Azure AD 后进行注册。 创建 DNS 别名（CNAME 记录类型）可以简化用户注册其设备的过程。 如果创建 DNS CNAME 资源记录，用户即可连接 Intune 并在其中进行注册，而无需输入 Intune 服务器名称。

### <a name="create-cnames-to-simplify-enrollment"></a>创建 CNAME 以简化注册
为公司的域创建 CNAME DNS 资源记录。 例如，如果你的公司网站为 contoso.com，则你将在 DNS 中创建将 EnterpriseEnrollment.contoso.com 重定向到 enterpriseenrollment-s.manage.microsoft.com 的 CNAME。

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

`EnterpriseEnrollment-s.manage.microsoft.com` – 支持从电子邮件的域名重定向到具有域识别的 Intune 服务

对 DNS 记录所做的更改可能最多需要 72 小时才能进行传播。 你无法在 Intune 中验证 DNS 更改，直到 DNS 记录开始进行传播。

## <a name="tell-users-how-to-enroll-devices"></a>告知用户如何注册设备  

 设置完成后，需要让用户知道如何注册其设备。 有关指南，请参阅[需要使用户了解的有关设备注册的内容](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 可以将用户定向到[在 Intune 中注册 Windows 设备](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows)。 此信息适用于 Microsoft Intune 和 Configuration Manager 托管的移动设备。

> [!div class="button"]
[< 上一步](create-service-connection-point.md)  [下一步 >](set-up-additional-management.md)
