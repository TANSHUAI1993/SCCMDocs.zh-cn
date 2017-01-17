---
title: "管理启动映像 | Microsoft Docs"
description: "在 Configuration Manager 中，了解如何管理在操作系统部署过程中使用的 Windows PE 启动映像。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
caps.latest.revision: 23
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 8c41c39a7f984be2612ae882d3bc08d92278dba6


---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理启动映像

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的一个启动映像是在操作系统部署过程中使用的 [Windows PE (WinPE)](https://msdn.microsoft.com/library/windows/hardware/dn938389%28v=vs.85%29.aspx) 映像。 启动映像用于在 WinPE 中启动计算机，它是用于准备在目标计算机上安装 Windows 的有限组件和服务的最精简操作系统。  使用下列部分来管理启动映像。

##  <a name="a-namebkmkbootimagedefaulta-default-boot-images"></a><a name="BKMK_BootImageDefault"></a>默认启动映像  
 Configuration Manager 提供两个默认启动映像：一个用于支持 x86 平台，另一个用于支持 x64 平台。 这些映像存储在以下路径中：\\\\*servername*>\SMS_<*sitecode*>\osd\boot\\<*x64 or i386*。  

 将 Configuration Manager 升级到新版本时，Configuration Manager 可能会将此位置中的默认启动映像以及基于默认启动映像的自定义启动映像替换为更新的文件。 更新启动映像（包括驱动程序）时，在站点上对默认启动映像配置的选项（如可选组件）会转入。 源驱动程序对象必须有效（包括驱动程序源文件），否则驱动程序不会添加到站点上的已更新启动映像。 不基于默认启动映像的其他启动映像（即使基于相同的 Windows ADK 版本）不会更新。 更新启动映像之后，需要将它们重新分发到分发点。 使用启动映像的任何媒体都需要重新创建。 如果不希望自动更新自定义默认启动映像，则应将它们存储在不同位置。  

 向已添加到“软件库”的所有启动映像中添加了 Configuration Manager 跟踪日志工具。 处于 WinPE 中时，可以通过从命令提示符键入 **CMTrace** 以启动 Configuration Manager 跟踪日志工具。  

##  <a name="a-namebkmkbootimagecustoma-customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a>自定义启动映像  
 Configuration Manager 控制台基于来自受支持的 Windows ADK 版本中的 Windows PE 版本时，可从 Configuration Manager 控制台自定义启动映像或[修改启动映像](#BKMK_ModifyBootImages)。 使用新版本升级站点并且安装新版本的 Windows ADK 时，不会使用新版本的 Windows ADK 更新自定义启动映像（不在默认启动映像位置）。 发生这种情况时，你不再能够在 Configuration Manager 控制台中自定义启动映像。 但是，它们将继续如同升级之前一样正常工作。  

 当启动映像基于站点上安装的不同版本的 Windows ADK 时，你必须使用其他方法自定义启动映像，如使用 Windows AIK 和 Windows ADK 中的部署映像服务和管理 (DISM) 命令行工具。 有关详细信息，请参阅[自定义启动映像](customize-boot-images.md)。  

##  <a name="a-namebkmkaddbootimagesa-add-a-boot-image"></a><a name="BKMK_AddBootImages"></a>添加启动映像  

 在站点安装过程中，Configuration Manager 会自动添加 Windows ADK 支持版本中基于 WinPE 版本的启动映像。 根据 Configuration Manager 的版本，你能够添加 Windows ADK 支持版本中基于不同 WinPE 版本的启动映像。  如果尝试添加包含不受支持的 WinPE 版本的启动映像，则会发生错误。  

 下面提供了受支持的 Windows ADK 版本、可在 Configuration Manager 控制台中自定义的启动映像所基于的 Windows PE 版本，以及可使用 DISM 自定义，然后将映像添加到 Configuration Manager 的启动映像所基于的 Windows PE 版本。  

-   **Windows ADK 版本**  

     适用于 Windows 10 的 Windows ADK  

-   **可从 Configuration Manager 控制台中自定义的启动映像的 Windows PE 版本**  

     Windows PE 10  

-   **不可从 Configuration Manager 控制台中自定义的启动映像的 Windows PE 支持版本**  

     Windows PE 3.1<sup>1</sup> 和 Windows PE 5  

     <sup>1</sup> 只有当启动映像基于 Windows PE 3.1 时才能将该映像添加到 Configuration Manager 中。 安装适用于 Windows 7 SP1 的 Windows AIK 补充，以使用适用于 Windows 7 SP1（基于 Windows PE 3.1）的 Windows AIK 补充升级适用于 Windows 7（基于 Windows PE 3）的 Windows AIK。 你可以从 [Microsoft 下载中心](http://www.microsoft.com/download/details.aspx?id=5188)下载适用于 Windows 7 SP1 的 Windows AIK 补充。  

     例如，如果具有 Configuration Manager，则可以利用 Configuration Manager 控制台自定义适用于 Windows 10 的 Windows ADK 中的启动映像（基于 Windows PE 10）。 但是，当支持基于 Windows PE 5 的启动映像时，你必须在不同的计算机中自定义它们，并使用随适用于 Windows 8 的 Windows ADK 一起安装的 DISM 版本。 然后，可以向 Configuration Manager 控制台添加启动映像。 有关自定义启动映像（添加可选组件和驱动程序）、对启动映像启用命令支持、将启动映像添加到 Configuration Manager 控制台中，以及使用启动映像更新分发点的步骤的详细信息，请参阅[自定义启动映像](customize-boot-images.md)。

 使用下列过程来手动添加启动映像。  

#### <a name="to-add-a-boot-image"></a>添加启动映像  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

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

 启动映像现在列出在 Configuration Manager 控制台的“启动映像”节点中。 但是，你必须将启动映像分发到分发点、分发点组或与分发点组关联的集合，然后才能使用该启动映像以部署操作系统。  

> [!NOTE]  
>  在 Configuration Manager 控制台中选择“启动映像”节点时，“大小(KB)”列会显示每个启动映像的解压缩大小。 但是，Configuration Manager 通过网络发送启动映像时，会发送映像的压缩副本，该副本通常远小于“大小(KB)”列中所列的大小。  

##  <a name="a-namebkmkdistributebootimagesa-distribute-boot-images-to-a-distribution-point"></a><a name="BKMK_DistributeBootImages"></a>将启动映像分发到分发点  
 将采用与分发其他内容相同的方式将启动映像分发到分发点。 大多数情况下，部署操作系统并创建媒体之前，必须将启动映像分发到至少一个分发点。  

> [!NOTE]  
>  若要使用 PXE 来部署操作系统，请在分发启动映像之前考虑以下因素：  
>   
>  -   至少配置一个分发点以接受 PXE 请求。  
> -   你必须将启用 x86 和 x64 PXE 的启动映像分发到至少一个启用 PXE 的分发点。  
> -   Configuration Manager 会将启动映像分发到启用 PXE 的分发点上的 **RemoteInstall** 文件夹。  
>   
>  有关使用 PXE 部署操作系统的详细信息，请参阅[使用 PXE 通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

 关于分发启动映像的步骤，请参阅 [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)。  

##  <a name="a-namebkmkmodifybootimagesa-modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a>修改启动映像  
 你可在映像中添加或删除设备驱动程序，或编辑与启动映像关联的属性。 你可添加或删除的设备驱动程序包括网络适配器或大容量存储设备驱动程序。 在修改启动映像时，请考虑以下因素：  

-   在将设备驱动程序添加到启动映像之前，你必须将这些驱动程序导入驱动程序目录并启用它们。  

-   在修改启动映像时，启动映像不会更改启动映像所引用的任何关联的包。  

-   对启动映像进行更改后，你必须 **更新** 已经具有启动映像的分发点上的启动映像，以便使用最新版本的启动映像。 有关详细信息，请参阅 [Manage content you have distributed](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkmanagea-manage-the-content-you-have-distributed)。  

 使用下列过程来修改启动映像。  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>修改启动映像的属性  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

3.  选择要修改的启动映像。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性”  打开启动映像的“属性”  对话框。  

5.  选择下列任何设置以更改启动映像的行为：  

    -   在“映像”  选项卡上，如果使用外部工具更改了启动映像的属性，请单击“重新加载” 。  

    -   在“驱动程序”  选项卡上，添加启动 WinPE 所需的 Windows 设备驱动程序。 在添加设备驱动程序时，请考虑以下各项：  

        -   选择“隐藏与启动映像体系结构不匹配的驱动程序”以仅显示适用于启动映像体系结构的驱动程序。 该体系结构以制造商提供的 .INF 中所报告的体系结构为基础。  

        -   选中“（对于启动映像）隐藏不属于存储或网络类的驱动程序”  以仅显示存储和网络驱动程序，并隐藏启动映像通常不需要的其他驱动程序（如视频驱动程序或调制解调器驱动程序）。  

        -   选中“隐藏未进行数字签名的驱动程序”  以隐藏未进行数字签名的驱动程序。  

        -   作为最佳方案，除非需要其他驱动程序作为 WinPE 的一部分，否则请仅向启动映像中添加 NIC 和批量存储驱动程序。  

        -   由于 WinPE 已经附带了许多内置驱动程序，因此请仅添加 WinPE 未提供的 NIC 和批量存储驱动程序。  

        -   确保添加到启动映像的驱动程序与启动映像的体系结构相匹配。  

        > [!NOTE]  
        >  在将设备驱动程序添加到启动映像之前，你必须将这些驱动程序导入驱动程序目录。 有关如何导入设备驱动程序的信息，请参阅[管理驱动程序](manage-drivers.md)。  

    -   在“自定义”  选项卡上，选择下列任意设置：  

        -   选中“启用预启动命令”  复选框以指定在运行任务序列之前运行的命令。 如果启用了预启动命令，你可以随后指定运行的命令行、是否需要支持文件来运行命令，以及这些支持文件的源位置。  

            > [!WARNING]  
            >  必须将 **cmd /c** 添加到命令行的开头。 如果未指定 **cmd /c**，则命令在运行之后不会关闭。 部署会继续等待命令完成，不会启动任何其他配置的命令或操作。  

            > [!TIP]  
            >  在任务序列媒体创建过程中，任务序列会将包 ID 和预启动命令行（包括任何任务序列变量的值）写入到运行 Configuration Manager 控制台的计算机上的 CreateTSMedia.log 日志文件。 你可以查看此日志文件以验证任务序列变量的值。  

        -   设置“Windows PE 背景”  设置以指定是要使用默认 WinPE 背景还是自定义背景。  

        -   选中“启用命令支持（仅限测试）”  ，以便在部署启动映像时通过使用“F8”  键来打开命令提示符。 在测试部署时，这对于故障排除非常有用。 不建议在生产部署中使用此设置。  

        -   配置 Windows PE 暂存空间，该空间是 WinPE 使用的临时存储（RAM 驱动器）。 例如，当应用程序在 WinPE 内运行并且需要写入临时文件时，WinPE 会将文件重定向到内存中的暂存空间以模拟硬盘的存在。 默认情况下，WinPE 分配 32 MB 的可写内存。  

    -   在“数据源”  选项卡上，更新下列任意设置：  

        -   设置“映像路径”  和“映像索引”  以更改启动映像的源文件。  

        -   选中“按计划更新分发点”  以针对何时更新启动映像创建计划。  

        -   如果不希望此包的内容从客户端缓存中脱离以为其他内容腾出空间，请选中“保留客户端缓存中的内容”  。  

        -   选中“启用二进制差异复制”  以指定只有当更新分发点上的启动映像包时才分发更改的文件。 此设置最大程度地减少了站点之间的网络流量，特别是在启动映像包很大并且变更相对较小时尤为如此。  

        -   如果将启动映像用于启用 PXE 的部署中，请选择“从启用 PXE 的分发点部署此启动映像”。  

            > [!NOTE]  
            >  有关详细信息，请参阅[使用 PXE 通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

    -   在“数据访问”  选项卡上，选择下列任意设置：  

        -   如果希望客户端从网络中安装此包中的内容，请选择“包共享设置”  。  

        -   设置“包更新设置”以指定希望 Configuration Manager 如何断开用户和分发点的连接。 当用户连接到分发点时，Configuration Manager 可能无法更新启动映像。  

    -   在“分发设置”  选项卡上，选择下列任意设置：  

        -   在“分发优先级”列表中，指定在向同一分发点分发多个包时希望 Configuration Manager 使用的优先级别。  

        -   如果要启用针对首选分发点的按需内容分发，请选择“将此包的内容分发到首选分发点”  。 如果启用此设置，则管理点会在客户端请求包内容并且内容在任何首选分发点上不可用时将内容分发到所有首选分发点。  

        -   设置“预留分发点设置”  以指定要如何将启动映像分发到为预留内容启用的分发点。  

            > [!NOTE]  
            >  有关预留内容的详细信息，请参阅 [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content)。  

    -   在“内容位置”  选项卡上，选择分发点或分发点组以执行下列任何操作：  

        -   单击“重新分发”  以将启动映像再次分发到所选分发点或分发点组。  

        -   单击“验证”  以检查所选分发点或分发点组上的启动映像包的完整性。  

    -   在“可选组件”选项卡上，指定要添加到 Windows PE 上以便与 Configuration Manager 一起使用的组件。 有关可用的可选组件的详细信息，请参阅 [WinPE: Add packages (Optional Components Reference)（WinPE：添加包（可选组件参考））](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx)。  

    -   在“安全”  选项卡上，选择管理用户并更改他们可执行的操作。  

6.  配置了属性后，单击“确定” 。  

##  <a name="a-namebkmkbootimagepxea-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a><a name="BKMK_BootImagePXE"></a>配置一个启动映像以从启用 PXE 的分发点部署  
 在为 PXE 操作系统部署使用启动映像之前，必须将启动映像配置为从启用 PXE 的分发点部署。  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>若要配置一个启动映像以从启用 PXE 的分发点部署  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

3.  选择要修改的启动映像。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性”  打开启动映像的“属性”  对话框。  

5.  在“数据源”  选项卡上选择“从启用 PXE 的分发点部署此启动映像” 。  

    > [!NOTE]  
    >  有关详细信息，请参阅[使用 PXE 通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

6.  配置了属性后，单击“确定” 。  

##  <a name="a-namebkmkbootimagelanguagea-configure-multiple-languages-for-boot-image-deployment"></a><a name="BKMK_BootImageLanguage"></a>为启动映像部署配置多种语言  
 语言中性的启动映像。 这样一来，在处于 WinPE 中时，如果将来自 Windows PE 可选组件的合适语言支持包括在内，并且设置了合适的任务序列变量以指示可以显示的语言，则你可以使用一个以多种语言显示任务序列文本的启动映像。 无论是哪个 Configuration Manager 版本，部署的操作系统的语言都独立于在处于 WinPE 中时显示的语言。 向用户显示的语言根据下列说明来确定：  

-   在用户从现有的操作系统运行任务序列时，Configuration Manager 会自动使用为用户配置的语言。 在规定的部署截止时间导致任务序列自动运行时，Configuration Manager 会使用操作系统的语言。  

-   对于使用 PXE 或媒体的操作系统部署，可以在作为预启动命令一部分的 SMSTSLanguageFolder 变量中设置语言 ID 值。 在计算机启动到 WinPE 时，会以你在此变量中指定的语言显示消息。 如果在访问指定文件夹中的语言资源文件时出错，或者你未设置此变量，则会以 WinPE 的语言显示消息。  

    > [!NOTE]  
    >  如果使用密码来保护媒体，则会始终以 WinPE 的语言来显示用于提示用户输入密码的文本。  

 使用下列过程为 PXE 或媒体启动的操作系统部署设置 WinPE 的语言。  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>为 PXE 或媒体启动的操作系统部署设置 Windows PE 的语言  

1.  在更新启动映像之前，验证合适的任务序列资源文件 (tsres.dll) 是否位于站点服务器上的相应语言文件夹中。 例如，英语资源文件位于以下位置：<*ConfigMgrInstallationFolder*>\OSD\bin\x64\00000409\tsres.dll。  

2.  将作为预启动命令一部分的 SMSTSLanguageFolder 环境变量设置为合适的语言 ID。 必须使用十进制而不是十六进制来指定语言 ID。 例如，若要将语言 ID 设置为英语，则应为文件夹名称指定十进制值 1033 而不是十六进制值 00000409。  



<!--HONumber=Dec16_HO3-->


