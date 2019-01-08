---
title: 部署软件更新
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 控制台中手动或自动部署软件更新。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 80effa7ec3439925248e19dbf9d35efcf1694b8a
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53419353"
---
# <a name="deploy-software-updates"></a>部署软件更新  

适用范围：System Center Configuration Manager (Current Branch)

软件更新部署阶段是指部署软件更新的过程。 无论如何部署软件更新，该站点：
- 将更新添加到软件更新组
- 将更新内容分发到分发点
- 将更新组部署到客户端  

创建部署后，站点向目标客户端发送关联的软件更新策略。 客户端将软件更新内容文件从内容源下载到其本地缓存。 Internet 上的客户端始终从 Microsoft 更新云服务中下载内容。 软件更新随后可供客户端安装。   

> [!Tip]  
>  如果未提供分发点，则 Intranet 上的客户端也可以从 Microsoft 更新下载软件更新。  

> [!NOTE]  
>  与其他部署类型不同，软件更新全部下载到客户端缓存。 这与客户端上的最大缓存大小设置无关。 有关客户端缓存设置的详细信息，请参阅[为 Configuration Manager 客户端配置客户端缓存](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache)。  

如果配置必需的软件更新部署，则软件更新将于计划的截止时间自动安装。 或者，客户端计算机上的用户可以在截止时间前计划或启动软件更新安装。 在尝试的安装后，客户端计算机会将状态消息发回站点服务器以报告软件更新安装是否成功。 有关软件更新部署的详细信息，请参阅 [Software update deployment workflows](/sccm/sum/understand/software-updates-introduction#BKMK_DeploymentWorkflows)。  

有三种主要的软件更新部署方案： 
- [手动部署](#BKMK_ManualDeployment)  
- [自动部署](#bkmk_auto)  
- [分阶段部署](#bkmk_phased)  

通常，首先手动部署软件更新以便为客户端创建基线，然后通过使用自动或分阶段部署来管理客户端上的软件更新。  

> [!Note]  
> 不能将自动部署规则与分阶段部署配合使用。



## <a name="BKMK_ManualDeployment"></a>手动部署软件更新
在 Configuration Manager 控制台中选择软件更新并手动启动部署过程。 通常使用此部署方法：  

- 在创建管理每月部署的自动部署规则之前，通过所需软件更新使客户端保持最新状态  

- 部署带外软件更新  


以下列表提供手动部署软件更新的一般工作流：  

1. 使用特定要求的软件更新的筛选。 例如，提供条件，以检索 50 多个客户端上所需的所有安全或严重软件更新。  

2. 创建包含软件更新的软件更新组。  

3. 下载软件更新组中的软件更新的内容。  

4. 手动部署软件更新组。  

有关详细信息和详细步骤，请参阅[手动部署软件更新](manually-deploy-software-updates.md)。

> [!Tip]  
> 手动部署 Office 365 客户端更新时，请在“软件库”工作区的“Office 365 客户端管理”下的“Office 365 更新”节点中找到它们。  



## <a name="bkmk_auto"></a> 自动部署软件更新

使用自动部署规则 (ADR) 配置自动软件更新部署。 这是部署每月软件更新（通常称为“周二补丁日”）的常见方法，并且用于管理定义更新。 定义 ADR 的条件以自动执行部署过程。 以下列表提供自动部署软件更新的一般工作流：  

1.  创建 ADR 以指定部署设置。  

2.  该站点将软件更新添加到软件更新组。  

3.  该站点将软件更新组部署到目标集合中的客户端。  

首先，确定自动软件更新部署策略。 例如，创建 ADR 并以测试客户端集合为最初目标。 验证测试组已成功安装软件更新后，向规则添加新部署。 还可以将现有部署中的目标集合更改为包含更多客户端的集合。 在决定使用的策略时，请考虑以下行为：  

- 可以修改 ADR 所创建的软件更新对象的属性。   

- 将软件更新添加到目标集合时，ADR 可自动向客户端部署软件更新。  

- 当用户或 ADR 将新的软件更新添加到软件更新组时，该站点可自动将它们部署到目标集合中的客户端。  

- 针对 ADR 随时启用或禁用部署。  


创建 ADR 后，将其他部署添加到规则。 此操作有助于管理将不同更新部署到不同集合的复杂性。 每个新部署均具有完整的功能和部署监视体验。  

你添加的每个新部署：  

- 使用的更新组和包与在 ADR 首次运行时创建的更新组和包相同  
- 可以针对不同的集合  
- 支持唯一部署属性，包括：  
  -   激活时间  
  -   截止时间  
  -   用户体验  
  -   针对每个部署的单独警报  


有关详细信息和详细步骤，请参阅[自动部署软件更新](automatically-deploy-software-updates.md)



## <a name="bkmk_phased"></a> 分阶段部署软件更新

<!--1358146--> 从版本 1810 开始，为软件更新创建分阶段部署。 通过分阶段部署，可以根据可自定义条件和组进行协调安排，有序推出软件。

有关详细信息，请参阅[创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)。

