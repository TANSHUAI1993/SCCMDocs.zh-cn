---
title: "评估 Configuration Manager | Microsoft Docs"
description: "创建实验室环境来评估 System Center Configuration Manager 在组织中的使用情况。"
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: "25"
caps.handback.revision: "0"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d7ea785ab1beee09b9adda735a87f89bc9481620
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>通过构建你自己的实验室环境来评估 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

 了解如何创建实验室环境来评估 System Center Configuration Manager 在组织中的使用。  

 System Center Configuration Manager 是一种功能全面的强大工具，用于管理用户、设备和软件。 在进行完整部署之前最好全面评估 System Center Configuration Manager，以便将概念性理解和实际练习相结合。  

 本指南主要针对在企业环境中评估 Configuration Manager 的使用情况的管理员：  

-   需要完全管理电脑、服务器和移动设备的解决方案的管理员  

-   既要求本地设备管理的安全性、又要求基于云的设备管理的灵活性的高安全性行业中的管理员  

-   需要扩大其本地服务器体系结构的管理员  

## <a name="what-this-lab-does"></a>此实验室能做什么  
 创建此实验室环境的主要目的是提供着手使用 Configuration Manager 所需的常规知识，并增强对 Configuration Manager 的理解。 将通过使用以下两台服务器引导用户快速组装 Configuration Manager 的当前版本：  

-   一台用于托管 Active Directory、域控制器和 DNS 服务器  

-   另一台用于托管 Configuration Manager 以及所有关联的 SQL Server 组件  

在 Hyper-V 内安装客户端计算机。 实验室本身也可以作为完全虚拟化的系统在一台服务器上运行。  

## <a name="what-this-lab-does-not-do"></a>此实验室不能做什么  
 此实验室不会向用户介绍所有 Configuration Manager 方案。 不能将此实验室立即迁移到活动环境中。  

 构建此实验室，你将获得一个用于工作的功能性环境。 但是，此环境不会针对系统性能、硬盘空间管理和 SQL Server 存储等因素进行优化。  

##  <a name="BKMK_EvalRec"></a> 构建实验室前的推荐读物  
 [System Center Configuration Manager 文档](http://docs.microsoft.com/sccm/)中提供了大量内容。 建议用户在开始构建实验室前，阅读此库的以下主题：  

-   在 [System Center Configuration Manager 简介](../../core/understand/introduction.md)中，可以了解 Configuration Manager 控制台、最终用户门户和示例方案的核心概念。  

-   在 [System Center Configuration Manager 的特性和功能](../../core/plan-design/changes/features-and-capabilities.md)中，可以了解 Configuration Manager 的主要管理功能。  

-   [System Center Configuration Manager 基础知识](../../core/understand/fundamentals.md)有助于巩固理解。  

-   在 [System Center Configuration Manager 的基于角色的管理基础](../../core/understand/fundamentals-of-role-based-administration.md)中，可以了解安全角色的重要性。  

-   在[内容管理的概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)中，可以了解内容管理。  

-   在[了解客户端如何为 System Center Configuration Manager 查找站点资源和服务](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)中，可以了解如何成功支持部署中的所有日常任务。  
