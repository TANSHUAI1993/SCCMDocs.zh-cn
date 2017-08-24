---
title: "软件更新的最佳方案 | Microsoft Docs"
description: "使用 System Center Configuration Manager 中软件更新的最佳做法。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: 5df20f3703442de1be6220ca2770e182e330c036
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-software-updates-in-system-center-configuration-manager"></a>System Center Configuration Manager 中软件更新的最佳方案

*适用范围：System Center Configuration Manager (Current Branch)*

本主题包括 System Center Configuration Manager 中软件更新的最佳做法。 此信息分类为初始安装和当前操作的最佳方案。  

## <a name="installation-best-practices"></a>安装最佳方案  
 在 Configuration Manager 中安装软件更新时，请使用下列最佳做法。  

### <a name="use-a-shared-wsus-database-for-software-update-points"></a>为软件更新点使用共享 WSUS 数据库  
 在主站点上安装多个软件更新点时，请为同一 Active Directory 林中的每个软件更新点使用同一 WSUS 数据库。 通过共享同一数据库，你可以明显减轻在客户端切换到新软件更新点时可能产生的客户端和网络性能影响。 当客户端切换到与旧软件更新点共享数据库的新软件更新点时，仍会进行增量扫描，但此扫描相对于在 WSUS 服务器有自己的数据库的情况下所进行的扫描要小很多。  

> [!IMPORTANT]  
>  为软件更新点使用共享的 WSUS 数据库时，还必须共享本地 WSUS 内容文件夹。  

 有关软件更新点切换的详细信息，请参阅[在 System Center Configuration Manager 中规划软件更新](../../sum/plan-design/plan-for-software-updates.md)主题中的[软件更新点切换](../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching)部分。  

### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-of-these-to-use-a-named-instance-and-the-other-to-use-the-default-instance-of-sql-server"></a>当 Configuration Manager 和 WSUS 使用同一 SQL Server 时，请将其中的一个配置为使用命名实例，并将另一个配置为使用 SQL Server 的默认实例  
 当 Configuration Manager 和 WSUS 数据库使用同一 SQL Server 并共享 SQL Server 的同一实例时，将无法轻松确定两个应用程序之间的资源使用情况。 如果为 Configuration Manager 和 WSUS 使用不同的 SQL Server 实例，将可以更轻松地解决和诊断每个应用程序可能发生的资源使用问题。  

### <a name="specify-the-store-updates-locally-setting-for-the-wsus-installation"></a>为 WSUS 安装指定“本地存储更新”设置  
 当安装 WSUS 时，选择“本地存储更新”设置。 如果选择此设置，则会在同步过程中下载与软件更新关联的许可条款，并存储在 WSUS 服务器的本地硬盘驱动器上。 如果未选择此设置，则客户端计算机可能无法扫描具有许可条款的软件更新的软件更新符合性。 当你安装软件更新点时，WSUS Synchronization Manager 默认情况下将每隔 60 分钟验证一次是否启用了此设置。  

## <a name="operational-best-practices"></a>操作最佳方案  
 在使用软件更新时，请使用下列最佳方案：  

### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a>将单个软件更新部署中的软件更新数限制为 1000  
 你必须为每个软件更新部署将软件更新数限制为 1000。 在创建自动部署规则时，请验证你指定的条件不会产生超过 1000 个软件更新。 在手动部署软件更新时，请不要选择超过 1000 个更新进行部署。  

### <a name="create-a-new-software-update-group-each-time-an-automatic-deployment-rule-runs-for-patch-tuesday-and-for-general-deployment"></a>每当自动部署规则为“Patch Tuesday”和一般部署运行时，创建新的软件更新组  
 软件更新部署的软件更新数限制为 1000 个。 在创建自动部署规则时，将指定是使用现有更新组还是在规则每次运行时创建新更新组。 如果在自动部署规则中指定的条件产生多个软件更新，并且规则定期运行，请指定在规则每次运行时创建新的软件更新组。 这将防止部署超过每个部署 1000 个软件更新的限制。  

### <a name="use-an-existing-software-update-group-for-automatic-deployment-rules-for-endpoint-protection-definition-updates"></a>为 Endpoint Protection 定义更新的自动部署规则使用现有软件更新组  
 如果经常使用自动部署规则来部署 Endpoint Protection 定义更新，请始终使用现有软件更新组。 否则，可能会在一段时间内创建数百个软件更新组。 通常，定义更新发布者会将定义更新设置为在被四个较新的更新取代时过期。 因此，自动部署规则创建的软件更新组最多只能包含发布者的 4 个定义更新：1 个活动更新和 3 个被取代的更新。  

## <a name="see-also"></a>另请参阅  
 [在 System Center Configuration Manager 中规划软件更新](../../sum/plan-design/plan-for-software-updates.md)
