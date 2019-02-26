---
title: 适用于 Windows 10 设备的共同管理
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 和 Microsoft Intune 同时管理 Windows 10 设备。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.collection: M365-identity-device-management
ms.openlocfilehash: c88bf98e035499c271de8acf9d8fa222e5058447
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754689"
---
# <a name="what-is-co-management"></a>什么是共同管理？

<!-- 1350871 --> 共同管理是一个要附加现有的配置管理器部署到 Microsoft 365 云的主要方式。 它可帮助你解锁其他云提供支持的功能，如条件性访问。 

共同管理，可使用 Configuration Manager 和 Microsoft Intune 同时管理 Windows 10 设备。 它允许你云附加现有投资在 Configuration Manager 中添加新功能。 通过使用共同管理，您可以使用最适合你的组织的技术解决方案的灵活性。 

如果 Windows 10 设备具有 Configuration Manager 客户端，并且会注册到 Intune，获得这两个服务的优势。 如果有的话，切换到 Intune 的颁发机构从 Configuration Manager，控制哪些工作负荷。 配置管理器将继续管理所有其他工作负荷，包括不切换到 Intune，并且所有其他功能的 Configuration Manager 的共同管理不支持这些工作负荷。

您还可以试验具有单独的设备集合的工作负荷。 试验，可切换更大的组之前测试的子集的设备的 Intune 功能。 

![共同管理的概要示意图](media/co-management-overview.png)



## <a name="paths-to-co-management"></a>共同管理的路径

有两个实现共同管理的主要方式：  

- **现有的 Configuration Manager 客户端**:必须已将 Configuration Manager 客户端的 Windows 10 设备。 设置混合 Azure AD 中，并在 Intune 中注册。  

- **新的基于 internet 的设备**:具有新的 Windows 10 设备加入 Azure AD 并自动注册到 Intune。 安装 Configuration Manager 客户端，以达到共同管理状态。  

在路径上的详细信息，请参阅[共同管理的路径](/sccm/comanage/quickstart-paths)。



## <a name="benefits"></a>优点 

当你注册共同管理中的现有 Configuration Manager 客户端时，可以获得以下即时值：  

- 使用设备符合性的条件访问  

- 基于 Intune 的远程操作，例如： 重新启动、 远程控制或恢复出厂设置

- 设备运行状况的集中可见性  

- 链接用户、 设备和应用与 Azure Active Directory (Azure AD)  

- 现代与 Windows Autopilot 预配  

- 远程操作

此值立即从共同管理的详细信息，请参阅向的快速入门系列[云连接通过共同管理](/sccm/comanage/quickstarts)。

共同管理还可通过 Intune 安排适用于多个工作负荷。 有关详细信息，请参阅[工作负荷](#workloads)部分。 



## <a name="prerequisites"></a>先决条件

共同管理的以下区域中具有这些系统必备组件：

- [许可](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [权限和角色](#permissions-and-roles)  

### <a name="licensing"></a>许可

- Azure AD Premium 
- 适用于所有用户的 EMS 或 Intune 许可证  

    > [!Note]  
    > 企业移动性 + 安全性 (EMS) 订阅包括 Azure Active Directory Premium 和 Microsoft Intune。

> [!Tip]  
> 请确保向用于登录到你的租户的帐户分配 Intune 许可证。 否则，登录会失败并显示错误消息"无法识别的用户"。  


### <a name="configuration-manager"></a>配置管理器

共同管理需要 Configuration Manager 版本 1710年或更高版本。

从 Configuration Manager 版本 1806年开始，可以连接到单一的 Intune 租户的多个配置管理器实例。 <!--1357944-->  

启用共同管理本身不需要你加入你的站点与 Azure AD。 有关[第二个路径方案](#paths-to-co-management)，基于 internet 的 Configuration Manager 客户端需要[云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)(CMG)。 CMG 需要的站点是[登记到 Azure AD 进行云管理](/sccm/core/servers/deploy/configure/azure-services-wizard)。 


### <a name="azure-ad"></a>Azure AD

- Windows 10 设备必须加入 Azure AD。 它们可以是以下任一类型：  

    - [混合 Azure AD 加入](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)，其中设备已加入到本地 Active Directory 且使用 Azure Active Directory 注册。  

    - 仅限[已联接 Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)。 （此类型有时称为“已加入云域”）<!--SCCMDocs issue 605-->  


### <a name="intune"></a>Intune

- [设置 Intune](https://docs.microsoft.com/intune/setup-steps)  

- [启用 Windows 10 自动注册](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

> [!Note]  
> 如果具有混合 MDM 环境（Intune 与 Configuration Manager 集成），则无法启用共同管理。 但是，你可以开始将用户迁移到 Intune 独立版本，然后对其关联的 Windows 10 设备启用共同管理。 有关迁移到 Intune 独立版本的详细信息，请参阅[开始从混合 MDM 迁移到 Intune 独立版本](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)。  
> 
> 若正在使用[混合机构](/sccm/mdm/deploy-use/migrate-mixed-authority)，请先迁移到 Intune 独立版。 然后，在设置共同管理前将 MDM 机构设置为 Intune。<!--SCCMDocs issue #797-->


### <a name="windows-10"></a>Windows 10

将设备升级到 Windows 10 版本 1709年或更高版本。 有关详细信息，请参阅[采用 Windows 作为服务](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service)。

> [!IMPORTANT]
> Windows 10 移动设备不支持共同管理。


### <a name="permissions-and-roles"></a>权限和角色
<!--SCCMDocs issue #667-->

| 操作 | 所需角色 |
|----|----|
| 设置云管理网关配置管理器中 | Azure**订阅管理器** |
| 从 Configuration Manager 中创建 Azure AD 应用 | Azure AD**全局管理员** |
| 导入 Azure 应用程序在配置管理器 | 配置管理器**完全权限管理员**<br>所需的任何其他的 Azure 角色 |
| 启用共同管理配置管理器中 | Azure AD 用户<br>配置管理器**完全权限管理员**与**所有**作用域权限。<!--SCCMDoc issue 626--> | 

要详细了解 Azure 角色，请参阅[了解不同角色](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles)。

有关配置管理器角色的详细信息，请参阅[的基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。


## <a name="workloads"></a>工作负载 

无需切换工作负荷，或您可以在单独执行准备就绪后这些。 配置管理器将继续管理所有其他工作负荷，包括不切换到 Intune，并且所有其他功能的 Configuration Manager 的共同管理不支持这些工作负荷。

共同管理支持以下工作负荷：

- 相容性策略  

- Windows 更新策略  

- 资源访问策略  

- Endpoint Protection  

- 设备配置  

- Office 即点即用应用  

- 客户端应用程序  

有关详细信息，请参阅[工作负荷](/sccm/comanage/workloads)。



## <a name="monitor-co-management"></a>监视共同管理

共同管理仪表板可帮助你查看你的环境中共同管理的计算机。 图形有助于标识可能需要注意的设备。

![共同管理仪表板的屏幕截图](media/co-management-dashboard.png)

有关详细信息，请参阅[如何监视共同管理](/sccm/comanage/how-to-monitor)。



## <a name="next-steps"></a>后续步骤

- [了解有关即时值以及如何开始使用共同管理的详细信息](/sccm/comanage/quickstarts)  

- [教程：启用共同管理现有 Configuration Manager 客户端](/sccm/comanage/tutorial-co-manage-clients)  

