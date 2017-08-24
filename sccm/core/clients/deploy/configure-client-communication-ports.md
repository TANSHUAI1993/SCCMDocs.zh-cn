---
title: "配置客户端通信端口 | Microsoft Docs"
description: "在 System Center Configuration Manager 设置客户端通信端口。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstack
ms.author: robstackmsft
manager: angrobe
ms.openlocfilehash: 63e033fdb436930ac5f37e7408ca9292bc444560
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-communication-ports-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中配置客户端通信端口

*适用范围：System Center Configuration Manager (Current Branch)*

可以更改 System Center Configuration Manager 客户端用来与使用 HTTP 和 HTTPS 进行通信的站点系统通信的请求端口号。 虽然为防火墙配置了 HTTP 或 HTTPS 的可能性更高，但是，与使用自定义端口号相比，使用 HTTP 或 HTTPS 的客户端通知在管理点计算机上将需要使用更多的 CPU 资源和内存。 如果通过使用传统的唤醒数据包唤醒客户端，则还可以指定要使用的站点端口号。  

 在指定 HTTP 和 HTTPS 请求端口时，可以指定默认端口号和备用端口号。 在使用默认端口通信失败后，客户端会自动尝试使用备用端口。 可以指定 HTTP 和 HTTPS 数据通信的设置。  

 客户端请求端口的默认值是 **80** （对于 HTTP 流量）和 **443** （对于 HTTPS 流量）。 仅在你不想使用这两个默认值时才更改它们。 使用自定义端口的典型情况是，你在 IIS 中使用自定义网站而不是默认网站。 如果更改 IIS 中的默认网站的默认端口号，而其他应用程序也使用此默认网站，则它们可能会失败。  

> [!IMPORTANT]  
>  不要在不了解后果的情况下更改 Configuration Manager 中的端口号。 例如：  
>   
>  -   如果在站点配置中更改客户端请求服务的端口号，而且没有重新配置现有的客户端以使用新的端口号，则这些客户端将变为非管理的客户端。  
> -   在配置非默认的端口号之前，请确保防火墙和所有介入性网络设备都能支持此配置，并在必要时对它们进行重新配置。 如果你将在 Internet 上管理客户端，并且更改默认的 HTTPS 端口号 443，则 Internet 上的路由器和防火墙可能会阻止此通信。  

 为了确保在你更改请求端口号后客户端不会变为非管理的客户端，必须配置客户端以使用新的请求端口号。 在更改主站点上的请求端口时，任何连接的辅助站点均会自动继承相同的端口配置。 使用本主题中的过程来配置主站点上的请求端口。  

> [!NOTE]  
>  有关如何为运行 Linux 和 UNIX 的计算机上的客户端配置请求端口的信息，请参阅[为适用于 Linux 和 UNIX 的客户端配置请求端口](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations)。  

 当 Configuration Manager 站点发布到 Active Directory 域服务时，可以访问此信息的新客户端和现有客户端将自动配置为它们的站点端口设置，并且您无需采取其他操作。 无法访问发布到 Active Directory 域服务的此信息的客户端包括：工作组客户端、其他 Active Directory 林中的客户端、配置为仅通过 Internet 进行管理的客户端，以及目前位于 Internet 上的客户端。 如果在已安装这些客户端后更改默认端口号，请使用以下方法之一重新安装这些客户端和安装任何新的客户端：  

-   使用“客户端请求安装向导”重新安装客户端。 客户端请求安装会自动使用当前的站点端口配置来配置客户端。 有关如何使用“客户端请求安装向导”的详细信息，请参阅[如何使用客户端请求安装 Configuration Manager 客户端](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。  

-   使用 CCMSetup.exe 以及 CCMHTTPPORT 和 CCMHTTPSPORT 的 client.msi 安装属性来重新安装客户端。 有关这些属性的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

-   使用搜索 Active Directory 域服务以查找 Configuration Manager 客户端安装属性这一方法来重新安装客户端。 有关详细信息，请参阅[关于 System Center Configuration Manager 中的发布到 Active Directory 域服务的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)。  

 若要重新配置现有客户端的端口号，你也可以使用随安装媒体提供的且位于 SMSSETUP\Tools\PortConfiguration 文件夹中的脚本 PORTSWITCH.VBS。  

> [!IMPORTANT]  
>  对于当前在 Internet 上的现有客户端和新客户端，你必须使用 CCMHTTPPORT 和 CCMHTTPSPORT 的 CCMSetup.exe client.msi 属性来配置非默认端口号。  

 更改站点上的请求端口后，使用覆盖整个站点的客户端请求安装方法安装的新客户端将自动配置为站点的当前端口号。  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>配置站点的客户端通信端口号  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置” ，单击“站点” ，然后选择要配置的主站点。  

3.  在“主页”  选项卡上，单击“属性” ，再单击“端口”  选项卡。  

4.  选择任意项，然后单击“属性”图标以显示“端口详细信息”  对话框。  

5.  在“端口详细信息”  对话框中，指定该项的端口号和描述，然后单击“确定” 。  

6.  若要将自定义网站名称 **SMSWeb** 用于运行 IIS 的站点系统，请选择“使用自定义网站”  。  

7.  单击“确定”  以关闭站点的属性对话框。  

 为层次结构中的所有主站点重复此过程。
