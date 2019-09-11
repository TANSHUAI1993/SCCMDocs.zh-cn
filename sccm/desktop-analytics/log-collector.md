---
title: 日志收集器
titleSuffix: Configuration Manager
description: 使用日志收集器工具帮助排查桌面分析问题
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 24f8b723a82f2adb4eb160b0e3edab1efbca1e95
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70891752"
---
# <a name="desktop-analytics-log-collector"></a>桌面分析日志收集器

从 Configuration Manager 版本1906开始，使用 Configuration Manager 安装目录中的**DesktopAnalyticsLogsCollector**工具来帮助解决桌面分析设备注册问题。 它会运行一些基本故障排除步骤，并将相关日志收集到单个工作目录中。 你可以与 Microsoft 支持部门共享此内容。


## <a name="prerequisites"></a>先决条件

- 运行 Windows 10、Windows 8.1 或带有 Service Pack 1 的 Windows 7 的桌面分析客户端

- 在设备上以管理用户身份运行脚本，并以**管理员身份运行**。

    > [!Tip]
    > 您可以使用此工具的 Configuration Manager**脚本**功能。 有关详细信息，请[参阅示例5：通过 Configuration Manager**脚本**](#bkmk_ex5)部署脚本。

- PowerShell 版本4.0 或更高版本
    - .NET framework 4.6 或更高版本
    - Windows Management Framework 4.0 或更高版本

## <a name="usage"></a>用法

从 Configuration Manager 安装内容获取脚本：`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>参数

### `-LogPath`

指定用于放置日志和其他输出文件的本地或 UNC 路径。

**值**：

- 本地路径（最大长度 = 130），例如：`c:\myfolder`

- UNC 路径（最大长度 = 130），例如：`\\myserver\myfolder`

**类型**：String

**位置**：1

**默认值**：`$Env:SystemDrive\M365AnalyticsLogs`（当此参数为 null、空或空格时，该脚本将在系统驱动器下创建 M365AnalyticsLogs 文件夹。）

### `-LogMode`

指定日志的详细级别。

**值**：

- `0`：仅将脚本消息记录到 PowerShell 命令窗口。

- `1`：在输出文件夹和 PowerShell 命令窗口下，将脚本消息记录到两个日志文件。

- `2`：仅将脚本消息记录到 output 文件夹下的日志文件。

**类型**：Int16

**位置**：2

**默认值**：`1`（将脚本消息记录到日志文件和 PowerShell 命令窗口。）

### `-CollectNetTrace`

指定脚本是否收集网络跟踪。

**值**：

- `0`：不要启用网络跟踪。

- `1`（任何非零整数值）：启用网络跟踪并收集结果。

**类型**：Int16

**位置**：3

**默认值**：`0`（不要启用网络跟踪）

### `-CollectUTCTrace`

指定脚本是否收集 Windows UTC 跟踪和运行连接性诊断。

**值**：

- `0`：不要启用 UTC 跟踪或运行连接性诊断。

- `1`（任何非零整数值）：启用 UTC 跟踪，运行连接性诊断，并收集结果。

**类型**：Int16

**位置**：4

**默认值**：`0`（不要启用 UTC 跟踪或运行连接性诊断）


## <a name="output"></a>Output

该脚本在指定的路径下创建一个*工作文件夹*。 例如， **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**。 它将其所有输出文件放入此工作文件夹。

如果允许脚本写入*日志文件*，则会在工作文件夹中生成一个。 例如， **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss**。

该脚本还会在工作文件夹中生成其他*诊断文件*。 例如：

- `installedKBs.txt`：设备上安装的 Windows 更新的列表
- `appcompat`：应用程序兼容性数据
- `Reg*.txt`：一系列文件，其中包含从 Windows 注册表导出的数据


## <a name="examples"></a>示例

### <a name="bkmk_ex1"></a>示例1：通过具有默认值的 PowerShell 命令窗口运行脚本

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="bkmk_ex2"></a>示例2：通过具有指定参数的 PowerShell 命令窗口运行脚本

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="bkmk_ex3"></a>示例3：通过具有指定参数的 PowerShell 命令窗口运行脚本

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="bkmk_ex4"></a>示例4：通过带有指定参数和详细消息的 PowerShell 命令窗口运行脚本

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="bkmk_ex5"></a>示例5：通过 Configuration Manager**脚本**部署脚本

有关详细信息，请参阅[从 Configuration Manager 控制台创建并运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)。

DesktopAnalyticsLogsCollector 由 Microsoft 进行数字签名。 可能需要在目标设备上将其 Microsoft 代码签名证书作为受信任的发布者添加。

1. 在 Windows 资源管理器中打开该脚本的属性。 切换到 "**数字签名**" 选项卡，然后选择 "**详细信息**"。

1. 在 "**常规**" 选项卡上，选择 "**查看证书**"。

    > [!Note]
    > 若要通过其他机制分发证书，请首先将证书导出到文件。 中转到 "**详细信息**" 选项卡，并选择 "**复制到文件**"。

1. 选择 "**安装证书**"。 导入证书，并将其放入 "**受信任的发行者**" 存储区。


## <a name="see-also"></a>另请参阅

- [桌面分析疑难解答](/sccm/desktop-analytics/troubleshooting)

- [从 Configuration Manager 控制台创建并运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)
