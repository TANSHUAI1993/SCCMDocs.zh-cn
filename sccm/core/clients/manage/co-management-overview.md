---
title: "适用于 Windows 10 设备的共同管理"
description: "了解如何使用 Configuration Manager 和 Microsoft Intune 同时管理 Windows 10 设备。"
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 0cc11a05013fd9c25ee98ec35adcbe822d8a21fb
ms.sourcegitcommit: 389c4e5b4e9953b74c13b1689195f99c526fa737
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="co-management-for-windows-10-devices"></a>适用于 Windows 10 设备的共同管理    
<!-- 1350871 -->
许多客户想要使用一种基于云的简单低成本解决方案通过管理移动设备的相同方式来管理 Windows 10 设备。 然而，实现从传统管理到现代管理的转换可能具有挑战性。 在以前的 Windows 10 更新中，已经可以将 Windows 10 设备同时联接到本地 Active Directory (AD) 和基于云的 Azure AD（混合 Azure AD）。 从 Configuration Manager 1710 版本开始，共同管理利用此项改进来使你能够使用 Configuration Manager 和 Intune 来同时管理 Windows 10 设备版本 1709（也称为 Fall Creators Update）。 它是一种解决方案，在传统管理与现代管理之间架起一座桥梁，为你提供利用分阶段的方法实现转换的途径。 

有两个实现共同管理的主要方式。  其中一个是预配了 Configuration Manager 的共同管理，这种情况中，由 Configuration Manager 管理且加入了混合 Azure AD 的 Windows 10 设备注册到 Intune。 另一个是预配了 Intune 的共同管理，设备在 Intune 中注册然后安装有 Configuration Manager 客户端，从而实现共同管理的状态。

## <a name="prerequisites"></a>先决条件
必须具备以下先决条件才能实现共同管理。 有一般先决条件，以及针对安装了 Configuration Manager 客户端的设备和未安装该客户端的设备的不同先决条件。

> [!IMPORTANT]
> Windows 10 移动设备不支持共同管理。

### <a name="general-prerequisites"></a>一般先决条件
以下是实现共同管理的一般先决条件：  

- Configuration Manager 版本 1710 或更高版本
- Azure AD
- 适用于所有用户的 EMS 或 Intune 许可证
- [Azure AD 自动注册](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)已启用
- Intune 订阅（Intune 中的 MDM 机构设置为 Intune）


   > [!Note]  
   > 如果具有混合 MDM 环境（Intune 与 Configuration Manager 集成），则无法实现共同管理。 如果有兴趣迁移到 Intune 独立版本，请参阅[从混合 MDM 迁移到 Intune 独立版本](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)。

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>针对安装了 Configuration Manager 客户端的设备的其他先决条件
- Windows 10 版本 1709（也称为 Fall Creators Update）及更高版本
- [已联接混合 Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)（联接到 AD 和 Azure AD）

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>针对未安装 Configuration Manager 客户端的设备的其他先决条件
- Windows 10 版本 1709（也称为 Fall Creators Update）及更高版本
- Configuration Manager 中的[云管理网关](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway)（当你使用 Intune 安装 Configuration Manager 客户端时）

## <a name="workloads-you-can-switch-to-intune"></a>可以切换到 Intune 的工作负荷
启用共同管理后，Configuration Manager 将继续管理所有工作负荷。 如果决定已准备就绪，即可使 Intune 开始管理可用的工作负荷。 可以使 Intune 管理以下工作负荷。   

### <a name="compliance-policies"></a>相容性策略
符合性策略定义设备必须遵从的规则和设置，以便将设备视为符合条件访问策略。 也可使用符合性策略来监视和修正独立于条件访问的设备符合性问题。 有关详细信息，请参阅[设备符合性策略](/sccm/mdm/deploy-use/device-compliance-policies)。  

### <a name="windows-update-for-business-policies"></a>适用于企业的 Windows 更新策略
通过适用于企业的 Windows 更新策略，可以针对 Windows 10 功能更新或直接由适用于企业的 Windows 更新托管的 Windows 10 设备的质量更新，配置延迟策略。 有关详细信息，请参阅[配置适用于企业的 Windows 更新延迟策略](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)。  

### <a name="resource-access-policies"></a>资源访问策略
资源访问策略在设备上配置 VPN、Wi-Fi、电子邮件以及证书设置。 有关详细信息，请参阅[部署资源访问配置文件](/sccm/protect/deploy-use/deploy-wifi-vpn-email-cert-profiles)。

## <a name="architectural-overview-for-co-management"></a>共同管理体系结构概述
下图提供共同管理的体系结构概述，以及它如何适用于现有的配置和 Intune 基础结构。

![共同管理体系结构关系图](./media/co-management-arch.svg)

## <a name="scenarios-to-enable-co-management"></a>启用共同管理的方案  
可以对在 Microsoft Intune 和现有 Windows 10 Configuration Manager 客户端中注册的 Windows 10 设备启用共同管理。 这两种方案都将导致 Windows 10 设备由 Configuration Manager 和 Intune 同时管理，并联接到 AD 和 Azure AD。  

### <a name="devices-enrolled-in-intune"></a>在 Intune 中注册的设备  
如果在 Intune 中注册 Windows 10 设备，可在设备上安装 Configuration Manager 客户端（使用特定的命令行参数），使客户端准备好进行共同管理。 然后，从 Configuration Manager 控制台中启用共同管理，开始针对特定 Windows 10 设备将特定的工作负荷移动到 Intune。  

对于尚未在 Intune 中注册的 Windows 10 设备，可以在 Azure 中使用自动注册来注册设备。 对于新的 Windows 10 设备，可以使用 [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) 配置全新体验 (OOBE)，其中包括在 Intune 中注册设备的自动注册。  

### <a name="configuration-manager-clients"></a>Configuration Manager 客户端
如果具有属于 Configuration Manager 客户端的 Windows 10 设备，可注册设备并从 Configuration Manager 控制台启用共同管理。 Configuration Manager 根据 Azure AD 租户信息将自动注册触发到 Intune。  


## <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Azure 上 Intune 中适用于共同管理设备的可用远程操作
如果为 Windows 10 设备启用了共同管理，在 Azure 上的 Intune 中可以执行以下远程操作：  
- [恢复出厂设置](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [选择性擦除](https://docs.microsoft.com/intune/apps-selective-wipe)
- [删除设备](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [重启设备](https://docs.microsoft.com/intune/device-restart)
- [全新启动](https://docs.microsoft.com/intune/device-fresh-start)

## <a name="next-steps"></a>后续步骤
[准备 Windows 10 设备进行共同管理](co-management-prepare.md)