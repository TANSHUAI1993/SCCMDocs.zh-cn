---
title: "管理 BIOS 转换为 UEFI 所采用的任务序列步骤 | Configuration Manager"
description: "了解如何自定义操作系统部署任务的序列，以便为到 UEFI 的转换准备 FAT32 分区。"
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 528ce515c86c4e778532290026a90a46476c4576
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>管理 BIOS 转换为 UEFI 所采用的任务序列步骤
Windows 10 提供了许多需要启用 UEFI 的设备的新安全功能。 你可能拥有支持 UEFI 的新式 Windows 电脑，但正在使用旧版 BIOS。 将设备转换为 UEFI 需要你转到每台电脑、对硬盘重新分区并重新配置固件。 通过在 Configuration Manager 中使用任务序列，你可以准备用于 BIOS 到 UEFI 转换的硬盘，作为就地升级过程的一部分从 BIOS 转换为 UEFI，并收集 UEFI 信息作为硬件清单的一部分。

## <a name="hardware-inventory-collects-uefi-information"></a>硬件清单将收集 UEFI 信息
从版本 1702 开始，新的硬件清单类 (**SMS_Firmware**) 和属性 (**UEFI**) 可用于帮助你确定计算机是否以 UEFI 模式启动。 如果以 UEFI 模式启动计算机，则 **UEFI** 属性设为 **TRUE**。 默认情况下，这在硬件清单中处于启用状态。 有关硬件清单的详细信息，请参阅[如何配置硬件清单](/sccm/core/clients/manage/inventory/configure-hardware-inventory)。

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>创建自定义任务序列以准备用于 BIOS 到 UEFI 转换的硬盘
自 1610 版 Configuration Manager 起，现在可以使用新的变量 TSUEFIDrive 自定义操作系统部署任务的序列，以便“重启计算机”步骤为到 UEFI 的转换在硬盘驱动器上准备 FAT32 分区。 以下过程提供了有关如何创建任务序列步骤以便为 BIOS 到 UEFI 的转换准备硬盘驱动器的示例。

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>为到 UEFI 的转换准备 FAT32 分区：
在现有的用于安装操作系统的任务序列中，添加一个新组，并包含将 BIOS 转换为 UEFI 的步骤。

1. 在捕获文件和设置之后，并在安装操作系统之前，创建新的任务序列组。 例如，在“捕获文件和设置”组之后创建名为“BIOS-to-UEFI”的组。
2. 在新组的“选项”选项卡中，添加一个新的任务序列变量作为条件，其中 **_SMSTSBootUEFI**  **不等于** **true**。 这样可以在计算机已处于 UEFI 模式时，防止运行组中的步骤。

  ![BIOS 转 UEFI 组](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. 在新组中，添加“重启计算机”任务序列步骤。 在“指定重启后要运行的内容”中，选择“已选择分配给此任务序列的启动映像”以在 Windows PE 中启动计算机。  
4. 在“选项”选项卡中，添加一个任务序列变量作为条件，其中 **_SMSTSInWinPE 等于 false**。 这样在计算机已处于 Windows PE 时，防止运行此步骤。

  ![“重启计算机”步骤](../../core/get-started/media/restart-in-windows-pe.png)
5. 添加一个步骤以启动 OEM 工具，该工具可将固件从 BIOS 转换到 UEFI。 这通常是**运行命令行**任务序列步骤，其中有一个命令行可以启动 OEM 工具。
6. 添加“格式化磁盘并分区”任务序列步骤，用于对硬盘进行分区和格式化。 在该步骤中，执行以下操作：
  1. 创建 FAT32 分区，该分区在安装操作系统之前将转换为 UEFI。 为“磁盘类型”选择“GPT”。
    ![格式化磁盘并分区步骤](../media/format-and-partition-disk.png)
  2. 转到 FAT32 分区的属性。 在“变量”字段中输入“TSUEFIDrive”。 当任务序列检测到此变量时，它将为 UEFI 转换做准备，准备就绪后会重启计算机。
    ![分区属性](../../core/get-started/media/partition-properties.png)
  3. 创建 NTFS 分区，任务序列引擎使用此分区保存其状态和存储日志文件。
7. 添加“重启计算机”任务序列步骤。 在“指定重启后要运行的内容”中，选择“已选择分配给此任务序列的启动映像”以在 Windows PE 中启动计算机。  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>在就地升级过程中从 BIOS 转换为 UEFI
Windows 10 创意者更新引入了一个简单的转换工具，可自动执行对用于启用 UEFI 的硬件的硬盘重新分区的过程，并将该转换工具集成到 Windows 7 到 Windows 10 的就地升级过程中。 将此工具与操作系统升级任务序列和将固件从 BIOS 转换为 UEFI 的 OEM 工具组合时，可以在就地升级到 Windows 10 创意者更新的过程中将计算机从 BIOS 转换为 UEFI。

**要求**：
- Windows 10 创意者更新
- 支持 UEFI 的计算机
- 将计算机固件从 BIOS 转换为 UEFI 的 OEM工具

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>在就地升级过程中从 BIOS 转换为 UEFI
1. 创建一个操作系统升级任务序列，用于执行到 Windows 10 创意者更新的就地升级。
2. 编辑任务序列。 在“正在后处理组”中，添加以下任务顺序步骤：
   1. 从“常规”中，添加“运行命令行”步骤。 你将添加 MBR 2 GPT 工具的命令行，该工具将磁盘从 MBR 转换为 GPT，而不会修改或删除磁盘中的数据。 在命令行中，键入以下内容：**MBR2GPT /convert /disk:0 /AllowFullOS**。 你也可以选择在 Windows PE 中运行 MBR 2 GPT.EXE 工具，而不是在完整的操作系统中运行。 你可以通过在运行 MBR2GPT.EXE 工具并从命令行中删除 /AllowFullOS 选项之前添加重启计算机到 WinPE 的步骤来执行此操作。 有关该工具和可用选项的详细信息，请参阅 [MBR2GPT.EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt)。
   2. 添加一个步骤以启动 OEM 工具，该工具可将固件从 BIOS 转换到 UEFI。 这通常是一个运行命令行任务序列步骤，其中有一个命令行来启动 OEM 工具。
   3. 从“常规”中，添加“重新启动计算机”步骤。 要指定重新启动后要运行的内容，请选择“当前安装的默认操作系统”。
3. 部署任务序列。
