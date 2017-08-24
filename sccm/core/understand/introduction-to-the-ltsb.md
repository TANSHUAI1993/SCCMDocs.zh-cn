---
title: "Long-Term Servicing Branch 简介 | Microsoft Docs"
description: "了解 System Center Configuration Manager 的 Long-Term Servicing Branch。"
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 91c1ca860069c6ebe0d20230c4620bf3f68735a2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager 的 Long-Term Servicing Branch 简介

*适用范围：System Center Configuration Manager (Long-Term Servicing Branch)*

System Center Configuration Manager 的 Long-Term Servicing Branch (LTSB) 是 Configuration Manager 的单独分支，旨在成为面向所有客户的安装选项。 不过，这是面向已终止软件保障 (SA) 或同等 Configuration Manager 订阅权限的客户的唯一选项。


LTSB 是在 Configuration Manager 版本 1606 基础之上构建而成，与 Configuration Manager 的 Current Branch 相比，它减少了功能。

 > [!TIP]   
 > 如果查找有关 **Windows 服务器**的分支的信息，请参阅 [Windows Server 2016 的新 Current Branch for Business 服务选项]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/)。

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Configuration Manager 的 LTSB 不提供的功能
Configuration Manager 的 Current Branch 支持以下功能，但 LTSB 并不支持这些功能：

-   添加新功能和改进的控制台中更新。
-   支持将新发布的操作系统用于网站服务器和客户端。
-   使用 Microsoft Intune 订阅可以支持：
    -   配置为混合移动设备管理 (MDM) 的 Intune
    -   本地 MDM
-   Windows 10 服务仪表板和服务计划，包括对最新版 Windows 10 Current Branch (CB) 和 Current Branch for Business (CBB) 的支持。  
-   支持今后推出的 Windows Server 和 Windows 10 LTSB 版本
-   资产智能
-   基于云的分发点
-   作为 Exchange Connector 的 Exchange Online    

虽然 LTSB 不支持这些功能，但一些功能依然会显示在 Configuration Manager 控制台中，只是不能选择或使用。


## <a name="find-documentation-for-the-ltsb"></a>查找 LTSB 文档
LTSB 是在 Current Branch 版本 1606 基础之上构建而成。 若要查找产品文档，请参考 [Current Branch 文档](https://docs.microsoft.com/sccm/)，其中包含 LTSB 专属注意事项和限制。 以下联机主题中标出了这些注意事项和限制：

-     [Long-Term Servicing Branch 简介](introduction-to-the-ltsb.md)：（本主题）
-     [安装 Long-Term Servicing Branch](install-the-ltsb.md)
-     [将 Long-Term Servicing Branch 升级到 Current Branch](convert-to-current-branch.md)
-     [Long-Term Servicing Branch 的支持配置](supported-configurations-for-ltsb.md)
-   [System Center Configuration Manager 的 Long-Term Servicing Branch](manage-the-ltsb.md)

对 LTSB 参考 Current Branch 文档时，适用于版本 1606 的详细信息也适用于 LTSB。 随版本 1610 或更高版本一起引入的功能或详细信息不受 LTSB 支持。


## <a name="licensing-overview-for-the-ltsb"></a>LTSB 证书概述   
自 2016 年 10 月 1 日起，具有 System Center Configuration Manager 许可证上可用的软件保障 (SA) 或同等订阅权限的客户，有权使用 System Center Configuration Manager 的 2016 年 10 月发行的版本 1606。 自 2016 年 10 月 1 日起（含），对 System Center Configuration Manager 具有权限的客户在安装时将会发现两个已许可的选项：Current Branch 和 Long-Term Servicing Branch (LTSB)。

对 System Center Configuration Manager 具有永久权限或者允许 SA 或订阅在 10 月 1 日之后失效的客户，可以在失效时安装当前的 System Center Configuration Manager LTSB 版本。

[可在此处](http://go.microsoft.com/fwlink/?LinkId=800052)找到通过 Microsoft 批量许可计划购买的产品的完整条款和条件。

请参阅 [System Center Configuration Manager 的许可和分支](learn-more-editions.md)，详细了解 Configuration Manager 分支的许可。

## <a name="next-steps"></a>后续步骤

如果确定 Configuration Manager LTSB 是适合环境的正确分支，请在新层次结构中[安装新 LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) 网站，或[升级 System Center 2012 Configuration Manager 网站](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager)和层次结构。

如果没有安装介质，请参阅 [System Center 2016 文档](https://technet.microsoft.com/system-center-docs/system-center)，了解如何获取 System Center 2016，其中包括可用于安装 System Center Configuration Manager LTSB 的介质。  
