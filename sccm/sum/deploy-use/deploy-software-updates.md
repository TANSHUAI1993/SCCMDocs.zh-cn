---
title: "部署软件更新 | Microsoft Docs"
description: "在 Configuration Manager 控制台中选择软件更新以手动启动部署过程或自动部署更新。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 70a0ad1da03a7ca88df206fec683ab1df2b531e1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_SUMDeploy"></a> 部署软件更新  

*适用范围：System Center Configuration Manager (Current Branch)*

软件更新部署阶段是指部署软件更新的过程。 无论如何部署软件更新，更新通常都会添加到软件更新组，软件更新会下载到分发点，并且更新组会部署到客户端。 当你创建部署时，系统会将关联软件更新策略发送到客户端计算机，从分发点将软件更新内容文件下载至客户端计算机上的本地缓存，然后即可从客户端安装软件更新。 Internet 上的客户端将从 Microsoft 更新下载内容。  

> [!NOTE]  
>  你可以在 Intranet 上配置客户端，以在未提供分发点时从 Microsoft 更新下载软件更新。  

> [!NOTE]  
>  与其他部署类型不同，无论客户端上的最大缓存大小如何设置，所有软件更新均会下载到客户端缓存中。 有关客户端缓存设置的详细信息，请参阅 [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache)。  

如果配置必需的软件更新部署，则软件更新将于计划的截止时间自动安装。 或者，客户端计算机上的用户可以在截止时间前计划或启动软件更新安装。 在尝试的安装后，客户端计算机会将状态消息发回站点服务器以报告软件更新安装是否成功。 有关软件更新部署的详细信息，请参阅 [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows)。  

部署软件更新有两个主要方案：手动部署和自动部署。 通常，首先会手动部署软件更新以为客户端计算机创建基线，然后将通过使用自动部署来管理客户端上的软件更新。  

## <a name="BKMK_ManualDeployment"></a>手动部署软件更新
可以在 Configuration Manager 控制台中选择软件更新并手动启动部署过程。 在创建将管理进行中的每月软件更新部署的自动部署规则之前，你通常将使用此部署方法以用所需的软件更新使客户端计算机保持最新，并部署带外软件更新要求。 以下列表提供手动部署软件更新的一般工作流：  

1. 使用特定要求的软件更新的筛选。 例如，你可以提供条件，以检索在 50 多台客户端设备上所需要的所有安全或严重软件更新。  
2. 创建包含软件更新的软件更新组。  
3. 下载软件更新组中的软件更新的内容。  
4. 手动部署软件更新组。

有关详细步骤，请参阅[手动部署软件更新](manually-deploy-software-updates.md)。

## <a name="automatically-deploy-software-updates"></a>自动部署软件更新
通过使用自动部署规则 (ADR).配置自动软件更新部署。 这是部署每月软件更新（通常称为“周二补丁日”）的常见方法，并且用于管理定义更新。 规则运行时，软件更新将从软件更新组中删除（如果使用现有更新组），将符合指定条件（例如，在最后一月中发布的所有安全软件更新）的软件更新添加到软件更新组中，软件更新的内容文件将下载和复制到分发点，并将软件更新部署到目标集合中的客户端。 以下列表提供自动部署软件更新的一般工作流：  

1.  创建 ADR 以指定部署设置。
2.  软件更新会添加到软件更新组中。  
3.  如果已指定软件更新组，则将其部署到目标集合中的客户端计算机。  

必须确定要在环境中使用的部署策略。 例如，你可以创建 ADR 并以测试客户端集合为目标。 验证在测试组上是否安装了软件更新之后，你可以在规则中添加新部署或将现有部署中的集合更改为包含更大客户端集的目标集合。 ADR 所创建的软件更新对象具有交互性。  

-   使用 ADR 部署的软件更新会自动部署到已添加到目标集合的新客户端。  
-   添加到软件更新组的新软件更新会自动部署到目标集合中的客户端。  
-   你可以针对 ADR 随时启用或禁用部署。  

创建 ADR 后，可以将其他部署添加到规则。 这可以帮助你管理将不同更新部署到不同集合的复杂性。 每个新部署均具有完整的功能和部署监视体验，且你添加的每个新部署具有以下特性：  

-   使用的更新组和包与在 ADR 首次运行时创建的更新组和包相同  
-   可以指定不同的集合  
-   支持唯一部署属性，包括：  
   -   激活时间  
   -   截止时间  
   -   显示或隐藏最终用户体验  
   -   针对此部署的单独警报  

有关详细步骤，请参阅[自动部署软件更新](automatically-deploy-software-updates.md)

<!-- ###  <a name="BKMK_ClientCache"></a> Client cache setting  
The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits to download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually starts the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  -->


 <!-- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  -->
