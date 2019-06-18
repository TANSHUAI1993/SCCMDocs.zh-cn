---
title: 桌面分析
titleSuffix: Configuration Manager
description: 与 Configuration Manager 集成的 Desktop 分析服务概述。
ms.date: 06/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a298bd0504ea719d6b60d2c86692942d6ba989b8
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159034"
---
# <a name="what-is-desktop-analytics"></a>什么是桌面分析？

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

桌面 Analytics 是一个集成使用 Configuration Manager 的基于云的服务。 该服务提供见解和智能，以便做出更明智的决策的 Windows 客户端的更新准备情况。 它将从你的组织数据与从数百万台设备连接到 Microsoft 云服务聚合的数据相结合。

使用桌面 Analytics 与 Configuration Manager 到：  

- 创建你的组织中运行应用的清单  

- 评估与最新的 Windows 10 功能更新的应用程序兼容性  

- 确定兼容性问题，并接收基于云的数据的见解的缓解建议  

- 创建表示整个应用程序和驱动程序空间在最小的一组设备的试验组  

- 将 Windows 10 部署到试验和生产管理设备  

![在 Azure 门户中的桌面分析主页的屏幕截图](media/portal-home.png)

> [!Note]  
> 桌面分析是一种 Windows Analytics 的后续任务。 *Windows Analytics*服务包括升级就绪情况、 更新符合性和设备运行状况。
>
> 所有这些功能结合*Desktop 分析*服务。 桌面分析也更加紧密的集成使用 Configuration Manager。



## <a name="benefits"></a>优点

许多客户会遇到与获取和了解最新的 Windows 10 的挑战。 主要的挑战测试应用程序。 此过程为通常手动操作。 它是适用于 IT 管理员和应用程序所有者以持续分析现有的应用程序非常耗时。 然后修正出现的任何问题。

桌面分析提供以下优势：

- **设备和软件清单**:清单的关键因素，如应用和 Windows 的版本。  

- **试验标识**:设备，可提供因素范围最广范围的最小集的标识。 它主要关注对试运行 Windows 升级和更新最重要的因素。 确保来说，试点更大的成功，可更快、 更有信心地进入生产环境中广泛部署。  

- **查明问题**:使用聚合的市场数据以及你环境中的数据，该服务预测潜在问题并了解最新的 Windows。 这样会建议可能的缓解措施。  

- **Configuration Manager 集成**:服务云启用现有的本地基础结构。 使用此数据和分析来部署和管理 Windows 设备上。  



## <a name="prerequisites"></a>先决条件

若要使用 Desktop 分析，请确保你的环境满足以下先决条件。


### <a name="technical"></a>技术

- 有效的 Azure 订阅，使用[全局管理员](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator)权限  

    - **工作区所有者**或**参与者**权**设置工作区**，和以下角色：  

       - [**Desktop 分析管理员**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)角色。

       - [**Log Analytics 参与者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor)并[**用户访问管理员**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)上要使用现有的工作区或现有资源组中创建新的工作区的资源组。

        - [**所有者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)，或[**参与者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor)并[**用户访问管理员**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)上的权限若要创建新的资源组中的工作区的订阅。  

- Configuration Manager，版本 1902年更新汇总 (4500571) 或更高版本。 有关详细信息，请参阅[更新 Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix)。  

    - **完全权限管理员**角色在 Configuration Manager  

- 运行 Windows 7、 Windows 8.1 或 Windows 10 设备  

    - 安装最新的更新。 有关详细信息，请参阅[更新设备](/sccm/desktop-analytics/enroll-devices#update-devices)。  

    - 设备还需要让 Configuration Manager 客户端版本 1902年更新汇总 (4500571) 或更高版本。 有关详细信息，请参阅[更新 Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix)。  

    > [!Note]  
    > 桌面分析不支持升级到 Windows 10 的长期维护服务频道 (LTSC)。 有关详细信息，请参阅[作为服务概述 Windows](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)。
    >
    > 桌面 Analytics 设计为最佳支持就地升级方案。 如果你需要从 32 位到 64 位体系结构，如做出重大更改，使用图像处理方案。 桌面进行分析洞察经典操作系统部署方案中，仍然有价值，但可以忽略就地升级特定指南。 有关详细信息，请参阅[部署企业操作系统使用 Configuration Manager 的方案](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems)。

- Windows 诊断数据。 有关详细信息，请参阅下列文章：  

    - [诊断数据级别](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [桌面分析隐私](/sccm/desktop-analytics/privacy)  

- 从设备到 Microsoft 公有云网络连接。 有关详细信息，请参阅[如何启用数据共享](/sccm/desktop-analytics/enable-data-sharing)  


### <a name="licensing"></a>许可

桌面分析需要以下许可证订阅之一：

- Windows 10 企业版 E3 或 E5;或 Microsoft 365 F1、 E3 或 E5  

- Windows 10 教育版 A3 或 A5;Microsoft 365 A3 或 A5  

- Windows VDA E3 或 E5  




## <a name="next-steps"></a>后续步骤

以下教程提供了开始使用桌面 Analytics 和 Configuration Manager 的分步指南：  

- [将 Windows 10 部署到试运行](/sccm/desktop-analytics/tutorial-windows10)  
