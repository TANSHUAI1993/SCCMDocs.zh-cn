---
title: "管理 BIOS 转换为 UEFI 所采用的任务序列步骤 | Configuration Manager"
description: "了解如何自定义操作系统部署任务的序列，以便为到 UEFI 的转换准备 FAT32 分区。"
ms.custom: na
ms.date: 11/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 54089ac8aa95154534d010bee8c7e2cbd70d1c7e
ms.openlocfilehash: 30838ed3ad045f781a748f96c874bf543ea05462


---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>管理 BIOS 转换为 UEFI 所采用的任务序列步骤
自 1610 版 Configuration Manager 起，现在可以使用新的变量 TSUEFIDrive 自定义操作系统部署任务的序列，以便“重启计算机”步骤为到 UEFI 的转换在硬盘驱动器上准备 FAT32 分区。 以下过程提供了有关如何创建任务序列步骤以便为 BIOS 到 UEFI 的转换准备硬盘驱动器的示例。

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>为到 UEFI 的转换准备 FAT32 分区：
在现有的用于安装操作系统的任务序列中，添加一个新组，并包含将 BIOS 转换为 UEFI 的步骤。

1. 在捕获文件和设置之后，并在安装操作系统之前，创建新的任务序列组。 例如，在“捕获文件和设置”组之后创建名为“BIOS-to-UEFI”的组。
2. 在新组的“选项”选项卡中，添加一个新的任务序列变量作为条件，其中 **_SMSTSBootUEFI** ** 不等于** **true**。 这样可以在计算机已处于 UEFI 模式时，防止运行组中的步骤。
![BIOS 转 UEFI 组](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. 在新组中，添加“重启计算机”任务序列步骤。 在“指定重启后要运行的内容”中，选择“已选择分配给此任务序列的启动映像”以在 Windows PE 中启动计算机。  
4. 在“选项”选项卡中，添加一个任务序列变量作为条件，其中 **_SMSTSInWinPE 等于 false**。 这样在计算机已处于 Windows PE 时，防止运行此步骤。

    ![“重启计算机”步骤](../../core/get-started/media/restart-in-windows-pe.png)
5. 添加一个步骤以启动 OEM 工具，该工具可将固件从 BIOS 转换到 UEFI。 这通常是**运行命令行**任务序列步骤，其中有一个命令行可以启动 OEM 工具。
6.  添加“格式化磁盘并分区”任务序列步骤，用于对硬盘进行分区和格式化。 在该步骤中，执行以下操作：
    1.  创建 FAT32 分区，该分区在安装操作系统之前将转换为 UEFI。 为“磁盘类型”选择“GPT”。
    ![格式化磁盘并分区步骤](../../core/get-started/media/format-and-partition-disk.png)
    2.  转到 FAT32 分区的属性。 在“变量”字段中输入“TSUEFIDrive”。 当任务序列检测到此变量时，它将为 UEFI 转换做准备，准备就绪后会重启计算机。
    ![分区属性](../../core/get-started/media/partition-properties.png)
    3. 创建 NTFS 分区，任务序列引擎使用此分区保存其状态和存储日志文件。
6.  添加“重启计算机”任务序列步骤。 在“指定重启后要运行的内容”中，选择“已选择分配给此任务序列的启动映像”以在 Windows PE 中启动计算机。  



<!--HONumber=Dec16_HO3-->


