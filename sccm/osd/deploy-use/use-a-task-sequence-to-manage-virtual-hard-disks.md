---
title: "使用任务序列管理虚拟硬盘 | Microsoft Docs"
description: "通过 Configuration Manager 创建和修改 VHD、添加应用程序和软件更新，以及将 VHD 发布到 System Center Virtual Machine Manager (VMM)。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0212b023-804a-4f84-b880-7a59cdb49c67
caps.latest.revision: "5"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: f77af4b8fcb193ed44511c0e5eea7290f55dbbf8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-task-sequence-to-manage-virtual-hard-disks-in-system-center-configuration-manager"></a>使用任务序列来管理 System Center Configuration Manager 中的虚拟硬盘

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中，可以通过 Configuration Manager 控制台管理虚拟硬盘 (VHD) 并将所创建的 VHD 集成到数据中心中。 具体而言，可以通过 Configuration Manager 控制台创建和修改 VHD、向 VHD 中添加应用程序和软件更新，以及将 VHD 发布到 System Center Virtual Machine Manager (VMM)。  

 使用下列部分在 Configuration Manager 中管理 VHD。

## <a name="prerequisites"></a>先决条件  
 在开始之前，请验证下列先决条件：  

-   你从中管理 VHD 的计算机必须运行下列操作系统之一：  

    -   Windows 8.1 x64  

    -   Windows 8 x64  

    -   Windows Server 2008 R2  

    -   Windows Server 2012  

    -   Windows Server 2012 R2  

-   必须在 BIOS 中启用虚拟化，并且必须在从中运行 Configuration Manager 控制台来管理 VHD 的计算机上安装 Hyper-V。 同时，作为最佳方案，请安装 Hyper-V 管理工具来帮助你测试和诊断虚拟硬盘。 例如，若要监视 smsts.log 文件以跟踪 Hyper-V 中任务序列的进度，你必须安装 Hyper-V 管理工具。 有关 Hyper-V 要求的详细信息，请参阅 [安装 Hyper-V 的先决条件](http://technet.microsoft.com/library/cc731898.aspx)。  

    > [!IMPORTANT]  
    >  创建 VHD 的过程会消耗处理器时间和内存。 因此，建议通过不是安装在站点服务器上的 Configuration Manager 控制台来管理 VHD。  

-   当你通过远离站点服务器的计算机管理 VHD 时，站点服务器必须对包含 VHD 文件的文件夹具有“写入”  访问权限。  

-   验证在你从中管理 VHD 的计算机上是否有足够的可用磁盘空间。 VHD 的硬盘空间要求将因你安装的操作系统和应用程序而异。  

-   验证在你从中管理 VHD 的计算机上是否有足够的内存。 在创建 VHD 的过程中，虚拟机配置为消耗 2 GB 内存。  

-   在你从中将 VHD 上载到 VMM 的计算机上安装 System Center Virtual Machine Manager (VMM) 控制台。 你可以将 VMM 控制台安装在从中管理 VHD 的单独计算机上，这意味着无需安装 Hyper-V 即可将 VHD 导入到 VMM。  

    > [!NOTE]  
    >  如果在 Configuration Manager 控制台已打开的同时安装 VMM 控制台，必须在 VMM 控制台安装完成后重启 Configuration Manager 控制台。 否则， Configuration Manager 将无法成功连接到 VMM 管理服务器以上传 VHD。  

##  <a name="BKMK_CreateVHDSteps"></a> 创建 VHD 的步骤  
 要创建 VHD，你必须创建一个包含用于创建 VHD 的步骤的任务序列，然后在“创建虚拟硬盘向导”中使用该任务序列创建 VHD。 以下部分提供了创建 VHD 的步骤。  

###  <a name="BKMK_CreateTS"></a> 为 VHD 创建任务序列  
 你必须创建将包含创建 VHD 的步骤的任务序列。 在“创建任务序列向导”中，你可以选择“将现有的映像包安装到虚拟硬盘”  选项，该选项创建用于创建 VHD 的步骤。 例如，向导将添加所需的下列步骤：在 Windows PE 中重启、对磁盘进行格式化和分区、应用操作系统以及关闭计算机。 当处于完整操作系统中时，你无法创建 VHD。 此外，Configuration Manager 必须等待虚拟机关闭，然后才能完成包。 默认情况下，向导在关闭虚拟机之前将等待 5 分钟。 创建任务序列后，你可以在必要时添加其他步骤。  

> [!IMPORTANT]  
>  下列过程通过使用“将现有的映像包安装到虚拟硬盘”  选项来创建任务序列，该选项自动包括成功创建 VHD 的必需步骤。 如果选择使用现有任务序列或手动创建任务序列，请确保在任务序列的结尾添加“关闭计算机”步骤。 如果没有此步骤，将不会删除临时虚拟机，并且创建 VHD 的过程不会完成。 但是，向导将完成并报告成功。  

 使用下列过程来创建任务序列以创建 VHD：  

#### <a name="to-create-the-task-sequence-to-create-the-vhd"></a>创建任务序列以创建 VHD  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“任务序列” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建任务序列”  以启动创建任务序列向导。  

4.  在“创建新的任务序列”  页上，单击“将现有的映像包安装到虚拟硬盘” ，然后单击“下一步” 。  

5.  在“任务序列信息”  页上，指定以下设置，然后单击“下一步” 。  

    -   “任务序列名称”：指定用于标识任务序列的名称。  

    -   “描述”：指定任务序列的描述。  

    -   **启动映像包**：指定用于在目标计算机上安装操作系统的启动映像。 有关详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

6.  在“安装 Windows”  页上，指定以下设置，然后单击“下一步” 。  

    -   “映像包”：指定包含要安装的操作系统映像的包。  

    -   “映像”：如果操作系统映像包有多个映像，请指定要安装的操作系统映像的索引。  

    -   “产品秘钥”：指定要安装的 Windows 操作系统的产品密钥。 你可以指定编码的批量许可证密钥和标准产品密钥。 如果使用非编码的产品密钥，则必须通过短划线 (-) 分隔每组 5 个字符。 例如： *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   “服务器授权模式”：指定服务器许可证为“每客户” , 或未指定许可证。 如果服务器许可证为“每服务器” ，则还需指定服务器连接的最大数量。  

    -   指定如何处理在部署操作系统映像时使用的管理员帐户。  

        -   “随机生成本地管理员密码并禁用所有支持的平台上的帐户（建议）”：使用此设置让向导随机创建本地管理员帐户的密码并在部署操作系统映像后禁用该帐户。  

        -   “启用帐户并指定本地管理员密码”：使用此设置以便为部署操作系统映像的所有计算机上的本地管理员帐户使用特定密码。  

7.  在“配置网络”  页上，指定以下设置，然后单击“下一步” 。  

    -   “加入工作组”：指定是否将目标计算机添加到工作组。  

    -   “加入域”：指定是否将目标计算机添加到域。 在“域” 中，指定域的名称。  

        > [!IMPORTANT]  
        >  你可以浏览以查找本地林中的域，但对于远程林则必须指定域名。  

         你还可以指定组织单位 (OU)。 这是一项可选设置，用于指定在其中创建计算机帐户的 OU 的 LDAP X.500 可分辨名称（如果尚未存在）。  

    -   “帐户”：指定具有加入指定域的权限的帐户的用户名和密码。 例如： *domain\user* 或 *%variable%*。  

8.  在“安装 Configuration Manager”页上，指定要安装到目标计算机上的 Configuration Manager 客户端包，然后单击“下一步”。  

9. 在“安装应用程序”  页上，指定要安装在目标计算机上的应用程序，然后单击“下一步” 。 如果指定多个应用程序，你也可以指定任务序列在特定应用程序的安装失败时继续进行。  

10. 完成向导。  

###  <a name="BKMK_CreateVHD"></a> 创建 VHD  
 为 VHD 创建任务序列之后，请使用“创建虚拟硬盘向导”来创建 VHD。  

> [!IMPORTANT]  
>  在运行此过程之前，请验证是否满足本主题开头列出的先决条件。  

 使用下列过程来创建 VHD。  

#### <a name="to-create-a-vhd"></a>创建 VHD  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“虚拟硬盘” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建虚拟硬盘”  以启动“创建虚拟硬盘向导”。  

    > [!NOTE]  
    >  Hyper-V 必须安装在运行 Configuration Manager 控制台（从中管理 VHD）的计算机上，否则不会启用“创建虚拟硬盘”选项。 有关 Hyper-V 要求的详细信息，请参阅 [安装 Hyper-V 的先决条件](http://technet.microsoft.com/library/cc731898.aspx)。  

    > [!TIP]  
    >  若要组织 VHD，请在“虚拟硬盘”  节点下创建一个新文件夹或选择现有文件夹，然后从该文件夹中单击“创建虚拟硬盘”  。  

4.  在“常规”  页上，指定以下设置，然后单击“下一步” 。  

    -   “名称”：为 VHD 指定唯一名称。  

    -   “版本”：为 VHD 指定版本号。 这是一个可选设置。  

    -   “注释”：为 VHD 指定描述。  

    -   “路径”：指定向导将在其中创建 VHD 文件的位置的路径和文件名。  

         你必须以 UNC 格式输入有效的网络路径。 例如：**\\\servername\\<sharename\>\\<filename\>.vhd**。  

        > [!WARNING]  
        >  Configuration Manager 必须对指定路径具有“写入”访问权限才能创建 VHD。 如果 Configuration Manager 未能访问该路径，它会将关联的错误记录在站点服务器上的 distmgr.log 文件中。  

5.  在“任务序列”  页上，指定你在前面部分中指定的任务序列，然后单击“下一步” 。  

6.  在“分发点”  页上，选择包含任务序列所需的内容的一个或多个分发点，然后单击“下一步” 。  

7.  在“自定义”  页面上，单击“下一步” 。 VHD 的创建过程将忽略你在此页面上指定的任何设置。  

8.  查看设置，然后单击“下一步” 。 此向导将创建 VHD。  

    > [!TIP]  
    >  完成该过程以创建 VHD 的过程的时间可能有所不同。 在向导进行此过程的同时，你可以监视下列日志文件来跟踪进度。 默认情况下，这些日志位于运行 Configuration Manager 控制台的计算机上的 %ProgramFiles(x86)%\Microsoft Configuration Manager\AdminConsole\AdminUILog 中。  
    >   
    >  -   “”：向导在创建任务序列媒体时将信息写入此日志。 查看此日志文件来跟踪向导在创建独立媒体时的进度。  
    > -   “”：向导在进行创建 VHD 的过程时将信息写入此日志。 查看此日志文件来跟踪向导在创建独立媒体后所有步骤的进度。  
    >   
    >  此外，当操作系统安装启动时，你可以打开 Hyper-V 管理器（如果在计算机上安装了 Hyper-V 管理工具），并连接到向导创建的临时虚拟机以查看正在运行的任务序列。 从该虚拟机中，你可以监视 smsts.log 文件来跟踪任务序列的进度。 如果在完成任务序列步骤时出现问题，你可以使用此日志文件来帮助你解决问题。 smsts.log 文件位于 x: \windows\temp\smstslog\smsts.log（在硬盘格式化前），位于 c:\\_SMSTaskSequence\Logs\Smstslog\（在格式化后）。 任务序列步骤完成后，虚拟机（默认情况下）会在 5 分钟后关闭并被删除。  

 Configuration Manager 创建 VHD 后，它位于“软件库”工作区中“操作系统部署”节点下 Configuration Manager 控制台中的“虚拟硬盘”中。  

> [!NOTE]  
>  Configuration Manager 通过连接到 VHD 的源位置来检索 VHD 的大小。 如果 Configuration Manager 无法访问 VHD 文件，则 VHD 的“大小 (KB)”列中显示 **0**。  

##  <a name="BKMK_ModifyVHDSteps"></a> 修改现有 VHD 的步骤  
 要修改 VHD，你必须创建一个包含修改 VHD 所需的步骤的任务序列。 然后，在“修改虚拟硬盘向导”中选择该任务序列。 该向导会将 VHD 连接到虚拟机、在 VHD 中运行任务序列，然后更新 VHD 文件。 以下部分提供了修改 VHD 的步骤。  

###  <a name="BKMK_ModifyTS"></a> 创建任务序列以修改 VHD  
 要修改现有的 VHD，必须首先创建一个任务序列。 仅选择修改任务序列所需的步骤。 例如，如果要将应用程序添加到 VHD 中，请创建自定义任务序列，然后仅添加“安装应用程序”步骤。  

 使用下列过程来创建任务序列以修改 VHD。  

#### <a name="to-create-a-custom-task-sequence-to-modify-the-vhd"></a>创建自定义任务序列以修改 VHD  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“任务序列” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建任务序列”  以启动创建任务序列向导。  

4.  在“创建新的任务序列”  页面上，选择“创建新的自定义任务序列” ，然后单击“下一步” 。  

5.  在“任务序列信息”  页上，指定以下设置，然后单击“下一步” 。  

    -   “任务序列名称”：指定用于标识任务序列的名称。  

    -   “描述”：指定任务序列的描述。  

    -   **启动映像包**：指定用于在目标计算机上安装操作系统的启动映像。 有关详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

6.  完成向导。  

 使用下列过程将任务序列步骤添加到自定义任务序列中。  

#### <a name="to-add-task-sequence-steps-to-the-custom-task-sequence"></a>将任务序列步骤添加到自定义任务序列中  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，单击“任务序列” ，然后选择在上一个过程中创建的自定义任务序列。  

3.  在“主页”  选项卡上的“任务序列”  组中，单击“编辑”  以启动任务序列编辑器。  

4.  添加用于修改 VHD 的任务序列步骤。  

5.  单击“确定”  退出任务序列编辑器。  

###  <a name="BKMK_ModifyVHD"></a> 修改 VHD  
 为 VHD 创建任务序列之后，请使用“修改虚拟硬盘向导”来修改 VHD。  

 使用下列过程来修改 VHD。  

#### <a name="to-modify-a-vhd"></a>修改 VHD  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，单击“虚拟硬盘” ，然后选择要修改的 VHD。  

3.  在“主页”  选项卡上的“虚拟硬盘”  组中，单击“修改虚拟硬盘”  以启动“修改虚拟硬盘向导”。  

    > [!NOTE]  
    >  Hyper-V 必须安装在运行 Configuration Manager 控制台（从中管理 VHD）的计算机上，否则不会启用“修改虚拟硬盘”选项。 有关 Hyper-V 要求的详细信息，请参阅 [安装 Hyper-V 的先决条件](http://technet.microsoft.com/library/cc731898.aspx)。  

4.  在“常规”  页上，确认下列设置，然后单击“下一步” 。  

    -   “名称”：为 VHD 指定唯一名称。  

    -   “版本”：为 VHD 指定版本号。 这是一个可选设置。  

    -   “注释”：为 VHD 指定描述。  

    -   “路径”：指定 VHD 文件所在位置的路径和文件名。 你无法修改此设置。  

        > [!WARNING]  
        >  Configuration Manager 必须对指定路径具有“写入”访问权限才能创建 VHD。 如果 Configuration Manager 未能访问该路径，它会将关联的错误记录在站点服务器上的 distmgr.log 文件中。  

5.  在“任务序列”  页上，指定你在前面部分中创建的自定义任务序列，然后单击“下一步” 。  

6.  在“分发点”  页上，选择包含任务序列所需的内容的一个或多个分发点，然后单击“下一步” 。  

7.  在“自定义”  页面上，单击“下一步” 。 VHD 的修改过程将忽略你在此页面上指定的任何设置。  

8.  查看设置，然后单击“下一步” 。 此向导将创建修改的 VHD。  

    > [!TIP]  
    >  完成该过程以修改 VHD 的过程的时间可能有所不同。 在向导进行此过程的同时，你可以监视下列日志文件来跟踪进度。 默认情况下，这些日志位于运行 Configuration Manager 控制台的计算机上的 %ProgramFiles(x86)%\Microsoft Configuration Manager\AdminConsole\AdminUILog 中。  
    >   
    >  -   “”：向导在创建任务序列媒体时将信息写入此日志。 查看此日志文件来跟踪向导在创建独立媒体时的进度。  
    > -   “”：向导在进行修改 VHD 的过程时将信息写入此日志。 查看此日志文件来跟踪向导在创建独立媒体后所有步骤的进度。  
    >   
    >  此外，你可以打开 Hyper-V 管理器（如果在计算机上安装了 Hyper-V 管理工具），并连接到向导创建的临时虚拟机以查看正在运行的任务序列。 从该虚拟机中，你可以监视 smsts.log 文件来跟踪任务序列的进度。 如果在完成任务序列步骤时出现问题，你可以使用此日志文件来帮助你解决问题。 smsts.log 文件位于 x: \windows\temp\smstslog\smsts.log（在硬盘格式化前），位于 c:\\_SMSTaskSequence\Logs\Smstslog\（在格式化后）。 任务序列步骤完成后，虚拟机（默认情况下）会在 5 分钟后关闭并被删除。  

##  <a name="BKMK_ApplyUpdates"></a> 将软件更新应用于 VHD  
 我们会定期发布适用于你的 VHD 中的操作系统的新软件更新。 你可以按指定计划将适用的软件更新应用于 VHD。 Configuration Manager 将按指定的计划将所选的软件更新应用于 VHD。  

 有关 VHD 的信息存储在站点数据库中，包括在创建 VHD 时应用的软件更新。 自 VHD 最初创建以来已应用于 VHD 的软件更新也存储在站点数据库中。 当你启动向导以将软件更新应用于 VHD 时，向导将检索尚未应用于 VHD 的适用软件更新的列表供你选择。  

 可以选择“出错时继续”设置，即使应用选择的一个或多个软件更新时出错，Configuration Manager 也可继续应用软件更新。  

> [!NOTE]  
>  将从站点服务器上的内容库中复制软件更新。  

 使用下列过程将软件更新应用于 VHD。  

#### <a name="to-apply-software-updates-to-a-vhd"></a>将软件更新应用于 VHD  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“虚拟硬盘” 。  

3.  选择要应用软件更新的 VHD。  

4.  在“主页”  选项卡上的“虚拟硬盘”  组中，单击“计划更新”  以启动向导。  

5.  在“选择更新”  页上，选择要应用于 VHD 的软件更新，然后单击“下一步” 。  

6.  在“设置计划”  页上，指定以下设置，然后单击“下一步” 。  

    1.  “计划”：指定有关何时将软件更新应用于 VHD 的计划。  

    2.  “出错时继续”：选择此选项以便即使在出错时也继续将软件更新应用于映像。  

7.  在“摘要”  页上，验证以下信息，然后单击“下一步” 。  

8.  在“完成”  页上，验证软件更新是否已成功应用于操作系统映像。  

##  <a name="BKMK_ImportToVMM"></a> 将 VHD 导入到 System Center Virtual Machine Manager  
 System Center VMM 是用于虚拟化数据中心的管理解决方案，使你能够配置和管理虚拟化主机、网络以及存储资源，以便创建虚拟机和服务并将它们部署到你创建的私有云。 在 Configuration Manager 中创建 VHD 之后，可通过使用 VMM 来导入和管理 VHD。  

> [!TIP]  
>  在将 VHD 上载到 VMM 之前，请验证 VMM 控制台是否成功连接到 VMM 管理服务器。  

 使用下列过程将 VHD 导入到 VMM。  

#### <a name="to-import-a-vhd-to-vmm"></a>将 VHD 导入到 VMM  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“虚拟硬盘” 。  

3.  在“主页”  选项卡上的“虚拟硬盘”  组中，单击“上载到 Virtual Machine Manager”  以启动“上载到 Virtual Machine Manager 向导”。  

4.  在“常规”  页上，配置下列设置，然后单击“下一步” 。  

    -   “VMM 服务器名称”：指定在其上安装 VMM 管理服务器的计算机的 FQDN。 向导将连接到 VMM 管理服务器以下载服务器的库共享。  

    -   “VMM 库共享”: Specify the  from the drop-down list.  

    -   “使用未加密的传输”：选择此设置以在不使用加密的情况下将 VHD 文件传输到 VMM 管理服务器。  

5.  在“摘要”页面上验证设置，然后完成向导。 上载 VHD 所花费的时间可能会因 VHD 文件的大小以及连接到 VMM 管理服务器的网络带宽而异。  
