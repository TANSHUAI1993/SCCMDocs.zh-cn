---
title: 使用共同管理的条件访问
titleSuffix: Configuration Manager
description: 控制用户对组织根据从 Intune 的符合性规则的资源访问
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754655"
---
# <a name="conditional-access-with-co-management"></a>使用共同管理的条件访问

条件性访问可确保只有受信任的用户才能访问组织资源上受信任的设备使用受信任的应用。 它是从零开始在云中构建的。 无论您是使用 Intune 或扩展 Configuration Manager 部署通过共同管理的设备，它的工作方式相同。

在以下视频中，高级项目经理 Joey Glocke 和产品营销经理 Locky Ainley 讨论和演示的共同管理的条件性访问：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

通过共同管理，Intune 评估以确定它是如何可信网络中的每个设备。 它在以下两种方式执行此评估版：

1. Intune 可确保设备或应用程序管理和安全配置。 此检查取决于如何设置你的组织符合性策略。 例如，确保所有设备启用加密并不是已越狱。  

    - 此评估版是预安全漏洞和配置基于  

    - 有关共同管理的设备，配置管理器也能基于配置的评估。 例如，所需更新或应用程序的符合性。 Intune 将合并其自己的评估以及此评估版。  

2. Intune 检测到的设备上的活动的安全事件。 它使用的智能安全[Windows Defender 高级威胁防护](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/get-started)和其他[移动威胁防御供应商](https://www.lookout.com/about/partners/microsoft)。 这些合作伙伴在设备上运行正在进行的行为分析。 此分析检测到活动的事件，然后将此信息传递到 Intune 以进行实时的符合性评估。  

    - 此评估非常后的安全漏洞和基于事件的  

Microsoft 公司副总裁 Brad Anderson 在 Ignite 2018 主题演讲期间讨论现场演示的深度中的条件访问。 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

条件性访问还提供了集中式的地方可以查看所有已连接网络的设备的运行状况。 获取云规模，尤其是对于非常重要测试 Configuration Manager 生产实例的优点。


## <a name="benefits"></a>优点

每个 IT 团队深受网络安全。 它是必须确保每个设备访问你的网络之前满足安全和业务需求。 使用条件性访问，您可以确定以下因素： 
- 如果每个设备进行加密  
- 如果安装了恶意软件  
- 如果其设置更新  
- 如果它是否已越狱或取得 root 权限  

条件访问结合了用户体验，可以在任何位置从任何设备上的工作人员工作效率最大化组织数据的精细控制。

下面的视频演示如何[高级线程防护](https://www.microsoft.com/windowsforbusiness/windows-atp)(ATP) 集成到您经常遇到的常见方案：

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

通过共同管理，Intune 可以将合并用于评估您的安全标准符合性所需的更新或应用的配置管理器的职责。 此行为是重要的 IT 组织，想要继续使用 Configuration Manager 进行复杂的应用程序和修补程序管理。

条件性访问也是开发的关键部分你[零信任网络](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/)体系结构。 使用条件性访问合规的设备访问控件所涉及的零信任网络的基础层。 此功能是如何保护你的组织在将来的大部分内容。

有关详细信息，请参阅博客文章上[增强 Windows Defender 高级威胁防护中的计算机风险数据的条件性访问](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559)。



## <a name="case-studies"></a>案例研究

IT 咨询公司 Wipro 使用条件性访问来保护和管理所有 91,000 员工使用的设备。 在最新的案例研究副总裁 Wipro 记下的 IT:

> *实现条件性访问是 Wipro 一大优点。现在，我们的所有员工都具有对按需的信息的移动访问。* 
> *我们增强了安全状况和员工提高工作效率。现在 91,000 员工受益于大于 100 的高度安全的访问中随处播放任意设备的应用。*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

其他示例包括： 

- Nestle，谁为超过 150,000 员工使用基于应用的条件性访问  

- 自动化软件公司，节奏、 可以现在请确保"仅托管的设备有权访问 Office 365 应用，如团队和公司的 intranet。" 它们也能提供希望员工队伍"更安全访问 Workday 和 Salesforce 等其他基于云的应用程序。" 有关使用 Intune 的节奏的体验的详细信息，请参阅[节奏增加移动的协作工具，Microsoft 365 中的业务的步伐](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365)。

Intune 与 Cisco ISE、 Aruba Clear Pass 和 Citrix NetScaler 等合作伙伴也完全集成。 与这些合作伙伴可以维护这些其他平台中基于 Intune 注册和设备符合性状态的访问控制。

有关详细信息，请参阅以下视频：
- [在详细信息的 Brad Anderson 演示条件性访问](https://youtu.be/8321obNofgM?t=547)  
- [从终结点区域 1805年的更多详细信息](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>价值主张

要使用条件性访问和 ATP 集成，增强每个 IT 组织的基本组件： 保护云的访问。

在超过 63%的所有数据泄露，攻击者获取弱、 默认设置，或被盗的用户凭据通过组织的网络访问权限。 条件性访问主要用于保护用户标识，因为它会限制凭据被盗。 条件性访问管理和保护标识，无论特权还是非特权。 没有更好方法来保护设备和其上的数据。

因为条件性访问是企业移动性 + 安全性 (EMS) 的核心组件，所以也无需在本地设置或所需的体系结构。 使用 Intune 和 Azure Active Directory (Azure AD)，快速可以在云中配置条件性访问。 如果当前正在使用 Configuration Manager，可以轻松地扩展到共同管理与云环境并开始立即使用。

有关 ATP 集成的详细信息，请参阅此博客文章[Windows Defender ATP 设备风险评分公开新的介入，驱动器条件性访问以保护网络](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/)。 它详细说明如何使用永远不会先看到工具的高级的黑客组。 Microsoft 云检测到并停止它们，因为目标的用户有条件性访问。 入侵激活设备的基于风险的条件性访问策略。 虽然攻击者已在网络中建立一席之地，但被利用的计算机已自动限制访问组织服务和数据由 Azure AD 管理。



## <a name="configure"></a>配置

当条件性访问是易于使用您[启用共同管理](/sccm/comanage/how-to-enable)。 它需要移动**符合性策略**工作负荷到 Intune。 有关详细信息，请参阅[如何将 Configuration Manager 工作负载切换为 Intune](/sccm/comanage/how-to-switch-workloads)。 

有关使用条件性访问的详细信息，请参阅以下文章： 

- [Azure AD 中的条件性访问](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Intune 设备符合性策略](https://docs.microsoft.com/intune/device-compliance)  

- [使用 Intune 的基于应用的条件性访问](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> 条件性访问功能变得可立即用于混合 Azure AD 加入设备。 这些功能包括多重身份验证和混合 Azure AD 联接访问控制。 此行为是因为它们基于 Azure AD 属性。 若要利用 Intune 和 Configuration Manager 从基于配置的评估，请启用共同管理。 此配置可直接从 Intune 兼容设备的访问控制。 它还为您提供了 Intune 的符合性策略评估功能。  

