---
title: "创建用于升级操作系统的任务序列 | Microsoft Docs"
description: "System Center Configuration Manager 中的任务序列可自动将操作系统从 Windows 7 或更高版本升级到 Windows 10。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 4a3c69edc85a4ea7501510b6b3f12c72ad3a24ff
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>创建任务序列来升级 System Center Configuration Manager 中的操作系统

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中使用任务序列，自动在目标计算机上将操作系统从 Windows 7 或更高版本升级到 Windows 10，或从 Windows Server 2012 或更高版本升级到 Windows Server 2016。 你创建一个任务序列，该任务序列引用要安装在目标计算机上的操作系统映像，以及要安装的任何其他附加内容（例如应用程序或软件更新）。 用于升级操作系统的任务序列属于[将 Windows 升级到最新版本](upgrade-windows-to-the-latest-version.md)方案的一部分。  

##  <a name="BKMK_UpgradeOS"></a>创建用于升级操作系统的任务序列  
 若要升级计算机上的操作系统，可以创建一个任务序列，并在“创建任务序列向导”中选择“通过升级包升级操作系统”。 该向导将添加一些步骤，用于升级操作系统、应用软件更新和安装应用程序。 在创建任务序列之前，必须部署以下内容：    

-   **必需**  

     - [操作系统升级包](../get-started/manage-operating-system-upgrade-packages.md)必须在 Configuration Manager 控制台中可用。
     - 升级到 Windows Server 2016 时，必须在“升级操作系统任务序列步骤”中选择“忽略任何可拒绝的兼容性消息”设置，否则升级将失败。

-   **必需（若使用）**  

    -   必须在 Configuration Manager 控制台中同步[软件更新](../../sum/get-started/synchronize-software-updates.md)。  

    -   必须将[应用程序](../../apps/deploy-use/create-applications.md)添加到 Configuration Manager 控制台。  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>创建可升级操作系统的任务序列  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“任务序列” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建任务序列”  以启动创建任务序列向导。  

4.  在“创建新的任务序列”  页上，单击“从升级包升级操作系统” ，然后单击“下一步” 。  

5.  在“任务序列信息”  页上，指定以下设置，然后单击“下一步” 。  

    -   **任务序列名称**：指定用于标识任务序列的名称。  

    -   “说明”：指定任务序列所执行的任务的描述。  

6.  在“升级 Windows 操作系统”  页上，指定以下设置，然后单击“下一步” 。  

    -   “升级包”：指定包含操作系统升级源文件的升级包。 你可以通过查看“属性”  窗格中的信息来验证你是否选择了正确的升级包。 有关详细信息，请参阅[管理操作系统升级包](../get-started/manage-operating-system-upgrade-packages.md)。  

    -   “版本索引”：如果包中有多个操作系统版本索引可用，请选择所需的版本索引。 默认情况下，选择第一项。  

    -   “产品秘钥”：指定要安装的 Windows 操作系统的产品密钥。 你可以指定编码的批量许可证密钥和标准产品密钥。 如果使用非编码的产品密钥，则必须通过短划线 (-) 分隔每组 5 个字符。 例如： *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*。 当对批量许可证版本进行升级时，不需要产品密钥。 仅对零售 Windows 版本进行升级时，才需要产品密钥。  

    -   **忽略任何可拒绝的兼容性消息**：如果要升级到 Windows Server 2016，请选择此设置。 如果不选择此设置，则任务序列无法完成，因为 Windows 安装程序正等待用户在“Windows 应用兼容性”对话框上单击“确认”。   

7.  在“包括更新”  页上，指定是安装必需的软件更新、所有软件更新还是不安装软件更新，然后单击“下一步” 。 如果指定要安装软件更新，Configuration Manager 将只会安装以包含目标计算机的集合为目标的那些软件更新。  

8.  在“安装应用程序”  页上，指定要安装在目标计算机上的应用程序，然后单击“下一步” 。 如果指定多个应用程序，你也可以指定任务序列在特定应用程序的安装失败时继续进行。  

9. 完成向导。  



## <a name="configure-pre-cache-content"></a>配置预先缓存内容
从版本 1702 开始，对于任务序列的可用部署，可选择使用预先缓存功能，让客户端在用户安装内容之前仅下载相关内容。
> [!TIP]  
> 在 1702 版本中引入，预先缓存是一项预发行功能。 若要启用此功能，请参阅[使用更新中的预发行功能](/sccm/core/servers/manage/pre-release-features)。

例如，假设要部署 Windows 10 就地升级任务序列，只想为所有用户提供单个任务序列，并且具有多个体系结构和/或语言。 在版本 1702 之前，如果创建可用部署，然后用户在软件中心中单击“安装”，则将在此时下载内容。 这在安装准备启动之前增加了额外时间。 另外，将下载任务序列中引用的所有内容。 这包括所有语言和体系结构的操作系统升级包。 如果每个包大小都约为 3 GB，则下载包可能会很大。

借助预先缓存内容，用户可选择允许客户端在收到部署后立即下载适用的内容。 因此，当用户在软件中心中单击“安装”时，内容便已就绪，并且安装可以快速启动，因为内容位于本地硬盘上。

### <a name="to-configure-the-pre-cache-feature"></a>配置预先缓存功能

1. 为特定体系结构和语言创建操作系统升级包。 在包的“数据源”选项卡上指定体系结构和语言。 对于语言，使用十进制转换（例如，英语的十进制为 1033，其十六进制等效项是 0x0409）。 有关详细信息，请参阅[创建用于升级操作系统的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)。

    体系结构和语言值用于匹配将在下一步中创建的任务序列步骤条件，以确定是否应预先缓存操作系统升级包。
2. 为不同的语言和体系结构创建具有条件步骤的任务序列。 例如，对于英语版本，可创建如下所示的步骤：

    ![预先缓存属性](../media/precacheproperties2.png)

    ![预先缓存选项](../media/precacheoptions2.png)  

3. 部署任务序列。 对于预先缓存功能，请配置以下各项：
    - 在“常规”选项卡上，选择“此任务序列的预下载内容”。
    - 在“部署设置”选项卡上，配置任务序列，将“目的”配置为“可用”。 如果创建**所需**部署，预先缓存功能将不起作用。
    - 在“计划”选项卡上，对于“当此部署可用时进行计划”设置，选择将来的某一时间，以便在部署对用户可用之前为客户端提供足够的时间来预先缓存内容。 例如，可将可用时间设置为未来 3 小时，以便有足够的时间来预先缓存内容。  
    - 在“分发点”选项卡上，配置“部署选项”设置。 如果用户开始安装之前，该内容未预先缓存到客户端，则使用这些设置。


### <a name="user-experience"></a>用户体验
- 客户端收到部署策略时，将开始预先缓存内容。 这包括所有引用的内容（任何其他包类型），并且仅包括基于任务序列中设置的条件匹配客户端的操作系统升级包。
- 部署对用户可用时（部署的“计划”选项卡上的设置），将显示一条通知，告知用户有关新部署的信息以及该部署在软件中心中可见。 用户可转到软件中心并单击“安装”以开始安装。
- 如果内容未完全预先缓存，则它将使用部署的“部署选项”选项卡上指定的设置。 建议在创建部署和用户可使用部署之间保留足够的时间，以允许客户端预先缓存内容。



## <a name="download-package-content-task-sequence-step"></a>下载包内容的任务序列步骤  
 在以下方案中，可先使用[下载包内容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)步骤，再使用升级操作系统步骤：  

-   你想要使用可用于 x86 和 x64 平台的单一升级任务序列。 为了实现这一目的，在“升级准备”  组中包括两个“下载包内容”  步骤，以及检测客户端体系结构的条件和仅下载相应操作系统升级包的条件。 将每个“下载包内容”步骤配置为使用相同的变量，并将该变量用于“升级操作系统”步骤的媒体路径。  

-   若要动态下载适用的驱动程序包，请使用两个“下载包内容”步骤以及检测每个驱动程序包的相应硬件类型的条件。 将每个“下载包内容”  步骤配置为使用相同的变量，并将该变量用于“升级操作系统”  步骤的驱动程序部分中的“分步内容”  值。  

   > [!NOTE]
   > 当有多个包时，Configuration Manager 会向变量名称中添加数字后缀。 例如，如果指定变量 %mycontent% 作为自定义变量，它就是用于存储所有引用内容（可以是多个包）的根目录。 当引用子序列步骤中的变量时（如升级操作系统），会为该变量添加数字后缀。 在本例中，%mycontent01% 或 %mycontent02%，其中的数字对应于包在此步骤中列出的顺序。

## <a name="optional-post-processing-task-sequence-steps"></a>可选的后续处理任务序列步骤  
 创建任务序列后，你可以添加其他步骤以卸载具有已知兼容性问题的应用程序，也可以添加要在重启电脑并成功升级到 Windows 10 后运行的后续处理操作。 在任务序列的后续处理组中添加这些附加步骤。  

> [!NOTE]  
>  由于此任务序列不是线性的，因此，针对步骤的某些条件可能对任务序列的结果产生影响，具体取决于是否成功升级客户端计算机，或者是否必须将客户端计算机回滚到开始升级的操作系统版本。  

## <a name="optional-rollback-task-sequence-steps"></a>可选的回滚任务序列步骤  
 当重启计算机后升级过程出现问题时，安装程序会此升级回滚到以前的操作系统，并且任务序列将继续执行回滚组中的任何步骤。 创建任务序列后，你可以将可选步骤添加到回滚组。  

## <a name="folder-and-files-removed-after-computer-restart"></a>重启计算机后删除文件夹和文件  
 用于将操作系统升级到 Windows 10 的任务序列和任务序列中的所有其他步骤完成后，重启计算机后将删除后处理和回滚脚本。  这些脚本文件不包含敏感信息。  
