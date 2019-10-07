---
title: 创建独立媒体
titleSuffix: Configuration Manager
description: 使用独立媒体在无网络连接的计算机上部署 OS。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37143372acdadb6a340c2ee556901f5133683c5f
ms.sourcegitcommit: 160bcdaf783f3946ad5c7869b2566cbfc4da545c
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401578"
---
# <a name="create-stand-alone-media"></a>创建独立媒体

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的独立媒体包含在无网络连接的计算机上部署 OS 所需的所有内容。

在以下 OS 部署方案中使用独立媒体：  

- [使用新版的 Windows 刷新现有的计算机](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)  

- [在新计算机（裸机）上安装新版的 Windows](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

- [将 Windows 升级到最新版本](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  


## <a name="usage"></a>用法

独立媒体包含自动执行用于安装 OS 和所有其他所需内容的步骤的任务序列。 此内容包括启动映像、OS 映像和设备驱动程序。 由于部署 OS 所需的所有内容均存储在独立媒体上，因此，独立媒体所需的磁盘空间将显著大于其他类型的媒体所需的磁盘空间。

在管理中心站点上创建独立媒体时，客户端会从 Active Directory 检索其分配的站点代码。 在子站点上创建的独立媒体会自动将该站点的站点代码分配给客户端。  


## <a name="prerequisites"></a>先决条件

在使用“创建任务序列媒体向导”创建独立媒体之前，请确保满足所有条件。

### <a name="create-a-task-sequence-to-deploy-an-os"></a>创建用于部署 OS 的任务序列

作为独立媒体的一部分，请指定用于部署 OS 的任务序列。 有关详细信息，请参阅[创建用于安装 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system)。

#### <a name="unsupported-actions-for-stand-alone-media"></a>独立媒体不支持的操作

独立媒体不支持下列操作：

- 任务序列中的[自动应用驱动程序](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers)步骤。 独立媒体不支持自动应用驱动程序目录中的设备驱动程序。 可使用[应用驱动程序包](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage)步骤以使一组特定驱动程序可用于 Windows 安装程序。  

- 任务序列中的[下载包内容](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent)步骤。 管理点信息在独立媒体上不可用，因此该步骤尝试枚举内容位置将失败。  

- 安装软件更新。  

- 在部署 OS 之前安装软件。  

- 非 OS 部署的自定义任务序列。  

- 将用户与目标计算机关联以支持用户设备相关性。  

- 通过[安装包](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)步骤安装动态包。  

- 通过[安装应用程序](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication)步骤安装动态应用程序。

- “安装 Windows 和 ConfigMgr”任务序列步骤中的“使用预生产客户端包(可用时)”设置   。 有关此设置的详细信息，请参阅[安装 Windows 和 ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)。  

> [!NOTE]  
> 如果任务序列包括[安装包](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)步骤，并且在管理中心站点创建独立媒体，则可能发生错误。 管理中心站点没有必需的客户端配置策略。 在运行任务序列期间启用软件分发代理时需要这些策略。 在 CreateTsMedia.log  文件中可能会出现以下错误：  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> 对于包括“安装包”步骤的独立媒体，请在已启用软件分发代理的主站点创建独立媒体  。
>
> 或者，使用自定义[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)步骤。 在[安装 Windows 和 ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)步骤之后，第一个**安装包**步骤之前执行该步骤。 “运行命令行”  步骤运行以下 WMIC 命令，以便在第一个“安装包”步骤运行之前启用软件分发代理：  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>分发与任务序列关联的所有内容

将任务序列所需的所有内容至少分发到一个分发点。 此内容包括启动映像、OS 映像和其他关联文件。 向导在创建媒体时从分发点中收集内容。

用户帐户至少需要具有对该分发点上的内容库的  读取访问权限。 有关详细信息，请参阅[分发内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)。

### <a name="prepare-the-removable-usb-drive"></a>准备可移动的 USB 驱动器

如果使用的是可移动 USB 驱动器，则将其连接到运行“创建任务序列媒体向导”的计算机。 USB 驱动器必须可被 Windows 检测为可移动设备。 向导将在创建媒体时直接写入 USB 驱动器。

独立媒体使用 FAT32 文件系统。 如果独立媒体的内容包含超过 4 GB 大小的文件，则无法在可移动 USB 驱动器上创建独立媒体。

### <a name="create-an-output-folder"></a>创建一个输出文件夹

在运行“创建任务序列媒体向导”以便为 CD 或 DVD 集创建媒体之前，为向导创建的输出文件创建一个文件夹。 为 CD 或 DVD 集创建的媒体将以 .ISO 文件形式直接写入该文件夹。


## <a name="process"></a>过程

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，选择“任务序列”  节点。  

2. 在功能区的“主页”选项卡上，在“创建”组中，选择“创建任务序列媒体”    。 此操作会启动“创建任务序列媒体向导”。  

3. 在“选择媒体类型”  页上，指定以下选项：  

    - 选择“独立媒体”  。  

    - （可选）如果你希望仅允许部署 OS 而不需要用户输入，请选择“允许无人参与的操作系统部署”  。  

        > [!IMPORTANT]  
        > 如果选择此选项，则不会提示用户输入网络配置信息或可选的任务序列。 如果针对密码保护配置媒体，则仍会提示用户输入密码。  

4. 在“媒体类型”页上，指定媒体是“可移动 USB 驱动器”还是“CD/DVD 集”    。 然后配置以下选项：  

    > [!IMPORTANT]  
    > 媒体使用 FAT32 文件系统。 如果媒体的内容包含超过 4 GB 大小的文件，则无法在 USB 驱动器上创建媒体。  

    - 如果选择“可移动 USB 驱动器”  ，则选择要在其中存储内容的驱动器。  

        - **格式化可移动 U 盘 (FAT32) 并使其可启动**：默认情况下，让 Configuration Manager 准备 U 盘。 很多较新的 UEFI 设备都需要可启动的 FAT32 分区。 但是，此格式还限制文件的大小和驱动器的总容量。 如果已格式化并配置了可移动驱动器，请禁用此选项。

    - 如果选择“CD/DVD 集”，请指定媒体的容量（媒体大小）以及输出文件（媒体文件）的名称和路径    。 向导会将输出文件写入到此位置。 例如：`\\servername\folder\outputfile.iso`  

        如果媒体的容量太小，无法存储整个内容，则会创建多个文件。 然后必须将内容存储在多张 CD 或 DVD 上。 如果需要多个媒体文件，Configuration Manager 会在创建的每个输出文件的名称中添加序号。  

        如果将应用程序与 OS 一起部署，而单个媒体无法容纳应用程序，Configuration Manager 会将应用程序存储到多个媒体中。 在运行独立媒体时，Configuration Manager 会提示用户提供下一个存储了应用程序的媒体。  

        > [!IMPORTANT]  
        > 如果选择现有的 .iso 映像，任务序列媒体向导将在你进入向导的下一页后立即从驱动器或共享中删除该映像。 即使随后取消该向导，也会删除这个现有的映像。  

    - **暂存文件夹**<!--1359388-->：媒体创建过程可能需要大量临时驱动器空间。 默认情况下，此位置类似于以下路径：`%UserProfile%\AppData\Local\Temp`。 从版本 1902 开始，若要更灵活地选择存储这些临时文件的位置，请将此值更改为其他驱动器和路径。  

    - **媒体标签**<!--1359388-->：从版本 1902 开始，向任务序列媒体添加标签。 此标签可帮助你在创建媒体后更好地识别媒体。 默认值为 `Configuration Manager`。 此文本字段显示在以下位置：  

        - 如果安装 ISO 文件，Windows 会将此标签显示为已安装驱动器的名称  

        - 如果格式化 U 盘，它将使用标签的前 11 个字符作为其名称  

        - Configuration Manager 将名为 `MediaLabel.txt` 的文本文件写入媒体的根目录。 默认情况下，该文件包含一行文本：`label=Configuration Manager`。 如果自定义媒体标签，则此行使用你的自定义标签而不是默认值。  

    - **在媒体上加入 autorun.inf 文件**<!-- 4090666 -->：从版本 1906 开始，默认情况下，Configuration Manager 不会添加 autorun.inf 文件。 反恶意软件通常会阻止此文件。 有关 Windows 的 AutoRun 功能的详细信息，请参阅 [Creating an AutoRun-enabled CD-ROM Application](https://docs.microsoft.com/windows/desktop/shell/autoplay)（创建启用 AutoRun 的 CD-ROM 应用程序）。 如果情况仍然需要，请选择此选项以加入该文件。  

5. 在“安全”  页上，指定以下选项：

    - **使用密码保护媒体**：输入强密码来帮助防止未经授权访问媒体。 如果指定密码，则用户必须提供该密码才能使用媒体。  

        > [!IMPORTANT]  
        > 作为最佳安全方案，请始终分配密码来帮助保护媒体。  
        >
        > 在独立媒体上，只会加密任务序列步骤及其变量。 不会加密媒体的其余内容。 请勿在任务序列脚本中包含任何敏感信息。 请使用任务序列变量来存储和提供所有敏感信息。  

    - **为此独立媒体选择有效日期范围**：在媒体上设置可选的开始日期和到期日期。 默认情况下，此设置处于禁用状态。 独立介质运行前，该日期将与计算机上的系统时间进行比较。 如果系统时间早于开始时间或晚于到期时间，则独立介质不会启动。 也可通过使用 [New-CMStandaloneMedia](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps) PowerShell cmdlet 启用这些选项。  

6. 在“独立 CD/DVD”  页上，选择用于部署 OS 的任务序列。 还可以仅选择那些与启动映像关联的任务序列。 验证任务序列引用的内容的列表。  

    - **检测关联的应用程序依赖项并将其添加到此媒体**：同时还将内容添加到应用程序依赖项的媒体中。  

        > [!TIP]  
        > 如果看不到预期的应用程序依赖项，请取消选择并重新选择此选项以刷新列表。  

7. 在“选择应用程序”  页上，指定要作为媒体文件的一部分包含的其他应用程序内容。  

8. 在“选择包”  页上，指定要作为媒体文件的一部分包含的其他包内容。  

9. 在“选择驱动程序包”  页上，指定要作为媒体文件的一部分包含的其他驱动程序包内容。  

10. 在“分发点”  页上，指定包含所需内容的分发点。  

    Configuration Manager 仅显示具有内容的分发点。 先将与任务序列相关联的所有内容分发到至少一个分发点上，然后再继续操作。 在分发内容后，刷新分发点列表。 删除此页中已选中的任何分发点，然后返回到“分发点”  页。 或者，重启该向导。 有关详细信息，请参阅[分发任务序列引用的内容](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DistributeTS)和[管理内容和内容基础结构](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)  

11. 在“自定义”  页上，指定以下选项：  

    - 添加用于任务序列的任何变量。  

    - **启用预启动命令**：指定想要在运行任务序列之前运行的任何预启动命令。 预启动命令是一个脚本或可执行文件，它可以在任务序列运行之前在 Windows PE 中与用户交互。 有关详细信息，请参阅[任务序列媒体的预启动命令](/sccm/osd/understand/prestart-commands-for-task-sequence-media)。  

        > [!TIP]  
        > 在媒体创建过程中，任务序列会将包 ID 和预启动命令行（包括任何任务序列变量的值）写入到运行 Configuration Manager 控制台的计算机上的 CreateTSMedia.log  文件。 你可以查看此日志文件以验证任务序列变量的值。  

        如果预启动命令需要任何内容，请选择“包括预启动命令的文件”  选项。  

12. 完成向导。  

在目标文件夹中创建独立媒体文件 (.ISO)。 如果选择了“CD/DVD 集”  ，则将输出文件复制到一组 CD 或 DVD。


## <a name="next-steps"></a>后续步骤

[使用独立媒体部署 Windows，而不使用网络](/sccm/osd/deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network)
