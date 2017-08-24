---
title: "创建可启动介质 - Configuration Manager | Microsoft Docs"
description: "Configuration Manager 中的可启动媒体有助于更轻松地安装新版本的 Windows 或替换计算机和传输设置。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 9032698fa12bf453041ea06bf330d3b4687c2a97
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-bootable-media-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建可启动媒体

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的可启动媒体包含启动映像、可选的预启动命令和关联的文件，以及 Configuration Manager 文件。 为以下操作系统部署方案使用预留媒体：  

-   [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)  

-   [替换现有计算机和传输设置](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_CreateBootableMedia"></a> 创建可启动媒体  
 当你启动至可启动媒体时，目标计算机会启动、连接到网络，并从网络中检索指定任务序列、操作系统映像和任何其他必需的内容。 由于任务序列不在媒体上，因此，你无需重新创建媒体就能更改任务序列或内容。 可启动媒体上的包并未加密。 必须采取适当的安全措施（例如向媒体添加密码），以确保未经授权的用户不能访问包内容。  

 在使用“创建任务序列媒体向导”创建可启动媒体之前，请确保满足以下所有条件：  

|任务|描述|  
|----------|-----------------|  
|启动映像|请考虑以下将用于在任务序列中部署操作系统的启动映像的相关事项：<br /><br /> -   启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。<br />-   确保启动映像包含预配目标计算机所需的网络和大容量存储驱动程序。|  
|创建用于部署操作系统的任务序列|作为可启动媒体的一部分，必须指定用于部署操作系统的任务序列。 有关创建新任务序列的步骤，请参阅 [Create a task sequence to install an operating system](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)（创建用于安装操作系统的任务序列）。|  
|分发与任务序列关联的所有内容|必须将任务序列所需的所有内容至少分发到一个分发点。 这包括启动映像和其他相关联的预启动文件。 向导在创建可启动媒体时从分发点中收集信息。 必须具有对该分发点上的内容库的 **读取** 访问权限。  有关详细信息，请参阅[关于内容库](../../core/plan-design/hierarchy/the-content-library.md)。|  
|准备可移动的 USB 驱动器|对于可移动的 USB 驱动器：<br /><br /> 如果你要使用可移动的 USB 驱动器，该 USB 驱动器必须连接到运行向导的计算机，并且 USB 驱动器必须可被 Windows 检测为可移动设备。 向导将在创建媒体时直接写入 USB 驱动器。 独立媒体使用 FAT32 文件系统。 如果独立媒体的内容包含超过 4 GB 大小的文件，则无法在 USB 闪存驱动器上创建独立媒体。|  
|创建一个输出文件夹|对于 CD/DVD 集：<br /><br /> 在运行创建任务序列媒体向导以便为 CD 或 DVD 集创建媒体之前，你必须为向导创建的输出文件创建一个文件夹。 为 CD 或 DVD 集创建的媒体将以 .iso 文件形式直接写入该文件夹。|  

 使用以下过程来创建可启动媒体。  

### <a name="to-create-bootable-media"></a>创建可启动媒体  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”工作区中，展开“操作系统”，然后单击“任务序列”。  

3.  在“主页”选项卡上的“创建”组中，单击“创建任务序列媒体”，以启动创建任务序列媒体向导。  

4.  在“选择媒体类型”  页上，指定以下选项，然后单击“下一步” 。  

    -   选择“可启动媒体” 。  

    -   （可选）如果你希望仅允许部署操作系统而不需要用户输入，请选择“允许无人参与的操作系统部署” 。  

        > [!IMPORTANT]  
        >  如果选择此选项，则不会提示用户输入网络配置信息或可选的任务序列。 但是，如果针对密码保护配置了媒体，则仍会提示用户输入密码。  

5.  在“媒体管理”  页上，指定以下选项之一，然后单击“下一步” 。  

    -   如果要允许管理点根据客户端在站点边界中的位置将媒体重定向到另一个管理点，请选择“动态媒体”  。  

    -   如果希望媒体仅与指定的管理点联系，请选择“基于站点的媒体”  。  

6.  在“媒体类型”  页上，指定媒体是闪存驱动器还是 CD/DVD 集，然后单击进行以下配置：  

    > [!IMPORTANT]  
    >  独立媒体使用 FAT32 文件系统。 如果独立媒体的内容包含超过 4 GB 大小的文件，则无法在 USB 闪存驱动器上创建独立媒体。  

    -   如果选择“USB 闪存驱动器”，则指定要在其中存储内容的驱动器。  

    -   如果选择“CD/DVD 集”，请指定媒体的容量以及输出文件的名称和路径。 向导会将输出文件写入到此位置。 例如：**\\\servername\folder\outputfile.iso**  

         如果媒体的容量太小，无法存储整个内容，则会创建多个文件，从而必须将内容存储在多张 CD 或 DVD 上。 当需要多个媒体时，Configuration Manager 会在创建的每个输出文件的名称中添加序号。 此外，如果将应用程序与操作系统一起部署，而单个媒体无法容纳应用程序，则 Configuration Manager 会将应用程序存储到多个媒体中。 在运行独立媒体时，Configuration Manager 会提示用户提供下一个存储了应用程序的媒体。  

        > [!IMPORTANT]  
        >  如果选择现有的 .iso 映像，任务序列媒体向导将在你进入向导的下一页后立即从驱动器或共享中删除该映像。 即使随后取消该向导，也会删除这个现有的映像。  

     单击“下一步” 。  

7.  在“安全”  页上，指定以下选项，然后单击“下一步” 。  

    -   选中“启用未知计算机支持”复选框，使媒体能够将操作系统部署到不是由 Configuration Manager 托管的计算机。 Configuration Manager 数据库中没有这些计算机的记录。  

         未知计算机包括下列各项：  

        -   未安装 Configuration Manager 客户端的计算机  

        -   未导入到 Configuration Manager 中的计算机  

        -   未被 Configuration Manager 发现的计算机  

    -   选中“使用密码保护媒体”  复选框，并输入强密码来帮助防止未经授权访问媒体。 如果指定密码，则用户必须提供该密码才能使用可启动媒体。  

        > [!IMPORTANT]  
        >  作为最佳安全方案，请始终分配密码来帮助保护可启动媒体。  

    -   对于 HTTP 通信，选择“创建自签名媒体证书” ，然后指定该证书的开始日期和到期日期。  

    -   对于 HTTPS 通信，选择“导入 PKI 证书” ，然后指定要导入的证书及其密码。  

         有关用于启动映像的此客户端证书的详细信息，请参阅 [PKI 证书要求](../../core/plan-design/network/pki-certificate-requirements.md)。  

    -   **用户设备相关性**：若要在 Configuration Manager 中支持以用户为中心的管理，请指定希望媒体如何将用户与目标计算机相关联。 有关操作系统部署如何支持用户设备相关性的详细信息，请参阅[如何将用户与目标计算机相关联](../get-started/associate-users-with-a-destination-computer.md)。  

        -   如果你希望媒体自动将用户与目标计算机关联，请指定“通过自动批准允许用户设备相关性”  。 此功能以部署操作系统的任务序列的操作为基础。 在此方案中，当任务序列将操作系统部署到目标计算机时，它会在指定的用户和目标计算机之间创建关系。  

        -   如果希望媒体获得批准后将用户与目标计算机关联，请指定“允许用户设备相关性挂起管理员批准”  。 此功能以部署操作系统的任务序列的作用域为基础。  在此方案中，任务序列在指定用户和目标计算机之间创建关系，但在部署操作系统之前等待管理用户的批准。  

        -   如果不希望媒体将用户与目标计算机关联，请指定“不允许用户设备相关性”  。 在此方案中，当任务序列部署操作系统时，它不会将用户与目标计算机关联。  

8.  在“启动映像包”  页上，指定以下选项，然后单击“下一步” 。  

    > [!IMPORTANT]  
    >  分发的启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。  

    -   在“启动映像包”  框中，指定用于启动目标计算机的启动映像。  

    -   在“分发点”  框中，指定启动映像所在的分发点。 向导将从分发点中检索启动映像并将其写入媒体。  

        > [!NOTE]  
        >  必须具有对分发点上的内容库的“读取”  访问权限。  

    -   如果在向导的“媒体管理”  页上创建基于站点的可启动媒体，请从“管理点”  框中的主站点指定管理点。  

    -   如果在向导的“媒体管理”  页上创建动态可启动媒体，请在“关联的管理点” 中指定要使用的主站点管理点以及初始通信的优先级顺序。  

9. 在“自定义”  页上，指定以下选项，然后单击“下一步” 。  

    -   指定任务序列用于部署操作系统的变量。  

    -   指定想要在运行任务序列之前运行的任何预启动命令。 预启动命令是一个脚本或可执行文件，它可以在任务序列运行以安装操作系统之前在 Windows PE 中与用户交互。 有关详细信息，请参阅[任务序列媒体的预启动命令](../understand/prestart-commands-for-task-sequence-media.md)。  

        > [!TIP]  
        >  在任务序列媒体创建过程中，任务序列会将包 ID 和预启动命令行（包括任何任务序列变量的值）写入到运行 Configuration Manager 控制台的计算机上的 CreateTSMedia.log 日志文件。 你可以查看此日志文件以验证任务序列变量的值。  

         根据需要选中“包括预启动命令的文件”  复选框，以包括预启动命令所需的任何文件。  

10. 完成向导。  

## <a name="create-bootable-media-on-a-usb-drive-from-a-network-share"></a>在 USB 驱动器上从网络共享创建可启动媒体
当闪存驱动器未连接到运行 Configuration Manager 控制台的计算机时，可借助此部分信息在闪存驱动器上创建可启动媒体。 若要在 USB 驱动器上创建可启动媒体，可创建任务序列启动媒体、装载 ISO 并将文件从 ISO 传输到 USB 驱动器。

1. [创建任务序列启动媒体](#to-create-task-boobable-media)。 在“媒体类型”页上，选择“CD/DVD 集”。 向导会将输出文件写入到指定位置。 例如：**\\\servername\folder\outputfile.iso**。  
2. 准备可移动的 USB 驱动器。 该驱动器必须经过格式化处理并且为可启动的空驱动器。
3. 从共享位置装载 ISO，并将文件从 ISO 传输到 USB 驱动器。

## <a name="next-steps"></a>后续步骤  
[使用可启动媒体通过网络部署 Windows](use-bootable-media-to-deploy-windows-over-the-network.md)  
