---
title: 软件更新的最佳方案
titleSuffix: Configuration Manager
description: 使用这些 Configuration Manager 中软件更新的最佳做法。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb5471c5a993a1a2f683807a12dfc01ea00bf275
ms.sourcegitcommit: 5ee9487c891c37916294bd34a10d04e398f111f7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59069511"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Configuration Manager 中软件更新的最佳做法

*适用范围：System Center Configuration Manager (Current Branch)*

本文介绍 Configuration Manager 中软件更新的最佳做法。 此信息分类为初始安装和当前操作的最佳做法。  



## <a name="bkmk_install"></a> 安装最佳做法  

在 Configuration Manager 中安装软件更新时，请使用下列最佳做法。  


### <a name="bkmk_shared-susdb"></a> 将共享 WSUS 数据库用于软件更新点  

在主站点上安装多个软件更新点时，请为同一 Active Directory 林中的每个软件更新点使用同一 WSUS 数据库。 如果共享相同的数据库，则可以起到显著的缓解作用，但并不能在客户端切换到新软件更新点时完全消除可能对客户端和网络性能产生的影响。 当客户端切换到与旧软件更新点共享数据库的新软件更新点时，仍然会进行增量扫描，但与 WSUS 服务器使用自己的数据库相比，扫描工作量会低很多。 有关软件更新点切换的详细信息，请参阅[软件更新点切换](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching)。  

> [!IMPORTANT]  
>  将共享的 WSUS 数据库用于软件更新点时，请共享本地 WSUS 内容文件夹。  

若要详细了解 WSUS 数据库共享，请参阅以下博客文章：  

- [How to implement a shared SUSDB for Configuration Manager software update points](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)（如何为 Configuration Manager 软件更新点实现共享 SUSDB）  

- [Considerations for multiple WSUS instances sharing a content database when using System Center Configuration Manager](https://blogs.technet.microsoft.com/wsus/2014/03/22/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb/)（在使用 System Center Configuration Manager 时共享内容数据库的多个 WSUS 实例的注意事项）  


### <a name="bkmk_sql-instance"></a> 当 Configuration Manager 和 WSUS 使用同一 SQL Server 时，请将其中的一个配置为使用命名实例，并将另一个配置为使用默认实例  

当 Configuration Manager 和 WSUS 数据库共享 SQL Server 的同一实例时，无法轻松确定两个应用程序之间的资源使用情况。 将不同 SQL Server 实例用于 Configuration Manager 和 WSUS。 此配置能更轻松地解决和诊断每个应用程序可能发生的资源使用问题。  


### <a name="bkmk_store-local"></a> 指定“在本地存储更新”设置  

安装 WSUS 时，请选择“在本地存储更新”设置。 此设置会让 WSUS 下载与软件更新关联的许可条款。 它会在同步过程中下载这些条款，并将它们存储在 WSUS 服务器的本地硬盘上。 如果未选择此设置，客户端计算机可能无法扫描具备许可条款的软件更新的符合性。 默认情况下，软件更新点的 WSUS 同步管理器组件每隔 60 分钟会验证一次是否启用了此设置。  



## <a name="bkmk_operation"></a> 操作最佳做法  

在使用软件更新时，请使用下列最佳方案：  


### <a name="bkmk_object-limit"></a> 将单个软件更新部署中的软件更新数限制为 1000  

将每个软件更新部署中的软件更新数量限制为 1000。 在创建自动部署规则时，请验证所指定的条件是否会产生超过 1000 个软件更新。 在手动部署软件更新时，请勿选择超过 1000 个的更新。  


### <a name="bkmk_new-group"></a> 每当为“周二补丁日”和一般部署运行 ADR 时，创建新的软件更新组  

在部署中，对软件更新数存在 1000 个的限制。 在创建自动部署规则 (ADR) 时，指定是使用现有更新组还是在规则每次运行时创建新的更新组。 如果在 ADR 中指定的条件产生多个软件更新，并且规则定期运行，则在规则每次运行时创建新的软件更新组。 此行为能防止部署中的软件更新数超过 1000 个的限制。  


### <a name="bkmk_same-group"></a> 为 Endpoint Protection 定义更新的 ADR 使用现有软件更新组  

如果经常使用 ADR 来部署 Endpoint Protection 定义更新，请始终使用现有的软件更新组。 否则，ADR 可能会在一段时间内创建数百个软件更新组。 定义更新发布者通常会在定义更新被四个较新的更新取代时将其设置为过期。 因此，ADR 创建的软件更新组最多只能包含发布者的 4 个定义更新：1 个活动更新和 3 个被取代的更新。  



## <a name="see-also"></a>另请参阅  
 [规划软件更新](/sccm/sum/plan-design/plan-for-software-updates)
