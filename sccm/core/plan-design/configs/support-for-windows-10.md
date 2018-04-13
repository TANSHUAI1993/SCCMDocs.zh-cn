---
title: 支持 Windows 10
titleSuffix: Configuration Manager
description: 了解支持作为客户端或 OSD 对 System Center Configuration Manager 使用的 Windows 10 版本
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 877732c4095438b19a863335a4a0026b7b088b24
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="support-for-windows-10-in-system-center-configuration-manager"></a>支持在 System Center Configuration Manager 中使用 Windows 10  

*适用范围：System Center Configuration Manager (Current Branch)*


了解 Configuration Manager 支持的 Windows 10 版本，包括：
 -  作为 Configuration Manager 客户端的 Windows 10
 -  适用于 Windows 10 的 Windows 评估和部署工具包 (ADK)

## <a name="windows-10-as-a-client"></a>作为客户端的 Windows 10
在每个 Windows 10 新版本发布后，Configuration Manager 会尽快提供支持，允许将新版本用于客户端。 由于产品有单独的开发和发布计划，因此 Configuration Manager 提供的支持取决于每个产品的发布时间。

例如，Configuration Manager 版本在[对该版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)结束后从矩阵删除。 同样，对 Enterprise 2015 LTSB 或 1511 等 Windows 10 版本的支持也在它们不受支持时从矩阵中删除。 有关详细信息，请参阅[已弃用的操作系统](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems)。


-   下面的信息补充了[客户端和设备支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)。
-   如果使用 Configuration Manager 的 Long-Term Servicing Branch，请参阅 [Long-Term Servicing Branch 的支持配置](/sccm/core/understand/supported-configurations-for-ltsb)。

| Windows 10 版本 | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 |
|---------------------|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| 1607   <br />（参阅版本）<!--04/10/2018-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| 1703   <br />（参阅版本）<!--10/09/2018-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| 1709   <br />（参阅版本）<!--04/09/2019-->   | ![后向兼容](media/blue_compat.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**版本：**企业版、专业版、教育版、专业教育版   

|项|
|--|
|![支持](media/green_check.png) = **支持**  |
|![向后兼容](media/blue_compat.png)  = **向后兼容** - 现有客户端管理功能应适用于 Windows 10 新版本。 例如，硬件清单、软件清单和软件更新。 我们会记录任何已知问题或注意事项。 <br><br>借助此方法，可以立即通过应用程序兼容性支持来部署和管理 Windows 新版本，无需 Configuration Manager 更新新版本。 |
|![不支持](media/Red_X.png) = **不支持**|

 > [!NOTE]
 > 从版本 1802 开始，Configuration Manager 在 Windows 10 ARM64 设备上支持客户端。 现有客户端管理功能应适用于这些新设备。 例如，硬件和软件清单、软件更新和应用程序管理。 当前不支持操作系统部署。 <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows 10 ADK
使用 Configuration Manager 部署操作系统时，[Windows ADK 是必需的外部依赖项](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。

下表列出了可用于不同版本 Configuration Manager 的 Windows 10 ADK 的版本。

| Windows 10 ADK 版本  | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802   |
|--------------------|-----|-----|-----|
| 1607  | ![不支持](media/Red_X.png)   | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) |
| 1703  | ![支持](media/green_check.png) | ![后向兼容](media/blue_compat.png) | ![后向兼容](media/blue_compat.png) |
| 1709  | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |

|项|
|--|
|![支持](media/green_check.png)  =  **支持** - Windows 建议使用与要部署的 Windows 版本匹配的 Windows ADK。 例如，部署 Windows 10 版本 1703 时，使用适用于 Windows 10 版本 1703 的 Windows ADK。 有关 Windows ADK 组件支持能力的详细信息，请参阅 [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)（DISM 支持的平台）和 [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1)（USMT 要求）。 |
|![向后兼容](media/blue_compat.png)   =  **向后兼容** - 此组合未经测试，但应该有效。 我们会记录任何已知问题或注意事项。 |
|![不支持](media/Red_X.png) = **不支持**|

 > [!Note]
 > Configuration Manager 仅支持 Windows 10 ADK 的 x86 和 amd64 组件。 当前不支持 arm 或 arm64 组件。 