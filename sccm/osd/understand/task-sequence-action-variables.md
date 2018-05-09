---
title: 任务序列操作变量
titleSuffix: Configuration Manager
description: 使用序列操作变量（如网络设置变量）来指定 Configuration Manager 任务序列中单个步骤的配置设置。
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e2269031-0977-4f01-a274-420e00630575
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f66203e335524fa922ec1b6ab3dd4dc5fb917b0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的任务序列操作变量

*适用范围：System Center Configuration Manager (Current Branch)*

任务序列操作变量指定在 System Center Configuration Manager 任务序列中单个步骤使用的配置设置。 默认情况下，任务序列步骤在运行之前会先初始化其设置。 仅当相关联的任务序列步骤运行时，这些设置才可用。 换句话说，任务序列在运行之前，会将操作变量值添加到任务序列环境。 该步骤运行之后，任务序列再从环境中删除该值。  

## <a name="action-variable-example"></a>操作变量示例  
 例如，通过使用“运行命令行”  任务序列步骤为命令行操作指定开始目录。 此步骤包括“开始”  属性，其默认值作为 **WorkingDirectory** 变量存储在任务序列环境中。 **WorkingDirectory** 环境变量在运行“运行命令行”  任务序列操作前会被初始化。 在“运行命令行”  步骤过程中，通过“开始”  属性可以访问 **WorkingDirectory** 值。 该步骤完成之后，任务序列从环境中删除 WorkingDirectory 变量值。 如果序列包含另一个“运行命令行”任务序列步骤，则该任务序列会初始化新的 WorkingDirectory 变量并将其设置为当前步骤的启动值。  

 任务序列步骤运行时，任务序列操作变量的默认值为 present。 如果设置为新值，该值可供任务序列中的多个步骤使用。 如果使用任务序列变量创建方法之一来替代内置变量值，则新值仍将保留在环境中，并替代任务序列中其他步骤的默认值。 例如，如果将“设置任务序列变量”步骤添加为任务序列的第一个步骤，并将 WorkingDirectory 变量设置为 C:\\，则任务序列中的任何“运行命令行”步骤都将使用新的开始目录值。  

## <a name="action-variables-for-task-sequence-actions"></a>任务序列操作的操作变量  
 Configuration Manager 任务序列变量按照关联的任务序列操作进行分组。 使用以下链接收集与特定操作相关联的操作变量的相关信息。 任务序列变量控制任务序列操作的工作方式。 任务序列操作读取和使用标记为输入变量的变量。 或者，也可以使用[设置任务序列变量](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)步骤或 TSEnvironment COM 对象在运行时设置变量。 只有任务序列操作会将变量标记为输出变量。 任务序列中稍后发生的操作会读取这些输出变量。  

> [!NOTE]  
>  不是所有的任务序列操作都与任务序列变量集相关联。 例如，虽然有与启用 BitLocker 操作相关联的变量，但没有与禁用 BitLocker 操作相关联的变量。  



###  <a name="BKMK_ApplyDataImage"></a>应用数据映像   
 有关详细信息，请参阅[应用数据映像](task-sequence-steps.md#BKMK_ApplyDataImage)。 

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (input)|指定应用于目标计算机上的映像的索引值。|  
|OSDWipeDestinationPartition<br /><br /> (input)|指定是否删除位于目标分区上的文件。<br /><br /> 有效值：<br /><br /> true（默认值）<br /><br /> false|  



###  <a name="BKMK_ApplyDriverPackage"></a>应用驱动程序包   
有关详细信息，请参阅[应用驱动程序](task-sequence-steps.md#BKMK_ApplyDriverPackage)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (input)|指定要从驱动程序包中进行安装的大容量存储驱动程序的内容 ID。 如果没有指定此变量，则不安装大容量存储驱动程序。|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (input)|指定要安装的大容量存储驱动程序的 INF 文件。<br /><br /> <br /><br /> 如果设置了 OSDApplyDriverBootCriticalContentUniqueID，则需要此任务序列变量。|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (input)|指定无论是否安装大容量存储设备驱动程序，此变量都必须为 scsi。<br /><br /> 如果设置了 OSDApplyDriverBootCriticalContentUniqueID，则需要此任务序列变量。|  
|OSDApplyDriverBootCriticalID<br /><br /> (input)|指定要安装的大容量存储设备驱动程序的启动关键 ID。 此 ID 列在设备驱动程序 txtsetup.oem 文件的 scsi 部分中。<br /><br /> 如果设置了 OSDApplyDriverBootCriticalContentUniqueID，则需要此任务序列变量。|  
|OSDAllowUnsignedDriver<br /><br /> (input)|指定是否将 Windows 配置为允许安装未签名的设备驱动程序。 部署 Windows Vista 和更高版本的操作系统时不使用此任务序列变量。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  



###  <a name="BKMK_ApplyNetworkSettings"></a>应用网络设置   
 有关详细信息，请参阅[应用网络设置](task-sequence-steps.md#BKMK_ApplyNetworkSettings)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (input)|此任务序列变量是一个数组变量。 数组中的每个元素都代表计算机上单个网络适配器的设置。 通过将数组变量名称与基于零的网络适配器下标及属性名称组合，访问每个适配器的设置。<br /><br />如果此步骤配置多个网络适配器，则定义第二个网络适配器的属性，方法是使用变量名称中的下标。 例如，OSDAdapter1EnableDHCP、OSDAdapter1IPAddressList、OSDAdapter1DNSDomain、OSDAdapter1WINSServerList 和 OSDAdapter1EnableWINS。<br /><br />例如，以下变量名称可用于为将由此任务序列步骤配置的第一个网络适配器定义属性：<br /><br /> <ul><li>**OSDAdapter0EnableDHCP**：设置为“true”将为适配器启用动态主机配置协议 (DHCP)。<br />    此设置是必需的。 可用的值有：True 或 False。</li><li>**OSDAdapter0IPAddressList**：以逗号分隔的适配器 IP 地址列表。 除非 **EnableDHCP** 设置为 **false**，否则将忽略此属性。<br />    此设置是必需的。</li><li>**OSDAdapter0SubnetMask**：以逗号分隔的子网掩码列表。 除非 **EnableDHCP** 设置为 **false**，否则将忽略此属性。<br />    此设置是必需的。</li><li>**OSDAdapter0Gateways**：以逗号分隔的 IP 网关地址列表。 除非 **EnableDHCP** 设置为 **false**，否则将忽略此属性。<br />    此设置是必需的。</li><li>**OSDAdapter0DNSDomain**：适配器的域名系统 (DNS) 域。</li><li>**OSDAdapter0DNSServerList**：以逗号分隔的适配器 DNS 服务器列表。<br />    此设置是必需的。</li><li>**OSDAdapter0EnableDNSRegistration**：设置为 true 将在 DNS 中为适配器注册 IP 地址。</li><li>**OSDAdapter0EnableFullDNSRegistration**：设置为 true 将根据计算机的完整 DNS 名称在 DNS 中为适配器注册 IP 地址。</li><li>**OSDAdapter0EnableIPProtocolFiltering**：设置为 true 将在适配器上启用 IP 协议筛选。</li><li>**OSDAdapter0IPProtocolFilterList**：以逗号分隔的协议列表，这些协议被允许在 IP 的上层运行。 如果 **EnableIPProtocolFiltering** 设置为 **false**，将忽略此属性。</li><li>**OSDAdapter0EnableTCPFiltering**：设置为 true 将为适配器启用 TCP 端口筛选。</li><li>**OSDAdapter0TCPFilterPortList**：以逗号分隔的端口列表，这些端口将被授予对 TCP 的访问权限。 如果 **EnableTCPFiltering** 设置为 **false**，将忽略此属性。</li><li>**OSDAdapter0TcpipNetbiosOptions**：TCP/IP 上层的 NetBIOS 选项。 可能的值如下：<br /><br /> <ul><li>**0**：使用 DHCP 服务器中的 NetBIOS 设置。</li><li>**1**：启用 TCP/IP 上层的 NetBIOS。</li><li>**2**：禁用 TCP/IP 上层的 NetBIOS。</li></ul></li><li>**OSDAdapter0EnableWINS**：设置为 true 将为名称解析使用 WINS。</li><li>**OSDAdapter0WINSServerList**：以逗号分隔的 WINS 服务器 IP 地址列表。 除非 **EnableWINS** 设置为 **true**，否则将忽略此属性。</li><li>**OSDAdapter0MacAddress**：MAC 地址，用于匹配物理网络适配器的设置。</li><li>**OSDAdapter0Name**：显示在网络连接控制面板程序中的网络连接的名称。 该名称的长度介于 0 到 255 个字符之间。</li><li>**OSDAdapter0Index**：设置数组中网络适配器设置的下标。<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (input)|指定目标计算机上安装的网络适配器的数目。 在设置 **OSDAdapterCount** 值时，必须为每个适配器的所有配置选项设置值。 例如，如果为一个特定的适配器设置 **OSDAdapterTCPIPNetbiosOptions** 值，那么也必须设置该适配器的所有值。<br /><br />如果未指定此值，将忽略所有的 **OSDAdapter** 值。|  
|OSDDNSDomain<br /><br /> (input)|指定目标计算机使用的主 DNS 服务器。|  
|OSDDomainName<br /><br /> (input)|指定目标计算机加入的 Windows 域的名称。 指定的值必须是有效的 Active Directory 域服务的域名。|  
|OSDDomainOUName<br /><br /> (input)|指定目标计算机加入的组织单位 (OU) 的 RFC 1779 格式名称。 如果指定了值，该值必须包含完整路径。<br /><br /> 例如：<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (input)|指定是否启用 TCP/IP 筛选。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  
|OSDJoinAccount<br /><br /> (input)|指定用于将目标计算机添加到 Windows 域的网络帐户。|  
|OSDJoinPassword<br /><br /> (input)|指定用于将目标计算机添加到 Windows 域的网络密码。|  
|OSDNetworkJoinType<br /><br /> (input)|指定目标计算机是否加入 Windows 域或工作组。<br /><br /> “0”指示目标计算机加入 Windows 域。 “1”指定计算机加入工作组。<br /><br /> 有效值：<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (input)|指定目标计算机的 DNS 搜索顺序。|  
|OSDWorkgroupName<br /><br /> (input)|指定目标计算机加入的工作组的名称。<br /><br /> 指定此值或 OSDDomainName 值。 工作组名称最多可使用 32 个字符。<br /><br /> 例如：<br /><br /> Accounting|  



###  <a name="BKMK_ApplyOperatingSystem"></a>应用操作系统映像   
 有关详细信息，请参阅 [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (input)|指定与操作系统部署包关联的操作系统部署答案文件的文件名。|  
|OSDImageIndex<br /><br /> (input)|指定应用于目标计算机上的 WIM 文件的映像索引值。|  
|OSDInstallEditionIndex<br /><br /> (input)|指定安装的 Windows Vista 或更高版本操作系统的版本。 如果没有指定版本，Windows 安装程序将使用引用的产品密钥来确定安装哪个版本。<br /><br /> 如果以下条件成立，则仅使用零 (0) 值：<br /><br /> -   正在安装 Windows Vista 预装版操作系统<br />-   正在安装批量许可证版或更高版的 Windows Vista，没有指定产品秘钥。<br /><br /> 有效值：<br /><br /> 0（默认值）|  
|OSDTargetSystemDrive (output)|指定包含操作系统文件的分区的驱动器号。|  



###  <a name="BKMK_ApplyWindowsSettings"></a>应用 Windows 设置   
 有关详细信息，请参阅 [应用 Windows 设置](task-sequence-steps.md#BKMK_ApplyWindowsSettings)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (input)|指定目标计算机的名称。<br /><br /> 例如：<br /><br /> %_SMSTSMachineName%默认值|  
|OSDProductKey<br /><br /> (input)|指定 Windows 产品密钥。 指定的值字符数必须介于 1 和 255 之间。|  
|OSDRegisteredUserName<br /><br /> (input)|指定新操作系统中的默认注册用户名。 指定的值字符数必须介于 1 和 255 之间。|  
|OSDRegisteredOrgName<br /><br /> (input)|指定新操作系统中的默认注册组织名称。 指定的值字符数必须介于 1 和 255 之间。|  
|OSDTimeZone<br /><br /> (input)|指定在新操作系统中使用的默认时区设置。|  
|OSDServerLicenseMode<br /><br /> (input)|指定使用的 Windows Server 许可证模式。<br /><br /> 有效值：<br /><br /> PerSeat<br /><br /> PerServer|  
|OSDServerLicenseConnectionLimit<br /><br /> (input)|指定允许的最大连接数。 指定的连接数必须介于 5 和 9999 之间。|  
|OSDRandomAdminPassword<br /><br /> (input)|指定在新操作系统中为管理员帐户随机生成的密码。 如果设置为 true，Windows 安装程序将在目标计算机上禁用本地管理员帐户。 如果设置为 false，Windows 安装程序将在目标计算机上启用本地管理员帐户，并将帐户密码设置为值 OSDLocalAdminPassword。<br /><br /> 有效值：<br /><br /> true（默认值）<br /><br /> false|  
|OSDLocalAdminPassword<br /><br /> (input)|指定本地管理员密码。 如果启用“随机生成本地管理员密码并在所有支持的平台上禁用帐户” ，则该步骤将忽略此变量。 指定的值字符数必须介于 1 和 255 之间。|  



###  <a name="BKMK_AutoApplyDrivers"></a>自动应用驱动程序   
 有关详细信息，请参阅[自动应用驱动程序](task-sequence-steps.md#BKMK_AutoApplyDrivers)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (input)|驱动程序目录类别唯一 ID 的以逗号分隔的列表。 “自动应用驱动程序”步骤只考虑至少一个指定类别中的驱动程序。 此值是可选的，默认情况下不设置。 可以通过枚举站点上的 SMS_CategoryInstance 对象列表来获取可用的类别 ID。|  
|OSDAllowUnsignedDriver<br /><br /> (input)|指定是否将 Windows 配置为允许安装未签名的设备驱动程序。 部署 Windows Vista 和更高版本的操作系统时不使用此任务序列变量。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  
|OSDAutoApplyDriverBestMatch<br /><br /> (input)|如果驱动程序目录中有多个设备驱动程序与硬件设备兼容，此变量确定步骤的操作。 如果设置为 true，则此步骤仅安装最好的设备驱动程序。 如果设置为 false此步骤会安装所有兼容的设备驱动程序并且 Windows 会选择使用最适合的驱动程序。<br /><br /> 有效值：<br /><br /> true（默认值）<br /><br /> false|  
|SMSTSDriverRequestConnectTimeOut|请求驱动程序目录时，此变量用于指定任务序列等待 HTTP 服务器连接的秒数。 如果连接时间超过超时设定值，任务序列会取消该请求。 默认情况下，超时时间设置为 60 秒。|  
|SMSTSDriverRequestReceiveTimeOut|请求驱动程序目录时，此变量用于指定任务序列等待响应的秒数。 如果连接时间超过超时设定值，任务序列会取消该请求。 默认情况下，超时时间设置为 480 秒。|
|SMSTSDriverRequestResolveTimeOut|请求驱动程序目录时，此变量用于指定任务序列等待 HTTP 名称解析的秒数。 如果连接时间超过超时设定值，任务序列会取消该请求。 默认情况下，超时时间设置为 60 秒。|
|SMSTSDriverRequestSendTimeOut|请求驱动程序目录时，此变量用于指定任务序列等待发送请求的秒数。 如果请求时间超过超时设定值，任务序列会取消该请求。 默认情况下，超时时间设置为 60 秒。|



###  <a name="BKMK_CaptureNetworkSettings"></a>捕获网络设置   
 有关详细信息，请参阅[捕获网络设置](task-sequence-steps.md#BKMK_CaptureNetworkSettings)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (input)|指定是否捕获网络适配器设置（TCP/IP、DNS 和 WINS）的配置信息。<br /><br /> 示例：<br /><br /> true（默认值）<br /><br /> false|  
|OSDMigrateNetworkMembership<br /><br /> (input)|指定是否将工作组或域成员身份信息作为操作系统部署的一部分进行迁移。<br /><br /> 示例：<br /><br /> true（默认值）<br /><br /> false|  



###  <a name="BKMK_CaptureOperatingSystemImage"></a>捕获操作系统映像   
 有关详细信息，请参阅[捕获操作系统映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (input)|指定在网络共享上有权限存储捕获的映像的 Windows 帐户名称。|  
|OSDCaptureAccountPassword<br /><br /> (input)|指定用于将捕获映像存储到网络共享的 Windows 帐户的密码。|  
|OSDCaptureDestination<br /><br /> (input)|指定保存捕获的操作系统映像的位置。 目录名称的最大长度为 255 个字符。|  
|OSDImageCreator<br /><br /> (input)|创建映像的用户的名称（可选）。 此名称存储在 WIM 文件中。 此用户名称的最大长度为 255 个字符。|  
|OSDImageDescription<br /><br /> (input)|捕获的操作系统映像的用户定义的描述（可选）。 此描述存储在 WIM 文件中。 此描述的最大长度为 255 个字符。|  
|OSDImageVersion<br /><br /> (input)|向捕获的操作系统映像分配的用户定义的版本号（可选）。 该版本号存储在 WIM 文件中。 此值可以为字母的任意组合（最大长度为 32 个字符）。|  
|OSDTargetSystemRoot<br /><br /> (input)|指定引用计算机上已安装操作系统的 Windows 目录的路径。 此操作系统由 Configuration Manager 确认为可进行捕获的受支持操作系统。|  



###  <a name="BKMK_CaptureUserState"></a>捕获用户状态   
 有关详细信息，请参阅[捕获用户状态](task-sequence-steps.md#BKMK_CaptureUserState)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|保存用户状态的文件夹的 UNC 或本地路径名称。 无默认值。|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (input)|任务序列用于捕获用户状态的其他用户状态迁移工具 (USMT) 命令行选项。 此步骤在任务序列编辑器中不公开这些设置。 将这些选项指定为一个字符串，任务序列将该字符串追加到自动生成的 USMT 命令行。<br /><br />在运行任务序列之前，使用此任务序列变量指定的 USMT 选项未通过精确度验证。|  
|OSDMigrateMode<br /><br /> (input)|允许自定义 USMT 捕获的文件。 如果此变量设置为“Simple”，则任务序列只会使用标准 USMT 配置文件。 如果此变量设置为“Advanced”，则任务序列变量 OSDMigrateConfigFiles 会指定 USMT 使用的配置文件。<br /><br /> 有效值：<br /><br /> Simple<br /><br /> Advanced|  
|OSDMigrateConfigFiles<br /><br /> (input)|指定用于控制对用户配置文件的捕获的配置文件。 仅当 OSDMigrateMode 设置为“Advanced”时，才使用此变量。 设置此逗号分隔的列表值，以执行自定义的用户配置文件迁移。<br /><br /> 例如：miguser.xml、migsys.xml、migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (input)|如果 USMT 无法捕获某些文件，此变量允许继续进行用户状态捕获。<br /><br /> 有效值：<br /><br /> true（默认值）<br /><br /> false|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|启用 USMT 的详细日志记录。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (input)|指定是否捕获加密文件。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  
|_OSDMigrateUsmtPackageID<br /><br /> (input)|指定包含 USMT 文件的 Configuration Manager 包的包 ID。 此变量是必需的。|  



###  <a name="BKMK_CaptureWindowsSettings"></a>捕获 Windows 设置   
 有关详细信息，请参阅[捕获 Windows 设置](task-sequence-steps.md#BKMK_CaptureWindowsSettings)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (input)|指定是否迁移计算机名称。<br /><br /> 有效值：<br /><br /> true（默认值）<br /><br /> false<br /><br /> 如果值为“true”，则将 OSDComputerName 变量设置为计算机的 NetBIOS 名称。|  
|OSDComputerName<br /><br /> (output)|设置为计算机的 NetBIOS 名称。 仅当 OSDMigrateComputerName 变量设置为“true”时设置该值。|  
|OSDMigrateRegistrationInfo<br /><br /> (input)|指定该步骤是否迁移用户和组织信息。<br /><br /> 有效值：<br /><br /> true（默认值）<br /><br /> false<br /><br /> 如果值为“true”，则将 OSDRegisteredOrgName 变量设置为计算机的注册组织名称。|  
|OSDRegisteredOrgName<br /><br /> (output)|设置为计算机的注册组织名称。 仅当 OSDMigrateRegistrationInfo 变量被设置为“true”时，才设置该值。|  
|OSDMigrateTimeZone<br /><br /> (input)|指定是否迁移计算机名称时区。<br /><br /> 有效值：<br /><br /> true（默认值）<br /><br /> false<br /><br /> 如果值为“true”，则将变量 OSDTimeZone 设置为计算机的时区。|  
|OSDTimeZone<br /><br /> (output)|设置为计算机的时区。 仅当 OSDMigrateTimeZone 变量设置为“true”时，才设置该值。|  



###  <a name="BKMK_ConnecttoNetworkFolder"></a>连接到网络文件夹   
 有关详细信息，请参阅[连接到网络文件夹](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (input)|指定用于连接到网络共享的管理员帐户。|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (input)|指定要连接的网络驱动器号。 此值是可选的；如果不指定此值，网络连接将不映射到某个驱动器号。 如果指定此值，其范围必须为 D: 到 Z:。 此外，不要使用 X:，因为它在 Windows PE 阶段中是 Windows PE 使用的驱动器号。<br /><br /> 示例：<br /><br /> D:<br /><br /> E:|  
|SMSConnectNetworkFolderPassword<br /><br /> (input)|指定用于连接到网络共享的网络密码。|  
|SMSConnectNetworkFolderPath<br /><br /> (input)|指定连接的网络路径。<br /><br /> 例如：<br /><br /> **\\\servername\sharename**|  



###  <a name="BKMK_EnableBitLocker"></a>启用 BitLocker   
 有关详细信息，请参阅[启用 BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (input)|“启用 BitLocker”  任务序列操作使用指定的值作为恢复密码，而不是生成随机恢复密码。 此值必须是有效的数字 BitLocker 恢复密码。|  
|OSDBitLockerStartupKey<br /><br /> (input)|“启用 BitLocker”步骤使用受信任的平台模块 (TPM) 作为启动密钥，而不是为密钥管理选项“仅 USB 上的启动密钥”生成随机启动密钥。 此值必须是一个有效的 256 位 Base-64 编码的 BitLocker 启动密钥。|  



###  <a name="BKMK_FormatPartitionDisk"></a>格式化磁盘并分区   
 有关详细信息，请参阅[格式化磁盘并分区](task-sequence-steps.md#BKMK_FormatandPartitionDisk)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (input)|指定要分区的物理磁盘编号。|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (input)|对硬盘进行分区以便与某些类型的 BIOS 兼容时，使用此变量指定是否禁用缓存对齐优化。 此操作在部署 Windows XP 或 Windows Server 2003 操作系统时非常必要。 有关详细信息，请参阅 Microsoft 知识库中的 [文章 931760](http://go.microsoft.com/fwlink/?LinkId=134081) 和 [文章 931761](http://go.microsoft.com/fwlink/?LinkId=134082) 。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）| 
|OSDGPTBootDisk<br /><br /> (input)|指定是否在 GPT 硬盘上创建 EFI 分区。 基于 EFI 的计算机使用此分区作为启动磁盘。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  
|OSDPartitions<br /><br /> (input)|指定一个分区设置数组；有关在任务序列变量环境中访问数组变量的信息，请参阅 SDK 主题。<br /><br /> 此任务序列变量是一个数组变量。 数组中的每个元素都代表硬盘上单个分区的设置。 通过将数组变量名称与基于零的磁盘分区号及属性名称组合，可以访问为每个分区定义的设置。<br /><br /> 例如，以下变量名称可用于为此步骤在硬盘上创建的第一个分区定义属性：<br /><br /> - **OSDPartitions0Type**：指定分区的类型。 此属性为必需。 有效值为 Primary、Extended、Logical 和 Hidden。<br />-   **OSDPartitions0FileSystem**：指定格式化分区时使用的文件系统类型。 此属性为可选。 如果不指定文件系统，此步骤不会格式化分区。 有效值为 FAT32 和 NTFS。<br />-   **OSDPartitions0Bootable**：指定分区是否可引导。 此属性为必需。 如果 MBR 磁盘的该值设置为“TRUE”，则此步骤将该分区标记为活动分区。<br />-   **OSDPartitions0QuickFormat**：指定使用的格式类型。 此属性为必需。 如果此值设置为“TRUE”，此步骤执行快速格式化。 否则，该步骤执行完全格式化。<br />-   **OSDPartitions0VolumeName**：指定格式化时分配给该卷的名称。 此属性为可选。<br />-   **OSDPartitions0Size**：指定分区的大小。 单位由 **OSDPartitions0SizeUnits** 变量指定。 此属性为可选。 如果未指定此属性，将使用所有剩余可用空间来创建分区。<br />-   **OSDPartitions0SizeUnits**：该步骤使用这些单位来解释 OSDPartitions0Size 变量。 此属性为可选。 有效值为 MB（默认值）、GB 和百分数。<br />-   **OSDPartitions0VolumeLetterVariable**：此步骤创建分区后，分区始终使用 Windows PE 中的下一可用驱动器号。 使用此可选属性指定另一个任务序列变量的名称。 该步骤使用此变量保存新的驱动器号，供将来参考。<br /><br />如果使用此任务序列操作定义多个分区，可使用变量名称中的下标来定义第二个分区的属性。 例如：OSDPartitions1Type、OSDPartitions1FileSystem、OSDPartitions1Bootable、OSDPartitions1QuickFormat 和 OSDPartitions1VolumeName。|  
|OSDPartitionStyle<br /><br /> (input)|指定对磁盘进行分区时使用的分区类型。 “MBR”表示主启动记录分区形式，“GPT”表示 GUID 分区表形式。<br /><br /> 有效值：<br /><br /> GPT<br /><br /> MBR|  



###  <a name="BKMK_InstallApplication"></a>安装应用程序   
 有关详细信息，请参阅[安装应用程序](task-sequence-steps.md#BKMK_InstallApplication)。  

#### <a name="details"></a>详细信息  

|操作变量名称<br /><br /> (input)|说明|  
|----------------------------------------|-----------------|  
| TSErrorOnWarning |指定任务序列引擎是否在此步骤中将检测到的警告视为错误。 由于未满足要求而导致一个或多个应用程序或所需的依赖项未安装时，任务序列会将 _TSAppInstallStatus 变量设置为“Warning”。 将此变量设置为“True”时，如果任务序列将 _TSAppInstallStatus 设置为“Warning”，结果会出错。 值 **False** 是默认行为。| 
|SMSTSMPListRequestTimeoutEnabled|使用此变量启用重复的 MPList 请求，以便在客户端不在 Intranet 上时刷新客户端。 <br />默认情况下，此变量设置为 True。 当客户端位于 Internet 上时，可以将此变量设置为 False 以避免不必要的延迟。 此变量仅适用于安装应用程序和安装软件更新任务序列步骤。|  
|SMSTSMPListRequestTimeout|指定任务序列在利用定位服务检索管理点列表失败后重新尝试安装应用程序之前等待的毫秒数。 默认情况下，任务序列会在等待 60,000 毫秒（60 秒）后重试此步骤，最多重试三次。|  



###  <a name="BKMK_InstallSoftwareUpdates"></a>安装软件更新   
有关详细信息，请参阅[安装软件更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)。  

#### <a name="details"></a>详细信息  

|操作变量名称<br /><br /> (input)|说明|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (input)|指定是否安装所有更新或仅安装必备更新。<br /><br /> 有效值：<br /><br /> **所有**<br /><br /> **强制**|  
|SMSTSSoftwareUpdateScanTimeout| 控制此步骤中软件更新扫描的超时。 例如，如果预计在扫描期间有大量更新，则增加该值。 默认值为 1,800 秒（30 分钟）。 变量值以秒为单位。 |
|SMSTSWaitForSecondReboot|可使用这一可选的任务序列变量在软件更新安装需要两次重启时控制客户端行为。 在此步骤之前设置此变量，以防软件更新安装的第二次重启导致任务序列失败。<br /><br /> 设置 SMSTSWaitForSecondReboot 值（以秒为单位），指定在此步骤中，任务序列在计算机重启时的暂停的秒数。 预留充足的时间，以防还有第二次重启。 <br />例如，如果将 SMSTSWaitForSecondReboot 设置为 600，重启后任务序列将暂停 10 分钟，然后再运行其他步骤。 当单个安装软件更新任务序列步骤中需安装数百个软件更新时，这一变量十分有用。| 
|SMSTSMPListRequestTimeoutEnabled|使用此变量启用重复的 MPList 请求，以便在客户端不在 Intranet 上时刷新客户端。 <br />默认情况下，此变量设置为 True。 当客户端位于 Internet 上时，可以将此变量设置为 False 以避免不必要的延迟。 此变量仅适用于安装应用程序和安装软件更新任务序列步骤。|  
|SMSTSMPListRequestTimeout|指定任务序列在利用定位服务检索管理点列表失败后重新尝试安装软件更新之前等待的毫秒数。 默认情况下，任务序列会在等待 60,000 毫秒（60 秒）后重试此步骤，最多重试三次。|  



###  <a name="BKMK_JoinDomainWorkgroup"></a>加入域或工作组   
 有关详细信息，请参阅[加入域或工作组](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (input)|指定目标计算机加入 Active Directory 域时使用的帐户。 此变量是加入域时必需的变量。|  
|OSDJoinDomainName<br /><br /> (input)|指定目标计算机加入的 Active Directory 域的名称。 域名长度必须介于 1 到 255 个字符之间。|  
|OSDJoinDomainOUName<br /><br /> (input)|指定目标计算机加入的组织单位 (OU) 的 RFC 1779 格式名称。 如果指定了值，该值必须包含完整路径。 OU 名称的长度必须介于 0 到 32,767 个字符之间。 如果 OSDJoinType 变量设置为“1”（加入工作组），则不设置此值。<br /><br /> 例如：<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (input)|指定目标计算机加入 Active Directory 域时使用的网络密码。 如果任务序列环境不包括此变量，Windows 安装程序会尝试使用空密码。 如果变量 OSDJoinType 设置为“0”（加入域），则此值为必需。|  
|OSDJoinSkipReboot<br /><br /> (input)|指定在目标计算机加入域或工作组后是否跳过重新启动。<br /><br /> 有效值：<br /><br /> true<br /><br /> false|  
|OSDJoinType<br /><br /> (input)|指定目标计算机是否加入 Windows 域或工作组。 若要将目标计算机加入到 Windows 域中，请指定为“0”。 若要将目标计算机加入到工作组中，请指定为“1”。<br /><br /> 有效值：<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (input)|指定目标计算机加入的工作组的名称。 工作组的名称长度必须介于 1 到 32 个字符之间。<br /><br /> 例如：<br /><br /> Accounting|  



###  <a name="BKMK_PrepareWindowsCapture"></a>准备 Windows 以便捕获   
 有关详细信息，请参阅[准备 Windows 以便捕获](task-sequence-steps.md#BKMK_PrepareWindowsforCapture)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (input)|指定 Sysprep 是否构建大容量存储设备驱动程序列表。 此设置仅应用于 Windows XP 和 Windows Server 2003。 此变量使用所有大容量存储设备驱动程序上的信息填充 sysprep.inf 的 [SysprepMassStorage] 部分，这些驱动程序受到要捕获的映像的支持。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  
|OSDKeepActivation<br /><br /> (input)|指定 sysprep 是否重置产品激活标志。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  
|OSDTargetSystemRoot<br /><br /> (output)|指定引用计算机上已安装操作系统的 Windows 目录的路径。 此操作系统由 Configuration Manager 确认为可进行捕获的受支持操作系统。|  



###  <a name="BKMK_ReleaseStateStore"></a>发布状态存储   
 有关详细信息，请参阅[发布状态存储](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|从中还原用户状态的位置的 UNC 或本地路径名。 此值由“捕获用户状态”  任务序列操作和“还原用户状态”  任务序列操作这两者使用。|  



###  <a name="BKMK_RequestState"></a>请求状态存储   
  有关详细信息，请参阅[发布状态存储](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (input)|当计算机帐户无法连接到状态迁移点时，此变量指定任务序列步骤是否应回退到使用网络访问帐户 (NAA)。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  
|OSDStateSMPRetryCount<br /><br /> (input)|指定在步骤失败前，任务列表步骤尝试查找状态迁移点的次数。 指定的计数必须介于 0 和 600 之间。|  
|OSDStateSMPRetryTime<br /><br /> (input)|指定任务序列步骤在重新尝试之间等待的秒数。 秒数最多可为 30 个字符。|  
|OSDStateStorePath<br /><br /> (output)|保存或还原用户状态的状态迁移点上的文件夹的 UNC 路径。|  



###  <a name="BKMK_RestartComputer"></a>重新启动计算机   
 有关详细信息，请参阅[重启计算机](task-sequence-steps.md#BKMK_RestartComputer)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (input)|指定重新启动计算机之前要向用户显示的消息。 如果未设置此变量，则显示默认消息文本。 指定的消息不能超过 512 个字符。<br /><br /> 例如：<br /><br /> **在计算机重启之前保存工作。**|  
|SMSRebootTimeout<br /><br /> (input)|指定计算机重新启动之前向用户显示警告的秒数。 指定零秒表示不显示重新启动消息。<br /><br /> 示例：<br /><br /> 0（默认值）<br /><br />  **60**|  



###  <a name="BKMK_RestoreUserState"></a>还原用户状态   
  有关详细信息，请参阅[还原用户状态](task-sequence-steps.md#BKMK_RestoreUserState)。  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|从中还原用户状态的文件夹的 UNC 或本地路径名。|  
|OSDMigrateContinueOnRestore<br /><br /> (input)|继续执行过程，即使 USMT 无法还原某些文件。<br /><br /> 有效值：<br /><br /> true（默认值）<br /><br /> false|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|启用 USMT 工具的详细日志记录。 此值是该操作所必需的。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  
|OSDMigrateLocalAccounts<br /><br /> (input)|指定是否还原本地计算机帐户。<br /><br /> 有效值：<br /><br /> true<br /><br /> false（默认值）|  
|OSDMigrateLocalAccountPassword<br /><br /> (input)|如果 OSDMigrateLocalAccounts 变量为“true”，此变量必须包含分配给所有已迁移的本地帐户的密码。 USMT 将相同的密码分配给所有已迁移的本地帐户。 将此密码视为临时密码，稍后使用其他方法进行更改。|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (input)|指定其他用户状态迁移工具 (USMT) 命令行选项，这些选项将在还原用户状态时使用。 其他选项以附加到自动生成的 USMT 命令行的字符串形式指定。 在运行任务序列之前，使用此任务序列变量指定的 USMT 选项未通过精确度验证。|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (input)|指定包含 USMT 文件的 Configuration Manager 包的包 ID。 此变量是必需的。|  



###  <a name="BKMK_RunCommand"></a>运行命令行   
  有关详细信息，请参阅[运行命令行](task-sequence-steps.md#BKMK_RunCommandLine)  

#### <a name="details"></a>详细信息  

|操作变量名称|说明|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (input)|默认在 64 位操作系统上，任务序列使用 WOW64 文件系统重定向程序在命令行查找并运行程序。 此行为允许使用命令查找 32 位版本的操作系统程序和 DLL。 将此变量设置为 true 可禁用 WOW64 文件系统重定向程序。 此命令查找本机 64 位版本的操作系统程序和 DLL。 在 32 位操作系统上运行时，此变量没有任何作用。|  
|WorkingDirectory<br /><br /> (input)|指定命令行操作的开始目录。 指定的目录名称不能超过 255 个字符。<br /><br /> 示例：<br /><br /> -   **C:\\**<br />-   **%SystemRoot%**|  
|SMSTSRunCommandLineUserName<br /><br /> (input)|指定运行命令行所依据的帐户。 此值为用户名或域\用户名形式的字符串。|  
|SMSTSRunCommandLinePassword<br /><br /> (input)|为 SMSTSRunCommandLineUserName 变量所指定的帐户指定密码。|  



### <a name="set-dynamic-variables"></a>设置动态变量  
有关详细信息，请参阅[设置动态变量](task-sequence-steps.md#BKMK_SetDynamicVariables)  

#### <a name="details"></a>详细信息  

|操作变量名称<br /><br /> (input)|说明|  
|----------------------------------------|-----------------|  
|_SMSTSMake|指定计算机的品牌。|  
|_SMSTSModel|指定计算机的型号。|  
|_SMSTSMacAddresses|指定计算机使用的 MAC 地址。|  
|_SMSTSIPAddresses|指定计算机使用的 IP 地址。|  
|_SMSTSSerialNumber|指定计算机的序列号。|  
|_SMSTSAssetTag|指定计算机的资产标记。|  
|_SMSTSUUID|指定计算机的 UUID。|  
|_SMSTSDefaultGateways|指定计算机使用的默认网关。|  



###  <a name="BKMK_SetupWindows"></a>安装 Windows 和 ConfigMgr   
  有关详细信息，请参阅[安装 Windows 和 ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)。  

#### <a name="details"></a>详细信息  

|操作变量名称<br /><br /> (input)|说明|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (input)|指定在安装 Configuration Manager 客户端时应使用的客户端安装属性。|  



### <a name="upgrade-operating-system"></a>升级操作系统  
 有关详细信息，请参阅[升级操作系统](task-sequence-steps.md#BKMK_UpgradeOS)  

#### <a name="details"></a>详细信息  

|操作变量名称<br /><br /> (input)|说明|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (input)|指定在 Windows 10 升级过程中添加到 Windows 安装程序的其他命令行选项。 任务序列不验证命令行选项。<br /><br /> 有关详细信息，请参阅 [Windows 安装程序命令行选项](/windows-hardware/manufacture/desktop/windows-setup-command-line-options)。|  
