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
ms.openlocfilehash: e217c7afc2910a23fe3f29fa215d58574f3d79d8
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137807"
---
# <a name="prepare-intune-for-user-migration"></a>准备 Intune 以进行用户迁移 

适用范围：*System Center Configuration Manager (Current Branch)*    
用户从混合 MDM 迁移至 Intune 独立版之前，请执行步骤来准备 Intune。 这些步骤帮助确保，已迁移的用户和他们的设备继续得到管理。 当完成这些步骤并开始将迁移到 Intune 时，会给您的用户没有大量影响。  

## <a name="fix-issues-found-during-data-collection-and-import"></a>修复在数据收集和导入过程中发现的问题
如果你使用 Intune 数据导入程序工具[Configuration Manager 数据导入到 Microsoft Intune](migrate-import-data.md)，它汇总无法导入的对象。 下表列出了一些典型问题和解决在 Intune 中的步骤： 

|问题  |修复  |
|---------|---------|
|基于直接成员身份或复杂集合不会自动迁移。|在 Azure 以替换未导入的集合中创建 Azure Active Directory (Azure AD) 组。 然后，将对象分配到组。|
|没有可导入策略 |重新创建该策略在 Intune 中。|
|对象的部署未导入|将对象分配到组。 组应包括部署的集合中的相同用户。|

## <a name="create-intune-objects"></a>创建 Intune 对象 
如果您[Configuration Manager 数据导入到 Microsoft Intune](migrate-import-data.md)和修复问题，在过程中，验证是否正确配置导入的对象。 此外需要在组织中的 Intune 中创建任何其他对象 （策略、 配置文件和应用）。 

## <a name="assign-intune-licenses-to-migrated-users"></a>将 Intune 许可证分配给已迁移用户
在配置管理器中，向 Intune 订阅添加集合和集合的成员才能注册其设备。 尽管 Intune 许可证保留给已注册的设备，将这些许可证不与用户或设备相关联。 例如，不会为已注册的设备的用户在 Azure AD 中找到 Intune 许可证。 

在 Intune 独立配置每个用户的 Intune 许可证。 将许可证配置*之前*将用户迁移至 Intune 独立版。 此操作可确保，用户和他们的设备由 Intune MDM 机构更改后。 有关详细信息，请参阅[将 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/licenses-assign)。 

## <a name="verify-intune-user-groups"></a>验证 Intune 用户组
将用户和组很可能已在 Azure AD 中，因为已配置的目录同步。 若要确保你的用户属于正确的用户组，建议对你的 Intune 用户组进行审阅。 您为目标策略、 配置文件和应用到这些组。 请确保迁移至 Intune 独立版的用户属于正确的组。 

## <a name="configure-role-based-administration-control-rbac"></a>配置基于角色的管理控制 (RBAC)
作为迁移的一部分，请在 Intune 中配置所有必需的 RBAC 角色，并将用户分配至这些角色。 例如资源的范围有 RBAC 在 Configuration Manager 和 Intune 之间的差异。 有关详细信息，请参阅[Intune 基于角色的管理控制 (RBAC)](https://docs.microsoft.com/intune/role-based-access-control)。

## <a name="assign-apps-and-policies-to-aad-groups"></a>将应用和策略分配至 AAD 组
如果您[Configuration Manager 数据导入到 Microsoft Intune](migrate-import-data.md)，很多对象可能已分配给 Azure AD 组。 验证 （应用、 策略和配置文件） 的所有对象均都分配到正确的 Azure AD 组。 如果对象分配正确之后在用户迁移和迁移不应具有对用户造成任何大量影响, 自动配置用户的设备。 有关如何将对象分配给 Azure AD 组的详细信息，请参阅以下文章： 
- [分配策略](https://docs.microsoft.com/intune/get-started-policies)  
- [分配配置文件](https://docs.microsoft.com/intune/device-profile-assign)  
    > [!NOTE]  
    > 在 Intune 部署新的电子邮件配置文件，用户将收到重新输入其密码的提示。 此行为会导致正在 redownloaded 用户设备上的电子邮件。 由用户完成任何自定义修改将需要再次执行。 
- [分配应用](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>条款和条件策略
和其他租户级策略一样，一旦为租户启用了混合机构，条款和条件策略都自动迁移到 Intune。  但是，必须分配条款和条件包含的组进行迁移的用户可以准确地报告的已迁移的用户接受并确保未来的条款和条件更新和设备的正确目标的条款和条件注册。 用户无需重新接受条款和条件，除非存在于 Configuration Manager 控制台中的策略所做的更改。 有关详细信息，请参阅[分配条款和条件](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions)。

## <a name="configure-the-exchange-connector"></a>配置 Exchange Connector
如果使用 Exchange 并且在 Configuration Manager 中有本地 Exchange Connector，则需要[在 Intune 中配置本地 Exchange Connector](https://docs.microsoft.com/intune/exchange-connector-install)。 此外请考虑以下各节以帮助您迁移到 Intune Exchange Connector，并确保可在迁移后正常工作条件性访问中的信息。

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>帮助你迁移到 Intune Exchange Connector 的 PowerShell 脚本 
PowerShell 脚本可帮助你做好准备，将 Exchange 设备从 Configuration Manager Exchange Connector 转换到 Intune Exchange Connector。 虽然运行这些脚本为可选操作，但我们建议你选择运行，以从 Exchange 中删除非活动设备，来防止 Intune 发现不必要的设备。 运行脚本可确保通过 Exchange 发现的设备可以尽可能顺利地与注册 Intune 的设备合并。 在设置 Intune Exchange Connector 之前运行这些脚本。 PowerShell 脚本是 Intune 数据导入程序安装的一部分，可用于后续文章中介绍的[将 Configuration Manager 数据导入到 Microsoft Intune](migrate-import-data.md)。 有关详细信息及脚本下载，请转到 [Microsoft Intune 数据导入程序](https://github.com/ConfigMgrTools/Intune-Data-Importer) GitHub 页面。

### <a name="steps-to-make-sure-conditional-access-works-properly-after-user-migration"></a>步骤以确保正常运行用户迁移后确保条件性访问的工作原理
条件访问正常工作后迁移用户，并确保你的用户继续有权访问其电子邮件服务器，请确保设置以下配置：
- 如果 Exchange ActiveSync 默认访问级别设置 (DefaultAccessLevel) 被设置为“阻止”或“隔离”，则设备可能会无法访问电子邮件。 
- 如果 Exchange Connector 的安装 Configuration Manager 中，**时由规则不管理移动设备的访问级别**设置的值为**允许访问**，安装[内部部署 Exchange 连接器](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access)之前迁移用户的 Intune 中。 在配置在 Intune 中的默认访问级别设置**Exchange 本地**页面**高级 Exchange ActiveSync 访问设置**。 有关详细信息，请参阅[配置 Exchange 本地访问](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access)。
- 为两个连接器使用相同的配置。 最新配置的连接器将覆盖以前由其他连接器写入的 ActiveSync 组织设置。 如果以不同的方式配置连接器，它可能导致意外的条件访问更改。
- 用户迁移至 Intune 独立版后，从面向 Configuration Manager 的条件访问中删除这些用户。

## <a name="configure-the-microsoft-intune-certificate-connector"></a>配置 Microsoft Intune 证书连接器
如果通过 NDES 使用 SCEP 来颁发证书，需要配置 Microsoft Intune 证书连接器。 在 Intune 中 NDES 连接器的计算机不能为承载 NDES 连接器配置管理器中的同一台计算机。 有关详细信息，请参阅[配置和管理使用 Intune SCEP 证书](https://docs.microsoft.com/intune/certificates-scep-configure)。 

> [!Important]    
> 配置连接器后，修改已导入的 SCEP 配置文件以引用新的服务器 URL。

## <a name="next-step"></a>下一步
为迁移准备 Intune 后，即可将一组测试用户迁移至 Intune 独立版。 有关详细信息，请参阅[（混合机构） 的特定用户的 MDM 机构更改](migrate-mixed-authority.md)。


