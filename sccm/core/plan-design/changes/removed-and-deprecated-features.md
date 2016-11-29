---
title: "弃用的功能 | System Center Configuration Manager"
description: "了解有关 System Center Configuration Manager 不再支持的功能、产品和操作系统的信息。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f1e1070fd5b56b1abf22159e9f95b3b4bd8a8c6


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>System Center Configuration Manager 的已删除和已弃用的功能

*适用范围：System Center Configuration Manager (Current Branch)*

本主题介绍 System Center Configuration Manager 不再支持或将在将来更新中删除（弃用）的功能、产品和操作系统。 目的是针对可能会影响使用 Configuration Manager 的将来更改提出早期警告。  

 此信息在将来版本中可能有所变化，并且可能不会包括每一个弃用的功能、产品或操作系统。  

## <a name="deprecated-features-products-and-operating-systems"></a>弃用的功能、产品和操作系统  
 作为“已弃用”列出的 Microsoft 产品和操作系统可能受到延长支持或者已经达到寿命终点。 仍将使用当前 Configuration Manager 版本测试作为“已弃用”列出的 Microsoft 产品和操作系统，直到它们超出其 Microsoft 支持生命周期。  有关详细信息，请参阅 [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle) 网站。  

 **已弃用的功能：**  


|**功能**|**首次宣布弃用**|**删除的支持**|  
|-|-|-|  
|网络访问保护 (NAP)- 在 System Center 2012 Configuration Manager 中找到|7/10/2015|√|  
|带外管理- 在 System Center 2012 Configuration Manager 中找到|10/16/2015|√|  

 **已弃用的服务器操作系统：**  

 |**操作系统**|**首次宣布弃用**|**删除的支持**|  
|-|-|-|  
|Windows Server 2008|7/10/2015|此支持在 2016 年 12 月 31 日发布第一个更新时结束（请参阅注释 1）|  
|Windows Server 2008 R2|7/10/2015|此支持在 2016 年 12 月 31 日发布第一个更新时结束（请参阅注释 2）|  

-   注释 1：支持结束后，站点服务器或大多数站点系统角色将不再支持此操作系统。 但是，分发点站点系统角色（包括请求分发点）仍会继续支持此操作系统，直至正式宣布此支持弃用或此操作系统的扩展支持期过期。  

-   注释 2：支持结束后，站点服务器或大多数站点系统角色将不再支持此操作系统。 但是，状态迁移点和分发点站点系统角色（包括请求分发点、PXE 和多播）仍会继续支持此操作系统，直至正式宣布弃用此支持或此操作系统的扩展支持期过期。  从版本 1602 开始，可以对站点服务器的操作系统进行就地升级，从 Windows Server 2008 R2 升级到 Windows Server 2012 R2。  

     有关站点服务器操作系统就地升级的详细信息，请参阅 [System Center Configuration Manager 中的更改内容](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)中的[就地升级运行 Windows Server 2008 R2 的站点服务器的操作系统](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS)部分。



 **已弃用的客户端操作系统：**  

 除非另有说明，否则支持每种作为 Configuration Manager 客户端进行支持的操作系统，直至此操作系统的扩展支持结束日期为止，如 [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)中所述。  如果对某个操作系统的 Configuration Manager 支持将在扩展支持结束日期前结束，则此处将列出此操作系统的弃用日期和支持删除日期。  

|**操作系统**|**首次宣布弃用**|**删除的支持**|  
|-|-|-|  
|Windows XP|7/10/2015|√|  
|Windows XP Embedded|7/10/2015|此支持在 2016 年 12 月 31 日之后发布第一个更新时结束|  
|Windows Server 2003|7/10/2015|√|  
|Windows Server 2003 R2|7/10/2015|√|  
|Windows Vista|7/10/2015|√|  
|Mac OS X 10.6 - 10.8|7/10/2015|√|  
|Windows Mobile 6.0 - 6.5|7/10/2015|√|  
|Nokia Symbian Belle|7/10/2015|√|  
|Windows CE 5.0 - 6.0|7/10/2015|√|  


 **SQL Server 版本作为站点数据库的已弃用支持：**  

|**SQL Server 版本**|**首次宣布弃用**|**删除的支持**|   
|-|-|-|  
|SQL Server 2008|7/10/2015|√|  
|SQL Server 2008 R2|7/10/2015|此支持在 2016 年 12 月 31 日之后发布第一个更新时结束|  

## <a name="features-removed-in-system-center-configuration-manager"></a>System Center Configuration Manager 中删除的功能  
 从初始的 System Center Configuration Manager 版本开始，以下功能会被删除：

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a>带外管理  
 通过 Configuration Manager，已删除 Configuration Manager 控制台中基于 AMT 的计算机的本机支持。  

-   使用 [适用于 Microsoft System Center Configuration Manager Intel SCS 外接程序](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)时，基于 AMT 的计算机保持完全托管  

-   使用外接程序让你可以在 Configuration Manager 能够合并这些更改之前使用用于管理 AMT 的最新功能，同时删除引入的限制  

-   System Center 2012 Configuration Manager 中的带外管理不受此更改的影响  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a>网络访问保护  
 System Center Configuration Manager 已不再支持网络访问保护。 该功能已在 Windows Server 2012 R2 中弃用并从 Windows 10 中删除。  

 有关网络访问保护备选方案，请参阅 **网络策略和访问服务概述** 的 [已弃用功能](https://technet.microsoft.com/library/hh831683.aspx)部分。  



<!--HONumber=Nov16_HO1-->


