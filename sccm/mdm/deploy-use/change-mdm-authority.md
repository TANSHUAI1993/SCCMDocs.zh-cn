---
title: 更改 MDM 机构
titleSuffix: Configuration Manager
description: 了解如何将 MDM 机构从 Configuration Manager（混合）更改为 Intune 独立版
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: 692ffb04546da4f65b2198e582999582c996fdb2
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584512"
---
# <a name="change-your-mdm-authority"></a>更改 MDM 机构

*适用范围：System Center Configuration Manager (Current Branch)*

你可以更改 MDM 颁发机构，而无需联系 Microsoft 支持部门，并且无需取消注册并重新注册现有的受管理设备。 本文提供将从 Configuration Manager 控制台（混合）配置的现有 Microsoft Intune 租户更改为由 Intune 独立版管理的步骤。 完成本文中的步骤后，设备将由 [Azure 门户](https://portal.azure.com)中的 Microsoft Intune 管理。 

本文将介绍在以前尚未迁移用户时更改 MDM 机构。 若要在[迁移用户子集](migrate-hybridmdm-to-intunesa.md)后更改 MDM 机构，请参阅[更改 MDM 机构](migrate-change-mdm-authority.md)。

> [!Important]  
> 自 2018 年 8 月 13 日起，混合移动设备管理[功能停用](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。 有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<!--Intune feature 2683117-->  



## <a name="key-considerations"></a>重要注意事项

更改 MDM 机构后，转换时间最长为八小时。 在设备签入并与服务器同步之前可能需要等待这么一段时间。 若要确保注册的设备在更改后能够继续受到管理和保护，可在 Intune 中直接配置设置。 请注意以下事项：

- 设备必须在更改后与服务连接，以便来自新 MDM 机构（Intune 独立版）的设置可替换设备上的现有设置。  

- 更改 MDM 机构后，来自先前 MDM 机构（混合）的一些基本设置（如配置文件）将在设备上最长保留七天。 建议尽快在新的 MDM 机构中配置应用和设置（策略、配置文件、应用等）。 此外，向包含具有现有已注册设备的用户的用户组部署设置。 当设备在更改 MDM 机构后连接到服务时，它将从新的 MDM 机构接收新设置。 任何新设定的策略都将覆盖设备上的现有策略。  

- 更改为新的 MDM 机构后，[Azure 门户](https://portal.azure.com)中的符合性数据可能需要长达一周的时间才能准确报告。 但是，Azure Active Directory 和设备上的符合性状态是准确的。 设备仍会受到保护。  

- 没有关联用户的设备不会迁移到新的 MDM 机构。 在 iOS 设备注册计划或批量注册方案中，此行为非常典型。 对于这些设备，请联系支持部门获取帮助以将它们移动到新 MDM 机构。  



## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>准备将 MDM 机构更改为 Intune (Standalone)

检查以下信息，准备对 MDM 机构的更改：

- 更改为新的 MDM 机构后，设备最多可能需要八小时才能连接到服务。  

- 在更改 MDM 机构之前，确保当前通过混合方式管理的所有用户都具有分配给他们的 Intune/EMS 许可证。 此许可证将确保用户及其设备在更改 MDM 机构后由 Intune 独立版托管。 有关详细信息，请参阅[将 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)。  

- 请确保向管理员用户帐户分配了 Intune/EMS 许可证。 在更改 MDM 机构之前，请确认管理员用户帐户可以登录 Intune。 在更改 MDM 机构之前，MDM 机构应在 [Azure 门户](https://portal.azure.com)中的 Intune 中显示“设置为 Configuration Manager”（混合租户）。  

- 更改 MDM 机构期间应不会对最终用户产生明显影响。 



## <a name="change-the-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune (Standalone)

将 MDM 机构更改为 Intune (Standalone) 的过程包括以下高级步骤：  

- 在 Configuration Manager 控制台中，使用“将 MDM 机构更改为 Microsoft Intune”选项来删除现有的 Microsoft Intune 订阅。  

- 在 [Azure 门户](https://portal.azure.com)的 Intune 中，从新的 MDM 机构 (Intune) 中配置和部署新的设置和应用。  

- 下一次设备连接到服务时，它将同步并从新的 MDM 机构接收新的设置。  

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune (Standalone) 的具体步骤
1. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“云服务”，然后选择“Microsoft Intune 订阅”节点。 删除现有的 Intune 订阅。  

2. 选择“将 MDM 机构更改为 Microsoft Intune”，然后单击“下一步”。  

   ![删除 Microsoft Intune 订阅向导，说明页面](./media/mdm-change-delete-subscription.png)

3. 登录到在 Configuration Manager 中设置 MDM 机构时最初使用的 Intune 租户。  

4. 单击“下一步”并完成向导。  

5. MDM 机构现在设置为“Microsoft Intune”。 Configuration Manager 控制台的 Microsoft Intune 订阅节点中不显示 Intune 订阅。  

6. 要验证 MDM 机构是否设置，请执行以下步骤：  

    1. 通过之前使用的同一 Intune 租户登录到 [Azure 门户](https://portal.azure.com)。  

    2. 依次选择“所有服务”、 > “Intune”、 > “设备注册”。 MDM 机构显示在“概述”的右上角部分。  



## <a name="next-steps"></a>后续步骤

更改 MDM 机构完成后，请复查以下步骤：  

- 当 Intune 服务检测到租户的 MDM 机构已更改时，它将向所有已注册的设备发送通知消息，以便签入并与服务同步。 定期计划的签入除外。 因此，租户的 MDM 机构从混合环境更改为 Intune 独立版后，开机且联机的所有设备将与服务连接，接收新的 MDM 机构，并由 Intune 独立版托管。 对这些设备的管理和保护不会中断。  

- 更改 MDM 机构过程中（或在不久之后），关闭或脱机的设备将在它们开机且联机时在新的 MDM 机构中连接到服务并与其同步。   

- 用户可以通过手动启动从设备到服务的签入来快速更改为新的 MDM 机构。 用户可以通过使用公司门户应用轻松执行此操作，并启动设备符合性检查。  

- 更改 MDM 机构后，要验证设备签入并与服务同步后一切工作是否正常运行，可在 [Azure 门户](https://portal.azure.com)中查找设备。 之前由 Configuration Manager（混合）托管的设备现在会显示为由 Intune 托管的设备。    

- 在更改 MDM 机构期间设备处于脱机状态时，以及设备签入服务，会存在一个过渡期。 为帮助确保设备在此过渡期间仍然受到保护并可正常运行，以下配置文件将在设备上保留长达七天（或直到设备与新的 MDM 机构连接并接收将覆盖现有设置的新设置为止）：  
    - 电子邮件配置文件
    - VPN 配置文件
    - 证书配置文件
    - Wi-Fi 配置文件
    - 配置文件  

- 若要覆盖旧设置，请确保用于覆盖现有设置的新设置与以前的设置具有相同的名称。 否则，设备可能会出现冗余配置文件和策略。    

  > [!TIP]   
  > 在 MDM 机构更改完成后立即创建所有管理设置和配置以及部署。 此操作可帮助在过渡期间保护和主动管理设备。   

-  更改 MDM 机构后，请执行以下步骤来验证新设备是否成功注册到新的机构：   

    - 注册新设备  

    - 确保新注册的设备显示在 [Azure 门户](https://portal.azure.com)中。  

    - 执行一个从 [Azure 门户](https://portal.azure.com)到设备的操作，如远程锁定。 如果成功，则表示该设备将由新的 MDM 机构管理。  
    
- 如果特定设备存在问题，请取消注册并重新注册这些设备。 此操作会将设备连接至新机构并使其尽快受到管理。  

- 如果已将 [Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client) 启用为混合租户并将租户迁移至 Intune 独立版，受注册限制影响，Android for Work 设置可能会显示为“阻止”而不是“允许”。 请将其手动设置为“允许”以重新启用 Android for Work 注册。<!--512117-->  

- 在更改 MDM 机构后，不会自动删除 Apple VPP 令牌和关联的[批量采购的 iOS 应用](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)。 若要清除此信息，请按照[删除 Apple VPP 令牌](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps#delete-an-apple-vpp-token)中的步骤操作。 操作完成后，该站点将删除令牌。 它还会从“许可应用商店应用”节点那里删除该令牌的任何应用程序元数据。<!--SCCMDocs issue 579-->  

    在极少数情况下，可能会看到站点无法删除管理对象的错误。  

    - 如果令牌不可见，则忽略此错误  

    - 如果令牌仍显示，请重试将其删除  

