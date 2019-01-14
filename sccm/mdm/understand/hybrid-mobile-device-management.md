---
title: 使用 Microsoft Intune 的混合 MDM
titleSuffix: Configuration Manager
description: 了解使用 Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)。
ms.date: 11/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a84dfc33fe79f5eb4d5397505a12052b8e92aebf
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250606"
---
# <a name="hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>使用 Configuration Manager 和 Microsoft Intune 的混合 MDM

适用范围：System Center Configuration Manager (Current Branch)

> [!Important]  
> 自 2018 年 8 月 14 日起，混合移动设备管理[功能停用](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。
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
> - 许可将保持不变。 混合 MDM 中随附 Azure 上的 Intune 许可证。  
> 
> - Configuration Manager 中的条件访问和本地 MDM 功能并未弃用。 即将对 Configuration Manager 进行的更改将允许这些功能在没有混合 MDM 的情况下运行。 
> 
> - 2019 年 9 月 1 日，任何剩余的混合 MDM 设备将不再接收策略、应用或安全更新。  
> 
> **我需要如何准备应对此项变化？**
> 
> - 开始为 MDM 规划从 ConfigMgr 控制台迁移到 Azure。 包括 Microsoft IT 在内的许多客户都执行了这一迁移过程。 有关详细信息，请参阅 [Microsoft 案例研究](https://aka.ms/Intune_MSFT)。  
> 
> - 请查看以下工具和文档，简化从混合 MDM 迁移到 Azure 上的 Intune 的过程：  
>     - [将 Configuration Manager 数据导入 Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data)  
>     - [将混合 MDM 用户及其设备迁移至 Intune 独立版](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  
> 
> - 请联系你的名义伙伴或 FastTrack 以获取帮助。 [适用于 Microsoft 365 的 FastTrack](https://aka.ms/hybrid_fasttrack) 可以帮助你从混合 MDM 迁移到 Azure 上的 Intune。 
> 
> 有关详细信息，请参阅 [Intune 支持博客文章](https://aka.ms/hybrid_notification)。



借助 Configuration Manager 的混合移动设备管理 (MDM) 功能，可以管理 iOS、Windows 和 Android 设备。 可通过 Configuration Manager 控制台处理所有管理任务，还可处理通过 Internet 与 Microsoft Intune 联机服务无缝集成的其余管理任务。 借助 Configuration Manager，用户可以通过安全的托管方式访问其设备上的公司资源。 通过使用设备管理，你可以保护公司数据，同时允许用户注册其个人设备或公司拥有的设备，以访问公司数据。 

本文假定你使用 Configuration Manager 来管理计算机。 还假定你有兴趣使用 Intune 扩展 Configuration Manager 控制台以管理移动设备。 



## <a name="capabilities"></a>功能

混合 MDM 支持设备上的以下管理功能：

-   停用和擦除设备  

-   配置密码、安全性、漫游、加密和无线通信等符合性设置  

-   将业务线 (LOB) 应用部署到设备  

-   将应用部署到连接到 Windows 应用商店、Windows Phone 应用商店、应用商店或 Google Play 的设备  

-   收集硬件清单  

-   使用内置报表收集软件清单  

若要阅读有关哪些新功能可用于混合 MDM 的信息，请参阅[混合移动设备管理中的新增功能](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management)。



## <a name="hybrid-mdm-enrollment"></a>混合 MDM 注册

若要对设备进行混合管理，设备必须向该服务注册。 设备的注册方式取决于设备类型、所有权和所需的管理级别。

- **"自带设备办公"(BYOD)**:用户注册其个人电话、 平板电脑  

- **企业拥有的设备 (COD)**:启用管理方案，如远程擦除、 共享的设备或设备的用户关联  

- 如果使用本地或在云中托管的 [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager)，则无需注册即可启用简单的 Intune 管理。 还可使用 [Intune 客户端软件](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune)管理 Windows 电脑。
