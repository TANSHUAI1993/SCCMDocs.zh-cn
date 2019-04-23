---
title: 桌面分析
titleSuffix: Configuration Manager
description: 与 Configuration Manager 集成的 Desktop 分析服务概述。
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1229dabb0fedf600f7d57a2a400df87906945ba4
ms.sourcegitcommit: d23ccf7b95e6c2a6b156975194ebbc375cb5e6ea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60124414"
---
# <a name="what-is-desktop-analytics"></a>什么是桌面分析？

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

桌面 Analytics 是一个集成使用 Configuration Manager 的基于云的服务。 该服务提供见解和智能，以便做出更明智的决策的 Windows 和 Office 客户端的更新准备情况。 它将从你的组织数据与从数百万台设备连接到 Microsoft 云服务聚合的数据相结合。 

使用桌面 Analytics 与 Configuration Manager 到：  

- 创建你的组织中运行应用的清单  

- 评估与 Windows 10 和 Office 365 专业增强版的最新的功能更新的应用程序兼容性  

- 确定兼容性问题，并接收基于云的数据的见解的缓解建议  

- 创建表示整个应用程序和驱动程序空间在最小的一组设备的试验组  

- 将 Windows 10 和 Office 365 专业增强版部署到试验和生产托管设备  

![在 Azure 门户中的桌面分析主页的屏幕截图](media/portal-home.png)

> [!Note]  
> 桌面分析是一种 Windows Analytics 的后续任务。 *Windows Analytics*服务包括升级就绪情况、 更新符合性和设备运行状况。 
> 
> 所有这些功能结合*Desktop 分析*服务。 桌面分析也更加紧密的集成使用配置管理器中，并包括 Windows 和 Office。 



## <a name="benefits"></a>优点

许多客户会遇到与获取和了解最新的 Windows 10 和 Office 365 专业增强版的挑战。 主要的挑战测试应用程序。 此过程为通常手动操作。 它是适用于 IT 管理员和应用程序所有者以持续分析现有的应用程序非常耗时。 然后修正出现的任何问题。 

桌面分析提供以下优势：

- **设备和软件清单**:关键因素，例如应用、 加载项、 宏和版本的 Office 和 Windows 的清单。  

- **试验标识**:设备，可提供因素范围最广范围的最小集的标识。 它主要关注对试运行 Windows 和 Office 的升级和更新最重要的因素。 确保来说，试点更大的成功，可更快、 更有信心地进入生产环境中广泛部署。  

- **查明问题**:使用聚合的市场数据以及你环境中的数据，该服务预测潜在问题并了解最新的 Windows 和 Office。 这样会建议可能的缓解措施。  

- **Configuration Manager 集成**:服务云启用现有的本地基础结构。 使用此数据和分析来部署和管理设备上的 Windows 和 Office。  



## <a name="prerequisites"></a>先决条件

若要使用 Desktop 分析，请确保你的环境满足以下先决条件。 


### <a name="technical"></a>技术

- 有效的 Azure 订阅  
    
    - [**公司管理员**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator)到 Azure 中的权限**接受服务协议**，**确认你的订阅**和**提供用户的访问** 

    - **工作区所有者**或**参与者**权**设置工作区**和  

        - [**Log Analytics 参与者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor)并[**用户访问管理员**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)上要使用现有的工作区或现有资源组中创建新的工作区的资源组。

        - [**所有者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)，或[**参与者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor)并[**用户访问管理员**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)上的权限若要创建新的资源组中的工作区的订阅。

- Configuration Manager，版本 1810年与更新汇总 4488598 或更高版本。 有关详细信息，请参阅[更新 Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix)。  

    - **完全权限管理员**角色在 Configuration Manager  

- 运行 Windows 7、 Windows 8.1 或 Windows 10 设备  

    - 安装最新的更新。 有关详细信息，请参阅[更新设备](/sccm/desktop-analytics/enroll-devices#update-devices)。  

    - 设备还需要让 Configuration Manager 客户端版本 1810年 4486457 或更高版本的更新汇总。 有关详细信息，请参阅[更新 Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix)。  

- Windows 诊断数据。 有关详细信息，请参阅下列文章：  

    - [诊断数据级别](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [桌面分析隐私](/sccm/desktop-analytics/privacy)  

- 从设备到 Microsoft 公有云网络连接。 有关详细信息，请参阅[如何启用数据共享](/sccm/desktop-analytics/enable-data-sharing)  


### <a name="licensing"></a>许可

桌面 Analytics 中的大多数功能不需要任何额外的许可证或订阅。 正确配置后，使用 Desktop Analytics 不会产生任何 Azure 费用。 

若要访问 Windows 运行状况见解，或将数据导出，没有其他许可要求。 如果你不具有以下订阅之一，你仍可以设置和使用 Desktop 分析，但未授权使用 Windows 运行状况见解，或将数据导出：

- Windows 10 企业版或 Windows 10 教育版： 每个设备具有有效软件保障  

- Windows 10 企业版 E3 或 E5： 每个设备或每个用户订阅 （包含在 Microsoft 365 F1、 E3 或 E5）  

- Windows 10 教育版 A3 或 A5 （随附 Microsoft 365 教育版 A3 或 A5）  

- Windows 虚拟桌面访问 E3 或 E5： 每个设备的每个用户的订阅  

> [!Note]  
> 对于每个设备许可证，你无需激活许可证的每个设备。 你只需在桌面 Analytics 中注册的设备的足够的许可证。  


<!-- 
## Top task
> *Optional*  
> *An effective way to structure your overview article is to create an H2 for the top customer tasks and describe how the product/service helps customers with that task.*  
> *Create a new H2 for each task you list.*  
 -->



## <a name="next-steps"></a>后续步骤

以下教程提供了开始使用桌面 Analytics 和 Configuration Manager 的分步指南：  

- [将 Office 365 部署到试运行](/sccm/desktop-analytics/tutorial-office-365)  

<!-- for future
- [Deploy Windows 10 to a pilot](/sccm/desktop-analytics/tutorial-windows)  
-->
