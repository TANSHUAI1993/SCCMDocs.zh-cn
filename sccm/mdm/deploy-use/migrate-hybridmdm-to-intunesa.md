---
title: "将混合 MDM 用户及其设备迁移至 Intune 独立版"
titleSuffix: Configuration Manager
description: "了解如何在 Azure 上将混合 MDM 用户及其设备迁移至 Intune。"
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: a6e430248fdeedd310087c9a32c6d69ca1864a09
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
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

<!--
The following provides a typical workflow for migrating users from hybrid MDM to Intune standalone:
1.  Admin runs the Microsoft Intune Data Importer Tool, selecting which objects and assignments to import. Selected objects are imported into Intune standalone.
    1. Some objects cannot be imported because they contain settings the tool does not understand or setting that are not available in Intune standalone.
    2. Assignments are migrated. However, only if the collection an object was targeted to is based on a single Active Directory (AD) security group and the same group exists in Azure Active Directory (AAD).
    > [!Note]    
    > If you want, you can skip this step and create the objects that you want directly in Intune in the Azure portal without running the Intune Data Importer Tool. 
2.  Admin logs into the Intune on Azure portal
    1. Creates any additional objects required for their organization that were not imported by the Microsoft Intune Data Importer tool.
    2. Creates any required AAD groups and makes any additional assignments for each object to AAD groups.
    3. Installs the NDES connector on an on-premises server if using SCEP or PFX certificate deployment.
    4. Installs the Exchange connector on an on-premises server if using conditional access. 
3.  Admin ensures that all existing Intune users in their organization have an Intune license assigned to them using AAD or the Office administrator portal.
4.  Admin selects some test users to migrate to Intune standalone and removes them from the collection associated with the Intune subscription in Configuration Manager.
5.  Once removed from the collection, the user and all devices are managed by Intune in the Azure portal. Remaining users and devices continue to be managed by hybrid mobile device management in Configuration Manager. 
6.  Admin validates that things are working as expected on the device and moves more users to Intune standalone by removing them from the collection associated with the Intune subscription in Configuration Manager.
7.  Once the admin is comfortable with the functionality in Intune standalone, they can move the rest of their users and devices by switching their MDM authority to Intune standalone. This can be done by removing the Intune subscription from SCCM and choosing to change the MDM authority. Tenant level policies will be automatically migrated to Intune standalone, all objects and assignments in Intune standalone will remain, and devices will not be required to re-enroll.
-->