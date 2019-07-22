---
title: 使用的帐户
titleSuffix: Configuration Manager
description: 标识和管理 Configuration Manager 中使用的 Windows 组、帐户和 SQL 对象。
ms.date: 05/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 254639f905ca52f922d84fd19366807c3be2c339
ms.sourcegitcommit: d74415e49a6db28ee5198440c7f321529a9f7f33
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68312485"
---
# <a name="accounts-used-in-configuration-manager"></a>Configuration Manager 中使用的帐户

适用范围：  System Center Configuration Manager (Current Branch)

使用以下信息来标识 Configuration Manager 中使用的 Windows 组、帐户和 SQL 对象及其使用方式和任何要求。  

- [Configuration Manager 创建和使用的 Windows 组](#bkmk_groups)  
    - [ConfigMgr_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
    - [ConfigMgr_DViewAccess](#configmgr_dviewaccess)  
    - [ConfigMgr 远程控制用户](#configmgr-remote-control-users)  
    - [SMS 管理员](#sms-admins)  
    - [SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>](#bkmk_remotemp)  
    - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>](#bkmk_remoteprov)  
    - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>](#bkmk_remotestat)  
    - [SMS_SiteToSiteConnection_&lt;sitecode\>](#bkmk_filerepl)  

- [Configuration Manager 使用的帐户](#bkmk_accounts)
    - [Active Directory 组发现帐户](#active-directory-group-discovery-account)  
    - [Active Directory 系统发现帐户](#active-directory-system-discovery-account)  
    - [Active Directory 用户发现帐户](#active-directory-user-discovery-account)  
    - [Active Directory 林帐户](#active-directory-forest-account)  
    - [证书注册点帐户](#certificate-registration-point-account)  
    - [捕获 OS 映像帐户](#capture-os-image-account)  
    - [客户端请求安装帐户](#client-push-installation-account)  
    - [注册点连接帐户](#enrollment-point-connection-account)  
    - [Exchange Server 连接帐户](#exchange-server-connection-account)  
    - [管理点连接帐户](#management-point-connection-account)  
    - [多播连接帐户](#multicast-connection-account)  
    - [网络访问帐户](#network-access-account)  
    - [包访问帐户](#package-access-account)  
    - [Reporting Services 点帐户](#reporting-services-point-account)  
    - [远程工具“允许的查看者”帐户](#remote-tools-permitted-viewer-accounts)  
    - [站点安装帐户](#site-installation-account)
    - [站点系统安装帐户](#site-system-installation-account)  
    - [站点系统代理服务器帐户](#site-system-proxy-server-account)  
    - [SMTP 服务器连接帐户](#smtp-server-connection-account)  
    - [软件更新点连接帐户](#software-update-point-connection-account)  
    - [源站点帐户](#source-site-account)  
    - [源站点数据库帐户](#source-site-database-account)  
    - [任务序列域加入帐户](#task-sequence-domain-join-account)  
    - [任务序列网络文件夹连接帐户](#task-sequence-network-folder-connection-account)  
    - [任务序列运行方式帐户](#task-sequence-run-as-account)  

- [Configuration Manager 在 SQL 中使用的用户对象](#bkmk_sqlobjects)
    - [smsdbuser_ReadOnly](#smsdbuser_readonly)
    - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
    - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

## <a name="bkmk_groups"></a>Configuration Manager 创建和使用的 Windows 组  

 Configuration Manager 会自动创建并在许多情况下自动维护以下 Windows 组：  

> [!NOTE]  
>  当 Configuration Manager 在作为域成员的计算机上创建组时，该组为本地安全组。 如果计算机是域控制器，则该组是域本地组。 此类组在域中的所有域控制器之间共享。  


### <a name="configmgr_collectedfilesaccess"></a> ConfigMgr_CollectedFilesAccess

Configuration Manager 使用此组来授予查看软件清单所收集的文件的访问权限。  

有关详细信息，请参阅[软件清单简介](/sccm/core/clients/manage/inventory/introduction-to-software-inventory)。

#### <a name="type-and-location"></a>类型和位置
此组是在主站点服务器上创建的本地安全组。

卸载站点时，不会自动删除此组。 卸载站点后需手动删除。

#### <a name="membership"></a>Membership
Configuration Manager 自动管理组成员身份。 成员身份管理用户，这些管理用户被授予对分配的安全角色中“集合”  安全对象的“查看收集的文件”  权限。

#### <a name="permissions"></a>权限
默认情况下，该组对站点服务器上的以下文件夹具有“读取”权限：`C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`   


### <a name="configmgr_dviewaccess"></a>ConfigMgr_DViewAccess  

 此组是由 Configuration Manager 在子主站点的站点数据库服务器或数据库副本服务器上创建的本地安全组。 使用分布式视图在层次结构中的站点之间进行数据库复制时，站点会创建它。 它包含管理中心站点的站点服务器和 SQL Server 计算机帐户。

 有关详细信息，请参阅[站点间数据传输](/sccm/core/servers/manage/data-transfers-between-sites)。


### <a name="configmgr-remote-control-users"></a>ConfigMgr 远程控制用户  

 Configuration Manager 远程工具使用此组来存储在“允许的查看者”列表中设置的帐户和组  。 该站点将此列表分配给每个客户端。  

有关详细信息，请参阅[远程控制简介](/sccm/core/clients/manage/remote-control/introduction-to-remote-control)。

#### <a name="type-and-location"></a>类型和位置
此组是在客户端接收启用远程工具的策略时在 Configuration Manager 客户端上创建的本地安全组。

为客户端禁用远程工具后，不会自动删除此组。 禁用远程工具后需手动删除。

#### <a name="membership"></a>Membership
默认情况下，此组中没有成员。 将用户添加到“允许的查看者”列表时，会将这些用户自动添加到此组中  。

使用“允许的查看者”列表来管理此组的成员身份，而不是将用户或组直接添加到此组  。

除了作为允许的查看者外，管理用户还必须具有“集合”  对象的“远程控制”  权限。 使用“远程工具操作人员”安全角色分配此权限  。  

#### <a name="permissions"></a>权限
默认情况下，此组无权访问计算机上的任何位置。 它仅用于保留“允许的查看者”列表  。  


### <a name="sms-admins"></a>SMS 管理员  

 Configuration Manager 使用此组通过 WMI 授予对 SMS 提供程序的访问权限。 需要 SMS 提供程序的访问权限才能在 Configuration Manager 控制台中查看和更改对象。  

> [!NOTE]  
>  管理用户的基于角色的管理配置确定他们在使用 Configuration Manager 控制台时可查看和管理哪些对象。  

有关详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)。

#### <a name="type-and-location"></a>类型和位置
此组是在具有 SMS 提供程序的每台计算机上创建的本地安全组。 

卸载站点时，不会自动删除此组。 卸载站点后需手动删除。

#### <a name="membership"></a>Membership
Configuration Manager 自动管理组成员身份。 默认情况下，层次结构中的每个管理用户和站点服务器计算机帐户都是站点中每个 SMS 提供程序计算机上的“SMS 管理员”组的成员  。

#### <a name="permissions"></a>权限
可在“WMI 控件”MMC 管理单元中查看 SMS 管理员组权限  。 默认情况下，授予该组对 `Root\SMS`WMI 命名空间“启用帐户”和“远程启用”的权限   。 经过身份验证的用户具有**执行方法**、**提供程序写入**和**启用帐户**权限。

使用远程 Configuration Manager 控制台时，请在站点服务器计算机和 SMS 提供程序上配置“远程激活”DCOM 权限  。 将这些权限授予“SMS 管理员”组  。 此操作简化了管理，而不是直接向用户或组授予这些权限。 有关详细信息，请参阅[为远程 Configuration Manager 控制台配置 DCOM 权限](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ConfigDCOMforRemoteConsole)。 


### <a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>  
 
远离站点服务器的管理点使用此组来连接到站点数据库。 此组向管理点提供对站点服务器上的收件箱文件夹和站点数据库的访问权限。  

#### <a name="type-and-location"></a>类型和位置
此组是在具有 SMS 提供程序的每台计算机上创建的本地安全组。

卸载站点时，不会自动删除此组。 卸载站点后需手动删除。

#### <a name="membership"></a>Membership
Configuration Manager 自动管理组成员身份。 默认情况下，成员身份包括具有站点管理点的远程计算机的计算机帐户。

#### <a name="permissions"></a>权限
默认情况下，该组对站点服务器上的以下文件夹具有“读取”、“读取和执行”以及“列出文件夹内容”权限：`C:\Program Files\Microsoft Configuration Manager\inboxes`    。 此组对管理点向其中写入客户端数据的“Write”下的子文件夹具有额外的“inboxes”权限   。


### <a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>  
 
远程 SMS 提供程序计算机使用此组来连接到站点服务器。  

#### <a name="type-and-location"></a>类型和位置
此组是在站点服务器上创建的本地安全组。

卸载站点时，不会自动删除此组。 卸载站点后需手动删除。

#### <a name="membership"></a>Membership
Configuration Manager 自动管理组成员身份。 默认情况下，成员资格包括计算机帐户或域用户帐户。 它使用此帐户从每个远程 SMS 提供程序连接到站点服务器。

#### <a name="permissions"></a>权限
默认情况下，该组对站点服务器上的以下文件夹具有“读取”、“读取和执行”以及“列出文件夹内容”权限：`C:\Program Files\Microsoft Configuration Manager\inboxes`    。 该组具有“写入”和“修改”到收件箱下方子文件夹的附加权限   。 SMS 提供程序需要访问这些文件夹。

该组还对 `C:\Program Files\Microsoft Configuration Manager\OSD\Bin` 下的站点服务器上的子文件夹具有“读取”权限  。 

它还具有 `C:\Program Files\Microsoft Configuration Manager\OSD\boot` 下面的子文件夹的以下权限：
- **读取**  
- **读取和执行**  
- **列出文件夹内容**  
- **写入**  
- **修改**   


### <a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>  

Configuration Manager 远程站点系统计算机上的文件分派管理器使用此组来连接到站点服务器。  

#### <a name="type-and-location"></a>类型和位置
此组是在站点服务器上创建的本地安全组。

卸载站点时，不会自动删除此组。 卸载站点后需手动删除。

#### <a name="membership"></a>Membership
Configuration Manager 自动管理组成员身份。 默认情况下，成员资格包括计算机帐户或域用户帐户。 它使用此帐户从运行文件分派管理器的每个远程站点系统连接到站点服务器。

#### <a name="permissions"></a>权限
默认情况下，该组对站点服务器上的以下文件夹及其子文件夹具有“读取”、“读取和执行”以及“列出文件夹内容”权限：`C:\Program Files\Microsoft Configuration Manager\inboxes`    。 

该组对站点服务器上的以下文件夹具有“写入”和“修改”附加权限：`C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box`   。


### <a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_&lt;sitecode\>  
 Configuration Manager 使用此组在层次结构中的站点之间实现基于文件的复制。 对于将文件直接传输到此站点的每个远程站点，此组包含设为“文件复制帐户”  的帐户。  

#### <a name="type-and-location"></a>类型和位置
此组是在站点服务器上创建的本地安全组。

#### <a name="membership"></a>Membership
安装新站点作为另一个站点的子站点时，Configuration Manager 会自动将新站点的计算机帐户添加到父站点服务器上的组。 Configuration Manager 还会将父站点计算机帐户添加到新站点服务器上的组中。 如果为基于文件的传输指定另一个帐户，请将此帐户添加到目标站点服务器上的此组。

卸载站点时，不会自动删除此组。 卸载站点后需手动删除。

#### <a name="permissions"></a>权限
默认情况下，此组具有对以下文件夹的“完全控制”权限：`C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive`  。



## <a name="bkmk_accounts"></a> Configuration Manager 使用的帐户  

 可以为 Configuration Manager 设置下列帐户。  


### <a name="active-directory-group-discovery-account"></a>Active Directory 组发现帐户  

 该站点使用“Active Directory 组发现帐户”从指定的 Active Directory 域服务中的位置发现以下对象  ：
- 本地、全局和通用安全组
- 这些组内的成员资格
- 分发组内的成员资格
   - 不会以组资源的形式发现通讯组

  此帐户可以是运行发现的站点服务器的计算机帐户，或者是 Windows 用户帐户。 它必须对为发现指定的 Active Directory 位置具有“读取”访问权限  。  

  有关详细信息，请参阅 [Active Directory 组发现](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutGroup)。


### <a name="active-directory-system-discovery-account"></a>Active Directory 系统发现帐户  

 该站点使用“Active Directory 系统发现帐户”从指定的 Active Directory 域服务中的位置发现计算机  。  

 此帐户可以是运行发现的站点服务器的计算机帐户，或者是 Windows 用户帐户。 它必须对为发现指定的 Active Directory 位置具有“读取”访问权限  。  

 有关详细信息，请参阅 [Active Directory 系统发现](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutSystem)。


### <a name="active-directory-user-discovery-account"></a>Active Directory 用户发现帐户  
 
 该站点使用“Active Directory 系统发现帐户”从指定的 Active Directory 域服务中的位置发现用户帐户  。  

 此帐户可以是运行发现的站点服务器的计算机帐户，或者是 Windows 用户帐户。 它必须对为发现指定的 Active Directory 位置具有“读取”访问权限  。  

 有关详细信息，请参阅 [Active Directory 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser)。 


### <a name="active-directory-forest-account"></a>Active Directory 林帐户  

 该站点使用“Active Directory 林帐户”发现 Active Directory 林中的网络基础结构  。 管理中心站点和主站点也用它来将站点数据发布到林的 Active Directory 域服务。  

 > [!NOTE]  
 >  辅助站点始终使用辅助站点服务器计算机帐户来发布到 Active Directory。  

 要发现和发布到不受信任的林，Active Directory 林帐户必须是全局帐户。 如果不使用站点服务器的计算机帐户，则只能选择全局帐户。  

 此帐户必须对要在其中发现网络基础结构的每个 Active Directory 林具有“读取”  权限。  

 此帐户必须对要在其中发布站点数据的每个 Active Directory 林中的“系统管理”容器及其所有子对象具有“完全控制”权限   。 有关详细信息，请参阅[为站点发布准备 Active Directory](/sccm/core/plan-design/network/extend-the-active-directory-schema)。  

 有关详细信息，请参阅 [Active Directory 林发现](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutForest)。


### <a name="certificate-registration-point-account"></a>证书注册点帐户  

 证书注册点使用“证书注册点帐户”连接到 Configuration Manager 数据库  。 它默认使用其计算机帐户，但可以改为配置用户帐户。 当证书注册点位于站点服务器的不受信任域中时，必须指定用户帐户。 此帐户只需要站点数据库的“读取”  权限，因为写入任务由状态消息系统处理。  

 有关详细信息，请参阅[证书配置文件简介](/sccm/protect/deploy-use/introduction-to-certificate-profiles)。


### <a name="capture-os-image-account"></a>捕获 OS 映像帐户  

 捕获 OS 映像时，Configuration Manager 使用“捕获 OS 映像帐户”访问存储捕获映像的文件夹  。 如果将“捕获 OS 映像”步骤添加到任务序列，则需要此帐户  。  

 该帐户必须在存储捕获图像的网络共享上具有“读取”和“写入”权限   。  

 如果更改 Windows 帐户的密码，请使用新密码更新任务序列。 Configuration Manager 客户端在下次下载客户端策略时接收新密码。  

 如果需要使用此帐户，请创建一个域用户帐户。 授予它访问所需网络资源的最小权限，并将其用于所有捕获任务序列。  

 > [!IMPORTANT]  
 >  请勿向此帐户分配交互式登录权限。  
 >   
 >  请勿将网络访问帐户用于此帐户。  

 有关详细信息，请参阅[创建用于捕获 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system)。


### <a name="client-push-installation-account"></a>客户端请求安装帐户  

 使用客户端请求安装方法部署客户端时，站点使用“客户端请求安装帐户”连接到计算机并安装 Configuration Manager 客户端软件  。 如果未指定此帐户，站点服务器会尝试使用其计算机帐户。  

 该帐户必须是目标客户端计算机上本地“管理员”组的成员  。 此帐户不需要“域管理员”权限  。  

 你可以指定多个客户端请求安装帐户。 Configuration Manager 依次尝试每一个，直到成功。  

> [!TIP]  
>  如果你有大型的 Active Directory 环境并需要更改此帐户，请使用以下过程更有效地协调此帐户更新： 
> 1. 使用其他名称创建一个新帐户   
> 2. 将新帐户添加到 Configuration Manager 中的客户端请求安装帐户列表中  
> 3. 为 Active Directory 域服务复制新帐户留出足够的时间  
> 4. 然后从 Configuration Manager 和 Active Directory 域服务中删除旧帐户  

> [!IMPORTANT]  
>  请勿向此帐户授予本地登录的权限。  

 有关详细信息，请参阅[客户端请求安装](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation)。


### <a name="enrollment-point-connection-account"></a>注册点连接帐户  

 注册点使用“注册点连接帐户”连接到 Configuration Manager 站点数据库  。 它默认使用其计算机帐户，但可以改为配置用户帐户。 当注册点位于站点服务器的不受信任域中时，必须指定用户帐户。 此帐户需要站点数据库的“读取”  和“写入”  权限。  

 有关详细信息，请参阅[为本地 MDM 安装站点系统角色](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm)。


### <a name="exchange-server-connection-account"></a>Exchange Server 连接帐户  

 站点服务器使用“Exchange Server 连接帐户”连接到指定的 Exchange 服务器  。 它使用此连接来查找和管理连接到 Exchange Server 的移动设备。 此帐户需要 Exchange PowerShell cmdlet 以提供对 Exchange Server 计算机的所需权限。 有关 cmdlet 的详细信息，请参阅[使用 Configuration Manager 和 Exchange 管理移动设备](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)。  


### <a name="management-point-connection-account"></a>管理点连接帐户  

 管理点使用“管理点连接帐户”连接到 Configuration Manager 站点数据库  。 它使用此连接来发送和检索客户端的信息。 管理点默认使用其计算机帐户，但可以改为配置用户帐户。 当管理点位于站点服务器的不受信任域中时，必须指定用户帐户。  

 在运行 Microsoft SQL Server 的计算机上将此帐户创建为低权限本地帐户。  

> [!IMPORTANT]  
>  请勿向此帐户授予交互式登录的权限。  


### <a name="multicast-connection-account"></a>多播连接帐户  

 启用多播的分发点使用“多播连接帐户”从站点数据库中读取信息  。 默认情况下，服务器使用其计算机帐户，但可以改为配置用户帐户。 当站点数据库在不受信任的林中时，必须指定用户帐户。 例如，数据中心具有非站点服务器和站点数据库的林中的外围网络，则可以使用此帐户从站点数据库中读取多播信息。  

 如果需要此帐户，请在运行 Microsoft SQL Server 的计算机上将此帐户创建为低权限本地帐户。  

> [!IMPORTANT]  
>  请勿向此帐户授予交互式登录的权限。  

 有关详细信息，请参阅[使用多播通过网络部署 Windows](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)。


### <a name="network-access-account"></a>网络访问帐户  

 当客户端计算机无法使用其本地计算机帐户访问分发点上的内容时，它们将使用“网络访问帐户”  。 它主要适用于来自不受信任的域中的工作组客户端和计算机。 当安装 OS 的计算机在域上还没有计算机帐户时，也可能会在 OS 部署过程中使用此帐户。  

> [!Important]  
>  决不会将网络访问帐户用作安全性上下文来运行程序、安装软件更新或运行任务序列。 它仅用于访问网络上的资源。  

 Configuration Manager 客户端首先尝试使用其计算机帐户下载内容。 如果失败，则会自动尝试网络访问帐户。  

 从 1806 版开始，工作组或 Azure AD 加入的客户端可以安全地从分发点访问内容，而无需网络访问帐户。 此行为包括 OS 部署方案，其中任务序列从启动媒体、PXE 或软件中心运行。 有关详细信息，请参阅[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)。<!--1358228,1358278-->

 > [!Note]  
 > 如果启用“增强型 HTTP”以不需要网络访问帐户，则分发点需要运行 Windows Server 2008 R2 SP1 或更高版本  。 <!--SCCMDocs-pr issue #2696-->
>  
> 在启用此功能之前，请将客户端至少升级到 1806 版。 如果仅允许“增强型 HTTP”连接，则较旧的客户端无法使用此方法进行身份验证，因此无法从分发点下载客户端升级包  。 <!--vso2841213-->   

#### <a name="permissions"></a>权限

 授予此帐户对内容的最低合适权限，客户端需要此权限来访问软件。 在该分发点上，帐户必须具有“从网络访问此计算机”  权限。 每个站点最多可以配置 10 个网络访问帐户。  

 在任何域中创建将提供资源的所需访问权限的帐户。 网络访问帐户必须始终包含一个域名。 此帐户不支持传递安全性。 如果在多个域中具有分发点，请在受信任的域中创建帐户。  

> [!TIP]  
> 为了避免帐户锁定，请不要对现有网络访问帐户更改密码。 而是在 Configuration Manager 中创建新帐户并设置此新帐户。 在经过足够的时间让所有客户端接收新帐户详细信息之后，请从网络共享文件夹中移除旧帐户并删除该帐户。  

> [!IMPORTANT]  
>  请勿向此帐户授予交互式登录的权限。  
>   
>  请勿授予此帐户将计算机加入到域的权限。 如果在任务序列过程中必须将计算机加入到域中，请使用[任务序列域加入帐户](#task-sequence-domain-join-account)。  

#### <a name="configure-the-network-access-account"></a>配置网络访问帐户  

1.  在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。 然后选择站点。  

2.  在功能区的“设置”组中，选择“配置站点组件”，再选择“软件分发”    。  

3.  选择“网络访问帐户”选项卡  。设置一个或多个帐户，然后选择“确定”  。  


### <a name="package-access-account"></a>包访问帐户  

 利用“包访问帐户”，可以设置 NTFS 权限，该权限用于指定可以访问分发点上的包内容的用户和用户组  。 默认情况下，Configuration Manager 仅向通用访问帐户“用户”和“管理员”授予访问权限   。 可以通过使用其他的 Windows 帐户或组来控制客户端计算机的访问权限。 移动设备始终会匿名检索包内容，所以这些设备不使用包访问帐户。  

 默认情况下，当 Configuration Manager 将内容文件复制到分发点时，它会授予对本地“用户”组的“读取”权限以及对本地“管理”组的“完全控制”权限     。 所需的实际权限取决于包。 如果你的客户端在工作组或不受信任的林中，则那些客户端会使用网络访问帐户访问包内容。 请使用定义的包访问帐户来确保网络访问帐户具有对包的权限。  

 在域中使用可以访问分发点的帐户。 如果在创建包之后创建或修改帐户，则必须重新分发包。 更新包不会更改对包的 NTFS 权限。  

 不必将网络访问帐户添加为包访问帐户，因为“用户”组的成员身份会自动添加它  。 将包访问帐户限制为网络访问帐户不会阻止客户端访问包。  

#### <a name="manage-package-access-accounts"></a>管理包访问帐户  

1.  在 Configuration Manager 控制台中，选择“软件库”  。  

2.  在“软件库”  工作区中，确定要为其管理访问帐户的内容的类型，并按以下提供的步骤进行操作：  

    -   **应用程序**：展开“应用程序管理”，选择“应用程序”，然后选择要为其管理访问帐户的应用程序   。  

    -   **包**：展开“应用程序管理”，选择“包”，然后选择要为其管理访问帐户的包   。  

    -   **软件更新部署包**：展开“软件更新”，选择“部署包”，然后选择要为其管理访问帐户的部署包   。  

    -   **驱动程序包**：展开“操作系统”，选择“驱动程序包”，然后选择要为其管理访问帐户的驱动程序包   。  

    -   **OS 映像**：展开“操作系统”，选择“操作系统映像”，然后选择要为其管理访问帐户的操作系统映像   。  

    -   **OS 升级包**：展开“操作系统”，选择“操作系统升级包”，然后选择要为其管理访问帐户的操作系统升级包   。  

    -   **启动映像**：展开“操作系统”，选择“启动映像”，然后选择要为其管理访问帐户的启动映像   。  

3.  右键单击所选对象，然后选择“管理访问帐户”  。  

4.  在“添加帐户”  对话框中，指定将为其授予内容访问权限的帐户类型，然后指定与帐户关联的访问权限。  

    > [!NOTE]  
    >  为帐户添加用户名且 Configuration Manager 发现具有该名称的本地用户帐户和域用户帐户时，Configuration Manager 将为域用户帐户设置访问权限。  


### <a name="reporting-services-point-account"></a>Reporting Services 点帐户  
 
 SQL Server Reporting Services 使用“Reporting Services 点帐户”从站点数据库中检索 Configuration Manager 报表的数据  。 你指定的 Windows 用户帐户和密码经过加密，并存储在 SQL Server Reporting Services 数据库中。  

 > [!NOTE]  
 > 指定的帐户在承载 SQL Reporting Services 数据库的计算机上必须具有“本地登录”权限  。

 有关详细信息，请参阅[报表简介](/sccm/core/servers/manage/introduction-to-reporting)。


### <a name="remote-tools-permitted-viewer-accounts"></a>远程工具“允许的查看者”帐户  

 你为远程控制指定的“允许的查看者”  帐户是一系列获准在客户端上使用远程工具功能的用户。  

有关详细信息，请参阅[远程控制简介](/sccm/core/clients/manage/remote-control/introduction-to-remote-control)。


### <a name="site-installation-account"></a>站点安装帐户
<!--SCCMDocs issue #572-->
使用域用户帐户登录运行 Configuration Manager 安装程序的服务器并安装新站点。

此帐户要求具有以下权限：  

- 下列服务器上的管理员  权限：
    - 站点服务器  
    - 托管站点数据库的每个服务器  
    - 站点的每个 SMS 提供程序实例  

- 托管站点数据库的 SQL Server 实例上的 **Sysadmin**  

Configuration Manager 安装程序会自动将此帐户添加到 [SMS 管理员](#sms-admins)组。

安装后，此帐户是唯一具有 Configuration Manager 控制台权限的用户。 如果需要删除此帐户，请务必先将其权限添加到其他用户。

展开独立站点以包含管理中心站点时，此帐户在独立主站点上需要“完全权限管理员”或“基础结构管理员”基于角色的管理权限   。


### <a name="site-system-installation-account"></a>站点系统安装帐户  

 站点服务器使用“站点系统安装帐户”安装、重新安装、卸载和设置站点系统  。 如果将站点系统设置为要求站点服务器启动到此站点系统的连接，则在安装站点系统和任何角色之后，Configuration Manager 还会使用此帐户从站点系统计算机中提取数据。 每个站点系统都可能具有不同的安装帐户，但只能设置一个安装帐户来管理该站点系统上的所有角色。  

 此帐户需要目标站点系统上的本地管理权限。 此外，此帐户必须在目标站点系统的安全策略中指定“从网络访问此计算机”  。  

 > [!TIP]  
 >  如果有多个域控制器并且跨域使用这些帐户，请在设置站点系统之前，检查 Active Directory 是否已复制这些帐户。  
 >   
 >  在指定位于要管理的每个站点系统上的本地帐户时，该配置比使用域帐户更安全。 它会限制在此帐户受到侵害时攻击者可能造成的损害。 但是，域帐户更易于管理。 所以需就安全管理和有效管理进行权衡与协调。  


### <a name="site-system-proxy-server-account"></a>站点系统代理服务器帐户
<!--SCCMDocs issue #648-->
 以下站点系统角色使用“站点系统代理服务器帐户”通过需要对访问进行身份验证的代理服务器或防火墙访问 Internet  ：

- 资产智能同步点
- Exchange Server 连接器
- 服务连接点
- 软件更新点

> [!IMPORTANT]  
>  为所需的代理服务器或防火墙指定具有可能最低的权限的帐户。  

 有关详细信息，请参阅[代理服务器支持](/sccm/core/plan-design/network/proxy-server-support)。


### <a name="smtp-server-connection-account"></a>SMTP 服务器连接帐户  

 当 SMTP 服务器需要对访问进行身份验证时，站点服务器使用“SMTP 服务器连接帐户”来发送电子邮件警报  。  

> [!IMPORTANT]  
>  指定具有可能最低的权限的帐户来发送电子邮件。  

 有关详细信息，请参阅[使用警报和状态系统](/sccm/core/servers/manage/use-alerts-and-the-status-system)。


### <a name="software-update-point-connection-account"></a>软件更新点连接帐户  

 站点服务器将“软件更新点连接帐户”用于下列两项软件更新服务  ：  

-   Windows Server Update Services (WSUS)，用于设置诸如产品定义、分类和上游设置等设置。  

-   WSUS Synchronization Manager，它请求同步到上游 WSUS 服务器或 Microsoft 更新。  

[站点系统安装帐户](#site-system-installation-account)可以安装软件更新的组件，但无法在软件更新点上执行特定于软件更新的功能。 如果因为软件更新点在不受信任的林中而无法将站点服务器计算机帐户用于该功能，则除指定站点系统安装帐户之外，还必须指定此帐户。  

此帐户必须是安装 WSUS 的计算机上的本地管理员。 它还必须属于本地“WSUS 管理员”组  。  

有关详细信息，请参阅[规划软件更新](/sccm/sum/plan-design/plan-for-software-updates)。


### <a name="source-site-account"></a>源站点帐户  

 迁移过程使用“源站点帐”来访问源站点的 SMS 提供程序  。 此帐户需要源站点中的站点对象的“读取”  权限来收集迁移作业的数据。  

 如果有 Configuration Manager 2007 分发点或具有共置分发点的辅助站点，则在将它们升级到 Configuration Manager（当前分支）分发点时，此帐户还必须具有对“站点”类的“删除”权限   。 此权限是在升级期间从 Configuration Manager 2007 站点成功删除分发点。  

> [!NOTE]  
>  源站点帐户和[源站点数据库帐户](#source-site-database-account)均在 Configuration Manager 控制台“管理”工作区的“帐户”的节点中被标识为“迁移管理器”    。  

 有关详细信息，请参阅[在层次结构之间迁移数据](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies)。


### <a name="source-site-database-account"></a>源站点数据库帐户  

 迁移过程使用“源站点数据库帐户”来访问源站点的 SQL Server 数据库  。 若要从源站点的 SQL Server 数据库中收集数据，源站点数据库帐户必须具有源站点 SQL Server 数据库的“读取”和“执行”权限   。  

 如果使用 Configuration Manager（当前分支）计算机帐户，请确保此帐户的所有以下内容都是真的：  
   
 - 它是与 Configuration Manager 2007 站点位于同一域中的“分布式 COM 用户”安全组的成员   
 - 它是“SMS 管理员”安全组的成员   
 - 它具有对所有 Configuration Manager 2007 对象的“读取”权限   

> [!NOTE]  
>  源站点帐户和[源站点数据库帐户](#source-site-database-account)均在 Configuration Manager 控制台“管理”工作区的“帐户”的节点中被标识为“迁移管理器”    。  

 有关详细信息，请参阅[在层次结构之间迁移数据](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies)。


### <a name="task-sequence-domain-join-account"></a>任务序列域加入帐户 

 Windows 安装程序使用“任务序列域加入帐户”将新映像的计算机加入域  。 [加入域或工作组](/sccm/osd/understand/task-sequence-steps#BKMK_JoinDomainorWorkgroup)任务序列步骤以及“加入域”选项，需要此帐户  。 也可以使用[应用网络设置](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyNetworkSettings)步骤设置此帐户，但这不是必需的。  

 此帐户需要在目标域中具有“域加入”权限  。  

> [!TIP]  
>  创建一个具有加入域最低权限权限的域用户帐户，并将其用于所有任务序列。  

> [!IMPORTANT]  
>  请勿向此帐户分配交互式登录权限。  
>   
>  请勿将网络访问帐户用于此帐户。  


### <a name="task-sequence-network-folder-connection-account"></a>任务序列网络文件夹连接帐户  

 任务序列引擎使用“任务序列网络文件夹连接帐户”连接到网络上的共享文件夹  。 [连接到网络文件夹](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)任务序列步骤需要此帐户。  

 此帐户需要具有访问指定共享文件夹的权限。 必须是域用户帐户。  

> [!TIP]  
>  创建一个具有访问所需网络资源的最低权限的域用户帐户，并将其用于所有任务序列帐户。  

> [!IMPORTANT]  
>  请勿向此帐户分配交互式登录权限。  
>   
>  请勿将网络访问帐户用于此帐户。  


### <a name="task-sequence-run-as-account"></a>任务序列运行方式帐户  

 任务序列引擎使用“任务序列运行方式帐户”来运行具有除本地系统帐户之外的凭据的命令行或 PowerShell 脚本  。 [运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)和[运行 PowerShell 脚本](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript)任务序列步骤需要此帐户，并选择“将此步骤作为以下帐户运行”  。  

 设置此帐户，使其具有运行在任务序列中指定的命令行所需的最低权限。 此帐户需要交互式登录权限。 它通常需要安装软件和访问网络资源的能力。 对于运行 PowerShell 脚本任务，此帐户需要本地管理员权限。 

> [!IMPORTANT]  
>  请勿将网络访问帐户用于此帐户。  
>   
>  切勿将此帐户设为域管理员。  
>   
>  切勿为此帐户设置漫游配置文件。 任务序列运行时，它会为该帐户下载漫游配置文件。 这会导致该配置文件在本地计算机上面临易被访问的风险。  
>   
>  要限制此帐户的作用域。 例如，为每个任务序列创建不同的任务序列运行方式帐户。 然后，如果一个帐户受到侵害，则只会损害该帐户有权访问的客户端计算机。  
>   
>  如果命令行需要计算机上的管理权限，请考虑在所有运行任务序列的计算机上为此帐户单独创建一个本地管理员帐户。 不再需要该帐户时请立即将其删除。  


## <a name="bkmk_sqlobjects"></a> Configuration Manager 在 SQL 中使用的用户对象 
<!--SCCMDocs issue #1160-->
Configuration Manager 自动在 SQL 中创建和维护以下用户对象。  这些对象位于 Configuration Manager 数据库中的 Security/Users 下。  

> [!IMPORTANT]  
>  修改或删除这些对象可能会导致 Configuration Manager 环境中出现严重问题。  建议不要对这些对象进行任何更改。


### ### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

此对象用于在只读上下文中运行查询。  此对象与多个存储过程结合使用。


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

此对象用于为动态 SQL 语句提供权限。


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

此对象用于运行 SQL 报告执行。  以下存储过程与此函数结合使用：spSRExecQuery。
