---
title: "通过构建你自己的实验室环境来评估 System Center Configuration Manager | Microsoft Docs"
description: "创建实验室环境来评估 System Center Configuration Manager 在组织中的使用情况。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: 25
caps.handback.revision: 0
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: e72acbe0a2f5592b5bdf9a3612db62bfb066fadf


---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>通过构建你自己的实验室环境来评估 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

了解如何创建实验室环境来评估 System Center Configuration Manager 在组织中的使用。  

## <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>通过构建你自己的实验室环境来评估 System Center Configuration Manager  
 System Center Configuration Manager 是一种功能全面的强大工具，用于管理用户、设备和软件。 建议在进行完整部署之前应完成 System Center Configuration Manager 的全面评估，以便将概念性理解和实际练习相结合。  

 本指南主要针对评估企业环境中 Configuration Manager 的使用情况的管理员。  

-   正在寻找用于完全管理 PC、服务器和移动设备的解决方案的管理员  

-   既要求本地设备管理的安全性、又要求基于云的设备管理的灵活性的高安全性行业中的管理员  

-   希望能够扩大本地服务器体系结构的管理员  

### <a name="what-this-lab-does"></a>此实验室能做什么  
 创建此环境的主要目的是提供着手使用 Configuration Manager所需的常规知识，并通过操作增强对 Configuration Manager 的理解。 通过引导用户快速组装 Configuration Manager 的当前版本来实现这一目标，并且将使用两台服务器：  

-   一台用于托管 Active Directory、域控制器和 DNS 服务器  

-   另一台用于托管 Configuration Manager 以及所有关联的 SQL Server 组件。  

-   在 Hyper-V 内安装客户端计算机。 实验室本身也可以作为完全虚拟化的系统在一台服务器上运行。  

### <a name="what-this-lab-does-not-do"></a>此实验室不能做什么  
 此实验室不会逐一演示所有的 Configuration Manager 方案，且不适合立即迁移到活动环境中。  

 构建此实验室，你将获得一个用于工作的功能性环境。 但是，此环境将不针对系统性能、硬盘空间管理、SQL Server 存储等进行优化。  

###  <a name="a-namebkmkevalreca-recommended-reading-prior-to-beginning-the-lab"></a><a name="BKMK_EvalRec"></a> 开始构建实验室前推荐阅读的内容  
 [System Center Configuration Manager 文档](http://docs.microsoft.com/sccm/)中提供了大量有价值的内容。 以下包含了此库中的精选主题，建议所有从事实验工作的管理员在开始这些练习之前阅读这些主题。  

-   在 [System Center Configuration Manager 简介](../../core/understand/introduction.md)中，可以了解 Configuration Manager 控制台、最终用户门户和示例方案的核心概念  

-   在 [System Center Configuration Manager 的特性和功能 ](../../core/plan-design/changes/features-and-capabilities.md)中，可以了解 Configuration Manager 的主要管理功能  

-   [System Center Configuration Manager 基础知识](../../core/understand/fundamentals.md)有助于巩固理解  

-   在 [System Center Configuration Manager 的基于角色的管理基础](../../core/understand/fundamentals-of-role-based-administration.md)中，可以了解安全角色的重要性  

-   理解这些[内容管理的概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)，以此来了解与内容管理相关的特定概念  

-   [了解客户端如何为 System Center Configuration Manager 查找站点资源和服务](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)，以便成功支持部署中的所有日常操作  



<!--HONumber=Dec16_HO3-->


