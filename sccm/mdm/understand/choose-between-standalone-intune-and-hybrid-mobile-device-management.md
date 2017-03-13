---
title: "选择 Intune 独立版或混合 MDM | Microsoft Docs"
description: "选择是使用 Intune 和 Configuration Manager 部署混合移动设备管理还是运行 Intune 独立版。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 84e3896dd05a8c157f4e94625b0eca60aacc11d3
ms.openlocfilehash: 8f2625aadfd0aed92d9922c7e3c0d3d166a78cdd
ms.lasthandoff: 02/25/2017

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>在 Microsoft Intune 独立版与使用 System Center Configuration Manager 实现的混合移动设备管理之间做出选择

*适用范围：System Center Configuration Manager (Current Branch)*

有关使用 Microsoft Intune 进行移动设备管理 (MDM) 的最常见问题之一是“应该将 Intune 与 Configuration Manager（混合 MDM）进行集成还是应该在只涉及云的配置中运行 Intune 独立版本？” 若要回答此问题，应仔细比较这两个选项，并考虑 2017 年初会推出的 Intune 独立版更新。

## <a name="what-is-intune-standalone"></a>Intune 独立版是什么？

Intune 独立版是仅涉及云而不涉及本地资源的 MDM 解决方案，并使用可从全世界任意位置访问的 Web 控制台进行管理。 Intune 数据中心托管于北美、欧洲和亚洲。 由于 Intune 是云服务，因此可在较短时间范围内将 Intune 管理部署到设备。 如果你的组织正在迁移到云中，也可选择 Intune 独立版。

## <a name="what-is-hybrid-mdm-with-configuration-manager"></a>什么是使用 Configuration Manager 的混合 MDM？

混合 MDM 是一种解决方案，它将 Intune 用作策略、配置文件和应用程序到设备的传递通道，但将 Configuration Manager 本地基础结构用于存储和管理内容以及管理设备。 如果已经在 Configuration Manager 中进行了大量投资，并希望将其扩展以管理移动设备，则可以选择混合 MDM。 混合实现提供“单一管理平台”控制，这意味着可使用同一本地基础结构和管理控制台来管理具有 Intune 的移动设备，以及具有传统 Configuration Manager 客户端的电脑和服务器。

## <a name="whats-coming-to-intune-standalone-in-early-2017"></a>2017 年初即将推出的 Intune 独立版新增功能

如果在独立版和混合版之间选择，应将2017 年初即将推出的 Intune 独立版的功能考虑在内。 现在，混合 MDM 具有多个高级功能，而这就是长久以来一些客户选择使用混合 MDM 而不是 Intune 独立版来管理设备的原因：

-   编程访问 (API) – SDK 和 PowerShell 管理选项。

-   自定义报表 - 创建自定义报表。

-   基于角色的访问控制 - 基于分配的角色限制对管理功能的访问。

-   缩放 - 部署和管理超过 100,000 台移动设备。

-   单一管理平台 – 使用同一控制台管理传统电脑客户端和 Intune 管理的设备。

如果正在开始计划 Intune 部署，并且有为期几个月的试验、验收测试和部署时段，则可考虑选择 Intune 独立版，同时了解云服务的更新将包含更多功能。 2017 年上半年，Intune 独立版将接收更新，提供使用 Configuration Manager 的混合部署的大部分高级功能。 Intune 独立版将很快移动到 Microsoft Azure 云平台，它将具有增强的可扩展性、通过 Azure 门户基于角色的访问、自定义报表和通过 Azure 图形 API 的编程访问。

可从混合模式版本切换到 Intune 独立版本，或从独立版本切换到混合版本，但需要 Microsoft 支持和操作的帮助。 还需要在管理机构更改后取消注册并重新注册所有设备。  Microsoft 正致力于改善未来服务更新中切换配置的体验。

