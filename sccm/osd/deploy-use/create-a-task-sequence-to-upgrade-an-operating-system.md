---
title: 创建 OS 升级任务序列
titleSuffix: Configuration Manager
description: 使用任务序列自动从 Windows 7 或更高版本升级到 Windows 10
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6054ce9c276c18e578315b92fbe3d100061795fa
ms.sourcegitcommit: e2e07d74779a2f48693ecaa17a5974204949d109
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999418"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>在 Configuration Manager 中创建任务序列来升级操作系统

*适用范围：System Center Configuration Manager (Current Branch)*

在 Configuration Manager 中使用任务序列，自动升级目标计算机上的 OS。 可以从 Windows 7 或更高版本升级到 Windows 10，或从 Windows Server 2012 或更高版本升级到 Windows Server 2016。 创建一个任务序列，该任务序列引用要安装的 OS 升级包和任何其他内容，如应用程序或软件更新。 用于升级 OS 的任务序列是[将 Windows 升级到最新版本](upgrade-windows-to-the-latest-version.md)方案的一部分。  


## <a name="prerequisites"></a>先决条件

在创建任务序列之前，必须满足以下要求：

### <a name="required"></a>必需

- [OS 升级包](/sccm/osd/get-started/manage-operating-system-upgrade-packages)必须在 Configuration Manager 控制台中可用。  

- 升级到 Windows Server 2016 时，请在“升级操作系统”任务序列步骤中选择“忽略任何可拒绝的兼容性消息”  。 否则，升级将失败。  

### <a name="required-if-used"></a>必需（若使用）  

- 必须在 Configuration Manager 控制台中同步[软件更新](/sccm/sum/get-started/synchronize-software-updates)。  

- 必须将[应用程序](/sccm/apps/deploy-use/create-applications)添加到 Configuration Manager 控制台。  


## <a name="BKMK_UpgradeOS"></a> 创建用于升级 OS 的任务序列  

若要升级客户端上的 OS，请创建一个任务序列，并在“创建任务序列向导”中选择“通过升级包升级操作系统”  。 该向导添加任务序列步骤，用于升级 OS、应用软件更新和安装应用程序。

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“任务序列”    。  

2. 在功能区的“主页”选项卡上的“创建”组中，选择“创建任务序列”    。  

3. 在创建任务序列向导的“创建新的任务序列”页上，选择“通过升级包升级操作系统”，然后选择“下一步”    。  

4. 在“任务序列信息”页上，指定以下设置  ：  

    - “任务序列名称”  ：指定用于标识任务序列的名称。  

    - **描述**：（可选）指定描述。  

5. 在“升级 Windows 操作系统”页上，指定以下设置  ：  

    - **升级包**：指定包含 OS 升级源文件的升级包。 可以通过查看“属性”窗格中的信息来验证是否选择了正确的升级包  。 有关详细信息，请参阅[管理 OS 升级包](/sccm/osd/get-started/manage-operating-system-upgrade-packages)。  

    - **版本索引**：如果包中有多个 OS 版本索引可用，请选择所需的版本索引。 默认情况下，该向导会选择第一个索引。  

    - **产品密钥**：指定要安装的 OS 的 Windows 产品密钥。 请指定编码的批量许可证密钥或标准产品密钥。 如果使用标准产品密钥，请用短划线 (`-`) 将每五个字符分隔为一组。 例如： `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`。 在对批量许可证版本进行升级时，则可能不需要产品密钥。  

        > [!Note]  
        > 此产品密钥可以是多次激活密钥 (MAK) 或通用批量授权密钥 (GVLK)。 GVLK 也叫密钥管理服务 (KMS) 客户端安装密钥。 有关详细信息，请参阅[规划批量激活](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)。 如需 KMS 客户端设置密钥的列表，请参阅 Windows Server 激活指南的[附录 A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。

    - **忽略任何可拒绝的兼容性消息**：如果要升级到 Windows Server 2016，请选择此设置。 如果不选择此设置，则任务序列无法完成，因为 Windows 安装程序正等待用户在“Windows 应用兼容性”对话框上选择“确认”  。  

6. 在“包括更新”页上，指定是安装必需、全部，还是不安装软件更新  。 然后选择“下一步”  。 如果指定要安装软件更新，则 Configuration Manager 仅安装以目标计算机所在的集合为目标的那些更新。  

7. 在“安装应用程序”  页上，指定要安装在目标计算机上的应用程序，然后选择“下一步”  。 如果指定多个应用程序，也请指定任务序列是否要在特定应用程序的安装失败时继续进行。  

8. 完成向导。  

> [!Important]  
> 在设备上运行任务序列时，Configuration Manager 客户端会创建多个脚本，用于控制各种方案中的任务序列行为。 任务序列完成后，客户端在计算机重启之前都不会删除这些脚本。 这些脚本文件不包含敏感信息。  

Windows 10 就地升级任务序列的默认模板包括其他组，其中包含要在升级过程前后添加的建议操作。 这些操作在许多将设备成功升级到 Windows 10 的客户之间是通用的。 有关详细信息，请参阅建议的任务序列步骤以[准备升级](#recommended-task-sequence-steps-to-prepare-for-upgrade)和[进行后期处理](#recommended-task-sequence-steps-for-post-processing)。

从版本 1806 开始，此任务序列模板还包括在升级过程失败的情况下要添加的带建议操作的组。 这些操作有助于进行故障排除。 有关详细信息，请参阅[在失败情况下推荐的任务序列步骤](#recommended-task-sequence-steps-on-failure)。<!--1358500-->  


## <a name="configure-pre-cache-content"></a>配置预先缓存内容

<!--1021244-->
对于任务序列的可用部署，可使用预先缓存功能让客户端在用户安装任务序列之前下载相关 OS 升级包内容。  

有关详细信息，请参阅[配置预缓存内容](/sccm/osd/deploy-use/configure-precache-content)。


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>准备升级的建议任务序列步骤

Windows 10 就地升级的默认任务序列模板包括在升级过程前要添加的带建议操作的其他组。 “准备升级”组中的这些操作在许多将设备成功升级到 Windows 10 的客户之间是通用的  。 如果你具有尚未执行这些操作的现有任务序列, 请在 "**准备升级**" 组中将其手动添加到任务序列中。  

### <a name="battery-checks"></a>电池检查

在此组中添加步骤，检查计算机是在使用电池还是有线电源。 此操作需要自定义脚本或实用工具来执行此检查。

#### <a name="battery-check-example"></a>电池检查示例

使用 WbemTest 并连接到`root\cimv2`命名空间。 然后运行以下查询：

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

如果返回任何结果，则设备是依靠电池运行的。 否则，设备将连接到有线电源。  

### <a name="networkwired-connection-checks"></a>网络/有线连接检查

在此组中添加步骤，检查计算机是否已连接到网络，以及是否未使用无线连接。 此操作需要自定义脚本或实用工具来执行此检查。

#### <a name="network-check-example"></a>网络检查示例

使用 WbemTest 并连接到`root\cimv2`命名空间。 然后运行以下查询：

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

如果返回任何结果，则设备是依靠 Wi-Fi 运行的。 否则，设备将连接到有线网络连接。

### <a name="remove-incompatible-applications"></a>删除不兼容的应用程序

在此组中添加步骤，删除任何与此版本的 Windows 10 不兼容的应用程序。 卸载应用程序的方法不同。  

如果应用程序使用 Windows Installer，则从应用程序的 Windows Installer 部署类型属性上的“程序”  选项卡中复制“卸载程序”  命令行。 然后在此组中添加“运行命令行”  步骤，并附加卸载程序命令行。 例如：

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>删除不兼容的驱动程序

在此组中添加步骤，删除任何与此版本的 Windows 10 不兼容的驱动程序。  

### <a name="removesuspend-third-party-security"></a>删除/暂停第三方安全程序

在此组中添加步骤，删除或暂停防病毒程序等第三方安全程序。  

如果使用的是第三方磁盘加密程序，请为 Windows 安装程序的加密驱动程序提供 `/ReflectDrivers` [命令行选项](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#23)。 在此组的任务序列中添加[设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)步骤。 将任务序列变量设置为“OSDSetupAdditionalUpgradeOptions”  。 将值设置为 `/ReflectDrivers`，并附加驱动程序的路径。 此[任务序列变量](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions)附加了任务序列使用的 Windows 安装程序命令行。 请联系你的软件供应商，以获得有关此进程的任何其他指导。  

### <a name="download-package-content-task-sequence-step"></a>下载包内容的任务序列步骤  

在以下方案中，可先使用[下载包内容](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent)步骤，再使用“升级操作系统”步骤  ：  

- 使用可用于 x86 和 x64 平台的单一升级任务序列。 包括“准备升级”组中的两个“下载包内容”步骤   。 在每个步骤上设置条件，检测客户端体系结构。 此条件可使该步骤仅下载相应的 OS 升级包。 将每个“下载包内容”  步骤配置为使用相同的变量，并将该变量用于“升级操作系统”  步骤的媒体路径。  

- 若要动态下载适用的驱动程序包，请使用两个“下载包内容”  步骤以及检测每个驱动程序包的相应硬件类型的条件。 配置每个“下载包内容”步骤，使其使用相同的变量  。 然后将该变量用于“升级操作系统”步骤上驱动程序部分中的“预留内容”变量   。  

    > [!NOTE]  
    > Configuration Manager 向此变量名称中添加数字后缀。 例如，若将 `%mycontent%` 指定为自定义变量，客户端会将所有引用内容存储在此位置。 当引用后续步骤（如“升级操作系统”）中的变量时，请使用带数字后缀的变量  。 在本示例中，使用 `%mycontent01%` 或 `%mycontent02%`，其中编号对应于“下载包内容”步骤列出此特定内容的顺序  。  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>后期处理的建议任务序列步骤

创建任务序列后，在任务序列的“后期处理”组中添加其他步骤  。  

> [!NOTE]  
> 此任务序列不是线性的。 步骤中存在可能影响任务序列结果的条件。 此行为取决于是否成功升级客户端计算机，或是否必须将客户端计算机回滚到原始 OS。  

Windows 10 就地升级的默认任务序列模板包括在升级过程后要添加的带建议操作的其他组。 “后期处理”组中的这些操作在许多将设备成功升级到 Windows 10 的客户之间是通用的  。 如果你具有尚未执行这些操作的现有任务序列, 请在**后期处理**组中将其手动添加到任务序列中。  

### <a name="apply-setup-based-drivers"></a>应用基于设置的驱动程序

在此组中添加步骤，从包中安装基于设置的驱动程序(.exe)。  

### <a name="installenable-third-party-security"></a>安装/启用第三方安全程序

在此组中添加步骤，安装或启用防病毒程序等第三方安全程序。  

### <a name="set-windows-default-apps-and-associations"></a>设置 Windows 默认应用和关联

在此组中添加步骤，设置 Windows 默认应用和文件关联。

1. 准备一台具备所需应用关联的参考计算机。
1. 运行以下导出命令行：  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. 将 XML 文件添加到包。
1. 在此组中添加[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)步骤。 指定包含 XML 文件的包，然后指定以下命令行：  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

有关详细信息，请参阅[导出或导入默认的应用关联](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)。

### <a name="apply-customizations-and-personalization"></a>应用自定义项和个性化设置

在此组中添加步骤，应用整理程序组等“开始”菜单自定义项。 有关详细信息，请参阅[自定义“开始”屏幕](/windows-hardware/manufacture/desktop/customize-the-start-screen)。  


## <a name="optional-task-sequence-steps-for-rollback"></a>回滚的可选任务序列步骤  

如果重启计算机后升级过程出现问题，Windows 安装程序会将系统回滚到以前的 OS。 然后，任务序列继续执行“回滚”组中的任何步骤  。 创建任务序列后，请在必要时在此组中添加可选步骤。 例如，撤消在“准备升级”组中对系统所做的任何更改，例如卸载不兼容的软件。


## <a name="recommended-task-sequence-steps-on-failure"></a>在失败情况下推荐的任务序列步骤

<!--1358500-->
从版本 1806 开始，Windows 10 就地升级的默认任务序列模板包括一个“如果失败，则运行操作”的组  。 此组包括在升级失败时要添加的推荐操作。 这些操作有助于进行故障排除。

### <a name="collect-logs"></a>收集日志

若要从客户端中收集日志，请在此组中添加步骤。  

- 一种常见的做法是将日志文件复制到网络共享中。 若要建立此连接，请使用[连接到网络文件夹](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)步骤。  

- 若要执行复制操作，请通过[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)或[运行 PowerShell 脚本](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript)步骤来使用自定义脚本或实用工具。  

- 要收集的文件可能包括以下日志：  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- 有关 Setupact.log 和其他 Windows 安装程序日志的详细信息，请参阅 [Windows 安装程序日志文件](https://docs.microsoft.com/windows/deployment/upgrade/log-files)。  

- 有关 Configuration Manager 客户端日志的详细信息，请参阅 [Configuration Manager 客户端日志](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs)。  

- 有关 _SMSTSLogPath  和其他有用变量的详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables)。  

### <a name="run-diagnostic-tools"></a>运行诊断工具

若要运行其他诊断工具，请在此组中添加步骤。 请自动运行这些工具，以便在出现故障后立即收集系统中的其他信息。  

其中一个工具是 Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag)。 它是一个独立的诊断工具，可获取有关 Windows 10 升级失败原因的详细信息。  

- 在 Configuration Manager 中，[创建工具包](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program)。  

- 向该组任务序列添加[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)步骤。 使用“包”  选项来引用该工具。 以下字符串是一个示例命令行  ：  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`  


## <a name="additional-recommendations"></a>其他建议

### <a name="windows-documentation"></a>Windows 文档

查看 Windows 文档，以[解决 Windows 10 升级错误](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)。 本文还包含了关于升级过程的详细信息。  

### <a name="check-minimum-disk-space"></a>检查最小磁盘空间

在默认的“检查准备情况”  步骤中，启用“确保最小可用磁盘空间 (MB)”  。 对于 32 位 OS 升级包，将值设置为至少 16384  (16 GB)，对于 64 位设置为至少 20480  (20 GB)。  

### <a name="retry-downloading-policy"></a>重试下载策略

使用 SMSTSDownloadRetryCount  [任务序列变量](/sccm/osd/understand/task-sequence-variables#SMSTSDownloadRetryCount)重试下载策略。 当前在默认情况下，客户端重试两次；此变量设置为二 (2)。 如果客户端未连接到有线的 Intranet 网络，额外的重试会帮助客户端获得策略。 使用该变量不会产生负面的副作用，除了因无法下载策略导致的延迟故障。<!--501016--> 此外，也可以增加“SMSTSDownloadRetryDelay”  变量的值（默认值为 15 秒）。  

### <a name="perform-an-inline-compatibility-assessment"></a>执行内联兼容性评估

1. 在“准备升级”  组中提前添加第二个“升级操作系统”  步骤。  

    1. 将其命名为“升级评估”  。
    1. 指定相同的升级包，然后启用选项“不启动升级即执行 Windows 安装程序兼容性扫描”  。
    1. 启用“选项”选项卡上的“出错时继续”  。  

1. 紧跟此“升级评估”  步骤，添加“运行命令行”  步骤。 指定以下命令行：

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

1. 在“选项”  选项卡上，添加以下条件：

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

此返回代码为 MOSETUP_E_COMPAT_SCANONLY (0xC1900210) 的等效十进制数，表示不存在任何问题的成功兼容性扫描。 如果“升级评估”步骤成功并返回此代码，任务序列会跳过此步骤  。 否则，如果评估步骤返回任何其他返回代码，则此步骤的任务序列将失败，并会从 Windows 安装程序兼容性扫描中返回代码。 有关 _SMSTSOSUpgradeActionReturnCode  的详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode)。

有关详细信息，请参阅[升级操作系统](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)。  

### <a name="convert-from-bios-to-uefi"></a>从 BIOS 转换为 UEFI

如果要在此任务序列过程中将设备从 BIOS 更改为 UEFI，请参阅[在就地升级过程中从 BIOS 转换为 UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)。  

### <a name="manage-bitlocker"></a>管理 BitLocker

<!--SCCMDocs issue #494-->
如果使用 BitLocker 磁盘加密，则在默认情况下 Windows 安装程序会在升级期间自动将它暂停。 从 Windows 10 版本 1803 开始，Windows 安装程序包括了 `/BitLocker` 命令行参数，以便控制此行为。 如果安全要求需要磁盘加密全程保持活动状态，请使用“准备升级”  组中的 OSDSetupAdditionalUpgradeOptions  [任务序列变量](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions)来包含 `/BitLocker TryKeepActive`。 有关详细信息，请参阅 [Windows 安装程序命令行选项](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#33)。

### <a name="remove-default-apps"></a>删除默认应用

<!--SCCMDocs issue #526-->
部分客户删除了 Windows 10 中默认预配的应用。 例如，必应天气应用或 Microsoft Solitaire Collection。 在某些情况下，这些应用会在 Windows 10 后重新出现。 有关详细信息，请参阅[如何从 Windows 10 中彻底删除应用](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update)。

向“准备升级”组中的任务序列添加“运行命令行”步骤   。 指定类似以下示例的命令行：

`cmd /c reg delete "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
