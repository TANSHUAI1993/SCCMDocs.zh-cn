---
title: 使用 Azure AD 进行共同管理
titleSuffix: Configuration Manager
description: 与 Azure AD，可以充分利用提高工作效率为用户和安全资源，在云中和本地环境
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b773c0bfe8cd0f8253a67ac96f5a0113b7206c0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754699"
---
# <a name="use-azure-ad-for-co-management"></a>使用 Azure AD 进行共同管理

在云中，标识是新的控制平面。 Azure Active Directory (Azure AD)，可链接在本地和云环境中的用户、 设备和应用程序。 到 Azure AD 设备注册，可提高工作效率为你的用户并为你的资源的安全。 在 Azure AD 中拥有的设备是共同管理和基于设备的条件性访问的基础。 

基于设备的条件性访问的详细信息，请参阅[How To:需要使用条件性访问的云应用访问权限的被管理的设备](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

在下面的视频中，高级项目经理 Sandeep Deo 产品营销的经理 Adam Harbour 讨论和演示 Azure AD 进行共同管理：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD 提供公司拥有的设备以满足组织的需要两个的选项：  

- **Azure AD 加入设备**:将你的 Windows 10 设备加入到 Azure AD，而无需将它们加入到你的本地 Active Directory  

    - 支持 Windows 10

    - 而无需任何额外配置才能在本地环境设置  

    - 通过在 Azure AD 中启用的一些设置，可以让用户将设备加入 Azure AD 通过 Windows 安装程序体验 (OOBE)  

    - 有关详细信息，请参阅[如何：计划你的 Azure AD 联接实现](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **混合 Azure AD 加入设备**:将现有的已加入域的设备加入到 Azure AD  

    - 支持 Windows 10，Windows 8.1 和 Windows 7

    - 使用 AD FS 声明或 Azure AD Connect 设置  

    - 适用于 Windows 10 中执行联接计算机上下文中，因此用户无需执行额外的步骤  

    - 有关详细信息，请参阅[如何计划你的混合 Azure Active Directory 联接实现](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

这两个选项为用户提供类似的功能。 它非常灵活，以便选择其中之一根据你的需求。 例如，可以[访问本地资源](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso)从 Azure AD 加入计算机即使它们未加入到 Active Directory。 

您可以加入到各种环境中的 Azure AD 的设备而不管你[身份验证方法](https://docs.microsoft.com/azure/security/azure-ad-choose-authn)。 例如，联合身份验证，或者云身份验证。 

如果已在本地 Active Directory，设置任一选项非常简单。 



## <a name="benefits"></a>优点

将设备加入 Azure AD 提供了到你的组织的以下好处：

#### <a name="single-sign-on-to-cloud-resources"></a>对云资源的单一登录
在加入到 Azure AD 的设备，你获取访问的任何云或本地资源的集成的体验。 后登录到已加入 Azure AD 的 Windows 计算机时，会获得单一登录方式登录到所有应用程序没有任何其他的登录提示。  

#### <a name="windows-hello-for-business"></a>Windows hello 企业版
Windows hello 企业版提供强密码身份验证对 Windows 10。 通过加入到 Azure AD 的设备，你可以启用 Windows hello 企业版跨用户群的在本地和云资源。 Windows hello 企业版消除记住复杂的密码或无意中将它们公开的问题。 其登录的进程是简单且安全。 

有关详细信息，请参阅 [Windows Hello 企业版](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)。  

#### <a name="device-based-conditional-access"></a>基于设备的条件性访问
启用基于设备状态以更好地保护你组织的数据的条件性访问。 基于设备的条件性访问需要的托管的设备。 此设备必须是合规的设备或混合 Azure AD 加入设备。 对于加入 Azure AD 的设备，需要 Intune 将设备标记为符合。 但对于混合 Azure AD 加入设备，设备状态本身用于评估条件性访问。 共同管理为你提供一些额外的优点的评估符合性通过 Intune 的混合 Azure AD 加入设备。 此功能可确保该设备的配置保持不变。 

基于设备的条件性访问的详细信息，请参阅[How To:需要使用条件性访问的云应用访问权限的被管理的设备](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)。  

#### <a name="automatic-device-licensing"></a>自动设备授权
所有 Windows 10 设备加入 Azure AD 都要通过检查许可证。 这些检查，可自动将其升级从专业版到企业通过 Microsoft 云。 当从用户中删除相关的订阅时，设备会自动将降级其许可证。 此功能提供单个窗格控件，用于管理 Windows 许可证，而无需任何复杂的进程或在本地系统。

#### <a name="self-service-functionality"></a>自助服务功能
自助服务功能包括自助服务密码重置和 BitLocker 恢复密钥。 Azure AD 还提供了直接的选项以重置密码或访问 BitLocker 恢复密钥。 可以使用 Azure AD 来重置密码，直接从 Windows 锁定屏幕，而不是从 web 浏览器。 这些功能减少冲突的用户，并帮助降低支持人员成本为你的组织。  

有关详细信息，请参阅[快速入门：自助服务密码重置](https://docs.microsoft.com/azure/active-directory/authentication/quickstart-sspr)。

#### <a name="enterprise-state-roaming"></a>企业状态漫游
所有加入到 Azure AD 的设备可以同步到云及其设置。 向其用户登录同步其提高工作效率体验的所有设置的任何设备。  



## <a name="value-proposition"></a>价值主张

通过这两种方法将设备加入到 Azure AD 是加快数字化转型。 这样，Microsoft 365 提供的更多的功能。 您将有更好的体验，并且将为你的数据具有更高的安全性。 

Azure AD 提供多个选项来简化您的工作负载，例如：

- 从单个位置管理你的组织中的所有设备标识  

- 自助服务密码重置，从而降低技术支持成本。 然后用户可以重置 Windows 10 锁定屏幕中的密码，你的设备上在任何时间。  



## <a name="configure"></a>配置

如果已有的本地 Active Directory 环境，并且你想要将已加入域的设备加入到 Azure AD，配置混合 Azure AD 加入设备。 有关详细信息[如何计划你的混合 Azure Active Directory 联接实现](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)。 

Configuration Manager 具有客户端设置设[与 Azure AD 中自动注册新的 Windows 10 已加入域的设备](/sccm/core/clients/deploy/about-client-settings#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory)。 有关配置客户端设置的详细信息，请参阅[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。

如果你想要配置 Azure AD 加入设备而无需还将它们加入到你的本地的域，查看的注意事项适用于 Azure AD 加入您的环境中。 一旦您决定使用 Azure AD 加入，您有多种方法可部署它根据组织的需求。 有关详细信息，请参阅下列文章：
- [如何：计划你的 Azure AD 联接实现](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [了解预配选项](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  

