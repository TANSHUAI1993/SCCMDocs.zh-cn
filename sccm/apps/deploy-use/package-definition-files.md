---
title: 包定义文件
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用包定义文件创建包和程序
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba927286e79d88a6e034fd7eb14f5190cb1f34d6
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537675"
---
# <a name="package-definition-files"></a>包定义文件

*适用范围：System Center Configuration Manager (Current Branch)*

包定义文件是用于帮助你在 Configuration Manager 中自动创建[包和程序](/sccm/apps/deploy-use/packages-and-programs)的脚本。 它们提供 Configuration Manager 创建包和程序所需的所有信息，包源文件的位置除外。

## <a name="about-the-package-definition-file-format"></a>关于包定义文件格式

每个包定义文件都是使用 .ini 文件格式的 ASCII 或 UTF-8 文本文件。 它包含以下部分：  

### <a name="pdf"></a>[PDF]

本部分为包定义文件中标识的文件。 它包含以下信息：  

- **版本**：指定文件使用的包定义文件格式的版本。 此版本对应于为其编写的 Configuration Manager 版本。 此项是必需的。  

### <a name="package-definition"></a>[Package Definition]

指定包和程序的属性。 它提供以下信息：  

- **名称**：包的名称，最多 50 个字符。  

- **版本**（可选）：包的版本，最多 32 个字符。  

- **图标**（可选）：包含用于此包的图标的文件。 如果指定，此图标将替换 Configuration Manager 控制台中的默认包图标。

- **发布者**：包的发布服务器，最多 32 个字符。

- **语言**：包的语言版本，最多 32 个字符。

- **备注**（可选）：关于包的注释，最多 127 个字符。

- **ContainsNoFiles**: 此项指示包是否包含任何源文件。  

- **程序**: 为此包定义的程序。 每个程序名称对应于此包定义文件中的一个 **[Program]** 部分。  

    例如：  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**：包含包状态的管理信息格式 (MIF) 文件的名称，最多 50 个字符。  

- **MIFName**：包的名称（与 MIF 匹配），最多 50 个字符。  

- **MIFVersion**：包的版本号（与 MIF 匹配），最多 32 个字符。  

- **MIFPublisher**：包的软件发布服务器（与 MIF 匹配），最多 32 个字符。  

### <a name="program"></a>[Program]

为在 **[Package Definition]** 部分的 Program 项中指定的每  个程序包含 [Program] 部分。 本部分定义每个程序。 每个程序一节提供了以下信息：  

- **名称**：程序的名称，最多 50 个字符。 此项必须是唯一的包中。  

- **图标**（可选）：指定包含用于此程序的图标的文件。 此图标替换 Configuration Manager 控制台中的默认程序图标。 将程序部署到集合时, 客户端也会显示此图标。

- **备注**（可选）：关于程序的注释，最多 127 个字符。

- **CommandLine**：指定程序的命令行，最多 127 个字符。 命令与包源文件夹有关。

- **StartIn**：指定程序的工作文件夹，最多 127 个字符。 此项可以是客户端计算机上的绝对路径，也可以是相对于包源文件夹的路径。

- **运行**：指定程序运行的程序模式。 可以指定 **Minimized**、 **Maximized**或 **Hidden**。 如果不包含此项, 程序将以正常模式运行。  

- **AfterRunning**：指定程序成功完成后会发生的任何特殊操作。 可用的选项有 **SMSRestart**、 **ProgramRestart**或 **SMSLogoff**。 如果不包含此项, 程序将不会运行特殊操作。  

- **EstimatedDiskSpace**：指定在计算机上运行软件程序所需的磁盘空间量。 默认值是“未知”  。 可以将该值设置为大于或等于零的整数。 如果指定一个值, 则还应包括值的单位。  

    例如：  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**：指定预计程序在客户端计算机上运行的持续时间（以分钟计）。 默认值为 120  。 您可以将该值设置为大于零的整数, 或设置为 " **Unknown**"。  

    例如：  

    `EstimatedRunTime=25`  

- **SupportedClients**：指定将在其上运行该程序的处理器和操作系统。 用逗号分隔平台。 如果不包含此项, 则客户端不会检查此程序的支持平台。  

- **SupportedClientMinVersionX**、**SupportedClientMaxVersionX**：指定在 **SupportedClients** 项中指定的操作系统版本号起止范围。  

    例如：  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements**（可选）：提供客户端计算机的任何其他信息或要求，最多 127 个字符。

- **CanRunWhen**：指定在客户端计算机上运行程序所需的用户状态。 可用的值有 **UserLoggedOn**、 **NoUserLoggedOn**或 **AnyUserStatus**。 默认值为 **UserLoggedOn**。  

- **UserInputRequired**：指定程序是否需要与用户交互。 可用的值是 **True** 或 **False**。 默认值为 **True**。 如果 CanRunWhen  未设置为 UserLoggedOn  ，则此项将会设置为 False  。  

- **AdminRightsRequired**：指定程序是否需要计算机的管理凭据才能运行。 可用的值是 **True** 或 **False**。 默认值为 **False**。 如果 CanRunWhen  未设置为 UserLoggedOn  ，则此项将会设置为 True  。  

- **UseInstallAccount**：指定程序在客户端计算机上运行时是否使用客户端软件安装帐户。 默认情况下，该值为 **False**。 如果将 **CanRunWhen** 设置为 **UserLoggedOn** ，则该值也为 **False**。  

- **DriveLetterConnection**：指定程序是否需要将驱动器号与分发点上的包文件进行连接。 可以指定 **True** 或 **False**。 默认值为 **False**，这允许程序使用通用命名约定 (UNC) 连接。 当此值设置为 True  时，客户端将使用下一个可用的驱动器号（以 Z: 开头并向后继续）。  

- **SpecifyDrive**（可选）：指定程序连接到分发点上的包文件所需的驱动器号。 此设置可以将指定的驱动器号强制用于与分发点的客户端连接。

- **ReconnectDriveAtLogon**：指定用户登录时，计算机是否重新连接到分发点。 可用的值是 **True** 或 **False**。 默认值为 **False**。  

- **DependentProgram**：指定此包中的程序必须在当前程序之前运行。 此项使用格式`DependentProgram=<ProgramName>`, 其中`<ProgramName>`是包定义文件中该程序的**名称**条目。 如果没有从属程序，则将此项留空。  

    示例：  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **分配**：指定如何将程序分配给用户。 此值可以为：

    - **FirstUser**: 仅登录到客户端的第一个用户运行程序
    - **EveryUser**: 登录的每个用户都运行程序

    如果 CanRunWhen  未设置为 UserLoggedOn  ，则此项将会设置为 FirstUser  。  

- **Disabled**: 指定是否可以将此程序部署到客户端。 可用的值是 **True** 或 **False**。 默认值为 **False**。  


## <a name="use-a-package-definition-file"></a>使用包定义文件  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“应用程序管理”，然后选择“包”节点    。  

2. 在功能区的“主页”选项卡上的“创建”组中，选择“从定义创建包”    。  

3. 在**从定义创建包向导**的 "**包定义**" 页上, 选择现有包定义文件。 若要打开新的包定义文件, 请选择 "**浏览**"。 指定新的包定义文件后, 从 "**包定义**" 列表中选择它。

4. 在“源文件”  页上，指定包和程序所需的任何源文件信息。  

5. 如果包需要源文件, 请在 "**源文件夹**" 页上, 指定站点可从中获取源文件的位置。  

6. 完成向导。  


## <a name="see-also"></a>另请参阅

[包和程序](/sccm/apps/deploy-use/packages-and-programs)
