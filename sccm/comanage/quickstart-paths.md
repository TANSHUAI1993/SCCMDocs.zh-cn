---
title: 共同管理的路径
titleSuffix: Configuration Manager
description: 了解设置共同管理的两种主要方法的先决条件。
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c34cf73133086f08cb390f39ab4fe715dfcefd2
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550668"
---
# <a name="paths-to-co-management"></a>共同管理的路径

可以使用两种主要方法来设置共同管理。 请务必了解每种方法的先决条件。 这两种方法都需要结合使用 Azure Active Directory (Azure AD)、Configuration Manager、Microsoft Intune 和 Windows 10。 

1. [将现有 Configuration Manager 管理的设备自动注册到 Intune](#bkmk_path1)  
2. [使用新式配置启动 Configuration Manager 客户端](#bkmk_path2)  

![共同管理方法的关系图](media/co-management-paths.png)



## <a name="bkmk_path1"></a>方法 1：自动注册现有客户端

采用此方法可将现有的 Configuration Manager 管理的设备快速注册到 Intune。 在 Configuration Manager 中管理这些设备的方式与启用共同管理之前没有差别。 现在，可以获得所有基于云的优势。 此方法对用户而言是透明的。

以下是需要设置的选项：
- 混合 Azure AD
    - 以下 [Azure AD 混合标识选项](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin)之一：  
       - 含[无缝单一登录 (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) 的[密码哈希同步](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization)
       - 含[无缝单一登录 (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) 的[直通身份验证](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta)
       - [联合 SSO（含 Active Directory 联合身份验证服务 (AD FS)）](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium 许可证
    - 配置混合 Azure AD 联接（选择一个选项）：
        - 针对托管域
        - 针对联盟域
- 混合 Azure AD 联接的客户端代理设置
- 配置设备自动注册到 Intune
- 分配 Intune 用户许可证
- 在 Configuration Manager 中启用共同管理

有关此方法的教程，请参阅[教程：为现有 Configuration Manager 客户端启用共同管理](/sccm/comanage/tutorial-co-manage-clients)。



## <a name="bkmk_path2"></a> 方法 2：使用新式预配启动

以下是需要设置的选项：

1. [设置增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [在 Azure 中创建云服务](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [配置管理点和客户端以使用云管理网关](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [使用 Intune 部署 Configuration Manager 客户端](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> 此方法的教程即将推出。

