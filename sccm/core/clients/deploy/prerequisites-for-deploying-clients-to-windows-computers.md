---
title: "Windows 客户端部署先决条件 | Microsoft Docs"
description: "了解在 System Center Configuration Manager 中将客户端部署到 Windows 计算机的先决条件。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
caps.latest.revision: "16"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6636ce4d929326fad0210407d7634ea585eb0a2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中将客户端部署到 Windows 计算机的先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

在环境中部署 Configuration Manager 客户端有下列外部依赖关系和产品内部依赖关系。 此外，每个客户端部署方法有其自己的先决条件，要成功安装客户端，必须满足其自己的先决条件。  

  请确保同时查看 [System Center Configuration Manager 支持的配置](../../../core/plan-design/configs/supported-configurations.md)以确认设备满足 Configuration Manager 客户端的最低硬件和操作系统要求。  

 有关适用于 Linux 和 UNIX 的 Configuration Manager 客户端的先决条件的信息，请参阅[在 System Center Configuration Manager 中规划 Linux 和 UNIX 计算机的客户端部署](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)。  

> [!NOTE]  
>  本文中显示的软件版本号仅列出所需的最低版本号。  

##  <a name="BKMK_prereqs_computers"></a>计算机客户端的先决条件  
 使用下列信息来确定在计算机上安装 Configuration Manager 客户端时的先决条件。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系  

|||  
|-|-|  
|Windows Installer 版本 3.1.4000.2435|这是支持将 Windows Installer 更新文件 (.msp) 用于包和软件更新所必需的。|  
|[KB2552033](http://go.microsoft.com/fwlink/p/?LinkId=240048)|如果启用了客户端请求安装，则必须在运行 Windows Server 2008 R2 的站点服务器上安装此修补程序。|  
|Microsoft 后台智能传输服务 (BITS) 2.5 版|需要允许客户端计算机和 Configuration Manager 站点系统之间的受限数据传输。 客户端安装过程中不会自动下载 BITS。 在计算机上安装了 BITS 后，通常需要重启来完成安装。<br /><br /> 大多数操作系统都包括 BITS，但如果未包括（例如，Windows Server 2003 R2 SP2），则必须在安装 Configuration Manager 客户端之前安装 BITS。|  
|Microsoft 任务计划程序|在客户端上启用此服务，以便完成客户端安装。|  

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a>Configuration Manager 的外部依赖关系及安装过程中的自动下载  
 Configuration Manager 客户端有一些可能的外部依赖关系。 这些依赖关系取决于操作系统以及客户端计算机上安装的软件。  

 如果需要这些依赖关系来完成客户端安装，则它们将随客户端软件一起自动安装。  

|||  
|-|-|  
|Windows Update 代理版本 7.0.6000.363|Windows 要求支持更新检测和部署。|  
|Microsoft Core XML Services (MSXML) 版本 6.20.5002 或更高版本|要求支持在 Windows 中处理 XML 文档。|  
|Microsoft 远程差分压缩 (RDC)|需要该项以优化网络上的数据传输。|  
|Microsoft Visual C++ 2013 可再发行组件版本 12.0.21005.1|需要该项以支持客户端操作。 客户端计算机上安装此更新后，可能需要重新启动才能完成安装。|  
|Microsoft Visual C++ 2005 可再发行组件版本 8.0.50727.42|对于 1606 或更早版本，需要该项以支持 Microsoft SQL Server Compact 操作。|  
|Windows 映像 API 6.0.6001.18000|需要该项以允许 Configuration Manager 管理 Windows 映像 (.wim) 文件。|  
|Microsoft 策略平台 1.2.3514.0|需要该项以允许客户端评估符合性设置。|  
|Microsoft Silverlight 5.1.41212.0（从 Configuration Manager 版本 1602 开始）|需要该项以支持应用程序目录网站用户体验。|  
|Microsoft .NET Framework 版本 4.5.2|需要该项以支持客户端操作。 如果没有安装 Microsoft .NET Framework 4.5 或更高版本，那么将自动将其安装在客户端计算机上。 有关详细信息，请参阅[有关 Microsoft .NET Framework 版本 4.5.2 的其他详细信息](#dotNet)。|  
|Microsoft SQL Server Compact 3.5 SP2 组件|需要该项以存储与客户端操作相关的信息。|  
|Microsoft Windows 映像组件|对于 64 位计算机，适用于 Windows Server 2003 或 Windows XP SP2 的 Microsoft .NET Framework 4.0 需要该组件。|
|Microsoft Intune 电脑软件客户端|你不能在同一台电脑上运行 Intune 电脑软件客户端和 Configuration Manager 客户端。 在安装 Configuration Manager 客户端之前，请确保删除 Intune 客户端。|

####  <a name="dotNet"></a>有关 Microsoft .NET Framework 版本 4.5.2 的其他详细信息  

> [!NOTE]  
>  对 .NET 4.0、4.5 和 4.5.1 的支持已于 2016 年 1 月 12 日过期。 有关详细信息，请参阅 support.microsoft.com 处的 [Microsoft .NET Framework 支持生命周期策略常见问题解答](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update)。  

 可能需要重启以完成安装 Microsoft .NET Framework 版本 4.5.2。 用户将在系统托盘中看到 **需要重启** 通知。  需要客户端计算机重启的常见场景：  

-   计算机上正在运行.NET 应用程序或服务。  

-   .NET 安装所需的一个或多个软件更新丢失。  

-   计算机正在等待从 .NET Framework 软件更新的先前安装中重启。  

 安装.NET Framework 4.5.2 后，它的其他更新可能会随后安装，这可能需要另外重启计算机。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  
 有关以下站点系统角色的详细信息，请参阅[为 System Center Configuration Manager 客户端确定站点系统角色](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)  

|||  
|-|-|  
|管理点|尽管部署 Configuration Manager 客户端不需要管理点，但要在客户端计算机和 Configuration Manager 服务器之间传输信息，则必须有管理点。 没有管理点，就无法管理客户端计算机。|  
|分发点|分发点是可选的，但建议为客户端部署使用该站点系统角色。 所有分发点都承载客户端源文件，从而使计算机能够在客户端部署过程中找到从中下载客户端源文件的最近分发点。 如果站点没有分发点，则计算机从其管理点中下载客户端源文件。|  
|回退状态点|回退状态点是可选的，但建议为客户端部署使用该站点系统角色。 当 Configuration Manager 站点中的计算机不能与管理点通信时，回退状态点将跟踪客户端部署并允许这些计算机发送状态消息。|  
|Reporting Services 点|Reporting Services 点是可选的，但建议使用该站点系统角色，它能够显示与客户端部署和管理相关的报表。 有关详细信息，请参阅 [System Center Configuration Manager 中的报表](../../../core/servers/manage/reporting.md)。|  

### <a name="installation-method-dependencies"></a>安装方法依赖关系  
 以下先决条件特定于客户端的各种不同安装方法。  

-   客户端请求安装  

    -   客户端请求安装帐户用于连接到计算机以安装客户端，并且是在“客户端请求安装属性”  对话框的“帐户”  选项卡上指定的。 该帐户必须是目标计算机上本地管理员组的成员。  

         如果未指定客户端请求安装帐户，则使用站点服务器计算机帐户。  

    -   必须已通过至少一种 Configuration Manager 发现方法发现要在其中安装客户端的计算机。  

    -   计算机具有 ADMIN$ 共享。  

    -   如果要对发现的资源自动请求 Configuration Manager 客户端，则必须在“客户端请求安装属性”对话框中选择“对已分配资源启用客户端请求安装”。  

    -   客户端计算机必须能够联系分发点或管理点以便下载支持文件。  

     必须具有下列安全权限才能通过使用客户端请求安装 Configuration Manager 客户端：  

    -   配置客户端请求安装帐户：“站点”  对象的 **修改** 和读取权限。  

    -   使用客户端请求将客户端安装到集合、设备和查询：“集合”对象的 **修改资源** 和 **读取** 权限。  

     “基础结构管理员”  安全角色包括管理客户端请求安装所需的权限。  

-   基于软件更新点的安装  

    -   如果尚未扩展 Active Directory 架构，或者要从另一个林中安装客户端，则必须使用组策略在计算机的注册表中设置 CCMSetup.exe 的安装属性。 有关详细信息，请参阅  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision)。  

    -   必须将 Configuration Manager 客户端发布到软件更新点。  

    -   客户端计算机必须能够联系分发点或管理点以便下载支持文件。  

     有关管理 Configuration Manager 软件更新所需的安全权限，请参阅 [System Center Configuration Manager 中软件更新的先决条件](../../../sum/plan-design/prerequisites-for-software-updates.md)。  

-   基于组策略的安装  

    -   如果尚未扩展 Active Directory 架构，或者要从另一个林中安装客户端，则必须使用组策略在计算机的注册表中设置 CCMSetup.exe 的安装属性。 有关详细信息，请参阅  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision)。  

    -   客户端计算机必须能够联系管理点以便下载支持文件。  

-   基于登录脚本的安装  

     除非您在命令提示符处指定了包含命令行属性 **ccmsetup /source**的 CCMSetup.exe，否则客户端计算机必须能够联系分发点或管理点以便下载支持文件。  

-   手动安装  

     除非您在命令提示符处指定了包含命令行属性 **ccmsetup /source**的 CCMSetup.exe，否则客户端计算机必须能够联系分发点或管理点以便下载支持文件。  

-   工作组计算机安装  

     为了访问 Configuration Manager 站点服务器域中的资源，必须为该站点配置网络访问帐户。  

     有关如何配置“网络访问帐户”的详细信息，请参阅 [System Center Configuration Manager 中内容管理的基本概念](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)。  

-   基于软件分发的安装（仅针对升级）  

    -   如果尚未扩展 Active Directory 架构，或者要从另一个林中安装客户端，则必须使用组策略在计算机的注册表中设置 CCMSetup.exe 的安装属性。 有关详细信息，请参阅 [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision)。  

    -   客户端计算机必须能够联系分发点或管理点以便下载支持文件。  

     有关使用应用程序管理升级 Configuration Manager 客户端所需的安全权限，请参阅[应用程序管理的安全和隐私](../../../apps/plan-design/security-and-privacy-for-application-management.md)。  

-   自动客户端升级  

     你必须是“完全权限管理员”  安全角色的成员才能配置自动客户端升级。  

### <a name="firewall-requirements"></a>防火墙要求  
 如果站点系统服务器与你想要在其上安装 Configuration Manager 客户端的计算机之间存在防火墙，请参阅 [System Center Configuration Manager 中客户端的 Windows 防火墙和端口设置](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md)。  

##  <a name="BKMK_prereqs_mobiledevices"></a>移动设备客户端的先决条件  
 使用下列信息来确定在移动设备上安装 Configuration Manager 客户端和使用 Configuration Manager 注册这些设备时的先决条件。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系  

-   Microsoft 企业证书颁发机构 (CA) 及证书模板，用于部署和管理移动设备所需的证书。  

     颁发 CA 必须在注册过程中自动批准来自移动设备用户的证书请求。  

     有关证书要求的详细信息，请参阅 [System Center Configuration Manager 中证书配置文件的安全和隐私](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md)。  

-   一个安全组，其中包含可注册其移动设备的用户。  

     此安全组用于配置在移动设备注册过程中使用的证书模板。  

-   可选但建议使用：为您将在其上安装注册代理点的站点系统服务器名称配置的 DNS 别名（CNAME 记录），名为 **ConfigMgrEnroll** 。  

     必须有此 DNS 别名，才能支持注册服务自动发现：如果您未配置此 DNS 记录，则用户必须在注册过程中手动指定注册代理点的站点系统服务器名称。  

-   将运行注册点和注册代理点站点系统角色的计算机的站点系统角色依赖关系。  

     请参阅[站点系统服务器支持的操作系统](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  
 有关以下站点系统角色的详细信息，请参阅[为 System Center Configuration Manager 客户端确定站点系统角色](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)。  

-   为 HTTPS 客户端连接配置并为移动设备启用的管理点  

     必须使用管理点才能在移动设备上安装 Configuration Manager 客户端。 除了 HTTPS 要求和为移动设备启用的要求外，还必须将管理点配置为具有 Internet FQDN 并接受来自 Internet 的客户端连接。  

-   注册点和注册代理点  

     注册代理点管理来自移动设备的注册请求，注册点完成注册过程。 注册点必须位于站点服务器所在的 Active Directory 林中，但注册代理点则可位于另一个林中。  

-   移动设备注册的客户端设置  

     配置客户端设置以允许用户注册移动设备并至少配置一个注册配置文件。  

-   Reporting Services 点  

     Reporting Services 点是可选的，但建议使用该站点系统角色，它能够显示与移动设备注册和客户端管理相关的报表。  

     有关详细信息，请参阅 [System Center Configuration Manager 中的报表](../../../core/servers/manage/reporting.md)。  

-   要针对移动设备配置注册，你必须具有下列安全权限：  

    -   添加、修改和删除注册站点系统角色：“站点”  对象的 **修改** 权限。  

    -   配置客户端设置以供注册：默认客户端设置需要“站点”  对象的 **修改** 权限，自定义客户端设置需要 **客户端代理**  权限。  

     “完全权限管理员”  安全角色包括配置注册站点系统角色所需的权限。  

     要管理注册的移动设备，你必须具有下列安全权限：  

    -   擦除或停用移动设备：“集合”  对象的 **删除资源** 权限。  

    -   取消擦除或停用命令：“集合”  对象的 **删除资源** 权限。  

    -   允许和阻止移动设备：“集合”  对象的 **修改资源** 权限。  

    -   远程锁定或重置移动设备上的密码：“集合”  对象的 **修改资源** 权限。  

     “操作管理员”  安全角色包括管理移动设备所需的权限。  

     有关如何配置安全权限的详细信息，请参阅 [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md) 和  [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md)。  

### <a name="firewall-requirements"></a>防火墙要求  
 诸如路由器和防火墙以及 Windows 防火墙（如果适用）等干预网络设备必须允许与移动设备注册相关联的通讯：  

-   移动设备和注册代理点之间：HTTPS（默认情况下为 TCP 443）  

-   注册代理点和注册点之间：HTTPS（默认情况下为 TCP 443）  

 如果你使用代理 Web 服务器，则必须针对 SSL 隧道对其进行配置；移动设备不支持 SSL 桥接。  
