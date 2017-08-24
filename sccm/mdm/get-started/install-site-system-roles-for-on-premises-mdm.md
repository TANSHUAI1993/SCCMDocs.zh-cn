---
title: "为本地 MDM 安装角色 - Configuration Manager | Microsoft Docs"
description: "在 System Center Configuration Manager 中为本地移动设备管理安装站点系统角色。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
caps.latest.revision: "9"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4913606e2f8a36e0004f711b24ecd836d0485124
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中为本地移动设备管理安装站点系统角色

*适用范围：System Center Configuration Manager (Current Branch)*

本地移动设备管理上的 System Center Configuration Manager 需要 Configuration Manager 站点基础结构中的下列站点系统角色：  

-   注册点  

-   注册代理点  

-   分发点  

-   设备管理点  

-   服务连接点  

 如果组织中的大多数电脑和设备都是使用 Configuration Manager 客户端软件进行管理的，则向组织添加本地移动设备管理时，可能要求现有的基础结构中已安装大多数站点系统角色。 如果没有，请参阅[为 System Center Configuration Manager 添加站点系统角色](../../core/servers/deploy/configure/add-site-system-roles.md)，了解如何向站点添加站点系统角色的完整信息。  

> [!NOTE]  
>  如果你以设备管理点站点系统角色使用数据库副本，那么新注册的设备最初无法连接到设备管理点，直到数据库副本与之同步。 此连接失败的原因是数据库副本没有建立成功连接所需的新注册设备的信息。 副本每 5 分钟同步一次，因此设备在注册之后的最初 5 分钟将无法连接（通常尝试 2 次连接），在此之后设备将成功连接。  

 无论使用现有站点系统角色还是添加新角色，你都必须将其配置用于管理新式设备。 按照下列步骤配置分发点和设备管理点，使它们在本地移动设备管理上正常工作：  

> [!NOTE]  
>  Configuration Manager 的 Current Branch 仅支持从设备到分发点和设备管理点的 Intranet 连接，以便进行本地移动设备管理。 但是，如果你还管理着 Mac OS X 计算机，则这些客户端将需要通过 Internet 连接到这些站点系统角色。 在这种情况下，配置分发点和设备管理点的属性时应改用“允许 Intranet 和 Internet 连接”设置。  

### <a name="to-configure-site-system-roles-to-manage-modern-devices"></a>若要配置站点系统角色以管理新式设备：  

1.  在 Configuration Manager 控制台中，单击“管理” > “概述” > “站点配置” > “服务器和站点系统角色”。  

2.  选择具有想要配置的分发点或设备管理点的站点系统服务器，打开“站点系统”的属性并确保其已指定 FQDN。 单击" **确定**"。  

3.  打开分发点站点系统角色的属性。 在“常规”选项卡上，确保选中“HTTPS”，并选择“仅允许 Intranet 连接”。  

     如果还通过 Configuration Manager 客户端单独管理着 Mac 计算机，请改用“允许 Intranet 和 Internet 连接”。  

    > [!NOTE]  
    >  为 Intranet 连接配置的分发点需要为其配置站点边界。 Configuration Manager 的 Current Branch 仅支持用于本地移动设备管理的 IPv4 范围边界。 有关配置站点边界的详细信息，请参阅[为 System Center Configuration Manager 定义站点边界和边界组](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。  

4.  单击“允许移动设备连接到此分发点”旁边的复选框，然后单击“确定”。  

5.  打开管理点站点系统角色的属性。 在“常规”选项卡上，确保选中“HTTPS”，并选择“仅允许 Intranet 连接”。  

     如果还通过 Configuration Manager 客户端单独管理着 Mac 计算机，请改用“允许 Intranet 和 Internet 连接”。  

6.  单击“允许移动设备和 Mac 计算机使用此管理点”旁的复选框。 单击" **确定**"。  

     这会将该管理点有效地变为设备管理点。  

 添加站点系统角色并将其配置用于管理新式设备后，需要将承载该角色的服务器配置为受信任终结点，以便注册托管设备并与之通信。 有关详细信息，请参阅 [为 System Center Configuration Manager 中的本地移动设备管理的受信任通信设置证书](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)。  
