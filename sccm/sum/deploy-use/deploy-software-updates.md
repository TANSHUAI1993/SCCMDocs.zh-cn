---
title: "部署軟體更新 | Microsoft Docs"
description: "在 Configuration Manager 主控台中選擇軟體更新，以手動開始部署程序，或自動部署更新。"
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
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_SUMDeploy"></a> 部署軟體更新  

適用於：System Center Configuration Manager (最新分支)

軟體更新部署階段是部署軟體更新的程序。 不論您如何部署軟體更新，更新通常會新增到軟體更新群組，軟體更新會下載到發佈點，然後更新群組會部署至用戶端。 在您建立部署時，會將相關軟體更新原則傳送至用戶端電腦，然後從發佈點將軟體更新內容檔案下載到用戶端電腦上的本機快取，接著就能從用戶端安裝軟體更新。 網際網路上的用戶端則會從 Microsoft Update 下載內容。  

> [!NOTE]  
>  若沒有可用的發佈點，您可以在內部網路上設定用戶端，從 Microsoft Update 下載軟體更新。  

> [!NOTE]  
>  和其他部署類型不同的是，無論用戶端上設定的最大快取大小是多少，所有的軟體更新都會下載到用戶端快取。 如需有關用戶端快取設定的詳細資訊，請參閱 [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache)。  

如果您設定必要的軟體更新部署，就會在排程期限自動安裝軟體更新。 或者，用戶端電腦上的使用者可以在期限前排程或起始軟體更新安裝。 在嘗試安裝後，用戶端電腦會將狀態訊息傳回網站伺服器，回報軟體更新安裝是否成功。 如需軟體更新部署的詳細資訊，請參閱 [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows)。  

部署軟體更新的主要狀況有兩種：手動部署和自動部署。 通常，您一開始會以手動部署軟體更新以建立用戶端電腦的基準，然後使用自動部署管理用戶端上的軟體更新。  

## <a name="BKMK_ManualDeployment"></a> 手動部署軟體更新
您可以在 Configuration Manager 主控台中選取軟體更新，並手動開始部署程序。 在您建立自動部署規則以管理每月進行中的軟體更新部署之前，您通常會使用這種部署方式以必要的軟體更新讓用戶端電腦保持在最新狀態，以及部署超出訊號範圍的軟體更新需求。 以下清單提供手動部署軟體更新的一般工作流程：  

1. 篩選使用特定需求的軟體更新。 例如，您可以提供可擷取所有安全性或 50 部以上用戶端電腦上必要的重要軟體更新的準則。  
2. 建立含有軟體更新的軟體更新群組。  
3. 在軟體更新群組中下載軟體更新的內容。  
4. 手動部署軟體更新群組。

如需詳細步驟，請參閱[手動部署軟體更新](manually-deploy-software-updates.md)。

## <a name="automatically-deploy-software-updates"></a>自動部署軟體更新
自動軟體更新部署是使用自動部署規則 (ADR) 來設定。 這是每月軟體更新 (一般稱為「週二修補程式日」(Patch Tuesday)) 和管理定義更新的常見部署方式。 執行規則時，軟體更新會從軟體更新群組中移除 (使用現有更新群組時)，符合指定準則的軟體更新 (例如，上個月發行的所有安全性軟體更新) 會新增至軟體更新群組，軟體更新的內容檔案會下載並複製到發佈點，且軟體更新會部署至目標集合中的用戶端。 以下清單提供自動部署軟體更新的一般工作流程：  

1.  建立指定部署設定的 ADR。
2.  軟體更新會新增至軟體更新群組。  
3.  軟體更新群組會部署至目標集合中的用戶端電腦 (如果有指定)。  

您必須決定要在您的環境中使用哪種部署策略。 例如，您可能會建立 ADR，並且以測試用戶端集合為目標。 在您確認軟體更新已安裝在測試群組上之後，您便可以在規則中加入新的部署，或將現有部署中的集合變更為包含更多用戶端集合的目標集合。 ADR 建立的軟體更新物件皆為互動式。  

-   使用 ADR 部署的軟體更新會自動部署至已加入目標集合的新用戶端。  
-   新增至軟體更新群組的軟體更新會自動部署至目標集合中的用戶端。  
-   您可以隨時啟用或停用 ADR 的部署。  

建立 ADR 之後，您可以將其他的部署加入規則中。 如此可協助您管理將不同更新部署到不同集合的複雜性。 每個新部署都會有完整的功能和部署監視體驗，而且每個加入的新部署都：  

-   使用 ADR 第一次執行時所建立的相同更新群組和封裝  
-   可以指定不同的集合  
-   支援獨特的部署內容，包括：  
   -   啟用時間  
   -   期限  
   -   顯示或隱藏使用者經驗  
   -   分隔這個部署的警示  

如需詳細步驟，請參閱[自動部署軟體更新](automatically-deploy-software-updates.md)

<!-- ###  <a name="BKMK_ClientCache"></a> Client cache setting  
The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits to download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually starts the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  -->


 <!-- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  -->
