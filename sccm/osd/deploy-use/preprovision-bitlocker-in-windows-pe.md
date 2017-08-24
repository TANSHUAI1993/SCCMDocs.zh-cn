---
title: "预先设置 Windows PE 中的 BitLocker | Microsoft Docs"
description: "在部署操作系统之前，可通过 Configuration Manager 中的预设置 BitLocker 任务从 Windows 预安装环境启用 BitLocker。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: baca498dbc5b8e168852aa3c18ee23a9c483e69c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="preprovision-bitlocker-in-windows-pe-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 预先设置在 Windows PE 中的 BitLocker

*适用范围：System Center Configuration Manager (Current Branch)*

利用 System Center Configuration Manager 中的“预设置 BitLocker”任务序列步骤，可以在部署操作系统之前从 Windows 预安装环境 (Windows PE) 中启用 BitLocker。 由于仅加密使用的磁盘空间，因此加密时间要短得多。 这是通过在运行 Windows 设置进程之前将随机生成的清除保护程序应用于格式化的卷并对卷进行加密来完成的。 Windows 8 和 Windows Server 2012 引入了预设置 BitLocker 的功能。 但是，只要遵循特定步骤，即可在硬盘上预设置 BitLocker 并安装 Windows 7。 当 Windows 7 安装程序完成后，你必须设置 BitLocker 密钥保护程序，因为 Windows 7 BitLocker 控制面板不使用清除保护程序支持 BitLocker。 你必须执行“启用 BitLocker”  步骤或者使用 manage-bde.exe 命令行工具来添加密钥保护程序。  

 通常，你必须执行以下操作，以在将安装 Windows 7 的计算机上成功预设置 BitLocker：  

-   在 Windows PE 中重启计算机  

    > [!IMPORTANT]  
    >  你必须使用带有 Windows PE 4 或更高版本的启动映像来预设置 BitLocker。 有关 Configuration Manager 中支持的 Windows PE 版本的详细信息，请参阅 [Configuration Manager 的外部依赖关系](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies)。  

-   对硬盘进行分区和格式化  

-   中的“预设置 BitLocker”  

-   使用特定的操作系统和网络设置安装 Windows 7  

-   将密钥保护程序添加到 BitLocker 中  

 在 Configuration Manager 中，在硬盘上预设置 BitLocker 以及安装 Windows 7 的建议方法为：创建新任务序列，并从“创建任务序列向导”的“新建任务序列”页中选择“安装现有的映像包”。 此向导将创建下表中列出的任务序列步骤。  

> [!NOTE]  
>  任务序列可能具有其他步骤，具体取决于你在向导中配置设置的方式。 例如，如果在向导的“状态迁移”  页上选择了“捕获 Microsoft Windows 设置”  ，则可能具有“捕获 Windows 设置”  步骤。  

|任务序列步骤|详细信息|  
|------------------------|-------------|  
|禁用 BitLocker|如果当前启用了 BitLocker 加密，则此步骤将禁用该加密。 有关详细信息，请参阅[禁用 BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker)。|  
|在 Windows PE 中重启计算机|此步骤通过运行分配给任务序列的启动映像在 Windows PE 中重启计算机。 你必须使用带有 Windows PE 4 或更高版本的启动映像来预设置 BitLocker。 有关详细信息，请参阅[重启计算机](../understand/task-sequence-steps.md#BKMK_RestartComputer)。|  
|对磁盘 0 分区 - BIOS<br /><br /> 对磁盘 0 分区 - UEFI|这些步骤使用 BIOS 或 UEFI 对目标计算机上的指定驱动器进行格式化和分区。 当任务序列检测到目标计算机处于 UEFI 模式时，它会使用 UEFI。 有关详细信息，请参阅[格式化磁盘并分区](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk)。|  
|中的“预设置 BitLocker”|在 Windows PE 中，此步骤将在驱动器上启用 BitLocker。 仅加密使用的驱动器空间。 因为你在上一个步骤中对硬盘进行了分区和格式化，因此没有数据并且加密完成得非常快。 有关详细信息，请参阅[预设置 BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker)。|  
|应用操作系统|此步骤准备用于在目标计算机上安装操作系统的答案文件，并将 OSDTargetSystemDrive 任务序列变量设置为包含操作系统文件的分区的驱动器号。 “安装 Windows 和 ConfigMgr”步骤使用答案文件和变量来安装操作系统。 有关详细信息，请参阅 [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)。|  
|应用 Windows 设置|此步骤将 Windows 设置添加到答案文件中。 “安装 Windows 和 ConfigMgr”步骤使用答案文件来安装操作系统。 有关详细信息，请参阅 [应用 Windows 设置](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings)。|  
|应用网络设置|此步骤将网络设置添加到答案文件中。 “安装 Windows 和 ConfigMgr”步骤使用答案文件来安装操作系统。 有关详细信息，请参阅[应用网络设置步骤](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings)。|  
|应用设备驱动程序|此步骤在操作系统部署过程中匹配和安装驱动程序。 有关详细信息，请参阅[自动应用驱动程序](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers)。|  
|安装 Windows 和 ConfigMgr|此步骤执行从 Windows PE 到新操作系统的转换。 此任务序列步骤是在部署任何操作系统时都必需的部分。 该步骤会将 Configuration Manager 客户端安装到新操作系统中，并为任务序列在新操作系统中继续执行做好准备。 有关详细信息，请参阅[安装 Windows 和 ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)。|  
|启用 BitLocker|此步骤在硬盘上启用 BitLocker 加密并设置密钥保护程序。 因为用 BitLocker 预设置了硬盘，所以此步骤完成得非常快。 Windows 7 要求你添加密钥保护程序。 如果你未使用此步骤，则可以运行 manage-bde.exe 命令行工具来设置密钥保护程序。 有关详细信息，请参阅[启用 BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker)。|  
