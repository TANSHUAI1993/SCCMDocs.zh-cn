---
title: 创建独立媒体
titleSuffix: Configuration Manager
description: 使用独立媒体在无网络连接的计算机上部署操作系统。
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cdf2c0e1501707e836c914265e0edf2d9c88521f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138051"
---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建独立媒体

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 中的独立媒体包含在无网络连接的计算机上部署操作系统 (OS) 所需的所有内容。 在以下 OS 部署方案中使用独立媒体：  

-   [使用新版的 Windows 刷新现有的计算机](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)  

-   [将 Windows 升级到最新版本](upgrade-windows-to-the-latest-version.md)  

独立媒体包含自动执行用于安装 OS 和所有其他所需内容的步骤的任务序列。 此内容包括启动映像、操作系统映像和设备驱动程序。 由于部署 OS 所需的所有内容均存储在独立媒体上，因此，独立媒体所需的磁盘空间将显著大于其他类型的媒体所需的磁盘空间。 在管理中心站点上创建独立媒体时，客户端会从 Active Directory 检索其分配的站点代码。 在子站点上创建的独立媒体会自动将该站点的站点代码分配给客户端。  

##  <a name="BKMK_CreateStandAloneMedia"></a>创建独立媒体  
在使用“创建任务序列媒体向导”创建独立媒体之前，请确保满足以下条件：  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>创建用于部署操作系统的任务序列
作为独立媒体的一部分，必须指定用于部署操作系统的任务序列。 有关创建新任务序列的步骤，请参阅[在 System Center Configuration Manager 中创建用于安装操作系统的任务序列](create-a-task-sequence-to-install-an-operating-system.md)。

独立媒体不支持下列操作：
- 任务序列中的“自动应用驱动程序”步骤。 独立媒体不支持自动应用驱动程序目录中的设备驱动程序。 可使用“应用驱动程序包”步骤以使一组特定驱动程序可用于 Windows 安装程序。
- 任务序列中的“下载包内容”步骤。 管理点信息在独立媒体上不可用，因此该步骤尝试枚举内容位置将失败。
- 安装软件更新。
- 在部署操作系统之前安装软件。
- 用于非操作系统部署的任务序列。
- 将用户与目标计算机关联以支持用户设备相关性。
- 通过“安装包”任务安装动态程序包。
- 通过“安装应用程序”任务安装动态应用程序。

> [!NOTE]    
> 如果任务序列包括[安装包](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage)步骤，并且在管理中心站点创建独立媒体，则可能发生错误。 管理中心站点没有必需的客户端配置策略。 在执行任务序列期间启用软件分发代理时需要这些策略。 在 CreateTsMedia.log 文件中可能会出现以下错误：    
>     
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`    
> 
> 对于包括“安装包”步骤的独立媒体，请在已启用软件分发代理的主站点创建独立媒体。 
>
> 或者，在任务序列的[安装 Windows 和 ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) 步骤之后和第一个“安装包”步骤之前，添加[运行命令行](../understand/task-sequence-steps.md#BKMK_RunCommandLine)步骤。 “运行命令行”步骤运行以下 WMIC 命令，以便在第一个“安装包”步骤运行之前启用软件分发代理：    
>    
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`


> [!IMPORTANT]    
> 请勿选择独立媒体“安装 Windows 和 ConfigMgr”任务序列步骤中的“使用可用的预生产客户端包”设置。 独立媒体不支持使用此设置。 有关此设置的详细信息，请参阅[安装 Windows 和 ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)。


### <a name="distribute-all-content-associated-with-the-task-sequence"></a>分发与任务序列关联的所有内容
将任务序列所需的所有内容至少分发到一个分发点。 此内容包括启动映像、操作系统映像和其他相关联的文件。 向导在创建独立媒体时从分发点中收集信息。 必须具有对该分发点上的内容库的**读取**访问权限。 有关详细信息，请参阅[任务序列引用的分发内容](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS)。

### <a name="prepare-the-removable-usb-drive"></a>准备可移动的 USB 驱动器
*对于可移动的 USB 驱动器：*

如果使用可移动 U 盘，需将 U 盘连接到运行该向导的计算机。 U 盘必须可被 Windows 识别为可移动设备。 向导将在创建媒体时直接写入 USB 驱动器。 独立媒体使用 FAT32 文件系统。 如果独立媒体的内容包含超过 4 GB 大小的文件，则无法在 USB 闪存驱动器上创建独立媒体。

### <a name="create-an-output-folder"></a>创建一个输出文件夹
*对于 CD/DVD 集：*

在运行创建任务序列媒体向导以便为 CD 或 DVD 集创建媒体之前，你必须为向导创建的输出文件创建一个文件夹。 为 CD 或 DVD 集创建的媒体将以 .iso 文件形式直接写入该文件夹。


 使用下列过程来为可移动的 USB 驱动器或 CD/DVD 集创建独立媒体。  

## <a name="to-create-stand-alone-media"></a>创建独立媒体  

1. 在 Configuration Manager 控制台中，单击“软件库”。  

2. 在“软件库”工作区中，展开“操作系统”，然后单击“任务序列”。  

3. 在“主页”选项卡上的“创建”组中，单击“创建任务序列媒体”，以启动创建任务序列媒体向导。  

4. 在“选择媒体类型”页上，指定以下选项，然后单击“下一步”。  

   -   选择“独立媒体”。  

   -   （可选）如果你希望允许在不需要用户输入的情况下部署操作系统，则选择“允许无人参与的操作系统部署”。 如果选择此选项，则不会提示用户输入网络配置信息或可选的任务序列。 如果针对密码保护配置了媒体，则仍会提示用户输入密码。  

5. 在“媒体类型”页，指定媒体是可移动 U 盘还是 CD/DVD 盘：  

   > [!IMPORTANT]  
   >  默认情况下，独立媒体使用 FAT32 文件系统。 如果独立媒体的内容包含超过 4 GB 大小的文件，则无法在可移动 U 盘上创建独立媒体。  

   - 如果选择“可移动 U 盘”，则指定要在其中存储内容的驱动器。  

     - **格式化可移动 U 盘 (FAT32) 并使其可启动**：默认情况下，让 Configuration Manager 准备 USB 驱动器。 很多较新的 UEFI 设备都需要可启动的 FAT32 分区。 但是，此格式还限制文件的大小和驱动器的总容量。 如果已格式化并配置了可移动驱动器，请禁用此选项。 

   - 如果选择“CD/DVD 集”，请指定媒体的容量以及输出文件的名称和路径。 向导会将输出文件写入到此位置。 例如：**\\\servername\folder\outputfile.iso**  

      如果媒体的容量太小，无法存储整个内容，则会创建多个文件，从而必须将内容存储在多张 CD 或 DVD 上。 当需要多个媒体时，Configuration Manager 会在创建的每个输出文件的名称中添加序号。 此外，如果将应用程序与操作系统一起部署，而单个媒体无法容纳应用程序，则 Configuration Manager 会将应用程序存储到多个媒体中。 在运行独立媒体时，Configuration Manager 会提示用户提供下一个存储了应用程序的媒体。   

      > [!IMPORTANT]  
      >  如果选择现有的 .iso 映像，任务序列媒体向导将在你进入向导的下一页后立即从驱动器或共享中删除该映像。 即使随后取消该向导，也会删除这个现有的映像。  

     单击“下一步” 。  

6. 在“安全”页，从以下设置中进行选择，然后单击“下一步”：
   - **使用密码保护媒体**：输入强密码来帮助保护媒体。 如果指定了密码，则必须提供密码才能使用媒体。  

       > [!IMPORTANT]  
       >  在独立媒体上，只会加密任务序列步骤及其变量。 不会加密媒体的其余内容，因此，请勿在任务序列脚本中包含任何敏感信息。 请使用任务序列变量来存储和提供所有敏感信息。  

   - **选择此独立媒体的有效日期范围**（从版本 1702 开始）：在媒体上设置可选的开始日期和到期日期。 默认情况下，这些设置处于禁用状态。 独立介质运行前，该日期将与计算机上的系统时间进行比较。 如果系统时间早于开始时间或晚于过期时间，则独立介质不会启动。 也可通过使用 New-CMStandaloneMedia PowerShell cmdlet 启用这些选项。
7. 在“独立 CD/DVD”页上，指定将部署操作系统的任务序列，然后单击“下一步”。 选择“检测关联的应用程序依赖项并将其添加到此媒体”以将内容添加到应用程序依赖项的独立媒体中。
   > [!TIP]
   > 如果你未看到想要的应用程序依赖项，请取消选中并重新选择“检测关联的应用程序项并将其添加到此媒体”设置以刷新列表。

   向导允许你仅选择那些与启动映像关联的任务序列。  

8. 在“选择应用程序”页（从版本 1702 开始），指定应用程序内容以作为媒体文件的一部分内容，然后单击“下一步”。
9. 在“选择程序包”页（从版本 1702 开始），指定程序包内容以作为媒体文件的一部分，然后单击“下一步”。
10. 在“选择驱动程序包”页（从版本 1702 开始），指定驱动程序包内容以作为媒体文件的一部分，然后单击“下一步”。
11. 在“分发点”页上，指定包含任务序列所需的内容的分发点，然后单击“下一步”。  

    Configuration Manager 仅显示具有内容的分发点。 先将与任务序列相关联的所有内容分发到至少一个分发点上，然后再继续操作。 在分发内容后，刷新分发点列表。 删除此页中已选中的任何分发点，然后返回到“分发点”页。 或者，重启该向导。 有关详细信息，请参阅[分发任务序列引用的内容](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS)和[管理内容和内容基础结构](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)  

    > [!NOTE]  
    >  必须具有对分发点上的内容库的“读取”访问权限。  

12. 在“自定义”  页上，指定以下信息，然后单击“下一步” 。  

    -   指定任务序列用于部署操作系统的变量。  

    -   指定要在任务序列之前运行的任何预启动命令。 预启动命令是在任务序列启动之前在 Windows PE 中运行的一个脚本或可执行文件。 有关详细信息，请参阅[任务序列媒体的预启动命令](../understand/prestart-commands-for-task-sequence-media.md)。  

         选择“包括预启动命令的文件”，以包括预启动命令所需的任何文件（可选）。  

        > [!TIP]  
        >  在创建任务序列媒体期间，Configuration Manager 将包 ID 和预启动命令行写入到运行 Configuration Manager 控制台的计算机上的 CreateTSMedia.log 文件。 此输出包括任何任务序列变量的值。 查看此日志文件以验证任务序列变量的值。  

13. 完成向导。  

    在目标文件夹中创建独立媒体文件 (.iso)。 如果选择了“独立 CD/DVD”，现在可以将输出文件复制到一组 CD 或 DVD。  

##  <a name="BKMK_StandAloneMediaTSExample"></a>独立媒体的任务序列示例  
 使用下表作为指导，使用独立媒体创建用于部署操作系统的任务序列。 此表有助于你决定任务序列步骤的一般序列。 它还有助于将任务序列步骤组织到逻辑组中并进行构造。 您创建的任务序列可能与此示例有所不同并可以包含多个或更少的任务序列步骤和组。  

> [!NOTE]  
>  您始终必须使用任务序列媒体向导来创建独立媒体。  

|任务序列组或步骤|说明|  
|---------------------------------|-----------------|  
|捕获文件和设置 - **（新建任务序列组）**|创建任务序列组。 任务序列组将保留在一起以更好地组织和错误控制类似的任务序列步骤。|  
|捕获 Windows 设置|使用此任务序列步骤在重置映射之前从目标计算机捕获 Windows 设置。 捕获计算机名称、用户和组织信息以及时区设置。|  
|捕获网络设置|使用此任务序列步骤来从接收任务序列的计算机捕获网络设置。 您可以捕获计算机和网络适配器的设置信息的域或工作组成员身份。|  
|捕获用户文件和设置 - （新的任务序列子组）|创建任务序列组内的一个任务序列组。 此子组包含在重置映像之前，从目标计算机捕获用户状态数据的步骤。 与添加的初始组类似，此子组将相似的任务序列步骤保存到一起，以实现更好的组织和错误控制。|  
|设置本地状态位置|使用此任务序列步骤来指定使用受保护的路径任务序列变量的本地位置。 用户状态存储在硬盘驱动器上受保护的目录中。|  
|捕获用户状态|使用此任务序列步骤以捕获用户文件和您想要迁移到新操作系统的设置。|  
|安装操作系统 - **（新建任务序列组）**|创建另一个任务序列子组。 此子组包含安装操作系统所需的步骤。|  
|重新启动到 Windows PE 或硬盘|使用此任务序列步骤来指定接收此任务序列的计算机的重新启动选项。 此步骤向用户显示一条消息：计算机将重启以继续该安装。<br /><br /> 此步骤使用只读 **_SMSTSInWinPE** 任务序列变量。 如果相关联的值等于 false 任务序列步骤将继续。|  
|应用操作系统|使用此任务序列步骤安装到目标计算机上的操作系统映像。 此步骤将删除该卷上的所有文件，但 Configuration Manager 特定的控制文件除外。 然后，它会将 WIM 文件中包含的所有卷映像应用到相应的顺序磁盘卷上。 你还可以指定“sysprep”答案文件以配置要用于安装的磁盘分区。|  
|应用 Windows 设置|使用此任务序列步骤配置目标计算机的 Windows 设置配置信息。 这些设置包括用户和组织信息、产品或许可密钥信息、时区，以及本地管理员密码。|  
|应用网络设置|使用此任务序列步骤来指定为目标计算机的网络或工作组配置信息。 此外可以指定计算机使用 DHCP 服务器是否可以静态地分配的 IP 地址信息。|  
|应用驱动程序包|使用此任务序列步骤以使驱动程序包中所有设备驱动程序可用于使用 Windows 安装程序。 所有必要的设备驱动程序必须包含在独立媒体中。|  
|设置操作系统 - **（新建任务序列组）**|创建另一个任务序列子组。 此子组包含安装 Configuration Manager 客户端所需的步骤。|  
|安装 Windows 和 ConfigMgr|使用此任务序列步骤安装 Configuration Manager 客户端软件。 Configuration Manager 安装和注册 Configuration Manager 客户端 GUID。 你可以在“安装属性”窗口中分配必要的安装参数。|  
|还原用户文件和设置 - **（新建任务序列组）**|创建另一个任务序列子组。 此子组包含还原用户状态所需的步骤。|  
|还原用户状态|使用此任务序列步骤来启动用户状态迁移工具 (USMT)。 USMT 将之前使用“捕获用户状态”步骤捕获到的用户状态和设置还原到目标计算机。|  
