---
title: "站点系统的网站 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的站点系统服务器的默认和自定义网站。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 886ff3b8e867fc340c79648a57feae81653b0ccd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的站点系统服务器网站

*适用范围：System Center Configuration Manager (Current Branch)*

多个 Configuration Manager 站点系统角色需要使用 Microsoft Internet Information Services (IIS) 和默认的 IIS 网站来托管站点系统服务。 当必须在同一服务器上运行其他 Web 应用程序，且设置与 Configuration Manager 不兼容时，请考虑使用 Configuration Manager 的自定义网站。  

> [!TIP]  
>  安全的最佳方案是将一台服务器专用于需要 IIS 的 Configuration Manager 站点系统。 在 Configuration Manager 站点系统上运行其他应用程序时，会增大该计算机的受攻击面。  




##  <a name="BKMK_What2Know"></a>选择使用自定义网站前的须知  
 默认情况下，站点系统角色使用 IIS 中的“默认网站”。 这会在站点系统角色安装时自动设置。 但在主站点上，可以转而选择使用自定义网站。 使用自定义网站时：  

-   为整个站点启用自定义网站，而不是为单独的站点系统服务器或角色启用。  

-   在主站点上，将承载适用的站点系统角色的每台计算机必须设置有名为 **SMSWEB** 的自定义网站。 在创建此网站且将此计算机上的站点系统角色设置为使用自定义网站之前，客户端可能无法与此计算机上的站点系统角色进行通信。  

-   由于当主父站点设置为使用自定义网站时，其辅助站点也会自动如此设置，因此还必须在每个需要 IIS 的辅助站点系统服务器上的 IIS 中创建自定义网站。  


  **使用自定义网站的先决条件：**  

 启用选项以使用站点的自定义网站之前，你必须：  

-   在每个需要 IIS 的站点系统服务器上的 IIS 中，创建名为 **SMSWEB** 的自定义网站。 在主站点和任何子辅助站点中执行此操作。  

-   设置自定义网站，以响应为 Configuration Manager 客户端通信设置的同一端口（客户端请求端口）。  

-   对于每个自定义网站或使用自定义文件夹的默认网站，请将所用的默认文档类型的副本放到承载网站的根文件夹中。 例如，在使用默认配置的 Windows Server 2008 R2 计算机上，**iisstart.htm** 是几种默认可用的文档类型之一。 可以在默认网站的根文件夹中找到此文件，然后将此文件的副本（或所用默认文档类型的副本）放到承载 SMSWEB 自定义网站的根文件夹中。 有关默认文档类型的详细信息，请参阅 [IIS 的默认文档 &lt;defaultDocument\>](http://www.iis.net/configreference/system.webserver/defaultdocument)。  

**关于 IIS 要求：**
**下列站点系统角色需要 IIS 和网站才能托管站点系统服务：**  

-   应用程序目录 Web 服务点  

-   应用程序目录网站点  

-   分发点  

-   注册点  

-   注册代理点  

-   回退状态点  

-   管理点  

-   软件更新点  

-   状态迁移点  

其他注意事项：  

-   当主站点启用了自定义网站时，分配到此站点的客户端将被定向为与自定义网站（而不是适用的站点系统服务器上的默认网站）进行通信  

-   如果对某个主站点使用自定义网站，请考虑为层次结构中的所有主站点使用自定义网站，以确保客户端可成功地在层次结构中漫游。 （当客户端计算机移动到不同站点托管的新网络段时进行漫游。 漫游可影响客户端可本地访问，而不是通过 WAN 链接访问的资源）。  

-   使用 IIS 但不接受客户端连接的站点系统角色（例如 Reporting Services 点）也使用 SMSWEB 网站，而非默认网站。  

-   自定义网站需要你指定不同于计算机默认网站所使用的端口号。 如果默认网站和自定义网站均尝试使用相同的 TCP/IP 端口，则它们无法同时运行。  

-   在 IIS 中为自定义网站设置的 TCP/IP 端口必须与此站点的客户端请求端口匹配。  

## <a name="switch-between-default-and-custom-websites"></a>在默认网站和自定义网站之间切换  
虽然你可随时选中或取消选中在主站点使用自定义网站的复选框（此复选框位于站点“属性”的“常规”选项卡上），但在进行此更改之前请仔细规划。 当此配置更改时，必须卸载主站点和子辅助站点中所有适用的站点系统角色，然后重新安装：  

以下角色将 **自动重新安装**：  

-   管理点  

-   分发点  

-   软件更新点  

-   回退状态点  

-   状态迁移点  

以下角色必须 **手动重新安装**：  

-   应用程序目录 Web 服务点  

-   应用程序目录网站点  

-   注册点  

-   注册代理点  

此外：  

-   从使用默认网站更改为使用自定义网站时，Configuration Manager 不会删除旧虚拟目录。 如果想删除 Configuration Manager 使用的文件，必须手动删除在默认网站下创建的虚拟目录。  

-   如果更改站点以使用自定义网站，则必须将已分配到站点的客户端重新配置为使用针对自定义网站的新客户端请求端口。 请参阅[如何在 System Center Configuration Manager 中配置客户端通信端口](../../../core/clients/deploy/configure-client-communication-ports.md)。  

## <a name="set-up-custom-websites"></a>设置自定义网站  
由于自定义网站的创建步骤随操作系统版本的不同而有所不同，所以请参阅你操作系统版本的文档以了解确切步骤，但请在适当时使用以下信息：  

-   网站名称必须是：**SMSWEB**。  

-   设置 HTTPS 时，必须先指定 SSL 证书才能保存配置。  

-   创建自定义网站后，请删除 IIS 中所用的其他网站的自定义网站端口：  

    1.  编辑其他网站的“绑定”，以删除与分配给 **SMSWEB** 网站的端口匹配的端口。  

    2.  启动 **SMSWEB** 网站。  

    3.  在站点的站点服务器上重启 **SMS_SITE_COMPONENT_MANAGER** 服务。  
