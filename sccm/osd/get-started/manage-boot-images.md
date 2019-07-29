---
title: 管理启动映像
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中，了解如何管理在 OS 部署过程中使用的 Windows PE 启动映像。
ms.date: 02/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ddc856b3c1615045aadba60c4616223349a7b61d
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340422"
---
# <a name="manage-boot-images-with-configuration-manager"></a>使用 Configuration Manager 管理启动映像

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的一个启动映像是在 OS 部署过程中使用的 [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) 映像。 启动映像用于在 WinPE 中启动计算机。 此最小 OS 包含有限的组件和服务。 Configuration Manager 使用 WinPE 准备用于安装 Windows 的目标计算机。 



## <a name="BKMK_BootImageDefault"></a>默认启动映像

Configuration Manager 提供两个默认启动映像：一个用于支持 x86 平台，另一个用于支持 x64 平台。 这些映像存储在站点服务器以下共享的 x64  或 i386  文件夹中：`\\<SiteServerName>\SMS_<sitecode>\osd\boot\`。 将根据所采用的操作更新或重新生成默认启动映像。

针对所描述的默认启动映像的任何操作，请考虑下列行为：

- 源驱动程序对象必须有效。 这些对象包括驱动程序源文件。 如果对象无效，站点不会将驱动程序添加到启动映像。  

- 不会修改不基于默认启动映像的启动映像（即使使用相同的 Windows PE 版本）。  

- 将已修改的启动映像重新分发到分发点。  

- 重新创建要使用修改后的启动映像的媒体。  

- 如果不希望自动更新自定义/默认启动映像，请勿将它们存储在默认位置。  

> [!NOTE]
> 向“软件库”中的所有启动映像添加了 Configuration Manager 日志工具 (CMTrace)   。 位于 Windows PE 中时，通过在命令提示符处键入 `cmtrace` 来启动该工具。 
> 
> 从版本 1802 开始，在 Windows PE 中启动 CMTrace 时不再提示选择是否将此程序设置为日志文件的默认查看器。


### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>使用更新和服务来安装最新版本的 Configuration Manager

如果升级 Windows 评估和部署工具包 (ADK) 版本，然后使用更新和服务安装 Configuration Manager 的最新版本，站点将重新生成默认启动映像。 此项更新包括已更新的 Windows ADK 中的新 WinPE 版本、新版本的 Configuration Manager 客户端、驱动程序以及自定义项。 站点不会修改自定义启动映像。


### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>从 Configuration Manager 2012 升级到当前分支

将 Configuration Manager 2012 升级到当前分支后，站点会重新生成默认启动映像。 此项更新包括已更新的 Windows ADK 中的新 WinPE 版本以及新版本的 Configuration Manager 客户端。 所有启动映像的自定义项保持不变。 站点不会修改自定义启动映像。


### <a name="update-distribution-points-with-the-boot-image"></a>利用启动映像更新分发点

从控制台中的“启动映像”节点使用“更新分发点”操作时，站点使用客户端组件、驱动程序以及自定义项更新目标启动映像   。    

可以使用 Windows ADK 安装目录中最新版本的 WinPE 重载启动映像。  更新分发点向导的常规页面提供下列信息： 
- 站点服务器上安装的当前 Windows ADK 版本
- 当前生产客户端版本
- 启动映像中的 WinPE 的 Windows ADK 版本
- 启动映像中的 Configuration Manager 客户端版本

如果启动映像中的版本已过时，请使用选项“使用 Windows ADK 中的当前 Windows PE 版本重载此启动映像”  。 

> [!Important]  
> 此操作适用于默认和自定义启动映像。 在重载启动映像的过程中，站点不会保留在 Configuration Manager 外部进行的任何手动自定义设置。 这些自定义设置包括第三方扩展。 此选项使用最新版的 WinPE 和最新客户端版本重新生成启动映像。 仅重新应用在启动映像的属性上指定的配置。 <!--SCCMDocs issue #1283-->

 启动映像节点还包括新的一列（客户端版本）  。 使用此列可以快速查看每个启动映像中的 Configuration Manager 客户端版本。    



##  <a name="BKMK_BootImageCustom"></a>自定义启动映像  

如果启动映像基于支持的 Windows ADK 版本中的 WinPE 版本，可以从控制台自定义启动映像或[修改启动映像](#BKMK_ModifyBootImages)。 升级站点并安装新版本的 Windows ADK 时，不会使用新版本的 Windows ADK 更新自定义启动映像。 发生这种情况时，无法在 Configuration Manager 控制台中自定义启动映像。 但是，它们会继续如同升级之前一样正常运行。  

如果启动映像基于站点上安装的另一个 Windows ADK 版本，则必须自定义启动映像。 使用另一种方法来自定义这些启动映像，例如使用部署映像服务以及管理 (DISM) 命令行工具。 DISM 是 Windows ADK 的一部分。 有关详细信息，请参阅[自定义启动映像](customize-boot-images.md)。  



##  <a name="BKMK_AddBootImages"></a>添加启动映像  

在站点安装过程中，Configuration Manager 会自动添加 Windows ADK 支持版本中基于 WinPE 版本的启动映像。 根据 Configuration Manager 的版本，可以添加 Windows ADK 支持版本中基于不同 WinPE 版本的启动映像。 如果尝试添加包含不受支持的 WinPE 版本的启动映像，则会发生错误。 以下列表中是当前支持的 Windows ADK 和 WinPE 版本： 


|  |  |
|---------|---------|
| Windows ADK 版本 | 适用于 Windows 10 的 Windows ADK |
| 可从 Configuration Manager 控制台自定义的启动映像的 Windows PE 版本 | Windows PE 10 |
| 不可从 Configuration Manager 控制台自定义的启动映像的受支持 Windows PE 版本  | - Windows PE 3.1<sup>[注释 1](#bkmk_note1)</sup> <br> - Windows PE 5 |

例如，利用 Configuration Manager 控制台通过适用于 Windows 10 的 Windows ADK 自定义基于 Windows PE 10 的启动映像。 对于基于 Windows PE 5 的启动映像，请使用适用于 Windows 8 的 Windows ADK 中的 DISM 版本从另一台计算机对其进行自定义。 然后向 Configuration Manager 控制台添加自定义启动映像。 有关详细信息，请参阅下列文章：
- [自定义启动映像](/sccm/osd/get-started/customize-boot-images)
- [支持 Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)
- [DISM 支持的平台](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)

#### <a name="bkmk_note1"></a>注释 1：支持 Windows PE 3.1

只有当启动映像基于 Windows PE 版本 3.1  时才能将该映像添加到 Configuration Manager。 使用适用于 Windows 7 SP1（基于 Windows PE 3.1）的 Windows AIK 补充来升级适用于 Windows 7（基于 Windows PE 3.0）的 Windows AIK。 从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=5188)下载适用于 Windows 7 SP1 的 Windows AIK 补充程序。  


#### <a name="process-to-add-a-boot-image"></a>添加启动映像的过程  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“启动映像”节点    。  

2. 在功能区“主页”选项卡的“创建”组中，选择“添加启动映像”    。 此操作将启动“添加启动映像向导”。  

3. 在“数据源”页上，指定以下选项  ：  

    - 在“路径”  框中，指定启动映像 WIM 文件的路径。 指定的路径必须是 UNC 格式的有效网络路径。 例如：`\\ServerName\ShareName\BootImageName.wim`

    - 从“启动映像”  下拉列表中选择启动映像。 如果 WIM 文件包含多个启动映像，则选择相应的映像。  

4. 在“常规”页上，指定以下各选项  ：  

    - 在“名称”  框中，为启动映像指定唯一名称。  

    - 在“版本”  框中，为启动映像指定版本号。  

    - 在“备注”  框中，指定有关启动映像使用方式的简要说明。  

5. 完成向导。  

“启动映像”  节点中现在列出启动映像。 在使用启动映像部署 OS 之前，请将启动映像分发到分发点。 

> [!Tip]  
> 在控制台的“启动映像”节点中，“大小(KB)”列会显示每个启动映像的解压缩大小   。 当站点通过网络发送启动映像时，它会发送压缩副本。 此副本通常小于“大小(KB)”列中列出的大小  。  



##  <a name="BKMK_DistributeBootImages"></a>分发启动映像  

将采用与分发其他内容相同的方式将启动映像分发到分发点。 在部署 OS 或创建媒体之前，请将启动映像分发到至少一个分发点。   

若要详细了解如何分发启动映像，请参阅[分发内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)。  

若要使用 PXE 来部署 OS，请在分发启动映像之前考虑以下几点：  
- 配置分发点以接受 PXE 请求。  
- 将启用 x86 和 x64 PXE 的启动映像分发到至少一个启用 PXE 的分发点。  
- Configuration Manager 会将启动映像分发到启用 PXE 的分发点上的 **RemoteInstall** 文件夹。  
  
有关使用 PXE 部署操作系统的详细信息，请参阅[使用 PXE 通过网络部署 Windows](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)。  



##  <a name="BKMK_ModifyBootImages"></a>修改启动映像  

在映像中添加或删除设备驱动程序，或编辑启动映像的属性。 可添加或删除的驱动程序包括网络或存储驱动程序。 在修改启动映像时，请考虑以下因素：  

- 在将驱动程序添加到启动映像之前，将这些驱动程序导入设备驱动程序目录并启用它们。  

- 在修改启动映像时，启动映像不会更改启动映像所引用的任何关联的包。  

- 对启动映像进行更改后，在已有该启动映像的分发点上更新它  。 此过程让客户端可以使用该启动映像的最新版本。 有关详细信息，请参阅[管理已分发的内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage)。  


### <a name="process-to-modify-the-properties-of-a-boot-image"></a>修改启动映像属性的过程  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“启动映像”节点    。  

2. 选择要修改的启动映像。  

3. 在功能区“主页”  选项卡的“属性”  组中，选择“属性”  。  

4. 选择下列任何设置以更改启动映像的行为：  

#### <a name="images"></a>映像
在“映像”  选项卡上，如果使用外部工具更改启动映像的属性，请单击“重载”  。  

#### <a name="drivers"></a>驱动程序
在“驱动程序”  选项卡上，添加启动 WinPE 所需的 Windows 设备驱动程序。 在添加设备驱动程序时，请考虑以下几点：  

- 确保添加到启动映像的驱动程序与启动映像的体系结构相匹配。  

- 若要仅显示适用于启动映像体系结构的驱动程序，请选中“隐藏与启动映像体系结构不匹配的驱动程序”  。 驱动程序的体系结构以制造商提供的 INF 中所报告的体系结构为基础。  

- WinPE 已经内置了许多驱动程序。 仅添加 WinPE 中未包含的网络和存储驱动程序即可。  

- 除非 WinPE 需要其他驱动程序，否则请仅向启动映像添加网络和存储驱动程序。  

- 若要仅显示存储和网络驱动程序，请选中“隐藏不位于(用于启动映像的)存储或网络类中的驱动程序”  。 此选项还会隐藏启动映像通常不需要的其他驱动程序，例如视频或调制解调器驱动程序。  

- 若要隐藏无有效数字签名的驱动程序，请选中“隐藏未进行数字签名的驱动程序”  。  

> [!NOTE]  
> 在将设备驱动程序添加到启动映像之前，请将这些驱动程序导入驱动程序目录。 有关如何导入设备驱动程序的信息，请参阅[管理驱动程序](manage-drivers.md)。  

#### <a name="customization"></a>自定义
在“自定义”  选项卡上，选择下列任意设置：  

- 选中“启用预启动命令”  选项以指定在运行任务序列之前运行的命令。 启动此选项时，还指定要运行的命令行以及该命令需要的任何支持文件。  

    > [!WARNING]  
    > 将 cmd /c  添加到命令行的开头。 如果未指定 cmd /c  ，则命令在运行之后不会关闭。 部署会继续等待命令完成，不会启动任何其他配置的命令或操作。  

    > [!TIP]  
    > 在任务序列媒体创建过程中，该向导会将包 ID 和预启动命令行写入到 CreateTSMedia.log 日志文件。 此信息包括任何任务序列变量的值。 此日志位于运行 Configuration Manager 控制台的计算机上。 查看此日志文件以验证任务序列变量的值。  

- 设置“Windows PE 背景”  设置以指定是要使用默认 WinPE 背景还是自定义背景。  

- 选中“启用命令支持（仅限测试）”  ，以便在部署启动映像时通过使用“F8”  键来打开命令提示符。 在测试部署时，此选项对于故障排除非常有用。 出于安全考虑，不建议在生产部署中使用此设置。  

- 配置 Windows PE 暂存空间，该空间是 WinPE 使用的临时存储（RAM 驱动器）。 例如，当应用程序在 WinPE 内运行并且需要写入临时文件时，WinPE 会将文件重定向到内存中的暂存空间以模拟硬盘的存在。 默认情况下，对于 RAM 超过 1 GB 的设备，此数量为 512 MB，否则默认值为 32 MB。  

#### <a name="optional-components"></a>可选组件
在“可选组件”  选项卡上，指定要添加到 Windows PE 上以便与 Configuration Manager 一起使用的组件。 有关可用的可选组件的详细信息，请参阅 [WinPE: Add packages (Optional Components Reference)（WinPE：添加包（可选组件参考））](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference)。  

以下组件是 Configuration Manager 的必备组件，并且始终添加到启动映像：
- 脚本 (WinPE-Scripting)
- 启动 (WinPE-SecureStartup)
- 网络 (WinPE-WDS-Tools)
- 脚本 (WinPE-WMI)

“组件”  列表显示添加到此启动映像的其他项。 若要添加更多组件，请选择金色的星号。 若要删除组件，请从列表中选中它，然后选择红色的 X。 

客户通常使用以下组件：
- Microsoft .NET (WinPE-NetFX): 此组件是 PowerShell 的必备组件。 它是较大的可选组件之一。  
- Windows PowerShell (WinPE-PowerShell): 此组件需要 .NET, 并添加有限的 PowerShell 支持。 如果在任务序列的 WinPE 阶段运行自定义 PowerShell 脚本，请添加此组件。 还有一些其他 PowerShell cmdlet 可能还需要的其他组件。   
- HTML (WinPE-HTA)：如果在任务序列的 WinPE 阶段运行自定义 HTML 应用程序，请添加此组件。 

有关添加语言的详细信息，请参阅[配置多种语言](#BKMK_BootImageLanguage)。 

#### <a name="data-source"></a>“数据源”
在“数据源”  选项卡上，更新下列任意设置：  

- 设置“映像路径”  和“映像索引”  以更改启动映像的源文件。  

- 选中“按计划更新分发点”  以针对何时更新启动映像创建计划。  

- 如果不希望此包的内容从客户端缓存中脱离以为其他内容腾出空间，请选中“保留客户端缓存中的内容”  。  

- 若要指定站点在更新分发点上的启动映像包时只分发更改的文件，请选中“启用二进制差异复制”  (BDR)。 此设置能最大程度地减少站点之间的网络流量。 在启动映像包较大且更改相对较小时，BDR 会特别有用。  

- 如果将启动映像用于启用 PXE 的部署中，请选择“从启用 PXE 的分发点部署此启动映像”  。 有关详细信息，请参阅[使用 PXE 通过网络部署 Windows](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)。  

#### <a name="data-access"></a>数据访问
在“数据访问”  选项卡上，可以配置包共享设置。 如果环境需要，请将选项设置为“将此包中的内容复制到分发点上的包共享”  。 然后，可以使用附加选项“为包共享使用自定义名称”  ，并指定自定义的“共享名称”  。 如果启用此选项，则分发点上需要更多的磁盘空间。 它适用于接收此启动映像的所有分发点。 

#### <a name="distribution-settings"></a>分发设置
在“分发设置”  选项卡上，选择下列任意设置：  

- 在“分发优先级”列表中指定优先级别  。 当站点将多个包分发至同一个分发点时，Configuration Manager 使用此优先级列表。  

- 如果要启用针对首选分发点的按需内容分发，请选择“启用按需分发”  。 如果启用此设置，则管理点会在客户端请求包内容并且内容在任何分发点上都不可用时分发内容。 有关详细信息，请参阅[按需内容分发](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution)。  

- 设置“预留分发点设置”  以指定要如何将启动映像分发到为预留内容启用的分发点。 有关预留内容的详细信息，请参阅 [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage)。  

#### <a name="content-locations"></a>内容位置
在“内容位置”  选项卡上，选择分发点或分发点组，并执行下列操作：  

- **验证**：检查所选分发点或分发点组上的启动映像包的完整性。  

- **重新分发**：将启动映像再次分发到所选分发点或分发点组。  

- **删除**：从所选分发点或分发点组删除启动映像。  

#### <a name="security"></a>安全
在“安全”  选项卡上，查看对此对象具有权限的管理用户。



## <a name="BKMK_BootImagePXE"></a>为 PXE 配置启动映像  

在为基于 PXE 的部署使用启动映像之前，将启动映像配置为从启用 PXE 的分发点部署。  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“启动映像”节点    。  

2. 选择要修改的启动映像。  

3. 在功能区“主页”  选项卡的“属性”  组中，选择“属性”  。  

4. 在“数据源”  选项卡上选择“从启用 PXE 的分发点部署此启动映像”  。 有关详细信息，请参阅[使用 PXE 通过网络部署 Windows](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)。  



## <a name="BKMK_BootImageLanguage"></a>配置多种语言

语言中性的启动映像。 此功能允许在 WinPE 中使用单个启动映像以多种语言显示任务序列文本。 包括启动映像“可选组件”选项卡中适用的语言支持  。然后设置合适的任务序列变量以指示要显示的语种。 已部署的 OS 的语言独立于 WinPE 中的语言。 WinPE 向用户显示的语言根据下列说明来确定：  

- 在用户从现有的 OS 运行任务序列时，Configuration Manager 会自动使用为用户配置的语言。 在规定的部署截止时间导致任务序列自动运行时，Configuration Manager 会使用 OS 的语言。  

- 对于使用 PXE 或媒体的 OS 部署，请在作为预启动命令一部分的 SMSTSLanguageFolder 变量中设置语言 ID 值  。 在计算机启动到 WinPE 时，会以你在此变量中指定的语言显示消息。 如果在访问指定文件夹中的语言资源文件时出错，或者未设置此变量，WinPE 会以默认语言显示消息。  

    > [!NOTE]  
    > 如果使用密码来保护媒体，则会始终以 WinPE 的语言来显示用于提示用户输入密码的文本。  

使用下列过程为 PXE 或媒体启动的 OS 部署设置 WinPE 的语言。  

#### <a name="process-to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>为 PXE 或媒体启动的 OS 部署设置 Windows PE 语言的过程  

1. 在更新启动映像之前，请验证相应的任务序列资源文件 (tsres.dll) 是否位于站点服务器上相应的语言文件夹中。 例如，英语资源文件位于下列位置：`<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. 将作为预启动命令一部分的 SMSTSLanguageFolder  环境变量设置为相应的语言 ID。 必须使用十进制而不是十六进制格式来指定语言 ID。 例如，若要将语言 ID 设置为英语，应为文件夹名称指定十进制值 1033  而不是十六进制值 00000409。  
