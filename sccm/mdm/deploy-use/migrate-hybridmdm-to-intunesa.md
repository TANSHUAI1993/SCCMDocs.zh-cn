---
title: 将混合 MDM 资源迁移至 Intune 独立版
titleSuffix: Configuration Manager
description: 了解如何在 Azure 上将混合 MDM 用户及其设备迁移至 Intune。
author: aczechowski
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: cff1a695f3f3227f7ec849b34b75762b082c3f31
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584554"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>将混合 MDM 用户及其设备迁移至 Intune 独立版

*适用范围：System Center Configuration Manager (Current Branch)*    

本文将介绍在 Azure 上使用 Intune 从混合 MDM 迁移到云（仅限云）的体验。 

> [!Important]  
> 自 2018 年 8 月 14 日起，混合移动设备管理[功能停用](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。 有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<!--Intune feature 2683117-->  


使用分阶段方法开始迁移至 Intune 独立版。 使用此方法时，将测试一小部分用户和设备，而大部分用户和设备仍通过混合 MDM 进行托管。 在验证 Intune 功能后，开始将更多资源迁移至 Intune。    

有关详细信息，请参阅下列文章：    
  
1.  [将 Configuration Manager 数据导入 Microsoft Intune](migrate-import-data.md)   

    Intune 数据导入工具：  

    - 收集有关从 Configuration Manager 层次结构选择的对象的数据  

    - 提供有关可选择导入的对象的详细信息   

    - 说明某些对象无法导入的原因  

    - 可以将选定对象导入 Microsoft Intune 租户  

    此步骤是可选的。 它可以自动执行在 Configuration Manager 和 Intune 间重新创建对象的过程，从而节省时间。  

2.  [准备 Intune 以便进行用户迁移](migrate-prepare-intune.md)    

    - 从 Configuration Manager 验证导入的对象  

    - 创建新对象  

    - 创建 Azure AD 组并将对象分配给这些组  

    - 安装 NDES 和 Exchange 连接器  

    完成这些步骤并开始迁移至 Intune 独立版时，这对你的用户应该是透明的。   

3.  [更改特定用户的 MDM 机构（混合 MDM 机构）](migrate-mixed-authority.md)    

    在同一租户中配置混合 MDM 机构。 选择要在 Intune 中托管的用户，同时继续使用混合 MDM 管理所有其他设备。 开始迁移其他用户之前，先以小部分用户测试 Intune 功能在设备上是否正常运行。   

4.  [将 MDM 机构更改为 Intune 独立版](change-mdm-authority.md)     

    将租户级 MDM 机构从 Configuration Manager 更改为 Intune。 所有剩余用户和设备被迁移至 Intune 独立版。 如果在上述步骤完成了 Intune 功能的全面测试，并且已迁移大部分或全部用户，那么可更改租户级 MDM 机构。



## <a name="request-assistance"></a>请求协助
<!--Intune bug 2339232--> 若要从 Microsoft FastTrack 计划请求协助，首先转到[适用于 Microsoft 365 的 FastTrack](https://fasttrack.microsoft.com/microsoft365/capabilities?view=security)。

1. 单击“登录”，然后输入组织 ID。  

2. 转到仪表板，并按照提示来访问“请求协助”窗体。    

3. Microsoft 将审核请求，并将其路由到相应的团队，以满足你的特定需求和资格。  

在此仪表板中，还可以通过 FastTrack 专家找到最佳做法、工具和资源，以帮助你在使用 Microsoft 云方面打造绝佳体验。

