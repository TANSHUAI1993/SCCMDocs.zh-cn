---
title: "Windows 客户端的防火墙和端口设置 | Microsoft Docs"
description: "在 System Center Configuration Manager 中选择客户端的 Windows 防火墙和端口设置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 79686514efcba344c4babc3d3be03b48adca7132
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="windows-firewall-and-port-settings-for-clients-in-system-center-configuration-manager"></a>System Center Configuration Manager 中客户端的 Windows 防火墙和端口设置

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中运行 Windows 防火墙的客户端计算机通常需要配置例外，以便允许与它们的站点进行通信。 必须配置的例外取决于与 Configuration Manager 客户端一起使用的管理功能。  

 使用下列部分来确定这些管理功能，并了解有关如何为这些例外配置 Windows 防火墙的详细信息。  

##  <a name="BKMK_ModifyingWindowsFirewall"></a> 修改 Windows 防火墙允许的端口和程序  
 使用下列过程在 Windows 防火墙上为 Configuration Manager 客户端修改端口和程序。  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>修改 Windows 防火墙允许的端口和程序  

1.  在运行 Windows 防火墙的计算机上，打开“控制面板”。  

2.  右键单击“Windows 防火墙” ，再单击“打开” 。  

3.  配置任何必需的例外，以及你需要的任何自定义程序和端口。  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Configuration Manager 所需的程序和端口  
 以下 Configuration Manager 功能需要在 Windows 防火墙上配置例外：  

### <a name="queries"></a>查询  
 如果在运行 Windows 防火墙的计算机上运行 Configuration Manager 控制台，则在初次运行查询时会失败，而且操作系统会显示一个对话框，询问是否想取消阻止 statview.exe。 如果取消阻止，则以后运行的查询不会遇到错误。 在运行查询之前，也可以在 Windows 防火墙的“例外”  选项卡上手动将 Statview.exe 添加到程序和服务列表中。  

### <a name="client-push-installation"></a>客户端请求安装  
 若要使用客户端请求来安装 Configuration Manager 客户端，请将下列项目作为例外添加到 Windows 防火墙中：  

-   出站和入站：“文件和打印机共享”   

-   入站：“Windows Management Instrumentation (WMI)”   

### <a name="client-installation-by-using-group-policy"></a>使用组策略进行的客户端安装  
 若要使用组策略安装 Configuration Manager 客户端，请将“文件和打印机共享”作为例外添加到 Windows 防火墙中。  

### <a name="client-requests"></a>客户端请求  
 为使客户端计算机能与 Configuration Manager 站点系统通信，请将下列项目作为例外添加到 Windows 防火墙中：  

 出站：TCP 端口 **80** （用于 HTTP 通信）  

 出站：TCP 端口 **443** （用于 HTTPS 通信）  

> [!IMPORTANT]  
>  这些为默认端口号，可在 Configuration Manager 中进行更改。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端通信端口](../../../core/clients/deploy/configure-client-communication-ports.md)。 如果已更改了这些端口的默认值，则还必须在 Windows 防火墙上配置相应的例外。  

### <a name="client-notification"></a>客户端通知  
 当管理用户在 Configuration Manager 控制台中选择了客户端操作时（例如下载计算机策略或启动恶意软件扫描），为使管理点能将它必须执行的操作通知客户端计算机，请将下列项目作为例外添加到 Windows 防火墙中：  

 出站：TCP 端口 **10123**  

 如果此通信不成功，则 Configuration Manager 会自动恢复使用现有的客户端到管理点 HTTP 或 HTTPS 通信端口：  

 出站：TCP 端口 **80** （用于 HTTP 通信）  

 出站：TCP 端口 **443** （用于 HTTPS 通信）  

> [!IMPORTANT]  
>  这些为默认端口号，可在 Configuration Manager 中进行更改。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端通信端口](../../../core/clients/deploy/configure-client-communication-ports.md)。 如果已更改了这些端口的默认值，则还必须在 Windows 防火墙上配置相应的例外。  

### <a name="remote-control"></a>远程控制  
 若要使用 Configuration Manager 远程控制，请开放以下端口：  

-   入站：TCP 端口**2701**  

### <a name="remote-assistance-and-remote-desktop"></a>远程协助和远程桌面  
 若要通过 Configuration Manager 控制台启动远程协助，请在客户端计算机上的 Windows 防火墙中，将自定义程序 **Helpsvc.exe** 和自定义入站端口 TCP **135** 添加到允许的程序和服务列表中。 还必须允许“远程协助”  和“远程桌面” 。 如果从客户端计算机启动远程协助，则 Windows 防火墙会自动配置并允许“远程协助”  和“远程桌面” 。  

### <a name="wake-up-proxy"></a>唤醒代理  
 如果启用唤醒代理客户端设置，则名为“ConfigMgr 唤醒代理”的新服务会使用对等协议来检查子网上的其他计算机是否处于唤醒状态，并根据需要唤醒它们。 此通信使用下列端口：  

 出站：UDP 端口 **25536**  

 出站：UDP 端口 **9**  

 通过使用“唤醒代理端口号 (UDP)”和“LAN 唤醒端口号 (UDP)”的“电源管理”客户端设置可在 Configuration Manager 中更改这些默认端口号。 如果你指定“电源管理” ：“针对唤醒代理的 Windows 防火墙例外”  客户端设置，则将在 Windows 防火墙中为客户端自动配置这些端口。 但是，如果客户端运行另一个防火墙，则你必须手动为这些端口号配置例外。  

 除了使用这些端口之外，唤醒代理还使用 Internet 控制消息协议 (ICMP) 来回显在客户端计算机之间发送的请求消息。 此通信用于确认网络上的另一台客户端计算机是否处于唤醒状态。 ICMP 有时称为 TCP/IP ping 命令。  

 有关唤醒代理的详细信息，请参阅[规划如何在 System Center Configuration Manager 中唤醒客户端](../../../core/clients/deploy/plan/plan-wake-up-clients.md)。  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Windows 事件查看器、Windows 性能监视器和 Windows 诊断  
 若要从 Configuration Manager 控制台中访问 Windows 事件查看器、Windows 性能监视器和 Windows 诊断，请在 Windows 防火墙中将“文件和打印机共享”作为例外进行启用。  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Configuration Manager 客户端部署期间使用的端口  
 下表列出了客户端安装过程中使用的端口。  

> [!IMPORTANT]  
>  如果站点系统服务器与客户端计算机之间存在防火墙，请确认防火墙是否允许您选择的客户端安装方法所需的端口进出流量。 例如，防火墙经常会阻止客户端请求安装继续进行，因为防火墙会阻止服务器消息块 (SMB) 和远程过程调用 (RPC)。 在此情况下，请使用其他客户端安装方法，如手动安装（运行 CCMSetup.exe）或基于组策略的客户端安装。 这些替代客户端安装方法不需要 SMB 或 RPC。  

 有关如何在客户端计算机上配置 Windows 防火墙的信息，请参阅 [修改 Windows 防火墙允许的端口和程序](#BKMK_ModifyingWindowsFirewall)。  

### <a name="ports-that-are-used-for-all-installation-methods"></a>用于所有安装方法的端口  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|为客户端分配回退状态点时用于从客户端计算机向回退状态点进行传输的超文本传输协议 (HTTP)。|--|80（请参阅备注 1， **可用的备用端口**）|  

### <a name="ports-that-are-used-with-client-push-installation"></a>用于客户端请求安装的端口  
 除了使用下表中列出的端口之外，客户端请求安装还使用站点服务器向客户端计算机发出的 Internet 控制消息协议 (ICMP) 回显请求消息来确认网络上是否有客户端计算机。 ICMP 有时称为 TCP/IP ping 命令。 ICMP 没有 UDP 或 TCP 协议号，因此未在下表中列出。 但是，为了使客户端请求安装成功，任何干预网络设备（如防火墙）都必须容许 ICMP 流量。  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|站点服务器与客户端计算机之间的服务器消息块 (SMB)。|--|445|  
|站点服务器与客户端计算机之间的 RPC 终结点映射程序。|135|135|  
|站点服务器与客户端计算机之间的 RPC 动态端口。|--|DYNAMIC|  
|在通过超文本传输协议 (HTTP) 进行连接时，用于从客户端计算机连接到管理点的 HTTP。|--|80（请参阅备注 1， **可用的备用端口**）|  
|在通过安全超文本传输协议 (HTTPS) 进行连接时，用于从客户端计算机连接到管理点的 HTTPS。|--|433（请参阅备注 1， **可用的备用端口**）|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>用于基于软件更新点的安装的端口  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|用于从客户端计算机向软件更新点进行传输的超文本传输协议 (HTTP)。|--|80 或 8530（请参阅备注 2， **Windows Server Update Services**）|  
|用于从客户端计算机向软件更新点进行传输的安全超文本传输协议 (HTTPS)。|--|443 或 8531（请参阅备注 2， **Windows Server Update Services**）|  
|指定 CCMSetup 命令行属性 **/source:&lt;Path\>** 时源服务器与客户端计算机之间的服务器消息块 (SMB)。|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>用于基于组策略的安装的端口  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|在通过超文本传输协议 (HTTP) 进行连接时，用于从客户端计算机连接到管理点的 HTTP。|--|80（请参阅备注 1， **可用的备用端口**）|  
|在通过安全超文本传输协议 (HTTPS) 进行连接时，用于从客户端计算机连接到管理点的 HTTPS。|--|433（请参阅备注 1， **可用的备用端口**）|  
|指定 CCMSetup 命令行属性 **/source:&lt;Path\>** 时源服务器与客户端计算机之间的服务器消息块 (SMB)。|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>用于手动安装和基于登录脚本的安装的端口  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|客户端计算机与从中运行 CCMSetup.exe 的网络共享之间的服务器消息块 (SMB)。<br /><br /> 安装 Configuration Manager 时，会从管理点上的 &lt;InstallationPath\>\Client 文件夹中复制客户端安装源文件并自动共享这些文件。 但是，您可以在网络上的任何计算机上复制这些文件并创建新共享。 或者，您可以通过以本地方式运行 CCMSetup.exe 来消除此网络流量，例如，使用可移动媒体。|--|445|  
|通过超文本传输协议 (HTTP) 进行连接且未指定 CCMSetup 命令行属性 **/source:&lt;Path\>** 时，用于从客户端计算机连接到管理点的 HTTP。|--|80（请参阅备注 1， **可用的备用端口**）|  
|通过安全超文本传输协议 (HTTPS) 进行连接且未指定 CCMSetup 命令行属性 **/source:&lt;Path\>** 时，用于从客户端计算机连接到管理点的 HTTPS。|--|433（请参阅备注 1， **可用的备用端口**）|  
|指定 CCMSetup 命令行属性 **/source:&lt;Path\>** 时源服务器与客户端计算机之间的服务器消息块 (SMB)。|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>用于基于软件分发的安装的端口  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|分发点与客户端计算机之间的服务器消息块 (SMB)。|--|445|  
|在通过超文本传输协议 (HTTP) 进行连接时，用于从客户端连接到分发点的 HTTP。|--|80（请参阅备注 1， **可用的备用端口**）|  
|在通过安全超文本传输协议 (HTTPS) 进行连接时，用于从客户端连接到分发点的 HTTPS。|--|433（请参阅备注 1， **可用的备用端口**）|  

## <a name="notes"></a>注意  
 **1 可用的备用端口** 在 Configuration Manager 中，您可以为此值定义备用端口。 如果定义了自定义端口，则为 IPsec 策略或为配置防火墙定义 IP 筛选器信息时将替代该自定义端口。  

 **2 Windows Server Update Services** 你可以在默认网站（端口 80）或自定义网站（端口 8530）上安装 Windows Server Update Services (WSUS)。  

 安装后，您可以更改端口。 不必在整个站点层次结构中使用相同的端口号。  

 如果 HTTP 端口为 80，则 HTTPS 端口必须为 443。  

 如果 HTTP 端口为其他端口，则 HTTPS 端口必须大 1。 例如 8530 和 8531。
