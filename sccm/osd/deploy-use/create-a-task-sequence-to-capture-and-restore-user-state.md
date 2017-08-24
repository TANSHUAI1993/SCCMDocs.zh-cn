---
title: "创建用于捕获和还原用户状态的任务序列 | Microsoft Docs"
description: "使用 System Center Configuration Manager 任务序列捕获和还原操作系统部署方案中的用户状态数据。"
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 4b3668094d576b1b8710f08b384aa2f7c5eb0cca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-system-center-configuration-manager"></a>创建任务序列以捕获和还原 System Center Configuration Manager 中的用户状态

*适用范围：System Center Configuration Manager (Current Branch)*

在希望保留当前操作系统的用户状态的操作系统部署方案中，可以使用 System Center Configuration Manager 任务序列来捕获和还原用户状态数据。 捕获和还原步骤可能会自动添加为任务序列的一部分，具体取决于创建的任务序列的类型。 在其他方案中，你可能需要手动将捕获和还原步骤添加到任务序列。 本主题提供必须添加到现有任务序列以捕获和还原用户状态数据的步骤。  

##  <a name="BKMK_CaptureRestoreUserState"></a>如何捕获和还原用户状态数据  
 若要捕获和还原用户状态，必须向任务序列添加以下步骤：  

-   **请求状态存储**：只有当将用户状态存储在状态迁移点上时才需要此步骤。  

-   **捕获用户状态**：此步骤捕获用户状态数据，并将其存储在状态迁移点上或使用链接以本地方式存储。  

-   **还原用户状态**：此步骤在目标计算机上还原用户状态数据。 它可从用户状态迁移点或目标计算机中检索数据。  

-   **发布状态存储**：只有当将用户状态存储在状态迁移点上时才需要此步骤。 此步骤从状态迁移点中删除此数据。  

 使用下列过程添加所需的任务序列步骤以捕获和还原用户状态。 有关创建任务序列的详细信息，请参阅[管理任务序列来自动执行任务](manage-task-sequences-to-automate-tasks.md)。  

#### <a name="to-add-task-sequence-steps-to-capture-the-user-state"></a>添加任务序列步骤以捕获用户状态  

1.  在“任务序列”列表中，选择一个任务序列，然后单击“编辑”。  

2.  如果使用状态迁移点来存储用户状态，则将“请求状态存储”步骤添加到任务序列中。 在“任务序列编辑器”对话框中，单击“添加”，指向“用户状态”，再单击“请求状态存储”。 为“请求状态存储”步骤指定下列属性和选项，然后单击“应用”。  

     在“属性”选项卡上，指定下列选项：  

    -   输入步骤的名称和描述。  

    -   单击“从计算机捕获状态”。  

    -   在“重试次数”框中，指定在发生错误时任务序列尝试捕获用户状态数据的次数。  

    -   在“重试延迟(秒)”框中，指定任务序列在重试捕获数据之前等待的秒数。  

    -   选择“如果计算机帐户未能连接到状态存储，则使用网络访问帐户”复选框以指定是否使用 Configuration Manager [网络访问帐户](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#a-namebkmknaaa-network-access-account)连接到状态存储。  

     在“选项”选项卡上，指定下列选项：  

    -   如果希望任务序列在此步骤失败时继续执行下一步，则选中“出错时继续”复选框。  

    -   指定必须满足的任何条件（如果出错，任务序列只有满足这些条件方可继续执行）。  

3.  将“捕获用户状态”步骤添加到任务序列中。 在“任务序列编辑器”对话框中，单击“添加”，指向“用户状态”，再单击“捕获用户状态”。 为“捕获用户状态”步骤指定下列属性和选项，然后单击“确定”。  

    > [!IMPORTANT]  
    >  将此步骤添加到任务序列时，还要设置“OSDStateStorePath”任务序列变量以指定用户状态数据的存储位置。 如果你以本地方式存储用户状态，请不要指定根文件夹，因为这可能会导致任务序列失败。 在以本地方式存储用户数据时，请始终使用文件夹或子文件夹。 有关此变量的信息，请参阅[捕获用户状态任务序列操作变量](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState)。  

     在“属性”选项卡上，指定下列选项：  

    -   输入步骤的名称和描述。  

    -   指定包含用于捕获用户状态数据的 USMT 源文件的包。  

    -   指定要捕获的用户配置文件：  

        -   单击“使用标准选项捕获所有用户配置文件”，以捕获所有用户配置文件。  

        -   单击“自定义用户配置文件捕获”，以指定要捕获的单独用户配置文件。 选择包含用户配置文件信息的配置文件（miguser.xml、migsys.xml 或 migapp.xml）。 不能在这里使用 config.xml 配置文件，但你可以手动将其添加到使用 OSDMigrageAdditionalCaptureOptions 和 OSDMigrateAdditionalRestoreOptions 变量的 USMT 命令行。

    -   选择“启用详细日志记录”，以指定在出错时将多少信息写入到日志文件中。  

    -   选择“使用加密文件系统(EFS)跳过文件”。  

    -   选择“使用文件系统访问权限复制”指定下列设置：  

        -   **如果无法捕获某些文件则继续**：此设置允许任务序列步骤继续执行迁移过程，即使无法捕获某些文件也是如此。 如果禁用此选项，并且无法捕获文件，则任务序列步骤会失败。 默认情况下会启用此选项。  

        -   **通过使用链接而不是通过复制文件以本地方式进行捕获**：此设置允许你使用 USMT 4.0 中提供的硬链接迁移功能。 如果使用的 USMT 版本早于 USMT 4.0，则会忽略此设置。  

        -   **在脱机模式下进行捕获（仅 Windows PE）**：利用此设置，你无需启动到现有的操作系统就能从 Windows PE 中捕获用户状态。 如果使用的 USMT 版本早于 USMT 4.0，则会忽略此设置。  

    -   选择“使用卷影复制服务(VSS)进行捕获”。 如果使用的 USMT 版本早于 USMT 4.0，则会忽略此设置。  

     在“选项”选项卡上，指定下列选项：  

    -   如果希望任务序列在此步骤失败时继续执行下一步，则选中“出错时继续”复选框。  

    -   指定必须满足的任何条件（如果出错，任务序列只有满足这些条件方可继续执行）。  

4.  如果正在使用状态迁移点来存储用户状态，则将[发布状态存储](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)步骤添加到任务序列中。 在“任务序列编辑器”对话框中，单击“添加”，指向“用户状态”，再单击“发布状态存储”。 为“发布状态存储”步骤指定下列属性和选项，然后单击“确定”。  

    > [!IMPORTANT]  
    >  在启动“发布状态存储”步骤之前，必须成功执行在“发布状态存储”步骤之前执行的任务序列操作。  

     在“属性”选项卡上，输入步骤的名称和描述。  

     在“选项”选项卡上，指定下列选项。  

    -   如果希望任务序列在此步骤失败时继续执行下一步，则选中“出错时继续”复选框。  

    -   指定必须满足的任何条件（如果出错，任务序列只有满足这些条件方可继续执行）。  

 部署此任务序列，以捕获目标计算机上的用户状态。 有关如何部署任务序列的信息，请参阅[部署任务序列](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。  

#### <a name="to-add-task-sequence-steps-to-restore-the-user-state"></a>添加任务序列步骤以还原用户状态  

1.  在“任务序列”列表中，选择一个任务序列，然后单击“编辑”。  

2.  将[还原用户状态](../understand/task-sequence-steps.md#BKMK_RestoreUserState)步骤添加到任务序列。 在“任务序列编辑器”对话框中，单击“添加”，指向“用户状态”，再单击“还原用户状态”。 此步骤与状态迁移点建立连接。 为“还原用户状态”步骤指定下列属性和选项，然后单击“确定”。  

     在“属性”选项卡上，指定下列属性：  

    -   输入步骤的名称和描述。  

    -   指定包含 USMT 的包，以还原用户状态数据。  

    -   指定要还原的用户配置文件：  

        -   单击“使用标准选项还原所有捕获的用户配置文件”，以还原所有用户配置文件。  

        -   单击“自定义用户配置文件还原”，以还原单个用户配置文件。 选择包含用户配置文件信息的配置文件（miguser.xml、migsys.xml 或 migapp.xml）。 不能在这里使用 config.xml 配置文件，但你可以手动将其添加到使用 OSDMigrageAdditionalCaptureOptions 和 OSDMigrateAdditionalRestoreOptions 变量的 USMT 命令行。

    -   选择“还原本地计算机用户配置文件”，以便为还原的配置文件提供新的密码。 无法迁移本地配置文件的密码。  

        > [!NOTE]  
        >  当拥有本地用户帐户并使用[捕获用户状态](../understand/task-sequence-steps.md#BKMK_CaptureUserState)步骤和选择“使用标准选项捕获所有用户配置文件”时，必须在[还原用户状态](../understand/task-sequence-steps.md#BKMK_RestoreUserState)步骤中选择“还原本地计算机用户配置文件”设置，否则任务序列将会失败。  

    -   如果希望“还原用户状态”步骤在无法还原文件时继续执行，则选择“如果无法还原某些文件则继续”。  

         如果使用本地链接存储用户状态，并且还原不成功，则管理用户可以手动删除为存储数据而创建的硬链接，否则任务序列可能会运行 USMTUtils 工具。 如果使用 USMTUtils 来删除硬链接，请在运行 USMTUtils 之后添加[重启计算机](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)步骤。  

    -   选择“启用详细日志记录”，以指定在出错时将多少信息写入到日志文件中。  

     在“选项”选项卡上，指定下列选项：  

    -   如果希望任务序列在此步骤失败时继续执行下一步，则选中“出错时继续”复选框。  

    -   指定必须满足的任何条件（如果出错，任务序列只有满足这些条件方可继续执行）。  

3.  如果正在使用状态迁移点来存储用户状态，则将[发布状态存储](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore)步骤添加到任务序列中。 在“任务序列编辑器”对话框中，单击“添加”，指向“用户状态”，再单击“发布状态存储”。 为“发布状态存储”步骤指定下列属性和选项，然后单击“确定”。  

    > [!IMPORTANT]  
    >  在启动“发布状态存储”步骤之前，必须成功执行在“发布状态存储”步骤之前执行的任务序列操作。  

     在“属性”选项卡上，输入步骤的名称和描述。  

     在“选项”选项卡上，指定下列选项。  

    -   如果希望任务序列在此步骤失败时继续执行下一步，则选中“出错时继续”复选框。  

    -   指定必须满足的任何条件（如果出错，任务序列只有满足这些条件方可继续执行）。  

 部署此任务序列，以还原目标计算机上的用户状态。 有关部署任务序列的信息，请参阅[部署任务序列](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。  

## <a name="next-steps"></a>后续步骤
[监视任务序列部署](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
