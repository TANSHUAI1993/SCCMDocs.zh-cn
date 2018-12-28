---
title: 管理 Skype for Business Online 访问
titleSuffix: Configuration Manager
description: 了解如何使用条件访问策略管理对 Skype for Business Online 的访问。
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f5a03629fdea4a8fc496db624d0b32657d9bec83
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53419098"
---
# <a name="manage-skype-for-business-online-access"></a>管理 Skype for Business Online 访问

*适用于：System Center Configuration Manager (Current Branch)*


基于你指定的条件，使用 Skype for Business Online 的条件访问策略管理对 Skype for Business Online 的访问权限。  


 当目标用户尝试在其设备上使用 Skype for Business Online 时，将评估以下方面：![ConditionalAccess_SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>先决条件  

- 为 Skype for Business Online 启用[新式验证](https://aka.ms/SkypeModernAuth)。   

- 你的所有用户必须使用 Skype for Business Online。 如果部署中同时具有 Skype for Business Online 和本地 Skype for Business，则条件访问策略不会应用于本地用户。  

- 需要访问 Skype for Business Online 的设备必须：  

  -   是 Android 或 iOS 设备

  -   已向 Microsoft Intune 注册

  -   符合任何已部署的 Microsoft Intune 符合性策略

  Azure Active Directory 保存设备状态，并可基于指定的条件授权访问或阻止访问。  
  如果不满足条件，则用户将在登录时看到以下消息的其中一条：  

- 如果设备未向 Microsoft Intune 注册，或未在 Azure Active Directory 中注册，则会显示一条说明告知用户如何安装公司门户应用并进行注册。  

- 如果设备不符合，则会显示一条消息，引导用户转到公司门户网站或公司门户应用。 公司门户中包含关于此问题及其修复方法的信息。  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>为 Skype for Business Online 配置条件访问  

### <a name="step-1-configure-active-directory-security-groups"></a>步骤 1:配置 Active Directory 安全组  
 在开始之前，针对条件访问策略配置 Azure Active Directory 安全组。 在 Office 365 管理中心中配置这些组。 这些组包含作为策略目标的用户或从策略排除的用户。 如果将某个用户设定为策略的目标，则其使用的每个设备必须合规才能访问资源。  

 你可以指定两种组类型以用于 Skype for Business 策略：  

-   **目标组**包含将应用策略的用户  

-   **免除组**包含从策略中排除的用户  
    如果用户位于两个组中，则会将其免除。  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>步骤 2:配置和部署合规性策略  
 创建符合性策略并将其部署到被设定为 Skype for Business Online 策略目标的所有设备。  

 有关如何配置符合性策略的详细信息，请参阅[管理设备符合性策略](../../protect/deploy-use/device-compliance-policies.md)。  

> [!NOTE]  
>  如果你尚未部署符合性策略，但是启用了 Skype for Business Online 策略，则允许所有已向 Microsoft Intune 注册的目标设备进行访问。  


### <a name="step-3-configure-the-skype-for-business-online-policy"></a>步骤 3:配置 Skype for Business Online 策略  
 配置策略以要求只有托管及符合性设备才能访问 Skype for Business Online。 此策略存储在 Azure Active Directory 中。  

1. 在 [Microsoft Intune 管理控制台](https://manage.microsoft.com)中，单击“策略” > “条件访问” > “Skype for Business Online 策略”。  

    ![ConditionalAccess_SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2. 选择“启用条件访问策略”。  

3. 在“应用程序访问”下，可以选择将条件访问策略应用到：  

   -   iOS  

   -   Android  

4. 在“目标组”下，单击“修改”以选择要应用策略的 Azure Active Directory 安全组。 可以选择将此策略应用于所有用户或仅针对特定用户组。  

5. 在“免除组” 下，可以选择“修改”  以选择从此策略中免除的 Azure Active Directory 安全组。  

6. 完成后，请单击“保存” 。  

   现在为 Skype for Business Online 配置了条件访问。 不需要部署条件访问策略，它将立即生效。  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>监视遵从性和条件性访问策略  
 在“组”工作区中，可以查看设备的条件访问状态。  

 选择任何移动设备组，然后在“设备”选项卡上，选择以下“筛选器”之一：  

-   未向 AAD 注册的设备会被阻止访问 Skype for Business Online

-   不符合的设备会被阻止访问 Skype for Business Online  

-   已向 AAD 注册的符合性设备可以访问 Skype for Business Online  

### <a name="see-also"></a>另请参阅  

 [在 System Center Configuration Manager 中管理设备合规性策略](../../protect/deploy-use/device-compliance-policies.md)
