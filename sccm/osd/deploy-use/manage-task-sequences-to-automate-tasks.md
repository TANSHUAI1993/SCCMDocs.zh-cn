---
title: 管理任务序列
titleSuffix: Configuration Manager
description: 创建、编辑、部署、导入和导出任务序列，在环境中管理任务并自动执行任务。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 041654b3ba1a25c832232fb26fa09f7ea12e8f97
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537075"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>管理任务序列来自动执行任务

*适用范围：System Center Configuration Manager (Current Branch)*

使用任务序列在 Configuration Manager 环境中自动执行步骤。 这些步骤可将 OS 映像部署到目标计算机，通过一组 OS 安装文件生成和捕获 OS 映像，并捕获和还原用户状态信息。 任务序列位于 Configuration Manager 控制台中。 在“软件库”工作区中，展开“操作系统”，并选择“任务序列”    。 将“任务序列”节点（包括所创建的子文件夹）复制到整个 Configuration Manager 层次结构  。 有关计划的信息，请参阅[计划自动执行任务时的考虑事项](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)。  



## <a name="BKMK_CreateTaskSequence"></a>创建任务序列  

通过使用创建任务序列向导来创建任务序列。 此向导可创建下列类型的任务序列：  

|任务序列类型|更多信息|  
|------------------------|----------------------|  
|[用于安装 OS 的任务序列](create-a-task-sequence-to-install-an-operating-system.md)|此任务序列类型创建用于安装 OS 的步骤。 它还包括迁移用户数据、包含软件更新和安装应用程序的选项。|  
|[用于升级 OS 的任务序列](create-a-task-sequence-to-upgrade-an-operating-system.md)|此任务序列类型创建用于升级 OS 的步骤。 它还包括包含软件更新和安装应用程序的选项。|  
|[用于捕获 OS 的任务序列](create-a-task-sequence-to-capture-an-operating-system.md)|此任务序列类型创建从引用计算机构建和捕获 OS 的步骤。 在捕获映像之前，可以在引用计算机上包括软件更新和安装应用程序。|  
|[用于捕获和还原用户状态的任务序列](create-a-task-sequence-to-capture-and-restore-user-state.md)|此任务序列提供要添加到现有任务序列以捕获和还原用户状态数据的步骤。|  
|[自定义任务序列](create-a-custom-task-sequence.md)|此任务序列类型不会给任务序列添加任何步骤。 创建此任务序列后，编辑并添加步骤。|  



## <a name="BKMK_ModifyTaskSequence"></a>编辑  

通过添加或删除步骤、添加或删除组或者更改步骤的顺序来修改任务序列。 使用以下过程修改现有任务序列：  

> [!IMPORTANT]  
> 编辑使用创建任务序列向导创建的任务序列时，步骤的名称可能是步骤的操作或类型。 例如，可能会看到名为“分区磁盘 0”的步骤，该名称是类型为[格式化磁盘并分区](/sccm/osd/understand/task-sequence-steps#BKMK_FormatandPartitionDisk)的步骤的操作。 所有任务序列步骤均按其类型记录，并不一定按编辑器中显示的步骤名称记录。  

### <a name="process-to-edit-a-task-sequence"></a>编辑任务序列的过程  

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，然后选择“任务序列”  节点。  

2. 在“任务序列”  列表中，选择要编辑的任务序列。  

3. 在功能区的“主页”选项卡上，在“任务序列”组中，选择“编辑”    。 然后执行以下任意操作：  

    - 若要添加任务序列步骤，请选择“添加”，选择步骤类型，然后选择要添加的步骤  。 例如，若要添加[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)步骤，可选择“添加”，选择“常规”，然后选择“运行命令行”    。  

    - 若要向任务序列中添加组，请选择“添加”  ，然后选择“新建组”  。 添加组后，可以向组中添加步骤。  

    - 要更改任务序列中步骤和组的顺序，请选择要重新排序的步骤或组，然后使用“上移项目”或“下移项目”图标   。 一次只能移动一个步骤或组。  

    - 若要删除步骤或组，请选择该步骤或组并选择“删除”  。  

4. 选择“确定”保存所做的更改并关闭窗口  。 选择“应用”保存所做的更改并使任务序列编辑器保持打开状态  。  

有关可用的任务序列步骤列表，请参阅[任务序列步骤](/sccm/osd/understand/task-sequence-steps)。  

### <a name="bkmk_sedo"></a> 回收锁定以编辑任务序列

<!--3699337-->
如果 Configuration Manager 控制台停止响应，你可能会被锁定而无法做出进一步更改，直到 30 分钟后锁定到期。 此锁定是 Configuration Manager SEDO（分布式对象的序列化编辑）系统的一部分。 有关详细信息，请参阅 [Configuration Manager SEDO](/sccm/develop/core/understand/sedo)。

从版本1906开始, 可以清除任务序列上的锁定。 此操作仅适用于被锁定的用户帐户，并且仅可在站点授予锁定的同一设备上执行。 尝试访问已锁定的任务序列时，现在可以放弃更改，并继续编辑对象  。 锁定过期时这些更改将丢失。


## <a name="bkmk_prop-general"></a> 配置软件中心属性

使用以下过程配置软件中心中显示的任务序列的详细信息。 这些详细信息仅供参考。  

1. 在 Configuration Manager 工作区中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”    。  

2. 选择要编辑的任务序列，然后选择“属性”  。  

3. 在“常规”  选项卡上，可使用软件中心的以下设置：  

    - **需要重启**：让用户了解安装期间是否需要重新启动。  

    - **下载大小 (MB)** ：指定任务序列在软件中心中显示多少兆字节。  

    - **预计运行时间(分钟)** ：指定任务序列在软件中心中显示的预计运行时间（以分钟为单位）。  



## <a name="bkmk_prop-advanced"></a> 配置高级任务序列设置

按照以下步骤在 Configuration Manager 客户端上配置任务序列的行为。  

1. 在 Configuration Manager 工作区中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”    。  

2. 选择要编辑的任务序列，然后选择“属性”  。  

3. 在“高级”选项卡上，有下列可用设置  ：  

    -  首先运行其他程序：选择此选项，可在此任务序列之前在其他包中运行一个程序。 默认情况下，此复选框已清除。 不需要单独部署指定要首先运行的程序。  

        > [!IMPORTANT]
        > 此设置仅适用于在完整 OS 中运行的任务序列。 如果使用 PXE 或启动媒体启动任务序列，Configuration Manager 将忽略此设置。  

        -  包：浏览包含要在此任务序列之前运行的程序的包。  

        -  程序：选择要在此任务序列之前运行的程序。  

        > [!NOTE]  
        > 如果所选程序在客户端上运行失败，则任务序列不会运行。 如果所选程序成功运行，则它不会再次运行，即使在同一客户端上重新运行了任务序列。  

    - **取消任务序列通知**：选择此选项可隐藏“新软件可用”Toast 通知  。 “新软件”  图标仍会显示在软件中心的通知区域中。 默认情况下禁用此选项。  

    -  在部署计算机上禁用此任务序列：如果选择此选项，Configuration Manager 会暂时禁用包含此任务序列的所有部署。 也会将任务序列从可运行部署列表中删除。 在启用之前，不会运行任务序列。 默认情况下禁用此选项。  

    -  最大允许运行时间：指定预计任务序列在目标计算机上运行的最长时间（分钟）。 使用等于或大于零的整数。 默认情况下，此值为 120 分钟。  

        > [!IMPORTANT]  
        > 当将维护时段用于部署此任务序列的集合时，如果“最大允许运行时间”  大于计划的维护时段，就可能出现冲突。 如果最大运行时间设置为 0  ，任务序列将在维护时段启动。 维护时段关闭后，它将继续运行，直到完成或失败。 因此，最大运行时间设置为“0”的任务序列可能运行到维护时段结束后。  如果将最大运行时间设置为具体时段（不为“0”），且此时段大于任何可用维护时段的长度，那么该任务序列不会运行。 有关详细信息，请参阅[如何使用维护时段](/sccm/core/clients/manage/collections/use-maintenance-windows)。  

        如果值设置为“0”  ，则 Configuration Manager 会将最大允许运行时间计算为 12  小时（720 分钟）以监视进度。 但是，只要倒计时持续时间不超过维护时段值，任务序列便会启动。  

        > [!NOTE]  
        > 当达到最大运行时间时，如果将选项设置为“使用管理权限运行”  ，而未将选项设置为“允许用户与此程序交互”  ，Configuration Manager 就会停止任务序列。 如果任务序列本身未停止，则达到最大允许运行时间后，Configuration Manager 将停止监视任务序列。  

    -  使用启动映像：可在运行任务序列时使用选定的启动映像。 选择“浏览”  可选择其他启动映像。 清除此选项，可在运行任务序列时禁用选定的启动映像。  

    -  此任务序列可以在任何平台上运行：如果选择此选项，则 Configuration Manager 在任务序列运行时不会检查目标计算机的平台类型。 默认情况下选择此选项。  

    -  此任务序列仅可以在指定的客户端平台上运行：此选项指定支持运行此任务序列的处理器、OS 版本和服务包。 选择此选项时，还必须从列表中至少选择一个平台。 默认情况下不选择任何平台。 Configuration Manager 在评估集合中的哪些目标计算机将接收部署的任务序列时，使用此信息。  

        > [!NOTE]  
        > 从启动媒体或 PXE 运行任务序列时，Configuration Manager 将忽略此选项。 任务序列的运行方式就如同“此程序可以在任何平台上运行”  选项处于选中状态。  



## <a name="configure-high-impact-task-sequence-settings"></a>配置影响重大的任务序列设置

将任务序列配置为“影响重大”，并自定义用户在运行任务序列时收到的消息。


### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>将任务序列设置为影响重大的任务序列

使用下列过程将任务序列设置为“影响重大”。

> [!NOTE]  
> 任何符合特定条件的任务序列都将自动定义为“影响重大”。 有关详细信息，请参阅[管理高风险部署](/sccm/protect/understand/settings-to-manage-high-risk-deployments)。

1. 在 Configuration Manager 工作区中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”    。  

2. 选择要编辑的任务序列，然后选择“属性”  。  

3. 在“用户通知”  选项卡上，选择“这是影响重大的任务序列”  。  


### <a name="create-a-custom-notification-for-high-risk-deployments"></a>创建高风险部署的自定义通知

使用以下过程为影响重大的部署创建自定义通知。

1. 在 Configuration Manager 工作区中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”    。  

2. 选择要编辑的任务序列，然后选择“属性”  。  

3. 在“用户通知”  选项卡上，选择“使用自定义文本”  。  

    > [!NOTE]
    > 只能在已选择选项“这是影响重大的任务序列”  时设置用户通知文本。  

4. 配置下列设置：  

    > [!Note]  
    > 每个文本框的最大限制为 255 个字符。  

    - **用户通知标题文本**：指定在软件中心用户通知上显示的蓝色文本。 例如，在默认用户通知中，本部分包含“确认想要升级此计算机上的操作系统”。  

    - **用户通知消息文本**：三个文本框提供自定义通知的正文。 所有文本框都需要添加文本。  

        - 第一个文本框：指定文本的主要正文，通常包含针对用户的说明。 例如，在默认用户通知中，本部分包含“操作系统升级需要一些时间，并且计算机可能会多次重启”。  

        - 第二个文本框：指定文本主要正文下的粗体文本。 例如，在默认用户通知中，本部分包含“此就地升级将安装新的操作系统并自动迁移你的应用、数据和设置”。  

        - 第三个文本框：指定粗体文本下的最后一行文本。 例如，在默认用户通知中，本部分包含“单击‘安装’以开始。 否则，单击‘取消’”的内容。  

#### <a name="example"></a>示例

假设在属性中配置以下自定义通知。

![任务序列属性的自定义“用户通知”选项卡](../media/user-notification.png)

当最终用户从软件中心打开安装时，将显示以下通知消息。

![软件中心中面向最终用户的自定义任务序列通知](../media/user-notification-enduser.png)



## <a name="BKMK_DistributeTS"></a>分发引用的内容  

在客户端运行引用内容的任务序列之前，将该内容分发到分发点。 你可以随时选择任务序列并分发其内容，以便为分发建立一个新的引用包列表。 如果使用更新的内容更改任务序列，则在内容可供客户端使用之前重新分发此内容。 使用以下过程来分发任务序列引用的内容。  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>将引用的内容分发到分发点的过程  

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，然后选择“任务序列”  节点。  

2. 在“任务序列”  列表中，选择要分发的任务序列。  

3. 在功能区的“主页”  选项卡上，在“部署”  组中，选择“分发内容”  。 此操作会启动“分发内容向导”。  

4. 在“常规”页上，验证是否为分发选择了正确的任务序列  。  

5. 在“内容”  页上，验证要分发的内容（例如任务序列引用的启动映像）。  

6. 在“内容目标”页上，指定要在其中分发任务序列内容的集合、分发点或分发点组  。  

    > [!IMPORTANT]  
    > 如果所选任务序列引用已分发到特定分发点的内容，则向导不会列出该分发点。  

7. 完成向导。  

还可以预留任务序列中引用的内容。 Configuration Manager 创建压缩的预安排内容文件，该文件包含所选内容的文件、关联依赖项和关联元数据。 然后在站点服务器、辅助站点或分发点中手动导入内容。 有关如何预留内容文件的详细信息，请参阅[预留内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage)。  



## <a name="BKMK_DeployTS"></a> 部署  

有关详细信息，请参阅 [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence)。

## <a name="BKMK_ExportImport"></a>导出和导入  

导出和导入任务序列（包含或不包含相关对象）。 此引用的内容包括以下对象：  

- OS 映像  
- 启动映像  
- 包（如客户端安装包）  
- 驱动程序包  
- 具有依赖项的应用程序  

导出和导入任务序列时，请考虑以下几点：  

- Configuration Manager 不会在任务序列中导出密码。 如果导出和导入包含密码的任务序列，则编辑导入的任务序列，以重新输入任何密码。 请查看以下可能包含密码的步骤：  

    - [加入域或工作组](/sccm/osd/understand/task-sequence-steps#BKMK_JoinDomainorWorkgroup)  
    - [连接到网络文件夹](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  
    - [运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

- 使用“设置动态变量”  步骤导出任务序列时，Configuration Manager 不会为配置了“机密值”  设置的变量导出值。 导入任务序列后，请重新输入这些变量的值。  

- 如果你具有多个主站点，请在管理中心站点导入任务序列。  


### <a name="process-to-export-task-sequences"></a>导出任务序列的过程  

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，然后选择“任务序列”  节点。  

2. 在“任务序列”  列表中，选择要导出的任务序列。 如果选择多个任务序列，它们将全部存储在一个导出文件上。  

3. 在功能区的“主页”选项卡上，在“任务序列”组中，选择“导出”    。 此操作会启动“导出任务序列向导”。  

4. 在“常规”  页上，指定下列设置：  

    - **文件**：指定导出文件的位置和名称。 如果直接输入文件名，请确保在文件名中包括 .zip 扩展名。 如果浏览导出文件，则向导会自动添加此文件扩展名。  

    - 如果不想导出任务序列依赖项，请取消选中“导出所有任务序列依赖项”  选项。 默认情况下，向导会扫描所有相关对象并与任务序列一起导出它们。 这包括应用程序的任何依赖项。  

    - 如果不想将包源中的内容复制到导出位置，请取消选中“导出所选任务序列和依赖项的所有内容”  选项。 如果选择此选项，“导入任务序列向导”会使用导入路径作为新包源位置。  

    - **管理员备注**：添加要导出的任务序列的说明。  

5. 完成向导。  

该向导会创建以下输出文件：  

- 如果不导出内容，则为一个 .zip 文件。  

- 如果导出内容，则为一个 .zip 文件和一个名为 *export*_files 的文件夹，其中 *export* 是包含导出内容的 .zip 文件的名称。  

如果导出任务序列时包括内容，请确保复制 .zip 文件和 export_files 文件夹，否则导入将失败  。  


### <a name="process-to-import-task-sequences"></a>导入任务序列的过程  

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，然后选择“任务序列”  节点。  

2. 在功能区的“主页”选项卡上，在“创建”组中，选择“导入任务序列”    。 此操作会启动“导入任务序列向导”。  

3. 在功能区的“常规”  页上，指定导出的 .zip 文件。  

4. 在“文件内容”  页上，为要导入的每个对象选择所需的操作。 此页显示已找到的 Configuration Manager 要导入的所有对象。  

    - 如果从未导入对象，请选择“新建”  。  

    - 如果以前导入过对象，请选择下列操作之一：  

        -  忽略重复项（默认值）：此操作不导入对象。 而是由向导将现有对象链接到任务序列。  

        - 覆盖  ：此操作用导入的对象覆盖现有对象。 对于应用程序，你可以添加修订以更新现有应用程序或创建新应用程序。  

5. 完成向导。  

导入任务序列之后，请编辑任务序列以指定原始任务序列中的任何密码。 出于安全原因，不会导出密码。  



## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>任务序列失败时返回上一页

运行任务序列出现故障时，可以返回到上一页面。 在以前版本的 Configuration Manager 中，出现故障时必须重启任务序列。 在以下应用场景中使用“上一页”按钮  ：

- 当计算机在 Windows PE 中启动时，任务序列可用之前可能会先显示任务序列启动对话框。 在此应用场景中选择“下一步”时，会显示任务序列的最后一页，同时显示一条消息，指示无可用的任务序列。 现在，可选择“上一页”  以再次搜索可用任务序列。 在出现可用任务序列之前，可重复此过程。  

- 运行任务序列但分发点上尚无可用从属内容包时，任务序列会失败。 如果缺少的内容未尚未分发，请立即将其分发。 或等待分发点提供该内容。 然后选择“上一页”，让任务序列再次搜索该内容  。



## <a name="BKMK_CreateTSVariables"></a>为计算机和集合创建任务序列变量  

可以为计算机和集合定义自定义的任务序列变量。 为计算机定义的变量称为特定于计算机的任务序列变量。 为集合定义的变量称为特定于集合的任务序列变量。 如有冲突，特定于计算机的变量优先于特定于集合的变量。 此行为意味着，分配到特定计算机的任务序列变量会自动获得比分配到包含该计算机的集合的变量更高的优先级。  

例如，计算机 XYZ 是集合 ABC 的成员。 将 MyVariable 分配到集合 ABC，值为 1。 同时将 MyVariable 分配到计算机 XYZ，值为 2。 分配给计算机 XYZ 的变量优先于分配给集合 ABC 的变量。 当具有此变量的任务序列在计算机 XYZ 上运行时，MyVariable 的值为 2。

可以隐藏特定于计算机和特定于集合的变量，以便它们在 Configuration Manager 控制台中不可见。 使用选项“不要在 Configuration Manager 控制台中显示此值”  时，控制台中不显示该变量的值。 但在变量运行时，任务序列仍可使用该变量。 如果不想再隐藏这些变量，请先删除它们。 然后重新定义变量，而无需选择选项来隐藏它们。  

> [!WARNING]  
> “不要在 Configuration Manager 控制台中显示此值”设置仅适用于 Configuration Manager 控制台  。 变量的值仍会显示在任务序列日志文件 (SMSTS.LOG) 中。

可以在主站点或管理中心站点上管理因计算机而异的变量。 Configuration Manager 不支持一台计算机具有 1,000 个以上的已分配变量。  

> [!IMPORTANT]  
> 将特定于集合的变量用于任务序列时，请注意以下行为：  
>
> - 对集合的更改始终会复制到整个层次结构。 对集合变量所做的任何更改不仅应用于当前站点的成员，还会应用于整个层次结构中该集合的所有成员。  
>  
> - 删除集合时，此操作还会删除为集合配置的任务序列变量。  


### <a name="process-to-create-task-sequence-variables-for-a-computer"></a>为计算机创建任务序列变量的过程  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备”节点   。  

2. 选择目标计算机，然后选择“属性”  。  

3. 在“属性”  对话框中，切换到“变量”  选项卡。  

4. 对于要创建的每个变量，请选择“新建”  图标。 指定任务序列变量的名称  和值  。 若要隐藏变量使其在 Configuration Manager 控制台中不可见，请选择“不在 Configuration Manager 控制台中显示此值”  选项。  

5. 将所有变量添加到计算机属性之后，选择“确定”  。  


### <a name="process-to-create-task-sequence-variables-for-a-collection"></a>为集合创建任务序列变量的过程  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”  工作区，并选择“设备集合”  节点。 选择目标集合，然后选择“属性”  。  

2. 在“属性”  对话框中，切换到“集合变量”  选项卡。  

3. 对于要创建的每个变量，请选择“新建”  图标。 指定任务序列变量的名称  和值  。 若要隐藏变量使其在 Configuration Manager 控制台中不可见，请选择“不在 Configuration Manager 控制台中显示此值”  选项。  

4. 根据需要为 Configuration Manager 指定要在评估任务序列变量时使用的优先级。  

5. 将所有变量添加到集合属性之后，选择“确定”  。  



## <a name="BKMK_AdditionalActionsTS"></a>用于管理任务序列的其他操作  

选择任务序列时，可以使用其他操作来管理任务序列。  

### <a name="available-options"></a>可用选项

#### <a name="edit"></a>编辑

有关详细信息，请参阅[编辑任务序列](#BKMK_ModifyTaskSequence)。

#### <a name="enable"></a>启用

启用任务序列，以便其能在客户端运行。 不需要在启用后重新部署任务序列。  

#### <a name="disable"></a>禁用

禁用任务序列，使其无法在计算机上运行。 可以部署禁用的任务序列，但在启用之前计算机不会运行任务序列。  

#### <a name="export"></a>导出

有关详细信息，请参阅[导出和导入任务序列](#BKMK_ExportImport)。

#### <a name="copy"></a>复制

为所选的任务序列创建副本。 在根据现有任务序列创建新的任务序列时，此操作很有用。

为某个文件夹中的任务序列创建副本时，副本会在该文件夹中列出，直至你刷新任务序列节点为止。 刷新后，副本将出现在根文件夹中。  

#### <a name="refresh"></a>刷新

刷新所选任务序列的详细信息。

#### <a name="delete"></a>删除

删除所选的任务序列。

#### <a name="create-phased-deployment"></a>创建分阶段部署

有关详细信息，请参阅[创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)。

#### <a name="deploy"></a>部署

有关详细信息，请参阅 [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence)。

#### <a name="distribute-content"></a>分发内容

启动“分发内容向导”将引用的内容发送到分发点。

#### <a name="create-prestaged-content-file"></a>创建预留的内容文件

启动“创建预留的内容文件向导”以预留任务序列内容。 有关如何创建预留的内容文件的信息，请参阅[预安排内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage)。

#### <a name="move"></a>移动

将所选的任务序列移动到“任务序列”  节点中的另一个文件夹。

#### <a name="set-security-scopes"></a>设置安全作用域

选择所选任务序列的安全作用域。 有关详细信息，请参阅 [安全作用域](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope)。

#### <a name="properties"></a>属性

有关详细信息，请参阅[配置软件中心属性](#bkmk_prop-general)并[配置高级任务序列设置](#bkmk_prop-advanced)。

#### <a name="view"></a>查看

<!--3633146-->
从版本 1902 开始，任务序列上的“查看”  操作是默认设置。 通过此操作可以查看任务序列的步骤，而无需将其锁定以进行编辑。  


## <a name="see-also"></a>另请参阅

[部署企业版操作系统的方案](scenarios-to-deploy-enterprise-operating-systems.md)
