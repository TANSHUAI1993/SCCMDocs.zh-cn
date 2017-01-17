---
title: "添加站点系统角色 | Microsoft Docs"
description: "了解 Configuration Manager 站点系统角色，以及如何添加它们才能扩展站点的功能和容量。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
caps.latest.revision: 12
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e0cc69baa2fdc5bb9c1327c89840e28d0f885608


---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>添加 System Center Configuration Manager 的站点系统角色

*适用范围：System Center Configuration Manager (Current Branch)*

每个 System Center Configuration Manager 站点都支持多个站点系统角色，其中每个角色都可扩展站点的功能和容量，以便为设备和用户提供服务以及管理设备和用户。 站点系统服务器上的每个站点系统角色必须来自同一站点。   

Configuration Manager 不支持单一站点系统服务器上多个站点的站点系统角色。  

> [!TIP]  
>  如果你不熟悉站点系统角色的基础或站点服务器、站点系统服务器和站点系统角色之间的差别，请参阅 [Fundamentals of System Center Configuration Manager](../../../../core/understand/fundamentals.md)。  

 以下主题详细介绍了安装站点系统角色的过程和相关详细信息：  

-   [安装 System Center Configuration Manager 的站点系统角色](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     本主题提供有关使用可用于安装新站点系统角色的两个控制台内部向导的基本指南。  

-   [在 Microsoft Azure 中安装 System Center Configuration Manager 基于云的分发点](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    如果想要使用 Microsoft Azure 托管部署到客户端的内容，则本主题中的信息可帮助你配置所需证书文件，以使 Configuration Manager 可以与 Microsoft Azure 订阅通信并使用该订阅。 此外，你需要配置名称解析以便使客户端可以查找基于云的分发点。  

-   [在 System Center Configuration Manager 中为本地移动设备管理安装站点系统角色](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     本主题有助于你成功配置站点系统角色，以支持使用 Configuration Manager 本地 MDM 管理新式设备。  

-   [System Center Configuration Manager 站点系统角色的配置选项](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     某些站点系统角色支持的配置所需要的详细信息比用户界面中可以说明的详细信息更多。 本主题提供这些详细信息。  



<!--HONumber=Dec16_HO3-->


