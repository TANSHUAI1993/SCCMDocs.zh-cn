---
title: "安装参考 | System Center Configuration Manager"
description: "查看此参考可帮助做好 Configuration Manager 站点或层次结构安装准备。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 06bab7e01fee2c0b030a2879fa67fd455bf668fe


---
# <a name="reference-for-system-center-configuration-manager-setup"></a>System Center Configuration Manager 安装的参考

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 安装程序提供了几个主题的链接，以下部分对相关内容进行了详细介绍。 以下部分中的信息有助于准备安装 Configuration Manager 站点或层次结构，且有助于为某些必须在安装过程中做出的决定做好准备：  

-   [在开始之前](#bkmk_start)  

-   [评估服务器准备情况](#bkmk_assess)  

-   [其他操作系统的客户端](#bkmk_Addclients)  

-   [System Center Configuration Manager 的诊断和使用情况数据](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

##  <a name="a-namebkmkstarta-before-you-begin"></a><a name="bkmk_start"></a>开始之前  
 在安装新的 Configuration Manager 站点之前，请确保已经查看以下信息，这些信息有助于为成功完成部署设计做好准备：  

-   [System Center Configuration Manager 基础知识](../../../../core/understand/fundamentals.md)  

-   [System Center Configuration Manager 基础结构规划](../../../plan-design/network/configure-firewalls-ports-domains.md)  

-   [准备安装 System Center Configuration Manager 站点](prepare-to-install-sites.md)  

##  <a name="a-namebkmkassessa-assess-server-readiness"></a><a name="bkmk_assess"></a>评估服务器准备情况  
 在开始安装新站点之前，请确保计划用于站点的站点服务器和远程站点系统服务器（如承载站点数据库的服务器）满足所有必备项配置。 文档库中的下列主题可有所帮助：  

-   [System Center Configuration Manager 支持的配置](../../../../core/plan-design/configs/supported-configurations.md)  

-   [先决条件检查程序](https://technet.microsoft.com/library/mt590813.aspx#bkmk_PreqChk)  

##  <a name="a-namebkmkaddclientsa-clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a>其他操作系统的客户端  
 可从 Microsoft 下载中心为以下操作系统下载 Configuration Manager 的客户端软件：  

-   Mac   (Apple)  

-   UNIX  

-   Linux  

**使用以下链接下载所使用的 Configuration Manager 版本的客户端：**  

-   [System Center Configuration Manager（当前分支）](http://www.microsoft.com/download/details.aspx?id=47719)  

-   [System Center 2012 R2 Configuration Manager SP1 和 System Center 2012 Configuration Manager SP2](http://go.microsoft.com/fwlink/?LinkID=626550)  

-   [System Center 2012 R2 Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=316448)  

-   [System Center 2012 Configuration Manager SP1](http://www.microsoft.com/en-pk/download/details.aspx?id=36212)  

##  <a name="a-namebkmkusagea-usage-data-levels-and-settings"></a><a name="bkmk_usage"></a>使用数据级别和设置  
安装第一个 System Center Configuration Manager 站点时，会在站点服务器上自动安装和配置新站点系统角色“服务连接点”，并具有以下默认设置：  

-   “联机” 模式（也支持脱机模式）  

-   数据收集级别为“增强”  （也支持“基本”和“完整”这两个数据收集级别）  

当此角色处于联机状态时，它可让 Microsoft 通过 Internet 自动收集诊断和使用情况信息。 收集的信息可帮助我们：  

-   识别和解决问题  

-   改进我们的产品和服务  

-   标识适用于所使用的 Configuration Manager 版本的 Configuration Manager 更新  

数据收集的三个级别包括：  

-   “基本” 包括有关安装和升级的数据，如站点的数目和启用的 Configuration Manager 功能。 不会传输任何个人身份信息。  

-   “增强” 包括“基本”设置中的数据，并传输有关层次结构、每个功能的使用方式（频率和持续时间）的数据以及增强的诊断信息（如出现系统或应用故障时，服务器的内存状态）。 不会传输任何个人身份数据。  

-   “完整” 包括“基本”和“增强”设置中的数据，并且还将发送高级诊断信息，如系统文件和内存快照。 此选项可能包括个人身份信息，但我们不会使用这些信息来确定你的身份或联系你，或定向发送广告。  

有关详细信息（包括各级别所收集详情的披露），请参阅 [System Center Configuration Manager 的诊断和使用情况数据](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)。  

[System Center Configuration Manager 隐私声明](http://go.microsoft.com/fwlink/?LinkID=626527)



<!--HONumber=Nov16_HO1-->


