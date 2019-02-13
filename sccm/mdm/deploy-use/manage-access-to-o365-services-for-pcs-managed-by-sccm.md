---
title: 管理 O365 服务的访问权限
titleSuffix: Configuration Manager
description: 了解如何为由 System Center Configuration Manager 管理的电脑配置对 Office 365 服务的条件访问。
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b45e9f586616a1f620864a6e6dc8d0777a118251
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122281"
---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>管理对由 System Center Configuration Manager 管理的电脑的 O365 服务的访问

适用范围：System Center Configuration Manager (Current Branch)

<!--1191496--> 配置 Configuration Manager 管理的电脑的 Office 365 服务的条件性访问。  

> [!Important]  
> 混合 MDM 包括本地条件性访问[已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。 有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<!--Intune feature 2683117-->  
> 
> 如果在使用 Configuration Manager 客户端管理的设备上使用条件性访问，以确保它们仍然受到保护，首次启用条件性访问在 Intune 中的为这些设备在迁移之前。 启用共同管理配置管理器中，将符合性策略工作负载移动到 Intune，然后完成从 Intune 混合版迁移到 Intune 独立版。 有关详细信息，请参阅[条件访问的共同管理](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access)。 


有关使用 Microsoft Intune 为注册设备和托管设备配置条件访问的信息，请参阅[在 System Center Configuration Manager 中管理服务访问权限](../../protect/deploy-use/manage-access-to-services.md)。 本文还介绍了已加入域但未对符合性进行评估的设备。

> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  


## <a name="supported-services"></a>支持的服务  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>支持的电脑  

-   Windows 7
-   Windows 8.1
-   Windows 10

## <a name="supported-windows-servers"></a>支持的 Windows 服务器

-   Windows Server 2008 R2
-   Windows Server 2012
-   Windows Server 2012 R2
-   Windows Server 2016

    > [!IMPORTANT]
    > 对于可能有多个用户同时登录的 Windows Servers，可将相同的条件访问策略部署到所有登录用户。

## <a name="configure-conditional-access"></a>配置条件访问  
 若要设置条件访问，必须先创建符合性策略并配置条件访问策略。 为电脑配置条件访问策略时，可以要求电脑是合规的，以便能够访问 Exchange Online 和 SharePoint Online 服务。  

### <a name="prerequisites"></a>先决条件  

- ADFS 同步和 O365 订阅。 O365 订阅用于设置 Exchange Online 和 SharePoint Online。  

- Microsoft Intune 订阅。 应在 Configuration Manager 控制台中配置 Microsoft Intune 订阅。 Intune 订阅用于将设备符合性状态中继到 Azure Active Directory 和用户授权。  

  电脑必须满足以下要求：  

- 将设备自动注册到 Azure Active Directory 所要满足的[先决条件](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)   

   可以通过合规性策略向 Azure AD 注册电脑。  

  -   对于 Windows 8.1 和 Windows 10 电脑，你可以使用 Active Directory 组策略将设备配置为自动注册到 Azure AD。  

  -   对于 Windows 7 电脑，必须通过 System Center Configuration Manager 将设备注册软件包部署到 Windows 7 电脑。 有关详细信息，请参阅[将已加入 Windows 域的设备自动注册到 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) 一文。  

- 必须使用[启用了](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)新式验证的 Office 2013 或 Office 2016。  

  下列步骤适用于 Exchange Online 和 SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>步骤 1。 配置合规性策略  
 在 Configuration Manager 控制台中，使用以下规则创建合规性策略：  

-   **需要在 Azure Active Directory 中的注册：** 此规则检查用户的设备工作场所加入 Azure AD 中，如果没有，请在 Azure AD 中自动注册该设备。 仅 Windows 8.1 支持自动注册。 对于 Windows 7 PC，请部署 MSI 来执行自动注册。 有关相关信息，请参阅[将设备自动注册到 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  

-   **在晚于特定天数的截止日期之前安装所有必需的更新：** 对于从用户的设备上的所需更新的部署截止时间在宽限期内指定的值。 添加此规则还会自动安装所有挂起的必需更新。 指定“必需的自动更新”规则中的必需更新。   

-   **需要使用 BitLocker 驱动器加密功能：** 此规则检查的主驱动器 (例如，c:\\) 在设备上进行 BitLocker 加密。 如果主要设备，访问电子邮件和 SharePoint services 不启用加密的 BitLocker 会被阻止。  

-   **需要反恶意软件：** 此规则检查 System Center Endpoint Protection 或 Windows Defender 是否已启用并正在运行。 如果未启用，则将阻止对电子邮件和 SharePoint 服务的访问。  

-   **报告为正常运行状况证明服务：** 这种情况包括四个子规则检查设备符合性对设备运行状况证明服务。 有关详细信息，请参阅[运行状况证明](/sccm/core/servers/manage/health-attestation)。 

    - **需要在设备上启用 BitLocker**
    - **需要在设备上启用安全启动** 
    - **需要在设备上启用代码完整性**
    - **需要在设备上启用开机初期启动的反恶意软件**  

    >[!Tip]  
    > 版本 1710 首次将设备运行状况证明的条件访问条件作为[预发布功能](/sccm/core/servers/manage/pre-release-features)引入。 从 1802 版开始，此功能不再属于预发行功能。<!--1235616-->  

    > [!Note]  
    > 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>步骤 2。 评估条件访问的影响  
 运行“条件访问符合性报告”。 可以在“报表” > “符合性和设置管理”下的“监视”工作区中找到它。 此报表显示所有设备的符合性状态。 会阻止报告为不符合的设备访问 Exchange Online 和 SharePoint Online。  

 ![Configuration Manager 控制台中，监视工作区、 报表、 报表、 符合性和设置管理：条件访问相容性报告](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>配置 Active Directory 安全组  
 根据策略类型将条件访问策略的目标设定为用户组。 这些组包含策略设定为目标的用户，或从策略中免除的用户。 如果将某个用户设定为策略的目标，则其使用的每个设备必须符合才能访问服务。  

 Active Directory 安全用户组 这些用户组应同步到 Azure Active Directory。 你还可以在 Office 365 管理中心或 Intune 帐户门户中配置这些组。  

 可以在每个策略中指定两种组类型。 ：  

-   **目标组** - 策略应用到的用户组。 同一个组应同时用于合规性和条件访问策略。  

-   **被免除的组** - 从策略中免除的用户组（可选）。  
    如果用户位于两个组中，则会将其从策略中免除。  

     仅会评估设定为条件访问策略的目标的组。  

### <a name="step-3-create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>步骤 3。 为 Exchange Online 和 SharePoint Online 创建条件访问策略  

1.  在 Configuration Manager 控制台中，单击“资产和符合性”。  

2.  若要为 Exchange Online 创建策略，请选择“启用 Exchange Online 的条件访问策略”。  

     若要为 SharePoint Online 创建策略，请选择“启用 Exchange Online 的条件访问策略”。  

3.  在“主页”选项卡的“链接”组，单击“在 Intune 控制台中配置条件性访问策略”。 你可能需要提供用于连接 Configuration Manager 和 Intune 的帐户的用户名和密码。  

     随即将打开 Intune 管理控制台。  

4.  对于 Exchange Online，在 Microsoft Intune 管理控制台中，单击“策略”>“条件访问”>“Exchange Online 策略”。  

     对于 SharePoint Online，在 Microsoft Intune 管理控制台中，单击“策略”>“条件访问”>“SharePoint Online 策略”。  

5.  将 Windows 电脑要求设置为**设备必须是合规的选项**。  

6.  在“目标组”下，单击“修改”以选择要应用策略的 Azure Active Directory 安全组。  

    > [!NOTE]  
    >  同一安全用户组应用于部署合规性策略，目标组应用于条件访问策略。  

     在“免除组”下，可以选择“修改”以选择从此策略中免除的 Azure Active Directory 安全组。  

7.  单击“保存”以创建和保存策略  

用户可在软件中心查看符合性信息。 如果由于不符合而被阻止，则在修正符合性问题后启动新的策略评估。  


## <a name="see-also"></a>另请参阅

- [使用 System Center Configuration Manager 保护数据和站点基础架构](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Configuration Manager 条件访问疑难解答流程图](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0)
