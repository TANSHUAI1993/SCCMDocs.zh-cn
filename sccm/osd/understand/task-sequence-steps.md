---
title: 任务序列步骤
titleSuffix: Configuration Manager
description: 了解可添加到 Configuration Manager 任务序列的步骤。
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5e62983f76b0f2a4277edfab08d4321da5d4a258
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416480"
---
# <a name="task-sequence-steps-in-configuration-manager"></a>Configuration Manager 中的任务序列步骤

 适用范围：System Center Configuration Manager (Current Branch)

 以下任务序列步骤可添加到 Configuration Manager 任务序列中。 有关编辑任务序列的信息，请参阅 [Edit a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence)。  

 以下设置常见于所有任务序列步骤：

#### <a name="properties-tab"></a>“属性”选项卡
 - **名称**：任务序列编辑器要求指定一个短名称，用于描述此步骤。 添加新步骤时，任务序列编辑器默认将名称设置为“Type”。 名称的长度不能超过 50 个字符。  

 - **描述**：（可选）指定有关此步骤的更多详细信息。 说明的长度不能超过 256 个字符。  


 本文的其余部分将介绍每个任务序列步骤的“属性”选项卡上的其他设置。

#### <a name="options-tab"></a>“选项”选项卡  

 - **禁用此步骤**：任务序列在计算机上运行时，会跳过此步骤。 此步骤的图标在任务序列编辑器中灰显。  

 - **出错时继续**：如果在运行该步骤时出现错误，继续执行任务序列。 有关详细信息，请参阅[计划自动执行任务时的考虑事项](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSGroups)。   

 - **添加条件**：任务序列判断这些条件语句，以确定其是否运行该步骤。 有关使用任务序列变量作为条件的示例，请参阅[如何使用任务序列变量](/sccm/osd/understand/using-task-sequence-variables#bkmk_access-condition)。   


 有关特定任务序列步骤的以下各节介绍了“选项”选项卡上的其他可能设置。



##  <a name="BKMK_ApplyDataImage"></a>应用数据映像   

 使用本步骤将数据映像复制到指定目标分区。  

 此步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。 

 在此步骤中使用以下任务序列变量：  
 - [OSDDataImageIndex](/sccm/osd/understand/task-sequence-variables#OSDDataImageIndex)  
 - [OSDWipeDestinationPartition](/sccm/osd/understand/task-sequence-variables#OSDWipeDestinationPartition)  


 单击任务序列编辑器中的“添加”，选择“映像”，然后选择“应用数据映像”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="image-package"></a>映像包  
 单击“浏览”以指定供此任务序列使用的“映像包”。 在“选择包”对话框中选择要安装的包。 每个现有映像包的关联属性信息显示在对话框的底部。 使用下拉列表，从所选的“映像包”中选择要安装的“映像”。  

 > [!NOTE]  
 >  此任务序列操作将映像视为数据文件。 此操作不会执行任何安装来将映像作为 OS 进行启动。  

#### <a name="destination"></a>目标  
 配置下列选项之一：

 - **下一个可用分区**：使用此任务序列中尚未被“应用操作系统”或“应用数据映像”步骤作为目标的下一个顺序分区。  

 - **特定磁盘和分区**：选择“磁盘”编号（从 0 开始）和“分区”编号（从 1 开始）。  

 - **特定逻辑驱动器号**：指定 Windows PE 分配给分区的“驱动器号”。 此驱动器号可不同于新部署的 OS 分配的驱动器号。  

 - **变量中存储的逻辑驱动器号**：指定包含 Windows PE 分配给分区的驱动器号的任务序列变量。 对于“格式化磁盘并分区”任务序列步骤，此变量通常在“分区属性”对话框的“高级”部分中设置。  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>应用映像之前删除分区中的所有内容  
 指定任务序列在安装映像前删除目标分区中的所有文件。 如果不删除分区内容，则此操作可用于将其他内容应用到以前的目标分区。  



##  <a name="BKMK_ApplyDriverPackage"></a>应用驱动程序包  

 使用此步骤可下载驱动程序包中的所有驱动程序，并将其安装在 Windows OS 上。

 “应用驱动程序包”任务序列步骤使 Windows 可以使用驱动程序包中的所有设备驱动程序。 将此步骤添加到“应用操作系统”与“安装 Windows 和 ConfigMgr”步骤之间，使包中的驱动程序可以用于 Windows。 通常，“应用驱动程序包”步骤位于“自动应用驱动程序”任务序列步骤之后。 “应用驱动程序包”任务序列步骤也可以与独立媒体部署方案配合使用。  

 将类似的设备驱动程序放入驱动程序包，并将其分发到合适的分发点。 例如，将一个制造商的所有驱动程序放入一个驱动程序包。 然后将该程序包分发到关联计算机可以对其进行访问的分发点。

 “应用驱动程序包”步骤可用于独立媒体。 此步骤也可用于安装一组特定的驱动程序。 这些类型的驱动程序包括 Windows 即插即用扫描检测不到的设备，例如网络打印机。  

 此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。 

 在此步骤中使用以下任务序列变量：  
 - [OSDApplyDriverBootCriticalContentUniqueID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalContentUniqueID)  
 - [OSDApplyDriverBootCriticalHardwareComponent](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalHardwareComponent)  
 - [OSDApplyDriverBootCriticalID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalID)  
 - [OSDApplyDriverBootCriticalINFFile](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalINFFile)  
 - [OSDInstallDriversAdditionalOptions](/sccm/osd/understand/task-sequence-variables#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->（从版本 1806 开始）  


 单击任务序列编辑器中的“添加”，选择“驱动程序”，然后选择“应用驱动程序包”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="driver-package"></a>驱动程序包
 指定包含所需的设备驱动程序的驱动程序包。 单击“浏览”以启动“选择包”对话框。 选择要应用的现有驱动程序包。 关联的包属性显示在对话框底部。  

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>选择包中需要安装的大容量存储驱动程序，然后在 Windows Vista 以前的操作系统上安装
 指定安装经典 OS 时所需的任何大容量存储驱动程序。  

#### <a name="driver"></a>驱动程序
 选择要在安装经典 OS 前安装的大容量存储驱动程序文件。 下拉列表根据指定包填充。  

#### <a name="model"></a>型号  
 指定 Windows Vista 之前的 OS 部署需要的启动关键设备。  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>在 Windows 版本上对未签名的驱动程序执行允许的无人参与安装
 此选项允许 Windows 安装没有数字签名的驱动程序。  



##  <a name="BKMK_ApplyNetworkSettings"></a>应用网络设置   

 使用此步骤指定目标计算机的网络或工作组配置信息。 任务序列将这些值存储在相应的答案文件中。 Windows 安装程序在“安装 Windows 和 ConfigMgr”操作过程中使用该答案文件。  

 此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。 

 在此步骤中使用以下任务序列变量：  
 - [OSDAdapter](/sccm/osd/understand/task-sequence-variables#OSDAdapter)  
 - [OSDAdapterCount](/sccm/osd/understand/task-sequence-variables#OSDAdapterCount)  
 - [OSDDNSDomain](/sccm/osd/understand/task-sequence-variables#OSDDNSDomain)  
 - [OSDDNSSuffixSearchOrder](/sccm/osd/understand/task-sequence-variables#OSDDNSSuffixSearchOrder)  
 - [OSDDomainName](/sccm/osd/understand/task-sequence-variables#OSDDomainName)  
 - [OSDDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDDomainOUName)  
 - [OSDEnableTCPIPFiltering](/sccm/osd/understand/task-sequence-variables#OSDEnableTCPIPFiltering)  
 - [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)  
 - [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)  
 - [OSDWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDWorkgroupName)  


 单击任务序列编辑器中的“添加”，选择“设置”，然后选择“应用网络设置”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="join-a-workgroup"></a>加入工作组
 选择此选项，使目标计算机加入指定的工作组。 在“工作组”行中输入工作组的名称。 此值可被“捕获网络设置”任务序列步骤所捕获的值替代。 

#### <a name="join-a-domain"></a>加入域
 选择此选项以将目标计算机加入指定的域。 指定或浏览到域，如 `fabricam.com`。 指定或浏览到组织单位的轻型目录访问协议 (LDAP) 路径。 例如： `LDAP//OU=computers, DC=Fabricam.com, C=com`。  

#### <a name="account"></a>帐户
 单击“设置”  以指定拥有将计算机加入域所需权限的帐户。 在“Windows 用户帐户”对话框中，使用下列格式输入用户名：`Domain\User`。 有关详细信息，请参阅[域连接帐户](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account)。 

#### <a name="adapter-settings"></a>适配器设置  
 指定计算机中每个网络适配器的网络配置。 单击 “新建”打开“网络设置”对话框，然后指定网络设置。 
 - 如果还使用“捕获网络设置”步骤，任务序列会将先前捕获的设置应用到网络适配器。 
 - 如果任务序列先前没有捕获网络设置，则会应用在此步骤中指定的设置。 
 - 任务序列将按 Windows 设备枚举顺序将这些设置应用到网络适配器。  
 - 任务序列不会立即将此步骤中指定的设置应用到计算机。 



##  <a name="BKMK_ApplyOperatingSystemImage"></a>应用操作系统映像  

 > [!TIP]  
 > 从 Windows 10 1709 版开始，媒体包括多个版本。 如果要将任务序列配置为使用 OS 升级包或 OS 映像，请务必选择[支持的版本](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client)。  

 使用此步骤，在目标计算机上安装 OS。 

 > [!NOTE]  
 >  “安装 Windows 和 ConfigMgr”步骤开始安装 Windows。 

 在“应用操作系统”操作运行之后，它会将 OSDTargetSystemDrive 变量设置为包含 OS 文件的分区的驱动器号。  

 此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。 

 在此步骤中使用以下任务序列变量：  
 - [OSDConfigFileName](/sccm/osd/understand/task-sequence-variables#OSDConfigFileName)  
 - [OSDImageIndex](/sccm/osd/understand/task-sequence-variables#OSDImageIndex)  
 - [OSDTargetSystemDrive](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemDrive)  


 单击任务序列编辑器中的“添加”，选择“映像”，然后选择“应用操作系统映像”以添加此步骤。 

 此步骤执行的操作具体取决于使用 OS 映像还是 OS 升级包。  

#### <a name="os-image-actions"></a>OS 映像操作
 使用 OS 映像时，“应用操作系统映像”步骤将执行以下操作：  

1. 删除目标卷中的所有内容，\_SMSTSUserStatePath 变量指定的文件夹中的文件除外。  

2. 将指定的 .wim 文件的内容提取到指定目标分区。  

3. 准备答案文件：  

   1.  为部署的 OS 创建新的默认 Windows 安装程序答案文件（sysprep.inf 或 unattend.xml）。  

   2.  合并用户提供的答案文件中的所有值。  

4. 将 Windows 启动加载程序复制到活动分区中。  

5. 设置 boot.ini 或启动配置数据库 (BCD) 来引用新安装的 OS。  

#### <a name="os-upgrade-package-actions"></a>OS 升级包操作
 使用 OS 升级包时，“应用操作系统映像”步骤将执行以下操作：  

1. 删除目标卷中的所有内容，\_SMSTSUserStatePath 变量指定的文件夹中的文件除外。  

2. 准备答案文件：  

   1.  使用 Configuration Manager 创建的标准值创建全新的答案文件。  

   2.  合并用户提供的答案文件中的所有值。  


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="apply-operating-system-from-a-captured-image"></a>从捕获的映像应用操作系统
 安装捕获的 OS 映像。 单击“浏览”以打开“选择包”对话框。 然后选择要安装的现有映像包。 如果指定的映像包关联了多个映像，请从下拉列表选择将用于此部署的关联映像。 可以通过单击每个现有映像查看有关该映像的基本信息。  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>从原始安装源应用操作系统映像
 使用 OS 升级包安装 OS，这也是原始安装源。 单击“浏览”以打开“选择和操作系统安装包”对话框。 然后选择要使用的现有 OS 升级包。 可以通过单击查看有关每个现有映像源的基本信息。 关联映像源属性显示在对话框底部的结果窗格中。 如果指定的包关联了多个版本，请使用下拉列表选择要使用的“版本”。  

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>使用无人参与或 Sysprep 答案文件进行自定义安装
 使用此选项提供 Windows 安装程序答案文件（unattend.xml、unattend.txt 或 sysprep.inf），取决于 OS 版本和安装方法。 你指定的文件可以包含 Windows 答案文件支持的任何标准的配置选项。 例如，可以使用它指定默认的 Internet Explorer 主页。 指定包含答案文件的包以及包中文件的关联路径。  

 > [!NOTE]  
 >  你提供的 Windows 安装程序答案文件可以包含形式为 `%varname%` 的嵌入任务序列变量，其中 varname 是指变量的名称。 “安装 Windows 和 ConfigMgr”步骤将变量字符串替换为实际变量值。 unattend.xml 答案文件的仅数字字段中不能使用这些嵌入的任务序列变量。  

 如果不提供 Windows 安装程序答案文件，此任务序列将自动生成一个答案文件。  

#### <a name="destination"></a>目标  
 配置下列选项之一：  

 - **下一个可用分区**：使用此任务序列中尚未被“应用操作系统”或“应用数据映像”步骤作为目标的下一个顺序分区。  

 - **特定磁盘和分区**：选择“磁盘”编号（从 0 开始）和“分区”编号（从 1 开始）。  

 - **特定逻辑驱动器号**：指定 Windows PE 分配给分区的“驱动器号”。 此驱动器号可不同于新部署的 OS 分配的驱动器号。  

 - **变量中存储的逻辑驱动器号**：指定包含 Windows PE 分配给分区的驱动器号的任务序列变量。 对于“格式化磁盘并分区”任务序列步骤，此变量通常在“分区属性”对话框的“高级”部分中设置。  


### <a name="options"></a>选项  

 除默认选项外，还可配置此任务序列步骤的“选项”选项卡上的以下其他设置：  

#### <a name="access-content-directly-from-the-distribution-point"></a>直接从分发点访问内容
 将任务序列配置为直接从分发点访问 OS 映像。 例如，在部署操作系统到存储容量有限的嵌入式设备时使用此选项。 选择此选项后，同时在 OS 映像属性的“数据访问”选项卡上配置包共享设置。  

 > [!NOTE]  
 >  此设置替代在“部署软件向导”的“分发点”页上配置的部署选项。 此替代仅适用于此步骤指定的 OS 映像，而非所有任务序列内容。  



##  <a name="BKMK_ApplyWindowsSettings"></a>应用 Windows 设置  

 使用此步骤配置目标计算机的 Windows 设置。 任务序列将这些值存储在相应的答案文件中。 Windows 安装程序在“安装 Windows 和 ConfigMgr”步骤过程中使用该答案文件。  

 此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。  

 在此步骤中使用以下任务序列变量：  
 - [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-input)  
 - [OSDLocalAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDLocalAdminPassword)  
 - [OSDProductKey](/sccm/osd/understand/task-sequence-variables#OSDProductKey)  
 - [OSDRandomAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDRandomAdminPassword)  
 - [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-input)  
 - [OSDRegisteredUserName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredUserName)  
 - [OSDServerLicenseConnectionLimit](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseConnectionLimit)  
 - [OSDServerLicenseMode](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseMode)  
 - [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-input)  


 单击任务序列编辑器中的“添加”，选择“设置”，然后选择“应用 Windows 设置”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="user-name"></a>用户名
 指定与目标计算机关联的已注册用户名。 此值可被“捕获 Windows 设置”任务序列步骤所捕获的值替代。  

#### <a name="organization-name"></a>组织名称
 指定与目标计算机关联的已注册组织名称。 此值可被“捕获 Windows 设置”任务序列步骤所捕获的值替代。  

#### <a name="product-key"></a>产品密钥  
 指定用于目标计算机上的 Windows 安装的产品密钥。  

#### <a name="server-licensing"></a>服务器授权  
 指定授权模式。 
 - 选择“每服务器”或“每用户”作为授权模式。  
 - 如果选择“每服务器”，则还需要指定每个许可协议将允许的最大连接数。  
 - 如果目标计算机不是服务器或你不想指定授权模式，请选择“不指定”。   

#### <a name="maximum-connections"></a>最大连接数
 指定许可协议中声明的可用于此计算机的最大连接数。  

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>随机生成本地管理员密码并在所有支持的平台上禁用帐户（推荐）  
 选择此选项，将本地管理员密码设为随机生成的字符串。 此选项还会对支持此功能的平台禁用本地管理员帐户。  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>启用帐户并指定本地管理员密码  
 选择此选项，以使用指定密码启用本地管理员帐户。 在“密码”行上输入密码，并在“确认密码”行上确认密码。  

#### <a name="time-zone"></a>时区
 指定要在目标计算机上配置的时区。 此值可被“捕获 Windows 设置”任务序列步骤所捕获的值替代。  



##  <a name="BKMK_AutoApplyDrivers"></a>自动应用驱动程序  

 使用此步骤匹配并安装驱动程序，作为 OS 部署的一部分。  

 “自动应用驱动程序”任务序列步骤执行以下操作：  

 1. 扫描硬件并为系统上存在的所有设备查找即插即用 ID。  

 2. 将设备列表以及设备的即插即用 ID 发送到管理点。 管理点从驱动程序目录中为每个硬件设备返回兼容的驱动程序列表。 列表包括所有嵌入的驱动程序，而不管它们位于哪个驱动程序包，还包括具有指定驱动程序类别标记的驱动程序。  

 3. 对于每个硬件设备，任务序列会选择最适合的驱动程序。 此驱动程序适用于已部署的 OS，位于可访问的分发点。  

 4. 任务序列从分发点下载选定的驱动程序，并将驱动程序暂存于目标 OS 上。  

    1. 在使用 OS 映像时，任务序列将驱动程序置于 OS 驱动程序存储区。  

    2. 当使用 OS 升级包作为原始安装源，任务序列会使用驱动程序的位置来配置 Windows 安装程序。  

 5.  在任务序列的“安装 Windows 和 ConfigMgr”步骤过程中，Windows 安装程序会查找此步骤暂存的驱动程序。  


 > [!IMPORTANT]  
 >  独立媒体无法使用“自动应用驱动程序”步骤。 此方案中，任务序列未连接到 Configuration Manager 站点。  

 此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。

 在此步骤中使用以下任务序列变量：  
 - [OSDAutoApplyDriverBestMatch](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverBestMatch)  
 - [OSDAutoApplyDriverCategoryList](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverCategoryList)  
 - [SMSTSDriverRequestConnectTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestConnectTimeOut)  
 - [SMSTSDriverRequestReceiveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestReceiveTimeOut)  
 - [SMSTSDriverRequestResolveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestResolveTimeOut)  
 - [SMSTSDriverRequestSendTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestSendTimeOut)  


 单击任务序列编辑器中的“添加”，选择“驱动程序”，然后选择“自动应用驱动程序”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>仅安装最匹配的兼容驱动程序
 指定任务序列步骤为检测到的每个硬件设备仅安装最匹配的驱动程序。  

#### <a name="install-all-compatible-drivers"></a>安装所有兼容的驱动程序
 任务序列安装与每个检测到的硬件设备兼容的所有驱动程序。 然后，Windows 安装程序选择最适合的驱动程序。 此选项占用更多网络带宽和磁盘空间。 任务序列下载更多驱动程序，但 Windows 可选择更好的驱动程序。  

#### <a name="consider-drivers-from-all-categories"></a>考虑所有类别的驱动程序
 任务序列搜索所有驱动程序类别，寻找适合的设备驱动程序。  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>将驱动程序匹配限制为仅考虑所选类别的驱动程序
 任务序列在指定驱动程序类别中搜索，寻找适合的设备驱动程序。  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>在 Windows 版本上对未签名的驱动程序执行允许的无人参与安装
 此选项允许 Windows 安装没有数字签名的驱动程序。   

 > [!IMPORTANT]  
 >  此选项不适用于不能配置驱动程序签名策略的操作系统。  



##  <a name="BKMK_CaptureNetworkSettings"></a>捕获网络设置  

 使用此步骤从运行该任务序列的计算机捕获 Microsoft 网络设置。 任务序列将这些设置保存在任务序列变量中。 这些设置替代“应用网络设置”步骤中配置的默认设置。  

 此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

 在此步骤中使用以下任务序列变量：  
 - [OSDMigrateAdapterSettings](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdapterSettings)  
 - [OSDMigrateNetworkMembership](/sccm/osd/understand/task-sequence-variables#OSDMigrateNetworkMembership)  


 单击任务序列编辑器中的“添加”，选择“设置”，然后选择“捕获网络设置”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="migrate-domain-and-workgroup-membership"></a>迁移域和工作组成员身份 
 捕获目标计算机的域和工作组成员身份信息。  

#### <a name="migrate-network-adapter-configuration"></a>迁移网络适配器配置
 捕获目标计算机的网络适配器配置。 它捕获以下信息： 
 - 全局网络设置  
 - 适配器数  
 - 以下网络设置与每个适配器相关联：DNS、WINS、IP 和端口筛选器



##  <a name="BKMK_CaptureOperatingSystemImage"></a>捕获操作系统映像  

 此步骤从引用计算机中捕获一个或多个映像。 任务序列在指定的网络共享中创建 Windows 映像 (.wim) 文件。 随后可以使用“添加操作系统映像包”向导将此映像导入 Configuration Manager 中，以便用于基于映像的 OS 部署。  

 Configuration Manager 将引用计算机上的每个卷（驱动器）捕获为 .wim 文件中的单独映像。 如果引用计算机有多个卷，则生成的 .wim 文件对于每个卷将包含单独的映像。 此步骤仅捕获格式化为 NTFS 或 FAT32 的卷。 其他格式的卷和 USB 卷会被忽略。  

 引用计算机上安装的 OS 必须是 Configuration Manager 支持的 Windows 版本。 使用 SysPrep 工具在引用计算机上准备 OS。 安装的 OS 卷和启动卷必须是相同的卷。  

 指定对选定网络共享具有写入权限的帐户。 有关此捕获 OS 映像帐户的详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#capture-operating-system-image-account)。

 此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。 

 在此步骤中使用以下任务序列变量：  
 - [OSDCaptureAccount](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccount)  
 - [OSDCaptureAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccountPassword)  
 - [OSDCaptureDestination](/sccm/osd/understand/task-sequence-variables#OSDCaptureDestination)  
 - [OSDImageCreator](/sccm/osd/understand/task-sequence-variables#OSDImageCreator)  
 - [OSDImageDescription](/sccm/osd/understand/task-sequence-variables#OSDImageDescription)  
 - [OSDImageVersion](/sccm/osd/understand/task-sequence-variables#OSDImageVersion)  
 - [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-input)  


 单击任务序列编辑器中的“添加”，选择“映像”，然后选择“捕获操作系统映像”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="target"></a>目标  
 Configuration Manager 在存储捕获的 OS 映像时所使用位置的文件系统路径。  

#### <a name="description"></a>说明  
 存储在映像文件中的捕获的 OS 映像的用户定义的描述（可选）。  

#### <a name="version"></a>版本  
 向捕获的 OS 映像分配的用户定义的版本号（可选）。 此值可以是字母和数字的任意组合。 它存储在映像文件中。  

#### <a name="created-by"></a>创建者  
 创建 OS 映像的用户的名称（可选）。 它存储在映像文件中。  

#### <a name="capture-operating-system-image-account"></a>捕获操作系统映像帐户  
 输入对指定的网络共享具有访问权限的 Windows 帐户。 单击“设置”以指定 Windows 帐户的名称。  



##  <a name="BKMK_CaptureUserState"></a>捕获用户状态  

 此步骤使用用户状态迁移工具 (USMT) 从运行该任务序列的计算机捕获用户状态和设置。 此任务序列步骤与“还原用户状态”任务序列步骤一起使用。 此步骤终使用由 Configuration Manager 生成并管理的加密密钥加密 USMT 状态存储。  

 有关部署操作系统时管理用户状态的详细信息，请参阅[管理用户状态](/sccm/osd/get-started/manage-user-state)。  

 如果要将用户状态设置保存到状态迁移点或从其还原设置，可以将此步骤与“请求状态存储”和“发布状态存储”步骤一起使用。  

 此步骤提供对最常用 USMT 选项的受限子网的控制。 使用 OSDMigrateAdditionalCaptureOptions 任务序列变量指定其他命令行选项。  

 此任务序列步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。   

 在此步骤中使用以下任务序列变量：  
 - [_OSDMigrateUsmtPackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtPackageID)  
 - [OSDMigrateAdditionalCaptureOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalCaptureOptions)  
 - [OSDMigrateConfigFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateConfigFiles)  
 - [OSDMigrateContinueOnLockedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnLockedFiles)  
 - [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)  
 - [OSDMigrateMode](/sccm/osd/understand/task-sequence-variables#OSDMigrateMode)  
 - [OSDMigrateSkipEncryptedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateSkipEncryptedFiles)  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 单击任务序列编辑器中的“添加”，选择“用户状态”，然后选择“捕获用户状态”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="user-state-migration-tool-package"></a>用户状态迁移工具包
 指定包含用户状态迁移工具 (USMT) 的包。 任务序列使用此版 USMT 捕获用户状态和设置。 此包不需要程序。 指定包含 32 位或 64 位版本 USMT 的包。 USMT 的体系结构取决于任务序列将从其中捕获状态的 OS 的体系结构。  

#### <a name="capture-all-user-profiles-with-standard-options"></a>使用标准选项捕获所有用户配置文件
 迁移所有用户配置文件信息。 此选项为默认设置。  

 如果选择此选项，但在“还原用户状态”步骤中未选择“还原本地计算机用户配置文件”，任务序列将失败。 Configuration Manager 无法在不向新帐户分配密码的情况下迁移这些帐户。 

 如果使用“新建任务序列”向导的“安装现有映像包”选项，生成的任务序列将默认为“使用标准选项捕获所有用户配置文件”。 此默认任务序列不会选择“还原本地计算机用户配置文件”选项，也不会选择非域用户帐户。  

 选择“还原本地计算机用户配置文件”，并为要迁移的帐户提供密码。 在手动创建的任务序列中，此设置可在“还原用户状态”步骤下找到。 在由新建任务序列向导创建的任务序列中，可在步骤“还原用户文件和设置”向导页面下方找到此设置。  

 如果没有本地用户帐户，此设置不适用。  

#### <a name="customize-how-user-profiles-are-captured"></a>自定义如何捕获用户配置文件
 选择此选项以指定迁移的自定义配置文件。 单击“文件”以选择 USMT 要在此步骤中使用的配置文件。 指定一个自定义 .xml 文件，该文件包含定义要迁移的用户状态文件的规则。  

#### <a name="click-here-to-select-configuration-files"></a>单击此处选择配置文件
 选择此选项以便在想要用于捕获用户配置文件的 USMT 包中选择配置文件。 单击“文件”按钮以启动“配置文件”对话框。 要指定配置文件，请在“文件名”  行中输入文件名称并单击“添加”  按钮。  

#### <a name="enable-verbose-logging"></a>启用详细日志记录
 启用此选项以生成更详细的日志文件信息。 捕获状态时，任务序列默认生成日志 ScanState.log 并存储在任务序列日志文件夹 `%WinDir%\ccm\logs` 中。   

#### <a name="skip-files-using-encrypted-file-system"></a>使用加密文件系统跳过文件
 启用此选项可跳过捕获使用加密文件系统 (EFS) 加密过的文件。 这些文件包括用户配置文件。 根据 OS 和 USMT 版本，还原后可能无法读取加密文件。 有关详细信息，请参阅 USMT 文档。  

#### <a name="copy-by-using-file-system-access"></a>使用文件系统访问进行复制
 启用此选项以指定任何以下设置：  

 - **如果无法捕获某些文件则继续**：启用此设置以在无法捕获某些文件时继续迁移过程。 如果禁用此选项，且无法捕获某个文件，此步骤将失败。 默认情况下会启用此选项。  

 - **通过使用链接而不是通过复制文件以本地方式进行捕获**：启用此设置以使用 NTFS 硬链接来捕获文件。  

     有关使用硬链接迁移数据的详细信息，请参阅 [硬链接迁移存储](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store)。  

 - **在脱机模式下进行捕获（仅 Windows PE）**：启用此设置可在 Windows PE 而不是整个 OS 中捕获用户状态。  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>使用卷影复制服务 (VSS) 进行捕获
 通过此选项，你可捕获文件，即使文件被锁定由其他应用程序编辑也无妨。  



##  <a name="BKMK_CaptureWindowsSettings"></a>捕获 Windows 设置  

 使用此步骤从运行该任务序列的计算机捕获 Windows 设置。 任务序列将这些设置保存在任务序列变量中。 这些捕获的设置将替代“应用 Windows 设置”步骤中配置的默认设置。  

 此任务序列步骤在 Windows PE 或完整 OS 中运行。  

 在此步骤中使用以下任务序列变量：  
 - [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-output)  
 - [OSDMigrateComputerName](/sccm/osd/understand/task-sequence-variables#OSDMigrateComputerName)  
 - [OSDMigrateRegistrationInfo](/sccm/osd/understand/task-sequence-variables#OSDMigrateRegistrationInfo)  
 - [OSDMigrateTimeZone](/sccm/osd/understand/task-sequence-variables#OSDMigrateTimeZone)  
 - [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-output)  
 - [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-output)  


 单击任务序列编辑器中的“添加”，选择“设置”，然后选择“捕获 Windows 设置”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="migrate-computer-name"></a>迁移计算机名称
 捕获计算机的 NetBIOS 计算机名称。  

#### <a name="migrate-registered-user-and-organization-names"></a>迁移注册用户和组织名称
 捕获计算机中已注册的用户和组织名称。  

#### <a name="migrate-time-zone"></a>迁移时区
 捕获计算机上的时区设置。  



##  <a name="BKMK_CheckReadiness"></a>检查准备情况  

 使用此步骤验证目标计算机是否满足指定的部署先决条件。  

 单击任务序列编辑器中的“添加”，选择“常规”，然后选择“检查就绪情况”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="ensure-minimum-memory-mb"></a>确保最小内存 (MB)
 验证内存量（以兆字节 (MB) 计算），是满足还是超过指定的量。 步骤默认启用此设置。  

#### <a name="ensure-minimum-processor-speed-mhz"></a>确保最低处理器速度 (MHz)  
 验证处理器的速度（以兆赫兹 (MHz) 计算），是满足还是超过指定的量。 步骤默认启用此设置。  

#### <a name="ensure-minimum-free-disk-space-mb"></a>确保最小可用磁盘空间 (MB)
 验证可用磁盘空间（以兆字节 (MB) 计算），是满足还是超过指定的量。  

#### <a name="ensure-current-os-to-be-refreshed-is"></a>确保要刷新的当前 OS
 验证目标计算机上安装的 OS 是否满足指定的要求。 此步骤将该设置默认设置为“客户端”。  


### <a name="options"></a>选项

 > [!NOTE]  
 > 如果启用此步骤的“选项”选项卡上的“出错时继续”，则仅记录就绪情况检查结果。 如果检查失败，任务序列不会停止。  



##  <a name="BKMK_ConnectToNetworkFolder"></a>连接到网络文件夹  

 使用此步骤创建与共享网络文件夹的连接。  

 此任务序列步骤在完整 OS 或 Windows PE 中运行。  

 在此步骤中使用以下任务序列变量：  
 - [SMSConnectNetworkFolderAccount](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderAccount)  
 - [SMSConnectNetworkFolderDriveLetter](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderDriveLetter)  
 - [SMSConnectNetworkFolderPassword](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPassword)  
 - [SMSConnectNetworkFolderPath](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPath)  


 单击任务序列编辑器中的“添加”，选择“常规”，然后选择“连接到网络文件夹”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="path"></a>路径  
 单击“浏览”，指定网络文件夹路径。 使用格式 `\\server\share`。

#### <a name="drive"></a>驱动器  
 选择分配给此连接的本地驱动器号。 

#### <a name="account"></a>帐户 
 单击“设置”以指定有权连接此网络文件夹的用户帐户。 有关任务序列网络文件夹连接帐户的详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-network-folder-connection-account)。



##  <a name="BKMK_DisableBitLocker"></a>禁用 BitLocker  

 使用此步骤，在当前 OS 驱动器或指定驱动器上禁用 BitLocker 加密。 此操作使得密钥保护程序在硬盘驱动器上以明文形式显示。 但是不会解密该驱动器的内容。 此操作几乎顷刻就能完成。  

 > [!NOTE]  
 >  BitLocker 驱动器加密提供磁盘卷内容的低级加密。  

 如果加密了多个驱动器，则需在任何数据驱动器上禁用 BitLocker，才能在 OS 驱动器上禁用 BitLocker。  

 此步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

 单击任务序列编辑器中的“添加”，选择“磁盘”，然后选择“禁用 BitLocker”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="current-operating-system-drive"></a>当前操作系统驱动器
 在当前 OS 驱动器上禁用 BitLocker。  

#### <a name="specific-drive"></a>特定驱动器  
 在特定驱动器上禁用 BitLocker。 使用下拉列表指定禁用 BitLocker 的驱动器。  



##  <a name="BKMK_DownloadPackageContent"></a>下载包内容  

 使用此步骤下载以下任何包类型：  

 - OS 映像  
 - OS 升级包  
 - 驱动程序包  
 - 包  
 - 启动映像  


 此步骤适用于任务序列，从而在以下方案中升级 OS：  

 - 若要使用可同时用于 x86 平台和 x64 平台的单一升级任务序列。 包括“准备升级”组中的两个“下载包内容”步骤。 在“选项”选项卡上指定条件，以检测客户端体系结构并仅下载适当的 OS 升级包。 配置每个“下载包内容”步骤，使其使用相同的变量。 将该变量用于“升级操作系统”步骤中的媒体路径。  

 - 若要动态下载适用的驱动程序包，请使用两个“下载包内容”步骤以及检测每个驱动程序包的相应硬件类型的条件。 配置每个“下载包内容”步骤，使其使用相同的变量。 将该变量用于“升级操作系统”步骤的驱动程序部分中的“预留内容”变量。  


 > [!NOTE]    
 > 在部署包含此步骤的任务序列时，请勿在部署软件向导的“分发点”页上为“部署选项”选择“在启动任务序列之前在本地下载所有内容”或“直接从分发点访问内容”。  

 此步骤在完整 OS 或 Windows PE 中运行。 Windows PE 中不提供将包保存在 Configuration Manager 客户端缓存中的选项。

 单击任务序列编辑器中的“添加”，选择“软件”，然后选择“下载包内容”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="select-package"></a>选择包  
 单击图标以选择要下载的包。 选择一个包后，再次单击图标以选择另一个包。  

#### <a name="place-into-the-following-location"></a>置于下列位置
 选择将包保存在下列位置之一：  

 - **任务序列工作目录**：此位置也称为任务序列缓存。  

 - **Configuration Manager 客户端缓存**：使用此选项可在客户端缓存中存储内容。 默认情况下，此路径为 `%WinDir%\ccmcache`。  

 - **自定义路径**：任务序列引擎首先会将包下载到任务序列工作目录。 然后将内容移动到指定的路径。 任务序列引擎会将包 ID 附加到路径中。  

#### <a name="save-path-as-a-variable"></a>将路径另存为一个变量
 将包路径保存到自定义任务序列变量。 然后在另一个任务序列步骤中使用此变量。 

 Configuration Manager 向变量名称中添加数字后缀。 例如，指定变量 `%MyContent%` 作为自定义变量。 它是任务序列存储此步骤中所有引用内容的位置的根。 此内容可能包含多个包。 引用该变量时，添加数字后缀。 有关第一个包，请参阅 `%MyContent01%`。 在子序列步骤（如“升级操作系统”）中引用变量时，将使用 `%MyContent02%` 或 `%MyContent03%`，其中的数字对应“下载包内容”步骤罗列包的顺序。  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>如果包下载失败，继续下载列表中的其他包
 如果任务序列未能下载某个包，会开始下载列表中的下一个包。  



##  <a name="BKMK_EnableBitLocker"></a>启用 BitLocker  

 使用此步骤在硬盘驱动器的至少两个分区上启用 BitLocker 加密。 第一个活动分区包含 Windows 启动代码。 另一个分区包含 OS。 启动分区必须保持为未加密状态。  

 在 Windows PE 中，使用“预设置 BitLocker”步骤可在驱动器上启用 BitLocker。 有关详细信息，请参阅[预设置 BitLocker](#BKMK_PreProvisionBitLocker)。  

 > [!NOTE]  
 >  BitLocker 驱动器加密提供磁盘卷内容的低级加密。  

 此步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。   

 在此步骤中使用以下任务序列变量：  
 - [OSDBitLockerRecoveryPassword](/sccm/osd/understand/task-sequence-variables#OSDBitLockerRecoveryPassword)  
 - [OSDBitLockerStartupKey](/sccm/osd/understand/task-sequence-variables#OSDBitLockerStartupKey)  


 当指定“仅 TPM”、“USB 上的 TPM 和启动密钥”或“TPM 和 PIN”时，受信任的平台模块 (TPM) 必须处于以下状态，然后才能运行“启用 BitLocker”步骤：  
 - Enabled  
 - 已激活  
 - 允许的所有权  


 此步骤将完成剩余的 TPM 初始化。 余下的步骤无需实际操作或重新启动。 “启用 BitLocker”步骤（如有必要）以透明方式完成下列剩余的 TPM 初始化步骤：  
 - 创建认可密钥对  
 - 创建所有者授权值和 Active Directory 的证书，后者必须已扩展为支持此值  
 - 取得所有权  
 - 创建存储根密钥，或在已存在但不兼容时重置  

   
 如果希望任务序列等待“启用 BitLocker”完成驱动器加密过程，则选择“等待”选项。 如果不选择“等待”选项，则驱动器加密过程在后台进行。 任务序列即时执行下一步骤。  

 BitLocker 可用于加密单个计算机系统上的多个驱动器（OS 和数据驱动器）。 若要加密数据驱动器，首先加密 OS 驱动器并完成加密过程。 需执行此操作的原因是 OS 驱动器存储数据驱动器的密钥保护程序。 如果加密相同任务序列中的 OS 和数据驱动器，请在“启用 BitLocker”步骤中为 OS 驱动器选择“等待”选项。  

 如果硬盘已加密，但 BitLocker 处于禁用状态，则“启用 BitLocker”步骤会重新启用密钥保护程序，并快速完成。 在这种情况下不需要重新加密硬盘。  

 单击任务序列编辑器中的“添加”，选择“磁盘”，然后选择“启用 BitLocker”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="choose-the-drive-to-encrypt"></a>选择要加密的驱动器
 指定要加密的驱动器。 若要加密当前 OS 驱动器，请选择“当前操作系统驱动器”。 然后配置下列密钥管理选项：  

 - **仅 TPM**：选择此选项，以仅使用受信任的平台模块 (TPM)。  

 - **仅 USB 上的启动密钥**：选择此选项以使用存储在 USB 闪存驱动器上的启动密钥。 选择此选项时，BitLocker 将锁定正常启动过程，直至含有 BitLocker 启动密钥的 USB 设备连接到计算机。  

 - **USB 上的 TPM 和启动密钥**：选择此选项以使用存储在 USB 闪存驱动器上的 TPM 和启动密钥。 选择此选项时，BitLocker 将锁定正常启动过程，直至含有 BitLocker 启动密钥的 USB 设备连接到计算机。  

 - **TPM 和 PIN**：选择此选项以使用 TPM 和个人标识号 (PIN)。 当选择此选项时，BitLocker 将锁定正常启动过程，直至用户提供 PIN。  


 要加密特定非 OS 数据驱动器，请选择“特定驱动器”。 然后从列表中选择驱动器。  

#### <a name="use-full-disk-encryption"></a>使用全磁盘加密
 <!--SCCMDocs-pr issue 2671--> 默认情况下，此步骤仅加密驱动器上的已用空间。 建议使用此默认行为，因为它更加快速高效。 从版本 1806 开始，如果贵组织需要在安装期间加密整个驱动器，请启用此选项。 Windows 安装程序会等待整个驱动器加密，所需时间较长（尤其是在大型驱动器上）。 

#### <a name="choose-where-to-create-the-recovery-key"></a>选择要创建恢复密钥的位置
 要在 Active Directory 中指定 BitLocker 创建和托管恢复密码的位置，请选择“在 Active Directory 中”。 此选项要求为 BitLocker 密钥托管扩展 Active Directory。 然后，BitLocker 可以在 Active Directory 中保存关联的恢复信息。 选择“请勿创建恢复密钥”，可以不创建密码。 创建密码为建议选项。  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>等待 BitLocker 完成所有驱动器上的驱动器加密过程之后，继续执行任务序列
 选择此选项以允许在运行任务序列中的下一步骤之前完成 BitLocker 驱动器加密。 如果选择此选项，则在用户能够登录到计算机之前，BitLocker 将对整个磁盘卷加密。  

 加密大型硬盘时，加密过程可能需要数小时才能完成。 不选择此选项将允许立即处理任务序列。  



##  <a name="BKMK_FormatandPartitionDisk"></a>格式化磁盘并分区  

 使用此步骤对目标计算机上的特定磁盘进行格式化和分区。  

 > [!IMPORTANT]  
 >  你为此步骤指定的所有设置均应用于单个特定磁盘。 若要对目标计算机上的另一个磁盘进行格式化和分区，则向该任务序列再添加一个“格式化磁盘并分区”步骤。  

 此步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。  

 在此步骤中使用以下任务序列变量：  
 - [OSDDiskIndex](/sccm/osd/understand/task-sequence-variables#OSDDiskIndex)  
 - [OSDGPTBootDisk](/sccm/osd/understand/task-sequence-variables#OSDGPTBootDisk)  
 - [OSDPartitions](/sccm/osd/understand/task-sequence-variables#OSDPartitions)  
 - [OSDPartitionStyle](/sccm/osd/understand/task-sequence-variables#OSDPartitionStyle)  


 单击任务序列编辑器中的“添加”，选择“磁盘”，然后选择“格式化磁盘并分区”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="disk-number"></a>磁盘编号
 要进行格式化的磁盘的物理磁盘编号。 该编号取决于 Windows 磁盘枚举排序。  

#### <a name="disk-type"></a>磁盘类型
 要格式化的磁盘类型。 可以从下拉列表中选择两个选项： 
 - **标准 (MBR)**：主启动记录  
 - **GPT**：GUID 分区表  


 > [!NOTE]  
 >  如果将磁盘类型从“标准 (MBR)”更改为“GPT”，并且分区布局包含扩展分区，则任务序列将从布局中删除所有扩展分区和逻辑分区。 任务序列编辑器会在更改磁盘类型前提示确认此操作。  
   
#### <a name="volume"></a>Volume
 指定有关任务序列要创建的分区或卷的信息，包括以下属性：  
 - 名称  
 - 剩余磁盘空间  


 要创建新的分区，请单击“新建”  以启动“分区属性”  对话框。 指定分区类型和大小，以及是否为启动分区。 要修改现有分区，请单击要修改的分区，然后单击“属性”按钮。 有关如何配置硬盘分区的详细信息，请参阅下列其中一篇文章：  

 - [基于 UEFI/GPT 的硬盘分区](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
 - [基于 BIOS/MBR 的硬盘分区](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  


 要删除分区，请选择分区，然后单击“删除”。  



##  <a name="BKMK_InstallApplication"></a>安装应用程序  

 此步骤安装指定的应用程序或一组由任务序列变量动态列表定义的应用程序。 当任务序列运行此步骤时，应用程序安装会立即开始而不等待策略轮询间隔。  

 应用程序必须符合以下条件：  

 - 应用程序的部署类型必须是 Windows Installer 或脚本安装程序。 不支持 Windows 应用程序包（.appx 文件）部署类型。  

 - 它必须在本地系统帐户而非用户帐户下运行。  

 - 它不得与桌面进行交互。 该程序必须无提示运行或在无人参与模式下运行。  

 - 它本身不能启动重新启动。 该应用程序必须使用标准的重新启动代码 (3010) 请求重新启动。 此行为可确保此步骤正确处理重新启动。 如果应用程序返回 3010 退出代码，则任务序列引擎将重启计算机。 重新启动后，任务序列自动继续。  


 当此步骤运行时，应用程序将检查部署类型的要求规则和检测方法的适用性。 根据此检查的结果，应用程序将安装适用的部署类型。 如果部署类型包含依赖关系，则对该依赖部署类型进行评估并将其作为此步骤的一部分进行安装。 独立媒体不支持应用程序依赖关系。  

 > [!NOTE]  
 >  要安装取代另一应用程序的应用程序，被取代的应用程序的内容文件必须可用。 否则任务序列步骤将失败。 例如，在客户端或捕获的映像中安装 Microsoft Visio 2010。 当运行“安装应用程序”步骤安装 Microsoft Visio 2013 时，Microsoft Visio 2010（被取代的应用程序）的内容文件必须在分发点上可用。 如果某个客户端或捕获映像未安装 Microsoft Visio，任务序列会安装 Microsoft Visio 2013，而不会检查 Microsoft Visio 2010 内容文件。  

 > [!NOTE]  
 > 如果客户端无法利用定位服务检索管理点列表，则使用 SMSTSMPListRequestTimeoutEnabled 和 SMSTSMPListRequestTimeout 任务序列变量。 这些变量指定任务序列重试安装应用程序之前要等待的毫秒数。 有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables)。

 此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

 在此步骤中使用以下任务序列变量：  
 - [_TSAppInstallStatus](/sccm/osd/understand/task-sequence-variables#TSAppInstallStatus)  
 - [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)  
 - [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)  
 - [TSErrorOnWarning](/sccm/osd/understand/task-sequence-variables#TSErrorOnWarning)  


 单击任务序列编辑器中的“添加”，选择“软件”，然后选择“安装应用程序”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，配置此部分描述的设置。  

#### <a name="install-the-following-applications"></a>安装以下应用程序
 任务序列按指定顺序安装这些应用程序。  

 Configuration Manager 将筛选出任何禁用的或具有以下设置的应用程序：  

 - 仅当用户登录时  
 - 使用用户权限运行  


 这些应用程序不会出现在“选择要安装的应用程序”对话框中。

#### <a name="install-applications-according-to-dynamic-variable-list"></a>根据动态变量列表安装应用程序
 任务序列使用此基本变量名安装应用程序。 基本变量名称适用于为集合或计算机定义的任务序列变量。 这些变量指定任务序列为该集合或计算机安装的应用程序。 每个变量名称都由其通用的基名称和一个数字后缀（从 01 开始）组成。 每个变量的值都必须包含应用程序的名称，且没有其他任何内容。  

 对于要使用动态变量列表安装的应用程序，请在应用程序“属性”的“常规”选项卡中启用以下设置：**允许通过“安装应用程序”任务序列操作安装此应用程序，而不是手动部署**。  

 > [!NOTE]  
 >  对于独立媒体部署，无法使用动态变量列表安装应用程序。  

 例如，要使用名为“AA01”的任务序列变量安装单个应用程序，需指定以下变量：  

 |变量名称|变量值：|  
 |-------------------|--------------------|  
 |AA01|Microsoft Office|  

 要安装两个应用程序，需指定以下变量：  

 |变量名称|变量值：|  
 |-------------------|--------------------|  
 |AA01|Microsoft Lync|  
 |AA02|Microsoft Office|  

 以下条件会影响任务序列安装的应用程序：  

 - 如果变量的值中包含应用程序名称之外的其他任何信息。 任务序列不会安装应用程序，并继续执行操作。  

 - 如果任务序列未找到带指定基本名称和“01”后缀的变量，任务序列不会安装任何应用程序。  


 > [!Important]  
 > 这些值区分大小写。 例如，“install”不同于“Install”。 如果需要更改值，任务序列编辑器无法检测大小写变化。 同时进行另一项编辑（例如，修改步骤说明）。<!--509714-->   

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>如果应用程序失败，继续安装列表中的其他应用程序
 此设置指定在单个应用程序安装失败时该步骤继续。 如果指定此设置，则任务序列将继续，不考虑任何安装错误。 如果未指定此设置且安装失败，步骤将立即结束。  


### <a name="options"></a>选项

 > [!NOTE]  
 > 在此步骤的“选项”选项卡上选择“出错时继续”时，该任务序列将在应用程序安装失败时继续。 如果不启用此选项，任务序列失败且不安装剩余的应用程序。  

 除默认选项外，还可配置此任务序列步骤的“选项”选项卡上的以下其他设置：  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>如果计算机意外重启，请重试此步骤
 如果安装其中一个应用程序时意外重启计算机，请重试此步骤。 两次重试此步骤后将默认启用此设置。 可以指定 1 到 5 次重试。  



##  <a name="BKMK_InstallPackage"></a>安装包

 作为任务序列的一部分，使用此步骤安装软件包。 此步骤运行时，安装会立即开始而不等待策略轮询间隔。  

 包必须符合以下条件：  

 - 它必须在本地系统帐户而非用户帐户下运行。  

 - 它不应与桌面进行交互。 该程序必须无提示运行或在无人参与模式下运行。  

 - 它本身不能启动重新启动。 该软件必须使用标准的重新启动代码 (3010) 请求重新启动。 此行为可确保任务序列正确处理重新启动。 如果该软件不返回 3010 退出代码，则任务序列引擎将重启计算机。 重新启动后，任务序列自动继续。  


 部署 OS 时不支持使用“首先运行其他程序”选项安装从属程序的程序。 如果启用了选项“首先运行其他程序”，且其从属程序已在目标计算机上运行，则将运行从属程序且任务序列将继续。 但是，如果从属程序尚未在目标计算机上运行，则任务序列步骤将失败。  

 > [!NOTE]  
 >  管理中心站点并没有任务序列期间启用软件分发代理所需的必要客户端配置策略。 当你在管理中心站点为任务序列创建独立媒体，而任务序列包含“安装包”  步骤时，CreateTsMedia.log 文件可能会出现以下错误：  
 >   
 >  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
 >   
 >  对于包括“安装包”步骤的独立媒体，请在已启用软件分发代理的主站点创建独立媒体。 或者，在“安装 Windows 和 ConfigMgr”步骤后及第一个“安装包”步骤前添加一个“运行命令行”步骤。 “运行命令行”步骤运行 WMIC 命令，以便在第一个“安装包”步骤之前启用软件分发代理。 在“运行命令行”步骤中使用以下命令：  
 >   
 >  `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
 >   
 >  有关创建独立媒体的详细信息，请参阅[创建独立媒体](/sccm/osd/deploy-use/create-stand-alone-media)。  


 此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

 单击任务序列编辑器中的“添加”，选择“软件”，然后选择“安装包”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="install-a-single-software-package"></a>安装单个软件包
 此设置会指定一个 Configuration Manager 软件包。 该步骤要等到安装完成后才开始。  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>根据动态变量列表安装软件包
 任务序列将使用此基本变量名称安装包。 基本变量名称适用于为集合或计算机定义的任务序列变量。 这些变量指定任务序列将为该集合或计算机安装的包。 每个变量名称都由其通用的基名称和一个数字后缀（从 001 开始）组成。 每个变量的值都必须包含包 ID 和软件名称，以冒号分隔。  

 对于要使用动态变量列表安装的软件，请在包“属性”的“高级”选项卡中启用以下设置：**允许在不部署的情况下从“安装包”任务序列安装此程序**。  

 > [!NOTE]  
 >  对于独立媒体部署，无法使用动态变量列表安装软件包。  

 例如，要使用名为 AA001 的任务序列变量安装单个软件包，需指定以下变量：  

 |变量名称|变量值：|  
 |-------------------|--------------------|  
 |AA001|CEN00054:Install|  

 要安装两三个软件包，需指定以下变量：  

 |变量名称|变量值：|  
 |-------------------|--------------------|  
 |AA001|CEN00054:Install|  
 |AA002|CEN00107:Install Silent|  
 |AA003|CEN00031:Install|  

 以下条件可影响任务序列所安装的包：  

 - 如果变量的值未以正确的格式创建，或者未指定有效的包 ID 和名称，则软件安装将失败。  

 - 如果包 ID 含有小写字符，则软件安装将失败。  

 - 如果任务序列未找到带指定基本名称和“001”后缀的变量，任务序列不会安装任何包。 任务序列将继续。  


 > [!Important]  
 > 这些值区分大小写。 例如，“install”不同于“Install”。 如果需要更改值，任务序列编辑器无法检测大小写变化。 同时进行另一项编辑（例如，修改步骤说明）。<!--509714-->   

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>如果软件包安装失败，则继续安装列表中的其他包
 此设置指定在单个软件包安装失败时该步骤继续。 如果指定此设置，则任务序列将继续，不考虑任何安装错误。 如果未指定此设置且安装失败，步骤将立即结束。  



##  <a name="BKMK_InstallSoftwareUpdates"></a>安装软件更新  

 使用此步骤在目标计算机上安装软件更新。 在运行此任务序列步骤时，才会评估目标计算机是否有适用的软件更新。 那时，会与其他 Configuration Manager 客户端一样评估目标计算机是否有合适的软件更新。 对于此安装软件更新的步骤，首先向目标计算机所属的集合部署更新。  

 > [!IMPORTANT]  
 > 对于最佳性能，安装最新版 Windows 更新代理。  

 此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。 

 在此步骤中使用以下任务序列变量：  
 - [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget)  
 - [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)  
 - [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)  
 - [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout)  
 - [SMSTSWaitForSecondReboot](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot)  


 > [!NOTE]  
 > 如果客户端无法利用定位服务检索管理点列表，则使用 SMSTSMPListRequestTimeoutEnabled 和 SMSTSMPListRequestTimeout 变量。 这些变量指定任务序列重试安装应用程序或软件更新之前要等待的毫秒数。 有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables)。  


 单击任务序列编辑器中的“添加”，选择“软件”，然后选择“安装软件更新”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>安装要求 - 仅必需的软件更新
 选择此选项，在管理员定义的安装截止日期前安装所有必需的软件更新。  

#### <a name="available-for-installation---all-software-updates"></a>可供安装 - 所有软件更新
 选择此选项以安装所有可用的软件更新。 先向计算机所属的集合部署这些更新。 任务序列将在目标计算机上安装所有可用的软件更新。  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>根据缓存的扫描结果评估软件更新
 默认情况下，此步骤使用从 Windows 更新代理中缓存的扫描结果。 禁用此选项以指示 Windows 更新代理从软件更新点下载最新目录。 如果使用任务序列[捕获和生成 OS 映像](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system)，则启用此选项。 此方案中可能包含大量软件更新。 

 其中许多更新具有依赖项。 例如，在更新 XYZ 显示为适用之前安装更新。 当禁用此设置并将任务序列部署到大量客户端时，它们将同时连接到软件更新点。 此行为会在更新目录处理和下载过程中导致性能问题。 

 在大多数情况下，使用默认设置来使用缓存的扫描结果。 

 SMSTSSoftwareUpdateScanTimeout 变量控制着此步骤期间的软件更新扫描超时。 默认值为 30 分钟。 有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout)。


### <a name="options"></a>选项   

 除默认选项外，还可配置此任务序列步骤的“选项”选项卡上的以下其他设置：  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>如果计算机意外重启，请重试此步骤
 如果其中一个更新意外重启计算机，请重试此步骤。 两次重试此步骤后将默认启用此设置。 可以指定 1 到 5 次重试。  

 > [!NOTE]  
 > 配置 SMSTSWaitForSecondReboot 变量，以指定此方案中任务序列在计算机重启后暂停的秒数。 有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot)。  



##  <a name="BKMK_JoinDomainorWorkgroup"></a>加入域或工作组  

 使用此步骤将目标计算机添加到工作组或域。  

 此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。   

 在此步骤中使用以下任务序列变量：  
 - [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)  
 - [OSDJoinDomainName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainName)  
 - [OSDJoinDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainOUName)  
 - [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)  
 - [OSDJoinSkipReboot](/sccm/osd/understand/task-sequence-variables#OSDJoinSkipReboot)  
 - [OSDJoinType](/sccm/osd/understand/task-sequence-variables#OSDJoinType)  
 - [OSDJoinWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDJoinWorkgroupName)  


 单击任务序列编辑器中的“添加”，选择“常规”，然后选择“加入域或工作组”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="join-a-workgroup"></a>加入工作组
 选择此选项，使目标计算机加入指定的工作组。 如果计算机当前是某个域的成员，选择此选项将导致计算机重新启动。  

#### <a name="join-a-domain"></a>加入域
 选择此选项以将目标计算机加入指定的域。  

 （可选）在指定的域中输入或浏览查找计算机要加入的组织单位 (OU)。 如果计算机当前是某个其他域或某个工作组的成员，此选项将导致计算机重新启动。 如果计算机已是其他 OU 的成员，由于 Active Directory 域服务不允许通过此方法更改 OU，Windows 安装程序会忽略此设置。  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>输入有权限加入域的帐户
 单击“设置”以输入有权限加入域的帐户的用户名和密码。 使用后述格式输入帐户：`Domain\account`。 有关任务序列域加入帐户的详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account)。  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a>准备 ConfigMgr 客户端以便捕获  

 使用此步骤删除或配置引用计算机上的 Configuration Manager 客户端。 此操作让计算机做好准备以进行捕获，作为映像创建过程的一部分。

 此步骤现在将完全删除 Configuration Manager 客户端，而不是仅删除密钥信息。 任务序列每次部署捕获的 OS 映像时，都将安装新的 Configuration Manager 客户端。  

 > [!Note]  
 >  任务序列引擎仅在执行“生成并捕获引用操作系统映像”任务序列期间才会删除客户端。 其他捕获方法执行期间，如捕获媒体或自定义任务序列等，任务序列不会删除客户端。  

 此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

 单击任务序列编辑器中的“添加”，选择“映像”，然后选择“准备 ConfigMgr 客户端以便捕获”以添加此步骤。 


### <a name="properties"></a>属性  

 此步骤不需要“属性”选项卡上的任何设置。



##  <a name="BKMK_PrepareWindowsforCapture"></a>准备 Windows 以便捕获  

 使用此步骤来指定捕获引用计算机上的 OS 映像时要使用的 Sysprep 选项。 此步骤运行 Sysprep，然后将计算机重新启动到为该任务序列指定的 Windows PE 启动映像。 如果引用计算机已加入域，此操作将失败。  

 此步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。   

 在此步骤中使用以下任务序列变量：  
 - [OSDKeepActivation](/sccm/osd/understand/task-sequence-variables#OSDKeepActivation)  
 - [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-output)  


 单击任务序列编辑器中的“添加”，选择“映像”，然后选择“准备 Windows 以便捕获”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="automatically-build-mass-storage-driver-list"></a>自动生成大容量存储驱动程序列表
 选择此选项以便 Sysprep 从引用计算机自动生成大容量存储驱动程序列表。 此选项在引用计算机上的 sysprep.inf 文件中启用“生成大容量存储驱动程序”选项。 有关此设置的详细信息，请参阅 Sysprep 文档。  

#### <a name="do-not-reset-activation-flag"></a>不重置激活标志
 选择此选项以阻止 Sysprep 重置产品激活标志。  

#### <a name="shutdown-the-computer-after-running-this-action"></a>运行此操作后关闭计算机
 <!--SCCMDocs-pr issue 2695--> 从版本 1806 开始，此选项指示 Sysprep 关闭计算机，代替其默认重启行为。 



##  <a name="BKMK_PreProvisionBitLocker"></a>预设置 BitLocker  

 在 Windows PE 中，使用此步骤将在驱动器上启用 BitLocker。 默认情况下，由于仅加密使用的磁盘空间，因此加密时间要短得多。 安装 OS 后，使用 [启用 BitLocker](#BKMK_EnableBitLocker) 步骤应用密钥管理选项。 

 此步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。  

 > [!IMPORTANT]  
 >  预配 BitLocker 时的操作系统至少需为 Windows 7。 计算机还必须包含受支持且已启用的信任平台模块 (TPM)。  

 单击任务序列编辑器中的“添加”，选择“磁盘”，然后选择“预配 BitLocker”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>将 BitLocker 应用于指定的驱动器
 指定要为其启用 BitLocker 的驱动器。 BitLocker 仅加密驱动器上使用的空间。  

#### <a name="use-full-disk-encryption"></a>使用全磁盘加密
 <!--SCCMDocs-pr issue 2671--> 默认情况下，此步骤仅加密驱动器上的已用空间。 建议使用此默认行为，因为它更加快速高效。 从版本 1806 开始，如果贵组织需要在安装期间加密整个驱动器，请启用此选项。 Windows 安装程序会等待整个驱动器加密，所需时间较长（尤其是在大型驱动器上）。 

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>对于没有 TPM 或 未启用 TPM 的计算机跳过此步骤
 选择此选项可跳过针对某类计算机的驱动器加密操作，这类计算机不包含受支持且已启用的 TPM。 例如，可在将 OS 部署到虚拟机时使用此选项。  



##  <a name="BKMK_ReleaseStateStore"></a>发布状态存储  

 使用此步骤通知状态迁移点，捕获或还原操作已完成。 将此步骤与“请求状态存储”、“捕获用户状态”和“还原用户状态”等步骤结合使用。 可通过使用状态迁移点和用户状态迁移工具 (USMT)，使用这些步骤迁移用户状态数据。  

 有关部署操作系统时管理用户状态的详细信息，请参阅[管理用户状态](/sccm/osd/get-started/manage-user-state)。  

 如果使用“请求状态存储”步骤请求访问状态迁移点以捕获用户状态，此步骤将通知状态迁移点捕获过程已完成。 然后，状态迁移点将用户状态数据标记为可还原。 状态迁移点设置用户状态数据的访问控制权限，以便仅还原的计算机具有只读访问权限。  

 如果使用“请求状态存储”步骤请求访问状态迁移点以还原用户状态，此步骤将通知状态迁移点还原过程已完成。 然后，状态迁移点将激活其配置的数据保留配置。  

 > [!IMPORTANT]  
 > 为“请求状态存储”和“发布状态存储”步骤之间的所有步骤设置“出错时继续”。 每个“请求状态存储”步骤必须有一个匹配的“发布状态存储”步骤。  

 此步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。   

 在此步骤中使用以下任务序列变量：  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 单击任务序列编辑器中的“添加”，选择“用户状态”，然后选择“发布状态存储”以添加此步骤。 


### <a name="properties"></a>属性  

 此步骤不需要“属性”选项卡上的任何设置。



##  <a name="BKMK_RequestStateStore"></a>请求状态存储  

 使用此步骤可以在捕获或还原状态时请求对状态迁移点的访问权限。  

 有关部署操作系统时管理用户状态的详细信息，请参阅[管理用户状态](/sccm/osd/get-started/manage-user-state)。  

 将此步骤与“发布状态存储”、“捕获用户状态”和“还原用户状态”等步骤结合使用。 可通过使用状态迁移点和用户状态迁移工具 (USMT) 使用这些步骤迁移计算机状态。  

 > [!NOTE]  
 >  新建状态迁移点时，用户状态存储最多可能需要一小时才能使用。 要促进可用性，请调整状态迁移点上的任何属性设置以触发站点控制文件更新。  

 此步骤在完整 OS 和脱机 USMT Windows PE 中运行。   

 在此步骤中使用以下任务序列变量：  
 - [OSDStateFallbackToNAA](/sccm/osd/understand/task-sequence-variables#OSDStateFallbackToNAA)  
 - [OSDStateSMPRetryCount](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryCount)  
 - [OSDStateSMPRetryTime](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryTime)  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 单击任务序列编辑器中的“添加”，选择“用户状态”，然后选择“请求用户存储”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="capture-state-from-the-computer"></a>从计算机捕获状态
 查找满足状态迁移点设置中所配置的最低要求的状态迁移点。 例如，“最大客户端数”和“最小可用磁盘空间量”。 此选项不保证在状态迁移时有足够空间可用。 此选项将请求访问状态迁移点，以便从计算机捕获用户状态和设置。  

 如果 Configuration Manager 站点具有多个活动状态迁移点，此步骤将查找具有可用磁盘空间的状态迁移点。 任务序列将查询管理点，以便获得状态迁移点列表，然后计算每个点，直到找到满足最低要求的迁移点。  

#### <a name="restore-state-from-another-computer"></a>从另一台计算机还原状态
 请求访问状态迁移点，以便将先前捕获的用户状态和设置还原到目标计算机。  

 如果具有多个状态迁移点，此步骤将查找具有目标计算机状态的状态迁移点。  

#### <a name="number-of-retries"></a>重试次数
 此步骤在失败之前尝试查找合适状态迁移点的次数。  

#### <a name="retry-delay-in-seconds"></a>重试延迟（秒）
 任务序列步骤在重试尝试之间等待的秒数。  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>如果计算机帐户无法连接到状态存储，请使用网络访问帐户
 如果任务序列无法使用计算机帐户访问状态迁移点，则使用网络访问帐户凭据进行连接。 此选项不太安全，因为其他计算机可以使用网络访问帐户来访问已存储的状态。 如果目标计算机未加入域，则必选此选项。  



##  <a name="BKMK_RestartComputer"></a>重新启动计算机  

 使用此步骤重启运行任务序列的计算机。 重新启动之后，计算机将自动地继续运行任务序列中的下一个步骤。  

 可以在完整 OS 或 Windows PE 中运行此步骤。   

 在此步骤中使用以下任务序列变量：  
 - [SMSRebootMessage](/sccm/osd/understand/task-sequence-variables#SMSRebootMessage)  
 - [SMSRebootTimeout](/sccm/osd/understand/task-sequence-variables#SMSRebootTimeout)  


 单击任务序列编辑器中的“添加”，选择“常规”，然后选择“重新启动计算机”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>分配给此任务序列的启动映像
 对目标计算机选择此选项以使用分配给该任务序列的启动映像。 在 Windows PE 中，任务序列使用启动映像运行后续步骤。  

#### <a name="the-currently-installed-default-operating-system"></a>当前安装的默认操作系统
 对目标计算机选择此选项以重新启动到安装的 OS。  

#### <a name="notify-the-user-before-restarting"></a>重新启动之前通知用户
 选择此选项以在目标计算机重新启动前向用户显示通知。 步骤默认选择此选项。  

#### <a name="notification-message"></a>通知消息
 输入在目标计算机重新启动之前向用户显示的通知消息。  

#### <a name="message-display-time-out"></a>消息显示超时
 指定在目标计算机重新启动之前的时间量（秒）。 默认值为 60 秒。  



##  <a name="BKMK_RestoreUserState"></a>还原用户状态  

 使用此步骤来启动用户状态迁移工具 (USMT) 将用户状态和设置还原到目标计算机。 将此步骤与“捕获用户状态”步骤结合使用。  

 有关部署操作系统时管理用户状态的详细信息，请参阅[管理用户状态](/sccm/osd/get-started/manage-user-state)。  

 将此步骤与“请求状态存储”和“发布状态存储”步骤结合使用，以使用状态迁移点保存或还原状态设置。 此选项始终使用由 Configuration Manager 生成并管理的加密密钥解密 USMT 状态存储。  

 “还原用户状态”步骤提供对最常用 USMT 选项的受限子网的控制。 为其他命令行选项指定 OSDMigrateAdditionalRestoreOptions 变量。  

 > [!IMPORTANT]  
 >  如果将此步骤用于与 OS 部署方案无关的目的，请在“还原用户状态”步骤之后（紧接着）添加[重启计算机](#BKMK_RestartComputer)步骤。  

 此步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。   

 在此步骤中使用以下任务序列变量：  
 - [_OSDMigrateUsmtRestorePackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtRestorePackageID)  
 - [OSDMigrateAdditionalRestoreOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalRestoreOptions)  
 - [OSDMigrateContinueOnRestore](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnRestore)  
 - [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)  
 - [OSDMigrateLocalAccounts](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccounts)  
 - [OSDMigrateLocalAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccountPassword)  
 - [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  


 单击任务序列编辑器中的“添加”，选择“用户状态”，然后选择“还原用户状态”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="user-state-migration-tool-package"></a>用户状态迁移工具包
 指定包，该包包含此步骤要使用的 USMT 版本。 此包不需要程序。 步骤运行时，任务序列使用指定的包中的 USMT 版本。 指定包含 32 位或 64 位版本 USMT 的包。 USMT 的体系结构取决于任务序列将向其还原状态的 OS 的体系结构。 

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>使用标准选项还原所有捕获的用户配置文件
 使用标准选项还原捕获的用户配置文件。 要自定义 USMT 还原的选项，请选择“自定义用户配置文件捕获”。  

#### <a name="customize-how-user-profiles-are-restored"></a>自定义如何还原用户配置文件
 允许你自定义想要还原到目标计算机的文件。 单击  “文件”以指定想要用于还原用户配置文件的 USMT 包中的配置文件。 要添加配置文件，请在“文件名”  框中输入文件的名称，然后单击“添加” 。 “文件”窗格列出 USMT 使用的配置文件。 指定的 .xml 文件用于定义 USMT 还原的用户文件。  

#### <a name="restore-local-computer-user-profiles"></a>还原本地计算机用户配置文件
 还原本地计算机用户配置文件。 这些配置文件不适用于域用户。 向已还原的本地用户帐户分配新密码。 USMT 无法迁移原始密码。 在“密码”  框中输入新密码，然后在“确认密码”  框中确认该密码。  

#### <a name="continue-if-some-files-cannot-be-restored"></a>如果无法还原某些文件则继续
 继续还原用户状态和设置，即使 USMT 无法还原某些文件。 步骤默认启用此选项。 如果还原文件时禁用此选项且 USMT 遇到错误，此步骤将立即失败。 USMT 不会还原所有文件。   

#### <a name="enable-verbose-logging"></a>启用详细日志记录
 启用此选项以生成更详细的日志文件信息。 还原状态时，任务序列将生成日志 Loadstate.log 并默认存储在 `%WinDir%\ccm\logs` 文件夹的任务序列日志文件夹中。  



##  <a name="BKMK_RunCommandLine"></a>运行命令行  

 使用此步骤运行指定命令行。  

 可以在完整 OS 或 Windows PE 中运行此步骤。   

 在此步骤中使用以下任务序列变量：  
 - [OSDDoNotLogCommand](/sccm/osd/understand/task-sequence-variables#OSDDoNotLogCommand)（从版本 1806 开始）<!--1358493-->  
 - [SMSTSDisableWow64Redirection](/sccm/osd/understand/task-sequence-variables#SMSTSDisableWow64Redirection)  
 - [SMSTSRunCommandLineUserName](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLineUserName)  
 - [SMSTSRunCommandLinePassword](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLinePassword)  
 - [WorkingDirectory](/sccm/osd/understand/task-sequence-variables#WorkingDirectory)  


 单击任务序列编辑器中的“添加”，选择“常规”，然后选择“运行命令行”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="command-line"></a>命令行
 指定任务序列运行的命令行。 此字段为必需字段。 包括文件扩展名，例如 .vbs 和 .exe。 包括所有必需的设置文件和命令行选项。  

 如果没有指定文件扩展名，则 Configuration Manager 会尝试查找 .com、.exe 和 .bat。 如果文件扩展名不是可执行文件类型，则 Configuration Manager 会尝试应用本地关联。 例如，如果命令行为 readme.gif，则 Configuration Manager 会启动目标计算机上指定的应用程序来打开 .gif 文件。  

 示例：  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

 > [!NOTE]  
 >  若要成功运行，在命令行操作之前使用 cmd.exe /c 命令。 这些操作的示例包括输出重定向、管道和复制命令。  

#### <a name="disable-64-bit-file-system-redirection"></a>禁用 64 位文件系统重定向
 64 位操作系统默认使用 WOW64 文件系统重定向程序运行命令行。 此行为可正确找到 32 位版本的 OS 可执行文件和库。 选择此选项可禁用 WOW64 文件系统重定向程序。 Windows 使用本机 64 位版本的 OS 可执行文件和库来运行命令。 如果在 32 位 OS 上运行，此选项没有任何影响。  

#### <a name="start-in"></a>开始于
 指定程序的可执行文件夹，最多 127 个字符。 此文件夹可以是目标计算机上的绝对路径，也可以是包含包的分发点文件夹的相对路径。 此字段是可选的。  

 示例：  

 `c:\officexp`  

 `i386`  

 > [!NOTE]  
 >  可使用“浏览”按钮浏览本地计算机上的文件和文件夹。 选择的任何内容还必须在目标计算机上。 它必须在相同的位置，并具有相同的文件名和文件夹名称。  

#### <a name="package"></a>包
 当在命令行上指定了目标计算机上尚不存在的文件或程序时，请选择此选项以指定包含所需文件的 Configuration Manager 包。 此包不需要程序。 如果指定的文件在目标计算机上，则不需要此选项。  

#### <a name="time-out"></a>超时
 指定表示 Configuration Manager 将允许命令行运行的时间长度的值。 此值的范围为 1 分钟至 999 分钟。 默认值为 15 分钟。 默认情况下禁用此选项。  

 > [!IMPORTANT]  
 >  如果输入的值未提供足够时间来成功完成指定命令，此步骤将失败。 整个任务序列可能失败，具体取决于步骤或组条件。 如果超时过期，Configuration Manager 将终止命令行进程。  

#### <a name="run-this-step-as-the-following-account"></a>作为以下帐户运行此步骤
 指定作为本地系统帐户之外的其他 Windows 用户帐户运行的命令行。  

 > [!NOTE]  
 >  若要在安装 OS 后使用其他帐户运行简单脚本或命令，则首先向计算机添加该帐户。 此外，可能需要还原 Windows 用户配置文件才能运行更复杂的程序，如 Windows Installer。  

#### <a name="account"></a>帐户
 指定此步骤运行命令行时要使用的 Windows 用户帐户。 命令行将使用指定帐户的权限运行。 单击“设置”  以指定本地用户或域帐户。 有关任务序列运行方式帐户的详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account)。

 > [!IMPORTANT]  
 >  如果此步骤指定用户帐户并在 Windows PE 中运行，操作将失败。 Windows PE 无法加入域。 smsts.log 文件将记录这一失败。  



##  <a name="BKMK_RunPowerShellScript"></a>运行 PowerShell 脚本  

 使用此步骤运行指定的 Windows PowerShell 脚本。  

 可以在完整 OS 或 Windows PE 中运行此步骤。 若要在 Windows PE 中运行此步骤，请在启动映像中启用 PowerShell。 从启动映像属性中的“可选组件”选项卡中启用 WinPE-PowerShell 组件。 有关如何修改启动映像的详细信息，请参阅[管理启动映像](/sccm/osd/get-started/manage-boot-images)。  

 > [!NOTE]  
 >  默认情况下，Windows Embedded 操作系统上未启用 PowerShell。  

 单击任务序列编辑器中的“添加”，选择“常规”，然后选择“运行 PowerShell 脚本”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="package"></a>包
 指定包含 PowerShell 脚本的 Configuration Manager 包。 一个包可以包含多个 PowerShell 脚本。  

#### <a name="script-name"></a>脚本名称
 指定要运行的 PowerShell 脚本的名称。 此字段为必需字段。  

#### <a name="parameters"></a>参数
 指定要传递给 PowerShell 脚本的参数。 这些参数与命令行中的 PowerShell 脚本参数相同。  

 > [!IMPORTANT]  
 >  提供脚本使用的参数，而不是为 Windows PowerShell 命令行。  
 >   
 >  以下示例包含有效的参数：  
 >   
 >  `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
 >   
 >  以下示例包含无效的参数。 前两项是 Windows PowerShell 命令行参数（-NoLogo 和 -ExecutionPolicy Unrestricted）。 脚本不会使用这些参数。  
 >   
 >  `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

#### <a name="powershell-execution-policy"></a>PowerShell 执行策略
 确定允许在计算机上运行的 PowerShell 脚本（如果有）。 选择以下其中一个执行策略：  

 -   **AllSigned**：只能运行由受信任的发布者签发的脚本  

 -   **Undefined**：请勿定义任何执行策略  

 -   **Bypass**：加载所有配置文件并运行所有脚本。 如果从 Internet 下载未签名的脚本，Windows PowerShell 不会在运行脚本前提示需要权限。  


 > [!IMPORTANT]  
 >  PowerShell 1.0 不支持未定义和旁路执行策略。  



##  <a name="child-task-sequence"></a> 运行任务序列

 > [!Note]  
 > 默认情况下，Configuration Manager 不启用此项可选功能。 在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。

 从 Configuration Manager 版本 1710 开始，可以添加运行另一个任务序列的新步骤。 此步骤将创建任务序列之间的父子关系。 使用子任务序列，可以创建更模块化、可重复使用的任务序列。

 将子任务序列添加到任务序列时，请考虑以下几点：  

 - 父和子任务序列有效地组合成客户端运行的单个策略。  

 - 该环境是全局环境。 如果父任务序列设置一个变量，然后子任务序列更改该变量，将保留最新值。 如果子任务序列新建一个变量，则可用于父任务序列的其余部分。  

 - 对于单个任务序列操作，状态消息均按正常发送。  

 - 任务序列将条目写入 smsts.log 文件，包括在子任务序列启动时使其清晰明确的新日志条目。  


 单击任务序列编辑器中的“添加”，选择“常规”，然后选择“运行任务序列”以添加此步骤。 


### <a name="properties"></a>属性

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="select-task-sequence-to-run"></a>选择要运行的任务序列
 单击“浏览”，选择子任务序列。 “选择任务序列”对话框不会显示父任务序列。



##  <a name="BKMK_SetDynamicVariables"></a>设置动态变量  

 使用此步骤来执行以下操作：  

 1.  从计算机及其环境中收集信息。 然后为指定的任务序列变量设置信息。  

 2.  评估定义的规则。 基于评估为 true 的规则设置任务序列变量。  


 任务序列自动设置以下只读任务序列变量：  
 - [\_SMSTSMake](/sccm/osd/understand/task-sequence-variables#SMSTSMake)  
 - [\_SMSTSModel](/sccm/osd/understand/task-sequence-variables#SMSTSModel)  
 - [\_SMSTSMacAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSMacAddresses)  
 - [\_SMSTSIPAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSIPAddresses)  
 - [\_SMSTSSerialNumber](/sccm/osd/understand/task-sequence-variables#SMSTSSerialNumber)  
 - [\_SMSTSAssetTag](/sccm/osd/understand/task-sequence-variables#SMSTSAssetTag)  
 - [\_SMSTSUUID](/sccm/osd/understand/task-sequence-variables#SMSTSUUID)  


 可以在完整 OS 或 Windows PE 中运行此步骤。  

 单击任务序列编辑器中的“添加”，选择“常规”，然后选择“设置动态变量”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="dynamic-rules-and-variables"></a>动态规则和变量
 若要设置在任务序列中使用的动态变量，请添加规则。 然后为规则中指定的每个变量设置一个值。 此外，还需在不添加规则的情况下添加一个或多个变量。 添加规则时，可以从以下类别中进行选择：  

 - **计算机**：评估硬件资产标记、UUID、序列号或 MAC 地址的值。 根据需要，设置多个值。 如果任何值为 true，则规则评估为 true。 例如，如果设备序列号为 5892087 且 MAC 地址为 22-A4-5A-13-78-26，则下面的规则评估为 true：  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

 - **位置**：评估默认网关的值  

 - **品牌和型号**：评估计算机的品牌和型号的值。 品牌和型号均必须评估为 true，规则才能评估为 true。   

    指定一个星号 (`*`) 和问号 (`?`) 作为通配符字符。 星号匹配多个字符，问号匹配单个字符。 例如，字符串 `DELL*900?` 同时匹配 `DELL-ABC-9001` 和 `DELL9009`。  

 - **任务序列变量**：添加要评估的任务序列变量、条件和值。 当为变量设置的值符合指定条件时，规则评估为 true。  

    指定为规则设置的一个或多个变量，该规则评估为 true，或设置变量而无需使用规则。 选择现有变量或创建自定义变量。  

     - **现有任务序列变量**：从现有任务序列变量的列表中选择一个或多个变量。 不可选择数组变量。  

     - **自定义任务序列变量**：定义自定义任务序列变量。 你也可指定现有任务序列变量。 此设置有助于指定现有变量数组，如 OSDAdapter，因为变量数组不在现有任务序列变量的列表中。  


 为规则选择变量后，为每个变量提供一个值。 规则评估为 true 时，则变量设置为指定的值。 对于每个变量，可以选择“机密值”  来隐藏该变量的值。 默认情况下，某些现有变量隐藏值，例如 OSDCaptureAccountPassword 变量。  

 > [!IMPORTANT]  
 >  当使用“设置动态变量”步骤导入任务序列时，Configuration Manager 删除标记为“机密值”的所有变量值。 导入任务序列后请重新输入动态变量的值。  



##  <a name="BKMK_SetTaskSequenceVariable"></a>设置任务序列变量  

 使用此步骤来设置与该任务序列配合使用的变量的值。  

 可以在完整 OS 或 Windows PE 中运行此步骤。 

 任务序列变量由任务序列操作读取，并指定这些操作的行为。 有关特定任务序列变量以及如何使用它们的详细信息，请参阅以下文章：  
 - [如何使用任务序列变量](/sccm/osd/understand/using-task-sequence-variables)  
 - [任务序列变量](/sccm/osd/understand/task-sequence-variables)  


 单击任务序列编辑器中的“添加”，选择“常规”，然后选择“设置任务序列变量”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="task-sequence-variable"></a>任务序列变量：
 指定任务序列内置或活动变量的名称，或者指定用户定义的变量名。  

#### <a name="do-not-display-this-value"></a>不显示此值
 <!--1358330--> 从版本 1806 开始，启用此选项来屏蔽存储在任务序列变量中的敏感数据。 例如，指定密码时。 

#### <a name="value"></a>值  
 任务序列将变量设置为此值。 使用语法 `%varname%` 将此任务序列变量设置为另一任务序列变量的值。  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a>安装 Windows 和 ConfigMgr  

 使用此步骤执行从 Windows PE 到新 OS 的转换。 此任务序列步骤是在部署任何 OS 时都必需的部分。 该步骤会将 Configuration Manager 客户端安装到新 OS 中，并为任务序列在新 OS 中继续执行做好准备。  

 此步骤仅可在 Windows PE 中运行。 它不会在完整的 OS 中运行。  

 在此步骤中使用以下任务序列变量：  
 - [SMSClientInstallProperties](/sccm/osd/understand/task-sequence-variables#SMSClientInstallProperties)  


 此步骤使用 Windows PE 安装目录 `X:\Windows` 替换 sysprep.inf 或 unattend.xml 目录变量，例如 `%WINDIR%` 和 `%ProgramFiles%`。 任务序列会忽略使用这些环境变量指定的变量。  

 单击任务序列编辑器中的“添加”，选择“映像”，然后选择“安装 Windows 和 ConfigMgr”以添加此步骤。 


### <a name="step-actions"></a>步骤操作

 此步骤将执行以下操作：  

#### <a name="preliminaries-windows-pe"></a>初步操作：Windows PE  

 1.  替换 unattend.xml 文件中的任务序列变量。  

 2.  下载包含 Configuration Manager 客户端的包。 将包添加到部署的映像。  

#### <a name="set-up-windows"></a>设置 Windows  

 -  基于映像的安装  

    1.  如果存在，请禁用映像中的 Configuration Manager 客户端。 换言之，为 Configuration Manager 客户端服务禁用“自动启动”。  

    2.  更新已部署映像中的注册表，使用与引用计算机上相同的驱动器号启动已部署的 OS。  

    3.  重新启动到部署的 OS。  

    4.  Windows 最小化安装使用先前指定的已禁用所有最终用户交互的 sysprep.inf 或 unattend.xml 答案文件运行。 如果使用“应用网络设置”步骤加入域，则该信息位于答案文件。 Windows 最小化安装会将计算机加入域。  

 -  基于 Setup.exe 的安装。 运行 Setup.exe 会执行典型的 Windows 安装过程：  

    1.  将“应用操作系统”步骤中指定的 OS 升级包复制到硬盘驱动器。  

    2.  重新启动到新部署的 OS。  

    3.  Windows 最小化安装使用先前指定的已禁用所有用户界面设置的 sysprep.inf 或 unattend.xml 答案文件运行。 如果使用“应用网络设置”步骤加入域，则该信息位于答案文件。 Windows 最小化安装会将计算机加入域。  

#### <a name="set-up-the-configuration-manager-client"></a>安装 Configuration Manager 客户端  

 1.  Windows 最小化安装结束后，任务序列将使用 setupcomplete.cmd 继续运行。  

 2.  根据在“应用 Windows 设置”步骤中选择的选项，启用或禁用本地管理员帐户。  

 3.  使用先前下载的包以及此步骤中指定的安装属性，安装 Configuration Manager 客户端。 客户端以“设置模式”进行安装。 此模式防止客户端在任务序列完成之前处理新策略请求。  

 4.  等待客户端完全可以操作。  

#### <a name="the-step-completes"></a>步骤完成
 任务序列继续运行下一个步骤。  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="client-package"></a>客户端包
 单击“浏览”，并选择此步骤要使用的 Configuration Manager 客户端安装包。  

#### <a name="use-pre-production-client-package-when-available"></a>如果可用，使用预生产客户端包
 如有可用的预生产客户端包，并且该计算机是试点集合的成员，则任务序列使用此包而非生产客户端包。 预生产客户端是在生产环境中用于测试的较新版本。 单击“浏览”，并选择此步骤要使用的预生产客户端安装包。  

#### <a name="installation-properties"></a>安装属性
 任务序列步骤自动指定站点分配和默认配置。 使用此字段来指定安装客户端时使用的任何其他安装属性。 要输入多个安装属性，请使用空格分隔。  

 指定要在客户端安装过程中使用的命令行选项。 例如，输入 `/skipprereq: silverlight.exe` 以通知 CCMSetup.exe 不安装 Microsoft Silverlight 必备组件。 有关 CCMSetup.exe 的可用命令行选项的详细信息，请参阅[关于客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。  


### <a name="options"></a>选项

 > [!NOTE]  
 > 请勿启用“选项”选项卡上的“出错时继续”。如果此步骤出错，不管是否启用此设置，任务序列都将失败。  



##  <a name="BKMK_UpgradeOS"></a>升级操作系统  

 > [!TIP]  
 > 从 Windows 10 1709 版开始，媒体包括多个版本。 如果要将任务序列配置为使用 OS 升级包或 OS 映像，请务必选择[支持的版本](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client)。  

 使用此步骤将较旧版本的 Windows 升级到较新版本的 Windows 10。  

 此任务序列步骤仅可在完整的 OS 中运行。 不可在 Windows PE 中运行。  

 在此步骤中使用以下任务序列变量：  
 - [_SMSTSOSUpgradeActionReturnCode](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode)  
 - [OSDSetupAdditionalUpgradeOptions](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions)  


 单击任务序列编辑器中的“添加”，选择“映像”，然后选择“升级操作系统”以添加此步骤。 


### <a name="properties"></a>属性  

 在此步骤的“属性”选项卡上，请配置此部分中描述的设置。  

#### <a name="upgrade-package"></a>升级包
 选择此选项以指定用于升级的 Windows 10 OS 升级包。  

#### <a name="source-path"></a>源路径
 指定 Windows 安装程序要使用的 Windows 10 媒体的本地或网络路径。 此设置对应于 Windows 安装程序命令行选项 `/InstallFrom`。 

 还可以指定一个变量，例如 `%MyContentPath%` 或 `%DPC01%`。 将变量用作源路径时，必须在任务序列中提前设置其值。 例如，使用[下载包内容](#BKMK_DownloadPackageContent)步骤，为 OS 升级包的位置指定一个变量。 然后，在此步骤中将该变量用作源路径。  

#### <a name="edition"></a>版本
 指定要用于升级的 OS 媒体的版本。  

#### <a name="product-key"></a>产品密钥
 指定要用于升级过程的产品密钥。  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>在升级过程中向 Windows 安装程序提供以下驱动程序内容
 升级过程中将驱动程序添加到目标计算机。 此设置对应于 Windows 安装程序命令行选项 `/InstallDriver`。 驱动程序必须与 Windows 10 兼容。 指定下列选项之一：  

 - **驱动程序包**：单击“浏览”并从列表中选择现有的驱动程序包。  

 - **预留内容**：选择此选项以指定驱动程序包的位置。 可以指定本地文件夹、网络路径或任务序列变量。 将变量用作源路径时，必须在任务序列中提前设置其值。 例如，通过使用[下载包内容](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent)步骤。  

#### <a name="time-out-minutes"></a>超时（分钟）
 指定 Configuration Manager 执行此步骤失败前的分钟数。 如果 Windows 安装程序停止进程但未终止，则此选项非常有用。  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>不启动升级而执行 Windows 安装程序兼容性扫描
 在不启动升级进程的情况下执行 Windows 安装程序兼容性扫描。 此设置对应于 Windows 安装程序命令行选项 `/Compat ScanOnly`。 使用此选项部署整个 OS 升级包。 

 <!--SCCMDocs-pr issue 2812--> 从版本 1806 开始，当启用此选项，此步骤不会将 Configuration Manager 客户端置于预配模式。 Windows 安装程序在后台以无提示方式运行，且客户端将继续正常工作。 

 安装程序将退出代码作为扫描结果返回。 下表提供了一些常见的退出代码：  

 |退出代码|详细信息|  
 |-|-|  
 |MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|不存在兼容性问题（“成功”）。|  
 |MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|可操作的兼容性问题。|  
 |MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|所选的迁移选项不可用。 例如，从 Enterprise 升级到 Professional。|  
 |MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|不适合 Windows 10。|  
 |MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|可用磁盘空间不足。|  

 有关此参数的详细信息，请参阅 [Windows 安装程序命令行选项](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#6)。  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>忽略任何不重要的兼容性消息
 指定安装程序完成安装，忽略任何不重要的兼容性消息。 此设置对应于 Windows 安装程序命令行选项 `/Compat IgnoreWarning`。  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>通过 Windows Update 动态更新 Windows 安装程序
 使安装程序能够执行动态更新操作，例如搜索、下载和安装更新。 此设置对应于 Windows 安装程序命令行选项 `/DynamicUpdate`。 此设置与 Configuration Manager 软件更新不兼容。 如果要使用独立 Windows Server Update Services (WSUS) 或适用于企业的 Windows 更新管理更新，可启用此选项。  

#### <a name="override-policy-and-use-default-microsoft-update"></a>替代策略并使用默认 Windows 更新
 临时实时覆盖本地策略以运行动态更新操作。 计算机从 Windows 更新获取更新。
