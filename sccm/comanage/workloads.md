---
title: 共同管理工作负荷
titleSuffix: Configuration Manager
description: 了解有关您可以从 Configuration Manager 切换到 Microsoft Intune 的工作负荷。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.collection: M365-identity-device-management
ms.openlocfilehash: a3723595091e57a7ad2267a4da325e7c134c7bf1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754668"
---
# <a name="co-management-workloads"></a>共同管理工作负荷

无需切换工作负荷，或您可以在单独执行准备就绪后这些。 配置管理器将继续管理所有其他工作负荷，包括不切换到 Intune，并且所有其他功能的 Configuration Manager 的共同管理不支持这些工作负荷。

共同管理支持以下工作负荷：

- [符合性策略](#compliance-policies)  

- [Windows 更新策略](#windows-update-policies)  

- [资源访问策略](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [设备配置](#device-configuration)  

- [Office 即点即用应用](#office-click-to-run-apps)  

- [客户端应用程序](#client-apps)  



## <a name="compliance-policies"></a>相容性策略 

符合性策略定义设备必须遵从的规则和设置，以便将设备视为符合条件访问策略。 也可使用符合性策略来监视和修正独立于条件访问的设备符合性问题。 

有关 Intune 功能的详细信息，请参阅[设备符合性策略](https://docs.microsoft.com/intune/device-compliance-get-started)。  



## <a name="windows-update-policies"></a>Windows 更新策略

通过适用于企业的 Windows 更新策略，可以针对 Windows 10 功能更新或直接由适用于企业的 Windows 更新托管的 Windows 10 设备的质量更新，配置延迟策略。 

有关 Intune 功能的详细信息，请参阅[配置 Windows Update for Business 延迟策略](https://docs.microsoft.com/intune/windows-update-for-business-configure)。  



## <a name="resource-access-policies"></a>资源访问策略

资源访问策略在设备上配置 VPN、Wi-Fi、电子邮件以及证书设置。 

有关 Intune 功能的详细信息，请参阅[部署资源访问配置文件](https://docs.microsoft.com/intune/device-profiles)。



## <a name="endpoint-protection"></a>Endpoint Protection
<!--1357365-->

从 Configuration Manager 1802 开始，Endpoint Protection 工作负荷包括了 Windows Defender 的反恶意软件保护功能套件： 

- Windows Defender 应用程序防护  
- Windows Defender 防火墙  
- Windows Defender SmartScreen  
- Windows 加密  
- Windows Defender 攻击防护  
- Windows Defender 应用程序控制  
- Windows Defender 安全中心  
- Windows Defender 高级威胁防护  
- Windows 信息保护  

有关 Intune 功能的详细信息，请参阅[Microsoft Intune 的 Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10)。



## <a name="device-configuration"></a>设备配置
<!--1357903-->

设备配置工作负荷从 Configuration Manager 1806，包括在组织中管理的设备的设置。 切换此工作负荷也会移动**的资源访问权限**并**Endpoint Protection**工作负荷。

即使设备配置颁发机构是 Intune，你仍可将 Configuration Manager 中的设置部署到共同托管的设备。 此异常可能用于配置你的组织要求，但尚未在 Intune 中可用的设置。 在 [Configuration Manager 配置基线](/sccm/compliance/deploy-use/create-configuration-baselines)上指定此异常。 启用选项**始终适用于此基线甚至共同托管客户端**创建基线时。 您可以在以后更改**常规**现有基线的属性选项卡。  

有关 Intune 功能的详细信息，请参阅[Microsoft Intune 中创建设备配置文件](https://docs.microsoft.com/intune/device-profile-create)。  



## <a name="office-click-to-run-apps"></a>Office 即点即用应用
<!--1357841-->

从 Configuration Manager 1806 开始，此工作负荷管理共同托管的设备上的 Office 365 应用。 

- 移动工作负荷后，此应用将显示在设备上的“公司门户”中  

- 除非重启设备，否则 Office 更新可能约在 24 小时后才能显示在客户端上  

- 存在一个新的全局条件，即“Office 365 应用程序是否在设备上由 Intune 进行托管”。 默认情况下将此条件作为一项要求添加到新的 Office 365 应用程序。 如果在转换此工作负荷时，共同托管客户端不满足应用程序的要求。 则不会安装通过 Configuration Manager 部署的 Office 365。  

有关 Intune 功能的详细信息，请参阅[分配 Office 365 应用部署到使用 Microsoft Intune Windows 10 设备](https://docs.microsoft.com/intune/apps-add-office365)。 



## <a name="client-apps"></a>客户端应用程序
<!--1357892-->

从 Configuration Manager 版本 1806年开始，使用 Intune 来管理客户端应用程序共同托管的 Windows 10 设备上。 转移此工作负荷之后，任何从 Intune 部署的可用应用在公司门户中也变得可用。 从 Configuration Manager 部署的应用在软件中心可用。

有关 Intune 功能的详细信息，请参阅[什么是 Microsoft Intune 应用管理？](https://docs.microsoft.com/intune/app-management)。 

> [!Note]  
> 客户端应用程序工作负荷是预发行功能。 若要启用此功能，请参阅[预发行功能](/sccm/core/servers/manage/pre-release-features)。  



## <a name="next-steps"></a>后续步骤

[如何切换工作负荷](/sccm/comanage/how-to-switch-workloads)  


