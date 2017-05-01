---
title: "对 Windows 10 的支持 | Microsoft Docs"
description: "了解支持运行 System Center Configuration Manager 客户端的 Windows 10 版本。"
ms.custom: na
ms.date: 3/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: db258a09ce21627ffba37eb1f3d521c1ea0341ed
ms.openlocfilehash: 7df4bde6970b63262eee9e785d983addbeac0908
ms.lasthandoff: 04/13/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>支持 Windows 10 作为 System Center Configuration Manager 的客户端

*适用范围：System Center Configuration Manager (Current Branch)*


 本主题介绍可用作 System Center Configuration Manager Current Branch 不同版本的客户端的 Windows 10 各版本。

- 这是对[客户端和设备支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)的补充。
- 如果使用 Configuration Manager 的 Long-Term Servicing Branch，请参阅 [Long-Term Servicing Branch 的支持配置](/sccm/core/understand/supported-configurations-for-ltsb)。

Windows 版本发布后，Configuration Manager 会尽快为每个新的 Windows 10 版本提供支持。 由于产品具有单独的开发和发布计划，因此 Configuration Manager 提供的支持取决于每个产品的版本和分支的发布时间。

例如，Configuration Manager 版本将在[对该版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)结束后从矩阵删除。 同样，对 Enterprise 2015 LTSB 或 1607 (CBB) 等 Windows 10 版本的支持将在它们从 Configuration Manager 支持的配置列表中删除时从矩阵中删除。 有关详细信息，请参阅[已弃用的操作系统](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems)。



|Windows 10 版本                    |Configuration Manager 1606          |Configuration Manager 1610          |    Configuration Manager 1702 |
|---------------------|-----|-----|-----|
|企业版 2015 长期服务                   |![支持](media/green_check.png) |![支持](media/green_check.png) |![支持](media/green_check.png) |
|1507 <br />（*请参见版本*）            |![支持](media/green_check.png) |![支持](media/green_check.png) |![支持](media/green_check.png) |
|1511 (CB)、(CBB)<br />（*请参见版本*） |![支持](media/green_check.png) |![支持](media/green_check.png) |![支持](media/green_check.png) |
|企业版 2016 长期服务                   |![支持](media/green_check.png) |![支持](media/green_check.png) |![支持](media/green_check.png) |
|1607 (CB)    <br />周年更新<br />（*请参见版本*）      |![后向兼容](media/blue_compat.png) |![支持](media/green_check.png) |![支持](media/green_check.png) |
|1607 (CBB)    <br />周年更新<br />（*请参见版本*）      |![不支持](media/Red_X.png)   |![支持](media/green_check.png) |![支持](media/green_check.png) |
|1703 (CB)    <br />创意者更新<br />（*请参见版本*）      |![不支持](media/Red_X.png)   |![不支持](media/Red_X.png) |![后向兼容](media/blue_compat.png) |



**版本：**企业版、专业版、教育版、专业教育版   

|项|
|--|
|![支持](media/green_check.png) = **支持**  |
|![不支持](media/blue_compat.png)  = **后向兼容** - 这意味着现有客户端管理功能（硬件清单、软件清单、软件更新等）应适用于新的 Windows 10 Current Branch 版本。 将记录任何已知问题或注意事项。 <br><br>借助此方法，可从一开始通过应用程序兼容性支持部署和管理新的 Windows 10 CB 版本，无需新的 Configuration Manager 更新版本。 |
|![支持](media/Red_X.png) = **不支持**|

