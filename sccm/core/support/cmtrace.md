---
title: CMTrace
titleSuffix: Configuration Manager
description: 了解如何使用 CMTrace 工具查看 Configuration Manager 的日志文件。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 87552016d1cd17e79abf01a9de9109195d3d2a70
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125289"
---
# <a name="cmtrace"></a>CMTrace

适用范围：System Center Configuration Manager (Current Branch)

CMTrace 是一个 [Configuration Manager 工具](/sccm/core/support/tools)。 可通过它查看和监视日志文件，包括以下类型：  

- Configuration Manager 或 Client Component Manager (CCM) 格式的日志文件  

- 纯 ASCII 或 Unicode 文本文件，例如 Windows Installer 日志  

该工具使用突出显示、筛选和错误查找功能来帮助分析日志文件。

从 1806 版开始，CMTrace 日志查看工具自动与 Configuration Manager 客户端一起安装。 它被添加到客户端安装目录，默认情况下为 `%WinDir%\CCM\CMTrace.exe`。<!--1357971-->

> [!Note]  
> CMTrace 不会自动注册到 Windows 以打开 .log 文件扩展名。 有关详细信息，请参阅[文件关联](#file-associations)。  



## <a name="usage"></a>用法

运行 **CMTrace.exe**。 第一次运行该工具时，会出现文件关联提示。 有关详细信息，请参阅[文件关联](#file-associations)。

可以在 CMTrace 的以下菜单中执行大部分操作：
- [File](#file-menu)
- [工具](#tools-menu)


### <a name="file-menu"></a>“文件”菜单

“文件”菜单中提供以下操作：  
- [打开](#open)
- [在服务器上打开](#open-on-server)
- [打印](#print)
- [首选项](#preferences)

“文件”菜单还列出最近使用的八个文件。 通过从“文件”菜单中选择其中一个日志，可快速重新打开该日志。 

#### <a name="open"></a>打开
显示“打开”对话框以浏览日志文件。 

筛选以下类型的文件的视图： 
- 日志文件 (\*.log)  
- 旧日志文件 (\*.lo_) 
- 所有文件 (\*.\*)

默认情况下未选择以下两个选项：  

- **忽略现有行**：选中后，CMTrace 会忽略所选日志文件的现有内容，仅显示所添加的新行。 当不需要日志文件的完整历史记录时，可使用此选项仅监视新操作。  

- **合并所选文件**：如果启用此选项并选择多个日志文件，CMTrace 会在视图中合并所选日志。 它将它们显示为单个日志文件。 合并后的日志像单个日志文件一样进行更新并支持其他所有 CMTrace 功能。  


#### <a name="open-on-server"></a>在服务器上打开
使用标准“浏览”对话框浏览站点系统计算机上的 Configuration Manager 日志文件夹。 还可以浏览网络中的远程计算机。   

选择要浏览的远程计算机时，CMTrace 会检查 Configuration Manager 共享。 如果找不到包含 Configuration Manager 日志文件的共享，则会显示错误消息。  

若要在不浏览的情况下直接连接到已知计算机，请使用[打开](#open)操作。 然后使用 UNC 格式输入服务器名称和共享。

#### <a name="print"></a>打印
显示标准的 Windows 打印对话框。 此操作会将当前日志文件发送到打印机。 它根据 CMTrace 首选项的“打印”选项卡上的设置格式化输出。

#### <a name="preferences"></a>首选项
配置 CMTrace 设置。 可用选项如下：  

- “常规” 选项卡  

     - **更新间隔**：控制 CMTrace 检查日志文件更改和加载新行的频率。 默认情况下，此值为 500 毫秒。  

     - **突出显示**：设置突出显示所选日志行时 CMTrace 使用的颜色。 默认情况下，此颜色为最基本的黄色（红色：255，绿色：255，蓝色：0）。  

     - **列**：配置日志视图中显示的列及其显示顺序。 默认情况下，它显示日志文本、组件、日期/时间和线程。  

- “打印”选项卡  

     - **列**：配置它在打印日志文件时使用的列及其显示顺序。 默认情况下，打印的列与显示的列相同。  

     - **方向**：设置打印日志文件时的默认打印方向。 在“打印”对话框中覆盖此设置。 默认情况下，它使用“纵向”方向。  
 
- “高级”选项卡  

     - **刷新间隔**：强制 CMTrace 在加载大量行时以指定的时间间隔更新日志视图。 默认情况下，此选项处于禁用状态且值为零。  

        > [!Note]  
        > 一般情况下，请勿修改“刷新间隔”。 它可能会显著增加打开大型日志文件所需的时间。 


### <a name="tools-menu"></a>“工具”菜单
“工具”菜单中提供以下操作：  
- [查找](#find)
- [查找下一个](#find-next)
- [复制到剪贴板](#copy-to-clipboard)
- [突出显示](#highlight)
- [筛选器](#filter)
- [错误查找](#error-lookup)
- [暂停](#pause)
- [显示/隐藏详细信息](#show-hide-details)
- [显示/隐藏信息窗格](#show-hide-info-pane)

#### <a name="find"></a>查找
在打开的日志文件中搜索指定的文本字符串。  

#### <a name="find-next"></a>查找下一个
如先前在“查找”对话框中指定的那样，查找下一个匹配字符串。  

#### <a name="copy-to-clipboard"></a>复制到剪贴板
将所选行以纯文本形式复制到 Windows 剪贴板。 如果你正在检查 Configuration Manager 和 CCM 日志文件，它会按照与视图相同的顺序复制列。 它用制表符分隔每一列。 将日志复制到电子邮件或其他文档时，可使用此操作。  

#### <a name="highlight"></a>突出显示
输入 CMTrace 用于搜索每个日志条目的文本的字符串。 然后，它会突出显示与输入的字符串匹配的所有日志文本。  

- 突出显示功能使用在“首选项”中指定的颜色。  

- 若要关闭突出显示，请清除此字段中的字符串。  

- 如果输入十进制数或十六进制数，CMTrace 会尝试将该值与“线程”列匹配。 此行为用于突出显示单个线程的处理，而不筛选掉可能与其交互的其他线程。  

- 若要比较字符串大小写，请启用“区分大小写”选项。  
 
#### <a name="filter"></a>筛选器
根据指定条件显示或隐藏日志行。 将筛选器应用于四列中的任何一列，无论它们是否可见。 这些设置适用于每个打开的日志文件。 

示例：<!--SCCMDocs issue #603-->
- 根据包含“the action”或“the group”的条目文本筛选 **smsts.log**。 
- 筛选条目文本包含“destination”的 **InventoryAgent.log**。


#### <a name="error-lookup"></a>错误查找
键入或粘贴十进制或十六进制格式的错误代码以显示说明。 可能的错误源包括：Windows、WMI 或 Winhttp。

#### <a name="pause"></a>暂停
挂起或重启日志监视。 以下用例是导致使用此操作的一些可能的原因：  

- 当 CMTrace 过快显示日志文件信息时  

- 暂停日志监视时，如果当前文件滚动更新为新日志，CMTrace 显示的信息不会丢失  

- 如果要在检查日志文件时阻止 CMTrace 显示新数据  

#### <a name="showhide-details"></a>显示/隐藏详细信息
显示或隐藏日志文本以外的所有列。 它还将日志文本列扩展为窗口宽度。 在显示分辨率较低的计算机上查看日志时，可使用此操作。 它会显示更多日志文本。  

> [!Note]   
> 查看纯文本文件时，CMTrace 会自动隐藏详细信息，因为它们始终为空。  
 
#### <a name="showhide-info-pane"></a>显示/隐藏信息窗格
显示或隐藏信息窗格。 在显示分辨率较低的计算机上查看日志时，可使用此操作。 它会显示更多日志记录详细信息。  



## <a name="log-pane"></a>日志窗格

日志窗格位于 CMTrace 窗口顶部。 它显示日志文件中的行。 

当你选中某行时，系统会使用 Windows 所选内容配色方案暂时突出显示该行。 

突出显示的行符合你使用“工具”菜单中的“突出显示”选项定义的条件。 突出显示功能使用在“首选项”中指定的颜色。

CMTrace 使用红色背景和黄色文本颜色显示有错误的行。 在 CCM 格式日志中，日志条目具有一个将该条目指示为错误的显式类型值。 对于其他日志格式，CMTrace 会在每个条目中以不区分大小写的形式搜索与“error”匹配的所有文本字符串。

它使用黄色背景显示包含警告的行。 在 CCM 格式日志中，日志条目具有一个将该条目指示为警告的显式类型值。 对于其他日志格式，CMTrace 会在每个条目中以不区分大小写的形式搜索与“warn”匹配的所有文本字符串。



## <a name="info-pane"></a>信息窗格

信息窗格位于 CMTrace 窗口底部。 它包括以下功能：   

- 有关当前所选日志条目的详细信息  

- 显示日志文本的文本框  

- 它显示回车符，使格式化文本更易于阅读  

- 更易于阅读日志窗格中不完全可见的长条目  

使用“工具”菜单上的“显示/隐藏信息窗格”选项显示或隐藏信息窗格。 如果信息窗格占用日志窗口的一半以上，CMTrace 会自动隐藏它。


### <a name="progress-bar"></a>进度栏

当你第一次打开日志文件时，CMTrace 会用进度栏替换信息窗格。 此进度指示它加载了多少现有文件内容。 进度达到 100% 时，CMTrace 会删除进度栏，将其替换为信息窗格。 加载大型文件时，此行为可以指示加载可能需要多长时间。


### <a name="status-bar"></a>状态栏

对于 Configuration Manager 格式和 CCM 格式的日志文件，状态栏显示所选日志条目的已用时间。 如果选择单个条目，该工具会显示从第一个日志条目到所选条目的时间。 如果选择多个条目，它会计算从最顶层的所选条目到最底层的所选条目的时间。 CMTrace 按下面所示格式化此信息：

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`



## <a name="windows-shell-integration"></a>Windows Shell 集成

CMTrace 支持[文件关联](#file-associations)和[拖放](#drag-and-drop)。


### <a name="file-associations"></a>文件关联 

CMTrace 可以将自身与 .log 和 .lo_ 文件扩展名相关联。 程序启动时，它会检查注册表，确定它是否已与这些文件扩展名相关联。 如果 CMTrace 尚未与任何文件扩展名相关联，则会提示你将文件扩展名与 CMTrace 相关联。 如果选择“不要再对此询问我”，CMTrace 会在此计算机上运行时跳过此检查。


### <a name="drag-and-drop"></a>拖放

CMTrace 支持基本的拖放功能。 将日志文件从 Windows 资源管理器拖到 CMTrace 以将其打开。



## <a name="other-tips"></a>其他提示

### <a name="last-directory-registry-key"></a>Last Directory 注册表项
<!--511280--> 默认情况下，CMTrace 会保存你打开的最后一个日志位置。 此行为在站点服务器上很有用，因为它每次都默认为日志路径。 

第一次在客户端上启动它时，它默认为当前工作目录。 此位置可能是保存 CMTrace 的路径，也可能是类似于 `%userprofile%\Desktop` 的路径。 

注册表项 `HKEY_CURRENT_USER\Software\Microsoft\Trace32` 中的“Last Directory”值可控制此默认位置。 如果在客户端上将此值设置为 `%windir%\CCM\Logs`，则 CMTrace 会在你第一次运行它时在该客户端日志位置中打开文件。


## <a name="see-also"></a>另请参阅

[日志文件](/sccm/core/plan-design/hierarchy/log-files)
