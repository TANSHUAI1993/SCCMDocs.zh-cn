---
title: "创建用于升级操作系统的任务序列"
titleSuffix: Configuration Manager
description: "System Center Configuration Manager 中的任务序列可自动将操作系统从 Windows 7 或更高版本升级到 Windows 10。"
ms.custom: na
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: "12"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 058b0710484a0452ddf19655bf2cabbb43f624ad
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>创建任务序列来升级 System Center Configuration Manager 中的操作系统

*适用范围：System Center Configuration Manager (Current Branch)*

在 Configuration Manager 中使用任务序列，自动升级目标计算机上的操作系统。 可以从 Windows 7 或更高版本升级到 Windows 10，或从 Windows Server 2012 或更高版本升级到 Windows Server 2016。 创建一个任务序列，该任务序列引用要安装的操作系统升级包和任何其他内容，如应用程序或软件更新。 用于升级操作系统的任务序列属于[将 Windows 升级到最新版本](upgrade-windows-to-the-latest-version.md)方案的一部分。  

##  <a name="BKMK_UpgradeOS"></a>创建用于升级操作系统的任务序列  
 若要升级计算机上的操作系统，可以创建一个任务序列，并在“创建任务序列向导”中选择“通过升级包升级操作系统”。 该向导将添加一些步骤，用于升级操作系统、应用软件更新和安装应用程序。 在创建任务序列之前，必须满足以下要求：    

-   **必需**  

     - [操作系统升级包](../get-started/manage-operating-system-upgrade-packages.md)必须在 Configuration Manager 控制台中可用。
     - 升级到 Windows Server 2016 时，请在“升级操作系统”任务序列步骤中选择“忽略任何可拒绝的兼容性消息”。 否则，升级将失败。

-   **必需（若使用）**  

    -   必须在 Configuration Manager 控制台中同步[软件更新](../../sum/get-started/synchronize-software-updates.md)。  

    -   必须将[应用程序](../../apps/deploy-use/create-applications.md)添加到 Configuration Manager 控制台。  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>创建可升级操作系统的任务序列  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”工作区中，展开“操作系统”，然后单击“任务序列”。  

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

7.  在“包括更新”  页上，指定是安装必需的软件更新、所有软件更新还是不安装软件更新，然后单击“下一步” 。 如果指定要安装软件更新，Configuration Manager 仅安装以目标计算机所在的集合为目标的那些软件更新。  

8.  在“安装应用程序”  页上，指定要安装在目标计算机上的应用程序，然后单击“下一步” 。 如果指定多个应用程序，你也可以指定任务序列在特定应用程序的安装失败时继续进行。  

9. 完成向导。  



## <a name="configure-pre-cache-content"></a>配置预先缓存内容
从版本 1702 开始，对于任务序列的可用部署，可使用预先缓存功能让客户端在用户安装任务序列之前仅下载相关内容。
> [!TIP]  
> 此功能在 1702 版本中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 从版本 1706 开始，此功能不再属于预发行功能。

例如，假设要部署 Windows 10 就地升级任务序列，只想为所有用户提供单个任务序列，并且具有多个体系结构和/或语言。 在以前的版本中，当用户从软件中心安装可用的任务序列部署时，就会开始下载内容。 此延迟在安装准备启动之前增加了额外时间。 另外，将下载任务序列中引用的所有内容。 此内容包括所有语言和体系结构的操作系统升级包。 如果每个升级包的大小约 3 GB，总内容也非常大。

借助预先缓存内容，用户可选择允许客户端在收到部署后立即下载适用的内容。 因此，当用户在软件中心中单击“安装”时，内容便已就绪，并且安装可以快速启动，因为内容位于本地硬盘上。

### <a name="to-configure-the-pre-cache-feature"></a>配置预先缓存功能

1. 为特定体系结构和语言创建操作系统升级包。 在包的“数据源”选项卡上指定体系结构和语言。 对于语言，使用十进制转换（例如，英语的十进制为 1033，其十六进制等效项是 0x0409）。 有关详细信息，请参阅[创建用于升级操作系统的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)。

    体系结构和语言值用于匹配任务序列步骤中的条件，以确定是否应预先缓存操作系统升级包。
1. 为不同的语言和体系结构创建具有条件步骤的任务序列。 例如，以下步骤使用英语版本：

    ![预先缓存属性](../media/precacheproperties2.png)

    ![预先缓存选项](../media/precacheoptions2.png)  

3. 部署任务序列。 对于预先缓存功能，请配置以下设置：
    - 在“常规”选项卡上，选择“此任务序列的预下载内容”。
    - 在“部署设置”选项卡上，配置任务序列，将“目的”配置为“可用”。
    - 在“计划”选项卡上，对于“当此部署可用时进行计划”设置，请选择当前所选时间。 客户端在部署的可用时间预先缓存内容。 目标客户端收到此策略时，可用时间是过去的时间，因此预先缓存下载会立即开始。 如果客户端收到此策略，但可用时间是将来的时间，则客户端不会开始预先缓存内容直到出现可用时间。 
    - 在“分发点”选项卡上，配置“部署选项”设置。 如果用户开始安装之前，该内容未预先缓存到客户端，则使用这些设置。


### <a name="user-experience"></a>用户体验
- 客户端收到部署策略时，将在部署的可用时间之后开始预先缓存内容。 此内容包括所有引用的包，并且根据任何序列中设置的条件，只有操作系统升级包与客户端匹配。
- 部署对用户可用时，将显示一条通知，告知用户有关新部署的信息以及任务序列在软件中心中可见。 用户可转到软件中心并单击“安装”以开始安装。
- 如果用户安装任务序列时内容未完全预先缓存，则客户端将使用部署的“部署选项”选项卡上指定的设置。 



## <a name="download-package-content-task-sequence-step"></a>下载包内容的任务序列步骤  
 在以下方案中，可先使用[下载包内容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)步骤，再使用升级操作系统步骤：  

-   使用可用于 x86 和 x64 平台的单一升级任务序列。 包括“准备升级”组中的两个“下载包内容”步骤。 在每个步骤上设置条件，检测客户端体系结构。 此条件可使该步骤仅下载相应的操作系统升级包。 将每个“下载包内容”步骤配置为使用相同的变量，并将该变量用于“升级操作系统”步骤的媒体路径。  

-   若要动态下载适用的驱动程序包，请使用两个“下载包内容”步骤以及检测每个驱动程序包的相应硬件类型的条件。 配置每个“下载包内容”步骤，使其使用相同的变量。 然后将该变量用于“升级操作系统”步骤上驱动程序部分中的“预留内容”变量。  

   > [!NOTE]
   > 当有多个包时，Configuration Manager 会向变量名称中添加数字后缀。 例如，如果将变量 %mycontent% 指定为自定义变量，此位置为客户端存储所有引用的内容的位置。 当引用后续步骤（如“升级操作系统”）中的变量时，请使用带数字后缀的变量。 在本例中，使用 %mycontent01% 或 %mycontent02%，其中编号对应于“下载包内容”步骤列出此特定内容的顺序。

## <a name="optional-post-processing-task-sequence-steps"></a>可选的后续处理任务序列步骤  
 创建任务序列后，必要时可添加其他步骤。 例如，卸载具有已知兼容性问题的应用程序时，或在重启计算机并成功升级到 Windows 10 后添加要运行的后续处理操作时。 在任务序列的后续处理组中添加这些附加步骤。  

> [!NOTE]  
>  由于此任务序列不是线性的，因此，针对步骤的某些条件可能对任务序列的结果产生影响，具体取决于是否成功升级客户端计算机，或者是否必须将客户端计算机回滚到开始升级的操作系统版本。  

## <a name="optional-rollback-task-sequence-steps"></a>可选的回滚任务序列步骤  
 如果重启计算机后升级过程出现问题，Windows 安装程序会将升级回滚到以前的操作系统。 然后，任务序列将继续执行回滚组中的任何步骤。 创建任务序列后，你可以将可选步骤添加到回滚组。  

## <a name="folder-and-files-removed-after-computer-restart"></a>重启计算机后删除文件夹和文件  
 任务序列完成后，除非重启计算机，否则客户端不会删除后处理和回滚脚本。 这些脚本文件不包含敏感信息。  
