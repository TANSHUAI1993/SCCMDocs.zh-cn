---
title: "客户端安装方法 | Microsoft Docs"
description: "了解 System Center Configuration Manager 的客户端安装方法。"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: "9"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: edca31249cc2bb3e0c67265962815c82e3f4711e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的客户端安装方法

*适用范围：System Center Configuration Manager (Current Branch)*

你可以使用不同的方法安装 Configuration Manager 客户端软件。 可使用一种方法或多种方法的组合。 在本主题中，你可以阅读每种方法的相关内容，从而了解最适合组织的方法。  

## <a name="client-push-installation"></a>客户端请求安装  

 **支持的客户端平台：** Windows  

 **优点**  

-   可用于将客户端安装在一台计算机、一组计算机或查询到的计算机上。  

-   可用于自动将客户端安装在发现的所有计算机上。  

-   自动使用在“客户端请求安装属性”  对话框中的“客户端”  选项卡上定义的客户端安装属性。  

 **缺点**  

-   在推送到大型集合时，可能会导致网络流量很高。  

-   只能在 Configuration Manager 已发现的计算机上使用。  

-   无法用于在工作组中安装客户端。  

-   必须指定在目标客户端计算机中具有管理权限的客户端请求安装帐户。  

-   必须在客户端计算机上配置 Windows 防火墙例外，以便能够完成客户端请求安装。  

-   无法取消客户端请求安装。 在将此客户端安装方法用于站点时，Configuration Manager 会尝试将客户端安装在发现的所有资源上，并会重试任何失败的安装（不超过 7 天）。  

 有关安装方法的详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 Windows 计算机](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)。  

## <a name="software-update-point-based-installation"></a>基于软件更新点的安装  
 **支持的客户端平台：** Windows  

 **优点：**  

-   可以使用现有的软件更新基础架构来管理客户端软件。  

-   如果正确配置 Windows Server Update Services (WSUS) 和 Active Directory 域服务中的组策略设置，则可以自动在新计算机上安装客户端软件。  

-   在可以安装客户端之前，无需发现计算机。  

-   计算机可以读取已发布到 Active Directory 域服务的客户端安装属性。  

-   如果删除了客户端软件，将会重新安装它。  

-   你无需为目标客户端计算机配置和维护安装帐户。  

 **缺点：**  

-   需要正常运行的软件更新基础结构作为必备组件。  

-   必须将相同的服务器用于客户端安装和软件更新，而且此服务器必须位于主站点中。  

-   若要安装新的客户端，必须利用客户端的活动软件更新点和端口来配置 Active Directory 域服务中的组策略对象 (GPO)。  

-   如果没有为 Configuration Manager 扩展 Active Directory 架构，则必须使用组策略设置来设置计算机的客户端安装属性。  

 有关安装方法的详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 Windows 计算机](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)。  

## <a name="group-policy-installation"></a>组策略安装  
 **支持的客户端平台：** Windows  

 **优点：**  

-   在可以安装客户端之前，无需发现计算机。  

-   可用于安装新客户端或执行升级。  

-   计算机可以读取已发布到 Active Directory 域服务的客户端安装属性。  

-   你无需为目标客户端计算机配置和维护安装帐户。  

 **缺点：**  

-   如果安装大量客户端，可能会导致网络流量很高。  

-   如果没有为 Configuration Manager 扩展 Active Directory 架构，则必须使用组策略设置将客户端安装属性添加到站点中的计算机。  

 有关安装方法的详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 Windows 计算机](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)。  

## <a name="logon-script-installation"></a>登录脚本安装  
 **支持的客户端平台：** Windows  

 **优点：**  

-   在可以安装客户端之前，无需发现计算机。  

-   支持使用 CCMSetup 的命令行属性。  

 **缺点：**  

-   如果在短时间内安装大量客户端，可能会导致网络流量很高。  

-   如果用户并非经常登录到网络，则可能需要很长时间才能安装到所有客户端计算机。  

 有关安装方法的详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 Windows 计算机](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)。  

## <a name="manual-installation"></a>手动安装  
 **支持的客户端平台：**Windows、UNIX/Linux、Mac OS X  

 **优点：**  

-   在可以安装客户端之前，无需发现计算机。  

-   可用于测试目的。  

-   支持使用 CCMSetup 的命令行属性。  

 **缺点：**  

-   无自动化，因此耗费时间。  

 有关如何在每个平台上手动安装客户端的详细信息，请参阅以下内容：  

-   [如何在 System Center Configuration Manager 中将客户端部署到 Windows 计算机](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

-   [如何在 System Center Configuration Manager 中将客户端部署到 UNIX 和 Linux 服务器](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)  

-   [如何在 System Center Configuration Manager 中将客户端部署到 Mac](../../../../core/clients/deploy/deploy-clients-to-macs.md)  
