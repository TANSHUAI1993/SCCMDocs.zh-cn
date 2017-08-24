---
title: "添加站点系统角色 | Microsoft Docs"
description: "了解 Configuration Manager 站点系统角色，以及如何添加它们以扩展站点的功能和容量。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1ad4abf1f06ed24bd1d505648280b5e5d80220c7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>添加 System Center Configuration Manager 的站点系统角色

*适用范围：System Center Configuration Manager (Current Branch)*

每个 System Center Configuration Manager 站点支持多个站点系统角色。 每个角色可扩展站点的功能和容量，以为站点提供服务并管理设备和用户。 站点系统服务器上的每个站点系统角色必须来自同一站点。   

Configuration Manager 不支持单一站点系统服务器上多个站点的站点系统角色。  

> [!TIP]  
>  如果不熟悉站点系统角色的基础知识或站点服务器、站点系统服务器和站点系统角色之间的差别，请参阅 [System Center Configuration Manager 基础知识](../../../../core/understand/fundamentals.md)。  

 以下主题详细介绍了安装站点系统角色的过程和相关详细信息：  

-   [安装 System Center Configuration Manager 的站点系统角色](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     本主题提供有关使用可用于安装新站点系统角色的两个控制台中向导的基本指南。  

-   [在 Microsoft Azure 中安装 System Center Configuration Manager 基于云的分发点](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    如果想要使用 Microsoft Azure 托管部署到客户端的内容，则本主题中的信息可帮助你设置所需证书文件，以使 Configuration Manager 可以与 Microsoft Azure 订阅通信并使用该订阅。 此外，需要设置名称解析使客户端可以查找基于云的分发点。  

-   [在 System Center Configuration Manager 中为本地移动设备管理安装站点系统角色](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     本主题有助于你成功设置站点系统角色，以支持使用 Configuration Manager 本地 MDM 管理新式设备。  

-   [System Center Configuration Manager 站点系统角色的配置选项](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     某些站点系统角色支持需要比用户界面中可以说明的更多详细信息的配置。 本主题提供这些详细信息。  
