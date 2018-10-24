---
title: 产品生命周期仪表板
titleSuffix: Configuration Manager
description: 通过 Configuration Manager 中的产品生命周期仪表板查看 Microsoft 生命周期策略。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd1a3a56bac6d7917c70db731b1735a195fae3df
ms.sourcegitcommit: dfb2cb01c1608b848f2f2fee7c84500e7adcb7a4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "49101239"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>使用 Configuration Manager 管理 Microsoft 生命周期策略

*适用范围：System Center Configuration Manager (Current Branch)*

从版本 1806 开始，可以使用 Configuration Manager 产品生命周期仪表板来查看 Microsoft 生命周期策略。 该仪表板显示 Microsoft 产品（安装在由 Configuration Manager 托管的设备上）的 Microsoft 生命周期策略的状态。 它还提供有关环境中 Microsoft 产品的信息、可支持性状态以及支持结束日期。 使用仪表板了解对每个产品的支持的可用性。 这些信息有助于规划在到达当前支持结束日期之前，何时更新使用的 Microsoft 产品。  

有关详细信息，请参阅 [Microsoft 生命周期策略](https://support.microsoft.com/lifecycle)。



## <a name="prerequisites"></a>先决条件 

 若要查看产品生命周期仪表板中的数据，需要以下组件：  

- 必须在运行 Configuration Manager 控制台的计算机上安装 Internet Explorer 9 或更高版本。  

- 仪表板中的超链接功能需要一个 Reporting Services 点。 仪表板链接到 SQL Server Reporting Services (SSRS) 报表。 有关详细信息，请参阅 [Configuration Manager 中的报告](/sccm/core/servers/manage/reporting)。  

- 必须配置并同步资产智能同步点。 该仪表板使用资产智能目录作为产品标题的元数据。 元数据将与层次结构中的清单数据进行比较。 有关详细信息，请参阅[在 Configuration Manager 中配置资产智能](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence)。  

     > [!NOTE]  
     > 如果是首次配置资产智能服务点，请确保[启用资产智能硬件清单类](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence)。 生命周期仪表板的内容取决于这些资产智能硬件清单类。 在客户端扫描并返回硬件清单后，仪表板才会显示数据。  



## <a name="use-the-product-lifecycle-dashboard"></a>使用产品生命周期仪表板

根据站点从托管设备中收集的清单数据，仪表板将显示有关所有当前产品的信息。 但是，显示的有关操作系统和 SQL Server 的信息仅限于以下版本：

- Windows Server 2008 及更高版本
- Windows XP 及更高版本
- SQL Server 2008 及更高版本

若要访问 Configuration Manager 控制台中的生命周期仪表板，请转到“资产和符合性”工作区，展开“资产智能”并选择“产品生命周期”节点。

> [!NOTE]  
> 仪表板中的数据基于 Configuration Manager 控制台连接到的站点。 如果控制台连接到顶层站点，你会看到整个层次结构的数据。 当连接到子主站点时，只显示来自该站点的数据。

### <a name="product-lifecycle-dashboard"></a>产品生命周期仪表板

![控制台中的产品生命周期仪表板的屏幕截图](media/product-lifecycle-dashboard.png)

该仪表板具有以下磁贴：  

- **已过期的前五大产品**：此磁贴是一个整合的数据视图，显示在环境中找到的已过期的产品。 此图显示与操作系统及 SQL Server 产品的支持生命周期相比较已过期的已安装软件。  

- **即将过期的前五大产品**：此磁贴是一个整合的数据视图，显示在环境中找到的即将在十八个月内过期的产品。 此图显示与操作系统及 SQL Server 产品的支持生命周期相比较，将在十八个月内过期的已安装软件。  

- **已安装产品的生命周期数据**：通过此磁贴可大致了解产品从支持到过期状态的转换过程。 该图表详细介绍了在其中安装产品的客户端数量、支持可用性状态，并提供了一个链接，用于详细了解要执行的后续步骤。 图表中包含以下信息：     
    - 剩余支持时间
    - 环境中的数量 
    - 主流支持结束日期
    - 延长的支持结束日期
    - 后续步骤  

> [!IMPORTANT]  
> 为方便起见，我们提供了此仪表板中显示的信息，并且仅供公司内部使用。 不应仅依赖此信息来确认符合性。 请务必验证提供过来的信息的准确性，并通过访问 [Microsoft 生命周期策略](https://support.microsoft.com/lifecycle)来验证支持信息的可用性。  



## <a name="reporting"></a>报表

其他报表也同样可用。 在 Configuration Manager 控制台中，转到“监视”工作区，展开“报表”并展开“报表”节点。 在类别“产品生命周期”下添加以下新报表：  

- **常规产品生命周期概述**：查看产品生命周期列表。 按产品名称和有效期对列表进行筛选。  

- **具有特定软件产品的计算机**：查看在其中检测到指定产品的计算机列表。  

- **在组织中找到的已过期产品列表**：查看环境中生命周期已过期的产品的详细信息。  

- **组织中的具有过期产品的计算机列表**：查看具有过期产品的计算机。 可以按产品名称筛选此报表。

