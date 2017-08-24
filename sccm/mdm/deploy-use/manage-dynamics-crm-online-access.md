---
title: "管理 Dynamics CRM Online 访问权限 | Microsoft Docs"
description: "了解如何使用 Microsoft Intune 条件访问从 iOS 和 Android 设备控制对 Microsoft Dynamics CRM Online 的访问。"
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bfc4c51-b25c-4c70-b81e-8a3b6ddf02c8
caps.latest.revision: "5"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: bd00f12ae3bc14a34d24c22c3d5277d275d51e85
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-dynamics-crm-online-access-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理 Dynamics CRM Online 访问

*适用范围：System Center Configuration Manager (Current Branch)*

可使用 Microsoft Intune 条件访问从 iOS 和 Android 设备控制对 Microsoft Dynamics CRM Online 的访问。  Intune 条件访问有两个组件：
* [设备合规性策略](../../protect/deploy-use/device-compliance-policies.md)，设备必须符合该策略才会被视为合规。
* [条件访问策略](../../protect/deploy-use/manage-access-to-services.md)在其中指定设备必须满足才可访问服务的条件。

若要深入了解条件访问的工作原理，请参阅文章[管理对服务的访问](../../protect/deploy-use/manage-access-to-services.md)。


目标用户尝试在其设备上使用 Dynamics CRM 应用时，将评估以下方面：

![图表显示了决策点，用于确定是允许还是阻止设备访问服务](media/mdm-ca-dynamics-crm-flow-diagram.png)

需要访问 Dynamics CRM Online 的设备必须：
* 是 **Android** 或 **iOS** 设备。
* 已向 Microsoft Intune **注册**。
* **符合**任何已部署的 Microsoft Intune 合规性策略。

基于指定的条件，设备状态存储在可授予或阻止访问的 Azure Active Directory 中。

如果不满足条件，则用户将在登录时看到以下消息的其中一条：
* 如果设备未向 Microsoft Intune 注册，或未在 Azure Active Directory 中注册，则会显示一条消息，说明如何安装公司门户应用并进行注册。
* 如果设备不合规，则会显示一条消息，将用户定向到 Microsoft Intune 公司门户网站或公司门户应用，用户可在其中找到有关该问题及其修正方式的信息。

## <a name="configure-conditional-access-for-dynamics-crm-online"></a>为 Dynamics CRM Online 配置条件访问  
### <a name="step-1-configure-active-directory-security-groups"></a>步骤 1：配置 Active Directory 安全组

在开始之前，针对条件访问策略配置 Azure Active Directory 安全组。 可在 **Office 365 管理中心**中配置这些组。 这些组用于从策略中确定目标用户或免除用户。 如果将某个用户设定为策略的目标，则其使用的每个设备必须合规才能访问资源。

可指定两种组类型用于 Dynamics CRM 策略：
* **目标组** - 包含将应用策略的用户组。
* **免除组** - 包含从策略中免除的用户的组。

如果用户位于两个组中，则会将其从策略中免除。

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>步骤 2：配置和部署合规性策略
对所有会受此策略影响的设备[创建和部署](../../protect/deploy-use/device-compliance-policies.md)合规性策略。 这些设备将是目标组中的用户使用的所有设备。

> [!NOTE]
> 将合规性策略部署到 Microsoft Intune 组，而条件访问策略以 Azure Active Directory 安全组为目标。

> [!IMPORTANT]
> 如果尚未部署合规性策略，则设备将被视为符合。

准备就绪后，继续执行步骤 3。
### <a name="step-3-configure-the-dynamics-crm-policy"></a>步骤 3：配置 Dynamics CRM 策略
接下来，配置策略，要求仅托管和合规设备可访问 Dynamics CRM。 此策略会存储在 Azure Active Directory 中。

1.  在 Microsoft Intune 管理控制台中，选择“策略”>“条件访问”>“Dynamics CRM Online 策略”。

     ![Dynamics CRM Online 条件性访问策略页的屏幕快照](media/mdm-ca-dynamics-crm-policy-configuration.png)

2.  选择“启用条件访问”策略。
3.  在“应用程序访问”下，可以选择将条件访问策略应用到：
  * **iOS**
  * **Outlook Web Access (OWA)**
4.  在“目标组”下，选择“修改”，选择将应用策略的 Azure Active Directory 安全组。 你可以选择将其应用于所有用户或仅针对特定用户组。
5.  在“免除组”下，可以选择“修改”，选择从此策略中免除的 Azure Active Directory 安全组。
6.  完成后，选择“保存”。

现已为 Dynamics CRM 配置了条件访问。 不需要部署条件访问策略，它将立即生效。
##  <a name="monitor-the-compliance-and-conditional-access-policies"></a>监视遵从性和条件性访问策略

在“组”工作区中，可以查看设备的条件访问状态。

选择任何移动设备组，然后在“设备”选项卡上，选择以下“筛选器”之一：
* **未向 AAD 注册的设备** - 从 Dynamics CRM 阻止这些设备。
* **不合规的设备** - 从 Dynamics CRM 阻止这些设备。
* **已向 AAD 注册的合规设备** - 这些设备可以访问 Dynamics CRM。

###  <a name="see-also"></a>另请参阅
[管理对电子邮件的访问](../../protect/deploy-use/manage-email-access.md)

[管理对 SharePoint Online 的访问](../../protect/deploy-use/manage-sharepoint-online-access.md)

[管理对 Skype for Business Online 的访问](../../protect/deploy-use/manage-skype-for-business-online-access.md)
