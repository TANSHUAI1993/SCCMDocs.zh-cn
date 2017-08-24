---
title: "站点和层次结构基础知识 | Microsoft Docs"
description: "获取有关 System Center Configuration Manager 站点和层次结构的基本信息。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: f13f38be2a19ab8a1ead246e5272515dd0570984
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-sites-and-hierarchies-for-system-center-configuration-manager"></a>System Center Configuration Manager 的站点和层次结构基础知识

*适用范围：System Center Configuration Manager (Current Branch)*

必须在 Active Directory 域中安装 System Center Configuration Manager 部署。 此部署的基础包括组成站点层次结构的一个或多个 Configuration Manager 站点。 从单站点到多站点层次结构，安装的站点类型和位置在必要时提供扩展（扩大）部署的能力，并向托管用户和设备提供重要服务。

## <a name="hierarchies-of-sites"></a>站点的层次结构
首次安装 System Center Configuration Manager 时，安装的第一个 Configuration Manager 站点将确定层次结构的作用域。 将以第一个 Configuration Manager 为基础管理企业中的设备和用户。 此第一个站点必须为管理中心站点或独立主站点。  

 *管理中心站点*适合大规模部署，并能集中管理和灵活地支持分布在全局网络基础架构中的设备。 安装管理中心站点后，将需要安装一个或多个主站点作为子站点。 此配置时必须的，因为管理中心站点不直接支持设备管理（这是主站点的功能）。 一个管理中心站点支持多个子主站点。 当托管设备处于不同地理位置时，可用这些子主站点直接管理设备和控制网络带宽。  

 *独立主站点*适合较小规模的部署，可用来管理设备而无需安装其他站点。 尽管独立主站点可以限制部署的大小，但它支持通过安装新的管理中心站点在稍后扩展层次结构的方案。 使用此站点扩展方案时，独立主站点将成为子主站点，你可以在新的管理中心站点下安装其他子主站点。 然后可以扩展初始部署以应对企业的未来增长。  

> [!TIP]  
>  独立主站点和子主站点实际上属于同一类型的站点：主站点。 名称差异基于某类层次结构关系，当你同时使用管理中心站点时会创建这一关系。 此层次结构关系还可能限制可扩展 Configuration Manager 功能的某些站点系统角色的安装。 角色的此限制出现的原因是，某些站点系统角色只能安装在层次结构的顶层站点上，即管理中心站点或独立主站点上。  

 安装第一个站点后，即可安装其他站点。 如果第一个站点是管理中心站点，则可安装一个或多个子主站点。 安装主站点（独立主站点或子主站点）后，即可安装一个或多个辅助站点。  

 “辅助站点”只能作为子站点安装在主站点下。 此站点类型可对主站点进行扩展，使其可管理通过慢速网络连接到主站点的位置的设备。 即使辅助站点扩展主站点，主站点仍管理所有客户端。 辅助站点对位于远程位置的设备提供支持。 辅助站点提供此支持的方法是：通过对网络中发送（部署）到客户端的信息和客户端发送回站点的信息的传输进行压缩和管理。  

 下图显示了一些示例站点设计。  

 ![层次结构示例](media/Hierarchy_examples.png)  

 有关详细信息，请参阅下列主题：  

-   [System Center Configuration Manager 简介](../../core/understand/introduction.md)  

-   [为 System Center Configuration Manager 设计站点层次结构](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [安装 System Center Configuration Manager 站点](/sccm/core/servers/deploy/install/installing-sites)  

## <a name="site-system-servers-and-site-system-roles"></a>站点系统服务器和站点系统角色  
 每个 Configuration Manager 站点都将安装支持管理操作的*站点系统角色*。 安装站点时，将默认安装以下角色：

-   将向安装站点的计算机分配站点服务器角色。

-   将向托管站点数据库的 SQL Server 分配站点数据库服务器角色。

其他站点系统角色是可选的，仅在你希望使用站点系统角色中活动的功能时使用。 托管站点系统角色的任何计算机都称为站点系统服务器。  

 对于 Configuration Manager 的较小部署，可在站点服务器计算机上直接初始运行所有站点系统角色。 然后，随着管理的环境规模的扩大以及需求的增长，你可以相应安装更多站点系统服务器来托管增加的站点系统角色，以改进站点向更多设备提供服务的效率。  

 有关不同的站点系统角色的信息，请参阅 [为 System Center Configuration Manager 规划站点系统服务器和站点系统角色](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)中的[站点系统角色](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)。

## <a name="publishing-site-information-to-active-directory-domain-services"></a>将站点信息发布到 Active Directory 域服务  
 为简化 Configuration Manager 的管理，可将 Active Directory 架构扩展为支持 Configuration Manager 所使用的详细信息，然后让站点将其关键信息发布到 Active Directory 域服务 (AD DS)。 然后，你想管理的计算机可从受信任的 AD DS 来源安全检索站点相关信息。 客户端可检索的信息将标识可用站点、站点系统服务器以及这些站点系统服务器提供的服务。  

 *扩展 Active Directory 架构*对于每个林只执行一次，且可在 Configuration Manager 安装前和安装后执行。   扩展架构之后，必须在每个域中创建名为“系统管理”的新 Active Directory 容器。 此容器包含一个 Configuration Manager 站点，它会发布数据以供客户端查找。 有关详细信息，请参阅[为站点发布准备 Active Directory](../../core/plan-design/network/extend-the-active-directory-schema.md)。  

 *发布站点数据*可提高 Configuration Manager 层次结构的安全性并减少管理开销，但不是基本 Configuration Manager 功能所必需的。  
