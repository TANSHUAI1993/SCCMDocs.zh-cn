---
title: 更改 MDM 机构
titleSuffix: Configuration Manager
description: 了解如何将 MDM 机构从混合 MDM 更改为 Intune 独立版的特定用户 （混合 MDM 机构）。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 05/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.collection: M365-identity-device-management
ms.openlocfilehash: ccc38188729a05329cc240a9f424ccce9fd433b2
ms.sourcegitcommit: d1df13fc95a1f1540177c294555d9be26161b9cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974078"
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>更改特定用户的 MDM 机构（混合 MDM 机构）

适用范围：System Center Configuration Manager (Current Branch)

您可以在同一租户中配置混合的 MDM 机构。 管理在 Microsoft Intune 和其他一些用户使用混合 mdm。 此文提供有关如何开始将用户移至 Intune 独立版的信息。 它假定你已完成以下步骤：  

- 使用数据导入工具[将 Configuration Manager 对象导入 Intune](migrate-import-data.md)（可选）。  

- [准备适用于用户迁移的 Intune](migrate-prepare-intune.md) 以确保在迁移用户及其设备后仍能继续对其进行管理。  

> [!Note]  
> 完全重置你的租户中删除所有策略、 应用和设备注册。 如果你决定你想要执行此过程，致电支持人员以获得帮助。  

管理已迁移的用户及其设备在 Intune 中。 继续管理 Configuration Manager 中的其他设备。 若要验证一切按预期方式工作，启动与小测试组用户。 然后逐渐迁移其他用户组。 在准备就绪时，为 Intune 独立版将租户级 MDM 机构从 Configuration Manager 切换。

> [!Important]  
> 自 2018 年 8 月 13 日起，混合移动设备管理[功能停用](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。 有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<!--Intune feature 2683117-->  



## <a name="things-to-know-before-you-migrate-users"></a>迁移用户前需知事项

- 分阶段迁移期间，Configuration Manager 中任何现有的 MDM 策略或应用继续适用于混合 MDM 设备。  

- 集合中与 Intune 订阅关联的用户的设备可以在混合 MDM 中注册。 只要用户具有 Intune/EMS 许可证，将在 Intune 中管理与不在集合中的用户相关联的所有设备。  

    > [!Note]  
    > 即使你已通过 Configuration Manager 控制台进行阻止，用户仍可以注册 Intune 独立版。 若要完全阻止用户进行注册，不要向不必要的用户授权 Intune 许可证。 他们不能注册许可证的情况下。<!--SCCMDocs issue 738-->  

- 将用户迁移至 Intune 时，该用户和设备会在约 15 分钟后出现在 Azure 门户的 Intune 中。  

- 将用户迁移至 Intune 独立版时，请为 Intune 独立版和混合 MDM 的设备继续管理 Configuration Manager 中的以下设置：  

    - [Apple Push Notification 服务 (APNS) 证书](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)  

    - [设备注册计划](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)  

        > [!Note]  
        > 不需要重新创建你的 DEP 令牌或从 Configuration Manager 中删除它。 它会自动迁移到 Intune 24 小时后你租户的 MDM 机构从 Configuration Manager 更改为 Intune。 此更改是迁移的最后一步。 （如果在 24 小时内不会迁移 DEP 令牌，请联系 Microsoft 支持部门以获得帮助。）  

    - 注册配置文件  

    - [Volume Purchase Program (VPP) 许可证](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)  

    - 企业标识符  

    - [代码签名证书](/sccm/mdm/deploy-use/enroll-hybrid-windows)  

    - [设备类别](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)  

    - [注册管理员](/sccm/mdm/plan-design/device-enrollment-methods)  

    - Terms and conditions  

    - Windows SLK  

    - 公司门户品牌  

    > [!Important]  
    > 使用 Configuration Manager 控制台继续编辑租户级策略。 检查完[更改租户级 MDM 机构](/sccm/mdm/deploy-use/change-mdm-authority)迁移至 Intune，已自动管理 Configuration Manager 中的租户级策略迁移到 Azure 上的 Intune。 此类策略的一个示例是 Apple Push Notification 服务 (APNs) 证书。<!--SCCMDocs issue #971-->  

- 如果使用代码签名证书，建议以分阶段的方式迁移用户。 在移动设备迁移后，证书颁发机构可以请求新的证书。 通过使用分阶段的方法来迁移用户（及其设备），可限制同时进行证书颁发机构请求的数量。  

- 不要迁移已在 Configuration Manager 中添加为设备注册管理员 (DEM) 的任何用户帐户。 接下来，将租户级 MDM 机构更改为 Intune 后，这些用户帐户将准确迁移。 如果执行迁移之前租户级 MDM 机构更改的 DEM 用户帐户，必须手动将用户添加为 Azure 上 Intune 中 DEM。 但是，通过使用 DEM 注册的设备不会成功迁移。 请致电支持部门来迁移这些设备。 有关详细信息，请参阅[添加设备注册管理器](https://docs.microsoft.com/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager)。  

    > [!Note]  
    > 在混合机构模式下，不要通过从 ConfigMgr 云集合中删除帐户来将它们移动到 Intune。 如果这样做，用户将成为标准用户，并且不能注册 15 台以上的设备。 相反，一旦完全将 MDM 机构切换租户迁移这些用户和他们的设备。<!--Intune bug 2174210-->  

- 通过使用 DEM 和设备，无需注册设备[用户相关性](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices)不会自动迁移到新的 MDM 机构。 若要切换这些 MDM 设备的管理机构，请参阅[迁移不具备用户关联的设备](#migrate-devices-without-user-affinity)。  



## <a name="migrate-users-to-intune"></a>将用户迁移至 Intune

若要测试 Intune 配置是否按预期运行，请先迁移一小部分用户及其设备。 接着，确认一切按预期运行后就可以开始迁移具有更多用户的更多 AAD 组及用户设备。



## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>将测试用户组迁移至 Intune 独立版

集合中与 Intune 订阅关联的用户的设备可以在混合 MDM 中注册。 如果用户具有分配的 Intune 许可证，可从集合中删除用户，当其已注册的设备迁移到 Intune 独立版。 你还没有已许可证分配给用户，如果你打算迁移，请参阅[分配 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/licenses-assign)。 在 Intune 订阅的集合中，可以从主集合中排除用户集合，以迁移已排除集合中的用户。

在下面的示例中，“混合用户”集合包含“所有用户”集合中的所有成员。 此配置允许任何用户将设备注册到混合 MDM。 若要将用户迁移至 Intune 独立版，请选择“排除集合”并添加具有要迁移的用户的集合。 当准备好迁移更多用户时，添加其他包含这些用户的排除集合。

![排除集合](../media/migrate-excludecollections.png)

> [!Note]  
> 当你具有**所有用户**为 Intune 订阅选择的集合，不允许你将添加一个规则以排除集合。 创建新的集合基于**所有用户**集合。 验证集合包含预期的用户。 然后编辑 Intune 订阅以使用新的集合。 可以从新集合中排除用户集合以迁移用户。  

若要将测试用户组迁移到 Intune，创建用户集合，其中包含要迁移的用户。 然后从用于 Intune 订阅集合中排除的用户集合。  

下图概述了用户迁移工作原理。

![混合机构概述](../media/migrate-mixedauthority.svg)

1. 验证用户是否具有 Intune/EMS 许可证。  

2. 创建一个要从 Intune 订阅集合中排除的集合。 在此示例中，“所有混合用户”集合中包含一个规则以排除“迁移试点”集合中的用户。 User1 是“迁移试点”集合中的一个成员，将从“所有混合用户”集合中排除。  

3. **User1**的设备现在在 Azure 门户中管理从 Intune。  

4. 所有其他设备继续通过 Configuration Manager 控制台进行管理。  

> [!Important]  
> 当将用户从混合环境移到独立版中时，删除的策略将挂起七天。<!-- SCCMDocs issue #1066 -->


## <a name="verify-intune-standalone-functionality"></a>验证 Intune 独立版功能

迁移了一小部分用户后，验证用户设备是否在 Intune 中列出。 转到“设备”，并选择“所有设备”。

然后验证策略、配置文件和应用是否在用户设备上按预期运行。



## <a name="migrate-additional-users"></a>迁移其他用户

验证 Intune 独立版按预期正常运行后，开始迁移其他用户。 就像使用一组测试用户创建集合，创建包含要迁移的用户的集合。 从与 Intune 订阅关联的集合中排除这些集合。 有关详细信息，请参阅[迁移至 Intune 独立版的测试用户组](#migrate-a-test-group-of-users-to-intune-standalone)。



## <a name="migrate-devices-without-user-affinity"></a>迁移无用户关联的设备

若要迁移到 Intune 不通过用户关联注册窗体的单独设备配置管理器，使用 Switch-mdmdeviceauthority PowerShell cmdlet。  在迁移中发生的 Azure 中的 Intune 中使用 cmdlet 迁移所选的设备验证后应为所选设备。 然后，当您准备，MDM 机构更改为 Intune 租户以完成具有为其的 MDM 机构的 Configuration Manager 的任何剩余的设备的迁移。

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet Switch-MdmDeviceAuthority

#### <a name="synopsis"></a>摘要

该 cmdlet 可切换无用户关联的 MDM 设备（例如，批量注册的设备）的管理机构。 该 cmdlet 将切换 Intune 和 Configuration Manager 管理机构。 它将切换为基于管理机构，当你运行 cmdlet 时指定的设备。

### <a name="syntax"></a>语法

`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>参数

#### `-Credential <PSCredential>`

切换设备管理权限时使用的 Azure AD 用户帐户的 PowerShell 凭据对象。 如果未指定参数，被提示用户提供凭据。 此用户帐户的目录角色应为“全局管理员”或“受限管理员”，管理角色为“Intune 管理员”。

#### `-DeviceIds <Guid[]>`

需要切换其管理机构的 MDM 设备的 ID。 设备 ID 是由 Configuration Manager 控制台显示的设备唯一标识符。

#### `-Force [<SwitchParameter>]`

指定参数以禁用“是否继续”提示。

#### `-LogFilePath <string>`

日志文件位置的路径。

#### `-LoggingLevel <SourceLevels>`

日志级别用于确定需要写入日志文件的日志类型。

以下是 LoggingLevel 的可能值：

- ActivityTracing
- All
- 严重
- 错误
- 信息
- 关闭
- 详细
- 警告

#### `-Confirm [<SwitchParameter>]`

将提示您在执行命令前进行确认。

#### `-WhatIf [<SwitchParameter>]`

描述如果执行该命令而不实际执行该命令会发生什么情况。

#### `<CommonParameters>`

此 cmdlet 支持以下公共参数：Verbose、 Debug、 ErrorAction、 ErrorVariable、 WarningAction、 WarningVariable、 OutBuffer、 PipelineVariable 和 OutVariable。 有关详细信息，请参阅 [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216)。

### <a name="example-1"></a>示例 1

``` powershell
C:\PS>Switch-MdmDeviceAuthority -Credential $creds -DeviceIds $deviceIds

  DeviceId       : 62e6ea43-18f8-4278-bcd4-a4baed2c6d24
  Success        : True
  FailureReason  :
  NewAuthority   : Intune
  CompletionTime : 11/15/2017 8:00:11 PM

Description

-----------

Successfully switched the management authority of the device from Configuration Manager to Intune.
```

### <a name="remarks"></a>备注

- 若要查看此示例，请键入：`get-help Switch-MdmDeviceAuthority -examples`  
- 要获取详细信息，请键入：`get-help Switch-MdmDeviceAuthority -detailed`  
- 要获取技术信息，请键入：`get-help Switch-MdmDeviceAuthority -full`  
- 要获取在线帮助，请键入：`get-help Switch-MdmDeviceAuthority -online`  



## <a name="next-steps"></a>后续步骤

在迁移用户并测试 Intune 功能后，请考虑是否已准备好为 Intune 租户[更改 MDM 机构](migrate-change-mdm-authority.md)，从 Configuration Manager 更改为 Intune。
