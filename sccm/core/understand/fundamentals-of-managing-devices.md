---
title: "管理设备的基础知识 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 管理设备。"
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 17b36eae97272c408fce20e1f88812dafc984773
ms.openlocfilehash: b907975db5b5ffa6fefef58902319b987e57dca6


---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理设备的基础知识

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 可管理两大类设备：

**客户端**是安装了 Configuration Manage 客户端软件的设备，例如工作站、笔记本电脑、服务器和移动设备。 某些管理功能（例如硬件清单）需要此客户端软件。  

**托管设备**可包括*客户端*，但通常表示没有安装 Configuration Manager 客户端软件，且用户通过使用 Microsoft Intune 或使用 Configuration Manager 的内置本地移动设备管理对其进行管理的移动设备。

也可以基于用户（而不仅仅基于客户端类型）来组合和识别设备。

## <a name="managing-devices-with-the-configuration-manager-client"></a>使用 Configuration Manager 客户端管理设备

若要使用 Configuration Manager 客户端软件管理设备，必须在网络上发现设备，然后将客户端软件部署到该设备，或者将客户端软件手动安装到一台新的计算机，然后在该计算机加入网络时让其加入站点。 若要发现尚未安装客户端软件的设备，请运行一个或多个内置发现方法。 发现设备后，使用众多方法之一来安装客户端软件。 有关使用发现的信息，请参阅[运行 System Center Configuration Manager 发现](../../core/servers/deploy/configure/run-discovery.md)。  

 发现支持运行 Configuration Manager 客户端软件的设备后，可以使用众多方法之一来安装软件。 安装软件并将客户端分配到主站点后，即可开始管理设备。  常见安装方法包括“客户端请求安装”、“基于软件更新的安装”、使用组策略、在计算机上手动安装，或者将客户端作为所部署操作系统映像的一部分。  

 安装客户端后，可以通过使用集合来简化管理设备的工作。 集合是创建的设备或用户组，以便作为一个组对其进行管理。 例如，可能希望在通过 Configuration Manager 注册的所有移动设备上安装移动设备应用程序。 如果是这种情况，可使用“所有移动设备”集合。  

 有关详细信息，请参阅以下主题：  

-   [为 System Center Configuration Manager 选择设备管理解决方案](../../core/plan-design/choose-a-device-management-solution.md)  

-   [System Center Configuration Manager 中的客户端安装方法](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [System Center Configuration Manager 中的集合简介](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>客户端设置  
 在初次安装 Configuration Manager 时，将通过使用可更改的默认客户端设置配置层次结构中的所有客户端。 这些客户端设置包括诸如以下配置选项：设备与站点通信的频率、是否为软件更新和其他管理操作启用客户端，或者用户是否能够将其移动设备注册为由 Configuration Manager 管理。  

可创建自定义客户端设置，然后将其分配到集合。  将集合中的成员配置为具有自定义设置，你可以创建多个自定义客户端设置，并根据你（按数值顺序）指定的顺序应用这些设置。  如果存在冲突的设置，则具有最低序号的设置优先于其他设置。  

下图显示了你如何能创建和应用自定义客户端设置的示例。  

 ![客户端设置](media/ClientSettings.gif)  

 若要了解有关客户端设置的详细信息，请参阅  
                [如何在 System Center Configuration Manager 中配置客户端设置](../../core/clients/deploy/configure-client-settings.md)和[关于 System Center Configuration Manager 中的客户端设置](../../core/clients/deploy/about-client-settings.md)。

## <a name="managing-devices-without-the-configuration-manager-client"></a>不使用 Configuration Manager 客户端而管理设备  
 Configuration Manager 支持管理未安装客户端软件（和不由 Microsoft Intune 管理）的设备。 有关详细信息，请参阅[在 System Center Configuration Manager 中使用本地基础结构管理移动设备](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)和[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

## <a name="user-based-management"></a>基于用户的管理  
 Active Directory 域服务用户的 Configuration Manager 集合。 使用用户集合时，可以在集合的所有成员登录的计算机上安装软件，并配置“用户设备相关性”，以便仅在指定为用户主要设备的设备上安装所部署的软件。 用户可以有一个或多个主设备。  

 用户可对其软件部署体验进行控制的一种方式是使用计算机客户端接口： **软件中心**。 软件中心自动安装在客户端计算机上，通过用户的“开始”菜单访问。 软件中心使用户能管理自己的软件，以及执行下列操作：  

-   安装软件  

-   将软件安排为在工作时间之外自动安装  

-   配置 Configuration Manager 在设备上安装软件的时间  

-   配置远程控制的访问权限设置（如果在 Configuration Manager 中启用了远程控制）  

-   配置电源管理的选项（如果管理用户启用了此项）  

 通过软件中心中的链接，用户可以连接到 **应用程序目录**，在该目录中，用户可以浏览、安装和请求软件。 此外，应用程序目录可以让用户配置某些首选项设置、擦除其移动设备，并且（当你允许此项配置时）为用户设备相关性指定其主设备。   

 由于应用程序目录是 IIS 中承载的一个网站，因此用户还可以通过浏览器从 Intranet 或 Internet 中直接访问应用程序目录。  



<!--HONumber=Dec16_HO1-->


