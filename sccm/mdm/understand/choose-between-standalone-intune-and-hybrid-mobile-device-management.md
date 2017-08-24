---
title: "选择 Intune 独立版或混合 MDM | Microsoft Docs"
description: "选择是使用 Intune 和 Configuration Manager 部署混合移动设备管理还是运行 Intune 独立版。"
ms.custom: na
ms.date: 07/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: "10"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 26c36df77c21254c7ad2b8a45906bd3706f9ec65
ms.sourcegitcommit: 06aef618f72c700f8a716a43fb8eedf97c62a72b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2017
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>在 Microsoft Intune 独立版与使用 System Center Configuration Manager 实现的混合移动设备管理之间做出选择

*适用范围：System Center Configuration Manager (Current Branch)*

有关使用 Microsoft Intune 进行移动设备管理 (MDM) 的最常见问题之一是“应该将 Intune 与 Configuration Manager（混合 MDM）进行集成还是应该在只涉及云的配置中运行 Intune 独立版本？” 要回答这个问题，应仔细比较两个选项。

## <a name="intune-standalone"></a>Intune 独立版
Intune 独立版是 Microsoft 推荐的部署拓扑。 Intune 独立版是仅涉及云的 MDM 解决方案，并使用可从全世界任意位置访问的 Web 控制台进行管理。 Intune 数据中心托管于北美、欧洲和亚洲。 由于 Intune 是云服务，因此可在较短时间范围内将 Intune 管理部署到设备。

客户通常会发现它可以更快、更轻松地部署独立拓扑，因为没有本地组件的依赖项。 Intune 独立版现在位于 Microsoft Azure 云平台上，并提供许多高级功能，例如：
- 集成式企业移动性管理平台 - 一款集成式云平台，并提供面向 Intune、 Azure AD Premium 和 Azure 信息保护的 Azure 门户的管理体验。
- 移动设备管理 - 丰富的移动设备管理和信息保护功能。
- 规模 - 部署和管理移动设备，而无需担心规模。
- 基于角色的访问控制 - 基于分配的角色和范围限制对管理功能的访问。
- 编程访问 (API) – Microsoft Graph API 支持、SDK 和 PowerShell 管理选项。
- Web 控制台 - 基于 HTML 5 的控制台，以 Web 标准构建而成，支持大多数现代 Web 浏览器。
- 高级报表 - 能够创建自定义报表。
- 灵活性 - 简单安装和快速传递新功能。


## <a name="hybrid-mdm-with-configuration-manager"></a>使用 Configuration Manager 的混合 MDM
混合 MDM 是一种解决方案，可将 Intune 的移动设备管理功能集成到 Configuration Manager。 它将 Intune 用作策略、配置文件和应用程序到设备的传递通道，但将 Configuration Manager 本地基础结构用于管理内容以及管理设备。 混合实现提供“单一管理平台”控制。  这意味着可使用同一本地基础结构和管理控制台来管理具有 Intune 的移动设备，以及具有传统 Configuration Manager 客户端的电脑和服务器。 出于以下原因，可以选择混合 MDM：  
- 想要从相同的管理控制台管理 Intune 中注册的移动设备以及使用 Configuration Manager 客户端托管的设备
- 基础结构要求具备多个 NDES 服务器以便将证书传递到移动设备
- 基础结构要求具备多个 Exchange 连接器
- 需要 S/MIME 加密支持


## <a name="changing-the-mdm-authority-setting"></a>更改 MDM 机构设置
如果需要更改 MDM 机构设置，可以自行更改而无需联系 Microsoft 支持部门，也无需取消注册并重新注册现有的托管设备。 有关详细信息，请参阅[更改 MDM 机构](../deploy-use/change-mdm-authority.md)。

> [!NOTE]    
> 必须具有 Configuration Manager 1610 或更高版本，才可将 MDM 机构更改为 Intune 独立版。 在具有较早版本的 Configuration Manager 时，可以更改 MDM 机构，但它需要 Microsoft 支持和操作的帮助。 它还要求用户取消注册，并在更改 MDM 机构后重新注册所有设备。  
