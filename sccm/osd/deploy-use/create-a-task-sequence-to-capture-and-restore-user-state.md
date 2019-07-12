---
title: 捕获和还原用户状态
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 任务序列捕获和还原 OS 部署方案中的用户状态数据。
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c82de88250a7faa44747fc897fcfee09bed45823
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678805"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>在 Configuration Manager 中创建用于捕获和还原用户状态的任务序列

 *适用范围：System Center Configuration Manager (Current Branch)*

 使用 Configuration Manager 任务序列捕获和还原 OS 部署方案中的用户状态数据。 在这些情况下，需要保留当前操作系统的用户状态。 捕获和还原步骤可能会自动添加为任务序列的一部分，具体取决于创建的任务序列的类型。 在其他方案中，你可能需要手动将捕获和还原步骤添加到任务序列。 本文提供必须添加到现有任务序列以捕获和还原用户状态数据的步骤。  



## <a name="task-sequence-steps"></a>任务序列步骤  

若要捕获和还原用户状态，可以向任务序列添加以下步骤：  

- [请求状态存储](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore)：如果将用户状态存储在状态迁移点上，则需要此步骤。  

- [捕获用户状态](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState)：此步骤用于捕获用户状态数据。 然后，它在状态迁移点上存储数据，或在本地磁盘上使用硬链接存储数据。  

- [还原用户状态](/sccm/osd/understand/task-sequence-steps#BKMK_RestoreUserState)：此步骤在目标计算机上还原用户状态数据。 它可以从状态迁移点检索数据，也可以在本地磁盘上进行硬链接。  

- [发布状态存储](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore)：如果将用户状态存储在状态迁移点上，则需要此步骤。 此步骤从状态迁移点中删除数据。  


 使用下列过程添加所需的任务序列步骤以捕获和还原用户状态。 有关创建任务序列的详细信息，请参阅[管理任务序列来自动执行任务](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks)。  



## <a name="capture-the-user-state"></a>捕获用户状态  

 要添加任务序列步骤以捕获用户状态，请使用以下步骤：

1.  在“任务序列”  列表中，选择一个任务序列，然后单击“编辑”  。  

2.  如果要使用状态迁移点来存储用户状态，则将“请求状态存储”  步骤添加到任务序列中。 在“任务序列编辑器”  中，单击“添加”  。 指向“用户状态”  ，然后单击“请求状态存储”  。 配置此步骤的属性和选项，然后单击“应用”  。 有关可用设置的详细信息，请参阅[请求状态存储](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore)。  

3.  将“捕获用户状态”  步骤添加到任务序列中。 在“任务序列编辑器”  中，单击“添加”  。 指向“用户状态”  ，然后单击“捕获用户状态”  。 配置此步骤的属性和选项，然后单击“应用”  。 有关可用设置的详细信息，请参阅[捕获用户状态](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState)。  

    > [!IMPORTANT]  
    >  将此步骤添加到任务序列时，还要设置“OSDStateStorePath”  任务序列变量以指定用户状态数据的存储位置。 如果你以本地方式存储用户状态，请不要指定根文件夹，因为这可能会导致任务序列失败。 在以本地方式存储用户数据时，请始终使用文件夹或子文件夹。 有关此变量的详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)。  

4.  如果使用状态迁移点，则将“发布状态存储”  步骤添加到任务序列中。 在“任务序列编辑器”  中，单击“添加”  。 指向“用户状态”  ，然后单击“发布状态存储”  。 配置此步骤的属性和选项，然后单击“应用”  。 有关可用设置的详细信息，请参阅[发布状态存储](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore)。  

    > [!IMPORTANT]  
    >  在启动“发布状态存储”  步骤之前，必须成功执行在“发布状态存储”  步骤之前执行的任务序列操作。  


 部署此任务序列，以捕获目标计算机上的用户状态。 有关如何部署任务序列的信息，请参阅[部署任务序列](/sccm/osd/deploy-use/deploy-a-task-sequence)。  



## <a name="restore-the-user-state"></a>还原用户状态  

 要添加任务序列步骤以还原用户状态，请使用以下步骤：

1. 在“任务序列”  列表中，选择一个任务序列，然后单击“编辑”  。  

2. 将**还原用户状态**步骤添加到任务序列。 在“任务序列编辑器”  中，单击“添加”  。 指向“用户状态”  ，然后单击“还原用户状态”  。 如有必要，此步骤与状态迁移点建立连接。 配置此步骤的属性和选项，然后单击“应用”  。 有关可用设置的详细信息，请参阅[还原用户状态](/sccm/osd/understand/task-sequence-steps#BKMK_RestoreUserState)。  

   > [!Important]  
   >  使用[捕获用户状态](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState)步骤和选择“使用标准选项捕获所有用户配置文件”  时，必须在“还原用户状态”  步骤中选择“还原本地计算机用户配置文件”  设置。 否则，任务序列将失败。  

   > [!Note]  
   > 如果使用本地硬链接存储用户状态，并且还原不成功，可以手动删除为存储数据而创建的硬链接。 任务序列可以运行 USMTUtils 工具，使用[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)步骤自动执行此操作。 如果使用 USMTUtils 来删除硬链接，请在运行 USMTUtils 之后添加[重启计算机](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer)步骤。  

3. 如果使用状态迁移点来存储用户状态，则将“发布状态存储”  步骤添加到任务序列中。 在“任务序列编辑器”  中，单击“添加”  。 指向“用户状态”  ，然后单击“发布状态存储”  。 配置此步骤的属性和选项，然后单击“应用”  。 有关可用设置的详细信息，请参阅[发布状态存储](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore)。  

   > [!IMPORTANT]  
   >  在启动“发布状态存储”  步骤之前，必须成功执行在“发布状态存储”  步骤之前执行的任务序列操作。  


 部署此任务序列，以还原目标计算机上的用户状态。 有关部署任务序列的信息，请参阅[部署任务序列](/sccm/osd/deploy-use/deploy-a-task-sequence)。  



## <a name="next-steps"></a>后续步骤

[监视任务序列部署](/sccm/osd/deploy-use/monitor-operating-system-deployments#BKMK_TSDeployStatus)
