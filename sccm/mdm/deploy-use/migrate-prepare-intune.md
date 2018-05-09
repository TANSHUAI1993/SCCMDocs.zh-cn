---
title: 准备 Intune 以进行用户迁移
titleSuffix: Configuration Manager
description: 了解如何在 Azure 上准备 Intune，以便从混合 MDM 迁移用户。
author: aczechowski
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: a2636713f8c121eecd826eeba060f8e3f8e865f3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-intune-for-user-migration"></a>准备 Intune 以进行用户迁移 

*适用范围：System Center Configuration Manager (Current Branch)*    

将用户从混合 MDM（Intune 与 Configuration Manager 集成）迁移至 Intune 独立版之前，必须采取步骤来准备 Intune。 这些步骤帮助确保已迁移的用户及其设备继续得到管理。 当完成这些步骤并开始迁移至 Intune 时，这对你的用户应该是透明的。  

## <a name="fix-issues-found-during-data-collection-and-import"></a>修复在数据收集和导入过程中发现的问题
如果已完成[将 Configuration Manager 数据导入 Microsoft Intune](migrate-import-data.md) 的过程，Intune 数据导入程序工具会提供一份有关所有无法导入的对象的摘要。 下表列出了一些可能遇到的典型问题，以及在 Intune 中可以采取的修复步骤： 

|问题  |修复  |
|---------|---------|
|基于直接成员资格的集合或复杂集合不能自动迁移。|必须在 Azure 中创建 Azure Active Directory (AAD) 组以替换未被导入的集合。 然后必须将对象分配到该组。|
|策略无法导入 |必须在 Intune 中重新创建策略。|
|对象的部署未导入|必须将对象分配到组。 该组应包含来自部署集合的相同用户。|

## <a name="create-intune-objects"></a>创建 Intune 对象 
如果已完成[将 Configuration Manager 数据导入 Microsoft Intune](migrate-import-data.md) 的过程并修复了导入进程中的问题，则应验证已导入对象的配置是否准确。 此外，在 Intune 中创建组织所需的任何其他对象（策略、配置文件、应用等）。 

## <a name="assign-intune-licenses-to-migrated-users"></a>将 Intune 许可证分配给已迁移用户
在 Configuration Manager 中将集合添加到 Intune 订阅，集合中的成员就可以注册他们的设备了。 虽然 Intune 许可证保留给已注册的设备，但是这些许可证和用户或设备之间没有特定关联。 例如，你不会在 AAD 中为具备已注册设备的用户找到 Intune 许可证。 但是在 Intune 独立版中，必须为每个用户配置 Intune 许可证。 必须在将用户迁移至 Intune 独立版之前就完成此操作，以确保用户及其设备在更改 MDM 机构后由 Intune 托管。 有关详细信息，请参阅[将 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/licenses-assign)。 

## <a name="verify-intune-user-groups"></a>验证 Intune 用户组
因为已配置目录数据同步，用户和组很可能已位于 AAD 中。 若要确保你的用户属于正确的用户组，建议对你的 Intune 用户组进行审阅。 使策略、配置文件、应用等面向这些组。 请确保迁移至 Intune 独立版的用户属于正确的组。 

## <a name="configure-role-based-administration-control-rbac"></a>配置基于角色的管理控制 (RBAC)
作为迁移的一部分，请在 Intune 中配置所有必需的 RBAC 角色，并将用户分配至这些角色。 请注意，Configuration Manager 和 Intune 中的 RBAC 有所不同，例如资源的范围。 有关详细信息，请参阅 [Intune 中基于角色的管理控制 (RBAC)](https://docs.microsoft.com/intune/role-based-access-control)。

## <a name="assign-apps-and-policies-to-aad-groups"></a>将应用和策略分配至 AAD 组
如果在迁移进程中已完成[将 Configuration Manager 数据导入 Microsoft Intune](migrate-import-data.md) 的阶段，将不同的 Configuration Manager 对象迁移到了 Intune，那么可能很多对象已分配至 AAD 组。 但是应验证是否所有对象（应用、策略、配置文件等）均已分配至正确的 AAD 组。 如果对象分配正确，用户设备会在用户迁移后自动配置，并且此迁移应对用户透明。 有关将对象分配至 AAD 组的详细信息，请参阅以下内容： 
- [分配策略](https://docs.microsoft.com/intune/get-started-policies) 
- [分配配置文件](https://docs.microsoft.com/intune/device-profile-assign) 
- [分配应用](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>条款和条件策略
和其他租户级策略一样，一旦为租户启用了混合机构，条款和条件策略都自动迁移到 Intune。  不过必须将条款和条件分配至包含已迁移用户的组，以准确反馈已迁移用户的接受情况，并确保这些条款和条件面向正确的目标，便于未来的条款和条件更新和设备注册。 用户无需重新接受条款和条件，除非 Configuration Manager 控制台中存在对策略的改动。 有关详细信息，请参阅[分配条款和条件](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions)。

## <a name="configure-the-exchange-connector"></a>配置 Exchange Connector
如果使用 Exchange 并且在 Configuration Manager 中有本地 Exchange Connector，则需要[在 Intune 中配置本地 Exchange Connector](https://docs.microsoft.com/intune/exchange-connector-install)。 此外请考虑以下各节中的信息以帮助你迁移到 Intune Exchange Connector，并确保迁移后可正常进行条件访问。

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>帮助你迁移到 Intune Exchange Connector 的 PowerShell 脚本 
PowerShell 脚本可帮助你做好准备，将 Exchange 设备从 Configuration Manager Exchange Connector 转换到 Intune Exchange Connector。 虽然运行这些脚本为可选操作，但我们建议你选择运行，以从 Exchange 中删除非活动设备，来防止 Intune 发现不必要的设备。 运行脚本可确保通过 Exchange 发现的设备可以尽可能顺利地与注册 Intune 的设备合并。 在设置 Intune Exchange Connector 之前运行这些脚本。 PowerShell 脚本是 Intune 数据导入程序安装的一部分，可用于后续文章中介绍的[将 Configuration Manager 数据导入到 Microsoft Intune](migrate-import-data.md)。 有关详细信息及脚本下载，请转到 [Microsoft Intune 数据导入程序](https://github.com/ConfigMgrTools/Intune-Data-Importer) GitHub 页面。

### <a name="steps-to-ensure-conditional-access-works-properly-after-user-migration"></a>确保用户迁移后正常进行条件访问的步骤
迁移用户后，为使条件访问能正常运行并确保用户可以继续访问其电子邮件服务器，请确保满足以下条件：
- 如果 Exchange ActiveSync 默认访问级别设置 (DefaultAccessLevel) 被设置为“阻止”或“隔离”，则设备可能会无法访问电子邮件。 
- 如果 Exchange Connector 安装在 Configuration Manager 中，并且“移动设备未由规则管理时的访问级别”设置的值为“允许访问”，那么在迁移用户之前必须在 Intune 中安装[本地 Exchange Connector](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access)。 在 Intune 中“高级 Exchange ActiveSync 访问设置”的“Exchange 本地部署”边栏选项卡上配置默认访问级别设置。 有关详细信息，请参阅[配置 Exchange 本地访问](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access)。
- 为两个连接器使用相同的配置。 最新配置的连接器将覆盖以前由其他连接器写入的 ActiveSync 组织设置。 如果以不同的方式配置连接器，它可能导致意外的条件访问更改。
- 用户迁移至 Intune 独立版后，从面向 Configuration Manager 的条件访问中删除这些用户。

## <a name="configure-the-microsoft-intune-certificate-connector"></a>配置 Microsoft Intune 证书连接器
如果通过 NDES 使用 SCEP 来颁发证书，需要配置 Microsoft Intune 证书连接器。 托管 Intune 中 NDES 连接器的计算机和托管 Configuration Manager 中 NDES 连接器的计算机不能相同。 有关详细信息，请参阅[使用 Intune 配置和管理 SCEP 证书](https://docs.microsoft.com/en-us/intune/certificates-scep-configure)。 

> [!Important]    
> 配置连接器之后，必须调整导入的 SCEP 配置文件以引用新的服务器 URL。

## <a name="next-step"></a>下一步
如果准备好 Intune 进行迁移，就可以将一组测试用户迁移至 Intune 独立版。 有关详细信息，请参阅[更改特定用户的 MDM 机构（混合机构）](migrate-mixed-authority.md)。


