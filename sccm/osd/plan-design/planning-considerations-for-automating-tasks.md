---
title: 自动执行任务计划
titleSuffix: Configuration Manager
description: 在创建任务序列之前制定计划以利用 Configuration Manager 自动执行任务。
ms.date: 10/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6030bb1a02a94e61cf3ef53b6d90f7b6a5ae4f7a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122094"
---
# <a name="planning-considerations-for-automating-tasks-in-configuration-manager"></a>计划在 Configuration Manager 中自动执行任务的注意事项

适用范围：System Center Configuration Manager (Current Branch)

 可以创建任务序列，以在 Configuration Manager 环境中自动执行任务。 这些任务涉及从捕获引用计算机上的 OS 到向一个或多个目标计算机部署 OS 在内的各种任务。 序列的各个步骤中定义了任务序列的操作。 任务序列运行时，它在本地系统上下文中的命令行级别运行每个操作步骤。 此行为意味着任务序列完全自动化运行，而无需用户干预。 



##  <a name="BKMK_TSStepsActions"></a>任务序列步骤和操作  

 步骤是任务序列的基本组件。 它们可以包括以下命令：  
   - 配置和捕获引用计算机的 OS  
   - 在目标计算机上安装 Windows、硬件驱动程序、Configuration Manager 客户端和软件   


 步骤的操作定义任务序列步骤的命令。 有两种类型的操作：  
   - 使用命令行字符串定义的操作称为“自定义操作”  
   - Configuration Manager 预定义的操作称为“内置操作”。  


 任务序列可以执行自定义和内置操作的任意组合。  

 任务序列步骤还可以包含控制步骤行为方式的条件。 这些行为包括在发生错误的情况下停止任务序列，或继续任务序列。 一种类型的条件是任务序列变量。 例如，使用 SMSTSLastActionRetCode 变量测试上一个步骤的条件。 将条件添加到单个或一组步骤中。  

 任务序列将按顺序处理步骤。 此序列包含步骤的操作和对步骤的任何条件。 在 Configuration Manager 开始处理任务序列步骤时，直到上一个操作完成，才会开始下一个步骤。 

 在以下条件下，任务序列被视为完成： 
   - 已完成其所有步骤  
   - 某步骤失败会导致 Configuration Manager 停止运行任务序列，无法完成其所有步骤。  


 例如，如果任务序列的步骤在分发点上找不到引用的映像或包，则任务序列将包含损坏的引用。 Configuration Manager 将停止运行任务序列，除非失败的步骤具有在出错时要继续的条件。  

 > [!IMPORTANT]  
 >  默认情况下，一个步骤或操作失败，将导致任务序列失败。 如果要在步骤失败后继续执行任务序列，请编辑任务序列，单击“选项”选项卡，然后选择“出错时继续”。  

 有关可添加到任务序列中的步骤的详细信息，请参阅[任务序列步骤](/sccm/osd/understand/task-sequence-steps)。  



##  <a name="BKMK_TSGroups"></a> 任务序列组  

 可以在一个任务序列中对多个步骤分组。 任务序列组由名称、可选说明和任何可选条件组成。 任务序列在继续下一个步骤之前，将组条件作为一个单元来评估。 在彼此之间嵌套组，或包含混用步骤和子组。 组对于合并共享公用条件的多个步骤十分有用。  

 为任务序列组分配一个名称。 不必是唯一的名称。 你还可以为任务序列组提供可选描述。  

 > [!IMPORTANT]  
 >  默认情况下，如果任务序列组中的任何步骤或嵌入的组失败，将导致此任务序列组失败。 如果要在步骤或嵌入的组失败后继续进行任务序列，请在步骤或组上选择“出错时继续”。  

 下表显示了组合步骤时“出错时继续” 选项是如何工作的。  

 在此示例中，有两组任务序列，各包含三个任务序列步骤。  

 |任务序列组或步骤|“出错时继续”设置|  
 |---------------------------------|-------------------------------|  
 |任务序列组 1|**已选中“出错时继续”** 。|  
 |任务序列步骤 1|**已选中“出错时继续”** 。|  
 |任务序列步骤 2|未设置。|  
 |任务序列步骤 3|未设置。|  
 |任务序列组 2|未设置。|  
 |任务序列步骤 4|未设置。|  
 |任务序列步骤 5|未设置。|  
 |任务序列步骤 6|未设置。|  


 -   如果任务序列步骤 1 失败，任务序列将继续执行任务序列步骤 2。  

 -   如果任务序列步骤 2 失败，任务序列将不会运行任务序列步骤 3。 因为任务序列组 1 配置为“出错时继续”，任务序列将继续执行任务序列组 2。 接下来，它将运行任务序列步骤 4。  

 -   如果任务序列步骤 4 失败，则不运行任何其他步骤。 任务序列失败，因为任务序列组 2未配置“出错时继续”设置。  



## <a name="add-child-task-sequences-to-a-task-sequence"></a>将子任务序列添加到任务序列
 <!--1261338--> 自 Configuration Manager 版本 1710 起，可以添加运行另一个任务序列的新任务序列步骤。 此步骤将创建任务序列之间的父子关系。 使用此步骤可创建更多可重复使用的模块式任务序列。  

 有关详细信息，请参阅[运行任务序列](/sccm/osd/understand/task-sequence-steps#child-task-sequence)。 

 > [!Note]  
 > 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  



##  <a name="BKMK_TSVariables"></a> 任务序列变量  

 任务序列变量是一组名称和值对。 它们向计算机、OS 以及 Configuration Manager 客户端上的用户状态配置任务提供配置和 OS 部署设置。 任务序列变量提供了一种机制来配置和自定义任务序列中的步骤。  

 运行任务序列时，许多任务序列设置会存储为环境变量。 可以访问或更改内置任务序列变量的值。 还可以创建新的任务序列变量以自定义任务序列在目标计算机上的运行方式。  

 使用任务序列变量来执行以下操作：  

 -   配置任务序列操作的设置  

 -   提供任务序列步骤的命令行参数  

 -   评估条件以确定是任务序列步骤还是组在运行  

 -   为任务序列中使用的自定义脚本提供值  


 例如，你有一个包含“加入域或工作组”任务序列步骤的任务序列。 将此任务序列部署到不同集合，其中的集合成员资格由域成员身份来决定。 为每个集合的域名指定一个每集合任务序列变量。 然后使用该任务序列变量在任务序列中提供合适的域名。  

 有关详细信息，请参阅[如何使用任务序列变量](/sccm/osd/understand/using-task-sequence-variables)。



##  <a name="BKMK_TSCreate"></a> 创建任务序列  

 通过使用创建任务序列向导来创建任务序列。 此向导可以创建执行特定任务的内置任务序列，或创建可执行许多不同任务的自定义任务序列。 此向导可创建下列类型的任务序列：

 - 在目标计算机上安装现有 OS 映像  

 - 生成和捕获引用计算机的 OS 映像  

 - 从目标计算机上的 OS 升级包升级到 Windows 10   

 - 创建执行自定义任务或专用 OS 部署的自定义任务序列  


 有关详细信息，请参阅[创建任务序列](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTaskSequence)。  



##  <a name="BKMK_TSEdit"></a>编辑任务序列  

 可以使用“任务序列编辑器”编辑任务序列。 编辑器可以对任务序列进行以下更改：  

 - 在任务序列中添加或删除步骤  

 - 更改任务序列的步骤的顺序  

 - 添加或删除步骤组  

 - 指定发生错误时任务序列是否继续  

 - 将条件添加到任务序列的步骤和组中  


 > [!IMPORTANT]  
 >  如果任务序列对编辑结果的对象进行了任何无关的引用，编辑器将要求你在关闭之前修复引用。 可能的操作包括：  
 > - 更正引用  
 > - 从任务序列中删除未引用的对象  
 > - 暂时禁用失败的任务序列步骤，直到更正或删除损坏的引用  


 有关如何编辑任务序列的信息，请参阅[编辑任务序列](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence)。  



##  <a name="BKMK_TSDeploy"></a>部署任务序列  

 向位于任何 Configuration Manager 集合中的目标计算机部署任务序列。 使用内置“所有未知计算机”集合将操作系统部署到未知计算机。 不能将任务序列部署到用户集合。  

 > [!IMPORTANT]  
 >  不要部署将操作系统安装到不适合的集合的任务序列。 请确保任务序列部署到的集合仅包含想在其中安装 OS 的那些计算机。 若要帮助防止不需要的 OS 部署，请配置高风险部署设置。 有关详细信息，请参阅[用于管理高风险部署的设置](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments)。  

 每个接收任务序列的目标计算机将根据部署中指定的设置运行该任务序列。 任务序列本身不包含关联的文件或程序。 任务序列引用的任何文件都必须已经存在于目标计算机上或位于客户端可访问的分发点上。 

 > [!NOTE]  
 > 任务序列会安装程序所引用的包，即使已在目标计算机上安装了程序或包也不例外。 
 > 
 > 如果任务序列安装应用程序，则只有在满足应用程序的要求规则并且还没有安装应用程序时，才会根据为应用程序指定的检测方法来安装该应用程序。  

 Configuration Manager 客户端在下载客户端策略后会运行任务序列部署。 要触发此操作而不是等到下一个轮询周期，请参阅 [为 Configuration Manager 客户端启动策略检索](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval)。  

 将任务序列部署到启用了写入筛选器的 Windows Embedded 设备时，可以指定是否在部署过程中对设备禁用写入筛选器，然后在部署后重启设备。 如果未禁用写入筛选器，则任务序列会部署到临时覆盖区，并且在重启设备时将不可用。  

 > [!NOTE]  
 >  将任务序列部署到 Windows Embedded 设备时，确保设备是配置了维护时段的集合的成员。 这样，你可以管理禁用和启用写入筛选器的时间，以及设备重启的时间。  
 >   
 >  如果客户端在维护时段之外下载任务序列，则会下载两次任务序列。 在此方案中，客户端下载任务序列、禁用写入筛选器、重新启动计算机，然后会再次下载任务序列。 此行为是因为任务序列最初已下载到临时覆盖区，当设备重新启动时就会被清除。  

 有关如何部署任务序列的详细信息，请参阅[部署任务序列](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)。  



##  <a name="BKMK_TSExportImport"></a> 导出和导入任务序列  

 Configuration Manager 允许导出和导入任务序列。 导出任务序列时，可以包括任务序列引用的对象。 

 有关详细信息，请参阅[导出和导入任务序列](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ExportImport)。  



##  <a name="BKMK_TSRun"></a> 运行任务序列  

 任务序列始终使用本地系统帐户运行。 运行任务序列时，Configuration Manager 客户端首先检查任何引用的包，然后会启动任务序列的步骤。 如果无法验证或下载引用的包，则任务序列将为关联任务序列步骤返回错误。  

 > [!Note]  
 > 利用任务序列步骤“运行命令行”，你能够用其他帐户运行命令。  

 如果将任务序列部署配置为“下载并运行”，Configuration Manager 客户端会将所有依赖项内容下载到它的缓存中。 如果客户端缓存大小过小或找不到内容，任务序列将失败。 客户端会生成状态消息。 

 此外可以指定客户端仅在需要时下载内容。 要执行此操作，选择任务序列部署中的“需要时通过运行任务序列本地下载内容”。 另一个选项是“从分发点运行程序”。 使用此选项时，客户端直接从分发点安装文件，而无需先将其下载到缓存。 

 当将任务序列部署配置为“可用”时，如果客户端找不到任务序列的相关内容，它会立即发送错误。 对于“必需”的部署，Configuration Manager 客户端会在这种情况下等待。 它会重试下载内容直到截止期限，以防内容尚未复制到客户端可访问的内容位置。  

 无论任务序列成功完成与否，Configuration Manager 都会在客户端历史记录中记录此情况。 

 在计算机上启动任务序列后，不能取消或停止。  

 > [!IMPORTANT]  
 >  如果任务序列步骤要求重启计算机，则客户端必须能够启动到格式化的磁盘分区。 否则，任务序列将失败，而与任务序列指定的任何错误处理无关。  

 如果任务序列的从属对象更新到较新版本，将自动更新引用包的任何任务序列。 它引用最新版本，而不考虑部署更新的次数。  



##  <a name="BKMK_TSMaintenanceWindow"></a> 使用维护时段指定任务序列何时可以运行  

 通过为设备集合定义维护时段，可以指定任务序列何时运行。 配置维护时段的开始日期、开始和完成时间以及定期模式。 在为维护时段设置计划时，可以指定维护时段仅应用于任务序列。 有关详细信息，请参阅[如何使用维护时段](/sccm/core/clients/manage/collections/use-maintenance-windows)。  

 > [!IMPORTANT]  
 >  在配置维护时段以运行任务序列时，一旦任务序列启动，即使维护时段结束，它也会继续运行。  



##  <a name="BKMK_TSNetworkAccessAccount"></a> 任务序列和网络访问帐户  

> [!Important]  
> 自版本 1806 开始，某些 OS 部署情况不需要使用网络访问帐户。 有关详细信息，请参阅[增强型 HTTP](#enhanced-http)。

虽然任务序列仅在本地系统帐户的上下文中运行，但在下列情况下，你可能需要配置[网络访问帐户](/sccm/core/plan-design/hierarchy/accounts#network-access-account)：  

- 如果任务序列尝试访问分发点上的 Configuration Manager 内容。 正确配置网络访问帐户，否则任务序列将失败。   

- 当使用启动映像来启动 OS 部署时。 在这种情况下，Configuration Manager 使用 Windows PE 环境，该环境不是一个完整的 OS。 Windows PE 环境使用自动生成的随机名称，该名称不是任何域的成员。 如果未正确配置网络访问帐户，计算机将无法访问任务序列所需的内容。  

> [!NOTE]  
>  网络访问帐户从不用作运行程序、安装应用程序、安装更新或运行任务序列的安全上下文。 网络访问帐户仅用于访问网络上的关联资源。  

有关网络访问帐户的详细信息，请参阅[网络访问帐户](/sccm/core/plan-design/hierarchy/accounts#network-access-account)。  


### <a name="enhanced-http"></a>增强型 HTTP
<!--1358278-->

自版本 1806 开始，当启用增强型 HTTP 时，以下情况不需要网络访问帐户即可从分发点下载内容：
  
- 从启动媒体或 PXE 运行的任务序列  
- 从软件中心运行的任务序列  

这些任务序列可以用于操作系统部署或者是自定义的。 它还支持工作组计算机。
 
有关详细信息，请参阅[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)。  

> [!Note]  
> 以下操作 OS 情况仍需要使用网络访问帐户：
>  
> - 任务序列[部署选项](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)“需要时通过运行任务序列从分发点直接访问内容”   
> - [请求状态存储](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore)步骤选项“如果计算机帐户无法连接到状态存储，请使用网络访问帐户” 
> - 与不受信任的域或跨 Active Directory 林连接时 
> - [应用 OS 映像](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyOperatingSystemImage)步骤选项“直接从分发点访问内容” 
> - 任务序列[高级设置](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#bkmk_prop-advanced)“首先运行其他程序” 
> - [多播](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)  



##  <a name="BKMK_TSCreateMedia"></a> 为任务序列创建媒体  

 可以将任务序列及其相关的文件和依赖关系写入到多种类型的媒体中。 Configuration Manager 支持可移动媒体，如 DVD 或 USB 闪存驱动器，适用于捕获、独立和可启动媒体。 预留媒体使用 Windows 映像 (WIM) 文件。  

 创建媒体时，指定密码来控制访问。 然后用户必须在目标计算机上输入密码来运行任务序列。  

 从媒体运行任务序列时，无法识别媒体指定的处理器体系结构。 如果指定的体系结构与目标计算机不匹配，任务序列仍尝试运行。 如果媒体的体系结构与目标计算机的体系结构不匹配，任务序列将失败。  

 有关详细信息，请参阅[创建任务序列媒体](/sccm/osd/deploy-use/create-task-sequence-media)。  


### <a name="media-types"></a>媒体类型
 Configuration Manager支持以下类型的媒体：  

#### <a name="capture-media"></a>捕获媒体
 捕获媒体捕获在 Configuration Manager 基础结构以外配置和创建的 OS 映像。 捕获媒体可以包含可在任务序列运行之前运行的自定义程序。 自定义程序可以与桌面交互、提示用户输入值，或创建任务序列将使用的变量。  

 有关详细信息，请参阅[创建捕获媒体](/sccm/osd/deploy-use/create-capture-media)。  

#### <a name="stand-alone-media"></a>独立媒体
 独立媒体包含任务序列，以及运行任务序列所必需的所有关联对象。 当 Configuration Manager 的网络连接受限或者没有网络连接时，独立媒体任务序列可以运行。 通过下列方式运行独立媒体：  

 - 如果没有启动目标计算机，则将从独立媒体中使用与任务序列关联的 Windows PE 映像，而且任务序列开始运行。  

 - 手动启动独立媒体。 如果用户登录到计算机，他们可以从媒体启动任务序列。  


 > [!IMPORTANT]  
 >  独立媒体任务序列的步骤必须能够运行，而无需从网络检索任何数据。 否则，尝试检索数据的任务序列步骤将失败。 例如，需要访问分发点以获取包的任务序列步骤将失败。 如果独立媒体包含必要的包，任务序列步骤将成功。  


 有关详细信息，请参阅[创建独立媒体](/sccm/osd/deploy-use/create-stand-alone-media)。  

#### <a name="bootable-media"></a>可启动媒体
 可启动媒体包含启动目标计算机所需的文件，以便此计算机能够连接到 Configuration Manager 基础结构。 然后根据它的集合成员身份确定要运行的任务序列。 此媒体不包括任务序列或从属对象。 相反，客户端通过网络下载内容。 对于新计算机或裸机部署，当目标计算机上没有 OS 时，此方法很有用。  

 有关详细信息，请参阅[创建可启动媒体](/sccm/osd/deploy-use/create-bootable-media)。  

#### <a name="prestaged-media"></a>预留媒体
 预留媒体将 OS 映像部署到未设置的目标计算机。 预留媒体存储为 Windows 映像 (WIM) 文件。 可由制造商在裸机计算机上安装此文件，或者在企业暂存中心执行此操作。 预留媒体的优点是，这些位置不需要连接到 Configuration Manager 环境。  

 有关详细信息，请参阅[创建预留媒体](/sccm/osd/deploy-use/create-prestaged-media)。  
