---
title: "Configuration Manager 使用的帐户 | Microsoft Docs"
description: "在 System Center Configuration Manager 中标识和管理 Windows 组和帐户。"
ms.custom: na
ms.date: 2/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a776667cc9f24bd4a468afea76e466c34ce66864
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="accounts-used-in-system-center-configuration-manager"></a>System Center Configuration Manager 中使用的帐户

*适用范围：System Center Configuration Manager (Current Branch)*

可以使用以下信息确定 System Center Configuration Manager 中使用的 Windows 组和帐户、它们的使用方式以及任何要求。  

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a>Configuration Manager 创建和使用的 Windows 组  
 Configuration Manager 会自动创建并在许多情况下自动维护以下 Windows 组。  

> [!NOTE]  
>  当 Configuration Manager 在作为域成员的计算机上创建组时，该组为本地安全组。 如果计算机是域控制器，则该组是在域中的所有域控制器之间共享的域本地组。  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess  
Configuration Manager 使用此组来授予查看软件清单所收集的文件的访问权限。  

下表列出了此组的其他详细信息：  

|详情|更多信息|  
|------------|----------------------|  
|类型和位置|此组是在主站点服务器上创建的本地安全组。<br /><br /> 卸载站点时，不会自动删除此组。 必须手动将其删除。|  
|Membership|Configuration Manager 自动管理组成员身份。 成员身份管理用户，这些管理用户被授予对分配的安全角色中“集合”  安全对象的“查看收集的文件”  权限。|  
|权限|默认情况下，此组对站点服务器上的以下文件夹具有 **Read** 权限： **%path%\Microsoft Configuration Manager\sinv.box\FileCol**。|  

### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  
 此组是由 Configuration Manager 在站点数据库服务器或数据库副本服务器上创建的本地安全组。 当前不使用该组，但将其保留以供将来使用。  

### <a name="configmgr-remote-control-users"></a>ConfigMgr 远程控制用户  
 Configuration Manager 远程工具使用此组将设置的帐户和组存储在分配到每个客户端的“允许的查看者”列表中。  

 下表列出了此组的其他详细信息：  

|详情|更多信息|  
|------------|----------------------|  
|类型和位置|此组是在客户端接收启用远程工具的策略时在 Configuration Manager 客户端上创建的本地安全组。<br /><br /> 为客户端禁用远程工具后，不会自动删除此组。 必须从每个客户端计算机中手动将其删除。|  
|Membership|默认情况下，此组中没有成员。 当你将用户添加到“允许的查看者”列表时，会将这些用户自动添加到此组中。<br /><br /> 可以使用“允许的查看者”列表来管理此组的成员身份，而不是将用户或组直接添加到此组。<br /><br /> 除了作为允许的查看者外，管理用户还必须具有“集合”对象的“远程控制”权限。 你可以通过使用“远程工具操作人员”安全角色来分配此权限。|  
|权限|默认情况下，此组无权访问计算机上的任何位置。 它仅用于保留“允许的查看者”列表。|  

### <a name="sms-admins"></a>SMS 管理员  
 Configuration Manager 通过 Windows Management Instrumentation (WMI) 使用此组授予对 SMS 提供程序的访问权限。 需要 SMS 提供程序的访问权限才能在 Configuration Manager 控制台中查看和更改对象。  

> [!NOTE]  
>  管理用户的基于角色的管理配置确定他们在使用 Configuration Manager 控制台时可查看和管理哪些对象。  

 下表列出了此组的其他详细信息：  

|详情|更多信息|  
|------------|----------------------|  
|类型和位置|此组是在具有 SMS 提供程序的每台计算机上创建的本地安全组。<br /><br /> 卸载站点时，不会自动删除此组。 必须手动将其删除。|  
|Membership|Configuration Manager 自动管理组成员身份。 默认情况下，层次结构中的每个管理用户以及站点服务器计算机帐户是站点中每台 SMS 提供程序计算机上的“SMS 管理员”组的成员。|  
|权限|在 WMI 控制 MMC 管理单元中设置 SMS 管理员权限。 默认情况下，授予 SMS 管理员组对 Root\SMS 命名空间的 **Enable Account** 和 **Remote Enable** 权限。 经过身份验证的用户具有**执行方法**、**提供程序写入**和**启用帐户**权限。<br /><br /> 使用远程 Configuration Manager 控制台的管理员用户均需要同时对站点服务器计算机和 SMS 提供程序计算机拥有“远程激活 DCOM”权限。 最佳方案是将这些权限授予“SMS 管理员”以简化管理，而不是将这些权限直接授予用户或组。 有关详细信息，请参阅 [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) 主题中的 [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) 部分。|  

### <a name="smssitesystemtositeserverconnectionmpltsitecode"></a>SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>  
 远离站点服务器的 Configuration Manager 管理点使用此组来连接到站点数据库。 此组向管理点提供对站点服务器上的收件箱文件夹和站点数据库的访问权限。  

 下表列出了此组的其他详细信息：  

|详情|更多信息|  
|------------|----------------------|  
|类型和位置|此组是在具有 SMS 提供程序的每台计算机上创建的本地安全组。<br /><br /> 卸载站点时，不会自动删除此组。 必须手动将其删除。|  
|Membership|Configuration Manager 自动管理组成员身份。 默认情况下，成员身份包括具有站点管理点的远程计算机的计算机帐户。|  
|权限|默认情况下，此组对站点服务器上的 **%path%\Microsoft Configuration Manager\inboxes** 文件夹具有“读取”、“读取和执行”和“列出文件夹内容”权限。 此组对管理点向其中写入客户端数据的 **Write** 下的子文件夹具有额外的 **inboxes** 权限。|  

### <a name="smssitesystemtositeserverconnectionsmsprovltsitecode"></a>SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>  
 远离站点服务器的 Configuration Manager SMS 提供程序计算机使用此组来连接到站点服务器。  

 下表列出了此组的其他详细信息：  

|详情|更多信息|  
|------------|----------------------|  
|类型和位置|此组是在站点服务器上创建的本地安全组。<br /><br /> 卸载站点时，不会自动删除此组。 必须手动将其删除。|  
|Membership|Configuration Manager 自动管理组成员身份。 默认情况下，成员身份包括用于从为站点安装了 SMS 提供程序的每台远程计算机连接到站点服务器的计算机帐户或域用户帐户。|  
|权限|默认情况下，此组对站点服务器上的 **%path%\Microsoft Configuration Manager\inboxes** 文件夹具有“读取”、“读取和执行”和“列出文件夹内容”权限。 对 **inboxes** 下 SMS 提供程序需要访问的子文件夹来说，此组具有额外权限 **Write** 或者“写入”和“修改”权限。<br /><br /> 此组还对 **%path%\Microsoft Configuration Manager\OSD\boot** 下的文件夹具有“读取”、“读取和执行”、“列出文件夹内容”、“写入”和“修改”权限，并对站点服务器上 **%path%\Microsoft Configuration Manager\OSD\Bin** 下的文件夹具有“读取”权限。|  

### <a name="smssitesystemtositeserverconnectionstatltsitecode"></a>SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>  
 Configuration Manager 远程站点系统计算机上的文件分派管理器使用此组来连接到站点服务器。  

 下表列出了此组的其他详细信息：  

|详情|更多信息|  
|------------|----------------------|  
|类型和位置|此组是在站点服务器上创建的本地安全组。<br /><br /> 卸载站点时，不会自动删除此组。 必须手动将其删除。|  
|Membership|Configuration Manager 自动管理组成员身份。 默认情况下，成员身份包括用于从运行文件分派管理器的每台远程站点系统计算机连接到站点服务器的计算机帐户或域用户帐户。|  
|权限|默认情况下，此组对站点服务器上的 **%path%\Microsoft Configuration Manager\inboxes** 文件夹和该位置下的子文件夹具有“读取”、“读取和执行”和“列出文件夹内容”权限。 此组具有对站点服务器上 **%path%\Microsoft Configuration Manager\inboxes\statmgr.box** 文件夹的额外权限（“写入”和“修改”）。|  

### <a name="smssitetositeconnectionltsitecode"></a>SMS_SiteToSiteConnection_&lt;sitecode\>  
 Configuration Manager 使用此组在层次结构中的站点之间实现基于文件的复制。 对于将文件直接传输到此站点的每个远程站点，此组包含设为“文件复制帐户”的帐户。  

 下表列出了此组的其他详细信息：  

|详情|更多信息|  
|------------|----------------------|  
|类型和位置|此组是在站点服务器上创建的本地安全组。|  
|Membership|安装新站点作为另一个站点的子站点时，Configuration Manager 会自动将新站点的计算机帐户添加到父站点服务器上的组。 Configuration Manager 还会将父站点计算机帐户添加到新站点服务器上的组中。 如果为基于文件的传输指定另一个帐户，请将此帐户添加到目标站点服务器上的此组。<br /><br /> 卸载站点时，不会自动删除此组。 必须手动将其删除。|  
|权限|默认情况下，此组具有对 **%path%\Microsoft Configuration Manager\inboxes\despoolr.box\receive** 文件夹的“完全控制”  权限。|  

## <a name="accounts-that-configuration-manager-uses"></a>Configuration Manager 使用的帐户  
 可以为 Configuration Manager 设置下列帐户。  

### <a name="active-directory-group-discovery-account"></a>Active Directory 组发现帐户  
 **Active Directory 组发现帐户**用于发现本地、全局和通用安全组、这些组内的成员身份，以及 Active directory 域服务中指定位置的通讯组内的成员身份。 不会以组资源的形式发现通讯组。  

 此帐户可以是运行发现的站点服务器的计算机帐户，或者是 Windows 用户帐户。 它必须对为发现指定的 Active Directory 位置具有“读取”  访问权限。  

### <a name="active-directory-system-discovery-account"></a>Active Directory 系统发现帐户  
 **Active Directory 系统发现帐户** 用于从 Active Directory 域服务中的指定位置发现计算机。  

 此帐户可以是运行发现的站点服务器的计算机帐户，或者是 Windows 用户帐户。 它必须对为发现指定的 Active Directory 位置具有“读取”  访问权限。  

### <a name="active-directory-user-discovery-account"></a>Active Directory 用户发现帐户  
 **Active Directory 用户发现帐户** 用于从 Active Directory 域服务中的指定位置发现用户帐户。  

 此帐户可以是运行发现的站点服务器的计算机帐户，或者是 Windows 用户帐户。 它必须对为发现指定的 Active Directory 位置具有“读取”  访问权限。  

### <a name="active-directory-forest-account"></a>Active Directory 林帐户  
 **Active Directory 林帐户**用于发现 Active Directory 林中的网络基础结构。 管理中心站点和主站点也用它来将站点数据发布到林的 Active Directory 域服务。  

> [!NOTE]  
>  辅助站点始终使用辅助站点服务器计算机帐户来发布到 Active Directory。  

> [!NOTE]  
>  Active Directory 林帐户必须是全局帐户才能发现和发布到不受信任林。 如果不使用站点服务器的计算机帐户，则只能选择全局帐户。  

 此帐户必须对要在其中发现网络基础结构的每个 Active Directory 林具有“读取”  权限。  

 此帐户必须对要在其中发布站点数据的每个 Active Directory 林中的“系统管理”容器及其所有子对象具有“完全控制”  权限。  

### <a name="asset-intelligence-synchronization-point-proxy-server-account"></a>资产智能同步点代理服务器帐户  
 资产智能同步点使用**资产智能同步点代理服务器帐户**通过需要对访问进行身份验证的代理服务器或防火墙访问 Internet。  

> [!IMPORTANT]  
>  为所需的代理服务器或防火墙指定具有可能最低的权限的帐户。  

### <a name="certificate-registration-point-account"></a>证书注册点帐户  
 **证书注册点帐户**将证书注册点连接到 Configuration Manager 数据库。 默认情况下，会使用证书注册点服务器的计算机帐户，但是可以改为设置用户帐户。 每当证书注册点在站点服务器的不受信任的域中时，都必须指定用户帐户。 此帐户只需要站点数据库的“读取”权限，因为写入任务由状态消息系统处理。  

### <a name="capture-operating-system-image-account"></a>捕获操作系统映像包帐户  
 Configuration Manager 使用**捕获操作系统映像帐户**来访问在部署操作系统时用于存储捕获映像的文件夹。 如果将“捕获操作系统映像包”  步骤添加到任务序列中，则需要此帐户。  

 此帐户对存储捕获映像的网络共享必须具有“读取”  和“写入”  权限。  

 如果在 Windows 中更改帐户的密码，则必须使用新密码更新任务序列。 Configuration Manager 客户端在下次下载客户端策略时将接收新密码。  

 如果使用此帐户，则可以创建一个具有访问所需网络资源的最低权限的域用户帐户，并将其用于所有任务序列帐户。  

> [!IMPORTANT]  
>  请勿向此帐户分配交互式登录权限。  
>   
>  请勿将网络访问帐户用于此帐户。  

### <a name="client-push-installation-account"></a>客户端请求安装帐户  
 如果使用客户端请求安装来部署客户端，则可以使用**客户端请求安装帐户**连接到计算机并安装 Configuration Manager 客户端软件。 如果未指定此帐户，则站点服务器帐户用于尝试安装客户端软件。  

 在要安装 Configuration Manager 客户端软件的计算机上，此帐户必须为本地“管理员”组的成员。 此帐户不需要**域管理员**权限。  

 可以指定一个或多个客户端请求安装帐户，而 Configuration Manager 会尝试这些帐户直到成功为止。  

> [!TIP]  
>  要更有效地在大型 Active Directory 部署中协调帐户更新，请使用不同的名称创建一个新帐户，然后将新帐户添加到 Configuration Manager 内客户端请求安装帐户的列表中。 请留出足够的时间让 Active Directory 域服务复制新帐户，然后从 Configuration Manager 和 Active Directory 域服务中删除旧帐户。  

> [!IMPORTANT]  
>  不要向此帐户授予本地登录的权限。  

### <a name="enrollment-point-connection-account"></a>注册点连接帐户  
 **注册点连接帐户**将注册点连接到 Configuration Manager 站点数据库。 默认情况下，会使用注册点的计算机帐户，但是可以改为设置用户帐户。 每当注册点在站点服务器的不受信任的域中时，都必须指定用户帐户。 此帐户需要站点数据库的“读取”和“写入”权限。  

### <a name="exchange-server-connection-account"></a>Exchange Server 连接帐户  
 **Exchange Server 连接帐户** 将站点服务器连接到指定的 Exchange Server 计算机以查找和管理连接到 Exchange Server 的移动设备。 此帐户需要 Exchange PowerShell cmdlet 以提供对 Exchange Server 计算机的所需权限。 有关 cmdlet 的详细信息，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

### <a name="exchange-server-connector-proxy-server-account"></a>Exchange Server 连接器代理服务器帐户  
 Exchange Server 连接器使用 **Exchange Server 连接器代理服务器帐户**通过需要对访问进行身份验证的代理服务器或防火墙访问 Internet。  

> [!IMPORTANT]  
>  为所需的代理服务器或防火墙指定具有可能最低的权限的帐户。  

### <a name="management-point-connection-account"></a>管理点连接帐户  
 **管理点连接帐户**用于将管理点连接到 Configuration Manager 站点数据库，以便它可以发送和检索客户端的信息。 默认情况下，会使用管理点的计算机帐户，但是可以改为设置用户帐户。 每当管理点在站点服务器的不受信任的域中时，都必须指定用户帐户。  

 在运行 Microsoft SQL Server 的计算机上将此帐户创建为低权限本地帐户。  

> [!IMPORTANT]  
>  不要向此帐户授予交互式登录的权限。  

### <a name="multicast-connection-account"></a>多播连接帐户  
 为多播设置的分发点使用**多播连接帐户**从站点数据库中读取信息。 默认情况下，会使用分发点的计算机帐户，但是可以改为设置用户帐户。 每当站点数据库在不受信任的林中时，都必须指定用户帐户。 例如，数据中心具有非站点服务器和站点数据库的林中的外围网络，则可以使用此帐户从站点数据库中读取多播信息。  

 如果创建此帐户，请在运行 Microsoft SQL Server 的计算机上将此帐户创建为低权限本地帐户。  

> [!IMPORTANT]  
>  不要向此帐户授予交互式登录的权限。  

### <a name="network-access-account"></a>网络访问帐户  
 客户端计算机无法使用其本地计算机帐户访问分发点上的内容时，它们则会使用**网络访问帐户**。 例如，这适用于来自不受信任的域中的工作组客户端和计算机。 当安装操作系统的计算机在域上还没有计算机帐户时，也可能会在操作系统部署过程中使用此帐户。  

> [!NOTE]  
>  决不会将网络访问帐户用作安全性上下文来运行程序、安装软件更新或运行任务序列。 它仅用于访问网络上的资源。  

 授予此帐户对内容的最低合适权限，客户端需要此权限来访问软件。 在具有包内容的分发点或其他服务器上，帐户必须具有“从网络访问此计算机”  权限。 每个站点最多可以配置 10 个网络访问帐户。  

> [!WARNING]  
>  当 Configuration Manager 尝试使用计算机名$ 帐户下载内容并失败时，它会自动重试网络访问帐户，即使以前尝试并失败过。  

 在任何域中创建将提供资源的所需访问权限的帐户。 网络访问帐户必须始终包含一个域名。 此帐户不支持传递安全性。 如果在多个域中具有分发点，请在受信任的域中创建帐户。  

> [!TIP]  
>  为了避免帐户锁定，请不要对现有网络访问帐户更改密码。 而是在 Configuration Manager 中创建新帐户并设置此新帐户。 在经过足够的时间让所有客户端接收新帐户详细信息之后，请从网络共享文件夹中移除旧帐户并删除该帐户。  

> [!IMPORTANT]  
>  不要向此帐户授予交互式登录的权限。
>   
>  不要授予此帐户将计算机加入到域的权限。 如果在任务序列过程中必须将计算机加入到域中，请使用任务序列编辑器域加入帐户。  

### <a name="package-access-account"></a>包访问帐户  
 利用**包访问帐户**，可以设置 NTFS 权限，该权限用于指定可以访问分发点上的包文件夹的用户和用户组。 默认情况下，Configuration Manager 仅向通用访问帐户“用户”和“管理员”授予访问权限。 可以通过使用其他的 Windows 帐户或组来控制客户端计算机的访问权限。 移动设备始终会匿名检索包内容，所以这些设备不使用包访问帐户。  

 默认情况下，当 Configuration Manager 在分发点上创建包共享时，它会授予对本地“用户”组的“读取”权限以及对本地“管理”组的“完全控制”权限。 所需的实际权限取决于包。 如果你的客户端在工作组或不受信任的林中，则那些客户端会使用网络访问帐户访问包内容。 请使用定义的包访问帐户来确保网络访问帐户具有对包的权限。  

 在域中使用可以访问分发点的帐户。 如果在创建包之后创建或更改帐户，则必须重新分发包。 更新包不会更改对包的 NTFS 权限。  

 不必将网络访问帐户添加为包访问帐户，因为用户组的成员身份会自动添加它。 将包访问帐户限制为网络访问帐户不会阻止客户端访问包。  

### <a name="reporting-services-point-account"></a>Reporting Services 点帐户  
 SQL Server Reporting Services 使用 **Reporting Services 点帐户**从站点数据库中检索 Configuration Manager 报表的数据。 你指定的 Windows 用户帐户和密码经过加密，并存储在 SQL Server Reporting Services 数据库中。  

### <a name="remote-tools-permitted-viewer-accounts"></a>远程工具“允许的查看者”帐户  
 你为远程控制指定的“允许的查看者”  帐户是一系列获准在客户端上使用远程工具功能的用户。  

### <a name="site-system-installation-account"></a>站点系统安装帐户  
 站点服务器使用**站点系统安装帐户**安装、重新安装、卸载和设置站点系统。 如果将站点系统设置为要求站点服务器启动到此站点系统的连接，则在安装站点系统和任何站点系统角色之后，Configuration Manager 还会使用此帐户从站点系统计算机中提取数据。 每个站点系统都可能具有不同的站点系统安装帐户，但是，只能设置一个站点系统安装帐户来管理该站点系统上的所有站点系统角色。  

 对于管理员将安装和设置的站点系统，此帐户需要具有这些系统上的本地管理权限。 此外，此帐户还要求在这些系统上的安全策略中指定“从网络访问此计算机”。  

> [!TIP]  
>  如果有多个域控制器，而且将跨域使用这些帐户，请在设置站点系统之前检查确认已复制这些帐户。  
>   
>  在指定位于要管理的每个站点系统上的本地帐户时，该配置比使用域帐户更安全，因为它在此帐户受到侵害时限制了攻击者可能造成的损害。 但是，域帐户更易于管理。 所以需就安全管理和有效管理进行权衡与协调。  

### <a name="smtp-server-connection-account"></a>SMTP 服务器连接帐户  
 当 SMTP 服务器需要对访问进行身份验证时，站点服务器使用 **SMTP 服务器连接帐户**来发送电子邮件警报。  

> [!IMPORTANT]  
>  指定具有可能最低的权限的帐户来发送电子邮件。  

### <a name="software-update-point-connection-account"></a>软件更新点连接帐户  
 站点服务器将**软件更新点连接帐户**用于下列两项软件更新服务：  

-   Windows Server Update Services (WSUS) Configuration Manager，用于设置诸如产品定义、分类和上游设置等设置。  

-   WSUS Synchronization Manager，它请求同步到上游 WSUS 服务器或 Microsoft 更新。  

站点系统安装帐户可以安装软件更新的组件，但无法在软件更新点上执行特定于软件更新的功能。 如果因为软件更新点在不受信任的林中而无法将站点服务器计算机帐户用于该功能，则除了指定站点系统安装帐户之外，还必须指定此帐户。  

此帐户必须是安装 WSUS 的计算机上的本地管理员。 它还必须属于本地 WSUS 管理员组。  

### <a name="software-update-point-proxy-server-account"></a>软件更新点代理服务器帐户  
 软件更新点使用**软件更新点代理服务器帐户**通过需要对访问进行身份验证的代理服务器或防火墙访问 Internet。  

> [!IMPORTANT]  
>  为所需的代理服务器或防火墙指定具有可能最低的权限的帐户。  

### <a name="source-site-account"></a>源站点帐户  
 迁移过程使用**源站点帐户**来访问源站点的 SMS 提供程序。 此帐户需要源站点中的站点对象的“读取”  权限来收集迁移作业的数据。  

 如果将 Configuration Manager 2007 分发点或具有共存分发点的辅助站点升级到 System Center Configuration Manager 分发点，则此帐户必须也具有“站点”类的“删除”权限才能在升级过程中从 Configuration Manager 2007 站点成功删除分发点。  

> [!NOTE]  
>  源站点帐户和源站点数据库帐户均在 Configuration Manager 控制台“管理”工作区的“帐户”的节点中被标识为“迁移管理器”。  

### <a name="source-site-database-account"></a>源站点数据库帐户  
 迁移过程使用**源站点数据库帐户**来访问源站点的 SQL Server 数据库。 若要从源站点的 SQL Server 数据库中收集数据，源站点数据库帐户必须具有源站点 SQL Server 数据库的“读取”和“执行”权限。  

> [!NOTE]  
>  如果使用 System Center Configuration Manager 计算机帐户，请确保此帐户符合下列所有条件：  
>   
> -   它是 Configuration Manager 2007 站点所在的域中的“Distributed COM Users”安全组的成员。  
> -   它是“SMS 管理员”  安全组的成员。  
> -   它具有对所有 Configuration Manager 2007 对象的“读取”权限。  

> [!NOTE]  
>  源站点帐户和源站点数据库帐户均在 Configuration Manager 控制台“管理”工作区的“帐户”的节点中被标识为“迁移管理器”。  

### <a name="task-sequence-editor-domain-joining-account"></a>任务序列编辑器域加入帐户  
 在任务序列中，使用 **任务序列编辑器域加入帐户** 将最近映像化的计算机加入到域。 如果将“加入域或工作组”  步骤添加到任务序列，然后选择“加入域” ，则需要此帐户。 如果将“应用网络设置”步骤添加到任务序列，则也可以设置此帐户，但这不是必需的。  

 此帐户需要获得计算机将加入的域中的“域加入”  权限。  

> [!TIP]  
>  如果需要将此帐户用于任务序列，则可以创建一个具有访问所需网络资源的最低权限的域用户帐户，并将其用于所有任务序列帐户。  

> [!IMPORTANT]  
>  请勿向此帐户分配交互式登录权限。  
>   
>  请勿将网络访问帐户用于此帐户。  

### <a name="task-sequence-editor-network-folder-connection-account"></a>任务序列编辑器网络文件夹连接帐户  
 任务序列使用**任务序列编辑器网络文件夹连接帐户**来连接到网络上的共享文件夹。 如果将“连接到网络文件夹”  步骤添加到任务序列中，则需要此帐户。  

 此帐户需要具有访问指定共享文件夹的权限。 它必须是域帐户。  

> [!TIP]  
>  如果需要将此帐户用于任务序列，则可以创建一个具有访问所需网络资源的最低权限的域用户帐户，并将其用于所有任务序列帐户。  

> [!IMPORTANT]  
>  请勿向此帐户分配交互式登录权限。  
>   
>  请勿将网络访问帐户用于此帐户。  

### <a name="task-sequence-run-as-account"></a>任务序列运行方式帐户  
 **任务序列运行方式帐户** 用于在任务序列中运行命令行，而且使用不同于本地系统帐户的凭据。 如果将“运行命令行”步骤添加到任务序列，但不希望任务序列在托管计算机上使用本地系统帐户权限来运行，则需要此帐户。  

 设置此帐户，使其具有运行在任务序列中指定的命令行所需的最低权限。 此帐户需要交互式登录权限，而且它通常需要安装软件和访问网络资源的能力。  

> [!IMPORTANT]  
>  请勿将网络访问帐户用于此帐户。  
>   
>  切勿将此帐户设为域管理员。  
>   
>  切勿为此帐户设置漫游配置文件。 任务序列运行时，它将为该帐户下载漫游配置文件。 这会导致该配置文件在本地计算机上面临易被访问的风险。  
>   
>  要限制此帐户的作用域。 例如，为每个任务序列创建不同的任务序列运行方式帐户，以便在某个帐户受到侵害时，只会损害该帐户能够访问的客户端计算机。  
>   
>  如果命令行需要计算机上的管理权限，请考虑在所有将运行任务序列的计算机上为任务序列运行方式帐户单独创建一个本地管理员帐户。 不再需要该帐户时请立即将其删除。  
