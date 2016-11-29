---
title: "站点系统网站 | System Center Configuration Manager"
description: "了解 System Center Configuration Manager 中的站点系统服务器的默认和自定义网站。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3f463aa804cb928b29fc26d9af8dede7f65222df


---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的站点系统服务器网站

*适用范围：System Center Configuration Manager (Current Branch)*

多个 Configuration Manager 站点系统角色需要使用 Microsoft Internet Information Services (IIS) 和默认的 IIS 网站来托管站点系统服务。 当必须在同一服务器上运行其他 Web 应用程序，且设置与 Configuration Manager 不兼容时，请考虑使用 Configuration Manager 的自定义网站。  

> [!TIP]  
>  最佳安全方案是，将一台服务器专用于需要 IIS 的 Configuration Manager 站点系统。 在 Configuration Manager 站点系统上运行其他应用程序时，会增大该计算机的受攻击面。  




##  <a name="a-namebkmkwhat2knowa-what-to-know-before-choosing-to-use-custom-websites"></a><a name="BKMK_What2Know"></a>选择使用自定义网站前的须知  
 默认情况下，站点系统角色使用 IIS 中的“默认网站”。 安装站点系统角色时自动配置。 但在主站点上，可以转而选择使用自定义网站。 使用自定义网站时：  

-   为整个站点启用了自定义网站，而不是为单独的站点系统服务器或角色启用。  

-   在主站点，将承载合适站点系统角色的每台计算机必须配置有名为 **SMSWEB** 的自定义网站。 在创建此网站且将此计算机上的站点系统角色配置为使用自定义网站之前，客户端不能与此计算机上的站点系统角色进行通信。  

-   由于当主父站点配置为使用自定义网站时，其辅助站点也会自动如此配置，所以你还必须在每个需要 IIS 的辅助站点系统服务器上创建 IIS 中的自定义网站。  


  **使用自定义网站的先决条件：**  

 启用选项以使用站点的自定义网站之前，你必须：  

-   在每个需要 IIS 的站点系统服务器上的 IIS 中，创建名为 **SMSWEB** 的自定义网站。 在主站点和任何子辅助站点中执行此操作。  

-   配置自定义网站，以响应为 Configuration Manager 客户端通信配置的同一端口（客户端请求端口）。  

-   对于每个自定义网站或使用自定义文件夹的默认网站，将所用的默认文档类型的副本放到托管网站的根文件夹中。 例如，在使用默认配置的 Windows Server 2008 R2 计算机上， **iisstart.htm** 是几种默认可用的文档类型之一。 可以在默认网站的根目录中找到此文件，然后将此文件副本（或所用默认文档类型的副本）放到承载 SMSWEB 自定义网站的根文件夹中。 有关默认文档类型的详细信息，请参阅 [IIS 的默认文档 &lt;defaultDocument\>](http://www.iis.net/configreference/system.webserver/defaultdocument)。  

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

-   在主站点启用了自定义网站时，分配到此站点的客户端将定向为与自定义网站（而不是合适站点系统服务器上的默认网站）进行通信  

-   如果将对某个主站点使用自定义网站，请考虑对层次结构中的所有主站点使用自定义网站，以确保客户端可在层次结构中成功漫游。 （当客户端计算机移动到不同站点托管的新网络段时进行漫游。 漫游可影响客户端可本地访问，而不是通过 WAN 链接访问的资源类型）。  

-   使用 IIS 但不接受客户端连接的站点系统角色（例如 Reporting Services 点）也使用 SMSWEB 网站而非默认网站  

-   自定义网站要求指定不同于计算机默认网站所使用的端口号。 如果默认网站和自定义网站均尝试使用相同的 TCP/IP 端口，则它们无法同时运行。  

-   在 IIS 中为自定义网站配置的 TCP/IP 端口必须与此站点的客户端请求端口匹配。  

## <a name="switching-between-default-and-custom-websites"></a>在默认网站和自定义网站之间切换  
虽然你可选择或清除可随时在主站点使用自定义网站的复选框（此复选框位于站点“属性”的“常规”选项卡上），但请在进行此更改时仔细规划。 当此配置更改时，必须卸载再重新安装主站点和子辅助站点中所有合适的站点系统角色：  

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

-   如果更改站点以使用自定义网站，则必须将已分配给站点的客户端重新配置为使用针对自定义网站的新客户端请求端口。 请参阅[如何在 System Center Configuration Manager 中配置客户端通信端口](../../../core/clients/deploy/configure-client-communication-ports.md)  

## <a name="configure-custom-websites"></a>配置自定义网站  
由于自定义网站的创建步骤随操作系统版本的不同而有所不同，所以请参阅你操作系统版本的文档以了解确切步骤，但请在适当时使用以下信息：  

-   网站名称必须是 **SMSWEB**  

-   配置 HTTPS 时，必须先指定 SSL 证书才能保存配置  

-   创建自定义网站后，请删除 IIS 中所用的其他网站的自定义网站端口：  

    1.  编辑其他网站的“绑定”  ，以删除与分配给 **SMSWEB** 网站的端口匹配的端口。  

    2.  启动 **SMSWEB** 网站  

    3.  在站点的站点服务器上重启 **SMS_SITE_COMPONENT_MANAGER** 服务。  



<!--HONumber=Nov16_HO1-->


