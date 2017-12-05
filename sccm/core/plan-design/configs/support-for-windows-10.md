---
title: "支持 Windows 10"
titleSuffix: Configuration Manager
description: "了解支持作为客户端或 OSD 对 System Center Configuration Manager 使用的 Windows 10 版本。"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: "5"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: b2cacddfbd94340c30681bf03fc3afd7d71122c8
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2017
---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>支持对 System Center Configuration Manager 使用 Windows 10  

*适用范围：System Center Configuration Manager (Current Branch)*


 本主题详细介绍了可用于 System Center Configuration Manager Current Branch 不同版本的 Windows 10 版本。 这包括：
 -  作为 Configuration Manager 客户端的 Windows 10。
 -  Windows 10 评估和部署工具包 (ADK)。

## <a name="windows-10-as-a-client"></a>作为客户端的 Windows 10
在每个 Windows 10 新版本发布后，Configuration Manager 会尽快提供支持，允许将新版本用于客户端。 由于产品有单独的开发和发布计划，因此 Configuration Manager 提供的支持取决于每个产品的发布时间。

例如，Configuration Manager 版本将在[对该版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)结束后从矩阵删除。 同样，对 Enterprise 2015 LTSB 或 1511 等 Windows 10 版本的支持将在它们不受支持时从矩阵中删除。 有关详细信息，请参阅[已弃用的操作系统](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems)。

-   下面的信息补充了[客户端和设备支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)。
-   如果使用 Configuration Manager 的 Long-Term Servicing Branch，请参阅 [Long-Term Servicing Branch 的支持配置](/sccm/core/understand/supported-configurations-for-ltsb)。

|Windows 10 版本                    |  Configuration Manager 1702          |    Configuration Manager 1706 |Configuration Manager 1710          |  
|---------------------|-----|-----|-----|
|企业版 2015 长期服务                   |![支持](media/green_check.png) |![支持](media/green_check.png) | ![支持](media/green_check.png) |
|企业版 2016 长期服务                   |![支持](media/green_check.png) |![支持](media/green_check.png) | ![支持](media/green_check.png) |
|1607   <br />（也称为周年更新）<br />（*请参见版本*）   |![支持](media/green_check.png) |![支持](media/green_check.png)            |![支持](media/green_check.png) |
|1703   <br />（也称为创意者更新）<br />（*请参见版本*）      |![后向兼容](media/blue_compat.png) |![支持](media/green_check.png) | ![支持](media/green_check.png) |
|1709   <br />（也称为 Fall Creators Update）<br />（*请参见版本*） |![不支持](media/Red_X.png)   |![后向兼容](media/blue_compat.png) | ![支持](media/green_check.png) |



**版本：**企业版、专业版、教育版、专业教育版   

|项|
|--|
|![支持](media/green_check.png) = **支持**  |
|![不支持](media/blue_compat.png)  = **后向兼容** - 这表示现有客户端管理功能（硬件清单、软件清单、软件更新等）应该用于 Windows 10 新版本。 将记录任何已知问题或注意事项。 <br><br>借助此方法，可以从第一天起就通过应用程序兼容性支持来部署和管理 Windows 新版本，无需 Configuration Manager 更新新版本。 |
|![支持](media/Red_X.png) = **不支持**|


## <a name="windows-10-adk"></a>Windows 10 ADK
使用 Configuration Manager 部署操作系统时，[Windows ADK 是必需的外部依赖项](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。

下表列出了可以对不同版本 Configuration Manager 使用的 Windows 10 ADK 版本。

|Windows 10 ADK 版本  |Configuration Manager 1702   |Configuration Manager 1706 |Configuration Manager 1710 |
|--------------------|-----|-----|-----|
|1607  |![后向兼容](media/blue_compat.png) |![不支持](media/Red_X.png)| ![不支持](media/Red_X.png) |
|1703  |![支持](media/green_check.png)            |![支持](media/green_check.png) | ![后向兼容](media/blue_compat.png)|
|1709  |![不支持](media/Red_X.png)              |![支持](media/green_check.png) | ![支持](media/green_check.png)|

|项|
|--|
|![支持](media/green_check.png)  =  **支持** - Windows 建议使用与要部署的 Windows 版本匹配的 Windows ADK。 例如，部署 Windows 10 版本 1703 时，使用适用于 Windows 10 版本 1703 的 Windows ADK。  |
|![向后兼容](media/blue_compat.png)   =  **向后兼容** - 此组合未经测试，但应该有效。 将记录任何已知问题或注意事项。 |
|![支持](media/Red_X.png) = **不支持**|
