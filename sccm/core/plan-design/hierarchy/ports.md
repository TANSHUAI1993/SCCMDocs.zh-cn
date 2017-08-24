---
title: "Configuration Manager 使用的端口 | Microsoft Docs"
description: "了解有关 System Center Configuration Manager 用于连接的必需的和可自定义端口。"
ms.custom: na
ms.date: 3/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 78caa69e10f5d386daab1e61e484d4d134469708
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="ports-used-in-system-center-configuration-manager"></a>System Center Configuration Manager 中使用的端口

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 是分布式客户端/服务器系统。 Configuration Manager 的分布式性质意味着可在站点服务器、站点系统和客户端之间建立连接。 某些连接使用不可配置的端口，而某些连接支持指定的自定义端口。 如果使用防火墙、路由器、代理服务器或 IPsec 等任何端口筛选技术，必须验证所需的端口是否可用。  

> [!NOTE]  
>  如果通过 SSL 桥接支持基于 Internet 的客户端，则除了满足端口要求，可能还必须允许某些 HTTP 谓词和标头遍历防火墙。   

 下面的端口列表由 Configuration Manager 使用，但不包括标准 Windows 服务的信息（例如 Active Directory 域服务或 Kerberos 身份验证的组策略设置）。 有关 Windows Server 服务和端口的信息，请参阅 [Windows 服务器系统的服务概述和网络端口要求](http://go.microsoft.com/fwlink/p/?LinkID=123652)。  

##  <a name="BKMK_ConfigurablePorts"></a> 你可以配置的端口：  
 Configuration Manager 可用于为以下通信类型配置端口：  

-   应用程序目录网站点到应用程序目录 Web 服务点  

-   注册代理点到注册点  

-   运行 IIS 的客户端到站点系统  

-   客户端到 Internet（作为代理服务器设置）  

-   软件更新点到 Internet（作为代理服务器设置）  

-   软件更新点到 WSUS 服务器  

-   站点服务器到站点数据库服务器  

-   Reporting Services 点  

    > [!NOTE]  
    >  在 SQL Server Reporting Services 中，配置用于 Reporting Services 点站点系统角色的端口。 之后，Configuration Manager 会在与 Reporting Services 点通信时使用这些端口。 请务必查看为 IPsec 策略或为配置防火墙定义 IP 筛选器信息的端口。  

默认情况下，客户端到站点系统通信所用的 HTTP 端口是端口 80，默认的 HTTPS 端口是 443。 在安装期间或在 Configuration Manager 站点的“站点属性”中，可更改通过 HTTP 或 HTTPS 进行客户端到站点系统通信的端口。  

在 SQL Server Reporting Services 中，配置用于 Reporting Services 点站点系统角色的端口。 之后，Configuration Manager 会在与 Reporting Services 点通信时使用这些端口。 请务必查看为 IPsec 策略或为配置防火墙定义 IP 筛选器信息时所用的端口。  

##  <a name="BKMK_NonConfigurablePorts"></a> 不可配置的端口  
Configuration Manager 不允许您为以下通信类型配置端口：  

-   站点到站点  

-   站点服务器到站点系统  

-   Configuration Manager 控制台到 SMS 提供程序  

-   Configuration Manager 控制台到 Internet  

-   与云服务的连接，例如 Microsoft Intune 和基于云的分发点  

##  <a name="BKMK_CommunicationPorts"></a> Configuration Manager 客户端和站点系统使用的端口  
下列章节详述了 Configuration Manager 中用于通信的端口。 章节标题中的箭头表示通信的方向：  

-   -- > 表明一台计算机发起通信，另一台计算机始终响应  

-   &lt; -- > 表明任一计算机均可发起通信  

###  <a name="BKMK_PortsAI"></a>资产智能同步点 -- > Microsoft  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文本传输协议 (HTTPS)|--|443|  

###  <a name="BKMK_PortsAI-to-SQL"></a> 资产智能同步点 -- > SQL Server  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsAppCatalogService-SQL"></a> 应用程序目录 Web 服务点 -- > SQL Server  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> 应用程序目录网站点 -- > 应用程序目录 Web 服务点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80（请参阅备注 2 **可用的备用端口**）|  
|安全超文本传输协议 (HTTPS)|--|443（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> 客户端 -- > 应用程序目录网站点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80（请参阅备注 2 **可用的备用端口**）|  
|安全超文本传输协议 (HTTPS)|--|443（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsClient-ClientWakeUp"></a> 客户端 -- &gt; 客户端  
 除了使用下表中列出的端口，唤醒代理还使用 Internet 控制消息协议 (ICMP) 来回显示为唤醒代理配置客户端时彼此间发送的请求消息。

此通信用于确认网络上的另一台客户端计算机是否处于唤醒状态。 ICMP 有时称为 TCP/IP ping 命令。 ICMP 没有 UDP 或 TCP 协议号，因此未在下表中列出。 但是，这些客户端计算机或者子网中的介入性网络设备上的任何基于主机的防火墙都必须允许 ICMP 流量，以便成功进行唤醒代理通信。  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|LAN 唤醒|9（请参阅备注 2 **可用的备用端口**）|--|  
|唤醒代理|25536（请参阅备注 2 **可用的备用端口**）|--|  

###  <a name="BKMK_PortsClient-PolicyModule"></a> 客户端 -- &gt; Configuration Manager 策略模块（网络设备注册服务）  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)||80|  
|安全超文本传输协议 (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-CloudDP"></a> 客户端 -- > 基于云的分发点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文本传输协议 (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-DP"></a> 客户端 -- > 分发点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80（请参阅备注 2 **可用的备用端口**）|  
|安全超文本传输协议 (HTTPS)|--|443（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsClient-DP2"></a> 客户端 -- > 配置进行多播的分发点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|多播协议|63000-64000|--|  

###  <a name="BKMK_PortsClient-DP3"></a> 客户端 -- > 为 PXE 配置的分发点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|动态主机配置协议 (DHCP)|67 和 68|--|  
|普通文件传输协议 (TFTP)|69（请参阅备注 4 **普通文件传输协议 (TFTP) 后台程序**）|--|  
|启动信息协商层 (BINL)|4011|--|  

###  <a name="BKMK_PortsClient-FSP"></a> 客户端 -- > 回退状态点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsClient-GCDC"></a> 客户端 -- > 全局编录域控制器  
 如果 Configuration Manager 客户端是工作组计算机或者配置为仅限 Internet 通信，则该客户端不会联系全局目录服务器。  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|全局编录 LDAP|--|3268|  
|全局编录 LDAP SSL|--|3269|  

###  <a name="BKMK_PortsClient-MP"></a> 客户端 -- > 管理点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|客户端通知（在回退到 HTTP 或 HTTPS 之前的默认通信）|--|10123（请参阅备注 2 **可用的备用端口**）|  
|超文本传输协议 (HTTP)|--|80（请参阅备注 2 **可用的备用端口**）|  
|安全超文本传输协议 (HTTPS)|--|443（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsClient-SUP"></a> 客户端 -- > 软件更新点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80 或 8530（请参阅备注 3 **Windows Server Update Services**）|  
|安全超文本传输协议 (HTTPS)|--|443 或 8531（请参阅备注 3 **Windows Server Update Services**）|  

###  <a name="BKMK_PortsClient-SMP"></a> 客户端 -- > 状态迁移点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80（请参阅备注 2 **可用的备用端口**）|  
|安全超文本传输协议 (HTTPS)|--|443（请参阅备注 2 **可用的备用端口**）|  
|服务器消息块 (SMB)|--|445|  

###  <a name="BKMK_PortsConsole-Client"></a> Configuration Manager 控制台 -- > 客户端  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|远程控制（控制）|--|2701|  
|远程辅助（RDP 和 RTC）|--|3389|  

###  <a name="BKMK_PortsConsole-Internet"></a> Configuration Manager 控制台 -- > Internet  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80|  

###  <a name="BKMK_PortsConsole-RSP"></a> Configuration Manager 控制台 -- > Reporting Services 点  


|描述|UDP|TCP|
|-----------------|---------|---------|   
|超文本传输协议 (HTTP)|--|80（请参阅备注 2 **可用的备用端口**）|  
|安全超文本传输协议 (HTTPS)|--|443（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsConsole-Site"></a> Configuration Manager 控制台 -- > 站点服务器  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|RPC（最初连接到 WMI，以找到提供程序系统）|--|135|  

###  <a name="BKMK_PortsConsole-Provider"></a> Configuration Manager 控制台 -- > SMS 提供程序  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager 策略模块（网络设备注册服务）-- > 证书注册点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文本传输协议 (HTTPS)|--|443（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsDist_MP"></a> 分发点 -- > 管理点  
 在以下情况中，分发点向管理点通信：  

-   报告预留内容的状态  

-   报告使用情况摘要数据  

-   报告内容验证  

-   报告包下载的状态（拉取分发点）

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80（请参阅备注 2 **可用的备用端口**）|  
|安全超文本传输协议 (HTTPS)|--|443（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsEndpointProtection_Internet"></a>Endpoint Protection 点 -- > Internet  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80|  

###  <a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection 点 -- > SQL Server  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> 注册代理点 -- > 注册点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文本传输协议 (HTTPS)|--|443（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> 注册点 -- > SQL Server  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server 连接器 -- &gt; Exchange Online  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|通过 HTTPS 进行的 Windows 远程管理|--|5986|  

###  <a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server 连接器 -- > 本地 Exchange Server  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|通过 HTTP 进行的 Windows 远程管理|--|5985|  

###  <a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Mac 计算机 -- > 注册代理点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文本传输协议 (HTTPS)|--|443|  

###  <a name="BKMK_PortsMP-DC"></a> 管理点 -- > 域控制器  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|轻型目录访问协议 (LDAP)|--|389|  
|LDAP（安全套接字层 [SSL] 连接）|636|636|  
|全局编录 LDAP|--|3268|  
|全局编录 LDAP SSL|--|3269|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsMP-Site"></a> 管理点 &lt; -- > 站点服务器  
 （请参阅备注 5 **站点服务器和站点系统之间的通信**）  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 终结点映射程序|--|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  
|服务器消息块 (SMB)|--|445|  

###  <a name="BKMK_PortsMP-SQL"></a> 管理点 -- > SQL Server  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> 移动设备 -- > 注册代理点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文本传输协议 (HTTPS)|--|443|  

###  <a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> 移动设备 -- > Microsoft Intune  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文本传输协议 (HTTPS)|--|443|  

###  <a name="BKMK_PortsRSP-SQL"></a> Reporting Services 点 -- > SQL Server  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> 服务连接点 -- > Microsoft Intune  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文本传输协议 (HTTPS)|--|443|
有关详细信息，请参阅服务连接点的 [Internet 访问要求](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)。

###  <a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> 站点服务器 &lt; -- > 应用程序目录 Web 服务点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> 站点服务器 &lt; -- > 应用程序目录网站点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsSite-AISP"></a> 站点服务器&lt; -- > 资产智能同步点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsSite-Client"></a> 站点服务器 -- > 客户端  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|LAN 唤醒|9（请参阅备注 2 **可用的备用端口**）|--|  

###  <a name="BKMK_PortsSiteServer-CloudDP"></a> 站点服务器 -- > 基于云的分发点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文本传输协议 (HTTPS)|--|443|  

###  <a name="BKMK_PortsSite-DP"></a> 站点服务器 -- > 分发点  
 （请参阅备注 5 **站点服务器和站点系统之间的通信**）  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsSite-DC"></a> 站点服务器 -- > 域控制器  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|轻型目录访问协议 (LDAP)|--|389|  
|LDAP（安全套接字层 [SSL] 连接）|636|636|  
|全局编录 LDAP|--|3268|  
|全局编录 LDAP SSL|--|3269|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> 站点服务器 &lt; -- > 证书注册点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsEndpointProtection_SiteServer"></a>站点服务器&lt; -- > Endpoint Protection 点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_EnrollmentPoint_SiteServer"></a> 站点服务器 &lt; -- > 注册点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> 站点服务器 &lt; -- > 注册代理点  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsSite-FSP"></a> 站点服务器 &lt; -- > 回退状态点  
 （请参阅备注 5 **站点服务器和站点系统之间的通信**）  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortSite-Internet"></a> 站点服务器 -- > Internet  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80（请参阅备注 1 **代理服务器端口**）|  

###  <a name="BKMK_PortsIssuingCA_SiteServer"></a> 站点服务器 &lt; -- > 证书颁发机构 (CA)  
 当你使用证书注册点部署证书配置文件时，将使用此通信。 层次结构中的每个站点服务器均不使用该通信。 而仅用于层次结构顶部的站点服务器。  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 终结点映射程序|135|135|  
|RPC (DCOM)|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsSite-RSP"></a> 站点服务器 &lt; -- > Reporting Services 点  
 （请参阅备注 5 **站点服务器和站点系统之间的通信**）  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsSite-Site"></a> 站点服务器 &lt; -- > 站点服务器  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  

###  <a name="BKMK_PortsSite-SQL"></a> 站点服务器 -- > SQL Server  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433（请参阅备注 2 **可用的备用端口**）|  

 安装使用远程 SQL Server 托管站点数据库的站点期间，必须在站点服务器和 SQL Server 之间打开以下端口：  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsSite-Provider"></a> 站点服务器 -- > SMS 提供程序  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  
|RPC|--|动态（请参阅备注 6 **动态端口**）|  

###  <a name="BKMK_PortsSite-SUP"></a> 站点服务器 &lt; -- > 软件更新点  
 （请参阅备注 5 **站点服务器和站点系统之间的通信**）  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|超文本传输协议 (HTTP)|--|80 或 8530（请参阅备注 3 **Windows Server Update Services**）|  
|安全超文本传输协议 (HTTPS)|--|443 或 8531（请参阅备注 3 **Windows Server Update Services**）|  

###  <a name="BKMK_PortsSite-SMP"></a> 站点服务器 &lt; -- > 状态迁移点  
 （请参阅备注 5 **站点服务器和站点系统之间的通信**）  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  
|RPC 终结点映射程序|135|135|  

###  <a name="BKMK_PortsProvider-SQL"></a> SMS 提供程序 -- &gt; SQL Server  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433（请参阅备注 2 **可用的备用端口**）|  

###  <a name="BKMK_PortsSUP-Internet"></a> 软件更新点 -- > Internet  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80（请参阅备注 1 **代理服务器端口**）|  

###  <a name="BKMK_PortsSUP-WSUS"></a> 软件更新点 -- > 上游 WSUS 服务器  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|超文本传输协议 (HTTP)|--|80 或 8530（请参阅备注 3 **Windows Server Update Services**）|  
|安全超文本传输协议 (HTTPS)|--|443 或 8531（请参阅备注 3 **Windows Server Update Services**）|  

###  <a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server  
 需要一个站点中的 SQL Server 直接与其父或子站点的 SQL Server 通信，才可进行站点间的数据库复制。  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server 服务|--|1433（请参阅备注 2 **可用的备用端口**）|  
|SQL Server Service Broker|--|4022（请参阅备注 2 **可用的备用端口**）|  

> [!TIP]  
>  Configuration Manager 不需要使用端口 UDP 1434 的 SQL Server Browser。  

###  <a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> 状态迁移点 -- > SQL Server  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433（请参阅备注 2 **可用的备用端口**）|  



###  <a name="BKMY_PortNotes"></a> 有关 Configuration Manager 客户端和站点系统使用的端口的备注  

1.  **代理服务器端口**：此端口不可配置，但可通过配置的代理服务器进行路由。  

2.  **可用的备用端口**：可在 Configuration Manager 中为此值定义备用端口。 如果定义了自定义端口，则为 IPsec 策略或为配置防火墙定义 IP 筛选器信息时将替代该自定义端口。  

3.  **Windows Server Update Services (WSUS)**：可以安装 WSUS 以使用端口 80/443 或端口 8530/8531 进行客户端通信。 在 Windows Server 2012 或 Windows Server 2016 中运行 WSUS 时，WSUS 被默认配置为针对 HTTP 使用端口 8530，针对 HTTPS 使用端口 8531。  

     安装后，可更改端口。 不必在整个站点层次结构中使用相同的端口号。  

    -   如果 HTTP 端口为 80，则 HTTPS 端口必须为 443。  

    -   如果 HTTP 端口为其他端口，则 HTTPS 端口号必须大于等于 1，例如 8530 和 8531。   

    > [!NOTE]  
    >  在配置使用 HTTPS 的软件更新点时，还必须打开 HTTP 端口。 未加密的数据（如特定更新的 EULA）使用 HTTP 端口。  

4.  **普通文件传输协议 (TFTP) 后台程序**：普通文件传输协议 (TFTP) 后台程序系统服务不需要用户名或密码，而且它是 Windows 部署服务 (WDS) 不可或缺的一部分。 普通文件传输协议后台程序服务支持下列 RFC 定义的 TFTP 协议：  

    -   RFC 350：TFTP  

    -   RFC 2347：选项扩展  

    -   RFC 2348：块大小选项  

    -   RFC 2349：超时间隔和传输大小选项  

     普通文件传输协议为支持无盘启动环境而设计。 TFTP 后台程序侦听 UDP 端口 69，但从动态分配的高端口响应。 因此，启用此端口将允许 TFTP 服务接收传入的 TFTP 请求，但不允许所选服务器响应这些请求。 除非 TFTP 服务器配置为从端口 69 响应，否则所选服务器无法响应入站 TFTP 请求。  

5.  **站点服务器和站点系统之间的通信**：默认情况下，站点服务器和站点系统之间的通信是双向的。 站点服务器启动通信以配置站点系统，然后大部分站点系统连接回站点服务器以发送状态信息。 Reporting Services 点和分发点不会发送状态信息。 如果在安装站点系统后选择站点系统属性页上的“要求站点服务器启动到此站点系统的连接” ，则该系统不会启动与站点服务器的通信。 相反，站点服务器会启动通信，并使用站点系统安装帐户执行站点系统服务器的身份验证。  

6.  **动态端口**：动态端口（也称为临时端口）使用操作系统版本定义的一系列端口号。 有关默认端口范围的详细信息，请参阅 [Service overview and network port requirements for Windows（Windows 的服务概述和网络端口要求）](http://go.microsoft.com/fwlink/p/?LinkId=317965)。  

##  <a name="BKMK_AdditionalPorts"></a> 其他端口列表  
 下列部分提供了有关 Configuration Manager 使用的端口的其他信息。  

###  <a name="BKMK_ClientShares"></a> 客户端到服务器共享  
 客户端在连接到 UNC 共享时使用服务器消息块 (SMB)。 例如：  

-   指定了 CCMSetup.exe **/source:** 命令行属性的手动客户端安装  

-   从 UNC 路径下载定义文件的 Endpoint Protection 客户端

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|服务器消息块 (SMB)|--|445|  

###  <a name="BKMK_SQLPorts"></a> 与 Microsoft SQL Server 的连接  
 对于与 SQL Server 数据库引擎的通信和站点间复制，可以使用默认的 SQL Server 端口，也可以指定自定义端口：  

-   站点间通信使用：  

    -   SQL Server Service Broker，默认为端口 TCP 4022。  

    -   SQL Server 服务，默认为端口 TCP 1433。  

-   SQL Server 数据库引擎与各种 Configuration Manager 站点系统角色之间的“站点内通信”默认使用端口 TCP 1433。  

- Configuration Manager 使用相同的端口和协议与承载站点数据库的每个 SQL 可用性组副本进行通信，就像该副本是独立的 SQL Server 实例。

使用 Azure 且站点数据库位于内部或外部负载均衡器后面时，在每个副本上配置以下防火墙异常，并为以下端口添加负载均衡规则：
 - SQL over TCP: TCP 1433
 - SQL Server Service Broker: TCP 4022
 - 服务器消息块 (SMB): TCP 445
 - RPC 终结点映射程序: TCP 135

> [!WARNING]  
>  Configuration Manager 不支持动态端口。 由于 SQL Server 命名实例默认情况下使用动态端口来连接到数据库引擎，因此，在使用命名实例时，必须手动配置要用于站点内通信的静态端口。  

 下列站点系统角色直接与 SQL Server 数据库进行通信：  

-   应用程序目录 Web 服务点  

-   证书注册点角色  

-   注册点角色  

-   管理点  

-   站点服务器  

-   Reporting Services 点  

-   SMS 提供程序  

-   SQL Server --> SQL Server  

在 SQL Server 承载多个站点中的数据库时，每个数据库都必须使用独立的 SQL Server 实例，而且必须用一组独特的端口来配置每个实例。  

如果在 SQL Server 计算机上启用了防火墙，请确保将它配置为允许部署使用端口。 还要在与 SQL Server 通信的计算机之间的网络上，将其他位置的防火墙配置为允许使用这些相同的端口。  

有关演示如何将 SQL Server 配置为使用指定的端口的示例，请参阅 SQL Server TechNet 库中的 [如何：将服务器配置为侦听特定的 TCP 端口 (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) 。  


### <a name="bkmk_discovery"></a>发现和发布
使用下列端口发现和发布站点信息：
 - 轻型目录访问协议 (LDAP)：389
 - LDAP（安全套接字层 [SSL] 连接）：636


 - 全局编录 LDAP：3268
 - 全局编录 LDAP SSL：3269


 - RPC 端点映射程序：135
 - RPC：动态分配的高 TCP 端口


 - TCP：1024: 5000
 - TCP：49152: 65535


###  <a name="BKMK_External"></a> Configuration Manager 建立的外部连接  
 Configuration Manager 客户端或站点系统可以建立下列外部连接：  

-   [资产智能同步点 -- &gt; Microsoft](#BKMK_PortsAI)  

-   [Endpoint Protection 点 -- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [客户端 -- &gt; 全局编录域控制器](#BKMK_PortsClient-GCDC)  

-   [Configuration Manager 控制台 -- &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [管理点 -- &gt; 域控制器](#BKMK_PortsMP-DC)  

-   [站点服务器 -- &gt; 域控制器](#BKMK_PortsSite-DC)  

-   [站点服务器 &lt; -- &gt; 证书颁发机构 (CA)](#BKMK_PortsIssuingCA_SiteServer)  

-   [软件更新点 -- &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [软件更新点 -- &gt; 上游 WSUS 服务器](#BKMK_PortsSUP-WSUS)  

-   [服务连接点 -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="BKMK_IBCMports"></a> 支持基于 Internet 的客户端的站点系统的安装要求  
 支持基于 Internet 的客户端的管理点和分发点、软件更新点以及回退状态点均使用下列端口进行安装和修复：  

-   站点服务器 --> 站点系统：RPC 端点映射程序使用 UDP 和 TCP 端口 135。  

-   站点服务器--> 站点系统：RPC 动态 TCP 端口  

-   站点服务器 &lt; --> 站点系统：服务器消息块 (SMB) 使用 TCP 端口 445

分发点上的应用程序和包安装需要下列 RPC 端口：  

-   站点服务器 --> 分发点：RPC 端点映射程序使用 UDP 和 TCP 端口 135

-   站点服务器--> 分发点：RPC 动态 TCP 端口  

使用 IPsec 帮助确保站点服务器和站点系统之间的通信安全。 如果必须限制针对 RPC 使用的动态端口，则可以使用 Microsoft RPC 配置工具 (rpccfg.exe) 为这些 RPC 数据包配置有限的端口范围。 有关 RPC 配置工具的详细信息，请参阅 [如何配置 RPC 以使用特定端口以及如何使用 IPsec 来帮助保护这些端口](http://go.microsoft.com/fwlink/p/?LinkId=124096)。  

> [!IMPORTANT]  
>  在安装这些站点系统之前，请确保站点系统服务器上正在运行远程注册表服务；如果站点系统位于不同的 Active Directory 林中且不具有信任关系，则另请确保指定了站点系统安装帐户。  

###  <a name="BKMK_PortsClientInstall"></a> Configuration Manager 客户端安装使用的端口  
安装客户端期间使用的端口取决于客户端部署方法。 有关各客户端部署方法所用端口的列表，请参阅 **System Center Configuration Manager 中客户端的 Windows 防火墙和端口设置**主题中的 [Configuration Manager 客户端部署期间使用的端口](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md)。 有关如何为客户端安装和安装后通信配置客户端上的 Windows 防火墙的信息，请参阅 [System Center Configuration Manager 中客户端的 Windows 防火墙和端口设置](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md)。  

###  <a name="BKMK_MigrationPorts"></a> 迁移使用的端口  
运行“迁移”的站点服务器使用多个端口连接到源层次结构中的适用站点，以便收集源站点 SQL Server 数据库中的数据并共享分发点。  

 有关这些端口的信息，请参阅 [System Center Configuration Manager 中迁移的先决条件](../../../core/migration/prerequisites-for-migration.md)主题中的[迁移的所需配置](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations)部分。  

###  <a name="BKMK_ServerPorts"></a> Windows Server 使用的端口  
 下表列出了 Windows Server 使用的一些关键端口及其各自的功能。 有关 Windows Server 服务和网络端口要求的更完整的列表，请参阅 [Windows 服务器系统的服务概述和网络端口要求](http://go.microsoft.com/fwlink/p/?LinkID=123652)。  

|描述|UDP|TCP|  
|-----------------|---------|---------|  
|域名系统 (DNS)|53|53|  
|动态主机配置协议 (DHCP)|67 和 68|--|  
|NetBIOS 名称解析|137|--|  
|NetBIOS 数据报服务|138|--|  
|NetBIOS 会话服务|--|139|  
