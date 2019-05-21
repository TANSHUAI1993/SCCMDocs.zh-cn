---
title: 创建可启动媒体
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的可启动媒体安装新版本的 Windows 或替换计算机。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b7a68dd6d0bdbc2fa043d552aba13562dc175fc
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082950"
---
# <a name="create-bootable-media"></a>创建可启动媒体

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的可启动媒体包含启动映像、可选的预启动命令和关联的文件，以及 Configuration Manager 文件。 为以下 OS 部署方案使用预留媒体：  

- [在新计算机（裸机）上安装新版的 Windows](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

- [替换现有计算机和传输设置](/sccm/osd/deploy-use/replace-an-existing-computer-and-transfer-settings)  


## <a name="usage"></a>用法

启动到可启动媒体时，会出现以下过程：

1. 目标计算机启动
1. 连接到网络
1. 从站点中检索以下内容：
    - 指定的任务序列
    - OS 映像
    - 任何其他所需的内容

由于任务序列不在媒体上，因此，无需重新创建媒体就能更改任务序列或内容。

可启动媒体上的包并未加密。 若要确保未经授权的用户不能访问包内容，请采取适当的安全措施。 例如，向媒体添加密码。

## <a name="prerequisites"></a>先决条件

在使用“创建任务序列媒体向导”创建可启动媒体之前，请确保满足所有条件。

### <a name="boot-image"></a>启动映像

在任务序列中使用启动映像部署 OS 时，请考虑以下注意事项：

- 启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。
- 确保启动映像包含预配目标计算机所需的网络和存储驱动程序。

### <a name="create-a-task-sequence-to-deploy-an-os"></a>创建用于部署 OS 的任务序列

作为可启动媒体的一部分，请指定用于部署 OS 的任务序列。 有关详细信息，请参阅[创建用于安装 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system)。

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>分发与任务序列关联的所有内容

将任务序列所需的所有内容至少分发到一个分发点。 此内容包括启动映像和其他相关联的预启动文件。 向导在创建可启动媒体时从分发点中收集内容。

用户帐户至少需要具有对该分发点上的内容库的读取访问权限。 有关详细信息，请参阅[分发内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)。

### <a name="prepare-the-removable-usb-drive"></a>准备可移动的 USB 驱动器

如果使用的是可移动 USB 驱动器，则将其连接到运行“创建任务序列媒体向导”的计算机。 USB 驱动器必须可被 Windows 检测为可移动设备。 向导将在创建媒体时直接写入 USB 驱动器。

### <a name="create-an-output-folder"></a>创建一个输出文件夹

在运行“创建任务序列媒体向导”以便为 CD 或 DVD 集创建媒体之前，为向导创建的输出文件创建一个文件夹。 为 CD 或 DVD 集创建的媒体将以 .ISO 文件形式直接写入该文件夹。


## <a name="process"></a>过程

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，选择“任务序列”节点。  

2. 在功能区的“主页”选项卡上，在“创建”组中，选择“创建任务序列媒体”。 此操作会启动“创建任务序列媒体向导”。  

3. 在“选择媒体类型”页上，指定以下选项：  

    - 选择“可启动媒体” 。  

    - （可选）如果你希望仅允许部署 OS 而不需要用户输入，请选择“允许无人参与的操作系统部署”。  

        > [!IMPORTANT]  
        > 如果选择此选项，则不会提示用户输入网络配置信息或可选的任务序列。 如果针对密码保护配置媒体，则仍会提示用户输入密码。  

4. 在“媒体管理”页上，指定以下选项之一：  

    - **动态媒体**：允许管理点根据客户端在站点边界中的位置将媒体重定向到另一个管理点。  

    - **基于站点的媒体**：媒体仅与指定的管理点联系。  

5. 在“媒体类型”页上，指定媒体是“可移动 USB 驱动器”还是“CD/DVD 集”。 然后配置以下选项：  

    > [!IMPORTANT]  
    > 媒体使用 FAT32 文件系统。 如果媒体的内容包含超过 4 GB 大小的文件，则无法在 USB 驱动器上创建媒体。  

    - 如果选择“可移动 USB 驱动器”，则选择要在其中存储内容的驱动器。  

        - **格式化可移动 U 盘 (FAT32) 并使其可启动**：默认情况下，让 Configuration Manager 准备 U 盘。 很多较新的 UEFI 设备都需要可启动的 FAT32 分区。 但是，此格式还限制文件的大小和驱动器的总容量。 如果已格式化并配置了可移动驱动器，请禁用此选项。

    - 如果选择“CD/DVD 集”，请指定媒体的容量（媒体大小）以及输出文件（媒体文件）的名称和路径。 向导会将输出文件写入到此位置。 例如：`\\servername\folder\outputfile.iso`  

        如果媒体的容量太小，无法存储整个内容，则会创建多个文件。 然后必须将内容存储在多张 CD 或 DVD 上。 如果需要多个媒体文件，Configuration Manager 会在创建的每个输出文件的名称中添加序号。  

        > [!IMPORTANT]  
        > 如果选择现有的 .iso 映像，任务序列媒体向导将在你进入向导的下一页后立即从驱动器或共享中删除该映像。 即使随后取消该向导，也会删除这个现有的映像。  

    - **暂存文件夹**<!--1359388-->：媒体创建过程可能需要大量临时驱动器空间。 默认情况下，此位置类似于以下路径：`%UserProfile%\AppData\Local\Temp`。 从版本 1902 开始，若要更灵活地选择存储这些临时文件的位置，请将此值更改为其他驱动器和路径。  

    - **媒体标签**<!--1359388-->：从版本 1902 开始，向任务序列媒体添加标签。 此标签可帮助你在创建媒体后更好地识别媒体。 默认值为 `Configuration Manager`。 此文本字段显示在以下位置：  

        - 如果安装 ISO 文件，Windows 会将此标签显示为已安装驱动器的名称  

        - 如果格式化 U 盘，它将使用标签的前 11 个字符作为其名称  

        - Configuration Manager 将名为 `MediaLabel.txt` 的文本文件写入媒体的根目录。 默认情况下，该文件包含一行文本：`label=Configuration Manager`。 如果自定义媒体标签，则此行使用你的自定义标签而不是默认值。  

    - **在媒体上加入 autorun.inf 文件**<!-- 4090666 -->：从版本 1902 开始，默认情况下，Configuration Manager 不会添加 autorun.inf 文件。 反恶意软件通常会阻止此文件。 有关 Windows 的 AutoRun 功能的详细信息，请参阅 [Creating an AutoRun-enabled CD-ROM Application](https://docs.microsoft.com/windows/desktop/shell/autoplay)（创建启用 AutoRun 的 CD-ROM 应用程序）。 如果情况仍然需要，请选择此选项以加入该文件。  

6. 在“安全”页上，指定以下选项：  

    - **启用未知计算机支持**：允许媒体将 OS 部署到不是由 Configuration Manager 托管的计算机上。 Configuration Manager 数据库中没有这些计算机的记录。 有关详细信息，请参阅[准备未知计算机部署](/sccm/osd/get-started/prepare-for-unknown-computer-deployments)。  

    - **使用密码保护媒体**：输入强密码来帮助防止未经授权访问媒体。 如果指定密码，则用户必须提供该密码才能使用可启动媒体。  

        > [!IMPORTANT]  
        > 作为最佳安全方案，请始终分配密码来帮助保护可启动媒体。  

    - 对于 HTTP 通信，选择“创建自签名媒体证书”。 然后指定证书的开始日期和到期日期。  

    - 对于 HTTPS 通信，选择“导入 PKI 证书”。 然后指定要导入的证书及其密码。  

        有关用于启动映像的此客户端证书的详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

    - **用户设备相关性**：若要在 Configuration Manager 中支持以用户为中心的管理，请指定希望媒体如何将用户与目标计算机相关联。 有关 OS 部署如何支持用户设备相关性的详细信息，请参阅[如何将用户与目标计算机相关联](/sccm/osd/get-started/associate-users-with-a-destination-computer)。  

        - **通过自动批准允许用户设备相关性**：媒体自动将用户与目标计算机关联。 此功能以部署 OS 的任务序列的操作为基础。 在此方案中，当任务序列将 OS 部署到目标计算机时，它会在指定的用户和目标计算机之间创建关系。  

        - **允许用户设备相关性挂起管理员批准**：媒体在获得批准后将用户与目标计算机关联。 此功能以部署 OS 的任务序列的作用域为基础。 在此方案中，任务序列在指定用户和目标计算机之间创建关系，但在部署 OS 之前等待管理用户的批准。  

        - **不允许用户设备相关性**：媒体不将用户与目标计算机关联。 在此方案中，当任务序列部署 OS 时，它不会将用户与目标计算机关联。  

7. 在“启动映像”页上，指定以下选项：  

    > [!IMPORTANT]  
    > 分发的启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。  

    - **启动映像**：选择用于启动目标计算机的启动映像。  

    - **分发点**：选择具有启动映像的分发点。 向导将从分发点中检索启动映像并将其写入媒体。  

        > [!NOTE]  
        > 用户帐户至少需要具有对该分发点上的内容库的读取权限。  

    - **管理点**：仅针对基于站点的媒体，从主站点中选择管理点。  

    - **关联的管理点**：仅针对动态媒体，选择要使用的主站点管理点以及初始通信的优先级顺序。  

8. 在“自定义”页上，指定以下选项：  

    - 添加用于任务序列的任何变量。  

    - **启用预启动命令**：指定想要在运行任务序列之前运行的任何预启动命令。 预启动命令是一个脚本或可执行文件，它可以在任务序列运行之前在 Windows PE 中与用户交互。 有关详细信息，请参阅[任务序列媒体的预启动命令](/sccm/osd/understand/prestart-commands-for-task-sequence-media)。  

        > [!TIP]  
        > 在媒体创建过程中，任务序列会将包 ID 和预启动命令行（包括任何任务序列变量的值）写入到运行 Configuration Manager 控制台的计算机上的 CreateTSMedia.log 文件。 你可以查看此日志文件以验证任务序列变量的值。  

        如果预启动命令需要任何内容，请选择“包括预启动命令的文件”选项。  

9. 完成向导。  


## <a name="alternate-method"></a>替代方法

当驱动器未连接到运行 Configuration Manager 控制台的计算机时，可以在可移动 USB 驱动器上创建可启动媒体。

1. [创建任务序列启动媒体](#process)。 在“媒体类型”页上，选择“CD/DVD 集”。 向导会将输出文件写入到指定位置。 例如： `\\servername\folder\outputfile.iso`。  

2. 准备可移动的 USB 驱动器。 该驱动器必须经过格式化处理并且为可启动的空驱动器。

3. 从共享位置装载 ISO，并将文件从 ISO 传输到 USB 驱动器。


## <a name="next-steps"></a>后续步骤

[使用可启动媒体通过网络部署 Windows](/sccm/osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network)  
