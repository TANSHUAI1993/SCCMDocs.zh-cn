---
title: 启用共同管理的条件访问
titleSuffix: Configuration Manager
description: 根据 Intune 的符合性规则控制用户对组织资源的访问
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d5e5c7d6075697431f8c537366dc16164fedd1f
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754655"
---
# <a name="conditional-access-with-co-management"></a>启用共同管理的条件访问

条件访问可确保只有受信任的用户才能使用受信任的应用访问受信任设备上的组织资源。 它是在云中从头开始构建的。 无论用户是使用 Intune 管理设备还是使用共同管理扩展 Configuration Manager 部署，它都以相同的方式工作。

在以下视频中，高级项目经理 Joey Glocke 和产品营销经理 Locky Ainley 将介绍并演示启用共同管理的条件访问：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

借助共同管理，Intune 可以评估网络中的每台设备，以便确定它的可信度。 它通过以下两种方式进行评估：

1. Intune 确保设备或应用得到管理并已安全配置。 此项检查取决于用户如何设置组织的符合性策略。 例如，确保所有设备都启用了加密且未越狱。  

    - 此评估在出现安全漏洞之前基于配置执行  

    - 对于共同管理的设备，Configuration Manager 还会执行基于配置的评估。 例如，必需的更新或应用符合性。 Intune 将此评估与自身的评估结合起来。  

2. Intune 检测设备上的活动安全事件。 它使用 [Windows Defender 高级威胁防护](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/get-started)和其他 [Mobile Threat Defense 提供程序](https://www.lookout.com/about/partners/microsoft)的智能安全。 这些合作伙伴对设备进行持续的行为分析。 此分析检测活动事件，然后将此信息传递给 Intune 用于实时符合性评估。  

    - 此评估在出现安全漏洞之后基于事件执行  

Microsoft 公司副总裁 Brad Anderson 在 Ignite 2018主题演讲期间通过现场演示深入探讨了条件访问。 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

条件访问还提供了一个集中的位置，以便查看所有联网设备的运行状况。 用户可以获得云规模的优势，这对于测试 Configuration Manager 生产实例尤其有用。


## <a name="benefits"></a>优点

所有 IT 团队都会在网络安全方面投入大量精力。 在访问网络之前，必须确保每台设备都满足安全和业务要求。 用户可以借助条件访问确定以下几个方面： 
- 每台设备是否加密  
- 设备是否安装了恶意软件  
- 设备设置是否更新  
- 设备是否已越狱或取得 root 权限  

条件访问将对组织数据的精细控制与用户体验相结合，从而最大限度地提高工作人员在任意位置的任何设备上的工作效率。

下面的视频介绍如何将[高级威胁防护](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) 集成到经常使用的常见方案中：

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

通过共同管理，Intune 可以纳入 Configuration Manager 的职责以评估所需更新或应用的安全标准符合性。 对于任何希望继续使用 Configuration Manager 管理复杂的应用和修补程序的 IT 组织，此行为非常重要。

条件访问也是开发[零信任网络](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/)体系结构的关键部分。 通过条件访问，符合要求的设备访问控制可覆盖零信任网络的基础层。 此功能是未来为组织提供保护的重要组成部分。

若要了解详细信息，请参阅有关[使用 Windows Defender 高级威胁防护中的计算机风险数据增强条件访问](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559)的博客文章。



## <a name="case-studies"></a>案例研究

IT 咨询公司 Wipro 使用条件访问来保护和管理所有 91,000 名员工所使用的设备。 在最近的案例研究中，Wipro 的 IT 副总裁指出：

> 实现条件访问是 Wipro 的一大胜利。现在，我们的所有员工都可以按需移动访问信息。
> 我们增强了安全性，并提高了员工生产效率。**** 现在，91,000 名员工可以从任何地方的任何设备高度安全地访问超过 100 个应用。

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

其他示例包括： 

- 雀巢公司为超过 150,000 名员工使用基于应用的条件访问  

- 自动化软件公司 Cadence 现在可以确保“只有托管设备才能访问 Office 365 应用（如 Teams）和公司的 Intranet”。 他们还可以让员工“更安全地访问基于云的其他应用，如 Workday 和 Salesforce”。 有关 Cadence 使用 Intune 的更多体验，请参阅 [Cadence 通过 Microsoft 365 中的移动协作工具提高业务处理速度](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365)。

Intune 还可与 Cisco ISE、Aruba Clear Pass 和 Citrix NetScaler 等合作伙伴完全集成。 集成了这些合作伙伴后，用户可以根据 Intune 注册和跨这些其他平台的设备符合性状态来维护访问控制。

有关详细信息，请参阅下列视频：
- [Brad Anderson 详细演示条件访问](https://youtu.be/8321obNofgM?t=547)  
- [终结点区域 1805 的其他详细信息](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>价值主张

通过集成的条件访问和 ATP，用户可以强化每个 IT 组织的基础环节：为云访问提供保护。

在超过 63% 的数据泄露中，攻击者通过较弱的、默认的或被盗的用户凭据访问组织的网络。 条件访问侧重于保护用户标识，它可避免凭据被盗。 条件访问管理和保护用户标识，无论是特权标识还是非特权标识都不例外。 没有更好的方法来保护设备及设备上的数据。

由于条件访问是企业移动性 + 安全性 (EMS) 的核心部分，因此，不需要本地设置或体系结构。 使用 Intune 和 Azure Active Directory (Azure AD)，可以在云中快速配置条件访问。 如果目前使用的是 Configuration Manager，可以通过共同管理轻松地将环境扩展到云，并立即开始使用。

有关 ATP 集成的更多信息，请参阅以下博客文章：[Windows Defender ATP 设备风险评分暴露新的网络攻击，推动条件访问以保护网络](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/)。 这篇文章详细介绍了一个高级黑客组织如何使用从未见过的工具。 Microsoft 云检测到攻击并加以阻止，因为目标用户使用了条件访问。 入侵激活了设备基于风险的条件访问策略。 虽然攻击者已经在网络中建立了立足点，但该策略会自动限制受攻击的计算机访问由 Azure AD 管理的组织服务和数据。



## <a name="configure"></a>配置

[启用共同管理](/sccm/comanage/how-to-enable)后，可以轻松使用条件访问。 它需要将符合性策略工作负载移至 Intune。 有关详细信息，请参阅[如何将 Configuration Manager 工作负载切换为 Intune](/sccm/comanage/how-to-switch-workloads)。 

有关使用条件访问的详细信息，请参阅以下文章： 

- [Azure AD 中的条件访问](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Intune 设备符合性策略](https://docs.microsoft.com/intune/device-compliance)  

- [Intune 基于应用的条件访问](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> 条件访问功能对于已联接混合 Azure AD 的设备是现成可用的。 这些功能包括多重身份验证和混合 Azure AD 联接访问控制。 具有此特性是因为它们基于 Azure AD 属性。 若要利用 Intune 和 Configuration Manager 中基于配置的评估，请启用共同管理。 通过此配置，可直接从 Intune 对符合要求的设备实现访问控制。 它还提供 Intune 的符合性策略评估功能。  

