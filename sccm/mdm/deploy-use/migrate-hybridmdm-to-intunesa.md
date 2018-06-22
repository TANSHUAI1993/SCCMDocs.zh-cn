---
title: 将混合 MDM 用户及其设备迁移至 Intune 独立版
titleSuffix: Configuration Manager
description: 了解如何在 Azure 上将混合 MDM 用户及其设备迁移至 Intune。
author: aczechowski
manager: dougeby
ms.date: 09/12/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: 4e2471b06c1767bcf914000d626bb22b6ee2bd6b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346315"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>将混合 MDM 用户及其设备迁移至 Intune 独立版

*适用范围：System Center Configuration Manager (Current Branch)*    

如果确定已准备好通过在 Azure 上使用 Intune 开始从混合 MDM（Intune 与 Configuration Manager 集成）迁移至仅使用云的体验，这篇文章能对你提供帮助。 如果尚未确定，请参阅[在 Microsoft Intune 独立版与使用 System Center Configuration Manager 实现的混合移动设备管理之间做出选择](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)。 

开始迁移至 Intune 独立版时可以使用分阶段的方法，也就是先以一小部分用户和设备进行测试，同时大部分用户和设备依然在混合 MDM 中管理。 接下来，在验证好 Intune 功能后，就可以开始迁移更多用户至 Intune。    

以下主题介绍将用户迁移至 Intune 独立版的分阶段步骤。    
  
1.  [将 Configuration Manager 数据导入 Microsoft Intune](migrate-import-data.md)   
    Intune 数据导入程序工具收集从 Configuration Manager 层次结构选择的对象的相关数据，并提供可以选为导入对象的对象详细信息以及某个对象无法被导入的相关信息，并让你将选定对象导入 Microsoft Intune 租户。 尽管此步骤是可选的，但它可以自动执行在 Configuration Manager 和 Intune 间重新创建对象的过程，从而节省很多时间。 
2.  [准备 Intune 以进行用户迁移](migrate-prepare-intune.md)    
    从 Configuration Manager 中验证导入的对象，创建新对象，创建 AAD 组并为这些组进行对象分配，安装 NDES 和 Exchange 连接器，等等。完成这些步骤并开始迁移至 Intune 独立版时，这对你的用户应该是透明的。  
3.  [更改特定用户的 MDM 机构（混合 MDM 机构）](migrate-mixed-authority.md)    
    若要在同一租户中配置混合 MDM 机构，可以选择部分用户在 Intune 中管理，而所有其他设备继续由混合 MDM 管理（Intune 与 Configuration Manager 集成）。 开始迁移其他用户之前，可以先以小部分用户测试 Intune 功能在设备上是否按预期运行。 
4.  [将 MDM 机构更改为 Intune 独立版](change-mdm-authority.md)     
    将租户级 MDM 机构从 Configuration Manager 更改为 Intune。 所有剩余用户和设备被迁移至 Intune 独立版。 如果在上述步骤完成了 Intune 功能的全面测试，并且已迁移大部分或全部用户，那么租户级 MDM 机构将会变更。