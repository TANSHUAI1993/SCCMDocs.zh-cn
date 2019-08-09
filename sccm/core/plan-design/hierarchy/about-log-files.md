---
title: 关于日志文件
titleSuffix: Configuration Manager
description: 使用日志文件解决 Configuration Manager 客户端和站点系统中的问题。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3885e4323e8c41bcf644de7c62fd1dcb22c684c8
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68538043"
---
# <a name="about-log-files-in-configuration-manager"></a>关于 Configuration Manager 中的日志文件

在 Configuration Manager 中，客户端和站点服务器组件都将进程信息记录在单独的日志文件中。 可以使用日志文件中的信息来帮助排除可能出现的问题。 Configuration Manager 默认启用客户端和服务器组件的日志记录。

本文提供了有关 Configuration Manager 日志文件的一般信息。 其中包含有关要使用的工具、如何配置日志以及在何处查找日志的信息。 有关特定日志文件的详细信息，请参阅[日志文件引用](/sccm/core/plan-design/hierarchy/log-files)。


## <a name="BKMK_AboutLogs"></a> 工作原理

Configuration Manager 中的大多数进程将操作信息写入专用于该进程的日志文件。 通过 **.log** 或 **.lo_** 文件扩展名标识这些日志文件。 Configuration Manager 将写入 .log 文件，直到该日志达到其最大大小。 当日志已满时，会将 .log 文件复制到名称相同但扩展名为 .lo_ 的文件，并且进程或组件将继续写入 .log 文件。 当 .log 文件再次达到其最大大小时，将覆盖 .lo_ 文件，并且该过程将重复。 某些组件会通过将日期和时间戳追加到日志文件名并保留 .log 扩展名来建立日志文件历史记录。


## <a name="bkmk_tools"></a> 日志查看器工具

所有 Configuration Manager 日志文件都是纯文本，因此你可以使用任何文本读取器（如记事本）来查看它们。 日志使用唯一格式，该格式要使用以下其中一个专用工具才能获得最佳效果：

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [支持中心日志查看器](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

若要查看日志，请使用 Configuration Manager 日志查看器工具 CMTrace  。 它位于 Configuration Manager 源媒体的 \\SMSSetup\\Tools 文件夹中。 向已添加到“软件库”的所有启动映像中添加 CMTrace 工具。 从 1806 版开始，CMTrace 日志查看工具自动与 Configuration Manager 客户端一起安装。<!--1357971--> 有关详细信息，请参阅 [CMTrace](/sccm/core/support/cmtrace)。

### <a name="onetrace"></a>OneTrace

从版本 1906 开始，OneTrace  是一个带有支持中心的新日志查看器。 它的工作方式与 CMTrace 类似，同时进行了一些改进。 有关详细信息，请参阅[支持中心 OneTrace](/sccm/core/support/support-center-onetrace)。

### <a name="support-center-log-viewer"></a>支持中心日志查看器

 支持中心包括最新日志查看器。 此工具取代了 CMTrace，提供可自定义的界面，并支持选项卡和可停靠窗口。 它具有快速表示层，可以在几秒钟内加载大型日志文件。 有关详细信息，请参阅[支持中心日志查看器引用](/sccm/core/support/support-center-ui-reference#bkmk_log-viewer)。

> [!Note]  
> 支持中心和 OneTrace 使用 Windows Presentation Foundation (WPF)。 此组件在 Windows PE 中不可用。 继续在具有任务序列部署的启动映像中使用 CMTrace。


## <a name="bkmk_logoptions"></a> 配置日志记录选项

可以更改日志文件的配置，如详细级别、大小和历史记录。 有多种方式可以更改这些设置：

- [在客户端安装期间](#bkmk_logoptions-clientprop)
- [使用 Configuration Manager 服务管理器](#bkmk_logoptions-sm)
- [使用 Windows 注册表](#bkmk_logoptions-registry)

### <a name="bkmk_logoptions-clientprop"></a> 在客户端安装期间配置日志记录选项

可以在安装期间设置客户端日志文件的配置。 使用以下属性：

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

有关详细信息，请参阅[客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties#clientMsiProps)。

### <a name="bkmk_logoptions-sm"></a>使用 Configuration Manager 服务管理器配置日志记录选项

可更改 Configuration Manager 存储日志文件时使用的位置，以及日志文件的大小。  

若要修改日志文件大小、更改日志文件名称和位置或强制多个组件写入单一日志文件，可执行以下步骤：  

#### <a name="modify-logging-for-a-component"></a>修改组件的日志记录  

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“系统状态”，然后选择“站点状态”或“组件状态”节点     。  

2. 在功能区中，选择“启动”，然后选择“Configuration Manager 服务管理器”   。  

3. 当 Configuration Manager 服务管理器打开时，连接到要管理的站点。 如果未显示要管理的站点，请选择“站点”  ，选择“连接”  ，然后输入正确的站点的站点服务器的名称。  

4. 展开站点并转到“组件”  或“服务器”  ，具体情况取决于要管理的组件位于何处。  

5. 在右侧窗格中，选择一个或多个组件。  

6. 在“组件”  菜单上，选择“日志记录”  。  

7. 在“Configuration Manager 组件日志记录”  对话框中，为所选内容完成可用配置选项。  

8. 选择“确定”  保存配置。  

### <a name="bkmk_logoptions-registry"></a> 使用 Windows 注册表配置日志记录选项

<!-- SCCMDocs#992 -->
使用服务器或客户端上的 Windows 注册表来更改以下日志记录选项：

- 详细级别
- 最大历史记录
- 最大大小

解决问题时，可以启用 Configuration Manager 的详细日志记录，以便在日志文件中写入其他详细信息。

> [!Warning]
> 这些设置的错误配置可能会导致 Configuration Manager 记录大量信息，或不记录任何信息。 尽管此数据有助于故障排除，但在生产站点中更改这些值时请谨慎。 始终先在实验室环境中测试这些更改。 因为这会产生过多日志记录，可能导致难以在日志文件中查找相关信息。

在对这些注册表设置进行更改后，请重新启动组件：

- 如果更改客户端设置，请重新启动“SMS 代理主机”  服务 (CcmExec)。
- 如果更改服务器设置，请重新启动“SMS Executive”  服务。

注册表设置因组件而异：

- [客户端和管理点](#bkmk_reg-client)
- [站点服务器](#bkmk_reg-site)
- [站点系统角色](#bkmk_reg-role)
- [Configuration Manager 控制台](#bkmk_reg-console)

#### <a name="bkmk_reg-client"></a> 客户端和管理点日志记录选项

若要为客户端或管理点站点系统上的所有组件配置日志记录选项，请在以下 Windows 注册表项下配置这些 REG_DWORD  值：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|名称  |值  |说明  |
|---------|---------|---------|
|LogLevel|`0`：详细<br>`1`：默认<br>`2`：警告和错误<br>`3`：仅错误|要写入日志文件的详细信息级别。|
|LogMaxHistory|任何大于或等于零的整数，例如：<br>`0`：无历史记录<br>`1`：默认|日志文件的大小达到上限时，客户端会将其重命名为备份，并创建新的日志文件。 指定要保留的先前版本数量。|
|LogMaxSize|任何大于或等于 10,000 的整数，例如：<br>250000|日志文件的最大大小（以字节为单位）。 当日志增长到指定大小时，客户端会将其重命名为历史文件，并创建一个新文件。 默认值为 250000 字节。|

> [!Note]  
> 不要更改此注册表项中可能存在的其他值。

对于高级调试，也可以在以下 Windows 注册表项下添加此 REG_SZ 值  ：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|名称  |值  |说明  |
|---------|---------|---------|
|Enabled | `True`：启用调试日志<br>`False`：禁用调试日志 |出于故障排除目的启用调试日志记录。|

此设置将使客户端记录有助于故障排除的低级信息。 避免在生产站点中使用此设置。 因为这会产生过多日志记录，可能导致难以在日志文件中查找相关信息。 确保在解决问题后关闭此设置。

#### <a name="bkmk_reg-site"></a> 站点服务器日志记录选项

可以全局配置设置，也可以为 Configuration Manager 站点服务器上的特定组件配置设置。

在以下 Windows 注册表项下配置这些值：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|名称  |值  |键入  |说明
|---------|---------|---------|---------|
|SqlEnabled| `1`：启用 SQL 跟踪<br> `0`：禁用 SQL 跟踪 |REG_DWORD|将 SQL 跟踪日志记录添加到所有站点服务器日志。|
|ArchiveEnabled| `1`：启用日志存档<br> `0`：禁用日志存档 | REG_DWORD |将站点服务器日志存档到不同的位置以进行历史保存。|
|ArchivePath| 有效的文件夹路径，例如 `C:\Logs\Archive` | REG_SZ |用于存档站点服务器日志的路径。|

仅出于故障排除目的启用 SQL 跟踪。 避免在生产站点中使用它。 因为这会产生过多日志记录，可能导致难以在日志文件中查找相关信息。 确保在解决问题后关闭此设置。

> [!Note]  
> 不要更改此注册表项中可能存在的其他值。

若要为特定服务器组件配置日志记录选项，请在以下 Windows 注册表项下配置这些 REG_DWORD  值：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|名称  |值  |说明  |
|---------|---------|---------|
|LoggingLevel|`0`：详细<br>`1`：默认<br>`2`：警告和错误<br>`3`：仅错误|要写入日志文件的详细信息级别。|
|LogMaxHistory|任何大于或等于零的整数，例如：<br>`0`：无历史记录<br>`1`：默认|日志文件的大小达到上限时，服务器会将其重命名为备份，并创建新的日志文件。 指定要保留的先前版本数量。|
|MaxFileSize|任何大于或等于 10,000 的整数，例如：<br>250000|日志文件的最大大小（以字节为单位）。 当日志增长到指定大小时，客户端会将其重命名为历史文件，并创建一个新文件。 默认值为 250000 字节。|
|DebugLogging| `1`：启用调试日志<br>`0`：禁用调试日志 |出于故障排除目的启用调试日志记录。|

DebugLogging 设置将使服务器记录有助于故障排除的低级信息。 避免在生产站点中使用此设置。 因为这会产生过多日志记录，可能导致难以在日志文件中查找相关信息。 确保在解决问题后关闭此设置。

> [!Note]  
> 不要更改此注册表项中可能存在的其他值。

#### <a name="bkmk_reg-role"></a> 站点系统角色日志记录选项

可以全局配置设置，也可以为托管 Configuration Manager 服务器角色的站点系统上的特定组件配置设置。

若要为特定服务器组件配置日志记录选项，请在以下 Windows 注册表项下配置这些 REG_DWORD  值：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

例如，对于分发点角色：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|名称  |值  |说明  |
|---------|---------|---------|
|LogLevel|`0`：详细<br>`1`：默认<br>`2`：警告和错误<br>`3`：仅错误|要写入日志文件的详细信息级别。|
|LogMaxHistory|任何大于或等于零的整数，例如：<br>`0`：无历史记录<br>`1`：默认|日志文件的大小达到上限时，服务器会将其重命名为备份，并创建新的日志文件。 指定要保留的先前版本数量。|
|LogMaxSize|任何大于或等于 10,000 的整数，例如：<br>250000|日志文件的最大大小（以字节为单位）。 当日志增长到指定大小时，服务器会将其重命名为历史文件，并创建一个新文件。 默认值为 250000 字节。|

> [!Note]  
> 不要更改此注册表项中可能存在的其他值。

#### <a name="bkmk_reg-console"></a> Configuration Manager 控制台日志记录选项

若要为 Configuration Manager 控制台更改 AdminUI.log 的详细级别，请使用以下过程：

1. 在 XML 编辑器（如记事本）中打开控制台配置文件 Microsoft.ConfigurationManagement.exe.config  。 默认配置文件位于以下位置：`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

1. 在“system.diagnostics” > “源” > “源元素”下，将 switchValue 属性从 `Error` 更改为 `Verbose`     。 例如：

    原始：`<source name="SmsAdminUISnapIn" switchValue="Error">` 新建：`<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. 保存文件并重新启动控制台。


## <a name="BKMK_LogLocation"></a> 查找日志文件

Configuration Manager 和依赖组件将日志文件存储在不同的位置。 这些位置取决于创建日志文件的过程，以及环境的配置。

以下位置是默认值。 如果在你的环境中自定义了安装目录，则实际路径可能会有所不同。

- 客户端：`C:\Windows\CCM\logs`
- 服务器：`C:\Program Files\Microsoft Configuration Manager\Logs`
- 管理点：`C:\SMS_CCM\Logs`
- Configuration Manager 控制台：`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog`
- IIS：`C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>任务序列日志位置

任务序列日志文件 smsts.log  的位置因任务序列的阶段而异：

- 在 Windows PE 中，执行[格式化磁盘并分区](/sccm/osd/understand/task-sequence-steps#BKMK_FormatandPartitionDisk)步骤之前：`X:\Windows\temp\smstslog\smsts.log`（X 是 Windows PE RAM 驱动器）
- 在 Windows PE 中，执行“格式化磁盘并分区  步骤之后：`X:\smstslog\smsts.log`，然后在驱动器就绪时复制到 `C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- 在新的 Windows OS 中，安装客户端之前：`C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- 在 Windows 中，安装客户端之后：`C:\Windows\CCM\Logs\smstslog\smsts.log`
- 在 Windows 中，任务序列完成之后：`C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> 只读任务序列变量 [_SMSTSLogPath](/sccm/osd/understand/task-sequence-variables#SMSTSLogPath) 始终包含当前日志文件的路径。


## <a name="see-also"></a>另请参阅

- [日志文件引用](/sccm/core/plan-design/hierarchy/log-files)

- [支持中心 OneTrace](/sccm/core/support/support-center-onetrace)

- [支持中心日志文件查看器](/sccm/core/support/support-center#support-center-log-file-viewer)

- [CMTrace](/sccm/core/support/cmtrace)
