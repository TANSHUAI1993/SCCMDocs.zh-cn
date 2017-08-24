---
title: "创建用于捕获操作系统的任务序列 | Microsoft Docs"
description: "“构建和捕获”任务序列将构建可以包括特定驱动程序和软件更新，以及操作系统的引用计算机。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
caps.latest.revision: "19"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: e9320e40b8e5031ffa3da5e5149c7da718cc87d5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-to-capture-an-operating-system-in-system-center-configuration-manager"></a>创建任务序列来捕获 System Center Configuration Manager 中的操作系统

*适用范围：System Center Configuration Manager (Current Branch)*

当使用任务序列将操作系统部署到 System Center Configuration Manager 中的计算机时，该计算机会安装在任务序列中指定的操作系统映像。 若要自定义操作系统映像以使其包含特定的驱动程序、应用程序、软件更新等，需要使用构建和捕获任务序列来构建引用计算机，然后从该引用计算机捕获操作系统映像。 如果已具有可进行捕获的引用计算机，你可以创建用于捕获操作系统的自定义任务序列。 使用以下部分来捕获自定义操作系统。  

##  <a name="BKMK_BuildCaptureTS"></a> 使用任务序列来构建和捕获引用计算机  
 “构建和捕获”任务序列对引用计算机进行分区和格式化，安装操作系统以及 Configuration Manager 客户端、应用程序和软件更新，然后从引用计算机捕获操作系统。 在分发点上与任务序列（如应用程序）相关联的包必须可用，然后才能创建构建和捕获任务序列。  

###  <a name="BKMK_CreatePackages"></a> 准备操作系统部署  
 有大量方案可用于将操作系统部署到环境中的计算机。 在大多数情况下，将创建任务序列并在“创建任务序列向导”中选择 **安装现有映像包** 来安装操作系统、迁移用户设置、应用软件更新和安装应用程序。 在创建任务序列以安装操作系统之前，以下方面必须已到位：  

-   **必需**  

    -   [启动映像](../get-started/manage-boot-images.md)在 Configuration Manager 控制台中必须可用。  

    -   [操作系统映像](../get-started/manage-operating-system-images.md)在 Configuration Manager 控制台中必须可用。  

-   **必需（若使用）**  

    -   [驱动程序包](../get-started/manage-drivers.md)在 Configuration Manager 控制台中必须可用，该程序包包含必要的 Windows 驱动程序以支持引用计算机上的硬件。 有关管理驱动程序的任务序列步骤的详细信息，请参阅[使用任务序列安装设备驱动器](../get-started/manage-drivers.md#BKMK_TSDrivers)。  

    -   必须在 Configuration Manager 控制台中同步[软件更新](../../sum/get-started/synchronize-software-updates.md)。  

    -   必须将[应用程序](../../apps/deploy-use/create-applications.md)添加到 Configuration Manager 控制台。  

###  <a name="BKMK_CreateBuildCaptureTS"></a> 创建一个构建和捕获任务序列  
 使用下列过程使用任务序列构建引用计算机和捕获操作系统。  

#### <a name="to-create-a-task-sequence-that-builds-and-captures-an-operating-system-image"></a>创建用于构建和捕获操作系统映像的任务序列  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“任务序列” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建任务序列”  以启动创建任务序列向导。  

4.  在“创建新的任务序列”  页上，选择“构建并捕获引用操作系统映像包” 。  

5.  在“任务序列信息”  页上，指定以下设置，然后单击“下一步” 。  

    -   “任务序列名称”：指定用于标识任务序列的名称。  

    -   “描述”：指定由该任务序列所执行的任务描述，例如任务序列创建的操作系统的描述。  

    -   “启动映像”：指定用于安装操作系统映像的启动映像。  

        > [!IMPORTANT]  
        >  启动映像的体系结构必须与目标计算机的硬件体系结构兼容。  

6.  在“安装 Windows”  页上，指定以下设置，然后单击“下一步” 。  

    -   **映像包**：指定包含安装操作系统所需文件的操作系统映像包。  

    -   “映像索引”：指定要安装的操作系统。 如果操作系统映像包含多个版本，则选择你想要安装的版本。  

    -   “产品秘钥”：指定要安装的 Windows 操作系统的产品密钥。 你可以指定编码的批量许可证密钥和标准产品密钥。 如果使用非编码的产品密钥，则必须通过短划线 (-) 分隔每组 5 个字符。 例如： *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   “服务器授权模式”：指定服务器许可证为“每客户” , 或未指定许可证。 如果服务器许可证为“每服务器” ，则还需指定服务器连接的最大数量。  

    -   指定如何处理在部署操作系统时使用的管理员帐户。  

        -   “随机生成本地管理员密码并禁用所有支持的平台上的帐户”：指定是否使用 Configuration Manager 创建本地管理员帐户的随机密码并在部署操作系统时禁用该帐户。  

        -   “启用该账户并指定本地管理员密码”：指定是否在部署了操作系统的所有计算机上使用相同的本地管理员帐户密码。  

7.  在“配置网络”  页上，指定以下设置，然后单击“下一步” 。  

    -   “加入工作组”：指定是否在部署操作系统时将目标计算机添加到工作组。  

    -   “加入域”：指定是否在部署操作系统时将目标计算机添加到域。 在“域” 中，指定域的名称。  

        > [!IMPORTANT]  
        >  你可以浏览以查找本地林中的域，但对于远程林则必须指定域名。  

         你还可以指定组织单位 (OU)。 这是一项可选设置，用于指定在其中创建计算机帐户的 OU 的 LDAP X.500 可分辨名称（如果尚未存在）。  

    -   “帐户”：指定具有加入指定域的权限的帐户的用户名和密码。 例如： *domain\user* 或 *%variable%*。  

        > [!IMPORTANT]  
        >  如果打算迁移域设置或工作组设置，你必须输入适当的域凭据。  

8.  在“安装 Configuration Manager”页上，指定 Configuration Manager 客户端包（其中包含要安装 Configuration Manager 客户端的源文件），并添加安装客户端所需的任何其他属性，然后单击“下一步”。  

     有关可用于安装客户端的属性的详细信息，请参阅[关于客户端安装属性](../../core/clients/deploy/about-client-installation-properties.md)。  

9. 在“包括更新”  页上，指定是安装必需的软件更新、所有软件更新还是不安装软件更新，然后单击“下一步” 。 如果指定要安装软件更新，Configuration Manager 将只会安装以包含目标计算机的集合为目标的那些软件更新。  

10. 在“安装应用程序”  页上，指定要安装在目标计算机上的应用程序，然后单击“下一步” 。 如果指定多个应用程序，你也可以指定任务序列在特定应用程序的安装失败时继续进行。  

11. 在“系统准备”  页上，指定以下设置，然后单击“下一步” 。  

    -   **包**：指定 Configuration Manager 包，其中包含要用于捕获引用计算机设置的适当版本的 Sysprep。  

         如果你运行的操作系统版本是 Windows Vista 或更高版本，则 Sysprep 自动安装在计算机上，而且你不必指定包。  

12. 在“映像属性”  页上，指定以下操作系统映像设置，然后单击“下一步” 。  

    -   “创建者”：指定创建操作系统映像的用户的名称。  

    -   “版本”：指定与操作系统映像关联的用户定义版本号。  

    -   “描述”：指定操作系统计算机映像的用户定义描述。  

13. 在“捕获映像”  页上，指定以下设置，然后单击“下一步” 。  

    -   “路径”：指定存储输出 .WIM 文件的共享网络文件夹。 此文件包含以你通过使用此向导指定的设置为基础的操作系统映像。 如果指定包含现有 .WIM 文件的文件夹，则会覆盖现有文件。  

    -   “账户”：指定对存储映像的网络共享具有权限的 Windows 帐户。  

14. 完成向导。  

15. 要向任务序列中添加其他步骤，请选择所创建的任务序列并单击“编辑” 。 有关如何编辑任务序列的信息，请参阅[编辑任务序列](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence)。  

 采用以下其中一种方式将任务序列部署到引用计算机：  

-   如果引用计算机为 Configuration Manager 客户端，则可以将构建和捕获任务序列部署到包含引用计算机的集合。 有关如何部署操作系统映像的信息，请参阅 [Create a task sequence to install an operating system](create-a-task-sequence-to-install-an-operating-system.md)（创建任务序列以安装操作系统）。  

    > [!NOTE]  
    >  如果任务序列具有磁盘分区任务序列步骤，请不要在部署任务序列时选择“下载程序”  选项。  

-   如果引用计算机不是 Configuration Manager 客户端，或者如果想手动在引用计算机上运行任务序列，则请运行“创建任务序列媒体向导”以创建可启动媒体。 有关如何创建可启动媒体的信息，请参阅[创建可启动媒体](create-bootable-media.md)。  

##  <a name="BKMK_CaptureExistingRefComputer"></a> 从现有引用计算机中捕获操作系统映像  
 如果已具有可随时用于捕获的引用计算机，则可以创建用于从引用计算机捕获操作系统的任务序列。 将使用“捕获操作系统映像”  任务序列步骤可从引用计算机捕获一个或多个映像，并将它们存储在指定网络共享上的映像文件 (wim) 文件中。 在 Windows PE 中使用启动映像启动引用计算机，将引用计算机上的每个硬盘驱动器作为 .wim 文件中的单独映像进行捕获。 如果引用计算机有多个驱动器，则生成的 .wim 文件对于每个卷将包含单独的映像。 仅捕获格式化为 NTFS 或 FAT32 的卷。 其他格式的卷和 USB 卷会被忽略。  

 使用以下过程从现有引用计算机中捕获操作系统映像。  

#### <a name="to-capture-an-operating-system-from-an-existing-reference-computer"></a>从现有引用计算机中捕获操作系统  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“任务序列” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建任务序列”  以启动创建任务序列向导。  

4.  在“创建新的任务序列”  页面上，选择“创建新的自定义任务序列” 。  

5.  在“任务序列信息”  页面上，指定任务序列的名称和任务序列的描述。  

6.  指定任务序列的启动映像。 此启动映像用于使用 Windows PE 启动引用计算机。  有关详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

7.  完成向导。  

8.  在“任务序列” 中，选择自定义任务序列，然后在“任务序列”  组中的“主页”  选项卡上，单击“编辑”  ，以打开任务序列编辑器。  

9. 仅当引用计算机上安装了 Configuration Manager 客户端时才使用此步骤。  

     依次单击**添加**和**映像**，然后单击[准备 ConfigMgr 客户端以便捕获](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)。 此任务序列步骤在引用计算机上获得 Configuration Manager 客户端，并且准备该客户端用于进行捕获（这是映像创建过程的一部分）。  

10. 依次单**添加**和**映像**，然后单击[准备 Windows 以便捕获](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture)。 此任务序列操作运行 Sysprep，然后将计算机重新启动到为该任务序列指定的 Windows PE 启动映像。 要使此操作成功完成，引用计算机不可加入域。  

11. 依次单击**添加**和**映像**，然后单击[捕获操作系统映像](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)。  此任务序列步骤将仅从 Windows PE 运行，以捕获引用计算机上的硬盘驱动器。 对任务序列步骤配置下列设置。  

    -   “名称” 和“描述” : Optionally, you can change the name of the task sequence step 和“描述” provide a description.  

    -   “目标”：指定存储输出 .WIM 文件的共享网络文件夹。 此文件包含以你通过使用此向导指定的设置为基础的操作系统映像。 如果指定包含现有 .WIM 文件的文件夹，则会覆盖现有文件。  

    -   “描述”, 和“创建者” （可选）提供有关将捕获的映像的详细信息。  

    -   “捕获操作系统映像帐户”：指定对指定的网络共享具有权限的 Windows 帐户。 单击“设置”  以指定该 Windows 帐户的名称。  

     单击“确定”  关闭任务序列编辑器。  

 采用以下其中一种方式将任务序列部署到引用计算机：  

-   如果引用计算机为 Configuration Manager 客户端，则可以将任务序列部署到包含引用计算机的集合。 有关如何部署操作系统映像的信息，请参阅 [Create a task sequence to install an operating system](create-a-task-sequence-to-install-an-operating-system.md)（创建任务序列以安装操作系统）。  

-   如果引用计算机不是 Configuration Manager 客户端，或者如果想手动在引用计算机上运行任务序列，则请运行“创建任务序列媒体向导”以创建可启动媒体。 有关如何创建可启动媒体的信息，请参阅[创建可启动媒体](create-bootable-media.md)。  

##  <a name="BKMK_BuildandCaptureTSExample"></a> 用于构建和捕获操作系统映像的任务序列示例  
 使用下表作为创建任务序列以构建和捕获操作系统映像时的指导。 该表将帮助您决定任务序列步骤的常规顺序，以及如何将这些任务序列步骤组织并构建成逻辑组。 你创建的任务序列可能与此示例有所不同，可以包含更多或较少的任务序列步骤和组。  

> [!IMPORTANT]  
>  始终使用“创建任务序列向导”来创建此类型的任务序列。  

 使用“新任务序列”  创建此新任务序列时，如果您手动将这些任务序列步骤添加至现有任务序列，则某些任务序列步骤名称可能与应使用的名称不同。 下表显示了命名差异：  

|新建任务序列向导任务序列步骤名称|相当的任务序列编辑器步骤名称|  
|------------------------------------------------------|-----------------------------------------------|  
|在 Windows PE 中重新启动|重新启动到 Windows PE 或硬盘|  
|对磁盘 0 分区|格式化磁盘并分区|  
|应用设备驱动程序|自动应用驱动程序|  
|安装更新|安装软件更新|  
|加入工作组|加入域或工作组|  
|准备 ConfigMgr 客户端|Prepare ConfigMgr Client for Capture|  
|准备操作系统|Prepare Windows for Capture|  
|捕获引用计算机|捕获操作系统映像|  

|任务序列组/步骤|参考|  
|-------------------------------|---------------|  
|构建引用计算机 - **（新建任务序列组）**|创建任务序列组。 任务序列组将类似的任务序列步骤放在一起，以获得更佳的组织和错误控制。<br /><br /> 此组包含构建引用计算机所需的操作。|  
|在 Windows PE 中重新启动|使用此任务序列步骤指定目标计算机的重新启动选项。 此步骤会向用户显示一则消息，指出将重新启动计算机以便可以继续安装。<br /><br /> 此步骤使用只读 **_SMSTSInWinPE** 任务序列变量。 如果关联值等于 **false** ，该任务序列步骤将继续。|  
|对磁盘 0 分区|使用此任务序列步骤指定格式化目标计算机上的硬盘时所需的操作。 默认磁盘编号为 **0**。<br /><br /> 此步骤使用只读的 **_SMSTSClientCache** 任务序列变量。 如果 Configuration Manager 客户端缓存不存在，则会运行此步骤。|  
|应用操作系统|使用此任务序列步骤在目标计算机上安装指定的操作系统映像。 此步骤首先删除目标计算机上相应的顺序磁盘卷上的所有文件（特定于 Configuration Manager 的控制文件除外），然后将 WIM 文件中包含的所有卷映像应用到该顺序磁盘卷。|  
|应用 Windows 设置|使用此任务序列步骤配置目标计算机的 Windows 设置配置信息。|  
|应用网络设置|使用此任务序列步骤指定目标计算机的网络或工作组配置信息。|  
|应用设备驱动程序|使用此任务序列步骤匹配驱动程序，并将其作为操作系统部署的一部分进行安装。 你可以通过选择“考虑所有类别的驱动程序”  允许 Windows 安装程序搜索所有现有的驱动程序类别；或者选择“将驱动程序匹配限制为仅考虑所选类别的驱动程序” 以限制 Windows 安装程序搜索的驱动程序类别。<br /><br /> 此步骤使用只读 **_SMSTSMediaType** 任务序列变量。 如果关联值不等于 **FullMedia** ，则将运行此任务序列步骤。|  
|安装 Windows 和 ConfigMgr|使用此任务序列步骤安装 Configuration Manager 客户端软件。 Configuration Manager 安装和注册 Configuration Manager 客户端 GUID。 你可以在“安装属性”  窗口中分配必要的安装参数。|  
|安装更新|使用此任务序列步骤指定如何在目标计算机上安装软件更新。 在运行此任务序列步骤时，才会评估目标计算机是否有适用的软件更新。 此时，会与其他 Configuration Manager 托管客户端一样，评估目标计算机是否有合适的软件更新。<br /><br /> 此步骤使用只读 **_SMSTSMediaType** 任务序列变量。 如果关联值不等于 **FullMedia** ，则将运行此任务序列步骤。|  
|捕获引用计算机 - **（新建任务序列组）**|创建其他任务序列组。 此组包含准备和捕获引用计算机的必需步骤。|  
|加入工作组|使用此任务序列步骤来指定使目标计算机加入工作组需要的信息。|  
|Prepare ConfigMgr Client for Capture|使用此步骤在引用计算机上获得 Configuration Manager 客户端，并且使其准备好以便捕获（这是映像创建过程的一部分）|  
|准备操作系统|使用此任务序列步骤来指定当从引用计算机捕获 Windows 设置时要使用的 Sysprep 选项。 此任务序列步骤运行 Sysprep，然后将计算机重新启动到为该任务序列指定的 Windows PE 启动映像。|  
|捕获操作系统映像|使用此任务序列步骤来访问特定的现有网络共享和在保存映像时使用的 .WIM 文件。 当使用“添加操作系统映像包向导” 添加操作系统映像包时，此位置用作包源位置。|  

 从引用计算机中捕获了映像后，请不要从该引用计算机中捕获另一个操作系统映像，因为在初始配置过程中会创建注册表项。 请在每次捕获操作系统映像时创建新引用计算机。 如果计划使用同一引用计算机来创建将来的操作系统映像，请首先卸载 Configuration Manager 客户端，然后重新安装 Configuration Manager 客户端。  

## <a name="next-steps"></a>后续步骤  
[部署企业版操作系统的方法](methods-to-deploy-enterprise-operating-systems.md)
