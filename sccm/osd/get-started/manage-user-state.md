---
title: "管理用户状态 - Configuration Manager| Microsoft Docs"
description: "System Center Configuration Manager 使用用户状态迁移工具捕获和还原操作系统部署方案中的用户状态数据。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: a0bd86587669c32377b1eafa6a890d37e10ac3f6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-user-state-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理用户状态

*适用范围：System Center Configuration Manager (Current Branch)*

在希望保留当前操作系统的用户状态的操作系统部署方案中，可以使用 System Center Configuration Manager 任务序列来捕获和还原用户状态数据。 例如：  

-   某些部署，其中你希望从一台计算机中捕获用户状态，然后在另一台计算机上将其还原。  

-   在更新部署中，你希望在同一台计算机上捕获和还原用户状态。  

 操作系统安装完成后，Configuration Manager 使用用户状态迁移工具 (USMT) 10.0 来管理从源计算机到目标计算机的用户状态数据迁移。 有关 USMT 10.0 常见迁移方案的详细信息，请参阅  [常见迁移方案](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)。  

 使用以下部分可帮助你捕获和还原用户数据。


##  <a name="BKMK_StoringUserData"></a> 存储用户状态数据  
 捕获用户状态时，可以在目标计算机或状态迁移点上存储用户状态数据。 要将用户状态存储在用户状态迁移点上，你必须使用承载状态迁移点站点系统角色的 Configuration Manager 站点系统服务器。 要将用户状态存储在目标计算机上，你必须配置任务序列以便使用链接以本地方式存储数据。  

> [!NOTE]  
>  用于以本地方式存储用户状态的链接称为硬链接。 硬链接是一项 USMT 10.0 功能，该功能将扫描计算机以查找用户文件和设置，然后创建指向这些文件的硬链接的目录。 然后，使用硬链接在部署了新操作系统之后还原用户数据。  

> [!IMPORTANT]  
>  你无法同时使用状态迁移点和使用硬链接来存储用户状态数据。  

 捕获用户状态信息后，可以使用下列方法之一存储信息：  

-   你可以通过配置状态迁移点以远程存储用户状态数据。 **捕获** 任务序列将数据发送到状态迁移点。 然后，在部署操作系统之后， **还原** 任务序列将检索数据并在目标计算机上还原用户状态。  

-   你可以以本地方式将用户状态数据存储到特定位置。 在此方案中， **捕获** 任务序列将用户数据复制到目标计算机上的特定位置。 然后，在部署操作系统之后， **还原** 任务序列从该位置检索用户数据。  

-   你可以指定可用于将用户数据还原到其原始位置的硬链接。 在此方案中，删除旧操作系统时，用户状态数据会保留在驱动器上。 然后，在部署新操作系统之后， **还原** 任务序列使用硬链接将用户状态数据还原到其原始位置。  

###  <a name="BKMK_UserDataSMP"></a> 在状态迁移点上存储用户数据  
 要将用户状态数据存储在状态迁移点上，必须执行下列操作：  

1.  用于存储用户状态数据的[Configure a state migration point](#BKMK_StateMigrationPoint) 。  

2.  在源计算机和目标计算机之间[Create a computer association](#BKMK_ComputerAssociation) 。 在源计算机上捕获用户状态之前，你必须创建此关联。  

3.  [创建任务序列以捕获和还原 System Center Configuration Manager 中的用户状态](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)。 具体而言，必须添加下列任务序列步骤以从计算机捕获用户数据，在状态迁移点上存储用户日期并将用户数据还原到一台计算机：  

    -   [请求状态存储](../understand/task-sequence-steps.md#BKMK_RequestStateStore)，在从计算机捕获状态或将状态还原到计算机时请求访问状态迁移点。  

    -   [捕获用户状态](../understand/task-sequence-steps.md#BKMK_CaptureUserState)，捕获用户状态数据并将其存储在状态迁移点上。  

    -   [还原用户状态](../understand/task-sequence-steps.md#BKMK_RestoreUserState)，通过从用户状态迁移点检索数据在目标计算机上还原用户状态。  

    -   [发布状态存储](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)，通知状态迁移点捕获或还原操作已完成。  

###  <a name="BKMK_UserDataDestination"></a> 在本地存储用户数据  
 若要在本地存储用户状态数据，必须执行以下操作：  

-   [创建用于捕获和还原用户状态的任务序列](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)。 具体而言，必须添加下列任务序列步骤以从计算机捕获用户数据，并通过使用硬链接将用户数据还原到一台计算机，  

    -   [捕获用户状态](../understand/task-sequence-steps.md#BKMK_CaptureUserState)，捕获用户状态数据并通过使用硬链接将其存储到本地文件夹。  

    -   [还原用户状态](../understand/task-sequence-steps.md#BKMK_RestoreUserState)，使用硬链接，通过检索数据在目标计算机上还原用户数据。  

        > [!NOTE]  
        >  在任务序列删除旧操作系统后，硬链接引用的用户状态数据保留在计算机上。 这是用于在部署新操作系统时用于还原用户状态的数据。  

##  <a name="BKMK_StateMigrationPoint"></a> Configure a state migration point  
 状态迁移点在一台计算机上存储捕获的用户状态数据，然后在另一台计算机上还原这些数据。 但是，当你在同一台计算机上捕获操作系统部署的用户设置时（例如在目标计算机上刷新操作系统的部署），你可以通过使用硬链接将数据存储在同一台计算机上或将数据存储在状态迁移点上。 对于某些计算机部署，当你创建状态存储时，Configuration Manager 会自动在状态存储和目标计算机之间创建关联。 你可以使用下列方法来配置状态迁移点以存储用户状态数据：  

-   使用“创建站点系统服务器向导”  为状态迁移点创建一个新站点系统服务器。  

-   使用“添加站点系统角色向导”  将状态迁移点添加到现有服务器。  

 在使用这些向导时，会提示你提供状态迁移点的下列信息：  

-   用于存储用户状态数据的文件夹。  

-   可在状态迁移点上存储数据的客户端的最大数量。  

-   供状态迁移点存储用户状态数据的最小可用空间。  

-   角色的删除策略。 你可以指定在计算机上还原用户状态数据之后立即删除该数据，或在计算机上还原用户数据后特定天数之后再删除该数据。  

-   状态迁移点是否仅响应还原用户状态数据的请求。 如果启用此选项，你将无法使用状态迁移点来存储用户状态数据。  

 有关状态迁移点以及对其进行配置的步骤的详细信息，请参阅[状态迁移点](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)。  

##  <a name="BKMK_ComputerAssociation"></a> Create a computer association  
 当你在新硬件上安装操作系统并且想捕获和还原用户数据设置时，请创建计算机关联以定义源计算机和目标计算机之间的关系。 源计算机是 Configuration Manager 管理的现有计算机。 在你将新操作系统部署到目标计算机时，源计算机包含迁移到目标计算机的用户状态。  

> [!NOTE]  
>  不支持在 Configuration Manager 父站点中的计算机与子站点中的计算机之间创建计算机关联。 计算机关联是特定于站点的，不会复制。  

#### <a name="to-create-a-computer-association"></a>创建计算机关联  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“用户状态迁移” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建计算机关联” 。  

4.  在“计算机关联属性”  对话框的“计算机关联”  选项卡上，指定具有要捕获的用户状态的源计算机，以及要在其上还原用户状态数据的目标计算机。  

5.  在“用户帐户”  选项卡上，指定要迁移到目标计算机的用户帐户。 指定下列设置之一：  

    -   **捕获并还原所有用户帐户**：此设置捕获和还原所有用户帐户。 使用此设置来创建与同一源计算机的多个关联。  

    -   **捕获所有用户帐户并还原指定的帐户**：此设置捕获源计算机上的所有用户帐户，并且仅在目标计算机上还原指定的帐户。 此外，你可以在要创建与同一源计算机的多个关联时使用此设置。  

    -   **捕获并还原指定的用户帐户**：此设置仅捕获和还原指定的帐户。 如果选择此设置，你无法创建与同一源计算机的多个关联。  

##  <a name="BKMK_MigrationFails"></a> 在操作系统部署失败时还原用户状态数据  
 如果操作系统部署失败，请使用 USMT 10.0 LoadState 功能检索在部署过程中捕获的用户状态数据。 这包括存储在状态迁移点上的数据，或者以本地方式保存在目标计算机上的数据。 有关此 USMT 功能的详细信息，请参阅 [LoadState 语法](https://technet.microsoft.com/library/mt299188\(v=vs.85\).aspx)。  
