---
title: 共同管理的路径
titleSuffix: Configuration Manager
description: 了解两种主要方式，以便设置共同管理的先决条件。
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 803f05dd14da8d280f08f2bcf3608865f384d273
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754653"
---
# <a name="paths-to-co-management"></a>共同管理的路径

有两种主要方式，以便设置了共同管理。 请务必了解每个路径的先决条件。 它们每个需要 Azure Active Directory (Azure AD)、 Configuration Manager、 Microsoft Intune 和 Windows 10 的某种组合。 

1. [自动注册到 Intune 现有 Configuration Manager 管理的设备](#bkmk_path1)  
2. [启动 Configuration Manager 客户端通过现代预配](#bkmk_path2)  

![共同管理路径的关系图](media/co-management-paths.png)



## <a name="bkmk_path1"></a> 路径 1:现有客户端中自动注册

采用此路径可以获取现有 Configuration Manager 托管的设备快速注册到 Intune。 启用共同管理之前，这些设备从 Configuration Manager 的管理并无不同。 现在，您有所有基于云的优势。 此路径是对用户透明。

下面是需要将其设置：
- 混合 Azure AD
    - Active Directory 联合身份验证服务 (ADFS) 与直通身份验证 (PTA)
    - Azure AD Connect
    - Azure AD Premium 许可证
    - 配置混合 Azure AD 联接 （选择一个选项）：
        - 托管域
        - 为联合域
- 客户端代理设置混合 Azure AD 联接
- 配置自动注册到 Intune 的设备
- 分配 Intune 用户许可证
- 启用共同管理配置管理器中

此路径的教程，请参阅[教程：启用共同管理现有 Configuration Manager 客户端](/sccm/comanage/tutorial-co-manage-clients)。



## <a name="bkmk_path2"></a> 路径 2:启动新式预配

下面是需要将其设置：

1. [安装程序增强了 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [在 Azure 中创建云服务](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [配置管理点和客户端使用云管理网关](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [使用 Intune 来部署 Configuration Manager 客户端](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> 此路径的教程即将推出。

