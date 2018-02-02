---
title: "服务型 Configuration Manager 和服务型 Windows 的基础知识"
titleSuffix: Configuration Manager
description: "获取有关采用服务型 Configuration Manager 以支持服务型 Windows 的基本信息。"
ms.custom: na
ms.date: 01/04/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 90542085af2a1e5cf0701c5eac6d2625c23eb8c6
ms.sourcegitcommit: db9978135d7a6455d83dbe4a5175af2bdeaeafd8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2018
---
# <a name="keep-windows-10-up-to-date-in-the-enterprise-using-configuration-manager"></a>使用 Configuration Manager 让 Windows 10 在企业中保持最新

适用范围：System Center Configuration Manager (Current Branch)，Windows 10（半年频道）

System Center Configuration Manager 提供对 Windows 10 的功能更新的全面控制。 若要完全采用服务型 Windows 模型，还必须采用服务型 Configuration Manager 模型。 若要让 Windows 10 保持最新，需要让 Configuration Manager 保持最新，以便获得最佳体验。 若要充分利用丰富强大的面向企业的 Windows 10 新功能，需要使用新版 Configuration Manager。 此内容用作重要文章的的登录页面，这些文章是采用服务型 Configuration Manager 所必需的。 服务型 Configuration Manager 可帮助实现服务型 Windows。

## <a name="key-topics-about-adopting-configuration-manager-as-a-service"></a>有关采用服务型 Configuration Manager 的关键主题

| 主题        | 说明          | 
| ------------- |-------------|
|[服务型 Configuration Manager 概述](/sccm/core/plan-design/changes/whats-new-incremental-versions)|简要概述全新 Configuration Manager 服务模型 (Current Branch) 的要点|
|[支持周期](/sccm/core/servers/manage/current-branch-versions-supported)|介绍新的支持和服务模型。|
|[已删除和已弃用的功能](/sccm/core/plan-design/changes/removed-and-deprecated-features)|针对可能会影响使用 Configuration Manager 的将来更改提出早期通知。|
|[配置服务型 Configuration Manager](/sccm/core/servers/manage/updates)|介绍在控制台内部实现的、将功能更新应用于 Configuration Manager 的简单方法。|
|[获取可用更新](/core/servers/manage/install-in-console-updates#get-available-updates)|介绍可用于获取新的 Configuration Manager 功能更新的两种模式。|
|[更新清单](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|如果适用，提供特定于更新版本的清单。| 
|[安装新的 Configuration Manager 功能更新](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|介绍功能更新的简单安装步骤。|
|[支持 Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)|提供 Windows 10（及 ADK）版本的支持矩阵。|
|[Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)|介绍 ConfigMgr 技术预览计划。|


## <a name="key-topics-about-adopting-windows-as-a-service"></a>有关采用服务型 Windows 的关键主题
| 主题        | 说明          | 
| ------------- |-------------|
|[将 Windows 作为一项服务来管理](/sccm/osd/deploy-use/manage-windows-as-a-service)|介绍如何使用服务计划来部署 Windows 10 功能更新。|
|[适用于企业的 Windows 更新集成（可选）](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|介绍如何使用 Configuration Manager 定义和部署适用于企业的 Windows 更新 (WUfB) 策略。|
|[配合使用共同管理和 Microsoft Intune 及适用于企业的 Windows 更新（可选）](/sccm/core/clients/manage/co-management-overview)|概述共同管理| 


## <a name="related-articles"></a>相关文章

- [从 ConfigMgr 2012 就地升级到 System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [有关从 ConfigMgr 2007 迁移到 System Center Configuration Manager (Current Branch) 的计划](/sccm/core/migration/planning-for-migration)