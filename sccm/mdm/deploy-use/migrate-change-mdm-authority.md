---
title: 将 MDM 机构更改为 Intune
titleSuffix: Configuration Manager
description: 了解如何将 MDM 机构从 Configuration Manager（混合）更改为 Intune 独立版。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d6a909be4b1817b9a251046d666839e2e351443
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62282161"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune 独立版

适用范围：System Center Configuration Manager (Current Branch)    

可以将从 Configuration Manager 控制台（混合 MDM）配置的现有 Microsoft Intune 租户更改为 Intune 独立版。 将租户级 MDM 机构更改为 Intune 是在仅限云的配置中[将混合 MDM 用户和设备迁移到 Intune 独立版](migrate-hybridmdm-to-intunesa.md)的过程中的最后一步。    

> [!Important]    
> 若要在不首先将混合 MDM 用户迁移到 Intune 的情况下更改 MDM 机构，请参阅[更改 MDM 机构](change-mdm-authority.md)。

此文提供有关如何从 Configuration Manager 控制台 （混合） 配置为 Intune 独立版的现有 Microsoft Intune 租户更改的信息。 它假定你已完成以下步骤：
- 使用 [Intune 数据导入工具](migrate-import-data.md)将 Configuration Manager 对象导入 Intune。 
- [准备适用于用户迁移的 Intune](migrate-prepare-intune.md) 以确保在迁移用户及其设备后仍能继续对其进行管理。
- [为特定用户更改 MDM 机构（混合 MDM 机构）](migrate-mixed-authority.md)以开始从 Azure 门户管理用户设备。


## <a name="users-and-devices-that-havent-been-migrated"></a>尚未迁移的用户和设备
你已经迁移多个用户并测试过 Intune 功能，以确保一切按预期方式。 你已在 Intune 中，配置策略、 配置文件和应用程序并且已全面测试设备上的对象。 在更改 MDM 机构之后，租户级策略应不再需要新的配置。 但是，对于用户和你以前尚未迁移的设备，查看在更改 MDM 机构后出现的情况有关的以下信息：    

- 有很多达八个小时，在设备签入并与服务同步之前转换时间。  

- 设备必须在更改后与服务连接，以便来自新 MDM 机构（Intune 独立版）的设置可替换设备上的现有设置。  

- 来自先前 MDM 机构（混合）的一些基本设置（如配置文件）将在设备上最长保留七天。  

- 没有关联用户的设备不会迁移到新的 MDM 机构。 这些设备通常是与方案适用于 iOS 设备注册计划或批量注册。 对于这些设备，需要调用支持以获取将它们移动到新 MDM 机构的帮助。



## <a name="prerequisites"></a>先决条件
检查以下信息，准备对 MDM 机构的更改：
- 你必须具有 Configuration Manager 版本 1610 或更高版本才能将 MDM 机构更改为可用。
- 请务必将 Intune/EMS 许可证分配给当前由混合 MDM 管理的所有用户 许可证可确保，用户和他们的设备由 Intune 独立版后更改 MDM 机构。 有关详细信息，请参阅[将 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)。
- 请确保向管理员用户帐户分配了 Intune/EMS 许可证。

## <a name="change-the-mdm-authority-to-intune"></a>将 MDM 机构更改为 Intune
使用下面的过程将租户级 MDM 机构更改为 Intune。

1. 在 Configuration Manager 控制台中，转到**Administration**工作区中，展开**云服务**，然后选择**Microsoft Intune 订阅**节点。 删除现有的 Intune 订阅。  

2. 选择**MDM 机构更改为 Microsoft Intune**，然后选择**下一步**。

    ![删除 Microsoft Intune 订阅对话框](media/mdm-change-delete-subscription.png)  

3. 登录到在 Configuration Manager 中设置 MDM 机构时最初使用的 Intune 租户。 选择**下一步**并完成向导。

    MDM 机构现已重置。 Intune 订阅在 Configuration Manager 控制台的 Microsoft Intune 订阅节点中不再显示。  

4. 登录到[Intune 门户](https://aka.ms/IntunePortal)。

5. 选择**设备注册**。  

6. 在设备注册概述中，请参阅**MDM 机构**属性。

   > [!Important]    
   > 不要使用 Intune 经典控制台。 在 Azure 门户中登录到 Intune。  

7. 确认 MDM 机构已被更改为 **Microsoft Intune**。 



## <a name="after-migration"></a>迁移后

更改 MDM 机构完成后，请复查以下信息：

- 更改 MDM 机构期间应不会对最终用户产生明显影响。  

- 您无需重新配置租户级策略。  

- 如果你需要编辑租户级策略，Intune 从 Azure 门户中执行此操作。  

- 如果特定设备存在问题，请取消注册并重新注册这些设备。 此操作将获取其连接到新机构并作为尽可能快地进行管理。


#### <a name="validate-new-device-enrollment"></a>验证新设备注册
更改 MDM 机构后，使用以下步骤来验证新设备成功注册到新机构：   
1. 注册新设备
2. 请确保新注册的设备显示在 Intune 中
3. 启动设备操作在 Intune 门户中，如[远程锁定](https://docs.microsoft.com/intune/device-remote-lock)。 如果成功，由新的 MDM 机构成功管理设备。


#### <a name="for-users-and-devices-that-you-havent-previously-migrated"></a>您以前尚未迁移用户和设备

- 验证设备现在显示在**设备**与托管设备的页面。 它们显示之前，这些设备必须签入并与服务同步后更改 MDM 机构。 

- 当 Intune 服务检测到租户的 MDM 机构已更改时，它将发送到所有已注册设备的通知消息。 它指示要签入并与服务同步的设备。 此通知发生之外定期计划的签入。 更改为 Intune 独立版从混合租户的 MDM 机构后，所有联机设备连接的服务。 它们接收新的 MDM 机构，然后管理由 Intune 独立版从现在起。 不会中断到的管理和保护这些设备。

- 对于期间或在更改 MDM 机构后不久处于脱机状态的设备，它们连接到并在它们开机且联机时同步到新的 MDM 机构该服务。  

- 可以通过手动启动签入的从设备到服务快速更改为新的 MDM 机构。 使用公司门户应用启动设备符合性检查。

- 没有一个过渡期，当设备处于脱机状态在更改 MDM 机构和该设备签入到服务时的过程。 若要确保该设备仍然受保护和功能在此过渡期间，以下配置文件保留在设备上最多七天。 它们还可保持直到设备与新的 MDM 机构连接并接收将覆盖现有的新设置：
    - 电子邮件配置文件
    - VPN 配置文件
    - 证书配置文件
    - Wi-Fi 配置文件
    - 配置文件

- 对于不是与用户关联的设备，请致电支持人员以帮助更改 MDM 机构。 

#### <a name="bkmk-ki-dep"></a> Apple DEP 设备记录
<!--ICM 105091970-->
完成从混合 MDM 迁移后，可能会注意到 Apple DEP 设备记录将保留在 Configuration Manager 控制台。 一旦将 MDM 机构更改为 Intune 后，不能从 Configuration Manager 中删除这些设备。 

有两种解决方法：

- 如果在更改 MDM 机构之前查看此行为，然后 DEP 记录从 Configuration Manager 中删除。  

- 如果已迁移，并且仍在使用配置管理器，然后使用以下 SQL 命令对站点数据库删除记录：  

    ```SQL
    Delete from MDMCorpOwnedDevices where DeviceType=8 and DiscoverySources=4
    ```



## <a name="next-steps"></a>后续步骤

现在，迁移就完成了，管理使用 Intune 移动设备。 有关详细信息，请参阅[什么是 Microsoft Intune 中的新增](https://docs.microsoft.com/intune/whats-new)。

