---
title: 准备 Intune 以进行用户迁移
titleSuffix: Configuration Manager
description: 了解如何在 Azure 上准备 Intune，以便从混合 MDM 迁移用户。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/26/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.collection: M365-identity-device-management
ms.openlocfilehash: 68cf60bd5ebcb38e08dd3de6d7cc144752de848c
ms.sourcegitcommit: b9cc8e723c5d8c3be44edad24ad29d75c0cdd2b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2019
ms.locfileid: "71826175"
---
# <a name="prepare-intune-for-user-migration"></a>准备 Intune 以进行用户迁移 

适用范围：*System Center Configuration Manager （Current Branch）*  @ no__t-1  
在将用户从混合 MDM 迁移到 Intune 独立版之前，请执行准备 Intune 的步骤。 这些步骤可帮助确保已迁移的用户及其设备继续受到管理。 完成这些步骤并开始迁移到 Intune 后，你的用户将不会产生任何 signifcant 影响。  

## <a name="fix-issues-found-during-data-collection-and-import"></a>修复在数据收集和导入过程中发现的问题
如果使用 Intune 数据导入工具工具将[Configuration Manager 数据导入 Microsoft Intune](migrate-import-data.md)，则会汇总无法导入的对象。 下表列出了一些典型的问题以及在 Intune 中修复这些问题的步骤： 

|问题  |能够  |
|---------|---------|
|基于直接成员身份或在复杂的集合不会自动迁移。|在 Azure 中创建 Azure Active Directory （Azure AD）组以替换未导入的集合。 然后，将对象分配给组。|
|无法导入策略 |在 Intune 中重新创建该策略。|
|对象的部署未导入|将对象分配给组。 组应包括部署的集合中的相同用户。|

## <a name="create-intune-objects"></a>创建 Intune 对象 
如果在过程中将[Configuration Manager 数据导入 Microsoft Intune](migrate-import-data.md)并修复了问题，请验证是否正确配置了导入的对象。 还需要在你的组织中创建你需要的 Intune 中的任何其他对象（策略、配置文件和应用）。 

## <a name="assign-intune-licenses-to-migrated-users"></a>将 Intune 许可证分配给已迁移用户
在 Configuration Manager 中，你将一个集合添加到 Intune 订阅，并且集合的成员可以注册其设备。 尽管 Intune 许可证是为注册的设备保留的，但这些许可证并不与用户或设备相关联。 例如，对于具有已注册设备的用户，你找不到 Azure AD 中的 Intune 许可证。 

在 Intune 独立版中，为每个用户配置 Intune 许可证。 在将用户迁移到 Intune 独立版*之前*，请配置许可证。 此操作可确保用户及其设备在更改 MDM 机构后由 Intune 管理。 有关详细信息，请参阅[将 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/licenses-assign)。 

## <a name="verify-intune-user-groups"></a>验证 Intune 用户组
你的用户和组可能已在 Azure AD 中，因为你已配置了目录同步。 若要确保你的用户属于正确的用户组，建议对你的 Intune 用户组进行审阅。 你将策略、配置文件和应用指向这些组。 请确保迁移至 Intune 独立版的用户属于正确的组。 

## <a name="configure-role-based-administration-control-rbac"></a>配置基于角色的管理控制 (RBAC)
作为迁移的一部分，请在 Intune 中配置所有必需的 RBAC 角色，并将用户分配至这些角色。 Configuration Manager 和 Intune 中的 RBAC 之间存在差异，例如资源的作用域。 有关详细信息，请参阅[Intune 的基于角色的管理控制（RBAC）](https://docs.microsoft.com/intune/role-based-access-control)。

## <a name="assign-apps-and-policies-to-aad-groups"></a>将应用和策略分配至 AAD 组
如果将[Configuration Manager 数据导入 Microsoft Intune](migrate-import-data.md)，则可能已将很多对象分配到 Azure AD 组。 验证是否已将所有对象（应用、策略和配置文件）分配给正确的 Azure AD 组。 如果正确分配对象，则在迁移用户后会自动配置用户的设备，并且迁移不会对用户造成任何 signifcant 影响。 有关将对象分配到 Azure AD 组的详细信息，请参阅以下文章： 
- [分配策略](https://docs.microsoft.com/intune/get-started-policies)  
- [分配配置文件](https://docs.microsoft.com/intune/device-profile-assign)  
    > [!NOTE]  
    > 当 Intune 部署新的电子邮件配置文件时，用户将收到重新输入其密码的提示。 此行为导致电子邮件要用户的设备上。 用户所做的任何自定义修改都需要再次完成。 
- [分配应用](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>条款和条件策略
和其他租户级策略一样，一旦为租户启用了混合机构，条款和条件策略都自动迁移到 Intune。  但是，你必须将条款和条件分配给包含已迁移用户的组，以准确报告已迁移用户的接受情况，并确保条款和条件正确定向到将来的条款和条件更新或设备登记. 除非在 Configuration Manager 控制台中对策略进行了更改，否则用户无需面向条款和条件。 有关详细信息，请参阅[分配条款和条件](https://docs.microsoft.com/intune/enrollment/terms-and-conditions-create#create-terms-and-conditions)。

## <a name="configure-the-exchange-connector"></a>配置 Exchange Connector
如果使用 Exchange 并且在 Configuration Manager 中有本地 Exchange Connector，则需要[在 Intune 中配置本地 Exchange Connector](https://docs.microsoft.com/intune/exchange-connector-install)。 还应考虑以下部分中的信息，以帮助你迁移到 Intune Exchange Connector，并确保迁移后的条件性访问可以正常工作。

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>帮助你迁移到 Intune Exchange Connector 的 PowerShell 脚本 
PowerShell 脚本可帮助你做好准备，将 Exchange 设备从 Configuration Manager Exchange Connector 转换到 Intune Exchange Connector。 虽然运行这些脚本为可选操作，但我们建议你选择运行，以从 Exchange 中删除非活动设备，来防止 Intune 发现不必要的设备。 运行脚本可确保通过 Exchange 发现的设备可以尽可能顺利地与注册 Intune 的设备合并。 在设置 Intune Exchange Connector 之前运行这些脚本。 PowerShell 脚本是 Intune 数据导入程序安装的一部分，可用于后续文章中介绍的[将 Configuration Manager 数据导入到 Microsoft Intune](migrate-import-data.md)。 有关详细信息及脚本下载，请转到 [Microsoft Intune 数据导入程序](https://github.com/ConfigMgrTools/Intune-Data-Importer) GitHub 页面。

### <a name="steps-to-make-sure-conditional-access-works-properly-after-user-migration"></a>确保条件访问在用户迁移后正常工作的步骤
要使条件访问在你迁移用户后正常工作，并确保你的用户能够继续访问其电子邮件服务器，请确保设置以下配置：
- 如果 Exchange ActiveSync 默认访问级别设置 (DefaultAccessLevel) 被设置为“阻止”或“隔离”，则设备可能会无法访问电子邮件。 
- 如果在 Configuration Manager 中安装 Exchange Connector，并且**当移动设备未通过规则的管理时访问级别**的值设置为 "**允许访问**"，则在 Intune 中安装[本地 Exchange Connector](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access)迁移用户。 在 "**高级 Exchange ActiveSync 访问设置**" 中的 " **exchange 内部部署**" 页上配置 Intune 中的默认访问级别设置。 有关详细信息，请参阅[配置 Exchange 本地访问](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access)。
- 为两个连接器使用相同的配置。 最新配置的连接器将覆盖以前由其他连接器写入的 ActiveSync 组织设置。 如果以不同的方式配置连接器，它可能导致意外的条件访问更改。
- 用户迁移至 Intune 独立版后，从面向 Configuration Manager 的条件访问中删除这些用户。

## <a name="configure-the-microsoft-intune-certificate-connector"></a>配置 Microsoft Intune 证书连接器
如果通过 NDES 使用 SCEP 来颁发证书，需要配置 Microsoft Intune 证书连接器。 在 Intune 中托管 NDES 连接器的计算机不能与在 Configuration Manager 中承载 NDES 连接器的计算机相同。 有关详细信息，请参阅[通过 Intune 配置和管理 SCEP 证书](https://docs.microsoft.com/intune/certificates-scep-configure)。 

> [!Important]    
> 在配置连接器后，请修改导入的 SCEP 配置文件以引用新的服务器 URL。

## <a name="next-step"></a>下一步
准备好用于迁移的 Intune 后，可以将一组测试用户迁移到 Intune 独立版。 有关详细信息，请参阅[更改特定用户的 MDM 机构（混合颁发机构）](migrate-mixed-authority.md)。


