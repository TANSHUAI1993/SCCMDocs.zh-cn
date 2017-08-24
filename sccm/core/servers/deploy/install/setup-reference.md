---
title: "安装参考 | Microsoft Docs"
description: "查看此参考可帮助做好 Configuration Manager 站点或层次结构安装准备。"
ms.custom: na
ms.date: 4/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: "22"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 739461a6cca0fd67431093524c1e8158afd80d0f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="reference-for-system-center-configuration-manager-setup"></a>System Center Configuration Manager 安装的参考

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 安装程序提供了几个主题的链接，以下部分对相关内容进行了详细介绍。 此处提供的信息有助于准备安装 Configuration Manager 站点或层次结构，且有助于为某些必须在安装过程中做出的决定做好准备。  


##  <a name="bkmk_start"></a> 在开始之前  
在安装新的 Configuration Manager 站点之前，请确保已经查看以下信息，这些信息有助于为成功完成部署设计做好准备：  

-   [System Center Configuration Manager 基础知识](../../../../core/understand/fundamentals.md)  
-   [System Center Configuration Manager 基础结构规划](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [准备安装 System Center Configuration Manager 站点](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> 评估服务器准备情况  
在开始安装新站点之前，请确保计划用于站点的站点服务器和远程站点系统服务器（如承载站点数据库的服务器）满足所有必备项配置。 文档库中的下列主题可有所帮助：  

-   [System Center Configuration Manager 支持的配置](../../../../core/plan-design/configs/supported-configurations.md)  
-   [先决条件检查程序](prerequisite-checker.md)  

##  <a name="bkmk_Addclients"></a> 其他操作系统的客户端  
可从 Microsoft 下载中心为以下操作系统下载 Configuration Manager 的客户端软件：  

-   Mac   (Apple)  
-   UNIX  
-   Linux  

使用以下链接下载所使用的 Configuration Manager 版本的客户端：  

-   请参阅 [Microsoft System Center Configuration Manager - 适用于其他操作系统的客户端](http://www.microsoft.com/download/details.aspx?id=47719)  

##  <a name="bkmk_usage"></a> 使用情况的数据级别和设置  
安装第一个 System Center Configuration Manager 站点时，Configuration Manager 会在站点服务器上自动安装和配置新站点系统角色“服务连接点”。 服务连接点具有以下默认设置：  

-   “联机”模式（也提供脱机模式）  
-   数据收集级别为“增强”（也提供“基本”和“完整”这两个数据收集级别）  

当服务连接点站点系统角色处于联机状态时，Microsoft 可通过 Internet 自动收集诊断和使用情况信息。 收集的信息可帮助我们：  

-   识别和解决问题  
-   改进我们的产品和服务  
-   标识适用于所使用的 Configuration Manager 版本的 Configuration Manager 更新  

### <a name="levels-of-data-collection"></a>数据收集级别  
数据收集包括以下三个级别：

-   “基本”包括有关安装和升级的数据，如站点的数目和启用的 Configuration Manager 功能。 不会传输任何个人身份信息。  

-   “增强”包括“基本”级别设置中的数据，并传输有关层次结构、每个功能的使用方式（频率和持续时间）的数据以及增强的诊断信息（如出现系统或应用故障时，服务器的内存状态）。 不会传输任何个人身份数据。  

-   “完整”包括“基本”和“增强”级别设置中的数据，并且还将发送高级诊断信息，如系统文件和内存快照。 此选项可能包括个人身份信息，但我们不会使用这些信息来确定你的身份或联系你，或定向发送广告。  

有关详细信息（包括各级别所收集详情的披露），请参阅 [System Center Configuration Manager 的诊断和使用情况数据](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)。  

若要在线查看 System Center Configuration Manager 隐私声明，请转到 [http://go.microsoft.com/fwlink/?LinkID=626527](http://go.microsoft.com/fwlink/?LinkID=626527)。
