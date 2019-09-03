---
title: LTSB 简介
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 的 Long-Term Servicing Branch。
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 54d8efa798f10bff8bb80fea6aaf2b052c4d1419
ms.sourcegitcommit: 2d38de4846ea47a03cc884cbd3df27db48f64a6a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70109845"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Configuration Manager 的 Long-Term Servicing Branch 简介

适用范围：  System Center Configuration Manager (Long-Term Servicing Branch)

Configuration Manager 的 Long-Term Servicing Branch (LTSB) 是单独分支，旨在成为面向所有客户的安装选项。 不过，这是面向已终止软件保障 (SA) 或同等 Configuration Manager 订阅权限的客户的唯一选项。

LTSB 是在 Configuration Manager 版本 1606 基础之上构建而成，与 Configuration Manager 的 Current Branch 相比，它减少了功能。

> [!TIP]   
> Configuration Manager LTSB 与 System Center suite 长期服务渠道 (LTSC) 无关。 有关详细信息，请参阅 [System Center 发行选项概述](https://docs.microsoft.com/system-center/ltsc-and-sac-overview)。

## <a name="features-that-arent-available"></a>不可用的功能

Configuration Manager 的 Current Branch 支持以下功能，但使用 LTSB 时并不支持这些功能：

- 添加新功能和改进的控制台中更新。
- 支持将新发布的操作系统用于网站服务器和客户端。
- 使用 Microsoft Intune 订阅可以支持：
  - 配置为混合移动设备管理 (MDM) 的 Intune
  - 本地 MDM
- Windows 10 服务仪表板和服务计划，包括对最新的 Windows 10 版本的支持。  
- 支持今后推出的 Windows Server 和 Windows 10 LTSB 版本
- 资产智能
- 基于云的分发点
- 作为 Exchange Connector 的 Exchange Online    

虽然 LTSB 不支持这些功能，但一些功能依然会显示在 Configuration Manager 控制台中，只是不能选择或使用。

云集成以及 Configuration Manager Current Branch 版本 1610 或更高版本附带的任何功能均不可用于 LTSB。 这些功能包括（但不限于）以下：<!--SCCMDocs#1823-->

- 共同管理
- 桌面分析
- 云管理网关
- Azure Active Directory 集成
- 来自适用于企业的 Microsoft Store 的应用

## <a name="find-ltsb-documentation"></a>查找 LTSB 文档

LTSB 是在 Current Branch 版本 1606 基础之上构建而成。 使用 [Current Branch 文档](https://docs.microsoft.com/sccm/)，其中包含 LTSB 专属注意事项和限制。 以下文章中标识了这些注意事项和限制：

- [安装 LTSB](install-the-ltsb.md)
- [将 LTSB 升级到 Current Branch](convert-to-current-branch.md)
- [LTSB 支持的配置](supported-configurations-for-ltsb.md)
- [管理 Configuration Manager 的 LTSB](manage-the-ltsb.md)

对 LTSB 参考 Current Branch 文档时，适用于版本 1606 或更早版本的详细信息也适用于 LTSB。 随版本 1610 或更高版本一起引入的功能或详细信息不受 LTSB 支持。

## <a name="licensing-overview-for-the-ltsb"></a>LTSB 证书概述   

自 2016 年 10 月 1 日起，具有 System Center Configuration Manager 许可证上可用的软件保障 (SA) 或同等订阅权限的客户，有权使用 System Center Configuration Manager 的 2016 年 10 月发行的版本 1606。 自 2016 年 10 月 1 日起（含），对 System Center Configuration Manager 具有权限的客户在安装时将会发现两个许可选项：Current Branch 和 Long Term Servicing Branch (LTSB)。

对 System Center Configuration Manager 具有永久权限或者允许 SA 或订阅在 10 月 1 日之后失效的客户，可以在失效时安装当前的 System Center Configuration Manager LTSB 版本。

有关这些许可证的详细信息，请参阅[通过 Microsoft 批量许可计划购买的产品的完整条款和条件](https://go.microsoft.com/fwlink/?LinkId=800052)。

有关 Configuration Manager 分支的许可详细信息，请参阅 [Configuration Manager 的许可和分支](learn-more-editions.md)。

## <a name="next-steps"></a>后续步骤

如果确定 Configuration Manager LTSB 是适合环境的正确分支，请在新层次结构中[安装新 LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) 网站，或[升级 System Center 2012 Configuration Manager 网站](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager)和层次结构。
