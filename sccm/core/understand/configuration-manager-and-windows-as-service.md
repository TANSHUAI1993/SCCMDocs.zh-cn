---
title: Configuration Manager 和服务型 Windows
titleSuffix: Configuration Manager
description: 获取有关采用 Configuration Manager Current Branch 以支持服务型 Windows 的基本信息。
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e2fb6b022526ce4bae1de21012ac996dbcea35cf
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36260901"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager 和服务型 Windows

适用范围：System Center Configuration Manager (Current Branch)

System Center Configuration Manager 提供对 Windows 10 的功能更新的全面控制。 若要完全采用服务型 Windows 模型，还必须采用 Configuration Manager Current Branch 模型。 若要让 Windows 10 保持最新，需要让 Configuration Manager 保持最新，以便获得最佳体验。 若要充分利用丰富强大的面向企业的 Windows 10 新功能，需要使用新版 Configuration Manager。 此文章用作重要文章的登录页面，这些文章是采用 Configuration Manager Current Branch 所必需的。 Configuration Manager Current Branch 可帮助实现服务型 Windows。

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>有关采用 Configuration Manager Current Branch 的重要文章

| 文章        | 说明          | 
| ------------- |-------------|
|[Configuration Manager Current Branch 概述](/sccm/core/plan-design/changes/whats-new-incremental-versions)|简要概述全新 Configuration Manager 服务模型 (Current Branch) 的要点|
|[支持周期](/sccm/core/servers/manage/current-branch-versions-supported)|介绍新的支持和服务模型。|
|[已删除和已弃用的项](/sccm//core/plan-design/changes/deprecated/removed-and-deprecated)|针对可能会影响使用 Configuration Manager 的将来更改提出早期通知。|
|[更新到 Configuration Manager Current Branch](/sccm/core/servers/manage/updates)|介绍在控制台内部实现的、将功能更新应用于 Configuration Manager 的简单方法。|
|[获取可用更新](/sccm/core/servers/manage/install-in-console-updates#get-available-updates)|介绍可用于获取新的 Configuration Manager 功能更新的两种模式。|
|[更新清单](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|如果适用，提供特定于更新版本的清单。| 
|[安装新的 Configuration Manager 功能更新](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|介绍功能更新的简单安装步骤。|
|[支持 Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)|提供 Windows 10（及 ADK）版本的支持矩阵。|
|[Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)|介绍 ConfigMgr 技术预览计划。|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>有关采用服务型 Windows 的关键文章
| 文章        | 说明          | 
| ------------- |-------------|
|[将 Windows 作为一项服务来管理](/sccm/osd/deploy-use/manage-windows-as-a-service)|介绍如何使用服务计划来部署 Windows 10 功能更新。|
|[通过任务序列升级 Windows 10](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)|使用其他建议创建任务序列以升级 Windows 10 的详细信息。|
|[分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|分阶段部署可在多个集合中自动协调有序地推出任务序列。|  
|[优化 Windows 10 更新传递](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)|使用 Configuration Manager 管理更新内容以及时了解 Windows 10 动态。|
|[与升级就绪情况集成](/sccm/core/clients/manage/upgrade/upgrade-analytics)|利用升级就绪情况，可以访问和分析环境中的设备对升级至 Windows 10 的准备情况。| 
|[适用于企业的 Windows 更新集成（可选）](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|介绍如何使用 Configuration Manager 定义和部署适用于企业的 Windows 更新 (WUfB) 策略。|
|[配合使用共同管理和 Microsoft Intune 及适用于企业的 Windows 更新（可选）](/sccm/core/clients/manage/co-management-overview)|概述共同管理| 


## <a name="related-articles"></a>相关文章

- [从 ConfigMgr 2012 就地升级到 System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [有关从 ConfigMgr 2007 迁移到 System Center Configuration Manager (Current Branch) 的计划](/sccm/core/migration/planning-for-migration)