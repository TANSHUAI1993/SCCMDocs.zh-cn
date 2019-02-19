---
title: 客户端安装参数和属性
titleSuffix: Configuration Manager
description: 了解用于安装 Configuration Manager 客户端的 ccmsetup 命令行参数和属性。
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebfcde2be230c9c5e04031210cb6e137ed81668c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126484"
---
# <a name="about-client-installation-parameters-and-properties-in-system-center-configuration-manager"></a>关于 System Center Configuration Manager 中的客户端安装参数和属性。

适用范围：System Center Configuration Manager (Current Branch)

使用 CCMSetup.exe 命令安装 Configuration Manager 客户端。 如果在命令行上提供客户端安装参数，它们则会修改安装行为。 如果在命令行上提供客户端安装属性，它们则会修改已安装客户端代理的初始配置。



##  <a name="aboutCCMSetup"></a> 关于 CCMSetup.exe  
 CCMSetup.exe 命令从管理点或源位置下载所需的文件以安装客户端。 这些文件可能包括：  

-   安装客户端软件的 Windows Installer 包 client.msi。  

-   Microsoft 后台智能传输服务 (BITS) 安装文件。  

-   Windows Installer 安装文件。  

-   Configuration Manager 客户端的更新和修补程序。  

> [!NOTE]  
>  在 Configuration Manager 中，不能直接运行 Client.msi 文件。  

 CCMSetup.exe 提供[命令行参数](#ccmsetup-exe-command-line-parameters)以自定义安装 -- 参数以反斜杠作为前缀，并按照约定采用小写。 在必要时，使用一个冒号紧跟所需的值来指定参数的值。 还可以提供属性以修改 CCMSetup.exe 命令行中的 client.msi 行为 -- 按照约定属性均采用大写。 使用等于号紧跟所需的值来指定参数的值。  

> [!IMPORTANT]  
>  指定 client.msi 的属性之前，先指定 CCMSetup 参数。  

 CCMSetup.exe 及支持文件位于 Configuration Manager 安装文件夹内“Client”文件夹中的站点服务器上。 该文件夹以 **&lt;站点服务器名称\>\SMS_&lt;站点代码 \>\Client** 的形式在网络上共享。  

 在命令提示符处，CCMSetup.exe 命令使用下列格式：  

 `CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

 例如：  

   `CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 此示例将执行以下操作：  

-   指定名为 SMSMP01 的管理点以请求用于下载客户端安装文件的分发点列表。  

-   指定在计算机已有客户端的某个版本时停止安装。  

-   指示 client.msi 将客户端分配到站点代码 S01。  

-   指示 client.msi 使用名为 SMSFP01 的回退状态点。  

> [!NOTE]  
>  如果属性值包含空格，则用引号括起来。  


> [!IMPORTANT]  
>  如果为 Configuration Manager 扩展了 Active Directory 架构，站点则会在 Active Directory 域服务中发布许多客户端安装属性。 Configuration Manager 客户端会自动读取这些属性。 有关详细信息，请参阅 [关于发布到 Active Directory 域服务的客户端安装属性](about-client-installation-properties-published-to-active-directory-domain-services.md)  



##  <a name="ccmsetupexe-command-line-parameters"></a>CCMSetup.exe 命令行参数  

### <a name=""></a>/?  

打开显示 ccmsetup.exe 的命令行参数的“CCMSetup” 对话框。  

示例： **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;路径\>  

 指定文件下载位置。 使用本地路径或 UNC 路径。 使用服务器消息块 (SMB) 协议下载文件。 若要使用 **/source**，用于客户端安装的 Windows 用户帐户对位置必须具有读取权限。

> [!NOTE]  
>  可在命令行上多次使用 /source 参数，以指定备用下载位置。  

 示例：**ccmsetup.exe /source:"\\\computer\folder"**  

### <a name="mpltserver"></a>/mp:&lt;Server\>

 指定计算机要连接到的源管理点。 计算机使用此管理点来查找最近的安装文件分发点。 如果没有分发点或者计算机在 4 个小时后无法从分发点下载文件，则将从指定的管理点下载文件。  

> [!IMPORTANT]  
>  此属性用于指定初始管理点，以供计算机查找下载源，此管理点可以是任何站点中的任何管理点。 它不会向管理点分配客户端。   

 计算机通过 HTTP 或 HTTPS 连接下载文件，具体情况视客户端连接的站点系统角色配置而定。 如果已配置，下载将使用 BITS 限制。 如果所有分发点和管理点都仅针对 HTTPS 客户端连接进行配置，则需验证客户端计算机是否具有有效的客户端证书。  

可使用 /mp 命令行参数来指定多个管理点。 如果计算机无法连接到第一个管理点，则会尝试连接指定列表中的下一个管理点。 在指定多个管理点时，请使用分号分隔各个值。

如果客户端使用 HTTPS 连接到管理点，通常必须指定 FQDN，而不是计算机名。 值必须匹配管理点的 PKI 证书使用者或使用者备用名称。 尽管 Configuration Manager 对于 Intranet 上的连接支持使用证书中的计算机名，但建议使用 FQDN。

使用计算机名称时的示例：`ccmsetup.exe /mp:SMSMP01`  

使用 FQDN 时的示例：`ccmsetup.exe /mp:smsmp01.contoso.com`  

该参数可指定云管理网关的 URL。 使用此 URL 在基于 Internet 的设备上安装客户端。 要获取此参数的值，请按以下步骤操作：
- 创建云管理网关。
- 在活动的客户端上，以管理员身份打开 Windows PowerShell 命令提示符。 
- 运行以下命令：`(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- 附加 “https://” 前缀以与 /mp 参数一起使用。

使用云管理网关 URL 时的示例：`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > 为 /mp 参数指定云管理网关的 URL 时，它必须以 https:// 开头。


### <a name="retryltminutes"></a>/retry:&lt;分钟数\>

CCMSetup.exe 无法下载安装文件时的重试间隔。 在达到 downloadtimeout 参数中指定的限制之前，CCMSetup 将不断重试。  

示例：`ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

默认情况下阻止 CCMSetup 以服务方式运行。 当 CCMSetup 作为服务运行时，它在计算机的本地系统帐户的上下文中运行。 此帐户可能没有足够权限访问安装所需的网络资源。 借助 **/noservice**，CCMSetup.exe 将在你用于启动安装过程的用户帐户的上下文中运行。 此外，如果使用脚本来运行带 /service 参数的 CCMSetup.exe，CCMSetup.exe 将在服务启动后退出，并且可能无法正确报告安装详细信息。   

示例：`ccmsetup.exe /noservice`  

### <a name="service"></a>/service

指定 CCMSetup 应作为使用本地系统帐户的服务运行。  

示例：`ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

指定应卸载的客户端软件。 有关详细信息，请参阅[如何管理客户端](../manage/manage-clients.md)。  

示例：`ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

如果已安装客户端的任何版本，该参数会指定应停止客户端安装。  

示例：`ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 指定如果需要重启才能完成安装，则 CCMSetup 应强制客户端计算机重启。 如果未指定此参数，则在需要重启时，CCMSetup 会退出。 然后在下一次手动重启后继续。  

 示例：`CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;优先级\>

 指定通过 HTTP 连接下载客户端安装文件时的下载优先级。 可能的值如下：  

- FOREGROUND  

- HIGH  

- NORMAL  

- LOW  

  默认值为 NORMAL。  

  示例：`ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;分钟数\>

CCMSetup 放弃下载客户端安装文件之前将尝试下载的时长（以分钟为单位）。 默认值为 1440 分钟（一天）。  

示例：`ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

如果指定，则客户端将使用包括客户端身份验证的 PKI 证书（如果证书可用）。 如果客户端找不到有效证书，则会使用带自签名证书的 HTTP 连接。 不使用此参数时，此行为是相同的。

> [!NOTE]  
>  某些情况下，安装客户端时不必指定此参数，并且仍可使用客户端证书。 这些情况包括使用客户端请求安装客户端以及基于软件更新点的客户端安装。 但是，无论何时手动安装客户端并使用 /mp 参数指定配置为仅接受 HTTPS 客户端连接的管理点时，都必须指定此参数。 安装客户端进行仅限 Internet 的通信时，也必须指定此参数。 将 CCMALWAYSINF=1 属性与基于 Internet 的管理点 (CCMHOSTNAME) 和站点代码 (SMSSITECODE) 的属性一起使用。 若要详细了解基于 Internet 的客户端管理，请参阅[来自 Internet 或不受信任林的客户端通信的注意事项](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

 示例：`CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 指定客户端在使用 PKI 证书通过 HTTPS 进行通信时应不检查证书吊销列表 (CRL)。  

 如果未指定，则客户端将在建立 HTTPS 连接之前检查 CRL。  

 有关客户端 CRL 检查的详细信息，请参阅 [PKI 证书吊销的规划](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)。  

 示例：`CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;配置文件\>

指定列出客户端安装属性的文本文件的名称。

- 如果不指定 /noservice CCMSetup 参数，此文件必须位于 CCMSetup 文件夹，对于 32 位和 64 位操作系统，为 %Windir%\\Ccmsetup。
- 如果指定 /noservice 参数，此文件必须位于你从中运行 CCMSetup.exe 的相同文件夹中。  

示例：`CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

要提供正确的文件格式，请使用站点服务器上 &lt;Configuration Manager 目录\>\\bin\\&lt;平台\> 文件夹中的 mobileclienttemplate.tcf 文件。 此文件也包含有关各个部分及其使用方式的注释。 指定 [Client Install] 部分中的客户端安装属性，其后紧跟下列文本：**Install=INSTALL=ALL**。  

[Client Install] 部分条目示例：`Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;文件名\>

 指定在安装 Configuration Manager 客户端时 CCMSetup.exe 不得安装指定的必备程序。 此参数支持输入多个值。 使用分号字符 (;) 来分隔各个值。  


 示例：`CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe` 或 `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`  

### <a name="forceinstall"></a>/forceinstall

 指定 CCMSetup.exe 卸载任何现有客户端，并安装新客户端。  

### <a name="excludefeaturesltfeature"></a>/ ExcludeFeatures:&lt;功能\>

指定在安装客户端时，CCMSetup.exe 不安装指定的功能。  

示例：`CCMSetup.exe /ExcludeFeatures:ClientUI` 不在客户端上安装软件中心。  

> [!NOTE]  
>  “ClientUI”是 /ExcludeFeatures 参数唯一支持的值。  



##  <a name="ccmsetupReturnCodes"></a> CCMSetup.exe 返回代码  
 CCMSetup.exe 命令完成时提供以下返回代码。 若要进行故障排除，请查看客户端计算机上的 ccmsetup.log 文件，以获取返回代码的上下文以及其他详细信息。  

|返回代码|含义|  
|-----------------|-------------|  
|0|成功|  
|6|错误|  
|7|需要重新启动|  
|8|安装程序已在运行|  
|9|先决条件评估失败|  
|10|安装程序清单哈希验证失败|  



## <a name="ccmsetupMsiProps"></a> Ccmsetup.msi 属性  
 下面的属性可修改 ccmsetup.msi 的安装行为。

### <a name="ccmsetupcmd"></a>CCMSETUPCMD 

指定由 ccmsetup.msi 安装 ccmsetup.exe 之后传递给 ccmsetup.exe 的命令行参数和属性。 将其他属性括在引号内。 当使用 Intune MDM 安装方法启动 Configuration Manager 客户端时使用此属性。 

示例：`ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

 > [!Tip]
 > Microsoft Intune 将该命令行限制为 1024 个字符。 



##  <a name="clientMsiProps"></a> Client.msi 属性  
 下面的属性可修改 client.msi 的安装行为。 如果使用客户端请求安装方法，则也可以在“客户端请求安装属性”  对话框的“客户端”  选项卡中指定这些属性。  


### <a name="aadclientappid"></a>AADCLIENTAPPID

指定 Azure Active Directory (Azure AD) 客户端应用标识符。 在为云管理[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)时，会创建或导入客户端应用。 Azure 管理员可从 Azure 门户获取该属性的值。 有关详细信息，请参阅[获取应用程序 ID](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key)。 对于 AADCLIENTAPPID 属性，此应用程序 ID 用于“本机”类型应用程序。

示例：`ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`


### <a name="aadresourceuri"></a>AADRESOURCEURI

指定 Azure AD 服务器应用标识符。 在为云管理[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)时，会创建或导入服务器应用。 创建服务器应用时，在“创建服务器应用程序”对话框中，该属性为 App ID URI。

Azure 管理员可从 Azure 门户获取该属性的值。 在“Azure Active Directory”边栏选项卡中，找到“应用注册”下的服务器应用。 此应用为“Web 应用/API”应用程序。 打开应用，单击“设置”，然后单击“属性”。 使用此 AADRESOURCEURI 客户端安装属性的 App ID URI 值。

示例：`ccmsetup.exe AADRESOURCEURI=https://contososerver`


### <a name="aadtenantid"></a>AADTENANTID

指定 Azure AD 租户标识符。 为云管理[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)时，此租户会链接到 Configuration Manager。 要获取此属性的值，请按以下步骤操作：
- 在加入同一 Azure AD 租户的 Windows 10 设备上，打开命令提示符。
- 运行以下命令：`dsregcmd.exe /status`
- 在“设备状态”部分中，找到 TenantId 值。 例如 `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

  > [!Note]
  > Azure 管理员还可在 Azure 门户中获取此值。 有关详细信息，请参阅[获取租户 ID](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-tenant-id)

示例：`ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

指定可访问客户端设置和策略的一个或多个 Windows 用户帐户或组。 Configuration Manager 管理员对客户端计算机没有本地管理凭据时，此属性很有用。 指定由分号分隔的帐户列表。  

示例：`CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

指定在客户端安装之后允许重启的计算机（如有必要）。  

> [!IMPORTANT]  
>  即使用户已登录，计算机也会在不发出警告的情况下重启。  

例如：**CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 设置为 1，指定客户端始终以 Internet 为基础并永远不会连接到 Intranet。 客户端的连接类型显示为“始终连接 Internet” 。  

 将此属性与 CCMHOSTNAME 结合使用，指定基于 Internet 的管理点的 FQDN。 也可将其与 CCMSetup 参数 /UsePKICert 以及站点代码结合使用。  

 若要详细了解基于 Internet 的客户端管理，请参阅[来自 Internet 或不受信任林的客户端通信的注意事项](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

 示例：`CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 指定证书颁发者列表，该列表是 Configuration Manager 站点信任的受信任根证书 (CA) 的列表。  

 若要详细了解证书颁发者列表以及客户端如何在证书选择过程中使用该列表，请参阅[规划 PKI 客户端证书选择](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection)。  

 此值是根 CA 证书中主题属性的匹配（区分大小写）。 属性可由逗号 (,) 或分号 (;) 分隔。 使用分隔线指定多个根 CA 证书。 例如：  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  要复制站点的 CertificateIssuers=&lt;string\>，请引用站点服务器上 &lt;Configuration Manager 目录\>\bin\\&lt;平台\> 文件夹中的 mobileclient.tcf 文件。  

### <a name="ccmcertsel"></a>CCMCERTSEL

 如果客户端有多个可用于 HTTPS 通信的证书，则指定证书选择条件。 此证书为包括客户端身份验证功能的有效证书。  

 可以在“使用者名称”或者“使用者可选名称”中搜索完全匹配（使用 **Subject:**），或者搜索部分匹配（使用 **SubjectStr:**）。 示例：  

 `CCMCERTSEL="Subject:computer1.contoso.com"` 搜索在“使用者名称”或者“使用者备用名称”中与计算机名称“computer1.contoso.com”完全匹配的证书。  

 `CCMCERTSEL="SubjectStr:contoso.com"` 搜索在“使用者名称”或者“使用者备用名称”中包含“contoso.com”的证书。  

 您还可以在“使用者名称”或者“使用者备用名称”属性中使用对象标识符 (OID) 或可分辨名称属性，例如：  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` 搜索以对象标识符表示且名为 Computers 的组织单位属性。  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` 搜索以可分辨名称表示且名为 Computers 的组织单位属性。  

> [!IMPORTANT]
>  如果使用“使用者名称框”，则 **Subject:** 区分大小写，而 **SubjectStr:** 不区分大小写。  
> 
>  如果使用“使用者备用名称”框，<strong>Subject:</strong> 和 **SubjectStr:** 均不区分大小写。  

 可用于证书选择的完整属性列表在[对于 PKI 证书选择条件支持的属性值](#BKMK_attributevalues)中列出。  

 如果多个证书与搜索相符，并且属性 CCMFIRSTCERT 已设置为 1，则选择有效期最长的证书。  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 如果用于 HTTPS 的客户端证书不在计算机存储的默认“个人”证书存储中，则指定备用证书存储名称。  

 示例：`CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  启用调试日志记录。 可将该值设置为 0（关 - 默认）或 1（开）。 此属性将使客户端记录有助于故障排除的低级信息。 最好避免在生产站点使用此属性， 因为这会产生过多日志记录，可能导致难以在日志文件中查找相关信息。 请将 CCMENABLELOGGING 也设置为 TRUE，以启用调试日志记录。  

  示例：`CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  默认情况下，此属性设置为 TRUE 来启用日志记录。 日志文件存储在 Configuration Manager 客户端安装文件夹的**日志**文件夹中。 默认情况下，此文件夹为 %Windir%\CCM\Logs。  

  示例：`CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 客户端运行状况评估工具 (ccmeval.exe) 运行时的频率。 可以是 **1** 到 **1440** 分钟。 默认情况下，每天运行一次。  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 客户端运行状况评估工具 (ccmeval.exe) 运行时的小时，在 **0** 点（午夜）和 **23** 点（晚上 11 点）之间。 默认情况下在午夜运行。  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 如果设置为 1，则此属性指定客户端应选择有效期最长的 PKI 证书。 如果将网络访问保护与 IPsec 强制配合使用，则可能需要此设置。  

 示例：`CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  


### <a name="ccmhostname"></a>CCMHOSTNAME

 如果客户端是通过 Internet 进行管理，则此属性指定基于 Internet 的管理点的 FQDN。  

 不要使用 SMSSITECODE=AUTO 的安装属性指定此选项。 基于 Internet 的客户端必须直接分配到其基于 Internet 的站点。  

 示例：`CCMSetup.exe  /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

该属性可指定云管理网关的地址。 要获取此属性的值，请按以下步骤操作：
- 创建云管理网关。
- 在活动的客户端上，以管理员身份打开 Windows PowerShell 命令提示符。 
- 运行以下命令：`(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- 将返回值按原样与 CCMHOSTNAME 属性一起使用。

例如：`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > 为 CCMHOSTNAME 属性指定云管理网关的地址时，不要附加 https:// 等前缀。 此前缀仅用于云管理网关的 /mp URL。



### <a name="ccmhttpport"></a>CCMHTTPPORT

 指定客户端在通过 HTTP 与站点系统服务器通信时应该使用的端口。 默认情况下设置为端口 80。  

 示例：`CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

指定客户端在通过 HTTPS 与站点系统服务器通信时应该使用的端口。 默认情况下设置为端口 443。  

示例：`CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 确定在其中安装 Configuration Manager 客户端文件的文件夹，默认为 *%Windir%* \CCM。 无论这些文件安装在哪个文件夹中，Ccmcore.dll 文件都始终安装在 *%Windir%\System32* 文件夹中。 此外，在 64 位操作系统上，Ccmcore.dll 文件的副本始终安装在 %Windir%\SysWOW64 folder 文件夹中。 此文件支持使用来自 Configuration Manager SDK 的 32 位版本的客户端 API 的 32 位应用程序。  

 示例：`CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

指定要写入 Configuration Manager 日志文件的详细级别。 指定 0 到 3 之间的一个整数，其中 0 表示最详细的日志记录，3 表示只记录错误。 默认值为 1。  

示例：`CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Configuration Manager 日志文件的大小达到上限时，客户端会将其重命名为备份，并创建新的日志文件。 默认情况下，最大大小为 250000 字节，或为 CCMLOGMAXSIZE 属性指定的值。

此属性指定保留先前版本的日志文件个数。 默认值为 1。 如果值设置为 0，则不保留任何旧的日志文件。  

示例：`CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

日志文件的最大大小（以字节为单位）。 当日志增长到指定大小时，客户端会将其重命名为历史文件，并创建一个新文件。 此属性至少必须设置为 10000 字节。 默认值为 250000 字节。  

示例：`CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 如果设置为 TRUE，则此属性会禁止管理用户更改 Configuration Manager 控制面板中分配的站点。  

 例如：**CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

如果设置为 TRUE，则此属性会禁止管理用户更改 Configuration Manager 控制面板中的客户端缓存文件夹设置。  

示例：`CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 为客户端指定 DNS 域以查找在 DNS 中发布的管理点。 找到管理点后，该管理点将告知客户端有关层次结构中其他管理点的信息。 此行为意味着使用 DNS 发布找到的管理点不必来自客户端站点，但可以是层次结构中的任何管理点。  

> [!NOTE]  
>  如果客户端与发布的管理点位于同一域中，则不必指定此属性。 在此情况下，会自动使用客户端的域来搜索 DNS 以查找管理点。  

 有关 DNS 发布作为 Configuration Manager 客户端的服务定位方法的详细信息，请参阅[服务定位和客户端如何确定向其分配的管理点](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)。  

> [!NOTE]  
>  默认情况下，Configuration Manager 中不启用 DNS 发布。  

 示例：`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

指定接收和处理 Configuration Manager 客户端计算机发送的状况消息的回退状态点。  

有关回退状态点的详细信息，请参阅[确定是否需要回退状态点](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point)。  

示例：`CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 指定在安装客户端之前不检查是否存在 Microsoft Application Virtualization (App-V) 的最低所需版本。  

> [!IMPORTANT]  
>  如果在未安装 App-V 的情况下安装 Configuration Manager 客户端，则无法部署虚拟应用程序。  

 示例：`CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

指定客户端报告状态，但不修复发现的问题。  

示例：`CCMSetup.exe NOTIFYONLY=TRUE`  

有关详细信息，请参阅[如何配置客户端状态](configure-client-status.md)。  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 如果客户端具有错误的 Configuration Manager 受信任的根密钥，且无法与受信任的管理点联系来接收受信任的新根密钥，请使用此属性手动删除旧的受信任的根密钥。 此情况可能在将客户端从一个站点层次结构移至另一个站点层次结构时发生。 此属性适用于使用 HTTP 和 HTTPS 客户端通信的客户端。  

 示例：`CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

与 [SMSSITECODE](#smssitecode)=AUTO 一起使用时，启用自动站点重新分配进行客户端升级。

示例：`CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

指定客户端计算机上用于存储临时文件的客户端缓存文件夹的位置。 默认情况下，此位置为 %Windir%\ccmcache。  

示例：`CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

此属性可以与 SMSCACHEFLAGS 属性结合使用，以控制客户端缓存文件夹位置。  

示例：`CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` 将客户端缓存文件夹安装在最大的可用客户端磁盘驱动器上。  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

指定客户端缓存文件夹的进一步安装详细信息。 可以单独或组合使用 SMSCACHEFLAGS 属性，组合使用时须以分号隔开。 如果未指定此属性，则将依据 SMSCACHEDIR 属性安装客户端缓存文件夹，该文件夹将不会压缩，且 SMSCACHESIZE 值会作为文件夹的大小（以 MB 为单位）。  

升级现有的客户端时忽略此设置。  

属性:  

-   PERCENTDISKSPACE：以总磁盘空间的百分比的形式指定文件夹大小。 如果指定此属性，则还必须以要使用的百分比值指定属性 SMSCACHESIZE。  

-   PERCENTFREEDISKSPACE：以可用磁盘空间的百分比指定文件夹大小。 如果指定此属性，则还必须以要使用的百分比值指定属性 SMSCACHESIZE。 例如，如果磁盘具有 10 MB 的可用空间且 SMSCACHESIZE 指定为 50，则文件夹大小将设置为 5 MB。 您不能将此属性与 PERCENTDISKSPACE 属性结合使用。  

-   MAXDRIVE：指定文件夹应该安装在最大的可用磁盘上。 如果已使用 SMSCACHEDIR 属性指定路径，则会忽略此值。  

-   MAXDRIVESPACE：指定文件夹应该安装在具有最多可用空间的磁盘驱动器上。 如果已使用 SMSCACHEDIR 属性指定路径，则会忽略此值。  

-   NTFSONLY：指定文件夹只能在 NTFS 磁盘驱动器上安装。 如果已使用 SMSCACHEDIR 属性指定路径，则会忽略此值。  

-   COMPRESS：指定文件夹应该以压缩方式存储。  

-   FAILIFNOSPACE：指定如果没有足够的空间来安装文件夹，则应删除客户端软件。  

示例：`CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> 客户端设置可用于指定客户端缓存文件夹的大小。 添加这些客户端设置有效地替代了使用 SMSCACHESIZE 作为 client.msi 属性指定客户端缓存的大小。 有关详细信息，请参阅[有关缓存大小的客户端设置](about-client-settings.md#client-cache-settings)。  

<!-- For 1602 and earlier, SMSCACHESIZE specifies the size of the client cache folder in megabyte (MB) or as a percentage when used with the PERCENTDISKSPACE or PERCENTFREEDISKSPACE property. If this property isn't set, the folder defaults to a maximum size of 5120 MB. The lowest value that you can specify is 1 MB.  -->

> [!NOTE]  
>  如果必须下载的新包会使文件夹超出其最大大小，并且无法通过清除文件夹来提供足够的可用空间，则无法下载此包，同时该程序或应用程序也无法运行。  

升级现有客户端和客户端下载软件更新时会忽略此设置。  

示例：`CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  如果重新安装客户端，则无法使用 SMSCACHESIZE 或 SMSCACHEFLAGS 安装属性将缓存大小设置为小于以前的值。 如果尝试执行此操作，则你的值会被忽略。 缓存大小会自动设置为以前的大小。  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

指定 Configuration Manager 安装程序检查配置设置的位置和顺序。 此属性是一个含一个或多个字符的字符串，其中每个字符都定义了一个特定的配置源。 单独或组合使用字符值 R、P、M 和 U：  

- R：检查注册表中的配置设置。  

  有关详细信息，请参阅[有关在注册表中存储客户端安装属性的信息](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision)。  

- P：检查在命令提示符处提供的安装属性中的配置设置。  

- M：检查用 Configuration Manager 客户端软件升级旧版客户端时的现有设置。  

- U：将安装的客户端升级为较新版本（并使用分配的站点代码）。  

  默认情况下，客户端安装使用 `PU` 先检查安装属性，然后再检查现有设置。  

  示例：`CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 指定客户端是否能使用 Windows Internet 名称服务 (WINS) 来查找接受 HTTP 连接的管理点。 如果客户端无法在 Active Directory 域服务或 DNS 中查找管理点，则会使用此方法。  

 此属性对客户端是否将 WINS 用于名称解析没有影响。  

 可以为此属性配置两种不同的模式：  

-   NOWINS：此值是此属性最安全的设置，可防止客户端查找 WINS 中的管理点。 如果你使用此设置，客户端必须有备用方法来查找 Intranet 上的管理点，例如 Active Directory 域服务或通过使用 DNS 发布。  

-   WINSSECURE（默认）：在此模式中，使用 HTTP 通信的客户端可使用 WINS 来查找管理点。 但是，该客户端必须具有受信任的根密钥的副本，然后才能成功地连接到管理点。 有关详细信息，请参阅[规划受信任的根密钥](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  


 示例：`CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

指定供 Configuration Manager 客户端使用的初始管理点。  

> [!IMPORTANT]  
>  如果管理点仅接受通过 HTTPS 进行的客户端连接，则必须为管理点名称加上前缀 https://。  

示例：`CCMSetup.exe SMSMP=smsmp01.contoso.com`

示例：`CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  


### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 在无法从 Active Directory 域服务中检索 Configuration Manager 信任的根密钥时，请指定此根密钥。 此属性适用于使用 HTTP 和 HTTPS 客户端通信的客户端。 有关详细信息，请参阅[规划受信任的根密钥](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

 示例：`CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 用于重新安装 Configuration Manager 信任的根密钥。 为包含受信任的根密钥的文件指定完整路径和文件名。 此属性适用于使用 HTTP 和 HTTPS 客户端通信的客户端。 有关详细信息，请参阅[规划受信任的根密钥](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

 例如：CCMSetup.exe SMSROOTKEYPATH=&lt;完整路径和文件名\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 在站点服务器上指定导出的自签名证书的完整路径和 .cer 文件名。  

 此证书存储在“SMS”  证书存储中，并且具有“站点服务器”  使用者名称以及“站点服务器签名证书” 友好名称。  

 例如：**CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;完整路径和文件名\>**  

### <a name="smssitecode"></a>SMSSITECODE

 指定要将客户端分配到的 Configuration Manager 站点。 此值可以是三个字符的站点代码，也可以是单词 AUTO。 如果指定了 AUTO 或者未指定此属性，则客户端会尝试从 Active Directory 域服务或指定的管理点确定其站点分配。 若要启用 AUTO 进行客户端升级，还必须将 [SITEREASSIGN](#sitereassign) 设置为 TRUE。    

> [!NOTE]  
>  如果还要指定基于 Internet 的管理点 (CCMHOSTNAME)，请不要使用 AUTO。 在这种情况下，必须将客户端直接分配到其站点。  

 示例：`CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> 对于 PKI 证书选择条件支持的属性值  
 对于 PKI 证书选择条件，Configuration Manager 支持 下列属性值：  

|OID 属性|可分辨名称属性|属性定义|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|域组件|  
|1.2.840.113549.1.9.1|E 或 E-mail|电子邮件地址|  
|2.5.4.3|CN|公用名|  
|2.5.4.4|SN|使用者名称|  
|2.5.4.5|SERIALNUMBER|序列号|  
|2.5.4.6|C|国家/地区代码|  
|2.5.4.7|L|区域|  
|2.5.4.8|S 或 ST|省或自治区名称|  
|2.5.4.9|STREET|街道地址|  
|2.5.4.10|O|组织名称|  
|2.5.4.11|OU|组织单位|  
|2.5.4.12|T 或 Title|标题|  
|2.5.4.42|G 或 GN 或 GivenName|给定名称|  
|2.5.4.43|I 或 Initials|缩写|  
|2.5.29.17|（没有值）|使用者可选名称|  
