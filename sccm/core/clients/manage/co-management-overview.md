---
title: 适用于 Windows 10 设备的共同管理
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 和 Microsoft Intune 同时管理 Windows 10 设备。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: a99983583aa8c21f8a987f3e20550752e7b77ba4
ms.sourcegitcommit: 83806460b6fd88a1d08a2c97f4d72b9e36e04102
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2018
ms.locfileid: "39495554"
---
# <a name="co-management-for-windows-10-devices"></a>适用于 Windows 10 设备的共同管理    

通过以前的 Windows 10 更新，已经可以将 Windows 10 设备同时联接到本地 Active Directory (AD) 和基于云的 Azure AD（混合 Azure AD）。 从 Configuration Manager 版本 1710 开始，共同管理利用了此项改进。 它使你可使用 Configuration Manager 和 Intune 同时管理 Windows 10 版本 1709 设备。 <!-- 1350871 -->


## <a name="why-co-management"></a>为什么选择共同管理？

许多客户想要使用一种基于云的简单低成本解决方案通过管理移动设备的相同方式来管理 Windows 10 设备。 然而，实现从传统管理到现代管理的转换可能具有挑战性。  


## <a name="what-is-co-management"></a>什么是共同管理？

通过共同管理，可以使用 Configuration Manager 和 Intune 同时管理 Windows 10 设备。 它是一种解决方案，在传统管理与现代管理之间架起一座桥梁，为你提供利用分阶段的方法实现转换的途径。


## <a name="benefits"></a>优点 

立即使用以下 Intune 功能：  
 
- 远程操作
    - [恢复出厂设置](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
    - [选择性擦除](https://docs.microsoft.com/intune/apps-selective-wipe)
    - [删除设备](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
    - [重启设备](https://docs.microsoft.com/intune/device-restart)
    - [全新启动](https://docs.microsoft.com/intune/device-fresh-start)  

- 使用 Intune 且面向以下工作负载的业务流程：
    - [符合性策略](https://docs.microsoft.com/intune/device-compliance-get-started)
    - [资源访问策略](https://docs.microsoft.com/intune/device-profiles)
    - [Windows 更新策略](https://docs.microsoft.com/intune/windows-update-for-business-configure)
    - [Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10)，从 Configuration Manager 1802 开始。 <!-- 1357365 -->
    - [设备配置](https://docs.microsoft.com/intune/device-profile-create)，从 Configuration Manager 1806 开始。 <!-- 1357903 -->
    - [Office 即点即用应用](https://docs.microsoft.com/intune/apps-add-office365)，从 Configuration Manager 1806 开始<!--1357841-->
    - [移动应用](https://docs.microsoft.com/intune/app-management)，从 Configuration Manager 1806 开始作为预发布功能。 <!--1357892-->



## <a name="how-to-configure-co-management"></a>如何配置共同管理

 有两个实现共同管理的主要方式：  

   - Configuration Manager 预配共同管理：将已加入 Azure AD 的 Windows 10 设备（已经是 Configuration Manager 客户端）注册到 Intune。  

   - 预配的 Intune：对于已注册到 Intune 的设备，安装 Configuration Manager 客户端以实现共同管理状态。 


### <a name="configuration-manager"></a>配置管理器

 -  升级到 Configuration Manager 版本 1710 或更高版本。


### <a name="azure-active-directory"></a>Azure Active Directory

 - Windows 10 设备必须加入 Azure AD。 它们可以是以下任一类型：  

     - [已加入混合 Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)，其中设备同时加入 Azure AD 和本地域  

     - 仅限已加入 Azure AD。 （此类型有时称为“已加入云域”）<!--SCCMDocs issue 605-->

 - [启用 Windows 10 自动注册](https://docs.microsoft.com/intune/windows-enroll)。  


### <a name="intune"></a>Intune

 - [如何设置 Intune 订阅。](/sccm/mdm/deploy-use/configure-intune-subscription)或[设置 Intune](/intune/setup-steps)  

 - [开始从混合 MDM 迁移到 Intune 独立版本](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

 > [!Note]  
 > 如果具有混合 MDM 环境（Intune 与 Configuration Manager 集成），则无法启用共同管理。 但是，你可以开始将用户迁移到 Intune 独立版本，然后对其关联的 Windows 10 设备启用共同管理。 有关迁移到 Intune 独立版本的详细信息，请参阅[开始从混合 MDM 迁移到 Intune 独立版本](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)。  


### <a name="enable-co-management"></a>启用共同管理 

 > [!Important]  
 > 从版本 1802 开始，要启用共同管理，Configuration Manager 中的管理用户帐户必须是具有所有安全作用域的“完全权限管理员”。 有关详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。<!--SCCMDoc issue 626-->  

 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。 单击功能区中的“配置共同管理”以打开“共同管理载入”向导。 
   
1. 在“订阅”页上，单击“登录”。 登录到你的 Intune 租户，然后单击“下一步”。  

    > [!Tip]   
    > 请确保登录租户时所用的帐户已分配有 Intune 许可证，否则操作将失败且显示错误消息“无法识别用户”。  

2. 在“启用”页上，选择“自动注册到 Intune”设置。 如果需要，复制已在 Intune 中注册的设备的命令行。  

    > [!Note]  
    > 从版本 1806 开始，并非所有客户端都立即自动注册。 此行为有助于更好地扩展大型环境的注册。 Configuration Manager 根据客户端数量随机注册。 例如，如果环境有 100,000 个客户端，则在启用此设置时，注册将持续几天。<!--1358003-->  

3. 在“工作负载”页上，为每个工作负载选择要移动的设备组以便使用 Intune 进行管理。  

4. 在“暂存”页上，选择一个设备集合作为“试点集合”。 验证“摘要”，然后完成该向导。  


### <a name="upgrade-windows-10-client"></a>升级 Windows 10 客户端

- 升级到 [Windows 10 版本 1709（也称为 Fall Creators Update）及更高版本](/sccm/osd/deploy-use/manage-windows-as-a-service)


### <a name="configure-workloads-to-switch-to-intune"></a>配置工作负载以切换到 Intune 

[能够转换到 Intune 的工作负载](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)文章介绍了如何将特定的 Configuration Manager 工作负载切换到 Intune。 此文还介绍了如何更改转换了工作负载的设备组的说明。

#### <a name="compliance-policies"></a>相容性策略 
符合性策略定义设备必须遵从的规则和设置，以便将设备视为符合条件访问策略。 也可使用符合性策略来监视和修正独立于条件访问的设备符合性问题。 有关详细信息，请参阅[设备符合性策略](https://docs.microsoft.com/intune/device-compliance-get-started)。  

#### <a name="windows-update-policies"></a>Windows 更新策略
通过适用于企业的 Windows 更新策略，可以针对 Windows 10 功能更新或直接由适用于企业的 Windows 更新托管的 Windows 10 设备的质量更新，配置延迟策略。 有关详细信息，请参阅[配置适用于企业的 Windows 更新延迟策略](https://docs.microsoft.com/intune/windows-update-for-business-configure)。  

#### <a name="resource-access-policies"></a>资源访问策略
资源访问策略在设备上配置 VPN、Wi-Fi、电子邮件以及证书设置。 有关详细信息，请参阅[部署资源访问配置文件](https://docs.microsoft.com/intune/device-profiles)。

#### <a name="endpoint-protection"></a>Endpoint Protection
从 Configuration Manager 1802 开始，Endpoint Protection 工作负荷可以转换到 Intune。 有关详细信息，请参阅[适用于 Microsoft Intune 的 Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10)<!-- 1357365 --> 和[能够转换到 Intune 的工作负荷](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)。

#### <a name="device-configuration"></a>设备配置
从 Configuration Manager 1806 开始，设备配置工作负荷可以转换到 Intune。 有关详细信息，请参阅[在 Microsoft Intune 中创建设备配置文件](https://docs.microsoft.com/intune/device-profile-create)和[能够转换到 Intune 的工作负荷](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)。  <!--1357903-->

#### <a name="office-click-to-run-apps"></a>Office 即点即用应用
从 Configuration Manager 1806 开始，Office 365 工作负荷可以转换到 Intune。 有关详细信息，请参阅[能够转换到 Intune 的工作负荷](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)。 <!--1357841-->

#### <a name="mobile-apps"></a>移动应用
从 Configuration Manager 版本 1806 开始，移动应用工作负荷可以转换到 Intune。 此功能是预发布功能。 若要启用此功能，请参阅[预发行功能](/sccm/core/servers/manage/pre-release-features)。 转移此工作负荷之后，任何从 Intune 部署的可用应用在公司门户中也变得可用。 从 Configuration Manager 部署的应用在软件中心可用。<!--1357892-->


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>将 Configuration Manager 客户端安装到在 Intune 中注册的设备

如果在 Intune 中注册 Windows 10 设备，请在设备上安装 Configuration Manager 客户端（[使用特定的命令行](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)），使客户端准备好进行共同管理。 然后，从 Configuration Manager 控制台中启用共同管理，开始针对特定 Windows 10 设备将特定的工作负荷移动到 Intune。
对于尚未在 Intune 中注册的 Windows 10 设备，请在 Azure 中使用自动注册来注册设备。 对于新的 Windows 10 设备，请使用 [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) 配置全新体验 (OOBE)，其中包括在 Intune 中注册设备的自动注册。

使用 Intune 安装 Configuration Manager 客户端时，请 在 Configuration Manager 中启用[云管理网关](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway)。



## <a name="monitor-co-management"></a>监视共同管理

[此共同管理仪表板](/sccm/core/clients/manage/co-management-dashboard)可帮助你查看环境中共同管理的计算机。 图形有助于标识可能需要注意的设备。



## <a name="next-steps"></a>后续步骤

[准备 Windows 10 设备进行共同管理](co-management-prepare.md)
