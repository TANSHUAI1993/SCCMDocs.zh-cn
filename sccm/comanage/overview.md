---
title: 适用于 Windows 10 设备的共同管理
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 和 Microsoft Intune 同时管理 Windows 10 设备。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/26/2019
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1e0ae5c392acd03509f70c19f551731065bc4be2
ms.sourcegitcommit: 23852dda81bb8496dd10c0a8ec4f740a8e15efc3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2019
ms.locfileid: "64873286"
---
# <a name="what-is-co-management"></a>什么是共同管理？

<!-- 1350871 -->
共同管理是将现有 Configuration Manager 部署附加到 Microsoft 365 云的主要方式之一。 它可帮助解锁其他由云提供支持的功能，例如条件访问。

通过共同管理，可以使用 Configuration Manager 和 Microsoft Intune 同时管理 Windows 10 设备。 它允许通过添加新功能在 Configuration Manager 中云附加现有投资。 通过使用共同管理，可以灵活地使用最适合组织的技术解决方案。

如果某台 Windows 10 设备既具有 Configuration Manager 客户端又已注册到 Intune，用户将同时获得这两项服务的优势。 可以控制将颁发机构从 Configuration Manager 切换到 Intune 时的工作负载（如果有）。 Configuration Manager 持续管理所有其他工作负载（其中包括不切换到 Intune 的那些工作负载）以及共同管理不支持的的所有其他 Configuration Manager 功能。

用户还可以使用单独的设备集合来试验工作负载。 借助试验功能，可以在切换大型组之前使用设备子集测试 Intune 功能。

![共同管理的概述图](media/co-management-overview.png)

> [!Note]  
> 同时使用 Configuration Manager 和 Microsoft Intune 来管理 Windows 10 设备，这种配置称为“共同管理”。 使用 Configuration Manager 管理设备并注册第三方 MDM 服务，这种配置称为“共存”。 如果没有在两者之间进行适当协调，为一个设备设置两个管理权限可能会很有挑战性。 通过共同管理，Configuration Manager 和 Intune 共同平衡[工作负荷](#workloads)，以确保没有冲突。 由于第三方服务中不存在这种交互，因此共存的管理功能存在一些限制。 有关详细信息，请参阅[第三方 MDM 与 Configuration Manager 共存](/sccm/comanage/coexistence)。


## <a name="paths-to-co-management"></a>共同管理的路径

有两个实现共同管理的主要方式：  

- **现有 Configuration Manager 客户端**：拥有已经是 Configuration Manager 客户端的 Windows 10 设备。 设置混合 Azure AD，并将其注册到 Intune。  

- **基于 Internet 的新设备**：拥有联接 Azure AD 并自动注册到 Intune 的新 Windows 10 设备。 安装 Configuration Manager 客户端以实现共同管理。  

有关这些方式的详细信息，请参阅[实现共同管理的方式](/sccm/comanage/quickstart-paths)。



## <a name="benefits"></a>优点

在共同管理中注册现有的 Configuration Manager 客户端时，将获得以下直接价值：  

- 遵守设备符合性的条件访问  

- 基于 Intune 的远程操作，例如：重启、远程控制或恢复出厂设置

- 设备运行状况的集中可见性  

- 将用户、设备和应用与 Azure Active Directory (Azure AD) 相关联  

- 通过 Windows Autopilot 进行新式预配  

- 远程操作

若要详细了解共同管理的直接价值，请参阅快速入门系列[启用了共同管理的云](/sccm/comanage/quickstarts)。

借助共同管理，还可以使用 Intune 协调多个工作负载。 有关详细信息，请参阅[工作负荷](#workloads)部分。



## <a name="prerequisites"></a>先决条件

共同管理具有以下方面的先决条件：

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
> 确保将 Intune 许可证分配到用于登录租户的帐户。 否则，登录将失败，并显示错误消息“无法识别用户”。  


### <a name="configuration-manager"></a>配置管理器

共同管理需要 Configuration Manager 1710 版或更高版本。

自 Configuration Manager 1806 版起，可将多个 Configuration Manager 实例连接到单个 Intune 租户。 <!--1357944-->  

启用共同管理本身并不要求使用 Azure AD 登录站点。 对于[第二种方式](#paths-to-co-management)，基于 Internet 的 Configuration Manager 客户端需要[云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG)。 CMG 要求站点[加入 Azure AD 以进行云管理](/sccm/core/servers/deploy/configure/azure-services-wizard)。 


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

将设备升级到 Windows 10 版本 1709 或更高版本。 有关详细信息，请参阅[采用 Windows 即服务](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service)。

> [!IMPORTANT]
> Windows 10 移动设备不支持共同管理。


### <a name="permissions-and-roles"></a>权限和角色

<!--SCCMDocs issue #667-->
| 操作 | 所需角色 |
|----|----|
| 在 Configuration Manager 中设置云管理网关 | Azure 订阅管理员 |
| 从 Configuration Manager 中创建 Azure AD 应用 | Azure AD 全局管理员 |
| 在 Configuration Manager 中导入 Azure 应用 | Configuration Manager 完全权限管理员<br>无需任何其他的 Azure 角色 |
| 在 Configuration Manager 中启用共同管理 | Azure AD 用户<br>具有所有范围权限的 Configuration Manager 完全权限管理员。<!--SCCMDoc issue 626--> |

要详细了解 Azure 角色，请参阅[了解不同角色](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles)。

有关 Configuration Manager 角色的详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。


## <a name="workloads"></a>工作负载

不必切换工作负载，或可以在准备好后单独执行这些工作负载。 Configuration Manager 持续管理所有其他工作负载（其中包括不切换到 Intune 的那些工作负载）以及共同管理不支持的的所有其他 Configuration Manager 功能。

共同管理支持以下工作负载：

- 相容性策略  

- Windows 更新策略  

- 资源访问策略  

- Endpoint Protection  

- 设备配置  

- Office 即点即用应用  

- 客户端应用  

有关详细信息，请参阅[工作负载](/sccm/comanage/workloads)。



## <a name="monitor-co-management"></a>监视共同管理

此共同管理仪表板可帮助你查看环境中共同管理的计算机。 图形有助于标识可能需要注意的设备。

![共同管理仪表板的屏幕截图](media/co-management-dashboard.png)

有关详细信息，请参阅[如何监视共同管理](/sccm/comanage/how-to-monitor)。



## <a name="next-steps"></a>后续步骤

- [详细了解直接价值并开始使用共同管理](/sccm/comanage/quickstarts)  

- [教程：为现有 Configuration Manager 客户端启用共同管理](/sccm/comanage/tutorial-co-manage-clients)  
