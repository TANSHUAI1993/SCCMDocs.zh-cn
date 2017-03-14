---
title: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 Windows 混合设备管理 | Microsoft Docs"
description: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 Windows 设备管理。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: a4fc4a16c78b0eaa0dcefdd596b049eacf1d255b
ms.lasthandoff: 03/06/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>设置 Windows 混合使用 System Center Configuration Manager 和 Microsoft Intune 的设备管理

*适用范围：System Center Configuration Manager (Current Branch)*

可以结合 Intune 使用 Configuration Manager 来管理台式机、笔记本电脑和其他将 Windows 作为移动设备运行的设备。 可设置 Azure Active Directory，使其允许自动注册 Windows 电脑。 还可配置 Configuration Manager 来简化使用公司门户应用进行注册的过程。


Windows 注册选项包括：

- [使用 Azure AD 进行自动注册](#azure-active-directory-enrollment)
- [Windows 电脑](#configure-windows-pc-enrollment)
- [Windows 10 移动版和 Windows Phone 设备](#enable-windows-phone-devices)

## <a name="azure-active-directory-enrollment"></a>Azure Active Directory 注册

通过添加工作或学校帐户并同意接受管理，自动注册可让用户在 Intune 中注册公司拥有的电脑或个人 Windows 10 电脑和 Windows 10 移动设备。 在后台注册用户设备并加入 Azure Active Directory。 注册后，可以通过 Intune 管理设备。

**先决条件**
- Azure Active Directory Premium 订阅（[试用订阅](http://go.microsoft.com/fwlink/?LinkID=816845)）
- Microsoft Intune 订阅


### <a name="configure-automatic-mdm-enrollment"></a>配置自动进行 MDM 注册

1. 在 [Azure 管理门户](https://manage.windowsazure.com) (https://manage.windowsazure.com) 中，导航到 **Active Directory** 节点并选择所需目录。

2. 单击“应用程序” 选项卡，会在应用程序列表看到“Microsoft Intune”。

    ![Azure AD 应用和 Microsoft Intune](../media/aad-intune-app.png)

3. 单击“Microsoft Intune”的箭头将出现一个页面，可在其中配置 Microsoft Intune。

4. 单击“配置”即可开始使用 Microsoft Intune 配置自动进行 MDM 注册。

5. 指定 Intune 的 URL：

  - **MDM 注册 URL** – 使用默认值。
  - **MDM 使用条款 URL** – 使用默认值。 注册设备时，此 URL 将显示用户的使用条款。
  - **MDM 合规性 URL** – 使用默认值。 如果发现设备不合规，此 URL 中将显示一条“访问被拒”的消息。 该 URL 指向一个页面，用户可从此页面了解其设备不合规的原因以及使其设备符合合规性策略的方法。

6.  指定应由 Microsoft Intune 管理的用户设备。 这些用户的 Windows 10 设备将自动注册，以使用 Microsoft Intune 进行管理。

  - **所有**
  - **组**
  - **无**

7. 选择“保存”。

## <a name="configure-windows-pc-enrollment"></a>配置 Windows 电脑注册
 若要启用 Windows 移动设备管理，需要启用操作系统的管理。  还可以添加 DNS CNAME，以简化用户注册。

### <a name="create-dns-alias-for-device-enrollment"></a>创建 DNS 别名以进行设备注册  
 通过在设备注册期间自动填充服务器名称，DNS 别名（CNAME 记录类型）可让用户更轻松地注册其设备。 若要创建 DNS 别名（CNAME 记录类型），必须在公司的 DNS 记录中配置 CNAME，将发送给公司域名中的 URL 的请求重定向到 Microsoft 的云服务服务器。  例如，贵公司的域为 contoso.com，则应在 DNS 中创建将 EnterpriseEnrollment.contoso.com 重定向到 EnterpriseEnrollment-s.manage.microsoft.com 的 CNAME。  

 虽然可选择性创建 CNAME DNS 条目，但 CNAME 记录可简化用户的注册。 如果找不到注册 CNAME 记录，系统会提示用户手动输入 MDM 服务器名称 enrollment.manage.microsoft.com。

|类型|主机名|指向|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  
### <a name="to-enable-enrollment-for-windows-devices"></a>若要启用 Windows 设备的注册  

1.  **先决条件** - 在为任何平台安装注册前，必须先完成[安装混合 MDM](setup-hybrid-mdm.md) 中的先决条件和过程。  

2.  在 Configuration Manager 控制台中的“管理”工作区中，转到“云服务” > “Microsoft Intune 订阅”。  

    > [!WARNING]  
    >  如果其他 Configuration Manager 对话框处于打开状态，请在继续执行此过程之前将其关闭。  

3.  在“主页”  选项卡上，单击“配置平台” ，然后单击“Windows” 。  

4.  在“常规”  选项卡上，选择“启用 Windows 注册” 。  

 设置完成后，需要让用户知道如何注册其设备。 请参阅[用户需要了解的有关设备注册的内容](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 此信息适用于 Microsoft Intune 和 Configuration Manager 托管的移动设备。

## <a name="enable-windows-phone-devices"></a>启用 Windows Phone 管理设备  
  如果你的用户将只注册 Windows Phone 8.1 和更高版本的设备，且你将不会把业务线应用部署到 Windows Phone 设备，则无需 Symantec 证书。 在启用 Windows Phone 注册之后，应指导用户从 Windows Phone 应用商店安装公司门户应用以注册其设备。  

  为将进行管理的 Windows Phone 设备完成以下步骤。  

### <a name="to-enable-enrollment-for-windows-phone-81-and-later-devices"></a>若要启用 Windows Phone 8.1 以及更高版本设备的注册  

 1.  **先决条件** - 在为任何平台安装注册前，必须先完成[安装混合 MDM](setup-hybrid-mdm.md) 中的先决条件和过程。  

 2.  在 Configuration Manager 控制台中的“管理”工作区中，转到“云服务” > “Microsoft Intune 订阅”。  

     > [!WARNING]  
     >  如果其他 Configuration Manager 对话框处于打开状态，请在继续执行此过程之前将其关闭。  

 3.  在“主页”  选项卡上，单击“配置平台” ，然后单击“Windows Phone” 。  

 4.  在“常规”选项卡上，选择“Windows Phone 8.1 和 Windows 10 移动版”。 你可以上传 AET .xml 文件数据或 .pfx 文件以支持公司门户的部署，也可以指导用户从 Windows Phone 应用商店中下载公司门户。  

      单击" **确定**"。  

  设置完成后，需要让用户知道如何注册其设备。 请参阅[用户需要了解的有关设备注册的内容](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 此信息适用于 Microsoft Intune 和 Configuration Manager 托管的移动设备。  

  > [!div class="button"]
  [< 上一步](create-service-connection-point.md)  [下一步 >](set-up-additional-management.md)

