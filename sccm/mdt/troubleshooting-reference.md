---
title: MDT 疑难解答
titleSuffix: Microsoft Deployment Toolkit
description: 'Microsoft Deployment Toolkit 的疑难解答参考 '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 91a7a69a-deac-4b0f-aac9-b7bd187c53fb
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: efb65086878a46bfb3485fdd8b0be6f613225261
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2018
ms.locfileid: "27821011"
---
# <a name="troubleshooting-reference-for-the-microsoft-deployment-toolkit"></a>Microsoft Deployment Toolkit 的疑难解答参考
 部署操作系统和应用程序以及迁移用户状态可能极具挑战性，即使是在具备相应工具和指南的情况下。 此参考随附 Microsoft® Deployment Toolkit (MDT) 2013 一并提供，其中列出当前的已知问题、其可能的解决方法以及疑难解答指南。  

> [!NOTE]
>  本文档中的 Windows 适用于 Windows 8.1、Windows 8、Windows 7、Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 操作系统，除非另行说明。 MDT 不支持基于 ARM 处理器的 Windows 版本。 同样，MDT 指 MDT 2013，除非另行说明。  

> [!NOTE]
>  Microsoft 诊断和恢复工具集 (DaRT) 包含一些强大的工具，可用于排查客户端不启动或变得不稳定的问题并进行恢复。 DaRT 可用于确定崩溃的原因和还原丢失的文件等。 此外，DaRT 还可用作开发和部署 Windows 操作系统时的故障排除工具。 例如，如果生成的映像无法正常启动，可使用诊断环境 ERD Commander 启动包含此映像的客户端计算机。 然后，可浏览客户端计算机的硬盘、查看事件日志、删除更新和更改操作系统设置等。 DaRT 是 Microsoft Desktop Optimization Pack for Software Assurance 的一部分。 若要了解有关 DaRT 的详细信息，请参阅 [http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx](http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx)。  

## <a name="understanding-logs"></a>日志介绍  
 必须先清晰了解操作系统部署期间使用的多个 .log 文件，才能有效地排查 MDT 的问题。 如果明确在何时搜索哪个日志文件查找哪个故障状况，曾经神秘而难解的问题可能就变得清晰易懂了。  

 MDT 日志文件格式设计专由 Trace32 读取，Trace32 是 System Center Configuration Manager 2007 Toolkit V2 的一部分，可从 [Microsoft 下载中心](http://www.microsoft.com/download/details.aspx?id=9257)下载。 还可通过 System Center 2012 Configuration Manager 及更高版本提供的 Configuration Manager Trace Log Tool (CMTrace) 读取日志。 请尽可能使用上述工具读取日志文件，以便大幅简化错误的查找。  

 本节其余部分详细介绍了部署和 Windows 安装过程中创建的日志文件。 本节还提供相关示例，介绍使用此文件进行故障排除的情形。  

### <a name="mdt-logs"></a>MDT 日志  
 每个 MDT 脚本均在运行时自动创建日志文件。 这些日志文件的名称与脚本名称一致，例如 ZTIGather.wsf 创建名为 ZTIGather.log 的日志文件。 每个脚本还会更新通用主日志文件 (BDD.log)，该文件包含 MDT 脚本创建的日志文件的全部内容。 部署过程中，MDT 日志文件驻留在 C:\MININT\SMSOSD\OSDLOGS 中。 根据正在执行的部署类型，日志文件将在部署完成时移动到 %WINDIR%\SMSOSD 或 %WINDIR%\TEMP\SMSOSD。 对于 Lite Touch Installation (LTI) 部署，日志在 C:\MININT\SMSOSD\OSDLogs 中启动。 任务序列进程完成后，它们在 %WINDIR%\TEMP\DeploymentLogs 中结束。  

 MDT 创建以下日志文件：  

-   **BDD.log**。 如果在 Customsettings.ini 文件中指定 SLShare 属性，则此文件是在部署结束时复制到网络位置的聚合 MDT 日志文件。  

-   **LiteTouch.log**。 此文件在 LTI 部署期间创建。 除非指定 /debug:true 选项，否则它位于 %WINDIR%\TEMP\DeploymentLogs。  

-   **Scriptname*.log**。 此文件由每个 MDT 脚本创建。 Scriptname 就是相关脚本的名称。  

-   **SMSTS.log**。 此文件由任务顺序器创建，提供任务顺序器所有事务的相关信息。 根据部署方案，它可能位于 %TEMP%、%WINDIR%\System32\ccm\logs、C:\\\_SMSTaskSequence 或 C:\SMSTSLog。  

-   **Wizard.log**。 此文件由部署向导进行创建和更新。  

-   **WPEinit.log**。 此文件在 Windows PE 初始化进程中创建，可用于排查启动 Windows PE 时遇到的错误。  

-   **DeploymentWorkbench_*id*.log**。 如果在启动部署工作台时指定 /debug，则在 %temp% 文件夹中创建此日志文件。  

### <a name="configuration-manager-operating-system-deployment-logs"></a>Configuration Manager 操作系统部署日志  
 若要了解 Microsoft System Center 2012 R2 Configuration Manager 创建的操作系统部署日志文件，请参阅 [Configuration Manager 中的日志文件的技术参考](http://technet.microsoft.com/library/hh427342.aspx)。  

 运行 Windows 用户状态迁移工具 (USMT) 时，MDT 自动添加将 USMT 日志文件保存到 MDT 日志文件位置的日志记录选项。 日志文件及其创建时间如下所示：  

-   **USMTEstimate.log**。 预估 USMT 需求时创建  

-   **USMTCapture.log**。 捕获数据时由 USMT 创建  

-   **USMTRestore.log**。 还原数据时由 USMT 创建  

 ZeroTouchInstallation.vbs 脚本自动扫描 USMT 进度日志文件中的错误和警告。 脚本将事件 ID 41010 生成到 Microsoft System Center Operations Manager，摘要如下（其中，usmt_type 为 ESTIMATE、SCANSTATE 或 LOADSTATE，error_count 为找到的错误总数，warning_count 为找到的警告总数）：  

```  
ZTI USMT <usmt_type> reported <error_count> errors and <warning_count> warnings  
```  

 如果错误计数大于 0，则此事件是错误类型。 如果警告计数大于 0 且没有错误，则此事件是警告类型。 否则，该事件是信息类型。  

## <a name="identifying-error-codes"></a>标识错误代码  
表 1 列出了 MDT 脚本创建的错误代码并提供每个错误代码的描述。 这些错误代码记录在 BDD.log 文件中。  

### <a name="table-1-error-codes-and-their-description"></a>表 1. 错误代码及其描述  

|**错误代码**|**描述**|  
|-|-|  
|5201|无法与部署共享建立连接。 将停止部署。|  
|5203|无法与部署共享建立连接。 将停止部署。|  
|5205|无法与部署共享建立连接。 将停止部署。|  
|5206|部署向导已取消或未成功完成。 将停止部署。|  
|5207|无法与部署共享建立连接。 将停止部署。|  
|5208|未设置 DeploymentType。 必须为 SkipWizard 设置一些值。|  
|5208|找不到 SMS 任务顺序器。 将停止部署。|  
|5400|创建对象: **Set *class_instance* = New *class_name***|  
|5490|创建 MSXML2.DOMDocument。|  
|5495|创建 MSXML2.DOMDocument.ParseErr.ErrCode。|  
|5496|LoadControlFile.FindFile: ConfigFile|  
|5601|验证 OS guid: 存在 %OSGUID%。|  
|5602|使用 OSGUID %OSGUID% 打开 XML。|  
|5610|验证文件。|  
|5630|验证文件: ImagePath。|  
|5640|验证文件: ImagePath。|  
|5641|FindFile: ImageX.exe。|  
|5643|查找 BootSect.exe。|  
|5650|验证目录: SourcePath。|  
|5651|验证目录: SourcePath\Platform。|  
|5652|FindFile: bootsect.exe。|  
|6001|验证驱动器。|  
|6002|验证驱动器。|  
|6010|测试 TSGUID。|  
|6020|Robocopy 返回值: Value。|  
|6021|Robocopy 返回值: Value。|  
|6101|检查文件: DeployCab。|  
|6102|从 DEPLOY.CAB 扩展 Sysprep 文件。|  
|6111|运行 Sysprep.exe。|  
|6121|运行 Sysprep。|  
|6191|在注册表中测试 CloneTag 来验证 Sysprep 已完成。|  
|6192|在注册表中测试 SystemSetupInProgress 来验证 Sysprep 已完成。|  
|6401|已授权 DHCP 服务器。|  
|6501|无法进行计算机备份，未指定网络路径(BackupShare、BackupDir)。|  
|6502|错误 - 无法定位 IMAGEX，无法执行备份。|  
|6601|GetObject(... root/wmi:BCDStore)。|  
|6602|BCD.OpenStore (BCDStore)。|  
|6701|已配置保护程序。|  
|6702|已移动启动文件。|  
|6703|已创建 BDE 分区。|  
|6704|碎片整理驱动器。|  
|6705|压缩驱动器。|  
|6706|测试多个分区。|  
|6707|创建启动文件。|  
|6708|加密磁盘。|  
|6709|连接到 MicrosoftVolumeEncryption WMI 提供程序。|  
|6710|正在加密磁盘。|  
|6711|ProtectKeyWithTPM。|  
|6712|ProtectKeyWithTPMAndPIN。|  
|6713|ProtectKeyWithTPMAndStartupKey。|  
|6714|在文件中保存外部密钥。|  
|6715|使用外部密钥进行保护。|  
|6716|在文件中保存外部密钥。|  
|6717|使用数字密码保护密钥。|  
|6718|GetKeyProtectorNumberialP@ssword。|  
|6718|在文件中保存密码。|  
|6719|打开 PasswordFile。|  
|6720|加密驱动器。|  
|6721|打开 DiskPartFile。|  
|6722|创建分区。|  
|6723|获取现有 BDE 驱动器。|  
|6724|打开 DiskPartFile。|  
|6727|尝试打开 DiskPartFile。|  
|6729|创建文本文件 DiskPartFile。|  
|6730|执行 cmd /c DISKPART.EXE /s DiskPartFile >> LogPath\ZTIMarkActive_diskpart.log 2>&1|  
|6731|查找 bcdboot.exe。|  
|6732|连接到 Microsoft TPM 提供程序。|  
|6733|在提供程序类中获取 TPM 实例。|  
|6734|获取 TPM 实例。|  
|6735|检查是否已启用 TPM。|  
|6736|检查是否已激活 TPM。|  
|6737|检查是否拥有 TPM。|  
|6738|检查是否允许 TPM 所有权。|  
|6739|检查是否已启用 TPM。|  
|6740|检查是否已激活 TPM。|  
|6741|检查是否拥有 TPM 且是否允许所有权。|  
|6741|TPM 所有者密码设置|  
|6742|TPM 所有者 P@ssword 设置为 AdminP@ssword。|  
|6743|将 TPM 所有者 P@ssword 设为值。|  
|6744|检查是否已启用 TPM。|  
|6745|检查 TPM 所有者。|  
|6746|检查认可密钥对。|  
|6747|检查是否已激活 TPM。|  
|6748|检查是否允许 TPM 所有权。|  
|6749|将所有者 p@ssword 转换为所有者授权。|  
|6750|创建认可密钥对。|  
|6751|更改所有者授权。|  
|6752|运行 CMD。|  
|6753|验证 TPM。|  
|6754|获取 BDE 实例。|  
|6755|使用 TPM 保护密钥。|  
|6756|检查要配置的可移动媒体。 ProtectKeyWithTpmAndStartupKey。|  
|6757|使用 TPM 和启动密钥保护密钥。|  
|6758|查找 BDE pin。|  
|6759|使用 TPM 和 Pin 保护密钥。|  
|6760|查找 BDEKeyLocation 的可移动媒体。|  
|6761|使用外部密钥进行保护。|  
|6762|正在将恢复 P@ssword 保存到 PasswordFile。|  
|6764|配置 BitLocker 策略。|  
|7000|无法定位 ZTIConfigure.xml；正在中止。|  
|7001|查找无人参与 AnswerFile。|  
|7100|错误 - 此脚本应仅在完整的 OS 中运行。|  
|7101|错误 - 提供的值不够，无法生成 DCPromo 答案文件。|  
|7102|错误 - 未指定创建新的副本域控制器时必需的属性。|  
|7103|错误 - 未指定创建新子域时必需的属性。|  
|7104|错误 - 未指定创建新林时必需的属性。|  
|7105|错误 - 未指定创建新林时必需的属性。|  
|7200|未安装服务，因此无法配置 DHCP 服务器。|  
|7201|无法读取作用域详细信息；`GetScopeDetails()` 失败。|  
|7202|指定的值不够，无法创建作用域。|  
|7203|提供的值不够，无法设置此作用域的 IP 范围。|  
|7204|未指定作用域排除范围的值。|  
|7300|无法发出 DNS 命令。|  
|7700|不是新计算机方案；正在退出磁盘分区。|  
|7701|磁盘大小不足以容纳系统和 BDE 分区，需要 1.5 GB。|  
|7702|磁盘大小不足以容纳系统和 WinRE 分区，需要 10 GB。|  
|7703|DeployRoot 位于磁盘 # DiskIndex 上。 运行 OEM 方案: 跳过。|  
|7704|运行 OEM 方案: 跳过。|  
|7704|BitLocker 不可用于扩展分区和逻辑分区。|  
|7712|存在验证驱动器/卷驱动器。 格式。|  
|7900|Findfile: Microsoft.BDD.PnpEnum.exe。|  
|7901|AllDrivers.Exists("GUID")。|  
|7904|AllDrivers.Exists("GUID")。|  
|9200|Findfile(PkgMgr.exe)。|  
|9601|错误 - 应在完整的 OS 中运行 ZTITatoo 状态还原任务；正在中止。|  
|9701|USMT 估计的非零返回代码，rc = Error。|  
|9702|无法捕获用户状态；本地空间不足且未指定网络路径(UDShare、UDDir)。|  
|9703|USMT 捕获的非零返回代码，rc = Error。|  
|9704|指定的命令行选项无效。|  
|9801|错误 - 正在尝试将客户端操作系统部署到运行服务器操作系统的计算机。|  
|9802|错误 - 正在尝试将服务器操作系统部署到运行客户端操作系统的计算机。|  
|9803|错误 - 未授权计算机升级(OSInstall=OSInstall)；正在中止。|  
|9804|错误 - 内存量(MB)不足。 至少需要 [xx] MB 内存。|  
|9805|错误 - ProcessorSpeed MHz 的处理器速度不足。  至少需要一个 ProcessorSpeed MHz 处理器。|  
|9806|错误 - 驱动器上的可用空间不足。 还需要 [xx] MB。|  
|9807|错误 - 驱动器上的可用空间不足。 还需要 [xx] MB。|  
|9901|不可在 Windows PE 中运行 ZTIWindowsUpdate 脚本。|  
|9902|ZTIWindowsUpdate 已运行且失败次数过多。 计数 = Count。|  
|9903|安装更新的 Windows 更新代理时出现意外问题，rc = Error。|  
|9904|未能创建对象: Microsoft.Update.Session。|  
|9905|未能创建对象: Microsoft.Update.UpdateColl。|  
|9906|未找到关键文件 File；正在中止。|  
|10000|创建对象: **Set oLTICleanup = New LTICleanup**。|  
|10201|无法加入域 Domain。 停止安装。|  
|10203|FindFile(LTISuspend.wsf)。|  
|10204|运行程序 LTISuspend。|  
|41024|运行 ImageX。|  
|52012|未设置部分向导参数。|  

 表 1 提供了日志文件摘要，演示如何查找日志文件。 在此摘要中，报告的错误代码为 5001。  

 **表 1.包含错误代码 5001 的 SMSTS.log 文件摘要**  

```  
.  
.  
.  
The operating system installation failed. Please contact your system administrator for assistance.  

The action "Zero Touch Installation - Validation" failed with exit code 5001  
.  
.  
.  

```  

### <a name="converting-error-codes"></a>转换错误代码  
 日志文件中显示的许多错误代码看起来相当隐晦，难以与实际错误情况进行联系。 但是，以下进程演示了如何转换错误代码以及如何获得可能协助解决问题的有用信息。  

 **问题**：图像捕获失败，错误代码为 0x80070040。  

 **可能的解决方案 1**：显示的错误代码为十六进制格式，需要转换为十进制格式。 为此，需要一个科学计算器，且 Windows 操作系统随附的计算器也适合执行此任务。  

 **若要转换错误代码**  

1.  单击“开始”，然后指向“所有程序”。 指向“附件”，然后单击“计算器”。  

2.  从“查看”菜单中，单击“科学型”。  

3.  选择“十六进制”，然后输入代码的最后四位数，本例中为 0040（如图 1 所示）。  

     ![TroubleshootingReference1](media/TroubleshootingReference1.jpg "TroubleshootingReference1")  
图 1. 错误转换  

     **图 1.错误转换**  

     请注意，计算器为十六进制模式时不显示前导零。  

4.  选择“十进制”。  

     十六进制值 40 转换为十进制值 64。  

5.  打开命令提示符窗口，键入 NET HELPMSG 64，然后按 Enter。  

     NET HELPMSG 命令将数字错误代码转换为有意义的文本。 对于此处提供的错误代码，它转换为“指定的网络名称不再可用”。  

 此信息表示目标计算机上或者目标计算机和部署共享所在的服务器之间可能存在网络问题。 这些问题可能包括网络驱动程序安装错误或速度和双工设置不匹配。  

 **可能的解决方案 2：** 使用 Microsoft Exchange 服务器错误代码查找实用程序。 此命令行实用程序在帮助错误代码转换方面非常有价值。 可从 [Microsoft 下载中心](http://www.microsoft.com/download/details.aspx?id=985)下载此程序。  

### <a name="review-of-sample-logs"></a>查看示例日志  
 MDT 创建可用于排查 MDT 部署过程中的问题的日志文件。 以下部分提供相关示例，介绍如何使用 MDT 日志文件排查部署进程相关问题：  

-   与 MDT 数据库 (MDT DB) 访问失败相关的问题，如[未能访问数据库](#FailuretoAccesstheDatabase)中所述  

####  <a name="FailuretoAccesstheDatabase"></a>未能访问数据库  
 **问题：** 运行使用带众多分区的 CustomSettings.ini 文件的部署且通过“优先级”属性指定要处理的每个分区的优先级时出现错误。 BDD.log 包含以下错误消息：  

-   ```  
    ERROR - Opening Record Set (Error Number = -2147217911) (Error Description: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'.)  
    ```  

-   ```  
    ADO error: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'. (Error #-2147217911; Source: Microsoft OLE DB Provider for SQL Server; SQL State: 42000; NativeError: 229  
    ```  

-   ```  
    ERROR - Unhandled error returned by ZTIGather: Object required (424)  
    ```  

> [!NOTE]
>  为清楚起见，上述日志文件的内容按用户通过 Trace32 程序查看时所显示的方式呈现。  

 **可能的解决方案：** 如日志文件示例第一行所述，此问题表示数据库的访问权限被拒绝。 因此，脚本无法建立到数据库的安全连接，这可能是由于用户 ID 和密码不可用。 所以系统尝试使用计算机帐户访问数据库。 最简单的解决方式是向所有人授予数据库的“读取”访问权限。  

## <a name="troubleshooting"></a>疑难解答  
 在开始深度故障排除进程之前，请查看以下各项，确保已满足所有相关要求：  

-   如果未满足某些软件和硬件先决条件，可能导致安装问题。  

### <a name="application-installation"></a>应用程序安装  
 查看应用程序安装问题和解决方案：  

-   由于安全原因而被阻止的安装源文件，如[已阻止可执行文件](#BlockedExecutables)中所述  

-   网络连接丢失，如[丢失网络连接](#LostNetworkConnections)中所述  

-   安装 2007 Microsoft Office system 或相关文件时的安装错误 30029，如 [2007 Microsoft Office System](#MicrosoftOfficeSystem)中所述  

####  <a name="BlockedExecutables"></a>已阻止可执行文件  
 **问题：** 如果从 Internet 下载安装源文件，则它们可能标记有一个或多个 NTFS 文件系统数据流。 有关 NTFS 数据流的详细信息，请参阅[文件流](http://msdn2.microsoft.com/library/aa364404\(VS.85\).aspx)。 NTFS 文件系统数据流的存在可能导致“打开文件 – 安全警告”提示。 只有在系统提示时单击“运行”，才能继续安装。  

 图 2 显示可使用“更多”命令行和[流实用程序](http://technet.microsoft.com/sysinternals/bb897440.aspx)查看 NTFS 文件系统数据流。  

 ![TroubleshootingReference2](media/TroubleshootingReference2.jpg "TroubleshootingReference2")  
图 2. NTFS 数据流  

 **图 2.NTFS 数据流**  

 **可能的解决方案 1：** 右键单击安装源文件，然后单击“属性”。 单击“解除阻止”后单击“确定”，删除文件中的 NTFS 文件系统数据流。 对每个由于存在一个或多个 NTFS 文件系统数据流而被阻止的安装源文件重复此过程。  

 **可能的解决方案 2：** 使用流实用程序（例如 REF \_Ref308173670 \\h 图 2 所示），删除安装源文件中的 NTFS 文件系统数据流。 流实用程序可立即删除一个或多个文件或文件夹中的 NTFS 文件系统数据流。  

####  <a name="LostNetworkConnections"></a>丢失网络连接  
 **问题：** 如果安装设备驱动程序或更改设备和网络配置，安装可能失败。 这些更改可能导致网络连接失效，从而造成安装失败。  

 **可能的解决方案：** 执行 ZTICacheUtil.vbs 脚本，以便下载和执行安装项。 此脚本旨在调整播发来进行下载和执行。 如果 Configuration Manager 分发点是基于 Web 的分布式创作且已启用版本管理和 BITS，则通过后台智能传输服务 \(BITS\) 进行下载。 同时，它修改 Configuration Manager，使其先运行 ZTICache.vbs 脚本，确保程序在部署过程中不删除自己。  

####  <a name="MicrosoftOfficeSystem"></a>2007 Microsoft Office System  
 **问题：** 部署 2007 Office system 且包含 Windows Installer 修补程序 \(MSP\) 文件时，安装可能失败，错误代码为 30029。  

 对 ZTIApplications.log 的进一步调查示以下消息：  

-   ```  
    About to run command: \\Server\Deployment$\Tools\X86\bddrun.exe \\Server\Share\Microsoft\Office\2007\Professional\setup.exe /adminfile \\Server\Share\Microsoft\Office\2007\Professional\file.msp  
    ```  

-   ```  
    ZTI Heartbeat: command has been running for 12 minutes (process ID 1600) Return code from command = 30029  
    ```  

-   ```  
    Application Microsoft Office 2007 Professional returned an unexpected return code: 30029  
    ```  

 **可能的解决方案 1：** 将 MSP 文件重定位到“更新”目录，然后运行 setup.exe，但不指定 \/adminfile 选项。 若要深入了解如何在安装过程中部署更新，请参阅[部署 2007 Office system](http://technet.microsoft.com/library/cc303395\(v=Office.12\).aspx)。  

 **可能的解决方案 2：** 验证确保 MSP 文件未选择“阻止模式”复选框。 若要深入了解如何配置此设置，请参阅 [2007 Office System 部署概述](http://technet.microsoft.com/library/bb490141.aspx)。  

### <a name="autologon"></a>AutoLogon  
 查看自动登录问题和解决方案：  

-   由于登录安全横幅而出现的 LTI 和 Zero Touch Installation \(ZTI\) 部署进程中断，如[登录安全横幅](#LogonSecutiryBanners)中所述  

-   由于用户凭据提示而出现的 LTI 和 ZTI 部署进程中断，如[提示输入用户凭据](#PromtedforUserCredentials)中所述  

####  <a name="LogonSecutiryBanners"></a>登录安全横幅  
 **问题：** 在交互用户会话中处理 MDT 任务序列，这需要目标计算机能使用指定的管理帐户自动登录。 如果部署了强制执行登录安全横幅的组策略对象 \(GPO\) ，则将禁止自动登录，因为在用户接受所声明的策略之前，安全横幅会停止登录进程。  

 **可能的解决方案：** 确保 GPO 应用到特定的组织单位 \(OU\) 且未包含在默认域 GPO 中。 将计算机添加到域时，请指定将它们添加到不受 GPO（强制执行登录安全横幅）影响的 OU。 在任务序列编辑器中，在最后的任务序列步骤中包含将计算机帐户重定位到所需的 OU 的脚本。  

> [!NOTE]
>  如果在重复使用现有的 Active Directory® 域服务 \(AD DS\) 帐户，请确保在部署到目标计算机之前，已将目标计算机的帐户重定位到不受 GPO（强制执行安全登录横幅）影响的 OU。  

####  <a name="PromtedforUserCredentials"></a>提示输入用户凭据  
 **问题：** 已创建加入域的计算机的映像。 将新的映像部署到目标计算机时，部署进程停止，因为计算机不自动登录，且系统提示用户输入适当的凭据。 提供凭据且用户登录后，继续执行部署进程。  

 **可能的解决方案：** 捕获映像时，源计算机不应加入域。 如果计算机已加入域，则将计算机加入工作组，重新捕获映像，再尝试部署到目标计算机来检查是否解决问题。  

### <a name="bios"></a>BIOS  
 **问题：** 部署到配备 Intel vPro 技术的目标计算机时，可能结束部署且出现停止错误。 即使更新后的所有驱动程序均作为现成驱动程序包含在部署工作台中，目标计算机也不启动。  

 可能的解决方案：检查目标计算机的基本输入\/输出系统 \(BIOS\) 中的设置，查看是否将默认串行高级技术附件模式配置为高级主机控制器接口 \(AHCI\)。 遗憾的是，默认情况下某些 Windows 操作系统不支持 AHCI。  

### <a name="database-problems"></a>数据库问题  
 查看数据库相关问题和解决方案\-：  

-   由于数据库服务器上的防火墙配置错误而生成的错误，如[已阻止 SQL Server 浏览器请求](#BlockedSQLServerBrowserRequests)中所述  

-   由于与数据库服务器中断连接而生成的错误，如[命名管道连接](#NamedPipeConnections)中所述  

####  <a name="BlockedSQLServerBrowserRequests"></a>已阻止 SQL Server 浏览器请求  
 **问题：** 在 MDT 部署过程中，可从 Microsoft SQL Server® 数据库检索信息。 但是，可能生成与数据库服务器上防火墙配置错误相关的错误。  

 **可能的解决方案：** Windows Server 的 Windows 防火墙有助于防止未经授权访问计算机资源的行为。 但如果防火墙配置错误，可能会阻止到 SQL Server 实例的连接。 若要访问受防火墙保护的 SQL Server 实例，请在运行 SQL Server 的计算机上配置防火墙。 若要深入了解如何为 SQL Server 配置防火墙端口，请参阅 Microsoft 支持文章：[如何在 Windows Server 2008 上打开 SQL Server 的防火墙端口？](http://support.microsoft.com/kb/968872)  

####  <a name="NamedPipeConnections"></a>命名管道连接  
 **问题：** 在 MDT 部署过程中，可从 SQL Server 数据库检索信息。 但是，可能生成与 SQL Server 连接中断相关的错误。 错误原因可能是未在 Microsoft SQL Server 中启用命名管道连接。  

 **可能的解决方案：** 要解决上述问题，请在 SQL Server 中启用命名管道。 同时指定 SQLShare 属性，在通过命名管道连接到外部数据库时需使用此属性。 使用命名管道进行连接时，请使用集成安全性建立到数据库的连接。 对于 LTI 部署，所指定的用户帐户建立到数据库的连接。 对于使用 Configuration Manager 的 ZTI 部署，网络访问帐户连接到数据库。 由于 Windows PE 默认情况下没有安全上下文，因此必须建立到数据库服务器的网络连接，以便为要进行连接的用户建立安全上下文。  

 SQLShare 属性指定的网络共享提供了一种连接到服务器以获取安全性上下文的方法。 必须具有共享的“读取”访问权限。 连接建立后，可接着建立到数据库的命名管道连接。 无需使用 SQLShare 属性，且在建立到数据库的 TCP\/IP 连接时不得使用此属性。  

 请根据所用的 SQL Server 版本，执行以下任务来启用命名管道连接：  

-   启用 SQL Server 2008 R2 的命名管道连接，如[在 SQL Server 2008 R2 中启用命名管道连接](#EnableNamedPipeConnectionsinSQLServer)中所述。  

-   启用 SQL Server 2005 的命名管道连接，如[在 SQL Server 2005 中启用命名管道连接](#EnableNamedPipeConnectionsinSQL)中所述。  

#####  <a name="EnableNamedPipeConnectionsinSQLServer"></a>在 SQL Server 2008 R2 中启用命名管道连接  
 若要在 SQL Server 2008 R2 中启用命名管道连接，请执行以下步骤：  

1.  在运行 SQL Server 2008 R2（托管要查询的数据库）的计算机上，单击“开始”，然后指向“所有程序”。 指向“Microsoft SQL Server 2008 R2”，然后单击“SQL Server Management Studio”。  

2.  在“Microsoft SQL Server Management Studio”控制台的“对象资源管理器”中，右键单击“sql\_server\_name”，然后单击“属性”（其中 sql\_server\_name 是运行要配置的 SQL Server 的计算机名称）。  

3.  随即显示“服务器属性 \- sql\_server\_name”对话框。  

4.  在“服务器属性 \- sql\_server\_name”对话框的“选择页”中，单击“连接”。  

5.  在“连接”页上，确保选中“允许远程连接到此服务器”复选框，然后单击“确定”。  

6.  关闭 Microsoft SQL Server Management Studio 控制台。  

7.  在运行 SQL Server 2008 R2（托管要查询的数据库）的计算机上，单击“开始”，然后指向“所有程序”。 指向“Microsoft SQL Server 2008 R2”，指向“配置工具”，然后单击“SQL Server 配置管理器”。  

8.  在“SQL Server 配置管理器”控制台中，转到 SQL Server 配置管理器\(本地\)\/SQL Server 网络配置\/sql\_instance 协议（其中 sql\_instance 是要配置的 SQL Server 实例的名称）。  

9. 在详细信息窗格中，右键单击“命名管道”，然后单击“启用”。  

     此时将出现“警告”对话框，指出所做更改将保存，但在服务停止和重启后才生效。  

10. 在“警告”对话框中，单击“确定”。  

11. 在“SQL Server 配置管理器”控制台中，转到 SQL Server 配置管理器\(本地\)\/SQL Server 服务。  

12. 在详细信息窗格中，右键单击 SQL Server \(sql\_instance\)，然后单击“重启”（其中 sql\_instance 是在步骤 2 中配置的 SQL Server 实例的名称）。  

     此时将显示 SQL Server 配置管理器进度栏，指出服务重启状态。 服务重启后，进度栏关闭。  

13. 关闭 SQL Server 配置管理器控制台。  

 有关其他信息，请参阅 [How to enable remote connections in SQL Server 2008](http://blogs.msdn.com/b/walzenbach/archive/2010/04/14/how-to-enable-remote-connections-in-sql-server-2008.aspx)（如何在 SQL Server 2008 中启用远程连接）。  

#####  <a name="EnableNamedPipeConnectionsinSQL"></a>在 SQL Server 2005 中启用命名管道连接  
 若要在 SQL Server 2005 中启用命名管道连接，请执行以下步骤：  

1.  在运行 SQL Server 2005（托管要查询的数据库）的计算机上，单击“开始”，然后指向“所有程序”。 指向“Microsoft SQL Server 2005”，指向“配置工具”，然后单击“SQL Server 外围应用配置器”。  

2.  在“SQL Server 2005 外围应用配置器”对话框中，单击“服务和连接的外围应用配置器”。  

3.  单击“服务和连接的外围应用配置器 – server\_name”对话框（其中 server\_name 是运行 SQL Server 2005 的计算机名称），在“选择组件，然后配置其服务和连接”中，转到 MSSQLSERVER\\数据库引擎，再单击“远程连接”。  

4.  依次单击“本地和远程连接”、“使用 TCP\/IP 和命名管道”以及“应用”。  

5.  单击“服务和连接的外围应用配置器 – server\_name”对话框（其中 server\_name 是运行 SQL Server 2005 的计算机名称），在“选择组件，然后配置其服务和连接”中，转到 MSSQLSERVER\\Database Engine，再单击“服务”。  

6.  单击“停止”。  

     MSSQLSERVER 服务随即停止。  

7.  单击“开始”。  

     MSSQLSERVER 服务随即启动。  

8.  单击“**确定**”。  

9. 关闭 SQL Server 2005 外围应用配置器。  

 有关其他信息，请参阅 Microsoft 支持文章：[如何配置 SQL Server 2005 以允许远程连接](http://support.microsoft.com/kb/914277)  

### <a name="deployment-scripts"></a>部署脚本  
 查看 MDT 相关问题和解决方案：  

-   提示输入用户凭据且可能显示错误 0x80070035，如 [Credentials_script](#Credentials_script) 中所述  

-   出现“找不到 Wuredist.cab”错误消息，如 [ZTIWindowsUpdate](#ZTIWindowsUpdate) 中所述  

####  <a name="Credentials_script"></a> Credentials\_script  
 **问题：** 在上次启动新部署的计算机期间，系统提示用户提供用户凭据且可能显示错误 0x80070035（表示找不到网络路径）。  

 **可能的解决方案：** 确保 WIM 文件不包含 MININT 和 \_SMSTaskSequence 文件夹。 要删除这些文件夹，请先使用 ImageX 实用程序装载 WIM 文件，然后再删除文件夹。  

> [!NOTE]
>  如果尝试从 WIM 文件删除文件夹时遇到“访问被拒绝”错误，请打开命令提示符窗口，切换到 WIM 文件中所含映像的根目录，然后运行 RD MININT 和 RD \_SMSTaskSequence。  

####  <a name="ZTIWindowsUpdate"></a>ZTIWindowsUpdate  
 **问题：** 如果在部署期间使用 ZTIWindowsUpdate.wsf 脚本应用软件更新，请注意此脚本可能直接与 Microsoft 更新网站进行通信，以下载和安装所需的 Windows 更新代理二进制文件，扫描适用的软件更新，下载适用软件更新的二进制文件，然后安装下载的二进制文件。 此过程要求你的网络基础结构配置为允许目标计算机访问 Microsoft 更新网站。  

 如果部署共享不包含 Windows 更新代理安装文件，且目标计算机没有适当的 Internet 访问权限，则在 ZTIWindowsUpdate.log 和 BDD.log 文件中报告“找不到 wuredist.cab”错误。  

 **可能的解决方案：** 按照 MDT 文档“工具箱参考”中的“ZTIWindowsUpdate.wsf”部分进行操作。  

### <a name="deployment-shares"></a>部署共享  
 检查部署共享相关问题和解决方案：  

-   更新部署共享时未能更新 WIM 文件，如[未能更新 WIM 文件](#FailuretoUpdateWIMFiles)中所述。  

####  <a name="FailuretoUpdateWIMFiles"></a>未能更新 WIM 文件  
 在“简单”环境中：  

-   MDT 通常从 C:\\Windows\\system32（始终在此路径中）获取 WIMGAPI.DLL。 WIMGAPI.DLL 的版本必须与操作系统的版本相匹配。  

-   在 64 位操作系统上，MDT 始终使用 x64 WIMGAPI.DLL 文件；系统路径中仅能使用该文件。 在 32 位操作系统上，MDT 始终使用 x86 WIMGAPI.DLL 文件；系统路径中仅能使用该文件。 （配置管理器等其他产品使用 WIMGAPI.DLL 的 32 位版本，即使是在 64 位操作系统上也要管理和安装此版本。）  

 **问题：** 尝试更新部署共享时，系统通知用户一个或多个 .wim 文件装载失败。  

 **可能的解决方案：** 打开命令提示符窗口并运行“WIMGAPI.DLL 位于何处”。 对于列表中的第一个条目（搜索路径找到的第一个位置），请确保“版本”属性与安装的 Windows 评估和部署工具包 \(Windows ADK\) 的版本一致。 还要确保该属性与操作系统生成号一致。  

### <a name="the-windows-deployment-wizard"></a>Windows 部署向导  
 查看 Windows 部署向导相关问题和解决方案：  

-   即使 LTI 配置为跳过向导页，仍显示 Windows 部署向导页，如[不跳过向导页](#WizardPagesareNotSkipped)中所述。  

####  <a name="WizardPagesareNotSkipped"></a>不跳过向导页  
 **问题：** 即使 MDT DB 或 CustomSettings.ini 文件指定应跳过向导，仍显示向导页。  

 **可能的解决方案：** 要正常跳过向导页，请包含适当时在 MDT DB 或 CustomSettings.ini 文件的此向导页上指定随同适当的值一同出现的所有属性。 如果所跳过的向导页的属性配置错误，则显示此页面。 若要深入了解需具备哪些属性才可确保跳过向导页，请参阅 MDT 文档“工具箱参考”的“提供所跳过的部署向导页的属性”部分。  

### <a name="disks-and-partitioning"></a>磁盘和分区  
 查看磁盘分区问题和解决方案：  

-   BitLocker® 驱动器加密问题，如 [BitLocker 驱动器加密](#BitLockerDriveEncryption)中所述  

-   磁盘分区错误，如磁盘分区错误中所述  

-   刷新计算机部署方案期间由逻辑或动态磁盘导致的故障，如[支持逻辑和动态磁盘](#SupportforLoogicalandDynamicDisks)中所述  

####  <a name="BitLockerDriveEncryption"></a>BitLocker 驱动器加密  
 需具备相应部署的特定配置才可部署 BitLocker。 以下潜在问题可能与目标计算机的配置有关：  

-   在 ZTI 和 UDI 部署中，ZTIBde.wsf 脚本失败，出现错误“无法打开注册表项 HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName 进行读取”，如 [ZTIBde.wsf 脚本失败，出现“无法打开注册表项 HKEY_CURRENT_USER\Control Panel\International\LocaleName 进行读取”错误](#ZTIBde.wsf)中所述。  

-   目标计算机上显示为多个驱动器号的的 USB 设备、CD 驱动器、DVD 驱动器或其他可移动媒体设备，如[设备显示为多个驱动器号](#DevicesAppearasMultipleDriveLetters)中所述  

-   在目标计算机上压缩驱动器 C，以提供足够的未分配磁盘空间，如[磁盘压缩问题](#ProblemswithShrinkingDisks)中所述  

#####  <a name="ZTIBde.wsf"></a>ZTIBde.wsf 脚本失败，出现“无法打开注册表项 HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName 进行读取”错误  
 **问题：** 尝试在目标计算机的 ZTI 或 UDI 中部署 BitLocker 时，ZTIBde.wsf 脚本失败，出现“无法打开注册表项 HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName 进行读取”错误。  

 **可能的解决方案：** 在“UILanguage”属性中指定区域设置。 在 ZTI 和 UDI 中，ZTIBde.wsf 脚本在系统控制中运行，因此未加载完整的用户配置文件。 当 ZTIBde.wsf 脚本尝试读取区域设置信息时，信息未在注册表中，因为注册表（用户配置文件）未完全加载。 解决方法是在“UILanguage”属性中指定区域设置。  

#####  <a name="DevicesAppearasMultipleDriveLetters"></a>设备显示为多个驱动器号  
 **问题：** 某些设备可能显示为多个逻辑驱动器号，具体取决于分区方式。 在某些情况下，它们可模拟 1.44 兆字节 \(MB\) 软盘驱动器和内存存储驱动器。 因此，Windows 可能向软盘模拟配置相同的设备驱动器号 A 和 B，并向内存存储驱动器分配 F。 默认情况下，MDT 脚本使用最低驱动器号（本例中为 A）。  

 **可能的解决方案：** 更改 Windows 部署向导的“指定 BitLocker 恢复详细信息”页上的默认设置。 Windows 部署向导摘要页将显示一条警告，通知用户选用于存储 BitLocker 恢复信息的驱动器号。 此外，BDD.log 和 ZTIBDE.log 文件记录检测到的可移动媒体设备以及选用于存储 BitLocker 恢复信息的设备。  

#####  <a name="ProblemswithShrinkingDisks"></a>磁盘压缩问题  
 **问题：** 目标计算机上未分配的磁盘空间不足，无法启用 BitLocker。 若要在目标计算机上部署 BitLocker，至少需使用 2 千兆字节 \(GB\) 未分配的磁盘空间来创建系统卷。 系统卷是包含 BIOS 启动计算机后加载 Windows 时所需的硬件特定文件的卷。  

 **可能的解决方案 1：** 在现有计算机上，使用 Diskpart 工具压缩驱动器 C，以便创建系统卷。 但在某些情况下，Diskpart 工具可能无法将磁盘 C 压缩到能提供 2 GB 的未分配磁盘空间，这可能由磁盘 C 中的碎片磁盘空间导致。  

 其中一种可能的解决方案是整理驱动器 C 的碎片。为此，请执行下列步骤：  

1.  运行 Diskpart shrink querymax 命令，确定能实现的未分配磁盘空间上限。  

2.  如果步骤 1 中返回的值小于 2 GB，请清理驱动器 C 中所有不必要的文件，然后进行碎片整理。  

3.  再次运行 Diskpart shrink querymax命令，验证能实现的未分配磁盘空间是否大于 2 GB。  

4.  如果步骤 3 中返回的值仍小于 2 GB，请执行下列任一任务：  

    -   反复整理驱动器 C 的碎片，保证将其完全优化。  

    -   在驱动器 C 上备份数据，删除现有分区，创建新分区，然后将数据还原到新分区。  

 **可能的解决方案 2：** ZTIBDE.wsf 脚本运行磁盘准备工具 \(bdehdcfg.exe\)，并将系统卷分区大小默认配置为 2 GB。 必要时，可自定义 ZTIBDE.wsf 脚本以更改此默认值。 但不建议修改 MDT 脚本。  

####  <a name="SupportforLoogicalandDynamicDisks"></a>支持逻辑和动态磁盘  
 **问题：** 执行“刷新计算机”部署方案时，如果部署到使用逻辑驱动器或动态磁盘的目标计算机，部署过程可能失败。  

 **可能的解决方案：** MDT 不支持将操作系统部署到逻辑驱动器和动态磁盘。  

### <a name="domain-join"></a>域加入  
 **问题：** 在部署期间，使用 Windows 部署向导提供目标计算机所需的全部信息，包括凭据、域加入信息和静态 IP 配置。 安装完成后，看到系统未加入域，而是仍位于工作组中。  

 **可能的解决方案：** MDT 的 LTI 部署在操作系统启动并运行后配置静态 IP 信息。 如果目标计算机位于没有动态主机配置协议 \(DHCP\) 的网络段上，则 Unattend.xml 中指定的自动域加入将在不具备 DHCP 的情况下失败。  

 配置 Unattend.xml 以加入工作组。 然后，使用内置的“从域中恢复”任务序列步骤在任务序列中添加步骤，以便在应用静态 IP 后加入域。  

### <a name="driver-installation"></a>驱动程序安装  
 为确保尽可能提供最佳用户体验，应尽可能无缝实现硬件设备和软件驱动程序的安全，没有或、少有用户干预。 Microsoft 提供了相应工具和指南，指导用户帮助创建满足此目标的安装包。 有关驱动程序安装的常规信息，请参阅[设备和驱动程序安装](http://www.microsoft.com/whdc/driver/install/default.mspx)。  

 查看设备驱动程序安装相关问题和解决方案：  

-   通过 MDT 使用 $OEM$ 大容量存储驱动程序时出现的问题，如“将 $OEM$ 大容量存储驱动程序和 MDT 大容量存储逻辑一起使用”中所述  

-   使用 SetupAPI.log 排查设备驱动程序安装问题，如[使用 SetupAPI.log 排查设备安装问题](#TroubleshootDeviceInstallationwithSetupAPI.log)中所述  

####  <a name="TroubleshootDeviceInstallationwithSetupAPI.log"></a>使用 SetupAPI.log 排查设备安装问题  
 有关 Windows 设备安装的调试信息，请参阅[使用 SetupAPI 日志文件排查设备安装问题](http://msdn.microsoft.com/windows/hardware/gg463393.aspx)白皮书。 具体而言，驱动程序开发人员和测试人员可按照此白皮书中的指南解释 SetupAPI 日志文件。  

 最适合用于调试的一个文件是 SetupAPI.log 文件。 此纯文本文件保存了 SetupAPI 记录的设备安装、服务包安装和更新安装相关信息。 具体来说，该文件保存了设备和驱动程序的更改记录，以及自 Windows 上次安装起出现的主要系统更改。 此白皮书重点介绍如何使用 SetupAPI 日志文件排查设备安装问题，不涉及与服务包和更新安装相关的日志文件部分。  

### <a name="new-computer-deployments"></a>新计算机部署  
 查看新计算机部署方案的问题和解决方案：  

-   使用预启动执行环境 \(PXE\) 启动部署进程时遇到的问题，如 [PXE 启动](#PXEBoot)中所述  

####  <a name="PXEBoot"></a>PXE 启动  
 简而言之，PXE 协议如下操作：客户端计算机通过广播 DHCP 发现数据包来启动协议，其中此数据包中的扩展可标识实现 PXE 协议的客户端计算机发出的请求。 假设实现此扩展协议的启动服务器可用，启动服务器会发送一个提议，其中包含将服务客户端的服务器的 IP 地址。 客户端使用日常文件传输协议从启动服务器下载可执行文件。 最后，客户端计算机运行所下载的启动程序。  

 此协议的初始阶段基于一部分 DHCP 消息，让客户端能够发现启动服务器（即传递可执行文件进行新计算机安装的服务器）。 客户端计算机可在此期间获取 IP 地址（这是预期行为），但并非一定要这样做。  

 此协议的第二阶段发生在客户端计算机与启动服务器之间，使用 DHCP 消息格式作为便捷的通信格式。 但第二阶段与标准的 DHCP 服务无关。 以下几页简要介绍了 PXE 客户端计算机初始化期间的分步过程。  

 若要深入了解如何在旧版或混合模式下运行的 Windows 部署服务中排查 PXE 启动相关问题，请参阅 Microsoft 支持文章：[PXE 客户端、DHCP 和 RIS 客户端之间的 PXE 交互说明](http://support.microsoft.com/kb/244036)。  

 查看下述针对 PXE 启动问题的解决方案：  

-   禁用到 SetupAPI.log 的 Windows PE 日志记录，如[在 Windows 部署服务中禁用 Windows PE 日志记录](#DisableWindowsPELogginginWindowsDeploymentServices)中所述。  

-   请确保 DHCP 配置正确，如[确保 DHCP 正确配置](#EnsuretheProperDHCPConfiguration)中所述。  

-   缩短将 IP 地址分配到 PXE 客户端计算机的响应时间，如[缩短 PXE IP 地址分配响应时间](#ImprovePXEIPAddressAssignmentResponseTime)中所述。  

#####  <a name="DisableWindowsPELogginginWindowsDeploymentServices"></a>在 Windows 部署服务中禁用 Windows PE 日志记录  
 建议首先是确保已禁用到 setupapi.log 的日志记录。  

#####  <a name="EnsuretheProperDHCPConfiguration"></a>确保 DHCP 正确配置  
 DHCP 广播转发的特定路由器配置可能支持子网（或路由器接口）或特定主机，这取决于当前使用的路由器模型。 如果 DHCP 服务器不在运行 Windows 部署服务的计算机上，请确保转发 DHCP 广播的路由器经过专门设计，让 DHCP 和 Windows 部署服务服务器都能接收客户端广播；否则，客户端计算机不接收对其远程启动请求的回复。  

 客户端计算机和远程安装服务器之间是否有路由器禁止基于 DHCP 的请求或响应通过？ 当 Windows 部署服务客户端计算机和 Windows 部署服务服务器在不同的子网上时，请将这两个系统之间的路由器配置为将 DHCP 数据包转发到 Windows 部署服务服务器。 必须如此安排，因为 Windows 部署服务客户端计算机使用 DHCP 广播消息发现 Windows 部署服务服务器。 如果未在路由器上设置 DHCP 转发，则客户端计算机的 DHCP 广播不会传输到 Windows 部署服务服务器。 路由器配置手册中有时将此 DHCP 转发过程称为“DHCP 代理”或“IP 帮助程序地址”。 若要深入了解如何在特定路由器上设置 DHCP 转发，请参阅路由器说明。  

#####  <a name="ImprovePXEIPAddressAssignmentResponseTime"></a>缩短 PXE IP 地址分配响应时间  
 如果 PXE 客户端计算机检索 IP 地址时耗时较长（15–20 秒），请检查以下元素：  

-   目标计算机上网络适配器与交换机或路由器的速度是否设置一致（自动、双工、完整等）  

-   Windows 部署服务服务器的 IP 地址是否位于建立连接的路由器上的 IP 帮助程序文件中？ 如果 IP 帮助程序文件中的 IP 地址列表太长，能否将 Windows 部署服务服务器地址移到靠近顶端的位置  

### <a name="restarting-the-deployment-process"></a>重启部署进程  
 **问题：** 测试和排查新的或已修改的任务序列后，可能需要重启目标计算机，才能从头开始进行部署。 由于 MDT 通过将数据写入到硬盘来跟踪其进度，因此可能出现意外结果；每次重启目标计算机时，都在 MDT 上次重启时所处的状态将其恢复。  

 **可能的解决方案：** 要从头开始进行部署，请先删除 C:\\MININT and C:\\\_SMSTaskSequence 文件夹，然后再重启目标计算机。  

### <a name="sysprep"></a>Sysprep  
 查看 Sysprep 相关问题和解决方案：  

-   目标计算机未显示在适当的 AD DS OU 中，如 [计算机帐户位于错误的 OU 中](#ComputerAccountisintheWrongOU)中所述。  

####  <a name="ComputerAccountisintheWrongOU"></a>计算机帐户位于错误的 OU 中  
 **问题：** 目标计算机已正确加入域，但计算机帐户位于错误的 OU 中。  

 **可能的解决方案 1：** 如果预先存在目标计算机的帐户，则此帐户保留在其原始 OU 中。 若要将帐户移到指定的 OU，请添加使用自动化工具（如 Microsoft Visual Basic® Scripting Edition）的任务序列步骤来移动帐户。  

 **可能的解决方案 2：** 验证指定的 OU 是否存在且其格式是否正确。 正确的 OU 格式应为 `OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`。  

### <a name="configuration-manager"></a>配置管理器  
 **问题：** 尝试通过“创建自签名 PXE 证书”选项创建 Configuration Manager PXE 服务点时，出现 REF \_Ref308174600 \\h 图 3 中所示的错误消息。  

 ![TroubleshootingReference3](media/TroubleshootingReference3.jpg "TroubleshootingReference3")  
图 SEQ Figure \\\* ARABIC 3. PXE 服务点错误  

 **图 SEQ Figure \\\* ARABIC 3.PXE 服务点错误**  

 **可能的解决方案：** 如果当前配置的服务器上已存在 PXE 服务点，则在你卸载 PXE 服务点时，它可能未删除自创建证书。 从 C:\\Documents and Settings\\user\_name\\Application Data\\Microsoft\\Crypto\\RSA 中删除 PXE 证书文件夹（其中 user\_name 是执行当前配置或执行之前配置的用户的名称）。 删除文件夹后，Configuration Manager 控制台的“新建站点角色”向导应当能成功完成。  

### <a name="task-sequences"></a>任务序列  
 查看任务序列相关问题和解决方案：  

-   任务序列未成功完成或出现不可预测的行为，如[任务序列未成功完成](#TaskSequenceDoesNotFinishSuccessfully)中所述。  

-   启动映像上列出了 LTI 的原始设备制造商 \(OEM\) 任务序列以及相对立的处理器体系结构，如 [OEM 任务序列错误地显示在为其他处理器体系结构创建的启动映像上](#OEMTaskSequenceIncorrectlyAppearsforBootImage)。  

-   Windows 部署向导显示“任务序列项错误\(OS GUID 无效\)”这一错误消息，如 [Windows 部署向导中的“任务序列项错误(OS GUID 无效)”消息](#BadTaskSequenceItem)中所述。  

-   配置网络连接名称时，显示“请输入有效的网络适配器名称”消息，如[应用网络设置](#ApplyNetworkSettings)中所述。  

-   针对任务序列不当配置“出错时继续”配置设置时可能出现的错误，如[使用“出错时继续”](#UseContinueonError)中所述。  

####  <a name="TaskSequenceDoesNotFinishSuccessfully"></a>任务序列未成功完成  
 **问题：** 任务序列未成功完成或出现不可预测的行为。  

 **可能的解决方案：** 可能在创建任务序列步骤后修改了“安装操作系统”任务序列步骤（针对 LTI）或“应用操作系统映像”任务序列步骤（针对 UDI 和 ZTI），这会导致不可预测的结果。 例如，如果创建任务序列来部署 32 位 Windows 8.1 映像，但之后将“安装操作系统”任务序列步骤或“应用操作系统映像”任务序列步骤更改为引用 64 位 Windows 8.1 映像，则任务序列可能无法成功运行。  

 建议创建新的任务序列来部署其他操作系统映像。  

####  <a name="OEMTaskSequenceIncorrectlyAppearsforBootImage"></a>OEM 任务序列错误地显示在为其他处理器体系结构创建的启动映像上  
 **问题：** 基于 LTI OEM 任务序列模板的任务序列显示在具有不同处理器体系结构的启动映像上。 例如，部署 64 位操作系统的 OEM 任务序列显示在 32 位启动映像上。  

 **可能的解决方案：** 这是预期行为，原因是 LTI 中的 OEM 任务序列不被视为“特定于平台”，因此无论启动映像的处理体系结构如何，都将列出它。  

####  <a name="BadTaskSequenceItem"></a>Windows 部署向导中显示“任务序列项错误\(OS GUID 无效\)”消息  
 **问题：** 运行 Windows 部署向导时，向导显示“任务序列项错误\(OS GUID 无效\)”这一错误消息。 操作系统位于 OperatingSystem.xml 文件；但部署工作台中不显示操作系统。  

 **可能的解决方案：** 原始操作系统源具有两个或更多关联的 WIM 文件。 已删除与任务序列关联的 SKU；但操作系统源的其他 SKU 仍然存在。 如果在 Windows 部署向导的“选择要在此计算机上执行的任务序列”向导页上选择引用已删除的 SKU 的任务序列，则在单击向导页上的“下一步”后将出现“任务序列项错误\(OS GUID 无效\)”错误消息。  

 要解决此问题，请执行以下任务之一：  

-   删除操作系统源中的所有 SKU。 之后，Windows 部署向导正常工作且不显示错误消息。  

-   将任务序列更改为使用其他操作系统映像。  

####  <a name="ApplyNetworkSettings"></a>应用网络设置  
 **问题：** 在部署工作台中配置网络连接名称时，系统出现验证错误，显示“请输入有效的网络适配器名称”消息。  

 **可能的解决方案：** 删除指定的连接名称中的全部空格和无效字符。  

####  <a name="UseContinueonError"></a>使用“出错时继续”  
 如果 MDT 任务序列配置为出错时不继续操作，且该任务序列返回错误，则系统跳过该任务序列组中所有未执行的任务序列。 但是，要处理剩余的任务序列组。 请考虑下列各项：  

 创建了两个任务序列组，其中一个组包含多个任务序列步骤：  

-   组 A  

    -   步骤 A  

    -   步骤 B  

-   组 B  

    -   步骤 A  

    -   步骤 B  

 如果组 A\\步骤 A 配置为出错时不继续操作，则不处理组 A\\步骤 B。 但会处理组 B 中的所有任务序列步骤。  

### <a name="the-user-state-migration-tool"></a>用户状态迁移工具  
 查看 USMT 相关问题和解决方案：  

-   指向网络共享文件夹中的文档的快捷方式可能未正确还原，如[缺少桌面快捷方式](#MissingDesktopShortcuts)中所述。  

####  <a name="MissingDesktopShortcuts"></a>缺少桌面快捷方式  
 **问题：** 使用 USMT 迁移用户数据时，可能未还原指向网络文档的快捷方式。 Scanstate 期间捕获了快捷方式，但永不在 Loadstate 期间还原到目标计算机。  

 **可能的解决方案：** 编辑 MigUser.xml 文件并对以下行添加注释：  

 原始：  

```  
<include> filter='MigXmlHelper.IgnoreIrrelevantLinks()'>  
```  

 修改后：  

```  
<include> <!-- filter='MigXmlHelper.IgnoreIrrelevantLinks()'> -->  
```  

### <a name="windows-imaging-format-files"></a>Windows 映像格式文件  
 查看 WIM 相关问题和解决方案：  

-   LTI 和 ZTI 部署失败，BDD.log 文件中出现 WIM 文件错误，如 [WIM 文件已损坏](#CorruptWIMFile)中所述，。  

####  <a name="CorruptWIMFile"></a>WIM 文件已损坏  
 **问题：** 部署映像时部署失败，且 BDD.log 中显示以下项：  

-   ```  
    The image \\Server\Deployment$\Operating Systems\Windows\version1.wim was not applied successfully by ImageX, rc = 2  
    ```  

-   ```  
    LTIApply COMPLETED.  Return Value = 2  
    ```  

-   ```  
    ZTI ERROR - Non-zero return code by LTIApply, rc = 2  
    ```  

 使用“数据无效”错误中的 ImageX 结果装载 WIM 文件，进行问题调查。 进一步的调查显示 .wim 文件的日期戳比当前日期早很多年。 情况可能是之前在读取或写入进程结束时关闭 .wim 文件之后，还有一个进程（例如病毒扫描程序）正在将此文件保持在打开状态。  

 **可能的解决方案：** 通过备份媒体还原 .wim 文件。  

### <a name="windows-pe"></a>Windows PE  
 查看 Windows PE 相关问题和解决方案：  

-   由于 RAM 或无线网络适配器内存不足，未启动 LTI 或 ZTI 部署进程，如[未启动部署进程 - RAM 或无线网络适配器内存有限](#LimitedRamorWirelessNetworkAdapter)中所述。  

-   由于缺少 Windows PE 组件，未启动 LTI 或 ZTI 部署进程，如[未启动部署进程 - 缺少组件](#MissingComponents)中所述。  

-   由于设备驱动程序缺失或不适合，未启动 LTI 或 ZTI 部署进程，如[未启动部署进程 - 驱动程序缺失或不适合](#MissingorIncorrectDrivers)中所述。  

####  <a name="LimitedRamorWirelessNetworkAdapter"></a>未启动部署进程 - RAM 或无线网络适配器内存有限  
 **问题：** 将映像部署到某些目标计算机时，Windows PE 将启动、运行“wpeinit”并打开命令提示符窗口，但实际上未启动部署进程。 通过映射来自目标计算机的网络驱动程序排查问题时发现未加载网络适配器驱动程序。  

 **可能的解决方案 1：** 由于 RAM 内存不足，不启动部署向导。 请验证确保目标计算机至少具有 512 MB 的 RAM，且共享视频所占内存不超过 64 MB（共 512 MB）。  

 MDT 支持的 Windows PE 版本不可在 RAM 内存量小于 512 MB 的目标计算机上运行。  

 **可能的解决方案 2：** 不要在 Windows PE 映像中包含无线驱动程序。  

####  <a name="MissingComponents"></a>未启动部署进程 - 缺少组件  
 **问题：** 排查失败的部署时，BDD.log 文件的评审列出以下项：  

```  
ERROR - Unable to create ADODB.Connection object, impossible to query SQL Server: ActiveX component can't create object (429).  
```  

 **可能的解决方案：** 此错误可能表示 Windows PE 映像不是使用 MDT 创建的。 如果使用的是 Configuration Manager，则不要使用此管理器创建的任何现有 Windows PE 映像，转而使用“导入 Microsoft 部署任务序列”向导创建映像。  

> [!NOTE]
>  Configuration Manager 创建的 Windows PE 映像包含支持脚本编写、XML 和 Windows Management Instrumentation (WMI) 的组件，但不具备支持 Microsoft ActiveX® 数据对象 (ADO) 的组件。  

####  <a name="MissingorIncorrectDrivers"></a>未启动部署进程 - 驱动程序缺失或不适合  
 **问题：** 在部署到某些目标计算机时，Windows PE 将启动、运行“wpeinit”并打开命令提示符窗口，但实际上未启动部署进程。 通过映射来自目标计算机的网络驱动器排除故障时发现未加载网络适配器驱动程序。 X:\Windows\System32\Inf 中的 SetupAPI.log 文件评审指出，Windows PE 在配置网络适配器时生成错误，其中一个错误为“此驱动程序不可用于此平台。” 已将“现成可用的驱动程序”列表中的驱动程序加入到映像中。  

 **可能的解决方案：** Windows PE 的某个驱动程序可能与其他驱动程序冲突。 在部署工作台中配置 Windows PE 映像的设置时，创建仅包含网络适配器和存储驱动程序的 Windows PE 驱动程序组，然后将部署共享配置为仅使用 Windows PE 驱动程序组。  

## <a name="deployment-process-flow-charts"></a>部署过程流程图  
 本节提供两组 MDT 流程图：分别用于 LTI 部署和借助 Configuration Manager 的 ZTI 部署。 每个流程图都显示此部署类型期间运行的任务。  

 请通过以下方式熟悉部署过程流程图：  

-   查看 LTI 部署过程流程图，如 [LTI 部署过程流程图](#LTIDeploymentProcessFlowcharts)中所述  

-   查看 ZTI 部署过程流程图，如 [ZTI 部署过程流程图](#ZTIDevelopmentProcessFlowcharts)中所述  

###  <a name="LTIDeploymentProcessFlowcharts"></a>LTI 部署过程流程图  
 提供的流程图具有以下阶段：  

-   验证（图 4）  

-   状态捕获（图 5 和图 6）  

-   预安装（图 7、图 8 和图 9）  

-   安装（图 10）  

-   后安装（图 11 和图 12）  

-   状态还原（图 13、图 14、图 15 和图 16）  

 ![TroubleshootingReference4](media/TroubleshootingReference4.jpg "TroubleshootingReference4")  
图 4。 验证阶段流程图  

 **图 4.验证阶段流程图**  

 ![TroubleshootingReference5](media/TroubleshootingReference5.jpg "TroubleshootingReference5")  
图 5. 状态捕获阶段流程图第 1 部分（共 2 部分）  

 **图 5.状态捕获阶段流程图第 1 部分（共 2 部分）**  

 ![TroubleshootingReference6](media/TroubleshootingReference6.jpg "TroubleshootingReference6")  
图 6. 状态捕获阶段流程图第 2 部分（共 2 部分）  

 **图 6.状态捕获阶段流程图第 2 部分（共 2 部分）**  

 ![TroubleshootingReference7](media/TroubleshootingReference7.jpg "TroubleshootingReference7")  
图 7. 预安装阶段流程图第 1 部分（共 3 部分）  

 **图 7.预安装阶段流程图第 1 部分（共 3 部分）**  

 ![TroubleshootingReference8](media/TroubleshootingReference8.jpg "TroubleshootingReference8")  
图 8. 预安装阶段流程图第 2 部分（共 3 部分）  

 **图 8.预安装阶段流程图第 2 部分（共 3 部分）**  

 ![TroubleshootingReference9](media/TroubleshootingReference9.jpg "TroubleshootingReference9")  
图 9. 预安装阶段流程图第 3 部分（共 3 部分）  

 **图 9.预安装阶段流程图第 3 部分（共 3 部分）**  

 ![TroubleshootingReference10](media/TroubleshootingReference10.jpg "TroubleshootingReference10")  
图 10. 安装阶段流程图  

 **图 10.安装阶段流程图**  

 ![TroubleshootingReference11](media/TroubleshootingReference11.jpg "TroubleshootingReference11")  
图 11. 后安装阶段流程图第 1 部分（共 2 部分）  

 **图 11.后安装阶段流程图第 1 部分（共 2 部分）**  

 ![TroubleshootingReference12](media/TroubleshootingReference12.jpg "TroubleshootingReference12")  
图 12. 后安装阶段流程图第 2 部分（共 2 部分）  

 **图 12. 后安装阶段流程图第 2 部分（共 2 部分）**  

 ![TroubleshootingReference13](media/TroubleshootingReference13.jpg "TroubleshootingReference13")  
图 13. 状态还原阶段流程图第 1 部分（共 4 部分）  

 **图 13.状态还原阶段流程图第 1 部分（共 4 部分）**  

 ![TroubleshootingReference14](media/TroubleshootingReference14.jpg "TroubleshootingReference14")  
图 14. 状态还原阶段流程图第 2 部分（共 4 部分）  

 **图 14.状态还原阶段流程图第 2 部分（共 4 部分）**  

 ![TroubleshootingReference15](media/TroubleshootingReference15.jpg "TroubleshootingReference15")  
图 15. 状态还原阶段流程图第 3 部分（共 4 部分）  

 **图 15.状态还原阶段流程图第 3 部分（共 4 部分）**  

 ![TroubleshootingReference16](media/TroubleshootingReference16.jpg "TroubleshootingReference16")  
图 16. 状态还原阶段流程图第 4 部分（共 4 部分）  

 **图 16.状态还原阶段流程图第 4 部分（共 4 部分）**  

###  <a name="ZTIDevelopmentProcessFlowcharts"></a>ZTI 部署过程流程图  
 对于借助 Configuration Manager 的 ZTI 部署，提供的流程图具有以下阶段：  

-   初始化（图 17）  

-   验证（图 18）  

-   状态捕获（图 19）  

-   预安装（图 20）  

-   安装（图 21）  

-   后安装（图 22）  

-   状态还原（图 23 和图 24）  

-   捕获（图 25）  

 ![TroubleshootingReference17](media/TroubleshootingReference17.jpg "TroubleshootingReference17")  
图 17. 初始化阶段流程图  

 **图 17.初始化阶段流程图**  

 ![TroubleshootingReference18](media/TroubleshootingReference18.jpg "TroubleshootingReference18")  
图 18. 验证阶段流程图  

 **图 18.验证阶段流程图**  

 ![TroubleshootingReference19](media/TroubleshootingReference19.jpg "TroubleshootingReference19")  
图 19. 状态捕获阶段流程图  

 **图 19.状态捕获阶段流程图**  

 ![TroubleshootingReference20](media/TroubleshootingReference20.jpg "TroubleshootingReference20")  
图 20. 预安装阶段流程图  

 **图 20.预安装阶段流程图**  

 ![TroubleshootingReference21](media/TroubleshootingReference21.jpg "TroubleshootingReference21")  
图 21. 安装阶段流程图  

 **图 21.安装阶段流程图**  

 ![TroubleshootingReference22](media/TroubleshootingReference22.jpg "TroubleshootingReference22")  
图 22. 后安装阶段流程图  

 **图 22.后安装阶段流程图**  

 ![TroubleshootingReference23](media/TroubleshootingReference23.jpg "TroubleshootingReference23")  
图 23. 状态还原阶段流程图第 1 部分（共 2 部分）  

 **图 23.状态还原阶段流程图第 1 部分（共 2 部分）**  

 ![TroubleshootingReference24](media/TroubleshootingReference24.jpg "TroubleshootingReference24")  
图 24. 状态还原阶段流程图第 2 部分（共 2 部分）  

 **图 24.状态还原阶段流程图第 2 部分（共 2 部分）**  

 ![TroubleshootingReference25](media/TroubleshootingReference25.jpg "TroubleshootingReference25")  
图 25. 捕获阶段流程图  

 **图 25.捕获阶段流程图**  

## <a name="finding-additional-help"></a>查找更多帮助  
 采用以下方式在 MDT 部署问题解决方面获取更多帮助：  

-   联系 Microsoft 支持部门，详见 [Microsoft 支持部门](#MicrosoftSupport)  

-   通过博客和其他 Internet 资源获取其他支持，详见 [Internet 支持](#InternetSupport)  

###  <a name="MicrosoftSupport"></a>Microsoft 支持部门  
 Microsoft 针对 Microsoft Deployment Toolkit 提供了顶级和专业级支持。  

 专业级支持：[http://support.microsoft.com/](http://support.microsoft.com/)  

 顶级支持：[https://premier.microsoft.com/](https://premier.microsoft.com/)  

> [!NOTE]
>  联系支持部门时，请说明问题与 MDT 有关并提供具体版本。  

###  <a name="InternetSupport"></a>Internet 支持  
 许多联机源都额外提供了本参考中未涉及的 MDT 故障排除协助。 此类联机源包括：  

-   Microsoft 托管的博客  

    -   [MDT 团队博客](http://blogs.technet.com/b/msdeployment/)  

    -   [Configuration Manager 团队博客](http://blogs.technet.com/b/configmgrteam/)  

    -   [Michael Niehaus 的博客](http://blogs.technet.com/b/mniehaus/)（Michael Niehaus 在博客上撰写与 Windows 和 Microsoft Office 部署相关的内容。）  

-   Microsoft 托管的新闻组和论坛：  

     可在下述新闻组和论坛中获取来自 Microsoft 员工、业内同行和 Microsoft 宝贵专家的支持：  

    -   [Configuration Manager - 操作系统部署](http://social.technet.microsoft.com/Forums/home?forum=configmanagerosd)  

    -   [Windows 8 安装、设置和部署](http://social.technet.microsoft.com/Forums/windows/home?forum=w8itproinstall)  

-   来自 Microsoft 外部的相关部署信息源：  

    -   [DeployVista.com](http://www.deployvista.com/)  

    -   [myITforum.com](http://www.myitforum.com/)
