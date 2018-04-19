---
title: 创建 OS 升级任务序列
titleSuffix: Configuration Manager
description: 使用任务序列自动从 Windows 7 或更高版本升级到 Windows 10
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 48a5e7aa381924e3c0ad052833c9588e3dffa4f5
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>创建任务序列来升级 System Center Configuration Manager 中的操作系统

*适用范围：System Center Configuration Manager (Current Branch)*

在 Configuration Manager 中使用任务序列，自动升级目标计算机上的操作系统。 可以从 Windows 7 或更高版本升级到 Windows 10，或从 Windows Server 2012 或更高版本升级到 Windows Server 2016。 创建一个任务序列，该任务序列引用要安装的 OS 升级包和任何其他内容，如应用程序或软件更新。 用于升级操作系统的任务序列属于[将 Windows 升级到最新版本](upgrade-windows-to-the-latest-version.md)方案的一部分。  



##  <a name="BKMK_UpgradeOS"></a>创建用于升级操作系统的任务序列  
 若要升级计算机上的操作系统，可以创建一个任务序列，并在“创建任务序列向导”中选择“通过升级包升级操作系统”。 该向导添加任务序列步骤，用于升级操作系统、应用软件更新和安装应用程序。 在创建任务序列之前，必须满足以下要求：    

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

7.  在“包括更新”页上，指定是安装必需、全部，还是不安装软件更新。 然后单击 **“下一步”**。 如果指定要安装软件更新，Configuration Manager 仅安装以目标计算机所在的集合为目标的那些软件更新。  

8.  在“安装应用程序”  页上，指定要安装在目标计算机上的应用程序，然后单击“下一步” 。 如果指定多个应用程序，你也可以指定任务序列在特定应用程序的安装失败时继续进行。  

9. 完成向导。  


 > [!Important] 
 > 任务序列完成后，除非重启计算机，否则客户端不会删除后处理和回滚脚本。 这些脚本文件不包含敏感信息。  


 > [!Note]
 > 从版本 1802 开始，Windows 10 就地升级的默认任务序列模板包括在升级过程前后要添加的带建议操作的其他组。 这些操作在许多将设备成功升级到 Windows 10 的客户之间是通用的。 有关详细信息，请参阅建议的任务序列步骤以[准备升级](#recommended-task-sequence-steps-to-prepare-for-upgrade)和[进行后期处理](#recommended-task-sequence-steps-for-post-processing)。



## <a name="configure-pre-cache-content"></a>配置预先缓存内容
<!--1021244-->
对于任务序列的可用部署，可使用预先缓存功能让客户端在用户安装任务序列之前下载相关 OS 升级包内容。  

> [!TIP]  
> 此功能在 1702 版本中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 从版本 1706 开始，此功能不再属于预发行功能。  


> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此选项。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  


例如，仅需为所有用户提供就地升级任务序列，并拥有许多体系结构和语言。 在以前的版本中，当用户从软件中心安装可用的任务序列部署时，就会开始下载内容。 此延迟在安装准备启动之前增加了额外时间。 将下载任务序列中引用的所有内容。 此内容包括所有语言和体系结构的操作系统升级包。 如果每个升级包的大小约 3 GB，总内容也非常大。

借助预先缓存内容，用户可选择允许客户端在收到部署后，立即下载适用的 OS 升级包以及引用的所有其他内容。 用户在软件中心内单击“安装”时，内容便已就绪，并且安装可以快速启动，因为内容位于本地硬盘上。

 > [!NOTE]
 > 此行为目前仅适用于 OS 升级包。 该包是你指定匹配体系结构或语言的唯一内容。 例如，如果任务序列还引用多个驱动程序包，则客户端当前会下载所有驱动程序包。 任务序列引擎在运行任务序列时（而不是提前）评估步骤条件。 客户端使用包属性上的标记来确定要预缓存的内容。

### <a name="to-configure-the-pre-cache-feature"></a>配置预先缓存功能

1. 为特定体系结构和语言创建 OS 升级包。 在包的“数据源”选项卡上指定体系结构和语言。 对于该语言，请使用十进制转换。 例如，英语的十进制值为 1033，其十六进制等效值是 0x0409。

    客户端评估体系结构和语言值，以确定在预缓存期间下载的 OS 升级包。

1. 为不同的语言和体系结构创建具有条件步骤的任务序列。 例如，以下步骤使用英语版本：

    ![显示 ENU、DEU 和 JPN 的多个升级 OS 步骤的任务序列编辑器](../media/precacheproperties2.png)

    ![任务序列编辑器，“选项”选项卡，显示区域设置和 OSArchitecture 的 WMI WQL 查询](../media/precacheoptions2.png)  

3. 部署任务序列。 对于预先缓存功能，请配置以下设置：
    - 在“常规”选项卡上，选择“此任务序列的预下载内容”。
    - 在“部署设置”选项卡上，配置任务序列，将“目的”配置为“可用”。
    - 在“计划”选项卡上，对于“当此部署可用时进行计划”设置，请选择当前所选时间。 客户端在部署的可用时间预先缓存内容。 目标客户端收到此策略时，可用时间是过去的时间，因此预先缓存下载会立即开始。 如果客户端收到此策略，但可用时间是将来的时间，则客户端不会开始预先缓存内容直到出现可用时间。 
    - 在“分发点”选项卡上，配置“部署选项”设置。 如果用户开始安装前未预缓存该内容，则客户端使用这些设置。
  

### <a name="user-experience"></a>用户体验
- 客户端收到部署策略时，将在部署的可用时间之后开始预缓存内容。 此内容包含引用的所有包，但仅包含与包上的体系结构和语言属性相匹配的 OS 升级包。
- 当客户端使部署可供用户使用时，将显示一条通知，告知用户有关新部署的信息。 现在，任务序列在软件中心内可见。 用户可转到软件中心并单击“安装”以开始安装。
- 如果用户安装任务序列时内容未完全预先缓存，则客户端将使用部署的“部署选项”选项卡上指定的设置。 



## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>准备升级的建议任务序列步骤

从版本 1802 开始，Windows 10 就地升级的默认任务序列模板包括在升级过程前要添加的带建议操作的其他组。 “准备升级”组中的这些操作在许多将设备成功升级到 Windows 10 的客户之间是通用的。 对于 1802 之前版本的站点，请手动将这些操作添加到“准备升级”组中的任务序列中。
- 电池检查：在此组中添加步骤，以检查计算机使用的是电池还是有线电源。 此操作需要自定义脚本或实用工具来执行此检查。
- 网络/有线连接检查：在此组中添加步骤，以检查计算机是否已连接到网络，并且未使用无线连接。 此操作需要自定义脚本或实用工具来执行此检查。
- 删除不兼容的应用程序：在此组中添加步骤，以删除与此版本的 Windows 10 不兼容的任何应用程序。 卸载应用程序的方法不同。 如果应用程序使用 Windows Installer，则从应用程序的 Windows Installer 部署类型属性上的“程序”选项卡中复制“卸载程序”命令行。 然后在此组中添加“运行命令行”步骤，并附加卸载程序命令行。 例如： </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- 删除不兼容的驱动程序：在此组中添加步骤，以删除与此版本的 Windows 10 不兼容的任何驱动程序。
- 删除/暂停第三方安全程序：在此组中添加步骤，以删除或暂停第三方安全程序，如防病毒程序。
   - 如果你使用的是第三方磁盘加密程序，则可以为 Windows 安装程序的加密驱动程序提供 /ReflectDrivers [命令行选项](/windows-hardware/manufacture/desktop/windows-setup-command-line-options)。 在此组的任务序列中添加[设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)步骤。 将任务序列变量设置为“OSDSetupAdditionalUpgradeOptions”。 将值设置为“/ReflectDriver”，并附加驱动程序的路径。 此[任务序列操作变量](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system)附加了任务序列使用的 Windows 安装程序命令行。 请联系你的软件供应商，以获得有关此进程的任何其他指导。

### <a name="download-package-content-task-sequence-step"></a>下载包内容的任务序列步骤  
 在以下方案中，可先使用[下载包内容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)步骤，再使用升级操作系统步骤：  

-   使用可用于 x86 和 x64 平台的单一升级任务序列。 包括“准备升级”组中的两个“下载包内容”步骤。 在每个步骤上设置条件，检测客户端体系结构。 此条件可使该步骤仅下载相应的操作系统升级包。 将每个“下载包内容”步骤配置为使用相同的变量，并将该变量用于“升级操作系统”步骤的媒体路径。  

-   若要动态下载适用的驱动程序包，请使用两个“下载包内容”步骤以及检测每个驱动程序包的相应硬件类型的条件。 配置每个“下载包内容”步骤，使其使用相同的变量。 然后将该变量用于“升级操作系统”步骤上驱动程序部分中的“预留内容”变量。  

   > [!NOTE]
   > 当有多个包时，Configuration Manager 会向变量名称中添加数字后缀。 例如，如果将变量 %mycontent% 指定为自定义变量，此位置为客户端存储所有引用的内容的位置。 当引用后续步骤（如“升级操作系统”）中的变量时，请使用带数字后缀的变量。 在本例中，使用 %mycontent01% 或 %mycontent02%，其中编号对应于“下载包内容”步骤列出此特定内容的顺序。



## <a name="recommended-task-sequence-steps-for-post-processing"></a>后期处理的建议任务序列步骤   
 创建任务序列后，在任务序列的“后期处理”组中添加其他步骤。  

> [!NOTE]  
>  此任务序列不是线性的。 步骤中存在可能影响任务序列结果的条件。 此行为取决于是否成功升级客户端计算机，或是否必须将客户端计算机回滚到原始 OS。  

从版本 1802 开始，Windows 10 就地升级的默认任务序列模板包括在升级过程后要添加的带建议操作的其他组。 “后期处理”组中的这些操作在许多将设备成功升级到 Windows 10 的客户之间是通用的。 对于 1802 之前版本的站点，请手动将这些操作添加到“后期处理”组中的任务序列中。
- 应用基于安装程序的驱动程序：在此组中添加步骤，以从包中安装基于安装程序的驱动程序 (.exe)。
- 安装/启用第三方安全程序：在此组中添加步骤，以安装或启用第三方安全程序，如防病毒程序。 
- 设置 Windows 默认应用和关联：在此组中添加步骤，以设置 Windows 默认应用和文件关联。 首先要准备一台具备所需应用关联的参考计算机。 然后运行以下导出命令行： </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>将 XML 文件添加到包。 然后在此组中添加[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)步骤。 指定包含 XML 文件的包，然后指定以下命令行： </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> 有关详细信息，请参阅[导出或导入默认的应用关联](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)。
- 应用自定义和个性化：在此组中添加步骤以应用“开始”菜单自定义，如组织程序组。 有关详细信息，请参阅[自定义“开始”屏幕](/windows-hardware/manufacture/desktop/customize-the-start-screen)。



## <a name="optional-task-sequence-steps-for-rollback"></a>回滚的可选任务序列步骤  
 如果重启计算机后升级过程出现问题，Windows 安装程序会将升级回滚到以前的操作系统。 然后，任务序列继续执行“回滚”组中的任何步骤。 创建任务序列后，可在回滚组中添加可选步骤。 例如，撤消在“准备升级”组中对系统所做的任何更改，例如卸载不兼容的软件。



## <a name="additional-recommendations"></a>其他建议
- 查看 Windows 文档，以[解决 Windows 10 升级错误](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)。 本文还包含了关于升级过程的详细信息。
- 在默认的“检查准备情况”步骤中，启用“确保最小可用磁盘空间 (MB)”。 对于 32 位 OS 升级包，将值设置为至少 16384 (16 GB)，对于 64 位设置为至少 20480 (20 GB)。 
- 使用 SMSTSDownloadRetryCount [内置任务序列变量](/sccm/osd/understand/task-sequence-built-in-variables)重试下载策略。 当前在默认情况下，客户端重试两次；此变量设置为二 (2)。 如果客户端未连接到有线公司网络，额外的重试将帮助客户端获得策略。 使用该变量不会产生负面的副作用，如果不能下载策略，则会导致延迟失败。<!-- 501016 --> 此外，也可以增加“SMSTSDownloadRetryDelay”变量的值（默认值为 15 秒）。
- 执行内联兼容性评估。 
   - 在“准备升级”组中提前添加第二个“升级操作系统”步骤。 将其命名为“升级评估”。 指定相同的升级包，然后启用选项“不启动升级即执行 Windows 安装程序兼容性扫描”。 启用“选项”选项卡上的“出错时继续”。 
   - 紧跟此“升级评估”步骤，添加“运行命令行”步骤。 指定以下命令行：</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>在“选项”选项卡上，添加以下条件： </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>此返回代码为 MOSETUP_E_COMPAT_SCANONLY (0xC1900210) 的等效十进制数，表示不存在任何问题的成功兼容性扫描。 如果“升级评估”步骤成功并返回此代码，则跳过此步骤。 否则，如果评估步骤返回任何其他返回代码，则此步骤的任务序列将失败，并会从 Windows 安装程序兼容性扫描中返回代码。
   - 有关详细信息，请参阅[升级操作系统](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)。
- 如果要在此任务序列过程中将设备从 BIOS 更改为 UEFI，请参阅[在就地升级过程中从 BIOS 转换为 UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)。
