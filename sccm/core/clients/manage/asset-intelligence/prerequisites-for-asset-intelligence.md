---
title: "资产智能先决条件 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中的资产智能先决条件。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
caps.latest.revision: "10"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 2bcc6dd84b236187ea9cbfa0b85c25e7ec25719c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-asset-intelligence-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的资产智能先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的资产智能具有外部依赖关系和产品内依赖关系。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系  
 下表提供 Configuration Manager 外部的资产智能依赖关系。  

|依赖关系|更多信息|  
|----------------|----------------------|  
|成功登录事件审核先决条件|四个资产智能报表显示从客户端计算机上的 Windows 安全事件日志收集的信息。 如果安全事件日志未配置为记录所有成功登录事件，则即使启用了适当的硬件清单报表类，这些报表也不包含任何数据。<br /><br /> 下列资产智能报表依赖于收集的 Windows 安全事件日志信息：<br /><br /> -   硬件 03A - 主计算机用户<br />-   硬件 03B - 特定主控制台用户的计算机<br />-   硬件 04A - 共享（多用户）计算机<br />-   硬件 05A - 特定计算机上的控制台用户<br /><br /> 要使硬件清单客户端代理能够列出支持这些报表所需的信息，必须先在客户端上将 Windows 安全事件日志设置修改为记录所有成功登录事件，并启用 **SMS_SystemConsoleUser** 硬件清单报表类。 有关将安全事件日志设置修改为记录所有成功登录事件的详细信息，请参阅[启用成功登录事件的审核](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents)。|  

> [!NOTE]  
>  **SMS_SystemConsoleUser** 硬件清单报表类在安全事件日志中仅保留前 90 天的成功登录事件数据，而不考虑日志的长度。 如果安全事件日志包含少于 90 天的数据，则读取整个日志。  

## <a name="dependencies-internal-to-configuration-manager"></a>Configuration Manager 的内部依赖关系  
 下表提供 Configuration Manager 内部的资产智能依赖关系。  

|依赖关系|更多信息|  
|----------------|----------------------|  
|客户端代理先决条件|资产智能报表依赖于通过客户端硬件和软件清单报表获取的客户端信息。 要获取所有资产智能报表所需的信息，必须启用下列客户端代理：<br /><br /> -   硬件清单客户端代理<br />-   软件计数客户端代理|  
|硬件清单客户端代理依赖关系|要收集某些资产智能报表所需的清单数据，必须启用硬件清单客户端代理。 此外，还必须在主站点服务器计算机上启用资产智能报表所依赖于的一些硬件清单报表类。<br /><br /> 有关启用硬件清单客户端代理的信息，请参阅[如何在 System Center Configuration Manager 中扩展硬件清单](../../../../core/clients/manage/inventory/extend-hardware-inventory.md)。|  
|软件计数客户端代理依赖关系|若干资产智能软件报表均依赖于软件计数客户端代理提供数据。 有关启用软件计数客户端代理的信息，请参阅[在 System Center Configuration Manager 中使用软件计数监视应用使用情况](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。<br /><br /> 下列资产智能报表依赖于软件计数客户端代理提供数据：<br /><br /> -   软件 07A - 按计算机数列出的最近使用过的可执行文件<br />-   软件 07B - 最近使用过指定的可执行文件的计算机<br />-   软件 07C - 特定计算机上最近使用的可执行文件<br />-   软件 08A - 按用户数列出的最近使用过的可执行文件<br />-   软件 08B - 最近使用过指定的可执行文件的用户<br />-   软件 08C - 按特定用户列出的最近使用过的可执行文件|  
|资产智能硬件清单报表类先决条件|Configuration Manager 中的资产智能报表依赖于特定的硬件清单报表类。 在硬件清单报表类已启用并且客户端基于这些类报告了硬件清单之前，关联资产智能报表不包含任何数据。 可以启用以下硬件清单报表类以支持资产智能报表要求：<br /><br /> -   SMS_SystemConsoleUsage<sup>1</sup><br />-   SMS_SystemConsoleUser<sup>1</sup><br />-   SMS_InstalledSoftware<br />-   SMS_AutoStartSoftware<br />-   SMS_BrowserHelperObject<br />-   Win32_USBDevice<br />-   SMS_InstalledExecutable<br />-   SMS_SoftwareShortcut<br />-   SoftwareLicensingService<br />-   SoftwareLicensingProduct<br />-   SMS_SoftwareTag<br /><br /> <sup>1</sup> 默认情况下， **SMS_SystemConsoleUsage** 和 **SMS_SystemConsoleUser** 资产智能硬件清单报表类处于启用状态。<br /><br /> 可以在 Configuration Manager 控制台的“资产和符合性”工作区中，在单击“资产智能”节点时编辑资产智能硬件清单报表类。 有关详细信息，请参阅[在 System Center Configuration Manager 中配置资产智能](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)主题的[启用资产智能硬件清单报表类](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence)部分。|  
|Reporting Services 点|必须先安装 Reporting Services 点站点系统角色才能显示软件更新报表。 有关创建 Reporting Services 点的详细信息，请参阅 [在 Configuration Manager 中配置报表](http://go.microsoft.com/fwlink/p/?LinkId=232661)。|  
