---
title: 桌面分析
titleSuffix: Configuration Manager
description: 与 Configuration Manager 集成的桌面分析服务的概述。
ms.date: 07/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5ee4075926f5c6f01dddcf41a2c329e88a4ee591
ms.sourcegitcommit: 160bcdaf783f3946ad5c7869b2566cbfc4da545c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401509"
---
# <a name="what-is-desktop-analytics"></a>什么是桌面分析？

> [!Note]  
> 此信息与预览版服务相关, 该服务可能会在商业发布之前进行大量修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

桌面分析是一项基于云的服务, 可与 Configuration Manager 集成。 本服务为你提供了见解和情报, 使你可以更明智地决定 Windows 客户端的更新准备情况。 它将组织的数据与与 Microsoft 云服务连接的数百万台设备聚合的数据组合在一起。

使用带有 Configuration Manager 的桌面分析:  

- 创建在你的组织中运行的应用的清单  

- 评估应用程序兼容性和最新的 Windows 10 功能更新  

- 确定兼容性问题, 并根据启用了云的数据见解接收缓解建议  

- 在一组最小的设备上创建代表整个应用程序和驱动程序的试点组  

- 将 Windows 10 部署到试点和生产管理的设备  

![Azure 门户中的桌面分析主页的屏幕截图](media/portal-home.png)

> [!Note]  
> 桌面分析是 Windows Analytics 的后续版本。 *Windows Analytics*服务包含升级就绪情况、更新符合性和设备健康状况。
>
> 所有这些功能都已合并到*桌面分析*服务中。 桌面分析还与 Configuration Manager 紧密集成。



## <a name="benefits"></a>优点

许多客户在使用 Windows 10 时都面临着挑战。 主要的难题是测试应用程序。 此过程通常是手动的。 IT 管理员和应用程序所有者在不断分析现有应用程序时需要花费很长时间。 然后修正出现的任何问题。

桌面分析具有以下优势:

- **设备和软件清单**:关键因素 (如应用和 Windows 版本) 的清单。  

- **试点标识**:提供最广泛的各种因素的最小设备集的标识。 它侧重于对 Windows 升级和更新的试验最为重要的因素。 确保试验更成功后, 可以更快、更自信地在生产环境中进行广泛的部署。  

- **问题标识**:使用聚合的市场数据以及环境中的数据, 服务可预测使用 Windows 获取和保持最新的潜在问题。 然后, 它会建议可能的缓解措施。  

- **Configuration Manager 集成**:服务云-启用你的现有本地基础结构。 使用此数据和分析在设备上部署和管理 Windows。  



## <a name="prerequisites"></a>先决条件

若要使用桌面分析, 请确保你的环境满足以下先决条件。


### <a name="technical"></a>技术

- 有效的 Azure 订阅, 具有[全局管理员](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)权限。 不支持[Microsoft 帐户](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts)。  

    > [!Important]  
    > 桌面分析当前要求在 Azure AD 租户中部署 Office 365 服务。 以后这不是必需的。

    - **工作区所有者**或**参与者**权限**设置你的工作区**, 以及以下角色:  

      - [**桌面分析管理员**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)角色。

      - [**Log Analytics**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor)资源组上的参与者和[**用户访问管理员**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)使用现有的工作区, 或在现有的资源组中创建新的工作区。

      - 用于在新资源组中创建工作区的订阅的[**所有者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)或[**参与者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor)和[**用户访问管理员**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)权限。  

- Configuration Manager, 版本1902更新汇总 (4500571) 或更高版本。 有关详细信息, 请参阅[Update Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix)。  

    - Configuration Manager 中的[**完全权限管理员**](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_Planroles)角色  

    > [!Note]  
    > 桌面分析支持每个 Azure Active Directory (Azure AD) 租户和 Configuration Manager 层次结构一个商业 ID。 如果你的环境中有多个层次结构, 请使用不同的商业 Id 并 Azure AD 租户。<!-- 4958160 -->

- 运行 Windows 7、Windows 8.1 或 Windows 10 的设备  

    - 安装最新更新。 有关详细信息, 请参阅[更新设备](/sccm/desktop-analytics/enroll-devices#update-devices)。  

    - 设备还需要具有更新汇总 (4500571) 或更高版本的 Configuration Manager 客户端版本1902。 有关详细信息, 请参阅[Update Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix)。  

    > [!Note]  
    > 桌面分析不支持升级到 Windows 10 长期服务通道 (LTSC)。 有关详细信息, 请参阅[Windows 即服务概述](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)。
    >
    > 桌面分析旨在最大程度地支持就地升级方案。 如果需要进行重大更改 (例如从32位到64位体系结构的更改), 请使用映像方案。 桌面分析见解在这些经典 OS 部署方案中仍有价值, 但你可以忽略就地升级特定的指南。 有关详细信息, 请参阅[部署具有 Configuration Manager 的企业操作系统的方案](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems)。

- Windows 诊断数据。 有关详细信息，请参阅下列文章：  

    - [诊断数据级别](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [桌面分析隐私](/sccm/desktop-analytics/privacy)  

- 从设备到 Microsoft 公有云的网络连接。 有关详细信息, 请参阅[如何启用数据共享](/sccm/desktop-analytics/enable-data-sharing)  

> [!Important]   
> Microsoft 对提供用于控制隐私的工具和资源提供了强大的承诺。 因此，Microsoft 不会从位于欧洲国家/地区（EEA 和瑞士）的设备中收集以下数据：
>
> - 来自 Windows 8.1 设备的 Windows 诊断数据
> - 适用于 Windows 7 的应用使用情况数据

### <a name="licensing-and-costs"></a>许可和成本

桌面分析需要以下许可证订阅之一:

- Windows 10 企业版 E3 或 E5;或 Microsoft 365 F1、E3 或 E5  

- Windows 10 教育版 A3 或 A5;或 Microsoft 365 A3 或 A5  

- Windows VDA E3 或 E5  

除了许可证订阅的成本之外，使用桌面分析无需额外付费。 在 Azure Log Analytics 中，桌面分析为 "零分级"。 这一评级意味着，无论选择哪种 Azure Log Analytics 定价层，都不会从数据限制和成本中排除。 有关 Azure Log Analytics 定价层的详细信息，请参阅[定价-Log Analytics](https://azure.microsoft.com/pricing/details/monitor/)。

- 如果使用免费层，而该免费层的数据量为每天收集的数据量，则桌面分析数据不会计入此上限。 您可以从您的设备收集所有桌面分析数据，并且仍有可用于从其他源收集其他数据的完全上限。

- 如果你使用付费层，按收集的数据量收费，则不会对桌面分析数据收费。 可以从设备收集所有桌面分析数据，不会产生任何费用。

> [!Note]  
> 不同的 Azure Log Analytics 计划具有不同的数据保持期。 桌面分析继承工作区的数据保留策略。 如果工作区位于免费计划中，则桌面分析将保留在工作区中收集的过去30天的 "每日快照数"。


## <a name="next-steps"></a>后续步骤

以下教程提供了有关桌面分析和 Configuration Manager 入门的分步指南:  

- [将 Windows 10 部署到试点](/sccm/desktop-analytics/tutorial-windows10)  
