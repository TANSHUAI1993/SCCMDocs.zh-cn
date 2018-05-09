---
title: '管理启动映像 '
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中，了解如何管理在操作系统部署过程中使用的 Windows PE 启动映像。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a2fe20896a781d7c897bd5a827d25a7b70390b7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理启动映像

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的一个启动映像是在操作系统部署过程中使用的 [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) 映像。 启动映像用于在 WinPE 中启动计算机。 此最小操作系统包含有限的组件和服务。 Configuration Manager 使用 WinPE 准备用于安装 Windows 的目标计算机。 使用下列部分来管理启动映像。

## <a name="BKMK_BootImageDefault"></a>默认启动映像
Configuration Manager 提供两个默认启动映像：一个用于支持 x86 平台，另一个用于支持 x64 平台。 这些映像存储在以下路径中：\\\\*servername*>\SMS_<*sitecode*>\osd\boot\\<*x64*> or <*i386*>。 将根据所采用的操作更新或重新生成默认启动映像。

针对所描述的默认启动映像的任何操作，请考虑下列行为：
- 源驱动程序对象必须有效。 这些对象包括驱动程序源文件。 如果对象无效，站点不会将驱动程序添加到启动映像。
- 不会修改不基于默认启动映像的启动映像（即使使用相同的 Windows PE 版本）。
- 将已修改的启动映像重新分发到分发点。
- 重新创建要使用修改后的启动映像的媒体。
- 如果不希望自动更新自定义/默认启动映像，请勿将它们存储在默认位置。

> [!NOTE]
> 向“软件库”中的所有启动映像添加了 Configuration Manager 跟踪日志工具 (CMTrace)。 位于 Windows PE 中时，通过在命令提示符处键入 CMTrace 来启动该工具。 从版本 1802 开始，在 Windows PE 中启动 cmtrace.exe 时不再提示选择是否将此程序设置为日志文件的默认查看器。

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>使用更新和服务来安装最新版本的 Configuration Manager
从版本 1702 开始，如果升级 Windows 评估和部署工具包 (ADK) 版本，然后使用更新和服务安装 Configuration Manager 的最新版本，站点将重新生成默认启动映像。 此项更新包括已更新的 Windows ADK 中的新 WinPE 版本、新版本的 Configuration Manager 客户端、驱动程序以及自定义项。 站点不会修改自定义启动映像。

在版本 1702 之前，Configuration Manager 会使用客户端组件、驱动程序以及自定义项更新现有启动映像，但不会使用 Windows ADK 中的最新版本 WinPE。 手动修改启动映像才能使用 Windows ADK 的最新版本。

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>从 Configuration Manager 2012 升级到 Configuration Manager Current Branch (CB)
通过使用安装过程从 Configuration Manager 2012 升级到 Configuration Manager CB 时，站点将重新生成默认启动映像。 此项更新包括已更新的 Windows ADK 中的新 WinPE 版本以及新版本的 Configuration Manager 客户端。 所有启动映像的自定义项保持不变。 站点不会修改自定义启动映像。

### <a name="update-distribution-points-with-the-boot-image"></a>利用启动映像更新分发点
从控制台中的“启动映像”节点使用“更新分发点”操作时，站点使用客户端组件、驱动程序以及自定义项更新目标启动映像。    

从 Configuration Manager 版本 1706 开始，使用 Windows ADK 安装目录中最新版本的 WinPE 重载启动映像。 更新分发点向导的常规页面提供下列信息： 
 - 站点服务器上安装的 Windows ADK 版本
 - 启动映像中的 WinPE 的 Windows ADK 版本
 - Configuration Manager 客户端的版本使用此信息帮助决定是否要重载启动映像。 启动映像节点还包括新的一列（客户端版本）。 使用此列可以快速查看每个启动映像中的 Configuration Manager 客户端版本。    


##  <a name="BKMK_BootImageCustom"></a>自定义启动映像  
 如果启动映像基于支持的 Windows ADK 版本中的 WinPE 版本，可以从控制台自定义启动映像或[修改启动映像](#BKMK_ModifyBootImages)。 使用新版本升级站点并且安装新版本的 Windows ADK 时，不会使用新版本的 Windows ADK 更新自定义启动映像（不在默认启动映像位置）。 发生这种情况时，无法在 Configuration Manager 控制台中自定义启动映像。 但是，它们会继续如同升级之前一样正常运行。  

 如果启动映像基于站点上安装的另一个 Windows ADK 版本，则必须自定义启动映像。 使用另一种方法来自定义这些启动映像，例如使用部署映像服务以及管理 (DISM) 命令行工具。 DISM 是 Windows ADK 的一部分。 有关详细信息，请参阅[自定义启动映像](customize-boot-images.md)。  

##  <a name="BKMK_AddBootImages"></a>添加启动映像  

 在站点安装过程中，Configuration Manager 会自动添加 Windows ADK 支持版本中基于 WinPE 版本的启动映像。 根据 Configuration Manager 的版本，你能够添加 Windows ADK 支持版本中基于不同 WinPE 版本的启动映像。 如果尝试添加包含不受支持的 WinPE 版本的启动映像，则会发生错误。 以下列表中是当前支持的 Windows ADK 和 WinPE 版本： 

-   **Windows ADK 版本**  

     适用于 Windows 10 的 Windows ADK  

-   **可从 Configuration Manager 控制台中自定义的启动映像的 Windows PE 版本**  

     Windows PE 10  

-   **不可从 Configuration Manager 控制台中自定义的启动映像的 Windows PE 支持版本**  

     Windows PE 3.1<sup>1</sup> 和 Windows PE 5  

     <sup>1</sup> 只有当启动映像基于 Windows PE 3.1 时才能将该映像添加到 Configuration Manager 中。 使用适用于 Windows 7 SP1（基于 Windows PE 3.1）的 Windows AIK 补充来升级适用于 Windows 7（基于 Windows PE 3.0）的 Windows AIK。 从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=5188)下载适用于 Windows 7 SP1 的 Windows AIK 补充程序。  

     例如，利用 Configuration Manager 控制台通过适用于 Windows 10 的 Windows ADK 自定义基于 Windows PE 10 的启动映像。 对于基于 Windows PE 5 的启动映像，请使用适用于 Windows 8 的 Windows ADK 中的 DISM 版本从另一台计算机对其进行自定义。 然后向 Configuration Manager 控制台添加自定义启动映像。 有关详细信息，请参阅[自定义启动映像](customize-boot-images.md)。

 使用下列过程来手动添加启动映像。  

#### <a name="to-add-a-boot-image"></a>添加启动映像  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“添加启动映像包”  以启动添加启动映像包向导。  

4.  在“数据源”  页上，指定以下选项，然后单击“下一步” 。  

    -   在“路径”  框中，指定启动映像 WIM 文件的路径。  

         指定的路径必须是 UNC 格式的有效网络路径。 例如：\\\\<*servername*\\<*sharename*>\\<*bootimagename*>.wim。  

    -   从“启动映像”  下拉列表中选择启动映像。 如果 WIM 文件包含多个启动映像，则选择正确的映像。  

5.  在“常规”   页上，指定以下选项，然后单击“下一步” 。  

    -   在“名称”  框中，为启动映像指定唯一名称。  

    -   在“版本”  框中，为启动映像指定版本号。  

    -   在“备注”  框中，指定有关启动映像使用方式的简要描述。  

6.  完成向导。  

 启动映像现在列出在 Configuration Manager 控制台的“启动映像”节点中。 在使用启动映像部署操作系统之前，请将启动映像分发到分发点。 

> [!NOTE]  
>  在控制台的“启动映像”节点中，“大小(KB)”列会显示每个启动映像的解压缩大小。 当站点通过网络发送启动映像时，它会发送压缩副本。 此副本通常小于“大小(KB)”列中列出的大小。  

##  <a name="BKMK_DistributeBootImages"></a>将启动映像分发到分发点  
 将采用与分发其他内容相同的方式将启动映像分发到分发点。 大多数情况下，部署操作系统并创建媒体之前，必须将启动映像分发到至少一个分发点。   

> [!NOTE]  
> 若要使用 PXE 来部署操作系统，请在分发启动映像之前考虑以下几点：  
> - 配置分发点以接受 PXE 请求。  
> - 将启用 x86 和 x64 PXE 的启动映像分发到至少一个启用 PXE 的分发点。  
> - Configuration Manager 会将启动映像分发到启用 PXE 的分发点上的 **RemoteInstall** 文件夹。  
>   
> 有关使用 PXE 部署操作系统的详细信息，请参阅[使用 PXE 通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

 关于分发启动映像的步骤，请参阅 [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)。  

##  <a name="BKMK_ModifyBootImages"></a>修改启动映像  
 你可在映像中添加或删除设备驱动程序，或编辑与启动映像关联的属性。 你可添加或删除的设备驱动程序包括网络适配器或大容量存储设备驱动程序。 在修改启动映像时，请考虑以下因素：  

-   在将设备驱动程序添加到启动映像之前，将这些驱动程序导入驱动程序目录并启用它们。  

-   在修改启动映像时，启动映像不会更改启动映像所引用的任何关联的包。  

-   对启动映像进行更改后，在已有该启动映像的分发点上更新它。 此过程让客户端可以使用该启动映像的最新版本。 有关详细信息，请参阅 [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage)。  

 使用下列过程来修改启动映像。  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>修改启动映像的属性  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

3.  选择要修改的启动映像。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性”  打开启动映像的“属性”  对话框。  

5.  选择下列任何设置以更改启动映像的行为：  

    -   在“映像”  选项卡上，如果使用外部工具更改了启动映像的属性，请单击“重新加载” 。  

    -   在“驱动程序”  选项卡上，添加启动 WinPE 所需的 Windows 设备驱动程序。 在添加设备驱动程序时，请考虑以下几点：  

        -   选择“隐藏与启动映像体系结构不匹配的驱动程序”以仅显示适用于启动映像体系结构的驱动程序。 该体系结构以制造商提供的 .INF 中所报告的体系结构为基础。  

        -   选择“隐藏不位于（用于启动映像的）存储或网络类中的驱动程序”，可只显示存储和网络驱动程序。 此选项还会隐藏启动映像通常不需要的其他驱动程序，例如视频或调制解调器驱动程序。  

        -   选中“隐藏未进行数字签名的驱动程序”以隐藏不具备有效数字签名的驱动程序。  

        -   作为最佳方案，除非 WinPE 需要其他驱动程序，否则请仅向启动映像添加网络和批量存储驱动程序。  

        -   由于 WinPE 已经附带了许多内置驱动程序，因此请仅添加 WinPE 未提供的网络和批量存储驱动程序。  

        -   确保添加到启动映像的驱动程序与启动映像的体系结构相匹配。  

        > [!NOTE]  
        >  在将设备驱动程序添加到启动映像之前，你必须将这些驱动程序导入驱动程序目录。 有关如何导入设备驱动程序的信息，请参阅[管理驱动程序](manage-drivers.md)。  

    -   在“自定义”  选项卡上，选择下列任意设置：  

        -   选中“启用预启动命令”  复选框以指定在运行任务序列之前运行的命令。 启动此选项时，还指定要运行的命令行以及该命令需要的任何支持文件。  

            > [!WARNING]  
            >  将 cmd /c 添加到命令行的开头。 如果未指定 cmd /c，则命令在运行之后不会关闭。 部署会继续等待命令完成，不会启动任何其他配置的命令或操作。  

            > [!TIP]  
            >  在任务序列媒体创建过程中，该向导会将包 ID 和预启动命令行（包括任何任务序列变量的值）写入到 CreateTSMedia.log 日志文件。 此日志位于运行 Configuration Manager 控制台的计算机上。 查看此日志文件以验证任务序列变量的值。  

        -   设置“Windows PE 背景”  设置以指定是要使用默认 WinPE 背景还是自定义背景。  

        -   选中“启用命令支持（仅限测试）”  ，以便在部署启动映像时通过使用“F8”  键来打开命令提示符。 在测试部署时，此选项对于故障排除非常有用。 不建议在生产部署中使用此设置。  

        -   配置 Windows PE 暂存空间，该空间是 WinPE 使用的临时存储（RAM 驱动器）。 例如，当应用程序在 WinPE 内运行并且需要写入临时文件时，WinPE 会将文件重定向到内存中的暂存空间以模拟硬盘的存在。 默认情况下，WinPE 分配 32 MB 的可写内存。  

    -   在“数据源”  选项卡上，更新下列任意设置：  

        -   设置“映像路径”和“映像索引”以更改启动映像的源文件。  

        -   选中“按计划更新分发点”以针对何时更新启动映像创建计划。  

        -   如果不希望此包的内容从客户端缓存中脱离以为其他内容腾出空间，请选中“保留客户端缓存中的内容”。  

        -   若要指定站点在更新分发点上的启动映像包时只分发更改的文件，请选中“启用二进制差异复制”(BDR)。 此设置能最大程度地减少站点之间的网络流量。 在启动映像包较大且更改相对较小时，BDR 会特别有用。  

        -   如果将启动映像用于启用 PXE 的部署中，请选择“从启用 PXE 的分发点部署此启动映像”。  

            > [!NOTE]  
            >  有关详细信息，请参阅[使用 PXE 通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

    -   在“数据访问”  选项卡上，选择下列任意设置：  

        -   如果希望客户端从网络中安装此包中的内容，请选择“包共享设置”  。  

        -   设置“包更新设置”以指定希望 Configuration Manager 如何断开用户和分发点的连接。 当用户连接到分发点时，Configuration Manager 可能无法更新启动映像。  

    -   在“分发设置”  选项卡上，选择下列任意设置：  

        -   在“分发优先级”列表中指定优先级别。 当站点将多个包分发至同一个分发点时，Configuration Manager 使用此优先级列表。  

        -   如果要启用针对首选分发点的按需内容分发，请选择“将此包的内容分发到首选分发点”。 如果启用此设置，则管理点会在客户端请求包内容并且内容在任何首选分发点上都不可用时将内容分发到所有首选分发点。  

        -   设置“预留分发点设置”以指定要如何将启动映像分发到为预留内容启用的分发点。  

            > [!NOTE]  
            >  有关预留内容的详细信息，请参阅 [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage)。  

    -   在“内容位置”  选项卡上，选择分发点或分发点组以执行下列任何操作：  

        -   单击“重新分发”  以将启动映像再次分发到所选分发点或分发点组。  

        -   单击“验证”  以检查所选分发点或分发点组上的启动映像包的完整性。  

    -   在“可选组件”选项卡上，指定要添加到 Windows PE 上以便与 Configuration Manager 一起使用的组件。 有关可用的可选组件的详细信息，请参阅 [WinPE: Add packages (Optional Components Reference)（WinPE：添加包（可选组件参考））](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference)。  

    -   在“安全”  选项卡上，选择管理用户并更改他们可执行的操作。  

6.  配置了属性后，单击“确定” 。  

##  <a name="BKMK_BootImagePXE"></a>配置一个启动映像以从启用 PXE 的分发点部署  
 在为 PXE 操作系统部署使用启动映像之前，必须将启动映像配置为从启用 PXE 的分发点部署。  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>若要配置一个启动映像以从启用 PXE 的分发点部署  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

3.  选择要修改的启动映像。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性”  打开启动映像的“属性”  对话框。  

5.  在“数据源”  选项卡上选择“从启用 PXE 的分发点部署此启动映像” 。  

    > [!NOTE]  
    >  有关详细信息，请参阅[使用 PXE 通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

6.  配置了属性后，单击“确定” 。  

##  <a name="BKMK_BootImageLanguage"></a>为启动映像部署配置多种语言  
 语言中性的启动映像。 此功能允许在 WinPE 中使用单个启动映像以多种语言显示任务序列文本。 包括启动映像“可选组件”选项卡中适用的语言支持。然后设置合适的任务序列变量以指示要显示的语种。 已部署的操作系统的语言独立于 WinPE 中的语言。 WinPE 向用户显示的语言根据下列说明来确定：  

-   在用户从现有的操作系统运行任务序列时，Configuration Manager 会自动使用为用户配置的语言。 在规定的部署截止时间导致任务序列自动运行时，Configuration Manager 会使用操作系统的语言。  

-   对于使用 PXE 或媒体的操作系统部署，请在作为预启动命令一部分的 SMSTSLanguageFolder 变量中设置语言 ID 值。 在计算机启动到 WinPE 时，会以你在此变量中指定的语言显示消息。 如果在访问指定文件夹中的语言资源文件时出错，或者未设置此变量，WinPE 则会以默认语言显示消息。  

    > [!NOTE]  
    >  如果使用密码来保护媒体，则会始终以 WinPE 的语言来显示用于提示用户输入密码的文本。  

 使用下列过程为 PXE 或媒体启动的操作系统部署设置 WinPE 的语言。  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>为 PXE 或媒体启动的操作系统部署设置 Windows PE 的语言  

1.  在更新启动映像之前，请验证合适的任务序列资源文件 (tsres.dll) 是否位于站点服务器上相应的语言文件夹中。 例如，英语资源文件位于以下位置：<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll。  

2.  将作为预启动命令一部分的 SMSTSLanguageFolder 环境变量设置为合适的语言 ID。 必须使用十进制而不是十六进制来指定语言 ID。 例如，若要将语言 ID 设置为英语，则应为文件夹名称指定十进制值 1033 而不是十六进制值 00000409。  
