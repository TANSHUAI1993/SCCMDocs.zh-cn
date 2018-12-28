---
title: 将 MDM 机构更改为 Intune
titleSuffix: Configuration Manager
description: 了解如何将 MDM 机构从 Configuration Manager（混合）更改为 Intune 独立版。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.openlocfilehash: 4ded99c2084f274d519680e78fdc54825b3857cb
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53419506"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune 独立版

*适用于：System Center Configuration Manager (Current Branch)*    

可以将从 Configuration Manager 控制台（混合 MDM）配置的现有 Microsoft Intune 租户更改为 Intune 独立版。 将租户级 MDM 机构更改为 Intune 是在仅限云的配置中[将混合 MDM 用户和设备迁移到 Intune 独立版](migrate-hybridmdm-to-intunesa.md)的过程中的最后一步。    

> [!Important]    
> 若要在不首先将混合 MDM 用户迁移到 Intune 的情况下更改 MDM 机构，请参阅[更改 MDM 机构](change-mdm-authority.md)。

本文提供有关如何将从 Configuration Manager 控制台（混合）配置的现有 Microsoft Intune 租户更改为 Intune 独立版的信息，并假定你已完成以下步骤：
- 使用 [Intune 数据导入工具](migrate-import-data.md)将 Configuration Manager 对象导入 Intune。 
- [准备适用于用户迁移的 Intune](migrate-prepare-intune.md) 以确保在迁移用户及其设备后仍能继续对其进行管理。
- [为特定用户更改 MDM 机构（混合 MDM 机构）](migrate-mixed-authority.md)以开始从 Azure 门户管理用户设备。


## <a name="users-and-devices-that-have-not-been-migrated"></a>尚未迁移的用户和设备
已迁移多个用户和测试过的 Intune 功能，以确保按预期工作。 因此，已在 Intune 中配置了策略、配置文件和应用等，且已全面测试了设备上的对象。 在更改 MDM 机构之后，租户级策略应不再需要新的配置。 但是，对于之前尚未迁移的用户和设备，请在更改 MDM 机构之后查看以下有关后续工作的信息：    
- 在设备签入并与服务同步之前，可能会有一定的过渡时间（最长八小时）。
- 设备必须在更改后与服务连接，以便来自新 MDM 机构（Intune 独立版）的设置可替换设备上的现有设置。
- 来自先前 MDM 机构（混合）的一些基本设置（如配置文件）将在设备上最长保留七天。 
- 不会将没有关联用户的设备（通常在具有 iOS 设备注册计划或批处理注册方案时）迁移到新的 MDM 机构。 对于这些设备，需要调用支持以获取将它们移动到新 MDM 机构的帮助。

## <a name="prerequisites"></a>先决条件
检查以下信息，准备对 MDM 机构的更改：
- 你必须具有 Configuration Manager 版本 1610 或更高版本才能将 MDM 机构更改为可用。
- 在更改 MDM 机构之前，确保当前通过混合 MDM 方式管理的所有用户都具有分配给他们的 Intune/EMS 许可证。 具有许可证将确保用户及其设备在更改 MDM 机构后由 Intune (Standalone) 托管。 有关详细信息，请参阅[将 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)。
- 请确保向管理员用户帐户分配了 Intune/EMS 许可证。

## <a name="change-the-mdm-authority-to-intune"></a>将 MDM 机构更改为 Intune
使用下面的过程将租户级 MDM 机构更改为 Intune。

1. 在 Configuration Manager 控制台中，转到“管理”&gt;“概述”&gt;“云服务”&gt;“Microsoft Intune订阅”，然后删除现有的 Intune 订阅。
2. 选择“将 MDM 机构更改为 Microsoft Intune”，然后单击“下一步”。

   ![删除 Microsoft Intune 订阅对话框](media/mdm-change-delete-subscription.png)
3. 登录到在 Configuration Manager 中设置 MDM 机构时最初使用的 Intune 租户。
4. 单击“下一步”并完成向导。
5. MDM 机构现已重置。 Intune 订阅在 Configuration Manager 控制台的 Microsoft Intune 订阅节点中不再显示。
6. 登录到 [Intune 门户](https://aka.ms/IntunePortal)。
7. 在 Microsoft Intune 边栏选项卡中单击“设备注册”。
8. “设备注册概述”边栏选项卡中会显示“MDM 机构”属性。

   > [!Important]    
   > 请勿使用 Intune 经典控制台。 必须登录到 Azure 门户中的 Intune。
9. 确认 MDM 机构已被更改为 **Microsoft Intune**。 

## <a name="next-steps"></a>后续步骤
更改 MDM 机构完成后，请复查以下信息：
- 更改 MDM 机构期间应不会对最终用户产生明显影响。 
- 无需重新配置租户级策略。 
- 更改 MDM 机构之后，可以从 Azure 门户中的 Intune 编辑租户级策略。
-  更改 MDM 机构后，请执行以下步骤来验证新设备是否成功注册到新的机构：   
    - 注册新设备
    - 确保新注册的设备显示在 Intune 中。
    - 执行一个从管理控制台到设备的操作，如远程锁定。 如果成功，则表示该设备将由新的 MDM 机构管理。
- 如果你对特定设备有疑问，则可以取消注册然后重新注册设备，以使其连接到新的机构并尽快接受管理。
- 对于之前尚未迁移的用户和设备：
    - 验证设备在“设备”边栏选项卡中显示为受管理设备。 在更改 MDM 机构之后，这些设备必须签入并与该服务进行同步，才能显示。 
    - 当 Intune 服务检测到租户的 MDM 机构已更改时，它将向所有已注册的设备发送通知消息，以便签入并与服务同步（并非计划的定期签入）。 因此，租户的 MDM 机构从混合环境更改为 Intune 独立版后，开机且联机的所有设备将与服务连接，接收新的 MDM 机构，并从现在开始由 Intune 独立版托管。 对这些设备的管理和保护不会中断。
    - 更改 MDM 机构过程中（或在不久之后），关闭或脱机的设备将在它们开机且联机时在新的 MDM 机构中连接到服务并与其同步。  
    - 用户可以通过手动启动从设备到服务的签入来快速更改为新的 MDM 机构。 用户可以通过使用公司门户应用轻松进行签入，并启动设备符合性检查。
    - 在更改 MDM 机构期间设备处于脱机状态时，以及设备签入服务，会存在一个过渡期。 为帮助确保设备在此过渡期间仍然受到保护并可正常运行，以下配置文件将在设备上保留长达七天（或直到设备与新的 MDM 机构连接并接收将覆盖现有设置的新设置为止）：
        - 电子邮件配置文件
        - VPN 配置文件
        - 证书配置文件
        - Wi-Fi 配置文件
        - 配置文件
    - 致电支持人员，以帮助更改与用户不关联的设备的 MDM 机构。 
