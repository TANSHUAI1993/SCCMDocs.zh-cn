---
title: "更改 MDM 机构"
titleSuffix: Configuration Manager
description: "了解如何将 MDM 机构从 Configuration Manager（混合）更改为 Intune 独立版"
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/17/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: c61a44cce443a7ff210a626d114068691541aaae
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="change-your-mdm-authority"></a>更改 MDM 机构
从 Configuration Manager 1610 版本开始，可以更改 MDM 机构而无需联系 Microsoft 支持部门，也无需取消注册并重新注册现有的受管理设备。 本文提供将从 Configuration Manager 控制台（混合）配置的现有 Microsoft Intune 租户更改为由 Intune 独立版管理的步骤。 完成本文中的步骤后，设备将由 [Azure 门户](https://portal.azure.com)中的 Microsoft Intune 管理。 

> [!Note]    
> 如果要更改现有的 Microsoft Intune 租户，同时将 MDM 机构设置为 Intune、Configuration Manager（混合），请参阅[更改 MDM 机构](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority)。

> [!Important]    
> 本文将介绍当以前尚未迁移用户时更改 MDM 机构。 若要在[迁移用户子集](migrate-hybridmdm-to-intunesa.md)后更改 MDM 机构，请参阅[更改 MDM 机构](migrate-change-mdm-authority.md)。

## <a name="key-considerations"></a>重要注意事项
在更改为新的 MDM 机构之后，在设备签入并与服务同步之前，可能会有一定的过渡时间（最长八小时）。 必须在新的 MDM 机构 (Intune Standalone) 中配置设置，以确保注册的设备在更改后能够继续得到管理和保护。 请注意以下事项：
- 设备必须在更改后与服务连接，以便来自新 MDM 机构（Intune 独立版）的设置可替换设备上的现有设置。
- 更改 MDM 机构后，来自先前 MDM 机构（混合）的一些基本设置（如配置文件）将在设备上最长保留七天。 建议尽快在新的 MDM 机构中配置应用和设置（策略、配置文件、应用等）。 此外，向包含具有现有已注册设备的用户的用户组部署设置。 当设备在更改 MDM 机构后连接到服务时，它将从新的 MDM 机构接收新设置。 任何新设定的策略都将覆盖设备上的现有策略。
- 更改为新的 MDM 机构后，[Azure 门户](https://portal.azure.com)中的符合性数据可能需要长达一周的时间才能准确报告。 但是，Azure Active Directory 和设备上的符合性状态是准确的，因此，设备仍将受到保护。
- 不会将没有关联用户的设备（通常在具有 iOS 设备注册计划或批处理注册方案时）迁移到新的 MDM 机构。 对于这些设备，需要调用支持以获取将它们移动到新 MDM 机构的帮助。

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>准备将 MDM 机构更改为 Intune (Standalone)
检查以下信息，准备对 MDM 机构的更改：
- 你必须具有 Configuration Manager 版本 1610 或更高版本才能将 MDM 机构更改为可用。
- 更改为新的 MDM 机构后，设备最多可能需要八小时才能连接到服务。
- 在更改 MDM 机构之前，确保当前通过混合方式管理的所有用户都具有分配给他们的 Intune/EMS 许可证。 具有许可证将确保用户及其设备在更改 MDM 机构后由 Intune (Standalone) 托管。 有关详细信息，请参阅[将 Intune 许可证分配给用户帐户](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)。
- 确保管理员用户帐户已分配 Intune/EMS 许可证，并确认管理员用户帐户在对 MDM 机构进行更改之前可以登录 Intune。 在更改 MDM 机构之前，MDM 机构应在 [Azure 门户](https://portal.azure.com)中的 Intune 中显示“设置为 Configuration Manager”（混合租户）。
- 更改 MDM 机构期间应不会对最终用户产生明显影响。 

## <a name="change-the-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune (Standalone)
将 MDM 机构更改为 Intune (Standalone) 的过程包括以下高级步骤：  
- 在 Configuration Manager 控制台中，使用“将 MDM 机构更改为 Microsoft Intune”选项来删除现有的 Microsoft Intune 订阅。
- 在 [Azure 门户](https://portal.azure.com)的 Intune 中，从新的 MDM 机构 (Intune) 中配置和部署新的设置和应用。
- 下一次设备连接到服务时，它将同步并从新的 MDM 机构接收新的设置。

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>将 MDM 机构更改为 Intune (Standalone) 的具体步骤
1. 在 Configuration Manager 控制台中，转到“管理”&gt;“概述”&gt;“云服务”&gt;“Microsoft Intune订阅”，然后删除现有的 Intune 订阅。
2. 选择“将 MDM 机构更改为 Microsoft Intune”，然后单击“下一步”。
   ![下载 APN 证书请求](./media/mdm-change-delete-subscription.png)
3. 登录到在 Configuration Manager 中设置 MDM 机构时最初使用的 Intune 租户。
4. 单击“下一步”  并完成向导。
5. MDM 机构现在设置为“Microsoft Intune”。 Intune 订阅在 Configuration Manager 控制台的 Microsoft Intune 订阅节点中不再显示。 
6. 要验证 MDM 机构是否设置，请执行以下步骤：a. 通过之前使用的同一 Intune 租户登录到 [Azure 门户](https://portal.azure.com)。 
    b. 依次选择“更多服务” > “监视 + 管理” > “Intune” > “设备注册”。 MDM 机构显示在“概述”边栏选项卡的右上角部分。 

## <a name="next-steps"></a>后续步骤
更改 MDM 机构完成后，请复查以下步骤：
- 当 Intune 服务检测到租户的 MDM 机构已更改时，它将向所有已注册的设备发送通知消息，以便签入并与服务同步（这并非计划的定期签入）。 因此，租户的 MDM 机构从混合环境更改为 Intune (Standalone) 后，开机且联机的所有设备将与服务连接，接收新的 MDM 机构，并且以后由 Intune（独立）版托管。 这些设备的管理和保护不会中断。
- 更改 MDM 机构过程中（或在不久之后），关闭或脱机的设备将在它们开机且联机时在新的 MDM 机构中连接到服务并与其同步。  
- 用户可以通过手动启动从设备到服务的签入来快速更改为新的 MDM 机构。 用户可以通过使用公司门户应用轻松执行此操作，并启动设备符合性检查。
- 更改 MDM 机构后，要验证设备签入并与服务同步后一切工作是否正常运行，可在 [Azure 门户](https://portal.azure.com)中查找设备。 之前由 Configuration Manager（混合）托管的设备现在将显示为由 Intune 托管的设备。    
- 在更改 MDM 机构期间设备处于脱机状态时，以及设备签入服务，会存在一个过渡期。 为帮助确保设备在此过渡期间仍然受到保护并可正常运行，以下内容将在设备上最多保留七天（或直到设备与新的 MDM 机构连接并接收将覆盖现有设置的新设置为止）：
    - 电子邮件配置文件
    - VPN 配置文件
    - 证书配置文件
    - Wi-Fi 配置文件
    - 配置文件
- 确保用于覆盖现有设置的新设置与以前的设置具有相同的名称，以确保覆盖旧设置。 否则，设备可能会出现冗余配置文件和策略。    

  > [!TIP]   
  > 作为最佳做法，你应该在 MDM 机构更改完成后立即创建所有管理设置和配置以及部署。 这将有助于确保在过渡期间对设备进行保护和主动管理。   
-  更改 MDM 机构后，请执行以下步骤来验证新设备是否成功注册到新的机构：   
    - 注册新设备
    - 确保新注册的设备显示在 [Azure 门户](https://portal.azure.com)中。
    - 执行一个从 [Azure 门户](https://portal.azure.com)到设备的操作，如远程锁定。 如果成功，则表示该设备将由新的 MDM 机构管理。
- 如果你对特定设备有疑问，则可以取消注册然后重新注册设备，以使其连接到新的机构并尽快接受管理。