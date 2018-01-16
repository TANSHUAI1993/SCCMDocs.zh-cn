---
title: "更改特定用户的 MDM 机构（混合 MDM 机构）"
titleSuffix: Configuration Manager
description: "了解如何将部分用户的 MDM 机构从混合 MDM 更改为 Intune 独立版。"
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 59fb06d14002f781e0448a64bb0064b4add2f087
ms.sourcegitcommit: ac9268e31440ffe91b133c2ba8405d885248d404
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>更改特定用户的 MDM 机构（混合 MDM 机构） 

*适用范围：System Center Configuration Manager (Current Branch)*    

若要在同一租户中配置混合 MDM 机构，可以选择部分用户在 Intune 中管理，其他用户则由混合 MDM 管理（Intune 与 Configuration Manager 集成）。 本文介绍如何开始将用户移至 Intune 独立版，并假定你已完成以下步骤：
- 使用数据导入工具[将 Configuration Manager 对象导入 Intune](migrate-import-data.md)（可选）。
- [准备适用于用户迁移的 Intune](migrate-prepare-intune.md) 以确保在迁移用户及其设备后仍能继续对其进行管理。

> [!Note]    
> 若决定要对租户执行将删除所有策略、应用和设备注册的完全重置，请致电支持部门寻求帮助。

已迁移的用户及其设备将在 Intune 中管理，其他设备则继续在 Configuration Manager 中管理。 首先以一小组测试用户开始，验证一切是否按预期进行。 接着会逐渐迁移其他用户组，直到准备好将租户级 MDM 机构从 Configuration Manager 切换至 Intune 独立版。 

## <a name="things-to-know-before-you-migrate-users"></a>迁移用户前需知事项
- 分阶段迁移期间，Configuration Manager 中任何现有的 MDM 策略或应用继续适用于混合 MDM 设备。
- 集合中与 Intune 订阅关联的用户的设备可以在混合 MDM 中注册。 只要用户具有 Intune/EMS 许可证，将在 Intune 中管理与不在集合中的用户相关联的所有设备。 
- 将用户迁移至 Intune 时，该用户和设备会在约 15 分钟后出现在 Azure 门户的 Intune 中。  
- 将用户迁移至 Intune 独立版时，请为 Intune 独立版和混合 MDM 的设备继续管理 Configuration Manager 中的以下设置：
    - [Apple Push Notification 服务 (APNS) 证书](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [设备注册计划](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
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
  > 使用 Configuration Manager 控制台继续编辑租户级策略。 [更改租户级 MDM 机构](change-mdm-authority.md)为 Intune 后，将在 Azure 上 Intune 中管理这些策略。 
-   如果使用代码签名证书，建议以分阶段的方式迁移用户。 在移动设备迁移后，证书颁发机构可以请求新的证书。 通过使用分阶段的方法来迁移用户（及其设备），可限制同时进行证书颁发机构请求的数量。
- 建议不要迁移已在 Configuration Manager 中添加为设备注册管理员的任何用户帐户。 接下来，将租户级 MDM 机构更改为 Intune 后，这些用户帐户将准确迁移。 如果在租户级 MDM 机构更改前迁移设备注册管理员用户帐户，则必须在 Azure 上 Intune 中手动将该用户添加为设备注册管理员。 但是使用设备注册管理员注册的设备不会成功迁移。 必须致电支持部门来迁移这些设备。 更多详细信息，请参阅[添加设备注册管理员](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager)。
- 使用设备注册管理员注册的设备和无[用户关联](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices)的设备不会自动迁移至新的 MDM 机构。 若要切换这些 MDM 设备的管理机构，请参阅[迁移不具备用户关联的设备](#migrate-devices-without-user-affinity)。

## <a name="migrate-users-to-intune"></a>将用户迁移至 Intune
若要测试 Intune 配置是否按预期运行，请先迁移一小部分用户及其设备。 接着，确认一切按预期运行后就可以开始迁移具有更多用户的更多 AAD 组及用户设备。

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>将测试用户组迁移至 Intune 独立版
集合中与 Intune 订阅关联的用户的设备可以在混合 MDM 中注册。 从集合删除用户时，如果该用户具备分配的 Intune 许可证，他们的注册设备将迁移至 Intune 独立版。 如果还未对计划迁移的用户分配许可证，请参阅[将 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/licenses-assign)。 在 Intune 订阅的集合中，可以从主集合中排除用户集合，以迁移已排除集合中的用户。 

在下面的示例中，“混合用户”集合包含“所有用户”集合中的所有成员。 这允许任何用户将设备注册到混合 MDM。 若要将用户迁移至 Intune 独立版，请选择“排除集合”并添加具有要迁移的用户的集合。 当准备好迁移更多用户时，可以添加其他包含这些用户的排除集合。 

![排除集合](../media/migrate-excludecollections.png)

> [!Note] 
> 如果为 Intune 订阅选择了“所有用户”集合，就不能对排除集合添加规则。 请基于“所有用户”集合创建一个新集合，验证此集合是否包含预期的用户，然后编辑 Intune 订阅以使用这个新集合。 可以从新集合中排除用户集合以迁移用户。 

若要将测试用户组迁移至 Intune，请创建包含待迁移用户的用户集合，然后从用于 Intune 订阅的集合中排除该用户集合。   

下图概述了用户迁移工作原理。

 ![混合机构概述](../media/migrate-mixedauthority.svg)

1. 验证用户是否具有 Intune/EMS 许可证。 
2. 创建一个要从 Intune 订阅集合中排除的集合。 在此示例中，“所有混合用户”集合中包含一个规则以排除“迁移试点”集合中的用户。 User1 是“迁移试点”集合中的一个成员，将从“所有混合用户”集合中排除。 
3. User1 的设备目前在 Azure 门户的 Intune 中进行管理。 
4. 所有其他设备继续通过 Configuration Manager 控制台进行管理。 

## <a name="verify-intune-standalone-functionality"></a>验证 Intune 独立版功能
迁移了一小部分用户后，验证用户设备是否在 Intune 中列出。 转到“设备”边栏选项卡并选择“所有设备”。 

然后验证你的策略、配置文件和应用等是否在用户设备上按预期运行。

## <a name="migrate-additional-users"></a>迁移其他用户
验证 Intune 独立版按预期正常运行后，就可以开始迁移其他用户。 如同创建测试用户集合一样，创建包含要迁移的用户的集合，并从 Intune 订阅关联的集合中排除这些集合。 有关详细信息，请参阅[与 Intune 订阅关联的集合](#collection-associated-with-your-intune-subscription)。

## <a name="migrate-devices-without-user-affinity"></a>迁移无用户关联的设备
使用设备注册管理员注册的设备和无[用户关联](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices)的设备不会自动迁移至新的 MDM 机构。 可以在以下方案中，使用 Switch-MdmDeviceAuthority PowerShell cmdlet 来切换 Intune 和 Configuration Manager 管理机构： 

-   方案 1：使用 Switch-MdmDeviceAuthority cmdlet 迁移所选的设备并验证是否可以在 Azure 中使用 Intune 来管理它们。 然后，准备就绪后，可以[将租户的 MDM 机构更改为 Intune](migrate-change-mdm-authority.md) 以完成设备迁移。 
-   方案 2：当准备好将租户的 MDM 机构更改为 Intune 时，你可以执行以下操作来迁移无用户关联的设备：
    - 使用 cmdlet 来更改无用户关联的设备的 MDM 机构，然后[将租户的 MDM 机构更改为 Intune](migrate-change-mdm-authority.md)。    
    - 将租户的 MDM 机构更改为 Intune 后，致电支持部门来切换无用户关联的设备。

若要切换这些 MDM 设备的管理机构，可以使用 Switch-MdmDeviceAuthority cmdlet 来切换 Intune 和 Configuration Manager 管理机构。 

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet Switch-MdmDeviceAuthority

#### <a name="synopsis"></a>简述
该 cmdlet 可切换无用户关联的 MDM 设备（例如，批量注册的设备）的管理机构。 在你运行 cmdlet 时，cmdlet 将为基于管理机构的指定设备切换 Intune 和 Configuration Manager 管理机构。

### <a name="syntax"></a>语法
`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>参数
``` powershell
-Credential <PSCredential>
Credential for Intune Tenant Admin or Service Admin account to use when switching device management authorities. The user is prompted for credentials if the parameter is not specified.

-DeviceIds <Guid[]>
The ids of the MDM devices that need to have their management authority switched. The device ids are unique identifiers for the devices displayed by the Configuration Manager console.

-Force [<SwitchParameter>]
Specify parameter to disable the Should Continue prompt.<br>
 
-LogFilePath <string>
Path to log file location.
 
-LoggingLevel <SourceLevels>
The log level used to determine the type of logs that need to be written to the log file.
 
The following are the possible values for LoggingLevel:

  - ActivityTracing
  - All
  - Critical
  - Error
  - Information
  - Off
  - Verbose
  - Warning
 
-Confirm [<SwitchParameter>]
Prompts you for confirmation before executing the command.
 
-WhatIf [<SwitchParameter>]
Describes what would happen if you executed the command without actually executing the command.
 
<CommonParameters>
This cmdlet supports the common parameters: Verbose, Debug,
ErrorAction, ErrorVariable, WarningAction, WarningVariable,
OutBuffer, PipelineVariable, and OutVariable. For more information, see
[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).
```

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
``` powershell
To see the examples, type: "get-help Switch-MdmDeviceAuthority -examples".
For more information, type: "get-help Switch-MdmDeviceAuthority -detailed".
For technical information, type: "get-help Switch-MdmDeviceAuthority -full".
For online help, type: "get-help Switch-MdmDeviceAuthority -online".
```

## <a name="next-steps"></a>后续步骤
迁移了用户并测试过 Intune 功能后，请考虑是否已准备好为 Intune 租户[更改 MDM 机构](migrate-change-mdm-authority.md)，从 Configuration Manager 更改为 Intune。 