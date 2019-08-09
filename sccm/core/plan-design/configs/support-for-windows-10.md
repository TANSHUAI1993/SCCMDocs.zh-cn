---
title: 支持 Windows 10
titleSuffix: Configuration Manager
description: 了解支持作为客户端或 OSD 对 System Center Configuration Manager 使用的 Windows 10 版本
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e95cc6be22c05afcf489fa7e9db8456cb0da0f79
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536797"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Configuration Manager 支持使用 Windows 10  

适用范围：  System Center Configuration Manager (Current Branch)

了解 Configuration Manager 支持的 Windows 10 版本，包括：

- [作为 Configuration Manager 客户端的 Windows 10](#windows-10-as-a-client)
- [适用于 Windows 10 的 Windows 评估和部署工具包 (ADK)](#windows-10-adk)

> [!Tip]
> 如同支持 Windows 10 版本一样支持作为客户端的 Windows Server 内部版本。 例如，Windows Server 2016 是与 Windows 10 LTSB 2016 相同的内部版本，Windows Server 版本 1803 是与 Windows 10 版本 1803 相同的内部版本。
>
> 有关作为站点系统的 Windows Server 的详细信息，请参阅 [Configuration Manager 站点系统服务器支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#bkmk_core)。


## <a name="windows-10-as-a-client"></a>作为客户端的 Windows 10

在每个 Windows 10 新版本发布后，Configuration Manager 会尽快提供支持，允许将新版本用于客户端。 由于产品有单独的开发和发布计划，因此 Configuration Manager 提供的支持取决于每个产品的发布时间。

Configuration Manager 版本将在[对该版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)结束后从列表中删除。 同样，对 Enterprise 2015 LTSB 或 1511 等 Windows 10 版本的支持也将在它们不受支持时从列表中删除。

- Configuration Manager Current Branch 的最新版本会接收安全更新和关键更新，其中可能包括 Windows 10 版本中问题的修补程序。 当 Microsoft 发布新版本的 Configuration Manager Current Branch 时，以前的版本将仅接收安全更新。 有关详细信息，请参阅[对 Configuration Manager Current Branch 版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)。  

    > [!Note]  
    > 使 Windows 10 保持最新的最佳方式是随时关注 Configuration Manager 的最新动态。 有关详细信息，请参阅 [Configuration Manager 和 Windows 即服务](/sccm/core/understand/configuration-manager-and-windows-as-service)。  

- 此信息补充了[客户端和设备支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)。  

- 如果使用 Configuration Manager 的 Long-Term Servicing Branch，请参阅 [Long-Term Servicing Branch 的支持配置](/sccm/core/understand/supported-configurations-for-ltsb)。  

<br/>
下表列出了 Windows 10 的版本，这些版本可用作具有不同 Configuration Manager 版本的客户端。

| Windows 10 版本 | Configuration Manager 1802 | Configuration Manager 1806 | Configuration Manager 1810 | Configuration Manager 1902 | Configuration Manager 1906 |
|---------------------|-----|-----|-----|-----|-----|
| 企业版 2015 长期服务 <!--10/14/2025-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| 企业版 2016 长期服务 <!--10/13/2026-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| Enterprise LTSC 2019 <!--01/09/2029-->   | ![不支持](media/Red_X.png)   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| 1703   <!--10/08/2019-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| 1709   <!--04/14/2020-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| 1803   <!--11/10/2020-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| 1809   <!--05/11/2021-->   | ![不支持](media/Red_X.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| 1903   <!--TBD-->   | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

> [!Note]  
> 支持 Windows 10 半年频道版本的版本包括：企业版、专业版、教育版和专业教育版。  

| 项 |
|--|
| ![支持](media/green_check.png) = **支持**  |
| ![不支持](media/Red_X.png) = **不支持** |

> [!NOTE]  
> Configuration Manager 在 Windows 10 ARM64 设备上支持客户端。 现有客户端管理功能应适用于这些新设备。 例如，硬件和软件清单、软件更新和应用程序管理。 当前不支持 OS 部署。 <!-- 1353704 -->

有关 Windows 生命周期的详细信息，请参阅 [Windows 生命周期简报](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)


## <a name="windows-10-adk"></a>Windows 10 ADK

使用 Configuration Manager 部署操作系统时，Windows ADK 是必需的外部依赖项。 有关详细信息，请参阅 [OS 部署的基础架构要求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10)。

> [!Important]  
> 从 Windows 10 版本 1809 开始，Windows PE 是单独的安装程序。 但是功能上没有任何区别。

<br/>
下表列出了可用于不同版本 Configuration Manager 的 Windows 10 ADK 的版本。

| Windows 10 ADK 版本  | Configuration Manager 1802 | Configuration Manager 1806 | Configuration Manager 1810 | Configuration Manager 1902 | Configuration Manager 1906 |
|--------------------|-----|-----|-----|-----|-----|
| **1703**<br>(10.1.15063) | ![后向兼容](media/blue_compat.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) |
| **1709**<br>(10.1.16299) | ![支持](media/green_check.png) | ![后向兼容](media/blue_compat.png) | ![不支持](media/Red_X.png)   | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![后向兼容](media/blue_compat.png) | ![后向兼容](media/blue_compat.png) | ![不支持](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![不支持](media/Red_X.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![后向兼容](media/blue_compat.png) |
| **1903**<br>(10.1.18362) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |

|项|
|--|
| ![支持](media/green_check.png) = **支持** <br/> Microsoft 建议使用与要部署的 Windows 版本匹配的 Windows ADK。 部署最新的 Windows 10 版本时，请使用最新的 Windows ADK 版本。 最新的 Windows ADK 版本可能支持部署较低的 OS 版本，如 Windows 7。<!-- SCCMDocs issue 1229 --> 有关 Windows ADK 组件支持能力的详细信息，请参阅 [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)（DISM 支持的平台）和 [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1)（USMT 要求）。 |
| ![Backwards compatible](media/blue_compat.png)  = 后向兼容  <br/> 此组合未经测试，但应该适用。 我们会记录任何已知问题或注意事项。 |
| ![不支持](media/Red_X.png) = **不支持** |

> [!Note]  
> Configuration Manager 仅支持 Windows 10 ADK 的 x86 和 amd64 组件。 当前不支持 ARM 或 ARM64 组件。

> [!Tip]
> Windows Server 内部版本具有与关联的 Windows 10 版本相同的 Windows ADK 需求。 例如，Windows Server 2016 的生成版本与 Windows 10 LTSB 2016 相同。
