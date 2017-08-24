---
title: "软件清单安全和隐私 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中软件清单的安全和隐私信息。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 7652e46d2168e2de623fa8e6d5b8663701764244
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-software-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中软件清单的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*

此主题包含 System Center Configuration Manager 中软件清单的安全和隐私信息。  

##  <a name="BKMK_Security_HardwareInventory"></a> 软件清单的最佳安全方案  
 在从客户端收集软件清单数据时使用下列最佳安全方案：  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|签名和加密清单数据|当客户端使用 HTTPS 与管理点通信时，他们发送的所有数据都使用 SSL 进行加密。 但是，当客户端计算机使用 HTTP 与内部网上的管理点通信时，客户端清单数据和收集的文件可以在未签名和未加密的状态下发送。 请确保将该站点配置为要求签名和使用加密。 此外，如果客户端可以支持 SHA-256 算法，请选择要求 SHA-256 算法的选项。|  
|不要使用文件收集来收集重要文件或敏感信息|Configuration Manager 软件清单使用 LocalSystem 帐户的所有权限，这样能够收集重要系统文件的副本，例如注册表或安全帐户数据库。 当这些文件在站点服务器中可用时，对存储的文件位置具有读取资源权限或 NTFS 权限的用户可以分析其内容，并且有可能识别关于客户端的重要详细信息，从而威胁其安全性。|  
|限制客户端计算机上的本地管理员权限|具有本地管理权限的用户可以发送无效的数据作为清单信息。|  

### <a name="security-issues-for-software-inventory"></a>软件清单的安全问题  
 收集清单会暴露潜在的漏洞。 攻击者可以执行以下操作：  

-   发送无效数据，即使禁用了软件清单客户端设置并启用文件收集，管理点也会接受这些数据。  

-   在一个或多个文件中发送超大量数据，这可能导致拒绝服务。  

-   在将清单信息传输到 Configuration Manager 时访问清单信息。  

 如果用户知道他们可以创建一个名为 **Skpswi.dat** 的隐藏文件并将它放在客户端硬盘的根目录中，以从软件清单中排除该文件，则你将无法从该计算机收集软件清单数据。  

 由于具有本地管理权限的用户可以发送任何信息作为清单数据，因此请不要认为 Configuration Manager 收集的清单数据具有权威性。  

 默认情况下，客户端设置中启用了软件清单。  

##  <a name="BKMK_Privacy_HardwareInventory"></a> 软件清单的隐私信息  
 硬件清单允许检索 Configuration Manager 客户端上注册表和 WMI 中存储的任何信息。 软件清单允许您发现具有指定类型的所有文件或从客户端收集任何指定的文件。 通过扩展硬件和软件清单并添加新的许可证管理功能，资产智能增强了清单功能。  

 默认情况下，客户端设置中启用了硬件清单，并且收集的 WMI 信息由你选择的选项确定。 默认情况下，软件清单处于启用状态，但默认情况下不收集文件。 尽管你可以选择启用硬件清单报告类，但资产智能数据集合会自动启用。  

 清单信息不会发送到 Microsoft。 清单信息存储在 Configuration Manager 数据库中。 当客户端使用 HTTPS 来连接到管理点时，它们向站点发送的清单数据在传输过程中是加密的。 如果客户端使用 HTTP 来连接到管理点，你可以选择启用清单加密。 清单数据不会以加密格式存储在数据库中。 信息将保留在数据库中，直到每 90 天后被站点维护任务“删除过期的清单历史”  或“删除过期的收集文件”  。 可以配置删除间隔。  

 在配置硬件清单、软件清单、文件收集或资产智能数据集合前，请考虑你的隐私要求。  
