---
title: 创建捕获媒体
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的捕获媒体从引用计算机中捕获 OS 映像。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bdd6ca5b2ab0c26caf0f558eff39fc8f01bc9d15
ms.sourcegitcommit: 160bcdaf783f3946ad5c7869b2566cbfc4da545c
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401560"
---
# <a name="create-capture-media"></a>创建捕获媒体

*适用范围：System Center Configuration Manager (Current Branch)*

使用 Configuration Manager 中的捕获媒体可以从引用计算机中捕获 OS 映像。 捕获媒体包含用于启动引用计算机的启动映像，以及用于捕获 OS 映像的任务序列。 使用捕获媒体[创建用于捕获 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system)。  


## <a name="prerequisites"></a>先决条件

在使用“创建任务序列媒体向导”创建捕获媒体之前，请确保满足所有条件。

### <a name="boot-image"></a>启动映像

在任务序列中使用启动映像部署 OS 时，请考虑以下注意事项：

- 启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。
- 确保启动映像包含预配目标计算机所需的网络和存储驱动程序。

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>分发与任务序列关联的所有内容

将任务序列所需的所有内容至少分发到一个分发点。 此内容包括启动映像、OS 映像和其他关联文件。 向导在创建捕获媒体时从分发点收集内容。

用户帐户至少需要具有对该分发点上的内容库的  读取访问权限。 有关详细信息，请参阅[分发内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)。

### <a name="prepare-the-removable-usb-drive"></a>准备可移动的 USB 驱动器

如果使用的是可移动 USB 驱动器，则将其连接到运行“创建任务序列媒体向导”的计算机。 USB 驱动器必须可被 Windows 检测为可移动设备。 向导将在创建媒体时直接写入 USB 驱动器。

### <a name="create-an-output-folder"></a>创建一个输出文件夹

在运行“创建任务序列媒体向导”以便为 CD 或 DVD 集创建媒体之前，为向导创建的输出文件创建一个文件夹。 为 CD 或 DVD 集创建的媒体将以 .ISO 文件形式直接写入该文件夹。


## <a name="process"></a>过程

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，选择“任务序列”  节点。  

2. 在功能区的“主页”选项卡上，在“创建”组中，选择“创建任务序列媒体”    。 此操作会启动“创建任务序列媒体向导”。  

3. 在“选择媒体类型”  页上，选择“捕获媒体”  。  

4. 在“媒体类型”页上，指定媒体是“可移动 USB 驱动器”还是“CD/DVD 集”    。 然后配置以下选项：  

    > [!IMPORTANT]  
    > 媒体使用 FAT32 文件系统。 如果媒体的内容包含超过 4 GB 大小的文件，则无法在 USB 驱动器上创建媒体。  

    - 如果选择“可移动 USB 驱动器”  ，则选择要在其中存储内容的驱动器。  

        - **格式化可移动 U 盘 (FAT32) 并使其可启动**：默认情况下，让 Configuration Manager 准备 U 盘。 很多较新的 UEFI 设备都需要可启动的 FAT32 分区。 但是，此格式还限制文件的大小和驱动器的总容量。 如果已格式化并配置了可移动驱动器，请禁用此选项。

    - 如果选择“CD/DVD 集”，请指定媒体的容量（媒体大小）以及输出文件（媒体文件）的名称和路径    。 向导会将输出文件写入到此位置。 例如：`\\servername\folder\outputfile.iso`  

        如果媒体的容量太小，无法存储整个内容，则会创建多个文件。 然后必须将内容存储在多张 CD 或 DVD 上。 如果需要多个媒体文件，Configuration Manager 会在创建的每个输出文件的名称中添加序号。  

        > [!IMPORTANT]  
        > 如果选择现有的 .iso 映像，任务序列媒体向导将在你进入向导的下一页后立即从驱动器或共享中删除该映像。 即使随后取消该向导，也会删除这个现有的映像。  

    - **暂存文件夹**<!--1359388-->：媒体创建过程可能需要大量临时驱动器空间。 默认情况下，此位置类似于以下路径：`%UserProfile%\AppData\Local\Temp`。 从版本 1902 开始，若要更灵活地选择存储这些临时文件的位置，请将此值更改为其他驱动器和路径。  

    - **媒体标签**<!--1359388-->：从版本 1902 开始，向任务序列媒体添加标签。 此标签可帮助你在创建媒体后更好地识别媒体。 默认值为 `Configuration Manager`。 此文本字段显示在以下位置：  

        - 如果安装 ISO 文件，Windows 会将此标签显示为已安装驱动器的名称  

        - 如果格式化 U 盘，它将使用标签的前 11 个字符作为其名称  

        - Configuration Manager 将名为 `MediaLabel.txt` 的文本文件写入媒体的根目录。 默认情况下，该文件包含一行文本：`label=Configuration Manager`。 如果自定义媒体标签，则此行使用你的自定义标签而不是默认值。  

    - **在媒体上加入 autorun.inf 文件**<!-- 4090666 -->：从版本 1906 开始，默认情况下，Configuration Manager 不会添加 autorun.inf 文件。 反恶意软件通常会阻止此文件。 有关 Windows 的 AutoRun 功能的详细信息，请参阅 [Creating an AutoRun-enabled CD-ROM Application](https://docs.microsoft.com/windows/desktop/shell/autoplay)（创建启用 AutoRun 的 CD-ROM 应用程序）。 如果情况仍然需要，请选择此选项以加入该文件。  

5. 在“启动映像”  页上，指定以下选项：  

    > [!IMPORTANT]  
    > 分发的启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。  

    - **启动映像**：选择用于启动目标计算机的启动映像。  

    - **分发点**：选择具有启动映像的分发点。 向导将从分发点中检索启动映像并将其写入媒体。  

        > [!NOTE]  
        > 用户帐户至少需要具有对该分发点上的内容库的  读取权限。  

6. 完成向导。  


## <a name="next-steps"></a>后续步骤

[创建用于捕获 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system)
