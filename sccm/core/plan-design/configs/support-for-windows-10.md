---
title: "对 Windows 10 的支持 | Microsoft Docs"
description: "了解支持运行 System Center Configuration Manager 客户端的 Windows 10 版本。"
ms.custom: na
ms.date: 2/10/2017
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
ms.sourcegitcommit: 3702993d6cf9644d5aebaadd168749668fbcb62c
ms.openlocfilehash: 4b90384621dd20475ab9ea33ea062c24f5ecf5fa
ms.lasthandoff: 02/22/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>支持 Windows 10 作为 System Center Configuration Manager 的客户端

*适用范围：System Center Configuration Manager (Current Branch)*


 本主题介绍可用作 System Center Configuration Manager Current Branch 不同版本的客户端的 Windows 10 各版本。

- 这是对[客户端和设备支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)的补充。
- 如果使用 Configuration Manager 的 Long-Term Servicing Branch，请参阅 [Long-Term Servicing Branch 的支持配置](/sccm/core/understand/supported-configurations-for-ltsb)。

Windows 版本发布后，Configuration Manager 会尽快为每个新的 Windows 10 版本提供支持。 由于产品具有单独的开发和发布计划，因此 Configuration Manager 提供的支持取决于每个产品的版本和分支的发布时间。  



|Windows 10 版本 |Configuration Manager 1602|Configuration Manager 1606|Configuration Manager 1610|
|---------------------|-----|-----|-----|
|企业版 2015 长期服务 |![支持](media/green_check.png) |![支持](media/green_check.png) |![支持](media/green_check.png) |
|1507 <br />Enterprise、Pro | ![支持](media/green_check.png)| ![支持](media/green_check.png)|![支持](media/green_check.png) |
|1511 <br />Enterprise、Pro <br />(CB)、(CBB) |![支持](media/green_check.png) |![支持](media/green_check.png) |![支持](media/green_check.png) |
|企业版 2016 长期服务    |![不支持](media/Red_X.png) |![支持](media/green_check.png) | ![支持](media/green_check.png)|
|1607 <br />Enterprise、Pro<br /> (CB)    |![不支持](media/Red_X.png) |![后向兼容](media/blue_compat.png) |![支持](media/green_check.png) |
|1607 <br />Enterprise、Pro <br />(CBB)    |![不支持](media/Red_X.png) |![后向兼容](media/Red_X.png) |![支持](media/green_check.png) |


|项|
|--|
|![支持](media/green_check.png) = **支持**  |
|![不支持](media/blue_compat.png)  = **后向兼容** - 这意味着现有客户端管理功能（硬件清单、软件清单、软件更新等）应适用于新的 Windows 10 Current Branch 版本。 将记录任何已知问题或注意事项。 <br><br>借助此方法，可从一开始通过应用程序兼容性支持部署和管理新的 Windows 10 CB 版本，无需新的 Configuration Manager 更新版本。 |
|![支持](media/Red_X.png) = **不支持**|

