---
title: 使用 Microsoft Intune 的混合 MDM
titleSuffix: Configuration Manager
description: 了解使用 Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)。
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f6c25817973dcfacefe8aae31f0db02dcbd5807
ms.sourcegitcommit: 160bcdaf783f3946ad5c7869b2566cbfc4da545c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401519"
---
# <a name="hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>使用 Configuration Manager 和 Microsoft Intune 的混合 MDM

适用范围：System Center Configuration Manager (Current Branch)

> [!WARNING]
> 从2019年9月1日起，混合 MDM 服务产品/服务已停用。 任何剩余的混合 MDM 设备都不会接收策略、应用或安全更新。

## <a name="remove-hybrid-mdm"></a>删除混合 MDM

如果 Configuration Manager 站点有 Microsoft Intune 订阅，则需要将其删除。

1. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“云服务”，然后选择“Microsoft Intune 订阅”节点。 删除现有的 Intune 订阅。

1. 在 "**删除 Microsoft Intune 订阅" 向导**中，选择 "**从 Configuration Manager 中删除 Microsoft Intune 订阅**" 选项，然后单击 "**下一步**"。

1. 完成向导。

## <a name="deprecation-announcement"></a>弃用公告

下面是原始弃用公告：

> [!Important]  
> 自 2018 年 8 月 14 日起，混合移动设备管理[功能停用](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。 自 1902 Intune 服务版本起，预计在 2019 年 2 月底，新客户便无法新建混合连接。
> <!--Intune feature 2683117-->  
> 自从一年多前在 Azure 上推出以来，Intune 已经增加了数百个客户要求和市场领先的新服务功能。 Intune 现在提供的功能远远超过了混合移动设备管理 (MDM)。 Azure 上的 Intune 为你的企业移动需求提供了更深入集成的简化管理体验。
>
> 因此，大多数客户选择 Azure 上的 Intune 而不是混合 MDM。 随着越来越多的客户迁移到云，使用混合 MDM 的客户数量持续减少。 因此，Microsoft 将在 2019 年 9 月 1 日停用混合 MDM 服务产品。 请计划[迁移到 Azure 上的 Intune](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) 以满足你的 MDM 需求。
>
> 此更改不会影响本地 Configuration Manager 或[适用于 Windows 10 设备的共同管理](/sccm/comanage/overview)。 如果你不确定自己是否在使用混合 MDM，请转到 Configuration Manager 控制台中的“管理”工作区，展开“云服务”，然后单击“Microsoft Intune 订阅。 如果设置了 Microsoft Intune 订阅，那么你的租户已针对混合 MDM 进行了配置。
>
> **这会对我产生哪些影响？**
>
> - Microsoft 将在明年支持使用混合 MDM。 该功能将继续接收主要 bug 修复。 Microsoft 将支持新版本操作系统上的现有功能，例如在 iOS 12 上注册。 将不再为混合 MDM 提供新功能。  
>
> - 如果在混合 MDM 产品/服务结束之前迁移到 Azure 上的 Intune，则不会对最终用户产生任何影响。  
>
> - 2019 年 9 月 1 日，任何剩余的混合 MDM 设备将不再接收策略、应用或安全更新。  
>
> - 许可将保持不变。 混合 MDM 中随附 Azure 上的 Intune 许可证。  
>
> - Configuration Manager 中的本地 MDM 功能不会弃用。 从 Configuration Manager 版本1810开始，你可以在不使用 Intune 连接的情况下使用本地 MDM。 有关详细信息，请参阅[新的本地 MDM 部署不再需要 Intune 连接](/sccm/core/plan-design/changes/whats-new-in-version-1810#bkmk_opmdm)。
>
> - 混合 MDM 还弃用了 Configuration Manager 的本地条件访问功能。 如果对使用 Configuration Manager 客户端管理的设备使用条件访问，请在迁移之前确保它们受到保护。
>     1. 在 Azure 中设置条件性访问策略
>     2. 在 Intune 门户中设置合规性策略
>     3. 完成混合迁移，并将 MDM 机构设置为 Intune
>     4. 启用共同管理
>     5. 将合规性策略共同管理工作负荷转移到 Intune
>
>     有关详细信息, 请参阅[使用共同管理的条件性访问](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access)。
>
> **我需要如何准备应对此项变化？**
>
> - 开始为 MDM 规划从 ConfigMgr 控制台迁移到 Azure。 包括 Microsoft IT 在内的许多客户都执行了这一迁移过程。 有关详细信息，请参阅 [Microsoft 案例研究](https://aka.ms/Intune_MSFT)。  
>
> - 请查看以下工具和文档，简化从混合 MDM 迁移到 Azure 上的 Intune 的过程：  
>   - [将 Configuration Manager 数据导入 Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data)  
>   - [将混合 MDM 用户及其设备迁移至 Intune 独立版](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  
>
> - 请联系你的名义伙伴或 FastTrack 以获取帮助。 [适用于 Microsoft 365 的 FastTrack](https://aka.ms/hybrid_fasttrack) 可以帮助你从混合 MDM 迁移到 Azure 上的 Intune。
>
> 有关详细信息，请参阅 [Intune 支持博客文章](https://aka.ms/hybrid_notification)。

<!--

With the hybrid mobile device management (MDM) feature of Configuration Manager, manage iOS, Windows, and Android devices. All management tasks are handled from the Configuration Manager console where you perform the rest of your management tasks seamlessly integrated with Microsoft Intune's online service over the internet. Use Configuration Manager to let users access company resources on their devices in a secure, managed way. By using device management, you protect company data while letting users enroll their personal or company-owned devices to access company data. 

This article assumes that you use Configuration Manager to manage computers. It also assumes that you're interested in extending the Configuration Manager console with Intune to manage mobile devices. 



## Capabilities

Hybrid MDM supports the following management capabilities on devices:

-   Retire and wipe devices  

-   Configure compliance settings such as passwords, security, roaming, encryption, and wireless communication  

-   Deploy line-of-business (LOB) apps to devices  

-   Deploy apps to devices that connect to Windows Store, Windows Phone Store, App Store, or Google Play  

-   Collect hardware inventory  

-   Collect software inventory by using built-in reports  



## Hybrid MDM enrollment

To bring devices into hybrid management, those devices must be enrolled with the service. How devices enroll devices depends on the device type, ownership, and the level of management needed.

- **"Bring your own device" (BYOD)**: Users enroll their personal phones, tablets, or PCs  

- **Corporate-owned device (COD)**: Enable management scenarios like remote wipe, shared devices, or user affinity for a device  

- If you use [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager), either on-premises or hosted in the cloud, you can enable simple Intune management without enrollment. Windows PCs can also be managed using [Intune client software](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).

-->

## <a name="next-steps"></a>后续步骤

有关支持的管理 MDM 设备功能的详细信息，请参阅以下文章：

- [什么是 Microsoft Intune？](https://docs.microsoft.com/intune/what-is-intune)
- [什么是本地 MDM？](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure)
- [使用 Exchange 管理设备](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)
