---
title: 如何使用任务序列变量
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 任务序列中的变量。
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18305b26937c87cbdb4d5726bded571699416793
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42756261"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>如何使用 Configuration Manager 中的任务序列变量

*适用范围：System Center Configuration Manager (Current Branch)*

 Configuration Manager 的 OS 部署功能中的任务序列引擎使用多个变量来控制其行为。 使用这些变量： 
 - 设置步骤条件  
 - 更改特定步骤的行为  
 - 在脚本中使用以执行更复杂的操作  


 有关所有可用的任务序列变量的引用，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables)。



## <a name="bkmk_types"></a> 变量类型

 有多种类型的变量：  
 - [内置](#bkmk_built-in)  
 - [操作](#bkmk_action)  
 - [自定义](#bkmk_custom)  
 - [只读](#bkmk_read-only)  
 - [数组](#bkmk_array)  


### <a name="bkmk_built-in"></a> 内置变量

 内置变量提供有关任务序列运行环境的信息。 其值可在整个任务序列中使用。 通常情况下，任务序列引擎会在运行任何步骤之前初始化内置变量。 

 例如，\_SMSTSLogPath 是一个环境变量，指定 Configuration Manager 组件用于写入日志文件的路径。 任何任务序列步骤均可访问此环境变量。 

 任务序列会在每个步骤前计算一些变量。 例如，\_SMSTSCurrentActionName 列出当前步骤的名称。 

### <a name="bkmk_action"></a> 操作变量

 任务序列操作变量指定单个任务序列步骤使用的配置设置。 默认情况下，该步骤在运行之前会先初始化其设置。 仅当相关联的任务序列步骤运行时，这些设置才可用。 运行步骤前，任务序列会将操作变量值添加到环境。 该步骤运行之后，任务序列会从环境中删除该值。

 例如，将“运行命令行”步骤添加到任务序列。 此步骤包括 Start In 属性。 任务序列将此属性的默认值存储为 WorkingDirectory 变量。 在运行“运行命令行”步骤之前，任务序列会初始化该值。 在运行此步骤时，从 WorkingDirectory 值访问 Start In 属性值。 该步骤完成之后，任务序列从环境中删除 WorkingDirectory 变量值。 如果任务序列包含另一个“运行命令行”步骤，它将初始化一个新的“WorkingDirectory”变量。 此时，任务序列会将变量设置为当前步骤的起始值。 有关详细信息，请参阅 [WorkingDirectory](using-task-sequence-variables.md#WorkingDirectory)。  

 步骤运行时，操作变量的默认值为“present”。 如果设置为新值，该值可供任务序列中的多个步骤使用。 如果重写默认值，新值将保留在环境中。 此新值将覆盖任务序列中其他步骤的默认值。 例如，添加“设置任务序列变量”步骤作为任务序列的第一步。 此步骤将 WorkingDirectory 变量设置为 `C:\`。 任务序列中的任何“运行命令行”步骤均使用新的起始目录值。  

 某些任务序列步骤将特定操作变量标记为“输出”。 任务序列中的后续步骤会读取这些输出变量。

 > [!Note]  
 > 并非所有任务序列步骤都具有操作变量。 例如，虽然有与“启用 BitLocker”操作相关联的变量，但没有与“禁用 BitLocker”操作相关联的变量。  


### <a name="bkmk_custom"></a> 自定义变量

 这些变量是 Configuration Manager 不会创建的任何变量。 将自己的变量初始化为条件，以便在命令行或脚本中使用。 

 为新任务序列变量指定名称时，请遵循以下准则：  

 - 任务序列变量名称可以包含字母、数字、下划线字符 (`_`) 和连字符 (`-`)。  

 - 任务序列变量名称长度至少为 1 个字符，最多为 256 个字符。  

 - 用户定义的变量必须以字母（`A-Z` 或 `a-z`）开头。  

 - 用户定义的变量名称不能以下划线字符开头。 仅只读任务序列变量的前面使用下划线字符。  

 - 任务序列变量名称不区分大小写。 例如，`OSDVAR` 和 `osdvar` 是相同的任务序列变量。  

 - 任务序列变量名称不能以空格开头或结尾。 此外还不能有嵌入空格。 变量名称开头或结尾的任何空格会被任务序列忽略。  


 对于可以创建的任务序列变量数量没有设定限制。 但是，变量数受任务序列环境大小的限制。 任务序列环境的总大小限制为 32 MB。  


### <a name="bkmk_read-only"></a> 只读变量

 不能更改一些只读变量的值。 通常该名称以下划线字符(\_) 开头。 任务序列将这些变量用于操作。 只读变量在任务序列环境中可见。 

 这些变量在脚本或命令行中很有用。 例如，运行命令行，并将输出结果传输到 \_SMSTSLogPath 中的日志文件，与其他日志文件结合使用。

 > [!NOTE]  
 >  只读任务序列变量可由任务序列中的步骤读取，但它们无法被设置。 例如，使用只读变量作为“运行命令行”步骤的命令行的一部分。 不能使用“设置任务序列变量”步骤设置只读变量。  



### <a name="bkmk_array"></a> 数组变量

 任务序列将一些变量存储为数组。 数组中的每个元素都代表单个对象设置。 当设备具有多个要配置的对象时，请使用这些变量。 下列任务序列步骤使用数组变量：

 - [应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

 - [格式化磁盘并分区](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  



## <a name="bkmk_set"></a> 如何设置变量

 对于自定义变量或并非只读的变量，可以通过以下几种方法来初始化并设置变量的值：  

 - [设置任务序列变量](#bkmk_set-ts-step)  
 - [设置动态变量](#bkmk_set-dyn-step)  
 - [集合和设备变量](#bkmk_set-coll-var)  
 - [TSEnvironment COM 对象](#bkmk_set-com)  
 - [预启动命令](#bkmk_set-prestart)  
 - [任务序列媒体向导](#bkmk_set-media)  


 从环境中删除变量的方法与创建变量相同。 要删除一个变量，请将变量值设置为空字符串。  

 可以组合多个方法以将任务序列变量设置为相同序列的不同值。 例如，使用任务序列编辑器设置默认值，然后使用脚本设置自定义值。 

 如果通过不同方法设置相同变量，任务序列引擎将使用以下顺序：  

 1. 它首先会计算集合变量。  

 2. 特定于设备的变量会重写在集合上设置的相同变量。  

 3. 由任务序列过程中的任何方法设置的变量优先于集合或设备变量。  


#### <a name="general-limitations-for-task-sequence-variable-values"></a>任务序列变量值的一般限制  

 - 任务序列变量值不能超过 4,000 个字符。  

 - 不能更改只读任务序列变量。 只读变量使用以下划线 (`_`) 字符开头的名称。  

 - 任务序列变量值可能区分大小写，具体情况视值的使用情况而定。 大多数情况下，任务序列变量值不区分大小写。 包含密码的变量区分大小写。  


### <a name="bkmk_set-ts-step"></a>设置任务序列变量

 在任务序列中使用此步骤将单个变量设置为单个值。 

 有关详细信息，请参阅[设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)。 


### <a name="bkmk_set-dyn-step"></a>设置动态变量

 在任务序列中使用此步骤设置一个或多个任务序列变量。 在此步骤中定义规则，以确定要使用哪些变量和值。 

 有关详细信息，请参阅[设置动态变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables)


### <a name="bkmk_set-coll-var"></a> 集合和设备变量

 在集合或特定设备的属性上设置变量。 

 有关详细信息，请参阅[为计算机和集合创建任务序列变量](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTSVariables)。


### <a name="bkmk_set-com"></a> TSEnvironment COM 对象

 若要使用脚本中的变量，请使用 TSEnvironment 对象。 

 有关详细信息，请参阅 Configuration Manager SDK 中的[如何在运行的任务序列中使用变量](/sccm/develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence)。


### <a name="bkmk_set-prestart"></a> 预启动命令

 预启动命令是在用户选择任务序列之前在 Windows PE 中运行的一个脚本或可执行文件。 预启动命令可以查询变量或提示用户输入信息，然后将其保存在环境中。 使用 [TSEnvironment](#bkmk_set-com) COM 对象来读取和写入来自预启动命令的变量。 

 有关详细信息，请参阅[任务序列媒体的预启动命令](/sccm/osd/understand/prestart-commands-for-task-sequence-media)。


### <a name="bkmk_set-media"></a> 任务序列媒体向导

 指定从媒体运行的任务序列的变量。 使用媒体部署 OS 时，添加任务序列变量，并在创建媒体时指定其值。 变量及其值存储在媒体上。  

 > [!NOTE]  
 >  任务序列存储在独立媒体上。 但是，所有其他类型的媒体，如预留媒体，会从管理点中检索任务序列。  

 从媒体运行任务序列时，可以在向导的“自定义”页添加一个变量。 

 使用媒体变量替代每集合变量或每计算机变量。 如果正在从媒体运行任务序列，则不应用也不使用每计算机变量和每集合变量。  

 > [!TIP]  
 >  任务序列将包 ID 和预启动命令行写入到运行 Configuration Manager 控制台的计算机上的 CreateTSMedia.log 文件。 此日志文件包括任何任务序列变量的值。 查看此日志文件以验证任务序列变量的值。  

 有关详细信息，请参阅[创建任务序列媒体](/sccm/osd/deploy-use/create-task-sequence-media)。



## <a name="bkmk_access"></a> 如何访问变量

 使用上一部分中所述的方法之一指定变量及其值之后，在任务序列中使用它。 例如，访问内置任务序列变量的默认值，或基于变量值设置步骤条件。  

 使用以下方法来访问任务序列环境中的变量值：
 - [在步骤中使用](#bkmk_access-step)  
 - [步骤条件](#bkmk_access-condition)  
 - [自定义脚本](#bkmk_access-script)  
 - [Windows 安装程序答案文件](#bkmk_access-answer)  
  

### <a name="bkmk_access-step"></a> 在步骤中使用

 在任务序列步骤中指定设置的变量值。 在任务序列编辑器中编辑步骤，并将变量名称指定为字段值。 将变量名称括在百分号 (`%`) 中。 

 例如，使用变量名称作为“运行命令行”步骤的“命令行”字段的一部分。 下面的命令行将计算机名称写入文本文件。 

 `cmd.exe /c %_SMSTSMachineName% > C:\File.txt`


### <a name="bkmk_access-condition"></a> 步骤条件

 使用内置或自定义任务序列变量作为步骤或组条件的一部分。 在运行步骤或组之前，任务序列会计算变量值。

 要添加计算变量值的条件，请执行下列步骤：  

 1. 在任务序列编辑器中，选择要添加条件的步骤或组。  

 2. 切换到步骤或组的“选项”选项卡。 单击“添加条件”，然后选择“任务序列变量”。  

 3. 在“任务序列变量”对话框中，指定以下设置：  

    - 变量：变量名称。 例如，`_SMSTSInWinPE`。  

    - 条件：计算变量值的条件。 例如，等于。  

    - 值：要检查的变量的值。 例如，`false`。  


 上面三个示例构成了测试的常见条件，即任务是否从 Windows PE 的启动映像运行： 

 > 任务序列变量 `_SMSTSInWinPE equals "false"`

 有关此情况，请参阅默认任务序列模板的“捕获文件和设置”组，以安装现有 OS 映像。


### <a name="bkmk_access-script"></a> 自定义脚本

 可以在运行任务序列时使用 Microsoft.SMS.TSEnvironment COM 对象读取和写入变量。

 下面的 Windows PowerShell 示例查询 _SMSTSLogPath 变量以获取当前日志位置。 该脚本还设置自定义变量。

 ```PowerShell
 # Create an object to access the task sequence environment
 $tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment
 
 # Query the environment to get an existing variable
 # Set a variable for the task sequence log path
 $LogPath = $tsenv.Value("_SMSTSLogPath")

 # Or, convert all of the variables currently in the environment to PowerShell variables
 $tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

 # Write a message to a log file
 Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append
 
 # Set a custom variable "startTime" to the current time
 $tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
 ```


###  <a name="bkmk_access-answer"></a> Windows 安装程序答案文件

所提供的 Windows 安装程序答案文件可包含嵌入任务序列变量。 使用窗体 `%varname%`，其中 varname 是变量的名称。 “安装 Windows 和 ConfigMgr”步骤将变量名称字符串替换为实际变量值。 unattend.xml 答案文件的仅数字字段中不能使用这些嵌入的任务序列变量。

有关详细信息，请参阅[安装 Windows 和 ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)。



## <a name="see-also"></a>另请参阅

- [任务序列步骤](/sccm/osd/understand/task-sequence-steps)
- [任务序列变量](/sccm/osd/understand/task-sequence-variables)
- [自动执行任务的规划注意事项](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
