---
title: 使用 Azure AD 进行共同管理
titleSuffix: Configuration Manager
description: 借助 Azure AD，可以在云和本地环境中提高用户的生产力并增强资源的安全性
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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754699"
---
# <a name="use-azure-ad-for-co-management"></a>使用 Azure AD 进行共同管理

在云中，标识是新的控制平面。 Azure Active Directory (Azure AD) 支持联接云和本地环境中的用户、设备和应用程序。 将设备注册到 Azure AD 可以提高用户的工作效率，并增强资源的安全性。 将设备置于 Azure AD 中是实现共同管理和基于设备的条件访问的基础。 

有关基于设备的条件访问的详细信息，请参阅[操作指南：使用条件访问要求托管设备实现云应用访问](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

在下面的视频中，高级项目经理 Sandeep Deo 和产品营销经理 Adam Harbour 介绍并演示了如何使用 Azure AD 进行共同管理：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD 提供了两个适用于公司自有设备的选项，以满足组织的需求：  

- **已联接 Azure AD 的设备**：无需将 Windows 10 设备联接本地 Active Directory，即可将它们联接 Azure AD  

    - 支持 Windows 10

    - 无需为本地环境提供任何额外配置，即可进行设置  

    - 启用 Azure AD 中的一些设置后，你的用户即可通过 Windows 设置体验 (OOBE) 将设备联接 Azure AD  

    - 有关详细信息，请参阅[如何：规划 Azure AD 联接实现](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **已联接混合 Azure AD 的设备**：将现有已加入域的设备联接 Azure AD  

    - 支持 Windows 10、Windows 8.1 和 Windows 7

    - 使用 AD FS 声明或 Azure AD Connect 设置  

    - 对于 Windows 10，联接操作在计算机上下文中执行，这样一来，用户就无需执行其他步骤  

    - 有关详细信息，请参阅[如何规划混合 Azure Active Directory 联接实现](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

两种选项为用户提供的功能相似。 可以根据自己的需求灵活选择任意一个。 例如，即使本地资源未联接 Active Directory，用户也可以从已联接 Azure AD 的计算机[访问本地资源](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso)。 

无论使用的是哪种[身份验证方法](https://docs.microsoft.com/azure/security/azure-ad-choose-authn)，都可以在各种环境中将设备联接 Azure AD。 例如，联合身份验证或云身份验证。 

如果已有本地 Active Directory，可轻松设置任意一种选项。 



## <a name="benefits"></a>优点

将设备联接 Azure AD 将为组织提供以下优势：

#### <a name="single-sign-on-to-cloud-resources"></a>单一登录到云资源
可以在已联接 Azure AD 的设备上获得访问任意云或本地资源的统一体验。 登录到已联接 Azure AD 的 Windows 计算机后，不再出现任何其他登录提示，即会单一登录到所有应用程序。  

#### <a name="windows-hello-for-business"></a>Windows Hello 企业版
Windows Hello 企业版将无强密码身份验证引入 Windows 10。 将设备联接 Azure AD 后，可以跨云资源和本地资源的用户群启用 Windows Hello 企业版。 Windows Hello 企业版让用户无需记忆复杂密码，也不会意外暴露密码。 它的登录过程简单且安全。 

有关详细信息，请参阅 [Windows Hello 企业版](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)。  

#### <a name="device-based-conditional-access"></a>基于设备的条件访问
启用基于设备状态的条件访问，进一步保护组织数据。 基于设备的条件访问要求设备是托管设备。 此设备必须是符合要求的设备，或已联接混合 Azure AD 的设备。 对于已联接 Azure AD 的设备，需要使用 Intune 将设备标记为符合要求的设备。 然而，对于已联接混合 Azure AD 的设备，将通过设备状态本身来评估条件访问。 共同管理还提供了额外的优势：对于已联接混合 Azure AD 的设备，通过 Intune 评估符合性。 此功能可确保设备配置完整无缺。 

有关基于设备的条件访问的详细信息，请参阅[操作指南：使用条件访问要求托管设备实现云应用访问](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)。  

#### <a name="automatic-device-licensing"></a>自动化设备许可
将对所有已联接 Azure AD 的 Windows 10 设备进行许可证检查。 这些检查支持通过 Microsoft 云自动将它们从 Pro 版升级到 Enterprise 版。 删除用户的相关订阅时，设备会自动将其许可证降级。 此功能提供了一个集中的控制平台来管理 Windows 许可证，且无需任何复杂流程或本地系统即可实现。

#### <a name="self-service-functionality"></a>自助服务功能
自助服务功能包括自助式密码重置和 BitLocker 恢复密钥。 此外，Azure AD 还为用户提供了重置密码或访问 BitLocker 恢复密钥的直接选项。 借助 Azure AD，无需通过 Web 浏览器，即可直接从 Windows 锁屏界面重置密码。 这些功能减少了用户冲突，有助于为组织缩减支持人员成本。  

有关详细信息，请参阅[快速入门：自助式密码重置](https://docs.microsoft.com/azure/active-directory/authentication/quickstart-sspr)。

#### <a name="enterprise-state-roaming"></a>企业状态漫游
所有已联接 Azure AD 的设备都可以将其设置同步到云。 用户登录的任何设备都会同步其所有设置，以提高效率。  



## <a name="value-proposition"></a>价值主张

通过任意方法将设备联接 Azure AD 有助于实现数字化转型。 可通过它启用 Microsoft 365 提供的更多功能。 用户能够获得更出色的体验，并增强数据安全性。 

Azure AD 提供了多个可简化工作负载的选项，例如：

- 集中管理组织内的所有设备标识  

- 通过启用自助式密码重置，降低支持人员成本。 用户可以随时从设备的 Windows 10 锁屏界面重置密码。  



## <a name="configure"></a>配置

如果已有本地 Active Directory 环境，并且想要将已加入域的设备联接 Azure AD，请配置已联接混合 Azure AD 的设备。 有关详细信息，请参阅[如何规划混合 Azure Active Directory 联接实现](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)。 

Configuration Manager 提供了[自动将已加入域的新 Windows 10 设备注册到 Azure AD](/sccm/core/clients/deploy/about-client-settings#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory) 的客户端设置。 若要详细了解如何配置客户端设置，请参阅[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。

若要在不将设备加入本地域的前提下为设备配置 Azure AD 联接，请查看相关注意事项，以在环境中实现 Azure AD 联接。 决定实现 Azure AD 联接后，可根据组织的需求从大量部署选项中进行选择。 有关详细信息，请参阅下列文章：
- [如何：规划 Azure AD 联接实现](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [了解预配选项](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  

